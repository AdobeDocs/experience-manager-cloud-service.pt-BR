---
title: Jornada para Dynamic Media, Parte II
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
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 1200dc41af22ae8f34f33d176de1c0db7c7ae424
workflow-type: tm+mt
source-wordcount: '2900'
ht-degree: 0%

---

# jornada Dynamic Media: Noções básicas, parte II  {#dm-journey-part2}

Bem-vindo ao Dynamic Media Jornada: Noções básicas, Parte II, onde você pode esperar aprender o seguinte:

* Anatomia de um URL do Dynamic Media e como o Dynamic Media fornece conteúdo
* Fundamentos da criação de predefinições de imagens para renderizar ativos
* Conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista

Consulte também [jornada Dynamic Media; Noções básicas, Parte I](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>Para obter melhores resultados, o Adobe recomenda que você leia e visualize esta Jornada Dynamic Media em um computador desktop.

## Anatomia de um URL do Dynamic Media e como o Dynamic Media fornece conteúdo {#dm-journey-d}

Depois que os ativos da Dynamic Media forem carregados e publicados, você poderá copiar o URL gerado de um ativo e colá-lo em seu navegador para ver como o ativo será exibido para um cliente. O URL copiado a seguir para uma imagem de observação é detalhado por cores para facilitar a leitura e a compreensão.

![Anatomia de um URL do Dynamic Media](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Anatomia de um URL do Dynamic Media._

A primeira parte do URL em vermelho é referenciar o próprio domínio do servidor. Nesse caso, o Dynamic Media está sendo executado em um domínio de servidor genérico, que é `https://s7d1.scene7.com/is/image/`. É fácil ver um conjunto de imagens e entender se elas estão sendo fornecidas pelo Dynamic Media apenas observando o domínio do servidor. O URL será bastante consistente. No entanto, há alguns clientes do Dynamic Media que mudaram para um domínio de servidor dedicado, onde ele pode estar `name-of-your-company.scene7.com`. Um domínio de servidor dedicado é necessário para o Smart Imaging.

O nome da conta é a parte em roxo. Nesse caso, a conta é chamada `jpearldemo`.

A ID ou o nome do ativo, `AdobeStock_28563982` está em verde. Observe que o ativo tem _não_ extensão de arquivo como `.png` ou `.jpg`. Quando os ativos são assimilados no Dynamic Media, a extensão de arquivo é removida e um tipo diferente de arquivo é criado: um arquivo TIFF pirâmid. O TIFF da pirâmica permite que o Dynamic Media crie rapidamente representações.

E finalmente, há alguns parâmetros de processamento de imagens. `?wid=1000&fmt=jpeg&qlt=85`, exibido em amarelo na extremidade.

O caminho do URL inteiro está ativo. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85){target=&quot;_blank&quot;}.

Com sua janela do navegador ainda aberta para o URL da Dynamic Media e a imagem de observação, vamos olhar mais de perto para como você pode criar representações da imagem apenas alterando o URL.

### Renderizar a imagem de observação por meio do URL

Comece excluindo manualmente apenas as regras de processamento de imagem no caminho do URL; deixe o nome do servidor, o nome da conta e a ID do ativo ou o nome da imagem. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target=&quot;_blank&quot;}.

Agora, adicione um parâmetro de processamento de imagem ao final do URL. No campo URL , à direita do nome da imagem, digite `?wid=500`e pressione **[!UICONTROL Enter]**. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target=&quot;_blank&quot;}.

Observe que uma nova representação do relógio é gerada. Uma opção importante para entender a partir desse simples exercício de alteração da largura da imagem é que a imagem vista é gerada 100% dinamicamente.

Agora, altere o valor de largura de `500` pixels para `1000` pixels e pressione **[!UICONTROL Enter]**. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000).
No momento em que você pressiona **[!UICONTROL Enter]**, o navegador volta para o servidor de imagem do Dynamic Media. Ele gera uma nova representação do relógio, com base no novo valor de largura que você acabou de digitar, depois entrega a nova imagem de volta ao navegador e a armazena em cache.

