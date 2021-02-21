---
title: Perguntas frequentes sobre entrega de conteúdo HTTP2
description: Saiba mais sobre o delivery de conteúdo HTTP2.
translation-type: tm+mt
source-git-commit: 193201670e5e78235025885f52215cca730ce556
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 3%

---


# Perguntas frequentes sobre entrega de conteúdo HTTP2{#http-delivery-of-content-faq}

O Adobe está empolgado em anunciar a disponibilidade do delivery HTTP/2 do conteúdo. Ao usar HTTP/2, ocorre um aumento geral no desempenho.

## O que é HTTP/2? {#what-is-http}

O HTTP/2 melhora a maneira como os navegadores e servidores se comunicam, permitindo uma transferência mais rápida de informações e reduzindo a quantidade de energia de processamento necessária.

O site a seguir descreve o HTTP/2 e seus benefícios de uma forma breve e simples:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Quais são os principais benefícios da mudança para HTTP/2 para o delivery de conteúdo? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

A melhoria do desempenho varia muito porque se baseia em vários fatores. Por exemplo, o código do seu site, como você usa o Dynamic Media, o dispositivo do consumidor, a tela e o local.

Os resultados obtidos foram os seguintes:

* Para imagens, o tempo de resposta melhorou de 7% a 28%, dependendo do dispositivo e do navegador. Os ganhos de desempenho mais notáveis foram nos dispositivos iOS.
* Para visualizadores, o desempenho do tempo de carregamento melhorou 15%.

A demonstração a seguir ilustra a diferença entre o carregamento HTTP/1 versus HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Estou qualificado para alternar para HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para usar HTTP/2, você deve atender aos seguintes requisitos:

* Use HTTPS seguro para suas solicitações de mídia avançada.
* Use o CDN (content delivery network) fornecido no Adobe como parte da sua licença do Dynamic Media Classic.
* Use um domínio dedicado (ou seja, `images.company.com` ou `mycompany.scene7.com`), não um domínio Dynamic Media genérico (ou seja, `s7d1.scene7.com`, `s7d2.scene7.com` ou `s7d13.scene7.com`).

   Para localizar seus domínios, abra o [aplicativo Dynamic Media Classic para desktop](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta.

   Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais]**. Procure o campo **Published Server Name**. Se você estiver usando um domínio Dynamic Media genérico no momento, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.

## Qual é o processo para habilitar HTTP/2 para minha conta Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dm-account}

[Use a Admin Console para criar um ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) caso de suporte e solicitar a alternância para HTTP/2; isso não é feito automaticamente para você.

1. Forneça as seguintes informações em seu caso de suporte:

   * Nome do contato principal, email e número de telefone.
   * Todos os domínios a serem transferidos para HTTP2. Ou seja, `images.company.com` ou `mycompany.scene7.com`.

   Para localizar seus domínios, abra o [aplicativo Dynamic Media Classic para desktop](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta.

   Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais]**. Procure o campo **[!UICONTROL Published Server Name]**.

   * Verifique se você usa HTTPS seguro para solicitações de mídia avançada.
   * Verifique se você está usando o CDN através do Adobe e não é gerenciado com um relacionamento direto.
   * Verifique se você está usando um domínio dedicado. Ou seja, `images.company.com` ou `mycompany.scene7.com`, não é um domínio genérico do Dynamic Media, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

   Para localizar seus domínios, abra o [aplicativo Dynamic Media Classic para desktop](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta.

   Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais]**. Procure o campo **[!UICONTROL Published Server Name]**. Se você estiver usando um domínio Dynamic Media genérico no momento, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.

   1. O suporte técnico o adiciona à lista de espera do cliente HTTP/2 com base na ordem em que as solicitações foram enviadas.
   1. Quando o Adobe estiver pronto para lidar com sua solicitação, o Atendimento ao cliente entrará em contato com você para coordenar a transição e definir uma data de público alvo.
   1. Você será notificado após a conclusão e poderá verificar uma transição bem-sucedida em HTTP2.



## Quando posso esperar a transição para HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

As solicitações são processadas na ordem em que são recebidas pelo Suporte Técnico.

>[!NOTE]
>
>Há um longo lead time porque a transição para HTTP/2 envolve a limpeza do cache. Portanto, somente algumas transições de clientes podem ser tratadas de cada vez.

## Quais são os riscos com a mudança para HTTP/2? {#what-are-the-risks-with-moving-to-http}

A transição para HTTP/2 limpa o cache no CDN porque envolve a mudança para uma nova configuração de CDN.

O conteúdo armazenado em cache atinge diretamente os servidores de Adobe não armazenados em cache até que o cache seja reconstruído novamente. Por causa dessa ação, o Adobe planeja lidar com algumas transições de clientes de cada vez. Esse método garante que o desempenho aceitável seja mantido ao retirar solicitações da origem.

## Como verificar se um URL ou site é ativado com HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Baixe uma extensão para usar com seu navegador da Web. Para Firefox e Chrome, há uma extensão chamada **[!UICONTROL HTTP/2 e Indicador SPDY]**. Os navegadores só suportam HTTP/2 com segurança, portanto, é necessário chamar um URL com HTTPS para verificar. Se o HTTP/2 for suportado, ele será indicado pela extensão na forma de um símbolo de Flash azul e um cabeçalho &quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.
