---
title: Implantação do AEM as a Cloud Service
description: Implantação do AEM as a Cloud Service
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: 3dd65a9bd67a0a029483d580dd819fb7ac2a10be
workflow-type: tm+mt
source-wordcount: '3542'
ht-degree: 88%

---

# Implantação do AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## Introdução {#introduction}

Os fundamentos do desenvolvimento de código são semelhantes no AEM as a Cloud Service em comparação às soluções locais do AEM e Managed Services. Os desenvolvedores criam o código e o testam localmente, e depois o enviam para ambientes remotos do AEM as a Cloud Service. O uso do Cloud Manager, que era uma ferramenta opcional de entrega de conteúdo do Managed Services, é obrigatório. Ele agora é o único mecanismo para implantar código nos ambientes de desenvolvimento, preparo e produção do AEM as a Cloud Service. Para uma rápida validação e depuração de recursos antes da implantação desses ambientes mencionados, o código pode ser sincronizado de um ambiente local em um [ambiente de desenvolvimento rápido](/help/implementing/developing/introduction/rapid-development-environments.md).

A atualização da [versão do AEM](/help/implementing/deploying/aem-version-updates.md) é sempre um evento de implantação separado do envio de [código personalizado](#customer-releases). Visto de outra maneira, as versões de código personalizado devem ser testadas em relação à versão do AEM que está em produção, pois é nela que o código será implantado. As atualizações frequentes da versão do AEM que ocorrem depois disso são aplicadas automaticamente. Elas são feitas para serem compatíveis com versões anteriores do código do cliente já implantado.

O resto deste documento descreverá como os desenvolvedores devem adaptar suas práticas para que possam trabalhar com as atualizações da versão do AEM as a Cloud Service e as atualizações do cliente.

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## Versões do cliente {#customer-releases}

### Codificar na versão correta do AEM {#coding-against-the-right-aem-version}

Para soluções anteriores do AEM, a versão mais recente era alterada com pouca frequência (geralmente de forma anual com pacotes de serviços trimestrais) e os clientes atualizavam as instâncias de produção para o Quickstart mais recente no seu próprio ritmo, referenciando o Jar da API. No entanto, os aplicativos do AEM as a Cloud Service são atualizados automaticamente para a versão mais recente com mais frequência, portanto, o código personalizado para versões internas deve ser criado baseado na versão mais recente do AEM.

Assim como nas versões fora da nuvem do AEM já existentes, haverá suporte para um desenvolvimento local e offline com base em um Quickstart específico, e essa deve ser a ferramenta preferencial para depuração na maioria dos casos.

>[!NOTE]
>Existem algumas diferenças operacionais sutis entre a maneira como o aplicativo funciona em um computador local comparado à Adobe Cloud. Essas diferenças de arquitetura devem ser respeitadas durante o desenvolvimento local e podem resultar em um comportamento diferente ao implantar na infraestrutura em nuvem. Devido a essas diferenças, é importante executar testes exaustivos nos ambientes de desenvolvimento e de preparo antes de implantar o novo código personalizado na produção.

Para desenvolver um código personalizado para uma versão interna, a versão relevante do [SDK do AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) deve ser baixada e instalada. Para obter informações adicionais sobre o uso das ferramentas do Dispatcher do AEM as a Cloud Service, consulte [esta página](/help/implementing/dispatcher/disp-overview.md).

O vídeo a seguir fornece uma visão geral de alto nível sobre como implantar código no AEM as a Cloud Service:

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## Implantação de pacotes de conteúdo por meio do Cloud Manager e do Gerenciador de pacotes {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Implantações via Cloud Manager {#deployments-via-cloud-manager}

<!-- Alexandru: temporarily commenting this out, until I get some clarification from Brian 

![image](https://git.corp.adobe.com/storage/user/9001/files/e91b880e-226c-4d5a-93e0-ae5c3d6685c8) -->

Os clientes implantam código personalizado em ambientes na nuvem por meio do Cloud Manager. Observe que o Cloud Manager transforma pacotes de conteúdo montados localmente em um artefato em conformidade com o modelo de recurso do Sling, que é a forma como um aplicativo do AEM as a Cloud Service é descrito ao ser executado em um ambiente na nuvem. Como resultado, ao examinar os pacotes do [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md) em ambientes na nuvem, o nome incluirá “cp2fm” e os pacotes transformados terão todos os metadados removidos. Não é possível interagir com eles, o que significa que não podem ser baixados, replicados ou abertos. A documentação detalhada sobre o conversor pode ser [encontrada aqui](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

Os pacotes de conteúdo criados para aplicativos do AEM as a Cloud Service devem ter uma separação clara entre conteúdo imutável e mutável (o Cloud Manager só instalará o conteúdo mutável), além de exibir uma mensagem como:

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

O resto desta seção descreverá a composição e as implicações dos pacotes imutáveis e mutáveis.

### Pacotes de conteúdo imutáveis {#immutabe-content-packages}

Todo conteúdo e código persistente no repositório imutável deve ser verificado no Git e implantado por meio do Cloud Manager. Em outras palavras, ao contrário das soluções atuais do AEM, o código nunca é implantado diretamente em uma instância em execução do AEM. Isso garante que o código executado para uma determinada versão seja idêntico em qualquer ambiente da nuvem, o que elimina o risco de uma variação não intencional do código na produção. Como exemplo, a configuração do OSGI deve ser enviada para o controle de origem em vez de ser gerenciada no tempo de execução por meio do gerenciador de configuração do console da web do AEM.

À medida que o aplicativo muda devido ao padrão de implantação ser ativado por um switch, ele não pode depender das alterações no repositório mutável, com exceção das alterações nos usuários de serviço, suas ACLs, tipos de nó e definições de índice.

Para clientes com bases de código já existentes, é muito importante realizar o exercício de reestruturação de repositório descrito na documentação do AEM para garantir que o conteúdo anteriormente contido em /etc seja movido para o local correto.

Algumas restrições adicionais se aplicam a esses pacotes de código, por exemplo, [instalar ganchos](https://jackrabbit.apache.org/filevault/installhooks.html) não é permitido.

## Configuração OSGI {#osgi-configuration}

Como mencionado acima, a configuração do OSGI deve ser confirmada pelo controle de origem em vez do console da web. As técnicas para fazer isso incluem:

* Fazer as alterações necessárias no ambiente local do desenvolvedor do AEM com o gerenciador de configuração do console da web do AEM e então exportar os resultados para o projeto do AEM no sistema de arquivos local
* Criar a configuração do OSGI manualmente no projeto do AEM no sistema de arquivos local, e então referenciar o gerenciador de configuração do console do AEM para os nomes de propriedades.

Leia mais sobre a configuração do OSGI em [Configuração do OSGi para o AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Conteúdo mutável {#mutable-content}

Em alguns casos, pode ser útil preparar as alterações de conteúdo no controle de origem para que elas possam ser implantadas pelo Cloud Manager sempre que um ambiente for atualizado. Por exemplo, pode ser razoável implantar determinadas estruturas de pastas raiz ou alinhar alterações em modelos editáveis a fim de ativar políticas para componentes que foram atualizados pela implantação do aplicativo.

Há duas estratégias para descrever o conteúdo que será implantado pelo Cloud Manager no repositório mutável: pacotes de conteúdo mutáveis e instruções repoinit.

### Pacotes de conteúdo mutáveis {#mutable-content-packages}

Conteúdos como hierarquias de caminho de pasta, usuários de serviço e controles de acesso (ACLs) normalmente são confirmados em um projeto do AEM baseado no arquétipo Maven. As técnicas incluem exportar do AEM ou gravar diretamente como XML. Durante o processo de criação e implantação, o Cloud Manager compacta o pacote de conteúdo mutável resultante. O conteúdo mutável é instalado em 3 momentos diferentes durante a fase de implantação no pipeline:

Antes da inicialização da nova versão do aplicativo:

* definições de índice (adicionar, modificar, remover)

Durante a inicialização da nova versão do aplicativo, mas antes da mudança:

* Usuários do serviço (adicionar)
* ACLs do usuário do serviço (adicionar)
* tipos de nó (adicionar)

Após a mudança para a nova versão do aplicativo:

* Todos os outros conteúdos são definidos por meio do vault do jackrabbit. Por exemplo:
   * Pastas (adicionar, modificar, remover)
   * Modelos editáveis (adicionar, modificar, remover)
   * Configuração sensível ao contexto (qualquer item abaixo de `/conf`) (adicionar, modificar, remover)
   * Scripts (os pacotes podem acionar ganchos de instalação em vários estágios do processo de instalação do pacote. Consulte a [documentação do Jackrabbit Filevault](https://jackrabbit.apache.org/filevault/installhooks.html) sobre ganchos de instalação. Observe que o AEM CS usa atualmente o Filevault versão 3.4.0, que limita os ganchos de instalação aos usuários administradores, usuários do sistema e membros do grupo de administradores)).

É possível limitar a instalação de conteúdo mutável para criar ou publicar incorporando pacotes em uma pasta install.author ou install.publish sob `/apps`. A reestruturação para refletir esta separação foi efetuada no AEM 6.5 e os detalhes sobre a reestruturação de projetos recomendada podem ser encontrados na [documentação do AEM 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=pt-BR)

>[!NOTE]
>Os pacotes de conteúdo são implantados em todos os tipos de ambiente (desenvolvimento, preparo, produção). Não é possível limitar a implantação a um ambiente específico. Esta limitação está em vigor para garantir a opção de uma execução de teste automatizada. Conteúdos que são específicos a um ambiente necessitam de instalação manual por meio do [Gerenciador de pacotes.](/help/implementing/developing/tools/package-manager.md)

Além disso, não há um mecanismo para reverter as alterações mutáveis no pacote de conteúdo após serem aplicadas. Se os clientes detectarem um problema, poderão optar por corrigi-lo na próxima versão do código ou, como último recurso, restaurar o sistema inteiro para um determinado estado antes da implantação.

Qualquer pacote de terceiros incluído deve ser validado como sendo compatível com o AEM as a Cloud Service, caso contrário, sua inclusão resultará em uma falha de implantação.

Como mencionado acima, os clientes com bases de código existentes devem estar em conformidade com o exercício de reestruturação do repositório exigido de acordo com as alterações da versão 6.5 do repositório, descritas na [documentação do AEM 6.5.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=pt-BR)

## Repoinit {#repoinit}

Nos casos a seguir, é preferível adotar a abordagem de codificação manual para criação de conteúdo explícito com instruções `repoinit` em configurações de fábrica do OSGI:

* Criar/excluir/desativar usuários do serviço
* Criar/excluir grupos
* Criar/excluir usuários
* Adicionar ACLs

  >[!NOTE]
  >
  >A definição de ACLs requer que as estruturas de nó já estejam presentes. Portanto, talvez sejam necessárias instruções de criação de caminho anteriores.

* Adicionar caminho (por exemplo, para estruturas de pasta raiz)
* Adicionar CNDs (definições de tipo de nó)

O repoinit é recomendado nesses casos de uso de modificação de conteúdo compatíveis devido aos seguintes benefícios:

* O repoinit cria recursos na inicialização para que a lógica possa tomar a existência desses recursos como garantida. Na abordagem do pacote de conteúdo mutável, os recursos são criados após a inicialização, portanto, o código do aplicativo que depende deles pode falhar.
* O repoinit é um conjunto de instruções relativamente seguro, pois você controla explicitamente a ação a ser tomada. Além disso, as únicas operações compatíveis são aditivas, com a exceção de alguns casos relacionados à segurança que permitem a remoção de Usuários, Usuários de serviços e Grupos. Em contrapartida, uma remoção de algo na abordagem do pacote de conteúdo mutável é explícita; quando você define um filtro, qualquer item presente coberto por um filtro será excluído. Ainda assim, deve-se ter cuidado, pois com qualquer conteúdo há cenários em que a presença de novo conteúdo pode alterar o comportamento do aplicativo.
* Repontar executa operações rápidas e atômicas. Em contraste, os pacotes de conteúdo variável podem depender muito do desempenho das estruturas cobertas por um filtro. Mesmo que você atualize um único nó, um instantâneo de uma árvore grande pode ser criado.
* É possível validar instruções repoinit em um ambiente de desenvolvimento local em tempo de execução, pois elas serão executadas quando a configuração OSGi for registrada.
* As instruções repoinit são atômicas e explícitas e serão ignoradas se o estado já estiver correspondente.

Quando o Cloud Manager implanta o aplicativo, ele executa essas instruções, independentemente da instalação de qualquer pacote de conteúdo.

Para criar instruções repoinit, siga o procedimento abaixo:

1. Adicione a configuração OSGi para PID de fábrica `org.apache.sling.jcr.repoinit.RepositoryInitializer` em uma pasta de configuração do projeto. Use um nome descritivo para a configuração, como **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**.
1. Adicione instruções repoinit à propriedade do script da configuração. A sintaxe e as opções estão documentadas em [Documentação do Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html). Observe que deve haver a criação explícita de uma pasta principal antes de suas pastas filho. Por exemplo, uma criação explícita de `/content` antes de `/content/myfolder`, antes de `/content/myfolder/mysubfolder`. Para ACLs configuradas em estruturas de baixo nível, é recomendável defini-las em um nível superior e trabalhar com uma restrição `rep:glob`.  Por exemplo, `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. Valide no ambiente de desenvolvimento local no tempo de execução.

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>Para ACLs definidas para nós abaixo de `/apps` ou `/libs` a execução repoinit será iniciada em um repositório em branco. Os pacotes são instalados após o repoinit, portanto, as instruções não podem depender de nada definido nos pacotes, mas devem definir as pré-condições como as estruturas principais abaixo.

>[!TIP]
>
>Para ACLs, a criação de estruturas profundas pode ser complicada, portanto, é mais razoável definir uma ACL em um nível superior e restringir onde ela deve atuar por meio de uma restrição rep:glob.

Mais detalhes sobre o repoinit podem ser encontrados na [Documentação do Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### Gerenciador de Pacotes “únicos” para Pacotes de conteúdo variável {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="Gerenciador de pacotes - Migração de pacotes de conteúdo variável"
>abstract="Explore o uso do gerenciador de pacotes para casos de uso em que um pacote de conteúdo deve ser instalado como “único”, o que inclui importar um conteúdo específico da produção para o preparo com o fim de depurar um problema de produção, transferir um pequeno pacote de conteúdo do ambiente local para ambientes de nuvem do AEM e muito mais."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=pt-BR#cloud-migration" text="Ferramenta Transferência de conteúdo"

Há casos de uso em que um pacote de conteúdo deve ser instalado como “único”. Por exemplo, importação de conteúdo específico da produção para o preparo a fim de depurar um problema de produção. Para esses cenários, o [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md) pode ser usado em ambientes do AEM as a Cloud Service.

Como o Gerenciador de pacotes é um conceito de tempo de execução, não é possível instalar conteúdo ou código no repositório invariável, portanto, esses pacotes de conteúdo devem ter apenas conteúdo variável (principalmente `/content` ou `/conf`). Se o pacote de conteúdo incluir conteúdo misto (conteúdo variável e invariável), somente o conteúdo variável será instalado.

>[!IMPORTANT]
>
>A interface do Gerenciador de pacotes pode retornar uma mensagem de erro **indefinida** se um pacote levar mais de 10 minutos para ser instalado.
>
>Isso não acontece devido a um erro na instalação, mas a um tempo limite que o Cloud Service tem para todas as solicitações.
>
>Não repita a instalação se esse erro aparecer. A instalação está ocorrendo corretamente em segundo plano. Se você reiniciar a instalação, alguns conflitos poderão ser introduzidos por vários processos de importação simultâneos.

Todos os pacotes de conteúdo instalados pelo Cloud Manager (variáveis e invariáveis) aparecerão em um estado congelado na interface do Gerenciador de pacotes do AEM. Esses pacotes não podem ser reinstalados, recriados ou até mesmo baixados e serão listados com um sufixo **“cp2fm”**, indicando que a instalação foi gerenciada pelo Cloud Manager.

### Inclusão de pacotes de terceiros {#including-third-party}

É comum que os clientes incluam pacotes pré-criados de fornecedores de software de terceiros, como parceiros de tradução da Adobe. A recomendação é hospedar esses pacotes em um repositório remoto e referenciá-los no `pom.xml`. Isso é possível para repositórios públicos e também para repositórios privados com proteção por senha, conforme descrito em [repositórios maven protegidos por senha](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

Se não for possível armazenar o pacote em um repositório remoto, os clientes poderão colocá-lo em um repositório Maven local baseado em sistema de arquivos, que é confirmado no SCM como parte do projeto e referenciado pelo que depender dele. O repositório seria declarado no pom do projeto, conforme ilustrado abaixo:


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

Quaisquer pacotes de terceiros incluídos devem estar em conformidade com as diretrizes de codificação e empacotamento do AEM as a Cloud Service descritas neste artigo; caso contrário, a inclusão resultará em uma falha de implantação.

O snippet `POM.xml` do Maven a seguir mostra como os pacotes de terceiros podem ser incorporados ao pacote “Container” do projeto, normalmente denominado **“todos”**, por meio da configuração do plug-in **filevault-package-maven-plugin** do Maven.

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          ...

          <!-- Include any other extra packages  -->
          <embedded>
              <groupId>com.vendor.x</groupId>
              <artifactId>vendor.plug-in.all</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/container/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

## Como funcionam as implantações contínuas {#how-rolling-deployments-work}

Assim como as atualizações do AEM, as versões do cliente são implantadas usando uma estratégia de implantação contínua para eliminar o tempo de inatividade do cluster de autor nas circunstâncias certas. A sequência geral de eventos é descrita abaixo, onde os nós com as versões antiga e nova do código do cliente estão executando a mesma versão do código AEM.

* Os nós com a versão antiga estão ativos e um candidato a lançamento para a nova versão é criado e fica disponível.
* Se houver definições de índice novas ou atualizadas, os índices correspondentes serão processados. Observe que os nós com a versão antiga sempre usarão os índices antigos, enquanto os nós com a nova versão sempre usarão os novos índices.
* Os nós com a nova versão são inicializados enquanto as versões antigas ainda fornecem tráfego.
* Os nós com a versão antiga estão em execução e continuam funcionando, enquanto os nós com a nova versão são verificados quanto à disponibilidade por meio de verificações de integridade.
* Os nós com a nova versão que estão prontos aceitarão o tráfego e substituirão os nós pela versão antiga, que é desativada.
* Com o tempo, os nós com a versão antiga são substituídos por nós com a nova versão até que apenas os nós com novas versões permaneçam, concluindo assim a implantação.
* Qualquer conteúdo mutável novo ou modificado é então implantado.

## Índices {#indexes}

Índices novos ou modificados causarão uma etapa adicional de indexação ou reindexação antes que a nova versão possa receber tráfego. Detalhes sobre a gestão de índice no AEM as a Cloud Service podem ser encontrados [neste artigo](/help/operations/indexing.md). Você pode verificar o status do trabalho de indexação na página de construção do Cloud Manager e receberá uma notificação quando a nova versão estiver pronta para receber tráfego.

>[!NOTE]
>
>O tempo necessário para uma implantação contínua varia de acordo com o tamanho do índice, já que a nova versão não pode aceitar tráfego até que o novo índice seja gerado.

No momento, o AEM as a Cloud Service não funciona com ferramentas de gerenciamento de índice, como a ferramenta ACS Commons Ensure Oak Index.

## Replicação {#replication}

O mecanismo de publicação é compatível com versões anteriores das [APIs Java de Replicação do AEM](https://helpx.adobe.com/br/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html).

Para desenvolver e testar a replicação com o início rápido do AEM pronto para nuvem, os recursos clássicos de replicação precisam ser usados com uma configuração de Autor/Publicação. No caso do ponto de entrada da interface no AEM Author ter sido removido para a nuvem, os usuários acessariam `http://localhost:4502/etc/replication` para configuração.

## Código compatível com versões anteriores para implantações em andamento {#backwards-compatible-code-for-rolling-deployments}

Como detalhado acima, a estratégia de implantação contínua do AEM as a Cloud Service implica que as versões antigas e novas possam estar funcionando ao mesmo tempo. Portanto, tenha cuidado com alterações de código que não sejam compatíveis com a versão antiga do AEM que ainda está em operação.

Além disso, a versão antiga deve ser testada quanto à compatibilidade com qualquer nova estrutura de conteúdo mutável aplicada pela nova versão em caso de reversão, já que o conteúdo mutável não é removido.

### Usuários do serviço e alterações de ACL {#service-users-and-acl-changes}

Alterar os usuários do serviço ou as ACLs necessárias para acessar o conteúdo ou o código pode levar a erros nas versões do AEM mais antigas, resultando no acesso a esse conteúdo ou código com usuários de serviço desatualizados. Para lidar com esse comportamento, a recomendação é fazer alterações em pelo menos duas versões, com a primeira atuando como uma ponte antes de limpar na versão subsequente.

### Alterações de índice {#index-changes}

Se forem feitas alterações nos índices, é importante que a nova versão continue a usar seus índices até que seja encerrada, enquanto a versão antiga usa seu próprio conjunto modificado de índices. O desenvolvedor deve seguir as técnicas de gerenciamento de índice descritas [neste artigo](/help/operations/indexing.md).

### Codificação conservadora para reversões {#conservative-coding-for-rollbacks}

Se uma falha for relatada ou detectada após a implantação, é possível que uma reversão para a versão antiga seja necessária. É recomendável garantir que o novo código seja compatível com qualquer nova estrutura criada por essa nova versão, já que as novas estruturas (qualquer conteúdo mutável) não serão revertidas. Se o código antigo não for compatível, as correções precisarão ser aplicadas nas versões subsequentes do cliente.

## Ambientes de desenvolvimento rápido (RDE) {#rde}

Os [ambientes de desenvolvimento rápido](/help/implementing/developing/introduction/rapid-development-environments.md) (ou RDEs) permitem que os desenvolvedores implantem e revisem alterações rapidamente, minimizando o tempo necessário para testar recursos que já comprovadamente funcionam em um ambiente de desenvolvimento local.

Diferentemente dos ambientes de desenvolvimento comuns, que implantam código por meio do pipeline do Cloud Manager, os desenvolvedores usam ferramentas de linha de comando para sincronizar o código de um ambiente de desenvolvimento local com o RDE. Depois que as alterações forem testadas com sucesso em um RDE, elas deverão ser implantadas em um ambiente de desenvolvimento em nuvem comum por meio do pipeline do Cloud Manager, o que transmitirá o código por meio das portas de qualidade apropriadas.

## Modos de execução {#runmodes}

Nas soluções do AEM existentes, os clientes têm a opção de executar instâncias com modos de execução arbitrários e aplicar a configuração OSGI ou instalar pacotes OSGI nessas instâncias específicas. Os modos de execução definidos normalmente incluem o *serviço* (autor e publicação) e o ambiente (RDE, desenvolvimento, preparo, produção).

O AEM as a Cloud Service, por outro lado, é mais opinativo sobre quais modos de execução estão disponíveis e como os pacotes OSGI e a configuração OSGI podem ser mapeados para eles:

* Os modos de execução da configuração OSGI devem fazer referência ao RDE, desenvolvimento, preparo e produção, no caso do ambiente, ou ao autor e à publicação, no caso do serviço. Uma combinação de `<service>.<environment_type>` está tendo suporte, mas elas devem ser usadas nessa ordem específica (por exemplo, `author.dev` ou `publish.prod`). Os tokens OSGI devem ser referenciados diretamente do código, em vez de usar o método de `getRunModes`, que não incluirá mais o `environment_type` no tempo de execução. Para obter mais informações, consulte [Configuração do OSGi para o AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).
* Os modos de execução de pacotes OSGI são limitados ao serviço (autor, publicação). Os pacotes OSGI do modo por execução devem ser instalados no pacote de conteúdo em `install.author` ou `install.publish`.

O AEM as a Cloud Service não permite o uso de modos de execução para instalar conteúdo em ambientes ou serviços específicos. Se um ambiente de desenvolvimento precisar ser semeado com dados ou HTML que não estejam nos ambientes de preparo ou produção, o gerenciador de pacotes poderá ser usado.

As configurações de modo de execução compatíveis são:

* **config** (*o padrão, que se aplica a todos os serviços do AEM*)
* **config.author** (*Aplica-se a todos os serviços AEM Author*)
* **config.author.dev** (*Aplica-se ao serviço do AEM Dev Author*)
* **config.author.rde** (*aplica-se ao serviço de autor do RDE do AEM*)
* **config.author.stage** (*Aplica-se ao serviço Autor de preparação AEM*)
* **config.author.prod** (*Aplica-se ao serviço Autor de produção AEM*)
* **config.publish** (*Aplica-se ao serviço Publicação AEM*)
* **config.publish.dev** (*Aplica-se ao serviço Desenvolvimento e Publicação AEM*)
* **config.publish.rde** (*aplica-se ao serviço de publicação do RDE do AEM*)
* **config.publish.stage** (*Aplica-se ao serviço Preparação de publicação AEM*)
* **config.publish.prod** (*Aplica-se serviço Produção de publicação AEM*)
* **config.dev** (*Aplica-se a serviços de Desenvolvimento AEM*)
* **config.rde** (*aplica-se aos serviços do RDE*)
* **config.stage** (*Aplica-se a serviços de Preparo AEM*)
* **config.prod** (*Aplica-se a serviços de Produção AEM*)

A configuração OSGI que tem os modos de execução mais correspondentes é usada.

Ao desenvolver localmente, um parâmetro de inicialização do modo de execução, `-r`, é usado para especificar a configuração OSGI do modo de execução.

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Configuração da Tarefa de manutenção no Controle de origem {#maintenance-tasks-configuration-in-source-control}

As configurações da Tarefa de manutenção devem ser mantidas no controle de origem já que a tela **Ferramentas > Operações** não estará mais disponível nos ambientes na nuvem. Isto tem o benefício de assegurar que as mudanças sejam intencionalmente persistentes em vez de aplicadas de forma reativa e talvez até esquecidas. Consulte o [artigo da Tarefa de manutenção](/help/operations/maintenance.md) para obter mais informações.
