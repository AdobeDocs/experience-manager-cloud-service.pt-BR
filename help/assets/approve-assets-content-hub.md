---
title: Aprovar ativos para o Content Hub
description: Saiba como aprovar ativos no Assets as a Cloud Service para disponibilizá-los no Content Hub.
exl-id: fc849028-ab56-4388-b8d6-e36cac8f868f
source-git-commit: 189fc257fed1115f66559d0f9063885ae527a0fa
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 2%

---

# Aprovar ativos para o Content Hub {#approve-assets-content-hub}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Aprovar ativos para o Content Hub](assets/content-hub-approve-assets.png)

Os gerentes e comerciantes de marca mantêm controle rigoroso sobre os ativos da marca. Somente as versões aprovadas e mais recentes do ativo estão disponíveis para uso no Content Hub, garantindo a consistência da marca em todos os canais e aplicativos.

É possível aprovar ativos usando o AEM Assets as a Cloud Service para simplificar o gerenciamento de ativos, garantindo um processo controlado e eficiente para manuseio de ativos.

## Antes de começar {#pre-requisites}

Antes de começar, você deve ter:

* Acesso ao AEM Assets as a Cloud Service

* Permissões de gravação para editar metadados de ativos para poder editar o campo **[!UICONTROL Status]** disponível em [propriedades de ativos](/help/assets/manage-organize-assets-view.md##manage-asset-status) para um ativo.

## Aprovar ativos para o Content Hub{#approve-assets-for-content-hub}

Os ativos marcados como `approved` no Assets as a Cloud Service ficam disponíveis automaticamente no Content Hub.

>[!NOTE]
>
>O Assets as a Cloud Service e o Content Hub devem usar a mesma organização para que os ativos sejam exibidos no Content Hub.

Para definir o status do ativo como `approved` usando o modo de exibição Assets no AEM as a Cloud Service:

1. Selecione o ativo e clique em **[!UICONTROL Detalhes]** na barra de ferramentas.

1. Na guia **[!UICONTROL Básico]**, selecione o status do ativo como `approved` na lista suspensa **[!UICONTROL Status]**.
1. Clique em **[!UICONTROL Salvar]**.

   >[!VIDEO](https://video.tv.adobe.com/v/3433172)

Se precisar aprovar ativos usando o modo de exibição de Administrador, consulte [Aprovar ativos usando o modo de exibição de Administrador](/help/assets/approve-assets.md#approve-assets).

## Aprovar ativos em massa para o Content Hub usando a exibição do Assets {#bulk-approve-assets-content-hub}

Aprovar ativos em massa usando a exibição do Assets para AEM Assets as a Cloud Service. Todos os ativos, aprovados em massa, ficam disponíveis no Content Hub.

Para aprovar ativos em massa em uma pasta na exibição do Assets:

1. Selecione o(s) ativo(s) e clique em **[!UICONTROL Editar metadados em massa]**.

1. Selecione **[!UICONTROL Aprovado]** no campo **[!UICONTROL Status]**, disponível na seção [!UICONTROL Propriedades] do painel direito.

1. Clique em **[!UICONTROL Salvar]**.

## Automatizar aprovação de ativos recém-assimilados na exibição do administrador {#automate-approval-newly-ingested-assets}

Depois de alternar da exibição do Assets para a exibição do Administrador, é possível definir as configurações da pasta para que todos os novos ativos adicionados à pasta sejam aprovados automaticamente.

Você pode alternar entre as visualizações Admin e Assets das seguintes maneiras:
![Minha visão geral do Workspace](assets/assets-view.png)

Siga estas etapas para automatizar a aprovação de ativos recém-assimilados em [!DNL Experience Manager Admin view]:

1. Crie uma pasta no ambiente de criação (https://author-pXXX-eYYY.adobeaemcloud.com). Substitua _XXX_ pela ID do programa e _AAAA_ pela ID do ambiente do Experience Manager.
1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Metadados]**.
1. Clique em **[!UICONTROL Criar]** no lado superior direito da página.
1. Adicione um título de Perfil e clique em **[!UICONTROL Criar]**. O perfil de metadados foi criado com sucesso.
1. Selecione o perfil de metadados recém-criado e clique em **[!UICONTROL Editar _(e)_]**. <br>O formulário **[!UICONTROL Editar Perfil de Metadados]**é aberto com a guia **[!UICONTROL Básico]**realçada.
1. Arraste e solte um **[!UICONTROL Campo de Texto de Linha Única]** da seção **[!UICONTROL Criar Formulário]** no lado direito para a seção Metadados no formulário.
1. Clique no campo recém-adicionado e faça as seguintes atualizações no painel **[!UICONTROL Configurações]**:
   1. Altere o **[!UICONTROL Rótulo do campo]** para _Assets Aprovado_.
   1. Atualize o **[!UICONTROL Mapear para a propriedade]** para _./jcr:content/metadata/dam:status_.
   1. Altere o valor padrão para _aprovado_.

1. Clique em **[!UICONTROL Salvar]**.
1. Na página **[!UICONTROL Perfis de metadados]**, selecione o perfil de metadados recém-criado.
1. Clique em **[!UICONTROL Aplicar perfil de metadados às pastas]** na barra de ações superior.
1. Selecione as pastas que você precisa aprovar e clique em **[!UICONTROL Aplicar]**.
   <br> A permissão para toda a pasta está definida para aprovação e todos os ativos carregados para essa pasta são automaticamente aprovados.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>Essa abordagem aprova os ativos recém-criados na pasta. Para ativos existentes na pasta, é necessário selecionar e aprovar manualmente.

## Gerenciar ativos carregados usando o Content Hub {#manage-assets-uploaded-using-content-hub}

[Os usuários do Content Hub com direitos para adicionar ativos](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) podem [adicionar ativos ao Content Hub](/help/assets/upload-brand-approved-assets.md) a partir do sistema de arquivos local ou importar ativos de fontes de dados do OneDrive ou do Dropbox. Todos os ativos são exibidos no nível superior do Content Hub, independentemente da estrutura de pastas disponível no sistema de arquivos local ou nas fontes de dados do OneDrive e do Dropbox para aprimorar os recursos de pesquisa.

A exibição de ativos carregados usando o Content Hub depende de se você [habilitou a opção de Aprovação automática](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub):

* Se a opção **[!UICONTROL Aprovação automática]** estiver habilitada, os ativos carregados usando o Content Hub estarão automaticamente disponíveis.

* Se a opção **[!UICONTROL Aprovação automática]** estiver desabilitada, os ativos carregados usando o Content Hub não serão exibidos automaticamente. Os ativos estão disponíveis na pasta `hydrated-assets` do seu ambiente as a Cloud Service do Assets. Navegue até a pasta e [edite em massa](#bulk-approve-assets-content-hub) o status desses ativos para `Approved` para que eles sejam exibidos no Content Hub.

![processo de aprovação do Content Hub](/help/assets/assets/content-hub-approval.png)
