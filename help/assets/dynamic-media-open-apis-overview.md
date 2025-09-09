---
title: Dynamic Media com recursos OpenAPI
description: Saiba mais sobre os principais conceitos, como por que usar o Dynamic Media com recursos OpenAPI e como ativá-lo.
role: User
exl-id: 658b6eff-9f5a-4166-9ff6-5dc8eb92ada3
source-git-commit: 73b1b7f2133a751ea2494d66960a7d225798d1dd
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---

# Dynamic Media com recursos OpenAPI {#new-dynaminc-media-apis-overview}

No mundo digital veloz de hoje, explorar todo o potencial dos ativos digitais da sua marca é crucial para se manter à frente da concorrência. Uma solução holística de Gerenciamento de Assets digital (DAM) facilita a governança de ativos, promove a consistência da marca e acelera a entrega de conteúdo, garantindo a integridade da marca e experiências excepcionais para o cliente.

O Dynamic Media, com recursos de OpenAPI, coloca o DAM no centro de um ecossistema ágil e eficiente de cadeia de fornecimento de conteúdo para garantir a governança e a entrega de ativos.

## Por que usar o Dynamic Media com recursos de OpenAPI? {#dynamic-media-open-api-features}

O Dynamic Media com recursos OpenAPI oferece os seguintes benefícios principais:

* **Integrações perfeitas**: o Dynamic Media com recursos OpenAPI oferece um conjunto abrangente de APIs de pesquisa e entrega. Ele permite que seus desenvolvedores [integrem facilmente a entrega de ativos a seus aplicativos](/help/assets/integrate-dynamic-media-open-apis.md). Os aplicativos incluem o Adobe e aplicativos de terceiros. Ele fornece uma [interface de usuário do seletor de ativos de front-end de micro](/help/assets/overview-asset-selector.md) para pesquisar e selecionar ativos aprovados. O seletor pode ser facilmente integrado a qualquer aplicativo com base em estruturas JavaScript, como React JS, Angular JS e Vanilla JS.

* **Gerenciamento centralizado de ativos digitais**: o DAM é a única fonte da verdade para todos os ativos digitais. Seus ativos digitais são gerenciados centralmente no AEM Assets e entregues a aplicativos de consumo por referência usando URLs de entrega, sem copiar binários de ativos.

* **Atualizações em tempo real**: quaisquer alterações feitas em ativos aprovados no DAM, incluindo atualizações de versão e modificações de metadados, são refletidas automaticamente nas URLs de entrega. Com um valor curto de TTL (Time-to-Live) de 10 minutos configurado para o Dynamic Media com recursos OpenAPI por meio do CDN, as atualizações ficam visíveis em todas as interfaces de criação e publicação em menos de 10 minutos.

* **Consistência da marca**: somente [ativos aprovados pela marca](/help/assets/approve-assets.md) são expostos aos aplicativos downstream. [Os gerentes de marca e profissionais de marketing mantêm controle rigoroso sobre os ativos da marca](/help/assets/restrict-assets-delivery.md). Somente as versões aprovadas e mais recentes do ativo estão disponíveis para uso, garantindo a consistência da marca em todos os canais e aplicativos.

* **Entrega otimizada para a Web**: os ativos digitais são entregues em formatos otimizados para a Web para aprimorar os Componentes principais da Web das suas experiências digitais. Isso inclui suporte para representações WebP para imagens, transmissão adaptável por meio dos protocolos HLS ou DASH para vídeos e representações originais para documentos.

