---
title: Implantação no AEM como um serviço em nuvem
description: 'Implantação no AEM como um serviço em nuvem '
translation-type: tm+mt
source-git-commit: de23de0b79e6b897a69bd18035d2e7fcd07104c5

---


# Implantação no AEM como um serviço em nuvem {#deploying-to-aem-as-a-cloud-service}

## Introdução {#introduction}

Os fundamentos do desenvolvimento de código são semelhantes no AEM como um serviço em nuvem em comparação com as soluções do AEM On Premise e Managed Services. Os desenvolvedores gravam o código e o testam localmente, que é então enviado para o AEM remoto como um ambiente de serviço em nuvem. O Cloud Manager, que era uma ferramenta opcional de entrega de conteúdo para Serviços gerenciados, é necessário. Agora, esse é o único mecanismo para implantar o código no AEM como ambientes de serviço em nuvem.

A atualização da versão do AEM é sempre um evento de implantação separado do código personalizado. De outra forma, as versões de código personalizadas devem ser testadas em relação à versão do AEM que está em produção, já que isso é o que será implantado no início. As atualizações de versão do AEM que ocorrem depois disso, que serão frequentes quando comparadas aos Serviços gerenciados hoje, são aplicadas automaticamente. Eles são compatíveis com o código do cliente já implantado.

O restante deste documento descreverá como os desenvolvedores devem adaptar suas práticas para que trabalhem com o AEM como atualizações de versão e atualizações de clientes de um serviço em nuvem.

>[!NOTE]
>Recomenda-se que os clientes com bases de código existentes passem pelo exercício de reestruturação do repositório descrito na documentação [do](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)AEM.


## Atualizações de versão do AEM {#version-updates}

É importante entender que o AEM será atualizado com frequência, com a mesma frequência que uma vez por dia, e se concentrará em correções de erros e melhorias de desempenho. A atualização ocorrerá de forma transparente e sem causar tempo de inatividade. A atualização foi projetada para ser compatível com versões anteriores, o que significa que você não precisa modificar o código personalizado. Na verdade, as atualizações do AEM são eventos independentes das implantações de código do cliente. A atualização do AEM é implantada em cima do último push de código bem-sucedido, o que implica que quaisquer alterações confirmadas desde o último push para produção não serão implantadas.

>[!NOTE]
>
> Se o código personalizado foi enviado para o armazenamento temporário e depois rejeitado por você, a próxima atualização do AEM removerá essas alterações para refletir a tag git da última versão do cliente bem-sucedida para a produção.

Em uma frequência regular, uma versão de recurso ocorrerá, com foco em adições de recursos e aprimoramentos que afetarão mais substancialmente a experiência do usuário em comparação às versões diárias. Uma versão de recurso é acionada não pela implantação de um grande conjunto de alterações, mas pelo giro de uma alternância de versão, ativando o código que vem se acumulando ao longo de dias ou semanas pelas atualizações diárias.

Os controlos de saúde são utilizados para monitorizar a saúde da aplicação. Se essas verificações falharem durante uma atualização do AEM como um serviço em nuvem, a versão não prosseguirá para esse ambiente e a Adobe investigará por que a atualização causou esse comportamento inesperado.

### Armazenamento de nós composto {#composite-node-store}

Como mencionado acima, as atualizações na maioria dos casos resultarão em tempo de inatividade zero, inclusive para o autor, que é um cluster de nós. Atualizações contínuas são possíveis devido ao recurso &quot;armazenamento de nó composto&quot; no Oak. Esse recurso permite que o AEM faça referência a vários repositórios simultaneamente. Em uma implantação contínua, a nova versão verde do AEM contém seu próprio repositório (o repositório executável baseado no TarMK), distinto da versão antiga do Azul AEM, embora ambos façam referência a um repositório mutável baseado no DocumentMK compartilhado que contém áreas como `/libs` , `/content`e outras `/conf``/etc` . Como o Azul e o Verde têm suas próprias versões do `/libs`, ambos podem estar ativos durante a atualização do acumulado, ambos assumindo o tráfego até que o azul seja totalmente substituído pelo verde.

## Versões do cliente {#customer-releases}

### Codificação na versão correta do AEM {#coding-against-the-right-aem-version}

