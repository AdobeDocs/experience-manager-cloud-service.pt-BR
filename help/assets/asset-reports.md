---
title: Relatórios sobre uso e compartilhamento
description: Relatórios sobre seus ativos em [!DNL Adobe Experience Manager Assets] que ajudam a entender o uso, a atividade e o compartilhamento dos ativos digitais.
contentOwner: AG
feature: Relatórios de ativos, Gerenciamento de ativos
role: Administrator,Business Practitioner
exl-id: ef617b01-0019-4379-8d58-c03215d7e28f
source-git-commit: 088531133faa4c7f071a8c27fe11d1ccd5f50c0b
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 6%

---

# Relatórios de ativos {#asset-reports}

O relatório de ativos permite avaliar a utilidade da implantação [!DNL Adobe Experience Manager Assets]. Com [!DNL Assets], você pode gerar vários relatórios para seus ativos digitais. Os relatórios fornecem informações úteis sobre o uso do sistema, como os usuários interagem com ativos e quais ativos são <!-- downloaded and --> compartilhados.

Use as informações nos relatórios para derivar as métricas principais de sucesso para medir a adoção de [!DNL Assets] em sua empresa e por clientes.

A estrutura de relatórios [!DNL Assets] usa tarefas [!DNL Sling] para processar de forma assíncrona solicitações de relatórios de maneira ordenada. É escalável para repositórios grandes. O processamento assíncrono de relatórios aumenta a eficiência e a velocidade com que os relatórios são gerados.

A interface de gerenciamento de relatórios é intuitiva e inclui opções e controles otimizados para acessar relatórios arquivados e visualizar status de execução de relatórios (sucesso, falha e enfileirado).

Quando um relatório é gerado, você é notificado por meio de <!-- through an email (optional) and --> uma notificação de caixa de entrada. Você pode exibir, baixar ou excluir um relatório da página de listagem de relatório, onde todos os relatórios gerados anteriormente são exibidos.

## Gerar relatórios {#generate-reports}

[!DNL Experience Manager Assets] gera os seguintes relatórios padrão para você:

* Imagem
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

[!DNL Adobe Experience Manager] Os administradores do podem gerar e personalizar facilmente esses relatórios para sua implementação. Um administrador pode seguir estas etapas para gerar um relatório:

