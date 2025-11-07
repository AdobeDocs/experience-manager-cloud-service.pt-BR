---
title: Formatos de arquivo não compatíveis
description: Formatos de arquivo compatíveis com os vários casos de uso do  [!DNL Assets view]
role: User, Leader, Admin, Developer
contentOwner: AG
exl-id: 5936ace2-318e-4888-9ad4-23e6f6bfb857
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 100%

---

# Suporte para formatos de arquivos no [!DNL Assets view] {#file-format-support}

O [!DNL Assets view] é compatível com uma grande variedade de formatos de arquivo e cada funcionalidade oferece suporte para diferentes tipos de arquivo.

* ![ícone de tipo de arquivo de imagem](assets/image-icon.svg) Imagens: JPG, PNG, GIF, TIFF e outros
* ![ícone de tipo da Creative Cloud](assets/creative-cloud-files.svg) Arquivos da Creative Cloud: PSD, PSB, AI e INDD
* ![ícone de tipo de câmera](assets/camera-icon.svg) Arquivos de câmera RAW: CR2/CR3, NEF, SRW/SRF e outros
* ![ícone de tipo de arquivo do documento](assets/document-icon.svg) Documentos: DOCX, PDF, PPTX e XLSX
* ![ícone de tipo de arquivo de vídeo](assets/video-icon.svg) Vídeos: MP4

O [!DNL Assets view] é compatível com qualquer formato de arquivo binário com serviços básicos, como armazenamento, upload, cópia, movimentação, exclusão e adição de metadados.

O [!DNL Assets view] também é compatível com arquivos de câmera RAW de variados formatos relacionados às principais fabricantes de câmeras, incluindo Canon (CR2/CR3), Nikon (NEF), Sony (SRW/SRF), Fujifilm (RAF), Olympus (ORF), entre outros, graças à tecnologia do Adobe Camera Raw.

Esses vários tipos de arquivos têm diferentes graus de compatibilidade com os casos de uso e recursos, conforme descrito abaixo. Use a legenda para entender o nível de compatibilidade.

| Nível de compatibilidade | Descrição |
|-------------------|-------------------------|
| ✓ | Compatível |
| ✓ ‡ | Condicionalmente compatível |
| − | Não aplicável |

## Adicionar, carregar e visualizar ativos {#support-to-upload-view}

<!-- TBD: For AEM, AI files require the PDF option to be selected when saving the AI file.
-->

| Tipo de ativo | [Navegar](/help/assets/navigate-assets-view.md) | Copiar | [Upload](/help/assets/add-delete-assets-view.md) | Criar | [Excluir](/help/assets/add-delete-assets-view.md#delete-assets) | Detalhes | Zoom da imagem | [Visualizado recentemente](/help/assets/navigate-assets-view.md) |
|-------------------|----------|----------|----------|----------|----------|-------------------|------------|-----------------|
| Imagens raster | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| Arquivos RAW | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| Pastas | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | − |
| Vídeos MP4 | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| PDF | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |
| PSD, PSB, AI e INDD | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| Outros arquivos binários | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |

<!-- Hiding CC Libraries (considered beta) as per PM feedback.
| CC Libraries  | &#10003; | &minus;  | &#10003; | &#10003; | &#10003; | &#10003; | &minus;    | &minus;         |
-->

## Pesquisar, usar e editar ativos {#support-to-search-use-edit}

<!--writer - please check RAW files row below. There was an extra column, so I deleted a duplicate section. I think I did it right. -->

| Tipo de ativo | [Download](/help/assets/manage-organize-assets-view.md#download) | Arrastar e soltar | [Editor de imagem](/help/assets/edit-images-assets-view.md) | [Pesquisar](/help/assets/search-assets-view.md) | [Tags inteligentes](/help/assets/metadata-assets-view.md#tags) | [Renomear](/help/assets/manage-organize-assets-view.md) | [Versões](/help/assets/manage-organize-assets-view.md#versions-of-assets) |
|---------------|----------|---------------|--------------|----------|------------|----------|----------|
| Imagens raster | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Arquivos RAW | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Pastas | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| Vídeos | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| Bibliotecas da CC | − | − | − | − | − | ✓ | ✓ |
| PDF | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| PSD e PSB | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| IA e INDD | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| Outros arquivos binários | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |


## Revisar ativos e colaborar {#support-to-review-collaborate}

| Tipo de ativo | Anotar | Comentar | Criar tarefas e revisar |
|---------------|----------|----------|-------------------------|
| Imagens raster | ✓ | ✓ | ✓ |
| Arquivos RAW | ✓ | ✓ | ✓ |
| Pastas | − | − | − |
| Vídeos | − | ✓ | ✓ |
| Bibliotecas da CC | − | − | − |
| PDF | − | ✓ | ✓ |
| PSD, PSB, AI e INDD | − | ✓ | ✓ |
| Outros arquivos binários | − | ✓ | ✓ |
| DOC | − | ✓ | ✓ |
| DOCX | − | ✓ | ✓ |
| PPT | − | ✓ | ✓ |
| PPTX | − | ✓ | ✓ |
| XLS | − | ✓ | ✓ |
| XLSX | − | ✓ | ✓ |
| TXT | − | ✓ | ✓ |
| RTF | − | ✓ | ✓ |

## Outras tarefas de gerenciamento de ativos {#support-to-manage-assets}

| Tipo de ativo | [Metadados](/help/assets/metadata-assets-view.md) | [Representações](/help/assets/add-delete-assets-view.md#renditions) | [Lixeira](/help/assets/add-delete-assets-view.md#delete-assets) | Copiar | Mover |
|---------------|-------------------|------------|----------|----------|----------|
| Imagens raster | ✓ | ✓ | ✓ | ✓ | ✓ |
| Arquivos RAW | ✓ | ✓ | ✓ | ✓ | ✓ |
| Pastas | ✓ | − | ✓ | ✓ | ✓ |
| Vídeos | ✓ | − | ✓ | ✓ | ✓ |
| Bibliotecas da CC | ✓ | − | − | − | − |
| PDF | ✓ | − | ✓ | ✓ | ✓ |
| IA e INDD | ✓ | − | ✓ | ✓ | ✓ |
| PSD e PSB | ✓ | ✓ | ✓ | ✓ | ✓ |
| Outros arquivos binários | ✓ | − | ✓ | ✓ | ✓ |

Usuários do [!DNL Adobe Asset Link] podem fazer upload e check-in (fazer upload de uma nova versão) de arquivos para o repositório do [!DNL Assets view] em aplicativos de desktop compatíveis da [!DNL Adobe Creative Cloud].

<!-- TBD: Saving the template table separately for later use.
| Asset type    | Features |
|---------------|----------|
| Raster images |          |
| Folders       |          |
| Videos        |          |
| CC Libraries  |          |
| PDF files     |          |
| PSD, PSB           |          |
| AI            |          |
| INDD          |          |

>[!MORELIKETHIS]
>
>* []()
-->

## Próximas etapas {#next-steps}

* Forneça feedback sobre o produto usando a opção [!UICONTROL Feedback] disponível na interface de visualização do Assets

* Forneça feedback sobre a documentação usando as opções [!UICONTROL Editar esta página] ![editar a página](assets/do-not-localize/edit-page.png) ou [!UICONTROL Registrar um problema] ![criar um problema do GitHub](assets/do-not-localize/github-issue.png) disponíveis na barra lateral direita

* Entre em contato com o [Atendimento ao cliente](https://experienceleague.adobe.com/pt-br?support-solution=General#support)
