---
title: Ativar proteção de hotlink no Dynamic Media
description: Saiba como ativar a proteção de hotlink no Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 9%

---

# Ativar proteção de hotlink no Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Hot linking é quando um site de terceiros usa o código de HTML para exibir uma imagem de seu site. Eles usam sua largura de banda toda vez que a imagem é solicitada, pois o navegador do visitante a está acessando diretamente do seu servidor. Hotlink *proteção* é um método para impedir que outros sites vinculem diretamente a imagens, CSS ou JavaScript nas suas páginas da Web. Esse tipo de blindagem ajuda a reduzir o uso desnecessário da largura de banda em sua conta do Dynamic Media.

[Suporte ao cliente Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=pt-BR#home) Você pode configurar um filtro de referenciador no nível da CDN. Isso garante que o conteúdo do Dynamic Media seja veiculado somente em sites da sua lista de sites permitidos para o domínio.

>[!NOTE]
>
>Esse recurso exige que você use a CDN predefinida fornecida com o Adobe Experience Manager Dynamic Media. Nenhum outro CDN personalizado é compatível com esse recurso. Para ativar a proteção de hot link, um administrador deve criar um tíquete de suporte para solicitar a alteração da configuração na sua conta do Dynamic Media. Não há custo adicional para ativar a proteção de hot link.
