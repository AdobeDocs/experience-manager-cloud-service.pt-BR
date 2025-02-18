---
title: Extensão do Universal Editor
description: Saiba mais sobre as diferentes opções para estender os recursos do Universal Editor para atender às necessidades dos autores de conteúdo.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0cab4a807be4aa402667feddb6a948f0d2db371f
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# Extensão do Universal Editor {#extending}

Saiba mais sobre as diferentes opções para estender os recursos do Universal Editor para atender às necessidades dos autores de conteúdo.

>[!TIP]
>
>O Editor Universal também oferece várias [opções de personalização](/help/implementing/universal-editor/customizing.md), permitindo que você atenda melhor às suas necessidades de projeto.

## Extensões  {#extensions}

Como um serviço do Adobe Experience Cloud, a interface do usuário do Editor universal pode ser estendida usando o App Builder e o Experience Manager. O Adobe oferece muitas extensões prontas que você pode usar para o seu projeto.

* **[Seletor de produto do AEM para Universal Editor](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**: integre dados do Adobe Commerce selecionando ou removendo dados do produto do editor.
* **[Rascunhos de Conteúdo do Editor Universal](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**: crie, edite e gerencie vários rascunhos de conteúdo.
* **[Seletor de ativos configuráveis](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**: habilitar a seleção de ativos de repositórios diferentes daquele usado pela página editada.
* **Editor de regras do Forms**: adicionar comportamento dinâmico a campos do AEM Forms visualmente, sem codificação.
* **[Exportar fragmentos de conteúdo para o Adobe Target](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**: exportar fragmentos de conteúdo criados no Adobe Experience Manager as a Cloud Service para o Adobe Target para serem usados como ofertas em atividades do Target, para testar e personalizar experiências em escala.
* **[Fluxos de trabalho de fragmento de conteúdo](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**: inicie um fluxo de trabalho do AEM para fragmentos de conteúdo selecionados.

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

* **[Blocos](/help/edge/developer/block-collection.md)**: no formato JSON simples, os projetos podem ajustar os blocos e os recursos UE disponíveis para criação de conteúdo.
* **[Interface do Usuário Personalizada](#extending-ui)**: as extensões podem exibir a interface do usuário necessária em painéis laterais ou caixas de diálogo modais.
* **[Eventos](/help/implementing/universal-editor/events.md)**: as extensões recebem eventos sobre as ações e seleções do autor na página para responder adequadamente.
