---
title: Pesquisar
description: Encontre seu conteúdo mais rapidamente com a pesquisa abrangente
exl-id: 8a799e9a-1461-4e79-ae90-1978af6cf0ed
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 83%

---

# Pesquisar   {#search-feature}

O ambiente de criação do AEM fornece vários mecanismos de pesquisa de conteúdo, dependendo do tipo de recurso.

## Noções básicas de pesquisa {#search-basics}

A pesquisa está disponível na barra de ferramentas superior:

![Ícone de Pesquisa](/help/sites-cloud/authoring/assets/search-icon.png)

Com o painel de pesquisa, você pode:

* Pesquise por uma palavra-chave, um caminho ou uma tag específica
* Filtre de acordo com os critérios específicos dos recursos, como datas modificadas, status da página, tamanho do arquivo e assim por diante.
* Defina e use uma [pesquisa salva](#saved-searches) - com base nos critérios acima

>[!NOTE]
>
>A pesquisa também pode ser invocada usando a tecla de atalho `/` (barra) sempre que o painel de pesquisa estiver visível.

## Pesquisar e filtrar {#search-and-filter}

Para pesquisar e filtrar os recursos:

1. Abra **Pesquisar** (com a lupa na barra de ferramentas) e insira o termo de pesquisa. Sugestões serão exibidas e poderão ser selecionadas:

   ![Termo de pesquisa](/help/sites-cloud/authoring/assets/search-term.png)

   Por padrão, os resultados da pesquisa são limitados à sua localização atual (ou seja, console e tipo de recurso relacionado):

   ![Local de pesquisa](/help/sites-cloud/authoring/assets/search-term-location.png)

1. Se necessário, você pode remover o filtro de localização (selecione **X** no filtro que deseja remover) para pesquisar em todos os tipos de consoles/recursos.
1. Os resultados são mostrados, agrupados de acordo com o console e o tipo de recurso relacionado.

   Você pode selecionar um recurso específico (para a ação adicional) ou detalhar selecionando o tipo de recurso desejado; por exemplo, **Exibir todos os sites**:

   ![Resultados da pesquisa](/help/sites-cloud/authoring/assets/search-results.png)

1. Se desejar mais detalhes, selecione o símbolo do Painel (parte superior esquerda) para abrir o painel lateral **Filtros e opções**.

   ![Botão Painel](/help/sites-cloud/authoring/assets/rail-button.png)

   De acordo com o tipo de recurso, a Pesquisa mostrará uma seleção predefinida de critérios de pesquisa/filtro.

   O painel lateral permite selecionar:

   * Pesquisas salvas
   * Diretório de pesquisa
   * Tags
   * Critérios de pesquisa, por exemplo, Datas modificadas, Status do Publish, Status da Live Copy

   >[!NOTE]
   >
   >Os critérios de pesquisa podem variar:
   >
   >* Dependendo do tipo de recurso selecionado; por exemplo, os critérios de Ativos e comunidades são compreensivelmente especializados.
   >* Sua instância, como os Formulários de pesquisa, pode ser personalizada (adequada ao local no AEM).

<!--
  >* Your instance as the [Search Forms](/help/sites-administering/search-forms.md) can be customized (appropriate to the location within AEM).
  -->

![Painel lateral de pesquisa](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. Você também pode adicionar outros termos de pesquisa.

1. Feche a **Pesquisa** com o **X** (canto superior direito).

>[!NOTE]
>
>Os critérios de pesquisa são mantidos ao selecionar um item nos resultados da pesquisa.
>
>Quando você seleciona um item na página de resultados da pesquisa e retorna à página de pesquisa após usar o botão Voltar do navegador, os critérios de pesquisa permanecem.

## Pesquisas salvas {#saved-searches}

Além de pesquisar por uma grande variedade de aspectos, também é possível salvar uma configuração de pesquisa específica para recuperar e usar em um estágio posterior:

1. Defina seus critérios de pesquisa e clique em **Salvar**.

   ![Como salvar uma pesquisa](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. Atribua um nome, em seguida, use **Salvar** para confirmar:

   ![Como salvar uma pesquisa com um nome](/help/sites-cloud/authoring/assets/search-save-name.png)

1. Sua pesquisa salva estará disponível no seletor da próxima vez que você acessar o painel de pesquisa:

   ![Pesquisas salvas](/help/sites-cloud/authoring/assets/saved-searches.png)

1. Depois de salvo, é possível:

   * Usar o **x** (próximo ao nome da pesquisa salva) para iniciar uma nova consulta (a pesquisa salva em si não será excluída).
   * **Editar pesquisa salva**, alterar as condições de pesquisa e **Salvar** novamente.

As pesquisas salvas podem ser modificadas ao selecionar a pesquisa salva e clicar em **Editar pesquisa salva** na parte inferior do painel de pesquisa.

![Modificação de uma pesquisa salva](/help/sites-cloud/authoring/assets/saved-searches-modify.png)
