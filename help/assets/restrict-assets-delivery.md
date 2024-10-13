---
title: Restringir a entrega de ativos com Dynamic Media com recursos OpenAPI
description: Saiba como restringir a entrega de ativos com recursos OpenAPI.
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: 6e9fa8301fba9cab1a185bf2d81917e45acfe3a3
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 0%

---

# Restringir a entrega de ativos com Dynamic Media com recursos OpenAPI {#restrict-access-to-assets}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

A governança de ativos centrais no Experience Manager permite que o administrador do DAM ou os gerentes de marca gerenciem o acesso aos ativos disponíveis por meio do Dynamic Media com recursos OpenAPI. Eles podem restringir a entrega de ativos aprovados (até um ativo individual) para usuários ou grupos selecionados do [Adobe Identity Management System (IMS)](https://helpx.adobe.com/in/enterprise/using/users.html#user-mgt-strategy), configurando determinados metadados nos ativos no serviço de autor do AEM as a Cloud Service.

Quando um ativo é restrito por meio do Dynamic Media com OpenAPIs, somente os usuários (Adobe IMS integrado) autorizados a acessar o ativo recebem acesso. Para acessar o ativo, o usuário deve aproveitar os recursos do [Search](search-assets-api.md) e do [Delivery](deliver-assets-apis.md) do Dynamic Media com OpenAPI.

![Acesso restrito a ativos](/help/assets/assets/restricted-access.png)

No Experience Manager Assets, a entrega restrita via IMS envolve dois estágios principais:

* Criação  
* Entrega

## Criação   {#authoring}

### Entrega restrita usando um token de portador IMS {#restrict-delivery-ims-token}

Você pode restringir a entrega de ativos em [!DNL Experience Manager] com base nas Identidades de Usuário e de Grupo IMS.

>[!NOTE]
>
> No momento, esse recurso não é de autoatendimento. Para restringir a entrega de ativos para IMS [Usuários](https://helpx.adobe.com/in/enterprise/using/manage-directory-users.html) e [Grupos](https://helpx.adobe.com/in/enterprise/using/user-groups.html), entre em contato com a equipe de Suporte Enterprise para obter orientação sobre como recuperar as informações necessárias para restringir o acesso no portal [Adobe Admin Console](https://adminconsole.adobe.com/) e como configurar o acesso no serviço de autor do AEM as a Cloud Service.

### Restringir a entrega de ativos usando data e hora de ativação e desativação {#restrict-delivery-assets-date-time}

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



## Entrega de ativos restritos {#delivery-restricted-assets}

A entrega de ativos restritos é baseada na autorização bem-sucedida para acessar ativos. A autorização é por meio de [Tokens de portador do IMS](https://developer.adobe.com/developer-console/docs/guides/authentication/UserAuthentication/IMS/) (aplicativo para solicitações iniciadas a partir do [Seletor de ativos do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector)), ou um cookie seguro (se você tiver provedores de identidade personalizados configurados nos serviços AEM Publish/Preview e tiver configurado a criação e a inclusão do cookie nas páginas).

### Entrega para solicitações do autor do AEM ou do Seletor de ativos {#delivery-aem-author-asset-selector}

Para permitir a entrega de ativos restritos caso a solicitação seja enviada do serviço de autor de AEM ou do Seletor de ativos de AEM, é essencial um token de portador IMS válido.\
Nos serviços de autor do AEM Cloud Service, bem como no Seletor de ativos, o Token de portador do IMS é gerado e usado automaticamente para solicitações após um logon bem-sucedido.

>[!NOTE]
>
>Para obter mais informações sobre como habilitar a autenticação IMS em integrações baseadas no Seletor de ativos AEM, entre em contato com o Suporte corporativo

1. Para experiências não baseadas no Seletor de ativos, o AEM as a Cloud Service e o Dynamic Media com recursos OpenAPI atualmente oferecem suporte a integrações de api do lado do servidor e podem gerar tokens de Portador IMS.
   * Siga as instruções [aqui](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#the-server-to-server-flow) para executar integrações de API de serviço para servidor que possam recuperar os tokens do Portador IMS por meio do [AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console)
   * Por tempo limitado, o acesso de desenvolvedor local (não destinado a casos de uso de produção), tokens de Portador IMS de vida curta para o usuário autenticado no [AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console) podem ser gerados seguindo as instruções [aqui](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#developer-flow)

1. Ao fazer solicitações de API de [Pesquisa](search-assets-api.md) e [Entrega](deliver-assets-apis.md), adicione o token do Portador IMS obtido ao cabeçalho **[!UICONTROL Autorização]** da solicitação HTTP (verifique se o valor tem o prefixo **[!UICONTROL Portador]**).

1. Para validar a restrição de acesso, inicie uma solicitação da API de Entrega com e sem o cabeçalho **[!UICONTROL Autorização]**.
   * A resposta produzirá um código de status de erro `404` nos casos em que não houver um token do Portador IMS ou o token do Portador IMS fornecido não pertencer ao usuário que recebeu acesso ao ativo (diretamente ou por meio de associação de grupo).
   * A resposta produzirá um código de status de sucesso `200` com o conteúdo binário do ativo se o token do Portador IMS for um dos usuários ou grupos aos quais foi concedido acesso ao ativo.

### Entrega para provedores de identidade personalizados no serviço Publish {#delivery-custom-identity-provider}

O AEM Sites, o AEM Assets e o Dynamic Media AEM com licenças OpenAPI podem ser usados em conjunto, e a entrega restrita de ativos pode ser configurada em sites entregues pelo Publish ou pelos serviços de Pré-visualização.
Se os serviços Publish e de Visualização do AEM Sites estiverem configurados para usar um [provedor de identidade personalizado (IdP)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), o grupo que deve ter acesso aos ativos protegidos no poderá ser incluído no atributo `groupMembership` durante o processo de instalação.\
Quando um usuário do site faz logon no provedor de identidade personalizado e acessa o site hospedado no serviço Publish/Preview, o atributo `groupMembership` é lido e um cookie seguro é construído e entregue no site após a autenticação bem-sucedida. Este cookie seguro é incluído em todas as solicitações subsequentes para entregar o conteúdo do site ao user-agent.

Quando um ativo seguro é solicitado em uma página, os níveis de AEM Publish e Pré-visualização extraem o material de autorização do cookie seguro e validam o acesso. Se houver uma correspondência, o ativo será exibido.

>[!NOTE]
>
> No [tíquete de suporte para ativar o Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities), mencione a entrega restrita no caso de uso. A engenharia de Adobe ajudará com os esclarecimentos necessários e/ou configurará o processo para entrega restrita.