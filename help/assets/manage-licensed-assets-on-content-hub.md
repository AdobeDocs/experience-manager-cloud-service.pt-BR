---
title: Gerenciar o Assets licenciado no Content Hub
description: Saiba mais sobre como adicionar um campo de licença ao formulário de metadados de ativos, aplicar a propriedade de metadados de licença às pastas de ativos e aprovar ativos com licenças para uso.
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---

# Gerenciar o Assets licenciado no Content Hub {#manage-licensed-assets-on-content-hub}

>[!AVAILABILITY]
>
>O guia do Content Hub agora está disponível no formato PDF. Baixe o guia inteiro e use o Assistente de IA da Adobe Acrobat para responder às suas consultas.
>
>[!BADGE PDF do Guia do Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Como administrador, edite o formulário de metadados para incluir o campo de licença de ativo para que ele seja exibido nas Propriedades do ativo no ambiente de autor do AEM. Em seguida, você pode aprovar o ativo, bem como sua licença para torná-lo licenciado e disponível no Content Hub.

Execute as seguintes etapas:

1. Edite o formulário de metadados para incluir um novo campo de texto para incluir os detalhes da licença. Mapeie o campo de texto para a propriedade `dc:license`. Para obter mais informações sobre como adicionar campos a um formulário de metadados e definir propriedades, consulte [Configurar Forms de Metadados](/help/assets/metadata-assets-view.md#metadata-forms).
   ![extração do zip](/help/assets/assets/metadata-form-edit.png)
1. Aplique o formulário de metadados à pasta de ativos para aplicar as configurações incorporadas na etapa 1. Para obter informações sobre como atribuir um formulário de metadados à pasta de ativos, consulte [Atribuir formulário de metadados a uma pasta](/help/assets/metadata-assets-view.md#metadata-forms).
1. [Aprovar o PDF licenciado](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. Selecione o ativo e clique em **Detalhes** para exibir suas propriedades. No campo de licença adicionado na Etapa 1, defina o caminho absoluto para a licença do ativo que foi aprovada na Etapa 3 ou que já foi aprovada anteriormente. O caminho absoluto do Content Hub segue este padrão: `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`. Por exemplo, /content/dam/teamA/projects/documents/file1.pdf
   ![caminho absoluto](/help/assets/assets/absolute-path.png)
1. Aprove o ativo para disponibilizá-lo no Content Hub e clique em **Salvar**. Para obter informações sobre como aprovar um ativo, consulte [Definir status do ativo](/help/assets/manage-organize-assets-view.md#set-asset-status).
