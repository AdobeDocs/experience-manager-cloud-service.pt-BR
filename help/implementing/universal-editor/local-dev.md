---
title: Execução do seu próprio serviço de editor universal
description: Saiba como executar seu próprio Universal Editor Service para desenvolvimento local ou como parte de sua própria infraestrutura.
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 2%

---


# Execução do seu próprio serviço de editor universal {#local-ue-service}

Saiba como executar seu próprio Universal Editor Service para desenvolvimento local ou como parte de sua própria infraestrutura.

>[!NOTE]
>
>Os Serviços locais do Universal Editor não são necessários ou compatíveis para projetos que usam a criação do AEM com o Edge Delivery Services.

## Visão geral {#overview}

O Universal Editor Service é o que vincula o Universal Editor e o sistema de back-end. Para desenvolver localmente para o Universal Editor, você deve executar uma cópia local do Universal Editor Service. Isso ocorre porque:

* O Serviço Universal Editor oficial da Adobe é hospedado globalmente, e sua instância local do AEM precisaria ser exposta à Internet.
* Ao desenvolver com um AEM SDK local, o Universal Editor Service da Adobe não pode ser acessado da Internet.
* Se sua instância do AEM tiver restrições de IP e o Universal Editor Service da Adobe não estiver em um intervalo de IP definido, você mesmo poderá hospedá-lo.

## Casos de uso {#use-cases}

Sua própria cópia do Universal Editor Service é útil se você deseja:

* Desenvolva localmente no AEM para uso com o Editor universal.
* Execute seu próprio Universal Editor Service como parte de sua própria infraestrutura, independentemente do Adobe Universal Editor Service.

Ambos os casos de uso são compatíveis. Este documento explica como executar o AEM em HTTPS junto com uma cópia local do Universal Editor Service.

Se você quiser executar seu próprio Universal Editor Service como parte de sua própria infraestrutura, siga as mesmas etapas do exemplo de desenvolvimento local.

## Configurar o AEM para ser executado em HTTPS {#aem-https}

Em um quadro externo protegido com HTTPS, um quadro HTTP não seguro não pode ser carregado. O Universal Editor Service é executado em HTTPS e, portanto, o AEM ou qualquer outra página remota também deve ser executado em HTTPS.

Para fazer isso, é necessário configurar o AEM para ser executado em HTTPS. Para fins de desenvolvimento, é possível usar o certificado autoassinado.

[Consulte este documento](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=pt-BR) sobre como configurar o AEM em execução em HTTPS, incluindo um certificado autoassinado que você pode usar.

## Instalar o Universal Editor Service {#install-ue-service}

O Universal Editor Service não é uma cópia completa do Universal Editor, mas apenas um subconjunto de seus recursos para garantir que as chamadas do seu ambiente local do AEM não sejam roteadas pela Internet, mas de um endpoint definido sob seu controle.

