---
title: Selecione dinamicamente um usuário ou grupo para etapas de fluxo de trabalho centradas no AEM Forms
seo-title: Dynamically select a user or group for AEM Forms-centric workflow steps
description: 'Saiba como selecionar um usuário ou grupo para um [!DNL AEM Forms] no tempo de execução. '
seo-description: Learn how to select a user or group for an [!DNL AEM Forms] workflow at the runtime.
uuid: 19dcbda4-61af-40b3-b10b-68a341373410
content-type: troubleshooting
topic-tags: publish
discoiquuid: e6c9f3bb-8f20-4889-86f4-d30578fb1c51
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 1%

---


# Selecione dinamicamente um usuário ou grupo para etapas de fluxo de trabalho centradas no AEM Forms {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

Saiba como selecionar um usuário ou grupo para um [!DNL AEM Forms] no tempo de execução.

Em grandes organizações, há requisitos para selecionar dinamicamente usuários para um processo. Por exemplo, selecionar um agente de campo para servir um cliente com base na proximidade do agente com o cliente. Nesse cenário, o agente é selecionado dinamicamente.

Atribuir tarefa e [!DNL Adobe Sign] etapas [Fluxos de trabalho centrados na Forms no OSGi](aem-forms-workflow.md) fornecer opções para selecionar dinamicamente um usuário. Você pode usar pacotes ECMAScript ou OSGi para selecionar dinamicamente um destinatário para a etapa Atribuir tarefa ou para selecionar signatários para a etapa Assinar documento.

## Use o ECMAScript para selecionar dinamicamente um usuário ou grupo {#use-ecmascript-to-dynamically-select-a-user-or-group}

O ECMAScript é uma linguagem de script. Ele é usado para aplicativos de servidor e scripts do lado do cliente. Execute as seguintes etapas para selecionar dinamicamente um usuário ou grupo usando o ECMAScript:

1. Abra o CRXDE Lite. O URL é `https://'[server]:[port]'/crx/de/index.jsp`
1. Crie um arquivo com a extensão .ecma no seguinte caminho. Se o caminho (estrutura do nó) não existir, crie-o:

   * (Etapa Caminho para atribuição de tarefa) `/apps/fd/dashboard/scripts/participantChooser`
   * (Etapa Caminho para assinatura) `/apps/fd/workflow/scripts/adobesign`

1. Adicione o ECMAScript, que tem a lógica de selecionar dinamicamente um usuário, ao arquivo .ecma. Clique em **[!UICONTROL Salvar tudo]**.

   Para obter exemplos de scripts, consulte [Exemplos de ECMAScripts para selecionar dinamicamente um usuário ou grupo](dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group).

1. Adicione o nome de exibição do script. Esse nome é exibido nas etapas do fluxo de trabalho. Para especificar o nome:

   1. Expanda o nó do script, clique com o botão direito do mouse no nó **[!UICONTROL jcr:content]** e clique em **[!UICONTROL Misturas]**.
   1. Adicione o `mix:title` na caixa de diálogo Editar misturas e clique em **OK**.
   1. Adicione a seguinte propriedade ao nó jcr:content do script:

      | Nome | Tipo | Valor |
      |--- |--- |--- |
      | jcr:title | Sequência de caracteres | Especifique o nome do script. Por exemplo, escolha o agente de campo mais próximo. Esse nome é exibido nas etapas Atribuir tarefa e Assinar documento . |

   1. Clique em **Salvar tudo**. O script fica disponível para seleção nos componentes AEM fluxo de trabalho.

      ![script](assets/script.png)

### Exemplos de ECMAScripts para escolher dinamicamente um usuário ou grupo {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

A amostra de ECMAScript a seguir seleciona dinamicamente um destinatário para a etapa Atribuir tarefa . Neste script, um usuário é selecionado com base no caminho da carga útil. Antes de usar esse script, verifique se todos os usuários mencionados no script existem no AEM. Se os usuários mencionados no script não existirem no AEM, o processo relacionado poderá falhar.

