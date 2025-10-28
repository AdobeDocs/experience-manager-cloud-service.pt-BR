---
title: Diretrizes de desenvolvimento do AEM as a Cloud Service
description: Conheça as diretrizes para desenvolvimento no AEM as a Cloud Service e as principais diferenças em relação ao AEM local e ao AEM no AMS.
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
feature: Developing
role: Admin, Architect, Developer
source-git-commit: c7ba218faac76c9f43d8adaf5b854676001344cd
workflow-type: tm+mt
source-wordcount: '2768'
ht-degree: 4%

---

# Diretrizes de desenvolvimento do AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="Diretrizes de desenvolvimento do AEM as a Cloud Service"
>abstract="Conheça as diretrizes para desenvolvimento no AEM as a Cloud Service e as principais diferenças em relação ao AEM local e ao AEM no AMS."
>additional-url="https://video.tv.adobe.com/v/330555/" text="Demonstração da estrutura do pacote"

Este documento apresenta diretrizes para desenvolvimento no AEM as a Cloud Service e sobre maneiras importantes de diferir do AEM no local e do AEM no AMS.

## O Código Deve Reconhecer Cluster {#cluster-aware}

O código em execução no AEM as a Cloud Service deve reconhecer o fato de que ele está sempre em execução em um cluster. Isso significa que sempre há mais de uma instância em execução. O código deve ser resiliente, especialmente porque uma instância pode ser interrompida a qualquer momento.

Durante a atualização do AEM as a Cloud Service, há instâncias com código novo e antigo em execução em paralelo. Portanto, o código antigo não deve quebrar com o conteúdo criado pelo novo código e o novo código deve ser capaz de lidar com o conteúdo antigo.

Se for necessário identificar o principal no cluster, a API de descoberta do Apache Sling poderá ser usada para detectá-lo.

## Estado na memória {#state-in-memory}

O estado não deve ser mantido na memória, mas mantido no repositório. Caso contrário, esse estado poderá ser perdido se uma instância for interrompida.

## Estado no sistema de arquivos {#state-on-the-filesystem}

Não use o sistema de arquivos da instância no AEM as a Cloud Service. O disco é efêmero e é descartado quando as instâncias são recicladas. O uso limitado do sistema de arquivos para armazenamento temporário relacionado ao processamento de solicitações únicas é possível, mas não deve ser usado para arquivos enormes. Isso ocorre porque pode ter um impacto negativo na cota de uso do recurso e gerar limitações de disco.

Como exemplo em que o uso do sistema de arquivos não é compatível, a camada de Publicação deve garantir que todos os dados que devem ser mantidos sejam enviados para um serviço externo para armazenamento de longo prazo.

## Observação {#observation}

Da mesma forma, com tudo o que está acontecendo de forma assíncrona, como agir em eventos de observação, não é possível garantir que seja executado localmente e, portanto, deve ser usado com cuidado. Isso é verdadeiro para eventos JCR e eventos de recursos Sling. Quando uma alteração estiver ocorrendo, a instância poderá ser desativada e substituída por outra instância. Outras instâncias na topologia que estão ativas nesse momento podem reagir a esse evento. Nesse caso, no entanto, não será um evento local e pode até não haver líder ativo no caso de uma eleição de líder em andamento quando o evento for emitido.

## Tarefas de segundo plano e tarefas de longa duração {#background-tasks-and-long-running-jobs}

O código executado como uma tarefa em segundo plano deve supor que a instância em que está sendo executada pode ser desativada a qualquer momento. Portanto, o código deve ser resiliente e, o mais importante, retomável. Isso significa que, se o código for executado novamente, ele não deverá começar do início novamente, mas sim próximo de onde parou. Embora esse não seja um requisito novo para esse tipo de código, no AEM as a Cloud Service é mais provável que ocorra uma interrupção de instância.

Para minimizar o problema, se possível, as tarefas de longa duração devem ser evitadas e devem ser retomadas no mínimo. Para executar esses trabalhos, use o Sling Jobs, que têm uma garantia de pelo menos uma vez e, portanto, se forem interrompidos, serão reexecutados o mais rápido possível. Mas elas provavelmente não devem recomeçar do início. Para agendar esses trabalhos, é melhor usar o agendador [Trabalhos do Sling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing), pois isso garante novamente a execução de pelo menos uma vez.

