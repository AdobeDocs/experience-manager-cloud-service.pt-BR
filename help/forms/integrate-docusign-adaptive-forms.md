---
title: Como integrar o DocuSign a um Formulário adaptável?
description: Saiba como usar o DocuSign com um formulário adaptável para coletar assinaturas eletrônicas.
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
source-git-commit: 92f89243b79c6c2377db3ca2b8ea244957416626
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 1%

---

# Uso do DocuSign com um formulário adaptável {#integrate-aem-forms-with-DocuSign}

O DocuSign é uma solução de assinatura eletrônica proeminente. Você pode usá-lo para assinar um contrato eletronicamente. É possível integrar o DocuSign a um formulário adaptável. Ele ajuda a enviar um formulário adaptável para assinaturas eletrônicas para vários recipients. O uso de assinaturas eletrônicas ajuda a:

- Feche negócios de qualquer dispositivo com processos totalmente automatizados de propostas, cotações e contratos.
- Conclua os processos de Recursos humanos com mais rapidez e ofereça aos seus funcionários as experiências digitais.
- Reduza os tempos de ciclo do contrato e integre seus fornecedores mais rapidamente.

O AEM Forms as a Cloud Service fornece uma [ação de envio personalizada para o DocuSign](#deploy-custom-submit-action). A ação de envio ajuda a enviar os formulários adaptáveis para assinaturas eletrônicas usando as APIs do DocuSign.

| Você também pode usar a solução de assinatura eletrônica do Adobe, Adobe Sign, para assinar eletronicamente um formulário adaptável. O AEM Forms tem uma integração muito mais profunda com o Adobe Sign e fornece controles muito mais finos, como assinatura sequencial e paralela, vários métodos de autenticação, experiência de assinatura no formulário e muito mais. Para obter mais informações, consulte [Uso do Adobe Sign em um formulário adaptável](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Pré-requisitos {#prerequisites}

Os itens a seguir são necessários para integrar o DocuSign ao AEM Forms:

- Um DocuSign [conta do desenvolvedor](https://developers.docusign.com/platform/account/)
- Um aplicativo DocuSign
- Credenciais (ID do cliente e Segredo do cliente) do aplicativo da API DocuSign.
- [Ação de envio personalizada e serviço em nuvem para o DocuSign](https://github.com/adobe/aem-forms-docusign-sample)
- (Somente para ambiente de desenvolvimento local) [Configurar documento de registro](setup-local-development-environment.md#docker-microservices).

## Configurar a ação de envio personalizada e o serviço em nuvem para o DocuSign {#deploy-custom-submit-action}

O AEM Forms as a Cloud Service fornece uma ação de envio personalizada para o DocuSign. A ação de envio ajuda a enviar os formulários adaptáveis para assinaturas eletrônicas usando as APIs do DocuSign. O código para ação de envio personalizada está disponível em [Repositório Git público de amostras do AEM Forms](https://github.com/adobe/aem-forms-docusign-sample). Você pode implantar o código da maneira que ele está no ambiente do AEM Forms ou personalizá-lo de acordo com os requisitos da sua organização.

Execute as seguintes etapas para configurar a ação de envio personalizada pronta para uso e o Cloud Service do DocuSign:

1. [Clonar o projeto do AEM Forms as a Cloud Service](setup-local-development-environment.md#forms-cloud-service-local-development-environment) ou criar um [!DNL Experience Manager Forms] as a [!DNL Cloud Service] projeto baseado em [Arquétipo AEM 27](https://github.com/adobe/aem-project-archetype) ou posteriormente. Para criar uma [!DNL Experience Manager Forms] as a [!DNL Cloud Service] projeto baseado no Arquétipo AEM:
   </br> Abra o prompt de comando e execute o comando abaixo para criar uma [!DNL Experience Manager Forms] as a Cloud Service projeto:

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Além disso, altere `appTitle`, `appId`, e `groupId`, no comando acima para refletir o ambiente.

1. Clonar o [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample) repositório. Esse repositório contém ações de envio personalizadas para o DocuSign e detalhes de configuração para se conectar com o servidor DocuSign.

1. Abra o projeto AEM Forms as a Cloud Service criado na Etapa 1 para edição no IDE de sua escolha.

1. Abra o `[AEM Forms as a Cloud Service project]\pom.xml` arquivo para edição e faça as seguintes alterações:

   1. Adicione o seguinte texto no final da `<properties>` tag:

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. Adicione o seguinte texto no final da `<repositories>` tag:

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      Se não houver `<repositories>` , crie a tag abaixo do `<properties>` tag.

   1. Adicione o seguinte texto no final da `<dependencyManagement>` tag:

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. Execute as seguintes etapas no `all/pom.xml` arquivo disponível na pasta do projeto Cloud Service:

   1. Adicione o seguinte texto no final da `<embeddeds>` tag:

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. Adicione o seguinte texto no final da `<dependencies>` tag:

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

   Depois de executar essas etapas, você pode visualizar uma nova ação de envio personalizada [Enviar com assinaturas eletrônicas do DocuSign](#enabledocusign) disponíveis na lista de opções de envio para um formulário adaptável e uma [Configuração do serviço de nuvem DocuSign](#configure-docusign-with-aem-forms) no ambiente de desenvolvimento local.

1. Compilar e [Implante o código no seu [!DNL AEM Forms] ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Integrar [!DNL DocuSign] com [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

Depois que os pré-requisitos estiverem em vigor, execute as seguintes etapas para integrar [!DNL DocuSign] com [!DNL AEM Forms] nas instâncias do Autor.

1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL DocuSign]** e selecione uma pasta para hospedar a configuração.

1. Na página de configurações, toque em **[!UICONTROL Criar]** para criar [!DNL DocuSign] configuração no AEM Forms.
1. No **[!UICONTROL Geral]** guia do **[!UICONTROL Criar configuração do DocuSign]** página, especifique um **[!UICONTROL Nome]** para a configuração e toque em **[!UICONTROL Próxima]**. Opcionalmente, é possível especificar um **[!UICONTROL Título]**.

1. Copie o URL na janela atual do navegador para um bloco de notas. O URL é necessário para configurar o [!DNL DocuSign] aplicativo com [!DNL AEM Forms] em uma etapa posterior.

1. Defina as configurações de OAuth para o [!DNL DocuSign] aplicativo:

   1. Abra uma janela do navegador e faça logon no [!DNL DocuSign] [conta do desenvolvedor](https://admindemo.docusign.com/apps-and-keys).
   1. Abra o aplicativo configurado para [!DNL AEM Forms].
   1. No **[!UICONTROL URI de redirecionamento]** adicione o URL copiado na etapa anterior e clique em **[!UICONTROL Salvar]**.
   1. Anote as chaves de integração e segredo.

   Para obter informações passo a passo sobre como definir as configurações de OAuth para um [!DNL DocuSign] e obter as chaves, consulte [Definir configurações de oAuth para o aplicativo](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys) documentação do desenvolvedor.

1. Volte para o **[!UICONTROL Criar configuração do DocuSign]** página. No **[!UICONTROL Configurações]** , a guia **[!UICONTROL URL do OAuth]** menciona o seguinte URL padrão:

   `https://account-d.docusign.com/oauth/auth`

1. Especifique a **[!UICONTROL ID do cliente]** (Chave de integração do DocuSign) e **[!UICONTROL Segredo do cliente]** (Chave secreta do DocuSign).

1. Toque **[!UICONTROL Conectar-se ao DocuSign]**. Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar [!DNL DocuSign] aplicação. Quando for solicitado que você confirme o acesso de `your developer account`, clique em **[!UICONTROL Permitir acesso]**. Se as credenciais estiverem corretas, uma mensagem de sucesso será exibida.

1. Toque **[!UICONTROL Criar]** para criar o [!DNL DocuSign] configuração.

1. Selecione a configuração e clique em **[!UICONTROL Publish]**, selecione a configuração e clique em **[!UICONTROL Publish]**. Ele replica a configuração nos ambientes de publicação correspondentes.

1. Repita todas as etapas acima nas instâncias de desenvolvedor, preparo e produção (qualquer uma que tenha restado) para concluir a configuração [!DNL DocuSign] com [!DNL AEM Forms] para o seu ambiente.

Agora, seu ambiente do AEM Forms está configurado para usar o DocuSign. Adicione o contêiner de configuração usado para o Cloud Service a todo o Forms adaptável que está sendo habilitado para [!DNL DocuSign]. Você pode especificar um contêiner de configuração nas propriedades de um Formulário adaptável.

### Uso [!DNL DocuSign] em um Formulário adaptável {#enabledocusign}

Você pode ativar [!DNL DocuSign] para um Formulário adaptável existente ou criar um [!DNL DocuSign] Formulário adaptável ativado. Escolha uma das seguintes opções:

- [Criar um [!DNL DocuSign] Formulário adaptável ativado](#create-an-adaptive-form-for-docusign)
- [Ativar [!DNL DocuSign] por um formulário adaptável existente](#editafsign).

#### Criar um formulário adaptável para o DocuSign {#create-an-adaptive-form-for-docusign}

Para criar um Formulário adaptável habilitado para assinatura:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Toque **[!UICONTROL Criar]** e selecione **[!UICONTROL Formulário adaptável]**. Uma lista de modelos é exibida. Selecione um modelo e toque em **[!UICONTROL Próxima]**.
1. No **[!UICONTROL Básico]** guia:

   1. Especifique a **[!UICONTROL Nome]** e **[!UICONTROL Título]** para o Formulário adaptável.

   1. Selecione o [contêiner de configuração](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) criado enquanto [integração [!DNL DocuSign] com [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

   O contêiner de configuração contém o [!DNL DocuSign] Cloud Service configurado para o seu ambiente. Esses serviços estão disponíveis para seleção no editor de Formulário adaptável.

1. No **[!UICONTROL Modelo de formulário]** selecione uma das seguintes opções:

   - Se você tiver um modelo de formulário personalizado e exigir um Documento de registro com base no modelo de formulário, selecione a **[!UICONTROL Associar o modelo de formulário como o documento de modelo de registro]** e selecione um modelo de Documento de registro. Quando você usa a opção, os documentos enviados para assinatura exibem apenas os campos que são baseados no modelo de formulário associado. Ele não exibe todos os campos do Formulário adaptável.

   - Se você não tiver um modelo de formulário personalizado, selecione o **[!UICONTROL Gerar documento de registro]** opção. Quando você usa a opção, o documento enviado para assinatura exibe todos os campos do Formulário adaptável.

1. Toque em **[!UICONTROL Criar.]** Um Formulário adaptável habilitado para assinatura é criado. Você pode adicionar seu [!DNL DocuSign] ao formulário e envie-o para assinatura.
1. Abra o formulário adaptável no modo de edição. No **[!UICONTROL Conteúdo]** toque na guia **[!UICONTROL Contêiner de formulário]** e toque em ![Configurar](assets/configure-icon.svg).

1. No **[!UICONTROL Envio]** , selecione **[!UICONTROL Enviar com assinaturas eletrônicas do DocuSign]** do **[!UICONTROL Ação de envio]** lista suspensa.

1. No **[!UICONTROL Configuração de ação]** seção, toque em **[!UICONTROL Adicionar]** para adicionar um recipient e especificar o endereço de email do recipient. Toque **[!UICONTROL Adicionar]** novamente para adicionar mais recipients.

1. Especifique o assunto da mensagem de email no campo **[!UICONTROL Assunto do email]** campo. Selecionar **Incluir anexos** para incluir anexos na mensagem de email.

1. Toque em ![Salvar](assets/save_icon.svg) para salvar as propriedades.

#### Ativar [!DNL DocuSign] para um Formulário adaptável {#editafsign}

Para usar [!DNL DocuSign] em um Formulário adaptável existente:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Selecione o Formulário adaptável e toque em **[!UICONTROL Propriedades]**.
1. No **[!UICONTROL Básico]** , selecione a [contêiner de configuração](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) criado durante a integração [!DNL DocuSign] com [!DNL AEM Forms].
1. No **[!UICONTROL Modelo de formulário]** selecione uma das seguintes opções:

   - Se você tiver um modelo de formulário personalizado e exigir um Documento de registro com base no modelo de formulário, selecione a **[!UICONTROL Associar o modelo de formulário como o documento de modelo de registro]** e selecione um modelo de Documento de registro. Quando você usa a opção, os documentos enviados para assinatura exibem apenas os campos que são baseados no modelo de formulário associado. Ele não exibe todos os campos do Formulário adaptável.

   - Se você não tiver um modelo de formulário personalizado, selecione o **[!UICONTROL Gerar documento de registro]** opção. Quando você usa a opção, o documento enviado para assinatura exibe todos os campos do Formulário adaptável.

1. Toque **[!UICONTROL Salvar e fechar]**. O formulário adaptável está ativado para [!DNL DocuSign]. Agora, você pode adicionar seu [!DNL DocuSign] ao formulário e envie-o para assinatura.

1. Abra o formulário adaptável no modo de edição. No **[!UICONTROL Conteúdo]** toque na guia **[!UICONTROL Contêiner de formulário]** e toque em ![Configurar](assets/configure-icon.svg).

1. No **[!UICONTROL Envio]** , selecione **[!UICONTROL Enviar com assinaturas eletrônicas do DocuSign]** do **[!UICONTROL Ação de envio]** lista suspensa.

1. No **[!UICONTROL Configuração de ação]** seção, toque em **[!UICONTROL Adicionar]** para adicionar um recipient e especificar o endereço de email do recipient. Toque **[!UICONTROL Adicionar]** novamente para adicionar mais recipients.

1. Especifique o assunto da mensagem de email no campo **[!UICONTROL Assunto do email]** campo. Selecionar **Incluir anexos** para incluir anexos na mensagem de email.

1. Toque em ![Salvar](assets/save_icon.svg) para salvar as propriedades.