A Dynamic Media tem vários parâmetros de processamento de imagens que você pode usar para ajustar os ativos de imagem nas páginas da Web. Você pode [veja uma lista deles aqui](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en).

Agora tente adicionar um parâmetro de rotação à imagem de observação. E o final do caminho do URL, imediatamente após `wid=1000`, tipo `&rotate=90`e pressione **[!UICONTROL Enter]**. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90){target=&quot;_blank&quot;}.

O relógio ainda está um pouco inclinado para a esquerda. Alterar o valor de girar de `90` para `92`e pressione **[!UICONTROL Enter]**. [Experimente](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target=&quot;_blank&quot;}.

Novamente, no momento que você pressiona **[!UICONTROL Enter]**, uma nova representação do relógio é gerada de forma quase instantânea. Você pode ver o tipo de desempenho que você obtém, o que explica por que o Dynamic Media pode fornecer mais de 800.000 solicitações de imagem. _por segundo_, em um fim de semana ocupado ou grande feriado.

Embora seja possível alterar parâmetros de processamento de imagens em um URL com base em imagem, não é um método eficiente, especialmente se você tiver dezenas de milhares de imagens que compõem seu site. Uma abordagem muito melhor é usar predefinições de imagens.

## Fundamentos da criação de predefinições de imagens para renderizar ativos {#dm-journey-e}

Há várias maneiras e locais em que você deseja criar uma imagem ou ter uma imagem disponível. Tradicionalmente, um Criativo entra no Adobe Photoshop e salva cada uma dessas diferentes representações como imagens estáticas.

![Imagens estáticas](/help/assets/dynamic-media/assets/dm-static-images.png)
_Bom: imagens estáticas, cada uma criada manualmente._

Agora imaginem o Creative Director olha para as imagens e diz:

_&quot;Eu realmente queria essa foto para que a mão grande apontasse para os quatro, e a mão pequena apontasse para o 1 para tornar o relógio mais fácil de ver.&quot;_

O anúncio teria que refazer todas essas novas imagens estáticas novamente.

Mas, com o Dynamic Media, se você tiver predefinições de imagens diferentes, poderá usar essas imagens onde precisar. As predefinições de imagens impõem padrões.

![Abordagem de arquivo principal](/help/assets/dynamic-media/assets/dm-onefile.png)
_Melhor: um arquivo com várias representações criadas em tempo real usando predefinições de imagem, como `Search_Grid` e `Thumbnail`._

| **Por que usar predefinições de imagens?** |  |
|---|---|
| Padrões | As predefinições de imagens impõem um tratamento padrão de processamento de imagens em qualquer imagem que seja solicitada. |
| Gerenciamento de alterações | Se for necessário alterar o processamento da imagem, basta editar o parâmetro da predefinição de imagem existente. A definição atualizada é propagada automaticamente para todas as solicitações. |

Cada lugar que você precisa para ter um tipo específico de imagem, por exemplo,

* uma página de detalhes do produto,
* grade de pesquisa,
* miniatura,
* cartão de compra, ou
* imagem herói

Você quer que a imagem seja entregue com os mesmos parâmetros onde quer que sejam usados.

Por um momento, vamos observar como uma predefinição de imagem é criada no Dynamic Media.