Para as soluções AEM anteriores, a versão mais recente do AEM foi alterada com pouca frequência (aproximadamente uma vez por ano com service packs trimestrais) e os clientes atualizariam as instâncias de produção para o início rápido mais recente em seu próprio tempo, referenciando o API Jar. No entanto, os aplicativos AEM como serviço de nuvem são atualizados automaticamente para a versão mais recente do AEM com mais frequência, de modo que o código personalizado para versões internas deve ser criado em relação a essas novas interfaces do AEM.

Assim como para versões AEM não-em nuvem existentes, um desenvolvimento local e offline baseado em um início rápido específico será suportado e deverá ser a ferramenta preferida para depuração na maioria dos casos.

> [!OBSERVAÇÃO}
>Há diferenças operacionais sutis entre o comportamento do aplicativo em uma máquina local e a Adobe Cloud. Essas diferenças arquitetônicas devem ser respeitadas durante o desenvolvimento local e podem levar a um comportamento diferente ao implantar na infraestrutura de nuvem. Devido a essas diferenças, é importante executar testes exaustivos em ambientes de desenvolvimento e estágio antes de implantar o novo código personalizado na produção.

Abaixo está o processo para um desenvolvedor acessar a versão relevante dos artefatos AEM, que chamaremos de AEM como um SDK de serviço em nuvem, necessário para desenvolver código personalizado para uma versão interna. As informações sobre o dispatcher podem ser encontradas [nesta página](/help/implementing/dispatcher/overview.md).

## O AEM como um SDK do serviço em nuvem {#aem-as-a-cloud-service-sdk}

O AEM como um SDK de serviço em nuvem é composto pelos seguintes artefatos:

* **Jar** de início rápido - O tempo de execução do AEM usado para desenvolvimento local
* **Java API Jar** - a Dependência Java Jar/Maven que expõe todas as APIs Java permitidas que podem ser usadas para desenvolvimento em relação ao AEM como serviço de nuvem. Anteriormente conhecido como Uberjar
* **Jar** Javadoc - O javadocs para o Java API Jar
* **Ferramentas** do Dispatcher - o conjunto de ferramentas usado para desenvolver no Dispatcher localmente. Separe artefatos para unix e janelas

Além disso, alguns clientes que foram implantados anteriormente com o AEM 6.5 ou versões anteriores usarão os artefatos abaixo. Se a compilação local não estiver funcionando com o jar do Quickstart e você suspeitar que isso seja devido a interfaces que foram removidas do AEM implantadas como um serviço em nuvem, entre em contato com o Suporte ao cliente para determinar se você precisa de acesso. Isso exigirá alterações no backend.

* **6.5 Java API Jar** obsoleto - um conjunto adicional de interfaces que foram removidas desde o AEM 6.5
* **6.5 Javadoc Jar** obsoleto - os Javadocs para o conjunto adicional de interfaces

## Acessar o AEM como um SDK de serviço em nuvem {#accessing-the-aem-as-a-cloud-service-sdk}

* Você pode verificar o ícone **Sobre o Adobe Experience Manager** do Admin Console do AEM para descobrir a versão do AEM que você está executando na produção.
* As Ferramentas QuickStart jar e Dispatcher podem ser baixadas como um arquivo zip do portal [de Distribuição de](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)software. Observe que o acesso às listagens do SDK é limitado àquelas com os serviços gerenciados do AEM ou o AEM como ambientes de serviço em nuvem.
* O Java API Jar e o Javadoc Jar podem ser baixados por meio da ferramenta maven, linha de comando ou com seu IDE preferencial.
* Os poms do projeto maven devem fazer referência ao seguinte pacote de API Jar. Essa dependência também deve ser referenciada em quaisquer salas de subpacotes.

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version> 
  <scope>provided</scope>
</dependency>
```

> [!NOTE] A entrada da versão do SDK deve corresponder à versão do AEM como um serviço em nuvem. Você pode ver qual versão está usando fazendo logon no AEM, indo para o ponto de interrogação no canto superior direito da tela e selecionando **[!UICONTROL Sobre o Adobe Experience Manager]**

* A coordenada remota para o repositório maven onde o pacote está hospedado deve ser incluída no arquivo pom.

```
<repository>
    <id>adobe-aem-releases</id>
    <name>Adobe AEM Repository</name>
    <url>https://downloads.experiencecloud.adobe.com/content/maven/public</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

