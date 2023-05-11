---
title: Utilização do Analisador de práticas recomendadas
description: Utilização do Analisador de práticas recomendadas
exl-id: e8498e17-f55a-4600-87d7-60584d947897
source-git-commit: df1fdbe0f3590708e1da44864b6e08075a521b51
workflow-type: tm+mt
source-wordcount: '2490'
ht-degree: 48%

---

# Utilização do Analisador de práticas recomendadas {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="Utilização do Analisador de Práticas Recomendadas"
>abstract="Consulte a documentação para usar o Analisador de Práticas Recomendadas (antigo Cloud Readiness Analyzer) e o relatório gerado. O relatório do Analisador de Práticas Recomendadas é usado para obter um alto nível de compreensão da preparação geral para a atualização."
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="[Webinário] Introdução às ferramentas para acelerar a jornada para o Adobe Experience Manager as a Cloud Service"

## Considerações importantes sobre o uso do Analisador de práticas recomendadas {#imp-considerations}

Siga a seção abaixo para entender as considerações importantes para a execução do BPA (Best Practices Analyzer):

* O relatório BPA é criado usando a saída do Adobe Experience Manager (AEM) [Detector de padrões](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html). A versão do Detector de padrões usada pelo BPA está incluída no pacote de instalação do BPA.

* O BPA só pode ser executado pelo **administrador** ou um usuário na **administradores** grupo.

* O BPA é compatível em instâncias AEM com a versão 6.1 e superior.

   >[!NOTE]
   >Consulte [Instalação no AEM 6.1](#installing-on-aem61) para os requisitos especiais de instalação do BPA no AEM 6.1.

* O BPA pode ser executado em qualquer ambiente, mas é preferível executá-lo em um *Fase* ambiente.

   >[!NOTE]
   >Para evitar um impacto em instâncias críticas para os negócios, é recomendável executar o BPA em um *Autor* ambiente o mais próximo possível *Produção* nas áreas de personalizações, configurações, conteúdo e aplicativos do usuário. Como alternativa, ele pode ser executado em um clone do ambiente de *Autor* de produção.

* A geração do conteúdo do relatório BPA pode demorar um tempo significativo, de vários minutos a algumas horas. O tempo necessário depende muito do tamanho e da natureza do conteúdo do repositório do AEM, da versão do AEM e de outros fatores.

* Devido ao tempo significativo que pode ser necessário para gerar o conteúdo do relatório, este é gerado por um processo em segundo plano e mantido em cache. A visualização e o download do relatório devem ser relativamente rápidos, pois ele utiliza o cache de conteúdo até expirar ou até o relatório ser atualizado. Durante a geração do conteúdo do relatório, você pode fechar a guia do navegador e retornar posteriormente para a visualização do relatório quando o conteúdo estiver disponível no cache.

## Disponibilidade {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_download"
>title="Baixar o Analisador de práticas recomendadas"
>abstract="É possível baixar o Analisador de Práticas Recomendadas como arquivo zip no Portal de distribuição de software. Você pode instalar o pacote por meio do Gerenciador de pacotes na sua instância de origem do Adobe Experience Manager (AEM)."

É possível baixar o Analisador de Práticas Recomendadas como arquivo zip no Portal de distribuição de software. Você pode instalar o pacote via [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md) na instância de origem do Adobe Experience Manager (AEM).

>[!NOTE]
>Baixe o Analisador de práticas recomendadas do [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal.

## Como visualizar o relatório do Analisador de práticas recomendadas {#viewing-report}

### Adobe Experience Manager 6.3.0 e versão posterior {#aem-later-versions}

Siga esta seção para saber como visualizar o relatório do Analisador de práticas recomendadas:

1. Selecione Adobe Experience Manager e navegue até ferramentas -> **Operações** -> **Analisador de práticas recomendadas**.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. Clique em **Gerar relatório** para executar o Analisador de práticas recomendadas.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

1. Enquanto o BPA está gerando o relatório, você pode ver o progresso feito pela ferramenta na tela. Ele exibe o número de itens analisados e também exibe o número de conclusões encontradas.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/BPA_pic3.png)

1. Depois que o relatório BPA é gerado, ele exibe um resumo e o número de conclusões em um formato de tabela organizado pelo tipo de descoberta e o nível de importância. Para obter mais detalhes sobre uma descoberta específica, clique no número que corresponde ao tipo de descoberta na tabela.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/BPA_pic4.png)

   A ação acima rolar-se-á automaticamente para o local da descoberta no relatório.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/BPA_pic5.png)

