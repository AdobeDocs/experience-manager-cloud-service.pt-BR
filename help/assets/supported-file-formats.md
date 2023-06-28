---
title: Formatos de arquivo não compatíveis
description: Formatos de arquivo compatíveis com os vários casos de uso do  [!DNL Assets View]
role: User,Leader,Admin,Architect,Developer
contentOwner: AG
exl-id: bc44e98d-446e-41ff-b5b4-9dc324834630
source-git-commit: b4b397a09960f507df1daa0cf6f5dc49d6b286c6
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 96%

---

# Suporte para formatos de arquivos no [!DNL Assets View] {#file-format-support}

O [!DNL Assets View] é compatível com uma grande variedade de formatos de arquivo e cada funcionalidade oferece suporte para diferentes tipos de arquivo.

* ![ícone de tipo de arquivo de imagem](assets/image-icon.svg) Imagens: JPG, PNG, GIF, TIFF e outros
* ![ícone do tipo da creative cloud](assets/creative-cloud-files.svg) Arquivos da Creative Cloud: PSD, AI e INDD
* ![ícone de tipo de câmera](assets/camera-icon.svg) Arquivos de câmera RAW: CR2/CR3, NEF, SRW/SRF e outros
* ![ícone de tipo de arquivo do documento](assets/document-icon.svg) Documentos: DOCX, PDF, PPTX e XLSX
* ![ícone de tipo de arquivo de vídeo](assets/video-icon.svg) Vídeos: MP4

O [!DNL Assets View] é compatível com qualquer formato de arquivo binário com serviços básicos, como armazenamento, upload, cópia, movimentação, exclusão e adição de metadados.

O [!DNL Assets View] também é compatível com arquivos de câmera RAW de variados formatos relacionados às principais fabricantes de câmeras, incluindo Canon (CR2/CR3), Nikon (NEF), Sony (SRW/SRF), Fujifilm (RAF), Olympus (ORF), entre outros, graças à tecnologia do Adobe Camera Raw.

Esses vários tipos de arquivos têm diferentes graus de compatibilidade com os casos de uso e recursos, conforme descrito abaixo. Use a legenda para entender o nível de compatibilidade.

| Nível de compatibilidade | Descrição |
|-------------------|-------------------------|
| ✓ | Compatível |
| ✓ ‡ | Condicionalmente compatível |
| − | Não aplicável |

## Adicionar, carregar e visualizar ativos {#support-to-upload-view}

<!-- TBD: For AEM, AI files require the PDF option to be selected when saving the AI file.
-->

| Tipo de ativo | [Navegar](/help/assets/navigate-view.md) | Copiar | [Upload](/help/assets/add-delete.md) | Criar | [Excluir](/help/assets/add-delete.md#delete-assets) | Detalhes | Zoom da imagem | [Visualizado recentemente](/help/assets/navigate-view.md) |
|-------------------|----------|----------|----------|----------|----------|-------------------|------------|-----------------|
| Imagens raster | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| Arquivos RAW | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| Pastas | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | − |
| Vídeos MP4 | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| PDF | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |
| PSD, AI e INDD | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| Outros arquivos binários | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |

<!-- Hiding CC Libraries (considered beta) as per PM feedback.
| CC Libraries  | &#10003; | &minus;  | &#10003; | &#10003; | &#10003; | &#10003; | &minus;    | &minus;         |
-->

## Pesquisar, usar e editar ativos {#support-to-search-use-edit}

| Tipo de ativo | [Download](/help/assets/manage-organize.md#download) | Arrastar e soltar | [Editor de imagem](/help/assets/edit-images.md) | [Pesquisar](/help/assets/search.md) | [Tags inteligentes](/help/assets/metadata.md#tags) | [Renomear](/help/assets/manage-organize.md) | [Versões](/help/assets/manage-organize.md#versions-of-assets) |
|---------------|----------|---------------|--------------|----------|------------|----------|----------|
| Imagens raster | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Arquivos RAW | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | ✓ |
| Pastas | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| Vídeos | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| Bibliotecas da CC | − | − | − | − | − | ✓ | ✓ |
| PDF | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| PSD | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
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
| PSD, AI e INDD | − | ✓ | ✓ |
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

| Tipo de ativo | [Metadados](/help/assets/metadata.md) | [Representações](/help/assets/add-delete.md#renditions) | [Lixeira](/help/assets/add-delete.md#delete-assets) | Copiar | Mover |
|---------------|-------------------|------------|----------|----------|----------|
| Imagens raster | ✓ | ✓ | ✓ | ✓ | ✓ |
| Arquivos RAW | ✓ | ✓ | ✓ | ✓ | ✓ |
| Pastas | ✓ | − | ✓ | ✓ | ✓ |
| Vídeos | ✓ | − | ✓ | ✓ | ✓ |
| Bibliotecas da CC | ✓ | − | − | − | − |
| PDF | ✓ | − | ✓ | ✓ | ✓ |
| PSD, AI e INDD | ✓ | − | ✓ | ✓ | ✓ |
| Outros arquivos binários | ✓ | − | ✓ | ✓ | ✓ |

Usuários do [!DNL Adobe Asset Link] podem fazer upload e check-in (fazer upload de uma nova versão) de arquivos para o repositório do [!DNL Assets View] em aplicativos de desktop compatíveis da [!DNL Adobe Creative Cloud].

<!-- TBD: Saving the template table separately for later use.
| Asset type    | Features |
|---------------|----------|
| Raster images |          |
| Folders       |          |
| Videos        |          |
| CC Libraries  |          |
| PDF files     |          |
| PSD           |          |
| AI            |          |
| INDD          |          |

>[!MORELIKETHIS]
>
>* []()
-->

## Próximas etapas {#next-steps}

* Forneça feedback sobre o produto usando o [!UICONTROL Feedback] opção disponível na interface da Exibição do Assets

* Forneça feedback sobre a documentação usando as opções [!UICONTROL Editar esta página] ![editar a página](assets/do-not-localize/edit-page.png) ou [!UICONTROL Registrar um problema] ![criar um problema do GitHub](assets/do-not-localize/github-issue.png) disponíveis na barra lateral direita

* Entre em contato com o [Atendimento ao cliente](https://experienceleague.adobe.com/?support-solution=General&amp;lang=pt-BR#support)
