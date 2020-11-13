---
title: Uso do Analisador de práticas recomendadas
description: Uso do Analisador de práticas recomendadas
translation-type: tm+mt
source-git-commit: 07180809ff8b4a42a07eb9c691ab7a99262742ec
workflow-type: tm+mt
source-wordcount: '2207'
ht-degree: 47%

---


# Uso do Analisador de práticas recomendadas {#using-best-practices-analyzer}

## Considerações importantes sobre o uso do Analisador de práticas recomendadas {#imp-considerations}

Siga a seção abaixo para entender as considerações importantes para executar o BPA (Best Practices Analyzer):

* The BPA report is built using the output of the Adobe Experience Manager (AEM) [Pattern Detector](https://docs.adobe.com/content/help/br/experience-manager-65/deploying/upgrading/pattern-detector.html). A versão do Detector de padrão usada pelo BPA está incluída no pacote de instalação do BPA.

* BPA may only be run by the **admin** user or a user in the **administrators** group.

* O BPA é suportado em instâncias AEM com a versão 6.1 e superior.

   >[!NOTE]
   > Please see [Installing on AEM 6.1](#installing-on-aem61) for special requirements for installing BPA on AEM 6.1.

* BPA can run on any environment, but it is preferred to have it run on a *Stage* environment.

   >[!NOTE]
   >In order to avoid an impact on business critical instances, it is recommended that you run BPA on an *Author* environment that is as close as possible to the *Production* environment in the areas of customizations, configurations, content and user applications. Como alternativa, ele pode ser executado em um clone do ambiente de *Autor* de produção.

* A geração de conteúdo do relatório BPA pode levar um tempo significativo, de vários minutos a algumas horas. O tempo necessário depende muito do tamanho e da natureza do conteúdo do repositório do AEM, da versão do AEM e de outros fatores.

* Devido ao tempo significativo que pode ser necessário para gerar o conteúdo do relatório, este é gerado por um processo em segundo plano e mantido em cache. A visualização e o download do relatório devem ser relativamente rápidos, pois ele utiliza o cache de conteúdo até expirar ou até o relatório ser atualizado. Durante a geração do conteúdo do relatório, você pode fechar a guia do navegador e retornar posteriormente para a visualização do relatório quando o conteúdo estiver disponível no cache.

## Disponibilidade {#availability}

O Analisador de práticas recomendadas pode ser baixado como um arquivo zip do portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM).

>[!NOTE]
>Download the Best Practices Analyzer from the [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal.

## Como visualizar o relatório do Analisador de práticas recomendadas {#viewing-report}

### Adobe Experience Manager 6.3.0 e versão posterior {#aem-later-versions}

Siga esta seção para saber como visualização o relatório Analisador de práticas recomendadas:

1. Select Adobe Experience Manager and navigate to tools -> **Operations** -> **Best Practices Analyzer**.

   ![imagem](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic1.png)

1. Clique em **Gerar relatório** para executar o Analisador de práticas recomendadas.

   ![imagem](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic2.png)

1. Enquanto o BPA está gerando o relatório, você pode ver o progresso feito pela ferramenta na tela. Exibe o número de itens analisados e também o número de descobertas encontradas.

   ![imagem](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic3.png)


1. Depois que o relatório BPA é gerado, ele exibe um resumo e o número de conclusões em um formato de tabela organizado pelo tipo de descoberta e o nível de importância. Para obter mais detalhes sobre uma determinada descoberta, clique no número que corresponde ao tipo de descoberta na tabela.

   ![imagem](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic4.png)

   A ação acima percorrerá automaticamente o local da descoberta no relatório.

   ![imagem](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic5.png)

1. You have the option of downloading the report in a comma-separated values (CSV) format by clicking on **CSV**, as shown in the figure below.

   ![imagem](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic6.png)

   >[!NOTE]
   >You may force the BPA to clear its cache and regenerate the report by clicking **Refresh Report**.

   ![imagem](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic7.png)

   >[!NOTE]
   >Enquanto o relatório está sendo regenerado, ele exibe o progresso em termos de porcentagem concluída, como mostrado na imagem abaixo.

   ![imagem](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic8.png)


### Adobe Experience Manager 6.2 e 6.1 {#aem-specific-versions}

A ferramenta Analisador de práticas recomendadas está limitada no Adobe Experience Manager 6.2 a um link que gera e baixa o relatório CSV.

Para o Adobe Experience Manager 6.1, a ferramenta não é funcional e apenas a interface HTTP pode ser usada.

>[!NOTE]
>Em todas as versões, o Detector de padrões incluído pode ser executado independentemente.

## Interpretação do relatório do Analisador de práticas recomendadas {#cra-report}

Quando a ferramenta Analisador de práticas recomendadas é executada na instância AEM, o relatório é exibido como resultados na janela da ferramenta.

O formato do relatório é:

* **Visão geral do relatório**: informações sobre o relatório propriamente dito, que incluem as seguintes informações:
   * **Hora do relatório**: quando o conteúdo do relatório foi gerado e disponibilizado pela primeira vez.
   * **Hora de expiração**: quando o cache do conteúdo do relatório expirará.
   * **Período de geração**: o tempo gasto pelo processo de geração de conteúdo do relatório.
   * **Contagem de conclusões**: o número total de conclusões incluídas no relatório.
* **Visão geral** do sistema: Informações sobre o sistema AEM no qual o BPA foi executado.
* **Categorias de conclusão**: várias seções que abordam uma ou mais conclusões da mesma categoria. Cada seção inclui o seguinte: nome da categoria, subtipos, contagem e importância das conclusões, resumo, link para a documentação da categoria e informações de conclusões individuais.

Um nível de importância é atribuído a cada conclusão para indicar uma prioridade aproximada de ação.

>[!NOTE]
>Para saber mais sobre cada Categoria de descoberta, consulte Categorias [do Detector de](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html)padrões.

Siga a tabela abaixo para entender os níveis de importância:

| Importância | Descrição |
|--- |--- |
| INFO | Essa conclusão é fornecida para fins informativos. |
| CONSULTIVO | Essa conclusão pode ser um problema de atualização. Recomenda-se uma investigação mais aprofundada. |
| IMPORTANTE | Essa conclusão provavelmente será um problema de atualização que deve ser resolvido. |
| CRÍTICO | Essa conclusão provavelmente será um problema de atualização que deve ser resolvido para evitar a perda de função ou do desempenho. |


## Interpretação do relatório CSV do Analisador de práticas recomendadas {#cra-csv-report}

When you click the **CSV** option from your AEM instance, the CSV format of the Best Practices Analyzer report is built from the content cache and returned to your browser. Dependendo das configurações do navegador, esse relatório será baixado automaticamente como um arquivo com o nome padrão de `results.csv`.

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

O BPA fornece uma interface HTTP que pode ser usada como uma alternativa à interface do usuário no AEM. A interface oferece suporte a comandos HEAD e GET. Ele pode ser usado para gerar o relatório BPA e retorná-lo em um dos três formatos: JSON, CSV e valores separados por tabulação (TSV).

The following URLs are available for HTTP access, where `<host>` is the hostname, and port if necessary, of the server on which the BPA is installed:
* `http://<host>/apps/best-practices-analyzer/analysis/report.json` para formato JSON
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv` para formato CSV
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv` para formato TSV

### Execução de uma solicitação HTTP {#executing-http-request}

A interface HTTP pode ser usada em diversos métodos.

Uma maneira simples é abrir uma guia do navegador no mesmo navegador no qual você já fez logon no AEM como administrador. Você pode digitar o URL na guia do navegador e fazer com que os resultados sejam exibidos ou baixados pelo navegador.

Você também pode usar uma ferramenta de linha de comando, como `curl` ou `wget`, além de qualquer aplicativo cliente HTTP. Quando não estiver usando uma guia do navegador com uma sessão autenticada, você deve fornecer um nome de usuário administrativo e uma senha como parte do comentário.

Este é um exemplo de como isso pode ser feito:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`.

### Cabeçalhos e parâmetros {#http-headers-and-parameters}

Os seguintes cabeçalhos HTTP são usados por essa interface:

* `Cache-Control: max-age=<seconds>`: Especifica a duração da frescura do cache em segundos. (Consulte [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: Especifica que o servidor deve responder de forma assíncrona. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1).)
* `Prefer: return=minimal`: Especifica que o servidor deve retornar uma resposta mínima. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2).)

Os seguintes parâmetros de consulta HTTP estão disponíveis como conveniência para quando cabeçalhos HTTP não puderem ser usados com facilidade:

* `max-age` (número, opcional): Especifica a duração da frescura do cache em segundos. Esse número deve ser 0 ou maior. A duração padrão de frescura é de 86400 segundos. Sem esse parâmetro ou o cabeçalho correspondente, um novo cache será usado para atender solicitações por 24 horas, e nesse ponto o cache deverá ser regenerado. O uso `max-age=0` forçará a limpeza do cache e iniciará a regeneração do relatório, usando a duração de frescura diferente de zero anterior para o cache recém-gerado.
* `respond-async` (booleano, opcional): Especifica que a resposta deve ser fornecida de forma assíncrona. Using `respond-async=true` when the cache is stale will cause the server to return a response of `202 Accepted` without waiting for the cache to be refreshed and for the report to be generated. Se o cache estiver atualizado, esse parâmetro não terá efeito. The default value is `false`. Without this parameter or the corresponding header the server will respond synchronously, which may require a significant amount of time and require an adjustment to the maximum response time for the HTTP client.
* `may-refresh-cache` (booleano, opcional): Especifica que o servidor pode atualizar o cache em resposta a uma solicitação se o cache atual estiver vazio, obsoleto ou em breve obsoleto. Se `may-refresh-cache=true`ou se não for especificado, o servidor poderá iniciar uma tarefa em segundo plano que chamará o Detector de padrão e atualizará o cache. Se `may-refresh-cache=false` isso acontecer, o servidor não iniciará nenhuma tarefa de atualização que, de outra forma, teria sido feita se o cache estivesse vazio ou obsoleto, caso em que o relatório estará vazio. Qualquer tarefa de atualização que já esteja em andamento não será afetada por esse parâmetro.
* `return-minimal` (booleano, opcional): Especifica que a resposta do servidor deve incluir apenas o status que contém a indicação de progresso e o status do cache no formato JSON. Se `return-minimal=true`, o corpo da resposta será limitado ao objeto de status. Se `return-minimal=false`, ou se não for especificado, será fornecida uma resposta completa.
* `log-findings` (booleano, opcional): Especifica que o servidor deve registrar o conteúdo do cache quando ele for criado ou atualizado pela primeira vez. Cada descoberta do cache será registrada como uma string JSON. Este registro só ocorrerá se `log-findings=true` e a solicitação gerar um novo cache.

Quando um cabeçalho HTTP e um parâmetro de consulta correspondente estiverem presentes, o parâmetro de consulta terá prioridade.

Uma maneira simples de iniciar a geração do relatório por meio da interface HTTP é com o seguinte comando:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`.

Depois que uma solicitação é feita, o cliente não precisa permanecer ativo para que o relatório seja gerado. A geração de relatórios pode ser iniciada com um cliente usando uma solicitação de GET HTTP e, depois que o relatório for gerado, visualizado do cache com outro cliente ou com a ferramenta BPA na interface do usuário AEM.

### Respostas {#http-responses}

Os seguintes valores de resposta são possíveis:

* `200 OK`: Indica que a resposta contém descobertas do Detector de padrão que foram geradas dentro do tempo de vida útil do cache.
* `202 Accepted`: Usado para indicar que o cache está obsoleto. Quando `respond-async=true` e `may-refresh-cache=true` essa resposta indica que uma tarefa de atualização está em andamento. Quando `may-refresh-cache=false` essa resposta simplesmente indica que o cache está obsoleto.
* `400 Bad Request`: indica que houve um erro com a solicitação. A message in Problem Details format (see [RFC 7807](https://tools.ietf.org/html/rfc7807)) provides more details.
* `401 Unauthorized`: Indica que a solicitação não foi autorizada.
* `500 Internal Server Error`: indica que ocorreu um erro de servidor interno. Uma mensagem no formato de Detalhes do problema fornece mais detalhes.
* `503 Service Unavailable`: indica que o servidor está ocupado com outra resposta e não pode atender a essa solicitação em tempo hábil. Isso só pode ocorrer quando forem feitas solicitações síncronas. Uma mensagem no formato de Detalhes do problema fornece mais detalhes.

## Informações do administrador

### Ajuste do tempo de vida do cache {#cache-adjustment}

A duração padrão do cache BPA é de 24 horas. Com a opção de atualizar um relatório e gerar novamente o cache, tanto na instância AEM quanto na interface HTTP, esse valor padrão provavelmente será apropriado para a maioria dos usos do BPA. Se o tempo de geração do relatório for particularmente longo para a sua instância do AEM, talvez você queira ajustar o tempo de vida do cache para minimizar a regeneração do relatório.

O valor vitalício do cache é armazenado como a propriedade `maxCacheAge` no seguinte nó do repositório:
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

O valor dessa propriedade é o tempo de vida do cache em segundos. Um administrador pode ajustar a duração do cache usando o CRX/DE Lite.

### Instalação no AEM 6.1 {#installing-on-aem61}

BPA utilizes a system service user account named `repository-reader-service` to execute the Pattern Detector. Essa conta está disponível no AEM 6.2 e nas versões posteriores. On AEM 6.1, this account must be created *prior to* installation of BPA by taking the following steps:

1. Siga as instruções em [Criar um novo usuário de serviço](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/administering/security/security-service-users.translate.html#creating-a-new-service-user) para criar um usuário. Defina a UserID como `repository-reader-service`, deixe o Caminho intermediário vazio e clique na marca de seleção verde.

2. Siga as instruções em [Gerenciar usuários e grupos](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/administering/security/security.translate.html#managing-users-and-groups), especificamente as instruções para adicionar usuários a um grupo, para adicionar o usuário `repository-reader-service` ao grupo `administrators`.

3. Instale o pacote BPA via Gerenciador de pacotes na instância de AEM de origem. (Essa etapa adiciona a alteração de configuração necessária à configuração ServiceUserMapper do usuário de serviço do sistema `repository-reader-service`.)
