---
title: Configurar uma conta de alias de empresa do Dynamic Media
description: Saiba como configurar uma conta empresarial alternativa no Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 886063d4-71dd-48c8-a342-884ad2c111ca
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---

# Sobre a configuração de uma conta alias de empresa do Dynamic Media {#about-dm-alias-acct}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas de metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>documentação para desenvolvedores do AEM Assets</b></a>
        </td>
    </tr>
</table>

<!-- hide: yes
hidefromtoc: yes -->

<!-- >[!NOTE]
>
>This feature to create a Dynamic Media company alias account is in the Prerelease Channel for January 2022. See [Prerelease Channel documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#enable-prerelease) for information on how to enable the feature for your environment. The feature is generally available in the February 2022 release. -->

Os URLs do Dynamic Media e o código de inserção do visualizador contêm o nome da conta da empresa. Esse nome de conta foi criado no momento do provisionamento do Dynamic Media. Pode haver cenários em que sua empresa tenha passado por uma aquisição ou reformulação da marca, ou em que você deseje simplesmente usar um nome mais fácil de memorizar. Nesses cenários, não é fácil atualizar manualmente o nome da conta da empresa em todos os URLs e o código de inserção do visualizador que aparece imediatamente. Além disso, há a possibilidade de que você afete o repositório existente do Dynamic Media ou o conteúdo ao vivo. Para resolver esse problema, você pode configurar uma conta alias de empresa do Dynamic Media.

Uma conta alias de empresa do Dynamic Media garante que todos os URLs do Dynamic Media e o código de inserção do visualizador na interface do usuário reflitam todas as atualizações feitas no contexto comercial, como a reformulação da marca. Uma conta alias também tem um impacto positivo na SEO (Otimização do mecanismo de pesquisa), pois os URLs do Dynamic Media e o código de inserção do visualizador refletem o novo nome de conta da empresa.

Ao configurar uma conta alias de empresa do Dynamic Media, esteja ciente do seguinte:

* Qualquer URL ou código de inserção de visualizador existente do Dynamic Media nas suas propriedades digitais do *live* deve ser atualizado manualmente para refletir o novo nome de alias. No entanto, todos os URLs ou visualizadores incorporam o código ao nome original da empresa do Dynamic Media continuam a funcionar para ativos existentes ou novos.
* O recurso de conta alias da empresa Dynamic Media é limitado ao modo de criação e entrega do Experience Manager Assets. O alias da empresa não funciona com o Experience Manager Sites. Os componentes do WCM (Web Content Management, gerenciamento de conteúdo da Web) não são atualizados para essa alteração. Esses componentes continuam a funcionar com o nome original da empresa do Dynamic Media para buscar ativos do Dynamic Media.
* Você pode configurar apenas uma conta alias de empresa na página **[!UICONTROL Editar configuração do Dynamic Media]**. No entanto, você pode criar quantas contas de alias de empresa desejar por meio de um caso de suporte e refletir manualmente o nome do alias necessário nos URLs do Dynamic Media ou no código de inserção do visualizador.
* O recurso [Invalidação de cache](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md) pronto para uso do Dynamic Media invalida as URLs com contas de Alias de Empresa e de Empresa configuradas na página Configuração do Dynamic Media no Cloud Services.
* Ao configurar uma conta alias de empresa na página **[!UICONTROL Editar Configuração do Dynamic Media]**, para que a invalidação de cache seja bem-sucedida, você deve invalidar simultaneamente as URLs de *ambas* a conta da **[!UICONTROL Empresa]** e o **[!UICONTROL Alias da Empresa]**.

Consulte também [Criar uma configuração de mídia dinâmica no Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)

## Configurar uma conta de alias de empresa do Dynamic Media {#configure-dm-alias-account}

Você começa a configurar uma conta alias de empresa do Dynamic Media enviando primeiro um caso de suporte. Esta etapa é obrigatória.

1. [Use o Admin Console para criar um caso de suporte](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).
1. Forneça as seguintes informações no seu caso de suporte:

   * O alias da empresa do Dynamic Media que você deseja usar. O nome deve conter *somente* letras (maiúsculas e minúsculas mistas permitidas), números, hifens e sublinhados.
   * Sua região.
   * Se algum [conjunto de regras](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md) está sendo usado anteriormente para obter a veiculação de conteúdo do Dynamic Media por meio de um nome de conta de empresa alternativo do Dynamic Media.

1. Depois que a conta alias do Dynamic Media for criada pelo suporte, na instância do autor do Experience Manager as a Cloud Service, selecione o logotipo do Experience Manager as a Cloud Service para acessar o console de navegação global.
1. À esquerda do console, selecione o ícone Ferramentas e vá para **[!UICONTROL Cloud Services > Configuração do Dynamic Media]**.
1. Na página Navegador de configuração do Dynamic Media, no painel esquerdo, selecione **[!UICONTROL global]** (não selecione o ícone de pasta à esquerda de **[!UICONTROL global]**). Em seguida, selecione **[!UICONTROL Editar]**.

   ![Campo de texto Alias da empresa do Dynamic Media](/help/assets/assets-dm/dm-company-alias.png)

1. Na página **[!UICONTROL Editar Configuração do Dynamic Media]**, no campo de texto **[!UICONTROL Alias da Empresa]**, digite o nome da conta de alias do Dynamic Media que você especificou anteriormente no caso de suporte.
1. No canto superior direito da página, selecione **[!UICONTROL Salvar]**.
A conta alias da empresa Dynamic Media agora é salva e ativada; todos os URLs e o código incorporado do visualizador para ativos existentes e novos agora refletem o novo nome alias da empresa.