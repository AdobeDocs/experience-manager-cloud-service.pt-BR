---
title: Configurando Credenciais e Autenticação da CDN
description: Saiba como configurar credenciais e autenticação do CDN declarando regras em um arquivo de configuração que é implantado usando o Pipeline de configuração do Cloud Manager.
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 73d0a4a73a3e97a91b2276c86d3ed1324de8c361
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 1%

---

# Configurando Credenciais e Autenticação da CDN {#cdn-credentials-authentication}

>[!NOTE]
>Esse recurso ainda não está disponível para o público geral. Para participar do programa de adoção antecipada, envie um email para `aemcs-cdn-config-adopter@adobe.com`.

A CDN fornecida por Adobe tem vários recursos e serviços, alguns dos quais dependem de credenciais e autenticação para garantir um nível apropriado de segurança corporativa. Ao declarar regras em um arquivo de configuração implantado usando o [Pipeline de Configuração do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline), os clientes podem configurar, por autoatendimento, o seguinte:

* O valor do cabeçalho HTTP usado pelo CDN do Adobe para validar solicitações provenientes de um CDN gerenciado pelo Cliente.
* O token de API usado para limpar recursos no cache do CDN.
* Uma lista de combinações de nome de usuário/senha que podem acessar conteúdo restrito, enviando um formulário de Autenticação básica.