## Atualização de um projeto local com uma nova versão do SDK {#refreshing-a-local-prokect-with-a-new-skd-version}

Quando é recomendado atualizar o projeto local com um novo SDK?

É *recomendável* atualizá-la pelo menos após uma versão de manutenção mensal.

É *opcional* atualizá-lo após qualquer versão de manutenção diária. Os clientes serão informados quando sua instância de produção for atualizada com êxito para uma nova versão do AEM. Para as versões de manutenção diárias, não é de se esperar que o novo SDK tenha mudado significativamente, se é que isso aconteceu. Mesmo assim, é recomendável atualizar ocasionalmente o ambiente local de desenvolvedor do AEM com o SDK mais recente, em seguida, recriar e testar o aplicativo personalizado. A versão de manutenção mensal normalmente inclui alterações mais impactantes e, portanto, os desenvolvedores devem atualizar, reconstruir e testar imediatamente.

Abaixo está o procedimento recomendado para atualizar um ambiente local:

1. Certifique-se de que qualquer conteúdo útil seja enviado para o projeto no controle de origem ou esteja disponível em um pacote de conteúdo mutável para importação posterior
1. O conteúdo do teste de desenvolvimento local precisa ser armazenado separadamente para que não seja implantado como parte da compilação do pipeline do Gerenciador de nuvem. Isso porque só precisa ser usado para o desenvolvimento local
1. Parar o início rápido atualmente em execução
1. Mova a `crx-quickstart` pasta para outra pasta para manter a segurança
1. Observe a nova versão do AEM, que é anotada no Gerenciador de nuvem (isso será usado para identificar a nova versão do QuickStart Jar para fazer download posteriormente)
1. Baixe o JAR QuickStart cuja versão corresponda à versão do Production AEM do Portal de distribuição de software
1. Crie uma nova pasta e insira o novo QuickStart Jar dentro
1. Inicie o novo QuickStart com os modos de execução desejados (renomeando o arquivo ou transmitindo os modos de execução via `-r`).
   * Certifique-se de que não há vestígios do arranque rápido antigo na pasta.
1. Criar seu aplicativo AEM
1. Implantar seu aplicativo AEM no AEM local via PackageManager
1. Instale todos os pacotes de conteúdo mutável necessários para testes de ambiente local via PackageManager
1. Continuar o desenvolvimento e implantar as alterações conforme necessário

Se houver conteúdo que deva ser instalado com cada nova versão de início rápido do AEM, inclua-o em um pacote de conteúdo e no controle de origem do projeto. Em seguida, instale-o sempre.

A recomendação é atualizar o SDK frequentemente (por exemplo, bisemanalmente) e descartar o estado local completo diariamente para não depender acidentalmente dos dados de estado no aplicativo.

