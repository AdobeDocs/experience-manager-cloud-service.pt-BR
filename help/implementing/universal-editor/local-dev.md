---
title: Desenvolvimento local do AEM com o editor universal
description: Saiba como o Editor universal oferece suporte à edição em instâncias locais do AEM para fins de desenvolvimento.
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
source-git-commit: 0bb649b91c42f43b852d7fdd54b367c0c5df2c99
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---


# Desenvolvimento local do AEM com o editor universal {#local-dev-ue}

Saiba como o Editor universal oferece suporte à edição em instâncias locais do AEM para fins de desenvolvimento.

## Visão geral {#overview}

O Universal Editor Service é o que vincula o Universal Editor e o sistema de back-end. Para desenvolver localmente para o Universal Editor, você deve executar uma cópia local do Universal Editor Service. Isso ocorre porque:

* O Serviço Editor Universal oficial do Adobe é hospedado globalmente, e sua instância AEM local precisaria ser exposta à internet.
* Ao desenvolver com um SDK AEM local, o Adobe Universal Editor Service não pode ser acessado na Internet.
* Se a instância do AEM tiver restrições de IP e o Adobe Universal Editor Service não estiver em um intervalo de IP definido, você mesmo poderá hospedá-lo.

Este documento explica como executar o AEM em HTTPS junto com uma cópia local do Universal Editor Service para que você possa desenvolver localmente no AEM para uso com o Universal Editor.

## Configurar AEM para execução em HTTPS {#aem-https}

Em um quadro externo protegido com HTTPS, um quadro HTTP não seguro não pode ser carregado. O Universal Editor Service é executado em HTTPS e, portanto, o AEM ou qualquer outra página remota também deve ser executado em HTTPS.

Para fazer isso, é necessário configurar o AEM para ser executado em HTTPS. Para fins de desenvolvimento, é possível usar o certificado autoassinado.

[Consulte este documento](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=pt-BR) sobre como configurar o AEM em HTTPS, incluindo um certificado autoassinado que você pode usar.

## Instalar o Universal Editor Service {#install-ue-service}

O Universal Editor Service não é uma cópia inteira do Universal Editor, mas apenas um subconjunto de seus recursos para garantir que as chamadas do seu ambiente local do AEM não sejam roteadas pela Internet, mas de um terminal definido sob seu controle.

[NodeJS versão 16](https://nodejs.org/en/download/releases) é necessário para executar uma cópia local do Universal Editor Service.

O Universal Editor Service está disponível por meio da Distribuição de software. Consulte a [Documentação de Distribuição de software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=pt-br) para obter detalhes sobre como acessá-lo.

Salve o `universal-editor-service.cjs` de Distribuição de software para o ambiente de desenvolvimento local.

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

```html
<meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
```

Depois de definido, você deve ver cada chamada de atualização de conteúdo ir para `https://localhost:8000` em vez do Universal Editor Service padrão.

>[!NOTE]
>
>Tentando acessar diretamente `https://localhost:8000` resulta em uma `404` erro. Esse é o comportamento esperado.
>
>Para testar o acesso ao Universal Editor Service local, use `https://localhost:8000/corslib/LATEST`. Consulte a [próxima seção](#editing) para obter detalhes.

>[!TIP]
>
>Para obter mais detalhes sobre como as páginas são instrumentadas para usar o Global Universal Editor Service, consulte o documento [Introdução ao editor universal no AEM](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Editar uma página com o serviço do Editor universal local {#editing}

Com o [Serviço do Editor Universal em execução localmente](#running-ue) e seu [página de conteúdo instrumentada para usar o serviço local,](#using-loca-ue) agora você pode iniciar o editor.

1. Abra o navegador para `https://localhost:8000/corslib/LATEST`.
1. Direcione o navegador para aceitar [seu certificado autoassinado.](#ue-https)
1. Quando o certificado autoassinado for confiável, você poderá editar a página usando o Serviço do Editor Universal local.
