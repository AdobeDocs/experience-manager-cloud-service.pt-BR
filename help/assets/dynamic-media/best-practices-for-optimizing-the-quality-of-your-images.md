---
title: Práticas recomendadas para otimização da qualidade de imagens
description: Conheça as práticas recomendadas que ajudam você a otimizar a qualidade dos seus ativos de imagem usando o Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management, Best Practices
role: User
exl-id: 2efc4a27-01d7-427f-9701-393497314402
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 1%

---

# Práticas recomendadas para otimização da qualidade de imagens {#best-practices-for-optimizing-the-quality-of-your-images}

{{work-with-dynamic-media}}

A otimização da qualidade da imagem pode ser um processo demorado, pois muitos fatores contribuem para a obtenção de resultados aceitáveis. O resultado é parcialmente subjetivo porque os indivíduos percebem a qualidade da imagem de forma diferente. A experimentação estruturada é fundamental.

O Adobe Experience Manager inclui mais de 100 comandos de entrega de imagem do Dynamic Media para ajustar e otimizar imagens e renderizar resultados. As diretrizes a seguir podem ajudar você a simplificar o processo e obter bons resultados rapidamente usando alguns comandos essenciais e práticas recomendadas.

<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## Ativar imagem inteligente no Dynamic Media {#bp-enable-smart-imaging}

**Imagens inteligentes:**

