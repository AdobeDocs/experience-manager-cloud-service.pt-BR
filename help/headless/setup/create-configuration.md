---
title: Criação de uma configuração - Configuração sem cabeçalho
description: Crie uma configuração como uma primeira etapa para começar a usar o headless em AEM as a Cloud Service.
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
source-git-commit: e81b852dc90e3cc5abc8b9f218f48d0fc1cc66eb
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 3%

---

# Criação de uma configuração - Configuração sem cabeçalho {#creating-configuration}

Como primeiro passo para começar a usar o headless em AEM as a Cloud Service, é necessário criar uma configuração.

## O que é uma configuração? {#what-is-a-configuration}

O Navegador de configuração fornece uma API de configuração genérica, estrutura de conteúdo, mecanismo de resolução para configurações no AEM.

No contexto do gerenciamento de conteúdo sem periféricos no AEM, considere uma configuração como um local de trabalho no AEM onde você pode criar os Modelos de conteúdo, que definem a estrutura do conteúdo futuro e os Fragmentos de conteúdo. É possível ter várias configurações para separar esses modelos.

Se você estiver familiarizado com [modelos de página em uma implementação de AEM de pilha completa,](/help/sites-cloud/authoring/features/templates.md) o uso de configurações para o gerenciamento de Modelos de conteúdo é semelhante.

## Como criar uma configuração {#how-to-create-a-configuration}

Um administrador só precisaria criar uma configuração uma vez ou muito automaticamente quando um novo espaço de trabalho for necessário para organizar seus Modelos de conteúdo. Para o objetivo deste guia de introdução, precisamos apenas criar uma configuração.

1. Efetue login AEM as a Cloud Service e, no menu principal, selecione **Ferramentas -> Geral -> Navegador de configuração**.
1. Forneça uma **Título** e **Nome** para sua configuração.
   * O **Título** deve ser descritiva.
   * O **Nome** se tornará o nome do nó no repositório.
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
>Opções de configuração além de **Modelos de fragmentos do conteúdo** e **Consultas Persistentes GraphQL** pode ser necessário, dependendo de seus requisitos de implementação.

## Próximas etapas {#next-steps}

Usando essa configuração, agora você pode seguir para a segunda parte do guia de introdução e [criar Modelos de fragmentos do conteúdo.](create-content-model.md)

>[!TIP]
>
>Para obter detalhes completos sobre o Navegador de configuração, [consulte a documentação do Navegador de configuração .](/help/implementing/developing/introduction/configurations.md)
