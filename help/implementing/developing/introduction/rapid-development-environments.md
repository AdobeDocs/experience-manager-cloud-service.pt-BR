---
title: Ambientes de desenvolvimento rápido
description: Saiba como usar Ambientes de desenvolvimento rápido para iterações de desenvolvimento rápido em um ambiente de nuvem.
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
feature: Developing
role: Admin, Architect, Developer
source-git-commit: fd57437b16a87de2b279b0f8bc10c12a7d3f721a
workflow-type: tm+mt
source-wordcount: '4537'
ht-degree: 3%

---

# Ambientes de desenvolvimento rápido {#rapid-development-environments}

Para implantar alterações, os ambientes de desenvolvimento de nuvem atuais exigem o uso de um processo que emprega regras abrangentes de segurança e qualidade de código chamadas de pipeline de CI/CD. Para situações em que são necessárias alterações rápidas e iterativas, o Adobe introduziu os RDEs (Rapid Development Environments, ambientes de desenvolvimento rápido).

As RDEs permitem que os desenvolvedores implantem e revisem alterações rapidamente, minimizando o tempo necessário para testar recursos que comprovadamente funcionam em um ambiente de desenvolvimento local.

Depois que as alterações forem testadas em um RDE, elas poderão ser implantadas em um ambiente de desenvolvimento de nuvem regular por meio do pipeline do Cloud Manager.

