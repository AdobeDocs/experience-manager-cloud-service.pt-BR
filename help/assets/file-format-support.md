---
title: Formatos de arquivo suportados e tipos MIME
description: Formatos de arquivo e tipos MIME suportados por [!DNL Experience Manager Assets] como [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 10%

---

# [!DNL Assets] formatos de arquivo compatíveis {#supported-file-formats}

[!DNL Adobe Experience Manager] como [!DNL Cloud Service] O suporta recursos básicos de gerenciamento de conteúdo — armazenamento, gerenciamento de metadados online, controle de versão, upload e download etc. — para qualquer arquivo binário, independente de seu formato. [!DNL Adobe Experience Manager Assets] O suporta uma grande variedade de formatos de arquivo e cada recurso de produto tem suporte variado para diferentes formatos.

Além disso, [!DNL Experience Manager Assets] O oferece suporte estendido para gerar visualizações e representações e extrair metadados e texto para indexação de texto completo. Este suporte estendido é fornecido usando [microsserviços de ativos](asset-microservices-configure-and-use.md).

Os destaques da conversão de ativos usando microsserviços de ativos incluem:

* Chave [Formatos de arquivo Adobe](#adobe-formats) produzidos por aplicações e serviços de Adobe, incluindo [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension]e [!DNL Adobe Acrobat] ou PDF.
* Chave [formatos de arquivo de imagem](#image-formats).
* [Formatos de arquivo Camera Raw](#camera-raw-formats) para uma grande variedade de câmeras, incluindo Canon, Nikon, FujiFilm, Olympus e outros fabricantes (viabilizada pela Adobe Camera Raw).
* Frequentes [formatos de documento](#document-formats), incluindo o Microsoft Office e formatos Open Document.
* Grande variedade de formatos de [vídeo](#video-formats) e [áudio.](#audio-formats)

A legenda a seguir descreve o nível de suporte para cada formato.

| Nível de suporte | Descrição |
| ------------- | --------------------------- |
| ✓ | Compatível |
| * | Ver observações abaixo do quadro |
| - | Não aplicável |

## Formatos Adobe {#adobe-formats}

| Formato de arquivo | Geração de miniaturas | Extração de texto completo | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLAGEM | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| IDEIAS | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* Para [!DNL Adobe InDesign] arquivos (INDD), o tamanho da representação é determinado pela visualização incorporada no arquivo INDD. Configure as preferências em [!DNL InDesign] (**[!UICONTROL Preferências > Manuseio de arquivo > Sempre salvar imagens de visualização com documentos, Tamanho da visualização]**) para incorporar uma representação maior.

## Formatos de imagem {#image-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura | Cortar |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | ✓ | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |
| WebP | ✓ | ✓ | ✓ | ✓ |

## Formatos 3D {#support-3d-formats}

Os seguintes formatos 3D são compatíveis.

Consulte também [Trabalhar com ativos 3D no Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

| Formato | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Visualização de miniatura | Visualização 3D | Delivery Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## [!DNL Camera RAW] formatos {#camera-raw-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ |
| ARMA | ✓ | ✓ | ✓ |
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
| PEF | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ |
| BRUTO | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## Formatos de documento {#document-formats}

Os formatos de documento compatíveis com os recursos de gerenciamento de ativos são os seguintes.

| Formato de arquivo | Geração de miniaturas | Extração de texto completo | Largura/altura | Gerenciamento de metadados | [Connected Assets](use-assets-across-connected-assets-instances.md) | Visualização completa do documento |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |--------|
| DOC | - | - | - | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| ePub | - | ✓ | - | - | - | - |
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

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ | - | ✓ |
| F4V | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ |
| M2T | ✓ | - | ✓ |
| M2TS | ✓ | - | ✓ |
| M2V | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ |
| MKV | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ |
| MTS | ✓ | - | ✓ |
| MXF | ✓ | - | ✓ |
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | - | ✓ | ✓ |
| SWF | ✓ | - | ✓ |
| WebM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## Formatos de áudio {#audio-formats}

[!DNL Assets] como [!DNL Cloud Service] fornece suporte XMP extração de metadados para formatos de áudio AIF, ASF, M4A, MP3, WAV e WMA.

## Formatos de entrada suportados para transcrição de áudio e vídeo {#audio-video-transcription-formats}

* FLV (com codecs H.264 e AAC) (.flv)
* MXF (.mxf)
* MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg)
* Windows Media Video (WMV)/ASF (.wmv, .asf)
* AVI (8 bits/10 bits descompactado) (.avi)
* MP4 (.mp4, .m4a, .m4v)
* Gravação de vídeo digital da Microsoft (DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## Dicas e limitações {#limitations-and-tips}

* Atualmente, o limite de tamanho do arquivo para extração de metadados é de aproximadamente 15 GB. Ao fazer upload de ativos muito grandes, às vezes a operação de extração de metadados falha.

## Dynamic Media - Formatos de vídeo de entrada compatíveis com transcodificação {#video-dynamic-media-transcoding}

| Extensão de arquivo de vídeo | Contêiner | Codecs de vídeo recomendados | Codecs de vídeo não suportados |
| --- | --- | --- | --- |
| AVI | Intercalação A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| FLV, F4V | Flash Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (arquivos de animação vetorial) |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediário, Animação do Apple |
| MP4 | MPEG-4 | H264/AVC (todos os perfis) | − |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | − |
| MXF ‡ | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | − |
| OGV, OGG | Ogg | Theora, VP3, Dirac | − |
| WebM | WebM | VP8 do Google | − |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Tela do Microsoft (MSS2), História de fotos do Microsoft (WVP2) |

‡ Este formato de vídeo ainda não é suportado para o uso com Vídeos interativos no Dynamic Media ou para o uso com Anotações no Experience Manager Assets.

## Dynamic Media - Formatos de documento compatíveis {#document-support-dynamic-media}

| Formato | Upload (Formato de entrada) | Criar predefinição de imagem (formato de saída) | Visualizar representação dinâmica | Fornecer representação dinâmica | Baixar representação dinâmica |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF (Consulte a observação abaixo) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>Para PDF seguros, somente Upload é suportado.

## Dynamic Media - Formatos de imagem rasterizada compatíveis {#image-support-dynamic-media}

| Formato | Upload (Formato de entrada) | Criar predefinição de imagem (formato de saída) | Visualizar representação dinâmica | Fornecer representação dinâmica | Baixar representação dinâmica | Definir tipos que suportam este formato |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- | ---------------------------------- |
| BMP | ✓ | - | - | - | - | [Imagem](/help/assets/dynamic-media/image-sets.md), [Mídia mista](/help/assets/dynamic-media/mixed-media-sets.md)e [Rotação](/help/assets/dynamic-media/spin-sets.md) |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/dynamic-media/image-sets.md), [Mídia mista](/help/assets/dynamic-media/mixed-media-sets.md)e [Rotação](/help/assets/dynamic-media/spin-sets.md) |
| PICT | ✓ | - | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/dynamic-media/image-sets.md), [Mídia mista](/help/assets/dynamic-media/mixed-media-sets.md)e [Rotação](/help/assets/dynamic-media/spin-sets.md) |
| PSD ‡ | ✓ | - | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/dynamic-media/image-sets.md), [Mídia mista](/help/assets/dynamic-media/mixed-media-sets.md)e [Rotação](/help/assets/dynamic-media/spin-sets.md) |

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada por [!DNL Adobe Photoshop] e está incluído no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

## Dynamic Media - Formatos de imagem rasterizada não aceitos {#unsupported-raster-image-formats-dm}

Os seguintes subtipos de formatos de arquivo de imagem rasterizada que são *not* com suporte em [!DNL Dynamic Media]:

* Arquivos PNG com um tamanho de bloco IDAT superior a 100 MB.
* Arquivos PSB.
* Arquivos PSD com um espaço de cores diferente de CMYK, RGB, Escala de cinza ou Bitmap não são compatíveis. Não há suporte para espaços de cores DuoTone, Lab e Indexado.
* Arquivos PSD com profundidade de bits superior a 16.
* Arquivos TIFF com dados de ponto flutuante.
* Arquivos TIFF com espaço de cores Lab.

## Dynamic Media - Formatos de arquivo 3D compatíveis {#support-3d-formats-dynamic-media}

Consulte também [Formatos 3D compatíveis](/help/assets/file-format-support.md#support-3d-formats)

| extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão binária GL | modelo/gltf-binário | Inclui os materiais e as texturas como um único ativo. |
| OBJ | Arquivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Arquivo Zip de descrição da cena universal | model/vnd.usdz+zip | *Suporte apenas para ingestão; nenhuma visualização ou interação está disponível.* USDZ é um formato 3D proprietário que pode ser visualizado originalmente pelo Safari ou pelo iOS. |

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

>[!MORELIKETHIS]
>
>* [Processamento de ativos usando microsserviços de ativos](asset-microservices-overview.md)
>* [Formatos de arquivo compatíveis para a marcação inteligente de ativos baseados em texto](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

