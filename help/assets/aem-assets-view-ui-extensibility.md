---
title: Extensibilidade da interface de usuário do AEM Assets View
description: Saiba mais sobre o recurso Extensibilidade da interface do usuário do AEM Assets View. A interface do usuário do AEM Assets View permite adicionar componentes de interface do usuário personalizados para atender a necessidades comerciais específicas.
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: bbb183470e12c0fc81c821fc2e0c1e7d77c33707
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Extensibilidade da interface de usuário do AEM Assets View{#AEM-Assets-View-UI-Extensibility}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

O AEM Assets View tem o recurso Extensibilidade da interface do usuário. Esse recurso permite que os usuários adicionem componentes personalizados da interface do usuário à interface do Assets View para atender a necessidades comerciais específicas que as funcionalidades prontas para uso da AEM Assets View não atendem. Esse recurso de extensibilidade melhora a flexibilidade do AEM Assets View, permitindo que as organizações adaptem a interface a workflows e requisitos específicos.
Você pode adicionar suas extensões no nível do ativo, pasta e coleção. A extensão adicionada é exibida em um painel dedicado na página Ativo, Coleção ou Detalhes da pasta.

>[!IMPORTANT]
>
> * A Extensibilidade da Interface de Exibição do AEM Assets está disponível com o [Assets Ultimate](/help/assets/assets-ultimate-overview.md).
> * Para obter acesso à extensibilidade da interface de exibição do Assets, [crie e envie um caso de Suporte ao Cliente do Adobe](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).
> * Você pode fornecer feedback sobre a documentação, expandindo as opções de Feedback detalhado e clicando em Relatar um problema.

## <a id="1"></a> Como acessar o Assets View

Acesse a visualização do Assets das seguintes maneiras:
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## Onde as extensões da interface do usuário são exibidas na interface do usuário do Assets View? {#ui-extensibility-panel-assets-view}

Na Exibição do Assets, navegue até a página Detalhes de um ativo, pasta ou coleção. Essa página Detalhes tem um painel dedicado que exibe a Extensão da interface do usuário adicionada.
![meu espaço de trabalho](/help/assets/assets/my-workspace-assets-view3.png)


## Pré-requisitos para adicionar o componente de extensibilidade

* [Acesso ao Assets View](#1).
* Acesso ao [Adobe app builder](https://developer.adobe.com/app-builder/docs/overview/).
* Qualificado para Desenvolvedor da função de Administrador do Sistema na Organização. Consulte [this](https://developer.adobe.com/uix/docs/guides/get-access/) para obter mais informações.
* A Adobe IO Command Line Tool (AIO CLI) deve ser instalada em seus computadores locais. Essa ferramenta é essencial para criar e implantar projetos de extensão. Consulte [this](https://developer.adobe.com/app-builder/docs/getting_started/#local-environment-set-up) para obter mais informações.
* Boa compreensão das tecnologias JavaScript, Node.js e React.

## Adição do componente de Extensibilidade da interface no Assets View UI{#Adding-UI-Extensibility-Component-on-Assets-View}

1. Consulte [Introdução](https://developer.adobe.com/uix/docs/getting-started/) para obter informações essenciais sobre extensões da interface do usuário e a estrutura do Adobe App Builder. Saiba como a Extensibilidade da interface permite a integração de lógica e interface personalizadas nos serviços da Adobe Experience Cloud e entenda a arquitetura e o fluxo de trabalho para implementar extensões de interface.
1. Consulte [Guias](https://developer.adobe.com/uix/docs/guides/) para obter informações gerais sobre extensibilidade da interface do usuário, incluindo configuração de ambiente local, visualização local, publicação e gerenciamento.
1. Consulte [Conceitos Comuns na Criação de Extensões](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/) para entender os fundamentos necessários ao desenvolvimento de uma extensão de interface do usuário para a Exibição do AEM Assets.
1. Adicionar painéis laterais personalizados à interface de Exibição do Assets. O aplicativo host (Assets View) gerencia esses painéis para lidar com interações da interface do usuário, como alternância e deep linking. As extensões usam o ponto de extensão `aem/assets/details/1` para integrar painéis personalizados que especificam propriedades, como ID de painel, título e URL de conteúdo. Os desenvolvedores registram painéis personalizados com o método `getPanels()` e criam rotas para exibir conteúdo personalizado. Para obter implementação detalhada, incluindo referências de API e exemplos de código, consulte [Exibição de Detalhes](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/).
1. Configure seu ambiente local e experimente o processo de desenvolvimento de extensões de interface do usuário na visualização do Assets em primeira mão, criando sua primeira extensão de interface do usuário. Consulte [Exibir Desenvolvimento de Extensão passo a passo do AEM Assets](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/) para obter mais detalhes.
1. Configure seu aplicativo usando a CLI da AIO para gerar a estrutura básica de extensão e o código necessário. Consulte [Geração de código para o AEM Assets View](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/) para obter informações detalhadas.
1. Teste suas extensões localmente para garantir que elas funcionem conforme o esperado antes da implantação. Execute sua extensão em um ambiente totalmente isolado ou com isolamento parcial e conecte sua extensão ao AEM Assets View de produção para teste. Consulte [Solução de problemas - Extensibilidade de exibição do AEM Assets](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/) para obter informações detalhadas.