Cada uma dessas opções, incluindo a sintaxe de configuração, é descrita em sua própria seção abaixo. A seção [Instalação Comum](#common-setup) ilustra a instalação comum a ambos, bem como a implantação. Finalmente, há uma seção sobre como [girar chaves](#rotating-secrets), o que é considerado uma boa prática de segurança.

## Valor do cabeçalho HTTP da CDN gerenciada pelo cliente {#CDN-HTTP-value}

Conforme descrito na página [CDN no AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN), os clientes podem optar por rotear o tráfego por meio de sua própria CDN, que é chamada de CDN do cliente (também chamada às vezes de BYOCDN).

Como parte da configuração, o CDN do Adobe e o CDN do cliente devem concordar com um valor do Cabeçalho HTTP `X-AEM-Edge-Key`. Esse valor é definido em cada solicitação, no CDN do cliente, antes de ser roteado para o CDN do Adobe, que então valida se o valor está conforme o esperado, para que possa confiar em outros cabeçalhos HTTP, incluindo aqueles que ajudam a rotear a solicitação para a origem AEM apropriada.

O valor `X-AEM-Edge-Key` é declarado com a sintaxe abaixo, com o(s) valor(es) real(is) referenciado(s) pelas propriedades edgeKey1 e edgeKey2. Consulte a seção [Instalação Comum](#common-setup) para saber como implantar a configuração.

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
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

A sintaxe para o valor `X-AEM-Edge-Key` inclui:

* Tipo, versão e metadados.
* Nó de dados que contém um nó `experimental_authentication` filho (o prefixo experimental será removido quando o recurso for lançado).
* Em `experimental_authentication`, um nó `authenticators` e um nó `rules`, ambos com matrizes.
* Autenticadores: permite declarar um tipo de token ou credencial, que, nesse caso, é uma chave de borda. Inclui as seguintes propriedades:
   * name - uma cadeia de caracteres descritiva.
   * tipo - deve ser `edge`.
   * edgeKey1 - o valor de *X-AEM-Edge-Key*, que deve fazer referência a um token secreto, que não deve ser armazenado no Git, mas declarado como uma [Variável de ambiente Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) do tipo segredo. Para o campo Serviço Aplicado, selecione Todos. É recomendável que o valor (por exemplo, `${{CDN_EDGEKEY_052824}}`) reflita o dia em que foi adicionado.
   * edgeKey2 - usado para a rotação de segredos, que é descrita na [seção de rotação de segredos](#rotating-secrets) abaixo. Defina-a de forma semelhante a edgeKey1. Pelo menos um de `edgeKey1` e `edgeKey2` deve ser declarado.
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* Regras: permite declarar quais dos autenticadores devem ser usados e se são para o nível de publicação e/ou pré-visualização.  Inclui:
   * name - uma cadeia de caracteres descritiva.
   * when - uma condição que determina quando a regra deve ser avaliada, de acordo com a sintaxe no artigo [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md). Normalmente, ela incluirá uma comparação da camada atual (por exemplo, publicar) para que todo o tráfego ativo seja validado como roteamento pela CDN do cliente.
   * ação - deve especificar &quot;autenticar&quot;, com o autenticador desejado referenciado.

>[!NOTE]
>A Chave do Edge deve ser configurada como uma [Variável de Ambiente do Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) do tipo `secret` (com *Todos* selecionados para o Serviço Aplicado), antes da implantação da configuração que faz referência a ela.

## Limpar token de API {#purge-API-token}

Os clientes podem [limpar o cache da CDN](/help/implementing/dispatcher/cdn-cache-purge.md) usando um token de API de limpeza declarado. O token é declarado com a sintaxe abaixo.  Consulte a seção [Configuração Comum](#common-setup) para saber como implantá-la.

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
* nó de dados que contém um nó `experimental_authentication` filho (o prefixo experimental será removido quando o recurso for lançado).
* Em `experimental_authentication`, um nó `authenticators` e um nó `rules`, ambos com matrizes.
* Autenticadores: permite declarar um tipo de token ou credencial, que, nesse caso, é uma chave de limpeza. Inclui as seguintes propriedades:
   * name - uma cadeia de caracteres descritiva.
   * tipo - deve ser expurgado.
   * purgeKey1 - seu valor deve fazer referência a um token secreto, que não deve ser armazenado no Git, mas declarado como [Variáveis de Ambiente Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) do tipo `secret`.
   * Para o campo Serviço Aplicado, selecione Todos. Recomenda-se que o valor (por exemplo, `${{CDN_PURGEKEY_031224}}`) reflita o dia em que foi adicionado.
   * purgeKey2 - usado para a rotação de segredos, que é descrita na [seção de rotação de segredos](#rotating-secrets) abaixo. Pelo menos um de `purgeKey1` e `purgeKey2` deve ser declarado.
* Regras: permite declarar quais dos autenticadores devem ser usados e se são para o nível de publicação e/ou pré-visualização.  Inclui:
   * nome - uma sequência descritiva
   * when - uma condição que determina quando a regra deve ser avaliada, de acordo com a sintaxe no artigo [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md). Normalmente, incluirá uma comparação do nível atual (por exemplo, publicar).
   * ação - deve especificar &quot;autenticar&quot;, com o autenticador desejado referenciado.

>[!NOTE]
>A Chave do Edge deve ser configurada como uma [Variável de Ambiente do Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) do tipo `secret`, antes da implantação da configuração que faz referência a ela.

## Autenticação básica {#basic-auth}

Protect determinados recursos de conteúdo, exibindo uma caixa de diálogo de autenticação básica que requer um nome de usuário e senha. Esse recurso destina-se principalmente a casos de uso de autenticação simples, como a análise de conteúdo pelas partes interessadas, e não como uma solução completa para os direitos de acesso do usuário final.

O usuário final terá uma caixa de diálogo de autenticação básica surgindo da seguinte maneira:

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


A sintaxe é declarada conforme descrito abaixo. Consulte a seção [Configuração Comum](#common-setup) abaixo para obter informações sobre como implantá-la.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
       - name: my-basic-authenticator
         type: basic
         credentials:
           - user: johndoe
             password: ${{JOHN_DOE_PASSWORD}}
           - user: janedoe
             password: ${{JANE_DOE_PASSWORD}}
    rules:
       - name: basic-auth-rule
         when: { reqProperty: path, like: "/summercampaign" }
         action:
           type: authenticate
           authenticator: my-basic-authenticator
```

A sintaxe inclui:

* tipo, versão e metadados.
* um nó de dados que contém um nó `experimental_authentication` (o prefixo experimental será removido quando o recurso for lançado).
* Em `experimental_authentication`, um nó `authenticators` e um nó `rules`, ambos com matrizes.
* Autenticadores: neste cenário, declare um autenticador básico, que tenha a seguinte estrutura:
   * nome - uma sequência descritiva
   * tipo - deve ser `basic`
   * uma matriz de credenciais, cada uma incluindo os seguintes pares de nome/valor, que os usuários finais podem inserir na caixa de diálogo de autenticação básica:
      * user - o nome do usuário
      * senha - seu valor deve fazer referência a um token secreto, que não deve ser armazenado no git, mas declarado como Variáveis de ambiente do Cloud Manager do tipo secreto (com **Todos** selecionados como o campo de serviço)
* Regras: permite declarar quais dos autenticadores devem ser usados e quais recursos devem ser protegidos. Cada regra inclui:
   * nome - uma sequência descritiva
   * when - uma condição que determina quando a regra deve ser avaliada, de acordo com a sintaxe no artigo [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md). Normalmente, isso incluirá uma comparação do nível de publicação ou caminhos específicos.
   * ação - deve especificar &quot;autenticar&quot;, com o autenticador desejado referenciado, que é basic-auth para este cenário

>[!NOTE]
>A Chave do Edge deve ser configurada como uma [Variável de Ambiente do Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) do tipo `secret`, antes da implantação da configuração que faz referência a ela.

## Configuração comum {#common-setup}

Todos os autenticadores são configurados da seguinte maneira:

* Primeiro, crie a seguinte pasta e estrutura de arquivo na pasta de nível superior do seu projeto Git:

```
config/
     cdn.yaml
```

* Em segundo lugar, o arquivo de configuração `cdn.yaml` deve conter os nós descritos nos exemplos abaixo. A propriedade `kind` deve ser definida como `CDN` e a versão deve ser definida como a versão do esquema, que atualmente é `1`. O nó de metadados tem uma propriedade &quot;envTypes&quot;, que indica em quais tipos de ambiente (dev, estágio, prod) essa configuração será avaliada.

* Por último, crie um pipeline de configuração de implantação direcionada no Cloud Manager. Consulte [configuração de pipelines de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e [configuração de pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

Observe que:

* Atualmente, os RDEs não oferecem suporte ao pipeline de configuração.
* Você pode usar `yq` para validar localmente a formatação YAML do seu arquivo de configuração (por exemplo, `yq cdn.yaml`).

## Rotação de segredos {#rotating-secrets}

É uma boa prática de segurança alterar ocasionalmente as credenciais. Isso pode ser feito conforme exemplificado abaixo, usando o exemplo de uma chave de borda, embora a mesma estratégia seja usada para chaves de limpeza.

* Inicialmente, apenas `edgeKey1` foi definido, neste caso referenciado como `${{CDN_EDGEKEY_052824}}`, que, como uma convenção recomendada, reflete a data em que foi criado.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
```

* Quando for a hora de girar a chave, crie um novo segredo do Cloud Manager, por exemplo `${{CDN_EDGEKEY_041425}}`.
* Na configuração, faça referência a ele a partir de `edgeKey2` e implante.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Depois de ter certeza de que a chave de borda antiga não será mais usada, remova-a removendo `edgeKey1` da configuração.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Exclua a referência secreta antiga (`${{CDN_EDGEKEY_052824}}`) da Cloud Manager e implante.
* Quando estiver pronto para a próxima rotação, siga o mesmo procedimento. No entanto, dessa vez, você adicionará `edgeKey1` à configuração, fazendo referência a um novo segredo do ambiente do Cloud Manager chamado, por exemplo, `${{CDN_EDGEKEY_031426}}`.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
      edgeKey1: ${{CDN_EDGEKEY_031426}}
```
