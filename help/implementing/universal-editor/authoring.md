---
title: Criação de conteúdo com o Editor universal
description: Saiba como é fácil e intuitivo para os autores criarem conteúdo utilizando o Editor universal.
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: 481202760e0d22cde9c32e0b781dc99f67d463e4
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 35%

---


# Criação de conteúdo com o Editor universal {#authoring}

Saiba como é fácil e intuitivo para os autores criarem conteúdo utilizando o Editor universal.

## Introdução {#introduction}

O Editor universal permite editar qualquer aspecto de qualquer conteúdo em qualquer implementação para que você possa fornecer experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência do desenvolvedor de última geração.

Para fazer isso, o Editor universal fornece aos autores de conteúdo uma interface intuitiva que requer treinamento mínimo para simplesmente serem capazes de começar a editar o conteúdo. Este documento descreve a experiência de criação do Universal Editor.

>[!TIP]
>
>Para obter uma introdução mais detalhada do Editor universal, consulte o documento [Introdução ao Editor universal.](introduction.md)

>[!NOTE]
>
>O Editor Universal ainda está em desenvolvimento. No momento, não é possível editar todos os tipos de conteúdo.

## Preparação do aplicativo {#prepare-app}

Para criar conteúdo para um aplicativo usando o Editor universal, o aplicativo deve ser instrumentado por um desenvolvedor para oferecer suporte ao editor.

>[!TIP]
>
>Consulte [Introdução ao editor universal no AEM](getting-started.md) para obter um exemplo de como configurar um aplicativo AEM para funcionar com o Editor universal.

## Fazer logon {#sign-in}

