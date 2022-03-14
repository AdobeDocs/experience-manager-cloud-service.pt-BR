---
title: Personalização e direcionamento de conteúdo
description: Saiba como AEM pode criar conteúdo personalizado
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 83%

---

# Personalização e direcionamento de conteúdo {#personalization}

## Personalização e direcionamento de conteúdo {#personalization-and-content-targeting}

O AEM fornece uma estrutura de ferramentas para criar conteúdo direcionado e apresentar experiências personalizadas.

## Modo Direcionar {#targeting-mode}

[Crie conteúdo direcionado usando o modo Direcionar do AEM. ](/help/sites-cloud/authoring/personalization/targeted-content.md) O modo de direcionamento e o componente do Target fornecem ferramentas para criar conteúdo para as experiências das suas atividades de marketing.

## Atividades {#activities}

Atividades definem e organizam seus esforços de marketing. Elas abrangem os públicos que você está direcionando e o período em que a o direcionamento é aplicado.

Por exemplo, seu catálogo de produtos pode incluir teasers que focalizam a atenção em produtos sazonais. A atividade Esportes de verão define os segmentos de marketing direcionados pelos teasers durante os meses de verão.

Atividades também identificam o [mecanismo de direcionamento](#targeting-engine) usado por suas páginas.

Use o [Console de atividades](/help/sites-cloud/authoring/personalization/activities.md) para criar e gerenciar as atividades das suas marcas. Você também pode criar atividades ao [criar conteúdo direcionado](/help/sites-cloud/authoring/personalization/targeted-content.md).

## Experiências {#experiences}

Para cada atividade, você define uma ou mais experiências que identificam os públicos que estão sendo direcionados. O AEM permite que você controle o conteúdo que compreende cada experiência.

Os públicos se baseiam em segmentos de marketing criados no AEM ou no Adobe Target. Quando um visitante abre uma página da Web, a lógica da página determina o público ao qual ele pertence e exibe o conteúdo que você criou para esse público.

Por exemplo, uma atividade define experiências para dois públicos separados: mulheres com mais de 30 anos e mulheres com menos de 30 anos. A página feminina de um site da Web pode exibir produtos diferentes para cada experiência.

Você define experiências para uma atividade. É possível usar o [console Atividades](/help/sites-cloud/authoring/personalization/activities.md#adding-editing-an-activity-using-the-activities-console) ou o [modo Direcionar](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode) para adicionar experiências a uma atividade.

## Ofertas {#offers}

Uma oferta é um conteúdo que aparece em uma localização em uma página para uma experiência. Use ofertas diferentes para experiências diferentes para maximizar a eficácia do conteúdo para os seus públicos.

Por exemplo, a página para mulheres de um site de exemplo pode usar ofertas como a imagem de teaser que aparece na parte superior da página. Uma oferta diferente é usada como teaser para a experiência Mulheres acima de 30 anos e para a experiência Mulheres com menos de 30 anos.

Use o [console Ofertas](/help/sites-cloud/authoring/personalization/offers.md) para criar ofertas que você possa usar em várias experiências. Crie ofertas de uso único ou adicione ofertas de uma biblioteca de ofertas ao [criar conteúdo direcionado](/help/sites-cloud/authoring/personalization/targeted-content.md).

## Mecanismo de direcionamento {#targeting-engine}

O mecanismo de direcionamento é o mecanismo que orienta a lógica do conteúdo segmentado. [Atividades](/help/sites-cloud/authoring/personalization/activities.md) são configuradas para usar um dos dois mecanismos de segmentação disponíveis: AEM e Adobe Target.

### AEM {#aem}

O AEM fornece um mecanismo de direcionamento integrado que processa solicitações de página e determina o conteúdo a ser exibido. Ao usar o mecanismo de direcionamento do AEM, você está limitado a usar segmentos criados no AEM para definir os públicos das suas experiências.

### Adobe Target {#adobe-target}

O mecanismo de direcionamento do Adobe Target faz com que as informações coletadas das visitas às páginas sejam rastreadas no Adobe Target.

* Ao usar esse mecanismo de direcionamento, você usa segmentos importados do Adobe Target para definir os públicos das suas experiências.
* As atividades que usam o mecanismo do Adobe Target são [sincronizadas com o Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

Você pode usar esse mecanismo quando tiver integrado com o Adobe Target. <!--You can use this engine when you have [integrated with Adobe Target](/help/sites-administering/opt-in.md).-->
