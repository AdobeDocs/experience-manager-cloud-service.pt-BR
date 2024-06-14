---
title: Formatos de arquivo e tipos MIME compatíveis
description: Formatos de arquivo e tipos MIME aceitos pelo [!DNL Experience Manager Assets] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management, Renditions
role: User, Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 34%

---

# [!DNL Assets] formatos de arquivo compatíveis {#supported-file-formats}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] O oferece suporte a recursos básicos de gerenciamento de conteúdo — armazenamento, gerenciamento de metadados on-line, controle de versão, upload e download etc. — para qualquer arquivo binário, independentemente de seu formato. [!DNL Adobe Experience Manager Assets] O é compatível com uma grande variedade de formatos de arquivo e cada recurso do produto oferece suporte para diferentes formatos.

Além disso, [!DNL Experience Manager Assets] O oferece suporte estendido para gerar visualizações e representações e extrair metadados e texto para indexação de texto completo. Esse suporte estendido é fornecido usando [microsserviços de ativos](asset-microservices-configure-and-use.md).

Os destaques da conversão de ativos usando microsserviços de ativos incluem:

* Chave [formatos de arquivo Adobe](#adobe-formats) produzidos por aplicações e serviços Adobe, incluindo [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension], e [!DNL Adobe Acrobat] ou PDF.
* Chave [formatos de arquivo de imagem](#image-formats).
* [Formatos de arquivo Camera Raw](#camera-raw-formats) para uma ampla variedade de câmeras, incluindo Canon, Nikon, Fujifilm, Olympus e outros fabricantes (equipados pela Adobe Camera Raw).
* Comum [formatos de documento](#document-formats), incluindo os formatos Microsoft® Office e Open Document.
* Ampla variedade de [vídeo](#video-formats) e [áudio](#audio-formats) formatos.

A legenda a seguir descreve o nível de suporte para cada formato.

| Nível de suporte | Descrição |
| ------------- | --------------------------- |
| ✓ | Compatível |
| * | Consulte as observações abaixo da tabela |
| - | Não aplicável |

## formatos de Adobe {#adobe-formats}

| Formato do arquivo | Geração de miniaturas | Extração de texto completo | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| IA | ✓ | - | ✓ | ✓ |
| COLAGEM | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| SBSAR | ✓ | - | ✓ | ✓ |
| IDEIAS | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ µ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* Para [!DNL Adobe InDesign] (INDD), o tamanho das representações é determinado pela pré-visualização incorporada no arquivo INDD. Configure as preferências no [!DNL InDesign] (**[!UICONTROL Preferências > Manuseio de arquivo > Sempre salvar imagens de visualização com documentos, Tamanho da visualização]**) para que você possa incorporar representações maiores.

## Formatos de imagem {#image-formats}

| Formato do arquivo | Geração de miniaturas | Extração de metadados | Largura/altura | Cortar |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | ✓ | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI™ | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |
| WebP | ✓ | ✓ | ✓ | ✓ |

## Formatos 3D {#support-3d-formats}

Os formatos 3D a seguir são compatíveis.

Consulte também [Trabalhar com ativos 3D no Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

| Formato | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Visualização da miniatura | Visualização 3D | Entrega do Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| FBX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| 3DS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| SBSAR | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |

## [!DNL Camera Raw] formatos {#camera-raw-formats}

| Formato do arquivo | Geração de miniaturas | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ |
| PAP | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ |
| BRUTO | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## Formatos de documento {#document-formats}

Os formatos de documento compatíveis com os recursos de gerenciamento de ativos são os seguintes.

| Formato do arquivo | Geração de miniaturas | Extração de texto completo | Largura/altura | Gerenciamento de metadados | [Connected Assets](use-assets-across-connected-assets-instances.md) | Visualização completa do documento |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |--------|
| DOC | - | - | - | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ | - |
| ODF | ✓ | ✓ | ✓ | - | - | - |
| ODM | ✓ | ✓ | ✓ | - | - | - |
| ODP | ✓ | ✓ | ✓ | - | - | - |
| ODS | ✓ | ✓ | ✓ | - | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| OFG | ✓ | ✓ | ✓ | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PS | - | - | ✓ | - | - | - |
| RTF | - | ✓ | - | ✓ | ✓ | ✓ |
| TXT | ✓ | ✓ | - | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - | - |

## Formatos de vídeo {#video-formats}

| Formato do arquivo | Geração de miniaturas | Extração de metadados | Largura/altura | Visualização | Saída |
| ----------- | -------------------- | ------------------- | ------------ | ------- | ------- |
| 3G2 | - | ✓ | - | - | - |
| 3GP | - | ✓ | - | - | - |
| AVI | ✓ | ✓ | ✓ | ✓ | - |
| DIVX | ✓ | - | ✓ | ✓ | - |
| F4V | ✓ | ✓ | ✓ | ✓ | - |
| FLV | ✓ | ✓ | ✓ | ✓ | - |
| M2T | ✓ | - | ✓ | ✓ | - |
| M2TS | ✓ | - | ✓ | ✓ | - |
| M2V | ✓ | - | ✓ | ✓ | - |
| M4V | ✓ | ✓ | ✓ | ✓ | - |
| MKV | ✓ | - | ✓ | ✓ | - |
| MOV | ✓ | ✓ | ✓ | ✓ | - |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | - |
| MPG | ✓ | ✓ | ✓ | ✓ | - |
| MTS | ✓ | - | ✓ | ✓ | - |
| MXF | ✓ | - | ✓ | ✓ | - |
| OGV | ✓ | - | ✓ | ✓ | - |
| QT | ✓ | - | ✓ | ✓ | - |
| R3D | - | ✓ | ✓ | ✓ | - |
| SWF | ✓ | - | ✓ | ✓ | - |
| WebM | ✓ | - | ✓ | ✓ | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | - |

## Formatos de áudio {#audio-formats}

[!DNL Assets] as a [!DNL Cloud Service] O fornece suporte à extração de metadados de XMP para os formatos de áudio AIF, ASF, M4A, MP3, WAV e WMA.

## Formatos de entrada compatíveis com a transcrição de áudio e vídeo {#audio-video-transcription-formats}

* FLV (com codecs H.264 e AAC) (.flv)
* MXF (.mxf)
* MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg)
* Vídeo do Windows Media (WMV)/ASF (.wmv, .asf)
* AVI (8 bits/10 bits não compactado) (.avi)
* MP4 (.mp4, .m4a, .m4v)
* Gravação de vídeo digital Microsoft® (DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## Dicas e limitações {#limitations-and-tips}

* Atualmente, o limite de tamanho do arquivo para extração de metadados é de aproximadamente 15 GB. Ao fazer upload de ativos grandes, às vezes a operação de extração de metadados falha.

## Dynamic Media - Formatos de vídeo de entrada compatíveis com transcodificação {#video-dynamic-media-transcoding}

| Extensão do arquivo de vídeo | Contêiner | Codecs de vídeo recomendados | Codecs de vídeo não suportados |
| --- | --- | --- | --- |
| AVI | Intercalação A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft® Video 1 (MS-CRAM) |
| FLV, F4V | Flash Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (arquivos de animação de vetor) |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 e HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Animação do Apple |
| MP4 | MPEG-4 | H264/AVC (todos os perfis) | − |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | − |
| MXF ‡ | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | − |
| OGV, OGG | OGG | Theora, VP3, Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Tela Microsoft® (MSS2), História de foto Microsoft® (WVP2) |

‡ Este formato de vídeo ainda não é suportado para ser usado com Vídeos interativos no Dynamic Media ou para ser usado com Anotação no Experience Manager Assets.

## Dynamic Media - Formatos de documento compatíveis {#document-support-dynamic-media}

| Formato | Upload (formato de entrada) | Criar predefinição de imagem (Formato de saída) | Visualizar representação dinâmica | Entregar representação dinâmica | Baixar representação dinâmica |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| IA | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF (consulte a Nota abaixo) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>Para PDF seguros, somente o Upload é suportado.

## Dynamic Media - Formatos de imagem rasterizada compatíveis {#image-support-dynamic-media}

| Formato | Upload (formato de entrada) | Criar predefinição de imagem (Formato de saída) | Visualizar representação dinâmica | Entregar representação dinâmica | Baixar representação dinâmica | Definir tipos que oferecem suporte a este formato |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| AVIF | − | − | − | ✓ | − | − |
| BMP | ✓ | − | − | − | − | [Imagem](/help/assets/dynamic-media/image-sets.md), [Mix de mídia](/help/assets/dynamic-media/mixed-media-sets.md), e [Rotação](/help/assets/dynamic-media/spin-sets.md) |
| [EPS](/help/assets/dynamic-media/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| HEIC | − | − | − | ✓ | − | − |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/dynamic-media/image-sets.md), [Mix de mídia](/help/assets/dynamic-media/mixed-media-sets.md), e [Rotação](/help/assets/dynamic-media/spin-sets.md) |
| PICT | ✓ | − | − | − | − | − |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/dynamic-media/image-sets.md), [Mix de mídia](/help/assets/dynamic-media/mixed-media-sets.md), e [Rotação](/help/assets/dynamic-media/spin-sets.md) |
| PSD ‡ | ✓ | − | − | − | − | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/dynamic-media/image-sets.md), [Mix de mídia](/help/assets/dynamic-media/mixed-media-sets.md), e [Rotação](/help/assets/dynamic-media/spin-sets.md) |
| WEBP | − | − | − | ✓ | − | − |
<!-- AVIF, HEIC, and WebP added to table above on March 4, 2024 based on CQDOC-21294 -->

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada por [!DNL Adobe Photoshop] e está incluído no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

## Dynamic Media - Formatos de imagem rasterizada não aceitos {#unsupported-raster-image-formats-dm}

Os seguintes subtipos de formatos de arquivos de imagens de varredura *não* compatível com o [!DNL Dynamic Media]:

* Arquivos PNG com tamanho de bloco IDAT maior que 100 MB.
* Arquivos PSB.
* Arquivos PSD com um espaço de cor diferente de CMYK, RGB, Tons de cinza ou Bitmap não são suportados. Espaços de cores DuoTone, Lab e Indexado não são compatíveis.
* Arquivos PSD com profundidade de bits superior a 16.
* Arquivos TIFF que possuem dados de ponto flutuante.
* Arquivos TIFF com espaço de cores Lab.

## Dynamic Media - Formatos de arquivo 3D compatíveis {#support-3d-formats-dynamic-media}

Consulte também [Formatos 3D compatíveis](/help/assets/file-format-support.md#support-3d-formats)

| Extensão de arquivo 3D | Formato do arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão GL Binária | model/gltf-binary | Inclui os materiais e texturas como um único ativo. |
| OBJ | Arquivo de objeto 3D do WaveFront | application/x-tgif | |
| STL | Estereolitografia | application/vnd.ms-pki.stl | |
| USDZ | Arquivo Zip de Descrição de Cena Universal | model/vnd.usdz+zip | *Suporte para geração de assimilação e miniatura; visualizações 3D ainda não compatíveis.* USDZ é um formato 3D que pode ser visualizado nativamente pelo Safari ou iOS. |

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar ativos no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Processamento de ativos usando microsserviços de ativos](asset-microservices-overview.md).
>* [Formatos de arquivo compatíveis com a marcação inteligente de ativos baseados em texto](/help/assets/smart-tags.md#smart-tags-supported-file-formats)