![Criação de uma predefinição de imagem a partir da guia Básico](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_Criação de uma predefinição de imagem a partir da guia Básico ._

No exemplo acima, você pode ver que uma nova predefinição de imagem foi criada com o nome _Médio_. O Dynamic Media usa um exemplo, a imagem integrada - a mochila - para ajudá-lo a ver as características da predefinição de imagem à medida que você a cria.

O _Médio_ a predefinição de imagem tem uma largura de 500 pixels e uma altura de 800 pixels. Na Parte I desta Jornada, você lê sobre o fornecimento de ativos em diferentes formatos. No **[!UICONTROL Formato]** no menu suspenso, é possível optar por fornecer ativos como JPEG, PNG, TIFF ou vários outros formatos. Você tem flexibilidade aqui.

Selecionar o **[!UICONTROL Avançado]** fornece opções para o espaço de cores do ativo. Dependendo do formato selecionado no **[!UICONTROL Básico]** guia - no exemplo acima, o JPEG foi selecionado - é possível fornecer ativos em RGB, Escala de cinza ou CMYK. No **[!UICONTROL Perfil de cores]** no menu suspenso, é possível selecionar como fornecer um ativo de imagem CMYK a ser usado para impressão. Observe também que há parâmetros adicionais que você pode aplicar para ajustar a nitidez de suas imagens. Nesse caso, **[!UICONTROL Tirar nitidez da máscara]** foi aplicada.

![Criação de uma predefinição de imagem selecionando opções na guia Avançado](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_Criar uma predefinição de imagem selecionando opções na guia Avançado ._

Você se lembra de [Anatomia de um URL do Dynamic Media](#dm-journey-d) anteriormente, que você lia sobre o URL do Dynamic Media e como ele foi criado. O **[!UICONTROL Modificador de imagem]** caixa de texto é onde você pode digitar os parâmetros adicionais de processamento de imagens que desejar. Os parâmetros são incluídos no nome predefinido do URL quando suas imagens são entregues, usando a predefinição . Na captura de tela acima, o parâmetro `bgc=451B15` foi adicionado. Ou seja, foi adicionada uma cor de fundo castanho escuro.

Você pode pensar em uma predefinição de imagem como receita para suas imagens. Ele vai fornecer qualquer imagem que use a predefinição, consistentemente, sempre. vai ser o mesmo. O parâmetro `&op_brightness=+10` foi também adicionada para aumentar ligeiramente o brilho.

Quando terminar, salve a predefinição e agora ela estará disponível para todas as imagens que você tiver. Nesse caso, queremos aplicar a variável _Médio_ imagem predefinida para uma imagem de uma tigela de chocolate líquido.

![Aplicar a predefinição de imagem *Médio* para gerar uma representação de uma imagem](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_Aplicação da mídia predefinida da imagem para gerar uma representação de uma imagem._

Você copia o URL e o cola no navegador para verificar a aparência da imagem. [Experimente](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target=&quot;_blank&quot;}. No seu navegador, observe o nome da predefinição de imagem _Médio_ no caminho do URL completo.

Você pode ver o tipo de clareza que é exibido na imagem. Essa qualidade deve-se, em parte, à forma como a tigela do chocolate foi abatida. Além disso, é parcialmente porque com o Dynamic Media, você pode armazenar imagens maiores do que o que está sendo entregue aos canais digitais.

Se tudo parecer satisfatório para sua tigela de chocolate, cole o URL em suas páginas da Web onde deseja que a imagem apareça em seu site.

Se você olhar novamente para a imagem de relógio abaixo, você poderá ver que há uma `Cart` predefinição de imagem, um `Grid` predefinição, um `Large` predefinição, um `PDP-page` Predefinição (Página de detalhes do produto) e várias outras.

![Predefinições de imagens estáticas e dinâmicas](/help/assets/dynamic-media/assets/dm-image-presets.png)
_Predefinições de imagens estáticas e dinâmicas. A imagem de observação foi renderizada usando o `PDP-page` predefinição de imagem._

Mas e se você tiver que mudar uma imagem em seu site? Por exemplo, suponha que você tenha feito alguns testes e descobriu que a imagem de 120 x 120 (a variável `Cart` predefinição de imagem) não está sendo recebida tão bem quanto você pensava. Você deve tornar a imagem maior ao aumentar a largura para 175 pixels e aumentar a altura para 175 pixels. Tradicionalmente, você teria que entrar no Adobe Photoshop e recriar todas essas imagens do carrinho. No entanto, com o Dynamic Media, basta editar a predefinição de imagem, atualizando os valores de Largura e Altura para 175 e salvar sua predefinição, como mostrado no exemplo abaixo.

![Edição de uma predefinição de imagem](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_Editar a largura e a altura do `Cart` predefinição de imagem._

Depois de alterar sua predefinição de imagem e liberar o cache, todas as imagens serão atualizadas e todos os URLs que estão sendo usados com essa predefinição, faça _not_ mude em qualquer lugar. Isso significa que não são necessários links quebrados e redirecionamentos de página da Web.

## Conjuntos de imagens, Conjuntos de rotação e Conjuntos de mídia mista {#dm-journey-f}

Alguns dos usos mais populares do Dynamic Media são a capacidade de você criar Conjuntos de imagens, Conjuntos de rotação e Conjuntos de mídia mista.

Os conjuntos de imagens normalmente são compostos de uma série de ativos de imagem que são apresentados como uma única entidade. Esses tipos de conjuntos fornecem aos usuários uma experiência de visualização integrada, onde os usuários podem ver diferentes visualizações de um item clicando em uma imagem em miniatura. Os conjuntos de imagens permitem que você apresente visualizações alternativas de algo e o visualizador oferece ferramentas de zoom para examinar imagens cuidadosamente. [Exibir um conjunto de imagens chamado &quot;Em execução&quot; que usa o visualizador Flyout](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

Aqui dentro do Dynamic Media você pode ver várias imagens de tênis de corrida. É uma série de linhas de produto que as vendas e o marketing querem que os clientes vejam como uma única apresentação; um conjunto de imagens.

![Criação de um conjunto de imagens](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_O início da criação de um conjunto de imagens._

Para criar o conjunto de imagens, você escolhe **[!UICONTROL Conjunto de imagens]** do **[!UICONTROL Criar]** menu suspenso. Observe no menu que também há opções para criar um **[!UICONTROL Conjunto de mídias mistas]**, a **[!UICONTROL Conjunto de rotação]** e um **[!UICONTROL Conjunto de carrossel]**. Você cria esses conjuntos da mesma forma que um conjunto de imagens.

Um conjunto de mídias mistas pode conter imagens, conjuntos de amostras, conjuntos de rotação, vídeos e conjuntos de Vídeo adaptável. [Experimente](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). Um conjunto de rotação simula o ato real de girar um objeto para examiná-lo. Os conjuntos de rotação permitem visualizar os detalhes visuais principais a partir de qualquer ângulo. [Experimente](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400){target=&quot;_blank&quot;}.

Criar um conjunto de imagens é simples. Basta adicionar os ativos de imagem que deseja incluir no conjunto.

![Criação de um conjunto de imagens](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_O Editor do conjunto de imagens permite que você adicione ativos de imagem e reordene sua aparência no conjunto._

Você deve dar um nome ao conjunto. Escolha o nome com cuidado, pois não é possível editá-lo mais tarde! No exemplo acima, o conjunto é chamado de `Running`. Quando terminar, salve o conjunto.

E aqui está o `Running` Imagem definida no Experience Manager Assets.

![A imagem em execução definida no Experience Manager Assets, Exibição de cartão](/help/assets/dynamic-media/assets/dm-image-set.png)
_O `Running` Imagem definida no Experience Manager Assets, Exibição de cartão._

Caso tenha criado um conjunto de Imagens, um conjunto de Mídia mista, um conjunto de Rotação ou qualquer outra mídia interativa após a criação do conjunto, você deseja ver como ele é exibido e se comporta para um cliente. A Dynamic Media tem vários visualizadores integrados que permitem que você faça exatamente isso.

Você começa selecionando o conjunto de imagens criado para abri-lo em uma visualização, como mostrado no exemplo a seguir.

![O conjunto Imagem em execução na visualização com a opção Visualizadores selecionada](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_O `Running` Imagem definida na opção Visualizar com visualizadores selecionada._

Observe na visualização que você pode selecionar as amostras de sapato de corrida e aplicar zoom nos sapatos. Para aplicar um visualizador ao conjunto, selecione **[!UICONTROL Visualizadores]** no menu suspenso.

![O conjunto de imagens em execução com o visualizador do Flyout aplicado a ele](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_O `Running` Conjunto de imagens com o visualizador do Flyout aplicado a ele._

Nesse caso, a variável `Flyout` o visualizador foi selecionado. Nesse ponto, você pode visualizar o conjunto de imagens no visualizador. Mas é melhor vê-lo em seu navegador, como um cliente o vê. Você seleciona **[!UICONTROL URL]** no canto inferior esquerdo, copie o URL e o cole no navegador. [Experimente](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout){target=&quot;_blank&quot;}.

O URL único permite que você use o conjunto de imagens e o visualizador, onde você precisa, onde ele está no site. Você pode ter notado no exemplo anterior que **[!UICONTROL Incorporar]** é à direita do botão URL . Ao selecionar **[!UICONTROL Incorporar]**, você pode copiar o código desse conjunto de imagens/visualizador e adicioná-lo a uma página da Web ou a um componente do Experience Manager Sites.

O visualizador do Flyout é um visualizador padrão, pronto para uso, cujas propriedades podem ser editadas. Ou, assim como criar uma predefinição de imagem, você pode criar seu próprio visualizador personalizado.

Suponha que sua equipe de vendas e marketing não goste do visualizador do Flyout. Eles gostam do recurso de zoom, mas querem que os clientes vejam o efeito de zoom diretamente sobre os sapatos. Nesse caso, basta aplicar o visualizador InlineZoom ao conjunto de imagens e copiar e colar o URL no navegador para ver como ele se comporta. [Experimente](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom){target=&quot;_blank&quot;}.

Quando você move o ponteiro do mouse sobre o sapato, você amplia a imagem e pode ver mais detalhes enquanto você move o ponteiro. E a razão para isso é simplesmente o tamanho da imagem que foi inicialmente carregada no Dynamic Media.

À medida que você considera viver como um consumidor, ou à medida que você trabalha em sua função diária, e à medida que você vai para sites diferentes, você vê coisas assim. Pense sobre como isso está sendo feito, e como você pode usar o poder do Dynamic Media em seu próprio trabalho e no site de sua empresa.

Você acabou de ler um pouco sobre conjuntos de imagens e visualizadores. Vamos ver outros visualizadores e experimentá-los em ativos únicos. Para redefinir o visualizador, clique no botão **[!UICONTROL Atualizar]** no canto inferior esquerdo.

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` visualizador aplicado a um ativo de imagem. [Experimente](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark){target=&quot;_blank&quot;}.
* `Zoom_light` visualizador aplicado a uma imagem. [Experimente](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light){target=&quot;_blank&quot;}.

## Opcional - Saiba mais

Se você quiser saber mais sobre o que acabou de ler, use os materiais abaixo para explorar conceitos com mais detalhes. Caso contrário, a Jornada do Dynamic Media estará concluída!

_Tópicos da Ajuda do Dynamic Media_

* [Como criar predefinições de imagens](/help/assets/dynamic-media/image-presets.md)
* Uma lista de [parâmetros de processamento de imagens](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) que você pode usar no campo Modificador de imagem ao criar uma predefinição de imagem
* [Como visualizar ativos](/help/assets/dynamic-media/previewing-assets.md)
* [Como visualizar ativos 3D](/help/assets/dynamic-media/previewing-3d-assets.md)
* [Como criar Conjuntos de imagens](/help/assets/dynamic-media/image-sets.md)
* [Como criar conjuntos de rotação](/help/assets/dynamic-media/spin-sets.md)
* [Como criar conjuntos de mídia mista](/help/assets/dynamic-media/mixed-media-sets.md)

_Tutoriais do Dynamic Media_

* [Usar o Dynamic Media com Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=pt-BR)
* [Biblioteca de conteúdo do Adobe Experience Manager](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (pesquisar em _Dynamic Media_)

_Visualizadores do Dynamic Media_

* [Demonstrações ao vivo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) de cada visualizador

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->