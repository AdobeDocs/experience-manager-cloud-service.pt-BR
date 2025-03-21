---
title: Gerenciar o Assets licenciado no Content Hub
description: Saiba mais sobre como adicionar um campo de licença ao formulário de metadados de ativos, aplicar a propriedade de metadados de licença às pastas de ativos e aprovar ativos com licenças para uso.
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---

# Gerenciar o Assets licenciado no Content Hub {#manage-licensed-assets-on-content-hub}

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

>[!AVAILABILITY]
>
>O guia do Content Hub agora está disponível no formato PDF. Baixe o guia inteiro e use o Assistente de IA da Adobe Acrobat para responder às suas consultas.
>
>[!BADGE PDF do Guia do Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Como administrador, edite o formulário de metadados para incluir o campo de licença de ativo para que ele seja exibido nas propriedades do ativo no ambiente de autor do AEM. Em seguida, você pode aprovar o ativo, bem como sua licença para torná-lo licenciado e disponível no Content Hub.

Execute as seguintes etapas:

1. Edite o formulário de metadados para incluir um novo campo de texto para incluir os detalhes da licença. Mapeie o campo de texto para a propriedade `dc:license`. Para obter mais informações sobre como adicionar campos a um formulário de metadados e definir propriedades, consulte [Configurar Forms de Metadados](/help/assets/metadata-assets-view.md#metadata-forms).
   ![extração do zip](/help/assets/assets/metadata-form-edit.png)
1. Aplique o formulário de metadados à pasta de ativos para aplicar as configurações incorporadas na etapa 1. Para obter informações sobre como atribuir um formulário de metadados à pasta de ativos, consulte [Atribuir formulário de metadados a uma pasta](/help/assets/metadata-assets-view.md#metadata-forms).
1. [Aprovar o PDF licenciado](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. Selecione o ativo e clique em **Detalhes** para exibir suas propriedades. No campo de licença adicionado na Etapa 1, defina o caminho absoluto para a licença do ativo que foi aprovada na Etapa 3 ou que já foi aprovada anteriormente. O caminho absoluto do Content Hub segue este padrão: `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`. Por exemplo, /content/dam/teamA/projects/documents/file1.pdf
   ![caminho absoluto](/help/assets/assets/absolute-path.png)
1. Aprove o ativo para disponibilizá-lo no Content Hub e clique em **Salvar**. Para obter informações sobre como aprovar um ativo, consulte [Definir status do ativo](/help/assets/manage-organize-assets-view.md#set-asset-status).
