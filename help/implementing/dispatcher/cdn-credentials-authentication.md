---
title: Configurando Credenciais e Autenticação da CDN
description: Saiba como configurar credenciais e autenticação do CDN declarando regras em um arquivo de configuração que é implantado usando o Pipeline de configuração do Cloud Manager.
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
source-git-commit: 7a53f936aacfb3e5aa431f26e5346c1809f9c76f
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 0%

---

# Configurando Credenciais e Autenticação da CDN {#cdn-credentials-authentication}

>[!NOTE]
>Esse recurso ainda não está disponível para o público geral. Para participar do programa de adoção antecipada, envie um email para `aemcs-cdn-config-adopter@adobe.com`.

A CDN fornecida por Adobe tem vários recursos e serviços, alguns dos quais dependem de credenciais e autenticação para garantir um nível apropriado de segurança corporativa. Declarando regras em um arquivo de configuração implantado com o uso do [Pipeline de configuração do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline), os clientes podem configurar, de forma automatizada, o seguinte:

* O valor do cabeçalho HTTP usado pelo CDN do Adobe para validar solicitações provenientes de um CDN gerenciado pelo Cliente.
* O token de API usado para limpar recursos no cache do CDN.

Cada uma dessas opções, incluindo a sintaxe de configuração, é descrita em sua própria seção abaixo. A variável [Configuração comum](#common-setup) A seção ilustra a configuração comum a ambos, bem como a implantação. Por fim, há uma seção sobre como [teclas de rotação](#rotating-secrets), que é considerada uma boa prática de segurança.

## Valor do cabeçalho HTTP da CDN gerenciada pelo cliente {#CDN-HTTP-value}

Conforme descrito na seção [CDN no AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) Os clientes podem optar por rotear o tráfego por meio de seu próprio CDN, que é chamado de CDN do cliente (também chamado às vezes de BYOCDN).

Como parte da configuração, o CDN do Adobe e o CDN do cliente devem concordar com um valor de `X-AEM-Edge-Key` Cabeçalho HTTP. Esse valor é definido em cada solicitação, no CDN do cliente, antes de ser roteado para o CDN do Adobe, que então valida se o valor está conforme o esperado, para que possa confiar em outros cabeçalhos HTTP, incluindo aqueles que ajudam a rotear a solicitação para a origem AEM apropriada.

A variável `X-AEM-Edge-Key` é declarado com a sintaxe abaixo. Consulte a [Configuração comum](#common-setup) para saber como implantá-la.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
      - name: edge-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_052824}}
        edgeKey2: ${{CDN_EDGEKEY_041425}}
        onFailure: log # optional, default: log, enum: log/block
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

A sintaxe para a variável `X-AEM-Edge-Key` o valor inclui:

