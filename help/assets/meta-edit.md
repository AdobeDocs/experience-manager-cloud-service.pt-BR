---
title: Como editar ou adicionar metadados
description: Saiba mais sobre metadados de ativos no [!DNL Experience Manager Assets] Há várias maneiras de editar metadados de ativos.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 12%

---

# Como editar ou adicionar metadados {#how-to-edit-or-add-metadata}

Os metadados são informações adicionais sobre o ativo que pode ser pesquisado. Ela é extraída automaticamente quando você faz upload de uma imagem. É possível editar os metadados existentes ou adicionar novas propriedades de metadados a campos existentes (por exemplo, quando um campo de metadados está em branco).

Como as empresas precisam de vocabulários de metadados controlados e confiáveis, [!DNL Experience Manager Assets] não permite a adição ad hoc de novas propriedades de metadados. Embora os autores não possam adicionar novos campos de metadados para ativos, os desenvolvedores podem. Consulte [Criação de nova propriedade de metadados para ativos](meta-edit.md#editing-metadata-schema).

## Edição de metadados de um ativo {#editing-metadata-for-an-asset}

Para editar metadados:

1. Siga uma das seguintes opções:

   * Na interface do usuário do Assets, selecione o ativo e clique/toque na **[!UICONTROL Propriedades da exibição]** ícone na barra de ferramentas.
   * Na miniatura do ativo, selecione o **[!UICONTROL Propriedades da exibição]** ação rápida.
   * Na página do ativo, clique/toque em **[!UICONTROL Propriedades da exibição]** na barra de ferramentas.

   A página do ativo exibe todos os metadados do ativo. Esses metadados eram extraídos automaticamente quando eram carregados (assimilados) no Experience Manager Assets.

1. Faça edições nos metadados em várias guias, conforme necessário, e quando concluído, clique/toque em **[!UICONTROL Salvar]** na barra de ferramentas para salvar as alterações. Clique/toque em **[!UICONTROL Fechar]** para retornar à interface da Web do Assets.

   >[!NOTE]
   >
   >Se um campo de texto estiver vazio, não há conjunto de metadados existente. Você pode inserir um valor no campo e salvá-lo para adicionar essa propriedade de metadados.

Quaisquer alterações nos metadados de um ativo são gravadas no binário original como parte de seus dados de XMP. Isso é feito por meio do fluxo de trabalho de gravação de metadados de Experience Manager. Alterações feitas nas propriedades existentes (como `dc:title`) são substituídas e as propriedades recém-criadas (incluindo propriedades personalizadas, como `cq:tags`) são adicionados junto com o schema.

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Editar esquema de metadados {#editing-metadata-schema}

Para obter detalhes sobre como editar o esquema de metadados, consulte [Edição de formulários de esquema de metadados](metadata-schemas.md#edit-metadata-schema-forms).

## Registro de um namespace personalizado no Experience Manager {#registering-a-custom-namespace-within-aem}

Você pode adicionar seus próprios namespaces no Experience Manager. Da mesma forma que há namespaces predefinidos como cq, jcr e sling, você pode ter um namespace para os metadados do repositório e o processamento xml.

1. Vá para a página de administração do tipo de nó *https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*.
1. Clique ou toque **[!UICONTROL Namespaces]** na parte superior da página. A página de administração do namespace é exibida em uma janela.

1. Para adicionar um namespace, clique ou toque em **[!UICONTROL Novo]** na parte inferior.
1. Especifique um namespace personalizado na convenção de namespace XML (especifique a ID no formato de um URI e um prefixo associado para a ID) e clique ou toque **[!UICONTROL Salvar]**.

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