1. Você tem a opção de baixar o relatório em um formato CSV (valores separados por vírgula) clicando em **Exportar para CSV**, conforme mostrado na figura abaixo.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/BPA_pic6.png)

   >[!NOTE]
   >Você pode forçar o BPA a limpar seu cache e gerar novamente o relatório clicando em **Atualizar relatório**.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/BPA_pic7.png)

   >[!NOTE]
   >Enquanto o relatório está sendo gerado novamente, ele exibe o progresso em termos de porcentagem concluída, como mostrado na imagem abaixo.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/BPA_pic8.png)

#### Uso de filtros no relatório do Analisador de práticas recomendadas {#bpa-filters}

Para filtrar as descobertas relacionadas a [ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)siga as etapas abaixo:

1. Clique no ícone do painel à esquerda no lado esquerdo da página. Isso exibirá a variável **Filtro ACS Commons**. Clique no botão **Filtro ACS Commons** para exibir a caixa de seleção interativa conforme mostrado na imagem abaixo.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
   >O ícone do painel à esquerda será exibido somente se o BPA detectar o uso de ACS Commons.

1. Desmarque a caixa para filtrar todas as conclusões relacionadas ao ACS Commons. Você deve ver um **Contagem de conclusões filtradas** no relatório, conforme mostrado na imagem abaixo. O filtro também é aplicado ao relatório quando ele é exportado em um formato CSV (valores separados por vírgula).

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
   >As conclusões do ACS Commons não devem ser ignoradas. Consulte [documentação](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility) para determinar a compatibilidade com AEM as a Cloud Service.

<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## Interpretação do relatório do Analisador de práticas recomendadas {#cra-report}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_interpreting"
>title="Interpretação do relatório do Analisador de práticas recomendadas"
>abstract="Há duas opções para visualizar relatórios do Analisador de Práticas Recomendadas: na interface e CSV. Quando o Analisador de Práticas Recomendadas é executado na instância do AEM, o relatório é exibido como resultado na janela da ferramenta. O formato CSV do relatório inclui informações geradas a partir da saída do Detector de padrões, classificadas e organizadas por tipo de categoria, subtipo e nível de importância."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#analysis-report" text="Revisão do relatório do Analisador de Práticas Recomendadas"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=en" text="Noções básicas sobre as categorias do relatório do Analisador de Práticas Recomendadas"

Quando a ferramenta Analisador de práticas recomendadas é executada na instância de AEM, o relatório é exibido como resultado na janela da ferramenta.

O formato do relatório é:

* **Visão geral do relatório**: informações sobre o relatório propriamente dito, que incluem as seguintes informações:
   * **Hora do relatório**: quando o conteúdo do relatório foi gerado e disponibilizado pela primeira vez.
   * **Hora de expiração**: quando o cache do conteúdo do relatório expirará.
   * **Período de geração**: o tempo gasto pelo processo de geração de conteúdo do relatório.
   * **Contagem de conclusões**: o número total de conclusões incluídas no relatório.
* **Visão geral do sistema**: Informações sobre o sistema de AEM no qual o BPA foi executado.
* **Categorias de conclusão**: várias seções que abordam uma ou mais conclusões da mesma categoria. Cada seção inclui o seguinte: nome da categoria, subtipos, contagem e importância das conclusões, resumo, link para a documentação da categoria e informações de conclusões individuais.

Um nível de importância é atribuído a cada conclusão para indicar uma prioridade aproximada de ação.

