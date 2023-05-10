---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: ea3a476f7f2d7d97a2428c6facf61b746dba7a23
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 65%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 11873 {#release-11873}

Resumidos abaixo estão as melhorias contínuas da versão de manutenção 11873, lançada publicamente em 3 de maio de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior: 11835.

A ativação de recursos desta versão de manutenção fornecerá o conjunto completo de recursos. Consulte as [notas de versão atuais](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter detalhes completos.

### Aprimoramentos {#enhancements}

- SITES-1200 - Melhorias na API de pesquisa com filtragem baseada em tags
- GRANITE-42939 - Adicionar anotações e avisos de descontinuação ao código oauth-server

### Problemas conhecidos {#known-issues-11873}

Nenhum.

### Problemas corrigidos {#fixed-issues-11873}

- SKYSI-19884/SKYOPS-53745 - Corrigido um problema com PublishPageRenderingErrorsHigh
- GRANITE-4388 - Correção da degradação da taxa de transferência após um grande número de gravações de ativos do DAM no Mongo
- SITES-11922 - Corrigido um problema com o cancelamento da publicação da visualização que não removia o status de sincronização
- ASSETS-21648 - Correção de um problema de permissão com a funcionalidade de relacionamento entre ativos

### Tecnologias integradas {#embedded-tech-11873}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API Oak 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API do Sling do AEM | Versão 2.27.0 | [API do Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.21.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