* A ativação da Imagem inteligente no Dynamic Media permite a otimização automática do formato, do tamanho e da qualidade da imagem com base nos recursos do navegador do cliente.
Quer saber mais? Vá para [Smart Imaging](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/imaging-faq).
* Ele melhora o desempenho do delivery de imagens ajustando dinamicamente esses parâmetros.
* Você pode avaliar o Smart Imaging usando a ferramenta de autoavaliação [Snapshot](https://snapshot.scene7.com/).

**Formatos de imagem:**

* Evite usar comandos `fmt=webp` ou `fmt=avif` explícitos em uma URL, a menos que especificamente necessário para um caso de uso.
* O Smart Imaging seleciona automaticamente o melhor formato, resultando em ganhos ideais de largura de banda.

**Comportamento padrão:**

* Quando nenhum comando format é especificado no URL e o Smart Imaging não está habilitado, a entrega da imagem do Dynamic Media é padronizada como o uso do formato JPEG.

Ao fazer escolhas informadas sobre formatos de imagem e ativar a Imagem inteligente, você pode afetar significativamente o desempenho e a experiência do usuário.


<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## Práticas recomendadas para selecionar a imagem de origem {#bp-select-source-image}

Considerações essenciais para trabalhar com imagens de origem:

* **Formato de imagem do Source:**
   * O uso de formatos sem perda, como PNG, TIFF ou PSD, garante que a qualidade da imagem permaneça alta sem artefatos de compactação.
   * Esses formatos preservam todos os dados originais, tornando-os ideais para edição e processamento adicional.
* **Tamanho da imagem do Source:**
   * Começar com uma imagem de alta resolução fornece mais detalhes e flexibilidade.
   * Quando as imagens precisam ser exibidas em tamanhos diferentes (por exemplo, em dispositivos ou resoluções de tela), ter uma imagem de origem maior permite um melhor dimensionamento.
   * Para imagens que oferecem suporte ao zoom (como fotos de produtos), direcione para dimensões de cerca de 2.000 pixels ou mais no lado mais longo.
   * Os logotipos ou banners que não exigem zoom podem ser carregados no maior tamanho necessário para o uso a que se destinam.

Ao fazer essas escolhas cuidadosas no nível da origem, você pode contribuir significativamente para a qualidade geral do seu conteúdo visual.

<!-- REMOVED TOPIC AS PER CQDOC-21594
## Best practices for image format (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG or PNG are the best choices to deliver images in good quality and with manageable size and weight.
* If no format command is supplied in the URL, Dynamic Media Image Delivery defaults to JPG for delivery.
* JPG compresses at a ratio of 10:1 and usually produces smaller image file sizes. PNG compresses at a ratio of about 2:1, except when images contain a white background. Typically though, PNG file sizes are larger than JPG files.
* JPG uses lossy compression, meaning that picture elements (pixels) are dropped during compression. PNG on the other hand uses lossless compression.
* JPG often compresses photographic images with better fidelity than synthetic images with sharp edges and contrast.
* If your images contain transparency, use PNG because JPG does not support transparency.

As a best practice for image format, start with the most common setting `&fmt=JPG`. -->

## Práticas recomendadas para tamanho de imagem {#best-practices-for-image-size}

Reduzir dinamicamente o tamanho da imagem é uma das tarefas mais comuns. Envolve a especificação do tamanho e, opcionalmente, o modo de redução da resolução usado para diminuir a escala da imagem.

* Para dimensionamento de imagem, a melhor e mais simples abordagem é usar `&wid=<value>` e `&hei=<value>,` ou apenas `&hei=<value>`. Esses parâmetros definem automaticamente a largura da imagem de acordo com a taxa de proporção.
* `&resMode=<value>`controla o algoritmo usado para reduzir a resolução. Comece com `&resMode=sharp2`. Esse valor fornece a melhor qualidade de imagem. Embora o uso da redução de resolução `value =bilin` seja mais rápido, geralmente resulta no uso de alias de artefatos.

Como prática recomendada para dimensionamento de imagem, use `&wid=<value>&hei=<value>&resMode=sharp2` ou `&hei=<value>&resMode=sharp2`

## Práticas recomendadas para nitidez de imagem {#best-practices-for-image-sharpening}

A nitidez de imagem é o aspecto mais complexo de controlar imagens no seu site e no qual muitos erros são cometidos. Reserve tempo para saber mais sobre como a nitidez e o mascaramento sem nitidez funcionam no Experience Manager, consultando os seguintes recursos úteis:

* White paper de práticas recomendadas [As práticas recomendadas de qualidade e nitidez de imagens da Adobe Dynamic Media Classic](/help/assets/dynamic-media/assets/sharpening_images.pdf) também se aplicam ao Experience Manager.

* Assista [Usar nitidez de imagem com o Experience Manager - Dynamic Media](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media).

Com o Experience Manager, você pode ajustar a nitidez de imagens na assimilação, no delivery ou em ambos. No entanto, geralmente é melhor ajustar a nitidez de imagens usando apenas um método ou outro, mas não ambos. A nitidez de imagens no delivery, em um URL, normalmente fornece os melhores resultados.

Há dois métodos de nitidez de imagem que podem ser usados:

* Nitidez simples ( `&op_sharpen`) - Semelhante ao filtro de nitidez usado no Photoshop, a nitidez simples aplica a nitidez básica à exibição final da imagem após o redimensionamento dinâmico. No entanto, esse método não é configurável pelo usuário. A prática recomendada é evitar o uso de `&op_sharpen`, a menos que seja necessário.
* Mascaramento sem nitidez ( `&op_USM`) - O mascaramento sem nitidez é um filtro de nitidez padrão do setor. A prática recomendada é tornar mais nítidas as imagens com mascaramento sem nitidez, seguindo as diretrizes abaixo. O mascaramento sem nitidez permite controlar os três parâmetros a seguir:

   * `&op_sharpen=`valor,raio,limite

      * **[!UICONTROL quantidade]** (0-5, intensidade do efeito.)
      * **[!UICONTROL raio]** (0-250, largura das &quot;linhas de nitidez&quot; desenhadas ao redor do objeto com nitidez, conforme medido em pixels.)

     Lembre-se de que o raio e a quantidade dos parâmetros funcionam uns contra os outros. A redução do raio pode ser compensada pelo aumento da quantidade. O raio permite um controle mais fino, pois um valor mais baixo aplica nitidez apenas aos pixels da borda, enquanto um valor mais alto aplica nitidez a uma faixa mais ampla de pixels.

      * **[!UICONTROL limite]** (0-255, sensibilidade de efeito.)

     Esse parâmetro determina como deve ser a diferença dos pixels com nitidez em relação à área ao redor antes de serem considerados pixels de borda e o filtro ajuste a nitidez deles. O parâmetro **[!UICONTROL threshold]** ajuda a evitar áreas de nitidez excessiva com cores semelhantes, como tons de pele. Por exemplo, um valor limite de 12 ignora pequenas variações no brilho do tom da pele para evitar a adição de &quot;ruído&quot;, enquanto ainda adiciona o contraste da borda a áreas de alto contraste, como onde as pálpebras tocam a pele.

     Para obter mais informações sobre como você define esses três parâmetros, incluindo as práticas recomendadas para usar com o filtro, consulte os seguintes recursos:

      * White paper de práticas recomendadas [As práticas recomendadas de qualidade e nitidez de imagens da Adobe Dynamic Media Classic](/help/assets/dynamic-media/assets/sharpening_images.pdf) também se aplicam ao Experience Manager.

      * Assista [Usar nitidez de imagem com o Experience Manager - Dynamic Media](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media).

      * O Experience Manager também permite controlar um quarto parâmetro: monocromático (0,1). Esse parâmetro determina se a máscara de nitidez é aplicada separadamente a cada componente de cor usando o valor 0 ou ao brilho/intensidade da imagem usando o valor 1.

Como prática recomendada, comece com o parâmetro Tirar nitidez do raio da máscara. As configurações de raio com as quais você pode começar são as seguintes:

* **[!UICONTROL Site]**: 0,2-0,3 pixels
* **[!UICONTROL Impressão fotográfica (250-300 ppi)]**: 0,3-0,5 pixels
* **[!UICONTROL Impressão deslocada (266-300 ppi)]**: 0,7-1,0 pixels
* **[!UICONTROL Impressão da tela de desenho (150 ppi)]**: 1,5-2,0 pixels

Aumente gradualmente a quantidade de 1,75 para 4. Se a nitidez ainda não for a desejada, aumente o raio em um ponto decimal e execute a quantidade novamente de 1,75 para 4. Repita conforme necessário.

Deixe a configuração de parâmetro monocromático em 0.

### Práticas recomendadas para compactação JPEF (`&qlt=`) {#best-practices-for-jpef-compression-qlt}

* Esse parâmetro controla a qualidade da codificação do JPG. Um valor mais alto significa uma imagem de qualidade superior, mas um tamanho de arquivo grande; como alternativa, um valor mais baixo significa uma imagem de qualidade inferior, mas um tamanho de arquivo menor. O intervalo desse parâmetro é de 0 a 100.
* Para otimizar a qualidade, não defina o valor do parâmetro como 100. A diferença entre um ajuste de 90 ou 95 e 100 é quase imperceptível. No entanto, 100 aumentam desnecessariamente o tamanho do arquivo de imagem. Portanto, para otimizar a qualidade, mas evitar que os arquivos de imagem fiquem muito grandes, defina o `qlt= value` como 90 ou 95.
* Para otimizar um tamanho de arquivo de imagem pequeno, mas manter a qualidade da imagem em um nível aceitável, defina o `qlt= value` como 80. Valores abaixo de 70 a 75 resultam em degradação significativa da qualidade da imagem.
* Como prática recomendada, para ficar no meio, defina o `qlt= value` como 85 para ficar no meio.
* Usando o sinalizador de croma em `qlt=`

   * O parâmetro `qlt=` tem uma segunda configuração que permite ativar a redução de resolução de cromaticidade de RGB usando o valor `,1` ou desativado usando o valor `,0`.
   * Para simplificar, comece com a redução de resolução de cromaticidade do RGB desativada (`,0`). Essa configuração geralmente resulta em melhor qualidade de imagem, especialmente para imagens sintéticas com muitas bordas e contraste nítidos.

Como prática recomendada para a compactação JPG, use `&qlt=85,0`.

## Práticas recomendadas para o dimensionamento do JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

O parâmetro `jpegSize` é útil se você quiser garantir que uma imagem não exceda um determinado tamanho para entrega em dispositivos que tenham memória limitada.

* Este parâmetro está definido em quilobytes (`jpegSize=&lt;size_in_kilobytes&gt;`). Ele define o tamanho máximo permitido para a entrega de imagens.
* `&jpegSize=` interage com o parâmetro de compactação JPG `&qlt=`. Se a resposta do JPG com o parâmetro de compactação JPG especificado (`&qlt=`) não exceder o valor ejpegSize, a imagem será retornada com `&qlt=` conforme definido. Caso contrário, `&qlt=` é diminuído gradualmente até que a imagem se ajuste ao tamanho máximo permitido. Ou até que o sistema determine que não é possível ajustá-lo e retorne um erro.

Como prática recomendada, defina `&jpegSize=` e adicione o parâmetro `&qlt=` se estiver entregando imagens do JPG a dispositivos com memória limitada.

## Resumo de práticas recomendadas {#best-practices-summary}

Como prática recomendada, para atingir uma alta qualidade de imagem e um tamanho de arquivo pequeno, comece com a seguinte combinação de parâmetros:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Essa combinação de configurações produz excelentes resultados na maioria das circunstâncias.

Se a imagem exigir mais otimização, ajuste gradualmente os parâmetros de nitidez (mascaramento sem nitidez), começando com um raio definido como 0,2 ou 0,3. Em seguida, aumente gradualmente o valor de 1,75 para no máximo 4 (equivalente a 400% no Photoshop). Verifique se o resultado desejado foi atingido.

Se os resultados da nitidez ainda não forem satisfatórios, aumente o raio em incrementos decimais. Para cada incremento decimal, reinicie o valor em 1,75 e aumente gradualmente para 4. Repita esse processo até atingir o resultado desejado. Embora os valores acima sejam uma abordagem validada pelos estúdios de criação, lembre-se de que você pode começar com outros valores e seguir outras estratégias. Se os resultados são satisfatórios para você ou não é uma questão subjetiva, portanto, a experimentação estruturada é fundamental.

À medida que você experimenta, as seguintes sugestões gerais são úteis para otimizar seu fluxo de trabalho:

* Experimente e teste diferentes parâmetros em tempo real, diretamente em um URL.
* Como prática recomendada, lembre-se de agrupar comandos do Servidor de imagens do Dynamic Media em uma predefinição de imagem. Uma predefinição de imagem é basicamente uma macro de comando de URL com nomes predefinidos personalizados como `$thumb_low$` e `&product_high$`. O nome da predefinição personalizada em um caminho de URL chama essas predefinições. Essa funcionalidade ajuda a gerenciar comandos e configurações de qualidade para diferentes padrões de uso de imagens no site e reduz o comprimento geral dos URLs.
* O Experience Manager também oferece maneiras mais avançadas de ajustar a qualidade da imagem, como aplicar nitidez às imagens na assimilação. Para ajustar e otimizar os resultados de renderização, os [serviços de consultoria da Adobe](https://business.adobe.com/br/customers/consulting-services/main.html) podem ajudá-lo com insights e práticas recomendadas personalizadas.