>[!NOTE]
>Para saber mais sobre cada Categoria de descoberta, consulte [Categorias de Detector de Padrões](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html).

Siga a tabela abaixo para entender os níveis de importância:

| Importância | Descrição |
|--- |--- |
| INFO | Essa conclusão é fornecida para fins informativos. |
| CONSULTIVO | Essa conclusão pode ser um problema de atualização. Recomenda-se uma investigação mais aprofundada. |
| IMPORTANTE | Essa conclusão provavelmente será um problema de atualização que deve ser resolvido. |
| CRÍTICO | Essa conclusão provavelmente será um problema de atualização que deve ser resolvido para evitar a perda de função ou do desempenho. |

## Interpretação do relatório CSV do Analisador de práticas recomendadas {#cra-csv-report}

Ao clicar no botão **CSV** da sua instância de AEM, o formato CSV do relatório do Analisador de práticas recomendadas é criado a partir do cache de conteúdo e retornado ao seu navegador. Dependendo das configurações do navegador, esse relatório será baixado automaticamente como um arquivo com o nome padrão de `results.csv`.

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

O BPA fornece uma interface HTTP que pode ser usada como alternativa à interface do usuário no AEM. A interface oferece suporte a comandos HEAD e GET. Ele pode ser usado para gerar o relatório BPA e retorná-lo em um dos três formatos: JSON, CSV e valores separados por tabulação (TSV).

Os seguintes URLs estão disponíveis para acesso HTTP, onde `<host>` é o nome do host e, se necessário, da porta do servidor no qual o BPA está instalado:
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

* `Cache-Control: max-age=<seconds>`: Especifica o tempo de vida da atualização do cache em segundos. (Consulte [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: Especifica que o servidor deve responder de forma assíncrona. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1).)
* `Prefer: return=minimal`: Especifica que o servidor deve retornar uma resposta mínima. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2).)

Os seguintes parâmetros de consulta HTTP estão disponíveis como conveniência para quando cabeçalhos HTTP não puderem ser usados com facilidade:

* `max-age` (número, opcional): Especifica o tempo de vida da atualização do cache em segundos. Esse número deve ser 0 ou maior. O tempo de vida padrão da atualização é de 86.400 segundos. Sem esse parâmetro ou o cabeçalho correspondente, um novo cache será usado para atender às solicitações por 24 horas, e nesse ponto o cache deverá ser gerado novamente. Usando `max-age=0` força a limpeza do cache e inicia a regeneração do relatório, usando o tempo de vida de atualização diferente de zero anterior para o cache recém-gerado.
* `respond-async` (booleano, opcional): Especifica que a resposta deve ser fornecida de forma assíncrona. Usando `respond-async=true` quando o cache estiver obsoleto, o servidor retornará uma resposta de `202 Accepted` sem esperar que o cache seja atualizado e o relatório seja gerado. Se o cache estiver atualizado, esse parâmetro não terá efeito. O valor padrão é `false`. Sem esse parâmetro ou o cabeçalho correspondente, o servidor responderá de forma síncrona, o que pode exigir uma quantidade significativa de tempo e um ajuste ao tempo máximo de resposta do cliente HTTP.
* `may-refresh-cache` (booleano, opcional): Especifica que o servidor pode atualizar o cache em resposta a uma solicitação se o cache atual estiver vazio, obsoleto ou prestes a ficar obsoleto. If `may-refresh-cache=true`, ou se não for especificado, o servidor poderá iniciar uma tarefa em segundo plano que chamará o Detector de padrões e atualizará o cache. If `may-refresh-cache=false` então o servidor não iniciará nenhuma tarefa de atualização que de outra forma teria sido feita se o cache estivesse vazio ou obsoleto, nesse caso, o relatório estará vazio. Qualquer tarefa de atualização que já esteja em andamento não será afetada por esse parâmetro.
* `return-minimal` (booleano, opcional): Especifica que a resposta do servidor deve incluir apenas o status que contém a indicação de progresso e o status do cache no formato JSON. If `return-minimal=true`, o corpo da resposta será limitado ao objeto de status . If `return-minimal=false`, ou se não for especificado, uma resposta completa será fornecida.
* `log-findings` (booleano, opcional): Especifica que o servidor deve registrar o conteúdo do cache quando ele for criado ou atualizado pela primeira vez. Cada descoberta do cache será registrada como uma sequência de caracteres JSON. Esse registro só ocorrerá se `log-findings=true` e a solicitação gera um novo cache.

