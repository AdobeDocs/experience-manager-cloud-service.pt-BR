---
title: Jornada no Dynamic Media, Parte II
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
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '2621'
ht-degree: 0%

---

# Jornada do Dynamic Media: Noções básicas, parte II  {#dm-journey-part2}

{{see-also-dm}}

Bem-vindo ao Dynamic Media Jornada: Noções básicas, Parte II, onde você pode esperar para saber o seguinte:

* Anatomia de um URL do Dynamic Media e como o Dynamic Media fornece conteúdo.
* Princípios básicos da criação de predefinições de imagens para renderizar ativos.
* Conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista.

Consulte também [Jornada do Dynamic Media; Noções básicas, Parte I](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>Para obter melhores resultados, a Adobe recomenda que você leia e visualize essa Jornada do Dynamic Media em um computador desktop.

## Anatomia de um URL do Dynamic Media e como o Dynamic Media fornece conteúdo {#dm-journey-d}

Depois que os ativos do Dynamic Media forem carregados e publicados, você poderá copiar o URL gerado de um ativo e colá-lo no navegador para ver como o ativo aparecerá para um cliente. O URL copiado a seguir para uma imagem observada é dividido por cores para facilitar a leitura e a compreensão.

![Anatomia de uma URL de Dynamic Media](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Anatomia de uma URL do Dynamic Media._

A primeira parte do URL em vermelho faz referência ao próprio domínio do servidor. Nesse caso, o Dynamic Media está em execução em um domínio de servidor genérico, que é `https://s7d1.scene7.com/is/image/`. É fácil ver um conjunto de imagens e entender se elas estão sendo veiculadas pelo Dynamic Media apenas observando o domínio do servidor. O URL será bastante consistente. No entanto, alguns clientes do Dynamic Media mudaram para um domínio de servidor dedicado, onde pode ser `name-of-your-company.scene7.com`. Um domínio de servidor dedicado é necessário para a Imagem inteligente.

O nome da conta é a parte em roxo. Nesse caso, a conta é chamada `jpearldemo`.

A ID ou o nome do ativo `AdobeStock_28563982` está em verde. Observe que o ativo tem _não_ extensão de arquivo, como `.png` ou `.jpg`. Quando os ativos são assimilados no Dynamic Media, a extensão de arquivo é removida e um tipo diferente de arquivo é criado: um arquivo de pirâmide TIFF. A pirâmide do TIFF permite que o Dynamic Media crie representações rapidamente.

E finalmente, existem alguns parâmetros de processamento de imagens, `?wid=1000&fmt=jpeg&qlt=85`, mostrados em amarelo no final.

O caminho do URL inteiro está ativo. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&fmt=jpeg&qlt=85){target="_blank"}.

Com a janela do navegador ainda aberta para o URL do Dynamic Media e a imagem do relógio, vamos examinar mais detalhadamente como criar representações da imagem simplesmente alterando o URL.

### Renderização da imagem observada por meio do URL

Comece excluindo manualmente apenas as regras de processamento de imagem no caminho do URL; deixe o nome do servidor, o nome da conta e a ID do ativo ou o nome da imagem. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target="_blank"}.

Agora adicione um parâmetro de processamento de imagem ao final do URL. No campo URL, à direita do nome da imagem, digite `?wid=500` e pressione **[!UICONTROL Enter]**. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target="_blank"}.

Observe que é gerada uma nova representação da inspeção. Uma vantagem importante para entender esse simples exercício de alteração da largura da imagem é que a imagem vista é gerada 100% dinamicamente.

Agora altere o valor de largura de `500` pixels para `1000` pixels e pressione **[!UICONTROL Enter]**. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target="_blank}.
No momento em que você pressiona **[!UICONTROL Enter]**, o navegador retorna ao Servidor de Imagens do Dynamic Media. Ele gera uma representação totalmente nova do relógio, com base no novo valor de largura que você acabou de inserir, em seguida, fornece a nova imagem de volta ao navegador e a armazena em cache.

