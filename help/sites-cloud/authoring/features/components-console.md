---
title: Console de componentes
description: O console Componentes permite navegar por todos os componentes definidos para a instância
exl-id: f4949331-5302-46d3-a004-b813bb95ec2f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 100%

---

# Console de componentes {#components-console}

O console Componentes permite navegar em todos os componentes definidos para a sua instância e exibir as principais informações de cada componente.

Ele pode ser acessado em **Ferramentas ->** **Geral ->** **Componentes**. Como não há uma estrutura de árvore para componentes, somente a visualização de lista está disponível.

![O console Componentes](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>O console Componentes mostra todos os componentes do sistema. O [Navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) mostra componentes que estão disponíveis para autores e oculta todos os grupos de componentes que começam com um ponto final ( `.`).

## Pesquisar {#search-field}

Com o ícone **Apenas conteúdo** (na parte superior esquerda), você pode abrir o painel **Pesquisar** para pesquisar e/ou filtrar os componentes: 

![Pesquisa no console Componentes](/help/sites-cloud/authoring/assets/components-console-search.png)

### Detalhes do componente {#component-details}

Para exibir detalhes sobre um componente específico, toque/clique no recurso desejado. As três guias fornecem:

* **Propriedades**

   ![Propriedades do console Componentes](/help/sites-cloud/authoring/assets/components-console-properties.png)

   Na guia Propriedades, é possível:

   * Veja as propriedades gerais do componente.
      * Visualizar como o ícone ou a abreviação foi definida para o componente. <!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * Clicar na origem do ícone levará você até esse componente.
   * Visualizar o **Tipo de recurso** e o **Supertipo do recurso** (se definido) para o componente.
      * Clicar no Supertipo do recurso levará você até esse componente.

   >[!NOTE]
   >
   >Como `/apps` não pode ser editado no tempo de execução, o console Componentes fica somente leitura.

* **Políticas**

   ![Políticas do console Componentes](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **Uso em tempo real**

   ![Uso em tempo real de componentes](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

   >[!CAUTION]
   >
   >Devido à natureza das informações coletadas para esta exibição, ela pode levar algum tempo para ser agrupada/exibida. 

* **Documentação**

   Se o desenvolvedor tiver fornecido a documentação referente ao componente, ela aparecerá na guia **Documentação**. Se não houver documentação disponível, a guia **Documentação** não será exibida. <!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

   ![Documentação do componente](/help/sites-cloud/authoring/assets/components-console-documentation.png)
