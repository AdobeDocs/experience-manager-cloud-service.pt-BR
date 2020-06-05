---
title: Tags inteligentes aprimoradas
description: Aplique tags comerciais contextuais e descritivas usando o serviço AI e ML do Adobe Sensei, para melhorar a descoberta de ativos e a velocidade do conteúdo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 41684858f1fe516046b9601c1d869fff180320e0
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 7%

---


# Configurar o Experience Manager para a marcação inteligente de ativos {#configure-aem-for-smart-tagging}

Marcar ativos com um vocabulário controlado por taxonomia garante que os ativos possam ser facilmente identificados e recuperados por pesquisas baseadas em tags. A Adobe fornece Tags inteligentes que usam inteligência artificial e algoritmos de aprendizado de máquina para treinar imagens. As Tags inteligentes usam uma estrutura de inteligência artificial do [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) para treinar seu algoritmo de reconhecimento de imagem na estrutura de tags e na taxonomia comercial.

A funcionalidade Tags inteligentes está disponível para compra como um complemento para [!DNL Experience Manager]. Após a compra, um email é enviado ao administrador da sua organização com um link para o Adobe Developer Console. O administrador acessa o link para integrar as Tags inteligentes com o [!DNL Experience Manager] uso do Adobe Developer Console.

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
4. Post-GA, if time permits, create a video.
-->

## Integrar-se ao Adobe Developer Console {#aio-integration}

Antes de marcar as imagens usando o SCS, integre-se [!DNL Adobe Experience Manager] ao serviço de Tags inteligentes usando o Adobe Developer Console. No back end, o [!DNL Experience Manager] servidor autentica suas credenciais de serviço no gateway do Adobe Developer Console antes de encaminhar sua solicitação ao serviço.

* Crie uma configuração em [!DNL Experience Manager] para gerar uma chave pública. Obtenha um certificado público para integração OAuth.
* Crie uma integração no Adobe Developer Console e carregue a chave pública gerada.
* Configure sua [!DNL Experience Manager] instância usando a chave da API e outras credenciais do Adobe Developer Console.
* Como opção, ative a marcação automática no upload de ativos.

### Pré-requisitos para a integração do Adobe Developer Console {#prerequisite-for-aio-integration}

Antes de usar as Tags inteligentes, verifique o seguinte para criar uma integração no Adobe Developer Console:

* Uma conta da Adobe ID que tem privilégios de administrador para a organização.
* As Tags inteligentes estão ativadas para sua organização.

### Obtain a public certificate {#obtain-public-certificate}

Um certificado público permite autenticar seu perfil no Adobe Developer Console. Você cria um certificado de dentro [!DNL Experience Manager].

1. Na interface do [!DNL Experience Manager] usuário, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > Configurações **[!UICONTROL do]** Adobe IMS.

1. Na página Configurações [!UICONTROL do] Adobe IMS, clique em **[!UICONTROL Criar]**. No menu Solução **[!UICONTROL da]** Cloud, selecione Tags **** inteligentes.

1. Selecione **[!UICONTROL Criar novo certificado]**. Forneça um nome e clique em **[!UICONTROL Criar certificado]**. Clique em **[!UICONTROL OK]**.

1. Clique em **[!UICONTROL Baixar chave]** pública.

   ![Tags inteligentes do Experience Manager criam chave pública](assets/aem_smarttags-config1.png)

### Reconfigurar se um certificado expirar {#certrenew}

Quando o certificado expira, ele não é mais confiável. Para adicionar um novo certificado, siga estas etapas. Não é possível renovar um certificado expirado.

1. Log in your [!DNL Experience Manager] deployment as an administrator. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.

1. Localize e clique em **[!UICONTROL dam-update-service]** user. Clique na guia **[!UICONTROL Keystore]** .
1. Exclua o armazenamento de chave **[!UICONTROL similaritysearch]** existente com o certificado expirado. Click **[!UICONTROL Save &amp; Close]**.

   ![Exclua a entrada de pesquisa de similaridade existente no Keystore para adicionar um novo certificado de segurança](assets/smarttags_delete_similaritysearch_keystore.png)

   *Figura: Exclua a`similaritysearch`entrada existente no Keystore para adicionar um novo certificado de segurança.*

1. Na interface do [!DNL Experience Manager] usuário, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > Configurações **[!UICONTROL do]** Adobe IMS. Abra a configuração disponível das Smart Tags. Para baixar um certificado público, clique em **[!UICONTROL Baixar certificado]** público.

