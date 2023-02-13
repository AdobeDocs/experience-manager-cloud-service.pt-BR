---
title: Ambientes de desenvolvimento rápido
description: Saiba como aproveitar os ambientes de desenvolvimento rápido para iterações de desenvolvimento rápidas em um ambiente em nuvem.
source-git-commit: 79f58c14625ed3e7a9d684006b3abbc97334ceeb
workflow-type: tm+mt
source-wordcount: '3069'
ht-degree: 5%

---


# Ambientes de desenvolvimento rápido {#rapid-development-environments}

>[!AVAILABILITY]
>
>Esse recurso está planejado para ser implantado gradualmente nos clientes durante o mês de fevereiro.

Para implantar alterações, os ambientes atuais de desenvolvimento da Cloud exigem o uso de um processo que emprega extensas regras de qualidade e segurança de código chamadas de pipeline de CI/CD. Para situações em que são necessárias alterações rápidas e iterativas, o Adobe introduziu Ambientes de Desenvolvimento Rápido (RDEs).

Os RDEs permitem que os desenvolvedores implantem e revisem rapidamente as alterações, minimizando o tempo necessário para testar os recursos que comprovadamente funcionam em um ambiente de desenvolvimento local.

Depois que as alterações forem testadas em um RDE, elas poderão ser implantadas em um ambiente de desenvolvimento de nuvem comum por meio do pipeline do Cloud Manager.

## Introdução {#introduction}

Os RDEs podem ser usados para configurações de código, conteúdo e Apache ou Dispatcher. Ao contrário dos ambientes comuns de desenvolvimento em nuvem, os desenvolvedores podem usar as ferramentas de linha de comando locais para sincronizar o código criado localmente em um RDE.

Cada programa é provisionado com um RDE. No caso de contas de sandbox, elas hibernam após algumas horas de não uso.

Após a criação, os RDEs são definidos para a versão de AEM mais recente disponível. Uma redefinição de RDE, que pode ser executada usando o Cloud Manager, alternará o RDE e o definirá como a versão de AEM mais recente disponível.

Normalmente, um RDE seria usado por um único desenvolvedor em um determinado momento, para testar e depurar um recurso específico. Quando a sessão de desenvolvimento é concluída, o RDE pode ser redefinido em um estado padrão para o próximo uso.

Os RDEs adicionais podem ser licenciados para programas de Produção (não sandbox).

## Ativando o RDE em um programa {#enabling-rde-in-a-program}

Siga estas etapas para usar o Cloud Manager para criar um RDE para seu programa.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa ao qual deseja adicionar um RDE para exibir seus detalhes.

   * Os RDEs podem ser adicionados a [programas sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) e [programas de produção.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)

1. Na página **Visão geral do programa**, clique em **Adicionar ambiente** no cartão **Ambientes** para adicionar um ambiente.

   ![Cartão Ambientes](/help/implementing/cloud-manager/assets/no-environments.png)

   * A opção **Adicionar ambiente** também está disponível na guia **Ambientes**.

      ![Guia Ambientes](/help/implementing/cloud-manager/assets/environments-tab.png)

   * A opção **Adicionar ambiente** pode estar desativada devido à falta de permissões ou dependendo dos recursos licenciados.