* Tipo, versão e metadados.
* Nó de dados que contém um filho `experimental_authentication` (o prefixo experimental será removido quando o recurso for lançado).
* Em experimental_authentication, com um nó autenticador e um nó de regras, ambos arrays.
* Autenticadores: permite declarar um tipo de token ou credencial, que, nesse caso, é uma chave de borda. Inclui as seguintes propriedades:
   * name - uma cadeia de caracteres descritiva.
   * tipo - deve ser borda.
   * edgeKey1 - o valor deve fazer referência a um token secreto, que não deve ser armazenado no git, mas declarado como um [Variável de ambiente do Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) do tipo segredo. Para o campo Serviço Aplicado, selecione Todos. Recomenda-se que o valor (por exemplo,`${{CDN_EDGEKEY_052824}}`) reflete o dia em que foi adicionado.
   * edgeKey2 - usado para a rotação de segredos, descrita na seção [seção rotação de segredos](#rotating-secrets) abaixo. Pelo menos um de `edgeKey1` e `edgeKey2` deve ser declarado.
   * OnFailure - define a ação, seja `log` ou `block`, quando uma solicitação não corresponde a `edgeKey1` ou `edgeKey2`. Para `log`, o processamento da solicitação continuará, enquanto `block` apresentará um erro 403. A variável `log` Esse valor é útil ao testar um novo token em um site ativo, já que você pode confirmar primeiro que a CDN está aceitando corretamente o novo token antes de alterar para `block` também reduz a chance de perda de conectividade entre o CDN do cliente e o CDN do Adobe, como resultado de uma configuração incorreta.
* Regras: permite declarar quais dos autenticadores devem ser usados e se são para o nível de publicação e/ou pré-visualização.  Inclui:
   * name - uma cadeia de caracteres descritiva.
   * when - uma condição que determina quando a regra deve ser avaliada, de acordo com a sintaxe no [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md) artigo. Normalmente, ela incluirá uma comparação da camada atual (por exemplo, publicar) para que todo o tráfego ativo seja validado como roteamento pela CDN do cliente.
   * ação - deve especificar &quot;autenticar&quot;, com o autenticador desejado referenciado.

>[!NOTE]
>A Chave de Borda deve ser configurada como uma [Variável de ambiente do Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) variável de tipo `secret`, antes da configuração que faz referência a ela ser implantada.

## Limpar token de API {#purge-API-token}

Os clientes podem [limpar o cache da CDN](/help/implementing/dispatcher/cdn-cache-purge.md) usando um token de API de limpeza declarado. O token é declarado com a sintaxe abaixo.  Consulte a [Configuração comum](#common-setup) para saber como implantá-la.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
       - name: purge-auth
         type: purge
         purgeKey1: ${{CDN_PURGEKEY_031224}}
         purgeKey2: ${{CDN_PURGEKEY_021225}}
    rules:
     - name: purge-auth-rule
       when: { reqProperty: tier, equals: "publish" }
       action:
         type: authenticate
         authenticator: purge-auth
```

A sintaxe inclui:

* tipo, versão e metadados.
* nó de dados que contém um filho `experimental_authentication` (o prefixo experimental será removido quando o recurso for lançado).
* Em `experimental_authentication`, com um único nó autenticadores one.
* Autenticadores: permite declarar um tipo de token ou credencial, que, nesse caso, é uma chave de limpeza. Inclui as seguintes propriedades:
   * name - uma cadeia de caracteres descritiva.
   * tipo - deve ser expurgado.
   * purgeKey1 - o valor deve fazer referência a um token secreto, que não deve ser armazenado no git, mas declarado como [Variáveis de ambiente do Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) do tipo `secret`.
   * Para o campo Serviço Aplicado, selecione Todos. Recomenda-se que o valor (por exemplo, `${{CDN_PURGEKEY_031224}}`) reflete o dia em que foi adicionado.
   * purgeKey2 - usado para a rotação de segredos, que é descrita na seção [seção rotação de segredos](#rotating-secrets) abaixo. Pelo menos um de `purgeKey1` e `purgeKey2` deve ser declarado.
* Regras: permite declarar quais dos autenticadores devem ser usados e se são para o nível de publicação e/ou pré-visualização.  Inclui:
   * nome - uma sequência descritiva
   * when - uma condição que determina quando a regra deve ser avaliada, de acordo com a sintaxe no [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md) artigo. Normalmente, incluirá uma comparação do nível atual (por exemplo, publicar).
   * ação - deve especificar &quot;autenticar&quot;, com o autenticador desejado referenciado.

>[!NOTE]
>A Chave de Borda deve ser configurada como uma [Variável de ambiente do Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) variável de tipo `secret`, antes da configuração que faz referência a ela ser implantada.

## Configuração comum {#common-setup}

Todos os autenticadores são configurados da seguinte maneira:

* Primeiro, crie a seguinte pasta e estrutura de arquivo na pasta de nível superior do seu projeto Git:

```
config/
     cdn.yaml
```

* Em segundo lugar, a `cdn.yaml` o arquivo de configuração deve conter os nós descritos nos exemplos abaixo. A variável `kind` propriedade deve ser definida como `CDN` e a versão deve ser definida como a versão do schema, que está `1`. O nó de metadados tem uma propriedade &quot;envTypes&quot;, que indica em quais tipos de ambiente (dev, estágio, prod) essa configuração será avaliada.

* Por último, crie um pipeline de configuração de implantação direcionada no Cloud Manager. Consulte [configuração de pipelines de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e [configuração de pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

Observe que:

* Atualmente, os RDEs não oferecem suporte ao pipeline de configuração.
* Você pode usar `yq` para validar localmente a formatação YAML do seu arquivo de configuração (por exemplo, `yq cdn.yaml`).

## Rotação de segredos {#rotating-secrets}

É uma boa prática de segurança alterar ocasionalmente as credenciais. Isso pode ser feito conforme exemplificado abaixo, usando o exemplo de uma chave de borda, embora a mesma estratégia seja usada para chaves de limpeza.

* Inicialmente apenas `edgeKey1` foi definido, neste caso referenciado como `${{CDN_EDGEKEY_052824}}`, que, como uma convenção recomendada, reflete a data de criação.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
```

* Quando chegar o momento de girar a chave, crie um novo segredo do Cloud Manager, por exemplo `${{CDN_EDGEKEY_041425}}`.
* Na configuração, faça referência a ela em `edgeKey2` e implantar.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Depois de ter certeza de que a chave de borda antiga não será mais usada, remova-a `edgeKey1` da configuração.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Excluir a referência secreta antiga (`${{CDN_EDGEKEY_052824}}`) no Cloud Manager e implante.
* Quando estiver pronto para a próxima rotação, siga o mesmo procedimento. No entanto, dessa vez, você adicionará `edgeKey1` à configuração, fazendo referência a um novo segredo de ambiente do Cloud Manager chamado, por exemplo, `${{CDN_EDGEKEY_031426}}`.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
      edgeKey1: ${{CDN_EDGEKEY_031426}}
```
