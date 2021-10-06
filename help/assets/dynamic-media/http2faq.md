---
title: Perguntas frequentes sobre entrega de conteúdo HTTP2
description: Saiba mais sobre a entrega de conteúdo HTTP2.
role: Admin,User
exl-id: 0a8a5fd8-a341-4e7f-84a5-409e2de97efe
source-git-commit: 49302452b9544b9414ec49ce2862d9913fbfc6a6
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# Perguntas frequentes sobre entrega de conteúdo HTTP2{#http-delivery-of-content-faq}

O Adobe está animado em anunciar a disponibilidade da entrega de conteúdo HTTP/2. Ao usar HTTP/2, ocorre um aumento geral no desempenho.

>[!NOTE]
>
>Esse recurso exige o uso da Rede de entrega de conteúdo pronta para uso, fornecida com o Adobe Experience Manager - Dynamic Media. Qualquer outra Rede de entrega de conteúdo personalizada não é compatível com esse recurso.

## O que é HTTP/2? {#what-is-http}

O HTTP/2 melhora a forma como os navegadores e servidores se comunicam, permitindo uma transferência mais rápida de informações e ao mesmo tempo reduzindo a quantidade de poder de processamento necessário.

O artigo do site [O que você deve saber sobre HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html) descreve HTTP/2 e seus benefícios de uma maneira breve e simples.

## Quais são os principais benefícios da migração para HTTP/2 para a entrega de conteúdo? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

O aprimoramento do desempenho varia muito porque é baseado em vários fatores. Por exemplo, o código do seu site, a forma como você usa o Dynamic Media, o dispositivo do consumidor, a tela e o local.

Resultados dos testes próprios:

* Para imagens, o tempo de resposta melhorou de 7% a 28%, dependendo do dispositivo e do navegador. Os ganhos de desempenho mais notáveis foram em dispositivos iOS.
* Para visualizadores, o desempenho do tempo de carregamento melhorou em 15%.

A demonstração a seguir ilustra a diferença entre o carregamento HTTP/1 e HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Posso mudar para HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para usar HTTP/2, você deve atender aos seguintes requisitos:

* Use HTTPS seguro para suas solicitações de mídia avançada.
* Use a CDN (Content Delivery Network) fornecida pelo Adobe como parte de sua licença da Dynamic Media Classic.
* Use um domínio dedicado (ou seja, `images.company.com` ou `mycompany.scene7.com`), não um domínio Dynamic Media genérico (ou seja, `s7d1.scene7.com`, `s7d2.scene7.com` ou `s7d13.scene7.com`).

   Para encontrar seus domínios, abra o [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta.

   Vá para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Definições Gerais]**. Procure o campo rotulado **Nome do Servidor Publicado**. Se você estiver usando um domínio genérico do Dynamic Media no momento, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.

## Qual é o processo para habilitar HTTP/2 para minha conta Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dm-account}

[Use o Admin Console para criar um ](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) caso de suporte e solicitar a mudança para HTTP/2; isso não é feito automaticamente para você.

1. Forneça as seguintes informações no caso de suporte:

   * Nome do contato principal, email e número de telefone.
   * Todos os domínios a serem transferidos para HTTP2. Ou seja, `images.company.com` ou `mycompany.scene7.com`.

   Para encontrar seus domínios, abra o [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta.

   Vá para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Definições Gerais]**. Procure o campo rotulado **[!UICONTROL Nome do Servidor Publicado]**.

   * Verifique se você usa HTTPS seguro para solicitações de mídia avançada.
   * Verifique se você está usando a CDN por meio do Adobe e não é gerenciada com uma relação direta.
   * Verifique se você está usando um domínio dedicado. Ou seja, `images.company.com` ou `mycompany.scene7.com`, não é um domínio genérico do Dynamic Media, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

   Para encontrar seus domínios, Abra o [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta.

   Vá para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Definições Gerais]**. Procure o campo rotulado **[!UICONTROL Nome do Servidor Publicado]**. Se você estiver usando um domínio genérico do Dynamic Media no momento, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.

   1. O Suporte ao cliente adiciona você à lista de espera do cliente HTTP/2 com base na ordem em que as solicitações foram enviadas.
   1. Quando o Adobe estiver pronto para lidar com sua solicitação, o Suporte ao cliente entrará em contato com você para coordenar a transição e definir uma data de destino.
   1. Você será notificado após a conclusão e poderá verificar uma transição bem-sucedida para HTTP2.



## Quando posso esperar uma transição para HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

As solicitações são processadas na ordem em que são recebidas pelo Suporte ao cliente.

>[!NOTE]
>
>Há um lead time longo porque a transição para HTTP/2 envolve limpar o cache. Portanto, apenas algumas transições de clientes podem ser tratadas por vez.

## Quais são os riscos com a mudança para HTTP/2? {#what-are-the-risks-with-moving-to-http}

A transição para HTTP/2 limpa seu cache no CDN porque envolve mudar para uma nova configuração de CDN.

O conteúdo armazenado em cache atinge diretamente os servidores de origem não-Adobe até que o cache seja recriado novamente. Por causa dessa ação, o Adobe planeja lidar com algumas transições de clientes de cada vez. Esse método garante que o desempenho aceitável seja mantido ao extrair solicitações da origem.

## Como é possível verificar se um URL ou site está ativado com HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Baixe uma extensão para usar com seu navegador da Web. Para Firefox e Chrome, há uma extensão chamada **[!UICONTROL HTTP/2 e Indicador SPDY]**. Os navegadores só suportam HTTP/2 com segurança, portanto, é necessário chamar um URL com HTTPS para verificar. Se HTTP/2 for suportado, ele será indicado pela extensão na forma de um símbolo de Flash azul e um cabeçalho &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.
