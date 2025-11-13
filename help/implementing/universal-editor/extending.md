---
title: Extensão do Universal Editor
description: Saiba mais sobre as diferentes opções para estender os recursos do Universal Editor para atender às necessidades dos autores de conteúdo.
feature: Developing
role: Admin, Developer
exl-id: 2f487fa5-57a7-477a-ad68-590e6cc12f4e
source-git-commit: d938abce2b46786343b19113454da1738a824ed0
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Extensão do Universal Editor {#extending}

Saiba mais sobre as diferentes opções para estender os recursos do Universal Editor para atender às necessidades dos autores de conteúdo.

>[!TIP]
>
>O Editor Universal também oferece várias [opções de personalização](/help/implementing/universal-editor/customizing.md), permitindo que você atenda melhor às suas necessidades de projeto.

## Extensões  {#extensions}

Como um serviço do Adobe Experience Cloud, a interface do usuário do Editor universal pode ser estendida usando o App Builder e o Experience Manager. A Adobe oferece muitas extensões prontas disponíveis por meio da [Extension Manager](https://experience.adobe.com/aem/extension-manager) que você pode usar para o seu projeto.

* **[Extensão MSM (Gerenciamento de Vários Sites) do AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)**: Interromper ou restabelecer a herança no nível do componente
* **[Extensão de Propriedades de Página do AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#page-properties)**: acessar a janela de propriedades de página da página no Editor Universal
* **[Extensão do Administrador do Site do AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#sites-console)**: abra o Console Sites no local da página no Editor Universal
* **[Extensão de Bloqueio de Página do AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#locking-pages)**: exibir e alterar o status de bloqueio de página do Editor Universal
* **[Extensão de Fluxos de Trabalho do AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#workflows)**: iniciar fluxos de trabalho na página e conteúdo da página do Editor Universal
* **[Gerar variações](/help/generative-ai/generate-variations-integrated-editor.md)**: use a inteligência artificial (AI) geradora para criar variações para o seu conteúdo diretamente no painel de propriedades.
* **[Seletor de produto do AEM para Universal Editor](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**: integre dados do Adobe Commerce selecionando ou removendo dados do produto do editor.
* **[Rascunhos de Conteúdo do Editor Universal](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**: crie, edite e gerencie vários rascunhos de conteúdo.
* **[Seletor de ativos configuráveis](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**: habilitar a seleção de ativos de repositórios diferentes daquele usado pela página editada.
* **Editor de regras do Forms**: adicionar comportamento dinâmico a campos do AEM Forms visualmente, sem codificação.
* **[Exportar fragmentos de conteúdo para o Adobe Target](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**: exportar fragmentos de conteúdo criados no Adobe Experience Manager as a Cloud Service para o Adobe Target para serem usados como ofertas em atividades do Target, para testar e personalizar experiências em escala.
* **[Fluxos de trabalho de fragmento de conteúdo](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**: inicie um fluxo de trabalho do AEM para fragmentos de conteúdo selecionados.

Para obter informações sobre como habilitar essas extensões, [consulte a documentação do Extension Manager.](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)

## Extensão da interface {#extending-ui}

As extensões da interface do usuário do Universal Editor são aplicativos do JavaScript criados com o Adobe App Builder. Usando essas mesmas ferramentas, você também pode adicionar seus próprios botões e ações ao menu de cabeçalho e ao painel de propriedades, bem como criar seus próprios eventos para o Editor universal.

Se quiser explorar as possibilidades de criar suas próprias extensões, consulte os seguintes recursos:

1. [Extensibilidade da Interface do Usuário](https://developer.adobe.com/uix/docs/) - Esta é a documentação do desenvolvedor para a extensão da Interface do Usuário.
1. [Guias de Extensibilidade da Interface do Usuário](https://developer.adobe.com/uix/docs/guides/) - Instruções detalhadas sobre como desenvolver sua própria extensão
1. [Os Pontos de Extensão da Interface do Usuário do Editor Universal](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - Documentação de pontos de extensão específicos do Editor Universal

>[!TIP]
>
>Se preferir aprender por exemplo, consulte o [tutorial de extensibilidade da interface do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview). Embora se concentre na extensão do console de Fragmentos de conteúdo, os conceitos para implementar uma extensão de interface no Editor universal são os mesmos.

[Usando o Extension Manager no AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/), você pode habilitar ou desabilitar suas extensões por instância, acessar extensões primárias do Adobe, inclusive as do Universal Editor, e muito mais.

## Pontos de extensão {#extension-points}

Além da extensibilidade da interface do usuário, o Universal Editor oferece muitos outros pontos de extensão flexíveis para permitir a integração perfeita de requisitos comerciais personalizados.

* **[Blocos](https://www.aem.live/developer/block-collection)**: no formato JSON simples, os projetos podem ajustar os blocos e os recursos UE disponíveis para criação de conteúdo.
* **[Interface do Usuário Personalizada](#extending-ui)**: as extensões podem exibir a interface do usuário necessária em painéis laterais ou caixas de diálogo modais.
* **[Eventos](/help/implementing/universal-editor/events.md)**: as extensões recebem eventos sobre as ações e seleções do autor na página para responder adequadamente.
