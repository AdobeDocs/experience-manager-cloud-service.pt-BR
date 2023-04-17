---
title: Criação de conteúdo com o Editor universal
description: Saiba como é fácil e intuitivo para os autores criarem conteúdo utilizando o Editor universal.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: ht
source-wordcount: '1152'
ht-degree: 100%

---


# Criação de conteúdo com o Editor universal {#authoring}

Saiba como é fácil e intuitivo para os autores criarem conteúdo utilizando o Editor universal.

## Introdução {#introduction}

O Editor universal permite editar qualquer aspecto do conteúdo das implementações, a fim de entregar experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvedor de última geração.

Para isso, ele fornece aos autores de conteúdo uma interface intuitiva que requer o mínimo de treinamento possível, permitindo simplesmente avançar e começar a editar o conteúdo.

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
>Consulte o documento [Introdução ao Editor universal no AEM](getting-started.md) para obter um exemplo de como configurar um aplicativo do AEM para funcionar com o Editor universal.

## Fazer logon {#sign-in}

Após o aplicativo ser instrumentado para funcionar com o Editor universal, será necessário fazer logon no Editor universal. Você precisará de uma Adobe ID para fazer logon e [ter acesso ao Editor universal.](getting-started.md#request-access)

Depois de fazer logon, insira o URL da página que deseja editar na [barra de endereços.](#address-bar) para começar a [editar o conteúdo.](#edit-content)

## Entenda a interface {#ui}

A interface é dividida em quatro áreas principais.

* [O cabeçalho da Experience Cloud](#experience-cloud-header)
* [O cabeçalho do Editor universal](#universal-editor-header)
* [O painel](#rail)
* [O editor](#editor)

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

Esse ícone será marcado com o número de [notificações](/help/implementing/cloud-manager/notifications.md) incompletas atribuídas atualmente.

![Notificações](assets/notifications.png)

#### Propriedades do usuário {#user-properties}

Toque ou clique no ícone que representa seu usuário para acessar suas configurações de usuário. Se você não tiver uma imagem de usuário configurada, um ícone será atribuído aleatoriamente.

![Propriedades do usuário](assets/user-properties.png)

### O cabeçalho do Editor universal {#universal-editor-header}

O cabeçalho do Editor universal está sempre presente na parte superior da tela, logo abaixo [do cabeçalho da Experience Cloud.](#experience-cloud-header) Ele fornece acesso rápido para navegar para outra página a ser editada, bem como para publicar a página atual.

![O cabeçalho do Editor universal](assets/universal-editor-header.png)

#### O menu de opções {#hamburger-menu}

O menu de opções ainda não foi implementado.

![Menu de opções](assets/hamburger-menu.png)

#### Barra de localização {#Location-bar}

A barra de localização mostra o endereço da página que você está editando. Toque ou clique para inserir o endereço de outra página para editar.

![Barra de localização](assets/address-bar.png)

>[!TIP]
>
>Use a tecla de atalho `L` para abrir a barra de endereços.

>[!NOTE]
>
>Qualquer página que você deseja editar com o Editor universal deve ser [instrumentada para oferecer suporte ao Editor universal.](getting-started.md)

#### Abrir visualização do aplicativo {#open-app-preview}

Toque ou clique no ícone Abrir visualização do aplicativo para abrir a página que você está editando no próprio navegador (fora do editor) e visualizar as alterações.

![Abrir visualização do aplicativo](assets/open-app-preview.png)

>[!TIP]
>
>Use a tecla de atalho `O` para abrir a visualização do aplicativo.

#### Publicação {#publish}

Toque ou clique no botão de publicação para que as alterações sejam publicadas no conteúdo ativo para os seus leitores.

![Botão de publicação](assets/publish.png)

>[!TIP]
>
>Consulte o documento [Publicação de conteúdo com o Editor visual universal](publishing.md) para obter mais informações sobre a publicação com o Editor universal.

### O painel {#rail}

O painel está sempre presente no lado esquerdo do editor. Isso permite alternar facilmente o editor entre o modo de visualização e o modo de edição.

![O painel](assets/rail.png)

#### Modo de visualização {#preview-mode}

No modo de visualização, a página é renderizada no editor da maneira como seria vista em seu serviço publicado. Isso permite que o autor de conteúdo navegue pelo conteúdo clicando em links etc.

![Modo de visualização](assets/preview-mode.png)

>[!TIP]
>
>Use a tecla de atalho `P` para alternar para o modo de visualização.

#### Modo de edição {#edit-mode}

No modo de edição, a página é renderizada no editor, mas o autor de conteúdo pode clicar e selecionar o conteúdo para editar. Esse é o modo padrão do editor quando uma página é carregada.

![Modo de edição](assets/edit-mode.png)

### O editor {#editor}

O editor ocupa a maior parte da janela e é renderizado na página especificada na [barra de endereços](#address-bar).

Dependendo de se o editor está em [modo de edição](#edit-mode) ou [modo de visualização,](#edit-mode) o conteúdo será editável ou navegável, respectivamente.

![Editor](assets/editor.png)

## Editar o conteúdo {#editing-content}

A edição de conteúdo é simples e intuitiva. No [modo de edição,](#edit-mode) ao passar o mouse sobre o conteúdo no editor, o conteúdo editável será destacado com uma caixa azul.

![O conteúdo editável é destacado por uma caixa azul](assets/editable-content.png)

Basta tocar ou clicar no conteúdo na caixa azul para iniciar um editor local que permite fazer as alterações. Pressione Enter ou Return para salvar as alterações.

![Editar o conteúdo](assets/editing-content.png)

Observe que, no modo de edição, tocar ou clicar no conteúdo tenta selecioná-lo para edição. Se você deseja navegar pelo seu conteúdo utilizando os links, alterne para o [modo de visualização.](#preview-mode)

## Visualização de conteúdo {#previewing-content}

Ao terminar de editar o conteúdo, você geralmente deseja navegar por ele e observar como ele é exibido em outras páginas. No [modo de visualização](#preview-mode), é possível clicar em links e navegar pelo conteúdo, como um leitor faria. O conteúdo é renderizado no editor como seria publicado.

Note que, no modo de visualização, a ação de tocar ou clicar no conteúdo funciona da mesma forma que para um leitor do conteúdo. Se desejar selecionar o conteúdo para edição, alterne para o [modo de edição.](#edit-mode)

## Recursos adicionais {#additional-resources}

Para saber mais sobre o Editor universal, consulte estes documentos.

* [Introdução ao Editor universal](introduction.md): saiba como o Editor universal permite editar qualquer aspecto do conteúdo das implementações, a fim de entregar experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvedor de última geração.
* [Publicação de conteúdo com o Editor universal](publishing.md): saiba como o Editor visual universal publica o conteúdo e como seus aplicativos podem lidar com esse conteúdo.
* [Introdução ao Editor universal no AEM](getting-started.md): saiba como obter acesso ao Editor universal e começar a instrumentar seu primeiro aplicativo do AEM para utilizá-lo.
* [Arquitetura do Editor universal](architecture.md): saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.
* [Atributos e tipos](attributes-types.md): saiba mais sobre os atributos e tipos de dados exigidos pelo Editor universal.
* [Autenticação do Editor universal](authentication.md): saiba como funciona a autenticação do Editor universal.
