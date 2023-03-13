---
title: Relatórios sobre uso e compartilhamento
description: Relatórios sobre seus ativos no [!DNL Adobe Experience Manager Assets] que ajudam você a entender o uso, a atividade e o compartilhamento de seus ativos digitais.
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: ef617b01-0019-4379-8d58-c03215d7e28f
source-git-commit: 5da3ca6a175e7e6d8a2c3ca568885ceeee5c3d06
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 6%

---

# Relatórios de ativos {#asset-reports}

Os relatórios de ativos permitem avaliar a utilidade do [!DNL Adobe Experience Manager Assets] implantação. Com [!DNL Assets], você pode gerar vários relatórios para seus ativos digitais. Os relatórios fornecem informações úteis sobre o uso do sistema, como os usuários interagem com os ativos e quais ativos são <!-- downloaded and --> compartilhados.

Use as informações nos relatórios para obter as principais métricas de sucesso e medir a adoção de [!DNL Assets] em sua empresa e por clientes.

A variável [!DNL Assets] usos da estrutura de relatórios [!DNL Sling] processos para processar solicitações de relatório de forma assíncrona e ordenada. Ele é escalável para repositórios grandes. O processamento assíncrono de relatórios aumenta a eficiência e a velocidade com que os relatórios são gerados.

A interface de gerenciamento de relatórios é intuitiva e inclui opções e controles refinados para acessar relatórios arquivados e exibir status de execução de relatórios (bem-sucedido, com falha e em fila).

Quando um relatório é gerado, você é notificado por meio de <!-- through an email (optional) and --> uma notificação na caixa de entrada. É possível visualizar, baixar ou excluir um relatório da página de listagem de relatórios, na qual todos os relatórios gerados anteriormente são exibidos.

## Gerar relatórios {#generate-reports}

[!DNL Experience Manager Assets] O gera os seguintes relatórios padrão para você:

* Upload
* Download
* Expiração
* Modificação
* Publicação
* [!DNL Brand Portal] Publicar
* Uso do disco
* Arquivos
* Compartilhamento de link

<!-- Removed download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Disk Usage
* Files
* Link Share
-->

[!DNL Adobe Experience Manager] os administradores podem gerar e personalizar facilmente esses relatórios para sua implementação. Um administrador pode seguir estas etapas para gerar um relatório:

1. Entrada [!DNL Experience Manager] clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Relatórios]**.

   ![Página Ferramentas para navegar pelo relatório de ativos](assets/navigation.png)

1. No [!UICONTROL Relatórios de ativos] clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. No **[!UICONTROL Criar relatório]** escolha o relatório que deseja criar e clique em **[!UICONTROL Próxima]**.

   ![Selecionar tipo de relatório](assets/choose_report.png)

