---
title: Gerenciar relatórios na visualização do Assets
description: Acesse os dados na seção de relatórios da visualização do Assets para avaliar o uso de produtos e recursos e obter insights sobre as principais métricas de sucesso.
exl-id: c7155459-05d9-4a95-a91f-a1fa6ae9d9a4
source-git-commit: df82681338f8ca1a34df6118cbddc6642aa8d4b5
workflow-type: ht
source-wordcount: '814'
ht-degree: 100%

---

# Gerenciamento de relatórios {#manage-reports}

>[!CONTEXTUALHELP]
>id="assets_reports"
>title="Relatórios"
>abstract="Os relatórios de ativos fornecem à administração a visibilidade das atividades do ambiente de visualização do Adobe Experience Manager Assets. Esses dados fornecem informações úteis sobre como os usuários interagem com o conteúdo e o produto. Todos os usuários atribuídos ao perfil de produto de administradores podem acessar o painel Insights ou criar relatórios definidos pelo usuário."

Os relatórios do Assets fornecem à administração a visibilidade das atividades do ambiente de visualização do Adobe Experience Manager Assets. Esses dados fornecem informações úteis sobre como os usuários interagem com o conteúdo e o produto.

## Acessar relatórios {#access-reports}

Todos os usuários atribuídos ao perfil de produto de administradores da visualização do Assets podem acessar o painel Insights e criar relatórios definidos pelo usuário na visualização do Assets.

## Exibir o Insights {#view-live-statistics}

A visualização do Assets permite visualizar dados do seu ambiente da visualização do Assets em tempo real, por meio do painel Insights. Você pode visualizar métricas de evento em tempo real dos últimos 30 dias ou dos últimos 12 meses.

![Opções da barra de ferramentas ao selecionar um ativo](assets/assets-essentials-live-statistics.png)

Clique na opção **[!UICONTROL Insights]**, disponível no painel de navegação esquerdo, para exibir os seguintes gráficos gerados automaticamente:

* **Downloads**: o número de arquivos baixados do ambiente de visualização do Assets nos últimos 30 dias ou 12 meses representados por meio de um gráfico de linhas.

* **Uploads**: o número de arquivos enviados para o ambiente de visualização do Assets nos últimos 30 dias ou 12 meses representados por meio de um gráfico de linhas.

* **Principais Pesquisas**: visualize os principais termos pesquisados junto com o número de vezes que esses termos foram pesquisados no ambiente de visualização do Assets nos últimos 30 dias ou 12 meses representados em formato de tabela.

<!--

* **Storage usage**: The storage usage, in gigabytes (GB), for the Assets view environment, for the last 30 days or 12 months represented using a bar chart.

-->

## Criar um relatório de downloads {#create-download-report}

Para criar um relatório de downloads:

1. Navegue até **[!UICONTROL Configurações]** > **[!UICONTROL Relatórios]** e clique em **[!UICONTROL Criar relatório]**.

1. Na guia [!UICONTROL Configuração], especifique o tipo de relatório como **[!UICONTROL Baixar]**.

1. Especifique um título e uma descrição opcional para o relatório.

1. Selecione o caminho da pasta que compreende os ativos para os quais o relatório será criado, usando o campo **[!UICONTROL Selecionar caminho da pasta]**.

1. Selecione o intervalo de datas do relatório.

   >[!NOTE]
   >
   > A visualização do Assets converte todos os fusos horários locais para o Tempo Universal Coordenado (UTC).

1. Na guia [!UICONTROL Colunas], selecione os nomes das colunas que devem ser exibidas no relatório.

1. Clique em **[!UICONTROL Criar]**.

   ![Baixar relatório](assets/download-reports-config.png)

A tabela a seguir explica o uso de todas as colunas que você pode adicionar ao relatório:

