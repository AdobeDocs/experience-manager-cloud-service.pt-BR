---
title: Tags inteligentes aprimoradas
description: Aplique tags comerciais contextuais e descritivas usando o serviço de IA e aprendizado de máquina do Adobe Sensei para melhorar a descoberta de ativos e a velocidade do conteúdo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a1213a1694a50d174b4ad1e7e4ba7c71944b861a
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 83%

---


# Configurar [!DNL Experience Manager] para marcação inteligente de ativos {#configure-aem-for-smart-tagging}

Marcar ativos com um vocabulário controlado por taxonomia garante que esses ativos possam ser facilmente identificados e recuperados por pesquisas baseadas em tags. A Adobe fornece tags inteligentes que usam inteligência artificial e algoritmos de aprendizado de máquina para treinar imagens. As tags inteligentes usam uma estrutura de inteligência artificial do [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) para treinar o algoritmo de reconhecimento de imagem de acordo com sua estrutura de tags e sua taxonomia comercial.

A funcionalidade Tag inteligentes está disponível para compra como suplemento do [!DNL Experience Manager]. Após a compra, um email é enviado ao administrador da sua organização com um link para o Console do desenvolvedor. O administrador acessa o link para integrar as Tags inteligentes ao [!DNL Experience Manager] usando o Console do desenvolvedor.

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
-->

