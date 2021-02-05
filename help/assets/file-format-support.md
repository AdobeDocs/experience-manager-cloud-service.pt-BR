---
title: Formatos de arquivo suportados e tipos MIME
description: Formatos de arquivo e tipos MIME suportados por [!DNL Experience Manager Assets] como a [!DNL Cloud Service].
contentOwner: AG
translation-type: tm+mt
source-git-commit: ceaa9546be160e01b124154cc827e6b967388476
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 10%

---


# [!DNL Assets] formatos de arquivo suportados  {#supported-file-formats}

[!DNL Adobe Experience Manager] como  [!DNL Cloud Service] suporte a recursos básicos de gestão de conteúdo — armazenamento, gerenciamento de metadados online, controle de versão, upload e download e assim por diante — para qualquer arquivo binário, independentemente de seu formato. [!DNL Adobe Experience Manager Assets] oferece suporte para uma grande variedade de formatos de arquivos e cada recurso de produto tem suporte variado para formatos diferentes.

Além disso, [!DNL Experience Manager Assets] oferece suporte estendido para gerar pré-visualizações e execuções e extrair metadados e texto para indexação de texto completo. Este suporte estendido é fornecido usando [ativos microservices](asset-microservices-configure-and-use.md).

Os destaques para conversão de ativos usando microserviços de ativos incluem:

