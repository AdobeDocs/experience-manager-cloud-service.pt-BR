---
title: Uso do Cloud Readiness Analyzer
description: Uso do Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: a0e58c626f94b778017f700426e960428b657806
workflow-type: tm+mt
source-wordcount: '1871'
ht-degree: 89%

---


# Uso do Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## Considerações importantes sobre o uso do Cloud Readiness Analyzer {#imp-considerations}

Consulte a seção abaixo para entender considerações importantes na execução do CRA (Cloud Readiness Analyzer):

* O relatório do CRA é criado usando a saída do [Detector de padrões](https://docs.adobe.com/content/help/br/experience-manager-65/deploying/upgrading/pattern-detector.html) do Adobe Experience Manager (AEM). A versão do Detector de padrões usada pelo CRA está incluída no pacote de instalação do CRA.

* CRA may only be run by the **admin** user or a user in the **administrators** group.

* O CRA tem suporte em instâncias do AEM com a versão 6.1 e superior.

   >[!NOTE]
   > Consulte [Instalação no AEM 6.1](#installing-on-aem61) para obter os requisitos especiais para instalar o CRA no AEM 6.1.

* O CRA pode ser executado em qualquer ambiente, mas é preferível executá-lo em um ambiente de *Preparo*.

   >[!NOTE]
   >Para evitar um impacto em instâncias críticas para os negócios, é recomendável executar o CRA em um ambiente de *Autor* o mais próximo possível do ambiente de *Produção* nas áreas de personalizações, configurações, conteúdo e aplicativos de usuários. Como alternativa, ele pode ser executado em um clone do ambiente de *Autor* de produção.

* A geração de conteúdo do relatório do CRA pode demorar um tempo significativo, desde vários minutos a algumas horas. O tempo necessário depende muito do tamanho e da natureza do conteúdo do repositório do AEM, da versão do AEM e de outros fatores.

* Devido ao tempo significativo que pode ser necessário para gerar o conteúdo do relatório, este é gerado por um processo em segundo plano e mantido em cache. A visualização e o download do relatório devem ser relativamente rápidos, pois ele utiliza o cache de conteúdo até expirar ou até o relatório ser atualizado. Durante a geração do conteúdo do relatório, você pode fechar a guia do navegador e retornar posteriormente para a visualização do relatório quando o conteúdo estiver disponível no cache.

## Disponibilidade {#availability}

O Cloud Readiness Analyzer pode ser baixado como um arquivo zip do portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM).

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

* `Cache-Control: max-age=<seconds>`: especifique o tempo de vida da atualização do cache em segundos. (Consulte [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: indica que o servidor deve responder de forma assíncrona. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1).)

Os seguintes parâmetros de consulta HTTP estão disponíveis como conveniência para quando cabeçalhos HTTP não puderem ser usados com facilidade:

* `max-age` (número, opcional): especifique o tempo de vida da atualização do cache em segundos. Esse número deve ser 0 ou maior. O tempo de vida da atualização padrão é de 86.400 segundos, o que significa que, sem esse parâmetro ou o cabeçalho correspondente, um novo cache será usado para atender a solicitações 24 horas antes de o relatório ser regenerado. O uso de `max-age=0` força a limpeza do cache e inicia a regeneração do relatório. Imediatamente após essa solicitação, o tempo de vida da atualização será redefinido para o valor diferente de zero anterior.
* `respond-async` (booleano, opcional): especifique que a resposta deve ser fornecida de forma assíncrona. Usar `respond-async=true` quando o cache estiver obsoleto faz com que o servidor retorne uma resposta de `202 Accepted, processing cache` sem esperar que o relatório seja gerado e o cache seja atualizado. Se o cache estiver atualizado, esse parâmetro não terá efeito. O valor padrão é `false`, o que significa que, sem esse parâmetro ou o cabeçalho correspondente, o servidor responde de forma síncrona, o que pode exigir uma quantidade significativa de tempo e um ajuste ao tempo máximo de resposta do cliente HTTP.

Quando um cabeçalho HTTP e um parâmetro de consulta correspondente estiverem presentes, o parâmetro de consulta terá prioridade.

Uma maneira simples de iniciar a geração do relatório por meio da interface HTTP é com o seguinte comando:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

Depois que uma solicitação é feita, o cliente não precisa permanecer ativo para que o relatório seja gerado. A geração de relatórios pode ser iniciada com um cliente usando uma solicitação GET HTTP e, depois que o relatório for gerado, visualizada do cache em outro cliente ou na ferramenta CSV na interface do usuário no AEM.

### Respostas {#http-responses}

Os seguintes valores de resposta são possíveis:

* `200 OK`: a resposta contém conclusões do Detector de padrões que foram geradas dentro do tempo de vida da atualização do cache.
* `202 Accepted, processing cache`: fornecido para respostas assíncronas para indicar que o cache estava obsoleto e que uma atualização estava em andamento.
* `400 Bad Request`: indica que houve um erro com a solicitação. Uma mensagem no formato de Detalhes do problema (consulte [RFC 7807](https://tools.ietf.org/html/rfc7807)) com mais detalhes.
* `401 Unauthorized`: a solicitação não foi autorizada.
* `500 Internal Server Error`: indica que ocorreu um erro de servidor interno. Uma mensagem no formato de Detalhes do problema fornece mais detalhes.
* `503 Service Unavailable`: indica que o servidor está ocupado com outra resposta e não pode atender a essa solicitação em tempo hábil. Isso só pode ocorrer quando forem feitas solicitações síncronas. Uma mensagem no formato de Detalhes do problema fornece mais detalhes.

## Informações do administrador

### Ajuste do tempo de vida do cache {#cache-adjustment}

A duração padrão do cache do CRA é de 24 horas. Com a opção de atualizar um relatório e regenerar o cache, tanto na instância do AEM quanto na interface HTTP, esse valor padrão provavelmente será apropriado para a maioria dos usos do CRA. Se o tempo de geração do relatório for particularmente longo para a sua instância do AEM, talvez você queira ajustar o tempo de vida do cache para minimizar a regeneração do relatório.

O valor vitalício do cache é armazenado como a propriedade `maxCacheAge` no seguinte nó do repositório:
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

O valor dessa propriedade é o tempo de vida do cache em segundos. Um administrador pode ajustar a duração do cache usando o CRX/DE Lite.

### Instalação no AEM 6.1 {#installing-on-aem61}

O CRA utiliza uma conta de usuário do serviço do sistema chamada `repository-reader-service` para executar o Detector de padrão. Esta conta está disponível no AEM 6.2 e posterior. No AEM 6.1, essa conta deve ser criada *antes* da instalação do CRA, executando as seguintes etapas:

1. Siga as instruções em [Criar um novo usuário](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user) de serviço para criar um usuário. Defina UserID como Caminho intermediário `repository-reader-service` e deixe-o vazio e clique na marca de seleção verde.

2. Siga as instruções em [Gerenciar usuários e grupos](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security.html#managing-users-and-groups), especificamente as instruções para Adicionar usuários a um grupo para adicionar o `repository-reader-service` usuário ao `administrators` grupo.

3. Instale o pacote CRA via Gerenciador de pacotes na instância AEM de origem. (Isso adicionará a emenda de configuração necessária à configuração ServiceUserMapper para o usuário do serviço do `repository-reader-service` sistema.)
