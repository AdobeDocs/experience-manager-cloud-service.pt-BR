---
title: Integração com o Adobe Target
description: 'Integração com o Adobe Target '
translation-type: tm+mt
source-git-commit: 7d3b5199333a60d69957819d874f8ce1bafdd797
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 2%

---


# Integração com o Adobe Target{#integrating-with-adobe-target}

Como parte do Adobe Marketing Cloud, a Adobe Target permite aumentar a relevância do conteúdo por meio da definição de metas e medição em todos os canais. A integração do Adobe Target e do AEM como Cloud Service exige:

* usando a interface de usuário para toque para criar uma Configuração de Público alvo em AEM como Cloud Service (configuração IMS necessária).
* adicionar e configurar o Adobe Target como uma extensão no [Adobe Launch](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/quick-start.html).

O Adobe Launch é necessário para gerenciar as propriedades do cliente para o Analytics e o Público alvo em páginas AEM (bibliotecas/tags do JS). Dito isso, a integração com o Launch é necessária para a &quot;definição de metas de experiência&quot;. Para que os Fragmentos de experiência exportem para o Público alvo, você precisa apenas da Configuração Adobe Target e IMS.

>[!NOTE]
>
>A Adobe Experience Manager como cliente Cloud Service que não tem uma conta de Público alvo existente pode solicitar acesso ao Público alvo Foundation Pack para Experience Cloud. O Foundation Pack fornece utilização limitada em volume do Público alvo.

## Criando a configuração do Adobe Target {#create-configuration}

1. Navegue até **Ferramentas** → **Cloud Services**.
   ![](assets/cloudservice1.png "Navegação")
2. Selecione **Adobe Target**.
3. Selecione o botão **Criar** .
   ![](assets/tenant1.png "CriarCriar")
4. Preencha os detalhes (veja abaixo) e selecione **Connect (Conectar**).
   ![](assets/open_screen1.png "Connect")

### Configuração IMS

Uma configuração IMS para o Launch e o Público alvo é necessária para integrar corretamente o Público alvo ao AEM e ao Launch. Embora a configuração IMS para Inicialização seja pré-configurada em AEM como um Cloud Service, a configuração IMS do Público alvo deve ser criada (após o Público alvo ser provisionado). Consulte [este vídeo](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html) e [esta página](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html) para saber como criar a configuração IMS do Público alvo.

### Edição da configuração do Público alvo {#edit-target-configuration}

Para editar a configuração do Público alvo, siga estas etapas:

1. Selecione uma configuração existente e clique em **Propriedades**.
2. Edite as propriedades.
3. Select **Re-connect to Adobe Target**.
   ![Reconecte-](assets/edit_config_page1.png "se")
4. Selecione **Salvar e fechar**.

### Adicionar uma configuração a um site {#add-configuration}

Para aplicar uma configuração de interface de usuário de toque a um site, vá para: **Sites** → **Selecione qualquer página** do site → **Propriedades** → **Avançado** → **Configuração** → Selecione o locatário da configuração.

## Integração da Adobe Target em sites AEM usando o Adobe Launch {#integrate-target-launch}

AEM oferta uma integração pronta para uso com o Experience Platform Launch. Ao adicionar a extensão do Adobe Target ao Experience Platform Launch, você pode usar os recursos do Adobe Target em AEM página(s) da Web.As bibliotecas de Públicos alvos só serão renderizadas usando o Launch.

>[!NOTE]
>
>As estruturas existentes (herdadas) ainda funcionam, mas não podem ser configuradas na interface do usuário para toque. É aconselhável recriar as configurações de mapeamento de variáveis no Launch.

Como uma visão geral, as etapas de integração são:

1. Criar uma propriedade de inicialização
2. Adicionar as extensões necessárias
3. Criar um elemento de dados (para capturar parâmetros de hub de contexto)
4. Criar uma regra de página
5. Criar e publicar

### Criação de uma propriedade Launch {#create-property}

Uma propriedade é um container que será preenchido com extensões, regras e elementos de dados.

1. Selecione o botão **Nova propriedade** .
2. Forneça um nome para sua propriedade.
3. Conforme o domínio, digite o IP/host no qual você deseja carregar a biblioteca de inicialização.
4. Selecione o botão **Salvar** .
   ![](assets/properties_newproperty1.png "LaunchpropertyLaunchproperty")

### Adicionar as extensões necessárias {#add-extension}

**Extensões** é o container que gerencia as configurações principais da biblioteca. A extensão do Adobe Target suporta implementações do lado do cliente usando o Público alvo JavaScript SDK para a Web moderna, o at.js. É necessário adicionar as extensões **Adobe Target** e **Adobe ContextHub** .

1. Selecione a opção Catálogo de extensão e procure o Público alvo no filtro.
2. Selecione **Adobe Target** at.js e clique na opção Instalar.
   ![Pesquisa](assets/search_ext1.png "do público alvo SearchTarget")
3. Select the **Configure** button. Observe a janela de configuração com as credenciais de conta de Público alvo importadas e a versão at.js para essa extensão.
4. Selecione **Salvar** para adicionar a Extensão do target à propriedade Iniciar. Você pode ver a Extensão do target listada na lista **Installed Extensions (Extensões** instaladas).
   ![Salvar extensão](assets/configure_extension1.png "ExtensionSave")
5. Repita as etapas acima para pesquisar a extensão **Adobe ContextHub** e instalá-la (isso é necessário para a integração com parâmetros contextuais, com base nos quais a definição de metas será feita).

### Criação de um elemento de dados {#data-element}

**Os elementos** de dados são os espaços reservados para os quais você pode mapear os parâmetros do hub de contexto.

1. Selecione Elementos **de dados**.
2. Selecione **Adicionar elemento** de dados.
3. Forneça o nome do elemento de dados e mapeie-o para um parâmetro de hub de contexto.
4. select **Save**.
   ![Elemento](assets/data_elem1.png "de dados")

### Criação de uma regra de página {#page-rule}

Em **Regra** , definimos e ordenamos uma sequência de ações, que serão executadas no site, para atingir a definição de metas.

1. Adicione um conjunto de ações como exemplificado na captura de tela.
   ![](assets/rules1.png "AçõesAções")
2. Em Adicionar parâmetros a todas as mboxes, adicione o elemento de dados configurado anteriormente (consulte o elemento de dados acima) ao parâmetro que será enviado na chamada da mbox.
   ![](assets/map_data1.png "MboxActions")

### Criar e publicar {#build-publish}

Para saber como criar e publicar, consulte esta [página](https://docs.adobe.com/content/help/en/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html).

## Alterações na estrutura do conteúdo entre as configurações de interface clássica e de toque {#changes-content-structure}

| **Alterar** | **Configuração da interface clássica** | **Configuração da interface de toque** | **Consequências** |
|---|---|---|---|
| Localização da Configuração do Público alvo. | /etc/cloudservices/testandtarget/ | /conf/locatário/settings/cloudservices/público alvo | Anteriormente, várias configurações estavam presentes em /etc/cloudservices/testandtarget, mas agora uma única configuração estará presente sob um locatário. |

>[!NOTE]
>
>As configurações herdadas ainda são compatíveis com os clientes existentes (sem a opção de editar ou criar novos). As configurações herdadas farão parte dos pacotes de conteúdo carregados pelo cliente usando o VSTS.
