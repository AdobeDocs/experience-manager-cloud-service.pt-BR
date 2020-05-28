---
title: Diretrizes de desenvolvimento do AEM as a Cloud Service
description: A completar
translation-type: tm+mt
source-git-commit: 8e8863d390132ff8df943548b04e9d7c636c4248
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 1%

---


# Diretrizes de desenvolvimento do AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

O código em execução no AEM como um serviço de nuvem deve estar ciente do fato de que ele está sempre em execução em um cluster. Isso significa que há sempre mais de uma instância em execução. O código deve ser resiliente, especialmente porque uma instância pode ser interrompida em qualquer momento.

Durante a atualização do AEM como um serviço em nuvem, haverá instâncias com o código novo e antigo em execução em paralelo. Portanto, o código antigo não deve quebrar com o conteúdo criado pelo novo código e o novo código deve ser capaz de lidar com o conteúdo antigo.
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

Se houver a necessidade de identificar o mestre no cluster, a Apache Sling Discovery API poderá ser usada para detectá-lo.

## Estado na memória {#state-in-memory}

O estado não deve ser mantido na memória, mas persistido no repositório. Caso contrário, esse estado pode ser perdido se uma instância for interrompida.

## Estado no sistema de arquivos {#state-on-the-filesystem}

O sistema de arquivos da instância não deve ser usado no AEM como um serviço em nuvem. O disco é efêmero e será descartado quando as instâncias forem recicladas. A utilização limitada do sistema de arquivos para armazenamentos temporários relacionados com o processamento de pedidos únicos é possível, mas não deve ser abusada para arquivos enormes. Isso ocorre porque pode ter um impacto negativo na cota de uso de recursos e ser executado em limitações de disco.

Como exemplo, onde o uso do sistema de arquivos não é suportado, a camada de publicação deve garantir que todos os dados que precisam ser persistentes sejam enviados para um serviço externo para armazenamento de longo prazo.

## Observação {#observation}

Da mesma forma, com tudo o que está a acontecer de forma assíncrona, como atuar sobre eventos de observação, não se pode garantir que seja executado localmente, pelo que tem de ser utilizado com cuidado. Isso é verdadeiro para eventos JCR e eventos de recursos Sling. No momento em que uma alteração ocorre, a instância pode ser retirada e substituída por uma instância diferente. Outras instâncias na topologia que estão ativas no momento poderão reagir a esse evento. No entanto, neste caso, este não será um evento local e pode até não haver um líder ativo no caso de uma eleição de líder em curso quando o evento for emitido.

## Tarefas em segundo plano e trabalhos de longa execução {#background-tasks-and-long-running-jobs}

O código executado como tarefas em segundo plano deve supor que a instância em que está sendo executado pode ser desativada a qualquer momento. Portanto, o código deve ser resiliente e a maior parte das importações retomável. Isso significa que, se o código for executado novamente, ele não deve ser start do início novamente, mas sim do ponto em que parou. Embora este não seja um novo requisito para esse tipo de código, no AEM como um serviço em nuvem é mais provável que ocorra uma interrupção de instância.

Para minimizar os problemas, devem ser evitados trabalhos de longa duração, se possível, e eles devem ser retomados no mínimo. Para executar esses trabalhos, use os Trabalhos Sling, que têm uma garantia pelo menos uma vez e, portanto, se forem interrompidos, serão executados novamente o mais rápido possível. Mas eles provavelmente não deveriam start desde o início novamente. Para agendar esses trabalhos, é melhor usar o scheduler [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) como essa novamente a execução pelo menos uma vez.

O Scheduler Sling Commons não deve ser usado para agendamento, pois a execução não pode ser garantida. É mais provável que seja agendada.

Da mesma forma, com tudo o que está a acontecer de forma assíncrona, como atuar sobre eventos de observação (quer seja, eventos de JCR ou eventos de recursos de Sling), não se pode garantir que seja executado e, portanto, deve ser usado com cuidado. Isso já é válido para implantações do AEM no momento.

