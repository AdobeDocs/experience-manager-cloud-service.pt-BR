---
title: Restringir a entrega de ativos no Experience Manager
description: Saiba como restringir a entrega de ativos no [!DNL Experience Manager].
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: 65f0018a25c57189229fc56332ad874ebd0deef4
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%

---

# Restringir o acesso a ativos em [!DNL Experience Manager] {#restrict-access-to-assets}

A governança de ativos centrais no Experience Manager permite que o administrador do DAM ou os gerentes de marca gerenciem o acesso aos ativos. Eles podem restringir o acesso configurando funções para ativos aprovados no lado da criação, especificamente na instância de autor do AEM as a Cloud Service.

Os usuários [pesquisando](search-assets-api.md) ou utilizando [URLs de entrega](deliver-assets-apis.md) podem obter acesso a ativos restritos após passar com êxito no processo de autorização.

![Acesso restrito a ativos](/help/assets/assets/restricted-access.png)

## Entrega restrita usando um token IMS {#restrict-delivery-ims-token}

No Experience Manager Assets, a entrega restrita via IMS envolve dois estágios principais:

* Criação  
* Entrega

### Criação   {#authoring}

Você pode restringir a entrega de ativos em [!DNL Experience Manager] com base em funções. Para configurar funções, execute as seguintes etapas:

1. Vá para [!DNL Experience Manager] como Administrador do DAM.
1. Selecione o ativo para o qual você precisa configurar a função.
1. Navegue até **[!UICONTROL Propriedades]** > **[!UICONTROL Avançadas]** e verifique se o campo **[!UICONTROL Funções]** existe na guia [!UICONTROL Metadados Avançados].

   ![Metadados das funções](/help/assets/assets/roles_metadata.jpg)
Se o campo não estiver disponível, use as seguintes etapas para adicionar o campo:

   1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de Metadados]**.
   1. Selecione o esquema de metadados e clique em **[!UICONTROL Editar _(e)_]**.
   1. Adicione um campo **[!UICONTROL Texto de vários valores]** da seção **[!UICONTROL Criar formulário]** no lado direito à seção Metadados no formulário.
   1. Clique no campo recém-adicionado e faça as seguintes atualizações no painel **[!UICONTROL Configurações]**:
      1. Altere o **[!UICONTROL Rótulo do campo]** para _Funções_.
      1. Atualize o **[!UICONTROL Mapear para a propriedade]** para _./jcr:content/metadata/dam:roles_.

1. Obtenha os grupos IMS que serão adicionados aos metadados de funções do ativo. Para buscar os grupos IMS, siga estas etapas:
   1. Entrar em `https://adminconsole.adobe.com/.`
   1. Vá para sua respectiva organização e navegue até **[!UICONTROL Grupos de Usuários]**.
   1. Selecione o **[!UICONTROL Grupo de Usuários]** que você precisa adicionar e extraia a **[!UICONTROL orgID]** e a **[!UICONTROL userGroupID]** da URL ou use sua ID da Organização, como `{orgID}@AdobeOrg:{usergroupID}`.

1. Adicione a ID do grupo ao campo **[!UICONTROL Funções]** das propriedades do ativo. <br>
As IDs de grupo definidas no campo **[!UICONTROL Funções]** são os únicos usuários que podem acessar o ativo. Além da ID do grupo IMS, também é possível adicionar a ID de usuário IMS e a ID de perfil IMS no campo **[!UICONTROL Funções]**. Por exemplo, `{orgId}@AdobeOrg:{profileId}`.

   >[!NOTE]
   >
   >Para a nova visualização do Assets, você só pode conceder acesso até o nível da pasta e exclusivamente a grupos, em vez de usuários individuais. Saiba mais sobre o [gerenciamento de permissões no Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### Restringir a entrega de ativos usando data e hora de ativação e desativação {#restrict-delivery-assets-date-time}

Os autores do DAM também podem restringir a entrega de ativos definindo um tempo Ligado ou Desligado para ativação disponível nas Propriedades do ativo.

Se você definir um No prazo para ativação de um ativo, um URL de entrega é gerado para o ativo no momento definido. O ativo permanece inativo antes do tempo definido. Da mesma forma, se você definir um Tempo de desativação para um ativo, ele será desativado no momento definido e o URL de entrega do ativo deixará de exibi-lo.

Execute as seguintes etapas para definir os horários de ativação e desativação do ativo:

1. Selecione o ativo e clique em **[!UICONTROL Propriedades]**.

1. Na seção **[!UICONTROL Ativação agendada (de)]** da guia **[!UICONTROL Básico]**, defina o Momento da ativação ou o Momento da desativação com base em suas necessidades.

Da mesma forma, no modo de exibição Assets, você pode selecionar o ativo e clicar em **[!UICONTROL Detalhes]** para exibir as propriedades do ativo e definir Momento da ativação e Momento da desativação.

O campo está disponível no formulário de metadados padrão. Se o ativo não for baseado no esquema de metadados padrão e os campos Momento da ativação e Momento da desativação não estiverem disponíveis nas propriedades do ativo, execute as seguintes etapas na exibição Administração:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de Metadados]**.
1. Selecione o esquema de metadados e clique em **[!UICONTROL Editar]**.
1. Adicione um campo **[!UICONTROL Data]** da seção **[!UICONTROL Criar formulário]** no lado direito à seção Metadados no formulário.
1. Clique no campo recém-adicionado e faça as seguintes atualizações no painel **[!UICONTROL Configurações]**:
   1. Altere o **[!UICONTROL Rótulo do Campo]** para **No Horário** ou **Fora do Horário**.
   1. Atualize o **[!UICONTROL Mapear para a propriedade]** para _./jcr:content/onTime_ para os campos **No Horário** e _./jcr:content/offTime_ para o campo **Tempo Desligado**.