Não use o Sling Commons Scheduler para agendamento, pois a execução não pode ser garantida. É mais provável que ela esteja programada.

Da mesma forma, com tudo o que está acontecendo de forma assíncrona, como a atuação em eventos de observação (ou seja, eventos JCR ou eventos de recursos Sling), não é garantido que seja executado e, portanto, deve ser usado com cuidado. Isso já é verdadeiro para implantações do AEM no presente.

## Conexões HTTP de Saída {#outgoing-http-connections}

É altamente recomendável que qualquer conexão HTTP de saída defina tempos limite de conexão e leitura razoáveis; os valores sugeridos são 1 segundo para o tempo limite da conexão e 5 segundos para o tempo limite de leitura. Os números exatos devem ser determinados com base no desempenho do sistema de back-end que lida com essas solicitações.

Para código que não aplica esses tempos limite, as instâncias do AEM em execução no AEM as a Cloud Service aplicarão um tempo limite global. Esses valores de tempo limite são de 10 segundos para chamadas de conexão e 60 segundos para chamadas de leitura para conexões.

A Adobe recomenda o uso da [biblioteca Apache HttpComponents Client 4.x](https://hc.apache.org/httpcomponents-client-ga/) fornecida para fazer conexões HTTP.

Alternativas que são conhecidas por funcionar, mas podem exigir que você forneça a dependência:

* [java.net.URL](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) e/ou [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html) (Fornecido pelo AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (não recomendado, pois está desatualizado e foi substituído pela versão 4.x)
* [OK Http](https://square.github.io/okhttp/) (Não fornecido pelo AEM)

Além de fornecer tempos limite, também deve ser implementado um tratamento adequado desses tempos limite e códigos de status HTTP inesperados.

## Lidar com limites de taxa de solicitação {#rate-limit-handling}

Quando a taxa de solicitações recebidas para o AEM excede os níveis íntegros, o AEM responde a novas solicitações com o código de erro HTTP 429. Os aplicativos que fazem chamadas programáticas para o AEM podem considerar a codificação de forma defensiva, tentando novamente após alguns segundos com uma estratégia de retirada exponencial. Antes de meados de agosto de 2023, o AEM respondia à mesma condição com o código de erro HTTP 503.

## Nenhuma personalização da interface clássica {#no-classic-ui-customizations}

O AEM as a Cloud Service só oferece suporte à interface para toque para código de cliente de terceiros. A interface clássica não está disponível para personalização.

## Não há binários nativos ou bibliotecas nativas {#avoid-native-binaries}

Os binários e bibliotecas nativos não devem ser implantados ou instalados em ambientes de nuvem.

Além disso, o código não deve tentar baixar binários nativos ou extensões Java nativas (por exemplo, JNI) no tempo de execução.

## Nenhum binário de transmissão por meio do AEM as a Cloud Service {#no-streaming-binaries}

Os binários devem ser acessados por meio da CDN, que fornecerá binários fora dos serviços principais da AEM.

Por exemplo, não use `asset.getOriginal().getStream()`, que dispara o download de um binário no disco efêmero do serviço AEM.

## Nenhum agente de replicação reversa {#no-reverse-replication-agents}

A replicação reversa de Publicar para Autor não é compatível com o AEM as a Cloud Service. Se essa estratégia for necessária, você poderá usar um armazenamento de persistência externo que é compartilhado entre o farm de instâncias de Publicação e possivelmente o cluster Autor.

## Talvez seja necessário transferir os agentes de replicação direta {#forward-replication-agents}

O conteúdo é replicado do Autor para a Publicação por meio de um mecanismo pub-sub. Os agentes de replicação personalizados não são compatíveis.

## Sem sobrecarga nos ambientes de desenvolvimento {#overloading-dev-envs}

Os ambientes de produção são dimensionados mais alto para garantir uma operação estável, enquanto os ambientes de preparo são dimensionados como ambientes de produção para garantir testes realistas em condições de produção.

Os ambientes de desenvolvimento e os ambientes de desenvolvimento rápido devem se limitar ao desenvolvimento, à análise de erros e aos testes funcionais, e não foram projetados para processar altas cargas de trabalho nem grandes quantidades de conteúdo.

Por exemplo, alterar uma definição de índice em um grande repositório de conteúdo em um ambiente de desenvolvimento pode resultar em reindexação, resultando em muito processamento. Os testes que exigem conteúdo substancial devem ser executados em ambientes de preparo.

## Monitoramento e depuração {#monitoring-and-debugging}

### Logs {#logs}

Para desenvolvimento local, as entradas de log são gravadas em arquivos locais na pasta `/crx-quickstart/logs`.

Em ambientes na nuvem, os desenvolvedores podem baixar logs por meio do Cloud Manager ou usar uma ferramenta de linha de comando para rastrear os logs. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Custom logs are not supported and so all logs should be output to the error log. -->

**Definindo o Nível de Log**

Para alterar os níveis de log para ambientes em nuvem, a configuração OSGI do Sling Logging deve ser modificada, seguida de uma reimplantação completa. Como isso não é instantâneo, tenha cuidado ao ativar registros detalhados em ambientes de produção que recebem muito tráfego. No futuro, é possível que haja mecanismos para alterar mais rapidamente o nível de log.

>[!NOTE]
>
>Para executar as alterações de configuração listadas abaixo, crie-as em um ambiente de desenvolvimento local e, em seguida, envie-as para uma instância do AEM as a Cloud Service. Para obter mais informações sobre como fazer isso, consulte [Implantação no AEM as a Cloud Service](/help/implementing/deploying/overview.md).

**Ativando o Nível de Log DEBUG**

O nível de log padrão é INFO, ou seja, as mensagens DEBUG não são registradas. Para ativar o nível de log DEBUG, atualize a propriedade a seguir para o modo de depuração.

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

Níveis de log discretos podem ser definidos para os diferentes ambientes do AEM usando o direcionamento de configuração OSGi baseada em modo de execução se for desejável sempre registrar em `DEBUG` durante o desenvolvimento. Por exemplo:

| Ambiente | Localização da configuração do OSGi por modo de execução | Valor da propriedade `org.apache.sling.commons.log.level` |
| - | - | - |
| Desenvolvimento | /apps/example/config/org.apache.sling.commons.log.LogManager.fatory.config~example.cfg.json | DEPURAR |
| Fase | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.fatory.config~example.cfg.json | AVISO |
| Produção | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.fatory.config~example.cfg.json | ERRO |

Uma linha no arquivo de depuração geralmente começa com DEBUG e, em seguida, fornece o nível de log, a ação do instalador e a mensagem de log. Por exemplo:

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Os níveis de log são os seguintes:

| 0 | Erro fatal | A ação falhou e o instalador não pode continuar. |
|---|---|---|
| 1 | Erro | Falha na ação. A instalação continua, mas uma parte do CRX não foi instalada corretamente e não funcionará. |
| 2 | Aviso | A ação foi bem-sucedida, mas encontrou problemas. O CRX pode ou não funcionar corretamente. |
| 3 | Informações | A ação foi bem-sucedida. |

### Despejos de encadeamento {#thread-dumps}

Os despejos de thread em ambientes na nuvem são coletados de forma contínua, mas não podem ser baixados de forma automatizada no momento. Enquanto isso, entre em contato com o suporte da AEM se os despejos de thread forem necessários para depurar um problema, especificando a janela de tempo exata.

## CRX/DE Lite e AEM as a Cloud Service Developer Console {#crxde-lite-and-developer-console}

### Desenvolvimento local {#local-development}

Para desenvolvimento local, os desenvolvedores têm acesso total ao CRXDE Lite (`/crx/de`) e ao AEM Web Console (`/system/console`).

No desenvolvimento local (usando o SDK), `/apps` e `/libs` podem ser gravados diretamente, o que é diferente dos ambientes em Nuvem, onde essas pastas de nível superior são imutáveis.

### Ferramentas de desenvolvimento do AEM as a Cloud Service {#aem-as-a-cloud-service-development-tools}

>[!NOTE]
>O AEM as a Cloud Service Developer Console não deve ser confundido com o [*Adobe Developer Console*](https://developer.adobe.com/developer-console/) de nome semelhante.
>

>[!NOTE]
>Alguns clientes terão a opção de experimentar uma experiência renovada para o AEM Cloud Service Developer Console. Consulte [este artigo](/help/implementing/developing/introduction/aem-developer-console.md) para obter mais informações.

Os clientes podem acessar o CRXDE lite no ambiente de desenvolvimento do nível do autor, mas não no ambiente de preparo ou produção. O repositório imutável (`/libs`, `/apps`) não pode ser gravado no tempo de execução, portanto, tentar fazer isso resultará em erros.

Em vez disso, o Navegador do repositório pode ser iniciado no AEM as a Cloud Service Developer Console, fornecendo uma visualização somente leitura no repositório para todos os ambientes nos níveis de criação, publicação e visualização. Para obter mais informações, consulte o [Navegador do Repositório](/help/implementing/developing/tools/repository-browser.md).

Um conjunto de ferramentas para depurar ambientes de desenvolvedor do AEM as a Cloud Service está disponível no AEM as a Cloud Service Developer Console para ambientes de RDE, desenvolvimento, preparo e produção. O URL pode ser determinado ajustando os URLs de serviço do Autor ou de Publicação da seguinte maneira:

`https://dev-console-<namespace>.<cluster>.dev.adobeaemcloud.com`

Como atalho, o seguinte comando da CLI do Cloud Manager pode ser usado para iniciar o AEM as a Cloud Service Developer Console com base em um parâmetro de ambiente descrito abaixo:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Consulte as [Informações da versão](/help/release-notes/home.md) para obter mais informações.

Os desenvolvedores podem gerar informações de status e resolver vários recursos.

Como ilustrado abaixo, as informações de status disponíveis incluem o estado dos pacotes, componentes, configurações OSGI, índices Oak, serviços OSGI e trabalhos Sling.

![Dev Console 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Como ilustrado abaixo, os desenvolvedores podem resolver as dependências de pacote e os servlets:

![Dev Console 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Dev Console 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Também útil para depuração, o AEM as a Cloud Service Developer Console tem um link para a ferramenta Explicar consulta:

![Dev Console 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Para programas de produção, o acesso ao AEM as a Cloud Service Developer Console é definido pela &quot;Função do desenvolvedor - Cloud Manager&quot; no Adobe Admin Console, enquanto para programas de sandbox, o AEM as a Cloud Service Developer Console está disponível para qualquer usuário com um perfil de produto que dê acesso ao AEM as a Cloud Service. Para todos os programas, &quot;Cloud Manager - Função do desenvolvedor&quot; é necessário para despejos de status, e o navegador do repositório e os usuários também devem ser definidos no Perfil de produto Usuários do AEM ou Administradores do AEM, nos serviços de criação e publicação, para exibir dados de ambos os serviços. Para obter mais informações sobre como configurar permissões de usuário, consulte a [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Monitoramento de desempenho {#performance-monitoring}

A Adobe monitora o desempenho dos aplicativos e toma medidas para corrigir qualquer deterioração observada. Atualmente, as métricas do aplicativo não podem ser observadas.

## Enviar email {#sending-email}

As seções abaixo descrevem como solicitar, configurar e enviar emails.

>[!NOTE]
>
>O Serviço de e-mail pode ser configurado com suporte ao OAuth2. Para obter mais informações, consulte [Suporte do OAuth2 para o Serviço de Email](/help/security/oauth2-support-for-mail-service.md).

### Ativação de email de saída {#enabling-outbound-email}

Por padrão, as portas usadas para enviar email são desativadas. Para ativar uma porta, configure a [rede avançada](/help/security/configuring-advanced-networking.md), certificando-se de definir para cada ambiente necessário as regras de encaminhamento de porta do ponto de extremidade `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`, que mapeia a porta pretendida (por exemplo, 465 ou 587) para uma porta proxy.

É recomendável configurar a rede avançada com um parâmetro `kind` definido como `flexiblePortEgress`, já que o Adobe pode otimizar o desempenho do tráfego de saída de porta flexível. Se um endereço IP de saída exclusivo for necessário, escolha um parâmetro `kind` de `dedicatedEgressIp`. Se você já tiver configurado a VPN por outros motivos, também poderá usar o endereço IP exclusivo fornecido por essa variação avançada de rede.

Você deve enviar um email por meio de um servidor de email, em vez de diretamente para clientes de email. Caso contrário, os emails poderão ser bloqueados.

### Envio de emails {#sending-emails}

O [Serviço OSGI do Day CQ Mail Service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) deve ser usado, e os emails devem ser enviados para o servidor de email indicado na solicitação de suporte, em vez de diretamente para os destinatários.

### Configuração {#email-configuration}

Os emails no AEM devem ser enviados usando o [Serviço OSGi do Day CQ Mail Service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Consulte a [documentação do AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) para obter detalhes sobre como definir configurações de email. Para o AEM as a Cloud Service, observe os seguintes ajustes necessários para o serviço `com.day.cq.mailer.DefaultMailService OSGI`:

* O nome de host do servidor SMTP deve ser definido como $[env:AEM_PROXY_HOST;default=proxy.tunnel]
* A porta do servidor SMTP deve ser definida com o valor da porta proxy original definida no parâmetro portForwards usado na chamada de API ao configurar a rede avançada. Por exemplo, 30465 (em vez de 465)

A porta do servidor SMTP deve ser definida como o valor `portDest` definido no parâmetro portForwards usado na chamada de API ao configurar a rede avançada, e o valor `portOrig` deve ser um valor significativo dentro do intervalo necessário de 30000 a 30999. Por exemplo, se a porta do servidor SMTP for 465, a porta 30465 deverá ser usada como o valor `portOrig`.

Nesse caso, e supondo que o SSL precise ser habilitado, na configuração do serviço OSGI **do** Day CQ Mail Service:

* Configurar `smtp.port` para `30465`
* Configurar `smtp.ssl` para `true`

Como alternativa, se a porta de destino for 587, um valor `portOrig` de 30587 deverá ser usado. E supondo que o SSL deve ser desativado, a configuração do serviço OSGI do Day CQ Mail Service:

* Configurar `smtp.port` para `30587`
* Configurar `smtp.ssl` para `false`

A propriedade `smtp.starttls` será automaticamente definida pelo AEM as a Cloud Service em tempo de execução como um valor apropriado. Assim, se `smtp.ssl` estiver definido como verdadeiro, `smtp.startls` será ignorado. Se `smtp.ssl` estiver definido como falso, `smtp.starttls` será definido como verdadeiro. Isso ocorre independentemente dos valores `smtp.starttls` definidos na sua configuração OSGI.


O Serviço de e-mail pode, opcionalmente, ser configurado com suporte para OAuth2. Para obter mais informações, consulte [Suporte do OAuth2 para o Serviço de Email](/help/security/oauth2-support-for-mail-service.md).

### Configuração de email herdada {#legacy-email-configuration}

Antes da versão 2021.9.0, o email era configurado por meio de uma solicitação de suporte ao cliente. Observe os seguintes ajustes necessários para o serviço `com.day.cq.mailer.DefaultMailService OSGI`:

O AEM as a Cloud Service exige que o email seja enviado pela porta 465. Se um servidor de e-mail não suportar a porta 465, a porta 587 poderá ser usada, desde que a opção TLS esteja habilitada.

Se a porta 465 tiver sido solicitada:

* definir `smtp.port` como `465`
* definir `smtp.ssl` como `true`

e se a porta 587 tiver sido solicitada:

* definir `smtp.port` como `587`
* definir `smtp.ssl` como `false`

A propriedade `smtp.starttls` será automaticamente definida pelo AEM as a Cloud Service em tempo de execução como um valor apropriado. Assim, se `smtp.ssl` estiver definido como verdadeiro, `smtp.startls` será ignorado. Se `smtp.ssl` estiver definido como falso, `smtp.starttls` será definido como verdadeiro. Isso ocorre independentemente dos valores `smtp.starttls` definidos na sua configuração OSGI.

O host do servidor SMTP deve ser definido como o do seu servidor de e-mail.

## Evite propriedades grandes de vários valores {#avoid-large-mvps}

O repositório de conteúdo do Oak subjacente ao AEM as a Cloud Service não deve ser usado com um número excessivo de propriedades de vários valores (MVPs). Uma regra geral é manter os MVPs abaixo de 1000. No entanto, o desempenho real depende de muitos fatores.

Os avisos são registrados por padrão depois de exceder 1000. Elas são semelhantes às seguintes.

```text
org.apache.jackrabbit.oak.jcr.session.NodeImpl Large multi valued property [/path/to/property] detected (1029 values). 
```

MVPs grandes podem levar a erros porque o documento MongoDB excede 16 MB, resultando em erros semelhantes aos seguintes.

```text
Caused by: com.mongodb.MongoWriteException: Resulting document after update is larger than 16777216
```

Consulte a [documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property) para obter mais detalhes.

## Diretrizes de desenvolvimento e casos de uso do [!DNL Assets] {#use-cases-assets}

Para saber mais sobre os casos de uso de desenvolvimento, as recomendações e os materiais de referência do Assets as a Cloud Service, consulte [Referências do desenvolvedor para o Assets](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