O Dynamic Media tem vários parâmetros de processamento de imagens que você pode usar para ajustar os ativos de imagem nas páginas da Web. Você pode [ver uma lista deles aqui](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=pt-BR).

Agora, tente adicionar um parâmetro de rotação à imagem observada. E o fim do caminho da URL, imediatamente após `wid=1000`, digite `&rotate=90` e pressione **[!UICONTROL Enter]**. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&rotate=90){target="_blank"}.

O relógio ainda está ligeiramente inclinado para a esquerda. Altere o valor de rotação de `90` para `92` e pressione **[!UICONTROL Enter]**. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&rotate=9){target="_blank"}.

Novamente, no momento em que você pressiona **[!UICONTROL Enter]**, uma nova representação do relógio é gerada quase instantaneamente. Você pode observar o tipo de desempenho obtido, o que explica por que o Dynamic Media pode fornecer mais de 800.000 solicitações de imagem, _por segundo_, em um fim de semana movimentado ou em um feriado importante.

Embora seja possível alterar os parâmetros de processamento de imagem em um URL imagem por imagem, não é um método eficiente, especialmente se você tiver dezenas de milhares de imagens que compõem seu site. Uma abordagem muito melhor é usar predefinições de imagem.

## Princípios básicos da criação de predefinições de imagens para renderizar ativos {#dm-journey-e}

Há várias maneiras e lugares em que você desejará criar uma imagem ou disponibilizar uma imagem. Tradicionalmente, um Creative entra no Adobe Photoshop e salva cada uma dessas representações diferentes como imagens estáticas.

![Imagens estáticas](/help/assets/dynamic-media/assets/dm-static-images.png)
_Bom: imagens estáticas, cada uma criada manualmente._

Agora imagine que o Diretor do Creative olhe para as imagens e diga:

_&quot;Eu realmente queria esta captura para que a mão grande apontasse para as quatro, e a mão pequena apontasse para a 1 para facilitar a visualização do mostrador do relógio.&quot;_

O criativo teria que refilmar todas as novas imagens estáticas novamente.

Porém, com o Dynamic Media, se você tiver predefinições de imagens diferentes, poderá usá-las sempre que precisar delas. As predefinições de imagens impõem padrões.

![Abordagem de arquivo principal](/help/assets/dynamic-media/assets/dm-onefile.png)
_Melhor: um arquivo com várias representações criadas em tempo real usando predefinições de imagem, como `Search_Grid` e `Thumbnail`._

| **Por que usar predefinições de imagens?** | |
|---|---|
| Padrões | As predefinições de imagem impõem um tratamento de processamento de imagem padrão em qualquer imagem com a qual ela é solicitada. |
| Gerenciamento de alterações | Se precisar alterar o processamento da imagem, basta editar o parâmetro da predefinição de imagem existente. A definição atualizada é propagada automaticamente para todas as solicitações. |

Cada local necessário para ter um tipo específico de imagem, por exemplo,

* uma página de detalhes do produto,
* grade de pesquisa,
* miniatura,
* cartão de compra, ou
* imagem herói

Essa imagem deve ser entregue com os mesmos parâmetros onde quer que eles sejam usados.

Por um momento, vamos examinar como uma predefinição de imagem é criada no Dynamic Media.

