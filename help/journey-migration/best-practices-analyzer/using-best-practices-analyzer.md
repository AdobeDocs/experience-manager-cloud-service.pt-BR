---
title: Utilização do Analisador de práticas recomendadas
description: Saiba como usar o Analisador de práticas recomendadas para entender a disponibilidade da atualização.
exl-id: e8498e17-f55a-4600-87d7-60584d947897
feature: Migration
role: Admin
source-git-commit: 951f7fb56d1d8a3285973fda945cbc21f310925f
workflow-type: tm+mt
source-wordcount: '2796'
ht-degree: 37%

---

# Utilização do Analisador de práticas recomendadas {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="Utilização do Analisador de Práticas Recomendadas"
>abstract="Consulte a documentação para usar o Analisador de Práticas Recomendadas (antigo Cloud Readiness Analyzer) e o relatório gerado. O relatório do Analisador de Práticas Recomendadas é usado para obter um alto nível de compreensão da preparação geral para a atualização."
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="[Webinário] Introdução às ferramentas para acelerar a jornada para o Adobe Experience Manager as a Cloud Service"

## Considerações importantes sobre o uso do Analisador de práticas recomendadas {#imp-considerations}

Siga a seção abaixo para entender considerações importantes na execução do Analisador de práticas recomendadas (BPA):

* O relatório do BPA é criado usando a saída do [Detector de Padrões](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html?lang=pt-BR) do Adobe Experience Manager (AEM). A versão do Detector de padrões usada pelo BPA está incluída no pacote de instalação do BPA.

* O BPA só pode ser executado pelo usuário **administrador** ou por um usuário do grupo **administradores**.

