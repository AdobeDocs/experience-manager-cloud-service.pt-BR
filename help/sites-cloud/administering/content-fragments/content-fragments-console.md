---
title: Console de fragmentos de conteúdo
description: Saiba como gerenciar fragmentos de conteúdo no Console de fragmentos de conteúdo.
landing-page-description: Saiba como gerenciar fragmentos de conteúdo no Console de fragmentos de conteúdo, que está focado no alto volume de uso de fragmentos de conteúdo para casos de uso headless, mas que também é usado para a criação de páginas.
exl-id: 0e6e3b61-a0ca-44b8-914d-336e29761579
source-git-commit: 99e3c07f8376859692db41c633bfaa602ed65358
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 97%

---

# Console de fragmentos de conteúdo  {#content-fragments-console}

Saiba como o Console de fragmentos de conteúdo otimiza o acesso aos fragmentos de conteúdo, ajudando você a criá-los, pesquisá-los e gerenciá-los realizando ações administrativas como publicar, desfazer a publicação e copiar.

O Console de fragmentos de conteúdo é dedicado ao gerenciamento, pesquisa e criação de fragmentos de conteúdo. Ele foi otimizado para uso em um contexto headless, mas também é usado ao criar fragmentos de conteúdo para uso na criação de páginas.

>[!NOTE]
>
>Esse console só exibe fragmentos de conteúdo. Ele não exibe outros tipos de ativos como imagens e vídeos.

>[!NOTE]
>
>No momento, o acesso aos fragmentos de conteúdo é possível através:
>
>* deste console de **Fragmentos de conteúdo**
>* do console de **Ativos** — consulte [Gerenciamento de fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md)


>[!NOTE]
>
>Uma seleção de [atalhos de teclado estão disponíveis para uso neste console](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md).

O Console de fragmentos de conteúdo pode ser acessado diretamente do nível superior da navegação global:

![Navegação global - Console de fragmentos de conteúdo](assets/cfc-global-navigation.png)

Selecionar **Fragmentos de conteúdo** abrirá o console em uma nova guia.

![Console de fragmentos de conteúdo - Visão geral](assets/cfc-console-overview.png)

Aqui você pode ver três áreas principais:

* A barra de ferramentas superior
   * Fornece a funcionalidade padrão do AEM
   * Também mostra sua organização IMS
* O painel esquerdo
   * Aqui você pode ocultar ou revelar a árvore de pastas
   * É possível selecionar uma ramificação específica da árvore
* O painel principal/direito; aqui, você pode:
   * Consultar a lista de todos os fragmentos de conteúdo na ramificação selecionada da árvore
      * A localização é indicada pela navegação estrutural; elas também podem ser usadas para alterar a localização
      * Os fragmentos de conteúdo da pasta selecionada e de todas as pastas derivadas serão mostrados
         * Vários campos de informação sobre um fragmento de conteúdo fornecem links; eles podem abrir o fragmento apropriado no editor
      * Você pode selecionar um cabeçalho de coluna para classificar a tabela de acordo com essa coluna; selecione novamente para alternar entre ordem crescente e decrescente
   * **[Criar](#creating-new-content-fragment)** um novo fragmento de conteúdo
   * [Filtrar](#filtering-fragments) os fragmentos de conteúdo de acordo com uma seleção de predicados e salvar o filtro para uso futuro
   * [Pesquisar](#searching-fragments) os fragmentos de conteúdo
   * Personalizar a visualização da tabela para mostrar as colunas de informações selecionadas
   * Usar o recurso **Abrir no Assets** para abrir o local atual diretamente no console de **Ativos**.

      >[!NOTE]
      >
      >O console de **Ativos** é usado para acessar ativos, como imagens, vídeos etc.  Esse console pode ser acessado:
      >
      >* usando o link **Abrir no Assets** (no Console de fragmentos de conteúdo)
      >* diretamente do painel de navegação global


Selecionar um fragmento específico abrirá uma barra de ferramentas focada nas ações disponíveis para esse fragmento. Também é possível selecionar vários fragmentos; a seleção de ações será ajustada de acordo.

![Console de fragmentos de conteúdo - Barra de ferramentas de um fragmento selecionado](assets/cfc-fragment-toolbar.png)

## Criar um novo fragmento de conteúdo {#creating-new-content-fragment}

Selecionar **Criar** abre a caixa de diálogo compacta **Novo fragmento de conteúdo**:

![Console de fragmentos de conteúdo - Criar um novo fragmento](assets/cfc-console-create.png)

## Filtrar fragmentos {#filtering-fragments}

O painel Filtro oferece:

* uma seleção de predicados que podem ser selecionados e combinados
* a oportunidade de **Salvar** sua configuração
* a opção de recuperar um filtro de pesquisa salvo para reutilização

![Console de fragmentos de conteúdo - Filtragem](assets/cfc-console-filter.png)

## Pesquisar fragmentos {#searching-fragments}

A caixa de pesquisa é compatível com a pesquisa de texto completo. Inserir seus termos de pesquisa na caixa de pesquisa:

![Console de fragmentos de conteúdo - Pesquisar](assets/cfc-console-search-01.png)

Fornecerá os resultados selecionados:

![Console de fragmentos de conteúdo - Resultados da pesquisa](assets/cfc-console-search-02.png)

A caixa de pesquisa também fornece acesso rápido aos **Fragmentos de conteúdo recentes** e às **Pesquisas salvas**:

![Console de fragmentos de conteúdo - Recentes e salvos](assets/cfc-console-search-03.png)
