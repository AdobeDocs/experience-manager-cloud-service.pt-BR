---
title: Dynamic Media Jornada, Parte I
description: A Jornada do Dynamic Media aborda as noções básicas do Dynamic Media, como ele funciona, o que ele pode fazer por você e qual valor ele agrega ao seu trabalho e aos seus clientes.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: f3472006-d5ae-4f70-af3e-44e73aee85cc
source-git-commit: af4c85686be5299433974c455f35c907bd6776fd
workflow-type: tm+mt
source-wordcount: '3585'
ht-degree: 1%

---

# jornada Dynamic Media: Noções básicas, Parte I {#dm-journey-part1}

Bem-vindo à Jornada do Dynamic Media.

Esta jornada aborda as noções básicas do Dynamic Media, como ele funciona, o que ele pode fazer por você e qual valor ele agrega ao seu trabalho e aos seus clientes.

**_Pré-requisitos_**

* Noções básicas sobre formatos de imagem e vídeo
* Noções básicas sobre HTML e CSS
* Compreensão básica de ferramentas de design como Adobe Illustrator, Adobe Photoshop, Adobe XD
* O acesso ao Dynamic Media no Experience Manager é útil, mas não é obrigatório

**_O que você pode esperar aprender_**

_Parte I_

* O que é o Dynamic Media e como ele pode ajudá-lo?
* Casos de uso do Dynamic Media
* Como um ativo flui pelo sistema Dynamic Media

_Parte II_

* Anatomia de um URL do Dynamic Media e como o Dynamic Media fornece conteúdo
* Fundamentos da criação de predefinições de imagens para renderizar ativos
* Conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista

**_Público_**
O público-alvo que melhor se encaixa nesta jornada é o seguinte, que é novo no Dynamic Media no Experience Manager:

* Administrador
* Analista de negócios
* Arquitetura de conteúdo
* Autor do conteúdo
* Designer
* Desenvolvedor
* Marketing
* Gerente/proprietário do produto

>[!TIP]
>
>Para obter melhores resultados, o Adobe recomenda que você leia e visualize a Jornada do Dynamic Media em um computador desktop.

## O que é o Dynamic Media e como ele pode ajudá-lo? {#dm-journey-a}

O Dynamic Media ajuda você a fornecer ativos de marketing e merchandising visual por demanda. Também ajuda a criar e veicular experiências de visualização interativas, incluindo zoom, rotação de 360 graus e vídeo. Seus ativos são dimensionados dinamicamente para consumo na Web, em dispositivos móveis e sites sociais. Usando um conjunto de ativos de origem primária - como imagens, vídeo e 3D - a Dynamic Media gera e fornece várias variações desse conteúdo rico, em tempo real por meio de seu CDN (Content Delivery Network) global, escalável e otimizado para desempenho.

O Dynamic Media incorpora os fluxos de trabalho da solução de gerenciamento de ativos digitais do Adobe Experience Manager Assets para simplificar e simplificar o processo de gerenciamento de campanhas digitais.

### Um arquivo com possibilidades infinitas

Um dos principais pontos para entender o Dynamic Media é o conceito de _Um arquivo de ativo principal com possibilidades infinitas_.

Para entender melhor esse conceito, pense na maneira tradicional de trabalhar com um único ativo, como uma imagem ou um vídeo. Geralmente, você cria um ativo principal. Em seguida, você cria manualmente versões desse mesmo ativo para cada experiência, cada dispositivo necessário, cada página da Web e cada propriedade em que ele é usado. Com o tempo, esse único ativo pode crescer para 20, 30 ou mais versões, sem o histórico de versões anexado a ele. Agora, imagine fazer isso para cada imagem ou vídeo que você tem. O número de versões de ativos rapidamente se tornaria esmagador para manter e atualizar, sem falar no aumento dos custos de armazenamento.

O Dynamic Media, no entanto, é fundamentalmente diferente de outros sistemas, pois você o usa para fornecer sua mídia _dinamicamente_ de ativos únicos primários e de chamadas de URL. Os caminhos de URL do Dynamic Media solicitados incluem instruções que informam o servidor de publicação do Adobe sobre como exibir o ativo quando ele é entregue à tela de um cliente. Por exemplo, usando o mesmo ativo principal único, você pode entregá-lo instantaneamente em representações ilimitadas, alterando tamanho, formato, resolução, peso, cor, recorte e efeitos, como uma visualização de zoom.

