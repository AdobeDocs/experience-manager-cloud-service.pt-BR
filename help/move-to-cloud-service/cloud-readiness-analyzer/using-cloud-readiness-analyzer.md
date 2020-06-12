---
title: Uso do Cloud Readiness Analyzer
description: Uso do Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 1ca9b2091befbafad0878d83fc7963c779146b2a
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 0%

---


# Uso do Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## Considerações importantes sobre o uso do Cloud Readiness Analyzer {#imp-considerations}

Siga a seção abaixo para entender as considerações importantes ao executar o CRA (Cloud Readiness Analyzer):

* O relatório CRA é criado usando a saída do Detector de [padrões](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html)do Adobe Experience Manager (AEM). A versão do Detector de padrão usada pelo CRA está incluída no pacote de instalação do CRA.

* O CRA só pode ser executado pelo usuário *administrador* ou por um usuário no grupo **Administradores** .

* O CRA é compatível com instâncias do AEM com a versão 6.1 e superior.

* O CRA pode ser executado em qualquer ambiente, mas é preferível executá-lo em um ambiente *Stage* .

   >[!NOTE]
   >Para evitar um impacto em instâncias críticas para os negócios, é recomendável executar o CRA em um ambiente de preparo de *Autor* o mais próximo possível do ambiente de produção nas áreas de personalizações, configurações, conteúdo e aplicativos de usuário. Como alternativa, ele pode ser executado em um clone do ambiente do *Autor* de produção.

* A geração de relatórios CRA pode levar um tempo significativo, de vários minutos a algumas horas. O tempo necessário depende muito do tamanho e da natureza do conteúdo do repositório do AEM, da versão do AEM e de outros fatores.

* Devido ao tempo significativo necessário para gerar o relatório, os resultados são mantidos em cache e estão disponíveis para visualização e download subsequentes até que o cache expire ou o relatório seja explicitamente atualizado.

## Disponibilidade {#availability}

O Cloud Readiness Analyzer pode ser baixado como um arquivo zip do Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na instância de origem do Adobe Experience Manager (AEM).

>[!NOTE]
>Baixe o Cloud Readiness Analyzer do Portal de distribuição de software *pendente*.

## Execução do Analisador de disponibilidade da nuvem {#running-tool}

Siga esta seção para saber como executar o Cloud Readiness Analyzer:

1. Selecione o Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> Analisador de prontidão da **nuvem**.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. Após clicar em **Cloud Readiness Analyzer**, os start de ferramenta que geram o relatório e, após alguns minutos, o relatório de resumo estará disponível na sua instância do AEM.

   >[!NOTE]
   >Será necessário rolar a página para baixo para visualização do relatório completo.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### AEM 6.3 e posterior {#aem-older-version}

Para o AEM 6.3 e superior, a principal maneira de executar o Cloud Readiness Analyzer é:

1. Selecione a instância do Adobe Experience Manager e navegue até Ferramentas -> **Operações** -> Analisador **de prontidão da** nuvem.

   >[!NOTE]
   >O CRA iniciará um processo em segundo plano para gerar o relatório assim que a ferramenta for aberta. Ele exibe uma indicação de que a geração do relatório está em andamento até que o relatório esteja pronto. Você pode fechar a guia do navegador e retornar posteriormente para visualização do relatório quando ele for concluído.

1. Depois que o relatório CRA for gerado e exibido, você terá a opção de baixar o relatório em um CSV (valores separados por vírgula). Clique em **CSV** para baixar o relatório de resumo completo no formato CSV (valores separados por vírgula), como mostrado na figura abaixo.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)

   >[!NOTE]
   >Você pode forçar o CRA a limpar seu cache e gerar novamente o relatório clicando no botão **Atualizar relatório** no canto superior esquerdo.

### AEM 6.2 e 6.1 {#aem-specific-versions}

A interface do usuário do Cloud Readiness Analyzer é limitada no AEM 6.2 a um link que gera e baixa o relatório CSV. Para o AEM 6.1, a interface do usuário não está funcional e somente a interface HTTP pode ser usada.

Em todas as versões, o Detector de padrão incluído pode ser executado independentemente.

Siga as etapas abaixo para baixar o relatório CSV do Adobe Experience Manager (AEM) 6.1 e 6.2:

1. Navegue até **Adobe Experience Manager Web ConsoleConfiguração** usando `https://serveraddress:serverport/system/console/configMgr`.

1. Selecione a guia **Status** e procure **Pattern Detector** na lista suspensa, como mostrado na figura abaixo.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-4.png)

1. Você pode baixar o relatório de resumo em uma pasta zip ou em um formato JSON.

## Relatório de resumo da CRA {#cra-summary-report}

Quando o Cloud Readiness Analyzer é executado na interface do usuário do AEM, o relatório é exibido como resultados na janela da ferramenta.

O formato do relatório é:

* *Visão geral* do relatório: Informações sobre o próprio relatório, incluindo quando foi gerado.
* *Visão geral* do sistema: Informações sobre o sistema AEM no qual o CRA foi executado.
* *Encontrando Categorias*: Várias seções que abordam uma ou mais descobertas da mesma categoria. Cada seção inclui o seguinte: Nome da Categoria, subtipos, contagem e importância da descoberta, resumo, link para a documentação da categoria e informações de localização individual.

A cada descoberta é atribuído um nível de importância para indicar uma prioridade aproximada para a ação.

Siga a tabela abaixo para entender os níveis de importância:

| Importância | Descrição |
|--- |--- |
| INFO | Esta constatação é fornecida para fins informativos. |
| CONSULTORIA | Essa descoberta pode ser um problema de atualização. Recomenda-se uma investigação mais aprofundada. |
| MAIOR | Essa descoberta provavelmente será um problema de atualização que deve ser resolvido. |
| CRÍTICO | Essa descoberta provavelmente será um problema de atualização que deve ser resolvido para evitar perda de função ou desempenho. |

## Relatório CSV CRA {#crs-csv-report}

Quando você clica na opção **CSV** da sua instância do AEM, o formato CSV do relatório do Analisador de prontidão da nuvem é criado a partir do cache de resultados e retornado ao seu navegador. Dependendo das configurações do navegador, este relatório será baixado automaticamente como um arquivo com o nome padrão de `results.csv`. Se o cache tiver expirado, o relatório será gerado novamente antes que o arquivo CSV seja criado e baixado.

O formato CSV do relatório inclui informações geradas a partir da saída do Detector de padrão, classificadas e organizadas por tipo de categoria, subtipo e nível de importância. Seu formato é adequado para exibição e edição em um aplicativo como o Microsoft Excel. O objetivo é fornecer todas as informações de localização em um formato repetível que possam ser úteis ao comparar relatórios ao longo do tempo para medir o progresso.

As colunas do relatório de formato CSV são:

* **código**: o código de categoria
* **tipo**: o nome da categoria
* **subtipo**: o subtipo categoria
* **importância**: nível de importância
* **identificador**: o identificador principal da descoberta
* **outros**: informações adicionais sobre a descoberta
* **mensagem**: a mensagem fornecida para a descoberta
* **moreInfo**: um link que pode ser usado para acessar a ajuda online sobre a categoria
* **contexto**: uma string JSON para localizar dados

Um valor de &quot;\N&quot; em uma coluna para uma descoberta individual indica que nenhum dado foi fornecido.

## Interface HTTP {#http-interface}

O CRA fornece uma interface HTTP que pode ser usada como uma alternativa à interface do usuário do AEM. A interface suporta comandos HEAD e GET. Ele pode ser usado para gerar o relatório CRA e retorná-lo em um dos três formatos: JSON, CSV e valores separados por tabulação (TSV).

Os seguintes URLs estão disponíveis para acesso HTTP, onde `<host>` é o nome do host e a porta, se necessário, do servidor no qual o CRA está instalado:
* `http://<host>/apps/readiness-analyzer/analysis/result.json` para formato JSON
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` para formato CSV
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` para formato TSV

### Executando uma solicitação HTTP {#executing-http-request}

A interface HTTP pode ser usada em diversos métodos.

Uma maneira simples é abrir uma guia do navegador no mesmo navegador no qual você já fez logon no AEM como administrador. Você pode digitar o URL na guia do navegador e fazer com que os resultados sejam exibidos ou baixados pelo navegador.

