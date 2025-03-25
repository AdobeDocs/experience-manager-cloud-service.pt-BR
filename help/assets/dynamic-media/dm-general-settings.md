---
title: Definir configurações gerais do Dynamic Media
description: Saiba como gerenciar configurações gerais no Dynamic Media. Você pode configurar os nomes dos servidores de publicação e origem e definir as opções de substituição de imagem. Ajuste as configurações padrão de upload para obter mascaramento e processamento de arquivos sem nitidez para arquivos PostScript, Photoshop, PDF e Illustrator.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: a4d28786-cffa-42ab-98d3-90a15313e401
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 0%

---

# Definir configurações gerais do Dynamic Media

<!-- hide: yes
hidefromtoc: yes -->

{{work-with-dynamic-media}}

A definição de **[!UICONTROL Configurações Gerais do Dynamic Media]** só estará disponível se:

* Você tem uma *Configuração existente* do **[!UICONTROL Dynamic Media]** (no **[!UICONTROL Cloud Services]**) no Adobe Experience Manager as a Cloud Service. Consulte [Criar uma configuração de Dynamic Media no Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
* Você é um administrador de sistema da Experience Manager com privilégios de administrador.

Desenvolvedores e programadores de sites experientes são o público-alvo das Configurações gerais do Dynamic Media. O Adobe Dynamic Media recomenda que os usuários que alteram as configurações de publicação estejam familiarizados com o Dynamic Media no Adobe Experience Manager e com a tecnologia básica de geração de imagens.

Na criação da conta, o Adobe Dynamic Media fornece automaticamente os servidores atribuídos à sua empresa. Esses servidores são usados para criar cadeias de caracteres de URL para o site e os aplicativos. Essas chamadas de URL são específicas da sua conta.

A página Configuração de publicação do Dynamic Media estabelece configurações padrão que determinam como os ativos são entregues dos servidores do Adobe Dynamic Media para sites ou aplicativos. Se nenhuma configuração for especificada, o servidor do Adobe Dynamic Media fornecerá um ativo de acordo com uma configuração padrão definida na página Configuração de publicação do Dynamic Media.

Consulte também [Opcional - Configuração e definição das definições do Dynamic Media](/help/assets/dynamic-media/config-dm.md#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings) para obter mais tarefas de configuração opcionais.

>[!NOTE]
>
>Atualização do Dynamic Media Classic para o Dynamic Media no Adobe Experience Manager? As páginas Configurações gerais e [Configuração de publicação](/help/assets/dynamic-media/dm-publish-settings.md) do Dynamic Media são pré-preenchidas com os valores obtidos da sua conta do Dynamic Media Classic. As exceções são todos os valores listados na área **[!UICONTROL Opções de carregamento padrão]** da página Configurações Gerais. Esses valores já estão no Experience Manager. Dessa forma, todas as alterações feitas em **[!UICONTROL Opções de carregamento padrão]**, em qualquer uma das cinco guias, por meio da interface do usuário do Experience Manager, serão refletidas no Dynamic Media, não no Dynamic Media Classic. Todas as outras configurações e valores na página Configurações gerais e na página [Configuração de publicação](/help/assets/dynamic-media/dm-publish-settings.md) são mantidos entre o Dynamic Media Classic e o Dynamic Media no Experience Manager.

**Para definir as Configurações Gerais do Dynamic Media:**

1. No modo Autor do Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global.
1. No painel à esquerda, clique no ![ícone Ferramentas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) > **[!UICONTROL Assets]** > ![Edição de engrenagens](https://spectrum.adobe.com/static/icons/workflow_18/Smock_GearsEdit_18_N.svg) **[!UICONTROL Configurações gerais do Dynamic Media]**.
1. Na página Servidor, defina o **[!UICONTROL Nome do Servidor Publicado]** e o **[!UICONTROL Nome do Servidor de Origem]** e use as cinco guias para configurar as opções de carregamento padrão para a Edição de Imagens e para arquivos Postscript, Photoshop, PDF e Illustrator.

   * [Servidor](#server-general-setting)
   * [Carregar no aplicativo](#upload-to-application)
   * Guia [Edição de imagem](#image-editing-tab)
   * Guia [PostScript](#postscript-tab)
   * Guia [Photoshop](#photoshop-tab)
   * Guia [PDF](#pdf-tab)
   * Guia [Illustrator](#illustrator-tab)

   ![Página de configurações gerais do Dynamic Media](/help/assets/assets-dm/dm-general-settings.png)
   *Página Configurações Gerais do Dynamic Media, com a guia **[!UICONTROL Edição de Imagem]**selecionada.*<br><br>

1. Quando terminar, próximo ao canto superior direito da página, clique em **[!UICONTROL Salvar]**.

## Servidor {#server-general-setting}

Na criação da conta, o Adobe Dynamic Media fornece automaticamente os servidores atribuídos à sua empresa. Esses servidores são usados para criar cadeias de caracteres de URL para o site e os aplicativos. Essas chamadas de URL são específicas da sua conta.

| Opção | Descrição |
| --- | --- |
| **[!UICONTROL Nome do Servidor Publicado]** | Obrigatório.<br>O nome deve usar `https://` no caminho.<br>Este servidor é o servidor CDN (Content Deliver Network) ativo usado em todas as chamadas de URL geradas pelo sistema que são específicas para sua conta. Altere este nome de servidor somente quando for instruído a fazê-lo pelo Suporte técnico da Adobe. |
| **[!UICONTROL Nome do Servidor de Origem]** | Obrigatório.<br>Este servidor é usado apenas para testes de controle de qualidade. Altere este nome de servidor somente quando for instruído a fazê-lo pelo Suporte técnico da Adobe. |

## Carregar no aplicativo {#upload-to-application}

* **[!UICONTROL Substituir imagens]**

  O Adobe Dynamic Media não permite que dois arquivos tenham o mesmo nome. A ID do Adobe Dynamic Media de cada item (o nome da imagem menos a extensão do nome do arquivo) deve ser exclusiva. Devido a esta regra, **[!UICONTROL Carregar no Aplicativo]** tem uma substituição. O efeito exato dessa opção depende da opção &#39;Substituir imagens&#39; especificada que você escolheu. Essas opções especificam como as imagens de substituição são carregadas: se elas substituem as imagens originais ou se tornam imagens duplicadas. Imagens duplicadas são renomeadas com um `-1`. Por exemplo, `chair.tif` foi renomeado `chair-1.tif`. Essas opções afetam as imagens carregadas em uma pasta diferente da original ou as imagens com uma extensão de nome de arquivo diferente da original, como JPG, TIF ou PNG.

  >[!NOTE]
  >
  >Para manter a consistência com o Experience Manager, selecione a opção Substituir imagens **[!UICONTROL Substituir na pasta atual, mesmo nome base/extensão]**.

  | opção Substituir imagens | Descrição |
  | --- | --- |
  | **[!UICONTROL Substituir na pasta atual, mesmo nome base/extensão]** | *Padrão* somente para novas contas do Dynamic Media.<br>Esta opção é a regra mais rígida para substituição. Ela requer que você faça upload da imagem de substituição para a mesma pasta da original e que a imagem de substituição tenha a mesma extensão de nome de arquivo da original. Se esses requisitos não forem atendidos, uma duplicata será criada.<br>*Para manter a consistência com o Experience Manager, selecione esta opção*. |
  | **[!UICONTROL Substituir na pasta atual, mesmo nome base independentemente da extensão]** | Ele requer que você faça upload da imagem de substituição para a mesma pasta da original, no entanto, a extensão do nome do arquivo pode ser diferente da original. Por exemplo, chair.tif substitui chair.jpg. |
  | **[!UICONTROL Substituir em qualquer pasta, mesmo nome/extensão do ativo base]** | Ela requer que a imagem de substituição tenha a mesma extensão de nome de arquivo que a imagem original (por exemplo, chair.jpg deve substituir chair.jpg, não chair.tif). Entretanto, é possível fazer upload da imagem de substituição em uma pasta diferente da original. A imagem atualizada está na nova pasta; o arquivo não pode mais ser encontrado em seu local original. |
  | **[!UICONTROL Substituir em qualquer pasta, mesmo nome de ativo base independentemente da extensão]** | Essa opção é a regra de substituição mais inclusiva. É possível fazer upload de uma imagem de substituição para uma pasta diferente da original, fazer upload de um arquivo com uma extensão de nome de arquivo diferente e substituir o arquivo original. Se o arquivo original estiver em uma pasta diferente, a imagem de substituição ficará localizada na nova pasta para a qual foi carregada. |

* **[!UICONTROL Preservar corte]**

  Controla a preservação de qualquer definição de corte manual existente.

  Consulte também `preserveCrop` em [UploadPostJob](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job) e [ReprocessAssetsJob](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job), ambos no Guia de Referência de Visualizadores do Dynamic Media.

## Opções de upload padrão {#default-upload-options}

### Guia Edição de imagem {#image-editing-tab}

Esse filtro permite ajustar um efeito de filtro de nitidez na imagem final com resolução reduzida. Ela ajuda a controlar a intensidade do efeito, o raio do efeito (medido em pixels) e um limite de contraste ignorado.

O efeito Tirar nitidez da máscara usa as mesmas opções do filtro Tirar nitidez da máscara do Photoshop. Ao contrário do que o nome sugere, Unsharp Mask é um filtro de nitidez.

| Opções de Tirar nitidez da máscara | Descrição |
| --- | --- |
| **[!UICONTROL Valor]** | Obrigatório.<br>Ele controla a quantidade de contraste aplicada aos pixels de borda.<br>Pense nisso como a intensidade do efeito. Os valores de intensidade de Tirar nitidez da máscara diferem entre o Adobe Dynamic Media e o Adobe Photoshop. A Photoshop oferece um intervalo de valores de 1% a 500%. Já no Adobe Dynamic Media, o intervalo de valores é de `0.0` a `5.0`. Um valor de 5,0 no Adobe Dynamic Media é o equivalente aproximado de 500% no Photoshop; um valor de 0,9 é o equivalente de 90% e assim por diante. |
| **[!UICONTROL Raio]** | Obrigatório.<br>Controla o raio do efeito.<br>O intervalo de valores é de `0` a `250`. O efeito é executado em todos os pixels em uma imagem e irradia de todos os pixels em todas as direções. O raio é medido em pixels. Por exemplo, para obter um efeito de nitidez semelhante para uma imagem de 2000 x 2000 pixels e uma imagem de 500 x 500 pixels, você definiria um raio de dois pixels na imagem de 2000 x 2000 pixels. Em seguida, defina um valor de raio de um pixel na imagem de 500 x 500 pixels. Um valor maior é usado para uma imagem com mais pixels. |
| **[!UICONTROL Limite]** | Obrigatório.<br>O limite é um intervalo de contraste ignorado quando o filtro Tirar nitidez da máscara é aplicado. Esse efeito é importante para que nenhum &quot;ruído&quot; seja introduzido em uma imagem quando esse filtro for usado. O intervalo de valores é `0` - `255`, que é o número de etapas de brilho em uma imagem em tons de cinza. `0`=preto, `128`=50% cinza e `255`=branco.<br>Um valor limite de `12` ignora pequenas variações no brilho do tom da pele para evitar a adição de ruído, mas ainda adiciona o contraste da borda a áreas de contraste, como onde as pálpebras tocam a pele.<br>Se você tiver uma foto do rosto de alguém, a Máscara de Nitidez afetará as partes contrastadas da imagem. Por exemplo, onde pestanas e pele se encontram para criar uma área óbvia de contraste e a própria pele lisa. Mesmo a pele mais suave exibe alterações sutis nos valores de brilho. Se você não usar um valor de limite, o filtro acentua essas alterações sutis nos pixels de capa. Por sua vez, um efeito ruidoso e indesejável é criado enquanto o contraste das pálpebras é aumentado, aumentando a nitidez.<br>Para evitar esse problema, é introduzido um valor limite que informa ao filtro para ignorar os pixels que não alteram drasticamente o contraste, como a capa lisa.<br>No gráfico de zíper mostrado anteriormente, observe a textura ao lado dos zíperes. O ruído da imagem é exibido porque os valores de limite eram muito baixos para suprimir o ruído. |
| **[!UICONTROL Monocromático]** | Selecione para desfazer a nitidez da imagem de brilho (intensidade).<br>Desmarque para remover a nitidez de cada componente de cor separadamente. |

Consulte também [Nitidez de imagens no Adobe Dynamic Media e no Servidor de Imagens](https://experienceleague.adobe.com/docs/experience-manager-65/assets/sharpening_images.pdf?lang=en).

### Guia PostScript {#postscript-tab}

É possível rasterizar arquivos Adobe PostScript®, manter planos de fundo transparentes, escolher uma resolução e um espaço de cores.

Você pode usar arquivos Adobe PostScript® (EPS) no Adobe Dynamic Media. O Adobe Dynamic Media oferece comandos para configurar esses arquivos à medida que você os carrega.

Ao fazer upload de arquivos de imagem do PostScript (EPS), você pode formatá-los de várias maneiras. É possível rasterizar os arquivos, manter o plano de fundo transparente, escolher uma resolução e escolher um espaço de cores.

| opção PostScript | Descrição |
| --- | --- |
| **[!UICONTROL Processando]** | Escolha Rasterizar para converter os gráficos vetoriais no arquivo para o formato de bitmap. |
| **[!UICONTROL Manter um plano de fundo transparente em imagens renderizadas]** | Ele preserva a transparência de plano de fundo do arquivo. |
| **[!UICONTROL Resolução (pixel/polegada)]** | Determina a configuração de resolução. Essa configuração determina quantos pixels são exibidos por polegada no arquivo. |
| **[!UICONTROL Espaço de cor]** | · **[!UICONTROL Detectar automaticamente]** - Retém o espaço de cores do arquivo.<br>· **[!UICONTROL Forçar como RGB]** - Converte para o espaço de cores do RGB.<br>· **[!UICONTROL Forçar como CMYK]** - Converte para o espaço de cores CMYK.<br>· **[!UICONTROL Forçar como Tons de Cinza]** - Converte para o espaço de cores Tons de Cinza. |

### Guia Photoshop {#photoshop-tab}

É possível criar modelos a partir de arquivos Adobe® Photoshop®, manter camadas, especificar o nome das camadas, extrair texto e especificar como as imagens são ancoradas nos modelos.

| opção Photoshop | Descrição |
| --- | --- |
| **[!UICONTROL Manter camadas]** | Extrai as camadas na PSD, se houver, para ativos individuais. As camadas de ativos permanecem associadas à PSD. É possível visualizá-las abrindo o arquivo PSD na Exibição de detalhes e selecionando o painel de camada. Consulte Exibição e edição de camadas em um arquivo do PSD. |
| **[!UICONTROL Criar um modelo]** | Cria um modelo a partir das camadas no arquivo PSD. |
| **[!UICONTROL Extrair texto]** | Extrai o texto para que os usuários possam pesquisar texto em um Visualizador. |
| **[!UICONTROL Estender camadas para o tamanho do plano de fundo]** | Estende o tamanho das camadas de imagem extraídas para o tamanho da camada de plano de fundo. |
| **[!UICONTROL Nomeação da camada]** | Estende o tamanho das camadas de imagem extraídas para o tamanho da camada de plano de fundo.<br>· **[!UICONTROL Nome da camada]** - Nomeia as imagens de acordo com seus nomes de camadas no arquivo PSD. Por exemplo, uma camada chamada Etiqueta de preço no arquivo original do PSD se torna uma imagem chamada Etiqueta de preço. No entanto, se os nomes das camadas no arquivo do PSD forem nomes de camadas padrão do Photoshop (Plano de fundo, Camada 1, Camada 2 e assim por diante), as imagens serão nomeadas após seus números de camada no arquivo do PSD. <br>· **[!UICONTROL Photoshop e número da camada]** - Nomeia as imagens de acordo com seus números de camada no arquivo PSD, ignorando os nomes das camadas originais. As imagens são nomeadas com o nome de arquivo do Photoshop e um número de camada anexado. Por exemplo, a segunda camada de um arquivo chamado `Spring Ad.psd` é chamada `Spring Ad_2` mesmo se tiver um nome não padrão no Photoshop.<br>· **[!UICONTROL Photoshop e nome da camada]** - Nomeia as imagens após o arquivo PSD seguido pelo nome ou número da camada. O número da camada é usado se os nomes das camadas no arquivo do PSD forem nomes de camadas padrão do Photoshop. Por exemplo, uma camada chamada `Price Tag` em um arquivo PSD chamado `SpringAd` é chamada `Spring Ad_Price Tag`. Uma camada com o nome padrão Layer 2 é chamada `Spring Ad_2`. |
| **[!UICONTROL Âncora]** | Especifique como as imagens são ancoradas em modelos que são gerados a partir da composição em camadas produzida a partir do arquivo PSD. Por padrão, a âncora é o centro. Uma âncora central permite que imagens de substituição preencham melhor o mesmo espaço, independentemente da proporção da imagem de substituição. As imagens com um aspecto diferente que substituem essa imagem, ao referenciar o modelo e usar a substituição de parâmetro, ocupam efetivamente o mesmo espaço. Altere para uma configuração diferente se seu aplicativo exigir que as imagens de substituição preencham o espaço alocado no modelo. |

### Guia PDF {#pdf-tab}

O número máximo de páginas para uma PDF a ser considerado para extração é 5000 para novos uploads. Esse limite será alterado para 100 páginas (para todos os PDFs) em 31 de dezembro de 2022. Consulte também [limitações do Dynamic Media](/help/assets/dynamic-media/limitations.md).

É possível optar por rasterizar os arquivos, extrair palavras e links de pesquisa, definir a resolução e escolher um espaço de cores.

| opção PDF | Descrição |
| --- | --- |
| **[!UICONTROL Processando]** | · **[!UICONTROL Nenhum]** - Nenhum processamento do PDF foi concluído.<br>· **[!UICONTROL Miniatura]** - Extrai cada página do arquivo PDF e a converte em uma imagem de miniatura.<br> · **[!UICONTROL Rasterizar]** - Extrai as páginas no arquivo PDF e converte gráficos de vetor em imagens bitmap. Para criar um eCatalog, escolha essa opção. |
| **[!UICONTROL Extrair]** | · **[!UICONTROL Nenhum]** - Nenhuma palavra de pesquisa ou link extraído do PDF.<br>· **[!UICONTROL Palavras de pesquisa]** - O sistema extrai palavras de pesquisa do arquivo PDF, habilitando pesquisas por palavras-chave em um Visualizador de eCatalog.<br>· **[!UICONTROL Links]** - Extrai links dos arquivos PDF e os converte em Mapas de Imagens usados em um Visualizador de eCatalog.<br>· **[!UICONTROL Pesquisar palavras e links]** - Extrai palavras de pesquisa e links para uso em um visualizador de eCatalog. |
| **[!UICONTROL Resolução (pixel/polegada)]** | Determina a configuração de resolução. Essa configuração determina quantos pixels são exibidos por polegada no arquivo PDF. O padrão é 150. |
| **[!UICONTROL Espaço de cor]** | · **[!UICONTROL Detectar automaticamente]** - Mantém o espaço de cores do arquivo PDF.<br>· **[!UICONTROL Forçar como RGB]** - Converte para o espaço de cores do RGB.<br>· **[!UICONTROL Forçar como CMYK]** - Converte para o espaço de cores CMYK.<br>· **[!UICONTROL Forçar como Tons de Cinza]** - Converte para o espaço de cores Tons de Cinza. |

### Guia Illustrator {#illustrator-tab}

É possível rasterizar arquivos Adobe Illustrator®, manter planos de fundo transparentes, escolher uma resolução e um espaço de cores.

Você pode usar os arquivos do Adobe® Illustrator® (AI) no Adobe Dynamic Media. O Adobe Dynamic Media oferece comandos para configurar esses arquivos à medida que você os carrega.

Ao fazer upload de arquivos de imagem do Illustrator (AI), você pode formatá-los de várias maneiras. É possível rasterizar os arquivos, manter o plano de fundo transparente, escolher uma resolução e escolher um espaço de cores. As opções de formatação de arquivos PostScript e Illustrator estão disponíveis na tela Fazer upload, em Opções da PostScript e Opções do Illustrator na caixa Fazer upload das opções de trabalho.


| opção Illustrator | Descrição |
| --- | --- |
| **[!UICONTROL Processando]** | Escolha Rasterizar para converter os gráficos vetoriais no arquivo para o formato de bitmap. |
| **[!UICONTROL Manter um plano de fundo transparente em imagens renderizadas]** | Ele preserva a transparência de plano de fundo do arquivo. |
| **[!UICONTROL Resolução (pixel/polegada)]** | Determina a configuração de resolução. Essa configuração determina quantos pixels são exibidos por polegada no arquivo. |
| **[!UICONTROL Espaço de cor]** | · **[!UICONTROL Detectar automaticamente]** - Retém o espaço de cores do arquivo.<br>· **[!UICONTROL Forçar como RGB]** - Converte para o espaço de cores do RGB.<br>· **[!UICONTROL Forçar como CMYK]** - Converte para o espaço de cores CMYK.<br>· **[!UICONTROL Forçar como Tons de Cinza]** - Converte para o espaço de cores Tons de Cinza. |
