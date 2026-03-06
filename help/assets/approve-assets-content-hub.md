---
title: Aprovar ativos para o Content Hub
description: Saiba como aprovar ativos no Assets as a Cloud Service para disponibilizá-los no Content Hub.
exl-id: fc849028-ab56-4388-b8d6-e36cac8f868f
source-git-commit: 282ab15d8c498b3c0ddba8165b1262bc20729b75
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 4%

---

# Aprovar ativos para o Content Hub {#approve-assets-content-hub}

![Aprovar ativos para o Content Hub](assets/content-hub-approve-assets.png)

>[!AVAILABILITY]
>
>O guia do Content Hub agora está disponível no formato PDF. Baixe o guia inteiro e use o Assistente de IA da Adobe Acrobat para responder às suas consultas.
>
>[!BADGE PDF do Guia do Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Os gerentes e comerciantes de marca mantêm controle rigoroso sobre os ativos da marca. Somente as versões aprovadas e mais recentes do ativo estão disponíveis para uso no Content Hub, garantindo a consistência da marca em todos os canais e aplicativos.

Você pode aprovar ativos usando o AEM Assets as a Cloud Service para simplificar o gerenciamento de ativos, garantindo um processo controlado e eficiente para manuseio de ativos.

## Antes de começar {#pre-requisites}

Antes de começar, você deve ter:

* Acesso ao AEM Assets as a Cloud Service

* Permissões de gravação para editar metadados de ativos para poder editar o campo **[!UICONTROL Status]** disponível em [propriedades de ativos](/help/assets/manage-organize-assets-view.md##manage-asset-status) para um ativo.

## Aprovar ativos para o Content Hub{#approve-assets-for-content-hub}

Os ativos marcados como `approved` no Assets as a Cloud Service estão automaticamente disponíveis no Content Hub.

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

Aprovar ativos em massa usando a exibição do Assets para o AEM Assets as a Cloud Service. Todos os ativos, aprovados em massa, ficam disponíveis no Content Hub.

Para aprovar ativos em massa em uma pasta na exibição do Assets:

1. Selecione o(s) ativo(s) e clique em **[!UICONTROL Editar metadados em massa]**.

1. Selecione **[!UICONTROL Aprovado]** no campo **[!UICONTROL Status]**, disponível na seção [!UICONTROL Propriedades] do painel direito.

1. Clique em **[!UICONTROL Salvar]**.

## Definir público alvo de aprovação {#set-approval-target}

A exibição do Assets permite publicar ativos aprovados no Dynamic Media com recursos OpenAPI, Content Hub ou ambos com base no valor definido no campo **Destino de aprovação**, disponível na página Detalhes do ativo.

Para definir o público alvo de aprovação:

1. Selecione o ativo e clique em **[!UICONTROL Detalhes]** na barra de ferramentas.

1. Na guia **[!UICONTROL Básico]**, selecione o status do ativo na lista suspensa **[!UICONTROL Status]**. Os valores possíveis incluem Aprovado, Rejeitado e Sem status (padrão).

1. Se você selecionar **Aprovado** na etapa 2, selecione um destino de aprovação. Os valores possíveis incluem Delivery e Content Hub.

   * **Delivery** é a opção padrão selecionada no menu suspenso e publica o ativo no [Dynamic Media com OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) e no [Content Hub](/help/assets/product-overview.md), se ambos estiverem habilitados para Experience Manager Assets.

   * Selecionar **Content Hub** publica o ativo apenas no Content Hub. O Content Hub é exibido como uma opção somente se estiver ativado para o Experience Manager Assets.

   * Se você não selecionar uma opção na lista suspensa, a opção padrão ativada para o ambiente do AEM as a Cloud Service será aplicada automaticamente ao ativo.


   Para obter mais informações sobre as opções disponíveis, consulte [Destino de aprovação padrão e destinos de publicação para ativos aprovados](#default-approval-target-options-publish-destinations).

   ![Status de aprovação](/help/assets/assets/approval-status-delivery.png)

1. Especifique outras propriedades do ativo e clique em **[!UICONTROL Salvar]**.

Alguns pontos adicionais a serem observados incluem:

* Quando você não estiver usando o formulário de metadados padrão e não puder exibir o campo **[!UICONTROL Destino da Aprovação]**, [edite o formulário de metadados](/help/assets/metadata-assets-view.md#metadata-forms) para arrastar o campo **[!UICONTROL Aprovação para]** dos componentes disponíveis para o formulário de metadados e clique em **[!UICONTROL Salvar]**.

* Ao selecionar o público alvo de aprovação como `Content Hub` usando a exibição do Assets, os ativos são disponibilizados no Content Hub para os usuários que fazem parte da mesma organização.

### Destino de aprovação padrão e destinos de publicação para ativos aprovados {#default-approval-target-options-publish-destinations}

A tabela a seguir ilustra os pré-requisitos para exibição da lista suspensa `Approval Target` e do público alvo de aprovação padrão com base na habilitação do DM com OpenAPI e Content Hub no seu ambiente AEM as a Cloud Service:

| Dynamic Media com OpenAPI | Centro de conteúdo | A lista suspensa Approval Target é exibida? | Público alvo de aprovação padrão para ativos aprovados | Destino de publicação |
| --- | --- | --- | --- |---|
| Habilitado | Habilitado | Sim | Entrega | Dynamic Media com OpenAPI e Content Hub |
| Não habilitado | Habilitado | Sim | Centro de conteúdo | Centro de conteúdo |
| Habilitado | Não habilitado | Sim | Entrega | Dynamic Media com OpenAPI |
| Não habilitado | Não habilitado | Não | N/A | N/A |

## Automatizar aprovação de ativos recém-assimilados na exibição do administrador {#automate-approval-newly-ingested-assets}

Depois de alternar da exibição do Assets para a exibição do Administrador, é possível definir as configurações da pasta para que todos os novos ativos adicionados à pasta sejam aprovados automaticamente.

Você pode alternar entre as visualizações Admin e Assets das seguintes maneiras:
![Minha visão geral do Workspace](assets/assets-view.png)

Siga estas etapas para automatizar a aprovação de ativos recém-assimilados em [!DNL Experience Manager Admin view]:

1. Crie uma pasta no ambiente de criação (https://author-pXXX-eYYY.adobeaemcloud.com). Substitua _XXX_ pela ID do programa e _AAAA_ pela ID do ambiente da Experience Manager.
1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Metadados]**.
1. Clique em **[!UICONTROL Criar]** no lado superior direito da página.
1. Adicione um título de Perfil e clique em **[!UICONTROL Criar]**. O perfil de metadados foi criado com sucesso.
1. Selecione o perfil de metadados recém-criado e clique em **[!UICONTROL Editar _(e)_]**. <br>O formulário **[!UICONTROL Editar Perfil de Metadados]**é aberto com a guia **[!UICONTROL Básico]**realçada.
1. Arraste e solte um **[!UICONTROL Campo de Texto de Linha Única]** da seção **[!UICONTROL Criar Formulário]** no lado direito para a seção Metadados no formulário.
1. Clique no campo recém-adicionado e faça as seguintes atualizações no painel **[!UICONTROL Configurações]**:
   1. Altere o **[!UICONTROL Rótulo do campo]** para _Assets Aprovado_.
   1. Atualize o **[!UICONTROL Mapear para a propriedade]** para _./jcr:content/metadata/dam :status_.
   1. Altere o valor padrão para _aprovado_.

1. Semelhante à Etapa 6, arraste um **[!UICONTROL Campo de Texto de Linha Única]** da seção **[!UICONTROL Criar Formulário]** no lado direito para a seção Metadados no formulário.
1. Clique no campo recém-adicionado e faça as seguintes atualizações no painel **[!UICONTROL Configurações]**:
   1. Altere o **[!UICONTROL Rótulo do campo]** para _Destino da Ativação_.
   1. Atualize o **[!UICONTROL Mapear para a propriedade]** para _./jcr:content/metadata/dam :activationTarget_.
   1. Altere o valor padrão para _contentub_.

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

* Se a opção **[!UICONTROL Aprovação automática]** estiver desabilitada, os ativos carregados usando o Content Hub não serão exibidos automaticamente. Os ativos estão disponíveis na pasta `hydrated-assets` do seu ambiente do Assets as a Cloud Service. Navegue até a pasta e [edite em massa](#bulk-approve-assets-content-hub) o status desses ativos para `Approved` para que eles sejam exibidos no Content Hub.

![processo de aprovação do Content Hub](/help/assets/assets/content-hub-approval.png)

## Perguntas frequentes {#faqs-content-hub-approved-assets}

### Qual é a finalidade da aprovação de ativos para o Content Hub no Experience Manager as a Cloud Service? {#approving-assets-content-hub}

A aprovação de ativos garante que somente as versões mais recentes e aprovadas estejam disponíveis para uso no Content Hub, mantendo a rígida consistência da marca em todos os canais e aplicativos. Esse processo controlado simplifica o gerenciamento de ativos para gerentes de marca e profissionais de marketing.

### Quais são os pré-requisitos necessários para aprovar ativos para o Content Hub?

Você deve ter acesso ao AEM Assets as a Cloud Service e permissões de gravação para editar metadados de ativos, especificamente o campo **Status** nas propriedades dos ativos.

### Como você aprova um único ativo usando a exibição do Assets no AEM as a Cloud Service?

Selecione o ativo, clique em **Detalhes** na barra de ferramentas, navegue até a guia **Básico**, escolha **Aprovado** na lista suspensa **Status** e clique em **Salvar**. O ativo é disponibilizado no Content Hub.

### Os ativos podem ser aprovados em massa para o Content Hub e, em caso afirmativo, como?

Sim, os ativos podem ser aprovados em massa. Na exibição do Assets, selecione vários ativos, clique em **Editar metadados em massa**, selecione **Aprovado** no campo **Status** em Propriedades e clique em **Salvar**. Todos os ativos selecionados estão disponíveis no Content Hub.

### Como funciona o processo de aprovação de ativos no Content Hub? {#asset-approval-content-hub}

Se o botão Aprovação automática estiver ativado, os ativos carregados usando o Content Hub estarão disponíveis automaticamente. Se estiver desativado, os ativos carregados serão colocados na pasta **ativos hidratados** do Assets as a Cloud Service e você precisará editar manualmente o status em massa para **Aprovados** para que sejam exibidos no Content Hub.

### O que é o campo Destino de aprovação e como ele afeta a publicação de ativos?

O campo **Destino da aprovação** na página Detalhes do ativo permite escolher onde os ativos aprovados são publicados. As opções incluem **Delivery** (publica no Dynamic Media com OpenAPI e Content Hub) ou somente **Content Hub**. Se nenhuma opção for selecionada, o padrão para o ambiente Assets as a Cloud Service será aplicado. Consulte [Destino de aprovação padrão e destinos de publicação para ativos aprovados](#default-approval-target-options-publish-destinations) para obter mais informações.


### O que acontece se você não visualizar o campo Destino da aprovação na página Exibir detalhes do ativo do Assets?

Se o campo **Destino da Aprovação** estiver ausente na página Exibir detalhes do ativo da Assets, você deverá editar o formulário de metadados, arrastar o campo **Aprovação para** dos componentes disponíveis para o formulário e clicar em **Salvar**. Isso permite definir metas de aprovação para ativos.

### Como você pode automatizar a aprovação de ativos recém-assimilados na visualização de administrador?

Crie uma pasta no ambiente de criação, navegue até **Ferramentas** > **Assets** > **Perfis de Metadados**, crie e edite um perfil de metadados. Adicione um Campo de Texto de Linha Única, rotule-o como **Assets Aprovado**, mapeie-o como &#39;./jcr:content/metadata/dam:status&#39; e defina seu valor padrão como `approved`. Aplique o perfil de metadados à pasta. Isso aprova automaticamente novos ativos adicionados à pasta.

### Quem pode acessar ativos aprovados no Content Hub e quais controles estão em vigor?

Os ativos aprovados estão disponíveis para usuários que fazem parte da mesma organização na Content Hub. Controles rigorosos garantem que somente as versões mais recentes e aprovadas estejam acessíveis, ajudando a manter a consistência e a segurança da marca.
