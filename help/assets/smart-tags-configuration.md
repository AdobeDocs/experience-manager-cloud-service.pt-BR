---
title: Tags inteligentes aprimoradas
description: Aplique tags comerciais contextuais e descritivas usando o serviço AI e ML do Adobe Sensei, para melhorar a descoberta de ativos e a velocidade do conteúdo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b5af8cad55c8644ba613370cf65b6a04b3abf9ed
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 12%

---


# Configurar o Experience Manager para a marcação inteligente de ativos {#configure-aem-for-smart-tagging}

Marcar ativos com um vocabulário controlado por taxonomia garante que os ativos possam ser facilmente identificados e recuperados por pesquisas baseadas em tags. A Adobe fornece o Smart Content Service (SCS) que usa inteligência artificial e algoritmos de aprendizado de máquina para treinar imagens. O Smart Content Service usa uma estrutura de inteligência artificial do [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) para treinar seu algoritmo de reconhecimento de imagem na estrutura de tags e na taxonomia comercial.

O Serviço de conteúdo inteligente está disponível para compra como um complemento para [!DNL Experience Manager]. Após a compra, um email é enviado ao administrador da sua organização com um link para a E/S da Adobe. O administrador acessa o link para integrar o Serviço de conteúdo inteligente ao [!DNL Experience Manager].

<!-- TBD: 
1. Create a similar flowchart for how training works in CS. ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
4. Post-GA, if time permits, create a video.
-->

## Integrar com E/S da Adobe {#aio-integration}

Antes de marcar as imagens usando o SCS, integre-se [!DNL Adobe Experience Manager] ao Serviço de conteúdo inteligente usando a E/S da Adobe. Use essa configuração para acessar o Serviço de conteúdo inteligente de dentro [!DNL Experience Manager].

O artigo detalha as seguintes tarefas principais que são necessárias para configurar o Serviço de conteúdo inteligente. No back end, o [!DNL Experience Manager] servidor autentica suas credenciais de serviço no gateway de E/S da Adobe antes de encaminhar sua solicitação ao Serviço de conteúdo inteligente.

* Crie uma configuração do Serviço de conteúdo inteligente em [!DNL Experience Manager] para gerar uma chave pública. Obtenha um certificado público para integração OAuth.
* Crie uma integração em E/S da Adobe e carregue a chave pública gerada.
* Configure sua [!DNL Experience Manager] instância usando a chave da API e outras credenciais da E/S da Adobe.
* Como opção, ative a marcação automática no upload de ativos.

### Pré-requisitos para integração de E/S da Adobe {#prerequisite-for-aio-integration}

Antes de usar o Serviço de conteúdo inteligente, verifique o seguinte para criar uma integração em E/S da Adobe:

* Uma conta da Adobe ID que tem privilégios de administrador para a organização.
* O serviço Smart Content Service está habilitado para sua organização.

### Obtain a public certificate {#obtain-public-certificate}

Um certificado público permite autenticar seu perfil em E/S da Adobe.

1. Na interface do [!DNL Experience Manager] usuário, acesse **[!UICONTROL Ferramentas]** > Serviços **[!UICONTROL da]** Cloud > Serviços **** herdados da Cloud.

1. On the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. Na caixa de diálogo **[!UICONTROL Criar configuração]** , especifique um título e um nome para a configuração de Tags inteligentes. Clique em **[!UICONTROL Criar]**.

1. Na caixa de diálogo Serviço **[!UICONTROL de conteúdo inteligente do]** AEM, use os seguintes valores:

   **[!UICONTROL URL do serviço]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorização]**: `https://ims-na1.adobelogin.com`

   Deixe os outros campos em branco por enquanto (a ser fornecido posteriormente). Clique em **[!UICONTROL OK]**.

   ![Caixa de diálogo do Serviço de conteúdo inteligente do Experience Manager para fornecer o URL do serviço de conteúdo](assets/aem_scs.png)

1. Clique em **[!UICONTROL Baixar certificado público para integração]** OAuth e baixe o arquivo de certificado público `AEM-SmartTags.crt`.

   ![Uma representação das configurações criadas para o serviço de marcação inteligente](assets/download_link.png)

### Reconfigurar se um certificado expirar {#certrenew}

Quando o certificado expira, ele não é mais confiável. Para adicionar um novo certificado, siga estas etapas. Não é possível renovar um certificado expirado.

1. Log in your [!DNL Experience Manager] deployment as an administrator. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.

1. Localize e clique em **[!UICONTROL dam-update-service]** user. Clique na guia **[!UICONTROL Keystore]** .
1. Exclua o armazenamento de chave **[!UICONTROL similaritysearch]** existente com o certificado expirado. Click **[!UICONTROL Save &amp; Close]**.

   ![Exclua a entrada de pesquisa de similaridade existente no Keystore para adicionar um novo certificado de segurança](assets/smarttags_delete_similaritysearch_keystore.png)

   *Figura: Exclua a`similaritysearch`entrada existente no Keystore para adicionar um novo certificado de segurança.*

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Serviços da nuvem herdados]**. Clique em **[!UICONTROL Tags inteligentes de ativos]** > **[!UICONTROL Mostrar configuração]** > **[!UICONTROL Configurações disponíveis]**. Clique na configuração necessária.

