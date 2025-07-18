---
title: Como configurar um ambiente do  [!DNL AEM Forms] as a cloud service?
description: Saiba como instalar e configurar um ambiente  [!DNL AEM Forms] as a Cloud Service.
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 42f53662-fbcf-4676-9859-bf187ee9e4af
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 6%

---

# Integrar a [!DNL AEM Forms] as a Cloud Service {#overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |


## Decidir personas {#personas-aem-forms-project}

<!-- When you sign up for the service, Adobe creates an Organization identifier for your company in the Adobe Identity Management System (IMS), where your users and their permissions can be managed. So, --> Antes de integrar a um ambiente as a Cloud Service do Adobe Experience Manager (AEM) Forms, decida os perfis e estruture uma equipe para o seu projeto. Uma equipe típica de projeto [!DNL AEM Forms] tem as seguintes personalidades:

* **Designer de Experiência do Usuário (UX)**: uma Designer de Experiência do Usuário (UX) define estilo, layout e identidade visual para [!DNL AEM Forms] ativos.

* **Profissional do Forms**: um profissional do Forms cria Forms adaptável, temas e modelos de acordo com o estilo, o layout e a marca fornecidos pelo Designer UX. O profissional também cria e integra o formulário adaptável a um modelo de dados de formulário (FDM) e fluxos de trabalho de AEM. Um profissional da Forms normalmente executa tarefas relacionadas ao front-end.

* **Desenvolvedor do Forms**: um desenvolvedor do Forms desenvolve uma solução de formulários personalizada. Um desenvolvedor do Forms normalmente realiza o desenvolvimento de back-end, como desenvolver componentes personalizados, fluxos de trabalho de AEM, serviços de pré-preenchimento e muito mais.

* **Administrador de AEM**: um administrador AEM ajuda na configuração geral, como configurar usuários, fortalecer o ambiente, configurar fontes de dados, configurar email e software de terceiros. O administrador do AEM também ajuda em integrações como a integração com o Adobe Analytics, o Adobe Target e o Adobe Sign.

* **Usuário final**: um usuário interage com o formulário publicado e o envia, assina formulários enviados, rastreia aplicativos enviados por meio de um portal da web e recebe comunicações personalizadas.

<!-- While onboarding to the service, assign the following AEM groups to [!DNL AEM Forms] as a Cloud Service based on their role:

| User type | AEM group |
|---|---|
| Form Practitioner | forms-users (AEM Forms Users), template-authors, workflow-user, workflow-editors, and fdm-author  |
| UX Designer| forms-users, template-authors|
| End-User| <ul> <li>When a user must login to view and submit an Adaptive Form, add such users to forms-users group. </li> <li>When no user authentication is required to access Adaptive Forms, do not assign any group to such users. </li> </ul>| -->

## Integração ao serviço {#onboarding}

* [Integrar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/overview.html?lang=pt-BR) à as a Cloud Service [!DNL Adobe Experience Manager].

* (Somente para sandboxes) Após a integração do serviço, [crie](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/pipelines/production-pipelines.html?lang=pt-BR) e [execute](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html?lang=pt-BR) os pipelines de produção e não produção. As a Cloud Service Ele habilita e traz os recursos mais recentes do [!DNL AEM Forms] para o seu ambiente.

Você pode usar o Forms as a Cloud Service para criar um formulário adaptável (Inscrição digital) ou gerar uma comunicação com o cliente. Depois de concluir a [Integração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/overview.html?lang=pt-BR) aos as a Cloud Service [!DNL Adobe Experience Manager], execute as seguintes ações para habilitar os recursos Forms - Inscrição Digital ou Comunicação com o Cliente. <!--You can also enable both the features-->:

1. Faça logon no Cloud Manager e abra a instância do AEM Forms as a Cloud Service.
1. Abra a opção Editar programa, vá para a guia Soluções &amp; Complementos:

   * Se você tiver um ambiente de produção, selecione a opção **[!UICONTROL Forms - Comunicações]** para habilitar o Forms - Registro Digital e o Forms - Complemento de Comunicações.

     ![Comunicações](assets/communications.png)

   <!-- If you have already enabled the **[!UICONTROL Forms - Digital Enrollment]** option, then select the **[!UICONTROL Forms - Communications Add-On]** option. ![Addon](assets/add-on.png) -->

   * Se você tiver um ambiente de sandbox, selecione **[!UICONTROL Forms]** para habilitar o Forms - Inscrição Digital e o Forms - Complemento de Comunicações.

     ![Seleção de Inscrição Digital de Formulário](assets/forms-digital-enrollment1.png)