Você também pode usar uma ferramenta de linha de comando, como `curl` ou `wget` qualquer aplicativo cliente HTTP. Quando não estiver usando uma guia do navegador com uma sessão autenticada, você deverá fornecer um nome de usuário administrativo e uma senha como parte do comentário.

Este é um exemplo de como isso pode ser feito:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`.

### Cabeçalhos e parâmetros {#http-headers-and-parameters}

Os seguintes cabeçalhos HTTP são usados por esta interface:

* `Cache-Control: max-age=<seconds>`: Especifique a duração da frescura do cache em segundos. (Consulte [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: Indica que o servidor deve responder de forma assíncrona. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1).)

Os seguintes parâmetros de query HTTP estão disponíveis como conveniência para quando os cabeçalhos HTTP podem não ser usados com facilidade:

* `max-age` (número, opcional): Especifique a duração da frescura do cache em segundos. Esse número deve ser 0 ou maior. A duração de atualização padrão é de 86400 segundos, o que significa que, sem esse parâmetro ou o cabeçalho correspondente, um novo cache será usado para atender solicitações de 24 horas antes do relatório ser regenerado. O uso `max-age=0` forçará a limpeza do cache e iniciará a regeneração do relatório. Imediatamente após essa solicitação, a duração da frescura será redefinida para o valor diferente de zero anterior.
* `respond-async` (booleano, opcional): Especifique que a resposta deve ser fornecida de forma assíncrona. Usar `respond-async=true` quando o cache estiver obsoleto fará com que o servidor retorne uma resposta de `202 Accepted, processing cache` sem esperar que o relatório seja gerado e o cache seja atualizado. Se o cache estiver atualizado, esse parâmetro não terá efeito. O valor padrão é `false`, o que significa que sem esse parâmetro ou o cabeçalho correspondente, o servidor responderá de forma síncrona, o que pode exigir uma quantidade significativa de tempo e um ajuste ao tempo máximo de resposta do cliente HTTP.

Quando um cabeçalho HTTP e um parâmetro de query correspondente estiverem presentes, o parâmetro query terá prioridade.

Uma maneira simples de iniciar a geração do relatório por meio da interface HTTP é com o seguinte comando:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

Depois que uma solicitação é feita, o cliente não precisa permanecer ativo para que o relatório seja gerado. A geração de relatórios pode ser iniciada com um cliente usando uma solicitação HTTP GET e, depois que o relatório for gerado, visualizado do cache em outro cliente ou ferramenta CSV na interface do usuário do AEM.

### Respostas (#http-response)

Os seguintes valores de resposta são possíveis:

* `200 OK`: A resposta contém descobertas do Detector de padrão que foram geradas dentro do tempo de vida útil do cache.
* `202 Accepted, processing cache`: Fornecido para respostas assíncronas para indicar que o cache estava obsoleto e que uma atualização estava em andamento.
* `400 Bad Request`: Indica que houve um erro com a solicitação. Uma mensagem no formato Detalhes do problema (consulte [RFC 7807](https://tools.ietf.org/html/rfc7807)) fornece mais detalhes.
* `401 Unauthorized`: O pedido não foi autorizado.
* `500 Internal Server Error`: Indica que ocorreu um erro de servidor interno. Uma mensagem no formato Detalhes do problema fornece mais detalhes.
* `503 Service Unavailable`: Indica que o servidor está ocupado com outra resposta e não pode atender essa solicitação em tempo hábil. Isso ocorre somente quando são feitas solicitações síncronas. Uma mensagem no formato Detalhes do problema fornece mais detalhes.

## Ajuste da duração do cache {#cache-adjustment}

A duração padrão do cache CRA é de 24 horas. Com a opção de atualizar um relatório e gerar novamente o cache, tanto na interface do usuário quanto na interface HTTP, esse valor padrão provavelmente será apropriado para a maioria dos usos do CRA. Se o tempo de geração do relatório for particularmente longo para a sua instância do AEM, você pode desejar ajustar a duração do cache para minimizar a regeneração do relatório.

O valor do tempo de vida do cache é armazenado como a `maxCacheAge` propriedade no seguinte nó do repositório:
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

O valor dessa propriedade é a duração do cache em segundos. Um administrador pode ajustar a duração do cache usando a interface CRX/DE Lite para o AEM.





