---
title: 'Pesquisar  '
description: Localize seu conteúdo mais com mais rapidez usando uma pesquisa abrangente
exl-id: 8a799e9a-1461-4e79-ae90-1978af6cf0ed
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 99%

---

# Pesquisar   {#search-feature}

O ambiente de criação do AEM fornece vários mecanismos de pesquisa de conteúdo, dependendo do tipo de recurso.

## Noções básicas de pesquisa {#search-basics}

A pesquisa está disponível na barra de ferramentas superior:

![Ícone de Pesquisa](/help/sites-cloud/authoring/assets/search-icon.png)

Com o painel de pesquisa, você pode:

* Pesquise por uma palavra-chave, um caminho ou uma tag específica
* Filtre de acordo com os critérios específicos dos recursos, como datas modificadas, status da página, tamanho do arquivo, etc.
* Defina e use uma [pesquisa salva](#saved-searches) - com base nos critérios acima

>[!NOTE]
>
>A pesquisa também pode ser invocada usando a tecla de atalho `/` (barra) sempre que o painel de pesquisa estiver visível.

## Pesquisar e filtrar {#search-and-filter}

Para pesquisar e filtrar os recursos:

1. Abra **Pesquisar** (com a lupa na barra de ferramentas) e insira o termo de pesquisa. Serão feitas sugestões que poderão ser selecionadas:

   ![Pesquisar termo](/help/sites-cloud/authoring/assets/search-term.png)

   Por padrão, os resultados da pesquisa ficarão limitados à sua localização atual (ou seja, o console e o tipo de recurso relacionado): 

   ![Local de pesquisa](/help/sites-cloud/authoring/assets/search-term-location.png)

1. Se necessário, é possível remover o filtro de localização (selecione **X** no filtro que deseja remover) para pesquisar em todos os consoles/tipos de recurso.
1. Os resultados serão mostrados, agrupados de acordo com o console e o tipo de recurso relacionado.

   Você pode selecionar um recurso específico (para a ação adicional) ou detalhar selecionando o tipo de recurso desejado; por exemplo, **Exibir todos os sites**: 

   ![Resultados da pesquisa](/help/sites-cloud/authoring/assets/search-results.png)

1. Se desejar mais detalhes, selecione o símbolo do Painel (parte superior esquerda) para abrir o painel lateral **Filtros e opções**.

   ![Botão Painel](/help/sites-cloud/authoring/assets/rail-button.png)

   De acordo com o tipo de recurso, a Pesquisa mostrará uma seleção predefinida de critérios de pesquisa/filtro.

   O painel lateral permite selecionar:

   * Pesquisas salvas
   * Diretório de pesquisa
   * Tags
   * Critérios de pesquisa, por exemplo, datas modificadas, status de publicação, status da Live Copy.

   >[!NOTE]
   >
   >O critério de pesquisa pode variar:
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
>Os critérios de pesquisa persistem ao selecionar um item nos resultados de pesquisa.
>
>Quando você seleciona um item na página de resultados da pesquisa e retorna à página de pesquisa após usar o botão Voltar do navegador, os critérios de pesquisa permanecem.

## Pesquisas salvas {#saved-searches}

Além de pesquisar por uma grande variedade de aspectos, também é possível salvar uma configuração de pesquisa específica para recuperar e usar em um estágio posterior:

1. Defina o seu critério de pesquisa e selecione **Salvar**.

   ![Como salvar uma pesquisa](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. Atribua um nome, em seguida, use **Salvar** para confirmar:

   ![Como salvar uma pesquisa com um nome](/help/sites-cloud/authoring/assets/search-save-name.png)

1. Sua pesquisa salva estará disponível no seletor da próxima vez que você acessar o painel de pesquisa:

   ![Pesquisas salvas](/help/sites-cloud/authoring/assets/saved-searches.png)

1. Depois de salvo é possível:

   * Use **X** (em comparação ao nome da pesquisa salva) para iniciar uma nova consulta (a própria pesquisa salva não será excluída).
   * **Edite a pesquisa salva**, altere as condições de pesquisa e, em seguida, **Salve** novamente.

As pesquisas salvas podem ser modificadas ao selecionar a pesquisa salva e clicar em **Editar pesquisa salva** na parte inferior do painel de pesquisa.

![Modificação de uma pesquisa salva](/help/sites-cloud/authoring/assets/saved-searches-modify.png)
