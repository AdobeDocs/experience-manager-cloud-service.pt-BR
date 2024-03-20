---
title: Manuseio básico
description: Acostume-se com a navegação pelo AEM e seu uso básico
exl-id: ae87a63a-c6d3-4220-ab3d-07a20b21b93b
source-git-commit: 7e0ca5dad5cd53c2304e2eba48a5131d587967ef
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 63%

---


# Manuseio básico {#basic-handling}

Este documento foi projetado para fornecer uma visão geral do manuseio básico ao usar o ambiente de autor do AEM.

>[!TIP]
>
>Atalhos de teclado estão disponíveis em todo o AEM. Em especial, quando [uso do console sites](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) e [o editor de páginas](/help/sites-cloud/authoring/page-editor/keyboard-shortcuts.md).

{{edge-delivery-authoring}}

## Uma interface de usuário habilitada para toque {#a-touch-enabled-ui}

A interface do usuário do AEM é habilitada para toque. Uma interface habilitada para toque permite que você use toques para interagir com o software por meio de gestos, como tocar, tocar e segurar e deslizar o dedo. Como a interface do usuário do AEM é habilitada para toque, você pode usar os gestos de toque nos dispositivos de toque, como celular ou tablet. No entanto, as ações do mouse em um dispositivo de desktop tradicional também estão disponíveis, o que proporciona flexibilidade na maneira como você escolhe criar conteúdo.

## Primeiras etapas {#first-steps}

