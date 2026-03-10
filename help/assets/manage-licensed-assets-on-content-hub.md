---
title: Gerenciar o Assets licenciado no Content Hub
description: Saiba mais sobre como adicionar um campo de licença ao formulário de metadados de ativos, aplicar a propriedade de metadados de licença às pastas de ativos e aprovar ativos com licenças para uso.
badgeSaas: label="AEM Assets" type="Positive" tooltip="Aplicável ao AEM Assets)."
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 59f97fc6ded4274c27400f56b50b4a3329cc471a
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# Gerenciar o Assets licenciado no Content Hub {#manage-licensed-assets-on-content-hub}

Como administrador, edite o formulário de metadados para incluir o campo de licença de ativo para que ele seja exibido nas propriedades do ativo no ambiente de autor do AEM. Em seguida, você pode aprovar o ativo, bem como sua licença para torná-lo licenciado e disponível no Content Hub.

Execute as seguintes etapas:

1. Edite o formulário de metadados para incluir um novo campo de texto para incluir os detalhes da licença. Mapeie o campo de texto para a propriedade `dc:license`. Para obter mais informações sobre como adicionar campos a um formulário de metadados e definir propriedades, consulte [Configurar Forms de Metadados](/help/assets/metadata-assets-view.md#metadata-forms).
   ![extração do zip](/help/assets/assets/metadata-form-edit.png)
1. Aplique o formulário de metadados à pasta de ativos para aplicar as configurações incorporadas na etapa 1. Para obter informações sobre como atribuir um formulário de metadados à pasta de ativos, consulte [Atribuir formulário de metadados a uma pasta](/help/assets/metadata-assets-view.md#metadata-forms).
1. [Aprovar o PDF licenciado](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. Selecione o ativo e clique em **Detalhes** para exibir suas propriedades. No campo de licença adicionado na Etapa 1, defina o caminho absoluto para a licença do ativo que foi aprovada na Etapa 3 ou que já foi aprovada anteriormente. O caminho absoluto do Content Hub segue este padrão: `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`. Por exemplo, /content/dam/teamA/projects/documents/file1.pdf
   ![caminho absoluto](/help/assets/assets/absolute-path.png)
1. Aprove o ativo para disponibilizá-lo no Content Hub e clique em **Salvar**. Para obter informações sobre como aprovar um ativo, consulte [Definir status do ativo](/help/assets/manage-organize-assets-view.md#set-asset-status).

## Perguntas frequentes {#faqs-manage-licensed-assets-content-hub}

### Qual é a finalidade do gerenciamento de ativos licenciados no AEM Assets Content Hub?

O gerenciamento de ativos licenciados no AEM Assets Content Hub permite que os administradores garantam que somente ativos aprovados com licenças válidas estejam disponíveis para uso, mantendo a conformidade e o rastreamento de metadados adequado no ambiente de criação do AEM.

### Como posso adicionar um campo de licença às propriedades do ativo no Experience Manager as a Cloud Service?

No modo AEM Assets, é possível adicionar um campo de licença às propriedades do ativo editando o formulário de metadados para incluir um novo campo de texto mapeado para a propriedade `dc:license`. Esse campo aparece nas propriedades do ativo no ambiente de criação do AEM Assets.

### Como aplicar um formulário de metadados a uma pasta de ativos para incluir o campo de licença nas propriedades do ativo no AEM Assets?

Na exibição do AEM Assets, edite o formulário de metadados para incluir o campo de licença. Aplique esse formulário de metadados à pasta de ativos desejada para garantir que as novas configurações sejam incorporadas para todos os ativos nessa pasta.

### Como especificar os detalhes da licença de um ativo na exibição do AEM Assets?

Para especificar os detalhes da licença, selecione o ativo, clique em **Detalhes** para exibir suas propriedades e insira o caminho absoluto da licença de ativo aprovada no campo de licença adicionado ao formulário de metadados.

### Qual é o formato necessário para o caminho absoluto do AEM Assets Content Hub para uma licença de ativo?

O caminho absoluto do Content Hub deve seguir o padrão: /content/dam/(A hierarquia de pastas do ativo no repositório DAM)/(asset_name).(extensão_de_arquivo). Por exemplo, `/content/dam/teamA/projects/documents/file1.pdf`.

### Por que é importante aprovar o ativo e sua licença para disponibilizá-los no AEM Assets Content Hub?

A aprovação do ativo e de sua licença garante que somente os ativos devidamente licenciados e autorizados sejam disponibilizados no AEM Assets Content Hub, ajudando a manter a conformidade e os direitos de uso adequados.

### Como disponibilizo um ativo no AEM Assets Content Hub depois de aprovar sua licença?

Depois de definir o caminho de licença nas propriedades do ativo, aprove o ativo e clique em Salvar. Essa ação disponibiliza o ativo licenciado no AEM Assets Content Hub.

### Quem é responsável pelo gerenciamento de ativos licenciados no AEM Assets Content Hub?

Os administradores são responsáveis por editar formulários de metadados, atribuí-los a pastas de ativos e aprovar ativos e suas licenças no AEM Assets Content Hub.
