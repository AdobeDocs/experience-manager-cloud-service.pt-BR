---
title: Registro
description: Saiba como configurar parâmetros globais para o serviço de registro central, configurações específicas para os serviços individuais ou como solicitar registro de dados.
translation-type: tm+mt
source-git-commit: 1b10561af9349059aaee97e4f42d2e339f629700

---


# Registro{#logging}

AEM como um serviço em nuvem oferta a possibilidade de configurar:

* parâmetros globais para o serviço central de registro
* solicitar o registro de dados; uma configuração de registro especializada para informações de solicitação
* definições específicas para cada serviço; por exemplo, um arquivo de log individual e um formato para as mensagens de log

Para desenvolvimento local, as entradas de registros são gravadas em arquivos locais na `/crx-quickstart/logs` pasta.

Nos ambientes da Cloud, os desenvolvedores podem baixar os logs por meio do Cloud Manager ou usar uma ferramenta de linha de comando para rastrear os logs.

>[!NOTE]
>
>Fazer logon no AEM como um serviço em nuvem é baseado nos princípios do Sling. Consulte [Sling Logging](https://sling.apache.org/site/logging.html) para obter mais informações.

<!-- ## Global Logging {#global-logging}

[Apache Sling Logging Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) is used to configure the root logger. This defines the global settings for logging in AEM as a Cloud Service:

* the logging level
* the location of the central log file
* the number of versions to be kept
* version rotation; either maximum size or a time interval
* the format to be used when writing the log messages
-->

## Registradores e Escritores para Serviços Individuais {#loggers-and-writers-for-individual-services}

Além das configurações globais de registro, o AEM como um serviço em nuvem permite que você defina configurações específicas para um serviço individual:

* o nível de registro específico
* o agente de log (o serviço OSGi que fornece as mensagens de log)

Isso permite que você canal mensagens de log de um único serviço em um arquivo separado. Isto pode ser particularmente útil durante o desenvolvimento ou testes; por exemplo, quando você precisa de um nível de log aumentado para um serviço específico.

O AEM como um serviço em nuvem usa o seguinte para gravar mensagens de registro no arquivo:

1. Um serviço **** OSGi (logger) grava uma mensagem de registro.
1. Um **Logging Logger** pega essa mensagem e a formata de acordo com sua especificação.
1. Um Gravador **de** log grava todas essas mensagens no arquivo físico que você definiu.

Estes elementos estão ligados pelos seguintes parâmetros para os elementos apropriados:

* **Logger (Logging Logger)**

   Defina os serviços que geram as mensagens.

* **Arquivo de log (registrador de log)**

   Defina o arquivo físico para armazenar as mensagens de log.

   Isso é usado para vincular um Logging Logger a um Logging Writer. O valor deve ser idêntico ao mesmo parâmetro na configuração do Gravador de log para que a conexão seja feita.

* **Arquivo de log (Gravador de log)**

   Defina o arquivo físico para o qual as mensagens de log serão gravadas.

   Isso deve ser idêntico ao mesmo parâmetro na configuração do Gravador de log, ou a correspondência não será feita. Se não houver correspondência, um Escritor implícito será criado com a configuração padrão (rotação diária do log).

### Registradores e escritores padrão {#standard-loggers-and-writers}

Determinados registradores e gravadores estão incluídos em um AEM padrão como uma instalação do serviço em nuvem.

O primeiro é um caso especial, pois controla os arquivos `request.log` e `access.log` :

* O Registrador:

   * Registrador de Dados de Solicitação Personalizável do Apache Sling

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Gravar mensagens sobre o conteúdo da solicitação para `request.log`.

* Links para:

   * Registro de solicitação Sling do Apache

      (org.apache.sling.engine.impl.log.RequestLogger)

   * Grava as mensagens em `request.log` ou `access.log`.

Eles podem ser personalizados se necessário, embora a configuração padrão seja adequada para a maioria das instalações.

Os outros pares seguem a configuração padrão:

* O Registrador:

   * Configuração do Apache Sling Logging Logger

      (org.apache.sling.commons.log.LogManager.fatory.config)

   * Grava `Information` mensagens em `logs/error.log`.

* Links para o Escritor:

   * Configuração do Apache Sling Logging Writer

      (org.apache.sling.commons.log.LogManager.fatory.writer)

* O Registrador:

   * Configuração do Apache Sling Logging Logger (org.apache.sling.commons.log.LogManager.fatory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Grava `Warning` mensagens para `../logs/error.log` o serviço `org.apache.pdfbox`.

* Não vincula a um Escritor específico, portanto, criará e usará um Escritor implícito com configuração padrão (rotação diária do log).

## Configuração do nível de log {#setting-the-log-level}

Para alterar os níveis de log dos ambientes do Cloud, a configuração de Sling Logging OSGI deve ser modificada, seguida de uma reimplantação completa. Como isso não é instantâneo, tenha cuidado ao ativar registros detalhados em ambientes de produção que recebem muito tráfego. No futuro, é possível que haja mecanismos para mudar mais rapidamente o nível de log.

>[!NOTE]
>
> Para executar as alterações de configuração listadas abaixo, é necessário criá-las em um ambiente de desenvolvimento local e, em seguida, enviá-las para um AEM como uma instância do Serviço de nuvem. Para obter mais informações sobre como fazer isso, consulte [Implantação no AEM como um serviço](/help/implementing/deploying/overview.md)em nuvem.

### Ativando o nível de log DEBUG {#activating-the-debug-log-level}

>[!WARNING]
>
> A ativação global do nível de log DEBUG gerará uma grande quantidade de informações que será difícil de filtrar. É recomendável ativá-la somente para os serviços que exigem depuração. Para obter mais informações, consulte [Loggers e Writers for Individual Services](logging.md#loggers-and-writers-for-individual-services).

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

### Criando seus próprios registradores e escritores {#creating-your-own-loggers-and-writers}

Você pode definir seu próprio par de Registrador/Escritor:

1. Crie uma nova instância da Configuração de fábrica Configuração do [Apache Sling Logging Logger Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

   1. Especifique o arquivo de log.
   1. Especifique o registrador.

<!-- 1. Create a new instance of the Factory Configuration [Apache Sling Logging Writer Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

    1. Specify the Log File - this must match that specified for the Logger.
    1. Configure the other parameters as required. -->

### Configurar o registro {#configure-logging}

>[!NOTE]
>
>Ao trabalhar com o Adobe Experience Manager, há vários métodos de gerenciar as configurações desses serviços.

Em determinadas circunstâncias, você pode querer criar um arquivo de log personalizado com um nível de log diferente. Você pode fazer isso no repositório:

1. Se ainda não existir, crie uma nova pasta de configuração ( `sling:Folder`) para o seu projeto `/apps/<*project-name*>/config`.
1. Em `/apps/<*project-name*>/config`, crie um nó para a nova configuração do Apache Sling Logging Logger:

   * Nome: `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` (como este é um Logger)

      Onde `<*identifier*>` é substituído pelo texto livre que você (deve) deve digitar para identificar a instância (não é possível omitir essas informações).

      Por exemplo, `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * Tipo: `sling:OsgiConfig`
   >[!NOTE]
   >
   >Embora não seja um requisito técnico, é aconselhável tornar `<*identifier*>` único.

<!-- 1. Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file`

      Type: String

      Value: specify the Log File; for example, `logs/myLogFile.log`

    * Name: `org.apache.sling.commons.log.names`

      Type: String[] (String + Multi)

      Value: specify the OSGi services for which the Logger is to log messages; for example, all of the following:

        * `org.apache.sling`
        * `org.apache.felix`
        * `com.day`

    * Name: `org.apache.sling.commons.log.level`

      Type: String

      Value: specify the log level required ( `debug`, `info`, `warn` or `error`); for example `debug`

    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.pattern`

          Type: `String`

          Value: specify the pattern of the log message as required; for example,

          `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` supports up to six arguments.

   >
   >
   >{0} The timestamp of type `java.util.Date`
   >{1} the log marker
   >{2} the name of the current thread
   >{3} the name of the logger
   >{4} the log level
   >{5} the log message

   >
   >
   >If the log call includes a `Throwable` the stacktrace is appended to the message.

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names must have a value.

   >[!NOTE]
   >
   >Log writer paths are relative to the `crx-quickstart` location.
   >
   >
   >Therefore, a log file specified as:
   >
   >
   >`logs/thelog.log`

   >
   >
   >writes to:
   >
   >
   >`` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`.
   >
   >
   >And a log file specified as:
   >
   >
   >`../logs/thelog.log`

   >
   >
   >writes to a directory:
   >
   >
   >` <*cq-installation-dir*>/logs/`
   >``(i.e. next to ` `<*cq-installation-dir*>/`crx-quickstart/`)
 -->

<!-- open question: see if we need to leave the above warning note in place, but adjust it so that it doesn't mention filenames -->

<!-- 1. This step is only necessary when a new Writer is required (i.e. with a configuration that is different to the default Writer).

   >[!CAUTION]
   >
   >A new Logging Writer Configuration is only required when the existing default is not suitable.

   >
   >
   >If no explicit Writer is configured the system will automatically generate an implicit Writer based on the default.

   Under `/apps/<*project-name*>/config`, create a node for the new `Apache Sling Logging Writer` Configuration:

    * Name: `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` (as this is a Writer)

      As with the Logger, `<*identifier*>` is replaced by free text that you (must) enter to identify the instance (you cannot omit this information). For example, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

    * Type: `sling:OsgiConfig`

   >[!NOTE]
   >
   >Although not a technical requirement, it is advisable to make `<*identifier*>` unique.

   Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file`

      Type: `String`

      Value: specify the Log File so that it matches the file specified in the Logger;

      for this example, `../logs/myLogFile.log`.

    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.file.number`

          Type: `Long`

          Value: specify the number of log files you want kept; for example, `5`

        * Name: `org.apache.sling.commons.log.file.size`

          Type: `String`

          Value: specify as required to control file rotation by size/date; for example, `'.'yyyy-MM-dd`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` controls the rotation of the log file by setting either:
   >
   >* a maximum file size
   >* a time/date schedule
   >
   >to indicate when a new file will be created (and the existing file renamed according to the name pattern).
   >
   >* A size limit can be specified with a number. If no size indicator is given, then this is taken as the number of bytes, or you can add one of the size indicators - `KB`, `MB`, or `GB` (case is ignored).
   >* A time/date schedule can be specified as a `java.util.SimpleDateFormat` pattern. This defines the time period after which the file will be rotated; also the suffix appended to the rotated file (for identification).
   >
   >The default is '.'yyyy-MM-dd (for daily log rotation).
   >
   >So for example, at midnight of January 20th 2010 (or when the first log message after this occurs to be precise), ../logs/error.log will be renamed to ../logs/error.log.2010-01-20. Logging for the 21st of January will be output to (a new and empty) ../logs/error.log until it is rolled over at the next change of day.
   >
   >      | `'.'yyyy-MM` |Rotation at the beginning of each month |
   >      |---|---|
   >      | `'.'yyyy-ww` |Rotation at the first day of each week (depends on the locale). |
   >      | `'.'yyyy-MM-dd` |Rotation at midnight each day. |
   >      | `'.'yyyy-MM-dd-a` |Rotation at midnight and midday of each day. |
   >      | `'.'yyyy-MM-dd-HH` |Rotation at the top of every hour. |
   >      | `'.'yyyy-MM-dd-HH-mm` |Rotation at the beginning of every minute. |
   >
   >      Note: When specifying a time/date:
   >      1. You should "escape" literal text within a pair of single quotes (' ');
   >      this is to avoid certain characters being interpreted as pattern letters.
   >      1. Only use characters allowed for a valid file name anywhere in the option.

1. Read your new log file with your chosen tool.

   The log file created by this example will be `../crx-quickstart/logs/myLogFile.log`. -->

O Console do Felix também fornece informações sobre o suporte ao Sling Log em `../system/console/slinglog`; por exemplo `https://localhost:4502/system/console/slinglog`.draf