1. Para baixar um certificado público, clique em **[!UICONTROL Baixar certificado público para integração]** OAuth.
1. Acesse [https://console.adobe.io](https://console.adobe.io) e navegue até os Serviços de conteúdo inteligente existentes na página **[!UICONTROL Integrações]** . Carregue o novo certificado. Para obter mais informações, consulte as instruções em [Criar integração](#create-adobe-i-o-integration)de E/S da Adobe.

### Criar uma integração {#create-aio-integration}

Para usar as APIs do Serviço de conteúdo inteligente, crie uma integração em E/S da Adobe para gerar a chave da API, a ID da conta técnica, a ID da organização e o segredo do cliente.

1. Acesse [https://console.adobe.io](https://console.adobe.io/).
1. Na página **[!UICONTROL Integrações]** , selecione a conta apropriada e verifique se a função de organização associada é de administrador do sistema.
1. Clique em **[!UICONTROL Nova integração]**.
1. Na página **[!UICONTROL Criar uma nova integração]** , selecione **[!UICONTROL Acessar uma API]**. Clique em **[!UICONTROL Continuar]**.
1. Em **[!UICONTROL Experience Cloud]**, selecione **[!UICONTROL Conteúdo inteligente]**. Clique em **[!UICONTROL Continuar]**.
1. Na próxima página, selecione **[!UICONTROL Nova integração]**. Clique em **[!UICONTROL Continuar]**.
1. Na página Detalhes **[!UICONTROL da]** integração, especifique um nome para o gateway de integração e adicione uma descrição.
1. Nos certificados **[!UICONTROL de chaves]** públicas, carregue `AEM-SmartTags.crt` o arquivo baixado acima.
1. Clique em **[!UICONTROL Criar integração]**.
1. Para visualização das informações de integração, clique em **[!UICONTROL Continuar para obter os detalhes]** da integração.

   ![Na guia Visão geral, é possível revisar as informações fornecidas para integração.](assets/integration_details.png)

### Configurar o Serviço de conteúdo inteligente {#configure-smart-content-service}

Para configurar a integração, use os valores dos campos ID da conta técnica, ID da organização, segredo do cliente, servidor de autorização e chave da API da integração de E/S da Adobe. A criação de uma configuração em nuvem de Tags inteligentes permite a autenticação de solicitações de API da [!DNL Experience Manager] instância.

1. Em [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas > Serviço em nuvem > Serviços]** herdados em nuvem para abrir o console Serviços [!UICONTROL em] nuvem.
1. Em Tags **[!UICONTROL inteligentes de]** ativos, abra a configuração criada acima. Na página de configurações do serviço, clique em **[!UICONTROL Editar]**.
1. Na caixa de diálogo **[!UICONTROL Serviço de conteúdo inteligente do AEM]**, use os valores pré-preenchidos nos campos **[!UICONTROL URL do serviço]** e **[!UICONTROL Servidor de autorização]**.
1. Nos campos **[!UICONTROL Chave da API]**, **[!UICONTROL ID da conta técnica]**, **[!UICONTROL ID da organização]** e **[!UICONTROL Segredo do cliente]**, use os valores gerados acima.

### Validar a configuração {#validate-the-configuration}

Depois de concluir a configuração, você pode usar um MBean JMX para validar a configuração. Para validar, siga estas etapas.

1. Acesse seu [!DNL Experience Manager] servidor em `https://[aem_server]:[port]`.

1. Vá até **[!UICONTROL Ferramentas > Operações > Console]** da Web para abrir o console do OSGi. Clique em **[!UICONTROL Principal > JMX]**.
1. Clique em **[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**. Ele abre **[!UICONTROL SemelhançaPesquise Tarefas Diversas.]**
1. Clique em **[!UICONTROL validateConfigs()]**. Na caixa de diálogo **[!UICONTROL Validar configurações]** , clique em **[!UICONTROL Chamar]**.

   O resultado da validação é exibido na mesma caixa de diálogo.

## Habilitar marcação inteligente para ativos carregados recentemente (opcional) {#enable-smart-tagging-for-uploaded-assets}

1. Em [!DNL Experience Manager], vá até **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]**.
1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o modelo de fluxo de trabalho **[!UICONTROL Atualizar ativo do DAM]**.
1. Clique em **[!UICONTROL Editar]** na barra de ferramentas.
1. Expanda o painel lateral para exibir as etapas. Arraste a etapa **[!UICONTROL Ativo de tag inteligente]** disponível na seção Fluxo de trabalho do DAM e coloque-a após a etapa **[!UICONTROL Processar miniaturas]**.

   ![Adicione a etapa de ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Atualizar ativo do DAM](assets/chlimage_1-105.png)

   *Figura: Adicione uma etapa de ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho de Atualização de ativo do DAM.*

1. Abra a etapa a ser configurada. Em **[!UICONTROL Configurações avançadas]**, verifique se a opção **[!UICONTROL Avanço do manipulador]** está selecionada.

   ![chlimage_1-3](assets/smart-tags-workflow-handler-setting.png)

1. Na guia **[!UICONTROL Argumentos]** , selecione **[!UICONTROL Ignorar erros]** se desejar que o fluxo de trabalho ignore falhas ao prever tags. Para marcar os ativos quando eles forem carregados independentemente de a marcação inteligente estar ativada nas pastas, selecione **[!UICONTROL Ignorar sinalizador]** de tag inteligente.

1. Clique em **[!UICONTROL OK]** para fechar a etapa do processo e depois salve o fluxo de trabalho. Clique em **[!UICONTROL Sincronizar]**.

>[!MORELIKETHIS]
>
>* [Adicione tags a ativos usando o serviço inteligente](smart-tags.md)