Após o aplicativo ser instrumentado para funcionar com o Editor universal, será necessário fazer logon no Editor universal. Você precisará de uma Adobe ID para fazer logon e [ter acesso ao Editor universal.](getting-started.md#request-access)

Depois de fazer logon, insira o URL da página que deseja editar na [barra de localização.](#location-bar) para que você possa começar a editar conteúdo como [conteúdo de texto](#text-mode) ou [conteúdo de mídia.](#media-mode)

## Entenda a interface {#ui}

A interface do usuário do é dividida em cinco áreas principais.

* [O cabeçalho da Experience Cloud](#experience-cloud-header)
* [O cabeçalho do Editor universal](#universal-editor-header)
* [O painel de modo](#mode-rail)
* [O editor](#editor)
* [O painel de componentes](#component-rail)

![A interface do Editor universal](assets/ui.png)

### O cabeçalho da Experience Cloud {#experience-cloud-header}

O cabeçalho da Experience Cloud está sempre presente na parte superior da tela. É uma âncora que informa onde você está na Experience Cloud e o ajuda a navegar por outros aplicativos da Experience Cloud.

![O cabeçalho da Experience Cloud](assets/experience-cloud-header.png)

#### Experience Manager {#experience-manager}

Clique no link da Adobe Experience Cloud à esquerda do cabeçalho para navegar até a raiz da solução do Experience Manager e acessar ferramentas como o [Cloud Manager,](/help/onboarding/cloud-manager-introduction.md) o [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) e a [distribuição de softwares.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=pt-br)

![Botão de navegação global](assets/global-navigation.png)

#### Organização {#organization}

Exibe a organização na qual você está conectado no momento. Toque ou clique para alternar para outra organização se a Adobe ID estiver associada a mais do que uma.

![Indicador da organização](assets/organization.png)

#### Soluções {#solutions}

Tocar ou clicar no alternador de soluções permite acessar rapidamente as outras soluções da Experience Cloud.

![Alternador de soluções](assets/solutions.png)

#### Ajuda {#help}

O ícone de ajuda fornece acesso rápido aos recursos de aprendizagem e suporte.

![Ajuda](assets/help.png)

#### Notificações {#notifications}

Esse ícone contém o número de incompletos atribuídos no momento [notificações.](/help/implementing/cloud-manager/notifications.md)

![Notificações](assets/notifications.png)

#### Propriedades do usuário {#user-properties}

Toque ou clique no ícone que representa seu usuário para acessar suas configurações de usuário. Se você não tiver uma imagem de usuário configurada, um ícone será atribuído aleatoriamente.

![Propriedades do usuário](assets/user-properties.png)

### O cabeçalho do Editor universal {#universal-editor-header}

O cabeçalho do Editor universal está sempre presente na parte superior da tela, logo abaixo [do cabeçalho da Experience Cloud.](#experience-cloud-header) Ele fornece acesso rápido para navegar para outra página para editar e publicar a página atual.

![O cabeçalho do Editor universal](assets/universal-editor-header.png)

#### O menu de opções {#hamburger-menu}

O menu de opções ainda não foi implementado.

![Menu Hambúrguer](assets/hamburger-menu.png)

#### Barra de localização {#location-bar}

A barra de localização mostra o endereço da página que você está editando. Toque ou clique para inserir o endereço de outra página para editar.

![Barra de localização](assets/location-bar.png)

>[!TIP]
>
>Use a tecla de atalho `L` para abrir a barra de endereços.

>[!NOTE]
>
>Qualquer página que você deseja editar com o Editor universal deve ser [instrumentada para oferecer suporte ao Editor universal.](getting-started.md)

#### Configurações do emulador {#emulator}

Toque ou clique no ícone de emulação para definir como o Editor universal renderiza a página.

![Ícone de Emulador](assets/emulator.png)

Tocar ou clicar no ícone de emulação revela as opções.

![Opções de emulação](assets/emulation-options.png)

Por padrão, o editor será aberto no layout do desktop, onde a altura e a largura são definidas automaticamente pelo navegador.

Você também pode optar por emular um dispositivo móvel e, no Universal Editor:

* Definir sua orientação
* Definir largura e altura
* Alterar a orientação

#### Abrir visualização do aplicativo {#open-app-preview}

Toque ou clique no ícone de visualização do aplicativo aberto para abrir a página que você está editando no momento em sua própria guia do navegador, livre do editor para visualizar seu conteúdo.

![Abrir visualização do aplicativo](assets/open-app-preview.png)

>[!TIP]
>
>Usar a tecla de atalho `O` (a letra O) para abrir a pré-visualização do aplicativo.

#### Publicação {#publish}

Toque ou clique no botão Publicar para poder publicar as alterações no conteúdo em tempo real para consumo pelos leitores.

![Botão de publicação](assets/publish.png)

>[!TIP]
>
>Consulte o documento [Publicação de conteúdo com o Editor visual universal](publishing.md) para obter mais informações sobre a publicação com o Editor universal.

### O painel do modo {#rail}

O painel de modo está sempre presente no lado esquerdo do editor. Ele permite alternar facilmente o editor entre diferentes modos de edição.

![O painel de modo](assets/mode-rail.png)

#### Modo de visualização {#preview-mode}

No modo de visualização, a página é renderizada no editor da maneira como seria vista em seu serviço publicado. Isso permite que o autor de conteúdo navegue pelo conteúdo clicando em links etc.

![Modo de visualização](assets/preview-mode.png)

>[!TIP]
>
>Use a tecla de atalho `P` para alternar para o modo de visualização.

#### Modo de texto {#text-mode}

No modo de texto, o autor de conteúdo pode clicar em para selecionar o conteúdo do texto.

![Modo de texto](assets/text-mode.png)

* Você pode [editar texto simples](#editing-content) em vigor.
* Também é possível [editar rich text](#editing-rich-text) no local com opções de formatação adicionais exibidas no painel de componentes.

>[!TIP]
>
>Usar a tecla de atalho `T` para alternar para o modo texto.

#### Modo de mídia {#media-mode}

No modo de mídia, o autor de conteúdo pode clicar em para selecionar conteúdo de mídia.

![Modo de mídia](assets/media-mode.png)

Detalhes do conteúdo são exibidos no painel de componentes e o autor também pode [editar o conteúdo de mídia.](#editing-media)

>[!TIP]
>
>Usar a tecla de atalho `M` para alternar para o modo de mídia.

#### Modo de componente {#component-mode}

No modo de componente, o autor de conteúdo pode clicar para selecionar [Fragmentos de conteúdo.](/help/assets/content-fragments/content-fragments.md)

![Modo de componente](assets/component-mode.png)

Ao selecionar um Fragmento de conteúdo, os detalhes dele são exibidos no painel de componentes, onde você pode [editar o fragmento de conteúdo.](#edit-content-fragment)

>[!TIP]
>
>Usar a tecla de atalho `C` para alternar para o modo de componente.

#### Editar {#edit}

Quando em [modo componente,](#component-mode) se você selecionar um [Fragmento de conteúdo,](/help/assets/content-fragments/content-fragments.md) a opção editar é exibida no painel modo.

![Ícone Editar](assets/edit.png)

Tocar ou clicar no botão de edição abre o [Editor de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor) em uma nova guia, que permite acessar todo o potencial do Editor de fragmento de conteúdo.

Também é possível editar detalhes do fragmento de conteúdo na [painel de componentes](#edit-content-fragment) dependendo das necessidades do seu fluxo de trabalho.

>[!TIP]
>
>Usar a tecla de atalho `E` para editar um componente selecionado.

### O editor {#editor}

O editor ocupa a maior parte da janela e é onde a página especificada em [a barra de localização](#location-bar) é renderizado.

* Se o editor estiver em um modo de edição como [modo texto](#text-mode) ou [modo mídia,](#media-mode) o conteúdo será editável, mas você não poderá seguir os links.
* Se o editor estiver em [modo de visualização,](#preview-mode) o conteúdo será navegável e você poderá seguir os links, mas não poderá editar o conteúdo.

![Editor](assets/editor.png)

### Trilho do componente {#component-rail}

O painel de componentes está sempre presente no lado esquerdo do editor. Dependendo do modo, ele pode mostrar detalhes de um componente selecionado no conteúdo ou na hierarquia do conteúdo da página.

![O painel de componentes](assets/component-rail.png)

#### Modo de propriedades {#properties-mode}

No modo de propriedades, o painel mostra as propriedades do componente atualmente selecionado no editor. Este é o modo padrão do painel de componentes quando uma página é carregada.

![Modo de propriedades](assets/properties-mode.png)

Dependendo do tipo de componente selecionado, os detalhes podem ser exibidos e modificados no painel de propriedades.

![Detalhes do componente](assets/component-details.png)

Observe que nem todos os componentes têm detalhes que podem ser mostrados e/ou editados.

>[!TIP]
>
>Usar a tecla de atalho `D` para alternar para o modo de propriedades.

#### Modo de árvore de conteúdo {#Content-tree-mode}

No modo de árvore de conteúdo, o painel mostra a hierarquia do conteúdo da página.

![Modo de árvore de conteúdo](assets/content-tree-mode.png)

Ao selecionar um item na árvore de conteúdo, o editor rola até esse conteúdo e o seleciona.

![Árvore de conteúdo](assets/content-tree.png)

>[!TIP]
>
>Usar a tecla de atalho `F` para alternar para o modo de árvore de conteúdo.


## Editar o conteúdo {#editing-content}

A edição de conteúdo é simples e intuitiva. Nos modos de edição ([modo texto](#text-mode), [modo de mídia](#media-mode), e [modo do componente](#component-mode)), conforme você passa o mouse sobre o conteúdo no editor, o conteúdo editável é realçado com uma caixa azul.

![O conteúdo editável é destacado por uma caixa azul](assets/editable-content.png)

Observe que, no modo de edição, tocar ou clicar no conteúdo tenta selecioná-lo para edição. Se você deseja navegar pelo seu conteúdo utilizando os links, alterne para o [modo de visualização.](#preview-mode)

Dependendo do [modo](#mode-rail) estiver no e o conteúdo selecionado, tiver opções de edição no local diferentes e poder revisar propriedades adicionais para o conteúdo usando o [painel de componentes.](#component-rail)

### Edição de Texto sem Formatação {#edit-plain-text}

Se você estiver em [modo texto](#text-mode) e selecionar um componente de texto simples, é possível editar o texto no local.

![Editar o conteúdo](assets/editing-content.png)

Basta digitar para atualizar o conteúdo. Pressione enter/return ou toque ou clique fora da caixa de texto para salvar as alterações.

### Edição de Rich Text {#edit-rich-text}

Se você estiver em [modo texto](#text-mode) e selecionar um componente de rich text, é possível editar o texto no local.

Basta digitar para atualizar o conteúdo. Pressione enter/return ou toque ou clique fora da caixa de texto para salvar as alterações.

Além disso, as opções de formatação e os detalhes do texto estão disponíveis no painel de componentes.

![Edição de um componente de rich text](assets/rich-text-editing.png)

As alterações de formatação são salvas automaticamente no conteúdo.

### Editando mídia {#edit-media}

Se você estiver em [modo de mídia](#media-mode) e selecionar uma imagem, você poderá ver seus detalhes no painel de componentes.

![Edição de mídia](assets/ue-edit-media.png)

Toque ou clique no **Substituir** botão abaixo da visualização da imagem selecionada no painel de componentes para substituir a imagem por outra da biblioteca de ativos.

1. A variável [seletor de ativos](/help/assets/asset-selector.md#using-asset-selector) é aberta para permitir que você selecione um ativo.
1. Toque ou clique para selecionar um novo ativo.
1. Toque ou clique **Selecionar** para retornar ao painel de componentes onde o ativo foi substituído.

As alterações são salvas no conteúdo automaticamente.

>[!TIP]
>
>Usar a tecla de atalho `R` para abrir o seletor de ativos e substituir a imagem selecionada.

### Edição de fragmentos de conteúdo {#edit-content-fragment}

Se você estiver em [modo do componente](#component-mode) e você selecionar um [Fragmento de conteúdo,](/help/assets/content-fragments/content-fragments.md) é possível editar os detalhes no painel de componentes.

![Edição de um fragmento de conteúdo](assets/ue-edit-cf.png)

Os campos definidos no modelo de conteúdo do fragmento de conteúdo selecionado são exibidos e editáveis no painel de componentes.

As alterações são salvas no conteúdo automaticamente.

Se quiser editar o fragmento de conteúdo na caixa [Editor de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor) clique no link [botão editar](#edit) no painel de modos.

## Visualização de conteúdo {#previewing-content}

Ao terminar de editar o conteúdo, você geralmente deseja navegar por ele e observar como ele é exibido em outras páginas. No [modo de visualização](#preview-mode), é possível clicar em links e navegar pelo conteúdo, como um leitor faria. O conteúdo é renderizado no editor como seria publicado.

Note que, no modo de visualização, a ação de tocar ou clicar no conteúdo funciona da mesma forma que para um leitor do conteúdo. Se desejar selecionar o conteúdo para edição, alterne para um modo de edição como [modo texto](#text-mode) ou [modo de mídia.](#media-mode)

## Recursos adicionais {#additional-resources}

Para saber mais sobre o Editor universal, consulte estes documentos.

* [Introdução ao Universal Editor](introduction.md) : saiba como o Editor universal permite editar qualquer aspecto de qualquer conteúdo em qualquer implementação para que você possa fornecer experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência do desenvolvedor de última geração.
* [Publicação de conteúdo com o Editor universal](publishing.md): saiba como o Editor visual universal publica o conteúdo e como seus aplicativos podem lidar com esse conteúdo.
* [Introdução ao Editor universal no AEM](getting-started.md): saiba como obter acesso ao Editor universal e começar a instrumentar seu primeiro aplicativo do AEM para utilizá-lo.
* [Arquitetura do Editor universal](architecture.md): saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.
* [Atributos e tipos](attributes-types.md): saiba mais sobre os atributos e tipos de dados exigidos pelo Editor universal.
* [Autenticação do Editor universal](authentication.md): saiba como funciona a autenticação do Editor universal.