1. Na interface [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.

   ![Página Ferramentas para navegar no relatório de ativos](assets/navigation.png)

1. Na página [!UICONTROL Relatórios de ativos], clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Na página **[!UICONTROL Criar relatório]**, escolha o relatório que deseja criar e clique em **[!UICONTROL Próximo]**.

   ![Selecionar tipo de relatório](assets/choose_report.png)

1. Configure os detalhes do relatório, como título, descrição, miniatura e caminho da pasta no repositório CRX, onde o relatório é armazenado. Por padrão, o caminho da pasta é `/content/dam`. Você pode especificar um caminho diferente.

   ![Página para adicionar detalhes do relatório](assets/report_configuration.png)

   Escolha o intervalo de datas do seu relatório. Você pode optar por gerar o relatório agora ou em uma data e hora futuras.

   >[!NOTE]
   >
   >Se optar por agendar o relatório posteriormente, especifique a data e a hora nos campos Data e hora . Se você não especificar um valor, o mecanismo de relatório o tratará como um relatório que deve ser gerado instantaneamente.

   Os campos de configuração podem ser diferentes com base no tipo de relatório que você cria. Por exemplo, o relatório **[!UICONTROL Uso de disco]** fornece opções para incluir representações de ativos ao calcular o espaço em disco usado pelos ativos. Você pode optar por incluir ou excluir ativos em subpastas para o cálculo do uso do disco.

   >[!NOTE]
   >
   >O relatório **[!UICONTROL Uso de disco]** não inclui campos de intervalo de datas porque indica apenas o uso atual do espaço em disco.

   ![Página Detalhes do relatório de Uso de Disco](assets/disk_usage_configuration.png)

   Ao criar o relatório **[!UICONTROL Files]**, é possível incluir/excluir subpastas. No entanto, não é possível incluir representações de ativos para esse relatório.

   ![Página de detalhes do relatório Arquivos](assets/files_report.png)

   O relatório **[!UICONTROL Compartilhamento de links]** exibe URLs de ativos que são compartilhados com usuários externos a partir do [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> As colunas não são personalizáveis.

   O relatório **[!UICONTROL Compartilhamento de links]** não inclui opções para subpastas e representações porque apenas publica os URLs compartilhados que aparecem em `/var/dam/share`.

   ![Página de detalhes do relatório de Compartilhamento de links](assets/link_share.png)

1. Clique em **[!UICONTROL Avançar]** na barra de ferramentas.

1. Na página **[!UICONTROL Configurar colunas]**, algumas colunas são selecionadas para serem exibidas no relatório por padrão. Você pode selecionar mais colunas. Cancele a seleção de uma coluna para excluí-la no relatório.

   ![Selecionar ou cancelar seleção de colunas de relatório](assets/configure_columns.png)

   Para exibir um nome de coluna ou caminho de propriedade personalizado, configure as propriedades do binário de ativo no nó `jcr:content` no CRX. Como alternativa, adicione-o por meio do seletor de caminho de propriedade.

   ![Selecionar ou cancelar seleção de colunas de relatório](assets/custom_columns.png)

1. Clique em **[!UICONTROL Criar]** na barra de ferramentas. Uma mensagem notifica que a geração de relatório foi iniciada.
1. Na página [!UICONTROL Relatórios de Ativos], o status da geração de relatórios é baseado no estado atual do trabalho de relatório, por exemplo [!UICONTROL Sucesso], [!UICONTROL Falha], [!UICONTROL Em fila] ou [!UICONTROL Programado]. O mesmo status aparece na caixa de entrada de notificações.Para exibir a página do relatório, clique no link do relatório. Como alternativa, selecione o relatório e clique em **[!UICONTROL Exibir]** na barra de ferramentas.

   ![Um relatório gerado](assets/report_page.png)

   Clique em **[!UICONTROL Download]** na barra de ferramentas para baixar o relatório no formato CSV.

## Adicionar colunas personalizadas aos relatórios {#add-custom-columns}

Você pode adicionar colunas personalizadas aos seguintes relatórios para exibir mais dados para seus requisitos personalizados:

<!-- Remove download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Files
-->

* Imagem
* Expiração
* Modificação
* Publicação
* [!DNL Brand Portal] Publicar
* Arquivos

Para adicionar colunas personalizadas a esses relatórios, siga estas etapas:

1. No [!DNL Manager interface], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.
1. Na página [!UICONTROL Relatórios de ativos], clique em **[!UICONTROL Criar]** na barra de ferramentas.

1. Na página **[!UICONTROL Criar relatório]**, escolha um relatório a ser criado. Clique em **[!UICONTROL Avançar]**.

1. Configure os detalhes do relatório, como título, descrição, miniatura, caminho da pasta e intervalo de datas, conforme aplicável. Clique em **[!UICONTROL Avançar]**.

1. Selecione as informações aplicáveis na lista de **[!UICONTROL Colunas Padrão]**. Para exibir uma coluna personalizada, especifique o nome da coluna em **[!UICONTROL Colunas personalizadas]**.

   ![Especificar o nome da coluna personalizada do relatório](assets/custom_columns-1.png)

1. Adicione o caminho da propriedade no nó `jcr:content` no CRXDE usando o seletor de caminho de propriedade. Como alternativa, digite o caminho no campo do caminho da propriedade.

   ![Mapear o caminho da propriedade de caminhos em jcr:content](assets/property_picker.png)

   Para adicionar mais colunas personalizadas, clique em **[!UICONTROL Adicionar]** e repita as etapas acima.

1. Clique em **[!UICONTROL Criar]** na barra de ferramentas. Uma mensagem notifica que a geração de relatórios foi iniciada.

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## Informações de solução de problemas {#tips-troubleshoot}

* Se o [!UICONTROL Relatório de uso de disco] não for gerado e se você estiver usando [!DNL Dynamic Media], verifique se todos os ativos estão funcionando corretamente. Para resolver, reprocesse os ativos e gere o relatório novamente.

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
