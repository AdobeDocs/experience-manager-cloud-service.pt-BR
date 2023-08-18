---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: cf8b5d8b11452268b2839053c1e05cc2ec107a91
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 53%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 13173 {#release-13173}

Resumidos abaixo estão as melhorias contínuas da versão de manutenção 13173, que foi lançada publicamente em 18 de agosto de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior: versão 13099.

A Ativação de recursos 2023.8.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte a [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-13173}

Nenhum.

### Problemas corrigidos {#fixed-issues-13173}

- SITES-15463: Modelos de sites - Modelos não podem ser publicados.

### Problemas conhecidos {#known-issues-13173}

- SITES-15359: Fragmentos de conteúdo - O padrão de nome de variação não corresponde corretamente às variações que têm ```'_'``` em seus nomes de recursos.
- FORMS-10444: Modelos adaptáveis do Forms - Os modelos não podem ser publicados (solução alternativa: use o Console de distribuição).
- CQ-4354191: workflows - O iniciador personalizado pode ser acionado muitas vezes devido a metadados de replicação presentes em nós nt:unstructured (solução alternativa: atualize os iniciadores para excluir propriedades de metadados de replicação para evitar sobreposição).

### Tecnologias integradas {#embedded-tech-13173}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [API Oak 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| API do Sling do AEM | Versão 2.27.2 | [API do Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
