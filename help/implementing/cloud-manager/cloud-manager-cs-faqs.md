---
title: Cloud Manager - Perguntas frequentes do Cloud Services
seo-title: Cloud Manager FAQs
description: Consulte Perguntas frequentes sobre o Cloud Manager para Cloud Services para obter dicas sobre solução de problemas
seo-description: Follow this page to get answers on Cloud Manager - Cloud Services FAQs
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 1%

---

# Perguntas frequentes sobre o Cloud Manager {#cloud-manager-faqs}

A seção a seguir fornece respostas a perguntas frequentes relacionadas ao Cloud Manager para Cloud Services.

## É possível usar o Java 11 com builds do Cloud Manager? {#java-11-cloud-manager}

AEM build do Cloud Manager falha ao tentar alternar a build do Java 8 para o 11. O problema pode ter muitas causas e as mais comuns estão documentadas abaixo:

* Adicione o maven-toolchains-plugin com as configurações corretas para Java 11 conforme documentado [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started).  Por exemplo, consulte o [código de projeto de amostra wknd](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* Se encontrar o erro abaixo, é necessário remover o uso de `maven-scr-plugin` e converter todas as anotações OSGi em anotações OSGi R6. Para obter instruções, consulte [here](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/).

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* Para builds do Cloud Manager, o plug-in maven enforcer falha com erro `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. Esse é um problema conhecido porque o Cloud Manager usa uma versão diferente do Java para executar o comando maven versus o código de compilação. Por enquanto, omita `requireJavaVersion` das configurações maven-enforcer-plugin.

## Nossa implantação ficou paralisada porque a verificação de qualidade do código falhou. Existe uma maneira de ignorar esta verificação? {#deployment-stuck}

Todas as falhas de qualidade do código exceto para *Classificação de segurança* são métricas não críticas, portanto, podem ser ignoradas ao expandir os itens na interface do usuário de resultados.

Um usuário com [Gerenciador de implantação, Gerenciador de projeto ou Proprietário comercial](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements) pode substituir os problemas, caso o pipeline continue ou possa aceitar os problemas, caso o pipeline pare com uma falha.  Consulte [Portas de três níveis ao executar um pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use) para obter mais detalhes.


## Podemos usar o SNAPSHOT na versão do projeto Maven? Como o controle de versão dos pacotes e arquivos jar funciona para implantações de Preparo e Produção? {#snapshot-version}

Consulte os seguintes cenários para saber mais sobre o controle de versão dos pacotes e dos arquivos jar do pacote para implantações de Preparo e Produção:

1. Para implantações de desenvolvedores, a ramificação Git `pom.xml` os arquivos devem conter `-SNAPSHOT` no final do `<version>` valor. Isso permite a implantação subsequente em que a versão não é alterada para ainda ser instalada. Em implantações de desenvolvedores, nenhuma versão automática é adicionada ou gerada para a build maven.

1. Na implantação de Preparo e Produção, uma versão automática é gerada conforme documentado [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code).

1. Para o controle de versão personalizado em implantações de Preparo e Produção, defina uma versão maven correta de 3 partes como `1.0.0`. Aumente a versão sempre que precisar fazer outra implantação na produção.

1. O Cloud Manager adiciona automaticamente sua versão ao Stage e às builds de produção e até cria uma ramificação Git. Nenhuma configuração especial é necessária. Se a etapa 3 acima for ignorada, a implantação ainda funcionará corretamente e uma versão será definida automaticamente.

1. Não há problemas, se você deixar a versão com `-SNAPSHOT` para builds ou implantações de Preparo e Produção. O Cloud Manager define automaticamente um número de versão adequado e cria uma tag para você no Git. Essa tag pode ser consultada posteriormente, se necessário.

1. Se quiser experimentar algum código experimental no ambiente de desenvolvimento, você pode criar uma nova ramificação Git e definir o pipeline para usar essa ramificação diferente. Isso é útil quando as implantações começam a falhar e você gostaria de testar com versões mais antigas do código para ver quando quebrou.

   O comando Git abaixo cria uma ramificação remota chamada *testbranch1* contra uma confirmação preexistente específica `485548e4fbafbc83b11c3cb12b035c9d26b6532b`.  Essa ramificação especial pode ser usada no Cloud Manager sem afetar outras ramificações:

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   Consulte a [Documentação do Git](https://git-scm.com/book/en/v2/Git-Internals-Git-References) para obter mais detalhes.

   Se desejar excluir a ramificação de teste posteriormente, use o comando delete:

   `git push origin --delete testbranch1`

## A build do Maven falha nas implantações do Cloud Manager, mas é criada localmente sem erros. Como depurar? {#maven-build-fail}

Consulte [Recurso Git](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) para obter mais detalhes.

## O que fazer se a implantação do Cloud Manager falhar na etapa de implantação AEM ambiente as a Cloud Service? {#cloud-manager-deployment-cloud-service}

O motivo mais comum para as implantações falharem é devido a permissões insuficientes para o *sling-distribution-importer* usuário.
Consulte o exemplo abaixo para entender um problema, causa e solução:

**Problema**
Durante a implantação do Cloud Manager em AEM ambientes as a Cloud Service, a etapa de implantação falha e são observados erros como os abaixo.

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**Causa**

O usuário sling-distribution-importer precisa de permissões adicionais de acordo com os caminhos de conteúdo definidos no pacote ui.content.  Isso geralmente significa que precisamos adicionar permissões para /conf e /var.

**Solução**
A solução para isso é adicionar um [Configuração OSGi do RepositoryInitializer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=pt-BR#deploying) script para o pacote de implantação de aplicativos para adicionar ACLs para o usuário sling-distribution-importer.
No exemplo de erro acima, o pacote myapp-base.ui.content-*.zip inclui conteúdo em `/conf` e `/var/workflow`. Para que a implantação não falhe, precisaríamos adicionar permissões para sling-distribution-import nesses caminhos.
Veja um exemplo [org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) de uma dessas configurações OSGi que adiciona permissões adicionais para o usuário sling-distribution-importer.  Essa configuração adiciona permissões em /var.  Este arquivo xml abaixo [1] precisa ser adicionado ao pacote do aplicativo em `/apps/myapp/config` (onde myapp é a pasta onde o código do aplicativo está armazenado).
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. Se a variável *sling-distribution-importer* não for a causa, a implantação pode estar falhando devido a uma configuração OSGi incorreta que interrompe um serviço pronto para uso. Verifique os logs durante a implantação para ver se há erros óbvios.

1. A implantação pode falhar devido a configurações incorretas do dispatcher ou do apache. Teste as configurações do Apache e do Dispatcher localmente usando a imagem do Docker incluída no SDK. Consulte [Dispatcher na nuvem](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery) sobre como configurar o contêiner Docker do dispatcher para facilitar o teste local.

1. A implantação pode falhar devido a alguma outra falha durante a replicação dos pacotes de conteúdo (distribuição de sling) do autor para publicar instâncias.

   Consulte as etapas abaixo para simular isso em uma configuração local:

   * Instale uma instância de Autor e Publicação (usando os AEM jars do SDK mais recentes)
   * Faça logon na instância do autor
   * Ir para **Ferramentas** -> **Implantação** -> **Distribuição**
   * Distribua os pacotes de conteúdo que fazem parte da base de código e veja se a fila é bloqueada com um erro

## Não é possível definir uma variável por meio das variáveis de pipeline definidas do aio cloud manager. Como depurar esses problemas? {#set-variable}

Se você estiver recebendo um `403` ao tentar listar ou definir variáveis de pipeline por comandos semelhantes aos abaixo, você precisa ser adicionado como um *Gerenciador de implantação* Função de produto Cloud Manager no Admin Console.\
Consulte [Permissões de API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) para obter mais detalhes.

Comandos e erros relacionados:

`$ aio cloudmanager:list-pipeline-variables 222`

*Erro*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*Erro*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*Erro*: `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