* As teclas [formatos de arquivo Adobe](#adobe-formats) produzidas por aplicativos e serviços Adobe, incluindo [!DNL Adobe Photoshop], [!DNL Adobe InDesign], [!DNL Adobe Illustrator], [!DNL Adobe XD], [!DNL Adobe Dimension] e [!DNL Adobe Acrobat] ou PDF.
* Tecla [formatos de arquivo de imagem](#image-formats).
* [Camera Raw ](#camera-raw-formats) formatos de arquivos para uma grande variedade de câmeras, incluindo Canon, Nikon, Fujifilm, Olympus e outros fabricantes (alimentados pela Adobe Camera Raw).
* Formatos comuns de [documento](#document-formats), incluindo os formatos Microsoft Office e Open Documento.
* Grande variedade de formatos de [vídeo](#video-formats) e [áudio.](#audio-formats)

A legenda a seguir descreve o nível de suporte para cada formato.

| Nível de suporte | Descrição |
| ------------- | --------------------------- |
| Satélite | Compatível |
| * | Ver observações abaixo do quadro |
| - | Não aplicável |

## formatos Adobe {#adobe-formats}

| Formato de arquivo | Geração de miniaturas | Extração de texto completo | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | Satélite | - | Satélite | Satélite |
| COLAGEM | - | - | Satélite | - |
| DN | Satélite | - | Satélite | Satélite |
| IDEIAS | - | - | Satélite | - |
| INDD | Satélite | - | Satélite | * |
| INDT | - | - | Satélite | - |
| PDF | Satélite | Satélite | Satélite | Satélite |
| PROTO | - | - | Satélite | - |
| PSB | Satélite | - | Satélite | Satélite |
| PSD | Satélite | - | Satélite | Satélite |
| XD | Satélite | - | Satélite | Satélite |

\* Para arquivos [!DNL Adobe InDesign] (INDD), o tamanho da representação é determinado pela pré-visualização incorporada no arquivo INDD. Configure as preferências em [!DNL InDesign] (**[!UICONTROL Preferências > Manuseio de arquivos > Sempre salvar imagens de Pré-visualização com Documentos, Tamanho de Pré-visualização]**) para incorporar renderização maior.

## Formatos de imagem {#image-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura | Cortar |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | Satélite | - | Satélite | Satélite |
| EPS | - | Satélite | - | - |
| GIF | Satélite | Satélite | Satélite | Satélite |
| JPEG | Satélite | Satélite | Satélite | Satélite |
| PNG | Satélite | Satélite | Satélite | Satélite |
| RGB | Satélite | Satélite | Satélite | Satélite |
| RGBA | Satélite | Satélite | Satélite | Satélite |
| SGI | Satélite | Satélite | Satélite | Satélite |
| SVG | Satélite | - | Satélite | Satélite |
| TIFF | Satélite | Satélite | Satélite | - |

## Formatos de imagem em [!DNL Dynamic Media] {#image-support-dynamic-media}

| Formato | Carregar (formato de entrada) | Criar predefinição de imagem (formato de saída) | Execução dinâmica de pré-visualização | Fornecer representação dinâmica | Baixar representação dinâmica |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| BMP | Satélite | - | - | - | - |
| EPS | Satélite | Satélite | Satélite | Satélite | Satélite |
| GIF | Satélite | Satélite | Satélite | Satélite | Satélite |
| JPEG | Satélite | Satélite | Satélite | Satélite | Satélite |
| PICT | Satélite | - | - | - | - |
| PNG | Satélite | Satélite | Satélite | Satélite | Satélite |
| PSD   ‡ | Satélite | - | - | - | - |
| TIFF | Satélite | Satélite | Satélite | Satélite | Satélite |

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada por [!DNL Adobe Photoshop] e incluída no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

Os seguintes subtipos de formatos de arquivo de imagem rasterizada que não são suportados em [!DNL Dynamic Media]:

* Arquivos PNG com um tamanho de bloco IDAT maior que 100 MB.
* Arquivos PSB.
* Arquivos PSD com um espaço de cor diferente de CMYK, RGB, Escala de cinza ou Bitmap não são suportados. Espaços de cores Indexadas, Lab e DuoTone não são suportados.
* Arquivos PSD com uma profundidade de bits superior a 16.
* Arquivos TIFF com dados de ponto flutuante.
* Arquivos TIFF com espaço de cor Lab.

## Formatos 3D {#support-3d-formats}

Os seguintes formatos 3D são suportados.

Consulte também [Trabalhar com ativos 3D no Dynamic Media.](/help/assets/dynamic-media/assets-3d.md)

| Formato | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Pré-visualização em miniatura | pré-visualização 3D | delivery Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | Satélite | Satélite | Satélite | - | Satélite | Satélite | - | - |
| gLB | Satélite | Satélite | Satélite | Satélite | Satélite | - | Satélite | Satélite |
| gLTF | Satélite | Satélite | Satélite | - | Satélite | - | Satélite | - |
| OBJ | Satélite | Satélite | Satélite | Satélite | Satélite | - | Satélite | Satélite |
| STL | Satélite | Satélite | Satélite | Satélite | Satélite | - | Satélite | Satélite |
| USDz | Satélite | Satélite | Satélite | Satélite | Satélite | - | - | Satélite |

## [!DNL Camera RAW] formatos  {#camera-raw-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | Satélite | Satélite | Satélite |
| ARW | Satélite | Satélite | Satélite |
| CR2 | Satélite | Satélite | Satélite |
| CR3 | Satélite | Satélite | Satélite |
| CRW | Satélite | Satélite | Satélite |
| DCR | Satélite | Satélite | Satélite |
| DNG | Satélite | Satélite | Satélite |
| ERF | Satélite | Satélite | Satélite |
| FFF | Satélite | Satélite | Satélite |
| GPR | Satélite | Satélite | Satélite |
| IIQ | Satélite | Satélite | Satélite |
| KDC | Satélite | Satélite | Satélite |
| MEF | Satélite | Satélite | Satélite |
| MFW | Satélite | Satélite | Satélite |
| MOS | Satélite | Satélite | Satélite |
| MRW | Satélite | Satélite | Satélite |
| NEF | Satélite | Satélite | Satélite |
| NRW | Satélite | Satélite | Satélite |
| ORF | Satélite | Satélite | Satélite |
| PEF | Satélite | Satélite | Satélite |
| RAF | Satélite | Satélite | Satélite |
| RAW | Satélite | Satélite | Satélite |
| RW2 | Satélite | Satélite | Satélite |
| RWL | Satélite | Satélite | Satélite |
| SRF | Satélite | Satélite | Satélite |
| SRW | Satélite | Satélite | Satélite |
| X3F | Satélite | Satélite | Satélite |

## Formatos de documento {#document-formats}

Os formatos de documento compatíveis com os recursos de gerenciamento de ativos são os seguintes:

| Formato de arquivo | Geração de miniaturas | Extração de texto completo | Largura/altura | Gerenciamento de metadados | [Connected Assets](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| DOC | - | - | - | Satélite | Satélite |
| DOCX | Satélite | Satélite | Satélite | Satélite | Satélite |
| EPUB | - | Satélite | - | - | - |
| HTML | - | Satélite | - | Satélite | Satélite |
| ODF | Satélite | Satélite | Satélite | - | - |
| ODM | Satélite | Satélite | Satélite | - | - |
| ODP | Satélite | Satélite | Satélite | - | - |
| ODS | Satélite | Satélite | Satélite | - | - |
| ODT | Satélite | Satélite | Satélite | Satélite | Satélite |
| OFF | Satélite | Satélite | Satélite | - | - |
| PDF | Satélite | Satélite | Satélite | Satélite | Satélite |
| PPT | - | - | - | Satélite | Satélite |
| PPTX | Satélite | Satélite | Satélite | Satélite | Satélite |
| PS | - | - | Satélite | - | - |
| RTF | - | Satélite | - | Satélite | Satélite |
| TXT | - | Satélite | - | Satélite | Satélite |
| XLS | - | - | - | Satélite | Satélite |
| XLSX | Satélite | Satélite | Satélite | Satélite | Satélite |
| XML | - | Satélite | - | - | - |

## formatos de documento em [!DNL Dynamic Media] {#document-support-dynamic-media}

| Formato | Carregar (formato de entrada) | Criar predefinição de imagem (formato de saída) | Execução dinâmica de pré-visualização | Fornecer representação dinâmica | Baixar representação dinâmica |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | Satélite | - | - | - | - |
| INDD | Satélite | - | - | - | - |
| PDF | Satélite | Satélite | Satélite | Satélite | Satélite |

## Formatos de vídeo {#video-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | Satélite | - |
| 3GP | - | Satélite | - |
| AVI | Satélite | Satélite | Satélite |
| DIVX | Satélite | - | Satélite |
| F4V | Satélite | Satélite | Satélite |
| FLV | Satélite | Satélite | Satélite |
| M2T | Satélite | - | Satélite |
| M2TS | Satélite | - | Satélite |
| M2V | Satélite | - | Satélite |
| M4V | Satélite | Satélite | Satélite |
| MKV | Satélite | - | Satélite |
| MOV | Satélite | Satélite | Satélite |
| MP4 | Satélite | Satélite | Satélite |
| MPEG | Satélite | Satélite | Satélite |
| MPG | Satélite | Satélite | Satélite |
| MTS | Satélite | - | Satélite |
| MXF | Satélite | - | Satélite |
| OGV | Satélite | - | Satélite |
| QT | Satélite | - | Satélite |
| R3D | - | Satélite | Satélite |
| SWF | Satélite | - | Satélite |
| WebM | Satélite | - | Satélite |
| WMV | Satélite | Satélite | Satélite |

## Formatos de vídeo em [!DNL Dynamic Media] para transcodificação {#video-dynamic-media-transcoding}

| Extensão do arquivo de vídeo | Container | Codecs de vídeo recomendados | Codecs de vídeo não suportados |
|------------------------|--------------------|--------|-------|
| MP4 | MPEG-4 | H264/AVC (todos os perfis) | - |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Animação da Apple |
| FLV, F4V | Flash Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (arquivos de animação vetorial) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | Intercalação A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | VP8 do Google | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| R3D, RM | Vídeo vermelho bruto | MJPEG 2000 | - |
| RAM, RM | RealVideo | Não suportado | Real G2 (RV20), Real 8 (RV30), Real 10 (RV40) |
| FLAC | Flash nativo | Codec de áudio sem perda gratuito | - |
| MJ2 | Motion JPEG 2000 | Codec Motion JPEG 2000 | - |

## Formatos de áudio {#audio-formats}

[!DNL Assets] como um  [!DNL Cloud Service] fornece suporte XMP extração de metadados para os formatos de áudio AIF, ASF, M4A, MP3, WAV e WMA.

## Dicas e limitações {#limitations-and-tips}

* Atualmente, o limite de tamanho de arquivo para a extração de metadados é de aproximadamente 10 GB. Ao fazer upload de ativos muito grandes, às vezes a operação de extração de metadados falha.

>[!MORELIKETHIS]
>
>* [Processamento de ativos usando microserviços de ativos](asset-microservices-overview.md)
>* [Formatos de arquivo suportados para a marcação inteligente de ativos baseados em texto](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

