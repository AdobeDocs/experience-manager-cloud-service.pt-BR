---
title: Utilização da extensão de referências externas do AJO de fragmentos de conteúdo
description: Saiba mais sobre a extensão de referências externas do AJO do fragmento de conteúdo
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
exl-id: 79c90e6b-91da-4f5a-ac96-a98ef7f8d4cd
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# A Extensão De Referências Externas Do AJO Do Fragmento De Conteúdo {#content-fragment-external-references-extension}

Para visualizar as experiências do AEM em outro produto da Adobe, é possível habilitar a extensão da interface do usuário:

* **Referências externas do AJO**

A extensão Referências externas do AJO funciona buscando referências ao fragmento de conteúdo de todas as organizações e sandboxes associadas a tags predefinidas. A extensão mostra detalhes.

Por exemplo, para uma integração com o Adobe Journey Optimizer (AJO), os detalhes dependem se a referência é uma Campanha, uma Jornada ou um Modelo.

>[!NOTE]
>
>Para obter detalhes sobre como habilitar a extensão, consulte [Extension Manager no AEM Experience Manager.](https://developer.adobe.com/uix/docs/extension-manager/)

Por exemplo, para usar a extensão com o AJO:

>[!NOTE]
>
>Consulte também [Integração com o AJO](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/integrations/aem-fragments).

1. Abra o [Console de Fragmentos de Conteúdo](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console).

1. Navegue até o fragmento de conteúdo — o fragmento que foi criado e usado em vários canais do AJO.

1. Abra o fragmento de conteúdo no [editor](/help/sites-cloud/administering/content-fragments/managing.md#editing-the-content-of-your-fragment).

1. A extensão Referências externas do AJO está disponível como uma guia no painel direito. Selecione a guia para abrir a extensão:

   ![Extensão de Referências Externas do AJO](/help/sites-cloud/administering/content-fragments/assets/cf-ajo-fragment-external-references-extension.png)

   Depois que um tipo de referência é selecionado, a extensão exibe as referências externas correspondentes como uma tabela com as colunas:

   * **Nome**: o nome da referência onde o fragmento de Conteúdo é usado
   * **Visualizar** selecione este link para iniciar a visualização
   * **Status**: o status da referência

1. Você pode selecionar o **Tipo de Referência** no menu suspenso para alternar entre três tipos de referência:

   * **Campanha**
      * Exibe uma lista de todas as campanhas com links para o fragmento de conteúdo atual.
      * Você pode pré-visualizar uma campanha selecionada.
      * Padrão
   * **Jornada**
      * Exibe a Jornada mais recente.
      * Em seguida, é possível selecionar e visualizar uma Jornada selecionada.
   * **Modelo**
      * Exibe modelos relacionados ao fragmento de conteúdo.
      * Em seguida, é possível selecionar e visualizar um modelo selecionado.
