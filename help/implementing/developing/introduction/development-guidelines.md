---
title: Diretrizes de desenvolvimento do AEM as a Cloud Service
description: Conheça as diretrizes para o desenvolvimento AEM as a Cloud Service e sobre as formas importantes com que ele difere das AEM locais e AEM no AMS.
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: 5a8d66c2ca2bed664d127579a8fdbdf3aa45c910
workflow-type: tm+mt
source-wordcount: '2591'
ht-degree: 2%

---

# Diretrizes de desenvolvimento do AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="Diretrizes de desenvolvimento do AEM as a Cloud Service"
>abstract="Conheça as diretrizes para o desenvolvimento AEM as a Cloud Service e sobre as formas importantes com que ele difere das AEM locais e AEM no AMS."
>additional-url="https://video.tv.adobe.com/v/330555?captions=por_br/" text="Demonstração da estrutura do pacote"

O presente documento apresenta orientações para o desenvolvimento AEM as a Cloud Service e sobre formas importantes com que difere das AEM locais e AEM no AMS.

## O Código Deve Ser Sensível A Cluster {#cluster-aware}

O código em execução AEM as a Cloud Service deve estar ciente do fato de que ele está sempre em execução em um cluster. Isso significa que sempre há mais de uma instância em execução. O código deve ser resiliente, especialmente porque uma instância pode ser interrompida em qualquer momento.

Durante a atualização do AEM as a Cloud Service, haverá instâncias com o código antigo e o novo sendo executado simultaneamente. Portanto, o código antigo não deve ser quebrado com o conteúdo criado pelo novo código e o novo código deve ser capaz de lidar com o conteúdo antigo.

Se houver a necessidade de identificar o principal no cluster, a API Apache Sling Discovery poderá ser usada para detectá-lo.

## Estado na memória {#state-in-memory}

O estado não deve ser mantido na memória, mas persistido no repositório. Caso contrário, esse estado poderá ser perdido se uma instância for interrompida.

## Estado do sistema de arquivos {#state-on-the-filesystem}

O sistema de arquivos da instância não deve ser usado AEM as a Cloud Service. O disco é efêmero e será descartado quando as instâncias forem recicladas. A utilização limitada do sistema de arquivos para armazenamento temporário relacionado ao processamento de pedidos únicos é possível, mas não deve ser utilizada abusivamente para arquivos enormes. Isso ocorre porque pode ter um impacto negativo na cota de uso de recursos e encontrar limitações de disco.

Como exemplo, onde o uso do sistema de arquivos não é compatível, a camada Publicar deve garantir que todos os dados que precisam ser persistentes sejam enviados para um serviço externo para armazenamento de longo prazo.

## Observação {#observation}

Da mesma forma, com tudo o que está acontecendo de forma assíncrona como atuar em eventos de observação, não se pode garantir que seja executado localmente e, portanto, deve ser usado com cuidado. Isso é verdadeiro para eventos JCR e eventos de recurso Sling. No momento em que uma alteração ocorre, a instância pode ser removida e substituída por uma instância diferente. Outras instâncias na topologia que estão ativas nesse momento poderão reagir a esse evento. No entanto, neste caso, não se trata de um evento local e pode até não haver um líder ativo no caso de uma eleição de líder em curso, quando o evento é emitido.

## Tarefas em Segundo Plano e Trabalhos de Longa Execução {#background-tasks-and-long-running-jobs}

O código executado como uma tarefa em segundo plano deve supor que a instância em execução pode ser desativada a qualquer momento. Portanto, o código deve ser resiliente e, o mais importante, retomável. Isso significa que, se o código for executado novamente, ele não deverá começar do início novamente, mas antes próximo de onde parou. Embora esse não seja um novo requisito para esse tipo de código, em AEM as a Cloud Service é mais provável que ocorra uma interrupção da instância.

