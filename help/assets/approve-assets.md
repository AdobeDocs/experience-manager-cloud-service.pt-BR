---
title: Aprovar ativos no Experience Manager
description: Saiba como aprovar ativos no [!DNL Experience Manager].
role: User
exl-id: fe61a0f1-94d3-409a-acb9-195979668c25
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 1%

---

# Aprovar ativos em [!DNL Experience Manager]

Os gerentes e comerciantes de marca mantêm controle rigoroso sobre os ativos da marca. Somente as versões aprovadas e mais recentes do ativo estão disponíveis para uso, garantindo a consistência da marca em todos os canais e aplicativos.

Você pode aprovar ativos no AEM Assets para simplificar o gerenciamento de ativos, garantindo um processo controlado e eficiente para manuseio de ativos.

## Antes de começar {#pre-requisites}

Você deve ter acesso ao AEM Assets as a Cloud Service e permissões para editar a propriedade **[!UICONTROL Status da revisão]** de um ativo.

## Configuração

Você precisa fazer uma atualização única no esquema de metadados aplicável na Exibição de administrador antes de aprovar um ativo. Você pode ignorar essa configuração na exibição do Assets. Siga estas etapas para configurar o esquema de metadados:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de Metadados]**.
1. Selecione o esquema de metadados aplicável e clique em **[!UICONTROL Editar]**. <br>O **[!UICONTROL Editor do Formulário de Esquema de Metadados]** é aberto com a guia **[!UICONTROL Básico]** realçada.
1. Role para baixo e clique em **[!UICONTROL Status da revisão]**.
1. Clique na guia **[!UICONTROL Regras]** no painel direito.
1. Desmarcar **[!UICONTROL Desabilitar edição]**.
Se você precisar exibir a propriedade para a qual o campo **[!UICONTROL Status da Revisão]** está mapeado, navegue até a guia **[!UICONTROL Configurações]** e exiba o valor `./jcr:content/metadata/dam:status` no campo **[!UICONTROL Mapear para a propriedade]**.
1. Arraste e solte um campo **[!UICONTROL Suspenso]** da seção **[!UICONTROL Criar Formulário]** no lado direito para a seção Metadados no formulário.
1. Clique no campo recém-adicionado e faça as seguintes atualizações no painel **[!UICONTROL Configurações]**:
   1. Alterar o **[!UICONTROL Rótulo do campo]** para _Destino da Aprovação_.
   1. Atualize o **[!UICONTROL Mapear para a propriedade]** para _./jcr:content/metadata/dam:ativationTarget_.
   1. Adicione as opções com `contenthub` e `delivery` como valores de opção.

   >[!NOTE]
   >
   >Ao selecionar o público alvo de aprovação como Content Hub usando a exibição do Assets, os ativos são disponibilizados no Content Hub para os usuários que fazem parte da mesma organização. Ao selecionar o público alvo de aprovação como Entrega, os ativos ficam disponíveis para todos os usuários.

1. Clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Se os ativos ou pastas tiverem um esquema padrão diferente, certifique-se de fazer essa atualização nesse esquema específico.

## Aprovar ativos {#approve-assets}

Para aprovar ativos em [!DNL Experience Manager Admin view], siga estas etapas:

1. Selecione o(s) ativo(s) e clique em **[!UICONTROL Propriedades]** no painel superior.
1. Na guia **[!UICONTROL Básico]**, role para baixo até **[!UICONTROL Status de Revisão]**.
1. Alterar o status da revisão para **[!UICONTROL Aprovado]**.
   ![imagem](/help/assets/assets/approve-old-ui.png)
1. Clique em **[!UICONTROL Salvar e fechar]**.

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   Da mesma forma, você pode aprovar ativos usando a [nova exibição do Assets](/help/assets/manage-organize-assets-view.md).

## Aprovar ativos em massa {#bulk-approve-assets}

Simplifique o fluxo de trabalho aprovando rapidamente vários ativos de uma só vez. Você pode aprovar ativos em massa para acelerar o processo de aprovação, economizando tempo e melhorando a produtividade.
<br>Siga estas etapas para aprovar ativos em massa em [!DNL Experience Manager Admin view]:

1. Crie uma pasta no ambiente de criação (https://author-pXXX-eYYY.adobeaemcloud.com). Substitua _XXX_ pela ID do programa e _AAAA_ pela ID do ambiente da Experience Manager.
1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Metadados]**.
1. Clique em **[!UICONTROL Criar]** no lado superior direito da página.
1. Adicione um título de Perfil e clique em **[!UICONTROL Criar]**. O perfil de metadados foi criado com sucesso.
1. Selecione o perfil de metadados recém-criado e clique em **[!UICONTROL Editar _(e)_]**. <br>O formulário **[!UICONTROL Editar Perfil de Metadados]**é aberto com a guia **[!UICONTROL Básico]**realçada.
1. Arraste e solte um **[!UICONTROL Campo de Texto de Linha Única]** da seção **[!UICONTROL Criar Formulário]** no lado direito para a seção Metadados no formulário.
1. Clique no campo recém-adicionado e faça as seguintes atualizações no painel **[!UICONTROL Configurações]**:
   1. Altere o **[!UICONTROL Rótulo do campo]** para _Assets Aprovado_.
   1. Atualize o **[!UICONTROL Mapear para a propriedade]** para _./jcr:content/metadata/dam:status_.
   1. Altere o valor padrão para _aprovado_.

