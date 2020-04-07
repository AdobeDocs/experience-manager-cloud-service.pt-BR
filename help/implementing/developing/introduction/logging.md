---
title: Registro
description: Saiba como configurar parâmetros globais para o serviço de registro central, configurações específicas para os serviços individuais ou como solicitar registro de dados.
translation-type: tm+mt
source-git-commit: 73813dd87e3eebfe26673640125ea64916e14789

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

## Registro global {#global-logging}

[A Configuração](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) de registro do Apache Sling é usada para configurar o agente de registro raiz. Isso define as configurações globais para fazer logon no AEM como um serviço em nuvem:

* nível de registro
* a localização do ficheiro de registro central
* o número de versões a conservar
* rotação de versões; tamanho máximo ou intervalo de tempo
* o formato a ser usado ao gravar mensagens de registro

## Registradores e Escritores para Serviços Individuais {#loggers-and-writers-for-individual-services}

Além das configurações globais de registro, o AEM como um serviço em nuvem permite que você defina configurações específicas para um serviço individual:

* o nível de registro específico
* o local do arquivo de log individual
* o número de versões a conservar
* rotação de versões; tamanho máximo ou intervalo de tempo
* o formato a ser usado ao gravar mensagens de registro
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

> [!NOTE]
> 
> Para executar as alterações de configuração listadas abaixo, é necessário criá-las em um ambiente de desenvolvimento local e, em seguida, enviá-las para um AEM como uma instância do Serviço de nuvem. Para obter mais informações sobre como fazer isso, consulte [Implantação no AEM como um serviço](/help/implementing/deploying/overview.md)em nuvem.

### Ativando o nível de log DEBUG {#activating-the-debug-log-level}

> [!WARNING]
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
   1. Configure os outros parâmetros conforme necessário.