>[!IMPORTANT]
>
>Se suas [!DNL Experience Manager Assets] implantações foram criadas após a [versão de agosto de 2020](/help/release-notes/release-notes-cloud/2020/release-notes-2020-8-0.md#assets), [!DNL Adobe Developer Console] é integrado por padrão. Ajuda a configurar a funcionalidade de tags inteligentes com mais rapidez. Nas implantações mais antigas, os administradores podem configurar manualmente a integração usando as instruções a seguir.

## Integração com o Console do desenvolvedor {#aio-integration}

Antes de marcar as imagens usando o SCS, integre o [!DNL Adobe Experience Manager] ao serviço de Tags inteligentes usando o Console do desenvolvedor. No back-end, o servidor do [!DNL Experience Manager] autentica suas credenciais de serviço no gateway do Console do desenvolvedor antes de encaminhar sua solicitação ao serviço.

* Crie uma configuração no [!DNL Experience Manager] para gerar uma chave pública. [Obtenha um certificado público](#obtain-public-certificate) para a integração OAuth.
* [Crie uma integração no Console do desenvolvedor](#create-aio-integration) e faça upload da chave pública gerada.
* [Configure tags inteligentes](#configure-smart-content-service) na sua instância do [!DNL Experience Manager] usando a chave da API e outras credenciais do Console do desenvolvedor.
* [Teste a configuração](#validate-the-configuration).
* [Reconfigure após a expiração do certificado](#certrenew).

### Pré-requisitos para a integração com o Console do desenvolvedor {#prerequisite-for-aio-integration}

Antes de usar as Tags inteligentes, é necessário criar uma integração no Console do desenvolvedor, verificando as seguintes condições:

* Existência de uma Adobe ID com privilégios de administrador para a organização.
* Ativação das Tags inteligentes para a sua organização.

### Obter um certificado público {#obtain-public-certificate}

Um certificado público permite autenticar seu perfil no Console do desenvolvedor. Você cria um certificado dentro do [!DNL Experience Manager].

1. Na interface do [!DNL Experience Manager], acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**.

1. Na página [!UICONTROL Configurações do Adobe IMS], clique em **[!UICONTROL Criar]**. No menu **[!UICONTROL Solução da nuvem]**, selecione **[!UICONTROL Tags inteligentes]**.

1. Selecione **[!UICONTROL Criar novo certificado]**. Forneça um nome e clique em **[!UICONTROL Criar certificado]**. Clique em **[!UICONTROL OK]**.

1. Clique em **[!UICONTROL Baixar chave pública]**.

   ![[!DNL Experience Manager] Tags inteligentes criar chave pública](assets/aem_smarttags-config1.png)

### Criar uma integração {#create-aio-integration}

Para usar Tags inteligentes, crie uma integração no Console do desenvolvedor para gerar a Chave da API, a ID de conta técnica, a ID da organização e o Segredo do cliente.

1. Acesse [https://console.adobe.io](https://console.adobe.io/) em um navegador. Selecione a conta e verifique se a organização associada tem a função de administrador do sistema.
1. Crie um projeto com o nome que quiser. Clique em **[!UICONTROL Adicionar API]**.
1. Na página **[!UICONTROL Adicionar uma API]**, selecione **[!UICONTROL Experience Cloud]** e selecione **[!UICONTROL Conteúdo inteligente]**. Clique em **[!UICONTROL Avançar]**.
1. Selecione **[!UICONTROL Fazer upload da sua chave pública]**. Forneça o arquivo de certificado baixado do [!DNL Experience Manager]. Será exibida a mensagem [!UICONTROL Chave(s) pública(s) carregada(s) com êxito]. Clique em **[!UICONTROL Avançar]**.
1. [!UICONTROL A página Criar uma nova ] credencial de conta de serviço (JWT) exibe a chave pública da conta de serviço. Clique em **[!UICONTROL Avançar]**.
1. Na página **[!UICONTROL Selecionar perfis de produtos]**, selecione **[!UICONTROL Serviços de conteúdo inteligente]**. Clique em **[!UICONTROL Salvar API configurada]**. Uma página exibe mais informações sobre a configuração. Mantenha essa página aberta para copiar e adicionar esses valores em [!DNL Experience Manager] ao configurar as Tags inteligentes em [!DNL Experience Manager].

   ![Na guia Visão geral, é possível revisar as informações da integração.](assets/integration_details.png)

### Configurar Tags inteligentes {#configure-smart-content-service}

Para configurar a integração, use os valores dos campos Carga, Segredo do cliente, Servidor de autorização e Chave da API na integração com o Console do desenvolvedor.

1. Na interface do [!DNL Experience Manager], acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**.
1. Acesse a página **[!UICONTROL Configuração de conta técnica do Adobe IMS]** e forneça um **[!UICONTROL Título]**.
1. No campo **[!UICONTROL Servidor de autorização]**, forneça o URL do `https://ims-na1.adobelogin.com`.
1. No campo **[!UICONTROL Chave da API]**, forneça a **[!UICONTROL ID do cliente]** do [!DNL Adobe Developer Console].
1. No campo **[!UICONTROL Segredo do cliente]**, forneça o **[!UICONTROL Segredo do cliente]** do [!DNL Adobe Developer Console]. Clique na opção **[!UICONTROL Recuperar segredo do cliente]** para vê-lo.
1. No [!DNL Adobe Developer Console], no seu projeto, clique em **[!UICONTROL Conta de serviço (JWT)]** na margem esquerda. Clique na guia **[!UICONTROL Gerar JWT]**. Clique em **[!UICONTROL Copiar]** para copiar a **[!UICONTROL Carga JWT]** exibida. Forneça esse valor no campo **[!UICONTROL Carga]** do [!DNL Experience Manager]. Clique em **[!UICONTROL Criar]**.

### Validar a configuração {#validate-the-configuration}

Após concluir a configuração, siga as etapas seguintes para validá-la.

1. Na interface do [!DNL Experience Manager], acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**.

1. Selecione a configuração de Tags inteligentes. Clique em **[!UICONTROL Verificar integridade]** na barra de ferramentas. Clique em **[!UICONTROL Verificar]**. Uma caixa de diálogo com a mensagem [!UICONTROL Configuração correta] confirma que a configuração está funcionando.

![Validar a configuração de Tags inteligentes](assets/smart-tag-config-validation.png)

### Reconfigure se um certificado expirar {#certrenew}

Quando o certificado expira, ele não é mais confiável. Para adicionar um certificado, siga estas etapas. Não é possível renovar um certificado expirado.

1. Faça logon na implantação do [!DNL Experience Manager] como administrador. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.

1. Localize o usuário **[!UICONTROL dam-update-service]** e clique nele. Clique na guia **[!UICONTROL Armazenamento de chaves]**.
1. Exclua o armazenamento de chaves **[!UICONTROL similaritysearch]** existente com o certificado expirado. Clique em **[!UICONTROL Salvar e fechar]**.

   ![Exclua a entrada de pesquisa de similaridade existente no Armazenamento de chaves para adicionar um novo certificado de segurança](assets/smarttags_delete_similaritysearch_keystore.png)

   *Figura: Exclua a  `similaritysearch` entrada existente no Armazenamento de chaves para adicionar um certificado de segurança.*

1. Na interface do [!DNL Experience Manager], acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**. Abra a configuração disponível de Tags inteligentes. Para baixar um certificado público, clique em **[!UICONTROL Baixar certificado público]**.

1. Acesse [https://console.adobe.io](https://console.adobe.io) e vá para o serviço existente no Projeto. Faça upload do novo certificado e configure-o. Para obter mais informações sobre configuração, consulte as instruções em [Criar integração com o Console do desenvolvedor](#create-aio-integration).

## Habilitar marcação automática quando os ativos forem carregados (opcional) {#enable-smart-tagging-for-uploaded-assets}

1. No [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]**.
1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização DAM]**.
1. Clique em **[!UICONTROL Editar]** na barra de ferramentas.
1. Expanda o painel lateral para exibir as etapas. Arraste a etapa **[!UICONTROL Ativo de tag inteligente]** disponível na seção Fluxo de trabalho do DAM e coloque-a após a etapa **[!UICONTROL Processar miniaturas]**.

   ![Etapa para adicionar ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Ativo de atualização DAM](assets/chlimage_1-105.png)

   *Figura: etapa para adicionar ativo de tag inteligente após a etapa de miniatura do processo no fluxo de trabalho Ativo de atualização DAM*

1. Abra a etapa a ser configurada. Em **[!UICONTROL Configurações avançadas]**, verifique se a opção **[!UICONTROL Avanço do manipulador]** está selecionada.

   ![Configuração do manipulador para avançar até a próxima etapa do fluxo de trabalho.](assets/smart-tags-workflow-handler-setting.png)

1. Na guia **[!UICONTROL Argumentos]**, selecione **[!UICONTROL Ignorar erros]** se quiser que o fluxo de trabalho ignore falhas ao prever tags. Para marcar os ativos quando eles forem carregados independentemente de a marcação inteligente estar ativada nas pastas, selecione **[!UICONTROL Ignorar sinalizador de tag inteligente]**.

1. Clique em **[!UICONTROL OK]**. Ela fecha a etapa do processo. Salve o workflow. Clique em **[!UICONTROL Sincronizar]**.

>[!MORELIKETHIS]
>
>* [Adicione tags a ativos usando o serviço inteligente](smart-tags.md)

