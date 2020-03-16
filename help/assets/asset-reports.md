---
title: Relatórios de ativos
description: Este artigo descreve vários relatórios sobre ativos nos ativos AEM e como gerar relatórios.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6998ee5f3c1c1563427e8739998effe0eba867fc

---


# Relatórios dos ativos {#asset-reports}

O relatório de ativos é uma ferramenta essencial para avaliar a utilidade da implantação dos ativos Adobe Experience Manager (AEM). Com os ativos AEM, você pode gerar uma variedade de relatórios em torno de seus ativos digitais. Os relatórios fornecem informações úteis sobre o uso do sistema, como os usuários interagem com ativos e quais ativos são baixados e compartilhados.

Use as informações nos relatórios para obter as principais métricas de sucesso para medir a adoção dos ativos AEM na sua empresa e pelos clientes.

A estrutura de relatórios do AEM Assets aproveita os trabalhos Sling para processar de forma assíncrona solicitações de relatório de maneira ordenada. É escalável para repositórios grandes. O processamento assíncrono de relatórios aumenta a eficiência e a velocidade com que os relatórios são gerados.

A interface de gerenciamento de relatórios é intuitiva e inclui opções e controles refinados para acessar relatórios arquivados e exibir status de execução de relatórios (sucesso, falha e enfileirados).

Quando um relatório é gerado, você é notificado por <!-- through an email (optional) and --> uma notificação de caixa de entrada. Você pode exibir, baixar ou excluir um relatório da página de listagem do relatório, onde todos os relatórios gerados anteriormente são exibidos.

## Gerar relatórios {#generate-reports}

O AEM Assets gera os seguintes relatórios padrão para você:

* Imagem
* Download
* Expiração
* Modificação
* Publicação
* Publicação do Brand Portal
* Uso do disco
* Arquivos
* Compartilhamento de link

Os administradores do AEM podem facilmente gerar e personalizar esses relatórios para sua implementação. Um administrador pode seguir estas etapas para gerar um relatório:

1. Toque/clique no logotipo do AEM e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.

   ![navegação](assets/navigation.png)

1. Na página Relatórios de ativos, toque/clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Na página **[!UICONTROL Criar relatório]** , escolha o relatório que deseja criar e toque/clique em **[!UICONTROL Avançar]**.

   ![choice_report](assets/choose_report.png)

   >[!NOTE]
   >
   >Antes de gerar um relatório **[!UICONTROL Ativo baixado]**, verifique se o serviço de Download de ativos está ativado. No console da Web (`https://[aem_server]:[port]/system/console/configMgr`), abra a configuração **[!UICONTROL Day CQ DAM Event Recorder]** e selecione a opção **[!UICONTROL Ativo baixado (BAIXADO)]** em Tipos de evento, se ainda não estiver selecionada.

   >[!NOTE]
   >
   >Por padrão, os Fragmentos de conteúdo e compartilhamentos de link são incluídos no relatório de Ativo baixado. Selecione a opção apropriada para criar um relatório de compartilhamentos de link ou para excluir Fragmentos de conteúdo do relatório de download.

1. Configure detalhes do relatório, como título, descrição, miniatura e caminho da pasta no repositório CRX onde o relatório é armazenado. Por padrão, o caminho da pasta é */content/dam*. Você pode especificar um caminho diferente.

   ![report_configuration](assets/report_configuration.png)

   Escolha o intervalo de datas para seu relatório.

   Você pode optar por gerar o relatório agora ou em uma data e hora futuras.

   >[!NOTE]
   >
   >Se você optar por agendar o relatório em uma data posterior, especifique a data e a hora no campo Data e hora. Se você não especificar nenhum valor, o mecanismo de relatório o tratará como um relatório que deve ser gerado instantaneamente.

   Os campos de configuração podem diferir com base no tipo de relatório que você cria.

   Por exemplo, o relatório Uso **[!UICONTROL de]** disco fornece opções para incluir representações de ativos ao calcular o espaço em disco usado pelos ativos. Você pode optar por incluir ou excluir ativos em subpastas para o cálculo de uso do disco.

   >[!NOTE]
   >
   >O relatório **[!UICONTROL Uso de disco]** não inclui campos de intervalo de datas porque indica apenas o uso atual do espaço em disco.

   ![disk_usage_configuration](assets/disk_usage_configuration.png)

   Ao criar o relatório **[!UICONTROL Arquivos]** , é possível incluir/excluir subpastas. No entanto, não é possível incluir representações de ativos para este relatório.

   ![files_report](assets/files_report.png)

   O relatório **[!UICONTROL Compartilhamento de links]** exibe URLs de ativos que são compartilhados com usuários externos a partir do AEM Assets. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. --> As colunas não são personalizáveis.

   O relatório **[!UICONTROL Compartilhamento de links]** não inclui opções para subpastas e representações porque apenas publica os URLs compartilhados que aparecem em */var/dam/share*.

   ![link_share](assets/link_share.png)