1. Acesse [https://console.adobe.io](https://console.adobe.io) e navegue até o serviço existente no Projeto. Carregue o novo certificado e configure. Para obter mais informações sobre configuração, consulte as instruções em [Criar integração](#create-aio-integration)do Adobe Developer Console.

### Criar uma integração {#create-aio-integration}

Para usar Tags inteligentes, crie uma integração no Adobe Developer Console para gerar a chave de API, a ID de conta técnica, a ID de organização e o segredo do cliente.

1. Acesse [https://console.adobe.io](https://console.adobe.io/) em um navegador. Selecione a conta apropriada e verifique se a função de organização associada é o administrador do sistema.
1. Crie um projeto com qualquer nome desejado. Clique em **[!UICONTROL Adicionar API]**.
1. Na página **[!UICONTROL Adicionar uma API]** , selecione **[!UICONTROL Experience Cloud]** e selecione Conteúdo **** inteligente. Clique em **[!UICONTROL Avançar]**.
1. Selecione **[!UICONTROL Carregar sua chave]** pública. Forneça o arquivo de certificado baixado de [!DNL Experience Manager]. Será exibida a mensagem Chave(s) [!UICONTROL pública(s) carregada(s) com êxito] . Clique em **[!UICONTROL Avançar]**.
1. [!UICONTROL A página Criar uma nova credencial] de Conta de Serviço (JWT) exibe a chave pública para a conta de serviço recém-configurada. Clique em **[!UICONTROL Avançar]**.
1. Na página **[!UICONTROL Selecionar perfis]** de produtos, selecione Serviços **[!UICONTROL de conteúdo]** inteligente. Clique em **[!UICONTROL Salvar API]** configurada. Uma página exibe mais informações sobre a configuração. Mantenha esta página aberta para copiar e adicionar esses valores no Experience Manager ao configurar ainda mais as Tags inteligentes em [!DNL Experience Manager].

   ![Na guia Visão geral, é possível revisar as informações fornecidas para integração.](assets/integration_details.png)

### Configurar tags inteligentes {#configure-smart-content-service}

Para configurar a integração, use os valores dos campos Carga, Segredo do cliente, Servidor de autorização e chave da API da integração do Adobe Developer Console.

1. Na interface do [!DNL Experience Manager] usuário, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > Configurações **[!UICONTROL do]** Adobe IMS.
1. Acesse a página Configuração **[!UICONTROL técnica de conta do]** Adobe IMS e forneça um **[!UICONTROL Título]** desejado.
1. No campo Servidor **[!UICONTROL de]** autorização, forneça o `https://ims-na1.adobelogin.com` URL.
1. No campo Chave **[!UICONTROL da]** API, forneça a ID **[!UICONTROL do]** cliente do [!DNL Adobe Developer Console].
1. No campo Segredo **[!UICONTROL do]** cliente, forneça o Segredo **[!UICONTROL do]** cliente do [!DNL Adobe Developer Console]. Clique na opção **[!UICONTROL Recuperar segredo]** do cliente para vê-lo.
1. Em [!DNL Adobe Developer Console], no seu projeto, clique em Conta **[!UICONTROL de serviço (JWT)]** na margem esquerda. Clique na **[!UICONTROL guia Gerar JWT]** . Clique em **[!UICONTROL Copiar]** para copiar a carga **[!UICONTROL JWT exibida]**. Forneça esse valor no campo **[!UICONTROL Carga]** em [!DNL Experience Manager]. Clique em **[!UICONTROL Criar]**.

### Validar a configuração {#validate-the-configuration}

Após concluir a configuração, siga estas etapas para validar a configuração.

1. Na interface do [!DNL Experience Manager] usuário, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > Configurações **[!UICONTROL do]** Adobe IMS.

1. Selecione a configuração de Tags inteligentes. Clique em **[!UICONTROL Verificar integridade]** na barra de ferramentas. Clique em **[!UICONTROL Verificar]**. Uma mensagem de diálogo com configuração  saudável confirma que a configuração está funcionando.

![Validar a configuração das Tags inteligentes](assets/smart-tag-config-validation.png)

## Habilitar marcação inteligente para ativos carregados recentemente (opcional) {#enable-smart-tagging-for-uploaded-assets}

1. Em [!DNL Experience Manager], vá até **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]**.
1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o modelo de fluxo de trabalho **[!UICONTROL Atualizar ativo do DAM]**.
1. Clique em **[!UICONTROL Editar]** na barra de ferramentas.
1. Expanda o painel lateral para exibir as etapas. Arraste a etapa **[!UICONTROL Ativo de tag inteligente]** disponível na seção Fluxo de trabalho do DAM e coloque-a após a etapa **[!UICONTROL Processar miniaturas]**.

   ![Adicione a etapa de ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Atualizar ativo do DAM](assets/chlimage_1-105.png)

   *Figura: Adicione uma etapa de ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho de Atualização de ativo do DAM.*

1. Abra a etapa a ser configurada. Em **[!UICONTROL Configurações avançadas]**, verifique se a opção **[!UICONTROL Avanço do manipulador]** está selecionada.

   ![Configuração do manipulador para avançar para a próxima etapa do fluxo de trabalho.](assets/smart-tags-workflow-handler-setting.png)

1. Na guia **[!UICONTROL Argumentos]** , selecione **[!UICONTROL Ignorar erros]** se desejar que o fluxo de trabalho ignore falhas ao prever tags. Para marcar os ativos quando eles forem carregados independentemente de a marcação inteligente estar ativada nas pastas, selecione **[!UICONTROL Ignorar sinalizador]** de tag inteligente.

1. Clique em **[!UICONTROL OK]** para fechar a etapa do processo e depois salve o fluxo de trabalho. Clique em **[!UICONTROL Sincronizar]**.

>[!MORELIKETHIS]
>
>* [Adicione tags a ativos usando o serviço inteligente](smart-tags.md)