Caso você dependa do CryptoSupport ([pela configuração das credenciais do Cloudservices ou do serviço de Email SMTP no AEM ou pelo uso da API CryptoSupport no aplicativo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), as propriedades criptografadas serão criptografadas por uma chave gerada automaticamente na primeira inicialização de um ambiente AEM. Enquanto a configuração de nuvem cuida da reutilização automática da CryptoKey específica do ambiente, é necessário injetar a chave de criptografia no ambiente de desenvolvimento local.

Por padrão, o AEM está configurado para armazenar os dados principais na pasta de dados de uma pasta, mas para facilitar a reutilização no desenvolvimento, o processo do AEM pode ser inicializado na primeira inicialização com &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Isso gerará os dados de criptografia em &quot;`/etc/key`&quot;.

Para poder reutilizar pacotes de conteúdo contendo os valores criptografados, siga estas etapas:

* Ao iniciar o quickstart.jar local, adicione o parâmetro abaixo: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. É recomendado, mas opcional, sempre adicioná-lo.
* A primeira vez que você iniciou uma instância cria um pacote que contém um filtro para a raiz &quot;`/etc/key`&quot;. Isso manterá o segredo a ser reutilizado em todos os ambientes para os quais você deseja que eles sejam reutilizados
* Exporte qualquer conteúdo silencioso que contenha segredos ou procure os valores criptografados por meio `/crx/de` do para adicioná-lo ao pacote que será reutilizado em instalações
* Sempre que você gira uma nova instância (para substituir por uma nova versão ou como vários ambientes dev devem compartilhar as credenciais para teste), instale o pacote produzido nas etapas 2 e 3 para poder reutilizar o conteúdo sem a necessidade de reconfigurar manualmente. Isso porque agora a chave de criptografia está sincronizada.

## Implantação de pacotes de conteúdo por meio do Cloud Manager e do Package Manager {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Implantações por meio do Cloud Manager {#deployments-via-cloud-manager}

Os clientes implantam código personalizado em ambientes de nuvem por meio do Cloud Manager. Observe que o Cloud Manager transforma os pacotes de conteúdo montados localmente em um artefato que está em conformidade com o Modelo de recurso Sling, que é a forma como um AEM como um aplicativo do serviço de nuvem é descrito durante a execução em um ambiente de nuvem. Como resultado, ao analisar os pacotes no Package Manager em ambientes Cloud, o nome incluirá &quot;cp2fm&quot; e os pacotes transformados terão todos os metadados removidos. Eles não podem ser interagidos, o que significa que não podem ser baixados, replicados ou abertos. A documentação detalhada sobre o conversor pode ser [encontrada aqui](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

Os pacotes de conteúdo gravados para o AEM como aplicativos do Cloud Service devem ter uma separação clara entre conteúdo imutável e mutável e o Cloud Manager a imporá com falha na criação, resultando em uma mensagem como:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

O resto desta seção descreve a composição e as implicações dos pacotes imutáveis e silenciosos.

### Pacotes de conteúdo imutáveis {#immutabe-content-packages}

Todo o conteúdo e código persistente no repositório imutável devem ser verificados no git e implantados pelo Cloud Manager. Em outras palavras, ao contrário das soluções AEM atuais, o código nunca é implantado diretamente em uma instância do AEM em execução. Isso garante que o código executado para uma determinada versão em qualquer ambiente da Cloud seja idêntico, o que elimina o risco de variação não intencional do código na produção. Por exemplo, a configuração do OSGI deve ser comprometida com o controle de origem em vez de gerenciada no tempo de execução por meio do gerenciador de configuração do console da Web do AEM.

À medida que as alterações do aplicativo devido ao padrão de implantação Blue-Green são ativadas por um switch, elas não podem depender de alterações no repositório mutável, com exceção dos usuários do serviço, de suas ACLs, tipos de nó e alterações na definição do índice.

Para os clientes com bases de código existentes, é essencial passar pelo exercício de reestruturação do repositório descrito na documentação do AEM para garantir que o conteúdo anteriormente sob o /etc seja movido para o local correto.

## Configuração do OSGI {#osgi-configuration}

Como mencionado acima, a configuração do OSGI deve ser comprometida com o controle de origem em vez do console da Web. As técnicas para o fazer incluem:

* Fazer as alterações necessárias no ambiente AEM local do desenvolvedor com o gerenciador de configuração do console da Web do AEM e, em seguida, exportar os resultados para o projeto do AEM no sistema de arquivos local
* Criar a configuração do OSGI manualmente no projeto do AEM no sistema de arquivos local, a referência ao gerenciador de configuração do console do AEM para os nomes das propriedades.

## Conteúdo variável {#mutable-content}

Em alguns casos, pode ser útil preparar alterações de conteúdo no controle de origem para que ele possa ser implantado pelo Gerenciador de nuvem sempre que um ambiente for atualizado. Por exemplo, pode ser razoável implantar determinadas estruturas de pastas raiz ou alinhar alterações em modelos editáveis para ativar políticas nesses componentes que foram atualizados pela implantação do aplicativo.

Há duas estratégias para descrever o conteúdo que será implantado pelo Cloud Manager no repositório mutável, pacotes de conteúdo mutável e declarações de redirecionamento.

### Pacotes de conteúdo variável {#mutable-content-packages}

Conteúdo como hierarquias de caminho de pasta, usuários de serviço e controles de acesso (ACLs) são normalmente comprometidos em um projeto AEM baseado em arquétipo de pasta. As técnicas incluem exportar do AEM ou gravar diretamente como XML. Durante o processo de criação e implantação, o Cloud Manager agrupa o pacote de conteúdo mutável resultante. O conteúdo mutável é instalado em 3 momentos diferentes durante a fase de implantação no pipeline:

Antes da inicialização da nova versão do aplicativo:

* definições de índice (adicionar, modificar, remover)

Durante a inicialização da nova versão do aplicativo, mas antes da mudança:

* Usuários do serviço (adicionar)
* ACLs do usuário do serviço (adicionar)
* tipos de nó (adicionar)

Após alternar para a nova versão do aplicativo:

* Todos os outros conteúdos definíveis através do cofre do Jackrabbit. Por exemplo:
   * Pastas (adicionar, modificar, remover)
   * Modelos editáveis (adicionar, modificar, remover)
   * Configuração sensível ao contexto (qualquer item em `/conf`) (adicionar, modificar, remover)
   * Scripts (os pacotes podem acionar os ganchos de instalação em vários estágios do processo de instalação do pacote)

É possível limitar a instalação de conteúdo mutável para criar ou publicar incorporando pacotes em uma pasta install.author ou install.publish em `/apps`. Detalhes a serem encontrados na documentação [do](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/restructuring/repository-restructuring.html) AEM sobre a reestruturação recomendada do projeto.

>[!NOTE] Os pacotes de conteúdo são implantados em todos os tipos de ambiente (dev, stage, prod). Não é possível limitar a implantação a um ambiente específico. Essa limitação está em vigor para garantir a opção de uma execução de teste de execução automatizada. O conteúdo específico a um ambiente requer instalação manual por meio do Package Manager.

Além disso, não há um mecanismo para reverter as alterações no pacote de conteúdo mutável depois que elas forem aplicadas. Se os clientes detectarem um problema, poderão optar por corrigi-lo na próxima versão do código ou como último recurso, restaurar o sistema inteiro para um ponto no tempo antes da implantação.

Todos os pacotes de terceiros incluídos devem ser validados como AEM como um serviço de nuvem compatível, caso contrário, sua inclusão resultará em uma falha de implantação.

Como mencionado acima, os clientes com bases de código existentes devem estar em conformidade com o exercício de reestruturação do repositório descrito na documentação [do](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)AEM.

## Reapontar {#repoinit}

Para os seguintes casos, é preferível seguir a abordagem de codificação manual de `repoinit` declarações de criação de conteúdo explícito em configurações de fábrica OSGI:

* Criar/excluir/desativar usuários do serviço
* Criar/excluir grupos
* Criar/excluir usuários
* Adicionar ACLs
   > [!NOTE] A definição de ACLs exige que as estruturas de nó já estejam presentes. Portanto, as declarações de criação de caminho anteriores podem ser necessárias.
* Adicionar caminho (por exemplo, para estruturas de pastas raiz)
* Adicionar CNDs (definições de tipo de nó)

É preferível reapontar para esses casos de uso de modificação de conteúdo suportado devido aos seguintes benefícios:

* A opção de realocação cria recursos na inicialização para que a lógica possa tomar a existência desses recursos como adquiridos. Na abordagem do pacote de conteúdo mutável, os recursos são criados após a inicialização, portanto, o código do aplicativo que depende deles pode falhar.
* O realocamento é um conjunto de instruções relativamente seguro, já que você controla explicitamente a ação a ser tomada. Além disso, as únicas operações suportadas são aditivas, com exceção de alguns casos relacionados à segurança, que permitem a remoção de Usuários, Usuários do serviço e Grupos. Pelo contrário, a eliminação de algo na abordagem do pacote de conteúdos mutáveis é explícita;  conforme você define um filtro, qualquer item presente coberto por um filtro será excluído. Ainda assim, deve-se ter cuidado, pois com qualquer conteúdo há cenários nos quais a presença de novo conteúdo pode alterar o comportamento do aplicativo.
* Repontar realiza operações rápidas e atômicas. Em contraste, os pacotes de conteúdo variável podem depender muito do desempenho das estruturas cobertas por um filtro. Mesmo se você atualizar um único nó, um instantâneo de uma árvore grande pode ser criado.
* É possível validar instruções repoinit em um ambiente dev local em tempo de execução, pois elas serão executadas quando a configuração OSGi for registrada.
* As declarações de redirecionamento são atômicas e explícitas e ignorarão se o estado já corresponde.

Quando o Cloud Manager implanta o aplicativo, ele executa essas instruções, independentemente da instalação de qualquer pacote de conteúdo.

Para criar declarações de recondução, siga o procedimento abaixo:

1. Adicionar configuração OSGi para PID `org.apache.sling.jcr.repoinit.RepositoryInitializer` em uma pasta de configuração do projeto
1. Adicione instruções repoinit à propriedade script da configuração. A sintaxe e as opções estão documentadas na documentação [do](https://sling.apache.org/documentation/bundles/repository-initialization.html)Sling. Observe que deve haver uma criação explícita de uma pasta pai antes de suas pastas filhas. Por exemplo, uma criação explícita de `/content` before `/content/myfolder`, before `/content/myfolder/mysubfolder`. Para ACLs sendo definidas em estruturas de nível baixo, é recomendável definir essas em um nível superior e trabalhar com uma `rep:glob` restrição.  Por exemplo `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Valide no ambiente dev local em tempo de execução.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>Para ACLs definidas para nós abaixo `/apps` ou `/libs` a execução de redirecionamento será iniciada em um repositório em branco. Os pacotes são instalados após o redirecionamento, de modo que as instruções não podem depender de nada definido nos pacotes, mas devem definir as condições prévias como as estruturas pai abaixo.

>[!TIP]
>
>Para ACLs, a criação de estruturas profundas pode ser complicada, portanto, é mais razoável definir uma ACL em um nível mais alto e restringir o local onde ela deve agir por meio de uma restrição rep:glul.

Para obter mais detalhes sobre a recomendação, consulte a documentação do [Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Gerenciador de pacotes &quot;one-offs&quot; para pacotes de conteúdo variável {#package-manager-oneoffs-for-mutable-content-packages}

Há casos de uso em que um pacote de conteúdo deve ser instalado como um &quot;one off&quot;. Por exemplo, importar conteúdo específico da produção para o armazenamento temporário para depurar um problema de produção. Para esses cenários, o Gerenciador de pacotes pode ser usado no AEM como ambientes de serviço em nuvem.

Como o Package Manager é um conceito de tempo de execução, não é possível instalar conteúdo ou código no repositório imutável, portanto, esses pacotes de conteúdo devem consistir apenas em conteúdo mutável (principalmente `/content` ou `/conf`). Se o pacote de conteúdo incluir conteúdo misto (conteúdo mutável e imutável), somente o conteúdo mutável será instalado.

Todos os pacotes de conteúdo instalados pelo Cloud Manager (mutáveis e imutáveis) serão exibidos em um estado congelado na interface do usuário do AEM Package Manager. Esses pacotes não podem ser reinstalados, recriados ou mesmo baixados e serão listados com um sufixo **&quot;cp2fm&quot;** , indicando que sua instalação foi gerenciada pelo Cloud Manager.

### Incluindo pacotes de terceiros {#including-third-party}

É comum que os clientes incluam pacotes pré-criados de fontes terceirizadas, como fornecedores de software, como os parceiros de tradução da Adobe. A recomendação é hospedar esses pacotes em um repositório remoto e referenciá-los no `pom.xml`. Isso só é possível para repositórios públicos.

Se o armazenamento do pacote em um repositório remoto não for possível, os clientes poderão colocar em um repositório Maven local baseado em sistema de arquivos, que é enviado para SCM como parte do projeto e referenciado pelo que depender dele. O repositório seria declarado nos exemplos de projeto a seguir:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Todos os pacotes de terceiros incluídos devem estar em conformidade com o AEM como uma codificação do serviço de nuvem e diretrizes de empacotamento descritas neste artigo. Caso contrário, sua inclusão resultará em uma falha de implantação.

O trecho Maven POM XML a seguir mostra como os pacotes de terceiros podem ser incorporados ao pacote &quot;Contêiner&quot; do projeto, normalmente denominado **&#39;all&#39;**, através da configuração de plug-in **filevault-package-maven-plugin** Maven.

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <subPackages>
           
          <!-- Include the application's ui.apps and ui.content packages -->
          ...
 
          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <!-- Set the version for all dependencies, including 3rd party packages, in the project's Reactor POM -->
          <subPackage>
              <groupId>com.adobe.cq</groupId>
              <artifactId>core.wcm.components.all</artifactId>
              <filter>true</filter>
          </subPackage>
 
 
          <subPackage>
              <groupId>com.3rdparty.groupId</groupId>
              <artifactId>core.3rdparty.artifactId</artifactId>
              <filter>true</filter>
          </subPackage>
      <subPackages>
  </configuration>
</plugin>
...
```

## Como funcionam as implantações em andamento {#how-rolling-deployments-work}

Como as atualizações do AEM, as versões de clientes são implantadas usando uma estratégia de implantação móvel para eliminar o tempo de inatividade do cluster do autor nas circunstâncias certas. A sequência geral de eventos é a descrita abaixo, onde **Blue** é a versão antiga do código do cliente e **Green** é a nova versão. Azul e Verde estão executando a mesma versão do código AEM.

* A versão azul está ativa e um candidato a lançamento para Verde está criado e disponível
* Se houver definições de índice novas ou atualizadas, os índices correspondentes serão processados. Observe que a implantação azul sempre usará os índices antigos, enquanto o verde sempre usará os novos índices.
* O verde está começando enquanto o Blue ainda serve
* O azul está funcionando e servindo enquanto o Verde está sendo verificado quanto à prontidão por meio de verificações de integridade
* Nós verdes que estão prontos para aceitar o tráfego e substituir os nós Azul, que são desativados
* Com o tempo, os nós de azul são substituídos por nós de verde até que apenas o verde permaneça, concluindo assim a implantação
* Qualquer conteúdo mutável novo ou modificado é implantado

## Índices {#indexes}

Índices novos ou modificados causarão uma etapa adicional de indexação ou reindexação antes que a nova versão (verde) possa entrar no tráfego. Detalhes sobre o gerenciamento de índice no Skyline podem ser encontrados [neste artigo](/help/operations/indexing.md). Você pode verificar o status do trabalho de indexação na página de criação do Cloud Manager e receberá uma notificação quando a nova versão estiver pronta para receber tráfego.

>[!NOTE]
>
>O tempo necessário para uma implantação contínua varia dependendo do tamanho do índice, já que a versão em verde não pode aceitar tráfego até que o novo índice seja gerado.

No momento, o Skyline não funciona com ferramentas de gerenciamento de índice, como a ferramenta ACS Commons Assurance Index.

## Replicação {#replication}

O mecanismo de publicação é compatível com versões anteriores das APIs [Java de replicação do](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html)AEM.

Para desenvolver e testar a replicação com o AEM Quickstart pronto para a nuvem, os recursos de replicação clássica precisam ser usados com uma configuração de Autor/Publicação. No caso de o ponto de entrada da interface do usuário no AEM Author ter sido removido para a nuvem, os usuários acessariam `http://localhost:4502/etc/replication` a configuração.

## Código compatível com versões anteriores para implantações contínuas {#backwards-compatible-code-for-rolling-deployments}

Como detalhado acima, o AEM como estratégia de implantação contínua do serviço da Cloud implica que as versões antigas e novas possam estar funcionando ao mesmo tempo. Portanto, tenha cuidado com as alterações de código que não são compatíveis com versões anteriores do AEM que ainda estão em operação.

Além disso, a versão antiga deve ser testada para compatibilidade com qualquer nova estrutura de conteúdo mutável aplicada pela nova versão em caso de reversão, já que o conteúdo mutável não é removido.

### Usuários do serviço e alterações de ACL {#service-users-and-acl-changes}

A alteração dos usuários do serviço ou das ACLs necessárias para acessar o conteúdo ou código pode levar a erros nas versões mais antigas do AEM, resultando no acesso a esse conteúdo ou código com usuários desatualizados do serviço. Para lidar com esse comportamento, uma recomendação é fazer alterações distribuídas em pelo menos duas versões, com a primeira versão funcionando como uma ponte antes de limpar a versão subsequente.

### Alterações de índice {#index-changes}

Se forem feitas alterações nos índices, é importante que a versão Azul continue a usar seus índices até que seja encerrada, enquanto a versão Verde usa seu próprio conjunto modificado de índices. O desenvolvedor deve seguir as técnicas de gerenciamento de índice descritas [neste artigo](/help/operations/indexing.md).

### Codificação conservadora para retornos {#conservative-coding-for-rollbacks}

Se uma falha for relatada ou detectada após a implantação, é possível que uma reversão para a versão Azul seja necessária. Seria aconselhável garantir que o código azul seja compatível com quaisquer novas estruturas criadas pela versão verde, uma vez que as novas estruturas (qualquer conteúdo mutável) não serão revertidas. Se o código antigo não for compatível, as correções precisarão ser aplicadas nas versões subsequentes do cliente.

## modos de execução {#runmodes}

Nas soluções AEM existentes, os clientes têm a opção de executar instâncias com modos de execução arbitrários e aplicar configuração OSGI ou instalar pacotes OSGI a essas instâncias específicas. Os modos de execução definidos normalmente incluem o *serviço* (autor e publicação) e o ambiente (dev, stage, prod).

Por outro lado, o AEM como um serviço em nuvem tem mais opinião sobre quais modos de execução estão disponíveis e como os pacotes OSGI e a configuração OSGI podem ser mapeados para eles:

* Os modos de execução da configuração OSGI devem fazer referência a dev, stage, prod para o ambiente ou autor, publish para o serviço. Uma combinação de `<service>.<environment_type>` está sendo suportada, ao passo que elas precisam ser usadas nessa ordem específica (por exemplo, author.dev ou publish.prod). Os tokens OSGI devem ser referenciados diretamente do código em vez de usar o `getRunModes` método, que não incluirá mais os tokens `environment_type` em tempo de execução.
* Os modos de execução de pacotes OSGI são limitados ao serviço (autor, publicação). Os pacotes OSGI de modo por execução devem ser instalados no pacote de conteúdo sob `install/author` ou `install/publish`.

Como as soluções AEM existentes, não há como usar os modos de execução para instalar apenas conteúdo para ambientes ou serviços específicos. Se fosse desejado implantar um ambiente dev com dados ou HTML que não esteja no estágio ou na produção, o gerenciador de pacotes poderia ser usado.

As configurações de modo de execução suportadas são:

* **config** (*o padrão se aplica a todos os serviços* AEM)
* **config.author** (*aplica-se a todo o serviço* de autor de AEM)
* **config.author.dev** (*Aplica-se ao serviço* de autor de desenvolvedor do AEM)
* **config.author.stage** (*aplica-se ao serviço* de autor de preparo do AEM)
* **config.author.prod** (*aplica-se ao serviço* de autor de produção do AEM)
* **config.publish** (*aplica-se ao serviço* de publicação do AEM)
* **config.publish.dev** (*aplica-se ao serviço* de publicação do desenvolvedor do AEM)
* **config.publish.stage** (*aplica-se ao serviço* de publicação de armazenamento temporário AEM)
* **config.publish.prod** (*aplica-se ao serviço* de publicação de produção do AEM)
* **config.dev** (*Aplica-se aos serviços de desenvolvedor do AEM)
* **config.stage** (*Aplica-se aos serviços de armazenamento temporário AEM)
* **config.prod** (*Aplica-se aos serviços de produção do AEM)

A configuração OSGI que tem os modos de execução mais correspondentes é usada.

Ao desenvolver localmente, um parâmetro de inicialização do modo de execução pode ser passado para ditar qual configuração do modo de execução OSGI será usada.

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Configuração de Tarefas de Manutenção no Controle de Origem {#maintenance-tasks-configuration-in-source-control}

As configurações da tarefa de manutenção devem ser mantidas no controle de origem, pois a tela **Ferramentas > Operações** não estará mais disponível nos ambientes da Cloud. Isto tem o benefício de assegurar que as mudanças sejam intencionalmente persistentes, em vez de aplicadas de forma reativa e talvez esquecidas. Consulte o artigo [Tarefa de](/help/operations/maintenance.md) manutenção para obter mais informações.
