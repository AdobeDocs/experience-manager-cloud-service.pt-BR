---
title: Notas de versão de manutenção mais recentes da [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão de manutenção mais recentes da [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: 76da86d31e2780c2d22419cb8a338cf37963fad8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 5%

---


# Notas de versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as rotas de lançamento técnico da versão de manutenção mais recente do Experience Manager as a Cloud Service.

## Versão 10912 {#release-10912}

Resumidos abaixo estão as melhorias contínuas da versão de manutenção de 10912, lançada publicamente em 3 de fevereiro de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior 9850.

A ativação de recursos para esta versão de manutenção fornecerá o conjunto completo de recursos. Consulte a [notas de versão atuais](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter detalhes completos.

### Problemas conhecidos {#known-issues}

Não atualize se estiver usando o CORS. Identificamos um problema que afeta a parte da entrega de conteúdo do GraphQL nesta versão. Uma alteração na configuração padrão AEM dispatcher sobre como as consultas persistentes do GraphQL são armazenadas em cache pode quebrar a entrega de conteúdo do GraphQL de consultas persistentes para clientes usando uma configuração CORS.

### Tecnologias integradas {#embedded-tech}

| Tecnologia | Versão | Link |
|---|---|---|
| Componentes principais do WCM AEM | Versão 2.21.2 | [GitHub](https://github.com/adobe/aem-core-wcm-components) |
