---
title: Desenvolvimento local do AEM com o editor universal
description: Saiba como o Editor universal oferece suporte à edição em instâncias locais do AEM para fins de desenvolvimento.
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Desenvolvimento local do AEM com o editor universal {#local-dev-ue}

Saiba como o Editor universal oferece suporte à edição em instâncias locais do AEM para fins de desenvolvimento.

Este documento explicará como executar o AEM em HTTPS junto com uma cópia local do Universal Editor Service para que você possa desenvolver localmente no AEM usando o Universal Editor.

## Configurar AEM para execução em HTTPS {#aem-https}

Em um quadro externo protegido com HTTPS, um quadro HTTP não seguro não pode ser carregado. O Universal Editor Service é executado em HTTPS e, portanto, o AEM ou qualquer outra página remota também deve ser executado em HTTPS.

Para fazer isso, é necessário configurar o AEM para ser executado em HTTPS. Para fins de desenvolvimento, é possível usar o certificado autoassinado.

Consulte este documento sobre como configurar o AEM em execução em HTTPS, incluindo um certificado autoassinado que você pode usar.

## Instalar o Universal Editor Service {#install-ue-service}

O Universal Editor Service é o que vincula o Universal Editor e o sistema de back-end. Como o Universal Editor Service oficial está hospedado globalmente, sua instância de AEM local precisará ser exposta à Internet. Para evitar isso, execute uma cópia local do Universal Editor Service.

[NodeJS versão 16](https://nodejs.org/en/download/releases) é necessário para executar uma cópia local do Universal Editor Service

O Universal Editor Service é distribuído diretamente pela Engenharia de AEM. Entre em contato com seu engenheiro no programa VIP para obter uma cópia local.

A engenharia fornecerá a você uma `universal-editor-service.cjs` arquivo. Salve no ambiente de desenvolvimento local.

## Criar um certificado para executar o Universal Editor Service com HTTPS {#ue-https}

O Universal Editor Service também requer um certificado para ser executado em HTTPS no ambiente de desenvolvimento.

Execute o seguinte comando.

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

O comando gera um `key.pem` e uma `certificate.pem` arquivo. Salve esses arquivos no mesmo caminho do `universal-editor-service.cjs` arquivo.

## Definição da configuração do Serviço do Editor Universal {#setting-up-service}

Várias variáveis de ambiente devem ser definidas no NodeJS para executar o Universal Editor Service localmente.

No mesmo caminho que o `universal-editor-service.cjs`, `key.pem` e `certificate.pem` arquivos, crie um `.env` com o seguinte conteúdo.

```text
EXPRESS_PORT=8000
EXPRESS_PRIVATE_KEY=./key.pem
EXPRESS_CERT=./certificate.pem
NODE_TLS_REJECT_UNAUTHORIZED=0
```

A variável tem os seguintes significados:

* `EXPRESS_PORT`: define em qual porta o Serviço do Editor Universal escuta
* `EXPRESS_PRIVATE`: aponta para o seu [chave privada criada anteriormente,](#ue-https) `key.pem`
* `EXPRESS_CERT`: aponta para o seu [certificado criado anteriormente,](#ue-https) `certificate.pem`
* `NODE_TLS_REJECT_UNAUTHORIZED=0`: aceita certificados autoassinados

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

```
<meta name="urn:adobe:aem:editor:endpoint" content="https://localhost:8000">
```

Depois de definido, você deve ver cada chamada de atualização de conteúdo ir para `https://localhost:8000` em vez do Universal Editor Service padrão.

>[!TIP]
>
>Para obter mais detalhes sobre como as páginas são instrumentadas para usar o Global Universal Editor Service, consulte o documento [Introdução ao editor universal no AEM](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Editar uma página com o serviço do Editor universal local {#editing}

Com o [Serviço do Editor Universal em execução localmente](#running-ue) e seu [página de conteúdo instrumentada para usar o serviço local,](#using-loca-ue) agora você pode iniciar o editor.

1. Abra o navegador para `https://localhost:8000/`.
1. Direcione o navegador para aceitar [seu certificado autoassinado.](#ue-https)
1. Quando o certificado autoassinado for confiável, você poderá editar a página usando o Serviço do Editor Universal local.
