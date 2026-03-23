---
title: Adicionar um pipeline de não produção
description: Saiba como adicionar um pipeline de não produção para testar a qualidade do seu código antes de implantar em ambientes de produção.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 8391980183b8c5a91046e01474200b9eaf8e0546
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 19%

---


# Adicionar um pipeline de não produção {#configuring-non-production-pipelines}

Depois de configurar um programa e criar pelo menos um ambiente na interface do usuário do Cloud Manager, você pode adicionar pipelines de não produção. Esses pipelines permitem testar a qualidade do código antes de implantar em ambientes de produção.

Um usuário deve ter a função **[Gerente de Implantação](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar pipelines de não produção.

>[!NOTE]
>
>Você poderá [editar as configurações do pipeline](managing-pipelines.md) após a configuração inicial.

## Adicionar um novo pipeline de não produção {#adding-non-production-pipeline}

Depois de configurar um programa e criar pelo menos um ambiente na interface do usuário do Cloud Manager, você pode adicionar pipelines de não produção. Use esses pipelines para testar a qualidade do código antes de implantar em ambientes de produção.

**Para adicionar um novo pipeline de não produção:**

1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
1. Na seção **Acesso rápido**, clique em **Experience Manager**.
1. No painel lateral esquerdo, clique em **Cloud Manager**.
1. Selecione a organização desejada.
1. No console **Meus Programas**, clique em um programa.
1. No painel lateral esquerdo, clique em **Pipelines**.
1. Na página **Pipelines**, próximo ao canto superior direito, clique em **Adicionar pipeline** > **Adicionar pipeline de não produção**.

   ![Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. Na guia **Configuração** da caixa de diálogo **Adicionar pipeline de não produção**, selecione um dos seguintes pipelines de não produção que deseja criar:

   * **Pipeline de Qualidade de Código** - Cria um pipeline que cria o código em uma ramificação GIT, executa testes de unidade e avalia a qualidade do código sem implantar em um ambiente.
   * **Pipeline de Implantação** - Cria um pipeline que compila o código, executa testes de unidade, avalia a qualidade do código e realiza a implantação em um ambiente de não produção.

   ![Caixa de diálogo Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Na seção **Configuração de pipeline**, no campo **Nome do pipeline de não produção**, digite uma descrição para o pipeline de não produção.
1. Na seção **Opções de Implantação**, selecione um dos seguintes disparadores de implantação que você deseja usar:

   * **Manual**: permite iniciar manualmente o pipeline.
   * **Sobre alterações do Git**: inicia o pipeline sempre que confirmações forem adicionadas à ramificação Git configurada. Com essa opção, ainda é possível iniciar o pipeline manualmente, conforme necessário.

1. Selecione o **Comportamento de Falhas de Métricas Importantes** que deseja usar.

   * **Perguntar sempre**: esse comportamento é a configuração padrão e exige intervenção manual em qualquer falha importante.
   * **Falhar imediatamente**: se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. É basicamente semelhante a um usuário que rejeita manualmente cada falha.
   * **Continuar imediatamente**: se essa opção for selecionada, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. É basicamente semelhante a um usuário que aprova manualmente cada falha.

1. Clique em **Continuar**.

1. As etapas restantes que você usa para concluir a configuração do pipeline de não produção dependem do tipo de código-fonte que você escolher usar.
Na guia **Código Source** da caixa de diálogo **Adicionar pipeline de não produção**, selecione o tipo de código que o pipeline de não produção deve processar.

   * **[Estou usando o Código de Pilha Completa](#full-stack-code)**
   * **[Estou usando a implantação direcionada](#targeted-deployment)**

   Consulte [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obter mais informações sobre os tipos de pipelines.


### Estou usando o Código de pilha completa {#full-stack-code}

Um pipeline de código de pilha completa implanta simultaneamente compilações de código de back-end e front-end contendo um ou mais aplicativos de servidor do AEM, juntamente com a configuração HTTPD/Dispatcher.

>[!NOTE]
>
>Se um pipeline de código de pilha completa já existir para o ambiente selecionado, essa seleção será desabilitada.

Para concluir a configuração do pipeline de não produção do código de pilha completa, faça o seguinte:

1. Na seção **Código Source**, defina as seguintes opções.

   * **Ambientes de implantação qualificados** - Disponível somente quando você edita um pipeline de não produção. Se o pipeline for um pipeline de implantação, você deverá selecionar em quais ambientes ele deve ser implantado.
   * **Repositório** - Na lista suspensa, escolha o repositório Git que o pipeline usa como origem. O Cloud Manager cria código a partir do repositório escolhido aqui.

     >[!TIP]
     > 
     >Consulte [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Na lista suspensa, escolha de qual ramificação o pipeline deve compilar no repositório selecionado. O padrão é `main`. O pipeline usa a ramificação escolhida como origem para a compilação e a implantação. Se necessário, clique em **Atualizar** para atualizar a lista de ramificações disponíveis para o repositório selecionado. Use esta opção se uma ramificação criada recentemente não aparecer na lista.
   * **Estratégia de compilação**
      * **Compilação Completa** - Cria todos os módulos no repositório sempre
      * BETA **Compilação Inteligente** - Compila apenas módulos que foram alterados desde a última confirmação.<br>Saiba mais sobre [como usar o Smart Build em um pipeline de não produção](#about-smart-build).

        >[!IMPORTANT]
        >
        >O Smart Build está disponível somente para pipelines de Qualidade do código e pipelines de implantação do Código de pilha completa de desenvolvimento.

   * **Ignorar Configuração da Camada da Web** caixa de seleção - Quando marcada, o pipeline não implanta sua configuração da camada da Web.

1. Na seção **Pipeline**, se o pipeline for um pipeline de implantação, você poderá optar por executar uma fase de teste. Marque as opções que deseja habilitar nesta fase. Se nenhuma das opções for selecionada, a fase de teste não será exibida durante a execução do pipeline.

   * **Teste funcional do produto** - Execute [testes funcionais do produto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) no ambiente de desenvolvimento.
   * **Teste funcional personalizado** - Execute [testes funcionais personalizados](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) no ambiente de desenvolvimento.
   * **Teste de interface do usuário personalizada** - Execute [testes de interface do usuário personalizados](/help/implementing/cloud-manager/ui-testing.md) para aplicativos personalizados.
   * **Auditoria de Experiência** - Executar [Auditoria de Experiência](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![Pipeline de pilha completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Clique em **Salvar**.

O pipeline foi salvo e agora você pode [gerenciar seus pipelines]&#x200B;(managing-pipe
lines.md) no cartão **Pipelines** na página **Visão geral do programa**.

### Estou usando a implantação direcionada {#targeted-deployment}

Uma implantação direcionada implanta o código somente para partes selecionadas do aplicativo AEM. Nessa implantação, você pode optar por **Incluir** um dos seguintes tipos de código:

![Opções de implantação direcionada](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment1.png)

<!--
* **Config** - Configure settings for various features in your AEM environment.
  * See [Using Config Pipelines](/help/operations/config-pipeline.md) for a list of supported configurations, which include log forwarding, purge-related maintenance tasks, and various CDN configurations, and to manage them in your repository so they are deployed properly.
  * When running a targeted deployment pipeline, configurations are deployed, provided they are saved to the environment, repository, and branch you defined in the pipeline.
  * At any time, there can only be one config pipeline per environment.
* **Configure Edge Delivery Services config pipeline** - Edge Delivery Configuration Pipelines do not have separate development, staging, and production environments. In AEM as a Cloud Service, changes move through development, stage, and production tiers. In contrast, an Edge Delivery Configuration Pipeline applies its configuration directly to all Edge Delivery Sites domains registered in Cloud Manager. To learn more, see [Add an Edge Delivery Pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).
-->


* **Código de front-end** - Configure o JavaScript e o CSS para o front-end do seu aplicativo AEM.
   * Com os pipelines de front-end, é dada mais independência aos desenvolvedores de front-end e o processo de desenvolvimento pode ser acelerado.
   * Consulte o documento [Desenvolvimento de sites com o pipeline de front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber como esse processo funciona, além de algumas considerações a serem feitas para aproveitar ao máximo o potencial desse processo.
* **Configuração da Camada da Web** - Configure as propriedades do Dispatcher para armazenar, processar e entregar páginas da Web ao cliente.
   * Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) para obter mais detalhes.
   * Se existir um pipeline de código da Web para o ambiente selecionado, essa seleção será desabilitada.
   * Se um pipeline de pilha completa já for implantado em um ambiente, você ainda poderá criar um pipeline de configuração no nível da Web para esse mesmo ambiente. Quando você faz isso, o Cloud Manager ignora a configuração no nível da Web no pipeline de pilha completa.

     >[!NOTE]
     >
     >Os pipelines de nível da Web e de configuração não são compatíveis com repositórios privados. Consulte [Adicionando repositórios privados no Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md) para obter detalhes e a lista completa de limitações.

<!--
The steps to complete the creation of your non-production, targeted deployment pipeline are the same once you choose a deployment type.

1. Choose which deployment type you require.

![Targeted deployment options](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

1. Define the **Eligible Deployment Environments**.

   * If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
-->

1. Na seção **Código Source**, defina as seguintes opções:

   * **Repositório** - Essa opção define de qual repositório GIT o pipeline de não produção deve recuperar o código.

     >[!TIP]
     > 
     >Consulte [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código. Insira os primeiros caracteres do nome da ramificação e utilize o preenchimento automático deste campo. O recurso encontra as ramificações correspondentes que você pode selecionar.
   * **Localização do código**: essa opção define o caminho na ramificação do repositório selecionado do qual o pipeline deve recuperar o código.

<!--
   * **Pipeline** - For front-end non-production pipelines, you have the option to enable **[Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)**.
   
   ![Config pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)
-->

1. Se você habilitou a Auditoria de Experiência, clique em **Continuar** para avançar para a guia **Auditoria de Experiência**, na qual será possível definir os caminhos que sempre devem ser incluídos na Auditoria de Experiência.

   * Se você habilitou a **Auditoria de experiência**, consulte o documento [Auditoria de experiência](/help/implementing/cloud-manager/reports/report-experience-audit.md) para obter detalhes sobre como configurar.
   * Caso contrário, pule esta etapa.

1. Clique em **Salvar** para salvar o pipeline.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.


## Sobre o uso do Smart Build em um pipeline de não produção{#about-smart-build}

A **Compilação Inteligente** do Cloud Manager é uma estratégia de compilação otimizada para pipelines de não produção. O Smart Build reduz os tempos de criação ao armazenar em cache módulos e recriar apenas os módulos que foram alterados desde a última execução bem-sucedida. Os módulos inalterados são reutilizados do cache, enquanto apenas os módulos modificados e suas dependências são recriados, melhorando a eficiência dos workflows de desenvolvimento iterativos.

No momento, o Smart Build está disponível apenas para o seguinte:

* Pipelines de qualidade do código.
* Desenvolva pipelines de implantação de pilha completa.

>[!NOTE]
>
>A primeira execução após a ativação da Compilação inteligente se comporta como uma Compilação completa porque o cache está vazio.

O Smart Build é recomendado quando você tem o seguinte:
* Você está desenvolvendo e confirmando ativamente alterações incrementais frequentes.
* Seu projeto contém vários módulos Maven.
* As compilações completas estão demorando muito.

O Smart Build nem sempre é ideal quando você tem o seguinte:
* Sua build depende muito de plug-ins que executam operações fora do gráfico de dependência do Maven.
* Você precisa da validação completa de reconstrução em cada execução.

### Entender o desempenho da build{#smart-build-performance}

O ganho de desempenho com o uso do Smart Build depende de vários fatores, incluindo os seguintes:

* O número de módulos no projeto.
* A frequência e o escopo das alterações de código.
* A distribuição de dependências entre módulos.

Geralmente, projetos com muitos módulos independentes podem ver a maior melhoria.

### Recusa de cache por módulo{#smart-build-cache-optout}

O Smart Build fornece controle refinado que permite desativar o armazenamento em cache de módulos específicos. Essa capacidade é útil quando determinados módulos:

* Use plug-ins, como `exec-maven-plugin` ou `maven-antrun-plugin`.
* Executar operações de arquivo não rastreadas pelas dependências do Maven.
* O conteúdo em cache produz resultados inconsistentes.

### Desativar armazenamento em cache para um módulo{#smart-build-disable-caching}

Você pode adicionar a seguinte propriedade ao `pom.xml` do módulo afetado:

```xml
<properties>
  <maven.build.cache.enabled>false</maven.build.cache.enabled>
</properties>
```

Essa sintaxe força o módulo a ser recriado em cada execução de pipeline, enquanto outros módulos continuam a se beneficiar do armazenamento em cache.

### Limitações e considerações ao usar o Smart Build{#smart-build-limitations}

Lembre-se do seguinte ao usar o Smart Build:

* O Smart Build depende da análise de dependência do Maven.
* As alterações fora do gráfico de dependência não podem acionar recriações.
* Alguns plug-ins podem não ser totalmente compatíveis com o armazenamento em cache.
* Você pode voltar para a **Compilação completa** a qualquer momento editando o pipeline de não produção.

Se você encontrar um comportamento de compilação inesperado, considere desabilitar o cache de módulos específicos ou alternar temporariamente sua estratégia de compilação para **Compilação Completa**.

### Solução de problemas do Smart Build{#smart-build-troubleshoot}

| Problema | Soluções sugeridas |
| --- | --- |
| Os resultados da build são inconsistentes | · Desativar o armazenamento em cache para os módulos afetados.<br>· Verificar comportamento do plug-in (especialmente `exec`/`antrun` plug-ins). |
| Sem melhoria de desempenho | · Garantir que várias execuções tenham ocorrido (aquecimento de cache).<br>· Verifique se a maioria dos módulos está mudando com frequência. |
| Artefatos inesperados ou alterações ausentes | · Analisar se as alterações estão fora do rastreamento de dependência do Maven.<br>· Use **Compilação Completa** para verificação. |

Consulte [Adicionar um pipeline de não produção](#adding-non-production-pipeline) para habilitar o Smart Build.











<!--
## Add a non-production pipeline {#adding-non-production-pipeline}

Once you have set up your program and have at least one environment using the Cloud Manager UI, you are ready to add a non-production pipeline by following these steps.

1. Sign into Cloud Manager at [experiece.adobe.com](https://experience.adobe.com).
1. In the **Quick access** section, click **Experience Manager**.
1. In the left side panel, click **Cloud Manager**.
1. Select an organization that you want.
1. On the **My Programs** console, click a program. 

1. Access the **Pipelines** card from the Cloud Manager home screen. Click **+Add** and select **Add Non-Production Pipeline**. 

   ![Add non-production pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. On the **Configuration** tab of the **Add Non-Production Pipeline** dialog, select the type of non-production pipeline you with to add.

   * **Code Quality Pipeline** - Create a pipeline that builds your code, runs unit tests, and evaluates code quality but does NOT deploy.
   * **Deployment Pipeline** - Create a pipeline that builds your code, runs unit tests, evaluates code quality, and deploys to an environment.

   ![Add Non-Production pipeline dialog](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Provide a **Non-Production Pipeline Name** to identify your pipeline along with the following additional information.

   * **Deployment Trigger** - You have the following options when defining the deployment triggers to start the pipeline.
   
     * **Manual** - Use this option to start the pipeline manually.
     * **On Git Changes** - This option starts the CI/CD pipeline whenever commits are added to the configured Git branch. With this option, you can still start the pipeline manually as required.

1. If you choose to create a **Deployment Pipeline**, you must also define the **Important Metric Failures Behavior**.

   * **Ask every time** - This behavior is the default setting and requires manual intervention on any important failure.
   * **Fail Immediately** - If selected, the pipeline is canceled whenever an important failure occurs. It is essentially emulating a user manually rejecting each failure.
   * **Continue Immediately** - If selected, the pipeline procedes automatically whenever an important failure occurs. It is essentially emulating a user manually approving each failure.

1. Click **Continue**.

1. On the **Source Code** tab of the **Add Non-Production Pipeline** dialog, you must select which type of code the pipeline should process.

   * **[Full Stack Code](#full-stack-code)**
   * **[Targeted deployment](#targeted-deployment)**

See [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) for more information about the types of pipelines.

The steps to complete the creation of your non-production pipeline vary depending on the type of source code you selected. Follow the links above to jump to the next section of this document so you can complete the configuration of your pipeline.

### Full Stack Code {#full-stack-code}

A full-stack code pipeline simultaneously deploys back-end and front-end code builds containing one or more AEM server applications along with HTTPD/Dispatcher configuration.

>[!NOTE]
>
>If a full-stack code pipeline exists for the selected environment, this selection is disabled.

To finish the configuration of the full-stack code non-production pipeline, follow these steps.

1. On the **Source Code** tab, you must define the following options.

   * **Eligible Deployment Environments** - If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
   * **Repository** - This option defines from which git repo that the pipeline should retrieve the code.

   >[!TIP]
   > 
   >See [Adding and Managing Repositories](/help/implementing/cloud-manager/managing-code/managing-repositories.md) so you can learn how to add and manage repositories in Cloud Manager.

   * **Git Branch** - This option defines from which branch in the selected pipeline should retrieve the code.
     * Enter the first few characters of the branch name and the auto-complete feature of this field. It helps you find the matching branches that you can select.
   * **Ignore Web Tier Configuration** - When checked, the pipeline does not deploy your web tier configuration.
   * **Pipeline** - If your pipeline is a deployment pipeline, you can choose to run a testing phase. Check the options that you want to enable in this phase. If none of the options are selected, the testing phase is not displayed during the pipeline's run.

     * **Product Functional Testing** - Execute [product functional tests](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) against the development environment.
     * **Custom Functional Testing** - Execute [custom functional tests](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) against the development environment.
     * **Custom UI Testing** - Execute [custom UI tests](/help/implementing/cloud-manager/ui-testing.md) for custom applications.
     * **Experience Audit** - Execute [Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![Full-stack pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Click **Save**.

The pipeline is saved and you can now [manage your pipelines](managing-pipelines.md) on the **Pipelines** card on the **Program Overview** page.

-->



## Excluir pacotes do Dispatcher {#exclude-dispatcher-packages}

Se quiser que os pacotes do Dispatcher sejam criados no pipeline, mas não forem carregados para criar armazenamento, desative a publicação. Isso pode reduzir o tempo de execução do pipeline.

Adicione a seguinte configuração ao arquivo `pom.xml` do projeto para desabilitar a publicação de pacotes do Dispatcher. Defina uma variável de ambiente no contêiner de compilação do Cloud Manager para sinalizar quando ignorar os pacotes do Dispatcher. O pipeline lê esse sinalizador e os ignora adequadamente.

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>!true</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
