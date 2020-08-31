---
title: Componentes Visão geral
description: Os componentes são unidades modulares que obtêm funcionalidade específica para apresentar seu conteúdo em seu site
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 5%

---


# Visão geral dos componentes {#components-overview}

Esta página fornece uma visão geral dos componentes do Adobe Experience Manager (AEM), como os [usados para criação](/help/sites-cloud/authoring/fundamentals/components.md)de página.

## O que são os componentes? {#what-are-components}

Os componentes em AEM são:

* Unidades modulares que realizam funcionalidades específicas para apresentar seu conteúdo em seu site.
* Reutilizável.
* Desenvolvido como unidades independentes em uma pasta do repositório.
* Não tem arquivos de configuração ocultos.
* Pode conter outros componentes.
* Pode ser executado em qualquer lugar dentro de qualquer sistema AEM e também pode ser limitado a ser executado em componentes específicos.
* Tenha uma interface de usuário padronizada.
* Ter comportamento de edição que possa ser configurado.
* Use caixas de diálogo que são criadas usando subelementos com base nos componentes da interface do usuário do Granite.
* São desenvolvidos usando [HTL](https://docs.adobe.com/content/help/pt-BR/experience-manager-htl/using/overview.html).
* Pode ser desenvolvido para criar componentes personalizados que estendem a funcionalidade padrão.

Como os componentes são modulares, você pode:

* Desenvolva um novo componente na sua instância local.
* Implante-o no ambiente de teste.
* Implante-o em seu ambiente de criação ao vivo, onde eles permitem que autores e/ou administradores adicionem e configurem conteúdo.
* Implante-o em seus ambientes de publicação ao vivo, onde eles são usados para renderizar o conteúdo de visitantes em seu site.

Cada componente AEM:

* É um tipo de recurso.
* É uma coleção de scripts que executa completamente uma função específica.
* Pode funcionar isoladamente, ou seja, dentro de AEM ou de um portal.

## AEM Core Components {#aem-core-components}

[Os componentes](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) principais AEM são um conjunto de componentes padronizados de Gestão de conteúdo da Web (WCM) para AEM acelerar o tempo de desenvolvimento e reduzir o custo de manutenção de seus sites.

Os Componentes principais são fornecidos com AEM como um Cloud Service e o Tutorial [da](/help/implementing/developing/introduction/develop-wknd-tutorial.md) WKND ilustra como implementar e usar componentes. Os componentes são fornecidos com todo o código fonte e podem ser usados como estão ou como pontos de partida para componentes modificados ou estendidos.

### Exibindo componentes disponíveis {#viewing-available-components}

Para obter uma visão geral de todos os componentes disponíveis em sua instância AEM, use o Console [de](/help/sites-cloud/authoring/features/components-console.md)componentes.

Como alternativa, você também pode usar o CRXDE Lite para obter uma lista de todos os componentes disponíveis no repositório.

1. No **[!UICONTROL CRXDE Lite]**, selecione **[!UICONTROL Ferramentas]** na barra de ferramentas e, em seguida, no **[!UICONTROL Query]**, que abre a guia **[!UICONTROL Query]** .

1. Na guia **[!UICONTROL Query]** , selecione `XPath` como **[!UICONTROL Tipo]**.

1. No campo de entrada do **[!UICONTROL Query]** , digite a seguinte string:

   `//element(*, cq:Component)`

1. Clique em **[!UICONTROL Executar]** e os componentes são listados.

