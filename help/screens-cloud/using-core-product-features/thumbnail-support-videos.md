---
title: Suporte a miniaturas para vídeos no Screens as a Cloud Service
description: Esta página descreve como adicionar suporte de miniatura a vídeos no Screens as a Cloud Service.
hide: true
index: false
source-git-commit: ea96e811c0164e3cc7d323e734c1617d3c0e9308
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Suporte a miniaturas para vídeos {#thumbnail-support-videos}

## Introdução {#introduction}

Um autor de conteúdo pode definir uma miniatura de vídeos para que a imagem possa ser usada como um espaço reservado e testar corretamente a reprodução e o direcionamento do conteúdo, enquanto o vídeo real está sendo finalizado pela equipe apropriada. A imagem também pode ser usada caso a reprodução do vídeo falhe.

Adicionar suporte para uma imagem em miniatura no componente de vídeo permite que o cliente adicione corretamente um componente válido no canal, com conteúdo real, e execute qualquer configuração de definição de metas antes que o vídeo seja realmente entregue.

>[!NOTE]
>A imagem em miniatura, se configurada no componente de vídeo, é reproduzida em caso de falha na reprodução do vídeo no reprodutor. Isso permite fornecer a mensagem desejada ao público-alvo (reproduzindo o conteúdo) em vez de ignorá-la completamente.

O suporte a miniaturas permite:

* Prepare uma experiência de canal quando os vídeos ainda não estiverem prontos ou quando você não quiser necessariamente testar um download de ativo grande nos players

* Defina um mecanismo de fallback, caso haja problemas de reprodução no dispositivo.

## Usar miniaturas em vídeos {#using-thumbnails}

Siga as etapas abaixo para usar a miniatura em vídeos:

1. Navegue até um canal existente do Screens ou crie um novo canal.

   >[!NOTE]
   >Para saber como criar um canal e adicionar conteúdo a um canal, consulte [Criação e gerenciamento de um canal no Screens como um Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en).

1. Selecione o canal e clique em **Editar** na barra de ações para abrir o editor.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. Adicione ou edite um componente de vídeo existente, conforme mostrado na figura abaixo.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. Edite as propriedades do componente de vídeo.

1. Arraste uma imagem do seletor de ativos para a área de soltar Miniaturas .

1. Visualize o canal.

1. Se um vídeo estiver definido no componente, ele será reproduzido. Caso contrário, e a miniatura estiver definida, a miniatura será reproduzida. Caso contrário, o componente será considerado não configurado e será ignorado

## Casos de uso suportados ao usar miniatura em vídeos {#understand-use-case}

Consulte os seguintes casos de uso ao usar miniatura em vídeos.

Um componente de vídeo com:

* *nenhuma* configuração será ignorada

* *somente o conjunto de miniaturas* reproduzirá a miniatura

* *vídeo e miniatura* serão reproduzidos

* *a configuração de vídeo* reproduzirá a miniatura se houver um erro de reprodução ou simplesmente pulará para o próximo item caso a miniatura não esteja configurada