1. Clique em **[!UICONTROL Atualizar]**.
1. Execute o pipeline de build. Depois que o pipeline de build for bem-sucedido, a solução selecionada será habilitada para o seu ambiente.

>[!NOTE]
>
> Para habilitar e configurar APIs de manipulação de documentos, adicione a seguinte regra à [configuração do Dispatcher](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## Configurar usuários {#config-users}

Após concluir a integração com o serviço, faça logon no seu ambiente as a Cloud Service do [!DNL AEM Forms], abra instâncias de Autor e do Publish e adicione usuários a [grupos de](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=pt-BR#accessing) específicos do Forms AEM, com base na persona. A tabela a seguir lista os grupos AEM específicos do Forms, disponíveis imediatamente e os tipos de usuários correspondentes. A tabela também fornece o tipo de instância AEM para cada tipo de usuário:

| Tipos de usuário (Personas) | Grupos de usuários | Instância do AEM |
|---|---|---|
| Profissional de formulários /desenvolvedor do Forms | <ul> <li> [!DNL forms-users] </li><li> [!DNL template-author] </li><li> [!DNL workflow-users] </li><li> [!DNL workflow-editors] </li><li> [!DNL fdm-authors] </li></ul> | Instância do autor |
| Designer da experiência do usuário (UX) | <ul> <li> [!DNL forms-users]</li><li> [!DNL template-author] </li></ul> | Instância do autor |
| Administrador do AEM | <ul> <li>[!DNL aem-administrators],</li> <li>[!DNL fd-administrators] </li> </ul> | Autor e instância do Publish |
| Usuário final | <ul> <li>Quando um usuário precisar fazer logon para exibir e enviar um Formulário adaptável, adicione esses usuários ao grupo [!DNL forms-users]. </li> <li>Quando nenhuma autenticação de usuário for necessária para acessar o Adaptive Forms, não atribua nenhum grupo a esses usuários. </li> </ul> | Autor e instância do Publish |

Para obter mais informações sobre grupos AEM específicos do Forms e as permissões correspondentes, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

<!-- You can also create  [user groups](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=pt-BR#accessing) specific  to your organization, assign policies, and [users](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=pt-BR#accessing) to the groups. The policies help control permissions of the users that are part of the group. For information a -->

## Próxima etapa {#next-steps}

[Configurar um ambiente de desenvolvimento local](setup-local-development-environment.md). Você pode usar um ambiente de desenvolvimento local para criar um Formulário adaptável e ativos relacionados (Temas, Modelos, Ações de envio personalizadas, serviço de preenchimento prévio e muito mais). E [converta PDF forms em Forms Adaptável](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=pt-BR) sem fazer logon em um ambiente de desenvolvimento de nuvem.

<!-- ### Business unit and end-users {#business-unit-and-end-users}

| Role| Organization| Description|
|-----|-------|-----|
| UX Designer                  | Customer/System Integrator/Partner | Defines user experience design (style, layout, branding) as per organizational requirements for Adaptive Forms to allow AEM Forms practitioners to design the corresponding themes and templates.                                     |
| Forms Practitioner           | Customer                           | Authors Adaptive Forms, creates Form Data Model integrations, and creates business workflows using the Experience Manager Workflows. Typically undertakes the front-end work.                                                         |
| Business Executive - Digital | Customer                           | Responsible for business unit's product marketing strategy and revenues, main business stakeholders for digital use cases, solutions, and service offerings for the end-users, signs off on the use case implementation and delivery. |
| Customer Experience Lead     | Customer                           | Business user persona. Authors, personalizes and updates Adaptive Forms fields/rules/styling, identifies, and prioritizes business needs. Validates business use-case with SI/Partner developers/practitioners during UAT.            |
| Forms Back-Office User       | Customer                           | End-user internal to organization filling forms, participating in back-office Forms workflows such as review/approval of applications and so on.                                                                                            |
| Forms End-User               | External to customer               | Interacts with and submits the published form as end customer or citizen, signs submitted forms, tracks her applications through web portal, receives personalized interactive communications.                                        |

### Project team {#project-team}

| Role | Org | Description|
|-----|-----|-----|
| Experience Manager Administrator | System Integrator /Partner/Customer | Helps with overall installation, configures SSL certificates, configures data sources, email, and other third-party software, integrations like Adobe Analytics, Adobe Target, Automated Forms Conversion Services with Experience Manager instance. |
| Project Manager                  | System Integrator /Partner/Customer | Converts customer use-case into technical requirements, manages schedule/cost/scope for overall project.                                                                                                                                             |
| Product Owner                    | System Integrator /Partner/Customer | Prioritizes and evaluates scrum team's work for high-quality delivery on time.                                                                                                                                                                       |
| Scrum Master                     | System Integrator /Partner/Customer | Ensures agile values and processes in place to deliver on defined requirements as per prioritization by PO.                                                                                                                                          |
| Infrastructure / security expert | System Integrator /Partner/Customer | Provisions and configures best possible infrastructure, security controls and infra processes to address current and projected RASP requirements.                                                                                                    |
| Technical Architect              | System Integrator /Partner/Customer | Provides best high-level architecture and infrastructure guidance for use-case implementation and address RASP (Reliability, Availability, Scalability, and Performance) and security challenges.                                                    | -->

<!-- ## Onboard to the service {#onboarding}

[Onboard](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=pt-BR) to the [!DNL Adobe Experience Manager] as a Cloud Service. 

After you onboard the service, configure a [local development environment](setup-local-development-environment.md). 

Administrators are responsible for managing Adobe software and services for their organization. Administrators grant access to developers in their organization to connect and use your [!DNL AEM Forms] as a Cloud Service program. When an administrator is provisioned for an organization, the administrator receives an email with title 'You now have administrator rights to manage Adobe software and services for your organization'. If you are an administrator, check your mailbox for email with previously mentioned title and proceed to [add users](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=pt-BR#onboarding-users-in-admin-console) by way of IMS and assign [form-specific groups](forms-groups-privileges-tasks.md) to users based on their role.

## Next step {#next-steps} -->

<!-- ## Prerequisites {#prerequisites}

If you are new to AEM as a cloud service, contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS). Once Adobe has created an organization for your company, your designated administrator is added as the first member of the organization. The administrator can setup an [!DNL AEM Forms] as a Cloud Service instance. 

## Onboard and set up a new environment {#onboard-and-setup-a-new-environment}

Log in to Cloud Manager and create a program. After the program is ready, create environments, add developers or users to environments, and run the pipeline to get the latest version of [!DNL AEM Forms] as a Cloud Service and start developing for your environment. The detailed steps are:

1. Contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS) and provide access to an administrator in your organization.
1. Configure [Automated Forms Conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html?lang=pt-BR). After a configuration is complete, a profile for Automated Forms Conversion Service is available in [Admin Console](https://adminconsole.adobe.com/).

    If the service is not available, log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not use any other ID or Federated ID to login.
    1. Click **[!UICONTROL Automated Forms Conversion Service]** option.
    1. Click **[!UICONTROL New Profile]** in the Products tab.
    1. Specify **[!UICONTROL Name]**, **[!UICONTROL Display Name]**, and **[!UICONTROL Description]** for the profile. Click **[!UICONTROL Done]**. A profile is created. 
1. Log in to [Cloud Manager](https://experience.adobe.com/#/@marketinghub/experiencemanager) and [create a program](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) for your organization.
1. [Create environments](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=pt-BR#adding-environments) within your program.
1. Log in to [Admin console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/what-is-required/add-users-roles.html) and add developers or users to your organization.
1. Run the [build pipeline](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-manager/using/how-to-use/deploying-code.html). It brings latest [!DNL Experience Manager Forms] as a Cloud Service features to your environment.
1. [Start developing](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) and creating Adaptive Forms on [!DNL Experience Manager Forms] as a Cloud Service environment.
1. Configure the [local development environment](setup-local-development-environment.md) for rapid development

## Configure dispatcher caching {#caching}

You can make dispatcher caching related configuration changes to code on your local development instance and deploy the changes to your [!DNL AEM Forms] as a Cloud Service instance. For details, see [update dispatcher configuration](setup-local-development-environment.md).
 -->
