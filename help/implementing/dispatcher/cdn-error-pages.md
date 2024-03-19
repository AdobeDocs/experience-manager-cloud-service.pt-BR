---
title: Configuração de páginas de erro do CDN
description: Saiba como substituir a página de erro padrão hospedando arquivos estáticos no armazenamento auto-hospedado, como o Amazon S3 ou o Armazenamento de blobs do Azure, e fazendo referência a eles em um arquivo de configuração implantado usando o Pipeline de configuração do Cloud Manager.
feature: Dispatcher
source-git-commit: 11036c3e95f0444fc5d865232a7dccab5b7f26ae
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---


# Configuração de páginas de erro do CDN {#cdn-error-pages}

>[!NOTE]
>Esse recurso ainda não está disponível para o público geral. Para participar do programa de adoção antecipada, envie um email para `aemcs-cdn-config-adopter@adobe.com` e descreva seu caso de uso.

No caso improvável de a [CDN gerenciada por Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) não puder acessar a origem do AEM, o CDN por padrão fornece uma página de erro genérica e sem marca que indica que o servidor não pode ser acessado. Você pode substituir a página de erro padrão hospedando arquivos estáticos no armazenamento auto-hospedado, como o Amazon S3 ou o Armazenamento de blobs do Azure, e fazendo referência a eles em um arquivo de configuração implantado usando o [Pipeline de configuração do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline).

## Configurar {#setup}

Antes de substituir a página de erro padrão, é necessário fazer o seguinte:

* Primeiro, crie esta pasta e a estrutura de arquivo na pasta de nível superior do seu projeto Git:

```
config/
     cdn.yaml
```

* Em segundo lugar, a `cdn.yaml` o arquivo de configuração deve conter metadados e as referências da página de erro, conforme descrito abaixo.

### Configuração {#configuration}

A página de erro é implementada como um aplicativo de página única (SPA) e faz referência a algumas propriedades, como mostrado no exemplo abaixo.  Os arquivos estáticos referenciados pelos urls devem ser hospedados por você em um serviço acessível pela Internet, como o Amazon S3 ou o Armazenamento de blobs do Azure.

Exemplo de configuração:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_errorPages:
    spa:
      title: the error page
      icoUrl: https://www.example.com/error.ico
      cssUrl: https://www.example.com/error.css
      jsUrl: https://www.example.com/error.js
```

| Nome | Propriedades permitidas | Significado |
|-----------|--------------------------|-------------|
| **spa** | cargo | Título da página de erro. |
|     | icoUrl | URL para um arquivo de ícone. |
|     | cssUrl | URL para um arquivo CSS. |
|     | jsUrl | URL para um arquivo JavaScript. |

### HTML gerado por exemplo {#sample-generated-html}

O código HTML gerado pelo CDN e fornecido ao cliente, como um navegador, será semelhante (mas não idêntico) ao seguinte trecho:

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

Dessa forma, você aciona diretamente o manipulador de erros do CDN para testar a resposta sintética de determinado código de erro.
