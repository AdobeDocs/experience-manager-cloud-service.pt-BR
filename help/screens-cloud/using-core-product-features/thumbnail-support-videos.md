---
title: Suporte a miniaturas para vídeos no Screens as a Cloud Service
description: Esta página descreve como adicionar suporte a miniaturas para vídeos no Screens as a Cloud Service.
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# Suporte a miniaturas para vídeos {#thumbnail-support-videos}

## Introdução {#introduction}

Um autor de conteúdo pode definir uma miniatura de vídeos para que a imagem possa ser usada como um espaço reservado e testar corretamente a reprodução e o direcionamento do conteúdo, enquanto o vídeo real está sendo finalizado pela equipe apropriada. A imagem também pode ser usada caso a reprodução do vídeo falhe.

A adição de suporte para uma imagem em miniatura no componente de vídeo permite que o cliente adicione corretamente um componente válido no canal, com conteúdo real, e execute qualquer configuração de direcionamento antes que o vídeo seja realmente entregue.

>[!NOTE]
>A imagem em miniatura, se definida no componente de vídeo, é reproduzida em caso de falha na reprodução do vídeo no reprodutor. Isso permite enviar a mensagem desejada para o público-alvo (reproduzindo o conteúdo) em vez de ignorá-la completamente.

O Suporte a miniaturas permite:

* Prepare uma experiência de canal quando os vídeos ainda não estiverem prontos ou quando você não quiser necessariamente testar um download de um grande ativo nos reprodutores

* Defina um mecanismo de fallback, caso haja problemas de reprodução no dispositivo.

## Utilização de miniaturas em vídeos {#using-thumbnails}

>[!IMPORTANT]
>**Pré-requisitos**
>Antes de saber como usar miniaturas para vídeos, saiba como criar representações de vídeo para canais no projeto Screens as a Cloud Service. Consulte [aqui](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md) para obter mais detalhes.

Siga as etapas abaixo para usar a miniatura em vídeos:

1. Navegue até um canal do Screens existente ou crie um novo canal.

   >[!NOTE]
   >Para saber como criar um canal e adicionar conteúdo a um canal, consulte [Criação e gerenciamento de um canal no Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en).

1. Selecione o canal e clique em **Editar** na barra de ações para abrir o editor.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. Adicione ou edite um componente de vídeo existente, como mostrado na figura abaixo.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. Selecione o vídeo e clique no botão *chave inglesa* ícone para abrir as propriedades do vídeo.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. A variável **Vídeo** será aberta, onde você exibirá a **Miniatura** área de lançamento.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. Arraste e solte uma imagem do seletor de ativos para a **Miniatura** área designada e clique em **Concluído**.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. Clique em **Visualizar**.

1. Se um vídeo estiver definido no componente, ele será reproduzido. Caso contrário, e a miniatura estiver definida, a miniatura será reproduzida. Caso contrário, o componente será considerado não configurado e será ignorado.

## Casos de uso compatíveis ao usar a miniatura em vídeos {#understand-use-case}

A miniatura em vídeos oferece suporte aos seguintes casos de uso:

* Um componente de vídeo sem nada configurado será ignorado.

* Um componente de vídeo com apenas o conjunto de miniaturas reproduzirá a miniatura.

* Um componente de vídeo com o vídeo (se o vídeo tiver a representação correta) e o conjunto de miniaturas reproduzirá o vídeo.

* Um componente de vídeo com o conjunto de vídeos reproduzirá a miniatura, em caso de erro de reprodução, ou pulará para o próximo item, caso a miniatura não esteja configurada.
