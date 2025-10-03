---
title: Visualização de fragmentos de conteúdo
description: Entenda como visualizar seus fragmentos de conteúdo por uma variedade de métodos.
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
source-git-commit: 3781b494394405f69892686790c17ffa9c69f28b
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---

# Visualização de fragmentos de conteúdo {#previewing-content-fragments}

Os fragmentos de conteúdo podem ser usados para entrega headless e criação de página. Como os fragmentos são apenas conteúdo, sem formatação, revisá-los pode ser mais desafiador. Portanto, vários métodos de visualização dos fragmentos, em uma variedade de cenários, são fornecidos.

Há vários métodos disponíveis para Fragmentos de conteúdo, acessíveis no console de Fragmentos do console e no editor. O console e o editor descritos nesta seção foram desenvolvidos para entrega de conteúdo headless (embora possam ser usados para todos os cenários).

Você pode visualizar o fragmento:

* usando o [padrão de Visualização de URL](#preview-url-pattern)

* publicando e cancelando a publicação na [instância de Visualização](#preview-instance)

<!--
* with a HTML template, using **[Preview]()** from the Content Fragments console
-->

É claro que você também pode visualizar seu fragmento no [editor de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md).

>[!IMPORTANT]
>
>Os fragmentos de conteúdo podem ser acessados de dois consoles: **Fragmentos de conteúdo** e **Assets**.
>
>Também há dois editores para a criação de fragmentos de conteúdo; embora a funcionalidade básica seja a mesma, há algumas diferenças. Ambos os editores podem ser acessados em ambos os consoles.
>
>Esta seção trata do console de **Fragmentos de conteúdo** e do editor de Fragmento de conteúdo *new*. Eles foram desenvolvidos para entrega de conteúdo headless (embora possam ser usados para todos os cenários)
>
>Para obter mais informações, consulte:
>
>* uso do console **Assets** para [gerenciar fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md)
>* uso do [*original* editor de Fragmento de Conteúdo](/help/assets/content-fragments/content-fragments-variations.md),
>* usando [Fragmentos de conteúdo para a criação de páginas](/help/sites-cloud/authoring/fragments/content-fragments.md).

## Padrão de URL de visualização {#preview-url-pattern}

O editor de fragmento de conteúdo fornece aos autores a opção de visualizar suas edições em um aplicativo de front-end externo.

Para usar esse recurso, primeiro é necessário:

* Trabalhe com sua equipe de TI para configurar o aplicativo de front-end externo que renderizará o fragmento de conteúdo consumindo sua saída JSON.

* Quando o aplicativo de front-end externo está configurado, o **Padrão de URL de Visualização Padrão** deve ser definido como uma propriedade [do Modelo de Fragmento de Conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#model-properties) apropriado.

O URL de visualização deve seguir este padrão:

    `https://<preview_url>?param=${expression}`

As expressões disponíveis são:

* `${contentFragment.path}`
* `${contentFragment.model.path}`
* `${contentFragment.model.name}`
* `${contentFragment.variation}`
* `${contentFragment.id}`

Quando a URL tiver sido definida, o botão **[Visualizar](/help/sites-cloud/administering/content-fragments/authoring.md#preview-content-fragment)** ficará ativo na barra de ferramentas superior do editor. Você pode selecionar esse botão para iniciar o aplicativo externo (em uma guia separada) para renderizar o fragmento de conteúdo.

## Visualizar instância {#preview-instance}

Você pode **Publicar** e **Cancelar publicação**, seu fragmento no **[Serviço de visualização](/help/headless/deployment/architecture.md)** (bem como na instância de Publicação).

Você pode publicar o fragmento no editor ou no console.

Consulte:

* [Publicação e visualização de um fragmento](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment) para obter detalhes completos.

* [Desfazer a publicação de um fragmento](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment) para obter detalhes completos.

<!--
## Preview based on a HTML Template {#preview-based-on-a-html-template}

The Content Fragment console provides a **Preview** option for every fragment.

The icon can be selected to open a dialog that represents the fragment based on a HTML template. You can use the default template, or develop and load your own.
-->