Para minimizar os problemas, os empregos de longa duração devem ser evitados, se possível, e devem ser retomadas no mínimo. Para executar esses trabalhos, use os Trabalhos do Sling, que têm uma garantia pelo menos uma vez e, portanto, se forem interrompidos, serão executados novamente o mais rápido possível. Mas, provavelmente, não deveriam recomeçar desde o início. Para agendar essas tarefas, é melhor usar o [Trabalhos Sling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) o scheduler, dessa forma, garante novamente a execução pelo menos uma vez.

O Sling Commons Scheduler não deve ser usado para agendamento, pois a execução não pode ser garantida. É muito mais provável que seja agendado.

Da mesma forma, com tudo o que está acontecendo de forma assíncrona, como agir em eventos de observação (sejam eventos JCR ou eventos de recurso Sling), não pode ser garantido que seja executado e, portanto, deve ser usado com cuidado. Isso já é verdadeiro para implantações AEM no presente.

## Conexões HTTP de saída {#outgoing-http-connections}

É altamente recomendável que todas as conexões HTTP de saída definam conexões razoáveis e tempos limite de leitura; os valores sugeridos são 1 segundo para o tempo limite da conexão e 5 segundos para o tempo limite de leitura. Os números exatos devem ser determinados com base no desempenho do sistema de back-end que manipula essas solicitações.

Para código que não aplica esses tempos limite, as instâncias AEM executadas em AEM as a Cloud Service impõem um tempo limite global. Esses valores de tempo limite são de 10 segundos para chamadas de conexão e 60 segundos para chamadas de leitura para conexões.