Logo após o logon, você acessa o [painel de Navegação](#navigation-panel). Selecionar uma das opções abre o respectivo console.

![Painel Navegação](assets/basic-handling-navigation.png)

Para obter uma boa compreensão do uso básico do AEM, este documento se baseia no console de **Sites.** Selecionar em **Sites** para começar.

## Navegação do produto   {#product-navigation}

Sempre que um usuário acessa um console pela primeira vez, um tutorial de navegação de produto é iniciado. Reserve um minuto para fazer uma seleção e obter uma boa visão geral do tratamento básico do AEM.

![Tutorial de navegação](assets/basic-handling-tutorial.png)

Selecionar **Próxima** para avançar para a próxima página da visão geral. Selecionar **Fechar** ou selecione fora da caixa de diálogo de visão geral para fechar.

A visão geral será reiniciada na próxima vez que você acessar um console a menos que visualize todos os slides ou marque a opção **Não mostrar esta mensagem novamente**.

## Navegação global {#global-navigation}

É possível navegar entre os consoles usando o painel de navegação global. É acionado como um menu suspenso de tela cheia ao selecionar o **Adobe Experience Manager** no canto superior esquerdo da tela.

Você pode fechar o painel de navegação global clicando ou tocando em **Fechar** para retornar ao seu local anterior.

![Barra superior do painel Navegação](assets/basic-handling-navigation-options.png)

A navegação global possui dois painéis, representados por ícones na margem esquerda da tela:

* **[Navegação](#navigation-panel)** - Representado por uma bússola e o painel padrão ao fazer logon no AEM
* **[Ferramentas](#tools-panel)**: representadas por um martelo

As opções disponíveis nesses painéis estão descritas abaixo.

### Painel Navegação   {#navigation-panel}

A variável **Navegação** painel:

![Painel Navegação](assets/basic-handling-navigation.png)

O título da guia do navegador será atualizado para refletir sua localização à medida que você navega pelos consoles e conteúdo.

Em Navegação, os consoles disponíveis são:

| Console | Propósito |
|---|---|
| Projetos | O console Projetos concede acesso direto aos projetos. [Projetos são painéis virtuais](/help/sites-cloud/authoring/projects/overview.md) que podem ser usados para criar uma equipe. Você pode conceder a essa equipe acesso a recursos, fluxos de trabalho e tarefas, permitindo que as pessoas trabalhem por um objetivo comum. |
| Sites | [O console Sites](/help/sites-cloud/authoring/sites-console/introduction.md) O permite criar, exibir e gerenciar sites em execução na sua instância do AEM. Por meio desse console, você pode criar, copiar, mover e excluir páginas, iniciar fluxos de trabalho e publicar páginas. |
| Fragmentos de experiência | Um [Fragmento de experiência](/help/sites-cloud/authoring/fragments/content-fragments.md) é uma experiência independente que pode ser reutilizada em vários canais e que apresenta variações, evitando o trabalho de copiar e colar repetidamente as experiências ou partes das experiências. |
| Ativos | O console de Ativos permite importar e gerenciar [ativos digitais como imagens, vídeos, documentos e arquivos de áudio. ](/help/assets/overview.md) Esses ativos podem ser usados por um site em execução na mesma instância do AEM. Também é possível criar e gerenciar [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) no console de Ativos. |
| Personalização | Esse console fornece uma estrutura de ferramentas para a [criação de conteúdo direcionado e a apresentação de experiências personalizadas](/help/sites-cloud/authoring/personalization/overview.md). |
| Fragmentos de conteúdo | [Os fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md) permitem projetar, criar, preparar e publicar conteúdo independente de página. Eles permitem preparar conteúdo estruturado pronto para uso em vários locais/canais e são ideais para a criação de páginas e entrega headless. |

## Painel Ferramentas {#tools-panel}

No **Ferramentas** O painel tem um painel lateral que contém um intervalo de categorias que agrupa consoles semelhantes. A variável **Ferramentas** Os consoles fornecem acesso a várias ferramentas e consoles especializados que ajudam a administrar seus sites, ativos digitais e outros aspectos do seu repositório de conteúdo. <!--The [Tools consoles](/help/sites-administering/tools-consoles.md) provide access to several specialized tools and consoles that help you administer your websites, digital assets, and other aspects of your content repository.-->

![Painel Ferramentas](assets/basic-handling-tools.png)

## O Cabeçalho {#the-header}

O cabeçalho está sempre presente na parte superior da tela. Embora a maioria das opções no cabeçalho permaneça a mesma, independentemente de onde você esteja no sistema, algumas são específicas do contexto.

![Cabeçalho de navegação](/help/sites-cloud/authoring/assets/basic-handling-navigation-bar.png)

* [Navegação global](#global-navigation) - Selecione o **Adobe Experience Manager** link para navegar entre consoles.

  ![Navegação global](/help/sites-cloud/authoring/assets/basic-handling-global-navigation.png)

* Feedback

  ![Botão Feedback](/help/sites-cloud/authoring/assets/basic-handling-feedback.png)

* Sua organização IMS - selecione para alterar se necessário.

* [Soluções](https://www.adobe.com/br/experience-cloud.html) - Selecione esta opção para acessar suas outras soluções de Adobe.

  ![Botão Soluções](/help/sites-cloud/authoring/assets/basic-handling-solutions.png)

* [Pesquisar](/help/sites-cloud/authoring/search.md) - Você também pode usar o [tecla de atalho](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) `/` (barra) para invocar a pesquisa em qualquer console.

  ![Ícone de Pesquisa](/help/sites-cloud/authoring/assets/basic-handling-search-icon.png)

* [Ajuda](#accessing-help)

  ![Botão Ajuda](/help/sites-cloud/authoring/assets/basic-handling-help-icon.png)

* [Notificação](/help/sites-cloud/authoring/inbox.md) - Esse ícone contém o número de notificações incompletas atribuídas atualmente.

  ![Botão Notificações](/help/sites-cloud/authoring/assets/basic-handling-notifications.png)

* [Propriedades do usuário](/help/sites-cloud/authoring/account-environment.md) - Selecione esta opção para alterar as configurações do usuário.

  ![Botão Propriedades do usuário](/help/sites-cloud/authoring/assets/basic-handling-user-properties.png)

## Acessar ajuda   {#accessing-help}

Há vários recursos de ajuda disponíveis e algumas maneiras de acessá-los.

* **Barra de ferramentas** - Dependendo da sua localização, a variável **Ajuda** ícone abre os recursos apropriados:

  ![Ícone da ajuda](assets/basic-handling-help.png)

* **Console** - Na primeira vez que você navegar pelo sistema, [uma série de slides apresenta a navegação pelo AEM](#product-navigation).

  ![Tutorial](assets/basic-handling-console-tutorial.png)

* **Editor de páginas** - Na primeira vez que você edita uma página, uma série de slides apresenta o editor de páginas.

  ![Tutorial do editor](assets/basic-handling-editor-tutorial.png)

   * Navegue por essa visão geral como faria com a [visão geral de navegação do produto](#product-navigation) ao acessar qualquer console pela primeira vez.
   * No menu [**Informações da página,** é possível selecionar **Ajuda**](#accessing-help) para exibir isso novamente, a qualquer momento.

* **Console de ferramentas** - No **Ferramentas** console, você também pode acessar o console externo **Recursos**:

   * **Documentação** - exibir a documentação do Adobe® Experience Manager
   * **Recursos do desenvolvedor** - recursos e downloads do desenvolvedor

>[!TIP]
>
>É possível acessar uma visão geral das teclas de atalho disponíveis a qualquer momento, usando a tecla de atalho `?` (ponto de interrogação) em um console.
>
>Para obter uma visão geral de todos os atalhos de teclado, consulte a seguinte documentação:
>
>* [Atalhos de teclado para editar páginas](/help/sites-cloud/authoring/page-editor/keyboard-shortcuts.md)
>* [Atalhos de teclado para os consoles](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)
