---
title: Visão geral do Content Hub
description: Saiba mais sobre o Content Hub, seus principais benefícios, como acessá-lo e como fornecer feedback sobre as opções disponíveis nele.
exl-id: c5908058-f1ad-4aaa-9e8e-c0157e107ed1
source-git-commit: 797d1e275bcb8e949171d322871b377582e72a71
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 5%

---

# Visão geral do Content Hub {#overview-content-hub}

O Content Hub está disponível como parte do Experience Manager Assets as a Cloud Service para democratizar o acesso a conteúdo sobre a marca para organizações e seus parceiros de negócios. Ele se concentra na distribuição de ativos para ativação em escala e criação de variantes de conteúdo na marca para melhorar a agilidade de marketing.

## Demonstração do Content Hub {#content-hub-demo}

>[!IMPORTANT]
>
>[O Assets Ultimate](/help/assets/assets-ultimate-overview.md) e o Assets as a Cloud Service incluem 250 usuários limitados da Content Hub. [Assets Prime](/help/assets/assets-prime.md) inclui 50 usuários com limitações da Content Hub.

>[!VIDEO](https://video.tv.adobe.com/v/3463712)

## Por que Content Hub?

A Content Hub oferece os seguintes benefícios principais:

**Localize e compartilhe todos os ativos aprovados pela marca disponíveis em um portal intuitivo**

O AEM Assets serve como uma única fonte da verdade e todos os ativos aprovados são disponibilizados automaticamente no Content Hub em uma hierarquia simples para melhorar a experiência de pesquisa.

**Interface de usuário configurável**

As propriedades mais comuns no Content Hub, como filtros de pesquisa, campos disponíveis ao adicionar ou importar ativos, propriedades de ativos, conteúdo de banner para marca são configuráveis e um administrador pode configurar facilmente a interface do usuário do Content Hub com base em seus requisitos.

**Capacite os usuários não criativos a editar e remixar conteúdo enquanto permanecem na marca**

O Content Hub permite criar novo conteúdo com o Adobe Express (se você tiver direitos ao Adobe Express). Você pode editar o conteúdo existente com ferramentas fáceis de usar, produzir variações na marca com modelos e elementos da marca e criar novo conteúdo com os recursos mais recentes da GenAI da Adobe Firefly.

## Pré-requisitos {#prerequisites-content-hub}

O Content Hub requer um ambiente de autor de produção do Experience Manager as a Cloud Service versão 2024.6 ou mais recente (a versão mínima é 2024.6.16799).

## Como acessar o Content Hub? {#access-content-hub}

[Após configurar o Content Hub](/help/assets/deploy-content-hub.md) e adicionar um usuário ao [perfil de produto do Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile), o Content Hub pode ser acessado das seguintes maneiras:

* Acesse o Content Hub usando o seguinte link:

  `https://experience.adobe.com/#/assets/contenthub`

* Faça logon em [experience.adobe.com](https://auth.services.adobe.com/en_GB/index.html?callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fadobeid%2Fexc_app%2FAdobeID%2Ftoken%3Fredirect_uri%3Dhttps%253A%252F%252Fexperience.adobe.com%252F%2523old_hash%253Dold_hash%253D%252523%25252F%2526from_ims%253Dtrue%253Fclient_id%253Dexc_app%2526api%253Dauthorize%2526scope%253Dab.manage%252Caccount_cluster.read%252Cadditional_info%252Cadditional_info.job_function%252Cadditional_info.projectedProductContext%252Cadditional_info.roles%252CAdobeID%252Cadobeio.appregistry.read%252Cadobeio_api%252Caudiencemanager_api%252Ccreative_cloud%252Cmps%252Copenid%252Corg.read%252Cpps.read%252Cread_organizations%252Cread_pc%252Cread_pc.acp%252Cread_pc.dma_tartan%252Csession%26state%3D%257B%2522jslibver%2522%253A%2522v2-v0.31.0-2-g1e8a8a8%2522%252C%2522nonce%2522%253A%25222316022399331147%2522%257D%26code_challenge_method%3Dplain%26use_ms_for_expiry%3Dtrue&client_id=exc_app&scope=ab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&state=%7B%22jslibver%22%3A%22v2-v0.31.0-2-g1e8a8a8%22%2C%22nonce%22%3A%222316022399331147%22%7D&relay=64da7fa8-cd9e-47cf-9892-7f3ef3092f8c&locale=en_GB&flow_type=token&dctx_id=v%3A2%2Cs%2Cf%2Cb8e64530-b013-11ee-a6c1-e721bdec0171&idp_flow_type=login&response_type=token&profile_filter=%7B%22findFirst%22%3Atrue%2C+%22fallbackToAA%22%3Atrue%2C+%22preferForwardProfile%22%3Atrue%2C+%22searchEntireCluster%22%3Atrue%7D%3B+isOwnedByOrg%28%2776B329395DF155D60A495E2C%40AdobeOrg%27%29&code_challenge_method=plain&redirect_uri=https%3A%2F%2Fexperience.adobe.com%2F%23old_hash%3Dold_hash%3D%2523%252F%26from_ims%3Dtrue%3Fclient_id%3Dexc_app%26api%3Dauthorize%26scope%3Dab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&use_ms_for_expiry=true#/) e clique em **[!UICONTROL Experience Manager Assets Content Hub]**, disponível na seção **[!UICONTROL Acesso rápido]**:
  ![Acesso ao Content Hub](assets/access-content-hub.png)

* Faça logon em [experience.adobe.com](https://auth.services.adobe.com/en_GB/index.html?callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fadobeid%2Fexc_app%2FAdobeID%2Ftoken%3Fredirect_uri%3Dhttps%253A%252F%252Fexperience.adobe.com%252F%2523old_hash%253Dold_hash%253D%252523%25252F%2526from_ims%253Dtrue%253Fclient_id%253Dexc_app%2526api%253Dauthorize%2526scope%253Dab.manage%252Caccount_cluster.read%252Cadditional_info%252Cadditional_info.job_function%252Cadditional_info.projectedProductContext%252Cadditional_info.roles%252CAdobeID%252Cadobeio.appregistry.read%252Cadobeio_api%252Caudiencemanager_api%252Ccreative_cloud%252Cmps%252Copenid%252Corg.read%252Cpps.read%252Cread_organizations%252Cread_pc%252Cread_pc.acp%252Cread_pc.dma_tartan%252Csession%26state%3D%257B%2522jslibver%2522%253A%2522v2-v0.31.0-2-g1e8a8a8%2522%252C%2522nonce%2522%253A%25222316022399331147%2522%257D%26code_challenge_method%3Dplain%26use_ms_for_expiry%3Dtrue&client_id=exc_app&scope=ab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&state=%7B%22jslibver%22%3A%22v2-v0.31.0-2-g1e8a8a8%22%2C%22nonce%22%3A%222316022399331147%22%7D&relay=64da7fa8-cd9e-47cf-9892-7f3ef3092f8c&locale=en_GB&flow_type=token&dctx_id=v%3A2%2Cs%2Cf%2Cb8e64530-b013-11ee-a6c1-e721bdec0171&idp_flow_type=login&response_type=token&profile_filter=%7B%22findFirst%22%3Atrue%2C+%22fallbackToAA%22%3Atrue%2C+%22preferForwardProfile%22%3Atrue%2C+%22searchEntireCluster%22%3Atrue%7D%3B+isOwnedByOrg%28%2776B329395DF155D60A495E2C%40AdobeOrg%27%29&code_challenge_method=plain&redirect_uri=https%3A%2F%2Fexperience.adobe.com%2F%23old_hash%3Dold_hash%3D%2523%252F%26from_ims%3Dtrue%3Fclient_id%3Dexc_app%26api%3Dauthorize%26scope%3Dab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&use_ms_for_expiry=true#/) e clique em **[!UICONTROL Experience Manager Assets Content Hub]**, disponível no alternador de produto:
  ![Método de acesso Content Hub 3](assets/access-content-hub-alternate.png)

## Fornecer feedback sobre o Content Hub {#provide-content-hub-feedback}

Para recomendar melhorias relacionadas ao produto, clique em **[!UICONTROL Feedback]**, ao lado do nome da sua Organização, na parte superior da interface do usuário do Content Hub.

Especifique um assunto, uma descrição da recomendação e anexe arquivos, se necessário. Clique em **[!UICONTROL Enviar]** para enviar o feedback à Adobe.

![Comentários sobre o Content Hub](assets/content-hub-feedback.png)

## Configurar o Content Hub para sua equipe {#setup-content-hub}

Siga estas etapas para configurar o Content Hub para sua equipe:

1. [Habilite o Content Hub para Experience Manager Assets usando o Cloud Manager](deploy-content-hub.md#enable-content-hub).

1. [Integrar o administrador do Content Hub](deploy-content-hub.md#onboard-content-hub-administrator).

1. [Adicionar usuários-chave do Content Hub](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [Ativos aprovados no Experience Manager Assets como autor ou administrador do DAM](approve-assets.md).

1. [Configure a interface de usuário do Content Hub para outros usuários como administrador](configure-content-hub-ui-options.md).

1. [Conceder acesso à Content Hub a mais usuários da equipe](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [Acessar o portal Content Hub](#access-content-hub).

1. [Forneça comentários sobre o Content Hub](#provide-content-hub-feedback).


## Saiba mais sobre os principais recursos {#key-capabilities-content-module}

<table>
<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="Implantar o Centro de conteúdo" src="./assets/configure-assets.png" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>Configurar a interface do usuário do Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Saiba como os administradores podem configurar a interface do usuário do Content Hub. </em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-content-hub.md">
   <img alt="Pesquisar ativos disponíveis no Content Hub" src="./assets/search.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-content-hub.md">
      <strong>Pesquisar ativos disponíveis no Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Saiba como utilizar vários recursos para restringir os resultados da pesquisa.</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="Edição de imagens usando o Adobe Express" src="./assets/edit-images-content-hub.png" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>Editar imagens usando o Adobe Express</strong>
      </a>
   </div>
   <p>
      <em>Saiba como criar variantes de imagens no Content Hub usando o Adobe Express</em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/share-assets-content-hub.md">
   <img alt="Compartilhar ativos disponíveis no Content Hub" src="./assets/share-assets-banner.png" />
   </a>
   <div>
      <a href="/help/assets/share-assets-content-hub.md">
      <strong>Compartilhar ativos disponíveis no Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Saiba como compartilhar um ou vários ativos como um link e depois acessá-los.</em>
   </p>
</td>
<td>
   <a href="/help/assets/collections-content-hub.md">
   <img alt="Gerenciar coleções no Content Hub" src="./assets/manage-collection.png" />
   </a>
   <div>
      <a href="/help/assets/collections-content-hub.md">
      <strong>Gerenciar coleções no Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Saiba como criar coleções usando ativos e gerenciá-los.</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="Compartilhar ativos disponíveis no Content Hub" src="./assets/asset-insights-banner.jpg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>Exibir insights do ativo no Content Hub</strong>
      </a>
   </div>
   <p>
      O módulo de conteúdo <em> fornece informações valiosas sobre ativos, abordando um desafio comum que as partes interessadas de marketing encontram com frequência</em>
   </p>
</td>
</table>
