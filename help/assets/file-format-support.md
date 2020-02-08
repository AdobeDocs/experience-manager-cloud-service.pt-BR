---
title: Formatos de arquivo e tipos MIME suportados pelos ativos Experience Manager como um serviço em nuvem
description: Formatos de arquivo e tipos MIME suportados pelos ativos Experience Manager como um serviço em nuvem.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 776b089a322cc4f86fdcb9ddf1c3cc207fc85d39

---


# Formatos de arquivo compatíveis com ativos {#supported-file-formats}

O Adobe Experience Manager como um serviço em nuvem oferece suporte aos recursos básicos de gerenciamento de conteúdo - armazenamento, gerenciamento de metadados on-line, controle de versão, upload e download e assim por diante - para qualquer arquivo binário, independentemente de seu formato. Além disso, para os formatos de arquivo comumente usados, como imagem, propriedade da Adobe, documento e vídeo, ele oferece suporte estendido para gerar visualizações e execuções e extrair metadados e texto para indexação de texto completo. Esse suporte estendido é fornecido usando microserviços [de](asset-microservices-configure-and-use.md)ativos.

Alguns destaques dos formatos de arquivo com suporte estendido incluem:

* Formatos [de arquivo principais da](#adobe-formats) Adobe produzidos por aplicativos e serviços da Adobe, incluindo Adobe Photoshop, InDesign, Illustrator, XD, Dimension e Acrobat / PDF.
* Formatos de arquivo de [imagem principais](#image-formats)
* [Formatos](#camera-raw-formats) de arquivo Camera Raw para uma grande variedade de câmeras, incluindo Canon, Nikon, Fujifilm, Olympus e outros fabricantes (capacitados pelo Adobe Camera Raw)
* Formatos [de](#document-formats)documento comuns, incluindo os formatos [Microsoft Office](#microsoft-office-formats) (Word, Excel, PowerPoint) e [Open Document](#opendocument-formats)
* Grande variedade de formatos de [vídeo](#video-formats) e [áudio](#audio-formats)

## Legenda para obter informações detalhadas de suporte {#legend-for-detailed-support-information}

A legenda a seguir descreve o nível de suporte para um recurso:

| Nível de suporte | Descrição |
| ------------------------------------------------------------ | --------------------------- |
| ✓ | Suportado |
| * | Ver observações abaixo do quadro |
| - | Não aplicável |

As colunas das tabelas de suporte fornecem as seguintes informações:

| Coluna | Descrição |
| ------------ | --------------------------------------------------------------- |
| Formato | Formato de arquivo (extensão de arquivo) do binário original do ativo |
| GIF | Formato GIF para geração de representação |
| JPEG | Formato JPEG para geração de representação |
| PNG | Formato PNG para geração de representação |
| XMP | Extração de metadados do binário original |
| TXT | Extração de texto do documento para indexação |
| Largura/altura | Suporte para definir a largura e a altura de uma representação (pixels) |

<!-- Adding this checkmark icon ✓ does not look good in table. The icon's shade and size has to be toned down for good readability and less clutter.
@gklebus: I suggest using a checkmark character, either U+2713 ✓ CHECK MARK or U+2714 ✔ HEAVY CHECK MARK
-->

## Formatos da Adobe {#adobe-formats}

| Formato de arquivo | GIF | JPEG | PNG | TXT | XMP | Largura/altura |
| ----------- | --- | ---- | --- | --- | --- | ------------ |
| AI | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| COLAGEM | - | - | - | - | ✓ | - |
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| IDEIAS | - | - | - | - | ✓ | - |
| INDD | ✓ | ✓ | ✓ | - | ✓ | ✓* |
| INDT | - | - | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | - | - | ✓ | - |
| PSB | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| PSD | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| XD | ✓ | ✓ | ✓ | - | ✓ | ✓ |

\* Para INDD (arquivos do InDesign), o tamanho da execução é determinado pela visualização incorporada ao arquivo INDD. Configure as preferências no InDesign (**[!UICONTROL Preferências > Manuseio de arquivo > Sempre salvar imagens de visualização com documentos, tamanho]** de visualização) para incorporar renderização maior.

## Formatos de imagem {#image-formats}

| Formato de arquivo | GIF | JPEG | PNG | XMP | Largura/altura |
| ----------- | --- | ---- | --- | --- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |


## Formatos Camera RAW {#camera-raw-formats}

| Formato de arquivo | GIF | JPEG | PNG | XMP | Largura/altura |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3FR | ✓ | ✓ | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formatos de documento {#document-formats}

| Formato de arquivo | TXT | XMP |
| ----------- | --- | --- |
| EPUB | ✓ | - |
| HTML | ✓ | - |
| PS | - | ✓ |
| RTF | ✓ | - |
| TEXTO | ✓ | - |
| XML | ✓ | - |

## Formatos do Microsoft Office {#microsoft-office-formats}

| Formato de arquivo | GIF | JPEG | PNG | TEXTO | Largura/altura |
| ----------- | --- | ---- | --- | ---- | ------------ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formatos OpenDocument {#opendocument-formats}

| Formato de arquivo | GIF | JPEG | PNG | TEXTO | Altura |
| ----------- | --- | ---- | --- | ---- | ------ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formatos de vídeo {#video-formats}

| Formato de arquivo | GIF | JPEG | PNG | XMP | Largura/altura |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3G2 | - | - | - | ✓ | - |
| 3GP | - | - | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ | ✓ | ✓ |
| DIVX | ✓ | ✓ | ✓ |  | ✓ |
| F4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ | ✓ | ✓ |
| M2T | ✓ | ✓ | ✓ | - | ✓ |
| M2TS | ✓ | ✓ | ✓ | - | ✓ |
| M2V | ✓ | ✓ | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| MKV | ✓ | ✓ | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MTS | ✓ | ✓ | ✓ | - | ✓ |
| OGV | ✓ | ✓ | ✓ | - | ✓ |
| QT | ✓ | ✓ | ✓ | - | ✓ |
| R3D | ✓ | ✓ | ✓ | - | ✓ |
| SWF | ✓ | ✓ | ✓ | - | ✓ |
| WEBM | ✓ | ✓ | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | ✓ |

## Formatos de áudio {#audio-formats}

Os ativos como um serviço em nuvem fornecem suporte a XMP para estes formatos de áudio: AIF, ASF, M4A, MP3, WAV e WMA.

<!-- TBD: Some items from https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedinputvideoformatsforDynamicMediatranscoding may be applicable.

Bring more parity with https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedMIMEtypes.
https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#Supportedmultimediaformats
-->

>[!MORELIKETHIS]
>
>* [Processamento de ativos usando microserviços de ativos](asset-microservices-overview.md)