>[!NOTE]
> Entre em contato com os desenvolvedores de RDE em nosso [canal Discord](https://discord.com/channels/1131492224371277874/1245304281184079872). Sinta-se à vontade para fazer qualquer pergunta ou dar feedback sobre os tópicos RDE.

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


Você pode ver vídeos adicionais demonstrando [como configurá-lo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html), [como usá-lo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html) e o [ciclo de vida de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) usando RDE.

## Introdução {#introduction}

Os RDEs podem ser usados para configurações de código, conteúdo e Apache ou Dispatcher. Diferentemente dos ambientes de desenvolvimento de nuvem comuns, os desenvolvedores podem usar ferramentas de linha de comando locais para sincronizar o código criado localmente em um RDE.

Cada programa é provisionado com um RDE. Se houver contas de sandbox, elas hibernarão após algumas horas de inatividade.

Após a criação, os RDEs são definidos para a versão mais recente do Adobe Experience Manager (AEM). Uma reinicialização RDE, que pode ser executada usando Cloud Manager, circula o RDE e o configura para a versão AEM mais recente disponível.

Normalmente, um RDE seria usado por um único desenvolvedor em um determinado momento, para testar e depurar um recurso específico. Quando a sessão de desenvolvimento for concluída, o RDE poderá ser redefinido para um estado padrão para o próximo uso.

RDEs adicionais podem ser licenciados para programas de produção (não sandbox).

## Ativar o RDE em um programa {#enabling-rde-in-a-program}

Siga estas etapas para poder usar o Cloud Manager para criar um RDE para seu programa.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa ao qual deseja adicionar um RDE para mostrar seus detalhes.

   * Os RDEs podem ser adicionados a [programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) e [programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).

1. Na página **Visão geral do Programa**, clique em **Adicionar Ambiente** no cartão **Ambientes** para adicionar um ambiente.

   ![Cartão Ambientes](/help/implementing/cloud-manager/assets/no-environments.png)

   * A opção **Adicionar ambiente** também está disponível na guia **Ambientes**.

     ![Guia Ambientes](/help/implementing/cloud-manager/assets/environments-tab.png)

   * A opção **Adicionar ambiente** pode estar desativada devido à falta de permissões ou dependendo dos recursos licenciados.

1. Na caixa de diálogo **Adicionar ambiente**:

   * Selecione **Desenvolvimento rápido** no cabeçalho **Selecionar tipo de ambiente**.
      * O número de ambientes disponíveis/usados é exibido entre parênteses atrás do tipo de ambiente.
   * Forneça um **Nome** para o ambiente.
   * Forneça uma **Descrição** opcional para o ambiente.
   * Selecione a **Região da nuvem**.

   ![Caixa de diálogo Adicionar ambiente](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. Clique em **Salvar** para adicionar o ambiente especificado.

A tela **Visão geral** agora exibe seu novo ambiente no cartão **Ambientes**.

Após a criação, os RDEs são definidos para a versão mais recente do AEM disponível. Uma redefinição de RDE, que também pode ser executada usando o Cloud Manager, circula o RDE e o configura para a versão AEM mais recente disponível.

Para obter mais informações sobre como usar o Cloud Manager para criar ambientes, gerenciar quem tem acesso a eles e atribuir domínios personalizados, consulte [a documentação do Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

## Instalação das Ferramentas de Linha de Comando do RDE {#installing-the-rde-command-line-tools}

Depois de ter adicionado um RDE para seu programa usando o Cloud Manager, você pode interagir com ele configurando as ferramentas de linha de comando conforme descrito nas seguintes etapas:

>[!IMPORTANT]
>
>Verifique se você tem a versão 20 do [Nó e NPM instalados](https://nodejs.org/en/download/) para que a CLI do Adobe I/O e os plug-ins relacionados funcionem corretamente.


1. Instale as ferramentas CLI do Adobe I/O de acordo com este [procedimento](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. Instale o plug-in AEM RDE das ferramentas da CLI do Adobe I/O:

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. Faça logon usando o cliente aio.

   ```
   aio login
   ```
   As informações de logon (token) são armazenadas na configuração global do aio e, portanto, são compatíveis apenas com um logon e uma organização. Caso deseje usar vários RDEs que precisam de logons ou organizações diferentes, siga o exemplo abaixo introduzindo contextos.

   <details><summary>Siga este exemplo para configurar um contexto local para um de seus logons RDE</summary>
   Para armazenar as informações de logon localmente em um arquivo .aio no diretório atual em um contexto específico, siga estas etapas. Um contexto também é uma maneira inteligente de configurar um ambiente ou script de CI/CD.  Para usar esse recurso, use pelo menos a versão aio-cli 10.3.1. Atualize-o usando "npm install -g @adobe/aio-cli"

   Vamos criar um contexto chamado &#39;mycontext&#39;, que definimos como o contexto padrão usando o plug-in de autenticação antes de chamar o comando de logon.

   ```
   aio config set --json -l "ims.contexts.mycontext" "{ cli.bare-output: false }"
   aio auth ctx -s mycontext
   aio login --no-open
   ```


   >[!NOTE]
   > O comando de logon com a opção `--no-open` resultará em uma URL no terminal em vez de abrir o navegador padrão. Assim você pode copiar e abri-lo com uma janela **incógnita** do seu navegador. Dessa forma, a sessão conectada no momento na janela normal do navegador permanecerá intocada e você poderá garantir o uso do logon e da organização específicos necessários para o contexto.

   O primeiro comando cria uma nova configuração de contexto de logon, chamada `mycontext`, no arquivo de configuração `.aio` local (o arquivo é criado, se necessário). O segundo comando define o contexto `mycontext` como o contexto &quot;atual&quot;, ou seja, o padrão.

   Com essa configuração em vigor, o comando de logon armazena automaticamente os tokens de logon no contexto `mycontext` e, portanto, os mantém locais.

   Vários contextos podem ser gerenciados ao manter as configurações locais em várias pastas. Como alternativa, também é possível definir vários contextos em um único arquivo de configuração e alternar entre eles alterando o contexto &quot;atual&quot;.
   </details>

1. Configure o plug-in RDE para usar sua organização, programa e ambiente. O comando de configuração abaixo fornecerá interativamente ao usuário uma lista de programas em sua organização e mostrará os ambientes RDE nesse programa para escolher.

   ```
   aio aem:rde:setup
   ```

   A etapa de configuração pode ser ignorada se a intenção for usar um ambiente com script, nesse caso, os valores de organização, programa e ambiente podem ser incluídos em cada comando. [Consulte comandos rde abaixo para obter mais informações](#rde-cli-commands).

### A configuração interativa {#installing-the-rde-command-line-tools-interactive}

O comando setup perguntará se a configuração fornecida deve ser armazenada local ou globalmente.

```
Setup the CLI configuration necessary to use the RDE commands.
? Do you want to store the information you enter in this setup procedure locally? (y/N)
```

Escolha `no` para
* armazene a organização, o programa e o ambiente globalmente na configuração do aio.
* trabalhar apenas com um único RDE.

Escolha `yes` para
* armazenar a organização, o programa e o ambiente localmente no diretório atual, em um arquivo `.aio`. Isso é conveniente se você quiser confirmar o arquivo no controle de versão para que outras pessoas que clonarem o repositório Git possam usá-lo.
* trabalhar com muitos RDEs, de modo que a alternância para outro diretório usará essa configuração.
* use a configuração em um contexto programático como um script, que pode fazer referência a ela.


Depois que a configuração local ou global for selecionada, o comando de configuração tentará ler a ID da organização no logon atual e, em seguida, ler os programas da organização. Caso a organização não possa ser encontrada, você poderá inseri-la manualmente junto com algumas orientações.

```
 Selected only organization: XYXYXYXYXYXYXYXXYY
 retrieving programs of your organization ...
```

Depois que os programas forem recuperados, o usuário poderá selecionar na lista e também digitar para filtrar.
Quando o programa foi selecionado, uma lista de ambientes RDE é listada para escolher.
Caso haja apenas um programa e/ou ambiente RDE disponível, ele será selecionado automaticamente.

Para ver o contexto do ambiente atual, execute:

```aio aem rde setup --show```

O comando responderá com um resultado semelhante a:

```Current configuration: cm-p1-e1: programName - environmentName (organization: ...@AdobeOrg)```

### Procedimento de configuração manual em um ambiente não interativo {#manual-setup}

Para ambientes em que nenhum usuário pode executar interativamente o comando de configuração conforme descrito acima (como CI/CD ou scripts), os três parâmetros para organização, programa e ambiente podem ser configurados manualmente de acordo com as etapas a seguir.


<details>
  <summary>Expanda para encontrar detalhes sobre como configurar manualmente</summary>

1. Configure a ID da organização e substitua a sequência alfanumérica pela ID da própria organização.

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   * Sua própria ID da organização pode ser pesquisada usando o método documentado em [Exibir ID da organização](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. Em seguida, configure a ID do programa:

   `aio config:set cloudmanager_programid 12345`

1. Em seguida, configure a ID de ambiente à qual o RDE será anexado:

   `aio config:set cloudmanager_environmentid 123456`

1. Depois de concluir a configuração do plug-in, faça logon executando

   `aio login`

   Essas etapas exigem que você seja membro do Perfil de Produto Cloud Manager **Developer - Cloud Service**. Consulte [Atribuir membros da equipe a perfis de produto do Cloud Manager - Atribuir o perfil de produto do desenvolvedor](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) para obter mais detalhes.

Para obter mais informações e demonstração, assista ao tutorial em vídeo [como configurar um RDE (06:24)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html).
</details>

## Usar o RDE ao desenvolver um novo recurso {#using-rde-while-developing-a-new-feature}

A Adobe recomenda o seguinte fluxo de trabalho para desenvolver um novo recurso:

* Quando um marco intermediário for atingido e validado localmente com êxito com o SDK do AEM as a Cloud Service, confirme o código em uma ramificação de recurso do Git. A ramificação ainda não deve fazer parte da linha principal, embora a confirmação no Git seja opcional. O que constitui um &quot;marco intermediário&quot; varia com base nos hábitos da equipe. Os exemplos incluem algumas novas linhas de código, meio dia de trabalho ou a conclusão de um sub-recurso.

* Redefina o RDE se ele tiver sido usado por outro recurso e você quiser [redefini-lo para um estado padrão](#reset-rde). <!-- Alexandru: hiding for now, do not delete This can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). -->A redefinição leva alguns minutos e todo o conteúdo e código existentes é excluído. Você pode usar o comando RDE status para confirmar se o RDE está pronto. O RDE volta com a versão mais recente do AEM.

  >[!IMPORTANT]
  >
  > Se seus ambientes de preparo e produção não estiverem recebendo atualizações automáticas de lançamento de AEM e estiverem por trás da versão mais recente de lançamento de AEM, o código em execução no RDE pode não corresponder à forma como o código funciona no preparo e na produção. Nesse caso, é especialmente importante executar testes completos do código no preparo antes de implantá-lo na produção.


* Usando a interface de linha de comando do RDE, sincronize o código local com o RDE. As opções incluem instalar um pacote de conteúdo, um pacote específico, um arquivo de configuração OSGI, um arquivo de conteúdo e um arquivo zip de uma configuração Apache/Dispatcher. Também é possível fazer referência a um pacote de conteúdo remoto. Consulte [Ferramentas de Linha de Comando RDE](/help/implementing/developing/introduction/rapid-development-environments.md#rde-cli-commands) para obter mais informações. Você pode usar o comando status para validar se a implantação foi bem-sucedida. Opcionalmente, use o Gerenciador de pacotes para instalar pacotes de conteúdo.

* Teste o código no RDE. Os URLs do Author e do Publish estão disponíveis no Cloud Manager.

* Se o código não se comportar conforme esperado, use técnicas de depuração padrão para entender o problema e fazer as alterações apropriadas. Sem confirmar as modificações de código no Git (já que não foram validadas), use a CLI local para sincronizar o código ao RDE. Continue iterando até que o problema seja resolvido.

* Depois que o código se comportar conforme esperado, confirme-o na ramificação do recurso Git.

* O código sincronizado com o RDE não usa um pipeline do Cloud Manager, portanto, agora você deve usar um pipeline de não produção do Cloud Manager para implantar a ramificação do recurso Git no ambiente de desenvolvimento da nuvem. Isso valida que o código passe pelos quality gates (portais de qualidade) do Cloud Manager e permite que você tenha certeza de que ele será implantado posteriormente com êxito usando o pipeline de produção do Cloud Manager.

* Repita as etapas acima para cada marco intermediário até que todo o código do recurso esteja pronto e seja executado bem no RDE e no ambiente de desenvolvimento da nuvem.

* Implante o código para produção por meio do pipeline de produção do Cloud Manager.

## Utilização do RDE para depurar um recurso existente {#use-rde-to-debug-an-existing-feature}

O fluxo de trabalho é semelhante ao desenvolvimento de um novo recurso. A diferença é que o código que está sendo sincronizado com o RDE refletiria o rótulo do Git do que foi enviado para o ambiente em que o problema foi encontrado. Além disso, pode ser útil implantar o conteúdo correspondente ao ambiente de upstream. Isso pode ser feito por meio da exportação e importação de pacotes de conteúdo.

## Vários desenvolvedores colaborando no mesmo RDE {#multiple-developers-collaborating-on-the-same-rde}

Um RDE suporta um único projeto por vez. Como o código é sincronizado de um ambiente de desenvolvimento local para o ambiente RDE, é mais natural que um desenvolvedor o use sozinho em um determinado momento.

No entanto, com uma coordenação cuidadosa, é possível que mais de um desenvolvedor valide um recurso específico ou depure um problema específico. A chave é que cada desenvolvedor mantém seus projetos locais sincronizados para que as alterações de código feitas por um determinado desenvolvedor sejam absorvidas pelos outros desenvolvedores, caso contrário, um desenvolvedor pode inadvertidamente substituir o código do outro. A estratégia recomendada é para cada desenvolvedor confirmar as alterações em uma ramificação Git compartilhada antes de sincronizar com o RDE, para que os outros desenvolvedores extraiam as alterações antes de fazer suas próprias alterações.

## Comandos de Ferramentas de Linha de Comando do RDE {#rde-cli-commands}

### Ajuda/Informações gerais {#help}

* Para obter uma lista de comandos, digite:

  `aio aem:rde`

* Para obter ajuda detalhada sobre um comando, digite:

  `aio aem rde <command> --help`


### Sinalizadores globais {#global-flags}

* Para uma saída menos detalhada, use o sinalizador silencioso:

  `aio aem rde <command> --quiet`

  Isso remove determinados elementos, como giradores e barras de progresso, e limita a necessidade de entrada do usuário.

* Para JSON em vez da saída de log do console, use o sinalizador json:

  `aio aem rde <command> --json`

  Isso retorna um JSON válido ao suprimir qualquer saída do console. Consulte exemplos de JSON mais abaixo.

* Para evitar a configuração das informações de conexão do RDE usando o comando de configuração ou qualquer criação de configuração de aio, use os três sinalizadores para organização, programa e ambiente:

  `aio aem rde <command> --organizationId=<value> --programId=<value> --environmentId=<value>`

  Isso ainda requer que um ```aio login``` seja executado.

### Implantação no RDE {#deploying-to-rde}

Esta seção descreve o uso da CLI do RDE para implantar, instalar ou atualizar pacotes, configurações OSGI, pacotes de conteúdo, arquivos de conteúdo individuais e configurações do Apache ou Dispatcher.

O padrão de uso geral é `aio aem:rde:install <artifact>`.

Você pode encontrar alguns exemplos abaixo:

<u>Implantando um Pacote de Conteúdo</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

A resposta para uma implantação bem-sucedida se assemelha ao seguinte:

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

Como opção, você pode fazer referência a um repositório remoto:

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

Por padrão, os artefatos são implantados nos níveis de criação e publicação, mas o sinalizador &quot;-s&quot; pode ser usado para direcionar um nível específico.

Qualquer pacote AEM pode ser implantado, como pacotes com código, conteúdo ou um [pacote de contêiner](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) (também chamado de pacote &quot;all&quot;).

>[!IMPORTANT]
>
>A configuração do Dispatcher para o projeto WKND não é implantada por meio da instalação do pacote de conteúdo acima. Implante-o separadamente seguindo as etapas &quot;Implantar uma configuração do Apache/Dispatcher&quot;.

<u>Implantando uma Configuração OSGI</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

Onde a resposta para uma implantação bem-sucedida se assemelha ao seguinte:

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>Implantando um pacote</u>

Para implantar um pacote, use:

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

Onde a resposta para uma implantação bem-sucedida se assemelha ao seguinte:

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>Implantando um Arquivo de Conteúdo</u>

Para implantar um arquivo de conteúdo, use:

`aio aem:rde:install world.txt -p /apps/hello.txt`

Onde a resposta para uma implantação bem-sucedida se assemelha ao seguinte:

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>Implantando uma Configuração Apache/Dispatcher</u>

A estrutura de pastas inteira deve estar no formato de um arquivo zip para esse tipo de configuração.

No módulo `dispatcher` de um projeto AEM, você pode compactar a configuração do Dispatcher executando o comando maven abaixo:

`mvn clean package`

Ou usando o comando zip abaixo do diretório `src` do módulo `dispatcher`:

`zip -y -r dispatcher.zip .`

Em seguida, implante a configuração com este comando:

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>O comando acima presume que você está implantando as configurações de Dispatcher do projeto [WKND](https://github.com/adobe/aem-guides-wknd). Substitua o `X.X.X` pelo número de versão do projeto WKND correspondente ou pelo número de versão específico do seu projeto ao implantar a configuração do Dispatcher do seu projeto.

>[!NOTE]
>
>O RDE é compatível com a configuração Dispatcher do &quot;modo flexível&quot;, mas não com a configuração Dispatcher do &quot;modo herdado&quot;. Consulte a [documentação do Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para obter informações sobre os dois modos. Você também pode consultar a documentação sobre [migração para o modo Flexível](/help/implementing/dispatcher/validation-debug.md#migrating), se ainda não tiver feito isso.

Uma implantação bem-sucedida gera uma resposta que se assemelha ao seguinte:

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

O código implantado no RDE não é submetido a um pipeline de Cloud Manager e seus quality gates (portais de qualidade) associados. No entanto, o código passa por alguma análise, que relata os erros, conforme ilustrado na amostra de código abaixo:

```
$ aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar
...
#19: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D74FR1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
Logs:
The analyser found the following errors for author :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
The analyser found the following errors for publish :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
```

A amostra de código acima ilustra o comportamento se um pacote não resolver. Nesse caso, ele é &quot;preparado&quot; e só será instalado se seus requisitos (nesse caso, importações ausentes) forem atendidos por meio da instalação de outro código.

### Implantação de código front-end com base em temas de site e modelos de site {#deploying-themes-to-rde}

Os RDEs oferecem suporte para código front-end com base em [temas de site](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelos de site](/help/sites-cloud/administering/site-creation/site-templates.md). Com RDEs, isso é feito usando uma diretiva de linha de comando para implantar pacotes de front-end, em vez do [pipeline de front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md) do Cloud Manager usado para outros tipos de ambiente.

Como de costume, crie seu pacote de front-end usando npm:

`npm run build`

Ela deve gerar uma pasta `dist/`, de modo que a pasta do pacote front-end deve conter um arquivo `package.json` e uma pasta `dist`:

```
ls ./path-to-frontend-pkg-folder/
...
dist
package.json
```
Agora você está pronto para implantar o pacote de front-end no RDE apontando para a pasta de pacotes de front-end:

```
aio aem:rde:install -t frontend ./path-to-frontend-pkg-folder/
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

Como alternativa, você pode compactar o arquivo `package.json` e a pasta `dist` e implantar esse arquivo zip:

`zip -r frontend-pkg.zip ./path-to-frontend-pkg-folder/dist ./path-to-frontend-pkg-folder/package.json`

```
aio aem:rde:install -t frontend frontend-pkg.zip
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

>[!NOTE]
>
>A nomenclatura dos arquivos no pacote de front-end deve seguir as seguintes convenções de nomenclatura:
> * pasta &quot;dist&quot;, para a pasta do pacote de saída npm build
> * arquivo &quot;package.json&quot;, para o pacote de dependências npm

>[!TIP]
>
> Se você criou seu RDE antes de abril de 2023 e encontrou o erro &quot;UNEXPECTED_API_ERROR&quot; ao tentar o recurso de front-end pela primeira vez, tente excluir seu ambiente e criá-lo novamente.

### Verificação do Status do RDE {#checking-rde-status}

Você pode usar a CLI do RDE para verificar se o ambiente está pronto para ser implantado para, como quais implantações foram feitas por meio do plug-in RDE.

Em execução:

`aio aem:rde:status`

Retorna o seguinte:

```
Info for cm-p12345-e987654
Environment: Ready
- Bundles Author:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Bundles Publish:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Configurations Author:
 com.adobe.granite.demo.MyServlet
- Configurations Publish:
 com.adobe.granite.demo.MyServlet
```

Se o comando retornar uma observação sobre a implantação de instâncias, ainda será possível prosseguir e executar a próxima atualização, mas a última talvez ainda não esteja visível na instância.

### Mostrar histórico de implantação {#show-deployment-history}

Você pode verificar o histórico de implantações feitas no RDE executando:

`aio aem:rde:history`

Que retorna uma resposta na forma de:

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### Excluindo do RDE {#deleting-from-rde}

Você pode excluir configurações e pacotes que foram implantados anteriormente no RDE por meio das ferramentas da CLI. Use o comando `status` para obter uma lista do que pode ser excluído, que inclui `bsn` para pacotes e `pid` para configurações a serem referenciadas no comando delete.

Por exemplo, se `com.adobe.granite.demo.MyServlet.cfg.json` foi instalado, o `bsn` é apenas `com.adobe.granite.demo.MyServlet`, sem o sufixo **cfg.json**.

Não há suporte para a exclusão de pacotes de conteúdo ou arquivos de conteúdo. Para removê-los, o RDE deve ser redefinido, o que o retorna ao estado padrão.

Consulte o exemplo abaixo para obter mais detalhes:

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

Para obter mais informações e demonstração, consulte o tutorial em vídeo [como usar comandos RDE (10:01)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html).

## Logs {#rde-logging}

Semelhante a outros tipos de ambiente, os níveis de log podem ser definidos modificando as configurações do OSGi, embora, conforme descrito acima, o modelo de implantação para RDEs envolva uma linha de comando em vez de uma implantação do Cloud Manager. Consulte a [documentação de log](/help/implementing/developing/introduction/logging.md) para obter mais informações sobre como exibir, baixar e interpretar logs.

A CLI do RDE também tem seu próprio comando de registro que pode ser usado para configurar rapidamente quais classes e pacotes devem ser registrados e em que nível de registro. Essas configurações podem ser visualizadas como efêmeras, pois não modificam as propriedades OSGI no controle de versão. Esse recurso tem como foco rastrear logs em tempo real, em vez de pesquisar logs de um passado distante.

O exemplo a seguir ilustra como rastrear a camada do autor, com um pacote definido para um nível de log de depuração e dois pacotes (separados por espaços) definidos para um nível de depuração de informações. A saída que inclui um pacote **auth** está realçada.

`aio aem:rde:logs --target=author --debug=org.apache.sling --info=org.apache.sling.commons.threads.impl org.apache.sling.jcr.resource.internal.helper.jcr -H .auth.`

>[!TIP]
>
>Se você vir o erro `RDECLI:UNEXPECTED_API_ERROR` ao reproduzir os comandos de logs do serviço de autor, redefina seu ambiente e tente novamente. Esse erro será lançado se a última operação de redefinição for anterior ao final de maio de 2024.
>
```
>aio aem:rde:reset
>```

Consulte `aio aem:rde:logs --help` para obter o conjunto completo de opções de linha de comando.

Os recursos incluem:

* declaração de níveis de log em um nível por pacote ou classe
* personalização do formato de saída de log
* reduzindo até quatro configurações de registro atuais, cada uma em seu próprio terminal
* realce de logs específicos

Observe que os registros são armazenados na memória no RDE e esses registros são reciclados e, portanto, descartados se não forem descartados ou se a rede for muito lenta.


## Redefinir {#reset-rde}

A redefinição do RDE remove todos os códigos personalizados, configurações e conteúdo das instâncias do autor e de publicação. Essa redefinição é útil, por exemplo, se o RDE tiver sido usado para testar um recurso específico e você quiser redefini-lo para um estado padrão para que você possa testar um recurso diferente.

Uma redefinição define o RDE para a versão do AEM mais recente disponível.

<!-- Alexandru: hiding for now, do not delete

Resetting can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code is deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role to use the reset feature. If not, a reset action results in an error.

### Reset the RDE by way of Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

Você pode usar o Cloud Manager para redefinir seu RDE seguindo as etapas abaixo:

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa para o qual deseja redefinir o RDE.

1. Na página **Visão Geral**, clique na guia **Ambientes** na parte superior da tela.

   ![Guia Ambientes](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * Como alternativa, clique no botão **Mostrar Tudo** no cartão **Ambientes** para ir diretamente para a guia **Ambientes**.

     ![Mostrar todas as opções](/help/implementing/cloud-manager/assets/environment-showall.png)

1. A janela **Ambientes** é aberta e lista todos os ambientes do programa.

   ![Guia Ambientes](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. Clique no botão de reticências do RDE que você deseja redefinir e selecione **Redefinir**.

   ![Exibir detalhes do ambiente](/help/implementing/cloud-manager/assets/rde-reset.png)

1. Confirme se deseja redefinir o RDE clicando em **Redefinir** na caixa de diálogo.

   ![Confirmar redefinição](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. A Cloud Manager confirma por meio de uma notificação de banner que o processo de redefinição foi iniciado.

   ![Redefinir notificação de banner](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

Depois que o processo de redefinição do RDE é iniciado, ele geralmente leva alguns minutos para ser concluído e retornar o ambiente ao seu estado padrão. O status do processo de redefinição pode ser exibido a qualquer momento na coluna **Status** do cartão **Ambientes** ou na janela **Ambientes**.

![Status de redefinição de RDE](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

Você também pode redefinir o RDE usando o botão de reticências diretamente do cartão **Ambientes** na página **Visão geral**.

![Redefinir RDE do cartão Ambientes](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Para obter mais informações sobre como usar o Cloud Manager para gerenciar seus ambientes, consulte [a documentação do Cloud Manager](/help/implementing/cloud-manager/manage-environments.md).

## Comandos que oferecem suporte à saída JSON {#json-commands}

A maioria dos comandos dá suporte ao sinalizador global ```--json``` que suprime a saída do console e retorna um json válido para ser processado em scripts. Abaixo estão alguns comandos compatíveis, com exemplos da saída json.

### Status {#status}

<details>
  <summary>Expanda para ver exemplos de status</summary>

#### Um RDE limpo {#clean-rde}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Modification in progress | Deployment in progress | Upload in progress | Ready (instances are currently deploying) | Ready",
  "author": {
    "osgiBundles": [],
    "osgiConfigs": []
  },
  "publish": {
    "osgiBundles": [],
    "osgiConfigs": []
  }
}
```

#### Um RDE com alguns pacotes instalados {#rde-installed-bundles}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "author": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  },
  "publish": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  }
}
```
</details>

### Instalar {#install}

<details>
  <summary>Expanda para ver exemplos de instalação</summary>

```$ aio aem rde install ~/Downloads/hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "4",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:30:44.578Z",
        "processed": "2024-05-21T12:31:07.886468Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```
</details>

### Excluir {#delete}

<details>
  <summary>Expanda para ver exemplos de exclusão</summary>

```$ aio aem rde delete com.adobe.granite.hotdev.demo-1.0.0.SNAPSHOT --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "84",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:16.889Z",
        "processed": "2024-05-21T11:49:18.188420Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    },
    {
      "updateId": "85",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:23.857Z",
        "processed": "2024-05-21T11:49:25.237930Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```

</details>

### Histórico {#history}

<details>
  <summary>Expanda para ver exemplos de histórico</summary>

```$ aio aem rde history --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "items": [
    {
      "updateId": "112",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:07.934Z",
        "processed": "2024-05-21T12:53:09.118766Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "111",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:00.824Z",
        "processed": "2024-05-21T12:53:02.101560Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "110",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:52:12.123Z",
        "processed": "2024-05-21T12:52:31.026147Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507"
    }
  ]
}
```
</details>

### Redefinir {#reset}

<details>
  <summary>Expanda para ver exemplos de Redefinição</summary>

#### Disparar e esquecer, Sem espera {#fire-no-wait}

```$ aio aem rde reset --no-wait --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "resetting"
}
```

#### Aguardar a Conclusão {#wait}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset"
}
```
</details>

### Reiniciar {#restart}

<details>
  <summary>Expanda para ver exemplos de Reinicialização</summary>

```$ aio aem rde restart --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "restarted"
}
```

</details>

## Modos de execução {#runmodes}

A configuração OSGI específica para RDE pode ser aplicada usando sufixos no nome da pasta, como nos exemplos abaixo:

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

Consulte a [documentação do modo de execução](/help/implementing/deploying/overview.md#runmodes) para obter informações gerais sobre modos de execução.

>[!NOTE]
>
>A configuração OSGI do RDE é exclusiva na medida em que herda os valores de qualquer propriedade OSGI declarada pelo modo de execução `dev` do pacote.

Os RDEs são distintos de outros ambientes, pois o conteúdo pode ser instalado em uma pasta install.rde (ou install.author.rde ou install.publish.rde) em /apps. Isso permite confirmar o conteúdo no Git e entregá-lo ao RDE usando a ferramenta de linha de comando.

## Preencher com conteúdo {#populating-content}

Quando um RDE é redefinido, todo o conteúdo é removido e, portanto, se desejado, uma ação explícita deve ser tomada para adicionar conteúdo. Como prática recomendada, considere montar um conjunto de conteúdo a ser usado como conteúdo de teste para validar ou depurar recursos no RDE. Há várias estratégias possíveis para preencher o RDE com esse conteúdo:

1. Sincronizar o pacote de conteúdo explicitamente no RDE usando a ferramenta de linha de comando

1. Coloque e confirme o conteúdo de amostra no Git em uma pasta install.rde em /apps e sincronize o pacote de conteúdo abrangente com o RDE usando a ferramenta de linha de comando.

1. Use a [ferramenta de cópia de conteúdo](/help/implementing/developing/tools/content-copy.md) para copiar um conjunto de conteúdo definido de ambientes de produção, preparo ou desenvolvimento, ou de outro RDE.

1. Usar gerenciador de pacotes

Você está limitado a 1 GB ao sincronizar pacotes de conteúdo.


## Em que os RDEs são diferentes dos ambientes de desenvolvimento na nuvem? {#how-are-rds-different-from-cloud-development-environments}

Embora o RDE seja, de muitas maneiras, semelhante a um ambiente de desenvolvimento em nuvem, há algumas pequenas diferenças arquitetônicas para permitir a sincronização rápida do código. O mecanismo para obter o código para o RDE é diferente — para RDEs, um sincroniza o código de um ambiente de desenvolvimento local, enquanto para Ambientes de desenvolvimento em nuvem, um implanta o código por meio do Cloud Manager.

Por esses motivos, recomenda-se que, após validar o código em um ambiente de RDE, você implante o código em um Ambiente de desenvolvimento de nuvem usando o pipeline de não produção. Por fim, teste o código antes de implantar com o pipeline de produção.

Observe também as seguintes considerações:

* Os RDEs não incluem um nível de visualização
* Atualmente, os RDEs não oferecem suporte ao canal de pré-lançamento.


## De quantos RDEs preciso? {#how-many-rds-do-i-need}

Um RDE está disponível para cada solução licenciada e o Adobe também oferece RDEs adicionais, que podem ser licenciados para programas de produção (não sandbox).

O número de RDEs necessários depende da composição e dos processos de uma organização. O modelo mais flexível é quando uma organização compra um RDE dedicado para cada um de seus desenvolvedores do AEM Cloud Service. Neste modelo, cada desenvolvedor pode testar seu código no RDE sem coordenar com outros membros da equipe sobre se um ambiente RDE está disponível.

No outro extremo, uma equipe com um único RDE pode usar processos internos para coordenar quais desenvolvedores podem usar o ambiente em um determinado momento. Possivelmente, isso acontece sempre que um desenvolvedor atinge um marco de recurso intermediário e está pronto para validar em um ambiente de nuvem, onde pode fazer rapidamente as alterações necessárias.

Um modelo intermediário é aquele em que uma organização compra vários RDEs, de modo que há uma maior probabilidade de um RDE não utilizado estar disponível. Uma estratégia poderia ser alocar um RDE por equipe de scrum ou recurso principal. Processos internos podem ser usados para coordenar o uso dos ambientes.

## Como um RDE (Rapid Development Environment, ambiente de desenvolvimento rápido) da AEM Forms Cloud Service é diferente de outros ambientes? {#how-are-forms-rds-different-from-cloud-development-environments}

Os desenvolvedores da Forms podem usar o Ambiente de desenvolvimento Cloud Service Rapid da AEM Forms para desenvolver rapidamente Forms adaptável, fluxos de trabalho e personalizações, como a personalização de componentes principais, integrações com sistemas de terceiros e muito mais. O RDE (Rapid Development Environment, ambiente de desenvolvimento rápido) da AEM Forms Cloud Service não é compatível com as APIs de comunicação. Ele também não tem suporte para recursos e funcionalidades que exigem o Documento de registro, como gerar um Documento de registro no envio de um Formulário adaptável. Os recursos do AEM Forms listados abaixo não estão disponíveis em um Ambiente de desenvolvimento rápido (RDE):

* Configuração de um documento de registro para um formulário adaptável
* Gerar um documento de registro no envio de um formulário adaptável ou com uma etapa do fluxo de trabalho
* Enviar documento de registro como um anexo com a ação enviar de email ou com a etapa Email em um fluxo de trabalho
* Uso do Adobe Sign em um formulário adaptável ou em uma etapa de fluxo de trabalho
* APIs de comunicação

>[!NOTE]
>
> Não há diferença entre a interface do usuário do RDE (Rapid Development Environment, ambiente de desenvolvimento rápido) e outros ambientes de Cloud Service para o Forms. Todas as opções relacionadas ao Documento de registro, como selecionar um documento de modelo de registro para um formulário adaptável, continuam a aparecer na interface do usuário. Esses ambientes não têm APIs de comunicação e recursos de documento de registro para testar essas opções. Assim, se você escolher qualquer opção que exija APIs de comunicação ou recursos de documento de registro, nenhuma ação será executada e uma mensagem de erro será exibida.

## Tutorial RDE

Para saber mais sobre o RDE no AEM as a Cloud Service, veja o tutorial em vídeo que demonstra [como configurá-lo, como usá-lo e o ciclo de vida do desenvolvimento (01:25)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html).

# Resolução de problemas {#troubleshooting}

## Solução de problemas de RDE (#rde-troublehooting)

### Como obter a versão mais recente do AEM para um RDE existente {#get-latest-aem-version}

Após a criação, os RDEs são definidos para a versão mais recente do Adobe Experience Manager (AEM). Uma redefinição [RDE](#reset-rde), que pode ser executada usando o Cloud Manager ou o comando `aio aem:rde:reset`, desloca o RDE e o define para a versão AEM disponível mais recentemente.

## solução de problemas do plug-in aio RDE {#aio-rde-plugin-troubleshooting}

### Erros relacionados a permissões insuficientes {#insufficient-permissions}

Para usar o plug-in RDE, é necessário que você seja membro do Perfil de Produto Cloud Manager **Developer - Cloud Service**. Consulte [Atribuir membros da equipe a perfis de produto do Cloud Manager - Atribuir o perfil de produto do desenvolvedor](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) para obter mais detalhes.

Como alternativa, você pode confirmar que tem essa função de desenvolvedor se puder fazer logon no console do desenvolvedor executando este comando:

`aio cloudmanager:environment:open-developer-console`

>[!TIP]
>
>Se você vir o erro `Warning: cloudmanager:* is not a aio command.`, instale o [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) executando o comando abaixo:
>
>```
>aio plugins:install @adobe/aio-cli-plugin-cloudmanager
>```

Verifique se o logon foi concluído com êxito executando o

`aio cloudmanager:list-programs`

Isso deve listar todos os programas na organização configurada e confirmar que você tem a função correta atribuída.
