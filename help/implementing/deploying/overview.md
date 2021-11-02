---
title: Implantação do AEM as a Cloud Service
description: 'Implantação do AEM as a Cloud Service '
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: cf3273af030a8352044dcf4f88539121249b73e7
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 1%

---

# Implantação do AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## Introdução {#introduction}

Os fundamentos do desenvolvimento de código são semelhantes em AEM as a Cloud Service em comparação às soluções AEM no local e Managed Services. Os desenvolvedores gravam código e o testam localmente, que é então enviado para ambientes remotos AEM as a Cloud Service. O Cloud Manager, que era uma ferramenta opcional de entrega de conteúdo para o Managed Services, é necessário. Esse agora é o único mecanismo para implantar código em AEM ambientes as a Cloud Service.

A atualização do [Versão AEM](/help/implementing/deploying/aem-version-updates.md) é sempre um evento de implantação separado do push [código personalizado](#customer-releases). Exibidas de outra maneira, as versões de código personalizadas devem ser testadas em relação à versão de AEM que está em produção, pois é isso que ela será implantada no topo. AEM atualizações de versão que ocorrem depois disso, que serão frequentes e serão aplicadas automaticamente. Eles devem ser compatíveis com versões anteriores do código de cliente já implantado.

O resto deste documento descreverá como os desenvolvedores devem adaptar suas práticas para que trabalhem com as atualizações de versão AEM as a Cloud Service e as atualizações do cliente.

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## Versões do cliente {#customer-releases}

### Codificação em relação à versão AEM correta {#coding-against-the-right-aem-version}

Para soluções de AEM anteriores, a versão de AEM mais recente era alterada com pouca frequência (aproximadamente anualmente com service packs trimestrais) e os clientes atualizavam as instâncias de produção para o início rápido mais recente a seu próprio tempo, referenciando o API Jar. No entanto, AEM aplicativos as a Cloud Service são atualizados automaticamente para a versão mais recente do AEM com mais frequência, portanto, o código personalizado para versões internas deve ser criado em relação à versão mais recente do AEM.

Assim como para versões de AEM que não são em nuvem existentes, um desenvolvimento local e offline com base em um início rápido específico será suportado e deve ser a ferramenta preferida para depuração na maioria dos casos.

>[!NOTE]
>Existem sutis diferenças operacionais entre o comportamento do aplicativo em uma máquina local e o da Adobe Cloud. Essas diferenças arquitetônicas devem ser respeitadas durante o desenvolvimento local e podem levar a um comportamento diferente ao implantar na infraestrutura de nuvem. Devido a essas diferenças, é importante executar testes exaustivos em ambientes de desenvolvimento e de estágio antes de implantar o novo código personalizado na produção.

Para desenvolver um código personalizado para uma versão interna, a versão relevante do [AEM SDK as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) deve ser baixada e instalada. Para obter informações adicionais sobre o uso das ferramentas do Dispatcher as a Cloud Service AEM, consulte [esta página](/help/implementing/dispatcher/disp-overview.md).

O vídeo a seguir fornece uma visão geral de alto nível sobre como implantar o código AEM as a Cloud Service:

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## Implantação de pacotes de conteúdo por meio do Cloud Manager e do Gerenciador de pacotes {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Implantações via Cloud Manager {#deployments-via-cloud-manager}

Os clientes implantam código personalizado em ambientes de nuvem por meio do Cloud Manager. Observe que o Cloud Manager transforma pacotes de conteúdo montados localmente em um artefato que está em conformidade com o Modelo de recurso do Sling, que é a forma como um aplicativo as a Cloud Service AEM é descrito ao ser executado em um ambiente de nuvem. Como resultado, ao examinar os pacotes em [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md) em ambientes do Cloud, o nome incluirá &quot;cp2fm&quot; e os pacotes transformados terão todos os metadados removidos. Eles não podem ter interação, o que significa que não podem ser baixados, replicados ou abertos. A documentação detalhada sobre o conversor pode ser [encontrado aqui](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

Os pacotes de conteúdo escritos para AEM aplicativos as a Cloud Service devem ter uma separação limpa entre conteúdo imutável e mutável e o Cloud Manager só instalará o conteúdo mutável, além de exibir uma mensagem como:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

O resto desta seção descreve a composição e as implicações dos pacotes imutáveis e mutáveis.

### Pacotes de conteúdo imutáveis {#immutabe-content-packages}

Todo o conteúdo e código persistente no repositório imutável devem ser verificados no git e implantados por meio do Cloud Manager. Em outras palavras, ao contrário das soluções de AEM atuais, o código nunca é implantado diretamente em uma instância de AEM em execução. Isso garante que o código executado para uma determinada versão em qualquer ambiente do Cloud seja idêntico, o que elimina o risco de variação não intencional do código na produção. Como exemplo, a configuração de OSGI deve ser comprometida com o controle de origem em vez de gerenciada no tempo de execução por meio do gerenciador de configuração do console da Web AEM.

À medida que o aplicativo muda devido ao padrão de implantação Blue-Green é ativado por um switch, ele não pode depender de alterações no repositório mutável, com exceção dos usuários de serviço, suas ACLs, tipos de nó e alterações na definição do índice.

Para clientes com bases de código existentes, é importante passar pelo exercício de reestruturação de repositório descrito em AEM documentação para garantir que o conteúdo anteriormente sob o /etc seja movido para o local correto.

Algumas restrições adicionais se aplicam a esses pacotes de código, por exemplo [instalar ganchos](http://jackrabbit.apache.org/filevault/installhooks.html) não são compatíveis.

## Configuração OSGI {#osgi-configuration}

Como mencionado acima, a configuração de OSGI deve ser comprometida com o controle de origem em vez do console da Web. As técnicas para fazer isso incluem:

* Faça as alterações necessárias no ambiente de AEM local do desenvolvedor com o gerenciador de configuração do console da Web AEM e exporte os resultados para o projeto AEM no sistema de arquivos local
* Criando a configuração OSGI manualmente no projeto AEM no sistema de arquivos local, a referência ao gerenciador de configuração do console AEM para os nomes de propriedade.

Leia mais sobre a configuração OSGI em [Configuração do OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Conteúdo variável {#mutable-content}

Em alguns casos, pode ser útil preparar alterações de conteúdo no controle de origem para que ele possa ser implantado pelo Cloud Manager sempre que um ambiente for atualizado. Por exemplo, pode ser razoável implantar determinadas estruturas de pastas raiz ou alinhar alterações em modelos editáveis para ativar políticas nesses componentes que foram atualizados pela implantação do aplicativo.

Há duas estratégias para descrever o conteúdo que será implantado pelo Cloud Manager no repositório mutável, em pacotes de conteúdo mutáveis e em instruções para repontar.

### Pacotes de conteúdo variável {#mutable-content-packages}

Conteúdo como hierarquias de caminho de pasta, usuários de serviço e controles de acesso (ACLs) normalmente são comprometidas em um projeto de AEM baseado em arquétipo maven. As técnicas incluem exportar de AEM ou escrever diretamente como XML. Durante o processo de criação e implantação, o Cloud Manager compacta o pacote de conteúdo mutável resultante. O conteúdo mutável é instalado em 3 momentos diferentes durante a fase de implantação no pipeline:

Antes da inicialização da nova versão do aplicativo:

* definições de índice (adicionar, modificar, remover)

Durante a inicialização da nova versão do aplicativo, mas antes da mudança:

* Usuários do serviço (adicionar)
* ACLs do usuário do serviço (adicionar)
* tipos de nó (adicionar)

Após a mudança para a nova versão do aplicativo:

* Todo o outro conteúdo definível por meio do cofre do jackrabbit. Por exemplo:
   * Pastas (adicionar, modificar, remover)
   * Modelos editáveis (adicionar, modificar, remover)
   * Configuração sensível ao contexto (qualquer item abaixo de `/conf`) (adicionar, modificar, remover)
   * Scripts (pacotes podem acionar hooks de instalação em vários estágios do processo de instalação do pacote). Consulte a [Documentação do Jackrabbit filevault](http://jackrabbit.incubator.apache.org/filevault/installhooks.html) sobre ganchos de instalação. Observe que AEM CS usa atualmente o Filevault versão 3.4.0, que limita os ganchos de instalação para usuários administradores, usuários do sistema e membro do grupo de administradores).

É possível limitar a instalação de conteúdo mutável para criar ou publicar incorporando pacotes em uma pasta install.author or install.publish em `/apps`. A reestruturação para refletir esta separação foi efetuada no AEM 6.5 e podem ser obtidas informações pormenorizadas sobre a reestruturação de projetos recomendada no [AEM documentação 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

>[!NOTE]
>Os pacotes de conteúdo são implantados em todos os tipos de ambiente (desenvolvimento, estágio, produção). Não é possível limitar a implantação a um ambiente específico. Esta limitação está em vigor para garantir a opção de uma execução de teste de execução automatizada. O conteúdo específico de um ambiente requer instalação manual por meio de [Gerenciador de pacotes.](/help/implementing/developing/tools/package-manager.md)

Além disso, não há nenhum mecanismo para reverter as alterações no pacote de conteúdo mutável após sua aplicação. Se os clientes detectarem um problema, poderão optar por corrigi-lo na próxima versão de código ou como último recurso, restaurar o sistema inteiro para um ponto no tempo antes da implantação.

Qualquer pacote de terceiros incluído deve ser validado como sendo AEM compatível com o as a Cloud Service Service; caso contrário, sua inclusão resultará em uma falha de implantação.

Como mencionado acima, os clientes com bases de código existentes devem estar em conformidade com o exercício de reestruturação do repositório necessário pelas alterações do repositório 6.5 descritas na [AEM documentação 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

## Reapontar {#repoinit}

Nos casos a seguir, é preferível adotar a abordagem de codificação manual de criação de conteúdo explícito `repoinit` instruções nas configurações de fábrica OSGI:

* Criar/excluir/desativar usuários do serviço
* Criar/excluir grupos
* Criar/excluir usuários
* Adicionar ACLs

   >[!NOTE]
   >
   >A definição de ACLs requer que as estruturas de nó já estejam presentes. Portanto, talvez sejam necessárias instruções de criação de caminho anteriores.

* Adicionar caminho (por exemplo, para estruturas de pasta raiz)
* Adicionar CNDs (definições de tipo de nó)

O realce é preferível para esses casos de uso de modificação de conteúdo suportado devido aos seguintes benefícios:

* Reapontar cria recursos na inicialização para que a lógica possa tomar a existência desses recursos como adquiridos. Na abordagem do pacote de conteúdo mutável, os recursos são criados após a inicialização, portanto, o código do aplicativo que depende deles pode falhar.
* Reapontar é um conjunto de instruções relativamente seguro, pois você controla explicitamente a ação a ser tomada. Além disso, as únicas operações compatíveis são aditivas, com a exceção de alguns casos relacionados à segurança que permitem a remoção de usuários, usuários de serviços e grupos. Em contrapartida, uma remoção de algo na abordagem do pacote de conteúdo mutável é explícita; como você define um filtro, qualquer item presente coberto por um filtro será excluído. Ainda assim, deve-se ter cuidado, pois com qualquer conteúdo há cenários em que a presença de novo conteúdo pode alterar o comportamento do aplicativo.
* Repontar executa operações rápidas e atômicas. Em contraste, os pacotes de conteúdo variável podem depender muito do desempenho das estruturas cobertas por um filtro. Mesmo que você atualize um único nó, um instantâneo de uma árvore grande pode ser criado.
* É possível validar instruções de repont em um ambiente dev local em tempo de execução, pois elas serão executadas quando a configuração OSGi for registrada.
* As instruções de repont são atômicas e explícitas e ignorarão se o estado já estiver correspondente.

Quando o Cloud Manager implanta o aplicativo, ele executa essas instruções, independentemente da instalação de qualquer pacote de conteúdo.

Para criar instruções de reindicação, siga o procedimento abaixo:

1. Adicionar configuração OSGi para PID de fábrica `org.apache.sling.jcr.repoinit.RepositoryInitializer` em uma pasta de configuração do projeto. Use um nome descritivo para a configuração como **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**.
1. Adicione instruções repoinit à propriedade script da configuração. A sintaxe e as opções estão documentadas em [Documentação do Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html). Observe que deve haver a criação explícita de uma pasta pai antes de suas pastas filho. Por exemplo, uma criação explícita de `/content` before `/content/myfolder`antes de `/content/myfolder/mysubfolder`. Para ACLs configuradas em estruturas de baixo nível, é recomendável defini-las em um nível superior e trabalhar com um `rep:glob` restrição.  Por exemplo `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Valide no ambiente de desenvolvimento local no tempo de execução.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>Para ACLs definidas para nós abaixo de `/apps` ou `/libs` a execução do reponit será iniciada em um repositório em branco. Os pacotes são instalados após o reapontamento, de modo que as instruções não podem depender de nada definido nos pacotes, mas devem definir as condições prévias como as estruturas pai embaixo.

>[!TIP]
>
>Para ACLs, a criação de estruturas profundas pode ser complexa, portanto, é mais razoável definir uma ACL em um nível mais alto e restringir onde deveria agir por meio de uma restrição rep: glob.

Mais detalhes sobre o reponteiro podem ser encontrados na seção [Documentação do Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Gerenciador de Pacotes &quot;únicos&quot; para Pacotes de Conteúdo Mutável {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="Gerenciador de pacotes - Migração de pacotes de conteúdo variável"
>abstract="Explore o uso do gerenciador de pacotes para casos de uso, onde um pacote de conteúdo deve ser instalado como &quot;único&quot;, o que inclui a importação de conteúdo específico da produção para o armazenamento temporário, a fim de depurar um problema de produção, transferir um pacote de conteúdo pequeno do ambiente local para ambientes AEM Cloud e muito mais."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#cloud-migration" text="Ferramenta Transferência de conteúdo"

Há casos de uso em que um pacote de conteúdo deve ser instalado como um &quot;único&quot;. Por exemplo, importação de conteúdo específico da produção para o armazenamento temporário a fim de depurar um problema de produção. Para esses cenários, [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md) pode ser usado em ambientes AEM as a Cloud Service.

Como o Gerenciador de pacotes é um conceito de tempo de execução, não é possível instalar conteúdo ou código no repositório imutável, portanto, esses pacotes de conteúdo devem consistir apenas em conteúdo mutável (principalmente `/content` ou `/conf`). Se o pacote de conteúdo incluir conteúdo misto (conteúdo mutável e imutável), somente o conteúdo mutável será instalado.

>[!IMPORTANT]
>
>A interface do usuário do Gerenciador de pacotes pode retornar um **indefinido** mensagem de erro se um pacote levar mais de 10 minutos para ser instalado. Não repita a instalação se isso acontecer, pois ela está sendo executada corretamente em segundo plano e alguns conflitos podem ser introduzidos por vários processos de importação simultâneos.

Todos os pacotes de conteúdo instalados pelo Cloud Manager (mutáveis e imutáveis) aparecerão em um estado congelado na interface do usuário do Gerenciador de Pacotes AEM. Esses pacotes não podem ser reinstalados, recriados ou até mesmo baixados e serão listados com um **&quot;cp2fm&quot;** , indicando que a instalação foi gerenciada pelo Cloud Manager.

### Inclusão de pacotes de terceiros {#including-third-party}

É comum que os clientes incluam pacotes pré-criados de fornecedores de software de terceiros, como parceiros de tradução Adobe. A recomendação é hospedar esses pacotes em um repositório remoto e referenciá-los no `pom.xml`. Isso é possível para repositórios públicos e também para repositórios privados com proteção por senha, conforme descrito em [repositórios maven protegidos por senha](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

Se não for possível armazenar o pacote em um repositório remoto, os clientes poderão colocar em um repositório Maven local baseado em sistema de arquivos, que é comprometido com SCM como parte do projeto e referenciado pelo que depender dele. O repositório seria declarado nos exemplos de projeto ilustrados abaixo:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Quaisquer pacotes de terceiros incluídos devem estar em conformidade com as diretrizes de codificação e embalagem do serviço as a Cloud Service AEM descritas neste artigo; caso contrário, sua inclusão resultará em uma falha de implantação.

O trecho Maven POM XML a seguir mostra como os pacotes de terceiros podem ser incorporados ao pacote &quot;Contêiner&quot; do projeto, normalmente denominado **&#39;all&#39;**, por meio da configuração de plug-in **filevault-package-maven-plugin** do Maven.

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

Como AEM atualizações, as versões do cliente são implantadas usando uma estratégia de implantação contínua para eliminar o tempo de inatividade do cluster de criação nas circunstâncias certas. A sequência geral de eventos é a descrita abaixo, onde **Azul** é a versão antiga do código do cliente e **Verde** é a nova versão. Azul e Verde estão executando a mesma versão do código de AEM.

* A versão azul está ativa e um candidato a lançamento para Verde está criado e disponível
* Se houver definições de índice novas ou atualizadas, os índices correspondentes serão processados. Observe que a implantação azul sempre usará os índices antigos, enquanto o verde sempre usará os novos índices.
* Verde está sendo iniciado enquanto o Blue ainda está servindo
* O azul está sendo executado e servindo enquanto o Verde está sendo verificado por estar pronto por meio de verificações de saúde
* Nós verdes que estão prontos para aceitar o tráfego e substituir nós Azul, que são desativados
* Com o tempo, os nós azuis são substituídos por nós verdes até que apenas o verde permaneça, concluindo assim a implantação
* Qualquer conteúdo mutável novo ou modificado é implantado

## Índices {#indexes}

Índices novos ou modificados causarão uma etapa adicional de indexação ou reindexação antes que a nova versão (verde) possa ganhar tráfego. Detalhes sobre a gestão de índice no AEM as a Cloud Service podem ser encontrados em [este artigo](/help/operations/indexing.md). Você pode verificar o status do trabalho de indexação na página de build do Cloud Manager e receberá uma notificação quando a nova versão estiver pronta para receber tráfego.

>[!NOTE]
>
>O tempo necessário para uma implantação contínua varia dependendo do tamanho do índice, já que a versão em verde não pode aceitar tráfego até que o novo índice tenha sido gerado.

No momento, AEM as a Cloud Service não funciona com ferramentas de gerenciamento de índice, como a ferramenta ACS Commons Garante o índice Oak.

## Replicação {#replication}

O mecanismo de publicação é compatível com versões anteriores do [APIs Java de replicação AEM](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html).

Para desenvolver e testar a replicação com a nuvem pronta AEM início rápido, os recursos de replicação clássicos precisam ser usados com uma configuração Autor/Publicação . No caso do ponto de entrada da interface do usuário no AEM Author ter sido removido para a nuvem, os usuários acessariam `http://localhost:4502/etc/replication` para configuração.

## Código compatível com versões anteriores para implantações em andamento {#backwards-compatible-code-for-rolling-deployments}

Como detalhado acima, AEM estratégia de implantação contínua da as a Cloud Service implica que as versões antigas e novas possam estar funcionando ao mesmo tempo. Portanto, tenha cuidado com alterações de código que não são compatíveis com versões antigas do AEM que ainda estão em operação.

Além disso, a versão antiga deve ser testada quanto à compatibilidade com qualquer nova estrutura de conteúdo mutável aplicada pela nova versão em caso de reversão, já que o conteúdo mutável não é removido.

### Usuários do Serviço e Alterações de ACL {#service-users-and-acl-changes}

Alterar os usuários do serviço ou as ACLs necessárias para acessar o conteúdo ou o código pode levar a erros nas versões de AEM mais antigas, resultando no acesso a esse conteúdo ou código com usuários de serviço desatualizados. Para lidar com esse comportamento, uma recomendação é fazer alterações espalhadas em pelo menos 2 versões, com a primeira versão funcionando como uma ponte antes de limpar na versão subsequente.

### Alterações de Índice {#index-changes}

Se forem feitas alterações nos índices, é importante que a versão Azul continue a usar seus índices até que seja encerrada, enquanto a versão Verde usa seu próprio conjunto modificado de índices. O desenvolvedor deve seguir as técnicas de gerenciamento de índice descritas [neste artigo](/help/operations/indexing.md).

### Codificação Conservadora para Rollbacks {#conservative-coding-for-rollbacks}

Se uma falha for relatada ou detectada após a implantação, é possível que uma reversão para a versão Azul seja necessária. Seria sensato garantir que o código azul seja compatível com quaisquer novas estruturas criadas pela versão verde, uma vez que as novas estruturas (qualquer conteúdo mutável) não serão revertidas. Se o código antigo não for compatível, as correções precisarão ser aplicadas nas versões subsequentes do cliente.

## Runmodes {#runmodes}

Nas soluções de AEM existentes, os clientes têm a opção de executar instâncias com modos de execução arbitrários e aplicar a configuração OSGI ou instalar pacotes OSGI a essas instâncias específicas. Os modos de execução definidos normalmente incluem o *service* (criar e publicar) e o ambiente (dev, stage, prod).

AEM as a Cloud Service, por outro lado, é mais opinativo sobre quais modos de execução estão disponíveis e como os pacotes OSGI e a configuração OSGI podem ser mapeados para eles:

* Os modos de execução de configuração OSGI devem fazer referência ao desenvolvimento, ao estágio, à produção do ambiente ou do autor, à publicação do serviço. Uma combinação de `<service>.<environment_type>` está sendo apoiada, mas eles devem ser usados nessa ordem específica (por exemplo, `author.dev` ou `publish.prod`). Os tokens OSGI devem ser referenciados diretamente do código em vez de usar a variável `getRunModes` , que não incluirá mais a variável `environment_type` no tempo de execução. Para obter mais informações, consulte [Configuração do OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).
* Os modos de execução de pacotes OSGI são limitados ao serviço (autor, publicação). Os pacotes OSGI do modo por execução devem ser instalados no pacote de conteúdo em `install/author` ou `install/publish`.

Como as soluções de AEM existentes, não há como usar os modos de execução para instalar apenas o conteúdo de ambientes ou serviços específicos. Se desejasse implantar um ambiente de desenvolvimento com dados ou HTML que não esteja no estágio ou na produção, o gerenciador de pacotes poderia ser usado.

As configurações de modo de execução compatíveis são:

* **configuração** (*O padrão se aplica a todos os Serviços de AEM*)
* **config.author** (*Aplica-se a todos os serviços de autor do AEM*)
* **config.author.dev** (*Aplica-se a AEM serviço de Autor de Desenvolvimento*)
* **config.author.stage** (*Aplica-se ao serviço Autor de preparação AEM*)
* **config.author.prod** (*Aplica-se AEM serviço Autor de produção*)
* **config.publish** (*Aplica-se ao serviço de publicação do AEM*)
* **config.publish.dev** (*Aplica-se a AEM serviço de publicação de desenvolvimento*)
* **config.publish.stage** (*Aplica-se a AEM serviço de publicação de preparo*)
* **config.publish.prod** (*Aplica-se AEM serviço de publicação de produção*)
* **config.dev** (*Aplica-se a serviços de desenvolvimento AEM)
* **config.stage** (*Aplica-se a serviços de preparação de AEM)
* **config.prod** (*Aplica-se a serviços de produção AEM)

A configuração OSGI que tem os runmodes mais correspondentes é usada.

Ao desenvolver localmente, um parâmetro de inicialização do modo de execução pode ser transmitido para determinar qual configuração do OSGI do modo de execução será usada.

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Configuração de Tarefas de Manutenção no Controle de Origem {#maintenance-tasks-configuration-in-source-control}

As configurações da Tarefa de Manutenção devem ser mantidas no controle de origem desde que o **Ferramentas > Operações** não estará mais disponível em ambientes do Cloud. Isto tem o benefício de assegurar que as mudanças sejam intencionalmente persistentes em vez de aplicadas de forma reativa e talvez esquecidas. Consulte a [Artigo da Tarefa de manutenção](/help/operations/maintenance.md) para obter mais informações.