1. Na caixa de diálogo **Adicionar ambiente**:

   * Selecionar **Desenvolvimento rápido** nos termos do **Selecionar tipo de ambiente** cabeçalho.
      * O número de ambientes disponíveis/usados é exibido entre parênteses atrás do tipo de ambiente.
   * Forneça uma **Nome** para o ambiente.
   * Forneça uma **Descrição** para o ambiente.
   * Selecione a **Região da nuvem**.

   ![Caixa de diálogo Adicionar ambiente](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. Clique em **Salvar** para adicionar o ambiente especificado.

A tela **Visão geral** agora exibe seu novo ambiente no cartão **Ambientes.**

Após a criação, os RDEs são definidos para a versão de AEM mais recente disponível. Uma redefinição de RDE, que também pode ser executada usando o Cloud Manager, alternará o RDE e o definirá como a versão de AEM mais recente disponível.

Para obter mais informações sobre como usar o Cloud Manager para criar ambientes, gerenciar quem tem acesso a eles e atribuir domínios personalizados, consulte [a documentação do Cloud Manager.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Instalação das ferramentas de linha de comando RDE {#installing-the-rde-command-line-tools}

Depois de adicionar um RDE ao seu programa usando o Cloud Manager, você pode interagir com ele configurando as ferramentas de linha de comando, conforme descrito nas seguintes etapas:

>[!IMPORTANT]
>
>Certifique-se de ter a versão mais recente de [Nó e NPM instalado](https://nodejs.org/en/download/) para que a CLI do Adobe I/O e os plug-ins relacionados funcionem corretamente.


1. Instale as ferramentas da CLI do Adobe I/O de acordo com o procedimento [here](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. Instale o plug-in do gerenciador de nuvem das ferramentas da CLI do Adobe I/O e configure-os conforme descrito [here](https://github.com/adobe/aio-cli-plugin-cloudmanager).
1. Instale as ferramentas da CLI do Adobe I/O AEM o plug-in RDE executando estes comandos:

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. Configure o plug-in do cloud manager para a ID da organização:

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   e substitua a sequência alfanumérica pela sua ID da organização, que pode ser pesquisada usando a estratégia [here](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. Em seguida, configure o ID do programa:

   `aio config:set cloudmanager_programid 12345`

1. Em seguida, configure o ID de ambiente ao qual o RDE será anexado:

   `aio config:set cloudmanager_environmentid 123456`

1. Quando terminar de configurar o plug-in, faça logon executando

   `aio login`

   A resposta em um logon bem-sucedido deve ser semelhante à saída abaixo, mas você pode ignorar os valores exibidos.

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

1. Verifique se o logon foi concluído com êxito ao executar

   `aio cloudmanager:list-programs`

   Isso deve listar todos os programas em sua organização configurada.

   Observe que o acima requer que você seja membro do Cloud Manager **Desenvolvedor - Cloud Service** Perfil do produto Consulte [esta página](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) para obter mais detalhes.

   Como alternativa, você pode confirmar que tem essa função de desenvolvedor se puder fazer logon no console do desenvolvedor executando este comando:

   `aio cloudmanager:environment:open-developer-console`

   >[!TIP]
   >
   >Se você vir a variável `Warning: cloudmanager:list-programs is not a aio command.` , é necessário instalar o [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) executando o comando abaixo:
   >
   >
   ```
   >aio plugins:install @adobe/aio-cli-plugin-cloudmanager
   >```


## Usar o RDE ao desenvolver um novo recurso {#using-rde-while-developing-a-new-feature}

O Adobe recomenda o seguinte workflow para desenvolver um novo recurso:

* Quando um marco intermediário é atingido e validado com êxito localmente com o SDK as a Cloud Service AEM, o código deve ser comprometido com uma ramificação de recurso Git que ainda não faz parte da linha principal, embora o compromisso com git seja opcional. O que constitui um &quot;marco intermediário&quot; varia com base nos hábitos da equipe. Os exemplos incluem algumas novas linhas de código, meio dia de trabalho ou a conclusão de um subrecurso.

* Redefina o RDE se ele tiver sido usado por outro recurso e desejar [redefini-lo para um estado padrão](#reset-rde). <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->A redefinição levará alguns minutos e todo o conteúdo e código existentes serão excluídos. Você pode usar o comando RDE status para confirmar se o RDE está pronto. O RDE retornará a versão mais recente do AEM.

   >[!IMPORTANT]
   >
   > Se os seus ambientes de armazenamento temporário e produção não estiverem recebendo atualizações automáticas de versão de AEM e estiverem muito atrás da versão mais recente da versão de AEM, lembre-se de que o código em execução no RDE pode não corresponder a como o código funcionará no armazenamento temporário e na produção. Nesse caso, é especialmente importante executar testes completos do código no armazenamento temporário antes de implantá-lo na produção.


* Usando a interface de linha de comando RDE, sincronize o código local com o RDE. As opções incluem instalar um pacote de conteúdo, um pacote específico, um arquivo de configuração OSGI, um arquivo de conteúdo e um arquivo zip de uma configuração do Apache/Dispatcher. A referência a um pacote de conteúdo remoto também é possível. Consulte a [Ferramentas de Linha de Comando RDE](#rde-cli-commands) para obter mais informações. Você pode usar o comando de status para validar que a implantação foi bem-sucedida. Como opção, use o Gerenciador de pacotes para instalar pacotes de conteúdo.

* Teste o código no RDE. Os URLs de criação e publicação estão disponíveis no Cloud Manager.

* Se o código não se comportar como esperado, use técnicas de depuração padrão para entender o problema e fazer as alterações apropriadas. Sem confirmar as modificações de código no git (já que elas não foram validadas), use a CLI local para sincronizar o código com o RDE. Continue a iterar até que o problema seja resolvido.

* Depois que o código se comportar conforme esperado, confira o código à ramificação de recursos git.

* O código sincronizado com o RDE não usa um pipeline do Cloud Manager, portanto, agora você deve usar um pipeline de não produção do Cloud Manager para implantar a ramificação de recursos do git no ambiente de desenvolvimento de nuvem. Isso valida que o código passa pelas portas de qualidade do Cloud Manager e permite que você tenha certeza de que o código será implantado com êxito posteriormente usando o pipeline de produção do Cloud Manager.

* Repita as etapas acima para cada marco intermediário até que todo o código do recurso esteja pronto e seja executado corretamente no ambiente de RDE e de desenvolvimento em nuvem.

* Implante o código para produção por meio do pipeline de produção do Cloud Manager.

## Uso do RDE para depurar um recurso existente {#use-rde-to-debug-an-existing-feature}

O fluxo de trabalho é semelhante ao desenvolvimento de um novo recurso. A diferença é que o código que está sendo sincronizado com o RDE refletiria o rótulo de git do que quer que tenha sido enviado para o ambiente onde o problema foi encontrado. Além disso, pode ser útil implantar conteúdo correspondente ao ambiente upstream. Isso pode ser feito através da exportação e importação de pacotes de conteúdo.

## Vários desenvolvedores colaborando no mesmo RDE {#multiple-developers-collaborating-on-the-same-rde}

Um RDE suporta um único projeto de cada vez. Como o código é sincronizado de um ambiente de desenvolvimento local para o ambiente RDE, é mais natural que um desenvolvedor o use sozinho em um determinado momento.

No entanto, com uma coordenação cuidadosa, é possível que mais de um desenvolvedor valide um recurso específico ou depure um problema específico. A chave é que cada desenvolvedor mantém os projetos locais sincronizados, de modo que as alterações de código feitas por um desenvolvedor específico sejam absorvidas pelos outros desenvolvedores, caso contrário, um desenvolvedor pode inadvertidamente substituir o código do outro. A estratégia recomendada é que cada desenvolvedor faça as alterações em uma ramificação git compartilhada antes de sincronizar com o RDE, para que os outros desenvolvedores façam as alterações antes de fazer suas próprias alterações.

## Comandos de Ferramentas de Linha de Comando RDE {#rde-cli-commands}

### Ajuda/Informações gerais {#help}

* Para obter uma lista de comandos, digite:

   `aio aem:rde`

* Para obter ajuda detalhada para um comando, digite:

   `aio aem rde <command> --help`

### Implantação no RDE {#deploying-to-rde}

Esta seção descreve o uso da CLI do RDE para implantar, instalar ou atualizar pacotes, configurações do OSGI, pacotes de conteúdo, arquivos de conteúdo individuais e configurações do Apache ou Dispatcher.

O padrão de uso geral é `aio aem:rde:install <artifact>`.

Você pode encontrar alguns exemplos abaixo:

<u>Implantação de um pacote de conteúdo</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

A resposta para uma implantação bem-sucedida é semelhante à seguinte:

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

Como opção, você pode fazer referência a um repositório remoto:

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

Por padrão, os artefatos são implantados em níveis de criação e publicação, mas o sinalizador &quot;-s&quot; pode ser usado para direcionar uma camada específica.

>[!IMPORTANT]
>
>A configuração do dispatcher para o projeto WKND não é implantada por meio da instalação do pacote de conteúdo acima. Você precisará implantá-lo separadamente seguindo as etapas de &quot;Implantação de uma configuração do Apache/Dispatcher&quot;.

<u>Implantação de uma configuração OSGI</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

em que a resposta para uma implantação bem-sucedida se assemelha ao seguinte:

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>Implantação de um pacote</u>

Para implantar um pacote, use:

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

em que a resposta para uma implantação bem-sucedida se assemelha ao seguinte:

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>Implantar um arquivo de conteúdo</u>

Para implantar um arquivo de conteúdo, use:

`aio aem:rde:install world.txt -p /apps/hello.txt`

em que a resposta para uma implantação bem-sucedida se assemelha ao seguinte:

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>Implantação de uma configuração do Apache/Dispatcher</u>

Toda a estrutura de pastas precisa estar no formato de um arquivo zip para esse tipo de configuração. Você pode compactá-lo executando esse comando da raiz de uma pasta de configuração do dispatcher:

`zip -y -r dispatcher.zip`

em seguida, implante a configuração através deste comando:

`aio aem:rde:install -t dispatcher-config dispatcher-wknd-2.1.0.zip`

Uma implantação bem-sucedida gerará uma resposta semelhante ao seguinte:

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

O código implantado no RDE não passa por um pipeline do Cloud Manager e suas portas de qualidade associadas, no entanto, o código passa por alguma análise, que relatará os erros, conforme ilustrado na amostra de código abaixo:

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

A amostra de código acima ilustra o comportamento se um pacote não for resolvido, nesse caso ele será &quot;preparado&quot; e só será instalado se seus requisitos (importações ausentes, neste caso) forem cumpridos por meio da instalação de outro código.

### Verificando o status do RDE {#checking-rde-status}

Você pode usar a CLI do RDE para verificar se o ambiente está pronto para ser implantado, pois quais implantações foram feitas por meio do plug-in do RDE.

Em execução:

`aio aem:rde:status`

retornará:

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

Se o comando retornar uma observação sobre a implantação de instâncias, você ainda poderá prosseguir e executar a próxima atualização, mas a última poderá não estar visível na instância.

### Mostrar Histórico de Implantação {#show-deployment-history}

Você pode verificar o histórico de implantações feitas no RDE executando:

`aio aem:rde:history`

que retorna uma resposta na forma de:

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### Excluindo do RDE {#deleting-from-rde}

Você pode excluir configurações e pacotes que foram implantados anteriormente no RDE por meio das ferramentas da CLI. Use o `status` para obter uma lista do que pode ser excluído, que inclui o `bsn` para pacotes e `pid` para configurações fazer referência no comando delete.

Por exemplo, se `com.adobe.granite.demo.MyServlet.cfg.json` foi instalado, a variável `bsn` é justo `com.adobe.granite.demo.MyServlet`sem a **cfg.json** sufixo.

Não há suporte para exclusão de pacotes de conteúdo ou arquivos de conteúdo. Para removê-los, o RDE deve ser redefinido, o que o retornará ao estado padrão.

Consulte o exemplo abaixo para obter mais detalhes:

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

## Redefinir {#reset-rde}

Redefinir o RDE remove todos os códigos, configurações e conteúdos personalizados das instâncias de autor e de publicação. Isso pode ser útil, por exemplo, se o RDE tiver sido usado para testar um recurso específico e você quiser redefini-lo para um estado padrão para testar um recurso diferente.

Uma redefinição definirá o RDE para a versão de AEM mais recente disponível.

<!-- Alexandru: hiding for now, please don't delete

Resetting can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code will be deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role in order to be able to use the reset feature. If not, a reset action will result in an error.

### Reset the RDE via Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

Você pode usar o Cloud Manager para redefinir seu RDE seguindo as etapas abaixo:

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa para o qual deseja redefinir o RDE.

1. Na página **Visão geral**, clique na guia **Ambientes** na parte superior da tela.

   ![Guia Ambientes](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * Como alternativa, clique no botão **Mostrar tudo** no cartão **Ambientes** para ir diretamente para a guia **Ambientes**.

      ![Mostrar todas as opções](/help/implementing/cloud-manager/assets/environment-showall.png)

1. O **Ambientes** abre e lista todos os ambientes do programa.

   ![Guia Ambientes](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. Clique no botão de redefinição do RDE que deseja redefinir e selecione **Redefinir**.

   ![Exibir detalhes do ambiente](/help/implementing/cloud-manager/assets/rde-reset.png)

1. Confirme se deseja redefinir o RDE clicando em **Redefinir** na caixa de diálogo.

   ![Confirmar redefinição](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. O Cloud Manager confirma por meio de uma notificação de banner que o processo de redefinição foi iniciado.

   ![Redefinir notificação do banner](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

Depois que o processo de redefinição de RDE é iniciado, ele geralmente leva alguns minutos para concluir e retornar o ambiente ao seu estado padrão. O status do processo de redefinição pode ser visualizado a qualquer momento no **Status** da coluna **Ambientes** ou na **Ambientes** janela.

![Status de redefinição RDE](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

Também é possível redefinir o RDE usando o botão de reticências diretamente do **Ambientes** no cartão **Visão geral** página.

![Redefinir RDE do cartão Ambientes](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Para obter mais informações sobre como usar o Cloud Manager para gerenciar seus ambientes, consulte [a documentação do Cloud Manager.](/help/implementing/cloud-manager/manage-environments.md)

## Modos de execução {#runmodes}

A configuração OSGI específica do RDE pode ser aplicada usando sufixos no nome da pasta, como nos exemplos abaixo:

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

Consulte a [documentação do runmode](/help/implementing/deploying/overview.md#runmodes) para obter informações gerais sobre modos de execução.

>[!NOTE]
>
>A configuração OSGI do RDE é exclusiva, pois herda os valores de quaisquer propriedades OSGI declaradas pelo pacote `dev` modo de execução.

Os RDEs são diferentes de outros ambientes no que o conteúdo pode ser instalado em uma pasta install.rde (ou install.author.rde ou install.publish.rde) em /apps. Isso permite confirmar o conteúdo para git e entregá-lo ao RDE usando a ferramenta de linha de comando.

## Preenchimento com conteúdo {#populating-content}

Quando um RDE é redefinido, todo o conteúdo é removido e, portanto, se desejado, uma ação explícita deve ser tomada para adicionar conteúdo. Como prática recomendada, considere reunir um conjunto de conteúdo a ser usado como conteúdo de teste para validar ou depurar recursos no RDE. Há várias estratégias possíveis para preencher o RDE com esse conteúdo:

1. Sincronize o pacote de conteúdo explicitamente com o RDE usando a ferramenta de linha de comando

1. Coloque e confirme o conteúdo de amostra no git dentro de uma pasta install.rde em /apps e sincronize o pacote de conteúdo abrangente com o RDE usando a ferramenta de linha de comando.

1. Usar o Gerenciador de Pacotes

Observe que você está limitado a 1 GB ao sincronizar pacotes de conteúdo.

## Logs {#logging}

Os níveis de log podem ser definidos modificando as configurações do OSGi. Verifique a [documentação](/help/implementing/developing/introduction/logging.md) para obter mais informações.

## Como os RDEs são diferentes dos ambientes de desenvolvimento de nuvem? {#how-are-rds-different-from-cloud-development-environments}

Embora o RDE seja, de muitas formas, semelhante a um Ambiente de desenvolvimento de nuvem, há algumas pequenas diferenças de arquitetura para permitir a sincronização rápida do código. O mecanismo para obter o código para o RDE é diferente — para RDEs, um sincroniza o código de um ambiente de desenvolvimento local, enquanto para Ambientes de desenvolvimento de nuvem, um implanta o código pelo Cloud Manager.

Por esses motivos, é recomendável que, depois de validar o código em um ambiente RDE, você implante o código em um Ambiente de desenvolvimento de nuvem usando o pipeline de não produção. Por fim, teste o código antes de implantar com o pipeline de produção.

Observe também as seguintes considerações:

* Os RDEs não incluem um nível de visualização
* No momento, os RDEs não suportam a visualização e a depuração do código front-end implantado usando o Pipeline de front-end do Cloud Manager.
* No momento, os RDEs não são compatíveis com o canal de pré-lançamento.


## Quantos RDEs eu preciso? {#how-many-rds-do-i-need}

Um RDE está disponível para cada solução licenciada e o Adobe também oferece RDEs adicionais, que podem ser licenciados para programas de produção (não sandbox).

O número de RDEs necessários depende da composição e dos processos de uma organização. O modelo mais flexível é o local em que uma organização compra um RDE dedicado para cada um de seus desenvolvedores de AEM Cloud Service. Neste modelo, cada desenvolvedor pode testar seu código no RDE sem coordenar com outros membros da equipe sobre se um ambiente RDE está disponível.

No outro extremo, uma equipe com um único RDE pode usar processos internos para coordenar qual desenvolvedor pode usar o ambiente em um determinado momento. Isso pode ser possível sempre que um desenvolvedor atingir um marco de recurso intermediário e estiver pronto para validar em um ambiente do Cloud, onde poderá fazer rapidamente as alterações necessárias.

Um modelo intermediário é aquele em que uma organização compra vários RDEs para que haja uma maior probabilidade de um RDE não utilizado estar disponível. Uma estratégia poderia ser alocar um RDE por equipe de arranhão ou recurso principal. Processos internos podem ser usados para coordenar o uso dos ambientes.

## Como um RDE (AEM Forms Cloud Service Rapid Development Environment, ambiente de desenvolvimento rápido) é diferente de outros ambientes? {#how-are-forms-rds-different-from-cloud-development-environments}

Os desenvolvedores do Forms podem usar o Ambiente de desenvolvimento do AEM Forms Cloud Service Rapid para desenvolver rapidamente o Forms adaptável, fluxos de trabalho e personalizações, como personalizar componentes principais, integrações com sistemas de terceiros e muito mais. O AEM Forms Cloud Service Rapid Development Environment (RDE) não tem suporte para APIs de comunicação e para recursos e recursos que exigem Documento de registro, como gerar um Documento de registro no envio de um formulário adaptável. Os recursos listados abaixo do AEM Forms não estão disponíveis em um RDE (Rapid Development Environment, ambiente de desenvolvimento rápido):

* Configurar um documento de registro para um formulário adaptável
* Gerar um documento de registro no envio de um formulário adaptável ou com uma etapa de fluxo de trabalho
* Enviar documento de registro como anexo com a ação Enviar por email ou com a etapa Enviar por email em um fluxo de trabalho
* Uso do Adobe Sign em um formulário adaptável ou em uma etapa do fluxo de trabalho
* APIs de comunicação

>[!NOTE]
>
> Não há alteração entre a interface do usuário do Rapid Development Environment (RDE) e outros ambientes do Cloud Service para o Forms. Todas as opções relacionadas ao Documento de registro, como selecionar um documento de modelo de registro para um formulário adaptável, continuam a aparecer na interface do usuário. Esses ambientes não têm APIs de comunicação e recursos de Documento de registro para testar essas opções. Portanto, ao escolher qualquer opção que exija APIs de comunicação ou recursos de Documento de registro, nenhuma ação será executada e uma mensagem de erro será exibida ou retornada.

