---
title: Diretrizes de desenvolvimento do AEM como serviço de nuvem
description: 'A completar '
translation-type: tm+mt
source-git-commit: cedc14b0d71431988238d6cb4256936a5ceb759b

---


# Diretrizes de desenvolvimento do AEM como serviço de nuvem {#aem-as-a-cloud-service-development-guidelines}

## Tarefas em Segundo Plano e Trabalhos de Longa Duração {#background-tasks-and-long-running-jobs}

O código executado como tarefas em segundo plano deve supor que a instância em que está sendo executado pode ser desativada a qualquer momento. Portanto, o código deve ser resiliente e a maior parte das importações retomável. Isso significa que, se o código for executado novamente, ele não deverá começar do início novamente, mas sim perto de onde parou. Embora este não seja um novo requisito para esse tipo de código, no AEM como um serviço em nuvem é mais provável que ocorra uma interrupção de instância.

Para minimizar os problemas, devem ser evitados trabalhos de longa duração, se possível, e eles devem ser retomados no mínimo. Para executar esses trabalhos, use os Trabalhos Sling, que têm uma garantia pelo menos uma vez e, portanto, se forem interrompidos, serão executados novamente o mais rápido possível. Mas eles provavelmente não deveriam começar do início novamente. Para agendar esses trabalhos, é melhor usar o programador [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) como a execução pelo menos uma vez novamente.

O Sling Commons Scheduler não deve ser usado para agendamento, pois a execução não pode ser garantida. É mais provável que seja agendada.

Da mesma forma, com tudo o que está a acontecer de forma assíncrona, como atuar sobre eventos de observação (quer se trate de eventos de JCR ou de eventos de recurso Sling), não se pode garantir que seja executado e, portanto, deve ser usado com cuidado. Isso já é válido para implantações do AEM no momento.

## Conexões HTTP de Saída {#outgoing-http-connections}

É altamente recomendável que todas as conexões HTTP de saída definam tempos limite de conexão e leitura razoáveis. Para códigos que não aplicam esses tempos limite, as instâncias de AEM executadas no AEM como um serviço de nuvem imporão um tempo limite global. Esses valores de tempo limite são de 10 segundos para chamadas de conexão e 60 segundos para chamadas de leitura para conexões usadas pelas seguintes bibliotecas Java populares:

A Adobe recomenda o uso da biblioteca [do](https://hc.apache.org/httpcomponents-client-ga/) Apache HttpComponents Client 4.x para fazer conexões HTTP.

As alternativas que são conhecidas por funcionarem, mas que podem exigir que a dependência seja fornecida por você mesmo, são:

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) e/ou [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (fornecido pelo AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (não recomendado, pois está desatualizado e substituído pela versão 4.x)
* [OK Http](OK Http (Não fornecido pelo AEM)) (Não fornecido pelo AEM)

## Monitoramento e depuração {#monitoring-and-debugging}

### Logs {#logs}

* Para desenvolvimento local, as entradas de registros são gravadas em arquivos locais
   * `./crx-quickstart/logs`
* Em ambientes da Cloud, os desenvolvedores podem baixar os logs por meio do Cloud Manager ou usar uma ferramenta de linha de comando para rastrear os logs. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->
* Para alterar os níveis de log dos ambientes do Cloud, a configuração de Sling Logging OSGI deve ser modificada, seguida de uma reimplantação completa. Como isso não é instantâneo, tenha cuidado ao ativar registros detalhados em ambientes de produção que recebem muito tráfego. No futuro, é possível que haja mecanismos para mudar mais rapidamente o nível de log.

### Thread Dumps {#thread-dumps}

Os despejos de processos em ambientes da Cloud são coletados continuamente, mas não podem ser baixados de uma forma de autoatendimento no momento. Entretanto, entre em contato com o suporte do AEM se os despejos por thread forem necessários para depurar um problema, especificando a janela de hora exata.

### CRX/DE Lite e console do sistema {#crxde-lite-and-system-console}

## Desenvolvimento local {#local-development}

Para o desenvolvimento local, os desenvolvedores têm acesso total ao CRXDE Lite (`/crx/de`) e ao console da Web do AEM (`/system/console`).

Observe que no desenvolvimento local (usando o recurso de início rápido pronto para a nuvem), `/apps` e `/libs` pode ser gravado diretamente, o que é diferente dos ambientes da Cloud nos quais as pastas de nível superior são imutáveis.

## AEM como ferramentas de desenvolvimento de serviços em nuvem {#aem-as-a-cloud-service-development-tools}

Os clientes podem acessar a lista CRXDE no ambiente de desenvolvimento, mas não no estágio ou na produção. O repositório imutável (`/libs`, `/apps`) não pode ser gravado no tempo de execução, portanto, tentar fazer isso resultará em erros.

Um conjunto de ferramentas para depurar o AEM como ambientes de desenvolvedor do Cloud Service está disponível no Developer Console para ambientes de desenvolvimento, estágio e produção. O url pode ser determinado ajustando os urls do autor ou do serviço de publicação da seguinte maneira:

`https://dev-console>-<namespace>.<cluster>.dev.adobeaemcloud.com`

Como atalho, o seguinte comando da CLI do Gerenciador de nuvem pode ser usado para iniciar o console do desenvolvedor com base em um parâmetro de ambiente descrito abaixo:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Consulte [esta página](/help/release-notes/home.md) para obter mais informações.

Os desenvolvedores podem gerar informações de status e resolver vários recursos.

Conforme ilustrado abaixo, as informações de status disponíveis incluem o estado de pacotes, componentes, configurações OSGI, índices de carvalho, serviços OSGI e trabalhos Sling.

![Console de desenvolvedor 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Como ilustrado abaixo, os desenvolvedores podem resolver dependências de pacote e servlets:

![Console de desenvolvedor 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Console de desenvolvedor 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Também útil para depuração, o console Desenvolvedor tem um link para a ferramenta Explicar consulta:

![Console de desenvolvedor 4](/help/implementing/developing/introduction/assets/devconsole4.png)

**Serviço de armazenamento temporário e produção do AEM**

Os clientes não terão acesso à ferramenta para desenvolvedores para ambientes de armazenamento temporário e produção.

### Diagnóstico {#diagnostics}

O console do sistema está disponível para ambientes dev. No entanto, os despejos de diagnóstico para armazenamento temporário e produção não estão disponíveis.