* O BPA é compatível com instâncias do AEM com a versão 6.1 e superior.

  >[!NOTE]
  >Consulte [Instalação no AEM 6.1](#installing-on-aem61) para obter os requisitos especiais de instalação do BPA no AEM 6.1.

* O BPA pode ser executado em qualquer ambiente, mas é preferível executá-lo em um ambiente *Preparo*.

  >[!NOTE]
  >Para evitar um impacto em instâncias críticas para os negócios, é recomendável executar o BPA em um ambiente de *Preparo* o mais próximo possível do ambiente de *Produção* nas áreas de personalizações, configurações, conteúdo e aplicativos de usuários. Como alternativa, ele pode ser executado em um clone do ambiente de *Autor* de produção.

* A geração de conteúdo do relatório do BPA pode levar um tempo significativo, de vários minutos a algumas horas. O tempo necessário depende muito do tamanho e da natureza do conteúdo do repositório do AEM, da versão do AEM e de outros fatores.

* Devido ao tempo significativo que pode ser necessário para gerar o conteúdo do relatório, este é gerado por um processo em segundo plano e mantido em cache. A visualização e o download do relatório devem ser relativamente rápidos, pois ele utiliza o cache de conteúdo até expirar ou até o relatório ser atualizado. Durante a geração do conteúdo do relatório, você pode fechar a guia do navegador e retornar posteriormente para a visualização do relatório quando o conteúdo estiver disponível no cache.

## Disponibilidade {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_download"
>title="Baixar o Analisador de práticas recomendadas"
>abstract="É possível baixar o Analisador de Práticas Recomendadas como arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM)."

É possível baixar o Analisador de Práticas Recomendadas como arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio do [Gerenciador de Pacotes](/help/implementing/developing/tools/package-manager.md) na sua instância de origem do Adobe Experience Manager (AEM).

>[!NOTE]
>Baixe o Analisador de Práticas Recomendadas do portal [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Conectividade de ambiente do Source {#source-environment-connectivity}

A instância do AEM de origem pode estar sendo executada por trás de um firewall, em que só pode alcançar determinados hosts que foram adicionados a uma Lista de permissões. Para carregar automaticamente o relatório gerado pelo BPA para o Cloud Acceleration Manager com sucesso, os seguintes endpoints precisam estar acessíveis na instância que está executando o AEM:

* O serviço de armazenamento de blobs do Azure: `casstorageprod.blob.core.windows.net`


## Exibição do relatório do Analisador de práticas recomendadas {#viewing-report}

### Adobe Experience Manager 6.3.0 e posterior {#aem-later-versions}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa_upload_setup"
>title="Fazer upload automaticamente do relatório do analisador de práticas recomendadas (BPA) para o CAM"
>abstract="Forneça a chave de upload do BPA para enviar automaticamente o relatório do BPA gerado para o Cloud Acceleration Manager (CAM)."

Siga esta seção para saber como exibir o relatório do Analisador de práticas recomendadas:

1. Selecione o Adobe Experience Manager e navegue até Ferramentas > **Operações** > **Analisador de práticas recomendadas**.

   ![Analisador de práticas recomendadas](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. Clique em **Gerar relatório** para executar o Analisador de práticas recomendadas.

   ![Gerar relatório](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

>[!NOTE]
> A partir da versão 2.1.54 do BPA, um novo recurso foi introduzido para obter a pontuação do Lighthouse.


1. Depois de clicar em **Gerar relatório**, um pop-up será exibido solicitando a URL do Site Público da AEM para a Pontuação do Lighthouse. O usuário precisa inserir um URL válido no campo fornecido.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/bpa_popup_url.png)

   1. Se o URL for válido, uma mensagem de sucesso será exibida.

      ![imagem](/help/journey-migration/best-practices-analyzer/assets/valid_url.png)

   1. Se o URL for inválido, uma mensagem de erro será exibida.

      ![imagem](/help/journey-migration/best-practices-analyzer/assets/invalid_url.png)

1. Forneça a chave de carregamento de BPA para carregar automaticamente o relatório de BPA gerado no [Cloud Acceleration Manager (CAM)](/help/journey-migration/cloud-acceleration-manager/introduction/benefits-cam.md). Para obter a chave de carregamento, navegue até a [Análise de práticas recomendadas no CAM](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)

   ![Definir Chave de Carregamento do BPA](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key.png)

>[!NOTE]
>Você tem a opção de ignorar o carregamento automático para o CAM selecionando **Ignorar carregamento automático do relatório para o CAM**. Se você optar por ignorar, será necessário baixar manualmente o relatório do BPA como um arquivo de valor separado por vírgulas e, em seguida, fazer upload do arquivo no CAM. É recomendável usar a opção de chave de upload, pois ela simplifica a operação.

>[!IMPORTANT]
>Ao fazer upload manual para o CAM, os tamanhos do relatório são restritos a aproximadamente 200 MB. Para relatórios maiores, será necessário aproveitar o upload automático.

1. O botão **Gerar** fica ativo quando uma chave válida é fornecida. Clique em **Gerar** para iniciar a geração do relatório.

   ![Gerar relatório](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key1.png)

1. Enquanto o BPA está gerando o relatório, você pode ver o progresso feito pela ferramenta na tela. Ele exibe o progresso em termos de porcentagem concluída. Ele também exibe o número de itens analisados e o número de descobertas encontradas.

   ![Gerando relatório](/help/journey-migration/best-practices-analyzer/assets/BPA_generate_upload.png)

>[!NOTE]
>O carimbo de data e hora de expiração da chave de upload do BPA é exibido no canto superior direito. Você deve renovar a chave de upload do BPA quando estiver próxima de sua expiração. Para renovar a chave, você pode clicar em **Renovar** para navegar até o CAM para renovar a chave.

1. Depois que o relatório do BPA é gerado, ele exibe um resumo e o número de conclusões em um formato tabular organizado pelo tipo de descoberta e o nível de importância. Para obter mais detalhes sobre uma descoberta específica, você pode clicar no número que corresponde ao tipo de descoberta na tabela.

   ![Visão geral do relatório](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. Você tem a opção de baixar o relatório em um formato CSV (valores separados por vírgula) clicando em **Exportar para CSV**. Você também tem a opção de exibir o relatório no CAM clicando em **Ir para o CAM**. Você será direcionado à página [Análise de Práticas Recomendadas](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis) no CAM.

Você pode forçar o BPA a limpar seu cache e gerar novamente o relatório clicando em **Atualizar Relatório**.

![Atualizar relatório](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. Se o cache expirar, você terá a opção de visualizar o último relatório gerado no CAM clicando em **Exibir o último relatório gerado no CAM** ou iniciar uma nova geração de relatórios clicando em **Gerar novo relatório**.

![Nenhum relatório](/help/journey-migration/best-practices-analyzer/assets/BPA_regeneratereport.png)


#### Utilização de filtros no relatório do Analisador de práticas recomendadas {#bpa-filters}

Para filtrar os achados relacionados ao [ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), siga as etapas abaixo:

1. Clique no ícone do painel à esquerda no lado esquerdo da página. Isso exibirá o **Filtro ACS Commons**. Clique no **Filtro ACS Commons** para exibir a caixa de seleção interativa como mostrado na imagem abaixo.

   ![Filtro ACS Commons](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
   >O ícone do painel esquerdo será exibido somente se o BPA detectar o uso do ACS Commons.

1. Desmarque a caixa para filtrar todos os achados relacionados ao ACS Commons. Você deve ver uma **Contagem de Achados Filtrados** no relatório, como mostrado na imagem abaixo. O filtro também é aplicado ao relatório quando ele é exportado em um formato CSV (valores separados por vírgula).

   ![Contagem de Achados Filtrados](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
   >As conclusões do ACS Commons não devem ser ignoradas. Consulte a [documentação](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility) para determinar a compatibilidade com o AEM as a Cloud Service.

<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## Interpretação do relatório do analisador de práticas recomendadas {#cra-report}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_interpreting"
>title="Interpretação do relatório do analisador de práticas recomendadas"
>abstract="Há duas opções para visualizar relatórios do BPA: na interface e CSV. Quando o Analisador de Práticas Recomendadas é executado na instância do AEM, o relatório é exibido como resultado na janela da ferramenta. O formato CSV do relatório inclui informações geradas a partir do output do Detector de padrões, classificadas e organizadas por tipo de categoria, subtipo e nível de importância."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=pt-BR#analysis-report" text="Revisão do relatório do Analisador de práticas recomendadas"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=pt-BR" text="Noções básicas sobre as categorias do relatório do Analisador de Práticas Recomendadas"

Quando a ferramenta Analisador de práticas recomendadas é executada na instância do AEM, o relatório é exibido como resultado na janela da ferramenta.

O formato do relatório é:

* **Visão geral do relatório**: informações sobre o relatório propriamente dito, que incluem as seguintes informações:
   * **Hora do relatório**: quando o conteúdo do relatório foi gerado e disponibilizado pela primeira vez.
   * **Hora de expiração**: quando o cache do conteúdo do relatório expirará.
   * **Período de geração**: o tempo gasto pelo processo de geração de conteúdo do relatório.
   * **Contagem de conclusões**: o número total de conclusões incluídas no relatório.
* **Visão Geral do Sistema**: Informações sobre o sistema AEM no qual o BPA foi executado.
* **Categorias de conclusão**: várias seções que abordam uma ou mais conclusões da mesma categoria. Cada seção inclui o seguinte: nome da categoria, subtipos, contagem e importância das conclusões, resumo, link para a documentação da categoria e informações de conclusões individuais.

Um nível de importância é atribuído a cada conclusão para indicar uma prioridade aproximada de ação.

>[!NOTE]
>Para saber mais sobre cada Categoria de Achados, consulte [Categorias do Detector de Padrões](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=pt-BR).

Siga a tabela abaixo para entender os níveis de importância:

| Importância | Descrição |
|--- |--- |
| INFO | Essa conclusão é fornecida para fins informativos. |
| CONSULTIVO | Essa conclusão pode ser um problema de atualização. Recomenda-se uma investigação mais aprofundada. |
| IMPORTANTE | Essa conclusão provavelmente será um problema de atualização que deve ser resolvido. |
| CRÍTICO | Essa conclusão provavelmente será um problema de atualização que deve ser resolvido para evitar a perda de função ou do desempenho. |

## Interpretação do relatório CSV do Analisador de práticas recomendadas {#cra-csv-report}

Quando você clica na opção **CSV** da sua instância do AEM, o formato CSV do relatório do Analisador de práticas recomendadas é criado a partir do cache de conteúdo e retornado ao seu navegador. Dependendo das configurações do navegador, esse relatório é baixado automaticamente como um arquivo com o nome padrão de `results.csv`.

Se o cache tiver expirado, o relatório será gerado novamente antes que o arquivo CSV seja criado e baixado.

O formato CSV do relatório inclui informações geradas a partir da saída do Detector de padrões, classificadas e organizadas por tipo de categoria, subtipo e nível de importância. Seu formato é adequado para exibição e edição em um aplicativo como o Microsoft Excel. O objetivo é fornecer todas as informações de conclusão em um formato repetível, que pode ser útil na comparação de relatórios ao longo do tempo para medir o progresso.

As colunas do relatório em formato CSV são:

* **code**: o código da categoria
* **type**: o nome da categoria
* **subtype**: o subtipo da categoria
* **importance**: o nível de importância
* **identifier**: o identificador principal da conclusão
* **other**: informações adicionais sobre a conclusão
* **message**: a mensagem fornecida para a conclusão
* **moreInfo**: um link que pode ser usado para acessar a ajuda online sobre a categoria
* **context**: uma cadeia JSON de dados de conclusões

O valor &quot;\N&quot; em uma coluna para uma conclusão individual indica que nenhum dado foi fornecido.

## Interface HTTP {#http-interface}

O BPA fornece uma interface HTTP que pode ser usada como alternativa à interface do usuário no AEM. A interface oferece suporte a comandos HEAD e GET. Ela pode ser usada para gerar o relatório do BPA e retorná-lo em um dos três formatos: JSON, CSV e valores separados por tabulação (TSV).

As seguintes URLs estão disponíveis para acesso HTTP, em que `<host>` é o nome do host e da porta, se necessário, do servidor no qual o BPA está instalado:
* `http://<host>/apps/best-practices-analyzer/analysis/report.json` para formato JSON
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv` para formato CSV
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv` para formato TSV

### Execução de uma solicitação HTTP {#executing-http-request}

A interface HTTP pode ser usada em diversos métodos.

Uma maneira simples é abrir uma guia do navegador no mesmo navegador no qual você já fez logon no AEM como administrador. Você pode digitar o URL na guia do navegador e fazer com que os resultados sejam exibidos ou baixados pelo navegador.

Você também pode usar uma ferramenta de linha de comando como `curl` ou `wget` e qualquer aplicativo cliente HTTP. Quando não estiver usando uma guia do navegador com uma sessão autenticada, você deve fornecer um nome de usuário administrativo e uma senha como parte do comentário.

Este é um exemplo de como isso pode ser feito:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`.

### Cabeçalhos e parâmetros {#http-headers-and-parameters}

Os seguintes cabeçalhos HTTP são usados por essa interface:

* `Cache-Control: max-age=<seconds>`: especifica o tempo de vida da atualização do cache em segundos. (Consulte [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: especifica que o servidor deve responder de forma assíncrona. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1).)
* `Prefer: return=minimal`: especifica que o servidor deve retornar uma resposta mínima. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2).)

Os seguintes parâmetros de consulta HTTP estão disponíveis como conveniência para quando cabeçalhos HTTP não puderem ser usados com facilidade:

* `max-age` (número, opcional): especifica o tempo de vida da atualização do cache em segundos. Esse número deve ser 0 ou maior. O tempo de vida da atualização padrão é de 86.400 segundos. Sem esse parâmetro ou o cabeçalho correspondente, um novo cache é usado para atender a solicitações por 24 horas, momento em que o cache deve ser regenerado. O uso de `max-age=0` forçará a limpeza do cache e iniciará uma regeneração do relatório, usando o tempo de vida de atualização diferente de zero anterior para o cache recém-gerado.
* `respond-async` (booleano, opcional): especifica que a resposta deve ser fornecida de forma assíncrona. Usar `respond-async=true` quando o cache estiver obsoleto fará com que o servidor retorne uma resposta de `202 Accepted` sem esperar a atualização do cache e a geração do relatório. Se o cache estiver atualizado, esse parâmetro não terá efeito. O valor padrão é `false`. Sem esse parâmetro ou o cabeçalho correspondente, o servidor responderá de forma síncrona, o que pode exigir uma quantidade significativa de tempo e um ajuste ao tempo máximo de resposta do cliente HTTP.
* `may-refresh-cache` (booleano, opcional): especifica que o servidor pode atualizar o cache em resposta a uma solicitação se o cache atual estiver vazio, obsoleto ou prestes a ser obsoleto. Se `may-refresh-cache=true` ou se não for especificado, o servidor poderá iniciar uma tarefa em segundo plano que chamará o Detector de Padrões e atualizará o cache. Se `may-refresh-cache=false`, o servidor não iniciará nenhuma tarefa de atualização que teria sido realizada se o cache estivesse vazio ou obsoleto, caso em que o relatório está vazio. Qualquer tarefa de atualização que já esteja em andamento não será afetada por esse parâmetro.
* `return-minimal` (booleano, opcional): especifica que a resposta do servidor deve incluir apenas o status contendo a indicação de progresso e o status do cache no formato JSON. Se `return-minimal=true`, o corpo da resposta será limitado ao objeto de status. Se `return-minimal=false` ou se não for especificado, uma resposta completa será fornecida.
* `log-findings` (booleano, opcional): especifica que o servidor deve registrar o conteúdo do cache quando ele é compilado ou atualizado pela primeira vez. Cada descoberta do cache é registrada como uma cadeia de caracteres JSON. Este log só ocorrerá se `log-findings=true` e a solicitação gerarem um novo cache.

Quando um cabeçalho HTTP e um parâmetro de consulta correspondente estiverem presentes, o parâmetro de consulta terá prioridade.

Uma maneira simples de iniciar a geração do relatório por meio da interface HTTP é com o seguinte comando:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`.

Depois que uma solicitação é feita, o cliente não precisa permanecer ativo para que o relatório seja gerado. A geração de relatórios pode ser iniciada com um cliente usando uma solicitação HTTP GET e, depois que o relatório for gerado, visualizada do cache com outro cliente ou com a ferramenta BPA na interface do usuário do AEM.

### Respostas {#http-responses}

Os seguintes valores de resposta são possíveis:

* `200 OK`: indica que a resposta contém conclusões do Detector de Padrões que foram geradas dentro do tempo de vida da atualização do cache.
* `202 Accepted`: usado para indicar que o cache está obsoleto. Quando `respond-async=true` e `may-refresh-cache=true` esta resposta indica que uma tarefa de atualização está em andamento. Quando `may-refresh-cache=false` esta resposta simplesmente indica que o cache está obsoleto.
* `400 Bad Request`: indica que houve um erro com a solicitação. Uma mensagem no formato de Detalhes do Problema (consulte [RFC 7807](https://tools.ietf.org/html/rfc7807)) fornece mais detalhes.
* `401 Unauthorized`: indica que a solicitação não foi autorizada.
* `500 Internal Server Error`: indica que ocorreu um erro de servidor interno. Uma mensagem no formato de Detalhes do problema fornece mais detalhes.
* `503 Service Unavailable`: indica que o servidor está ocupado com outra resposta e não pode atender a essa solicitação em tempo hábil. Isso só pode ocorrer quando forem feitas solicitações síncronas. Uma mensagem no formato de Detalhes do problema fornece mais detalhes.

## Informações do administrador

### Ajuste da Duração do Cache {#cache-adjustment}

O tempo de vida padrão do cache do BPA é de 24 horas. Com a opção de atualizar um relatório e regenerar o cache, tanto na instância do AEM quanto na interface HTTP, esse valor padrão provavelmente será apropriado para a maioria dos usos do BPA. Se o tempo de geração do relatório for particularmente longo para sua instância do AEM, talvez você queira ajustar o tempo de vida do cache para minimizar a regeneração do relatório.

O valor vitalício do cache é armazenado como a propriedade `maxCacheAge` no seguinte nó do repositório:
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

O valor dessa propriedade é o tempo de vida do cache em segundos. Um administrador pode ajustar a duração do cache usando o CRX/DE Lite.

### Instalação no AEM 6.1 {#installing-on-aem61}

O BPA usa uma conta de usuário do serviço do sistema chamada `repository-reader-service` para executar o Detector de Padrões. Essa conta está disponível no AEM 6.2 e nas versões posteriores. No AEM 6.1, essa conta deve ser criada *antes* da instalação do BPA, executando as seguintes etapas:

1. Siga as instruções em [Criar um novo usuário de serviço](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html?lang=pt-BR#creating-a-new-service-user) para criar um usuário. Defina a UserID como `repository-reader-service`, deixe o Caminho intermediário vazio e clique na marca de seleção verde.

2. Siga as instruções em [Gerenciar usuários e grupos](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=pt-BR#managing-users-and-groups), especificamente as instruções para adicionar usuários a um grupo, para adicionar o usuário `repository-reader-service` ao grupo `administrators`.

3. Instale o pacote de BPA por meio do Gerenciador de pacotes na instância do AEM de origem. (Essa etapa adiciona a alteração de configuração necessária à configuração ServiceUserMapper do usuário de serviço do sistema `repository-reader-service`.)