* [Transformação dinâmica de ativos](https://developer.adobe.com/experience-cloud/experience-manager-apis): nosso sistema permite a transformação instantânea de imagens usando parâmetros de URL conhecidos como modificadores de imagem. Por exemplo, largura, altura, girar, virar, qualidade, recorte, formato e recorte inteligente. As representações transformadas são geradas dinamicamente e entregues perfeitamente por meio da CDN.

* **Entrega segura de ativos**: o Dynamic Media com recursos OpenAPI fornece um mecanismo para controlar o acesso aos seus ativos digitais. Você pode especificar funções ou grupos de usuários como metadados para ativos que serão protegidos e definir um período predefinido durante o qual [somente usuários autorizados podem acessar esses ativos](/help/assets/restrict-assets-delivery.md). Os URLs de entrega dos ativos protegidos não são resolvidos para usuários não autorizados durante o período restrito.

* **Insights de dados para tomar decisões informadas (no futuro)**: além do gerenciamento e da entrega de ativos, ele captura insights de dados de entrega em entregas de ativos na CDN, permitindo que os gerentes de marca rastreiem as métricas de entrega entre canais. Ele permite que eles tomem decisões orientadas por dados para a otimização contínua da governança de ativos e estratégias de entrega.

![Diagrama de fluxo de dados da API aberta do Dynamic Media](assets/dm-openapi-dfd.png)

Para obter informações sobre as ofertas do Dynamic Media disponíveis e seus recursos, consulte [Dynamic Media Prime e Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).

>[!NOTE]
>
>Os clientes do DM Prime podem usar modificadores básicos de imagem, incluindo girar, cortar, virar, altura, largura e qualidade. A Imagem inteligente não é compatível com AVIF para clientes do DM Prime.


## Pré-requisitos para acessar o Dynamic Media com recursos OpenAPI {#prerequisites-dynaminc-media-open-apis}

Para acessar o Dynamic Media com recursos OpenAPI, você deve ter licenças para:

* AEM Assets as a Cloud Service

* AEM Dynamic Media

## Como habilitar o Dynamic Media com recursos OpenAPI? {#enable-dynamic-media-open-apis}

Antes de enviar uma solicitação para habilitar o Dynamic Media com recursos OpenAPI no AEM as a Cloud Service, verifique se ele ainda não está habilitado.

Quando os [Pré-requisitos](#prerequisites-dynaminc-media-open-apis) forem atendidos e o Dynamic Media com recursos OpenAPI estiver habilitado na sua instância do AEM as a Cloud Service, haverá uma URL de entrega disponível para cada ativo aprovado no repositório. Para obter informações sobre como copiar a URL de entrega, consulte [Copiar URL de entrega para ativos aprovados](approve-assets.md#copy-delivery-url-approved-assets). A Adobe recomenda usar esse método para verificar se o Dynamic Media com recursos OpenAPI está ativado no AEM as a Cloud Service antes de enviar um tíquete de suporte para ativá-lo.

Para habilitar o Dynamic Media com recursos OpenAPI no AEM as a Cloud Service, envie um tíquete de suporte da Adobe com os seguintes detalhes:

* ID de programa e ambiente do Cloud Services

* Detalhes do caso de uso a ser resolvido com o Dynamic Media com integração de recursos OpenAPI.

* Detalhes dos aplicativos downstream para integrar ao Dynamic Media com recursos de OpenAPI.

  >[!NOTE]
  >
  > Para integrar a um aplicativo que não seja do Adobe, forneça nomes de domínio ao lista de permissões onde o aplicativo está hospedado.

* Detalhes dos principais contatos do cliente envolvidos no projeto de integração.

* Lista dos principais membros da equipe de conta da Adobe (email).

Depois de enviar o tíquete de suporte, o Adobe habilita o Dynamic Media com recursos OpenAPI no ambiente do Cloud Services e compartilha os detalhes, como a ID de cliente IMS, para você prosseguir com a integração.

>[!NOTE]
>
>Exclua `/conf/global/settings/dam/assets-configurations/assetdelivery` de qualquer pacote de conteúdo para evitar a desativação do Dynamic Media com recursos OpenAPI.

## Saiba mais sobre os principais recursos {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approve-assets.md">
   <img alt="Aprovar ativos no Experience Manager Assets" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approve-assets.md">
      <strong>Aprovar ativos no Experience Manager Assets</strong>
      </a>
   </div>
   <p>
      <em>Aprove ativos no AEM Assets para simplificar o gerenciamento de ativos, garantindo um processo controlado e eficiente para manuseio de ativos.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-dynamic-media-open-apis.md">
   <img alt="Integrar o AEM Assets com aplicativos downstream" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-dynamic-media-open-apis.md">
      <strong>Integrar o AEM Assets com aplicativos downstream</strong>
      </a>
   </div>
   <p>
      <em>Integre sua própria interface de usuário personalizada com o repositório do Experience Manager Assets usando as APIs de Pesquisa e Entrega ou use o Seletor de Ativos de Microfront-end do Adobe.</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="Seletor de ativos da Adobe" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>Seletor de ativos de microfront-end do Adobe</strong>
      </a>
   </div>
   <p>
      <em>Uma interface de usuário que interage com o repositório do AEM Assets para pesquisar ativos e usá-los na sua experiência de criação de aplicativos.</em>
   </p>
</td>
</table>
<table>



<table>
<td>
   <a href="/help/assets/search-assets-api.md">
   <img alt="Pesquisar repositório do Experience Manager Assets de ativos" src="./assets/search-assets-api-overview.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-api.md">
      <strong>Pesquisar ativos no repositório do Experience Manager Assets</strong>
      </a>
   </div>
   <p>
      <em>Pesquise ativos no repositório do AEM Assets para que eles possam ser entregues aos aplicativos downstream.</em>
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="Fornecer ativos aos aplicativos downstream" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong>Enviar ativos para aplicativos downstream</strong>
      </a>
   </div>
   <p>
      <em>Entregar ativos para aplicativos downstream integrados usando uma URL de Entrega.</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Restringir o acesso a ativos no Experience Manager" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Restringir o acesso aos ativos no Experience Manager</strong>
      </a>
   </div>
   <p>
      <em> Os administradores do DAM ou gerentes de marca restringem o acesso configurando funções para ativos aprovados na instância de autor do AEM as a Cloud Service.</em>
   </p>
</td>

</table>
<table>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="Integrar o AEM Assets remoto com o AEM Sites" src="./assets/connected-assets-rdam.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong>Integrar o AEM Assets remoto com o AEM Sites</strong>
      </a>
   </div>
   <p>
      <em>Saiba como integrar o AEM Assets remoto ao ambiente do AEM Sites. </em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media-open-apis-faqs.md">
   <img alt="Perguntas frequentes sobre o Dynamic Media com recursos OpenAPI" src="./assets/dynamic-media-faqs.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-faqs.md">
      <strong>Perguntas frequentes sobre o Dynamic Media com recursos OpenAPI</strong>
      </a>
   </div>
   <p>
      <em>Obtenha uma resposta às perguntas mais frequentes sobre o Dynamic Media com recursos OpenAPI.</em>
   </p>
</td>
<td>
   <a href="/help/assets/configure-custom-domain.md">
   <img alt="Configurar domínio personalizado" src="./assets/configure-custom-domain.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-custom-domain.md">
      <strong>Configurar domínio personalizado</strong>
      </a>
   </div>
   <p>
      <em>Embora o AEM as a Cloud Service venha com um domínio padrão, você pode personalizá-lo de acordo com suas necessidades.</em>
   </p>
</td>

</table>
