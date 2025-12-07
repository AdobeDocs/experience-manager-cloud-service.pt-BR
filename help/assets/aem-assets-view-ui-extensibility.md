---
title: Habilitar extensibilidade da interface do usuário em  [!DNL AEM Assets View]
description: Saiba mais sobre o recurso de Extensibilidade da Interface do Usuário do  [!DNL AEM Assets View]. [!DNL AEM Assets View] A interface do usuário permite adicionar componentes de interface do usuário personalizados para atender a necessidades comerciais específicas.
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Habilitar extensibilidade da interface do usuário em [!DNL AEM Assets View] {#AEM-Assets-View-UI-Extensibility}

O [!DNL AEM Assets View] oferece suporte à extensibilidade da interface do usuário, permitindo que você adicione componentes da interface do usuário personalizada à sua interface do usuário [!DNL Assets View] para fluxos de trabalho específicos e requisitos comerciais que não são atendidos pelos recursos prontos para uso do [!DNL AEM Assets View]. Esse recurso de extensibilidade de interface do usuário do [!DNL AEM Assets View] aumenta sua flexibilidade, permitindo que as organizações adaptem a interface a fluxos de trabalho e requisitos específicos.\
Você pode adicionar suas extensões no nível do **Ativo**, **Pasta** e **Coleção**. A extensão adicionada é exibida em um painel dedicado na página **Ativo**, **Coleção** ou **Pasta** **[!UICONTROL Detalhes]**.

>[!IMPORTANT]
>
> * A extensibilidade da interface do usuário [!DNL AEM Assets View] está disponível com [[!DNL Assets Ultimate]](/help/assets/assets-ultimate-overview.md).
> * Para obter acesso à extensibilidade da interface do usuário do [!DNL Assets view], [crie e envie um [!DNL Adobe] caso de Suporte ao Cliente](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).
> * Você pode fornecer comentários sobre a documentação, expandindo as **[!UICONTROL Opções de Comentários Detalhados]** e clicando em **[!UICONTROL Relatar um problema]**.

## <a id="1"></a> Acessar a Exibição do Assets{#add-UI-Extensibility-in-AEM-Assets-View}

Siga as etapas mencionadas na imagem abaixo para acessar o [!DNL Assets View]:
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## Exibir extensões da interface do usuário em [!DNL Assets View] {#ui-extensibility-panel-assets-view}

Em [!DNL Assets View], navegue até a página **[!UICONTROL Detalhes]** de um ativo, pasta ou coleção. A página **[!UICONTROL Detalhes]** exibe a extensão de interface do usuário adicionada em um painel dedicado.
![meu espaço de trabalho](/help/assets/assets/my-workspace-assets-view3.png)

## Pré-requisitos para adicionar o componente de extensibilidade{#assets-view-ui-extensibility}

Atenda aos seguintes requisitos para começar a adicionar o componente de extensibilidade em seu [!DNL Assets View UI]:

* [Acesso a [!DNL Assets View]](#1).
* Acesso a [[!DNL Adobe app builder]](https://developer.adobe.com/app-builder/docs/overview/).
* Direito ao desenvolvedor da função de administrador do sistema na organização. Consulte [esta documentação](https://developer.adobe.com/uix/docs/guides/get-access/) para obter mais informações.
* [!DNL Adobe IO command line tool (AIO CLI)] está instalado em seus computadores locais. Essa ferramenta é essencial para criar e implantar projetos de extensão. Consulte [Criar o Primeiro Aplicativo App Builder](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app#local-environment-set-up) (requer autenticação para acesso) para obter mais informações.
* Boa compreensão das tecnologias do [!DNL JavaScript], [!DNL Node.js] e [!DNL React].

## Adicionar o componente de extensibilidade da interface do usuário a [!DNL Assets View] {#ui-extensibility-in-assets-view}

1. Consulte [Introdução](https://developer.adobe.com/uix/docs/getting-started/) para obter informações essenciais sobre extensões da interface do usuário e a estrutura [!DNL Adobe App Builder]. Saiba como a Extensibilidade da Interface do Usuário permite a integração da lógica personalizada e da interface do usuário no [!DNL Adobe Experience Cloud services] e entenda a arquitetura e o fluxo de trabalho para implementar Extensões de Interface do Usuário.
1. Consulte [Guias](https://developer.adobe.com/uix/docs/guides/) para obter informações gerais sobre extensibilidade da interface do usuário, incluindo configuração de ambiente local, visualização local, publicação e gerenciamento.
1. Consulte [Conceitos comuns na criação de extensões](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/) para entender os fundamentos necessários ao desenvolvimento de uma extensão de interface do usuário para o [!DNL AEM Assets View].
1. Adicionar painéis laterais personalizados à interface [!DNL Assets View]. O aplicativo host ([!DNL Assets View]) gerencia esses painéis para lidar com interações da interface do usuário, como alternância e deep linking. As extensões usam o ponto de extensão `aem/assets/details/1` para integrar painéis personalizados que especificam propriedades, como ID de painel, título e URL de conteúdo. Os desenvolvedores registram painéis personalizados com o método `getPanels()` e criam rotas para exibir conteúdo personalizado. Para obter implementação detalhada, incluindo referências de API e exemplos de código, consulte [Exibição de Detalhes](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/).
1. Configure seu ambiente local e crie sua primeira extensão de interface do usuário para ter uma experiência direta do processo de desenvolvimento de extensões de interface do usuário no [!DNL Assets View]. Consulte [Exibir Desenvolvimento de Extensão passo a passo do AEM Assets](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/) para obter mais detalhes.
1. Configure seu aplicativo usando a CLI da AIO para gerar a estrutura básica de extensão e o código necessário. Consulte [geração de código para [!DNL AEM Assets View]](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/) para obter informações detalhadas.
1. Teste suas extensões localmente para garantir que elas funcionem conforme o esperado antes da implantação. Execute sua extensão em um ambiente totalmente isolado ou com isolamento parcial e conecte sua extensão à produção [!DNL AEM Assets View] para teste. Consulte [Solução de problemas - [!DNL AEM Assets View] extensibilidade](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/) para obter informações detalhadas.

## Personalizar ações na exibição do Assets {#customize-actions-assets-view}

A visualização AEM Assets permite personalizar as seguintes ações na visualização Procurar:

* Personalize as ações exibidas ao selecionar um ou mais ativos na Barra de ações.

* Personalize as ações exibidas ao clicar em Mais opções (...) no cartão de ativos.

* Personalize as ações disponíveis no menu Cabeçalho.

Para obter mais informações, consulte [Exibição de Navegação](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/browse-view/).

## Abrir caixas de diálogo personalizadas na exibição do Assets {#open-custom-dialogs-assets-view}

A visualização Assets também permite abrir caixas de diálogo personalizadas com texto de sua escolha. Também é possível adicionar links ao texto. Para obter mais informações, consulte [API modal](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/#modal-api).
