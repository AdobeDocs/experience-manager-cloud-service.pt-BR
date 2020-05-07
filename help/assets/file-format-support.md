---
title: Formatos de arquivo e tipos MIME suportados pelos ativos Experience Manager como um serviço em nuvem
description: Formatos de arquivo e tipos MIME suportados pelos ativos Experience Manager como um serviço em nuvem.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2830c1cb2a9a0c06e6f8a4a765420706f5ceb093
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 9%

---


# Assets supported file formats {#supported-file-formats}

O Adobe Experience Manager como um serviço em nuvem oferece suporte aos recursos básicos de gestão de conteúdo — armazenamento, gerenciamento de metadados online, controle de versão, upload e download e assim por diante — para qualquer arquivo binário, independentemente de seu formato. Os ativos Adobe Experience Manager oferecem suporte a uma grande variedade de formatos de arquivo e cada recurso de produto tem suporte variado para formatos diferentes.

Além disso, os ativos Experience Manager fornecem suporte estendido para gerar pré-visualizações e execuções e extrair metadados e texto para indexação de texto completo. Esse suporte estendido é fornecido usando microserviços [de](asset-microservices-configure-and-use.md)ativos.

Os destaques da conversão de ativos usando microserviços de ativos incluem:

* Formatos [de arquivo principais da](#adobe-formats) Adobe produzidos por aplicativos e serviços da Adobe, incluindo Adobe Photoshop, Adobe InDesign, Adobe Illustrator, Adobe XD, Adobe Dimension e Adobe Acrobat ou PDF.
* Formatos [de arquivo de](#image-formats)imagem principais.
* [Formatos](#camera-raw-formats) de arquivo Camera Raw para uma grande variedade de câmeras, incluindo Canon, Nikon, Fujifilm, Olympus e outros fabricantes (capacitados pelo Adobe Camera Raw).
* Formatos [comuns de](#document-formats)documento, incluindo os formatos Microsoft Office e Open Documento.
* Grande variedade de formatos de [vídeo](#video-formats) e [áudio.](#audio-formats)

A legenda a seguir descreve o nível de suporte.

| Nível de suporte | Descrição |
| ------------- | --------------------------- |
| ✓ | Compatível |
| * | Ver observações abaixo do quadro |
| - | Não aplicável |

## Formatos da Adobe {#adobe-formats}

| Formato de arquivo | Geração de miniaturas | extração de texto completo | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| COLAGEM | - | - | ✓ | - |
| DN | ✓ |  | ✓ | ✓ |
| IDEIAS | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* Para [!DNL Adobe InDesign] arquivos (INDD), o tamanho da representação é determinado pela pré-visualização incorporada ao arquivo INDD. Configure as preferências em [!DNL InDesign] (**[!UICONTROL Preferências > Manuseio de arquivo > Sempre salvar imagens de Pré-visualização com Documentos, tamanho]** de Pré-visualização) para incorporar renderizações maiores.

## Formatos de imagem {#image-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura | Cortar |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| SVG | - | ✓ | - | - |
| TIFF | ✓ | ✓ | ✓ | - |

## Formatos de imagem em [!DNL Dynamic Media] {#image-support-dynamic-media}

| Formato | Carregar (formato de entrada) | Criar predefinição de imagem (formato de saída) | Execução dinâmica de Pré-visualização | Fornecer representação dinâmica | Baixar representação dinâmica |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | - | - | - | - |
| PSD ‡ | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada por [!DNL Adobe Photoshop] e incluída no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

Os seguintes subtipos de formatos de arquivo de imagem rasterizada que não são suportados em [!DNL Dynamic Media]:

* Arquivos PNG com um tamanho de bloco IDAT maior que 100 MB.
* Arquivos PSB.
* Arquivos PSD com um espaço de cor diferente de CMYK, RGB, Escala de cinza ou Bitmap não são suportados. Espaços de cores Indexadas, Lab e DuoTone não são suportados.
* Arquivos PSD com uma profundidade de bits superior a 16.
* Arquivos TIFF com dados de ponto flutuante.
* Arquivos TIFF com espaço de cor Lab.

## [!DNL Camera RAW] formatos {#camera-raw-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura |
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
| PEF | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

## formatos de Documento {#document-formats}

Os formatos de documento compatíveis com os recursos de gerenciamento de ativos são os seguintes:

| Formato de arquivo | Geração de miniaturas | extração de texto completo | Largura/altura | Gerenciamento de metadados | [Connected Assets](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOC | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| OFF | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | - | ✓ | - | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

## formatos de Documento em [!DNL Dynamic Media] {#document-support-dynamic-media}

| Formato | Carregar (formato de entrada) | Criar predefinição de imagem (formato de saída) | Execução dinâmica de Pré-visualização | Fornecer representação dinâmica | Baixar representação dinâmica |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| INDD | ✓ | - | - | - | - |

## Formatos de vídeo {#video-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ |  | ✓ |
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
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | ✓ | - | ✓ |
| SWF | ✓ | - | ✓ |
| WEBM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## Formatos de vídeo em [!DNL Dynamic Media] para transcodificação {#video-dynamic-media-transcoding}

| Extensão do arquivo de vídeo | Container | Codecs de vídeo recomendados | Codecs de vídeo não suportados |
|------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| MP4 | MPEG-4 | H264/AVC (todos os perfis) |  |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Animação da Apple |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (arquivos de animação vetorial) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | Intercalação A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | VP8 do Google |  |
| OGV, OGG | Ogg | Theora, VP3, Dirac |  |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D, RM | Vídeo vermelho bruto | MJPEG 2000 |  |
| RAM, RM | RealVideo | Não suportado | Real G2 (RV20), Real 8 (RV30), Real 10 (RV40) |
| FLAC | Flash nativo | Codec de áudio sem perda gratuito |  |
| MJ2 | Motion JPEG 2000 | Codec Motion JPEG 2000 |  |

## Formatos de áudio {#audio-formats}

Os ativos como um serviço em nuvem fornecem suporte à extração de metadados XMP para os formatos de áudio AIF, ASF, M4A, MP3, WAV e WMA.

>[!MORELIKETHIS]
>
>* [Processamento de ativos usando microserviços de ativos](asset-microservices-overview.md)