![Criando uma predefinição de imagem começando com a guia Básico](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_Criando uma predefinição de imagem começando com a guia Básico._

No exemplo acima, você pode ver que uma nova predefinição de imagem foi criada com o nome _Medium_. O Dynamic Media usa um exemplo de imagem pronta para uso - a mochila - para ajudá-lo a ver as características da predefinição de imagem ao criá-la.

A predefinição de imagem _Medium_ tem uma largura de 500 pixels e uma altura de 800 pixels. Na Parte I desta Jornada, você lê sobre como fornecer ativos em diferentes formatos. No menu suspenso **[!UICONTROL Formatar]**, você pode optar por fornecer ativos como JPEG, PNG, TIFF ou vários outros formatos. Você tem flexibilidade aqui.

Selecionar a guia **[!UICONTROL Avançado]** fornece opções para o espaço de cores do ativo. Dependendo do formato selecionado na guia **[!UICONTROL Básico]** - no exemplo acima, o JPEG foi selecionado - você pode entregar ativos no RGB, em Tons de Cinza ou CMYK. No menu suspenso **[!UICONTROL Perfil de Cores]**, você pode selecionar como fornecer um ativo de imagem CMYK a ser usado para impressão. Observe também que há parâmetros adicionais que você pode aplicar para ajustar a nitidez das imagens. Neste caso, **[!UICONTROL Tirar nitidez da máscara]** foi aplicada.

![Criando uma predefinição de imagem selecionando opções na guia Avançado](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_Criando uma predefinição de imagem selecionando opções na guia Avançado._

Você lembra, em [Anatomia de um URL do Dynamic Media](#dm-journey-d) anteriormente, que leu sobre o URL do Dynamic Media e como ele é criado. A caixa de texto **[!UICONTROL Modificador de Imagem]** é onde você pode digitar os parâmetros de processamento de imagem adicionais desejados. Os parâmetros são incluídos no nome predefinido do URL quando as imagens são entregues, usando a predefinição. Na captura de tela acima, o parâmetro `bgc=451B15` foi adicionado. Ou seja, uma cor de fundo marrom-escuro foi adicionada.

Pense em uma predefinição de imagem como uma fórmula para suas imagens. Ele vai mostrar todas as imagens que usam a predefinição, de forma consistente, sempre; e vai ser o mesmo. O parâmetro `&op_brightness=+10` também foi adicionado para aumentar um pouco o brilho.

Quando terminar, salve a predefinição e ela agora estará disponível para todas as imagens que você tiver. Neste caso, você deseja aplicar a predefinição de imagem _Medium_ a uma imagem de uma tigela de chocolate líquido.

![Aplicando a predefinição de imagem *Medium* para gerar uma representação de uma imagem](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_Aplicando o Medium de predefinição de imagem para gerar uma representação de uma imagem._

Você copia o URL e o cola no navegador para verificar a aparência da imagem. [Experimente](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target="_blank"}.

Em seu navegador, observe o nome da predefinição de imagem _Medium_ no caminho completo da URL.

Você pode ver o tipo de clareza que é exibida na imagem. Essa qualidade é em parte devido ao modo como a tigela de chocolate foi filmada. Além disso, em parte porque, com o Dynamic Media, você pode armazenar imagens maiores do que o que está sendo entregue aos canais digitais.

Se tudo parece satisfatório para o seu prato de chocolate, você cola o URL em suas páginas da web onde você deseja que a imagem apareça em seu site.

Se você observar a imagem abaixo novamente, verá que há uma predefinição de imagem `Cart`, uma predefinição `Grid`, uma predefinição `Large`, uma predefinição `PDP-page` (Página de detalhes do produto) e várias outras.

![Predefinições de imagens estáticas e dinâmicas](/help/assets/dynamic-media/assets/dm-image-presets.png)
_Predefinições de imagens estáticas e dinâmicas. A imagem observada foi renderizada usando a predefinição de imagem `PDP-page`._

Mas e se você tiver que mudar uma imagem no seu site? Por exemplo, suponha que você tenha feito alguns testes e descobriu que a imagem de 120 x 120 (a predefinição de imagem `Cart`) não está sendo recebida como você pensava. É necessário aumentar a imagem, aumentando a largura para 175 pixels e a altura para 175 pixels. Tradicionalmente, você teria que entrar no Adobe Photoshop e recriar todas essas imagens do carrinho. Porém, com o Dynamic Media, basta editar a predefinição da imagem, atualizando os valores de Largura e Altura para 175, e salvar a predefinição, como visto no exemplo abaixo.

![Editando uma predefinição de imagem](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_Editando a Largura e a Altura da predefinição de imagem `Cart`._

Depois de alterar a predefinição de imagem e liberar o cache, todas as imagens são atualizadas e todas as URLs que estão sendo usadas com essa predefinição são alteradas para qualquer lugar. __ Isso significa que não há links quebrados nem redirecionamentos de página da Web necessários.

## Conjuntos de imagens, conjuntos de rotação e conjuntos de mix de mídia {#dm-journey-f}

Alguns dos usos mais populares do Dynamic Media são a capacidade de criar conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista.

Os conjuntos de imagens normalmente são compostos de uma série de ativos de imagem que são apresentados como uma única entidade. Esses tipos de conjuntos oferecem aos usuários uma experiência de visualização integrada, em que os usuários podem ver diferentes visualizações de um item clicando em uma imagem em miniatura. Os conjuntos de imagens permitem apresentar visualizações alternativas de algo e o visualizador oferece ferramentas de zoom para examinar as imagens de perto. [Exiba um conjunto de imagens chamado &quot;Em execução&quot; que usa o visualizador Flyout](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

Aqui dentro do Dynamic Media você pode ver várias imagens de tênis de corrida. É uma série de linhas de produtos que as equipes de vendas e marketing desejam que os clientes visualizem como uma única apresentação; um conjunto de imagens.

![Criando um conjunto de imagens](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_O início da criação de um conjunto de imagens._

Para criar o Conjunto de imagens, escolha **[!UICONTROL Conjunto de imagens]** no menu suspenso **[!UICONTROL Criar]**. Observe no menu que também há opções para criar um **[!UICONTROL Conjunto de mídias mistas]**, um **[!UICONTROL Conjunto de rotação]** e um **[!UICONTROL Conjunto de carrossel]**. Esses conjuntos são criados da mesma forma que um conjunto de imagens.

Um conjunto de Mídia mista pode conter imagens, conjuntos de amostras, conjuntos de rotação, vídeos e conjuntos de Vídeo adaptável. [Experimente](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). Um conjunto de rotação simula o ato do mundo real de virar um objeto para examiná-lo. Os conjuntos de rotação permitem visualizar os principais detalhes visuais de qualquer ângulo. [Experimente](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&stagesize=500,400){target="_blank"}.

Criar um conjunto de imagens é simples. Basta adicionar os ativos de imagem que deseja incluir no conjunto.

![Criando um conjunto de imagens](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_O Editor do Conjunto de Imagens permite adicionar ativos de imagem e reordenar sua aparência no conjunto._

É necessário dar um nome ao conjunto. Escolha o nome com cuidado porque não é possível editá-lo posteriormente! No exemplo acima, o conjunto é chamado `Running`. Quando terminar, salve o conjunto.

E aqui está a imagem `Running` definida no Experience Manager Assets.

![A imagem em execução definida no Experience Manager Assets, Exibição de Cartão](/help/assets/dynamic-media/assets/dm-image-set.png)
_A imagem `Running` definida no Experience Manager Assets, Exibição de Cartão._

Independentemente de ter criado um conjunto de imagens, um conjunto de mídia mista, um conjunto de rotação ou qualquer outra mídia interativa após a criação do conjunto, você deseja ver como ele aparece e se comporta para um cliente. O Dynamic Media tem vários visualizadores integrados que permitem fazer exatamente isso.

Você começa selecionando o conjunto de imagens criado para abri-lo em uma visualização, como pode ser visto no exemplo a seguir.

![O conjunto de imagens em execução na visualização com a opção Visualizadores selecionada](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_O conjunto de imagens `Running` na visualização com a opção Visualizadores selecionada._

Observe na visualização que é possível selecionar as amostras de sapato de corrida e aplicar mais ou menos zoom nos sapatos. Para aplicar um visualizador ao conjunto, selecione **[!UICONTROL Visualizadores]** no menu suspenso.

![O conjunto de imagens em execução com o visualizador Flyout aplicado a ele](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_O conjunto de imagens `Running` com o visualizador Flyout aplicado a ele._

Nesse caso, o visualizador `Flyout` foi selecionado. Nesse ponto, é possível visualizar o conjunto de imagens no visualizador. Porém, é melhor visualizá-lo em seu navegador, exatamente como um cliente o vê. Você seleciona **[!UICONTROL URL]** no canto inferior esquerdo, copia a URL e a cola no navegador. [Experimente](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&config=jpearldemo/Flyout){target="_blank"}.

O URL único permite usar o conjunto de imagens e o visualizador onde você precisa deles em seu site. Você pode ter notado no exemplo anterior que **[!UICONTROL Incorporar]** está à direita do botão URL. Ao selecionar **[!UICONTROL Incorporar]**, você pode copiar o código deste conjunto de imagens/visualizador e adicioná-lo a uma página da Web ou a um componente do Experience Manager Sites.

O visualizador Flyout é um visualizador padrão pronto para uso cujas propriedades você pode editar. Ou, assim como criar uma predefinição de imagem, você pode criar seu próprio visualizador personalizado.

Suponha que sua equipe de vendas e marketing não goste do visualizador de Flyout. Eles gostam do recurso de zoom, mas querem que os clientes vejam o efeito de zoom diretamente sobre os sapatos. Nesse caso, basta aplicar o visualizador InlineZoom ao conjunto de imagens e copiar e colar seu URL no navegador para ver como ele se comporta. [Experimente](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&config=jpearldemo/InlineZoom){target="_blank"}.

Quando você move o ponteiro do mouse sobre o sapato, amplia a imagem e vê mais detalhes enquanto move o ponteiro. E a razão para isso é simplesmente o tamanho da imagem que foi inicialmente carregada no Dynamic Media.

Enquanto você considera viver como um consumidor, ou enquanto você trabalha em seu papel diário, e conforme você vai a sites diferentes, você vê coisas como essas. Pense sobre como isso está sendo feito e como você pode usar o poder do Dynamic Media em seu próprio trabalho e no site de sua empresa.

Você leu sobre conjuntos de imagens e visualizadores. Vamos analisar outros visualizadores e testá-los em ativos únicos. Para redefinir o visualizador, clique no botão **[!UICONTROL Atualizar]** no canto inferior esquerdo.

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* Visualizador `ZoomVertical_dark` aplicado a um ativo de imagem. [Experimente](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&config=jpearldemo/ZoomVertical_dark){target="_blank"}.
* Visualizador `Zoom_light` aplicado a uma imagem. [Experimente](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&config=jpearldemo/Zoom_light){target="_blank"}.

## Opcional - Saiba mais

Se você quiser saber mais sobre o que acabou de ler, use os materiais abaixo para explorar os conceitos com mais detalhes. Caso contrário, sua Jornada do Dynamic Media estará concluída!

<!--
_Dynamic Media Help topics_

* [How to create image presets](/help/assets/dynamic-media/image-presets.md)
* A list of [image processing parameters](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=pt-BR) that you can use in the Image Modifier field when you create an image preset
* [How to preview assets](/help/assets/dynamic-media/previewing-assets.md)
* [How to preview 3D assets](/help/assets/dynamic-media/previewing-3d-assets.md)
* [How to create Image sets](/help/assets/dynamic-media/image-sets.md)
* [How to create Spin sets](/help/assets/dynamic-media/spin-sets.md)
* [How to create Mixed Media sets](/help/assets/dynamic-media/mixed-media-sets.md) -->

_Tutoriais do Dynamic Media_

* [Usar Dynamic Media com o Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=pt-BR)
* [Biblioteca de conteúdo do Adobe Experience Manager](https://experienceleague.adobe.com/pt-br?lang=en#recommended/solutions/experience-manager) (pesquisar no _Dynamic Media_)

_Visualizadores do Dynamic Media_

* [Demonstrações ao Vivo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) de cada visualizador

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->