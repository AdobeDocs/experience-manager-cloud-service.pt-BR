---
title: Como integrar o DocuSign a um Formulário adaptável?
description: Saiba como usar o DocuSign com um formulário adaptável para coletar assinaturas eletrônicas.
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 0%

---

# Uso do DocuSign com um formulário adaptável {#integrate-aem-forms-with-DocuSign}

O DocuSign é uma solução de assinatura eletrônica proeminente. Você pode usá-lo para assinar um contrato eletronicamente. É possível integrar o DocuSign a um formulário adaptável. Ele ajuda a enviar um formulário adaptável para assinaturas eletrônicas para vários recipients. O uso de assinaturas eletrônicas ajuda a:

- Feche negócios de qualquer dispositivo com processos totalmente automatizados de propostas, cotações e contratos.
- Conclua os processos de Recursos humanos com mais rapidez e ofereça aos seus funcionários as experiências digitais.
- Reduza os tempos de ciclo do contrato e integre seus fornecedores mais rapidamente.

O AEM Forms as a Cloud Service fornece uma [ação de envio personalizada para o DocuSign](#deploy-custom-submit-action). A ação de envio ajuda a enviar os formulários adaptáveis para assinaturas eletrônicas usando as APIs do DocuSign.

| Você também pode usar a solução de assinatura eletrônica da Adobe, o Adobe Sign, para assinar eletronicamente um formulário adaptável. O AEM Forms tem uma integração muito mais profunda com o Adobe Sign e fornece controles muito mais finos, como assinatura sequencial e paralela, vários métodos de autenticação, experiência de assinatura no formulário e muito mais. Para obter mais informações, consulte [Usando o Adobe Sign em um Formulário adaptável](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Pré-requisitos {#prerequisites}

Os itens a seguir são necessários para integrar o DocuSign ao AEM Forms:

- Uma [conta de desenvolvedor](https://developers.docusign.com/platform/account/) do DocuSign
- Um aplicativo DocuSign
- Credenciais (ID do cliente e Segredo do cliente) do aplicativo da API DocuSign.
- [Ação de envio personalizada e Serviço em nuvem para DocuSign](https://github.com/adobe/aem-forms-docusign-sample)
- (Somente para ambiente de desenvolvimento local) [Configurar Documento de Registro](setup-local-development-environment.md#docker-microservices).

## Configurar a ação de envio personalizada e o serviço em nuvem para o DocuSign {#deploy-custom-submit-action}

O AEM Forms as a Cloud Service fornece uma ação de envio personalizada para o DocuSign. A ação de envio ajuda a enviar os formulários adaptáveis para assinaturas eletrônicas usando as APIs do DocuSign. O código para ação de envio personalizada está disponível em [repositório Git público de amostras do AEM Forms](https://github.com/adobe/aem-forms-docusign-sample). Você pode implantar o código da maneira que ele está no ambiente do AEM Forms ou personalizá-lo de acordo com os requisitos da sua organização.

Execute as seguintes etapas para configurar a ação de envio personalizada pronta para uso e o DocuSign Cloud Service:

1. [Clonar seu projeto do AEM Forms as a Cloud Service](setup-local-development-environment.md#forms-cloud-service-local-development-environment) ou criar um [!DNL Experience Manager Forms] como um projeto [!DNL Cloud Service] com base no [Arquétipo AEM 27](https://github.com/adobe/aem-project-archetype) ou posterior. Para criar um projeto [!DNL Experience Manager Forms] as a [!DNL Cloud Service] com base no Arquétipo AEM:
   </br> Abra o prompt de comando e execute o comando abaixo para criar um projeto do as a Cloud Service [!DNL Experience Manager Forms]:

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Além disso, altere `appTitle`, `appId` e `groupId` no comando acima para refletir seu ambiente.

1. Clonar o repositório [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample). Esse repositório contém ações de envio personalizadas para o DocuSign e detalhes de configuração para se conectar com o servidor DocuSign.

1. Abra o projeto AEM Forms as a Cloud Service criado na Etapa 1 para edição no IDE de sua escolha.

1. Abra o arquivo `[AEM Forms as a Cloud Service project]\pom.xml` para edição e faça as seguintes alterações:

   1. Adicionar o seguinte texto ao final da marca `<properties>`:

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. Adicionar o seguinte texto ao final da marca `<repositories>`:

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      Se não houver uma marca `<repositories>`, crie a marca abaixo da marca `<properties>`.

   1. Adicionar o seguinte texto ao final da marca `<dependencyManagement>`:

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. Execute as seguintes etapas no arquivo `all/pom.xml` disponível na pasta do projeto Cloud Service:

   1. Adicionar o seguinte texto ao final da marca `<embeddeds>`:

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. Adicionar o seguinte texto ao final da marca `<dependencies>`:

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. Abra o prompt de comando e navegue até `aem-forms-samples\forms-integration-docusign` (clonado na etapa 3) e execute o seguinte comando:

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` refere-se ao nome da pasta criada na etapa 1 deste procedimento.

1. Implante o projeto no ambiente de desenvolvimento local. Você pode usar o comando a seguir para implantar no ambiente de desenvolvimento local

   `mvn -PautoInstallPackage clean install`

   Após executar essas etapas, você poderá exibir uma nova ação de envio personalizada [Enviar com assinaturas eletrônicas do DocuSign](#enabledocusign), disponível na lista de opções de envio para um formulário adaptável e uma [configuração do serviço de nuvem do DocuSign](#configure-docusign-with-aem-forms) em seu ambiente de desenvolvimento local.

1. Compile e [Implante o código em seu [!DNL AEM Forms] ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Integrar [!DNL DocuSign] a [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

Depois que os pré-requisitos estiverem em vigor, execute as seguintes etapas para integrar [!DNL DocuSign] a [!DNL AEM Forms] nas instâncias do Autor.

1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL DocuSign]** e selecione uma pasta para hospedar a configuração.

1. Na página de configurações, selecione **[!UICONTROL Criar]** para criar a configuração [!DNL DocuSign] no AEM Forms.
1. Na guia **[!UICONTROL Geral]** da página **[!UICONTROL Criar configuração do DocuSign]**, especifique um **[!UICONTROL Nome]** para a configuração e selecione **[!UICONTROL Avançar]**. Você pode especificar um **[!UICONTROL Título]**.

1. Copie o URL na janela atual do navegador para um bloco de notas. A URL é necessária para configurar o aplicativo [!DNL DocuSign] com [!DNL AEM Forms] em uma etapa posterior.

1. Defina as configurações de OAuth para o aplicativo [!DNL DocuSign]:

   1. Abra uma janela de navegador e entre na sua [!DNL DocuSign] [conta de desenvolvedor](https://admindemo.docusign.com/apps-and-keys).
   1. Abra o aplicativo configurado para [!DNL AEM Forms].
   1. Na caixa **[!UICONTROL Redirecionar URI]**, adicione a URL copiada na etapa anterior e clique em **[!UICONTROL Salvar]**.
   1. Anote as chaves de integração e segredo.

   Para obter informações passo a passo sobre como definir as configurações OAuth para um aplicativo [!DNL DocuSign] e obter as chaves, consulte [Definir configurações oAuth para a documentação do desenvolvedor do aplicativo](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys).

1. Volte para a página **[!UICONTROL Criar configuração do DocuSign]**. Na guia **[!UICONTROL Configurações]**, o campo **[!UICONTROL URL do OAuth]** menciona a seguinte URL padrão:

   `https://account-d.docusign.com/oauth/auth`

1. Especifique a **[!UICONTROL ID do Cliente]** (Chave de Integração DocuSign) e o **[!UICONTROL Segredo do Cliente]** (Chave Secreta DocuSign).

1. Selecione **[!UICONTROL Conectar ao DocuSign]**. Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar o aplicativo [!DNL DocuSign]. Quando solicitado a confirmar o acesso para `your developer account`, clique em **[!UICONTROL Permitir Acesso]**. Se as credenciais estiverem corretas, uma mensagem de sucesso será exibida.

1. Selecione **[!UICONTROL Criar]** para criar a configuração [!DNL DocuSign].

1. Selecione a configuração e clique em **[!UICONTROL Publicar]**, selecione a configuração e clique em **[!UICONTROL Publicar]**. Ele replica a configuração nos ambientes de publicação correspondentes.

1. Repita todas as etapas acima nas instâncias de desenvolvedor, preparo e produção (qualquer uma que tenha restado) para concluir a configuração do [!DNL DocuSign] com [!DNL AEM Forms] para o seu ambiente.

Agora, seu ambiente do AEM Forms está configurado para usar o DocuSign. Adicione o contêiner de configuração usado para o Cloud Service a toda a Forms adaptável que está sendo habilitada para [!DNL DocuSign]. Você pode especificar um contêiner de configuração nas propriedades de um Formulário adaptável.

### Usar [!DNL DocuSign] em um formulário adaptável {#enabledocusign}

Você pode habilitar [!DNL DocuSign] para um Formulário adaptável existente ou criar um Formulário adaptável habilitado para [!DNL DocuSign]. Escolha uma das seguintes opções:

- [Criar um Formulário adaptável  [!DNL DocuSign] habilitado](#create-an-adaptive-form-for-docusign)
- [Habilitar [!DNL DocuSign] para um Formulário Adaptável existente](#editafsign).

#### Criar um formulário adaptável para o DocuSign {#create-an-adaptive-form-for-docusign}

Para criar um Formulário adaptável habilitado para assinatura:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione **[!UICONTROL Criar]** e selecione **[!UICONTROL Formulário adaptável]**. Uma lista de modelos é exibida. Selecione um modelo e selecione **[!UICONTROL Próximo]**.
1. Na guia **[!UICONTROL Básico]**:

   1. Especifique o **[!UICONTROL Nome]** e o **[!UICONTROL Título]** para o Formulário adaptável.

   1. Selecione o [contêiner de configuração](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) criado durante a [integração [!DNL DocuSign] com [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

   O contêiner de configuração contém os Serviços de Nuvem do [!DNL DocuSign] configurados para o seu ambiente. Esses serviços estão disponíveis para seleção no Criador de formulários adaptáveis.

1. Na guia **[!UICONTROL Modelo de Formulário]**, selecione uma das seguintes opções:

   - Se você tiver um modelo de formulário personalizado e precisar de um Documento de registro com base no modelo de formulário, selecione a opção **[!UICONTROL Associar modelo de formulário como Documento de modelo de Registro]** e selecione um Documento de modelo de Registro. Quando você usa a opção, os documentos enviados para assinatura exibem apenas os campos que são baseados no modelo de formulário associado. Ele não exibe todos os campos do Formulário adaptável.

   - Se você não tiver um modelo de formulário personalizado, selecione a opção **[!UICONTROL Gerar documento de registro]**. Quando você usa a opção, o documento enviado para assinatura exibe todos os campos do Formulário adaptável.

1. Selecione **[!UICONTROL Criar]**. Um Formulário adaptável habilitado para assinatura é criado. Você pode adicionar os campos do [!DNL DocuSign] ao formulário e enviá-lo para assinatura.
1. Abra o formulário adaptável no modo de edição. Na guia **[!UICONTROL Conteúdo]**, selecione o **[!UICONTROL Contêiner de Formulário]** e selecione ![Configurar](assets/configure-icon.svg).

1. Na seção **[!UICONTROL Envio]**, selecione **[!UICONTROL Enviar com assinaturas eletrônicas DocuSign]** na lista suspensa **[!UICONTROL Ação de Envio]**.

1. Na seção **[!UICONTROL Configuração de ação]**, selecione **[!UICONTROL Adicionar]** para adicionar um destinatário e especificar o endereço de email dele. Selecione **[!UICONTROL Adicionar]** novamente para adicionar mais destinatários.

1. Especifique o assunto da mensagem de email no campo **[!UICONTROL Assunto do Email]**. Selecione **Incluir anexos** para incluir anexos na mensagem de email.

1. Selecione ![Salvar](assets/save_icon.svg) para salvar as propriedades.

#### Habilitar [!DNL DocuSign] para um Formulário adaptável {#editafsign}

Para usar [!DNL DocuSign] em um Formulário adaptável existente:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione o Formulário adaptável e selecione **[!UICONTROL Propriedades]**.
1. Na guia **[!UICONTROL Básico]**, selecione o [contêiner de configuração](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) criado ao integrar [!DNL DocuSign] a [!DNL AEM Forms].
1. Na guia **[!UICONTROL Modelo de Formulário]**, selecione uma das seguintes opções:

   - Se você tiver um modelo de formulário personalizado e precisar de um Documento de registro com base no modelo de formulário, selecione a opção **[!UICONTROL Associar modelo de formulário como Documento de modelo de Registro]** e selecione um Documento de modelo de Registro. Quando você usa a opção, os documentos enviados para assinatura exibem apenas os campos que são baseados no modelo de formulário associado. Ele não exibe todos os campos do Formulário adaptável.

   - Se você não tiver um modelo de formulário personalizado, selecione a opção **[!UICONTROL Gerar documento de registro]**. Quando você usa a opção, o documento enviado para assinatura exibe todos os campos do Formulário adaptável.

1. Selecione **[!UICONTROL Salvar e fechar]**. O Formulário adaptável está habilitado para [!DNL DocuSign]. Agora, você pode adicionar os campos do [!DNL DocuSign] ao formulário e enviá-lo para assinatura.

1. Abra o formulário adaptável no modo de edição. Na guia **[!UICONTROL Conteúdo]**, selecione o **[!UICONTROL Contêiner de Formulário]** e selecione ![Configurar](assets/configure-icon.svg).

1. Na seção **[!UICONTROL Envio]**, selecione **[!UICONTROL Enviar com assinaturas eletrônicas DocuSign]** na lista suspensa **[!UICONTROL Ação de Envio]**.

1. Na seção **[!UICONTROL Configuração de ação]**, selecione **[!UICONTROL Adicionar]** para adicionar um destinatário e especificar o endereço de email dele. Selecione **[!UICONTROL Adicionar]** novamente para adicionar mais destinatários.

1. Especifique o assunto da mensagem de email no campo **[!UICONTROL Assunto do Email]**. Selecione **Incluir anexos** para incluir anexos na mensagem de email.

1. Selecione ![Salvar](assets/save_icon.svg) para salvar as propriedades.
