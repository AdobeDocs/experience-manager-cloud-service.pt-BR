---
title: Visão geral do Content Hub
description: Saiba mais sobre o Content Hub, seus principais benefícios, como acessá-lo e como fornecer feedback sobre a opção disponível no Content Hub.
source-git-commit: ad6d213b6ecf902ec80c323a686231f21ee13811
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Visão geral do Content Hub {#overview-content-hub}

![Visão geral do Content Hub](assets/content-hub-overview.png)

O Content Hub está disponível como parte do Experience Manager Assets as a Cloud Service para democratizar o acesso a conteúdo sobre a marca para organizações e seus parceiros de negócios. Ele se concentra na distribuição de ativos para ativação em escala e criação de variantes de conteúdo na marca para melhorar a agilidade de marketing.

## Por que Content Hub?

A Content Hub oferece os seguintes benefícios principais:

**Encontre e compartilhe todos os ativos aprovados pela marca disponíveis em um portal intuitivo**

O AEM Assets serve como uma única fonte da verdade e todos os ativos aprovados são disponibilizados automaticamente no Content Hub em uma hierarquia simples para melhorar a experiência de pesquisa.

**Interface do usuário configurável**

As propriedades mais comuns no Content Hub, como filtros de pesquisa, campos disponíveis ao adicionar ou importar ativos, propriedades de ativos, conteúdo de banner para marca são configuráveis e um administrador pode configurar facilmente a interface do usuário do Content Hub com base em seus requisitos.

**Capacite os não criativos a editar e remixar conteúdo enquanto permanecem na marca**

O Content Hub permite criar novo conteúdo com o Adobe Express (se você tiver direitos ao Adobe Express). Você pode editar o conteúdo existente com ferramentas fáceis de usar, produzir variações na marca com modelos e elementos da marca e criar novo conteúdo com os recursos mais recentes da GenAI da Adobe Firefly.

**Obter insights sobre como o conteúdo é usado em equipes**

[!DNL Content Hub] O fornece insights valiosos sobre ativos, abordando um desafio comum que as partes interessadas de marketing muitas vezes encontram — estatísticas de uso de ativos usadas em campanhas de marketing, canais e diferentes regiões. Ao obter uma compreensão clara do desempenho e da popularidade dos ativos, ele fornece insights acionáveis essenciais para melhorar a experiência do usuário.

## Pré-requisitos {#prerequisites-content-hub}

O Content Hub requer um ambiente de autor de produção de Experience Manager as a Cloud Service, versão 2024.6 ou mais recente (a versão mínima é 2024.6.16799).

## Como acessar o Content Hub? {#access-content-hub}

[Depois de configurar o Content Hub](#deploy-content-hub) e adicionar um usuário à [Perfil de produto do Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile), o Content Hub pode ser acessado das seguintes maneiras:

* Acesse o Content Hub usando o seguinte link:

  `https://experience.adobe.com/#/assets/contenthub`

* Faça logon em experience.adobe.com e clique em **[!UICONTROL Experience Manager Assets Content Hub]** disponível no **[!UICONTROL Acesso rápido]** seção:
  ![Acesso ao Content Hub](assets/access-content-hub.png)

* Faça logon em experience.adobe.com e clique em **[!UICONTROL Experience Manager Assets Content Hub]** disponível no alternador de produtos:
  ![Método de acesso 3 do Content Hub](assets/access-content-hub-alternate.png)



## Fornecer feedback sobre o Content Hub {#provide-content-hub-feedback}

Para recomendar aprimoramentos relacionados ao produto, clique em **[!UICONTROL Feedback]** ao lado do nome da organização, na parte superior da interface do usuário do Content Hub.

Especifique um assunto, uma descrição da recomendação e anexe arquivos, se necessário. Clique em **[!UICONTROL Enviar]** para enviar o feedback ao Adobe.

![Feedback do Content Hub](assets/content-hub-feedback.png)

## Configurar o Content Hub para sua equipe {#setup-content-hub}

Siga estas etapas para configurar o Content Hub para sua equipe:

1. [Ativar o Content Hub para Experience Manager Assets usando o Cloud Manager](deploy-content-hub.md#enable-content-hub).

1. [Integrar o administrador do Content Hub](deploy-content-hub.md#onboard-content-hub-administrator).

1. [Adicionar usuários-chave do Content Hub](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [Autores ou administradores do DAM para aprovar ativos usando ativos do Experience Manager](approve-assets.md).

1. [Os administradores podem configurar a interface do Content Hub para outros usuários](configure-content-hub-ui-options.md).

1. [Conceder acesso ao Content Hub a mais usuários da equipe](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [Acessar o portal do Content Hub](#access-content-hub).

1. [Fornecer feedback sobre o Content Hub](#provide-content-hub-feedback).


## Saiba mais sobre os principais recursos {#key-capabilities-content-module}

<table>
<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="Implantar o Content Hub" src="./assets/configure-assets.png" />
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
      <em>Saiba como compartilhar um ou vários ativos como um link e acessá-los.</em>
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
      <em> O módulo de conteúdo fornece insights valiosos sobre ativos, abordando um desafio comum que as partes interessadas de marketing muitas vezes encontram</em>
   </p>
</td>
</table>
