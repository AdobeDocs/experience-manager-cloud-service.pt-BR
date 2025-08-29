---
title: Como criar uma ação enviar personalizada para um formulário adaptável com base nos componentes principais?
description: Saiba como criar uma Ação de envio personalizada para um Forms adaptável processar dados antes de enviá-los usando a ação de envio personalizada.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Intermediate
exl-id: a369b585-d148-4b5a-8afe-d5673ea865d0
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 1%

---

# Criar uma ação de envio personalizada para o Forms adaptável (Componentes principais)

Uma ação de envio permite que os usuários selecionem o destino dos dados capturados de um formulário e definam funcionalidades adicionais a serem executadas no envio do formulário. O formulário do AEM oferece suporte a várias [ações de envio prontas (OOTB)](/help/forms/configure-submit-actions-core-components.md), como enviar um email ou salvar dados no SharePoint ou OneDrive.

Você também pode criar uma ação de envio personalizada para adicionar funcionalidades não incluídas nas [opções predefinidas](/help/forms/configure-submit-actions-core-components.md#select-and-configure-a-submit-action-for-an-adaptive-form-select-and-configure-submit-action). Por exemplo, integre os dados do formulário a um aplicativo de terceiros ou acione uma notificação SMS personalizada com base na entrada do usuário.

<!-- ![Custom Submit Image](/help/forms/assets/custom-submit-action-hero-image.png)
-->

## Pré-requisitos

Antes de começar a criar sua primeira ação de envio personalizada para o Adaptive Forms, verifique se você tem o seguinte:

* **Editor de Texto sem Formatação (IDE)**: embora qualquer editor de texto sem formatação possa funcionar, um IDE (Ambiente de Desenvolvimento Integrado) como o Microsoft Visual Studio Code oferece recursos avançados para facilitar a edição.

* **Git**: este sistema de controle de versão é necessário para gerenciar alterações de código. Se não estiver instalado, baixe-o de https://git-scm.com.

## Criar a primeira ação de envio personalizada para o formulário

O diagrama abaixo descreve as etapas para criar uma ação de envio personalizada para um Formulário adaptável:

![Fluxo de trabalho personalizado de ação de envio](/help/forms/assets/custom-submit-action-workflow.png){width=50%, height-50%}

### Clonar o repositório Git do AEM as a Cloud Service.

1. Abra a linha de comando e escolha um diretório para armazenar seu repositório do AEM as a Cloud Service, como `/cloud-service-repository/`.

1. Execute o comando abaixo para clonar o repositório:

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **Onde encontrar essas informações?**

   Para obter as instruções passo a passo sobre como localizar esses detalhes, consulte o artigo &quot;[Acessando o Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)&quot; da Adobe Experience League.

   **Seu projeto está pronto!**

   Quando o comando for concluído com sucesso, você verá uma nova pasta criada no diretório local. Essa pasta é nomeada com base no aplicativo (por exemplo, app-id). Esta pasta contém todos os arquivos e códigos baixados do repositório Git da AEM as a Cloud Service. Você pode encontrar `<appid>` para seu Projeto AEM no arquivo `archetype.properties`.

   ![Propriedades do Arquétipo](/help/forms/assets/custom-submit-action-archetype-app-id.png)

   Neste guia, nos referimos a essa pasta como `[AEMaaCS project directory]`.

## Adicionar nova ação de envio

1. Abra a pasta do repositório em um editor.

   ![Repositório clonado](/help/forms/assets/custom-submit-action-clone-repo.png)

1. Navegue até o seguinte diretório no `[AEMaaCS project directory]`:

   ```
   /ui.apps/src/main/content/jcr_root/apps/<app-id>/
   ```

   **Importante**: substitua `<app-id>` pela ID do aplicativo real.

1. Crie uma nova pasta para sua ação de envio personalizada e dê a ela o nome de sua escolha. Por exemplo, nomeie a pasta como `customsubmitaction`.

   ![Criar pasta de ação de envio personalizada](/help/forms/assets/custom-submit-action-create-folder.png)

1. Navegue até o diretório de ação de envio personalizado adicionado.

   Em seu `[AEMaaCS project directory]`, navegue até o seguinte caminho:

   `/ui.apps/src/main/content/jcr_root/apps/<app-id>/customsubmitaction/`

   `Important`: Substitua `<app-id>` pela ID do aplicativo real.

1. Criar novo arquivo de configuração.
Na pasta `customsubmitaction`, crie um novo arquivo chamado `.content.xml`.

   ![Criar arquivo de configuração](/help/forms/assets/custom-submit-action-create-config-folder.png)

1. Abra este arquivo e cole o conteúdo a seguir, substituindo `[customsubmitaction]` pelo nome da sua ação de envio

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
   jcr:description="[customsubmitaction]"
   jcr:primaryType="sling:Folder"
   
   guideComponentType="fd/af/components/guidesubmittype"
   guideDataModel="basic,xfa,xsd"
   submitService="[customsubmitaction]"/>
   ```

   Por exemplo, substitua o `[customsubmitaction]` pelo nome da ação de envio personalizada como `Custom Submit Action`.

   ![Criar arquivo de configuração de ação de envio personalizado](/help/forms/assets/custom-submit-action-config-file.png)

   >[!NOTE]
   >
   > Lembre-se do nome de [customsubmitaction], pois o mesmo nome aparece na lista suspensa `Submit action` ao criar um formulário.


**Incluir a nova pasta em`filter.xml`**

1. Navegue até o arquivo `/ui.apps/src/main/content/META-INF/vault/filter.xml` no seu [diretório do projeto AEMaaCS].

1. Abra o arquivo e adicione a seguinte linha no final:

   ```
   <filter root="/apps/<app-id>/[customsubmitaction-folder]"/>
   ```

   Por exemplo, adicione a seguinte linha de código para adicionar a pasta `customsubmitaction` no arquivo `filter.xml`:

   ```
   <filter root="/apps/wknd/customsubmitaction"/>
   ```

   ![Adicionar as pastas criadas no filter.xml](/help/forms/assets/custom-submit-action-filter-xml.png)

1. Salve as alterações.

### Implementar o serviço para a ação enviar adicionada.

1. Navegue até o seguinte diretório no `[AEMaaCS project directory]`:
   `/core/src/main/java/com/<app-id>/core/service/`
   `Important`: Substitua `<app-id>` pela ID do aplicativo real.
1. Criar novo arquivo Java para implementar o serviço para a ação de envio adicionada. Por exemplo, adicione o novo arquivo Java como `CustomSubmitService.java`.

   ![Pasta de Ação de Envio Personalizada](/help/forms/assets/custom-submit-action-custom-submit-folder.png)

1. Abra este arquivo e adicione o código para sua implementação de ação de envio personalizada.

   Por exemplo, o código Java abaixo é um serviço OSGi que lida com o envio de formulário registrando os dados enviados e retorna o status `OK`. Adicionar o seguinte código no arquivo `CustomSubmitService.java`:

   ```
   package com.wknd.core.service;
   
   import com.adobe.aemds.guide.model.FormSubmitInfo;
   import com.adobe.aemds.guide.service.FormSubmitActionService;
   import java.util.HashMap;
   import java.util.Map;
   import org.osgi.service.component.annotations.Component;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
       @Component(
       service = FormSubmitActionService.class,
       immediate = true
           )
       public class CustomSubmitService implements FormSubmitActionService {
   
       private static final String serviceName = "Custom Submit Action";
   
       private static Logger log = LoggerFactory.getLogger(CustomSubmitService.class);
   
       @Override
       public String getServiceName() {
       return serviceName;
       }
   
       @Override
       public Map<String, Object> submit(FormSubmitInfo formSubmitInfo) {
       String data = formSubmitInfo.getData();
       log.info("Using custom submit action service, [data] --> " + data);
       Map<String, Object> result = new HashMap<>();
       result.put("status", "OK");
       return result;
        }
       }
   ```

   ![Serviço de ação de envio personalizado](/help/forms/assets/custom-submit-action-service.png)

1. Salve as alterações.

### Implante o código.

**Implantar código para ambiente de desenvolvimento local**

* Implante o AEM as a Cloud Service, `[AEMaaCS project directory]`, em seu ambiente de desenvolvimento local para experimentar a nova ação de envio em sua máquina local. Para implantar no ambiente de desenvolvimento local:

   1. Certifique-se de que o ambiente de desenvolvimento local esteja em funcionamento. Se você ainda não tiver configurado um ambiente de desenvolvimento local, consulte o manual em [Configurar um ambiente de desenvolvimento local para o AEM Forms](/help/forms/setup-local-development-environment.md).

   1. Abra a janela do terminal ou o prompt de comando.

   1. Navegue até `[AEMaaCS project directory]`.

   1. Execute o seguinte comando:

      ```
      mvn -PautoInstallPackage clean install
      ```

      ![Implantação local](/help/forms/assets/custom-submit-action-local-deployment.png)

**Implantar o código para o ambiente do Cloud Service**

* Implante o AEM as a Cloud Service, `[AEMaaCS project directory]`, no seu ambiente Cloud Service. Para implantar no ambiente do Cloud Service:

   1. Confirme suas alterações:

      Depois de adicionar a nova configuração de ação de envio personalizada, confirme suas alterações com uma mensagem Git clara. (Por exemplo, &quot;Adição de uma nova ação de envio personalizada&quot;).

   1. Implante o código atualizado:

      Acione uma implantação do seu código por meio do [pipeline de pilha completa existente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline). Ele cria e implanta automaticamente o código atualizado com o novo suporte personalizado às ações de envio.

      Se você ainda não tiver configurado um pipeline, consulte o manual sobre [como configurar um pipeline para o AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline).

      ![Implantação da nuvem](/help/forms/assets/custom-submit-action-cloud-deployment.png)

      **Como confirmar a instalação?**

      Depois que o projeto for compilado com êxito, a ação de envio personalizada aparecerá na lista suspensa `Submit action` ao criar um formulário.

      ![Lista Suspensa de Ação de Envio Personalizada](/help/forms/assets/custom-submit-action-drop-down-list.png)

  Seu ambiente agora está pronto para usar a ação de envio personalizada adicionada ao criar um formulário.

### Visualizar um formulário adaptável com a ação de envio recém-adicionada

1. Faça logon na sua instância do AEM Forms as a Cloud Service.
1. Ir para **Forms** > **Forms e Documentos**.

   ![Forms e Documentos](/help/forms/assets/custom-submit-action-fnd.png)

1. Selecione um Formulário adaptável e clique em **Editar**. O formulário é aberto no modo de edição.

   ![Editar formulário](/help/forms/assets/custom-submit-action-edit-af.png)

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique na guia **[!UICONTROL Envio]**.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione a ação de envio. Por exemplo, selecione a ação de envio como `Custom Submit Action`.

   ![Formulário de envio personalizado](/help/forms/assets/custom-submit-action-select-submit-action.png)

1. Preencha o formulário e envie-o.

   ![Enviar Formulário](/help/forms/assets/custom-submit-action-submit-form.png)

   ![Mensagem de agradecimento](/help/forms/assets/custom-submit-action-thankyou-msg.png)

   Depois que o formulário for enviado com êxito, você poderá verificar a **Configuração do Console da Web do Adobe Experience Manager** para verificar a ação da ação de envio personalizada no ambiente de desenvolvimento local.
1. Acesse `http://<host>:<port>/system/console/configMgr`.

1. Navegue até o **Suporte ao Log do Console da Web do Adobe Experience Manager** em `http://<host>:<port>/system/console/slinglog`.

   ![ConfigMgr](/help/forms/assets/custom-submit-action-sling-log.png)

1. Clique na opção `logs/error.log`.
   ![Abrir arquivo error.log](/help/forms/assets/custom-submit-action-error-log.png)

1. Abra o arquivo `error.log` para ver se os dados foram anexados a ele.

   ![arquivo de log de erros](/help/forms/assets/custom-submit-action-form-data-display.png)

   >[!NOTE]
   >
   > * Para exibir logs de erros no ambiente do AEM as a Cloud Service, você pode usar o Splunk.
   > * Se um serviço de ação de envio personalizado encontrar um erro não tratado, o AEM as a Cloud Service retornará uma página de erro 502 HTML.


## Perguntas frequentes

**P: Por que meu formulário adaptável mostra uma página de erro 5.x.x após o envio?**
Falha no serviço de ação de envio personalizado com um erro sem tratamento. O AEM Cloud Service retorna a página de erro padrão.

<!--
## Best practices

 * It is recommended to use the OSGi service approach for creating a custom submit action, as it is faster than the AEM servlet approach. 

## Next steps
-->

## Artigos relacionados

{{af-submit-action}}

<!-- The [Adaptive Forms Core Components](https://github.com/adobe/aem-core-forms-components) repository includes a sample folder, `customsubmission/logsubmit`, to simplify the process of adding new custom submit actions. It also provides the Java service implementation for the `logsubmit` custom submit action, named `CustomAFSubmitService`.java. These resources are available on GitHub. -->