<table>
    <tbody>
     <tr>
      <th><strong>Nome da coluna</strong></th>
      <th><strong>Descrição</strong></th>
     </tr>
     <tr>
      <td>Título</td>
      <td>O título do ativo.</td>
     </tr>
     <tr>
      <td>Caminho </td>
      <td>O caminho da pasta onde o ativo está disponível na visualização do Assets.</td>
     </tr>
     <tr>
      <td>Tipo MIME</td>
      <td>O tipo MIME do ativo.</td>
     </tr>
     <tr>
      <td>Tamanho</td>
      <td>O tamanho do ativo em bytes.</td>
     </tr>
     <tr>
      <td>Baixado por</td>
      <td>A ID do email do usuário que baixou o ativo.</td>
     </tr>
     <tr>
      <td>Data de download</td>
      <td>A data em que a ação de download do ativo foi executada.</td>
     </tr>
     <tr>
      <td>Autor</td>
      <td>O autor do ativo.</td>
     </tr>
     <tr>
      <td>Data de criação</td>
      <td>A data em que o ativo foi enviado para a visualização do Assets.</td>
     </tr>
     <tr>
      <td>Data da modificação</td>
      <td>A data em que o ativo foi modificado pela última vez.</td>
     </tr>
     <tr>
      <td>Expirado</td>
      <td>O status de expiração do ativo.</td>
     </tr>
     <tr>
      <td>Baixado por Nome de usuário</td>
      <td>O nome do usuário que baixou o ativo.</td>
     </tr>           
    </tbody>
   </table>

## Criar um relatório de uploads {#create-upload-report}

Para criar um relatório de uploads:

1. Navegue até **[!UICONTROL Configurações]** > **[!UICONTROL Relatórios]** e clique em **[!UICONTROL Criar relatório]**.

1. Na guia [!UICONTROL Configuração], especifique o tipo de relatório como **[!UICONTROL Fazer upload]**.

1. Especifique um título e uma descrição opcional para o relatório.

1. Selecione o caminho da pasta que compreende os ativos para os quais o relatório será criado, usando o campo **[!UICONTROL Selecionar caminho da pasta]**.

1. Selecione o intervalo de datas do relatório.

1. Na guia [!UICONTROL Colunas], selecione os nomes das colunas que devem ser exibidas no relatório.

1. Clique em **[!UICONTROL Criar]**.

   ![Relatório de uploads](assets/upload-reports-config.png)

A tabela a seguir explica o uso de todas as colunas que você pode adicionar ao relatório:

<table>
    <tbody>
     <tr>
      <th><strong>Nome da coluna</strong></th>
      <th><strong>Descrição</strong></th>
     </tr>
     <tr>
      <td>Título</td>
      <td>O título do ativo.</td>
     </tr>
     <tr>
      <td>Caminho </td>
      <td>O caminho da pasta onde o ativo está disponível na visualização do Assets.</td>
     </tr>
     <tr>
      <td>Tipo MIME</td>
      <td>O tipo MIME do ativo.</td>
     </tr>
     <tr>
      <td>Tamanho</td>
      <td>O tamanho do ativo.</td>
     </tr>
     <tr>
      <td>Autor</td>
      <td>O autor do ativo.</td>
     </tr>
     <tr>
      <td>Data de criação</td>
      <td>A data em que o ativo foi enviado para a visualização do Assets.</td>
     </tr>
     <tr>
      <td>Data da modificação</td>
      <td>A data em que o ativo foi modificado pela última vez.</td>
     </tr>
     <tr>
      <td>Expirado</td>
      <td>O status de expiração do ativo.</td>
     </tr>              
    </tbody>
   </table>

## Visualizar relatórios existentes {#view-report-list}

Depois de [criar o relatório](#create-download-report), é possível visualizar a lista de relatórios existentes e baixá-los em formato CSV ou excluí-los.

Para visualizar a lista de relatórios, navegue até **[!UICONTROL Configurações]** > **[!UICONTROL Relatórios]**.

É possível visualizar o título, o tipo, a descrição especificada durante a criação, o status, a ID de email do autor e a data de criação de cada relatório.

O status `Completed ` do relatório significa que ele está pronto para download.

![Lista de relatórios](assets/list-of-reports.png)


## Baixar um relatório em formato CSV {#download-csv-report}

Para baixar um relatório no formato CSV:

1. Navegue até **[!UICONTROL Configurações]** > **[!UICONTROL Relatórios]**.

1. Selecione um relatório e clique em **[!UICONTROL Baixar CSV]**.

O relatório selecionado é baixado no formato CSV. As colunas exibidas no relatório CSV dependem das colunas selecionadas ao [criar o relatório](#create-download-report).

## Excluir um relatório {#delete-report}

Para excluir um relatório:

1. Navegue até **[!UICONTROL Configurações]** > **[!UICONTROL Relatórios]**.

1. Selecione um relatório e clique em **[!UICONTROL Excluir]**.

1. Clique em **[!UICONTROL Excluir]** novamente para confirmar.
