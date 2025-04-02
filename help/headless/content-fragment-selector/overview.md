---
title: Seletor de fragmentos de conteúdo de front-end micro para Adobe Experience Manager as a Cloud Service
description: Use o Seletor de fragmento de conteúdo de micro front-end para pesquisar, localizar e recuperar fragmentos de conteúdo do aplicativo.
role: Admin, User
source-git-commit: 32e1b3cef768b420f32b70202ddadc80db2b74e8
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 6%

---


# Seletor de fragmentos de conteúdo de front-end micro {#micro-frontend-content-fragment-selector}

O Seletor de fragmento de conteúdo de micro front-end fornece uma interface do usuário que se integra facilmente ao repositório do as a Cloud Service no Adobe Experience Manager (AEM). A interface permite navegar ou pesquisar fragmentos de conteúdo no repositório e usá-los no aplicativo.

A interface de usuário de MicroFront-End é disponibilizada em seu aplicativo usando o pacote Seletor de fragmento de conteúdo. As atualizações do pacote são automaticamente importadas e carregadas no aplicativo.

![Seletor de Fragmento de Conteúdo de MicroFront-End - Visão Geral](/help/headless/assets/content-fragment-selector-overview.png)

O Seletor de fragmentos de conteúdo oferece muitos benefícios, como:

* Facilidade de integração com qualquer um dos aplicativos da Adobe.
* Fácil de manter, à medida que as atualizações no pacote Seletor de fragmento de conteúdo são implantadas automaticamente no Seletor de fragmento de conteúdo disponível para o aplicativo. Isso significa que seu aplicativo não precisa tomar medidas para carregar as modificações mais recentes.
* Facilidade de personalização, usando propriedades que controlam a exibição do Seletor de fragmento de conteúdo no aplicativo.
* A pesquisa de texto completo, juntamente com filtros personalizáveis, permite a navegação rápida dos Fragmentos de conteúdo na experiência de criação.
* Capacidade de alternar repositórios em uma organização IMS para seleção de Fragmento de conteúdo.
* Capacidade de classificar fragmentos de conteúdo e visualizá-los na exibição selecionada.

## Pré-requisitos {#prerequisites}

### Autenticação IMS {#ims-authentication}

Se você precisar do fluxo de trabalho de autenticação IMS, verifique se:

* O aplicativo está sendo executado em `HTTPS`.
* O URL do aplicativo está na lista de URLs de redirecionamento permitidos para o cliente IMS.
* O fluxo de logon do IMS é configurado e renderizado usando um pop-up no navegador da Web. Portanto, os pop-ups devem ser ativados ou permitidos no navegador de destino.

Como alternativa, se seu aplicativo já estiver autenticado com o fluxo de trabalho do IMS, você poderá adicionar as informações apropriadas do IMS.

## Instalação {#installation}

Use o componente `ContentFragmentSelector`. Há várias opções de instalação:

1. Registro NPM (Private Adobe Registry)

   * Adicionar o seguinte a `.npmrc`:

     ```html
     @aem-sites:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-aem-sites-release/
     ```

   * Depois instalar

     ```html
     npm install @aem-sites/content-fragment-selector
     ```

1. Repositório Git

   * Adicionar o seguinte a `package.json` dependências:

     ```html
     "@aem-sites/content-fragment-selector": "git+https://github.com/adobe/<your-private-repo-url>.git#version"
     ```

## Uso do Seletor de fragmentos de conteúdo {#using-the-Content-Fragment-selector}

Depois que o Seletor de fragmento de conteúdo estiver configurado e autenticado para usar o Seletor de fragmento de conteúdo com o aplicativo do AEM as a Cloud Service, você poderá selecionar Fragmentos de conteúdo ou executar várias outras operações para pesquisar os fragmentos no repositório:

![O Seletor de Fragmento do Conteúdo](/help/headless/assets/content-fragment-selector-using.png)

* Com o seletor **Repositório** na parte superior direita, você pode selecionar o repositório que deseja usar
* No painel esquerdo, é possível:
   * Ocultar ou mostrar pastas do repositório selecionado
   * Selecione uma pasta específica para mostrar os fragmentos de conteúdo nessa pasta
* No painel principal, é possível:
   * Selecione fragmentos de conteúdo
   * Pesquisar fragmentos de conteúdo
   * Classificar a lista atual de acordo com várias colunas; crescentes ou decrescentes
   * Ver o indicador do formato de visualização
   * Mostrar, ocultar e especificar filtros

### Ocultar/Mostrar painel {#hide-show-panel}

Para ocultar pastas na navegação à esquerda, clique no ícone **Ocultar pastas**. Para desfazer as alterações, clique no ícone **Ocultar pastas** novamente.

### Alternador de repositório {#repository-switcher}

O Seletor de fragmento de conteúdo permite selecionar um repositório para a seleção de fragmentos.

Você pode selecionar o repositório de sua escolha no menu suspenso **Repositório**, disponível na parte superior do painel principal.

![O Seletor de Fragmento do Conteúdo](/help/headless/assets/content-fragment-repository-selector.png)

As opções de repositório disponíveis na lista suspensa se baseiam na propriedade `repositoryId` definida no arquivo `index.html`. Essa propriedade se baseia no ambiente da organização IMS selecionada acessada pelo usuário conectado no momento.

Os consumidores podem passar um `repositoryID` preferencial para renderizar fragmentos de um repositório específico e parar de renderizar o alternador de repositório.

### Pastas de fragmentos de conteúdo {#content-fragments-folders}

O repositório de fragmentos de conteúdo é uma coleção de pastas de fragmento de conteúdo que você pode usar para executar operações.

### Filtros {#filters}

O Seletor de fragmento de conteúdo também fornece opções de filtro prontas para uso para refinar os resultados da pesquisa. Vários filtros estão disponíveis, incluindo:

* **Modelo de fragmento**
* **Localização**
* **Status**: o estado atual do fragmento; `New`, `Draft`, `Published`, `Modified`, `Unpublished`
* Tags
* Usuários
* Datas e horas

![Opções de filtro](/help/headless/assets/content-selector-filters.png)

Você também pode criar um filtro de pesquisa padrão para salvar para uso futuro. Para criar filtros de pesquisa personalizados para os fragmentos de conteúdo, você pode usar a propriedade `filterSchema`.

### Barra de pesquisa {#search-bar}

O Seletor de fragmentos de conteúdo permite executar uma pesquisa de texto completo dos fragmentos no repositório selecionado. Por exemplo, se você digitar a palavra-chave `wave` na barra de pesquisa, todos os fragmentos com a palavra-chave `wave` mencionada em qualquer uma das propriedades de metadados serão exibidos.

### Classificação {#sorting}

Você pode classificar fragmentos no Seletor de fragmento de conteúdo por várias propriedades. Também é possível classificar os fragmentos em ordem crescente ou decrescente.

### Visualizar tipo {#view-type}

O Seletor de fragmentos de conteúdo permite visualizar o fragmento no:

* **Modo de Exibição de Tabela**
