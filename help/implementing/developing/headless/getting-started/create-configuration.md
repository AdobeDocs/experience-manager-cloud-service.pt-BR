---
title: Criação de um Guia de início rápido sem cabeçalho de configuração
description: Crie uma configuração como uma primeira etapa para começar a usar o headless no AEM como um Cloud Service.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---


# Criação de um Guia de início rápido sem cabeçalho de configuração {#creating-configuration}

Como primeiro passo para começar a usar o headless no AEM as a Cloud Service, é necessário criar uma configuração.

## O que é uma configuração? {#what-is-a-configuration}

O Navegador de configuração fornece uma API de configuração genérica, estrutura de conteúdo, mecanismo de resolução para configurações no AEM.

No contexto do gerenciamento de conteúdo sem periféricos no AEM, considere uma configuração como um local de trabalho no AEM onde você pode criar os Modelos de conteúdo, que definem a estrutura do conteúdo futuro e os Fragmentos de conteúdo. É possível ter várias configurações para separar esses modelos.

Se você estiver familiarizado com [modelos de página em uma implementação de pilha completa,](/help/sites-cloud/authoring/features/templates.md) o uso de configurações para o gerenciamento de Modelos de conteúdo é semelhante.

## Como criar uma configuração {#how-to-create-a-configuration}

Um administrador só precisaria criar uma configuração uma vez ou muito automaticamente quando um novo espaço de trabalho for necessário para organizar seus Modelos de conteúdo. Para o objetivo deste guia de introdução, precisamos apenas criar uma configuração.

1. Efetue login no AEM como um Cloud Service e, no menu principal, selecione **Tools -> General -> Configuration Browser**.
1. Forneça um **Título** e um **Nome** para sua configuração.
   * O **Title** deve ser descritivo.
   * O **Name** se tornará o nome do nó no repositório.
      * Ele será gerado automaticamente com base no título e ajustado de acordo com [AEM convenções de nomenclatura.](/help/implementing/developing/introduction/naming-conventions.md)
      * Pode ser ajustado, se necessário.
1. Verifique as seguintes opções:
   * **Modelos de fragmentos do conteúdo**
   * **Consultas Persistentes GraphQL**

   ![Criar configuração](../assets/create-configuration.png)

1. Toque ou clique em **Criar**

É possível criar várias configurações, se necessário. As configurações também podem ser aninhadas.

>[!NOTE]
>
>As opções de configuração, além dos **Modelos de fragmento de conteúdo** e **Consultas persistentes de GraphQL** podem ser necessárias, dependendo dos requisitos de implementação.

## Próximas etapas {#next-steps}

Usando essa configuração, agora você pode seguir para a segunda parte do guia de introdução e [criar Modelos de Fragmento de Conteúdo.](create-content-model.md)

>[!TIP]
>
>Para obter detalhes completos sobre o Navegador de configuração, [consulte a documentação do Navegador de configuração.](/help/implementing/developing/introduction/configurations.md)
