---
title: Como editar ou adicionar metadados
description: Saiba mais sobre os metadados de ativos no [!DNL Experience Manager Assets]  e conheça as várias maneiras pelas quais você pode editar os metadados de ativos.
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 7%

---

# Como editar ou adicionar metadados {#how-to-edit-or-add-metadata}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas de metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>documentação para desenvolvedores do AEM Assets</b></a>
        </td>
    </tr>
</table>

Os metadados são informações adicionais sobre o ativo que pode ser pesquisado. Ela é extraída automaticamente quando você faz upload de uma imagem. É possível editar os metadados existentes ou adicionar novas propriedades de metadados a campos existentes (por exemplo, quando um campo de metadados está em branco).

Como as empresas precisam de vocabulários de metadados controlados e confiáveis, o [!DNL Experience Manager Assets] não permite a adição sob demanda de novas propriedades de metadados. Embora os autores não possam adicionar novos campos de metadados para ativos, os desenvolvedores podem. Consulte [Criando uma Nova Propriedade de Metadados para o Assets](meta-edit.md#editing-metadata-schema).

## Edição de metadados de um ativo {#editing-metadata-for-an-asset}

Para editar metadados:

1. Siga uma das seguintes opções:

   * Na interface do usuário do Assets, selecione o ativo e selecione o ícone **[!UICONTROL Exibir propriedades]** na barra de ferramentas.
   * Na miniatura do ativo, selecione a ação rápida **[!UICONTROL Exibir propriedades]**.
   * Na página do ativo, selecione **[!UICONTROL Exibir propriedades]** na barra de ferramentas.

   A página do ativo exibe os metadados do ativo. Esses metadados eram extraídos automaticamente quando eram carregados (assimilados) no Experience Manager Assets.

1. Faça edições nos metadados em várias guias, conforme necessário, e quando concluído, selecione **[!UICONTROL Salvar]** na barra de ferramentas para salvar as alterações. Selecione **[!UICONTROL Fechar]** para retornar à interface da Web do Assets.

   >[!NOTE]
   >
   >Se um campo de texto estiver vazio, não há conjunto de metadados existente. Você pode inserir um valor no campo e salvá-lo para adicionar essa propriedade de metadados.

Quaisquer alterações nos metadados de um ativo são gravadas no binário original como parte de seus dados do XMP. Isso é feito por meio do fluxo de trabalho de gravação de metadados do Experience Manager. As alterações feitas nas propriedades existentes (como `dc:title`) são substituídas e as propriedades criadas (incluindo propriedades personalizadas como `cq:tags`) são adicionadas ao esquema.

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Editar esquema de metadados {#editing-metadata-schema}

Para obter detalhes sobre como editar o esquema de metadados, consulte [Editar formulários de esquema de metadados](metadata-schemas.md#edit-metadata-schema-forms).

## Registro de um namespace personalizado no Experience Manager {#registering-a-custom-namespace-within-aem}

Você pode adicionar seus próprios namespaces no Experience Manager. Da mesma forma que há namespaces predefinidos como cq, jcr e sling, você pode ter um namespace para os metadados do repositório e o processamento xml.

1. Vá para a página de administração do tipo de nó *https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*.
1. Selecione **[!UICONTROL Namespaces]** na parte superior da página. A página de administração do namespace é exibida em uma janela.

1. Para adicionar um namespace, selecione **[!UICONTROL Novo]** na parte inferior.
1. Especifique um namespace personalizado na convenção de namespace XML (especifique a identificação no formato de um URI e um prefixo associado para a identificação) e selecione **[!UICONTROL Salvar]**.

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
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
