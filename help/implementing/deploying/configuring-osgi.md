---
title: Configuração do OSGi para AEM como um serviço em nuvem
description: 'Configuração do OSGi com valores secretos e valores específicos do Ambiente '
translation-type: tm+mt
source-git-commit: 10e12a8b15e6ea51e8b022deefaefed52780d48a
workflow-type: tm+mt
source-wordcount: '2509'
ht-degree: 0%

---


# Configuring OSGi for AEM as a Cloud Service {#configuring-osgi-for-aem-as-a-cloud-service}

[O OSGi](https://www.osgi.org/) é um elemento fundamental na pilha de tecnologias do Adobe Experience Manager (AEM). É usado para controlar os pacotes compostos do AEM e suas configurações.

O OSGi fornece as primitivas padronizadas que permitem que aplicativos sejam construídos a partir de componentes pequenos, reutilizáveis e colaborativos. Esses componentes podem ser compostos em um aplicativo e implantados. Isso permite o gerenciamento fácil de pacotes OSGi, pois eles podem ser interrompidos, instalados e iniciados individualmente. As interdependências são tratadas automaticamente. Cada componente OSGi está contido em um dos vários pacotes. Para obter mais informações, consulte a especificação [do](https://www.osgi.org/Specifications/HomePage)OSGi.

Você pode gerenciar as configurações de componentes OSGi por meio de arquivos de configuração que fazem parte de um projeto de código AEM.

## Arquivos de configuração do OSGi {#osgi-configuration-files}

As alterações de configuração são definidas nos pacotes de código do AEM Project (`ui.apps`) como arquivos de configuração (`.cfg.json`) em pastas de configuração específicas do modo de execução:

`/apps/example/config.<runmode>`

O formato dos arquivos de configuração OSGi é baseado em JSON, usando o `.cfg.json` formato definido pelo projeto Apache Sling.

As configurações OSGi públicos alvos componentes OSGi por meio de sua identificação persistente (PID), que assume o nome padrão da classe Java do componente OSGi. Por exemplo, para fornecer configuração OSGi para um serviço OSGi implementado por:

`com.example.workflow.impl.ApprovalWorkflow.java`

um arquivo de configuração OSGi é definido em:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

seguindo o formato [de configuração]cfg.json OSGi (após o formato de configuração cfg.json OSGi).

> [!NOTE]
>
> Versões anteriores de arquivos de configuração OSGi com suporte do AEM usando diferentes formatos de arquivo, como .cfg., .config e como definições de recurso XML sling:OsgiConfig. Esses formatos são substituídos pelo formato de configuração cfg.json OSGi.

## Resolução do modo de execução {#runmode-resolution}

Configurações específicas de OSGi podem ser direcionadas a instâncias específicas de AEM usando modos de execução. Para usar o modo de execução, crie pastas de configuração em `/apps/example` (onde exemplo é o nome do projeto), no formato:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Quaisquer configurações OSGi nessas pastas serão usadas se os modos de execução definidos no nome da pasta de configuração corresponderem aos modos de execução usados pelo AEM.

Por exemplo, se o AEM estiver usando o autor e o dev do runmode, nós de configuração em `/apps/example/config.author/` e `/apps/example/config.author.dev/` serão aplicados, enquanto nós de configuração em `/apps/example/config.publish/` e não `/apps/example/config.author.stage/` serão aplicados.

Se várias configurações para o mesmo PID forem aplicáveis, a configuração com o maior número de modos de execução correspondentes será aplicada.

A granularidade desta regra está em um nível PID. Isso significa que não é possível definir algumas propriedades para o mesmo PID em `/apps/example/config.author/` e mais específicas em `/apps/example/config.author.dev/` para o mesmo PID.  A configuração com o maior número de modos de execução correspondentes será eficaz para todo o PID.

Ao desenvolver localmente, um parâmetro de inicialização do modo de execução pode ser passado para ditar qual configuração do modo de execução OSGI será usada.

## Tipos de valores de configuração OSGi {#types-of-osgi-configuration-values}

Há três variedades de valores de configuração OSGi que podem ser usadas com o AEM como um serviço em nuvem.

1. **Valores** em linha, que são valores codificados permanentemente na configuração OSGi e armazenados em Git. Por exemplo:

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **Valores** secretos, que são valores que não devem ser armazenados em Git por motivos de segurança. Por exemplo:

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **Valores** específicos do Ambiente, que são valores que variam entre ambientes de desenvolvimento e, portanto, não podem ser direcionados com precisão pelo modo de execução (pois há um único `dev` modo de execução no AEM como um serviço de nuvem). Por exemplo:

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

## Como escolher o tipo de valor de configuração OSGi apropriado {#how-to-choose-the-appropriate-osgi-configuration-value-type}

O caso comum para OSGi usa valores de configuração OSGi em linha. As configurações específicas do Ambiente são usadas apenas para casos de uso específicos em que um valor é diferente entre ambientes dev.

![](assets/choose-configuration-value-type_res1.png)

As configurações específicas do Ambiente estendem as configurações OSGi tradicionais e definidas estaticamente que contêm valores em linha, proporcionando a capacidade de gerenciar os valores de configuração OSGi externamente por meio da API do Cloud Manager. É importante entender quando deve ser usada a abordagem comum e tradicional de definir valores em linha e armazená-los em Git, em vez de abstrair os valores em configurações específicas do ambiente.

As orientações a seguir abordam quando usar configurações não secretas e secretas específicas do ambiente:

### Quando usar valores de configuração embutidos {#when-to-use-inline-configuration-values}

Os valores de configurações em linha são considerados a abordagem padrão e devem ser usados quando possível. As configurações em linha oferecem os benefícios de:

* Eles são mantidos, com governança e histórico de versões no Git
* Os valores estão implicitamente vinculados às implantações de código
* Eles não exigem considerações adicionais de implantação nem coordenação

Sempre que definir um valor de configuração OSGi, start com valores em linha, qualquer configuração secreta ou específica do ambiente só será selecionada se necessário para o caso de uso.

### Quando usar valores de configuração não secretos específicos para Ambientes {#when-to-use-non-secret-environment-specific-configuration-values}

Use apenas configurações específicas do ambiente (`$[env:ENV_VAR_NAME]`) para valores de configuração não secretos quando os valores variarem entre ambientes de desenvolvimento. Isso inclui instâncias de desenvolvimento local e qualquer AEM como ambientes de desenvolvimento de serviços em nuvem. Evite usar configurações não secretas específicas de ambientes para o AEM como um Palco de serviço em nuvem ou ambientes de produção.

* Use apenas configurações não secretas específicas do ambiente para valores de configuração que diferem entre ambientes de desenvolvimento, incluindo instâncias de desenvolvimento local.
* Em vez disso, use os valores em linha padrão nas configurações OSGi para valores não secretos de Fase e Produção.  Neste contexto, não é recomendável usar configurações específicas do ambiente para facilitar as alterações de configuração no tempo de execução para o Palco e ambientes de Produção; estas alterações devem ser introduzidas através da gestão do código fonte.

### Quando usar valores de configuração secretos específicos do ambiente {#when-to-use-secret-environment-specific-configuration-values}

O AEM como um serviço em nuvem exige o uso de configurações específicas do ambiente (`$[secret:SECRET_VAR_NAME]`) para quaisquer valores secretos de configuração OSGi, como senhas, chaves de API privadas ou quaisquer outros valores que não possam ser armazenados no Git por motivos de segurança.

Use configurações secretas específicas ao ambiente para armazenar o valor dos segredos em todo o AEM como ambientes de serviço em nuvem, incluindo o Palco e a Produção.

### Adicionando uma nova configuração ao repositório {#adding-a-new-configuration-to-the-repository}

#### O que você precisa saber {#what-you-need-to-know}

Para adicionar uma nova configuração ao repositório, é necessário saber o seguinte:

1. A identidade **** persistente (PID) do serviço.

   Consulte o campo **Configurações** no console da Web. O nome é mostrado entre parênteses após o nome do pacote (ou nas Informações **de** configuração na parte inferior da página).

   Por exemplo, crie um nó `com.day.cq.wcm.core.impl.VersionManagerImpl.` para configurar o Gerenciador **de versões do** AEM WCM.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Se um modo de execução específico é necessário. Crie a pasta:

   * `config` - para todos os modos de execução
   * `config.author` - pelo ambiente do autor
   * `config.publish` - para o ambiente publish
   * `config.<run-mode>` - se for caso disso

1. Se uma configuração **de configuração** ou configuração de **fábrica** é necessária.
1. Os parâmetros individuais a configurar; incluindo qualquer definição de parâmetro existente que precise ser recriada.

   Consulte o campo de parâmetro individual no console da Web. O nome é mostrado entre parênteses para cada parâmetro.

   Por exemplo, crie uma propriedade
   `versionmanager.createVersionOnActivation` para configurar **Criar versão na Ativação**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Já existe uma configuração em `/libs`? Para lista de todas as configurações em sua instância, use a ferramenta **Query** no CRXDE Lite para enviar o seguinte query SQL:

   `select * from sling:OsgiConfig`

   Em caso afirmativo, essa configuração pode ser copiada para ` /apps/<yourProject>/`, em seguida, personalizada no novo local.

## Criação da configuração no repositório {#creating-the-configuration-in-the-repository}

Para adicionar a nova configuração ao repositório:

1. No projeto ui.apps, crie uma `/apps/…/config.xxx` pasta conforme necessário com base no modo de execução que você está usando

1. Crie um novo arquivo JSON com o nome do PID e adicione a `.cfg.json` extensão


1. Preencha o arquivo JSON com os pares de valores da chave de configuração OSGi

   >[!NOTE]
   >
   >Se você estiver configurando um serviço OSGi pronto, poderá procurar os nomes de propriedade OSGi por meio de `/system/console/configMgr`


1. Salve o arquivo JSON em seu projeto.

## Formato De Propriedade De Configuração No Controle De Origem {#configuration-property-format-in-source-control}

A criação de uma nova propriedade de configuração OSGI está descrita na seção [Adicionar uma nova configuração ao repositório](#creating-the-configuration-in-the-repository) acima. Siga essas etapas e modifique a sintaxe conforme descrito nas subseções abaixo:

### Valores em linha {#inline-values}

Como seria de esperar, os valores em linha são formatados como pares padrão de nome-valor, seguindo a sintaxe JSON padrão. Por exemplo:

```json
 {

 "my_var1": "val",
 "my_var2": "abc",
 "my_var3": 500

}
```

### Valores de Configuração Específicos do Ambiente {#environment-specific-configuration-values}

A configuração do OSGi deve atribuir um espaço reservado para a variável que deve ser definida por ambiente:

```
use $[env:ENV_VAR_NAME]
```

Os clientes só devem utilizar esta técnica para as propriedades de configuração OSGI relacionadas com o respectivo código personalizado; ele não deve ser usado para substituir a configuração OSGI definida pela Adobe.

### Valores de configuração secretos {#secret-configuration-values}

A configuração do OSGi deve atribuir um espaço reservado para o segredo que deve ser definido por ambiente:

```
use $[secret:SECRET_VAR_NAME]
```

### Nomeação de variável {#variable-naming}

O seguinte se aplica aos valores de configuração específicos e secretos do ambiente.

Os nomes das variáveis devem seguir as seguintes regras:

* Comprimento mínimo: 2
* Comprimento máximo: 100
* deve corresponder a regex: `[a-zA-Z_][a-zA-Z_0-9]*`

Os valores das variáveis não devem exceder 2048 caracteres.

### Valores padrão {#default-values}

O seguinte se aplica aos valores de configuração específicos e secretos do ambiente.

Se nenhum valor por ambiente for definido, no tempo de execução o espaço reservado não será substituído e mantido no lugar, pois nenhuma interpolação ocorreu. Para evitar isso, um valor padrão pode ser fornecido como parte do espaço reservado com a seguinte sintaxe:

```
$[env:ENV_VAR_NAME;default=<value>]
```

Com um valor padrão fornecido, o espaço reservado será substituído pelo valor por ambiente, se fornecido, ou pelo valor padrão fornecido.

### Desenvolvimento local {#local-development}

O seguinte se aplica aos valores de configuração específicos e secretos do ambiente.

As variáveis podem ser definidas no ambiente local para que sejam coletadas pelo AEM local no tempo de execução. Por exemplo, no Linux:

```bash
export ENV_VAR_NAME=my_value
```

É recomendável que um script bash simples seja gravado, que defina as variáveis de ambiente usadas nas configurações e execute-o antes de iniciar o AEM. Ferramentas como [https://direnv.net/](https://direnv.net/) ajudam a simplificar essa abordagem. Dependendo do tipo de valores, eles podem ser verificados no gerenciamento de código-fonte, se puderem ser compartilhados entre todos.

Os valores para segredos são lidos de arquivos. Portanto, para cada espaço reservado que usa um segredo, é necessário criar um arquivo de texto contendo o valor secreto.

Por exemplo, se `$[secret:server_password]` for usado, um arquivo de texto chamado **server_password** precisa ser criado. Todos esses arquivos secretos precisam ser armazenados no mesmo diretório e a propriedade framework `org.apache.felix.configadmin.plugin.interpolation.secretsdir` precisa ser configurada com esse diretório local.

### Configuração de autor versus publicação {#author-vs-publish-configuration}

Se uma propriedade OSGI exigir valores diferentes para autor versus publicação:

* pastas separadas `config.author` e `config.publish` OSGi devem ser usadas, conforme descrito na seção [Resolução](#runmode-resolution)Runmode.
* devem ser usados nomes de variáveis independentes. É recomendável usar um prefixo como `author_<variablename>` e `publish_<variablename>` onde os nomes das variáveis sejam os mesmos

### Exemplos de configuração {#configuration-examples}

Nos exemplos abaixo, suponha que haja 3 ambientes dev, além dos ambientes stage e prod.

**Exemplo 1**

O objetivo é que o valor da propriedade OSGI seja igual `my_var1` para stage e prod, mas diferente para cada um dos três ambientes dev.

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
{ "my_var1": "val", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

**Exemplo 2**

O objetivo é que o valor da propriedade OSGI seja diferente `my_var1` para stage, prod e para cada um dos 3 ambientes dev. Assim, a API do Gerenciador de nuvem precisará ser chamada para definir o valor para `my_var1` cada adenv dev.

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
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ "my_var1": "val2", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

**Exemplo 3**

A intenção é que o valor da propriedade OSGi seja o mesmo para o palco, produção e apenas um dos ambientes dev, mas que seja diferente para os outros dois ambientes dev. `my_var1` Nesse caso, a API do Gerenciador de nuvem precisará ser chamada para definir o valor de `my_var1` cada um dos ambientes dev, incluindo o ambiente dev que deve ter o mesmo valor que stage e production. Ele não herdará o valor definido na **configuração** da pasta.

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
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

Outra maneira de fazer isso seria definir um valor padrão para o token de substituição na pasta config.dev de modo que ele tenha o mesmo valor que na pasta **config** .

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
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1": "$[env:my_var1;default=val1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

## Formato da API do Cloud Manager para a definição de propriedades {#cloud-manager-api-format-for-setting-properties}

### Configuração de valores por API {#setting-values-via-api}

A chamada da API implantará as novas variáveis e valores em um ambiente da Cloud, de modo semelhante a um pipeline de implantação de código de cliente típico. Os serviços de autor e publicação serão reiniciados e farão referência aos novos valores, normalmente demorando alguns minutos.

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

Observe que as variáveis padrão não são definidas por API, mas na própria propriedade OSGi.

Consulte [esta página](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) para obter mais informações.

### Obter valores por meio da API {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

Consulte [esta página](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables) para obter mais informações.

### Excluindo valores por meio da API {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

Para excluir uma variável, inclua-a com um valor vazio.

Consulte [esta página](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) para obter mais informações.

### Obtendo valores pela linha de comando {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### Configuração de valores pela Linha de Comando {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### Exclusão de valores pela linha de comando {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

> [!NOTE]
>
> Consulte [esta página](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) para obter mais informações sobre como configurar valores usando o plug-in do Gerenciador de nuvem para a CLI de E/S da Adobe.

### Número de variáveis {#number-of-variables}

Até 20 variáveis podem ser declaradas.

## Considerações de implantação para valores de configuração secretos e específicos do Ambiente {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

Como os valores de configuração secretos e específicos do ambiente permanecem fora do Git e, portanto, não fazem parte do AEM formal como um mecanismo de implantação do Serviço em nuvem, o cliente deve gerenciar, administrar e integrar o AEM como um processo de implantação do Serviço em nuvem.

Como mencionado acima, chamar a API implantará as novas variáveis e valores em ambientes da Cloud, de modo semelhante a um pipeline de implantação de código do cliente típico. Os serviços de autor e publicação serão reiniciados e farão referência aos novos valores, normalmente demorando alguns minutos. Observe que as portas de qualidade e os testes executados pelo Gerenciador de nuvem durante uma implantação regular de código não são executados durante esse processo.

Normalmente, os clientes ligam para a API para definir variáveis de ambiente antes de implantar um código que depende deles no Cloud Manager. Em algumas situações, é possível modificar uma variável existente após a implantação do código.

Observe que a API pode não ter êxito quando um pipeline está em uso, seja uma atualização do AEM ou implantação do cliente, dependendo de qual parte do pipeline de fim a fim está sendo executada no momento. A resposta ao erro indicará que a solicitação não foi bem-sucedida, embora não indique o motivo específico.

Pode haver situações em que uma implantação programada de código de cliente dependa de variáveis existentes para ter novos valores, o que não seria apropriado com o código atual. Se isso for uma preocupação, é recomendável fazer modificações variáveis de uma forma aditiva. Para fazer isso, crie novos nomes de variáveis em vez de apenas alterar o valor de variáveis antigas para que o código antigo nunca faça referência ao novo valor. Em seguida, quando a nova versão do cliente parecer estável, é possível optar por remover os valores mais antigos.

Da mesma forma, como os valores de uma variável não têm controle de versão, uma reversão do código pode fazer com que ele faça referência a valores mais recentes que causam problemas. A estratégia de variáveis aditivas acima mencionada também ajudaria neste caso.

Essa estratégia de variável aditiva também é útil para cenários de recuperação de desastres em que, se o código de vários dias antes precisar ser implantado novamente, os nomes e os valores de variável aos quais ele faz referência permanecerão intactos. Isso depende de uma estratégia em que um cliente espera alguns dias antes de remover essas variáveis mais antigas, caso contrário, o código mais antigo não teria variáveis apropriadas para fazer referência.