```javascript
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

A amostra de ECMAScript a seguir seleciona dinamicamente um destinatário para a [!DNL Adobe Sign] etapa. Antes de usar o script abaixo, verifique se as informações do usuário (endereços de email e números de telefone) mencionadas no script estão corretas. Se as informações do usuário mencionadas no script estiverem incorretas, o processo relacionado poderá falhar.

>[!NOTE]
>
>Ao usar o ECMAScript para [!DNL Adobe Sign], o script deve estar localizado em crx-repository em /apps/fd/workflow/scripts/adobesign/, e deve ter uma função chamada getAdobeSignRecipients para retornar uma lista dos usuários.

```javascript
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## Usar interface Java para escolher dinamicamente um usuário ou grupo {#use-java-interface-to-dynamically-choose-a-user-or-group}

Você pode usar o [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Interface Java para escolher dinamicamente um usuário ou grupo para [!DNL Adobe Sign] e Atribuir etapas da tarefa. Você pode criar um pacote OSGi que usou o [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Interface Java e implante-a na [!DNL AEM Forms] servidor. Disponibiliza a opção para seleção em Atribuir tarefa e [!DNL Adobe Sign] componentes do Fluxo de trabalho AEM.

Você precisa [[!DNL AEM Forms] SDK do cliente](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) jar e [jarro de granito](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) arquivos para compilar a amostra de código listada abaixo. Adicione esses arquivos jar como dependências externas ao projeto do pacote OSGi. Você pode usar qualquer Java IDE para criar um pacote OSGi. O procedimento a seguir fornece etapas para usar o Eclipse para criar um pacote OSGi:

1. Abra o Eclipse IDE. Navegar para **[!UICONTROL Arquivo]**> **[!UICONTROL Novo projeto]**.
1. Na tela Selecionar um assistente , selecione **[!UICONTROL Projeto Maven]** e clique em **[!UICONTROL Próximo]**.
1. No projeto Novo Maven, mantenha os padrões e clique em **[!UICONTROL Próximo]**. Selecione um arquétipo e clique em **[!UICONTROL Próximo]**. Por exemplo, maven-archetype-quickstart. Especificar **[!UICONTROL ID do Grupo]**, **[!UICONTROL Id Do Artefato]**, **[!UICONTROL version]** e **[!UICONTROL pacote]** para o projeto e clique em **[!UICONTROL Concluir]**. O projeto é criado.
1. Abra o arquivo pom.xml para edição e substitua todo o conteúdo do arquivo pelo seguinte:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk</artifactId>
               <version>6.0.138</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. Adicionar código-fonte que usa [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Interface Java para escolher dinamicamente um usuário ou grupo para a etapa Atribuir tarefa . Para obter o código de amostra, consulte [Exemplo para escolher dinamicamente um usuário ou grupo usando a interface Java](#-sample-scripts-for).
1. Abra um prompt de comando e navegue até o diretório que contém o projeto do pacote OSGi. Use o seguinte comando para criar o pacote OSGi:

   `mvn clean install`

1. Fazer upload do pacote para um [!DNL AEM Forms] servidor. Você pode usar o Gerenciador de pacotes de AEM para importar o pacote para [!DNL AEM Forms] servidor.

Depois que o pacote é importado, a opção para escolher a interface Java para selecionar dinamicamente um usuário ou um grupo fica disponível nas etapas de Adobe Sign e Atribuir tarefa.

### Exemplo de código Java para escolher dinamicamente um usuário ou grupo {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

O código de amostra a seguir escolhe dinamicamente um destinatário para a etapa do Adobe Sign. Você usa o código em um pacote OSGi. Antes de usar o código listado abaixo, verifique se as informações do usuário (endereços de email e números de telefone) mencionadas no código estão corretas. Se as informações do usuário mencionadas no código estiverem incorretas, o processo relacionado poderá falhar.

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```