Esse método de entrega único garante que experiências de qualidade consistentes sejam enviadas para qualquer tela, independentemente do tamanho ou da largura de banda. Vídeos de tamanho total também são otimizados para todos os tipos de tela e transmitidos de forma adaptável para garantir também uma experiência do usuário consistente e de qualidade.

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![O Adobe Dynamic Media fornece a mesma imagem principal para diferentes mídias, em diferentes tamanhos e formatos.](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_O Adobe Dynamic Media garante experiências consistentes e de qualidade para qualquer tela, independentemente do tamanho ou da largura de banda._

Conforme você lê, aprenderá mais sobre por que esse conceito de &quot;um arquivo de ativo principal, possibilidades infinitas&quot; é importante.

### A rede de entrega de conteúdo

Quando estiver pronto para entrar em ação com um ativo de imagem ou um ativo de vídeo, ele será suportado pela espinha dorsal do Dynamic Media, que consiste em uma poderosa rede de entrega de nível superior. A rede serve centenas de clientes em todo o mundo todos os dias. Os ativos são distribuídos na Rede de entrega de conteúdo - ou CDN - hospedada pela Akamai. A CDN é um sistema de serviços de computador em rede que cooperam de forma transparente para fornecer conteúdo, especialmente conteúdo de mídia avançada, aos usuários finais.

No sistema CDN, o conteúdo da Web é armazenado em caches da Web pela Internet. Em seguida, é entregue do cache da Web para os usuários finais para proporcionar uma entrega mais rápida. Assim, na primeira vez que alguém baixa uma página da Web, os ativos que ela vê são entregues a um cache CDN. Eles são armazenados no servidor para que na próxima vez que alguém na mesma área acessar a página da Web, o mesmo conteúdo de cache seja entregue mais rápido. O conteúdo é entregue mais rápido porque está localizado mais próximo do usuário final. Um CDN faz com que a página da Web seja exibida com mais rapidez e, no entanto, diminui as demandas de largura de banda no servidor central porque o conteúdo é fornecido de uma rede de cache, não de um servidor central em cada instância. Esse fluxo otimizado significa uma melhor experiência do usuário, resultando em mais vendas.

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

Historicamente, a CDN fornece 3,5 petabytes de tráfego para os clientes, a cada mês. O sistema pode entregar 52 bilhões de ativos em um único dia. Esse número equivale a 864.000 imagens e vídeos entregues com êxito aos clientes, _a cada segundo_.

### Imagem inteligente

A Dynamic Media já faz um excelente trabalho de otimização de ativos e garantia de que cada ativo carregue rapidamente em sistemas móveis e de desktop, por meio da CDN. Para que isso aconteça, as predefinições de imagens serão usadas no Dynamic Media para definir a qualidade da imagem. Eles também definem o tipo de imagem que você está enviando, sua nitidez e outras partes para várias partes de suas experiências ou páginas.

Mas para adicionar mais valor ao Dynamic Media além das predefinições de imagem, há _Imagem inteligente_.

O Smart Imaging fornece desempenho de fornecimento de ativos de imagem ainda melhor, otimizando automaticamente o formato e o tamanho do arquivo de uma imagem com base na capacidade de um navegador do cliente. Funciona com as predefinições de imagens existentes (as predefinições de imagens são discutidas na Parte II desta jornada) e usa inteligência na entrega.

Essa inteligência reduz ainda mais o tamanho do arquivo de imagem com base na velocidade de conexão do navegador e da rede. Como os ativos de imagem constituem a maior parte do tempo de carregamento de uma página, a melhoria de desempenho pode ter um impacto profundo nos principais indicadores de negócios, como:

* Conversão mais alta
* Tempo gasto no site
* Taxa de rejeição do site mais baixa

Em geral, com a geração inteligente de imagens, você pode esperar uma melhoria de desempenho de 22% a 47% dependendo das configurações predefinidas de imagens existentes e das características específicas do usuário final. Ao mesmo tempo, mantinha a qualidade da imagem como se ela nunca tivesse sido tocada.

![Imagem inteligente](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_O Smart Imaging otimiza automaticamente o formato e o tamanho do arquivo de uma imagem com base no recurso de navegador do cliente e na velocidade da rede._

A geração de imagens inteligentes não é ativada por padrão porque requer um esforço coordenado entre você e o suporte técnico Adobe Dynamic Media. Além disso, ativar o Smart Imaging requer uma limpeza completa do cache CDN, que é preenchido com o tempo. Se você estiver interessado em usar a Smart Imaging, poderá trabalhar com o Adobe para ativá-la enviando um tíquete de suporte técnico. Em seguida, o suporte técnico fornece um parâmetro de URL que permite experimentar previamente a geração inteligente de imagens. Você pode experimentá-lo em qualquer página da Web ou imagem para que você possa ver o desempenho que obtém e a economia. É possível ativar a geração inteligente de imagens para o seu site completo.

### Conjuntos de vídeos adaptáveis

Quando há um vídeo em uma página, ou uma página principal, seus clientes tendem a se envolver com esse conteúdo por mais tempo e a permanecer na página por mais tempo, o que geralmente é bom. Esse comportamento foi exibido por meio de análises realizadas pelo Adobe. No entanto, o vídeo pode ser complexo. Por um lado, você geralmente tem um arquivo principal grande. É complicado determinar como dimensionar e fornecer vídeo, tudo para garantir que a experiência seja executada sem problemas, independentemente do dispositivo em que está sendo exibido e da largura de banda.

Para resolver esse problema, a Dynamic Media oferece a capacidade de criar _Conjuntos de vídeos adaptáveis_.

![Conjunto de vídeos adaptáveis](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_Um Conjunto de vídeos adaptáveis agrupa versões do mesmo vídeo codificadas em diferentes formatos e taxas de bits._

Você começa com seu vídeo original e principal, que você faz upload no sistema. o Dynamic Media tem tamanhos automáticos ou _transcódigos_, esse vídeo em vários vídeos. Em seguida, no momento do delivery, ele determina de forma inteligente qual tela de vídeo, qual qualidade e qual formato usar e o entrega ao telefone, tablet ou computador desktop.

Por exemplo, em um dispositivo móvel iOS, ele detecta uma largura de banda como 4G, 5G ou Wi-Fi. Em seguida, ele seleciona automaticamente o vídeo codificado direito dentre as várias taxas de bits de vídeo no Conjunto de vídeos adaptáveis. O vídeo é transmitido para dispositivos móveis, tablets ou computadores desktop.

Além disso, a qualidade do vídeo é automaticamente alternada se as condições da rede mudarem. E, se um cliente entrar no modo de tela cheia em um desktop, o Adaptive Video Set responde usando uma resolução melhor, melhorando a experiência de visualização do cliente.

O uso de conjuntos de vídeos adaptáveis oferece uma reprodução perfeita e de alta qualidade para os clientes que reproduzem vídeos do Dynamic Media em várias telas e dispositivos. Realmente tira a complexidade do vídeo.

## Casos de uso do Dynamic Media {#dm-journey-b}

Veja a seguir os problemas comuns de casos de uso e as soluções com as quais a Dynamic Media pode ajudá-lo a impulsionar um envolvimento positivo do cliente, fidelidade, conversão e ROI aumentado.

### Caso de uso: Abordagem de arquivo principal

Um dos casos de uso mais importantes do Dynamic Media também é um dos mais óbvios. Ou seja, reduzindo o peso das páginas e experiências e o tamanho do conteúdo, seja uma imagem ou um vídeo, que está sendo entregue.

A seguir, há uma experiência típica ou página da Web. Cerca de 90% de uma página é composta de mídias avançadas, como imagens e vídeos, que geralmente são arquivos muito mais pesados.

![Peso da página de conteúdo](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_Peso da página de conteúdo de uma página da Web típica._

Os 10% restantes são HTML, código CSS e tags específicas. Você deseja otimizar o peso de 90% dessa página e o Dynamic Media ajuda com esse esforço. Anteriormente, você leu sobre o conceito de _um arquivo de ativo principal com possibilidades infinitas_. Essa abordagem é importante para reduzir o peso geral da página. A capacidade de pegar um ativo principal e usá-lo em uma página de detalhes do produto, em uma página de miniatura, em seu carrinho de compras e em sua grade de pesquisa é uma excelente economia de tempo. E também garante consistência em todas as experiências.

![Abordagem de arquivo principal](/help/assets/dynamic-media/assets/dm-onefile.png)
_O relógio é um arquivo de ativo principal, mas com várias representações dele - não cópias - criadas em tempo real._

Vamos analisar mais detalhadamente os problemas que a Dynamic Media está resolvendo com um arquivo e algumas das soluções para essa abordagem.

| **Problema** | **Solução Dynamic Media** |
|---|---|
| Crie e armazene cada ativo. | Use um único arquivo de imagem, criando automaticamente as representações necessárias somente no momento do delivery. |
| Altos custos de armazenamento. | Elimina a necessidade de criar e armazenar várias cópias de um ativo. |
| Dificuldade em manter a cadeia de custódia. | Garante a entrega de experiências otimizadas e consistentes no dispositivo. |
| Nenhum histórico de versão. |  |
| Experiências de marca inconsistentes em todos os dispositivos. |  |
| Custo desnecessário da criação duplicada de ativos. |  |

Ao pensar em um arquivo, você está criando um ativo para cada tipo de experiência. Você pode ter uma imagem inicial e, em seguida, precisa criar 20, 30 ou 40 variações dessa imagem, que você terá que armazenar e pagar por esse armazenamento.

Em seguida, é necessário verificar se a imagem correta é usada e isso pode afetar sua capacidade de ter consistência em todas as marcas. E, se não conseguir encontrar uma imagem, você terá que voltar e duplicar esses ativos.

O Dynamic Media permite criar variações de imagens, em tempo real, a partir dessa imagem inicial. Ele permite que você seja criativo com esse ativo principal e não precise ir e voltar com seu artista de design gráfico ou estúdio de fotos para criar conteúdo adicional. E isso é dinheiro e tempo economizado.

Com a abordagem de um arquivo, você usa um único arquivo principal. Em seguida, crie as versões ou representações necessárias em seus sites, propriedades e experiências, somente no momento em que forem entregues ou visualizadas por um cliente. Essa eficiência pode diminuir bastante a quantidade de armazenamento necessário para seus ativos e reduzir a complexidade geral do fluxo de trabalho. E com o sistema de entrega do Dynamic Media, ele garante que todas as imagens e vídeos sejam otimizados, carregados rapidamente e tenham uma aparência ótima em todas as telas e dispositivos.

### Caso de uso: Vídeo

Outro caso de uso que o Dynamic Media soluciona é o vídeo. Vídeo é complexo. É difícil de gerir. Os arquivos de vídeo são desafiadores a armazenar e movimentar-se por causa de seus tamanhos de arquivo inerentes.

| **Problema** | **Solução Dynamic Media** |
|---|---|
| Difícil de gerenciar e fornecer vídeo otimizado para vários dispositivos. | Use um único vídeo que dimensiona automaticamente todos os dispositivos. |
| Vídeos são interrompidos ou reproduzidos em baixa qualidade devido à largura de banda disponível do usuário final. | Forneça vídeo por meio de um HTML player que detecta automaticamente a largura de banda disponível e adapta a qualidade para garantir alta fidelidade e reprodução sem problemas. |
| Inviável e demorado para criar manualmente todas as versões de um vídeo, somente para garantir uma boa exibição e reprodução em todos os dispositivos. | Elimine horas de trabalho tedioso de transcodificação com um fluxo de trabalho simplificado. |
|  | Liberte tempo para trabalho de maior valor. |

Os clientes vêm ao Dynamic Media com o seguinte problema que esperam resolver:

&quot;_Temos o vídeo, e gastamos muito dinheiro criando-o. Mas nós evitamos colocá-lo em páginas, ou entregá-lo, porque de nossos testes, nós realmente não podemos garantir a qualidade do vídeo, ou se ele realmente vai tocar. E, por fim, isso afeta nossas marcas e potencialmente nosso papel para até mesmo a conversão._&quot;

A solução do Dynamic Media é pegar um arquivo de vídeo principal e permitir que o Dynamic Media faça todos os tamanhos por meio de seu processo de transcodificação. Em seguida, emparelhe isso com o player de vídeo inteligente do Dynamic Media. Esse fluxo de trabalho garante que, esteja você usando esse vídeo na página de aterrissagem principal ou em uma categoria ou página de detalhes do produto, ele será consistente em todo o processo e entregue com alta qualidade.

Aqui estão vários outros casos de uso a serem considerados.

### Caso de uso: Fonte única de verdade

| **Problema** | **Solução Dynamic Media** |
|---|---|
| Ativos digitais distribuídos na organização, colocados em diferentes equipes ou unidades de negócios. | Armazene e gerencie todos os ativos digitais em um local central. |
| Membros da equipe baixam e criam versões locais. | Os membros da equipe usam um único arquivo principal para criar _e_ entregar todas as versões necessárias em vários tamanhos de tela e dispositivos. |
| Ativos de uso único criados para cada experiência e dispositivo. | Elimina ativos de uso único, economizando tempo e dinheiro na criação. |

### Caso de uso: Corte inteligente alimentado por IA para mídia avançada

| **Problema** | **Solução Dynamic Media** |
|---|---|
| Demorado e trabalhoso para desenhar, medir e recortar manualmente imagens ou vídeos para destacar o ponto focal e exibir adequadamente em todos os tamanhos de tela e dispositivos. | Usa o Recorte inteligente no Dynamic Media, um recurso de IA da Adobe Sensei, para detectar automaticamente o ponto focal em qualquer imagem ou vídeo e recortar para mantê-lo. |
| Tempo perdido que poderia ser melhor gasto criando experiências de alto impacto. | Captura o ponto de interesse pretendido independentemente do tamanho da tela. |
| Ativos de uso único criados para cada experiência e dispositivo. | Elimina tarefas manuais entediantes e fornece imagens e vídeos de alta qualidade e carregamento rápido que parecem bons em qualquer dispositivo ou tela. |

### Caso de uso: Criação de mídia interativa

| **Problema** | **Solução Dynamic Media** |
|---|---|
| Experiências simples e estáticas do cliente que não se envolvem, geram fidelidade ou impulsionam a conversão. | Permite que usuários não técnicos adicionem com facilidade e facilidade elementos interativos, como pontos de acesso, carrosséis e conjuntos de rotação, para obter experiências mais dinâmicas e envolventes. |
| Retorno limitado do investimento em ativos digitais e experiência de cliente inadequada. | Impulsiona a conversão e o retorno sobre o investimento a partir de experiências de mídia avançada. |

## Como um ativo flui pelo sistema Dynamic Media {#dm-journey-c}

A seguir, é exibido um fluxo de trabalho típico para o Dynamic Media.

![Fluxo de trabalho do Dynamic Media](/help/assets/dynamic-media/assets/dm-workflow.png)
_Como um ativo flui pelo sistema Dynamic Media._

Você começa com a fase de criação com a meta principal de ter o ativo principal no final. Esses ativos principais podem vir de fotos, de fornecedores de vídeo ou de alguns arquivos de áudio que você criou. Você pode usar aplicativos Adobe, Adobe Photoshop, Adobe Illustrator para ajudar você a trabalhar com o conteúdo.

Quando a parte de criação é concluída, você coloca o ativo na solução de Criação ao fazer upload do ativo no Dynamic Media. No Dynamic Media, verifique se você tem as predefinições de imagens e os visualizadores certos alinhados para suas várias páginas da Web no seu site.

E, por fim, você otimiza todo o conteúdo e o publica nos servidores da Dynamic Media para que ele esteja disponível para Web, impressão, email, desktops e dispositivos móveis.

### Upload de ativos no Dynamic Media

Quando terminar de criar um ativo principal, faça upload dele para o Dynamic Media. O tipo de arquivo carregado e o formato e tamanho do arquivo são atributos importantes para o Dynamic Media. É no momento do upload que você deseja garantir que obtenha o valor máximo de um suporte de arquivo.

Por exemplo, a imagem de relógio abaixo é de 4560 x 3020 pixels. E embora você nunca possa usar uma imagem desse tamanho, ainda é possível carregá-la. Quanto maior a imagem, melhor a qualidade que o Dynamic Media pode fornecer, mesmo que seja a representação em miniatura. Lembre-se: você pode _diminuição_ a resolução de uma imagem existente. Mas se você tentar _aumento_ Na resolução de uma imagem, o resultado provavelmente será insatisfatório.

![Formatos recomendados para fazer upload no Dynamic Media](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_Considerações para uploads de ativos._

O Adobe recomenda fazer upload de ativos em um formato sem perdas. Geralmente, é melhor evitar o JPEG porque quando você entrega o JPEG ou quando continua a salvar o JPEG, você começa a perder a qualidade da imagem ao longo do tempo. Você deseja começar com as imagens de resolução mais alta em um formato sem perdas com o qual você pode viver. Normalmente, esse formato é um arquivo TIFF ou PNG.

Em relação ao espaço de cores, quando você pensa em um canal digital ou exibição da Web, normalmente pensa em RGB (Vermelho, Verde, Azul).

A maioria nunca pensaria em fornecer algo no CMYK ou por que você pode até desejar entregar no CMYK. Isso ocorre porque o espaço de cores é usado com mais frequência para entregar itens impressos. Mas o Dynamic Media pode oferecer nos dois espaços de cores.

Há muitos clientes que ainda fazem a impressão, como clubes grossistas de depósito. E há mercearias que frequentemente imprimem panfletos semanalmente. Esses clientes exigem que suas imagens estejam em ambos os espaços de cores. Tradicionalmente, isso exigiria duas imagens diferentes: um no RGB e outro no CMYK. No entanto, é possível fazer upload de ativos CMYK diretamente no Dynamic Media e fazer com que o Dynamic Media entregue ativos do RGB por meio de uma predefinição de imagem ou por meio de um perfil de cores, automaticamente. Não há necessidade de criar várias versões de um arquivo, mantendo assim o conceito de _um arquivo de ativo principal com possibilidades infinitas_.

<!-- **The Value of Renditioning??? or Demo portion** -->

### Publicar e visualizar ativos

Depois de fazer upload de ativos no Dynamic Media, é uma boa prática _publicar_ selecionando-os e clicando em **[!UICONTROL Publicar]** ou **[!UICONTROL Publicação rápida]** no Dynamic Media. A publicação de ativos é necessária se você pretende usá-los em qualquer experiência. Depois que os ativos são publicados, eles ficam disponíveis para inclusão em uma página da Web usando um URL gerado pelo Dynamic Media que você copia ou por meio da incorporação do código na página.

Além de publicar ativos manualmente, você pode configurar o Dynamic Media para publicar ativos instantaneamente - sem nenhuma intervenção do usuário - no momento do upload.

Após o upload, há diferentes maneiras de visualizar as representações de um ativo no Dynamic Media. Visualizar representações pode ajudar a fornecer uma ideia do que o cliente vê. Um método de visualização comum é selecionar um ativo e depois exibir suas Representações selecionando um *predefinição de imagem* como se vê no exemplo seguinte.

![Visualização de uma representação de um ativo com base na predefinição de imagem grande](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_Visualização de uma representação de um ativo com base na predefinição de imagem &quot;Grande&quot; selecionada. O botão URL foi clicado. O caminho do URL resultante contém o nome predefinido de imagem &quot;Grande&quot; e pode ser usado em uma página da Web._

O URL acima está ativo! [Experimente](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$).

Outro método para visualizar um ativo é selecionar um ativo de imagem e, em seguida, selecionar um *Visualizadores* como mostrado no exemplo a seguir.

![Visualização de um ativo com base na predefinição do visualizador de Luz vertical de zoom](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_Visualização de um ativo com base na predefinição do visualizador &quot;ZoomVertical_light&quot; selecionada. O ponteiro do mouse (`+`) foi movido sobre o relógio para ampliar. Observe o URL e os botões Incorporar ._

A representação acima está ao vivo! [Experimente](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&amp;config=jpearldemo/ZoomVertical_light).

Vamos examinar esses URLs um pouco mais de perto para que você possa entender melhor o que está acontecendo. Leve-me para [jornada Dynamic Media: Noções básicas, Parte II](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d).

## Saiba mais

_Tópicos do Dynamic Media_

* [Trabalhar com o Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)
* [Imagem inteligente](/help/assets/dynamic-media/imaging-faq.md)
* [Conjuntos de vídeos adaptáveis](/help/assets/dynamic-media/video.md)
* [Práticas recomendadas para otimização da qualidade de imagens](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [Fazer upload de ativos](/help/assets/add-assets.md#upload-assets)
* [Visualizar ativos](/help/assets/dynamic-media/previewing-assets.md)
* [Pré-visualizar ativos 3D](/help/assets/dynamic-media/previewing-3d-assets.md)
* [Fornecer ativos da Dynamic Media](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [Publicar ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [Trabalhar com publicação seletiva no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md)

_Tutoriais do Dynamic Media_

* [Usar o Dynamic Media com Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=pt-BR)
* [Biblioteca de conteúdo do Adobe Experience Manager](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (pesquisar em *Dynamic Media*)

_Visualizadores do Dynamic Media_

* [Demonstrações ao vivo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html)

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->