---
title: Uso do Cloud Readiness Analyzer
description: Uso do Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: ba2105d389617fe0c7e26642799b3a7dd3adb8a1
workflow-type: tm+mt
source-wordcount: '2091'
ht-degree: 77%

---


# Uso do Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## Considerações importantes sobre o uso do Cloud Readiness Analyzer {#imp-considerations}

Consulte a seção abaixo para entender considerações importantes na execução do CRA (Cloud Readiness Analyzer):

* O relatório do CRA é criado usando a saída do [Detector de padrões](https://docs.adobe.com/content/help/br/experience-manager-65/deploying/upgrading/pattern-detector.html) do Adobe Experience Manager (AEM). A versão do Detector de padrões usada pelo CRA está incluída no pacote de instalação do CRA.

* O CRA só pode ser executado pelo usuário **administrador** ou por um usuário do grupo **de administradores**.

* As instâncias do AEM suportam o CRA nas versões 6.1 e superiores.

   >[!NOTE]
   > Consulte [Instalação no AEM 6.1](#installing-on-aem61) para conhecer os requisitos especiais de instalação do CRA no AEM 6.1.

* O CRA pode ser executado em qualquer ambiente, mas é preferível executá-lo em um ambiente de *Preparo*.

   >[!NOTE]
   >Para evitar um impacto em instâncias críticas para os negócios, é recomendável executar o CRA em um ambiente de *Autor* o mais próximo possível do ambiente de *Produção* nas áreas de personalizações, configurações, conteúdo e aplicativos de usuários. Como alternativa, ele pode ser executado em um clone do ambiente de *Autor* de produção.

* A geração de conteúdo do relatório do CRA pode demorar um tempo significativo, desde vários minutos a algumas horas. O tempo necessário depende muito do tamanho e da natureza do conteúdo do repositório do AEM, da versão do AEM e de outros fatores.

* Devido ao tempo significativo que pode ser necessário para gerar o conteúdo do relatório, este é gerado por um processo em segundo plano e mantido em cache. A visualização e o download do relatório devem ser relativamente rápidos, pois ele utiliza o cache de conteúdo até expirar ou até o relatório ser atualizado. Durante a geração do conteúdo do relatório, você pode fechar a guia do navegador e retornar posteriormente para a visualização do relatório quando o conteúdo estiver disponível no cache.

## Disponibilidade {#availability}

É possível baixar o arquivo ZIP do Cloud Readiness Analyzer no Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM).

>[!NOTE]
>Baixe o Cloud Readiness Analyzer no [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Visualização do relatório do Cloud Readiness Analyzer {#viewing-report}

### Adobe Experience Manager 6.3.0 e versão posterior {#aem-later-versions}

Consulte esta seção para saber como visualizar o relatório do Cloud Readiness Analyzer:

1. Selecione Adobe Experience Manager e acesse Ferramentas -> **Operações** > **Cloud Readiness Analyzer**.

   ![imagem](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. Depois de clicar em **Cloud Readiness Analyzer**, a ferramenta começa a gerar o relatório, exibindo-o assim que ele estiver disponível.

   >[!NOTE]
   >Será necessário rolar a página para baixo para visualizar o relatório completo.

   ![imagem](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-1.png)

1. Depois que o relatório do CRA for gerado e exibido, você terá a opção de baixá-lo em um formato CSV (valores separados por vírgula) clicando em **CSV**, como mostra a figura abaixo.

   ![imagem](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-2.png)

   >[!NOTE]
   >Você pode forçar o CRA a limpar seu cache e gerar novamente o relatório, clicando em **Atualizar relatório**.

### Adobe Experience Manager 6.2 e 6.1 {#aem-specific-versions}

No Adobe Experience Manager 6.2, a ferramenta Cloud Readiness Analyzer consiste em um link que gera e baixa o relatório CSV.

Para o Adobe Experience Manager 6.1, a ferramenta não é funcional e apenas a interface HTTP pode ser usada.

>[!NOTE]
>Em todas as versões, o Detector de padrões incluído pode ser executado independentemente.

## Interpretação do relatório do Cloud Readiness Analyzer {#cra-report}

Quando a ferramenta Cloud Readiness Analyzer é executada na instância do AEM, o relatório é exibido como resultado na janela da ferramenta.

O formato do relatório é:

* **Visão geral do relatório**: informações sobre o relatório propriamente dito, que incluem as seguintes informações:
   * **Hora do relatório**: quando o conteúdo do relatório foi gerado e disponibilizado pela primeira vez.
   * **Hora de expiração**: quando o cache do conteúdo do relatório expirará.
   * **Período de geração**: o tempo gasto pelo processo de geração de conteúdo do relatório.
   * **Contagem de conclusões**: o número total de conclusões incluídas no relatório.
* **Visão geral do sistema**: informações sobre o sistema AEM no qual o CRA foi executado.
* **Categorias de conclusão**: várias seções que abordam uma ou mais conclusões da mesma categoria. Cada seção inclui o seguinte: nome da categoria, subtipos, contagem e importância das conclusões, resumo, link para a documentação da categoria e informações de conclusões individuais.

Um nível de importância é atribuído a cada conclusão para indicar uma prioridade aproximada de ação.

Siga a tabela abaixo para entender os níveis de importância:

| Importância | Descrição |
|--- |--- |
| INFO | Essa conclusão é fornecida para fins informativos. |
| CONSULTIVO | Essa conclusão pode ser um problema de atualização. Recomenda-se uma investigação mais aprofundada. |
| IMPORTANTE | Essa conclusão provavelmente será um problema de atualização que deve ser resolvido. |
| CRÍTICO | Essa conclusão provavelmente será um problema de atualização que deve ser resolvido para evitar a perda de função ou do desempenho. |


## Interpretação do relatório CSV do Cloud Readiness Analyzer {#cra-csv-report}

Quando você clica na opção **CSV** da sua instância do AEM, o formato CSV do relatório do Cloud Readiness Analyzer é criado a partir do cache de conteúdo e retornado ao seu navegador. Dependendo das configurações do navegador, esse relatório será baixado automaticamente como um arquivo com o nome padrão de `results.csv`.

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

O CRA fornece uma interface HTTP que pode ser usada como alternativa à interface do usuário no AEM. A interface oferece suporte a comandos HEAD e GET. Ela pode ser usada para gerar o relatório do CRA e retorná-lo em um dos três formatos: JSON, CSV e valores separados por tabulação (TSV).

Os seguintes URLs estão disponíveis para acesso HTTP, em que `<host>` é o nome do host e da porta, se necessário, do servidor no qual o CRA está instalado:
* `http://<host>/apps/readiness-analyzer/analysis/result.json` para formato JSON
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` para formato CSV
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` para formato TSV

### Execução de uma solicitação HTTP {#executing-http-request}

A interface HTTP pode ser usada em diversos métodos.

Uma maneira simples é abrir uma guia do navegador no mesmo navegador no qual você já fez logon no AEM como administrador. Você pode digitar o URL na guia do navegador e fazer com que os resultados sejam exibidos ou baixados pelo navegador.

Você também pode usar uma ferramenta de linha de comando, como `curl` ou `wget`, além de qualquer aplicativo cliente HTTP. Quando não estiver usando uma guia do navegador com uma sessão autenticada, você deve fornecer um nome de usuário administrativo e uma senha como parte do comentário.

Este é um exemplo de como isso pode ser feito:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`.

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
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

Depois que uma solicitação é feita, o cliente não precisa permanecer ativo para que o relatório seja gerado. A geração de relatórios pode ser iniciada com um cliente usando uma solicitação de GET HTTP e, depois que o relatório for gerado, visualizado do cache com outro cliente ou com a ferramenta CRA na interface do usuário AEM.

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

A duração padrão do cache do CRA é de 24 horas. Com a opção de atualizar um relatório e regenerar o cache, tanto na instância do AEM quanto na interface HTTP, esse valor padrão provavelmente será apropriado para a maioria dos usos do CRA. Se o tempo de geração do relatório for particularmente longo para a sua instância do AEM, talvez você queira ajustar o tempo de vida do cache para minimizar a regeneração do relatório.

O valor vitalício do cache é armazenado como a propriedade `maxCacheAge` no seguinte nó do repositório:
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

O valor dessa propriedade é o tempo de vida do cache em segundos. Um administrador pode ajustar a duração do cache usando o CRX/DE Lite.

### Instalação no AEM 6.1 {#installing-on-aem61}

O CRA usa uma conta de usuário do serviço do sistema chamada `repository-reader-service` para executar o Detector de padrões. Essa conta está disponível no AEM 6.2 e nas versões posteriores. No AEM 6.1, essa conta deve ser criada *antes* da instalação do CRA, com a execução as seguintes etapas:

1. Siga as instruções em [Criar um novo usuário de serviço](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/administering/security/security-service-users.translate.html#creating-a-new-service-user) para criar um usuário. Defina a UserID como `repository-reader-service`, deixe o Caminho intermediário vazio e clique na marca de seleção verde.

2. Siga as instruções em [Gerenciar usuários e grupos](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/administering/security/security.translate.html#managing-users-and-groups), especificamente as instruções para adicionar usuários a um grupo, para adicionar o usuário `repository-reader-service` ao grupo `administrators`.

3. Instale o pacote do CRA por meio do Gerenciador de pacotes na instância do AEM de origem. (Essa etapa adiciona a alteração de configuração necessária à configuração ServiceUserMapper do usuário de serviço do sistema `repository-reader-service`.)
