---
title: Diretrizes de desenvolvimento do AEM as a Cloud Service
description: Conheça as diretrizes para desenvolvimento no AEM as a Cloud Service e as principais diferenças em relação ao AEM local e ao AEM no AMS.
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: 1683819d4f11d4503aa0d218ecff6375fc5c54d1
workflow-type: tm+mt
source-wordcount: '2733'
ht-degree: 4%

---

# Diretrizes de desenvolvimento do AEM as a Cloud Service {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="Diretrizes de desenvolvimento do AEM as a Cloud Service"
>abstract="Conheça as diretrizes para desenvolvimento no AEM as a Cloud Service e as principais diferenças em relação ao AEM local e ao AEM no AMS."
>additional-url="https://video.tv.adobe.com/v/330555?captions=por_br/" text="Demonstração da estrutura do pacote"

Este documento apresenta diretrizes para o desenvolvimento do AEM as a Cloud Service e sobre importantes maneiras em que ele difere do AEM em instalações e do AEM na AMS.

## O Código Deve Reconhecer Cluster {#cluster-aware}

O código em execução no AEM as a Cloud Service deve estar ciente do fato de que ele está sempre em execução em um cluster. Isso significa que sempre há mais de uma instância em execução. O código deve ser resiliente, especialmente porque uma instância pode ser interrompida a qualquer momento.

Durante a atualização do AEM as a Cloud Service, há instâncias com códigos antigos e novos sendo executados em paralelo. Portanto, o código antigo não deve quebrar com o conteúdo criado pelo novo código e o novo código deve ser capaz de lidar com o conteúdo antigo.

Se for necessário identificar o principal no cluster, a API de descoberta do Apache Sling poderá ser usada para detectá-lo.

## Estado na memória {#state-in-memory}

O estado não deve ser mantido na memória, mas mantido no repositório. Caso contrário, esse estado poderá ser perdido se uma instância for interrompida.

## Estado no sistema de arquivos {#state-on-the-filesystem}

O sistema de arquivos da instância não deve ser usado no AEM as a Cloud Service. O disco é efêmero e é descartado quando as instâncias são recicladas. O uso limitado do sistema de arquivos para armazenamento temporário relacionado ao processamento de solicitações únicas é possível, mas não deve ser usado para arquivos enormes. Isso ocorre porque pode ter um impacto negativo na cota de uso do recurso e gerar limitações de disco.

Como exemplo em que o uso do sistema de arquivos não é compatível, a camada de Publicação deve garantir que todos os dados que precisam ser mantidos sejam enviados para um serviço externo para armazenamento de longo prazo.

## Observação {#observation}

Semelhante, com tudo o que está acontecendo de forma assíncrona, como a ação em eventos de observação, não é possível garantir que seja executado localmente e, portanto, deve ser usado com cuidado. Isso é verdadeiro para eventos JCR e eventos de recursos Sling. No momento em que uma alteração estiver ocorrendo, a instância poderá ser desativada e substituída por outra instância. Outras instâncias na topologia que estão ativas nesse momento podem reagir a esse evento. Nesse caso, no entanto, não será um evento local e pode até não haver líder ativo no caso de uma eleição de líder em andamento quando o evento for emitido.

## Tarefas de segundo plano e tarefas de longa duração {#background-tasks-and-long-running-jobs}

O código executado como tarefas em segundo plano deve supor que a instância em que está sendo executada pode ser desativada a qualquer momento. Portanto, o código deve ser resiliente e, o mais importante, retomável. Isso significa que, se o código for executado novamente, ele não deverá começar do início novamente, mas sim próximo de onde parou. Embora esse não seja um requisito novo para esse tipo de código, no AEM as a Cloud Service, é mais provável que uma ocorrência seja interrompida.

Para minimizar o problema, se possível, a execução de trabalhos de longa duração deve ser evitada, e eles devem ser retomáveis no mínimo. Para executar esses trabalhos, use o Sling Jobs, que têm uma garantia de pelo menos uma vez e, portanto, se forem interrompidos, serão reexecutados o mais rápido possível. Mas elas provavelmente não devem recomeçar do início. Para agendar esses trabalhos, é melhor usar a variável [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) scheduler, pois isso garante novamente a execução de pelo menos uma vez.

O Sling Commons Scheduler não deve ser usado para agendamento, pois a execução não pode ser garantida. É mais provável que ela esteja programada.

Da mesma forma, com tudo o que está acontecendo de forma assíncrona, como a atuação em eventos de observação (ou seja, eventos JCR ou eventos de recursos Sling), não é garantido que seja executado e, portanto, deve ser usado com cuidado. Isso já é verdadeiro para implantações de AEM no presente.

## Conexões HTTP de Saída {#outgoing-http-connections}

