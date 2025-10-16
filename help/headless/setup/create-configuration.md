---
title: Criar uma configuração - Configuração do headless
description: Crie uma configuração como uma primeira etapa para começar a usar o headless no AEM as a Cloud Service.
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 68%

---

# Criar uma configuração - Configuração do headless {#create-configuration}

Como primeiro passo para começar a usar o headless no AEM as a Cloud Service, é necessário criar uma configuração.

## O que é uma configuração? {#what-is-a-configuration}

O Navegador de configuração fornece uma API de configuração genérica, uma estrutura de conteúdo e um mecanismo de resolução para configurações no AEM.

No contexto do gerenciamento de conteúdo headless no AEM, considere uma configuração como um local de trabalho dentro do AEM onde é possível criar modelos de conteúdo, que definem a estrutura do conteúdo futuro e dos fragmentos de conteúdo. É possível ter várias configurações para separar esses modelos.

Se você estiver familiarizado com os [modelos de página em uma implementação de pilha completa do AEM](/help/sites-cloud/authoring/page-editor/templates.md), o uso de configurações para o gerenciamento de Modelos de conteúdo é semelhante.

## Como criar uma configuração {#how-to-create-a-configuration}

Um administrador só precisaria criar uma configuração uma vez ou, muito raramente, quando um novo espaço de trabalho fosse necessário para organizar seus modelos de conteúdo. Para os propósitos deste guia de introdução, precisamos criar apenas uma configuração.

Para obter detalhes passo a passo, consulte [Habilitar a funcionalidade de fragmento de conteúdo no Navegador de Configuração](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser).

>[!NOTE]
>
>Outras opções de configuração além dos **Modelos de fragmento do conteúdo** e das **Consultas GraphQL persistidas** podem ser necessárias, dependendo de seus requisitos de implementação.

## Próximas etapas {#next-steps}

Usando essa configuração, agora é possível seguir para a segunda parte do guia de introdução e [criar modelos de fragmento de conteúdo](create-content-model.md).

>[!TIP]
>
>Para obter detalhes completos sobre o Navegador de Configuração, consulte a [documentação do Navegador de Configuração](/help/implementing/developing/introduction/configurations.md).
