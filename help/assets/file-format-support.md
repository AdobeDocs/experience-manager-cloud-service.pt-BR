---
title: Formatos de arquivo suportados e tipos MIME
description: Formatos de arquivo e tipos MIME suportados por [!DNL Experience Manager Assets] como [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: 6c17b048631a7f61305ec4f0a4f84c4b0577aec0
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 9%

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
| Instantâneo | Compatível |
| * | Ver observações abaixo do quadro |
| - | Não aplicável |

## Formatos Adobe {#adobe-formats}

| Formato de arquivo | Geração de miniaturas | Extração de texto completo | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | Instantâneo | - | Instantâneo | Instantâneo |
| COLAGEM | - | - | Instantâneo | - |
| DN | Instantâneo | - | Instantâneo | Instantâneo |
| IDEIAS | - | - | Instantâneo | - |
| INDD | Instantâneo | - | Instantâneo | * |
| INDT | - | - | Instantâneo | - |
| PDF | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| PROTO | - | - | Instantâneo | - |
| PSB | Instantâneo | - | Instantâneo | Instantâneo |
| PSD | Instantâneo | - | Instantâneo | Instantâneo |
| XD | Instantâneo | - | Instantâneo | Instantâneo |

\* Para [!DNL Adobe InDesign] arquivos (INDD), o tamanho da representação é determinado pela visualização incorporada no arquivo INDD. Configure as preferências em [!DNL InDesign] (**[!UICONTROL Preferências > Manuseio de arquivo > Sempre salvar imagens de visualização com documentos, Tamanho da visualização]**) para incorporar uma representação maior.

## Formatos de imagem {#image-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura | Cortar |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | Instantâneo | - | Instantâneo | Instantâneo |
| EPS | - | Instantâneo | - | - |
| GIF | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| JPEG | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| PNG | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| RGB | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| RGBA | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| SGI | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| SVG | Instantâneo | - | Instantâneo | Instantâneo |
| TIFF | Instantâneo | Instantâneo | Instantâneo | - |

## Formatos de imagem em [!DNL Dynamic Media] {#image-support-dynamic-media}

| Formato | Upload (Formato de entrada) | Criar predefinição de imagem (formato de saída) | Visualizar representação dinâmica | Fornecer representação dinâmica | Baixar representação dinâmica |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| BMP | Instantâneo | - | - | - | - |
| EPS | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| GIF | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| JPEG | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| PICT | Instantâneo | - | - | - | - |
| PNG | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| PSD ‡ | Instantâneo | - | - | - | - |
| TIFF | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada por [!DNL Adobe Photoshop] e está incluído no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

Os seguintes subtipos de formatos de arquivo de imagem rasterizada que não são aceitos no [!DNL Dynamic Media]:

* Arquivos PNG com um tamanho de bloco IDAT superior a 100 MB.
* Arquivos PSB.
* Arquivos PSD com um espaço de cores diferente de CMYK, RGB, Escala de cinza ou Bitmap não são compatíveis. Não há suporte para espaços de cores DuoTone, Lab e Indexado.
* Arquivos PSD com profundidade de bits superior a 16.
* Arquivos TIFF com dados de ponto flutuante.
* Arquivos TIFF com espaço de cores Lab.

## Formatos 3D {#support-3d-formats}

Os seguintes formatos 3D são compatíveis.

Consulte também [Trabalhar com ativos 3D no Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

| Formato | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Visualização de miniatura | Visualização 3D | Delivery Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo | - | - |
| gLB | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo |
| gLTF | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo | - | Instantâneo | - |
| OBJ | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo |
| STL | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo |
| USDz | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | - | Instantâneo |

## [!DNL Camera RAW] formatos {#camera-raw-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | Instantâneo | Instantâneo | Instantâneo |
| ARMA | Instantâneo | Instantâneo | Instantâneo |
| CR2 | Instantâneo | Instantâneo | Instantâneo |
| CR3 | Instantâneo | Instantâneo | Instantâneo |
| CRW | Instantâneo | Instantâneo | Instantâneo |
| DCR | Instantâneo | Instantâneo | Instantâneo |
| DNG | Instantâneo | Instantâneo | Instantâneo |
| ERF | Instantâneo | Instantâneo | Instantâneo |
| FFF | Instantâneo | Instantâneo | Instantâneo |
| GPR | Instantâneo | Instantâneo | Instantâneo |
| IIQ | Instantâneo | Instantâneo | Instantâneo |
| KDC | Instantâneo | Instantâneo | Instantâneo |
| MEF | Instantâneo | Instantâneo | Instantâneo |
| MFW | Instantâneo | Instantâneo | Instantâneo |
| MOS | Instantâneo | Instantâneo | Instantâneo |
| MRW | Instantâneo | Instantâneo | Instantâneo |
| NEF | Instantâneo | Instantâneo | Instantâneo |
| NRW | Instantâneo | Instantâneo | Instantâneo |
| ORF | Instantâneo | Instantâneo | Instantâneo |
| PEF | Instantâneo | Instantâneo | Instantâneo |
| RAF | Instantâneo | Instantâneo | Instantâneo |
| BRUTO | Instantâneo | Instantâneo | Instantâneo |
| RW2 | Instantâneo | Instantâneo | Instantâneo |
| RWL | Instantâneo | Instantâneo | Instantâneo |
| SRF | Instantâneo | Instantâneo | Instantâneo |
| SRW | Instantâneo | Instantâneo | Instantâneo |
| X3F | Instantâneo | Instantâneo | Instantâneo |

## Formatos de documento {#document-formats}

Os formatos de documento compatíveis com os recursos de gerenciamento de ativos são os seguintes.

| Formato de arquivo | Geração de miniaturas | Extração de texto completo | Largura/altura | Gerenciamento de metadados | [Connected Assets](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| DOC | - | - | - | Instantâneo | Instantâneo |
| DOCX | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| ePub | - | Instantâneo | - | - | - |
| HTML | - | Instantâneo | - | Instantâneo | Instantâneo |
| ODF | Instantâneo | Instantâneo | Instantâneo | - | - |
| ODM | Instantâneo | Instantâneo | Instantâneo | - | - |
| ODP | Instantâneo | Instantâneo | Instantâneo | - | - |
| ODS | Instantâneo | Instantâneo | Instantâneo | - | - |
| ODT | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| OFG | Instantâneo | Instantâneo | Instantâneo | - | - |
| PDF | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| PPT | - | - | - | Instantâneo | Instantâneo |
| PPTX | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| PS | - | - | Instantâneo | - | - |
| RTF | - | Instantâneo | - | Instantâneo | Instantâneo |
| TXT | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo |
| XLS | - | - | - | Instantâneo | Instantâneo |
| XLSX | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| XML | - | Instantâneo | - | - | - |

## Formatos de documento em [!DNL Dynamic Media] {#document-support-dynamic-media}

| Formato | Upload (Formato de entrada) | Criar predefinição de imagem (formato de saída) | Visualizar representação dinâmica | Fornecer representação dinâmica | Baixar representação dinâmica |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | Instantâneo | - | - | - | - |
| INDD | Instantâneo | - | - | - | - |
| PDF | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |

## Formatos de vídeo {#video-formats}

| Formato de arquivo | Geração de miniaturas | Extração de metadados | Largura/altura |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | Instantâneo | - |
| 3GP | - | Instantâneo | - |
| AVI | Instantâneo | Instantâneo | Instantâneo |
| DIVX | Instantâneo | - | Instantâneo |
| F4V | Instantâneo | Instantâneo | Instantâneo |
| FLV | Instantâneo | Instantâneo | Instantâneo |
| M2T | Instantâneo | - | Instantâneo |
| M2TS | Instantâneo | - | Instantâneo |
| M2V | Instantâneo | - | Instantâneo |
| M4V | Instantâneo | Instantâneo | Instantâneo |
| MKV | Instantâneo | - | Instantâneo |
| MOV | Instantâneo | Instantâneo | Instantâneo |
| MP4 | Instantâneo | Instantâneo | Instantâneo |
| MPEG | Instantâneo | Instantâneo | Instantâneo |
| MPG | Instantâneo | Instantâneo | Instantâneo |
| MTS | Instantâneo | - | Instantâneo |
| MXF | Instantâneo | - | Instantâneo |
| OGV | Instantâneo | - | Instantâneo |
| QT | Instantâneo | - | Instantâneo |
| R3D | - | Instantâneo | Instantâneo |
| SWF | Instantâneo | - | Instantâneo |
| WebM | Instantâneo | - | Instantâneo |
| WMV | Instantâneo | Instantâneo | Instantâneo |

## Formatos de vídeo em [!DNL Dynamic Media] para transcodificação {#video-dynamic-media-transcoding}

| Extensão de arquivo de vídeo | Contêiner | Codecs de vídeo recomendados | Codecs de vídeo não suportados |
| --- | --- | --- | --- |
| AVI | Intercalação A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| FLV, F4V | Flash Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (arquivos de animação vetorial) |
| M4V | Apple iTunes | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes42 HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediário, Animação do Apple |
| MP4 | MPEG-4 | H264/AVC (todos os perfis) | - |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| MXF |  | Formato de intercâmbio de mídia.<br>Apple ProRes422 | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| WebM | WebM | VP8 do Google | - |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Tela do Microsoft (MSS2), História de fotos do Microsoft (WVP2) |

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

>[!MORELIKETHIS]
>
>* [Processamento de ativos usando microsserviços de ativos](asset-microservices-overview.md)
>* [Formatos de arquivo compatíveis para a marcação inteligente de ativos baseados em texto](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

