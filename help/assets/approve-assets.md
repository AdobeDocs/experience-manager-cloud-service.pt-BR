---
title: Aprovar ativos no Experience Manager
description: Saiba como aprovar ativos no [!DNL Experience Manager].
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---

# Aprovar ativos no [!DNL Experience Manager]

Os gerentes e comerciantes de marca mantêm controle rigoroso sobre os ativos da marca. Somente as versões aprovadas e mais recentes do ativo estão disponíveis para uso, garantindo a consistência da marca em todos os canais e aplicativos.

Você pode aprovar ativos no AEM Assets para simplificar o gerenciamento de ativos, garantindo um processo controlado e eficiente para manuseio de ativos.

## Antes de começar {#pre-requisites}

Você deve ter acesso ao AEM Assets as a Cloud Service e permissões para editar o **[!UICONTROL Status da revisão]** para um ativo.

## Configuração

Você precisa fazer uma atualização única no esquema de metadados aplicável na [!DNL Experience Manager] antes de aprovar um ativo. Você pode ignorar essa configuração para [!DNL Experience Manager Assets]. Siga estas etapas para configurar o esquema de metadados:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadados]**.
1. Selecione o esquema de metadados aplicável e clique em **[!UICONTROL Editar]**. <br>A variável **[!UICONTROL Editor do formulário de esquema de metadados]** abre com a **[!UICONTROL Básico]** guia realçada.
1. Role para baixo e clique em **[!UICONTROL Status da revisão]**.
1. Clique em **[!UICONTROL Regras]** no painel do lado direito.
1. Desmarcar **[!UICONTROL Desativar edição]** e clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Se os ativos ou pastas tiverem um esquema padrão diferente, certifique-se de fazer essa atualização nesse esquema específico.

## Aprovar ativos {#approve-assets}

Você pode aprovar ativos em ambos [!DNL Experience Manager] e [!DNL Experience Manager Assets]. Para aprovar ativos no [!DNL Experience Manager], siga estas etapas:

1. Selecione o ativo (s) e clique em **[!UICONTROL Propriedades]** no painel superior.
1. No **[!UICONTROL Básico]** , role para baixo até **[!UICONTROL Status da revisão]**.
1. Alterar o status da revisão para **[!UICONTROL Aprovado]**.
   ![imagem](/help/assets/assets/approve-old-ui.png)
1. Clique em **[!UICONTROL Salvar e fechar]**.

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   Da mesma forma, é possível aprovar ativos usando o [nova visualização de Ativos](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/manage-organize.html?lang=en#manage-asset-status).

## Aprovar ativos em massa {#bulk-approve-assets}

Simplifique o fluxo de trabalho aprovando rapidamente vários ativos de uma só vez. Você pode aprovar ativos em massa para acelerar o processo de aprovação, economizando tempo e melhorando a produtividade.
<br>Siga estas etapas para aprovar ativos em massa no [!DNL Experience Manager]:

1. Crie uma pasta no ambiente de criação (https://author-pXXX-eYYY.adobeaemcloud.com). Substituir _XXX_ com a ID do programa e _AAAA_ com a ID de ambiente do Experience Manager.
1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de metadados]**.
1. Clique em **[!UICONTROL Criar]** no lado superior direito da página.
1. Adicione um título de Perfil e clique em **[!UICONTROL Criar]**. O perfil de metadados foi criado com sucesso.
1. Selecione o perfil de metadados recém-criado e clique em **[!UICONTROL Editar _e)_]**. <br>A variável **[!UICONTROL Editar perfil de metadados]**o formulário é aberto com a variável **[!UICONTROL Básico]**guia realçada.
1. Arraste e solte uma **[!UICONTROL Campo de texto de uma linha]** do **[!UICONTROL Formulário de criação]** no lado direito à seção Metadados no formulário.
1. Clique no campo recém-adicionado e faça as seguintes atualizações no **[!UICONTROL Configurações]** painel:
   1. Altere o **[!UICONTROL Rótulo do campo]** para _Ativos aprovados_.
   1. Atualize o **[!UICONTROL Mapear para a propriedade]** para _./jcr:content/metadata/dam:status_.
   1. Altere o valor padrão para _aprovado_.

1. Clique em **[!UICONTROL Salvar]**.
1. No **[!UICONTROL Perfis de metadados]** selecione o perfil de metadados recém-criado.
1. Clique em **[!UICONTROL Aplicar perfil de metadados às pastas]** na barra de ação superior.
1. Selecione as pastas que você precisa aprovar e clique em **[!UICONTROL Aplicar]**.
   <br> A permissão para toda a pasta é definida para aprovação e qualquer ativo carregado nesta pasta é aprovado automaticamente.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>Essa abordagem aprova os ativos recém-criados na pasta. Para ativos existentes na pasta, é necessário selecionar e aprovar manualmente. <br> Como alternativa, você pode usar o **[!UICONTROL Reprocessar]** opção para aplicar as alterações do perfil de metadados aos ativos mais antigos.