A Adobe recomenda o uso da variável [Biblioteca 4.x do Apache HttpComponents Client](https://hc.apache.org/httpcomponents-client-ga/) para fazer conexões HTTP.

As alternativas que são conhecidas por funcionar, mas que podem exigir que você mesmo forneça a dependência, são:

* [java.net.URL](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) e/ou [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html) (Fornecido por AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (não recomendado, pois está desatualizado e substituído pela versão 4.x)
* [OK Http](https://square.github.io/okhttp/) (Não fornecido pelo AEM)

Ao lado de fornecer limites de tempo, também é necessário lidar com limites de tempo e com códigos de status HTTP inesperados.

## Nenhuma personalização da interface clássica {#no-classic-ui-customizations}

AEM as a Cloud Service suporta apenas a interface do usuário de toque para código de cliente de terceiros. A interface do usuário clássica não está disponível para personalização.

## Evitar binários Nativos {#avoid-native-binaries}

O código não poderá baixar binários no tempo de execução nem modificá-los. Por exemplo, ele não poderá descompactar `jar` ou `tar` arquivos.

## Nenhum binário de transmissão por meio AEM as a Cloud Service {#no-streaming-binaries}

Os binários devem ser acessados por meio da CDN, que fornecerá binários fora dos principais serviços de AEM.

Por exemplo, não use `asset.getOriginal().getStream()`, que dispara o download de um binário no disco efêmero do serviço de AEM.

## Sem agentes de replicação inversa {#no-reverse-replication-agents}

A replicação inversa de Publicar para autor não é compatível com AEM as a Cloud Service. Se tal estratégia for necessária, você poderá usar um armazenamento de persistência externo compartilhado entre o farm de instâncias de Publicação e, potencialmente, o cluster Autor.

## Os agentes de replicação de encaminhamento podem precisar ser transferidos {#forward-replication-agents}

O conteúdo é replicado de Autor para Publicação por meio de um mecanismo de sub-rede. Não há suporte para agentes de replicação personalizados.

## Monitoramento e depuração {#monitoring-and-debugging}

### Logs {#logs}

Para desenvolvimento local, as entradas de logs são gravadas em arquivos locais na variável `/crx-quickstart/logs` pasta.

Em ambientes do Cloud, os desenvolvedores podem baixar logs por meio do Cloud Manager ou usar uma ferramenta de linha de comando para rastrear os logs. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Definir o nível de log**

Para alterar os níveis de log de ambientes do Cloud, a configuração OSGI do Sling Logging deve ser modificada, seguida por uma reimplantação completa. Como isso não é instantâneo, tenha cuidado ao ativar logs detalhados em ambientes de produção que recebem muito tráfego. No futuro, é possível que haja mecanismos para mudar mais rapidamente o nível de log.

>[!NOTE]
>
>Para executar as alterações de configuração listadas abaixo, é necessário criá-las em um ambiente de desenvolvimento local e depois enviá-las para uma instância AEM as a Cloud Service. Para obter mais informações sobre como fazer isso, consulte [Implantação para AEM as a Cloud Service](/help/implementing/deploying/overview.md).

**Ativando o Nível de Log DEBUG**

O nível de log padrão é INFO, ou seja, as mensagens DEBUG não são registradas. Para ativar o nível de log DEBUG, atualize a seguinte propriedade para o modo de depuração.

`/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level`

Por exemplo, defina `/apps/<example>/config/org.apache.sling.commons.log.LogManager.factory.config~<example>.cfg.json` com o seguinte valor.

```json
{
   "org.apache.sling.commons.log.names": [
      "com.example"
   ],
   "org.apache.sling.commons.log.level": "DEBUG",
   "org.apache.sling.commons.log.file": "logs/error.log",
   "org.apache.sling.commons.log.additiv": "false"
}
```

Não deixe o log no nível de log DEBUG por mais tempo do que o necessário, pois isso gera muitas entradas.

Níveis de log discretos podem ser definidos para os diferentes ambientes de AEM usando o direcionamento de configuração OSGi baseado em modo de execução, se for desejável sempre fazer logon em `DEBUG` durante o desenvolvimento. Por exemplo:

| Ambiente | Local de configuração OSGi por modo de execução | `org.apache.sling.commons.log.level` valor da propriedade | | - | - | - | | Desenvolvimento | /apps/example/config/org.apache.sling.commons.log.LogManager.fatory.config~example.cfg.json | DEPURAÇÃO | | Fase | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.fatory.config~example.cfg.json | AVISO | | Produção | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.fatory.config~example.cfg.json | ERRO |

Uma linha no arquivo de depuração geralmente começa com DEBUG e, em seguida, fornece o nível de log, a ação do instalador e a mensagem de log. Por exemplo:

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Os níveis de log são os seguintes:

| 0 | Erro fatal | A ação falhou e o instalador não pode continuar. |
|---|---|---|
| 1 | Erro | A ação falhou. A instalação continua, mas uma parte do CRX não foi instalada corretamente e não funcionará. |
| 2 | Aviso | A ação foi bem-sucedida, mas encontrou problemas. O CRX pode ou não funcionar corretamente. |
| 3 | Info | A ação foi bem sucedida. |

### Despejos de encadeamento {#thread-dumps}

Os despejos de encadeamento em ambientes do Cloud são coletados continuamente, mas não podem ser baixados de maneira automatizada no momento. Enquanto isso, entre em contato com AEM suporte se os despejos de encadeamento forem necessários para depurar um problema, especificando a janela de tempo exata.

## CRX/DE Lite e Console do desenvolvedor {#crxde-lite-and-developer-console}

### Desenvolvimento local {#local-development}

Para desenvolvimento local, os desenvolvedores têm acesso total ao CRXDE Lite (`/crx/de`) e o Console da Web AEM (`/system/console`).

Observe que, no desenvolvimento local (usando o SDK), `/apps` e `/libs` O pode ser gravado diretamente no , o que é diferente dos ambientes do Cloud, onde as pastas de nível superior são imutáveis.

### AEM ferramentas de desenvolvimento as a Cloud Service {#aem-as-a-cloud-service-development-tools}

Os clientes podem acessar o CRXDE lite no ambiente de desenvolvimento do nível de criação, mas não no ambiente de preparo ou produção. O repositório imutável (`/libs`, `/apps`) não pode ser gravado em no tempo de execução, portanto, tentar fazer isso resultará em erros.

Em vez disso, o Navegador de Repositório pode ser iniciado a partir do Console do Desenvolvedor, fornecendo uma visualização somente leitura no repositório para todos os ambientes nos níveis de criação, publicação e visualização. Leia mais sobre o Navegador de Repositório [here](/help/implementing/developing/tools/repository-browser.md).

Um conjunto de ferramentas para depurar AEM ambientes de desenvolvedor as a Cloud Service está disponível no Console do desenvolvedor para ambientes RDE, dev, stage e production. O url pode ser determinado ajustando os urls do serviço de Autor ou Publicação da seguinte maneira:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Como atalho, o seguinte comando da CLI do Cloud Manager pode ser usado para iniciar o console do desenvolvedor com base em um parâmetro de ambiente descrito abaixo:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Consulte [esta página](/help/release-notes/home.md) para obter mais informações.

Os desenvolvedores podem gerar informações de status e resolver vários recursos.

Conforme ilustrado abaixo, as informações de status disponíveis incluem o estado de pacotes, componentes, configurações OSGI, índices de oak, serviços OSGI e tarefas Sling.

![Console de desenvolvimento 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Conforme ilustrado abaixo, os desenvolvedores podem resolver dependências de pacote e servlets:

![Console de desenvolvimento 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Console de desenvolvimento 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Também útil para depuração, o console Desenvolvedor tem um link para a ferramenta Explicar Consulta:

![Console de desenvolvimento 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Para programas de Produção, o acesso ao Console do Desenvolvedor é definido pela &quot;Função do Desenvolvedor - Cloud Manager&quot; no Admin Console, enquanto para programas de sandbox, o Console do Desenvolvedor está disponível para qualquer usuário com um perfil de produto que dá acesso a AEM as a Cloud Service. Para todos os programas, &quot;Cloud Manager - Função do desenvolvedor&quot; é necessário para despejos de status e o navegador do repositório e os usuários também devem ser definidos no Perfil de produto Usuários do AEM ou Administradores do AEM nos serviços de criação e publicação para visualizar dados de ambos os serviços. Para obter mais informações sobre como configurar permissões de usuário, consulte [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Monitoramento de desempenho {#performance-monitoring}

O Adobe monitora o desempenho do aplicativo e toma medidas para corrigir se a deterioração é observada. No momento, as métricas do aplicativo não podem ser observadas.

## Envio de email {#sending-email}

As seções abaixo descrevem como solicitar, configurar e enviar emails.

>[!NOTE]
>
>O serviço de email pode ser configurado com suporte a OAuth2. Para obter mais informações, consulte [Suporte OAuth2 para o serviço de email](/help/security/oauth2-support-for-mail-service.md).

### Ativar Email de Saída {#enabling-outbound-email}

Por padrão, as portas usadas para enviar emails estão desativadas. Para ativar uma porta, configure [rede avançada](/help/security/configuring-advanced-networking.md), certificando-se de configurar, para cada ambiente necessário, a variável `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` as regras de encaminhamento de porta do endpoint, que mapeiam a porta desejada (por exemplo, 465 ou 587) para uma porta proxy.

É recomendável configurar uma rede avançada com um `kind` parâmetro definido como `flexiblePortEgress` já que o Adobe pode otimizar o desempenho do tráfego flexível de saída da porta. Se um endereço IP de saída exclusivo for necessário, escolha um `kind` parâmetro de `dedicatedEgressIp`. Se você já tiver configurado a VPN por outros motivos, também poderá usar o endereço IP exclusivo fornecido pela variação avançada de rede.

Você deve enviar emails por meio de um servidor de email, em vez de diretamente para clientes de email. Caso contrário, os emails poderão ser bloqueados.

### Envio de emails {#sending-emails}

O [Serviço OSGI do Day CQ Mail Service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) O deve ser usado e os emails devem ser enviados ao servidor de email indicado na solicitação de suporte, em vez de diretamente aos recipients.

### Configuração {#email-configuration}

Os emails no AEM devem ser enviados usando o [Serviço OSGi do Day CQ Mail Service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Consulte a [Documentação do AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) para obter detalhes sobre como definir configurações de email. Para AEM as a Cloud Service, observe os seguintes ajustes necessários na `com.day.cq.mailer.DefaultMailService OSGI` serviço:

* O nome do host do servidor SMTP deve ser definido como $[env:AEM_PROXY_HOST;default=proxy.túnel]
* A porta do servidor SMTP deve ser definida com o valor da porta proxy original definida no parâmetro portForwards usado na chamada da API ao configurar a rede avançada. Por exemplo, 30465 (em vez de 465)

A porta do servidor SMTP deve ser definida como `portDest` valor definido no parâmetro portForwards usado na chamada da API ao configurar a rede avançada e o `portOrig` deve ser um valor significativo que esteja dentro do intervalo necessário de 30000 - 30999. Por exemplo, se a porta do servidor SMTP for 465, a porta 30465 deverá ser usada como a `portOrig` valor.

Nesse caso, e supondo que o SSL precise ser habilitado, na configuração da variável **Day CQ Mail Service OSGI** serviço:

* Definir `smtp.port` para `30465`
* Definir `smtp.ssl` para `true`

Como alternativa, se a porta de destino for 587, um `portOrig` deve ser usado o valor 30587. E supondo que o SSL deveria ser desativado, a configuração do serviço OSGI do Day CQ Mail Service:

* Definir `smtp.port` para `30587`
* Definir `smtp.ssl` para `false`

O `smtp.starttls` será automaticamente definida por AEM as a Cloud Service em tempo de execução para um valor apropriado. Assim, se `smtp.ssl` está definido como verdadeiro, `smtp.startls` é ignorada. If `smtp.ssl` está definido como falso, `smtp.starttls` está definida como true. Isso não depende da variável `smtp.starttls` valores definidos na configuração OSGI.


Como opção, o Serviço de email pode ser configurado com suporte a OAuth2. Para obter mais informações, consulte [Suporte OAuth2 para o serviço de email](/help/security/oauth2-support-for-mail-service.md).

### Configuração de email herdada {#legacy-email-configuration}

Antes da versão 2021.9.0, o email era configurado por meio de uma solicitação de suporte ao cliente. Observe os seguintes ajustes necessários para `com.day.cq.mailer.DefaultMailService OSGI` serviço:

AEM as a Cloud Service requer que o correio seja enviado através da porta 465. Se um servidor de email não suportar a porta 465, a porta 587 poderá ser usada, desde que a opção TLS esteja habilitada.

Se a porta 465 tiver sido solicitada:

* set `smtp.port` para `465`
* set `smtp.ssl` para `true`

e se a porta 587 tiver sido solicitada:

* set `smtp.port` para `587`
* set `smtp.ssl` para `false`

O `smtp.starttls` será automaticamente definida por AEM as a Cloud Service em tempo de execução para um valor apropriado. Assim, se `smtp.ssl` está definido como verdadeiro, `smtp.startls` é ignorada. If `smtp.ssl` está definido como falso, `smtp.starttls` está definida como true. Isso não depende da variável `smtp.starttls` valores definidos na configuração OSGI.

O host do servidor SMTP deve ser definido como o do seu servidor de email.

## Evite propriedades grandes de vários valores {#avoid-large-mvps}

O repositório de conteúdo Oak subjacente AEM as a Cloud Service não deve ser usado com um número excessivo de propriedades de vários valores (MVPs). Um princípio básico é manter os MVPs abaixo de 1000. No entanto, o desempenho real depende de muitos fatores.

Os avisos são registrados por padrão após mais de 1000. Elas são semelhantes ao seguinte.

```text
org.apache.jackrabbit.oak.jcr.session.NodeImpl Large multi valued property [/path/to/property] detected (1029 values). 
```

Grandes MVPs podem levar a erros devido ao documento MongoDB exceder 16 MB, resultando em erros semelhantes aos seguintes.

```text
Caused by: com.mongodb.MongoWriteException: Resulting document after update is larger than 16777216
```

Consulte a [Documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property) para obter mais detalhes.

## [!DNL Assets] diretrizes de desenvolvimento e casos de uso {#use-cases-assets}

Para saber mais sobre casos de uso de desenvolvimento, recomendações e materiais de referência do Assets as a Cloud Service, consulte [Referências do desenvolvedor para Assets.](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis)
