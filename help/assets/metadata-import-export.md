---
title: Importar e exportar metadados de ativos em massa
description: Este artigo descreve como importar e exportar metadados em massa.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: fb70a068-3ba3-4459-952d-79155d286c42
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 13%

---

# Importar e exportar metadados de ativos em massa {#import-and-export-asset-metadata-in-bulk}

O Adobe Experience Manager Assets permite importar metadados de ativos em massa usando um arquivo CSV. Você pode fazer atualizações em massa para os ativos carregados recentemente ou os ativos existentes importando um arquivo CSV. Você também pode assimilar metadados de ativos em massa de sistemas de terceiros no formato CSV.

## Importar metadados {#import-metadata}

A importação de metadados é assíncrona e não impede o desempenho do sistema. A atualização simultânea dos metadados de vários ativos pode consumir muitos recursos devido à atividade de writeback de metadados usando microsserviços de ativos. a Adobe recomenda que você planeje quaisquer operações em massa durante o uso do servidor enxuto, para que o desempenho de outros usuários não seja afetado.

>[!NOTE]
>
>Para importar metadados em namespaces personalizados, primeiro registre os namespaces.

1. Navegue até [!DNL Assets] interface do usuário, selecione **[!UICONTROL Criar]** na barra de ferramentas e selecione **[!UICONTROL Metadados]** no menu.
1. No **[!UICONTROL Importação de metadados]** clique em **[!UICONTROL Selecionar arquivo]**. Selecione o arquivo CSV com os metadados.
1. Forneça os seguintes parâmetros:

   | Parâmetro | Descrição |
   | ---------------------- | ------- |
   | Tamanho do lote | Número de ativos em um lote para o qual os metadados devem ser importados. O valor padrão é 50. O valor máximo é 100. |
   | Separador de campos | O valor padrão é `,` (vírgula). Você pode especificar qualquer outro caractere. |
   | Delimitador de vários valores | Separador para valores de metadados. O valor padrão é `|`. |
   | Inicializar fluxos de trabalho | Falso por padrão. Quando definido como `true` As configurações padrão e estão em vigor para o fluxo de trabalho DAM Metadata WriteBack (que grava metadados nos dados binários do XMP). Habilitar os fluxos de trabalho torna o sistema lento. |
   | Nome de coluna do caminho do ativo | Define o nome da coluna do arquivo CSV com ativos. |

1. Selecionar **[!UICONTROL Importar]** na barra de ferramentas. Depois que os metadados forem importados, uma notificação será enviada para sua caixa de entrada de Notificações. Navegue até a página de propriedades do ativo e verifique se os valores de metadados são importados corretamente para os ativos.

1. Para adicionar data e hora para importar os metadados, use `YYYY-MM-DDThh:mm:ss.fff-00:00` formato para data e hora. A data e a hora são separadas por `T`, `hh` é horas no formato de 24 horas, `fff` é nanossegundos e `-00:00` é deslocamento de fuso horário. Por exemplo, `2020-03-26T11:26:00.000-07:00` é 26 de março de 2020 às 11:26:00.000 PST.

   * O formato de data depende do cabeçalho da coluna e do formato nela contido. Por exemplo, se a data for compatível com o formato `yyyy-MM-dd'T'HH:mm:ssXXX` o cabeçalho da respectiva coluna deve ser `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`.
   * O formato de data padrão é `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`.

<!-- Hidden via cqdoc-17869>

>[!CAUTION]
>
>If the date format does not match `YYYY-MM-DDThh:mm:ss.fff-00:00`, the date values are not set. The date formats of exported metadata CSV file is in the format `YYYY-MM-DDThh:mm:ss-00:00`. If you want to import it, convert it to the acceptable format by adding the nanoseconds value denoted by `fff`.
-->

## Exportar metadados {#export-metadata}

É possível exportar metadados de vários ativos em um formato CSV. Os metadados são exportados de forma assíncrona e não afetam o desempenho do sistema. Para exportar metadados, o Experience Manager atravessa as propriedades do nó do ativo `jcr:content/metadata` e seus nós filhos e exporta as propriedades de metadados em um arquivo CSV.

Alguns casos de uso para exportar metadados em massa são:

* Importe os metadados em um sistema de terceiros ao migrar ativos.
* Compartilhar metadados de ativos com uma equipe de projeto maior.
* Testar ou auditar os metadados quanto à conformidade.
* Externalize os metadados para localização separada.

1. Selecione a pasta de ativos que contém ativos para os quais deseja exportar metadados. Na barra de ferramentas, selecione **[!UICONTROL Exportar metadados]**.
1. Na caixa de diálogo Exportação de metadados, especifique um nome para o arquivo CSV. Para exportar metadados de ativos em subpastas, selecione **[!UICONTROL Incluir ativos em subpastas]**.

   ![Interface e opções para exportar metadados de todos os ativos em uma pasta](assets/export_metadata_page.png "Interface e opções para exportar metadados de todos os ativos em uma pasta")

1. Selecione as opções desejadas. Forneça um nome de arquivo e se necessário uma data.

1. No **[!UICONTROL Propriedades a serem exportadas]** especifique se deseja exportar todas as propriedades ou propriedades específicas. Se você escolher Propriedades seletivas para serem exportadas, adicione as propriedades desejadas.

1. Na barra de ferramentas, toque/clique **[!UICONTROL Exportar]**. Uma mensagem confirma que os metadados foram exportados. Feche a mensagem.
1. Abra a notificação da caixa de entrada do trabalho de exportação. Selecione o trabalho e clique em **[!UICONTROL Abrir]** na barra de ferramentas. Para baixar o arquivo CSV com os metadados, toque/clique em **[!UICONTROL Download de CSV]** na barra de ferramentas. Clique em **[!UICONTROL Fechar]**.

   ![Caixa de diálogo para baixar o arquivo CSV que contém metadados exportados em massa](assets/csv_download.png)

   *Figura: caixa de diálogo para baixar o arquivo CSV que contém metadados exportados em massa.*

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)

>[!MORELIKETHIS]
>
>* [Importar metadados ao importar ativos em massa](/help/assets/add-assets.md#asset-bulk-ingestor)

