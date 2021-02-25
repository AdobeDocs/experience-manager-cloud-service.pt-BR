---
title: Imagens inteligentes
description: A geração de imagens inteligentes aplica as características de exibição exclusivas de cada usuário para automaticamente servir as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento.
translation-type: tm+mt
source-git-commit: 20e37c385c2d3df91e37095bcf8a630fbfccbd16
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 2%

---


# Imagem inteligente {#smart-imaging}

## O que é &quot;Smart Imaging&quot;? {#what-is-smart-imaging}

A tecnologia Smart Imaging aplica os recursos do Adobe Sensei AI e funciona com &quot;predefinições de imagens&quot; existentes. Ele funciona para melhorar o desempenho do delivery de imagem otimizando automaticamente o formato, o tamanho e a qualidade da imagem, com base nos recursos do navegador do cliente.

>[!NOTE]
>
>Este recurso exige que você use o CDN pronto para uso fornecido com a Adobe Experience Manager Dynamic Media. Nenhum outro CDN personalizado é suportado com este recurso.

O Smart Imaging também se beneficia do aumento de desempenho ao ser totalmente integrado ao melhor serviço premium CDN (Content Delivery Network) do Adobe. Este serviço encontra a melhor rota da Internet entre servidores, redes e pontos de peering. Ele observa a menor latência, ou a menor taxa de perda de pacotes, ou ambos, em vez de simplesmente usar a rota padrão na Internet.

Os exemplos de ativos de imagem a seguir mostram a otimização adicionada de Imagens inteligentes:

