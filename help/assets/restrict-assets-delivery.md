---
title: Restringir a entrega de ativos no Experience Manager
description: Saiba como restringir a entrega de ativos no [!DNL Experience Manager].
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Restringir o acesso a ativos no [!DNL Experience Manager] {#restrict-access-to-assets}

A governança de ativos centrais no Experience Manager permite que o administrador do DAM ou os gerentes de marca gerenciem o acesso aos ativos. Eles podem restringir o acesso configurando funções para ativos aprovados no lado da criação, especificamente na instância de autor as a Cloud Service do AEM.

Usuários [pesquisando](search-assets-api.md) ou utilizando [URLs de entrega](deliver-assets-apis.md) O pode obter acesso aos ativos restritos após a aprovação bem-sucedida no processo de autorização.

![Acesso restrito a ativos](/help/assets/assets/restricted-access.png)

## Entrega restrita usando um token IMS {#restrict-delivery-ims-token}

No Experience Manager, a entrega restrita via IMS envolve dois estágios principais:

* Criação  
* Entrega

### Criação   {#authoring}

Para restringir a entrega de ativos, as funções devem ser configuradas para os ativos dentro do [!DNL Experience Manager] ou [!DNL Experience Manager Assets]. Para configurar funções no [!DNL Experience Manager], siga estas etapas:

1. Vá para a [!DNL Experience Manager] como administrador do DAM.
1. Selecione o ativo para o qual você precisa configurar a função.
1. Navegue até **[!UICONTROL Propriedades]** > **[!UICONTROL Avançado]** e assegurar que a **[!UICONTROL Funções]** o campo existe na variável [!UICONTROL Metadados avançados] guia.

   ![Metadados de funções](/help/assets/assets/roles_metadata.jpg)
Se o campo não estiver disponível, use as seguintes etapas para adicionar o campo:

   1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadados]**.
   1. Selecione o esquema de metadados e clique em **[!UICONTROL Editar _e)_]**.
   1. Adicionar um **[!UICONTROL Texto multivalor]** do campo **[!UICONTROL Formulário de criação]** no lado direito à seção Metadados no formulário.
   1. Clique no campo recém-adicionado e faça as seguintes atualizações no  **[!UICONTROL Configurações]** painel:
      1. Altere o **[!UICONTROL Rótulo do campo]** para _Funções_.
      1. Atualize o **[!UICONTROL Mapear para a propriedade]** para _./jcr:content/metadata/dam:roles_.

1. Obtenha os grupos IMS que serão adicionados aos metadados de funções do ativo. Para buscar os grupos IMS, siga estas etapas:
   1. Faça logon em https://adminconsole.adobe.com/.
   1. Acesse sua respectiva organização e navegue até **[!UICONTROL Grupos de usuários]**.
   1. Selecione o **[!UICONTROL Grupo de usuários]** é necessário adicionar e extrair o **[!UICONTROL orgID]** e **[!UICONTROL userGroupID]** do URL ou use sua ID organizacional, como `{orgID}@AdobeOrg:{usergroupID}`.

1. Adicione a ID do grupo à **[!UICONTROL Funções]** campo de propriedades do ativo. <br>
As IDs de grupo definidas no **[!UICONTROL Funções]** são os únicos usuários que podem acessar o ativo. Você também pode adicionar a ID do cliente IMS e a ID do perfil IMS na **[!UICONTROL Funções]** campo. Por exemplo, `{orgId}@AdobeOrg:{profileId}`.

   >[!NOTE]
   >
   >Para a nova visualização de Ativos, você só pode conceder acesso até o nível da pasta e exclusivamente a grupos, em vez de usuários individuais. Saiba mais sobre [gerenciamento de permissões no Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

### Entrega de ativos restritos {#delivery-restricted-assets}

A entrega de ativos restritos é baseada na autorização bem-sucedida para acessar ativos. A autorização é baseada em um token IMS se a solicitação for enviada de uma instância de autor AEM ou do Seletor de ativos, ou é baseada em um cookie especial se você tiver provedores de identidade personalizados configurados em sua instância de Publicação ou Visualização.

#### Entrega para autor de AEM ou Seletor de ativos {#delivery-aem-author-asset-selector}

Para habilitar a entrega de ativos restritos caso a solicitação seja enviada da instância do autor do AEM ou do Seletor de ativos, um token IMS válido é essencial. Siga estas etapas:

1. [Gerar um token de acesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * Faça logon no Dev Console do ambiente AEM as a Cloud Service.

   * Navegue até **[!UICONTROL Ambiente]** > **[!UICONTROL Integrações]** > **[!UICONTROL Token local]** > **[!UICONTROL Obter token de desenvolvimento local]** > **[!UICONTROL Copiar valor accessToken]**. Saiba mais sobre [como acessar o token e aspectos relacionados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. Integre o token de acesso obtido à **[!UICONTROL Autorização]** cabeçalho, verificando se o valor tem o prefixo **[!UICONTROL Portador]**.

1. Valide a funcionalidade do token de acesso iniciando uma solicitação. Ele deve gerar um erro 404 nos casos em que não há um token de acesso IMS ou o token de acesso fornecido não tem as mesmas entidades ou grupos que os adicionados nos metadados do ativo.

#### Entrega para provedores de identidade personalizados {#delivery-custom-identity-provider}

No caso de um provedor de identidade personalizado configurado na instância de Publicação ou Visualização, você pode mencionar o grupo que deve ter acesso aos ativos protegidos no `groupMembership` durante o processo de configuração. Ao fazer logon no provedor de identidade personalizado por meio de [Integração SAML](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), o `groupMembership` O atributo é lido e usado para construir um cookie, que é enviado em todas as solicitações de autenticação, semelhante a um token IMS no caso de uma solicitação do autor de AEM ou do Seletor de ativos.

Quando um ativo seguro está disponível em uma página e uma solicitação é feita ao URL de entrega para renderizar o ativo, o AEM verifica as funções presentes no cookie ou no token IMS e o compara com o `dam:roles property` aplicado durante a criação do ativo. Se houver uma correspondência, o ativo será exibido.
