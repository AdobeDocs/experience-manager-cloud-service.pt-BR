---
title: Edição de inicializações
description: Depois de criar uma inicialização para sua página (ou conjunto de páginas), você pode editar o conteúdo na cópia de inicialização da(s) página(s).
exl-id: d3cd3383-e0a0-4019-9f97-8baa3be99e6e
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 52%

---

# Edição de inicializações {#editing-launches}

## Editar páginas de lançamento {#editing-launch-pages}

Quando uma inicialização é criada para uma página (ou conjunto de páginas), é possível editar o conteúdo na cópia de inicialização da(s) página(s).

1. Acesse [Inicialização a partir de Referências (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar as ações disponíveis.
1. Selecionar **Ir para a página** para abrir a página para edição.

Ao editar a página, você verá uma indicação na barra de ferramentas superior, juntamente com as opções **Sair** e **Navegar**:

![Sair e navegar lançamento no editor de páginas](/help/sites-cloud/authoring/assets/launches-edit-01.png)

>[!NOTE]
>
>Você não tem permissão para mover uma página em um lançamento. Tentar esta ação acionará uma mensagem de aviso:
>
>* Aviso: esta página é a origem de um lançamento. Não é permitido mover a página.

### Edição de páginas de lançamento sujeitas a uma live copy {#editing-launch-pages-subject-to-a-live-copy}

Se o seu lançamento se basear em uma [Live Copy](/help/sites-cloud/administering/msm/overview.md), você:

* Verá símbolos de bloqueio (pequenos cadeados) ao editar um componente (conteúdo e/ou propriedades).
* Verá a guia **Live Copy** nas **Propriedades da página**

Uma livecopy é usada para sincronizar o conteúdo da *ramificação de origem* para a *ramificação de inicialização* (para manter a inicialização atualizada com as alterações feitas na origem).

É possível fazer alterações da mesma maneira que editar uma live copy padrão; por exemplo:

* Clicar em um cadeado fechado interromperá essa sincronização e permitirá que você faça novas atualizações no conteúdo em sua inicialização. Uma vez desbloqueadas (cadeado aberto) suas alterações não serão substituídas por quaisquer alterações feitas no mesmo local dentro da ramificação de origem.
* **Suspender** (e **Retomar**) herança de uma página específica.

Consulte [Alterar conteúdo da Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md) para obter mais informações.

## Comparação de uma página de lançamento à sua página de origem {#comparing-a-launch-page-to-its-source-page}

Para rastrear as alterações feitas, é possível exibir a inicialização em **Referências** e comparar a página de inicialização com a página de origem:

1. No console **Sites**, [navegue até a página de origem do seu lançamento e selecione-a](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra o **[Referências](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** e selecione **Lançamentos**.
1. Selecione o lançamento específico e **Comparar à origem**:

   ![Comparação do lançamento com a origem](/help/sites-cloud/authoring/assets/launches-compare.png)

1. As duas páginas (inicialização e origem) serão abertas lado a lado.

   Para obter informações completas sobre como usar esse recurso, consulte [Diferença de página](/help/sites-cloud/authoring/features/page-diff.md).

## Alteração das páginas de origem usadas {#changing-the-source-pages-used}

A qualquer momento, você pode adicionar ou remover páginas ao/do intervalo de páginas de origem para um lançamento:

1. Acesse e selecione o lançamento a partir do seguinte:
   * O [console Lançamentos](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Selecione **Editar**.
   * [Referências (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar as ações disponíveis:
      * Selecione **Editar lançamento**.
      * As páginas de origem são exibidas.
1. Faça as alterações necessárias e confirme com **Salvar**.

>[!NOTE]
>
>Para adicionar páginas a um lançamento, elas devem estar abaixo de uma raiz de idioma comum, ou seja, em um único site.

## Editar uma configuração de inicialização {#editing-a-launch-configuration}

A qualquer momento, você pode editar as propriedades de um lançamento:

1. Acesse e selecione o lançamento a partir do seguinte:
   * o [Iniciar console](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Selecionar **Propriedades**.
   * [Referências (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar as ações disponíveis:
      * Selecione **Editar propriedades**.
      * Os detalhes são mostrados.
1. Faça as alterações necessárias e confirme com **Salvar**.
   * Consulte [Inicializações - a Ordem dos eventos](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) para obter informações sobre a finalidade e interação dos campos **Data de inicialização** e **Pronto para produção**.

## Descobrir o status de lançamento de uma página {#discovering-the-launch-status-of-a-page}

O status é exibido ao selecionar uma inicialização específica na guia Referências (consulte [Lançamentos em referências (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)).

![Descobrindo o status de lançamento](/help/sites-cloud/authoring/assets/launches-status.png)
