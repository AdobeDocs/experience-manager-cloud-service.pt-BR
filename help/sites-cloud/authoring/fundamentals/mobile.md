---
title: Criação de uma página para dispositivos móveis
description: Ao publicar conteúdo para dispositivos móveis, será possível alternar entre vários emuladores para ver o que o usuário final verá
exl-id: fabd4468-3304-402f-9522-342da3bbae94
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '267'
ht-degree: 100%

---

# Criação de uma página para dispositivos móveis    {#authoring-a-page-for-mobile-devices}

As páginas do Adobe Experience Manager são baseadas em um layout responsivo. [O layout responsivo adapta o conteúdo para ajustá-lo automaticamente ao dispositivo de destino, eliminando a necessidade de criar conteúdo para dispositivos específicos.](/help/sites-cloud/authoring/features/responsive-layout.md)

Ao criar uma página para dispositivos móveis, a página será exibida de uma forma que emula o dispositivo móvel. Ao criar a página, será possível alternar entre vários emuladores para ver o que o usuário final verá ao acessá-la.

Os dispositivos são agrupados nas recurso de categorias, inteligente e de toque, de acordo com as capacidades dos dispositivos que renderizarão a página. Quando o usuário final acessa uma página para dispositivos móveis, o AEM detectará o dispositivo e enviará a representação que corresponde ao seu grupo de dispositivos.

>[!NOTE]
>
>Para criar um site para dispositivos móveis com base em um site padrão já existente, crie uma live copy do site padrão. Consulte [Criar Live Copies](/help/sites-cloud/administering/msm/creating-live-copies.md).
>
>Os desenvolvedores do AEM podem criar novos grupos de dispositivos. Consulte Criação de filtros de grupos de dispositivos.

<!--
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

Use o procedimento a seguir para criar uma página para dispositivos móveis:

1. Na navegação global, abra o console **Sites**.
1. Edite uma página de conteúdo.
1. Alterne para o emulador desejado, clicando no ícone de **Emulador** na parte superior da página.

   ![Ícone de Emulador](/help/sites-cloud/authoring/assets/emulator.png)

1. Arraste e solte os componentes do navegador de componentes ou do navegador de ativos na página.
1. [Modifique o layout responsivo](/help/sites-cloud/authoring/features/responsive-layout.md) da página e seus componentes com base no dispositivo selecionado.

A página será semelhante ao seguinte:

![Exemplo de dispositivo móvel](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>Os emuladores são desativados quando uma página na instância de autor é solicitada em um dispositivo móvel.
