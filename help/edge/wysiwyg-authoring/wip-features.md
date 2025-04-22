---
title: Recursos de sites de trabalho em andamento para o Edge Delivery Services
description: Saiba quais recursos e casos de uso do AEM Sites estão em andamento e descubra soluções alternativas ao usar o Edge Delivery Services.
solution: Experience Manager Sites
feature: Edge Delivery Services
role: User
exl-id: 21745f53-a7ef-4eec-9170-b267c2f4314e
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# Recursos de sites de trabalho em andamento para o Edge Delivery Services {#wip-sites-features}

Saiba quais recursos e casos de uso do AEM Sites estão em andamento e descubra soluções alternativas ao usar o Edge Delivery Services.

>[!TIP]
>
>Trabalho em andamento não significa o fim do caminho. Se você precisar de um recurso ou caso de uso listado como trabalho em andamento neste documento, entre em contato com o representante da Adobe. Você e a Adobe podem trabalhar juntos para entender suas necessidades específicas e encontrar soluções alternativas.

## Recursos do trabalho em andamento {#wip-features}

Ao usar o Edge Delivery Services com o AEM Sites, a maioria dos recursos do Sites está disponível. Por exemplo, quase todas as ações disponíveis no [Console de sites](/help/sites-cloud/authoring/sites-console/introduction.md) se aplicam ao Edge Delivery Services.

No entanto, alguns recursos são um trabalho em andamento (WIP). Os recursos WIP são recursos do console Sites que ainda não estão disponíveis para o Edge Delivery Services com AEM Sites ou estão apenas parcialmente disponíveis. Por esse motivo, os recursos do WIP podem ser apresentados de forma diferente dos seus equivalentes do Sites ou podem haver soluções alternativas para o caso de uso.

A lista a seguir apresenta esses recursos WIP e soluções alternativas. Se o seu projeto exigir um recurso WIP, revise as alternativas sugeridas abaixo e entre em contato com a Adobe para trabalhar em conjunto e entender seu caso de uso.

| Recurso do Sites | Status no Edge | Notas | Documentação do Edge |
|---|---|---|---|
| [Herança de página](/help/sites-cloud/administering/msm-and-translation.md) | Disponível |  | [Herança de conteúdo no Editor Universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Herança de componente](/help/sites-cloud/administering/msm-and-translation.md) | Parcialmente Disponível | Os componentes herdam conteúdo, mas a herança só pode ser revertida no nível da página | [Herança de conteúdo no Editor Universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Cópia de idioma](/help/sites-cloud/administering/translation/overview.md) | Parcialmente disponível | Os componentes herdam conteúdo, mas a herança só pode ser revertida no nível da página | [Herança de conteúdo no Editor Universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Gerenciamento de vários sites](/help/sites-cloud/administering/msm/overview.md) | Parcialmente disponível | Os componentes herdam conteúdo, mas a herança só pode ser revertida no nível da página | [Herança de conteúdo no Editor Universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Lançamentos](/help/sites-cloud/authoring/launches/overview.md) | Parcialmente Disponível | Os componentes herdam conteúdo, mas a herança só pode ser revertida no nível da página | [Herança de conteúdo no Editor Universal](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [Modelos de páginas](/help/sites-cloud/authoring/page-editor/templates.md) | Parcialmente disponível | As páginas criadas a partir de modelos são cópias independentes do modelo original. | [Usando Modelos de Página com o Editor Universal](/help/sites-cloud/authoring/universal-editor/templates.md) |
| [Context Hub e Targeting](/help/sites-cloud/authoring/personalization/overview.md) | Não disponível |  |  |
| [Timewarp](/help/sites-cloud/authoring/launches/preview.md) | Não disponível |  |  |
| [Conteúdo associado](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#associated-content-browser) | Não disponível |  |  |
| [Fragmentos de experiência](/help/sites-cloud/authoring/fragments/experience-fragments.md) | Alternativa | Criar uma página e usar um componente de fragmento |  |

## Casos de uso de trabalho em andamento {#wip-use-cases}

Como o Edge Delivery Services é construído em uma pilha de tecnologia inteiramente nova e moderna, os seguintes casos de uso do AEM Sites ainda não são totalmente cobertos e estão em andamento. Se o seu projeto exigir um caso de uso de Trabalho em andamento, entre em contato com a Adobe para trabalhar em conjunto e entender as necessidades do seu projeto.

| Caso de uso de sites | Detalhes |
|---|---|
| Lógica do lado do servidor para renderizar páginas | Uso do tempo de execução do AEM como servidor de aplicativos |
| Páginas dinâmicas | SSI ou qualquer técnica de inclusão dinâmica |
| Gerenciamento de usuários | Uso do AEM como IdP |
| Autenticação | Utilização do AEM para conteúdo seguro |
| Permissão de conteúdo | AEM como extranet segura |
