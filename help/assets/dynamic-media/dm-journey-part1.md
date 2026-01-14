---
title: Jornada do Dynamic Media, Parte I
description: A Jornada do Dynamic Media aborda as noções básicas do Dynamic Media, como ele funciona, o que ele pode fazer por você e qual o valor que ele agrega ao seu trabalho e aos seus clientes.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles,Best Practices
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: f3472006-d5ae-4f70-af3e-44e73aee85cc
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '3614'
ht-degree: 0%

---

# Jornada do Dynamic Media: Noções básicas, Parte I {#dm-journey-part1}

{{see-also-dm}}

Bem-vindo à Jornada do Dynamic Media.

Esta jornada aborda as noções básicas do Dynamic Media, como ele funciona, o que ele pode fazer por você e qual o valor que ele agrega ao seu trabalho e aos seus clientes.

**_Pré-requisitos_**

* Compreensão básica de formatos de imagem e vídeo
* Noções básicas sobre HTML e CSS
* Noções básicas sobre ferramentas de design, como Adobe Illustrator, Adobe Photoshop, Adobe XD
* O acesso ao Dynamic Media no Experience Manager é útil, mas não obrigatório

**_O que você pode esperar saber_**

_Parte I_

* O que é o Dynamic Media e como ele pode ajudá-lo?
* Casos de uso do Dynamic Media
* Como um ativo flui pelo sistema Dynamic Media

_Parte II_

* Anatomia de um URL do Dynamic Media e como o Dynamic Media fornece conteúdo
* Princípios básicos da criação de predefinições de imagens para renderizar ativos
* Conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista

**_Público_**
Os públicos-alvo que melhor se adaptam aos leitores dessa jornada são os seguintes, que são novos no Dynamic Media no Experience Manager:

* Administrador
* Analista de negócios
* Arquiteto de conteúdo
* Autor de conteúdo
* Designer
* Desenvolvedor
* Marketing
* Gerente/proprietário do produto

>[!TIP]
>
>Para obter melhores resultados, a Adobe recomenda que você leia e visualize essa Jornada do Dynamic Media em um computador desktop.

## O que é o Dynamic Media e como ele pode ajudá-lo? {#dm-journey-a}

O Dynamic Media ajuda você a fornecer ativos avançados de merchandising visual e marketing sob demanda. Ele também ajuda a criar e fornecer experiências de visualização interativa, incluindo zoom, rotação de 360 graus e vídeo. Seus ativos são dimensionados dinamicamente para consumo em sites da Web, móveis e sociais. Usando um conjunto de ativos de origem primária, como imagens, vídeo e 3D, o Dynamic Media gera e entrega várias variações desse conteúdo avançado, em tempo real, por meio de sua CDN (Content Delivery Network, rede de entrega de conteúdo) global, escalável e otimizada para o desempenho.

O Dynamic Media incorpora os fluxos de trabalho da solução de gerenciamento de ativos digitais da Adobe Experience Manager Assets para simplificar e simplificar o processo de gerenciamento de campanhas digitais.

### Um arquivo com infinitas possibilidades

Um dos principais pontos para entender sobre o Dynamic Media é o conceito de _Um arquivo de ativo principal com infinitas possibilidades_.

Para entender melhor esse conceito, pense na maneira como você trabalha tradicionalmente com um único ativo, como uma imagem ou vídeo. Normalmente, você cria um ativo principal. Em seguida, você cria manualmente versões desse mesmo ativo para cada experiência, cada dispositivo necessário, cada página da Web e cada propriedade onde é usado. Com o tempo, esse único ativo pode crescer para 20, 30 ou mais versões, sem nenhum histórico de versões anexado a ele. Agora, imagine fazer isso para cada imagem ou vídeo que você tem. O número de versões de ativos rapidamente se tornaria enorme para manter e atualizar, sem mencionar o aumento nos custos de armazenamento.

No entanto, o Dynamic Media é fundamentalmente diferente de outros sistemas, pois você o usa para fornecer sua mídia _dinamicamente_ de ativos únicos e primários e de chamadas de URL. Os caminhos de URL do Dynamic Media solicitados incluem instruções que informam ao servidor de publicação do Adobe como exibir o ativo quando ele é entregue à tela de um cliente. Por exemplo, usando o mesmo único ativo principal, você pode fornecê-lo instantaneamente em representações ilimitadas, alterando o tamanho, o formato, a resolução, o peso, a cor, o recorte e os efeitos, como uma exibição de zoom.

