---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 241dcc75e9f2c840be85c34800d8145457baa58d
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 43%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 12697 {#release-12697}

Resumidos abaixo estão as melhorias contínuas da versão de manutenção 12697, que foi lançada publicamente em 14 de julho de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior: versão 12549. A versão de manutenção 12697 substitui 12585 para corrigir um problema.

A Ativação de recursos 2023.7.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte a [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-12697}

- Melhorias gerais na estabilidade RDE (SKYOPS-61133, SKYOPS-55281, SKYOPS-61216 e SKYOPS-61401)
- DXML-12327: Guias AEM: Suporte para variáveis de idioma na publicação de PDF nativo
- DXML-11518: Guias AEM: suporte aprimorado a metadados na publicação de PDF nativo
- DXML-10093: Guias AEM: Suporte para conectar-se a fontes de dados externas e inserir dados em tópicos dita
- DXML-10699: Guias AEM: suporte para o formato XLIFF na tradução
- DXML-10141: Guias AEM: Opção para usar a publicação baseada em microsserviços para tipos de predefinição PDF (Nativo e DITA-OT), HTML e Personalizado
- SKYOPS-61385 - Atualize o dispatcher para usar libpcre2 ao avaliar expressões regulares no Apache HTTPD

### Problemas corrigidos {#fixed-issues-12697}

- Guias do AEM: Várias melhorias de PDF nativo e correções de estabilidade
- SKYOPS-53130: Melhore o suporte à ferramenta CA no RDE
- SKYOPS-57146: Corrigir bloqueio do Sling na inicialização do AEM

### Problemas conhecidos {#known-issues-12697}

Nenhum.

### Tecnologias integradas {#embedded-tech-12697}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [API Oak 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| API do Sling do AEM | Versão 2.27.2 | [API do Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
