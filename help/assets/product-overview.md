---
title: Visão geral do Content Hub
description: Saiba mais sobre o Content Hub, seus principais benefícios, como acessá-lo e como fornecer feedback sobre as opções disponíveis no Content Hub.
exl-id: c5908058-f1ad-4aaa-9e8e-c0157e107ed1
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# Visão geral do Content Hub {#overview-content-hub}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |----|-----|

![visão geral do Content Hub](assets/content-hub-overview.png)

>[!AVAILABILITY]
>
>O guia do Content Hub agora está disponível no formato PDF. Baixe o guia inteiro e use o Assistente de IA da Adobe Acrobat para responder às suas consultas.
>
>[!BADGE PDF do Guia do Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

O Content Hub está disponível como parte do Experience Manager Assets as a Cloud Service para democratizar o acesso a conteúdo sobre a marca para organizações e seus parceiros de negócios. Ele se concentra na distribuição de ativos para ativação em escala e criação de variantes de conteúdo na marca para melhorar a agilidade de marketing.

## Por que Content Hub?

A Content Hub oferece os seguintes benefícios principais:

**Localize e compartilhe todos os ativos aprovados pela marca disponíveis em um portal intuitivo**

O AEM Assets serve como uma única fonte da verdade e todos os ativos aprovados são disponibilizados automaticamente no Content Hub em uma hierarquia simples para melhorar a experiência de pesquisa.

**Interface de usuário configurável**

As propriedades mais comuns no Content Hub, como filtros de pesquisa, campos disponíveis ao adicionar ou importar ativos, propriedades de ativos, conteúdo de banner para marca são configuráveis e um administrador pode configurar facilmente a interface do usuário do Content Hub com base em seus requisitos.

**Capacite os usuários não criativos a editar e remixar conteúdo enquanto permanecem na marca**

O Content Hub permite criar novo conteúdo com o Adobe Express (se você tiver direitos ao Adobe Express). Você pode editar o conteúdo existente com ferramentas fáceis de usar, produzir variações na marca com modelos e elementos da marca e criar novo conteúdo com os recursos mais recentes da GenAI da Adobe Firefly.

**Obter insights sobre como o conteúdo é usado entre equipes**

O [!DNL Content Hub] fornece informações valiosas sobre ativos, abordando um desafio comum que as partes interessadas de marketing geralmente enfrentam: as estatísticas de uso de ativos usadas em campanhas de marketing, canais e diferentes regiões. Ao obter uma compreensão clara do desempenho e da popularidade dos ativos, ele fornece insights acionáveis essenciais para melhorar a experiência do usuário.

## Pré-requisitos {#prerequisites-content-hub}

O Content Hub requer um ambiente de autor de produção de Experience Manager as a Cloud Service, versão 2024.6 ou mais recente (a versão mínima é 2024.6.16799).

## Como acessar o Content Hub? {#access-content-hub}

[Após configurar o Content Hub](/help/assets/deploy-content-hub.md) e adicionar um usuário ao [perfil de produto do Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile), o Content Hub pode ser acessado das seguintes maneiras:

* Acesse o Content Hub usando o seguinte link:

  `https://experience.adobe.com/#/assets/contenthub`

* Faça logon em experience.adobe.com e clique em **[!UICONTROL Experience Manager Assets Content Hub]**, disponível na seção **[!UICONTROL Acesso rápido]**:
  ![Acesso ao Content Hub](assets/access-content-hub.png)

* Faça logon em experience.adobe.com e clique em **[!UICONTROL Experience Manager Assets Content Hub]**, disponível no alternador de produto:
  ![Método de acesso Content Hub 3](assets/access-content-hub-alternate.png)



## Fornecer feedback sobre o Content Hub {#provide-content-hub-feedback}

Para recomendar melhorias relacionadas ao produto, clique em **[!UICONTROL Feedback]**, ao lado do nome da sua Organização, na parte superior da interface do usuário do Content Hub.

Especifique um assunto, uma descrição da recomendação e anexe arquivos, se necessário. Clique em **[!UICONTROL Enviar]** para enviar o feedback para o Adobe.

![Comentários sobre o Content Hub](assets/content-hub-feedback.png)

## Configurar o Content Hub para sua equipe {#setup-content-hub}

Siga estas etapas para configurar o Content Hub para sua equipe:

1. [Habilite o Content Hub para Experience Manager Assets usando o Cloud Manager](deploy-content-hub.md#enable-content-hub).

1. [Integrar o administrador do Content Hub](deploy-content-hub.md#onboard-content-hub-administrator).

1. [Adicionar usuários-chave do Content Hub](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [Autores ou administradores do DAM para aprovar ativos usando ativos de Experience Manager](approve-assets.md).

1. [Os administradores podem configurar a interface de usuário do Content Hub para outros usuários](configure-content-hub-ui-options.md).

1. [Conceder acesso à Content Hub a mais usuários da equipe](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [Acessar o portal Content Hub](#access-content-hub).

1. [Forneça comentários sobre o Content Hub](#provide-content-hub-feedback).


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
      <strong>Editar imagens usando Adobe Express</strong>
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