1. Toque/clique em **[!UICONTROL Avançar]** na barra de ferramentas.

1. Na página **[!UICONTROL Configurar colunas]** , algumas colunas são selecionadas para aparecerem no relatório por padrão. É possível selecionar colunas adicionais. Desmarque uma coluna selecionada para excluí-la no relatório.

   ![configure_columns](assets/configure_columns.png)

   Para exibir um nome de coluna ou caminho de propriedade personalizado, configure as propriedades para o binário de ativo no nó jcr:content no CRX. Como alternativa, adicione-o através do seletor de caminho de propriedade.

   ![custom_columns](assets/custom_columns.png)

1. Tap/click **[!UICONTROL Create]** from the toolbar. Uma mensagem notifica que a geração de relatórios foi iniciada.
1. Na página Relatórios de ativos, o status de geração de relatórios se baseia no estado atual do trabalho de relatório, por exemplo, Sucesso, Falha, Enfileirado ou Agendado. O mesmo status é exibido na caixa de entrada de notificações.

   Para exibir a página do relatório, toque/clique no link do relatório. Como alternativa, selecione o relatório e toque/clique no ícone Exibir na barra de ferramentas.

   ![report_page](assets/report_page.png)

   Toque/clique no ícone Download na barra de ferramentas para baixar o relatório no formato CSV.

## Adicionar colunas personalizadas {#add-custom-columns}

Você pode adicionar colunas personalizadas aos seguintes relatórios para exibir mais dados para seus requisitos personalizados:

* Imagem
* Download
* Expiração
* Modificação
* Publicação
* Publicação do Brand Portal
* Arquivos

1. Toque/clique no logotipo do AEM e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.
1. Na página Relatórios de ativos, toque/clique em **[!UICONTROL Criar]** na barra de ferramentas.

1. Na página **[!UICONTROL Criar relatório]** , escolha o relatório que deseja criar e toque/clique em **[!UICONTROL Avançar]**.
1. Configure detalhes do relatório, como título, descrição, miniatura, caminho da pasta, intervalo de datas e assim por diante, conforme aplicável.

1. Para exibir uma coluna personalizada, especifique o nome da coluna em **[!UICONTROL Colunas personalizadas]**.

   ![custom_columns-1](assets/custom_columns-1.png)

1. Adicione o caminho da propriedade sob o `jcr:content` nó no CRXDE usando o seletor de caminho da propriedade.

   ![property_picker](assets/property_picker.png)

   Como alternativa, digite o caminho no campo de caminho da propriedade.

   ![property_path](assets/property_path.png)

   Para adicionar mais colunas personalizadas, toque/clique em **[!UICONTROL Adicionar]** e repita as etapas 5 e 6.

1. Tap/click **[!UICONTROL Create]** from the toolbar. Uma mensagem notifica que a geração de relatórios foi iniciada.

## Configurar o serviço de remoção {#configure-purging-service}

Para remover relatórios que não são mais necessários, configure o serviço de Expurgação de relatórios do DAM do console da Web para expurgar os relatórios existentes com base na quantidade e idade.

1. Acesse o console da Web (gerenciador de configurações) de `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração do Serviço **[!UICONTROL de Expurgação de Relatório]** DAM.
1. Especifique a frequência (intervalo de tempo) do serviço de expurgação no `scheduler.expression.name` campo. Você também pode configurar a idade e o limite de quantidade para os relatórios.
1. Salve as alterações.
