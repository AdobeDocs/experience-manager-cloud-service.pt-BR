---
title: Relatórios no Dynamic Media
description: Saiba como solicitar um relatório de erros para o Dynamic Media delivery URLs que falham.
contentOwner: Rick Brough
feature: Asset Management
role: User
hide: true
hidefromtoc: true
exl-id: 2488f813-df15-4dbb-8747-f827ee5925e1
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Solicitar um relatório de erros para URLs de entrega do Dynamic Media que falham

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

Você pode solicitar um relatório de erro que identifica os URLs do Dynamic Media que falharam no momento do delivery. O relatório é um agregado de dados de até cinco dias e está disponível em formato CSV. O relatório de erros inclui as seguintes informações:

* Falha no URL de entrega do Dynamic Media - Um URL com falha é um URL gerado pelo Dynamic Media que não pode produzir conteúdo no momento da entrega.
* URL do referenciador - O URL do referenciador do qual o URL de entrega com falha é chamado.
* Contagem de falhas - O número de vezes que o URL de entrega foi carregado que resultou em uma falha.

Ao solicitar o relatório de erros, a equipe do Dynamic Media da Adobe envia-o por email, no formato CSV. Abrange um período de cinco dias a partir do dia em que o seu pedido foi feito.

Você pode solicitar um relatório de erros uma vez por mês para uma determinada empresa.

**Para solicitar um relatório de erro para URLs de entrega do Dynamic Media que falharam:**

1. [Envie um email para reports-dynamic-media@adobe.com](mailto:reports-dynamic-media@adobe.com) com o nome da empresa associado à sua conta do Dynamic Media.

   Se você não souber o nome da empresa, consulte a página [Configuração do Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html?lang=pt-BR#configuring-dynamic-media-cloud-services) em **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração do Dynamic Media]**. Na página Navegador de configuração do Dynamic Media, clique em **[!UICONTROL global]**, marque a caixa de seleção *[Dynamic_Media_folder_icon]* e selecione **[!UICONTROL Editar]**. Você deve ter direitos de Administrador no AEM para acessar a página Configuração do Dynamic Media.

   ![Acessando a página Configuração do Dynamic Media.](/help/assets/dynamic-media/assets/reporting-accessdmconfig.png)