1. Arraste e solte um campo **[!UICONTROL Suspenso]** da seção **[!UICONTROL Criar Formulário]** no lado direito para a seção Metadados no formulário.
1. Clique no campo recém-adicionado e faça as seguintes atualizações no painel **[!UICONTROL Configurações]**:
   1. Alterar o **[!UICONTROL Rótulo do campo]** para _Destino da Aprovação_.
   1. Atualize o **[!UICONTROL Mapear para a propriedade]** para _./jcr:content/metadata/dam:ativationTarget_.
   1. Adicione as opções com `contenthub` e `delivery` como valores de opção.

   >[!NOTE]
   >
   >Ao selecionar o público alvo de aprovação como Content Hub usando a exibição do Assets, os ativos são disponibilizados no Content Hub para os usuários que fazem parte da mesma organização. Ao selecionar o público alvo de aprovação como Entrega, os ativos ficam disponíveis para todos os usuários.
1. Clique em **[!UICONTROL Salvar]**.
1. Na página **[!UICONTROL Perfis de metadados]**, selecione o perfil de metadados recém-criado.
1. Clique em **[!UICONTROL Aplicar perfil de metadados às pastas]** na barra de ações superior.
1. Selecione as pastas que você precisa aprovar e clique em **[!UICONTROL Aplicar]**.
   <br> A permissão para toda a pasta está definida para aprovação e todos os ativos carregados para essa pasta são automaticamente aprovados.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>Essa abordagem aprova os ativos recém-criados na pasta. Para ativos existentes na pasta, é necessário selecionar e aprovar manualmente. <br> Como alternativa, você pode usar a opção **[!UICONTROL Reprocessar]** para aplicar as alterações do perfil de metadados aos ativos mais antigos.

Da mesma forma, para aprovar ativos em massa em uma pasta na exibição do Assets:

1. Selecione o(s) ativo(s) e clique em **[!UICONTROL Editar metadados em massa]**.

1. Selecione **[!UICONTROL Aprovado]** no campo **[!UICONTROL Status]**, disponível na seção [!UICONTROL Propriedades] do painel direito.

   Se você selecionar o status como `Approved` e se o [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) ou o [Content Hub](/help/assets/product-overview.md), ou ambos, estiver habilitado para a sua Experience Manager Assets, você poderá exibir as opções de `Delivery` e `Content Hub` disponíveis no campo **[!UICONTROL Destino da Aprovação]**.

   * Selecione **[!UICONTROL Entrega]** para disponibilizar os ativos para o Dynamic Media com recursos OpenAPI e Content Hub. Se o Content Hub não estiver ativado, selecionar essa opção disponibiliza os ativos somente para o Dynamic Media com recursos OpenAPI.
   * Selecione **[!UICONTROL Content Hub]** para disponibilizar os ativos para o Content Hub.

   ![Status de aprovação](/help/assets/assets/approval-status-delivery.png)

   Se você não estiver usando o formulário de metadados padrão e não puder exibir o campo **[!UICONTROL Destino da Aprovação]**, [edite o formulário de metadados](/help/assets/metadata-assets-view.md#metadata-forms) para arrastar o campo **[!UICONTROL Aprovação para]** dos componentes disponíveis para o formulário de metadados e clique em **[!UICONTROL Salvar]**.

   >[!NOTE]
   >
   >Se você selecionar o público alvo de aprovação como `Content Hub` usando a exibição do Assets em uma organização, os ativos serão disponibilizados no Content Hub para os usuários que fazem parte da mesma organização.

1. Clique em **[!UICONTROL Salvar]**.

## Copiar URL de entrega dos ativos aprovados {#copy-delivery-url-approved-assets}

A URL de entrega de todos os ativos aprovados no repositório estará disponível se você tiver o [!UICONTROL Dynamic Media com recursos OpenAPI] habilitados na sua instância do AEM as a Cloud Service.

Para copiar o URL de entrega de um ativo aprovado no repositório:

1. Selecione o ativo e clique em **[!UICONTROL Detalhes]**.

1. Clique no ícone Dynamic Media disponível no painel direito.

1. Selecione o **[!UICONTROL Dynamic Media com OpenAPI]** disponível no painel **[!UICONTROL Dynamic Media]**.

1. Clique em **[!UICONTROL Copiar URL]** para copiar a URL de entrega do ativo.
   ![representações dinâmicas](/help/assets/assets/dm-with-openapi-non-image-assets.png)

   >[!NOTE]
   >
   >A opção para copiar o URL de entrega para ativos aprovados está disponível apenas na visualização Assets.

Para obter informações sobre outras representações exibidas no painel Dynamic Media, consulte [Exibir e baixar representações do Dynamic Media](/help/assets/renditions.md#view-download-dm-renditions).
