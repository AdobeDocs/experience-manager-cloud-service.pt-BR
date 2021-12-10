---
title: Integrar o DocuSign com um formulário adaptável
description: Saiba como usar o DocuSign com um formulário adaptável para coletar assinaturas eletrônicas.
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 0%

---

# Uso do DocuSign com um formulário adaptável {#integrate-aem-forms-with-DocuSign}

O DocuSign é uma solução proeminente de assinatura eletrônica. Você pode usá-lo para assinar um contrato por e-mail. É possível integrar o DocuSign com um formulário adaptável. Ajuda a enviar um formulário adaptável para assinaturas eletrônicas para vários destinatários. O uso de assinaturas eletrônicas ajuda a:

- Feche negócios de qualquer dispositivo com processos de proposta, cotação e contrato totalmente automatizados.
- Termine os processos de recurso humano mais rapidamente e dê aos seus funcionários as experiências digitais.
- Reduza mais rapidamente os tempos de ciclo do contrato e integre seus fornecedores.

O AEM Forms as a Cloud Service fornece uma [ação de envio personalizado para o DocuSign](#deploy-custom-submit-action). A ação de envio ajuda a enviar os formulários adaptáveis para assinaturas eletrônicas usando APIs do DocuSign.

| Você também pode usar a solução Adobe e-signature, Adobe Sign para assinar automaticamente um formulário adaptável. A AEM Forms tem uma integração muito mais profunda com o Adobe Sign e fornece controles muito mais refinados, como assinatura sequencial e paralela, vários métodos de autenticação, experiência de assinatura no formulário e muito mais. Para obter mais informações, consulte [Uso do Adobe Sign em um formulário adaptável](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Pré-requisitos {#prerequisites}

Os itens a seguir são necessários para integrar o DocuSign com o AEM Forms:

- Um DocuSign [conta do desenvolvedor](https://developers.docusign.com/platform/account/)
- Um aplicativo do DocuSign
- Credenciais (ID do cliente e Segredo do cliente) do aplicativo da API do DocuSign.
- [Ação de envio personalizado e Serviço na nuvem para o DocuSign](https://github.com/adobe/aem-forms-docusign-sample)
- (Apenas para o ambiente de desenvolvimento local) [Configurar documento de registro](setup-local-development-environment.md#docker-microservices).

## Configurar a ação de envio personalizada e o serviço em nuvem para o DocuSign {#deploy-custom-submit-action}

O AEM Forms as a Cloud Service fornece uma ação de envio personalizada para o DocuSign. A ação de envio ajuda a enviar os formulários adaptáveis para assinaturas eletrônicas usando APIs do DocuSign. O código para a ação de envio personalizado está disponível em [Repositório git público de amostras do AEM Forms](https://github.com/adobe/aem-forms-docusign-sample). Você pode implantar o código da forma como está no ambiente AEM Forms ou personalizá-lo de acordo com os requisitos de sua organização.

Execute as seguintes etapas para configurar a ação de envio personalizado e o Cloud Service do DocuSign prontos para uso:

1. [Clonar o projeto as a Cloud Service do AEM Forms](setup-local-development-environment.md#forms-cloud-service-local-development-environment) ou criar uma [!DNL Experience Manager Forms] como [!DNL Cloud Service] projeto baseado em [Arquétipo de AEM 27](https://github.com/adobe/aem-project-archetype) ou posterior. Para criar um [!DNL Experience Manager Forms] como [!DNL Cloud Service] projeto baseado no Arquétipo de AEM:
   </br> Abra o prompt de comando e execute o comando abaixo para criar um [!DNL Experience Manager Forms] Projeto as a Cloud Service:

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Além disso, altere `appTitle`, `appId`e `groupId`, no comando acima para refletir seu ambiente.

1. Clonar o [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample) repositório. Este repositório contém uma ação de envio personalizada para o DocuSign e detalhes de configuração para se conectar ao servidor do DocuSign.

1. Abra o projeto as a Cloud Service do AEM Forms criado na Etapa 1 para edição no IDE de sua escolha.

1. Abra o `[AEM Forms as a Cloud Service project]\pom.xml` para editar e fazer as seguintes alterações:

   1. Adicione o seguinte texto no final do `<properties>` tag:

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. Adicione o seguinte texto no final do `<repositories>` tag:

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      Se não houver `<repositories>` , crie a tag abaixo de `<properties>` .

   1. Adicione o seguinte texto no final do `<dependencyManagement>` tag:

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. Execute as seguintes etapas no `all/pom.xml` arquivo disponível na pasta Cloud Service project:

   1. Adicione o seguinte texto no final do `<embeddeds>` tag:

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. Adicione o seguinte texto no final do `<dependencies>` tag:

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

1. Implante o projeto no ambiente de desenvolvimento local. Você pode usar o seguinte comando para implantar em seu ambiente de desenvolvimento local

   `mvn -PautoInstallPackage clean install`

   Após executar essas etapas, é possível visualizar uma nova ação de envio personalizado [Enviar com assinaturas eletrônicas do DocuSign](#enabledocusign) disponível na lista de opções de envio para um formulário adaptável e um [Configuração do serviço em nuvem do DocuSign](#configure-docusign-with-aem-forms) no ambiente de desenvolvimento local.

1. Compilar e [Implante o código no [!DNL AEM Forms] Ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Integrar [!DNL DocuSign] com [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

Depois que os pré-requisitos estiverem em vigor, execute as seguintes etapas para integrar [!DNL DocuSign] com [!DNL AEM Forms] nas instâncias de Autor.

1. Navegar para **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL DocuSign]** e selecione uma pasta para hospedar a configuração.

1. Na página Configurações , toque em **[!UICONTROL Criar]** para criar [!DNL DocuSign] na AEM Forms.
1. No **[!UICONTROL Geral]** da guia **[!UICONTROL Criar configuração do DocuSign]** especifique um **[!UICONTROL Nome]** para a configuração, e toque em **[!UICONTROL Próximo]**. Como opção, você pode especificar uma **[!UICONTROL Título]**.

1. Copie o URL na janela atual do navegador para um bloco de notas. O URL é necessário para configurar [!DNL DocuSign] aplicativo com [!DNL AEM Forms] em uma etapa posterior.

1. Defina as configurações de OAuth para a variável [!DNL DocuSign] aplicativo:

   1. Abra uma janela do navegador e faça logon em sua [!DNL DocuSign] [conta do desenvolvedor](https://admindemo.docusign.com/apps-and-keys).
   1. Abra o aplicativo configurado para [!DNL AEM Forms].
   1. No **[!UICONTROL Redirecionar URI]** , adicione o URL copiado na etapa anterior e clique em **[!UICONTROL Salvar]**.
   1. Anote as Teclas de integração e segredo.

   Para obter informações passo a passo sobre a configuração do OAuth para um [!DNL DocuSign] e obtenha as chaves, consulte [Definir configurações de oAuth para o aplicativo](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys) documentação do desenvolvedor.

1. Volte para o **[!UICONTROL Criar configuração do DocuSign]** página. No **[!UICONTROL Configurações]** , a variável **[!UICONTROL URL de OAuth]** menciona o seguinte URL padrão:

   `https://account-d.docusign.com/oauth/auth`

1. Especifique a **[!UICONTROL ID do cliente]** (Chave de integração do DocuSign) e **[!UICONTROL Segredo do cliente]** (Chave Secreta DocuSign).

1. Toque **[!UICONTROL Conecte-se ao DocuSign]**. Quando solicitado a fornecer credenciais, forneça o nome de usuário e a senha da conta usada ao criar [!DNL DocuSign] aplicativo. Quando solicitado a confirmar o acesso para `your developer account`, clique em **[!UICONTROL Permitir acesso]**. Se as credenciais estiverem corretas, uma mensagem de sucesso será exibida.

1. Toque **[!UICONTROL Criar]** para criar o [!DNL DocuSign] configuração.

1. Selecione a configuração e clique em **[!UICONTROL Publicar]**, selecione a configuração e clique em **[!UICONTROL Publicar]**. Ele replica a configuração em ambientes de publicação correspondentes.

1. Repita todas as etapas acima nas instâncias de desenvolvedor, estágio e produção (o que restar) para concluir a configuração [!DNL DocuSign] com [!DNL AEM Forms] para seu ambiente.

Agora, seu ambiente AEM Forms está configurado para usar o DocuSign. Certifique-se de adicionar o contêiner de configuração usado para o Cloud Service a todo o Adaptive Forms que está sendo ativado para [!DNL DocuSign]. É possível especificar um contêiner de configuração a partir das propriedades de um formulário adaptável.

### Use [!DNL DocuSign] em um formulário adaptável {#enabledocusign}

Você pode ativar [!DNL DocuSign] para um formulário adaptável existente ou criar um [!DNL DocuSign] formulário adaptável habilitado. Escolha uma das opções a seguir:

- [Crie um [!DNL DocuSign] formulário adaptável ativado](#create-an-adaptive-form-for-docusign)
- [Habilitar [!DNL DocuSign] para um formulário adaptável existente](#editafsign).

#### Criar um formulário adaptável para o DocuSign {#create-an-adaptive-form-for-docusign}

Para criar um formulário adaptável habilitado para assinatura:

1. Navegar para **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Toque **[!UICONTROL Criar]** e selecione **[!UICONTROL Formulário adaptável]**. Uma lista de modelos é exibida. Selecione um modelo e toque em **[!UICONTROL Próximo]**.
1. No **[!UICONTROL Básico]** guia :

   1. Especifique a **[!UICONTROL Nome]** e **[!UICONTROL Título]** para o formulário adaptável.

   1. Selecione o [contêiner de configuração](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) criado ao [integração [!DNL DocuSign] com [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
   O contêiner de configuração contém a variável [!DNL DocuSign] Cloud Services configurados para o seu ambiente. Esses serviços estão disponíveis para seleção no editor de formulário adaptável.

1. No **[!UICONTROL Modelo de formulário]** selecione uma das seguintes opções:

   - Se você tiver um modelo de formulário personalizado e exigir um Documento de registro com base no modelo de formulário, selecione o **[!UICONTROL Associar modelo de formulário como o modelo Documento de registro]** e selecione um modelo Document of Record . Ao usar a opção , os documentos enviados para assinatura exibem apenas os campos que se baseiam no modelo de formulário associado. Não exibe todos os campos do Formulário adaptável.

   - Se não tiver um modelo de formulário personalizado, selecione **[!UICONTROL Gerar Documento de Registro]** opção. Quando você usa a opção , o documento enviado para assinatura exibe todos os campos do Formulário adaptável.

1. Toque **[!UICONTROL Criar.]** É criado um formulário adaptável habilitado para assinatura. Você pode adicionar [!DNL DocuSign] campos para o formulário e enviá-lo para assinatura.
1. Abra o formulário adaptável no modo de edição. No **[!UICONTROL Conteúdo]** toque na guia **[!UICONTROL Contêiner de formulário]** e tocar ![Configurar](assets/configure-icon.svg).

1. No **[!UICONTROL Submissão]** seção , selecione **[!UICONTROL Enviar com assinaturas eletrônicas do DocuSign]** do **[!UICONTROL Enviar ação]** lista suspensa.

1. No **[!UICONTROL Configuração de ação]** seção, toque em **[!UICONTROL Adicionar]** para adicionar um recipient e especificar o endereço de email do recipient. Toque **[!UICONTROL Adicionar]** novamente para adicionar mais recipients.

1. Especifique o assunto da mensagem de email no **[!UICONTROL Assunto do email]** campo. Selecionar **Incluir anexos** para incluir anexos na mensagem de email.

1. Toque ![Salvar](assets/save_icon.svg) para salvar as propriedades.

#### Habilitar [!DNL DocuSign] para um formulário adaptável {#editafsign}

Para usar [!DNL DocuSign] em um formulário adaptável existente:

1. Navegar para **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Selecione o formulário adaptável e toque em **[!UICONTROL Propriedades]**.
1. No **[!UICONTROL Básico]** selecione a guia [contêiner de configuração](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) criado ao integrar [!DNL DocuSign] com [!DNL AEM Forms].
1. No **[!UICONTROL Modelo de formulário]** selecione uma das seguintes opções:

   - Se você tiver um modelo de formulário personalizado e exigir um Documento de registro com base no modelo de formulário, selecione o **[!UICONTROL Associar modelo de formulário como o modelo Documento de registro]** e selecione um modelo Document of Record . Ao usar a opção , os documentos enviados para assinatura exibem apenas os campos que se baseiam no modelo de formulário associado. Não exibe todos os campos do Formulário adaptável.

   - Se não tiver um modelo de formulário personalizado, selecione **[!UICONTROL Gerar Documento de Registro]** opção. Quando você usa a opção , o documento enviado para assinatura exibe todos os campos do Formulário adaptável.

1. Toque **[!UICONTROL Salvar e fechar]**. O formulário adaptável está ativado para [!DNL DocuSign]. Agora, você pode adicionar seu [!DNL DocuSign] campos para o formulário e enviá-lo para assinatura.

1. Abra o formulário adaptável no modo de edição. No **[!UICONTROL Conteúdo]** toque na guia **[!UICONTROL Contêiner de formulário]** e tocar ![Configurar](assets/configure-icon.svg).

1. No **[!UICONTROL Submissão]** seção , selecione **[!UICONTROL Enviar com assinaturas eletrônicas do DocuSign]** do **[!UICONTROL Enviar ação]** lista suspensa.

1. No **[!UICONTROL Configuração de ação]** seção, toque em **[!UICONTROL Adicionar]** para adicionar um recipient e especificar o endereço de email do recipient. Toque **[!UICONTROL Adicionar]** novamente para adicionar mais recipients.

1. Especifique o assunto da mensagem de email no **[!UICONTROL Assunto do email]** campo. Selecionar **Incluir anexos** para incluir anexos na mensagem de email.

1. Toque ![Salvar](assets/save_icon.svg) para salvar as propriedades.
