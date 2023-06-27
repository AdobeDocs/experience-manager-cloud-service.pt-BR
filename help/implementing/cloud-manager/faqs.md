---
title: Perguntas frequentes sobre o Cloud Manager
description: Encontre respostas para as perguntas mais frequentes sobre o Cloud Manager no AEM as a Cloud Service.
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 65%

---


# Perguntas frequentes sobre o Cloud Manager {#cloud-manager-faqs}

Este documento fornece respostas às perguntas mais frequentes sobre o Cloud Manager no AEM as a Cloud Service.

## É possível usar o Java™ 11 com builds do Cloud Manager? {#java-11-cloud-manager}

Sim. Adicione o `maven-toolchains-plugin` com configurações adequadas para Java™ 11.

O processo está documentado [aqui](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started).

Por exemplo, consulte o [código do projeto de amostra do wknd](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

## Minha build falha com um erro sobre o maven-scr-plugin após alternar do Java™ 8 para o Java™ 11. O que posso fazer? {#build-fails-maven-scr-plugin}

A build do AEM Cloud Manager pode falhar ao tentar mudar do Java™ 8 para o 11. Se você encontrar o erro a seguir, será necessário remover `maven-scr-plugin` e converta todas as anotações OSGi em anotações OSGi R6.

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

Para obter instruções sobre como remover esse plug-in, veja [aqui](https://cqdump.joerghoh.de/2019/01/03/from-scr-annotations-to-osgi-annotations/).

## Minha build falha com um erro sobre RequireJavaVersion após alternar do Java™ 8 para o Java™ 11. O que posso fazer? {#build-fails-requirejavaversion}

Para compilações do Cloud Manager, `maven-enforcer-plugin` pode falhar com esse erro.

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

Esse erro é um problema conhecido porque o Cloud Manager usa uma versão diferente do Java™ para executar o comando maven em relação ao código de compilação. Basta omitir `requireJavaVersion` nas configurações `maven-enforcer-plugin`.

## A verificação de qualidade do código falhou e a implantação travou. Existe uma maneira de ignorar essa verificação? {#deployment-stuck}

Sim. Todas as falhas de verificação de qualidade do código, exceto a classificação de segurança, são métricas não críticas; portanto, podem ser ignoradas como parte de um pipeline de implantação, expandindo os itens na interface do usuário de resultados.

Um usuário com a função [Gerente de implantação, Gerente de projeto ou Proprietário da empresa](/help/onboarding/aem-cs-team-product-profiles.md#cloud-manager-product-profiles) pode substituir os problemas, caso em que o pipeline continua, ou pode aceitar os problemas, caso em que o pipeline é interrompido com uma falha.

Veja os documentos [Testes de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md#three-tiered-gate) e [Configuração de pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#non-production-pipelines) para obter mais detalhes.

## Posso usar o SNAPSHOT para a versão do projeto Maven? {#use-snapshot}

Sim. Para implantações de desenvolvedores, os arquivos `pom.xml` da ramificação Git devem conter `-SNAPSHOT` no final do valor `<version>`.

Esse valor permite que a implantação subsequente ainda seja instalada quando a versão não for alterada. Em implantações de desenvolvedores, nenhuma versão automática é adicionada ou gerada para a compilação maven.

Você também pode definir a versão como `-SNAPSHOT` para compilações ou implantações de preparo ou de produção. O Cloud Manager define automaticamente um número de versão adequado e cria uma tag para você no Git. Se necessário, essa tag pode ser consultada posteriormente.

Mais detalhes sobre o manuseio de versão estão [documentados aqui.](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

## Como funciona o controle de versão dos pacotes para implantações de preparo e produção? {#snapshot-version}

Em implantações de preparo e produção, uma versão automática é gerada como [documentado aqui.](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

Para o controle de versão personalizado em implantações de preparo e produção, defina uma versão maven adequada com três partes como `1.0.0`. Aumente a versão sempre que implantar na produção.

O Cloud Manager adicionará automaticamente a versão às compilações de preparo e produção e criará uma ramificação Git. Nenhuma configuração adicional é necessária. Se você não definir uma versão maven conforme descrito anteriormente, a implantação ainda será bem-sucedida e uma versão será definida automaticamente.

## Minha compilação maven falha para implantações do Cloud Manager, mas é criada localmente sem erros. O que há de errado? {#maven-build-fail}

Consulte [este recurso do Git](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) para obter mais detalhes.

## O que devo fazer se uma implantação do Cloud Manager falhar na etapa de implantação do AEM as a Cloud Service? {#cloud-manager-deployment-cloud-service}

O motivo mais comum para uma implantação falhar é devido a permissões insuficientes para o usuário `sling-distribution-importer`. Nesse caso, a etapa de implantação falha durante uma implantação do Cloud Manager e erros como os mostrados a seguir são gerados.

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

O usuário `sling-distribution-importer` precisa de permissões adicionais para os caminhos de conteúdo definidos em `ui.content package`. Essa regra geralmente significa que você deve adicionar permissões para ambos `/conf` e `/var`.

A solução é adicionar um script de [Configuração OSGi de RepositoryInitializer](/help/implementing/deploying/overview.md#repoint) ao pacote de implantação de aplicativos para adicionar ACLs para o usuário `sling-distribution-importer`.

No erro do exemplo anterior, o pacote `myapp-base.ui.content-*.zip` inclui conteúdo em `/conf` e `/var/workflow`. Para que a implantação tenha êxito, as permissões para `sling-distribution-importer` nesses caminhos.

Veja este exemplo de uma Configuração OSGi [`org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config`](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) que adiciona mais permissões ao usuário `sling-distribution-importer`.  A configuração adiciona permissões em `/var`. Essa configuração deve ser adicionada ao pacote do aplicativo em `/apps/myapp/config` (onde myapp é a pasta em que o código do aplicativo está armazenado).

## A implantação do My Cloud Manager falha na etapa de implantação do AEM as a Cloud Service e já adicionei uma configuração OSGi de RepositoryInitializer. O que mais posso fazer? {#build-failures}

Se [adicionar uma configuração OSGi de RepositoryInitializer](#cloud-manager-deployment-cloud-service) não resolver o erro, talvez seja devido a um destes outros problemas.

* A implantação pode falhar devido a uma configuração OSGi incorreta que interrompe um serviço predefinido.
   * Verifique os registros durante a implantação para ver se há erros óbvios.

* A implantação pode falhar devido a configurações incorretas do Dispatcher ou Apache.
   * Teste as configurações do Apache e Dispatcher localmente usando a imagem do Docker incluída no SDK.
   * Consulte [Dispatcher na nuvem](/help/implementing/dispatcher/disp-overview.md#content-delivery) sobre como configurar o contêiner Docker do Dispatcher para facilitar o teste local.

* A implantação pode falhar devido a alguma outra falha durante a replicação dos pacotes de conteúdo (distribuição Sling) entre as instâncias de autoria e publicação.
   * Siga estas etapas para simular o problema em uma configuração local.
      1. Instale uma instância de autoria e publicação localmente usando os jars mais recentes do SDK do AEM.
      1. Faça logon na instância de autoria.
      1. Acesse **Ferramentas** -> **Implantação** -> **Distribuição**.
      1. Distribua os pacotes de conteúdo que fazem parte da base de código e veja se a fila é bloqueada com um erro.

## Não consigo definir uma variável usando um comando aio. O que posso fazer? {#set-variable}

Você pode receber um `403` erro como o seguinte ao tentar listar ou definir variáveis de pipeline por meio de `aio` comandos.

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

Nesse caso, o usuário que executa esses comandos deve ser adicionado ao **Gerente de implantação** no Admin Console.

Consulte [Permissões da API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/) para obter mais detalhes.