Quando um cabeçalho HTTP e um parâmetro de consulta correspondente estiverem presentes, o parâmetro de consulta terá prioridade.

Uma maneira simples de iniciar a geração do relatório por meio da interface HTTP é com o seguinte comando:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`.

Depois que uma solicitação é feita, o cliente não precisa permanecer ativo para que o relatório seja gerado. A geração de relatórios pode ser iniciada com um cliente usando uma solicitação HTTP GET e, depois que o relatório for gerado, visualizada do cache com outro cliente ou com a ferramenta BPA na interface do usuário AEM.

### Respostas {#http-responses}

Os seguintes valores de resposta são possíveis:

* `200 OK`: Indica que a resposta contém conclusões do Detector de padrões que foram geradas dentro do tempo de vida da atualização do cache.
* `202 Accepted`: Usado para indicar que o cache está obsoleto. When `respond-async=true` e `may-refresh-cache=true` essa resposta indica que uma tarefa de atualização está em andamento. When `may-refresh-cache=false` essa resposta simplesmente indica que o cache está obsoleto.
* `400 Bad Request`: indica que houve um erro com a solicitação. Uma mensagem no formato de Detalhes do problema (consulte [RFC 7807](https://tools.ietf.org/html/rfc7807)) fornece mais detalhes.
* `401 Unauthorized`: Indica que a solicitação não foi autorizada.
* `500 Internal Server Error`: indica que ocorreu um erro de servidor interno. Uma mensagem no formato de Detalhes do problema fornece mais detalhes.
* `503 Service Unavailable`: indica que o servidor está ocupado com outra resposta e não pode atender a essa solicitação em tempo hábil. Isso só pode ocorrer quando forem feitas solicitações síncronas. Uma mensagem no formato de Detalhes do problema fornece mais detalhes.

## Informações do administrador

### Ajuste do tempo de vida do cache {#cache-adjustment}

O tempo de vida padrão do cache BPA é de 24 horas. Com a opção de atualizar um relatório e regenerar o cache, tanto na instância do AEM quanto na interface HTTP, esse valor padrão provavelmente será apropriado para a maioria dos usos do BPA. Se o tempo de geração do relatório for particularmente longo para a sua instância do AEM, talvez você queira ajustar o tempo de vida do cache para minimizar a regeneração do relatório.

O valor vitalício do cache é armazenado como a propriedade `maxCacheAge` no seguinte nó do repositório:
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

O valor dessa propriedade é o tempo de vida do cache em segundos. Um administrador pode ajustar a duração do cache usando o CRX/DE Lite.

### Instalação no AEM 6.1 {#installing-on-aem61}

O BPA utiliza uma conta de usuário do serviço do sistema chamada `repository-reader-service` para executar o Detector de padrões. Essa conta está disponível no AEM 6.2 e nas versões posteriores. No AEM 6.1, essa conta deve ser criada *antes de* instalação do BPA, seguindo as seguintes etapas:

1. Siga as instruções em [Criar um novo usuário de serviço](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user) para criar um usuário. Defina a UserID como `repository-reader-service`, deixe o Caminho intermediário vazio e clique na marca de seleção verde.

2. Siga as instruções em [Gerenciar usuários e grupos](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#managing-users-and-groups), especificamente as instruções para adicionar usuários a um grupo, para adicionar o usuário `repository-reader-service` ao grupo `administrators`.

3. Instale o pacote BPA por meio do Gerenciador de pacotes na instância de AEM de origem. (Essa etapa adiciona a alteração de configuração necessária à configuração ServiceUserMapper do usuário de serviço do sistema `repository-reader-service`.)
