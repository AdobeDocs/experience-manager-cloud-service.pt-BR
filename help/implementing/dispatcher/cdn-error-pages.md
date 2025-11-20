---
title: Configuração de páginas de erro do CDN
description: Saiba como substituir a página de erro padrão hospedando arquivos estáticos no armazenamento auto-hospedado, como o Amazon S3 ou o Armazenamento de blobs do Azure, e fazendo referência a eles em um arquivo de configuração implantado usando o pipeline de configuração do Cloud Manager.
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
role: Admin
source-git-commit: 3a46db9c98fe634bf2d4cffd74b54771de748515
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---


# Configuração de páginas de erro do CDN {#cdn-error-pages}

No evento improvável de que a [CDN gerenciada pela Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) não possa acessar a origem do AEM, a CDN serve por padrão uma página de erro genérica e sem marca que indica que o servidor não pode ser acessado. Você pode substituir a página de erro padrão hospedando arquivos estáticos no armazenamento auto-hospedado, como o Amazon S3 ou o Armazenamento de Blob do Azure, e fazendo referência a eles em um arquivo de configuração implantado com o uso do [pipeline de configuração](/help/operations/config-pipeline.md#managing-in-cloud-manager) do Cloud Manager.

## Configurar {#setup}

Antes de substituir a página de erro padrão, é necessário fazer o seguinte:

1. Crie um arquivo com o nome `cdn.yaml` ou similar, fazendo referência à seção de sintaxe abaixo.

1. Coloque o arquivo em algum lugar em uma pasta de nível superior chamada *config* ou similar, conforme descrito em [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#folder-structure).

1. Crie um pipeline de configuração no Cloud Manager, conforme descrito em [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#managing-in-cloud-manager).

1. Implante a configuração.

### Sintaxe {#syntax}

A página de erro é implementada como um aplicativo de página única (SPA) e faz referência a algumas propriedades, como mostrado no exemplo abaixo.  Os arquivos estáticos referenciados pelos urls devem ser hospedados por você em um serviço acessível pela Internet, como o Amazon S3 ou o Armazenamento de blobs do Azure.

Exemplo de configuração:

```
kind: "CDN"
version: "1"
data:
  errorPages:
    spa:
      title: the error page
      icoUrl: https://www.example.com/error.ico
      cssUrl: https://www.example.com/error.css
      jsUrl: https://www.example.com/error.js
```

Consulte [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#common-syntax) para obter uma descrição das propriedades acima do nó de dados. O valor da propriedade kind deve ser *CDN* e a propriedade `version` deve ser definida como *1*.


| Nome | Propriedades permitidas | Significado |
|-----------|--------------------------|-------------|
| **spa** | cargo | Título da página de erro. |
|     | icoUrl | URL para um arquivo de ícone. |
|     | cssUrl | URL para um arquivo CSS. |
|     | jsUrl | URL para um arquivo JavaScript. |

### HTML gerado por exemplo {#sample-generated-html}

O código HTML gerado pela CDN e fornecido ao cliente, como um navegador, será semelhante (mas não idêntico) ao seguinte trecho:

```
<!DOCTYPE html>
<html lang="en">
    <head>
        ...
        <title>the error page</title>
        <link rel="icon" href="https://www.example.com/error.ico">
        <link rel="stylesheet" href="https://www.example.com/error.css">
    </head>
    <body>
        ...
        <div id="root" status="403"></div>
        <script src="https://www.example.com/error.js"> </script>
    </body>
</html>
```

### Testes {#testing}

Para fins de teste, chame o endpoint dedicado com o código de erro compatível, por exemplo:

```
curl "https://publish-pXXXXX-eXXXXXX.adobeaemcloud.com/cdnstatus?code=403"
```

Os códigos compatíveis são: 403, 404, 406, 500 e 503.

Dessa forma, você aciona diretamente o manipulador de erros do CDN para testar a resposta sintética de um determinado código de erro.

### Tutorial

Consulte o tutorial [páginas de erro da CDN](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/content-delivery/custom-error-pages#cdn-error-pages) para obter instruções passo a passo sobre como criar, implantar e testar as páginas de erro fornecidas pela CDN.


