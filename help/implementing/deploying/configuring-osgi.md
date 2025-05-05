---
title: Configuração do OSGi para o Adobe Experience Manager as a Cloud Service
description: Configuração OSGi com valores secretos e valores específicos do ambiente
feature: Deploying
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '3321'
ht-degree: 1%

---


# Configuração do OSGi para o Adobe Experience Manager as a Cloud Service {#configuring-osgi-for-aem-as-a-cloud-service}

O [OSGi](https://www.osgi.org/) é um elemento fundamental na pilha de tecnologia do Adobe Experience Manager (AEM). É usado para controlar os pacotes compostos de AEM e suas configurações.

O OSGi fornece as primitivas padronizadas que permitem que os aplicativos sejam construídos a partir de componentes pequenos, reutilizáveis e colaborativos. Esses componentes podem ser compostos em um aplicativo e implantados. Isso permite o gerenciamento fácil de pacotes OSGi, pois eles podem ser interrompidos, instalados e iniciados individualmente. As interdependências são tratadas automaticamente. Cada componente OSGi está contido em um dos vários pacotes. Para obter mais informações, consulte a [especificação OSGi](https://help.eclipse.org/latest/index.jsp).

Você pode gerenciar as definições de configuração dos componentes OSGi por meio de arquivos de configuração que fazem parte de um projeto de código AEM.

>[!TIP]
>
>Você pode usar o Cloud Manager para configurar variáveis de ambiente. Para obter mais informações, consulte a documentação [aqui](/help/implementing/cloud-manager/environment-variables.md).

## Arquivos de configuração do OSGi {#osgi-configuration-files}

As alterações de configuração são definidas nos pacotes de código do Projeto AEM (`ui.config`) como arquivos de configuração (`.cfg.json`) nas pastas de configuração específicas do modo de execução:

`/apps/example/config.<runmode>`

O formato dos arquivos de configuração OSGi é baseado em JSON usando o formato `.cfg.json` definido pelo projeto Apache Sling.

As configurações do OSGi direcionam os componentes OSGi por meio de sua Identidade persistente (PID), que assume como padrão o nome de classe Java™ do componente OSGi. Por exemplo, para fornecer a configuração do OSGi para um serviço OSGi implementado por:

`com.example.workflow.impl.ApprovalWorkflow.java`

um arquivo de configuração OSGi é definido em:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

seguindo o formato de configuração OSGi `cfg.json`.

>[!NOTE]
>
>Versões anteriores do AEM davam suporte a arquivos de configuração OSGi usando diferentes formatos de arquivo, como `.cfg`, `.config` e como definições de recurso XML `sling:OsgiConfig`. Esses formatos são substituídos pelo formato de configuração OSGi `.cfg.json`.

>[!NOTE]
>
>As configurações de OSGi não são armazenadas em /apps como instâncias típicas do AEM na nuvem. Elas são armazenadas em um local externo. Faça check-in do Cloud Manager [Developer Console](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#configurations) para ver as configurações de OSGi.

## Resolução do modo de execução {#runmode-resolution}

>[!TIP]
>
>O AEM 6.x é compatível com modos de execução personalizados, no entanto, o AEM as a Cloud Service não. O AEM as a Cloud Service oferece suporte a [um conjunto exato de modos de execução](./overview.md#runmodes). Qualquer variação nas configurações de OSGi entre ambientes do AEM as a Cloud Service deve ser tratada usando [variáveis de ambiente de configuração de OSGi](#environment-specific-configuration-values).

Configurações OSGi específicas podem ser direcionadas a instâncias AEM específicas usando modos de execução. Para usar o modo de execução, crie pastas de configuração em `/apps/example` (onde exemplo é o nome do projeto), no formato:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Todas as configurações de OSGi nessas pastas serão usadas se os modos de execução definidos no nome da pasta de configuração corresponderem aos modos de execução usados pelo AEM.

Por exemplo, se AEM estiver usando o autor e o desenvolvimento runmodes, os nós de configuração em `/apps/example/config.author/` e `/apps/example/config.author.dev/` serão aplicados, enquanto os nós de configuração em `/apps/example/config.publish/` e `/apps/example/config.author.stage/` não serão aplicados.

Se várias configurações para o mesmo PID forem aplicáveis, a configuração com o maior número de modos de execução correspondentes será aplicada.

A granularidade dessa regra está em um nível PID. Isso significa que você não pode definir algumas propriedades para o mesmo PID em `/apps/example/config.author/` e outras mais específicas em `/apps/example/config.author.dev/` para o mesmo PID. A configuração com o maior número de modos de execução correspondentes é eficaz para todo o PID.

>[!NOTE]
>
>Uma pasta de configuração OSGi `config.preview` **não pode** ser declarada da mesma forma que uma `config.publish` pode ser declarada pasta. Em vez disso, o nível de visualização herda sua configuração OSGi dos valores do nível de publicação.

Ao desenvolver localmente, um parâmetro de inicialização do modo de execução, `-r`, é usado para especificar a configuração OSGI do modo de execução.

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

### Verificando modos de execução

Os modos de execução do AEM as a Cloud Service são bem definidos com base no tipo de ambiente e no serviço. Revise a [lista completa de modos de execução do AEM as a Cloud Service disponíveis](./overview.md#runmodes).

Os valores de configuração OSGi especificados pelo modo de execução podem ser verificados por:

1. Abrindo o AEM como um ambiente Cloud Service no [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=pt-BR)
1. Selecionando a(s) camada(s) de serviço a ser(em) inspecionada(s), usando a lista suspensa __Pod__
1. Selecionando a guia __Status__
1. Selecionando __Configurações__ da lista suspensa __Despejo de Status__
1. Selecionando o botão __Obter Status__

A visualização resultante exibe todas as configurações do componente OSGi para as camadas selecionadas com seus valores de configuração OSGi aplicáveis. Esses valores podem ser cruzados com os valores de configuração do OSGi no código-fonte do projeto AEM em `/apps/example/osgiconfig/config.<runmode(s)>`.


Para verificar se os valores de configuração OSGi apropriados foram aplicados:

1. Na saída da Configuração do Developer Console
1. Localize o `pid` que representa a configuração OSGi a ser verificada; esse é o nome do arquivo de configuração OSGi no código-fonte do projeto AEM.
1. Inspect a lista `properties` para o `pid` e verifique se a chave e os valores correspondem ao arquivo de configuração OSGi no código-fonte do projeto AEM para o modo de execução que está sendo verificado.=


## Tipos de valores de configuração OSGi {#types-of-osgi-configuration-values}

Há três variedades de valores de configuração OSGi que podem ser usadas com o Adobe Experience Manager as a Cloud Service.

1. **Valores embutidos**, que são valores codificados na configuração OSGi e armazenados no Git. Por exemplo:

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **Valores secretos**, que são valores que não devem ser armazenados no Git por motivos de segurança. Por exemplo:

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **Valores específicos do ambiente**, que são valores que variam entre ambientes de desenvolvimento e, portanto, não podem ser direcionados com precisão pelo modo de execução (já que há um único modo de execução `dev` no Adobe Experience Manager as a Cloud Service). Por exemplo:

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   Um único arquivo de configuração OSGi pode usar qualquer combinação desses tipos de valor de configuração em conjunto. Por exemplo:

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## Como escolher o tipo de valor de configuração OSGi apropriado {#how-to-choose-the-appropriate-osgi-configuration-value-type}

O caso comum de OSGi usa valores de configuração OSGi em linha. As configurações específicas do ambiente são usadas somente para casos de uso específicos em que um valor difere entre ambientes de desenvolvimento.

![Árvore decisória sobre como usar o tipo de valor de configuração adequado](assets/choose-configuration-value-type_res1.png)

As configurações específicas do ambiente estendem as configurações OSGi tradicionais definidas estaticamente que contêm valores em linha, permitindo gerenciar os valores de configuração do OSGi externamente por meio da API do Cloud Manager. É importante entender quando a abordagem comum e tradicional de definir valores em linha e armazená-los no Git deve ser usada, em vez de abstrair os valores em configurações específicas do ambiente.

As orientações a seguir abordam quando usar configurações específicas de ambiente não secreto e secreto:

### Quando usar valores de configuração em linha {#when-to-use-inline-configuration-values}

Os valores de configurações em linha são considerados a abordagem padrão e devem ser usados quando possível. As configurações em linha oferecem os benefícios de:

* Eles são mantidos, com governança e histórico de versões no Git
* Os valores estão implicitamente vinculados às implantações de código
* Eles não exigem considerações ou coordenação adicionais sobre implantação

Sempre que definir um valor de configuração OSGi, comece com valores em linha e selecione somente configurações secretas ou específicas do ambiente, se necessário, para o caso de uso.

### Quando usar valores de configuração específicos do ambiente não secreto {#when-to-use-non-secret-environment-specific-configuration-values}

Use apenas configurações específicas do ambiente (`$[env:ENV_VAR_NAME]`) para valores de configuração não secretos quando os valores variarem para o nível de visualização ou entre ambientes de desenvolvimento. Isso inclui instâncias de desenvolvimento locais e quaisquer ambientes de desenvolvimento do Adobe Experience Manager as a Cloud Service. Exceto para definir valores exclusivos para o nível de visualização, evite usar configurações específicas de ambiente não secreto para ambientes de Preparo ou Produção do Adobe Experience Manager as a Cloud Service.

* Use apenas configurações específicas do ambiente não secreto para valores de configuração que diferem entre o nível de publicação e visualização, ou para valores que diferem entre ambientes de desenvolvimento, incluindo instâncias de desenvolvimento locais.
* Além do cenário em que o nível de visualização deve variar do nível de publicação, use os valores embutidos padrão nas configurações de OSGi para valores não secretos de Preparo e Produção. Em relação a isso, não é recomendável usar configurações específicas do ambiente para facilitar a realização de alterações de configuração no tempo de execução em ambientes de Preparo e Produção; essas alterações devem ser introduzidas por meio do gerenciamento do código-fonte.

### Quando usar valores de configuração específicos do ambiente secreto {#when-to-use-secret-environment-specific-configuration-values}

O Adobe Experience Manager as a Cloud Service requer o uso de configurações específicas do ambiente (`$[secret:SECRET_VAR_NAME]`) para quaisquer valores de configuração OSGi secretos, como senhas, chaves de API privadas ou quaisquer outros valores que não possam ser armazenados no Git por motivos de segurança.

Use configurações específicas do ambiente secreto para armazenar o valor de segredos em todos os ambientes do Adobe Experience Manager as a Cloud Service, incluindo Preparo e Produção.

## Criação de configurações de OSGi {#creating-osgi-configurations}

Há duas maneiras de criar configurações OSGi, conforme descrito abaixo. A primeira abordagem é normalmente usada para configurar componentes OSGi personalizados que têm propriedades e valores OSGi bem conhecidos pelo desenvolvedor e a última para componentes OSGi fornecidos pelo AEM.

### Gravação de configurações OSGi {#writing-osgi-configurations}

Os arquivos de configuração OSGi formatados em JSON podem ser gravados manualmente diretamente no projeto AEM. Essa é geralmente a maneira mais rápida de criar configurações OSGi para componentes OSGi bem conhecidos e, especialmente, componentes OSGi personalizados que foram projetados e desenvolvidos pelo mesmo desenvolvedor que define as configurações. Essa abordagem também pode ser usada para copiar/colar e atualizar configurações para o mesmo componente OSGi em várias pastas de modo de execução.

1. No IDE, abra o projeto `ui.apps`, localize ou crie a pasta de configuração (`/apps/.../config.<runmode>`) que direciona os modos de execução que a nova configuração OSGi precisa ter em vigor
1. Nesta pasta de configuração, crie um arquivo `<PID>.cfg.json`. O PID é a identidade persistente do componente OSGi. Normalmente, é o nome de classe completo da implementação do componente OSGi. Por exemplo:
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
Os nomes de arquivo de fábrica de configuração OSGi usam a convenção de nomenclatura `<factoryPID>-<name>.cfg.json`
1. Abra o novo arquivo `.cfg.json` e defina as combinações chave/valor para a propriedade OSGi e os pares de valores, seguindo o [formato de configuração OSGi JSON](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).
1. Salve as alterações no novo arquivo `.cfg.json`
1. Adicione e confirme o novo arquivo de configuração OSGi no Git

### Gerar configurações OSGi usando o Quickstart do AEM SDK {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

O console da Web AEM do AEM SDK Quickstart Jar pode ser usado para configurar componentes OSGi e exportar configurações OSGi como JSON. Isso é útil para configurar componentes OSGi fornecidos pelo AEM cujas propriedades OSGi e seus formatos de valor podem não ser bem compreendidos pelo desenvolvedor que define as configurações OSGi no projeto AEM.

>[!NOTE]
>
>A interface de configuração do console da Web AEM grava `.cfg.json` arquivos no repositório. Portanto, esteja ciente desse fluxo de trabalho para evitar um comportamento potencial inesperado durante o desenvolvimento local, quando as configurações OSGi definidas pelo projeto AEM puderem diferir das configurações geradas.

1. Faça logon no console da Web AEM do SDK Quickstart Jar no AEM em `https://<host>:<port>/system/console` como o usuário administrador
1. Navegue até **OSGi** > **Configuração**
1. Para configurar, localize o componente OSGi e selecione o título para editar
   ![Configuração OSGi](./assets/configuring-osgi/configuration.png)
1. Edite os valores da propriedade de configuração OSGi por meio da interface do usuário da Web, conforme necessário
1. Registre a Identidade persistente (PID) no local seguro. Isso é usado posteriormente para gerar o JSON de configuração do OSGi
1. Selecione Salvar
1. Navegue até OSGi > Impressora de configuração do instalador OSGi
1. Cole no PID copiado na Etapa 5, verifique se o Formato de serialização está definido como &quot;OSGi Configurator JSON&quot;
1. Selecionar impressão
1. A configuração do OSGi no formato JSON será exibida na seção Propriedades da configuração serializada
   ![Impressora de Configuração do Instalador OSGi](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. No IDE, abra o projeto `ui.apps`, localize ou crie a pasta de configuração (`/apps/.../config.<runmode>`) que direciona os modos de execução que a nova configuração OSGi precisa ter.
1. Nesta pasta de configuração, crie um arquivo `<PID>.cfg.json`. O PID é o mesmo valor da Etapa 5.
1. Cole as Propriedades da Configuração Serializada da Etapa 10 no arquivo `.cfg.json`.
1. Salve as alterações no novo arquivo `.cfg.json`.
1. Adicione e confirme o novo arquivo de configuração OSGi no Git.


## Formatos de propriedade da configuração OSGi {#osgi-configuration-property-formats}

### Valores em linha {#inline-values}

Os valores em linha são formatados como pares de nome-valor padrão, seguindo a sintaxe JSON padrão. Por exemplo:

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### Valores de configuração específicos do ambiente {#environment-specific-configuration-values}

A configuração do OSGi deve atribuir um espaço reservado para a variável que deve ser definida por ambiente:

```
use $[env:ENV_VAR_NAME]
```

Os clientes devem usar essa técnica apenas para propriedades de configuração do OSGi relacionadas a seu código personalizado; ela não deve ser usada para substituir a configuração do OSGi definida por Adobe.

>[!NOTE]
>
>Os espaços reservados não podem ser usados em [instruções repoinit](/help/implementing/deploying/overview.md#repoinit).

### Valores de configuração do segredo {#secret-configuration-values}

A configuração do OSGi deve atribuir um espaço reservado para o segredo que deve ser definido por ambiente:

```
use $[secret:SECRET_VAR_NAME]
```

### Nomeação da variável {#variable-naming}

O seguinte se aplica aos valores de configuração específicos e secretos do ambiente.

Os nomes das variáveis devem seguir as seguintes regras:

* Comprimento mínimo: 2
* Tamanho máximo: 100
* Deve corresponder ao regex: `[a-zA-Z_][a-zA-Z_0-9]*`

Os valores das variáveis não devem exceder 2048 caracteres.

>[!CAUTION]
>
>Há regras relacionadas ao uso de determinados prefixos para nomes de variáveis:
>
>1. Nomes de variáveis com prefixos `INTERNAL_`, `ADOBE_` ou `CONST_` são reservados por Adobe. Quaisquer variáveis definidas pelo cliente que comecem com esses prefixos são ignoradas.
>
>1. Os clientes também não devem fazer referência a variáveis com prefixo `INTERNAL_` ou `ADOBE_`.
>
>1. As variáveis de ambiente com o prefixo `AEM_` são definidas pelo produto como API pública a ser usada e definida pelos clientes.
>   Embora os clientes possam usar e definir variáveis de ambiente começando com o prefixo `AEM_`, eles não devem definir suas próprias variáveis com esse prefixo.

### Valores padrão {#default-values}

O seguinte se aplica aos valores de configuração específicos e secretos do ambiente.

Se nenhum valor por ambiente for definido, no tempo de execução o espaço reservado não será substituído e permanecerá no lugar, pois nenhuma interpolação aconteceu. Para evitar isso, um valor padrão pode ser fornecido como parte do espaço reservado com a seguinte sintaxe:

```
$[env:ENV_VAR_NAME;default=<value>]
```

Com um valor padrão fornecido, o espaço reservado é substituído pelo valor por ambiente, se fornecido, ou pelo valor padrão fornecido.

### Desenvolvimento local {#local-development}

O seguinte se aplica aos valores de configuração específicos e secretos do ambiente.

As variáveis podem ser definidas no ambiente local para que sejam coletadas pelo AEM local no tempo de execução. Por exemplo, no Linux®:

```bash
export ENV_VAR_NAME=my_value
```

Recomenda-se que um script bash simples seja escrito, definindo as variáveis de ambiente usadas nas configurações e para executá-lo antes de iniciar o AEM. Ferramentas como [https://direnv.net/](https://direnv.net/) ajudam a simplificar esta abordagem. Dependendo do tipo dos valores, eles podem ser verificados no gerenciamento de código-fonte, se puderem ser compartilhados entre todos.

Os valores de segredos são lidos dos arquivos. Portanto, para cada espaço reservado que usa um segredo, um arquivo de texto contendo o valor secreto deve ser criado.

Por exemplo, se `$[secret:server_password]` for usado, um arquivo de texto chamado **server_password** deverá ser criado. Todos esses arquivos secretos devem ser armazenados no mesmo diretório e a propriedade de estrutura `org.apache.felix.configadmin.plugin.interpolation.secretsdir` deve ser configurada com esse diretório local.

>[!CAUTION]
>
>Extensões de arquivo não são permitidas para o arquivo de texto.
>
>Portanto, para o exemplo acima, o arquivo de texto deve ser nomeado como **server_password** - sem uma extensão de arquivo.

O `org.apache.felix.configadmin.plugin.interpolation.secretsdir` é uma propriedade de estrutura Sling; portanto, essa propriedade não está definida no console felix (/system/console), mas está definida no arquivo sling.properties usado quando o sistema é inicializado. Esse arquivo pode ser encontrado no subdiretório /conf da pasta Jar/install extraída (crx-quickstart/conf).

exemplo: adicione esta linha ao final do arquivo &#39;crx-quickstart/conf/sling.properties&#39;-file para configurar &#39;crx-quickstart/secretsdir&#39; como uma pasta secreta:

```
org.apache.felix.configadmin.plugin.interpolation.secretsdir=${sling.home}/secretsdir
```

### Configuração do autor versus Publish {#author-vs-publish-configuration}

Se uma propriedade OSGi exigir valores diferentes para autor e publicação:

* Separe as pastas OSGi `config.author` e `config.publish`, conforme descrito na [seção Resolução do Modo de Execução](#runmode-resolution).
* Há duas opções para criar os nomes de variáveis independentes que devem ser usadas:
   * a primeira opção, que é recomendada: em todas as pastas OSGi (como `config.author` e `config.publish`) declaradas para definir valores diferentes, use o mesmo nome de variável. Por exemplo

     `$[env:ENV_VAR_NAME;default=<value>]`, onde o padrão corresponde ao valor padrão para essa camada (autor ou publicação). Ao definir a variável de ambiente por meio da [API do Cloud Manager](#cloud-manager-api-format-for-setting-properties) ou por meio de um cliente, diferencie as camadas usando o parâmetro &quot;service&quot;, conforme descrito na [documentação de referência da API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/). O parâmetro &quot;service&quot; vinculará o valor da variável ao nível OSGi apropriado. Pode ser &quot;autor&quot; ou &quot;publicar&quot; ou &quot;pré-visualização&quot;.
   * a segunda opção, que é declarar variáveis distintas usando um prefixo como `author_<samevariablename>` e `publish_<samevariablename>`

### Exemplos de configuração {#configuration-examples}

Nos exemplos abaixo, suponha que haja três ambientes de desenvolvimento, além dos ambientes de preparo e produção.

**Exemplo 1**

A intenção é que o valor da propriedade OSGi `my_var1` seja o mesmo para estágio e produção, mas seja diferente para cada um dos três ambientes de desenvolvimento.

<table>
<tr>
<td>
<b>Pasta</b>
</td>
<td>
<b>Conteúdo de myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
&lbrace; 
 "my_var1": "val",
 "my_var2": "abc",
 "my_var3": 500
&rbrace;
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
&lbrace; 
 "my_var1" : "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
&rbrace;
</pre>
</td>
</tr>
</table>

**Exemplo 2**

A intenção é que o valor da propriedade OSGi `my_var1` seja diferente para o estágio, a produção e para cada um dos três ambientes de desenvolvimento. Assim, a API do Cloud Manager deve ser chamada para definir o valor de `my_var1` para cada ambiente dev.

<table>
<tr>
<td>
<b>Pasta</b>
</td>
<td>
<b>Conteúdo de myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config.stage
</td>
<td>
<pre>
&lbrace; 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
&rbrace;
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
&lbrace; 
 "my_var1": "val2",
 "my_var2": "abc",
 "my_var3": 500
&rbrace;
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
&lbrace; 
 "my_var1" : "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
&rbrace;
</pre>
</td>
</tr>
</table>

**Exemplo 3**

A intenção é que o valor da propriedade OSGi `my_var1` seja o mesmo para ambientes de preparo, produção e apenas um dos ambientes dev, mas que seja diferente para os outros dois ambientes dev. Nesse caso, a API do Cloud Manager deve ser chamada para definir o valor de `my_var1` para cada um dos ambientes dev, incluindo para o ambiente dev, que deve ter o mesmo valor que preparo e produção. Ele não herdará o valor definido na pasta **config**.

<table>
<tr>
<td>
<b>Pasta</b>
</td>
<td>
<b>Conteúdo de myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
&lbrace; 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
&rbrace;
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
&lbrace; 
 "my_var1" : "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
&rbrace;
</pre>
</td>
</tr>
</table>

Outra maneira de fazer isso seria definir um valor padrão para o token de substituição na pasta config.dev de modo que ele tenha o mesmo valor que na pasta **config**.

<table>
<tr>
<td>
<b>Pasta</b>
</td>
<td>
<b>Conteúdo de myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
&lbrace; 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
&rbrace;
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
&lbrace; 
 "my_var1": "$[env:my_var1;default=val1]"
 "my_var2": "abc",
 "my_var3": 500
&rbrace;
</pre>
</td>
</tr>
</table>

## Formato de API do Cloud Manager para propriedades de configuração {#cloud-manager-api-format-for-setting-properties}

Consulte [Adobe Cloud Manager no site da Adobe Developer](https://developer.adobe.com/experience-cloud/cloud-manager/docs/) para obter informações sobre a API do Cloud Manager e como configurá-la.

>[!NOTE]
>
>Certifique-se de que a API Cloud Manager usada atribuiu a função &quot;Gerente de implantação - Cloud Service&quot;. Outras funções não podem executar todos os comandos abaixo.

>[!TIP]
>
>Você também pode usar o Cloud Manager para configurar variáveis de ambiente. Para obter mais informações, consulte [Variáveis de ambiente do Cloud Manager](/help/implementing/cloud-manager/environment-variables.md).

### Configuração de valores por meio da API {#setting-values-via-api}

Chamar a API implanta as novas variáveis e valores em um ambiente na nuvem, de modo semelhante a um pipeline típico de implantação de código do cliente. Os serviços de criação e publicação são reiniciados e fazem referência aos novos valores, normalmente levando alguns minutos.

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```json
[
        {
                "name" : "MY_VAR1",
                "value" : "plaintext value",
                "type" : "string"  <---default
        },
        {
                "name" : "MY_VAR2",
                "value" : "<secret value>",
                "type" : "secretString"
        }
]
```

>[!NOTE]
>As variáveis padrão não são definidas por meio da API, mas na própria propriedade OSGi.
>
>Consulte [API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) para obter mais informações.

### Obtenção de valores por meio da API {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

Consulte [API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) para obter mais informações.

### Exclusão de valores por meio da API {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

Para excluir uma variável, inclua-a com um valor vazio.

Consulte [API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) para obter mais informações.

### Obtendo valores por meio da linha de comando {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### Configuração de valores por meio da Linha de comando {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### Exclusão de valores por meio da linha de comando {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>Consulte [o aio-cli-plugin-cloudmanager no GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para obter mais informações sobre como configurar valores usando o plug-in do Cloud Manager para a CLI do Adobe I/O.

### Número de variáveis {#number-of-variables}

É possível declarar até 200 variáveis por ambiente.

## Considerações sobre implantação para valores de configuração secretos e específicos do ambiente {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

Como os valores de configuração secretos e específicos do ambiente residem fora do Git e, portanto, não fazem parte dos mecanismos formais de implantação do Adobe Experience Manager as a Cloud Service, o cliente deve gerenciar, administrar e integrar ao processo de implantação do Adobe Experience Manager as a Cloud Service.

Como mencionado acima, chamar a API implanta as novas variáveis e valores em ambientes de nuvem, de modo semelhante a um pipeline típico de implantação de código do cliente. Os serviços de criação e publicação são reiniciados e fazem referência aos novos valores, normalmente levando alguns minutos. Os quality gates (portais de qualidade) e os testes que são executados pelo Cloud Manager durante uma implantação de código regular não são executados durante esse processo.

Normalmente, os clientes chamariam a API para definir variáveis de ambiente antes de implantar o código que depende delas no Cloud Manager. Em algumas situações, pode ser necessário modificar uma variável existente depois que o código já tiver sido implantado.

>[!NOTE]
>
>A API pode não ser bem-sucedida quando um pipeline estiver em uso, seja uma atualização de AEM ou implantação de cliente, dependendo de qual parte do pipeline de ponta a ponta está sendo executada no momento. A resposta de erro indicará que a solicitação não foi bem-sucedida, embora não indique o motivo específico.

Pode haver cenários em que uma implantação programada de código do cliente dependa de variáveis existentes para ter novos valores, o que não seria apropriado com o código atual. Se isso for um problema, é recomendável fazer modificações variáveis de maneira aditiva. Para fazer isso, crie novos nomes de variáveis em vez de apenas alterar o valor de variáveis antigas para que o código antigo nunca faça referência ao novo valor. Em seguida, quando a nova versão do cliente parecer estável, é possível optar por remover os valores mais antigos.

Da mesma forma, como os valores de uma variável não têm controle de versão, uma reversão de código pode fazer com que ela faça referência a valores mais recentes que causam problemas. A estratégia de variável aditiva mencionada anteriormente também ajudaria aqui.

Essa estratégia aditiva de variáveis também é útil para cenários de recuperação de desastres em que, se o código de vários dias antes precisasse ser reimplantado, os nomes e os valores das variáveis aos quais ele faz referência ainda estariam intactos. Isso depende de uma estratégia em que um cliente aguarda alguns dias antes de remover essas variáveis mais antigas. Caso contrário, o código mais antigo não teria variáveis apropriadas para referência.
