---
title: Configuração de páginas de erro do CDN
description: Saiba como substituir a página de erro padrão hospedando arquivos estáticos no armazenamento auto-hospedado, como o Amazon S3 ou o Armazenamento de blobs do Azure, e fazendo referência a eles em um arquivo de configuração implantado usando o Pipeline de configuração do Cloud Manager.
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 1%

---

# Configuração de páginas de erro do CDN {#cdn-error-pages}

No evento improvável de que o [CDN gerenciado por Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) não possa atingir a origem AEM, o CDN por padrão fornece uma página de erro genérica e sem marca que indica que o servidor não pode ser alcançado. Você pode substituir a página de erro padrão hospedando arquivos estáticos no armazenamento auto-hospedado, como o Amazon S3 ou o Armazenamento de Blobs do Azure, e fazendo referência a eles em um arquivo de configuração implantado usando o [Pipeline de Configuração do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline).

## Configurar {#setup}

Antes de substituir a página de erro padrão, é necessário fazer o seguinte:

* Crie esta pasta e estrutura de arquivo na pasta de nível superior do seu projeto Git:

```
config/
     cdn.yaml
```

* O arquivo de configuração `cdn.yaml` deve conter metadados e as regras descritas nos exemplos abaixo. O parâmetro `kind` deve ser definido como `CDN` e a versão deve ser definida como a versão do esquema, que atualmente é `1`.

* Crie um pipeline de configuração de implantação direcionada no Cloud Manager. Consulte [configuração de pipelines de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e [configuração de pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

**Notas**

* Atualmente, os RDEs não oferecem suporte ao pipeline de configuração.
* Você pode usar `yq` para validar localmente a formatação YAML do seu arquivo de configuração (por exemplo, `yq cdn.yaml`).

### Configuração {#configuration}

A página de erro é implementada como um aplicativo de página única (SPA) e faz referência a algumas propriedades, como mostrado no exemplo abaixo.  Os arquivos estáticos referenciados pelos urls devem ser hospedados por você em um serviço acessível pela Internet, como o Amazon S3 ou o Armazenamento de blobs do Azure.

Exemplo de configuração:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  errorPages:
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

Dessa forma, você aciona diretamente o manipulador de erros do CDN para testar a resposta sintética de um determinado código de erro.
