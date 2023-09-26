---
title: Visão geral dos componentes
description: Os componentes são unidades modulares que realizam funcionalidades específicas para apresentar conteúdo em seu site
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 67%

---

# Visão geral dos componentes {#components-overview}

Esta página fornece uma visão geral dos componentes do Adobe Experience Manager (AEM), como os [usados para criação de página](/help/sites-cloud/authoring/fundamentals/components.md).

## O que são componentes? {#what-are-components}

* Unidades modulares que realizam funcionalidades específicas para apresentar conteúdo em seu site.
* Reutilizável.
* Desenvolvidos como unidades independentes em uma pasta do repositório.
* Não contêm arquivos de configuração ocultos.
* Eles podem conter outros componentes.
* Eles podem ser executados em qualquer lugar dentro de qualquer sistema AEM e também podem ser limitados a ser executados em componentes específicos.
* Têm uma interface de usuário padronizada.
* Têm um comportamento de edição que pode ser configurado.
* Use caixas de diálogo que são criadas usando subelementos com base em componentes do Granite UI.
* Eles são desenvolvidos usando [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR).
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

[Os componentes principais do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) são um conjunto de componentes padronizados de Gerenciamento de Conteúdo na Web (WCM, na sigla em inglês) para o AEM a fim de acelerar o tempo de desenvolvimento e reduzir o custo de manutenção de seus sites.

Os Componentes principais são fornecidos com o AEM as a Cloud Service, e o [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) ilustra como implementar e usar esses componentes. Os componentes são fornecidos com todos os códigos-fonte e podem ser usados como estão ou como pontos de partida para componentes modificados ou estendidos.

### Visualização de componentes disponíveis {#viewing-available-components}

Para obter uma visão geral de todos os componentes disponíveis na instância do AEM, use o [Console de componentes](/help/sites-cloud/authoring/features/components-console.md).

Como alternativa, você também pode usar o CRXDE Lite para obter uma lista de todos os componentes disponíveis no repositório.

1. No **[!UICONTROL CRXDE Lite]**, clique em **[!UICONTROL Ferramentas]** na barra de ferramentas e, em seguida, em **[!UICONTROL Consulta]** para abrir a guia **[!UICONTROL Consulta]**.

1. Na guia **[!UICONTROL Consulta]**, selecione `XPath` como **[!UICONTROL Tipo]**.

1. No **[!UICONTROL Query]** insira a seguinte string:

   `//element(*, cq:Component)`

1. Clique em **[!UICONTROL Executar]** e os componentes serão listados.