É altamente recomendável que qualquer conexão HTTP de saída defina tempos limite de conexão e leitura razoáveis; os valores sugeridos são 1 segundo para o tempo limite da conexão e 5 segundos para o tempo limite de leitura. Os números exatos devem ser determinados com base no desempenho do sistema de back-end que lida com essas solicitações.

Para o código que não aplica esses tempos limite, as instâncias de AEM em execução no AEM as a Cloud Service aplicarão um tempo limite global. Esses valores de tempo limite são de 10 segundos para chamadas de conexão e 60 segundos para chamadas de leitura para conexões.

A Adobe recomenda o uso dos recursos [Biblioteca Apache HttpComponents Client 4.x](https://hc.apache.org/httpcomponents-client-ga/) para fazer conexões HTTP.

Alternativas que são conhecidas por funcionar, mas podem exigir que você forneça a dependência:

* [java.net.URL](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) e/ou [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html) (Fornecido por AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (não recomendado, pois está desatualizado e foi substituído pela versão 4.x)
* [OK Http](https://square.github.io/okhttp/) (Não fornecido pelo AEM)

Além de fornecer tempos limite, também deve ser implementado um tratamento adequado desses tempos limite e códigos de status HTTP inesperados.

## Lidar com limites de taxa de solicitação {#rate-limit-handling}

Quando a taxa de solicitações recebidas para o AEM excede os níveis íntegros, o AEM responde a novas solicitações com o código de erro HTTP 429. Os aplicativos que fazem chamadas programáticas para AEM podem considerar a codificação defensivamente, tentando novamente após alguns segundos com uma estratégia de retirada exponencial. Antes de meados de agosto de 2023, o AEM respondia à mesma condição com o código de erro HTTP 503.

## Nenhuma personalização da interface clássica {#no-classic-ui-customizations}

O AEM as a Cloud Service é compatível apenas com a interface para toque para código de clientes de terceiros. A interface clássica não está disponível para personalização.

## Não há binários nativos ou bibliotecas nativas {#avoid-native-binaries}

Os binários e bibliotecas nativos não devem ser implantados ou instalados em ambientes de nuvem.

Além disso, o código não deve tentar baixar binários nativos ou extensões java nativas (por exemplo, JNI) no tempo de execução.

## Nenhum binário de transmissão por meio do AEM as a Cloud Service {#no-streaming-binaries}

Os binários devem ser acessados por meio da CDN, que fornecerá binários fora dos serviços principais de AEM.

Por exemplo, não use `asset.getOriginal().getStream()`, que aciona o download de um binário no disco efêmero do serviço AEM.

## Nenhum agente de replicação reversa {#no-reverse-replication-agents}

A replicação reversa de Publicar para Autor não é compatível com o AEM as a Cloud Service. Se essa estratégia for necessária, você poderá usar um armazenamento de persistência externo que é compartilhado entre o farm de instâncias de Publicação e possivelmente o cluster Autor.

## Talvez seja necessário transferir os agentes de replicação direta {#forward-replication-agents}

O conteúdo é replicado do Autor para a Publicação por meio de um mecanismo pub-sub. Os agentes de replicação personalizados não são compatíveis.

## Sem sobrecarga nos ambientes de desenvolvimento {#overloading-dev-envs}

Os ambientes de produção são dimensionados mais alto para garantir uma operação estável, enquanto os ambientes de preparo são dimensionados como ambientes de produção para garantir testes realistas em condições de produção.

Os ambientes de desenvolvimento e os ambientes de desenvolvimento rápido devem se limitar ao desenvolvimento, à análise de erros e aos testes funcionais, e não foram projetados para processar altas cargas de trabalho nem grandes quantidades de conteúdo.

Por exemplo, alterar uma definição de índice em um grande repositório de conteúdo em um ambiente de desenvolvimento pode resultar na reindexação, resultando em muito processamento. Os testes que exigem conteúdo substancial devem ser executados em ambientes de preparo.

## Monitoramento e depuração {#monitoring-and-debugging}

### Logs {#logs}

Para desenvolvimento local, as entradas de log são gravadas em arquivos locais na `/crx-quickstart/logs` pasta.

Em ambientes da nuvem, os desenvolvedores podem baixar logs por meio do Cloud Manager ou usar uma ferramenta de linha de comando para rastrear os logs. <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**Definir o nível de log**

Para alterar os níveis de log para ambientes em nuvem, a configuração OSGI do Sling Logging deve ser modificada, seguida de uma reimplantação completa. Como isso não é instantâneo, tenha cuidado ao ativar registros detalhados em ambientes de produção que recebem muito tráfego. No futuro, é possível que haja mecanismos para alterar mais rapidamente o nível de log.

>[!NOTE]
>
>Para executar as alterações de configuração listadas abaixo, você as cria em um ambiente de desenvolvimento local e as envia para uma instância as a Cloud Service do AEM. Para obter mais informações sobre como fazer isso, consulte [Implantação no AEM as a Cloud Service](/help/implementing/deploying/overview.md).

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

É possível definir níveis de log discretos para os diferentes ambientes AEM usando o direcionamento de configuração OSGi baseada no modo de execução, se for desejável sempre fazer logon em `DEBUG` durante o desenvolvimento. Por exemplo:

| Ambiente | Localização da configuração do OSGi por modo de execução | `org.apache.sling.commons.log.level` valor da propriedade |
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
| 3 | Info | A ação foi bem-sucedida. |

### Despejos de encadeamento {#thread-dumps}

Os despejos de thread em ambientes na nuvem são coletados de forma contínua, mas não podem ser baixados de forma automatizada no momento. Enquanto isso, entre em contato com o suporte do AEM se os despejos de thread forem necessários para depurar um problema, especificando a janela de tempo exata.

## CRX/DE Lite e Console do desenvolvedor {#crxde-lite-and-developer-console}

### Desenvolvimento local {#local-development}

Para o desenvolvimento local, os desenvolvedores têm acesso total ao CRXDE Lite (`/crx/de`) e o console da Web do AEM (`/system/console`).

Observe que no desenvolvimento local (usando o SDK), `/apps` e `/libs` O pode ser gravado diretamente no, que é diferente de ambientes na nuvem, onde essas pastas de nível superior são imutáveis.

### Ferramentas de desenvolvimento do AEM as a Cloud Service {#aem-as-a-cloud-service-development-tools}

Os clientes podem acessar o CRXDE lite no ambiente de desenvolvimento do nível do autor, mas não no ambiente de preparo ou produção. O repositório imutável (`/libs`, `/apps`) não pode ser gravado no tempo de execução, portanto, tentar fazer isso resultará em erros.

Em vez disso, o Navegador do repositório pode ser iniciado no Console do desenvolvedor, fornecendo uma visualização somente leitura no repositório para todos os ambientes nos níveis de criação, publicação e visualização. Leia mais sobre o Navegador de repositório [aqui](/help/implementing/developing/tools/repository-browser.md).

Um conjunto de ferramentas para depurar ambientes de desenvolvedor as a Cloud Service para AEM está disponível no Console do desenvolvedor para ambientes de RDE, desenvolvimento, preparo e produção. O url pode ser determinado ajustando os urls do serviço de Autor ou Publicação da seguinte maneira:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Como atalho, o seguinte comando da CLI do Cloud Manager pode ser usado para iniciar o console do desenvolvedor com base em um parâmetro de ambiente descrito abaixo:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Consulte [esta página](/help/release-notes/home.md) para obter mais informações.

Os desenvolvedores podem gerar informações de status e resolver vários recursos.

Como ilustrado abaixo, as informações de status disponíveis incluem o estado dos pacotes, componentes, configurações OSGI, índices Oak, serviços OSGI e trabalhos Sling.

![Console de Desenvolvimento 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Como ilustrado abaixo, os desenvolvedores podem resolver as dependências de pacote e os servlets:

![Console de Desenvolvimento 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Console de Desenvolvimento 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Também útil para depuração, o console Desenvolvedor tem um link para a ferramenta Explicar consulta:

![Console de Desenvolvimento 4](/help/implementing/developing/introduction/assets/devconsole4.png)

Para programas de produção, o acesso ao Console do desenvolvedor é definido pela &quot;Função do desenvolvedor do Cloud Manager&quot; no Admin Console, enquanto para programas de sandbox, o Console do desenvolvedor está disponível para qualquer usuário com um perfil de produto que dê a ele acesso ao AEM as a Cloud Service. Para todos os programas, &quot;Cloud Manager - Função do desenvolvedor&quot; é necessário para despejos de status, e o navegador do repositório e os usuários também devem ser definidos no Perfil de produto Usuários do AEM ou Administradores do AEM nos serviços de criação e publicação para exibir dados de ambos os serviços. Para obter mais informações sobre a configuração de permissões de usuário, consulte [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Monitoramento de desempenho {#performance-monitoring}

O Adobe monitora o desempenho do aplicativo e toma medidas para lidar com a deterioração observada. No momento, as métricas de aplicação não podem ser observadas.

## Envio de email {#sending-email}

As seções abaixo descrevem como solicitar, configurar e enviar emails.

>[!NOTE]
>
>O Serviço de e-mail pode ser configurado com suporte ao OAuth2. Para obter mais informações, consulte [Suporte OAuth2 para o serviço de email](/help/security/oauth2-support-for-mail-service.md).

### Ativação de email de saída {#enabling-outbound-email}

Por padrão, as portas usadas para enviar email são desativadas. Para ativar uma porta, configure [rede avançada](/help/security/configuring-advanced-networking.md), certificando-se de definir para cada ambiente necessário o `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` regras de encaminhamento de porta do endpoint, que mapeia a porta pretendida (por exemplo, 465 ou 587) para uma porta proxy.

É recomendável configurar redes avançadas com um `kind` parâmetro definido como `flexiblePortEgress` já que o Adobe pode otimizar o desempenho do tráfego de saída de porta flexível. Se um endereço IP de saída exclusivo for necessário, escolha um `kind` parâmetro de `dedicatedEgressIp`. Se você já tiver configurado a VPN por outros motivos, também poderá usar o endereço IP exclusivo fornecido por essa variação avançada de rede.

Você deve enviar e-mails por meio de um servidor de e-mail em vez de diretamente para clientes de e-mail. Caso contrário, os emails poderão ser bloqueados.

### Envio de emails {#sending-emails}

A variável [Serviço OSGI do Day CQ Mail Service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) deve ser usado e os emails devem ser enviados ao servidor de email indicado na solicitação de suporte, em vez de diretamente aos recipients.

### Configuração {#email-configuration}

Emails no AEM devem ser enviados usando o [Serviço OSGi do Day CQ Mail Service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

Consulte a [Documentação do AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) para obter detalhes sobre as configurações de email. Para o AEM as a Cloud Service, observe os seguintes ajustes necessários no `com.day.cq.mailer.DefaultMailService OSGI` serviço:

* O nome do host do servidor SMTP deve ser definido como $[env:AEM_PROXY_HOST;default=proxy.tunnel]
* A porta do servidor SMTP deve ser definida com o valor da porta proxy original definida no parâmetro portForwards usado na chamada de API ao configurar a rede avançada. Por exemplo, 30465 (em vez de 465)

A porta do servidor SMTP deve ser definida como a `portDest` valor definido no parâmetro portForwards usado na chamada de API ao configurar a rede avançada e o `portOrig` O valor deve ser um valor significativo e estar dentro do intervalo necessário de 30000 a 30999. Por exemplo, se a porta do servidor SMTP for 465, a porta 30465 deverá ser usada como `portOrig` valor.

Nesse caso, e supondo que o SSL precise ser ativado, na configuração do **OSGI do serviço de email Day CQ** serviço:

* Definir `smtp.port` para `30465`
* Definir `smtp.ssl` para `true`

Como alternativa, se a porta de destino for 587, um `portOrig` deve ser usado o valor 30587. E supondo que o SSL deve ser desativado, a configuração do serviço OSGI do Day CQ Mail Service:

* Definir `smtp.port` para `30587`
* Definir `smtp.ssl` para `false`

A variável `smtp.starttls` A propriedade será automaticamente definida pelo AEM as a Cloud Service em tempo de execução com um valor apropriado. Assim, se `smtp.ssl` está definido como verdadeiro, `smtp.startls` é ignorado. Se `smtp.ssl` está definido como falso, `smtp.starttls` está definido como verdadeiro. Isso ocorre independentemente do `smtp.starttls` valores definidos na sua configuração OSGI.


O Serviço de e-mail pode, opcionalmente, ser configurado com suporte para OAuth2. Para obter mais informações, consulte [Suporte OAuth2 para o serviço de email](/help/security/oauth2-support-for-mail-service.md).

### Configuração de email herdada {#legacy-email-configuration}

Antes da versão 2021.9.0, o email era configurado por meio de uma solicitação de suporte ao cliente. Observe os seguintes ajustes necessários no `com.day.cq.mailer.DefaultMailService OSGI` serviço:

O AEM as a Cloud Service exige que o correio seja enviado através da porta 465. Se um servidor de e-mail não suportar a porta 465, a porta 587 poderá ser usada, desde que a opção TLS esteja habilitada.

Se a porta 465 tiver sido solicitada:

* set `smtp.port` para `465`
* set `smtp.ssl` para `true`

e se a porta 587 tiver sido solicitada:

* set `smtp.port` para `587`
* set `smtp.ssl` para `false`

A variável `smtp.starttls` A propriedade será automaticamente definida pelo AEM as a Cloud Service em tempo de execução com um valor apropriado. Assim, se `smtp.ssl` está definido como verdadeiro, `smtp.startls` é ignorado. Se `smtp.ssl` está definido como falso, `smtp.starttls` está definido como verdadeiro. Isso ocorre independentemente do `smtp.starttls` valores definidos na sua configuração OSGI.

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

Consulte a [Documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property) para obter mais detalhes.

## [!DNL Assets] diretrizes de desenvolvimento e casos de uso {#use-cases-assets}

Para saber mais sobre os casos de uso de desenvolvimento, recomendações e materiais de referência para o Assets as a Cloud Service, consulte [Referências do desenvolvedor para Assets](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
