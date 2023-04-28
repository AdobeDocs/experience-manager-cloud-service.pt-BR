---
title: Configurar restrições de upload de ativos
description: Configure os ativos Adobe Experience Manager para restringir o tipo de ativos que os usuários podem fazer upload com base no tipo MIME. Ajuda a evitar uploads acidentais de formato indesejado e arquivos mal-intencionados.
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 9%

---

# Configurar restrições de upload de ativos {#configure-asset-upload-restrictions}

Você pode configurar os ativos Adobe Experience Manager para restringir o tipo de ativos que os usuários podem fazer upload com base no tipo MIME.

>[!IMPORTANT]
>
>Por padrão, o Experience Manager Assets permite que os usuários façam upload de ativos de todos os tipos MIME. No entanto, você pode definir as configurações para restringir os usuários a carregarem arquivos de tipos MIME específicos apenas.

## Pré-requisitos {#prerequisites-asset-upload-restrictions}

Você deve ter privilégios de administrador para configurar restrições de upload de ativos.

## Aplicar restrições para uploads de ativos {#apply-restrictions-asset-uploadsssssss}

Para configurar [!DNL Experience Manager] para restringir usuários a fazer upload de arquivos de tipos MIME específicos:

1. Navegar para **[!UICONTROL Ferramentas > Ativos > Configurações de ativos]**.

1. Clique em **[!UICONTROL Restrições de upload]**.

1. Clique em **[!UICONTROL Adicionar]** para definir os tipos MIME permitidos.

1. Especifique o tipo MIME na caixa de texto. Você pode clicar em **[!UICONTROL Adicionar]** novamente para especificar tipos MIME mais permitidos. Você também pode clicar em ![ícone excluir](assets/delete-icon.svg) para excluir qualquer tipo MIME da lista.

1. Clique em **[!UICONTROL Salvar]**.

**Exemplo 1: Permitir o upload de todas as imagens e arquivos PDF para o Experience Manager Assets**

Para permitir o upload de imagens em todos os formatos e arquivos PDF para o Experience Manager Assets, faça o seguinte:

![Restrições de upload de ativos](assets/asset-upload-restrictions.png)

`image/*` já que o tipo MIME permite o upload de imagens em todos os formatos. `application/pdf` já que o tipo MIME permite o upload de arquivos PDF para o Experience Manager Assets.

Se você tentar fazer upload de um arquivo que não esteja incluído na lista de tipos MIME permitidos, o Experience Manager Assets exibirá a seguinte mensagem de erro:

![Arquivos restritos](assets/asset-upload-restricted-files.png)

`Screen Recording 2022-08-31 at 3.36.09 PM.mov` refere-se a um nome de arquivo que não está incluído nos tipos MIME permitidos.

**Exemplo 2: Permitir o upload de formatos de imagem específicos para o Experience Manager Assets**

Para adicionar formatos de imagem específicos aos tipos MIME permitidos e restringir o upload de todos os outros formatos de ativo, faça o seguinte:

![Restrições de ativos](assets/asset-restrictions.png)

Com base nas configurações mostradas na imagem, é possível fazer upload de imagens nos formatos .JPG, .PNG e .GIF para o Experience Manager Assets.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
