---
title: Visão geral dos componentes
description: Os componentes são unidades modulares que realizam funcionalidades específicas para apresentar seu conteúdo em seu site
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 4%

---

# Visão geral dos componentes {#components-overview}

Esta página fornece uma visão geral dos componentes do Adobe Experience Manager (AEM), como esses [usado para criação de página](/help/sites-cloud/authoring/fundamentals/components.md).

## O que são Componentes? {#what-are-components}

Os componentes em AEM são:

* Unidades modulares que realizam funcionalidades específicas para apresentar seu conteúdo em seu site.
* Reutilizável.
* Desenvolvido como unidades independentes em uma pasta do repositório.
* Não tem arquivos de configuração ocultos.
* Pode conter outros componentes.
* Pode ser executado em qualquer lugar em qualquer sistema de AEM e também pode ser limitado a ser executado em componentes específicos.
* Ter uma interface de usuário padronizada.
* Ter um comportamento de edição que possa ser configurado.
* Use caixas de diálogo que são criadas usando subelementos com base nos componentes da interface do Granite.
* São desenvolvidos usando [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=pt-BR).
* Pode ser desenvolvido para criar componentes personalizados que estendem a funcionalidade padrão.

Como os componentes são modulares, você pode:

* Desenvolva um novo componente na instância local.
* Implante-o no ambiente de teste.
* Implante-o no ambiente de criação ao vivo, onde eles permitem que autores e/ou administradores adicionem e configurem conteúdo.
* Implante-o em seu ambiente de publicação ao vivo, onde eles são usados para renderizar o conteúdo para os visitantes do seu site.

Cada componente AEM:

* É um tipo de recurso.
* É uma coleção de scripts que executa completamente uma função específica.
* Pode funcionar isoladamente, ou seja, dentro de AEM ou de um portal.

## Componentes principais do AEM {#aem-core-components}

[Os Componentes principais do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) são um conjunto de componentes padronizados do Web Content Management (WCM) para AEM a fim de acelerar o tempo de desenvolvimento e reduzir o custo de manutenção de seus sites.

Os Componentes principais são fornecidos com AEM as a Cloud Service e a variável [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) ilustra como implementar e usar componentes. Os componentes são fornecidos com todo o código-fonte e podem ser usados como estão ou como pontos de partida para componentes modificados ou estendidos.

### Visualizando componentes disponíveis {#viewing-available-components}

Para obter uma visão geral de todos os componentes disponíveis na sua instância do AEM, use o [Console de componentes](/help/sites-cloud/authoring/features/components-console.md).

Como alternativa, você também pode usar o CRXDE Lite para obter uma lista de todos os componentes disponíveis no repositório.

1. Em **[!UICONTROL CRXDE Lite]**, selecione **[!UICONTROL Ferramentas]** na barra de ferramentas, em seguida **[!UICONTROL Query]**, que abre o **[!UICONTROL Query]** guia .

1. No **[!UICONTROL Query]** guia , selecione `XPath` as **[!UICONTROL Tipo]**.

1. No **[!UICONTROL Query]** campo de entrada, digite a seguinte string:

   `//element(*, cq:Component)`

1. Clique em **[!UICONTROL Executar]** e os componentes são listados.
