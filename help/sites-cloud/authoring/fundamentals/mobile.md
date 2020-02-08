---
title: Criação de uma página para dispositivos móveis
description: Ao criar em dispositivos móveis, você pode alternar entre vários emuladores para ver o que o usuário final vê
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Criação de uma página para dispositivos móveis {#authoring-a-page-for-mobile-devices}

As páginas do Adobe Experience Manager são baseadas em um layout responsivo. O layout responsivo adapta seu conteúdo para ajustá-lo automaticamente ao dispositivo de destino, eliminando a necessidade de criar conteúdo para dispositivos específicos.

Ao criar uma página para dispositivos móveis, a página é exibida de uma maneira que emula o dispositivo móvel. Ao criar a página, você pode alternar entre vários emuladores para ver o que o usuário final vê ao acessar a página.

Os dispositivos são agrupados nas categorias Recurso, Inteligente e Toque, de acordo com as capacidades dos dispositivos de renderizar uma página. Quando o usuário final acessa uma página para dispositivos móveis, o AEM detecta o dispositivo e envia a representação que corresponde ao seu grupo de dispositivos.

>[!NOTE]
>
>Para criar um site móvel com base em um site padrão existente, crie uma live copy do site padrão. Consulte Criação de uma Live Copy para diferentes canais.
>
>Os desenvolvedores do AEM podem criar novos grupos de dispositivos. Consulte Criação de filtros de grupo de dispositivos.
<!--
>To create a mobile site based on an existing standard site, create a live copy of the standard site. (See [Creating a Live Copy for Different Channels](/help/sites-administering/msm-livecopy.md).)
>
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

Use o procedimento a seguir para criar uma página para dispositivos móveis:

1. From global navigation open the **Sites** console.
1. Edite uma página de conteúdo.
1. Switch to the desired emulator by clicking the **Emulator** icon at the top of the page.

   ![Ícone Emulador](/help/sites-cloud/authoring/assets/emulator.png)

1. Arraste e solte componentes do navegador de componentes ou do navegador de ativos na página.
1. [Modifique o layout](/help/sites-cloud/authoring/features/responsive-layout.md) responsivo da página e seus componentes com base no dispositivo selecionado.

A página será semelhante ao seguinte:

![Exemplo de dispositivo móvel](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>Os emuladores são desativados quando uma página na instância de autor é solicitada em um dispositivo móvel.