1. Clique em **[!UICONTROL Salvar]**.

Da mesma forma, na visualização do Assets, se o ativo não for baseado no esquema de metadados padrão e os campos Momento da ativação e Momento da desativação não estiverem disponíveis nas propriedades do ativo, execute as seguintes etapas:

1. Clique em **[!UICONTROL Metadata Forms]** na seção **[!UICONTROL Configurações]**.
1. Selecione o formulário de metadados e clique em **[!UICONTROL Editar]**.
1. Adicione um campo **[!UICONTROL Data]** da seção **[!UICONTROL Componentes]** no painel esquerdo ao formulário.
1. Clique no campo recém-adicionado e altere o **[!UICONTROL Rótulo]** para **Momento da ativação** ou **Momento da desativação**.
1. Atualize a **[!UICONTROL propriedade de Metadados]** para _./jcr:content/onTime_ para os campos **No Horário** e _./jcr:content/offTime_ para o campo **Tempo Desligado**.
1. Clique em **[!UICONTROL Salvar]**.



### Entrega de ativos restritos {#delivery-restricted-assets}

A entrega de ativos restritos é baseada na autorização bem-sucedida para acessar ativos. A autorização é baseada em um token IMS se a solicitação for enviada de uma instância de autor AEM ou do Seletor de ativos ou é baseada em um cookie especial se você tiver provedores de identidade personalizados configurados em sua instância do Publish ou de Pré-visualização.

#### Entrega para solicitações do autor do AEM ou do Seletor de ativos {#delivery-aem-author-asset-selector}

Para habilitar a entrega de ativos restritos caso a solicitação seja enviada da instância do autor do AEM ou do Seletor de ativos, um token IMS válido é essencial. Siga estas etapas:

1. [Gerar um token de acesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * Faça logon no Dev Console do ambiente do AEM as a Cloud Service.

   * Navegue até **[!UICONTROL Ambiente]** > **[!UICONTROL Integrações]** > **[!UICONTROL Token Local]** > **[!UICONTROL Obter Token de Desenvolvimento Local]** > **[!UICONTROL Copiar valor de accessToken]**. Saiba mais sobre [como acessar o token e aspectos relacionados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. Integre o token de acesso obtido ao cabeçalho **[!UICONTROL Autorização]**, garantindo que seu valor tenha o prefixo **[!UICONTROL Portador]**.

1. Valide a funcionalidade do token de acesso iniciando uma solicitação. Ele deve gerar um erro 404 nos casos em que não há um token de acesso IMS ou o token de acesso fornecido não tem as mesmas entidades ou grupos que os adicionados nos metadados do ativo.

#### Entrega para provedores de identidade personalizados na instância do Publish {#delivery-custom-identity-provider}

No caso de um provedor de identidade personalizado configurado na sua instância do Publish ou de Pré-visualização, você pode mencionar o grupo que deve ter acesso aos ativos protegidos no atributo `groupMembership` durante o processo de configuração. Ao fazer logon no provedor de identidade personalizado por meio da [integração SAML](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), o atributo `groupMembership` é lido e usado para construir um cookie, que é enviado em todas as solicitações de autenticação, de modo semelhante a um token IMS no caso de uma solicitação do autor de AEM ou do Seletor de ativos.

Quando um ativo seguro está disponível em uma página e uma solicitação é feita ao URL de entrega para renderizar o ativo, o AEM verifica as funções presentes no cookie ou no token IMS e o compara com a `dam:roles property` aplicada durante a criação do ativo. Se houver uma correspondência, o ativo será exibido.

>[!NOTE]
>
> No [tíquete de suporte para ativar o Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities), mencione a entrega restrita no caso de uso. A engenharia de Adobe ajudará com os esclarecimentos necessários e/ou configurará o processo para entrega restrita.
