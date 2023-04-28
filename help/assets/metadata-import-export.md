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

O Adobe Experience Manager Assets permite importar metadados de ativos em massa usando um arquivo CSV. É possível fazer atualizações em massa dos ativos recém-carregados ou dos ativos existentes ao importar um arquivo CSV. Também é possível assimilar metadados de ativos em massa de sistemas de terceiros no formato CSV.

## Importar metadados {#import-metadata}

A importação de metadados é assíncrona e não impede o desempenho do sistema. A atualização simultânea dos metadados para vários ativos pode exigir muitos recursos devido à atividade de gravação de metadados que usa microsserviços de ativos. O Adobe recomenda que você planeje quaisquer operações em massa durante o uso de servidor simplificado para que o desempenho para outros usuários não seja afetado.

>[!NOTE]
>
>Para importar metadados em namespaces personalizados, primeiro registre os namespaces.

1. Navegar para [!DNL Assets] interface do usuário, selecione **[!UICONTROL Criar]** na barra de ferramentas e selecione **[!UICONTROL Metadados]** no menu .
1. No **[!UICONTROL Importação de metadados]** página, clique em **[!UICONTROL Selecionar arquivo]**. Selecione o arquivo CSV com os metadados.
1. Forneça os seguintes parâmetros:

   | Parâmetro | Descrição |
   | ---------------------- | ------- |
   | Tamanho do lote | Número de ativos em um lote para o qual os metadados devem ser importados. O valor padrão é 50. O valor máximo é 100. |
   | Separador de campos | O valor padrão é `,` (vírgula). É possível especificar qualquer outro caractere. |
   | Delimitador de vários valores | Separador para valores de metadados. O valor padrão é `|`. |
   | Inicializar fluxos de trabalho | False por padrão. Quando definido como `true` e as configurações padrão estão em vigor para o fluxo de trabalho WriteBack de metadados de DAM (que grava metadados nos dados de XMP binários). Habilitar os workflows atrasa o sistema. |
   | Nome de coluna do caminho do ativo | Define o nome da coluna para o arquivo CSV com ativos. |

1. Selecionar **[!UICONTROL Importar]** na barra de ferramentas. Depois que os metadados são importados, uma notificação é enviada para a sua caixa de entrada de Notificação. Navegue até a página de propriedade do ativo e verifique se os valores de metadados foram importados corretamente para os ativos.

1. Para adicionar data e carimbo de data e hora para importar os metadados, use `YYYY-MM-DDThh:mm:ss.fff-00:00` para data e hora. A data e a hora são separadas por `T`, `hh` é horas no formato de 24 horas, `fff` é nanossegundos e `-00:00` é deslocamento de fuso horário. Por exemplo, `2020-03-26T11:26:00.000-07:00` é 26 de março de 2020 às 11:26:00.000 AM PST.

   * O formato de data depende do cabeçalho da coluna e do formato nela. Por exemplo, se a data for reclamação com formato `yyyy-MM-dd'T'HH:mm:ssXXX` em seguida, o respectivo cabeçalho da coluna deve ser `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`.
   * O formato de data padrão é `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`.

<!-- Hidden via cqdoc-17869>

>[!CAUTION]
>
>If the date format does not match `YYYY-MM-DDThh:mm:ss.fff-00:00`, the date values are not set. The date formats of exported metadata CSV file is in the format `YYYY-MM-DDThh:mm:ss-00:00`. If you want to import it, convert it to the acceptable format by adding the nanoseconds value denoted by `fff`.
-->

## Exportar metadados {#export-metadata}

Você pode exportar metadados para vários ativos em um formato CSV. Os metadados são exportados de forma assíncrona e não afetam o desempenho do sistema. Para exportar metadados, o Experience Manager atravessa as propriedades do nó do ativo `jcr:content/metadata` e seus nós filhos e exporta as propriedades dos metadados em um arquivo CSV.

Alguns casos de uso para exportar metadados em massa são:

* Importe os metadados em um sistema de terceiros ao migrar ativos.
* Compartilhe metadados de ativos com uma equipe de projeto mais ampla.
* Teste ou faça auditoria dos metadados para fins de conformidade.
* Externalize os metadados para localização separada.

1. Selecione a pasta de ativos que contém ativos para os quais deseja exportar metadados. Na barra de ferramentas, selecione **[!UICONTROL Exportar metadados]**.
1. Na caixa de diálogo Exportação de metadados, especifique um nome para o arquivo CSV. Para exportar metadados para ativos em subpastas, selecione **[!UICONTROL Incluir ativos em subpastas]**.

   ![Interface e opções para exportar metadados de todos os ativos em uma pasta](assets/export_metadata_page.png "Interface e opções para exportar metadados de todos os ativos em uma pasta")

1. Selecione as opções desejadas. Forneça um nome de arquivo e, se necessário, uma data.

1. No **[!UICONTROL Propriedades a exportar]** , especifique se deseja exportar todas as propriedades ou propriedades específicas. Se você escolher Propriedades seletivas para exportar, adicione as propriedades desejadas.

1. Na barra de ferramentas, toque/clique **[!UICONTROL Exportar]**. Uma mensagem confirma que os metadados são exportados. Feche a mensagem.
1. Abra a notificação da caixa de entrada do trabalho de exportação. Selecione o trabalho e clique em **[!UICONTROL Abrir]** na barra de ferramentas. Para baixar o arquivo CSV com os metadados, toque/clique em **[!UICONTROL Download de CSV]** na barra de ferramentas. Clique em **[!UICONTROL Fechar]**.

   ![Caixa de diálogo para baixar o arquivo CSV contendo metadados exportados em massa](assets/csv_download.png)

   *Figura: Caixa de diálogo para baixar o arquivo CSV contendo metadados exportados em massa.*

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