## Conexões HTTP de Saída {#outgoing-http-connections}

É altamente recomendável que todas as conexões HTTP de saída definam tempos limite de conexão e leitura razoáveis. Para códigos que não aplicam esses tempos limite, as instâncias de AEM executadas no AEM como um serviço de nuvem imporão um tempo limite global. Esses valores de tempo limite são de 10 segundos para chamadas de conexão e 60 segundos para chamadas de leitura para conexões usadas pelas seguintes bibliotecas Java populares:

A Adobe recomenda o uso da biblioteca [do](https://hc.apache.org/httpcomponents-client-ga/) Apache HttpComponents Client 4.x para fazer conexões HTTP.

As alternativas que são conhecidas por funcionarem, mas que podem exigir que a dependência seja fornecida por você mesmo, são:

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) e/ou [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (fornecido pelo AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (não recomendado, pois está desatualizado e substituído pela versão 4.x)
* [OK Http](https://square.github.io/okhttp/) (não fornecido pelo AEM)

## Nenhuma personalização de interface clássica {#no-classic-ui-customizations}

O AEM como um serviço em nuvem suporta apenas a interface de usuário para toque para código de cliente de terceiros. A interface clássica não está disponível para personalização.

## Evitar binários nativos {#avoid-native-binaries}

O código não poderá baixar binários em tempo de execução nem modificá-los. Por exemplo, ele não poderá desempacotar `jar` ou `tar` arquivos.

## Nenhum vínculo de fluxo por meio do AEM como um serviço em nuvem {#no-streaming-binaries}

Os binários devem ser acessados por meio do CDN, que disponibilizará binários fora dos principais serviços do AEM.

Por exemplo, não use `asset.getOriginal().getStream()`, o que aciona o download de um binário no disco efêmero do serviço AEM.

## Nenhum agente de replicação reverso {#no-reverse-replication-agents}

A replicação reversa de Publicar para Autor não é compatível com o AEM como um serviço em nuvem. Se tal estratégia for necessária, você poderá usar um armazenamento de persistência externo que seja compartilhado entre o farm de instâncias de Publicação e, potencialmente, o cluster Autor.

## Os agentes de replicação encaminhados podem precisar ser transferidos {#forward-replication-agents}

O conteúdo é replicado de Autor para Publicar por meio de um mecanismo de sub-publicação. Não há suporte para agentes de replicação personalizados.

## Monitoramento e depuração {#monitoring-and-debugging}

### Logs {#logs}

Para desenvolvimento local, as entradas de registros são gravadas em arquivos locais na `/crx-quickstart/logs` pasta.

Nos ambientes da Cloud, os desenvolvedores podem baixar os logs por meio do Cloud Manager ou usar uma ferramenta de linha de comando para rastrear os logs. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Configuração do nível de log**

Para alterar os níveis de log dos ambientes do Cloud, a configuração de Sling Logging OSGI deve ser modificada, seguida de uma reimplantação completa. Como isso não é instantâneo, tenha cuidado ao ativar registros detalhados em ambientes de produção que recebem muito tráfego. No futuro, é possível que haja mecanismos para mudar mais rapidamente o nível de log.

>[!NOTE]
>
>Para executar as alterações de configuração listadas abaixo, é necessário criá-las em um ambiente de desenvolvimento local e, em seguida, enviá-las para um AEM como uma instância do Serviço de nuvem. Para obter mais informações sobre como fazer isso, consulte [Implantação no AEM como um serviço](/help/implementing/deploying/overview.md)em nuvem.

**Ativando o nível de log DEBUG**

O nível de log padrão é INFO, ou seja, as mensagens DEBUG não são registradas.
Para ativar o nível de log DEBUG, defina a variável

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

propriedade para depurar. Não deixe o log no nível de log DEBUG mais tempo do que o necessário, pois ele gera muitos logs.
Uma linha no arquivo de depuração geralmente é start com DEBUG e, em seguida, fornece o nível de log, a ação do instalador e a mensagem de log. Por exemplo:

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

Os níveis de log são os seguintes:

| 0 | Erro fatal | A ação falhou e o instalador não pode continuar. |
|---|---|---|
| 1 | Erro | A ação falhou. A instalação continua, mas uma parte do CRX não foi instalada corretamente e não funcionará. |
| 2 | Aviso | A ação foi bem-sucedida, mas encontrou problemas. O CRX pode ou não funcionar corretamente. |
| 3 | Info | A ação foi bem sucedida. |

### Thread Dumps {#thread-dumps}

Os despejos de processos em ambientes da Cloud são coletados de forma contínua, mas não podem ser baixados de maneira automática no momento. Entretanto, entre em contato com o suporte do AEM se os despejos por thread forem necessários para depurar um problema, especificando a janela de hora exata.

## CRX/DE Lite e console do sistema {#crxde-lite-and-system-console}

### Desenvolvimento local {#local-development}

Para o desenvolvimento local, os desenvolvedores têm acesso total ao CRXDE Lite (`/crx/de`) e ao console da Web do AEM (`/system/console`).

Observe que no desenvolvimento local (usando o recurso de início rápido pronto para nuvem), `/apps` e `/libs` pode ser gravado diretamente, o que é diferente dos ambientes da nuvem nos quais as pastas de nível superior são imutáveis.

### AEM as a Cloud Service Development tools {#aem-as-a-cloud-service-development-tools}

Os clientes podem acessar a lista CRXDE no ambiente de desenvolvimento, mas não no estágio ou na produção. O repositório imutável (`/libs`, `/apps`) não pode ser gravado no tempo de execução, portanto, tentar fazer isso resultará em erros.

Um conjunto de ferramentas para depurar o AEM como ambientes de desenvolvedor do Cloud Service está disponível no Developer Console para ambientes de desenvolvimento, estágio e produção. O url pode ser determinado ajustando-se as urls do serviço Autor ou Publicação da seguinte maneira:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Como atalho, o seguinte comando da CLI do Gerenciador de nuvem pode ser usado para iniciar o console do desenvolvedor com base em um parâmetro de ambiente descrito abaixo:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Consulte [esta página](/help/release-notes/home.md) para obter mais informações.

Os desenvolvedores podem gerar informações de status e resolver vários recursos.

Conforme ilustrado abaixo, as informações de status disponíveis incluem o estado de pacotes, componentes, configurações OSGI, índices de carvalho, serviços OSGI e trabalhos Sling.

![Console de desenvolvedor 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Como ilustrado abaixo, os desenvolvedores podem resolver dependências de pacote e servlets:

![Console de desenvolvedor 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Console de desenvolvedor 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Também útil para depuração, o console Desenvolvedor tem um link para a ferramenta Explorar Query:

![Console de desenvolvedor 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Para programas regulares, o acesso ao Console do desenvolvedor é definido pelo &quot;Gerenciador de nuvem - Função do desenvolvedor&quot; no Admin Console, enquanto para programas de caixa de proteção, o Console do desenvolvedor está disponível para qualquer usuário com um perfil de produto que lhe dá acesso ao AEM como um serviço em nuvem. Para obter mais informações sobre como configurar permissões de usuário, consulte Documentação [do](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)Cloud Manager.



### Serviço de armazenamento temporário e produção do AEM {#aem-staging-and-production-service}

Os clientes não terão acesso à ferramenta para desenvolvedores para ambientes de preparo e produção.

### Monitoramento de desempenho {#performance-monitoring}

A Adobe monitora o desempenho do aplicativo e toma medidas para resolver se a deterioração é observada. No momento, as métricas do aplicativo não podem ser observadas.
