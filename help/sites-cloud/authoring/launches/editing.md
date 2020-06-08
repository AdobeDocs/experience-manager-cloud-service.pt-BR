---
title: Edição de lançamentos
description: 'Depois de criar um lançamento para a sua página (ou conjunto de páginas), você pode editar o conteúdo na cópia de lançamento da(s) página(s). '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 93%

---


# Edição de lançamentos {#editing-launches}

## Edição de páginas de lançamento {#editing-launch-pages}

Quando um lançamento foi criado para uma página (ou um conjunto de páginas), é possível editar o conteúdo na cópia de lançamento da(s) página(s).

1. Acesse [Lançamento a partir de Referências (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar as ações disponíveis.
1. Selecione **Vá para a página** para abrir a página para edição.

### Edição de páginas de lançamento sujeitas a uma live copy {#editing-launch-pages-subject-to-a-live-copy}

Se o seu lançamento se basear em uma live copy, você: <!--If your launch is based upon a [live copy](/help/sites-administering/msm.md) then you will:-->

* Consulte Bloquear símbolos (pequenos cadeados) ao editar um componente (conteúdo e/ou propriedades).
* See the **Live Copy** tab in **Page Properties**

Uma livecopy é usada para sincronizar o conteúdo da *ramificação de origem* para a *ramificação de inicialização* (para manter a inicialização atualizada com as alterações feitas na origem).

Você pode fazer alterações da mesma forma como pode editar uma live copy padrão, por exemplo:

* Clicar em um cadeado fechado interromperá essa sincronização e permitirá que você faça novas atualizações no conteúdo do seu lançamento. Após o desbloqueio (cadeado aberto), suas alterações não serão substituídas por quaisquer alterações feitas no mesmo local na ramificação de origem.
* **Suspender** (e **Retomar**) herança de uma página específica.

Consulte Alteração do conteúdo da live copy para obter mais informações. <!--See [Changing Live Copy Content](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) for further information.-->

## Comparação de uma página de lançamento com sua página de origem {#comparing-a-launch-page-to-its-source-page}

Para rastrear as alterações feitas, é possível exibir a inicialização em **Referências** e comparar a página de inicialização com a página de origem:

1. No console **Sites**, [navegue até a página de origem do seu lançamento e selecione-a](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra o painel **[Referências](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)**e selecione **Lançamentos**.
1. Selecione seu lançamento específico e depois **Comparar com a origem**:

   ![Comparação entre inicialização e origem](/help/sites-cloud/authoring/assets/launches-compare.png)

1. As duas páginas (lançamento e origem) serão abertas lado a lado.

   Para obter informações completas sobre como usar esse recurso, consulte [Diferencial de página](/help/sites-cloud/authoring/features/page-diff.md).

## Alteração nas páginas de origem usadas {#changing-the-source-pages-used}

A qualquer momento, você pode adicionar ou remover páginas ao/do intervalo de páginas de origem para um lançamento:

1. Acesse e selecione o lançamento a partir do seguinte:
   * The [Launches console](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Selecione **Editar**.
   * [Referências (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar as ações disponíveis:
      * Selecione **Editar lançamento**.
      * As páginas de origem serão mostradas.
1. Faça as alterações necessárias e confirme com **Salvar**.

>[!NOTE]
>
>Para adicionar páginas a um lançamento, elas devem estar abaixo de uma raiz de linguagem comum, isto é, dentro de um único site.

## Edição de configuração de lançamento {#editing-a-launch-configuration}

A qualquer momento, você pode editar as propriedades de um lançamento:

1. Acesse e selecione o lançamento a partir do seguinte:
   * o [console Lançamentos](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Selecione **Propriedades**.
   * [Referências (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar as ações disponíveis:
      * Selecione **Editar propriedades**.
      * Os detalhes serão mostrados.
1. Faça as alterações necessárias e confirme com **Salvar**.
   * Consulte [Lançamentos - a ordem de eventos](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) para obter informações sobre o propósito e a interação dos campos **Data de lançamento** e **Pronto para produção**.

## Descoberta do status de lançamento de uma página {#discovering-the-launch-status-of-a-page}

O status é mostrado quando você seleciona um lançamento específico na guia Referências (consulte [Lançamentos em Referências (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)).

![Descobrindo status de inicialização](/help/sites-cloud/authoring/assets/launches-status.png)
