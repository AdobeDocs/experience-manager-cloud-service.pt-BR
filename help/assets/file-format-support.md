---
title: Formatos de arquivo e tipos MIME suportados pelos ativos Experience Manager como um serviço em nuvem
description: Formatos de arquivo e tipos MIME suportados pelos ativos Experience Manager como um serviço em nuvem.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2e73a9bba91f15702bdeb1d57e87b688360661bd

---


# Assets supported file formats {#supported-file-formats}

O Adobe Experience Manager como um serviço em nuvem oferece suporte aos recursos básicos de gestão de conteúdo — armazenamento, gerenciamento de metadados online, controle de versão, upload e download e assim por diante — para qualquer arquivo binário, independentemente de seu formato. Os ativos Adobe Experience Manager oferecem suporte a uma grande variedade de formatos de arquivo e cada recurso de produto tem suporte variado para formatos diferentes.

Além disso, os ativos Experience Manager fornecem suporte estendido para gerar pré-visualizações e execuções e extrair metadados e texto para indexação de texto completo. Esse suporte estendido é fornecido usando microserviços [de](asset-microservices-configure-and-use.md)ativos.

A legenda a seguir descreve o nível de suporte.

| Nível de suporte | Descrição |
| ------------- | --------------------------- |
| ✓ | Compatível |
| * | Ver observações abaixo do quadro |
| - | Não aplicável |

## Conversão de ativos usando microserviços de ativos {#asset-microservices-supported-formats}

Os destaques incluem:

* Formatos [de arquivo principais da](#adobe-formats) Adobe produzidos por aplicativos e serviços da Adobe, incluindo Adobe Photoshop, Adobe InDesign, Adobe Illustrator, Adobe XD, Adobe Dimension e Adobe Acrobat ou PDF.
* Formatos [de arquivo de](#image-formats)imagem principais.
* [Formatos](#camera-raw-formats) de arquivo Camera Raw para uma grande variedade de câmeras, incluindo Canon, Nikon, Fujifilm, Olympus e outros fabricantes (capacitados pelo Adobe Camera Raw).
* Formatos [comuns de](#document-formats)documento, incluindo os formatos Microsoft Office e Open Documento.
* Grande variedade de formatos de [vídeo](#video-formats) e [áudio.](#audio-formats)

### Formatos da Adobe {#adobe-formats}

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

\* Para INDD (arquivos do InDesign), o tamanho da execução é determinado pela pré-visualização incorporada ao arquivo INDD. Configure as preferências no InDesign (**[!UICONTROL Preferências > Manuseio de arquivo > Sempre salvar imagens de Pré-visualização com Documentos, tamanho]** de Pré-visualização) para incorporar renderização maior.

### Formatos de imagem {#image-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura | Cortar |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| SVG | - | ✓ | - | - |
| TIFF | ✓ | ✓ | ✓ | - |

### Formatos Camera RAW {#camera-raw-formats}

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

### formatos de Documento {#document-formats}

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

### Formatos de vídeo {#video-formats}

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

### Formatos de áudio {#audio-formats}

Os ativos como um serviço em nuvem fornecem suporte à extração de metadados XMP para os formatos de áudio AIF, ASF, M4A, MP3, WAV e WMA.

>[!MORELIKETHIS]
>
>* [Processamento de ativos usando microserviços de ativos](asset-microservices-overview.md)