[A versão 20](https://nodejs.org/en/download/releases) do NodeJS é necessária para executar uma cópia local do Universal Editor Service.

O Universal Editor Service está disponível por meio da Distribuição de software. Consulte a [documentação de Distribuição de software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=pt-br) para obter detalhes sobre como acessá-la.

Salve o arquivo `universal-editor-service.cjs` da Distribuição de software no ambiente de desenvolvimento local.

## Criar um certificado para executar o Universal Editor Service com HTTPS {#ue-https}

O Universal Editor Service também requer um certificado para ser executado em HTTPS no ambiente de desenvolvimento.

Execute o seguinte comando.

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

O comando gera um arquivo `key.pem` e `certificate.pem`. Salve esses arquivos no mesmo caminho do arquivo `universal-editor-service.cjs`.

## Definição da Configuração do Serviço do Editor Universal {#setting-up-service}

Várias variáveis de ambiente devem ser definidas no NodeJS para executar o Universal Editor Service localmente.

No mesmo caminho dos arquivos `universal-editor-service.cjs`, `key.pem` e `certificate.pem`, crie um arquivo `.env` com o conteúdo a seguir.

```text
UES_PORT=8000
UES_PRIVATE_KEY=./key.pem
UES_CERT=./certificate.pem
UES_TLS_REJECT_UNAUTHORIZED=false
UES_CORS_PRIVATE_NETWORK=true
```

Esses são os valores mínimos necessários para o desenvolvimento local em nosso exemplo.

>[!NOTE]
>
>Se você estiver executando a versão 130+ do Chrome, deverá habilitar o envio de cabeçalhos CORS para [acesso à rede privada](https://wicg.github.io/private-network-access/#private-network-request) usando a opção `UES_CORS_PRIVATE_NETWORK`.


A tabela a seguir detalha esses e outros valores disponíveis.

| Valor | Opcional | Padrão | Descrição |
|---|---|---|---|
| `UES_PORT` | Sim | `8080` | Porta em que o servidor é executado |
| `UES_PRIVATE_KEY` | Sim | Nenhum | Caminho para a chave privada do servidor HTTPS |
| `UES_CERT` | Sim | Nenhum | Caminho para o arquivo de certificação do servidor HTTPS |
| `UES_TLS_REJECT_UNAUTHORIZED` | Sim | `true` | Rejeitar conexões TLS não autorizadas |
| `UES_DISABLE_IMS_VALIDATION` | Sim | `false` | Desativar validação de IMS |
| `UES_ENDPOINT_MAPPING` | Sim | Vazio | Mapeamento dos pontos de extremidade para regravações internas<br>Exemplo: `UES_ENDPOINT_MAPPING='[{"https://your-public-facing-author-domain.net": "http://10.0.0.1:4502"}]'`<br>Resultado: o Universal Editor Service se conectará a `http://10.0.0.1:4502` em vez da conexão fornecida `https://your-public-facing-author-domain.net` |
| `UES_LOG_LEVEL` | Sim | `info` | Nível de log do servidor. Os valores possíveis são `silly`, `trace`, `debug`, `verbose`, `info`, `log`, `warn`, `error` e `fatal` |
| `UES_SPLUNK_HEC_URL` | Sim | Nenhum | URL HEC para o ponto de extremidade do Splunk |
| `UES_SPLUNK_TOKEN` | Sim | Nenhum | Token de Splunk |
| `UES_SPLUNK_INDEX` | Sim | Nenhum | Índice no qual gravar logs |
| `UES_SPLUNK_SOURCE` | Sim | `universal-editor-service` | Nome da origem nos logs de splunk |
| `UES_CORS_PRIVATE_NETWORK` | Sim | `false` | Habilite o envio de cabeçalhos CORS para permitir [Rede privada](https://wicg.github.io/private-network-access/#private-network-request). Necessário para usuários do Chrome versão 130+ |

>[!NOTE]
>
>Antes da [versão 2024.08.13](/help/release-notes/universal-editor/current.md) do Editor Universal, as seguintes variáveis eram necessárias no arquivo `.env`. Esses valores terão suporte até 1 de outubro de 2024 para compatibilidade com versões anteriores.
>
>`EXPRESS_PORT=8000`
>`EXPRESS_PRIVATE_KEY=./key.pem`
>`EXPRESS_CERT=./certificate.pem`
>`NODE_TLS_REJECT_UNAUTHORIZED=0`

## Execução do Serviço do Editor Universal {#running-ue}

Para iniciar o Universal Editor Service, execute o seguinte comando:

```text
$ node ./universal-editor-service.cjs
```

Ele deve enviar o seguinte para o terminal:

```text
Universal Editor Service listening on port 8000 as HTTPS Server
```

Certifique-se de que o serviço inicie o Servidor HTTPS e não o Servidor HTTP.

## Usar o serviço do editor universal local em vez do serviço global {#using-local-ue}

O Editor universal sabe qual Serviço do Editor universal usar para editar uma página com base em como a página é instrumentada. Isso é feito por meio de metatags na página carregada no Editor universal.

Para que uma página seja editada usando seu Universal Editor Service local, a seguinte meta tag deve ser definida:

```html
<meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
```

Depois de definido, você deve ver todas as chamadas de atualização de conteúdo indo para `https://localhost:8000` em vez do Universal Editor Service padrão.

>[!NOTE]
>
>A tentativa de acessar diretamente `https://localhost:8000` resulta em um erro `404`. Esse é o comportamento esperado.
>
>Para testar o acesso ao Universal Editor Service local, use `https://localhost:8000/corslib/LATEST`. Consulte a [próxima seção](#editing) para obter detalhes.

>[!TIP]
>
>Para obter mais detalhes sobre como as páginas são instrumentadas para usar o Serviço Global Universal Editor, consulte o documento [Introdução ao Universal Editor no AEM](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Editar uma página com o serviço do Editor universal local {#editing}

Com o [Serviço do Editor Universal sendo executado localmente](#running-ue) e sua [página de conteúdo instrumentada para usar o serviço local](/help/implementing/universal-editor/getting-started.md), agora você pode iniciar o editor.

1. Abra o navegador no `https://localhost:8000/ping`.
1. Direcione o navegador para aceitar [seu certificado autoassinado](#ue-https).
1. Quando o certificado autoassinado for confiável, você poderá editar a página usando o Serviço do Editor Universal local.

