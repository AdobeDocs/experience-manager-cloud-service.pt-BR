---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 60952db4172b882b71a0b230fc8f4c27154e9cc0
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 36%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 15977 {#release-15977}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 15977, lançada publicamente em sábado, 19 de abril de 2024. A versão de manutenção anterior era a versão 15939.

A Ativação de recursos do 2024.4.0 fornece o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-15977}

* GRANITE-51335: Otimize a verificação de integridade do AEM para aumentar a estabilidade da instância.

### Problemas corrigidos {#fixed-issues-15977}

* CQ-4357226: corrija a regressão no suporte a configurações IMS para credenciais OAuth.
* GRANITE-51335: Atualização de Ratelimit para 5.0.4 Corrigidos registros Felix Health Check.

### Problemas conhecidos {#known-issues-15977}

* **(Somente para o AEM Forms)** Depois de instalar a versão de manutenção 15977 do AEM Cloud Foundation, os campos do Formulário adaptável são renderizados na ordem incorreta durante a criação do formulário e para formulários publicados. Se você usa o AEM Forms, a Adobe recomenda que você não atualize para a versão 15977 até que o problema seja resolvido na próxima versão de manutenção. Isso pode ajudá-lo a evitar inconvenientes.

### Recursos e APIs obsoletos {#deprecated-15977}

* [Descontinuação de credenciais JWT no console do Adobe Developer](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* A partir de 1 de maio de 2024, o Adobe Dynamic Media encerrará o suporte para o seguinte:

   * SSL (Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS (Transport Layer Security) 1.0 e 1.1
   * As seguintes cifras fracas no TLS 1.2:
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


Para saber o que está obsoleto ou foi removido no AEM as a Cloud Service, consulte [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Tecnologias integradas {#embedded-tech-15977}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.62.0 | [API Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| API DO SLING DO AEM | 2.27.2 | [API Apache Sling API 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.24.6 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
