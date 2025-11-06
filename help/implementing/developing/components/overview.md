---
title: Visão geral dos componentes
description: Os componentes são unidades modulares que realizam funcionalidades específicas para apresentar conteúdo em seu site
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 66%

---

# Visão geral dos componentes {#components-overview}

Esta página fornece uma visão geral dos componentes do Adobe Experience Manager (AEM), como os [usados para criação de página](/help/sites-cloud/authoring/page-editor/components.md).

## O que são componentes? {#what-are-components}

* Unidades modulares que realizam funcionalidades específicas para apresentar conteúdo em seu site.
* Reutilizável.
* Desenvolvidos como unidades independentes em uma pasta do repositório.
* Não contêm arquivos de configuração ocultos.
* Eles podem conter outros componentes.
* Eles podem ser executados em qualquer lugar em qualquer sistema da AEM e também podem ser limitados a componentes específicos.
* Têm uma interface de usuário padronizada.
* Têm um comportamento de edição que pode ser configurado.
* Use caixas de diálogo que são criadas usando subelementos com base em componentes do Granite UI.
* Eles são desenvolvidos usando o [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR).
* Eles podem ser desenvolvidos para criar componentes personalizados que estendam a funcionalidade padrão.

Como os componentes são modulares, você pode:

* Desenvolver um novo componente na instância local.
* Implantá-los no ambiente de teste.
* Implantá-los no ambiente de criação ativo, onde eles permitem que autores e/ou administradores adicionem e configurem conteúdo.
* Implante-o em seus ambientes de publicação em tempo real, onde eles são usados para renderizar conteúdo para os visitantes do seu site.

Cada componente do AEM:

* É um tipo de recurso.
* É uma coleção de scripts que executa completamente uma função específica.
* Pode funcionar isoladamente, ou seja, dentro do AEM ou de um portal.

## Componentes principais do AEM {#aem-core-components}

[Os Componentes principais do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) são um conjunto de componentes padronizados de Gerenciamento de Conteúdo Online (WCM, Web Content Management) para que o AEM acelere o tempo de desenvolvimento e reduza o custo de manutenção de seus sites.

Os Componentes principais são fornecidos com o AEM as a Cloud Service, e o [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) ilustra como implementar e usar esses componentes. Os componentes são fornecidos com todos os códigos-fonte e podem ser usados como estão ou como pontos de partida para componentes modificados ou estendidos.

### Visualização de componentes disponíveis {#viewing-available-components}

Para obter uma visão geral de todos os componentes disponíveis na sua instância do AEM, use o [Console de Componentes](/help/sites-cloud/authoring/components-console.md).

Como alternativa, você também pode usar o CRXDE Lite para obter uma lista de todos os componentes disponíveis no repositório.

1. No **[!UICONTROL CRXDE Lite]**, clique em **[!UICONTROL Ferramentas]** na barra de ferramentas e, em seguida, em **[!UICONTROL Consulta]** para abrir a guia **[!UICONTROL Consulta]**.

1. Na guia **[!UICONTROL Consulta]**, selecione `XPath` como **[!UICONTROL Tipo]**.

1. No campo de entrada **[!UICONTROL Consulta]**, digite a seguinte cadeia de caracteres:

   `//element(*, cq:Component)`

1. Clique em **[!UICONTROL Executar]** e os componentes serão listados.
