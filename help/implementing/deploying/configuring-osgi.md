---
title: Configuração do OSGi para Adobe Experience Manager as a Cloud Service
description: 'Configuração do OSGi com valores secretos e valores específicos do ambiente '
feature: Deploying
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
source-git-commit: f947650b0872785e1f1b5f4c6542afd41fa61309
workflow-type: tm+mt
source-wordcount: '2993'
ht-degree: 0%

---

# Configuração do OSGi para Adobe Experience Manager as a Cloud Service {#configuring-osgi-for-aem-as-a-cloud-service}

[OSGi](https://www.osgi.org/) é um elemento fundamental na pilha de tecnologia do Adobe Experience Manager (AEM). Ele é usado para controlar os pacotes compostos de AEM e suas configurações.

O OSGi fornece os primitivos padronizados que permitem que os aplicativos sejam construídos a partir de componentes pequenos, reutilizáveis e colaborativos. Esses componentes podem ser compostos em um aplicativo e implantados. Isso permite o gerenciamento fácil de pacotes OSGi, pois eles podem ser interrompidos, instalados e iniciados individualmente. As interdependências são manipuladas automaticamente. Cada componente OSGi está contido em um dos vários pacotes. Para obter mais informações, consulte o [Especificação OSGi](https://www.osgi.org/Specifications/HomePage).

Você pode gerenciar as configurações dos componentes OSGi por meio de arquivos de configuração que fazem parte de um projeto de código AEM.

## Arquivos de configuração do OSGi {#osgi-configuration-files}

As alterações de configuração são definidas nos pacotes de código do AEM Project (`ui.apps`) como arquivos de configuração (`.cfg.json`) em pastas de configuração específicas do modo de execução:

`/apps/example/config.<runmode>`

O formato dos arquivos de configuração OSGi é baseado em JSON usando o `.cfg.json` formato definido pelo projeto Apache Sling.

As configurações OSGi direcionam componentes OSGi por meio de sua Identidade Persistente (PID), que assume como padrão o nome de classe Java™ do componente OSGi. Por exemplo, para fornecer a configuração OSGi para um serviço OSGi implementado por:

`com.example.workflow.impl.ApprovalWorkflow.java`

um arquivo de configuração OSGi é definido em:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

seguindo o formato de configuração do OSGi cfg.json.

>[!NOTE]
>
>As versões anteriores AEM arquivos de configuração OSGi compatíveis usando formatos de arquivo diferentes, como .cfg., .config e como definições de recurso XML sling:OsgiConfig . Esses formatos são substituídos pelo formato de configuração OSGi cfg.json .

## Resolução do Modo de Execução {#runmode-resolution}

Configurações específicas de OSGi podem ser direcionadas a instâncias AEM específicas usando modos de execução. Para usar o runmode, crie pastas de configuração em `/apps/example` (onde por exemplo é o nome do seu projeto), no formato:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Todas as configurações OSGi nessas pastas serão usadas se os runmodes definidos no nome da pasta de configuração corresponderem aos runmodes usados pelo AEM.

Por exemplo, se AEM estiver usando os modos de execução author e dev, os nós de configuração em `/apps/example/config.author/` e `/apps/example/config.author.dev/` são aplicados, enquanto os nós de configuração em `/apps/example/config.publish/` e `/apps/example/config.author.stage/` não são aplicadas.

Se várias configurações para o mesmo PID forem aplicáveis, a configuração com o maior número de modos de execução correspondentes será aplicada.

A granularidade desta regra está em um nível PID. Isso significa que não é possível definir algumas propriedades para o mesmo PID em `/apps/example/config.author/` e mais específicas em `/apps/example/config.author.dev/` para o mesmo PID. A configuração com o maior número de modos de execução correspondentes será efetiva para todo o PID.

>[!NOTE]
>
>A `config.preview` Pasta de configuração OSGI **cannot** ser declaradas da mesma forma que `config.publish` pode ser a pasta declarada. Em vez disso, o nível de visualização herda sua configuração OSGI dos valores do nível de publicação.

Ao desenvolver localmente, um parâmetro de inicialização do modo de execução pode ser passado para ditar qual configuração de OSGI do modo de execução é usada.

## Tipos de valores de configuração do OSGi {#types-of-osgi-configuration-values}

Existem três variedades de valores de configuração de OSGi que podem ser usadas com o Adobe Experience Manager as a Cloud Service.

1. **Valores em linha**, que são valores codificados na configuração OSGi e armazenados no Git. Por exemplo:

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

1. **Valores específicos do ambiente**, que são valores que variam entre ambientes de desenvolvimento e, portanto, não podem ser direcionados com precisão pelo modo de execução (já que há um único `dev` runmode no Adobe Experience Manager as a Cloud Service). Por exemplo:

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   Observe que um único arquivo de configuração OSGi pode usar qualquer combinação desses tipos de valor de configuração em conjunto. Por exemplo:

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## Como escolher o tipo apropriado de valor de configuração do OSGi {#how-to-choose-the-appropriate-osgi-configuration-value-type}

O caso comum para OSGi usa valores de configuração OSGi em linha. As configurações específicas do ambiente são usadas apenas para casos de uso específicos em que um valor difere entre ambientes de desenvolvimento.

![](assets/choose-configuration-value-type_res1.png)

As configurações específicas do ambiente estendem as configurações OSGi tradicionais, definidas estaticamente, que contêm valores em linha, fornecendo a capacidade de gerenciar os valores de configuração do OSGi externamente por meio da API do Cloud Manager. É importante entender quando a abordagem comum e tradicional de definir valores em linha e armazená-los em Git deve ser usada, em vez de abstrair os valores em configurações específicas do ambiente.

As orientações a seguir abordam quando usar configurações específicas de ambiente não secretas e secretas:

### Quando usar valores de configuração embutidos {#when-to-use-inline-configuration-values}

Os valores de configurações em linha são considerados a abordagem padrão e devem ser usados quando possível. As configurações em linha oferecem os benefícios de:

* Eles são mantidos, com governança e histórico de versões no Git
* Os valores estão implicitamente vinculados a implantações de código
* Eles não exigem considerações ou coordenação adicionais de implantação

Sempre que definir um valor de configuração OSGi, comece com valores em linha e selecione somente configurações secretas ou específicas do ambiente, se necessário, para o caso de uso.

### Quando usar valores de configuração não secretos específicos do ambiente {#when-to-use-non-secret-environment-specific-configuration-values}

Usar somente configurações específicas do ambiente (`$[env:ENV_VAR_NAME]`) para valores de configuração não secretos quando os valores variam para o nível de visualização ou variam entre ambientes de desenvolvimento. Isso inclui instâncias de desenvolvimento local e quaisquer ambientes de desenvolvimento do Adobe Experience Manager as a Cloud Service. Exceto para definir valores exclusivos para o nível de visualização, evite usar configurações não secretas específicas do ambiente para ambientes do Adobe Experience Manager as a Cloud Service Stage ou de Produção.

* Use apenas configurações específicas de ambiente não secretas para valores de configuração que diferem entre publicar e visualizar camadas, ou para valores que diferem entre ambientes de desenvolvimento, incluindo instâncias de desenvolvimento local.
* Além do cenário em que o nível de visualização precisa variar do nível de publicação, use os valores em linha padrão nas configurações OSGi para valores não secretos de Preparo e Produção. Em relação a isso, não é recomendável usar configurações específicas do ambiente para facilitar as alterações de configuração em tempo de execução para ambientes de Preparo e Produção; essas alterações devem ser introduzidas por meio do gerenciamento do código-fonte.

### Quando usar valores de configuração secretos específicos do ambiente {#when-to-use-secret-environment-specific-configuration-values}

O Adobe Experience Manager as a Cloud Service requer o uso de configurações específicas do ambiente (`$[secret:SECRET_VAR_NAME]`) para quaisquer valores de configuração OSGi secretos, como senhas, chaves de API privadas ou quaisquer outros valores que não possam ser armazenados no Git por motivos de segurança.

Use configurações secretas específicas do ambiente para armazenar o valor de segredos em todos os ambientes do Adobe Experience Manager as a Cloud Service, incluindo Preparo e Produção.

## Criando configurações OSGi {#creating-sogi-configurations}

Há duas maneiras de criar configurações OSGi, conforme descrito abaixo. A primeira abordagem é normalmente usada para configurar componentes OSGi personalizados que têm propriedades e valores OSGi bem conhecidos pelo desenvolvedor, e a última para componentes OSGi fornecidos por AEM.

### Gravando configurações de OSGi {#writing-osgi-configurations}

Os arquivos de configuração OSGi formatados em JSON podem ser gravados manualmente diretamente no projeto AEM. Essa é frequentemente a maneira mais rápida de criar configurações OSGi para componentes OSGi bem conhecidos e, especialmente, componentes OSGi personalizados que foram projetados e desenvolvidos pelo mesmo desenvolvedor definindo as configurações. Essa abordagem também pode ser usada para copiar/colar e atualizar configurações para o mesmo componente OSGi em várias pastas do modo de execução.

1. No IDE, abra o `ui.apps` projeto, localize ou crie a pasta de configuração (`/apps/.../config.<runmode>`) que direciona os modos de execução que a nova configuração OSGi precisa aplicar
1. Nesta pasta de configuração, crie um novo `<PID>.cfg.json` arquivo. O PID é a Identidade Persistente do componente OSGi. Geralmente é o nome de classe completo da implementação do componente OSGi. Por exemplo:
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
Observe que os nomes de arquivos de fábrica de configuração OSGi usam o `<factoryPID>-<name>.cfg.json` convenção de nomenclatura
1. Abra o novo `.cfg.json` e defina as combinações de chave/valor para a propriedade OSGi e os pares de valor, seguindo o [Formato de configuração JSON OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).
1. Salve as alterações no novo `.cfg.json` arquivo
1. Adicionar e confirmar o novo arquivo de configuração OSGi no Git

### Gerar configurações de OSGi usando o Início rápido do SDK AEM {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

O AEM Web Console do AEM SDK Quickstart Jar pode ser usado para configurar componentes OSGi e exportar configurações OSGi como JSON. Isso é útil para configurar componentes OSGi fornecidos AEM cujas propriedades OSGi e seus formatos de valor podem não ser bem entendidos pelo desenvolvedor que define as configurações OSGi no projeto AEM.

>[!NOTE]
>
>A interface do usuário de configuração do Console da Web AEM grava `.cfg.json` arquivos no repositório. Portanto, esteja ciente disso para evitar um comportamento inesperado potencial durante o desenvolvimento local, quando as configurações OSGi definidas pelo AEM projeto podem diferir das configurações geradas.

1. Faça logon no console AEM Web do AEM SDK Quickstart Jar como o usuário administrador
1. Navegue até OSGi > Configuração
1. Para configurar, localize o componente OSGi e toque em seu título para editar
   ![Configuração do OSGi](./assets/configuring-osgi/configuration.png)
1. Edite os valores da propriedade de configuração OSGi por meio da interface do usuário da Web, conforme necessário
1. Registre a Identidade Persistente (PID) no local seguro. Isso é usado posteriormente para gerar a configuração JSON do OSGi
1. Toque em Salvar
1. Navegue até OSGi > Impressora de configuração do instalador OSGi
1. Colar no PID copiado na Etapa 5, certifique-se de que o Formato de Serialização esteja definido como &quot;OSGi Configurator JSON&quot;
1. Toque em Imprimir
1. A configuração OSGi no formato JSON será exibida na seção Propriedades de configuração serializadas
   ![Impressora de configuração do instalador OSGi](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. No IDE, abra o `ui.apps` projeto, localize ou crie a pasta de configuração (`/apps/.../config.<runmode>`) que direciona os modos de execução em que a nova configuração OSGi precisa ser aplicada.
1. Nesta pasta de configuração, crie um novo `<PID>.cfg.json` arquivo. O PID é o mesmo valor da Etapa 5.
1. Cole as propriedades de configuração serializadas da etapa 10 no `.cfg.json` arquivo.
1. Salve as alterações no novo `.cfg.json` arquivo.
1. Adicione e confirme seu novo arquivo de configuração OSGi no Git.


## Formatos de propriedade de configuração OSGi {#osgi-configuration-property-formats}

### Valores em linha {#inline-values}

Valores em linha são formatados como pares padrão de valor de nome, seguindo a sintaxe JSON padrão. Por exemplo:

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

Os clientes só devem utilizar esta técnica para as propriedades de configuração OSGI relacionadas com o respectivo código personalizado; ele não deve ser usado para substituir a configuração OSGI definida pelo Adobe.

>[!NOTE]
>
>Os espaços reservados não podem ser usados em [instruções repoinit](/help/implementing/deploying/overview.md#repoinit).

### Valores de configuração secretos {#secret-configuration-values}

A configuração OSGi deve atribuir um espaço reservado para o segredo que deve ser definido por ambiente:

```
use $[secret:SECRET_VAR_NAME]
```

### Nomenclatura de variável {#variable-naming}

O seguinte se aplica aos valores de configuração específicos do ambiente e secretos.

Os nomes das variáveis devem seguir as seguintes regras:

* Comprimento mínimo: 2
* Comprimento máximo: 100
* Deve corresponder ao regex: `[a-zA-Z_][a-zA-Z_0-9]*`

Os valores das variáveis não devem exceder 2048 caracteres.

>[!CAUTION]
>
>Há regras relacionadas ao uso de determinados prefixos para nomes de variáveis:
>
>1. Nomes de variáveis com o prefixo `INTERNAL_`, `ADOBE_`ou `CONST_` são reservadas pelo Adobe. As variáveis definidas pelo cliente que começam com esses prefixos serão ignoradas.
>
>1. Os clientes não devem fazer referência às variáveis com o prefixo `INTERNAL_` ou `ADOBE_` ou.
>
>1. Variáveis de ambiente com o prefixo `AEM_` são definidas pelo produto como API pública para ser usada e definida pelos clientes.
   >   Embora os clientes possam usar e definir variáveis de ambiente, a partir do prefixo `AEM_` elas não devem definir suas próprias variáveis com esse prefixo.


### Valores padrão {#default-values}

O seguinte se aplica aos valores de configuração específicos do ambiente e secretos.

Se nenhum valor por ambiente for definido, no tempo de execução, o espaço reservado não será substituído e será mantido no lugar, pois nenhuma interpolação ocorreu. Para evitar isso, um valor padrão pode ser fornecido como parte do espaço reservado com a seguinte sintaxe:

```
$[env:ENV_VAR_NAME;default=<value>]
```

Com um valor padrão fornecido, o espaço reservado é substituído pelo valor por ambiente, se fornecido, ou pelo valor padrão fornecido.

### Desenvolvimento local {#local-development}

O seguinte se aplica aos valores de configuração específicos do ambiente e secretos.

As variáveis podem ser definidas no ambiente local para que sejam selecionadas pelo AEM local no tempo de execução. Por exemplo, no Linux®:

```bash
export ENV_VAR_NAME=my_value
```

Recomenda-se que um script bash simples seja gravado, que defina as variáveis de ambiente usadas nas configurações e execute-o antes de iniciar o AEM. Ferramentas como [https://direnv.net/](https://direnv.net/) ajudar a simplificar esta abordagem. Dependendo do tipo de valor, eles podem ser verificados no gerenciamento do código-fonte, se puderem ser compartilhados entre todos.

Os valores para segredos são lidos de arquivos. Portanto, para cada espaço reservado usando um segredo, um arquivo de texto contendo o valor secreto deve ser criado.

Por exemplo, se `$[secret:server_password]` é usado, um arquivo de texto chamado **server_password** deve ser criado. Todos esses arquivos secretos devem ser armazenados no mesmo diretório e na propriedade framework `org.apache.felix.configadmin.plugin.interpolation.secretsdir` deve ser configurado com esse diretório local.

### Configuração de autor versus publicação {#author-vs-publish-configuration}

Se uma propriedade OSGI exigir valores diferentes para autor versus publicação:

* Separar `config.author` e `config.publish` As pastas OSGi devem ser usadas, conforme descrito na [Seção Resolução do Modo de Execução](#runmode-resolution).
* Há duas opções para criar nomes de variáveis independentes que devem ser usadas:
   * a primeira opção, que é recomendada: em todas as pastas OSGI (como `config.author` e `config.publish`) declarada para definir valores diferentes, use o mesmo nome de variável. Por exemplo
      `$[env:ENV_VAR_NAME;default=<value>]`, onde o padrão corresponde ao valor padrão dessa camada (autor ou publicação). Ao definir a variável de ambiente por meio de [API do Cloud Manager](#cloud-manager-api-format-for-setting-properties) ou por meio de um cliente, diferencie os níveis usando o parâmetro &quot;serviço&quot;, conforme descrito nesta [Documentação de referência da API](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables). O parâmetro &quot;service&quot; vinculará o valor da variável ao nível OSGI apropriado. Pode ser &quot;autor&quot; ou &quot;publicação&quot; ou &quot;visualização&quot;.
   * a segunda opção, que é declarar variáveis distintas usando um prefixo como `author_<samevariablename>` e `publish_<samevariablename>`

### Exemplos de configuração {#configuration-examples}

Nos exemplos abaixo, considere que há três ambientes de desenvolvimento, além dos ambientes de preparo e produção.

**Exemplo 1**

A intenção é do valor da propriedade OSGI `my_var1` para ser o mesmo para estágio e produção, mas diferente para cada um dos três ambientes de desenvolvimento.

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
{ "my_var1": "val", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

**Exemplo 2**

A intenção é do valor da propriedade OSGI `my_var1` para diferenciar para estágio, produção e para cada um dos três ambientes de desenvolvimento. Portanto, a API do Cloud Manager deve ser chamada para definir o valor de `my_var1` para cada dev env.

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
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ "my_var1": "val2", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

**Exemplo 3**

A intenção é do valor da propriedade OSGi `my_var1` para ser o mesmo para estágio, produção e apenas um dos ambientes de desenvolvimento, mas para que seja diferente para os outros dois ambientes de desenvolvimento. Nesse caso, a API do Cloud Manager deve ser chamada para definir o valor de `my_var1` para cada um dos ambientes de desenvolvimento, incluindo para o ambiente de desenvolvimento que deve ter o mesmo valor de estágio e produção. Ele não herdará o valor definido na pasta **configuração**.

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
configuração
</td>
<td>
<pre>
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

Outra maneira de fazer isso seria definir um valor padrão para o token de substituição na pasta config.dev de forma que ele tenha o mesmo valor do **configuração** pasta.

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
configuração
</td>
<td>
<pre>
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1": "$[env:my_var1;default=val1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

## Formato de API do Cloud Manager para propriedades de configuração {#cloud-manager-api-format-for-setting-properties}

Consulte [esta página](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md) sobre como a API deve ser configurada.
>[!NOTE]
>
>Verifique se a API do Cloud Manager usada atribuiu a função &quot;Gerenciador de implantação - Cloud Service&quot;. Outras funções não podem executar todos os comandos abaixo.

### Configuração de valores por API {#setting-values-via-api}

Chamar a API implanta as novas variáveis e valores em um ambiente do Cloud, de modo semelhante a um pipeline típico de implantação de código do cliente. Os serviços de criação e publicação serão reiniciados e farão referência aos novos valores, normalmente levando alguns minutos.

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```
]
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
>Consulte [esta página](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) para obter mais informações.

### Obter valores por meio da API {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

Consulte [esta página](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables) para obter mais informações.

### Exclusão de valores por API {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

Para excluir uma variável, inclua-a com um valor vazio.

Consulte [esta página](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) para obter mais informações.

### Obter valores através da linha de comando {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### Definindo valores através da Linha de Comando {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### Exclusão de valores por meio da linha de comando {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>Consulte [esta página](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para obter mais informações sobre como configurar valores usando o plug-in do Cloud Manager para a CLI do Adobe I/O.

### Número de variáveis {#number-of-variables}

É possível declarar até 200 variáveis por ambiente.

## Considerações de implantação para valores de configuração secretos e específicos do ambiente {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

Como os valores de configuração secretos e específicos do ambiente estão fora do Git e, portanto, não fazem parte dos mecanismos formais de implantação do Adobe Experience Manager as a Cloud Service, o cliente deve gerenciar, controlar e integrar o processo de implantação do Adobe Experience Manager as a Cloud Service.

Como mencionado acima, chamar a API implanta as novas variáveis e valores em ambientes do Cloud, de forma semelhante a um pipeline de implantação de código do cliente típico. Os serviços de criação e publicação serão reiniciados e farão referência aos novos valores, normalmente levando alguns minutos. Observe que as portas de qualidade e os testes que são executados pelo Cloud Manager durante uma implantação de código regular não são executados durante esse processo.

Normalmente, os clientes chamam a API para definir variáveis de ambiente antes de implantar um código que depende deles no Cloud Manager. Em algumas situações, pode ser necessário modificar uma variável existente depois que o código já tiver sido implantado.

>[!NOTE]
>
>A API pode não ter sucesso quando um pipeline está em uso, seja uma atualização de AEM ou implantação de cliente, dependendo de qual parte do pipeline de fim a fim está sendo executada no momento. A resposta do erro indicará que a solicitação não foi bem-sucedida, embora não indique o motivo específico.

Pode haver cenários em que uma implantação de código agendada do cliente dependa de variáveis existentes para ter novos valores, o que não seria apropriado com o código atual. Se isso for uma preocupação, é recomendável fazer modificações variáveis de maneira aditiva. Para fazer isso, crie novos nomes de variáveis em vez de apenas alterar o valor de variáveis antigas, de modo que o código antigo nunca faça referência ao novo valor. Em seguida, quando a nova versão do cliente parecer estável, é possível optar por remover os valores mais antigos.

Da mesma forma, como os valores de uma variável não têm controle de versão, uma reversão do código pode fazer com que faça referência a valores mais recentes que causem problemas. A estratégia de variável de aditivos anteriormente mencionada também ajudaria neste caso.

Essa estratégia de variável aditiva também é útil para cenários de recuperação de desastres em que, se o código de vários dias antes precisasse ser implantado novamente, os nomes e valores de variáveis referenciados ainda estarão intactos. Isso depende de uma estratégia em que um cliente aguarda alguns dias antes de remover essas variáveis mais antigas, caso contrário, o código mais antigo não teria as variáveis apropriadas para fazer referência.