| Image<br>(URL) | Miniatura  | Tamanho<br> (JPEG) | Tamanho (WebP)<br> (com Imagem inteligente) | % redução |
|---|---|---|---|---|
| [Imagem 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [Imagem 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [Imagem 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [Imagem 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![figura4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | Média = 51% |

Semelhante ao acima, o Adobe também executou um teste com URLs 7009 de sites ativos de clientes. Eles conseguiram uma média de 38% de otimização de tamanho de arquivo adicional para JPEG. Para PNG com formato WebP, eles conseguiram uma média de 31% mais de otimização de tamanho de arquivo. Esse tipo de otimização é possível por causa da capacidade da Imagem inteligente.

## Quais são os principais benefícios do Smart Imaging mais recente? {#what-are-the-key-benefits-of-smart-imaging}

As imagens constituem a maior parte do tempo de carregamento de uma página. Dessa forma, qualquer melhoria no desempenho pode ter um impacto profundo em taxas de conversão mais altas, tempo gasto em um site e taxas de rejeição do site mais baixas.

Aprimoramentos na versão mais recente do Smart Imaging:

* Serve conteúdo otimizado imediatamente (em tempo de execução).
* Usa a tecnologia Adobe Sensei para converter de acordo com a qualidade (qlt) especificada na solicitação de imagem.
* A Imagem inteligente pode ser desativada usando o parâmetro de URL &quot;bfc&quot;.
* TTL (Tempo de vida) independente. Anteriormente, um TTL mínimo de 12 horas era obrigatório para que a Imagem inteligente funcionasse.
* Anteriormente, as imagens original e derivada eram armazenadas em cache e era um processo de 2 etapas para invalidar o cache. Na última geração de imagens inteligentes, somente os derivados são armazenados em cache, permitindo um processo de invalidação de cache de etapa única.
* Clientes que usam cabeçalhos personalizados em seus conjuntos de regras. Por exemplo, &quot;Origem de permissão de tempo&quot;, &quot;X-Robot&quot; conforme sugerido em [Adicionar um valor de cabeçalho personalizado a respostas de imagem|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)) beneficiam-se da Imagem inteligente mais recente. Esses cabeçalhos não estão bloqueados, ao contrário da versão anterior do Smart Imaging.

## Há algum custo de licenciamento associado à geração de imagens inteligentes? {#are-there-any-licensing-costs-associated-with-smart-imaging}

Não. A Imagem inteligente está incluída na sua licença existente. Essa regra é verdadeira para Dynamic Media Classic ou Experience Manager Dynamic Media (no local, AMS e Experience Manager como Cloud Service).

>[!NOTE]
>
>O Smart Imaging não está disponível para clientes Dynamic Media - Híbrido.


## Como funciona a geração de imagens inteligentes? {#how-does-smart-imaging-work}

Quando uma imagem é solicitada por um consumidor, o Smart Imaging verifica as características do usuário. Em seguida, converte para o formato de imagem apropriado com base no navegador em uso. Essas conversões de formato são feitas de uma maneira que não diminui a fidelidade visual. A geração de imagens inteligentes converte automaticamente imagens em diferentes formatos, com base na capacidade do navegador da seguinte maneira.

* Converter automaticamente para WebP para os seguintes navegadores:
   * Cromo
   * Firefox
   * Microsoft Edge
   * Safari 14.0 +
      * Safari 14 somente com iOS 14.0 e superior e macOS BigSur e superior
   * Android
   * Opera
* Suporte a navegador herdado para o seguinte:

   | Navegador | Versão do navegador/SO | Formato |
   | --- | --- | --- |
   | Safari | iOS 14.0 ou anterior | JPEG2000 |
   | Borda | 18 ou anterior | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* Para navegadores que não suportam esses formatos, o formato de imagem solicitado originalmente é atendido.

Se o tamanho original da imagem for menor do que o que o Smart Imaging produz, então a imagem original será disponibilizada.

## Quais formatos de imagem são suportados? {#what-image-formats-are-supported}

Os seguintes formatos de imagem são suportados para Imagens inteligentes:
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## Como o Smart Imaging funciona com as predefinições de imagens existentes que já estão em uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

O Smart Imaging funciona com as &quot;predefinições de imagens&quot; existentes. Ele observa todas as configurações de imagem, exceto a qualidade (qlt) e o formato (fmt), se o formato de arquivo solicitado for JPEG ou PNG. Para conversão de formato, o Smart Imaging mantém a fidelidade visual completa, conforme definido pelas configurações predefinidas da imagem, mas em um tamanho de arquivo menor. Se o tamanho original da imagem for menor do que o que o Smart Imaging produz, então a imagem original será disponibilizada.

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## Preciso alterar quaisquer URLs, predefinições de imagens ou implantar qualquer novo código no meu site para o Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

O Smart Imaging funciona perfeitamente com os URLs de imagem e predefinições de imagem existentes se você configurar o Smart Imaging no domínio personalizado existente. Além disso, o Smart Imaging não exige que você adicione qualquer código ao seu site para detectar o navegador de um usuário. Toda essa funcionalidade é feita automaticamente.

Caso seja necessário configurar um novo domínio personalizado para usar a Imagem inteligente, os URLs devem ser atualizados para refletir esse domínio personalizado.

Para entender os pré-requisitos para o Smart Imaging, consulte [Estou qualificado para usar o Smart Imaging?](#am-i-eligible-to-use-smart-imaging).

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## A criação de imagens inteligentes funciona com HTTPS? Que tal HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

O Smart Imaging funciona com imagens entregues por HTTP ou HTTPS. Além disso, também funciona por HTTP/2.

## Estou qualificado para usar imagens inteligentes? {#am-i-eligible-to-use-smart-imaging}

Para usar o Smart Imaging, sua conta empresa Dynamic Media Classic ou Dynamic Media no Experience Manager deve atender aos seguintes requisitos:

* Use a CDN (Content Delivery Network, Rede de Adobe de conteúdo) como parte da sua licença.
* Use um domínio dedicado (por exemplo, `images.company.com` ou `mycompany.scene7.com`), não um domínio genérico (por exemplo, `s7d1.scene7.com`, `s7d2.scene7.com` ou `s7d13.scene7.com`).

Para localizar seus domínios, faça logon em sua conta ou contas de empresa.

Toque em **[!UICONTROL Configuração > Configuração de Aplicativo > Configurações Gerais]**. Procure o campo **[!UICONTROL Published Server Name]**. Se no momento você usa um domínio genérico, pode solicitar que você se mova para seu próprio domínio personalizado. Faça esta solicitação de transição ao enviar um ticket de suporte técnico.

Seu primeiro domínio personalizado não tem custo adicional com uma licença da Dynamic Media.

## Qual é o processo para ativar a criação de imagens inteligentes em minha conta? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Você inicia a solicitação para usar imagens inteligentes; ela não é ativada automaticamente.

1. [Use a Admin Console para criar um caso de suporte.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. Forneça as seguintes informações em seu caso de suporte:

   1. Nome do contato principal, email, telefone.
   1. Todos os domínios a serem ativados para geração de imagens inteligente (ou seja, `images.company.com` ou `mycompany.scene7.com`).

      Para localizar seus domínios, faça logon em sua conta ou contas de empresa.

      Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais]**.

      Procure o campo **[!UICONTROL Published Server Name]**.
   1. Verifique se você está usando o CDN através do Adobe e não é gerenciado com uma relação direta.
   1. Verifique se você está usando um domínio dedicado, como `images.company.com` ou `mycompany.scene7.com`, e não um domínio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para localizar seus domínios, faça logon em sua conta ou contas de empresa.

      Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais]**.

      Procure o campo **[!UICONTROL Published Server Name]**. Se você estiver usando um domínio genérico do Dynamic Media Classic, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.
   1. Indique se deseja que funcione por HTTP/2.

1. O Atendimento ao cliente do Adobe adiciona você à Lista de espera do cliente do Smart Imaging com base na ordem em que as solicitações são enviadas.
1. Quando o Adobe estiver pronto para lidar com sua solicitação, o Atendimento ao cliente entrará em contato com você para coordenar e definir uma data de público alvo.
1. **Opcional**: Como opção, você pode testar a geração inteligente de imagens no armazenamento temporário antes de o Adobe empurrar o novo recurso para a produção.
1. Você é notificado após a conclusão pelo Atendimento ao cliente.
1. Para maximizar os aprimoramentos de desempenho do Smart Imaging, o Adobe recomenda definir o Tempo de vida (TTL) como 24 horas ou mais. O TTL define quanto tempo os ativos são armazenados em cache pelo CDN. Para alterar essa configuração:

   1. Se você usar o Dynamic Media Classic, clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configuração de publicação > Servidor de imagem]**. Defina o valor **[!UICONTROL Default Client Cache Time To Live]** como 24 ou mais.
   1. Se você usar o Dynamic Media, siga [estas instruções](config-dm.md). Defina o valor **[!UICONTROL Expiração]** 24 horas ou mais.

## Quando posso esperar que minha conta seja ativada com a Smart Imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

As solicitações são processadas na ordem em que são recebidas pelo Suporte Técnico, de acordo com a Lista de Espera.

>[!NOTE]
Ocasionalmente, há um longo lead time porque a ativação da Imagem inteligente envolve a limpeza do cache pelo Adobe. Portanto, apenas algumas transições de clientes podem ser tratadas a qualquer momento.

## Quais são os riscos com a alternância para usar o Smart Imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Não há risco para uma página da Web do cliente. No entanto, a transição para o Smart Imaging limpa o cache de CDN. Esta operação envolve mudar para uma nova configuração do Dynamic Media Classic ou Dynamic Media no Experience Manager.

Durante a transição inicial, as imagens não armazenadas em cache diretamente acessadas nos servidores de origem são recriadas até que o cache seja reconstruído novamente. Sendo assim, o Adobe planeja lidar com algumas transições do cliente de cada vez para que o desempenho aceitável seja mantido ao retirar solicitações da origem. Para a maioria dos clientes, o cache é totalmente construído novamente no CDN dentro de 1 a 2 dias.

## Como posso verificar se a geração de imagens inteligentes está funcionando como esperado?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Depois que sua conta for configurada com imagens inteligentes, carregue um URL de imagem do Dynamic Media Classic (Scene7)/Dynamic Media no navegador.
1. Abra o painel do desenvolvedor do Chrome clicando em **[!UICONTROL Visualização > Desenvolvedor > Ferramentas do desenvolvedor]** no navegador. Ou escolha qualquer ferramenta de desenvolvedor de navegador de sua escolha.

1. Certifique-se de que o cache esteja desativado quando as ferramentas do desenvolvedor estiverem abertas.

   * No Windows - navegue até as configurações no painel de ferramentas do desenvolvedor e marque a caixa de seleção **[!UICONTROL Desativar cache (enquanto os devtools estiverem abertos)]**.
   * No Mac - no painel do desenvolvedor, na guia **[!UICONTROL Rede]**, selecione **[!UICONTROL desativar cache]** .

1. Observe que o Tipo de conteúdo é transformado no formato apropriado. A seguinte captura de tela mostra uma imagem PNG sendo convertida dinamicamente em WebP no Chrome.
1. Repita esse teste em navegadores e condições de usuário diferentes.

>[!NOTE]
Nem todas as imagens são convertidas. O Smart Imaging decide se a conversão é necessária para melhorar o desempenho. Às vezes, quando não há ganho de desempenho esperado ou o formato não é JPEG ou PNG, a imagem não é convertida.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## A Imagem inteligente pode ser desativada para qualquer solicitação?{#turning-off-smart-imaging}

Sim. Você pode desativar a Imagem inteligente adicionando o modificador `bfc=off` ao URL.

## Que &quot;ajuste&quot; está disponível? Há alguma configuração ou comportamento que possa ser definido? (#tuning-settings)

Atualmente, você pode ativar ou desativar a Imagem inteligente. Nenhum outro ajuste está disponível.

## Se o Smart Imaging gerenciar as configurações de qualidade, há mínimos e máximos que eu possa definir? Por exemplo, é possível definir &quot;não inferior a 60&quot; e &quot;qualidade não superior a 80&quot;? (#Minimum-maximum)

Não há essa capacidade de provisionamento na Imagem inteligente atual.

## Às vezes, uma imagem JPEG é retornada ao Chrome em vez de uma imagem WebP. Por que essa mudança acontece? (#jpeg-webp)

O Smart Imaging determina se a conversão é benéfica ou não. Ele retorna a nova imagem somente se a conversão resultar em um tamanho de arquivo menor com qualidade comparável.
