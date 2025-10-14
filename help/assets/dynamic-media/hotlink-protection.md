---
title: Ativar proteção de hotlink no Dynamic Media
description: Saiba como ativar a proteção de hotlink no Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---

# Ativar proteção de hotlink no Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Hot linking é quando um site de terceiros usa o código HTML para exibir uma imagem do seu site. Eles usam a largura de banda sempre que a foto é solicitada porque o navegador do visitante está acessando-a diretamente do seu servidor. A *proteção* do Hotlink é um método para impedir que outros sites vinculem diretamente a imagens, CSS ou JavaScript nas suas páginas da Web. Esse tipo de blindagem ajuda a reduzir o uso desnecessário da largura de banda na conta do Dynamic Media.

O [Suporte ao Cliente da Adobe](https://experienceleague.adobe.com/pt-br?support-solution=Experience+Manager&lang=pt-BR#home) pode configurar um filtro de referenciador no nível de CDN. Isso garante que o conteúdo do Dynamic Media seja enviado somente aos sites da lista de sites permitidos no domínio.

>[!NOTE]
>
>Esse recurso exige o uso da CDN pronta para uso que é fornecida com o Adobe Experience Manager Dynamic Media. Qualquer outra CDN personalizada não é compatível com esse recurso. Para ativar a proteção de hot link, um administrador precisa criar um tíquete de suporte para solicitar a alteração de configuração em sua conta do Dynamic Media. Não há custo adicional para ativar a proteção de hot link.
