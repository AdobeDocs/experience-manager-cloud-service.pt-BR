---
title: Como usar a API de sincronização de saída AFP?
description: Saiba como usar a API de sincronização de saída AFP para recuperar e sincronizar representações de saída.
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, User
exl-id: 5602fc63-ef74-44eb-b3be-61b8f8a2795a
source-git-commit: cbf640e0c4643616638de96e9daa460cdcf2a4a5
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 10%

---

# Gerar saída AFP usando a API do AEM Forms

<span class="preview"> É um recurso de pré-lançamento acessível através do nosso [canal de pré-lançamento](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/release-notes/prerelease#new-features). </span>

O AFP (Advanced Function Presentation) é um formato de documento de alto desempenho projetado principalmente para fins de impressão.\
Este guia descreve todas as etapas e configurações necessárias para gerar a saída AFP usando o AEM Forms.

<!--
## Prerequisites

To support AFP output generation, the following OSGi bundles must be present and in an **active** state:

* **AFP Core Bundle** – Available in the AFP repository
* **Forms Output Core** – Found in the Forms Output comments package
* **Bedrock Connector** – Provided by the Forms Output API
* **Cloud Ready Implementation** – Available through the Forms installer

>[!NOTE]
>
> * If any bundle is inactive, resolve dependency issues or reinstall manually.
> * To enable AFP generation, the `FT_FORMS-17887` toggle configurations must be set in AEM configuration manager.-->

## API de geração de AFP

Gera um arquivo AFP (Advanced Function Presentation) usando um modelo XDP e dados de entrada.

### Autorização

Você pode usar o **BasicAuth** (credenciais de administrador) para ambientes locais ou a autorização **OAuth Server-to-Server** para instâncias da AEM Cloud.

### Solicitação

**Ponto de extremidade:**
[https://[publish-url].adobeaemcloud.com/adobe/forms/doc/v1/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post)

### Cabeçalhos

| Chave | Valor |
| --------------- | ------------------------------------------------------ |
| `Content-Type` | `application/pdf` |
| `Authorization` | `(Bearer Access token)` |

### Corpo da solicitação

**Tipo de conteúdo: multipart/form-data**

| Chave | Tipo | Obrigatório | Descrição |
| ---------- | ---- | -------- | ------------------------------------------------------------------------- |
| `template` | Arquivo/Texto | Sim | Arquivo XDP usado como modelo para geração de AFP (por exemplo, `demo.xdp`) |
| `data` | Arquivo/Texto | Não | Arquivo de dados (XML ou JSON) a ser mesclado com o modelo (por exemplo, `data.xml`) |
| `options` | Texto | Não | Sequência JSON com opções para controlar a saída AFP (por exemplo, resolução, localidade) |

**Exemplo `options` JSON (campo de texto):**

```json
{
  "pdfVersion": "1.7",
  "resolution": 300,
  "locale": "en-US",
  "embedFonts": true,
  "contentRoot": "/usr/tmp"
}
```

### Respostas

| Código | Descrição |
| ----- | ------------------------------------------------------------------------- |
| `200` | Operação bem-sucedida. Retorna o fluxo de documentos AFP. |
| `400` | Solicitação inválida. A carga da solicitação está malformada ou sem campos obrigatórios. |
| `500` | Erro interno do servidor. Tente novamente mais tarde. |

### Comando Curl

```
curl --location 'http://<server>:<port>/adobe/forms/document/generate/afp' \
--header 'Authorization: Bearertoken <base64-encoded-credentials>' \
--form 'template=@"<path-to-template>.xdp"' \
--form 'data=@"<path-to-data-file>.xml"' \
--form 'options=<JSON-options-string>'
```

### Teste da API

É possível baixar o arquivo .yaml e carregá-lo no Postman para verificar a funcionalidade das APIs.

![Imagem Postman AFP](/help/forms/assets/afp-postman.png)

Você pode salvar a resposta e abrir o arquivo salvo no leitor AFP para visualizá-lo.

![Localizar IC Docu](/help/forms/interactive-communication/assets/introimg.png)