1. Configure os detalhes do relatório, como título, descrição, miniatura e caminho da pasta. Por padrão, o caminho da pasta é `/content/dam`. Você pode especificar um caminho diferente para executar o relatório em uma pasta específica.

   ![Página para adicionar detalhes do relatório](assets/report_configuration.png)

   Escolha o intervalo de datas do relatório. Você pode optar por gerar o relatório agora ou em uma data e hora futuras.

   >[!NOTE]
   >
   >Se optar por agendar o relatório posteriormente, certifique-se de especificar a data e a hora nos campos Data e Hora. Se você não especificar nenhum valor, o mecanismo de relatório o tratará como um relatório a ser gerado instantaneamente.

   Os campos de configuração podem diferir de acordo com o tipo de relatório que você cria. Por exemplo, a variável **[!UICONTROL Uso do disco]** O relatório de fornece opções para incluir representações de ativos ao calcular o espaço em disco usado pelos ativos. Você pode optar por incluir ou excluir ativos em subpastas para cálculo de uso do disco.

   >[!NOTE]
   >
   >O relatório **[!UICONTROL Uso de disco]** não inclui campos de intervalo de datas porque indica apenas o uso atual do espaço em disco.

   ![Página de detalhes do relatório de Uso de disco](assets/disk_usage_configuration.png)

   Ao criar a variável **[!UICONTROL Arquivos]** incluir/excluir subpastas. No entanto, não é possível incluir representações de ativos neste relatório.

   ![Página de detalhes do relatório Arquivos](assets/files_report.png)

   O relatório **[!UICONTROL Compartilhamento de links]** exibe URLs de ativos que são compartilhados com usuários externos a partir do [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> As colunas não são personalizáveis.

   A variável **[!UICONTROL Compartilhamento de link]** relatório, não inclui opções para subpastas e representações porque apenas publica os URLs compartilhados que aparecem em `/var/dam/share`.

   ![Página de detalhes do relatório Compartilhamento de links](assets/link_share.png)

1. Clique em **[!UICONTROL Próxima]** na barra de ferramentas.

1. No **[!UICONTROL Configurar colunas]** algumas colunas são selecionadas para aparecer no relatório por padrão. Você pode selecionar mais colunas. Cancele a seleção de uma coluna para excluí-la no relatório.

   ![Selecionar ou cancelar a seleção de colunas do relatório](assets/configure_columns.png)

   Para exibir um nome de coluna ou caminho de propriedade personalizado, configure as propriedades para o binário de ativo no `jcr:content` no CRX. Como alternativa, adicione-o por meio do seletor de caminho de propriedade.

   ![Selecionar ou cancelar a seleção de colunas do relatório](assets/custom_columns.png)

1. Clique em **[!UICONTROL Criar]** na barra de ferramentas. Uma mensagem notifica que a geração de relatório foi iniciada.
1. No [!UICONTROL Relatórios de ativos] página, o status de geração de relatório é baseado no estado atual do trabalho de relatório, por exemplo [!UICONTROL Sucesso], [!UICONTROL Failed], [!UICONTROL Em fila]ou [!UICONTROL Agendado]. O mesmo status aparece na caixa de entrada de notificações.Para exibir a página do relatório, clique no link do relatório. Como alternativa, selecione o relatório e clique em **[!UICONTROL Exibir]** na barra de ferramentas.

   ![Um relatório gerado](assets/report_page.png)

   Clique em **[!UICONTROL Baixar]** na barra de ferramentas para baixar o relatório no formato CSV.

   >[!NOTE]
   >
   >Você pode gerar relatórios com base nos eventos gerados durante os últimos 360 dias. O Experience Manager retém os dados da ID do usuário por 30 dias.

## Adicionar colunas personalizadas aos relatórios {#add-custom-columns}

Você pode adicionar colunas personalizadas aos seguintes relatórios para exibir mais dados de acordo com seus requisitos personalizados:

<!-- Remove download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Files
-->

* Upload
* Expiração
* Modificação
* Publicação
* [!DNL Brand Portal] Publicar
* Arquivos

Para adicionar colunas personalizadas a esses relatórios, siga estas etapas:

1. No [!DNL Manager interface], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Relatórios]**.
1. No [!UICONTROL Relatórios de ativos] clique em **[!UICONTROL Criar]** na barra de ferramentas.

1. No **[!UICONTROL Criar relatório]** escolha um relatório para criar. Clique em **[!UICONTROL Avançar]**.

1. Configure os detalhes do relatório, como título, descrição, miniatura, caminho da pasta e intervalo de datas, conforme aplicável. Clique em **[!UICONTROL Avançar]**.

1. Selecione as informações aplicáveis na lista de **[!UICONTROL Colunas padrão]**. Para exibir uma coluna personalizada, especifique o nome da coluna em **[!UICONTROL Colunas personalizadas]**.

   ![Especificar o nome da coluna personalizada do relatório](assets/custom_columns-1.png)

1. Adicione o caminho da propriedade sob o `jcr:content` no CRXDE usando o seletor de caminho de propriedade. Como alternativa, digite o caminho no campo caminho da propriedade.

   ![Mapeie o caminho da propriedade a partir de caminhos em jcr:content](assets/property_picker.png)

   Para adicionar mais colunas personalizadas, clique em **[!UICONTROL Adicionar]** e repita as etapas acima.

1. Clique em **[!UICONTROL Criar]** na barra de ferramentas. Uma mensagem notifica que a geração de relatório foi iniciada.

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## Informações de solução de problemas {#tips-troubleshoot}

* Se a variável [!UICONTROL Relatório de uso do disco] não gera e se estiver usando [!DNL Dynamic Media], certifique-se de que todos os ativos prossigam corretamente. Para resolver, reprocesse os ativos e gere o relatório novamente.

<!-- These notes were present in generate report section above. Removing commented text from in between the instructions to preserve the numbering of the ordered list.

TBD: How do enable this in CS now? Is it done using some OSGi config now?
   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.
-->

<!-- Removed download report.
   >[!NOTE]
   >
   >By default, the Content Fragments and link shares are included in the asset [!UICONTROL Download] report. Select the appropriate option to create a report of link shares or to exclude Content Fragments from the download report.

   >[!NOTE]
   >
   >The [!UICONTROL Download] report displays details of only those assets which are downloaded after selecting individually or are downloaded using Quick Action. However, it does not include the details of the assets that are inside a downloaded folder.
-->
