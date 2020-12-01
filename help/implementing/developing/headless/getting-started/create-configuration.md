---
title: Criando um Guia de Start Rápido sem Cabeçalhos de Configuração
description: Como primeiro passo para começar a usar o recurso sem rumo em AEM como Cloud Service, é necessário criar uma configuração.
translation-type: tm+mt
source-git-commit: 7ed96dc0da879800d731983a0399b4f4fb3d7d41
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 2%

---


# Criando um Guia de Start Rápido sem Cabeçalho de Configuração {#creating-configuration}

Como primeiro passo para começar a usar o recurso sem rumo em AEM como Cloud Service, é necessário criar uma configuração.

## O que é uma configuração? {#what-is-a-configuration}

O Navegador de configuração fornece uma API de configuração genérica, estrutura de conteúdo, mecanismo de resolução para configurações no AEM.

No contexto de gestão de conteúdo sem cabeçalho no AEM, pense em uma configuração como um local de trabalho dentro do AEM onde você pode criar seus Modelos de conteúdo, que definem a estrutura do conteúdo futuro e dos Fragmentos de conteúdo. É possível ter várias configurações para separar esses modelos.

Se você estiver familiarizado com [modelos de página em uma implementação de pilha completa AEM,](/help/sites-cloud/authoring/features/templates.md) o uso de configurações para o gerenciamento de Modelos de conteúdo é semelhante.

## Como criar uma configuração {#how-to-create-a-configuration}

Um administrador só precisaria criar uma configuração uma vez ou muito egoísta quando uma nova área de trabalho for necessária para organizar seus Modelos de conteúdo. Para os fins deste guia de introdução, precisamos apenas criar uma configuração.

1. Efetue login no AEM como um Cloud Service e, no menu principal, selecione **Ferramentas -> Geral -> Navegador de configuração**.
1. Forneça um **Título** e um **Nome** para a sua configuração.
   * O **Title** deve ser descritivo.
   * O **Name** se tornará o nome do nó no repositório.
      * Será gerado automaticamente com base no título e ajustado de acordo com [AEM convenções de nomenclatura.](/help/implementing/developing/introduction/naming-conventions.md)
      * Pode ser ajustado, se necessário.
1. Verifique as seguintes opções:
   * **Modelos de fragmentos do conteúdo**
   * **Query Persistentes GraphQL**

   ![Criar configuração](../assets/create-configuration.png)

1. Toque ou clique em **Criar**

É possível criar várias configurações, se necessário. As configurações também podem ser aninhadas.

>!![NOTE]
As opções de configuração além de **Modelos de fragmento de conteúdo** e **Query persistentes GraphQL** podem ser necessárias, dependendo de seus requisitos de implementação.

## Próximas etapas {#next-steps}

Usando essa configuração, agora você pode seguir para a segunda parte do guia de introdução e [criar Modelos de Fragmento de Conteúdo.](create-content-model.md)

>!![TIP]
Para obter detalhes completos sobre o Navegador de configuração, [consulte a documentação do Navegador de configuração.](/help/implementing/developing/introduction/configurations.md)
