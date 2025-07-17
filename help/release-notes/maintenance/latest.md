---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 2e90e40a0fe439653987a23792a4c1ec612aafd6
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 40%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 21570 {#21570}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 21570, lançada publicamente em quarta-feira, 15 de julho de 2025. A versão de manutenção anterior era 21484.

>[!NOTE]
>
>A [Versão 21484](/help/release-notes/maintenance/2025/2025-7-0.md#21484) tornou-se privada e foi substituída pela versão 21570.

A ativação de recursos do 2025.7.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-21570}

* Migrado para o Apache Httpd 2.4.63

### Problemas corrigidos {#fixed-issues-21570}

* SKYOPS-112722 - Correção de um problema que causava a falha da resolução de URLs personalizados

### Problemas conhecidos {#known-issues-21570}

* O AEM SDK relacionado possui uma ID de versão diferente (21575) e está disponível por meio do Portal de distribuição de software.
* A versão 2.4.63 do Apache HTTP Server introduziu uma mudança radical no modo como o `mod_rewrite` lida com pontos de interrogação (`?`) em URLs. Esta alteração foi implementada para impedir o uso do sinalizador `UnsafeAllow3F`, que foi considerado um risco de segurança. Isso afeta quaisquer diretivas `RewriteRule` que dependem da detecção de ponto de interrogação em padrões de URL.

### Recursos e APIs obsoletos {#deprecated-21570}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-21570}

Nenhum

### Tecnologias integradas {#embedded-tech-21570}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| Componentes principais do AEM | 2.29.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