Esse método de entrega exclusivo garante que experiências de qualidade consistentes sejam enviadas para qualquer tela, independentemente do tamanho ou da largura de banda. Vídeos em tamanho normal também são otimizados para todos os tipos de tela e transmitidos de maneira adaptável para garantir uma experiência do usuário consistente e de qualidade.

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![O Adobe Dynamic Media fornece a mesma imagem principal a mídias diferentes em tamanhos e formatos diferentes](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_O Adobe Dynamic Media garante que experiências consistentes e de qualidade sejam oferecidas em qualquer tela, independentemente do tamanho ou da largura de banda._

À medida que você lê, aprenderá mais sobre por que esse conceito de &quot;um arquivo de ativo principal, infinitas possibilidades&quot; é importante.

### A rede de entrega de conteúdo

Quando você está pronto para entrar em funcionamento com um ativo de imagem ou de vídeo, ele é compatível com o backbone do Dynamic Media, que consiste em uma rede de entrega avançada e de nível superior. A rede atende centenas de clientes em todo o mundo todos os dias. Os ativos são distribuídos na Rede de entrega de conteúdo - ou CDN - hospedada pela Akamai. A CDN é um sistema de serviços de computação em rede que cooperam de forma transparente para fornecer conteúdo, especialmente grandes conteúdos de mídia avançada, aos usuários finais.

No sistema CDN, o conteúdo da Web é armazenado em caches da Web na Internet. Em seguida, ele é entregue do cache da Web aos usuários finais para agilizar a entrega. Assim, na primeira vez que alguém baixa uma página da Web, os ativos que ele vê são entregues a um cache CDN. Eles são armazenados no servidor para que na próxima vez que alguém na mesma área acessar a página da Web, o mesmo conteúdo em cache seja entregue mais rapidamente. O conteúdo é entregue mais rápido porque está localizado mais próximo do usuário. Um CDN possibilita exibições mais rápidas da página da Web, além de diminuir as demandas de largura de banda do servidor central, pois o conteúdo é entregue a partir de uma rede de cache, não de um servidor central em cada instância. Esse fluxo otimizado significa uma melhor experiência do usuário, resultando em aumento das vendas.

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

Historicamente, a CDN fornece 3,5 petabytes de tráfego para os clientes todos os meses. O sistema pode entregar 52 bilhões de ativos em um único dia. Esse número equivale a 864.000 imagens e vídeos entregues com êxito aos clientes, _a cada segundo_.

### Imagem inteligente

O Dynamic Media já faz um excelente trabalho de otimização de ativos e garantia de que cada ativo seja carregado rapidamente em sistemas móveis e de desktop, por meio da CDN. Para fazer isso, as predefinições de imagem são usadas no Dynamic Media para definir a qualidade da sua imagem. Elas também definem o tipo de imagem que você está enviando, sua nitidez e outras partes para várias partes das suas experiências ou páginas.

Mas para adicionar valor ao Dynamic Media além das predefinições de imagem, há _Imagem inteligente_.

A Imagem inteligente oferece um desempenho ainda melhor do delivery de ativos de imagem, otimizando automaticamente o formato e o tamanho do arquivo de uma imagem com base no recurso de navegador do cliente. Ela funciona com suas predefinições de imagem existentes (as predefinições de imagem são discutidas na Parte II desta jornada) e usa inteligência no delivery.

Essa inteligência reduz ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador e da conexão de rede. Como os ativos de imagem compõem a maior parte do tempo de carregamento de uma página, a melhoria no desempenho pode ter um impacto completo nos principais indicadores de negócios, como:

* Maior conversão
* Tempo no site
* Menor taxa de rejeição do site

Em geral, com a geração inteligente de imagens, você pode esperar uma melhoria de desempenho de 22% a 47%, dependendo das configurações de predefinição de imagem existentes e das características específicas do usuário final. Tudo isso mantendo a qualidade da imagem como se ela nunca tivesse sido tocada.

![Imagens inteligentes](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_O Smart Imaging otimiza automaticamente o formato e o tamanho do arquivo de uma imagem com base na capacidade do navegador do cliente e na velocidade da rede._

A geração de imagens inteligentes não é ativada por padrão porque requer um esforço coordenado entre você e o suporte técnico do Adobe Dynamic Media. Além disso, a ativação do Smart Imaging requer a limpeza completa do cache da CDN, que é então reabastecido com tempo. Se você estiver interessado em usar Imagem inteligente, poderá trabalhar com o Adobe para ativá-la enviando um tíquete de suporte técnico. O suporte técnico fornece um parâmetro de URL que permite experimentar, antecipadamente, imagens inteligentes. Você pode experimentá-lo em qualquer uma de suas páginas da web ou imagens para que você possa ver o desempenho que você tem, e a economia. Você pode ativar a geração inteligente de imagens para seu site completo.

### Conjuntos de vídeos adaptados

Quando há um vídeo em uma página ou na página principal, seus clientes tendem a se envolver com esse conteúdo por mais tempo e permanecer na página por mais tempo, o que geralmente é uma boa coisa. Esse comportamento é exibido por meio de análises realizadas pela Adobe. No entanto, o vídeo pode ser complexo. Por um lado, você geralmente tem um arquivo principal grande. É complicado determinar o tamanho e o delivery do vídeo, tudo para garantir que a experiência seja executada sem problemas, independentemente do dispositivo em que está sendo visualizada e da largura de banda.

Para resolver esse problema, o Dynamic Media oferece a capacidade de criar _Conjuntos de vídeos adaptáveis_.

Um Conjunto de vídeos adaptados agrupa versões do mesmo vídeo codificadas em taxas de bits e formatos diferentes.

Você começa com seu vídeo original, o qual você carrega no sistema. O Dynamic Media dimensiona automaticamente, ou _transcodifica_, esse vídeo em vários vídeos. Em seguida, no momento do delivery, ele determina de forma inteligente qual tela de vídeo, qual qualidade e qual formato usar, além de fornecê-la ao telefone, tablet ou computador desktop.

Por exemplo, em um dispositivo móvel iOS, ele detecta uma largura de banda como 4G, 5G ou Wi-Fi. Em seguida, ele seleciona automaticamente o vídeo codificado correto entre as várias taxas de bits de vídeo no Conjunto de vídeos adaptados. O vídeo é transmitido para dispositivos móveis, tablets ou computadores de mesa.

Além disso, a qualidade do vídeo é comutada automaticamente de modo dinâmico se as condições da rede forem alteradas. E, se um cliente entrar no modo de tela cheia em um desktop, o Conjunto de vídeos adaptados responderá usando uma resolução melhor, melhorando a experiência de visualização do cliente.

O uso dos Conjuntos de vídeos adaptados oferece uma reprodução suave e de alta qualidade para clientes que reproduzem vídeos do Dynamic Media em várias telas e dispositivos. Isso realmente elimina a complexidade do vídeo.

## Casos de uso do Dynamic Media {#dm-journey-b}

Veja a seguir problemas comuns de casos de uso e soluções com as quais o Dynamic Media pode ajudá-lo a impulsionar um envolvimento positivo do cliente, fidelidade, conversão e aumento do ROI.

### Caso de uso: abordagem de arquivo principal

Um dos casos de uso mais importantes do Dynamic Media também é um dos mais óbvios. Ou seja, reduzindo o peso das páginas e experiências e o tamanho do conteúdo, seja uma imagem ou um vídeo que está sendo entregue.

Veja a seguir uma experiência típica ou uma página da Web. Cerca de 90% de uma página é composta de mídia avançada, como imagens e vídeos, que geralmente são arquivos muito mais pesados.

![Peso da página de conteúdo](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_Peso da página de conteúdo de uma página da Web típica._

Os 10% restantes são HTML, código CSS e tags específicas. Você deseja otimizar o peso de 90% dessa página, e o Dynamic Media ajuda nesse esforço. Você leu anteriormente sobre o conceito de _um arquivo de ativo principal com infinitas possibilidades_. Essa abordagem é significativa na redução do peso geral da página. A capacidade de pegar um ativo principal e usá-lo em uma página de detalhes do produto, uma página de miniatura, seu carrinho de compras e sua grade de pesquisa economiza tempo. E também garante a consistência entre as experiências.

![Abordagem de arquivo principal](/help/assets/dynamic-media/assets/dm-onefile.png)
_A observação é um arquivo de ativo principal, mas com várias representações - não cópias - criado em tempo real._

Vamos analisar mais detalhadamente os problemas que o Dynamic Media está solucionando com um arquivo e algumas das soluções para essa abordagem.

| **Problema** | **Solução do Dynamic Media** |
|---|---|
| Crie e armazene cada ativo. | Use um único arquivo de imagem, criando automaticamente as representações necessárias somente no momento do delivery. |
| Altos custos de armazenamento. | Elimina a necessidade de criar e armazenar várias cópias de um ativo. |
| Dificuldade em manter a cadeia de custódia. | Garante a entrega de experiências consistentes e otimizadas para dispositivos. |
| Nenhum histórico de versões. | |
| Experiências de marca inconsistentes entre dispositivos. | |
| Custo desnecessário da criação de ativos duplicados. | |

Ao pensar em um arquivo, você está criando um ativo para cada tipo de experiência. Você pode ter uma imagem inicial e, em seguida, criar 20, 30 ou 40 variações dessa imagem, que você terá que armazenar e pagar por esse armazenamento.

Em seguida, verifique se a imagem correta está sendo usada e se isso pode afetar sua capacidade de ter consistência entre as marcas. E, se não conseguir encontrar uma imagem, você terá que voltar no e duplicar esses ativos.

O Dynamic Media permite criar variações de imagens, em tempo real, a partir dessa imagem inicial. Ele permite que você seja criativo com esse ativo principal e não precise ir e voltar com seu artista de design gráfico ou estúdio de fotos para criar conteúdo adicional. E isso é dinheiro e tempo economizado.

Com a abordagem de um arquivo, você usa um único arquivo principal. Em seguida, crie as versões ou representações necessárias nos sites, propriedades e experiências, somente no momento em que forem entregues ou visualizadas por um cliente. Essa eficiência pode diminuir bastante a quantidade de armazenamento necessário para seus ativos e reduzir a complexidade geral do fluxo de trabalho. E com o sistema de entrega do Dynamic Media, ele garante que todas as imagens e vídeos sejam otimizados, carregados rapidamente e tenham uma ótima aparência em todas as telas e dispositivos.

### Caso de uso: Vídeo

Outro caso de uso para o qual o Dynamic Media pode ser resolvido é o vídeo. O vídeo é complexo. É difícil de gerenciar. Os arquivos de vídeo são desafiadores para armazenar e movimentar-se por causa de seus tamanhos de arquivo inerentes.

| **Problema** | **Solução do Dynamic Media** |
|---|---|
| Difícil de gerenciar e fornecer vídeo otimizado para vários dispositivos. | Use um único vídeo que seja dimensionado automaticamente para todos os dispositivos. |
| Os vídeos param ou são reproduzidos em baixa qualidade devido à largura de banda disponível do usuário. | Envie vídeos por meio de um reprodutor de HTML que detecta automaticamente a largura de banda disponível e adapta a qualidade para garantir alta fidelidade e reprodução sem problemas. |
| Inviável e demorado criar manualmente todas as versões de um vídeo, apenas para garantir uma boa exibição e reprodução entre dispositivos. | Elimine horas de trabalho entediante de transcodificação com um fluxo de trabalho simplificado. |
| | Libere tempo para um trabalho de maior valor. |

Os clientes acessam o Dynamic Media com os seguintes problemas que esperam resolver:

&quot;_Minha empresa tem o vídeo, e o departamento gastou uma grande quantidade de dinheiro criando-o, mas evitou colocá-lo em páginas ou entregá-lo. A razão era que, a partir de testes, a qualidade do vídeo não poderia ser garantida, ou mesmo se ele fosse realmente ir para a reprodução. E, em última análise, isso afeta a marca da empresa e potencialmente sua função na conversão._&quot;

A solução da Dynamic Media é pegar esse arquivo de vídeo principal e permitir que a Dynamic Media faça todos os tamanhos através de seu processo de transcodificação. Em seguida, combine-o com o player de vídeo inteligente do Dynamic Media. Esse fluxo de trabalho garante que você esteja usando esse vídeo na sua página de aterrissagem principal ou em uma categoria ou página de detalhes do produto, ele seja consistente e entregue com alta qualidade.

Estes são vários outros casos de uso a serem considerados.

### Caso de uso: única fonte da verdade

| **Problema** | **Solução do Dynamic Media** |
|---|---|
| Ativos digitais espalhados pela organização, em silos em diferentes equipes ou unidades de negócios. | Armazene e gerencie todos os ativos digitais em um local central. |
| Os membros da equipe baixam e criam versões locais. | Os membros da equipe usam um único arquivo primário para criar _e_ entregar todas as versões necessárias em vários dispositivos e tamanhos de tela. |
| Ativos de uso único criados para cada experiência e dispositivo. | Elimina ativos de uso único, economizando tempo e dinheiro para criá-los. |

### Caso de uso: corte inteligente alimentado por IA para mídia avançada

| **Problema** | **Solução do Dynamic Media** |
|---|---|
| É demorado e trabalhoso desenhar, medir e cortar manualmente imagens ou vídeos para destacar o ponto focal e exibir adequadamente em todos os tamanhos de tela e dispositivos. | O usa o Corte inteligente no Dynamic Media, um recurso de IA do Adobe, para detectar automaticamente o ponto focal em qualquer imagem ou vídeo e recortar para mantê-lo. |
| Tempo perdido que poderia ser mais bem gasto na criação de experiências de alto impacto. | Registra o ponto de interesse pretendido, independentemente do tamanho da tela. |
| Ativos de uso único criados para cada experiência e dispositivo. | Elimina tarefas manuais tediosas e fornece imagens e vídeos de alta qualidade e carregamento rápido que ficam bem em qualquer dispositivo ou tela. |

### Caso de uso: criação de mídia interativa

| **Problema** | **Solução do Dynamic Media** |
|---|---|
| Experiências estáticas e planas do cliente que não envolvem, geram fidelidade ou impulsionam a conversão. | Permite que usuários não técnicos adicionem elementos interativos de maneira fácil e contínua, como pontos de acesso, carrosséis e conjuntos de rotação, para proporcionar experiências mais dinâmicas e envolventes. |
| Retorno limitado sobre o investimento de ativos digitais e experiências de cliente pouco atraentes. | Impulsiona a conversão e o retorno sobre o investimento de experiências de mídia avançada. |

## Como um ativo flui pelo sistema Dynamic Media {#dm-journey-c}

A seguir, é mostrado um fluxo de trabalho típico do Dynamic Media.

![Fluxo de trabalho do Dynamic Media](/help/assets/dynamic-media/assets/dm-workflow.png)
_Como um ativo flui pelo sistema do Dynamic Media._

Você começa com a fase de criação com a meta principal de ter seu ativo principal no final. Esses ativos principais podem vir de sessões de fotos, de fornecedores de vídeo ou de alguns arquivos de áudio que você criou. Você pode usar os aplicativos do Creative Suite do Adobe, como o Adobe InDesign, o Adobe Photoshop e o Adobe Illustrator, para ajudar a resolver o problema.

Quando a parte de criação for concluída, você colocará o ativo na solução de criação carregando o ativo no Dynamic Media. No Dynamic Media, você deve ter as predefinições de imagem e os visualizadores certos alinhados para suas várias páginas da Web no site.

E, finalmente, você otimiza todo esse conteúdo e o publica nos servidores do Dynamic Media para que ele fique disponível para Web, impressão, e-mail, desktops e dispositivos móveis.

### Upload de ativos no Dynamic Media

Ao terminar de criar um ativo principal, faça upload dele para o Dynamic Media. O tipo de arquivo que você carrega, bem como o formato e o tamanho do arquivo, são atributos importantes do Dynamic Media. É no momento do upload que você deseja garantir que obtenha o valor máximo de um arquivo compatível.

Por exemplo, a imagem do relógio abaixo tem 4560 x 3020 pixels. E mesmo que você nunca use uma imagem desse tamanho, você ainda pode carregá-la. Quanto maior a imagem, melhor a qualidade que o Dynamic Media pode oferecer, até mesmo em uma representação de miniatura. Lembre-se: você pode facilmente _diminuir_ a resolução de uma imagem existente. Mas se você tentar _aumentar_ a resolução de uma imagem, o resultado provavelmente não será satisfatório.

![Formatos recomendados para carregar no Dynamic Media](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_Considerações para carregamentos de ativos._

A Adobe recomenda que você faça upload de ativos em um formato sem perdas. Geralmente, é melhor evitar o JPEG, pois ao fornecer o JPEG ou ao continuar a salvar o JPEG, você começa a perder a qualidade da imagem com o tempo. Você deseja começar com as imagens de maior resolução em um formato sem perdas com o qual possa viver. Normalmente, esse formato é um arquivo TIFF ou PNG.

Em relação ao espaço de cores, ao pensar em um canal digital ou visualização da Web, você geralmente pensa em RGB (vermelho, verde, azul).

A maioria nunca pensaria em fornecer algo em CMYK ou por que você poderia querer fornecer em CMYK. Isso ocorre porque esse espaço de cor é usado com mais frequência para entregar itens impressos. Porém, o Dynamic Media pode oferecer isso em ambos os espaços de cores.

Há muitos clientes que ainda fazem impressão, como clubes de atacado de armazém. E há supermercados que muitas vezes imprimem folhetos semanalmente. Esses clientes exigem que suas imagens estejam em ambos os espaços de cores. Tradicionalmente, isso exigiria duas imagens diferentes: uma no RGB e outra no CMYK. No entanto, é possível fazer upload de ativos CMYK diretamente no Dynamic Media e fazer com que o Dynamic Media forneça ativos do RGB por meio de uma predefinição de imagem ou por meio de um perfil de cores, automaticamente. Não há necessidade de criar várias versões de um arquivo, mantendo assim o conceito de _um arquivo de ativo principal com infinitas possibilidades_.

<!-- **The Value of Renditioning??? or Demo portion** -->

### Publicar e visualizar ativos

Após carregar os ativos no Dynamic Media, é recomendável _publicá-los_ selecionando-os e clicando em **[!UICONTROL Publicar]** ou **[!UICONTROL Publicação rápida]** no Dynamic Media. A publicação de ativos é necessária se você pretende usá-los em qualquer experiência. Depois que os ativos forem publicados, eles estarão disponíveis para inclusão em uma página da Web usando um URL gerado pelo Dynamic Media que você copia ou por meio da incorporação de código na página.

Além de publicar ativos manualmente, você pode configurar o Dynamic Media para publicar ativos instantaneamente, sem qualquer intervenção do usuário, no momento do upload.

Após o upload, há diferentes maneiras de pré-visualizar as representações de um ativo no Dynamic Media. Visualizar representações pode ajudar a fornecer uma ideia do que um cliente vê. Um método de visualização comum é selecionar um ativo e exibir suas representações ao selecionar uma _predefinição de imagem_, como visto a seguir.

![Visualização de uma representação de um ativo com base na predefinição de imagem grande](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_Pré-visualização de uma representação de um ativo com base na predefinição de imagem &quot;Grande&quot; selecionada. O botão URL foi clicado. O caminho de URL resultante contém o nome de predefinição de imagem &quot;Grande&quot; e pode ser usado em uma página da Web._

O URL acima está ativo. [Experimente](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$){target="_blank"}.

Outro método para visualizar um ativo é selecionar o ativo da imagem e, em seguida, selecionar uma predefinição de _Visualizadores_, como visto a seguir.

![Visualizando um ativo com base na predefinição do visualizador Zoom Vertical Light](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_Visualizando um ativo com base na predefinição do visualizador &quot;ZoomVertical_light&quot; selecionada. O ponteiro do mouse (`+`) foi movido sobre a inspeção para ampliar. Observe os botões URL e Incorporar._

A representação acima está ativa. [Experimente](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&config=jpearldemo/ZoomVertical_light){target="_blank"}.

## Opcional - Saiba mais

A parte I dessa jornada abordou as noções básicas de vários tópicos do Dynamic Media. Se você quiser saber mais sobre o que lê, utilize os materiais abaixo para explorar os conceitos com mais detalhes. Caso contrário, você pode continuar com a Parte II da sua jornada. Consulte [O que vem a seguir nesta Jornada do Dynamic Media](#whats-next).

<!--
_Dynamic Media Help topics_

* [Work with Dynamic Media in Experience Manager](/help/assets/dynamic-media/dynamic-media.md)
* [About Smart Imaging](/help/assets/dynamic-media/imaging-faq.md)
* [How to create Adaptive Video Sets](/help/assets/dynamic-media/video.md)
* [Best practices for optimizing the quality of your images](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [How to upload assets](/help/assets/add-assets.md#upload-assets)
* [How to preview assets](/help/assets/dynamic-media/previewing-assets.md)
* [How to preview 3D assets](/help/assets/dynamic-media/previewing-3d-assets.md)
* [How to deliver Dynamic Media Assets](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [How to publish assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [Work with Selective Publish in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md) -->

_Tutoriais do Dynamic Media_

* [Usar Dynamic Media com o Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html)
* [Biblioteca de conteúdo do Adobe Experience Manager](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (pesquisar no _Dynamic Media_)

_Visualizadores do Dynamic Media_

* [Demonstrações ao Vivo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) de cada visualizador

## O que vem a seguir nesta Jornada do Dynamic Media {#whats-next}

Na parte II desta jornada, você examina detalhadamente os URLs do Dynamic Media para entender melhor o que está acontecendo quando um ativo é entregue. Você também aprenderá mais sobre os fundamentos da criação de predefinições de imagens para renderizar ativos e sobre conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista, e como eles são criados.

Leve-me até [Dynamic Media Jornada: The Basics, Part II](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d).

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->