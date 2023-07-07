---
title: Criação de conteúdo com o Editor universal
description: Saiba como é fácil e intuitivo para os autores criarem conteúdo utilizando o Editor universal.
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: c6ab2d9b01a3f1abedb06d1d413e7eceb8b1c031
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 49%

---

# Criação de conteúdo com o Editor universal {#authoring}

Saiba como é fácil e intuitivo para os autores criarem conteúdo utilizando o Editor universal.

## Introdução {#introduction}

O Editor universal permite editar qualquer aspecto de qualquer conteúdo em qualquer implementação para que você possa fornecer experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência do desenvolvedor de última geração.

Para fazer isso, o Editor universal fornece aos autores de conteúdo uma interface intuitiva que requer treinamento mínimo para simplesmente serem capazes de começar a editar o conteúdo.

>[!TIP]
>
>Para obter uma introdução mais detalhada do Editor universal, consulte o documento [Introdução ao Editor universal.](introduction.md)

>[!NOTE]
>
>Atualmente, o Editor universal está em desenvolvimento e não pode editar todos os tipos de conteúdo.

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

Toque ou clique no ícone Abrir visualização do aplicativo para abrir a página que você está editando no próprio navegador (fora do editor) e visualizar as alterações.

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

No modo de texto, a página é renderizada no editor, mas o autor de conteúdo pode clicar em para selecionar o conteúdo do texto e editá-lo. Esse é o modo padrão do editor quando uma página é carregada.

![Modo de texto](assets/text-mode.png)

>[!TIP]
>
>Usar a tecla de atalho `T` para alternar para o modo texto.

#### Modo de mídia {#media-mode}

No modo de mídia, a página é renderizada no editor, mas o autor de conteúdo pode clicar em para selecionar o conteúdo de mídia e editá-lo.

![Modo de mídia](assets/media-mode.png)

>[!TIP]
>
>Usar a tecla de atalho `M` para alternar para o modo de mídia.

#### Modo de componente {#component-mode}

No modo de componente, a página é renderizada no editor, mas o autor de conteúdo pode clicar em para selecionar componentes de página.

![Modo de componente](assets/component-mode.png)

>[!TIP]
>
>Usar a tecla de atalho `C` para alternar para o modo de componente.

>[!NOTE]
>
>O modo de componente ainda está em desenvolvimento e está atualmente limitado à seleção de componentes.

### O editor {#editor}

O editor ocupa a maior parte da janela e é onde a página especificada em [a barra de localização](#location-bar) é renderizado.

* Se o editor estiver em um modo de edição como [modo texto](#text-mode) ou [modo mídia,](#media-mode) o conteúdo será editável e você não poderá seguir links.
* Se o editor estiver em [modo de visualização,](#preview-mode) o conteúdo será navegável e você poderá seguir os links, mas não poderá editar o conteúdo.

![Editor](assets/editor.png)

### Trilho do componente {#component-rail}

O painel de componentes está sempre presente no lado esquerdo do editor. Dependendo do modo, ele pode mostrar detalhes de um componente selecionado no conteúdo ou na hierarquia do conteúdo da página.

![O painel de componentes](assets/component-rail.png)

#### Modo de propriedades {#properties-mode}

No modo de propriedades, o painel mostra as propriedades do componente atualmente selecionado no editor. Este é o modo padrão do painel de componentes quando uma página é carregada.

![Modo de propriedades](assets/properties-mode.png)

Os detalhes do componente selecionado são mostrados no painel. Observe que nem todos os componentes precisam ser mostrados.

![Detalhes do componente](assets/component-details.png)

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

Basta tocar ou clicar no conteúdo na caixa azul para iniciar um editor local que permite fazer as alterações. Pressione Enter ou Return para salvar as alterações.

![Editar o conteúdo](assets/editing-content.png)

Observe que, no modo de edição, tocar ou clicar no conteúdo tenta selecioná-lo para edição. Se você deseja navegar pelo seu conteúdo utilizando os links, alterne para o [modo de visualização.](#preview-mode)

Dependendo do modo em que estiver e do conteúdo selecionado, você pode ter opções de edição diferentes no local. Além disso, talvez seja possível revisar propriedades adicionais para o conteúdo usando o [painel de componentes.](#component-rail)

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