1. Crie uma nova instância da Configuração de fábrica Configuração do [Apache Sling Logging Writer Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

   1. Especificar o arquivo de log - deve corresponder ao especificado para o Logger.
   1. Configure os outros parâmetros conforme necessário.

### Criar um arquivo de log personalizado {#create-a-custom-log-file}

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

1. Defina as seguintes propriedades neste nó:

   * Nome: `org.apache.sling.commons.log.file`

      Tipo: String

      Valor: especificar o arquivo de log; por exemplo, `logs/myLogFile.log`

   * Nome: `org.apache.sling.commons.log.names`

      Tipo: String[] (String + Multi)

      Valor: especificar os serviços OSGi para os quais o agente de registro deve registrar as mensagens; por exemplo, todas as seguintes opções:

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * Nome: `org.apache.sling.commons.log.level`

      Tipo: String

      Valor: especificar o nível de log necessário ( `debug`, `info`, `warn` ou `error`); por exemplo `debug`

   * Configure os outros parâmetros conforme necessário:

      * Nome: `org.apache.sling.commons.log.pattern`

         Tipo: `String`

         Valor: especificar o padrão da mensagem de registro, conforme necessário; por exemplo,

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` apoia até seis argumentos.

   >{0} O carimbo de data e hora do tipo `java.util.Date`
   >
   >{1} o marcador de log{2} o nome do thread atual{3} o nome do registrador{4} o nível de log{5} a mensagem de log

   >Se a chamada de log incluir um rastreamento de pilha, ele será anexado à mensagem. `Throwable`

   >[!CAUTION]
   org.apache.sling.commons.log.names deve ter um valor.

   >[!NOTE]
   Os caminhos do gravador de log são relativos ao `crx-quickstart` local.
   Portanto, um arquivo de log especificado como:
   `logs/thelog.log`

   >escreve para:
   `` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log&quot;.
   E um arquivo de log especificado como:
   `../logs/thelog.log`

   >grava em um diretório:
   ` <*cq-installation-dir*>/logs/`
&quot;(ou seja, ao lado de ` `&lt;*cq-installation-dir*>/`crx-quickstart/`)

1. Essa etapa só é necessária quando um novo Gravador é necessário (isto é, com uma configuração diferente do Gravador padrão).

   >[!CAUTION]
   Uma nova Configuração de Gravador de Log é necessária somente quando o padrão existente não é adequado.

   >Se nenhum Escritor explícito estiver configurado, o sistema gerará automaticamente um Escritor implícito com base no padrão.

   Em `/apps/<*project-name*>/config`, crie um nó para a nova `Apache Sling Logging Writer` Configuração:

   * Nome: `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` (como este é um Escritor)

      Assim como no Logger, `<*identifier*>` é substituído pelo texto livre que você (deve) digitar para identificar a instância (não é possível omitir essas informações). Por exemplo, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * Tipo: `sling:OsgiConfig`
   >[!NOTE]
   Embora não seja um requisito técnico, é aconselhável tornar `<*identifier*>` único.

   Defina as seguintes propriedades neste nó:

   * Nome: `org.apache.sling.commons.log.file`

      Tipo: `String`

      Valor: especificar o arquivo de log para que ele corresponda ao arquivo especificado no Log;

      para este exemplo, `../logs/myLogFile.log`.

   * Configure os outros parâmetros conforme necessário:

      * Nome: `org.apache.sling.commons.log.file.number`

         Tipo: `Long`

         Valor: especifique o número de arquivos de log que deseja manter; por exemplo, `5`

      * Nome: `org.apache.sling.commons.log.file.size`

         Tipo: `String`

         Valor: especificar, se for caso disso, o controlo da rotação dos ficheiros por dimensão/data; por exemplo, `'.'yyyy-MM-dd`
   >[!NOTE]
   `org.apache.sling.commons.log.file.size` controla a rotação do arquivo de log ao configurar:
   * um tamanho máximo de arquivo
   * uma programação de data/hora
   para indicar quando um novo arquivo será criado (e o arquivo existente será renomeado de acordo com o padrão de nome).
   * Um limite de tamanho pode ser especificado com um número. Se nenhum indicador de tamanho for fornecido, isso será considerado como o número de bytes, ou você poderá adicionar um dos indicadores de tamanho - `KB`, `MB`ou `GB` (caso seja ignorado).
   * Uma programação de hora/data pode ser especificada como um `java.util.SimpleDateFormat` padrão. Isso define o período após o qual o arquivo será girado; também o sufixo anexado ao arquivo girado (para identificação).
   O padrão é &#39;.&#39;aaaa-MM-dd (para rotação diária do log).
   Assim, por exemplo, à meia-noite de 20 de janeiro de 2010 (ou quando a primeira mensagem de registro depois disso ocorrer para ser precisa), ../logs/error.log será renomeado para ../logs/error.log.2010-01-20. O registro para o dia 21 de janeiro será enviado para (um novo e vazio) ../logs/error.log até que seja lançado na próxima mudança de dia.
       | `&#39;.&#39;aaaa-MM&quot;|Rotação no início de cada mês|
    |—|—|
    | &#39;&#39;.&#39;aaaa-ww`|Rotação no primeiro dia de cada semana (depende da localidade). |
       | `&#39;.&#39;aaaa-MM-dd`|Rotação à meia-noite todos os dias. |
       | `&#39;.&#39;aaaa-MM-dd-a&quot;|Rotação à meia-noite e ao meio-dia de cada dia. |
       | `&#39;.&#39;aaaa-MM-dd-HH`|Rotação no topo de cada hora. |
       | `&#39;.&#39;aaaa-MM-dd-HH-mm&quot;|Rotação no início de cada minuto. |
     
     Nota: Ao especificar uma data/hora:
       1. O texto literal &quot;escape&quot; deve estar dentro de um par de aspas simples ( &quot;&#39;);
       isso serve para evitar que determinados caracteres sejam interpretados como letras padrão.
       1. Use somente caracteres permitidos para um nome de arquivo válido em qualquer lugar na opção.
   

1. Leia seu novo arquivo de log com a ferramenta escolhida.

   O arquivo de log criado por este exemplo será `../crx-quickstart/logs/myLogFile.log`.

O Console do Felix também fornece informações sobre o suporte ao Sling Log em `../system/console/slinglog`; por exemplo `https://localhost:4502/system/console/slinglog`.draf