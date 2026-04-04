---
title: Adicionar um pipeline de produção
description: Saiba como adicionar um pipeline de produção para compilar e implantar seu código em ambientes de produção.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: aa8aba7f798e251c8a25ee247402e23517707e88
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 25%

---


# Adicionar um pipeline de produção {#configure-production-pipeline}

Saiba como configurar pipelines de produção para compilar e implantar seu código em ambientes de produção. Um pipeline de produção primeiro implanta o código no ambiente de preparo. Na aprovação, ele implanta o mesmo código no ambiente de produção.

Um usuário deve ter a função **[Gerente de implantação](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar pipelines de produção.

>[!NOTE]
>
>Um pipeline de produção não pode ser configurado até que o seguinte tenha acontecido:
>
>* O programa é criado.
>* O repositório Git tem pelo menos uma ramificação.
>* Os ambientes de produção e de preparo são criados.

Antes de começar a implantar seu código, defina as configurações de pipeline do [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Você poderá [editar as configurações do pipeline](managing-pipelines.md) após a configuração inicial.

## Adicionar um novo pipeline de produção {#adding-production-pipeline}

Depois de configurar seu programa e ter pelo menos um ambiente usando a interface do usuário do [!UICONTROL Cloud Manager], você estará pronto para adicionar um pipeline de produção seguindo essas etapas.

>[!TIP]
>
>Antes de configurar um pipeline de front-end, consulte a [Jornada de Criação rápida de sites do AEM](/help/journey-sites/quick-site/overview.md) para obter um guia completo sobre a ferramenta simples de Criação rápida de sites do AEM. Esta jornada pode ajudá-lo a simplificar o desenvolvimento de front-end do seu site do AEM, permitindo que você personalize seu site rapidamente sem conhecimento de back-end no AEM.

1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
1. Na seção **Acesso rápido**, clique em **Experience Manager**.
1. No painel lateral esquerdo, clique em **Cloud Manager**.
1. Selecione a organização desejada.
1. No console **Meus Programas**, clique em um programa.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Navegue até o cartão **Pipelines** da página **Visão geral do programa** e clique em **Adicionar** para selecionar **Adicionar pipeline de produção**.

   ![O cartão Pipelines na visão geral do Gerenciador de programas](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. A caixa de diálogo **Adicionar pipeline de produção** será exibida. Forneça um **Nome do pipeline** para identificar o pipeline junto com as opções a seguir. Clique em **Continuar**.

   **Acionador da implantação** - Você tem as seguintes opções ao definir os acionadores de implantação para iniciar o pipeline.

   * **Manual** - Iniciar o pipeline manualmente.
   * **Sobre Alterações do Git** - Inicia o pipeline de CI/CD sempre que confirmações são adicionadas à ramificação Git configurada. Com essa opção, ainda é possível iniciar o pipeline manualmente, conforme necessário.

   **Comportamento de falhas importantes da métrica** - Durante a configuração ou edição do pipeline, o **Gerente de implantação** tem a opção de definir o comportamento do pipeline quando uma falha importante é encontrada em qualquer um dos quality gates (portais de qualidade). As opções disponíveis são:

   * **Perguntar sempre** - Configuração padrão. Requer intervenção manual em qualquer falha importante.
   * **Falhar imediatamente**: se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. Esse processo é basicamente semelhante a um usuário que rejeita manualmente cada falha.
   * **Continuar imediatamente** - Se selecionado, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. Esse processo é basicamente semelhante a um usuário que aprova manualmente cada falha.

   ![Configuração do pipeline de produção](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. Na guia **Código Source**, selecione o tipo de código que o pipeline deve processar.

   * **[Estou usando o Código de Pilha Completa](#full-stack-code)**
   * **[Configurar um pipeline de implantação direcionado](#targeted-deployment)**

Consulte [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obter mais informações sobre os tipos de pipelines.

As etapas para concluir a criação do pipeline de produção variam de acordo com o tipo de código-fonte selecionado. Siga os links acima para acessar a próxima seção deste documento e concluir a configuração do pipeline.

### Estou usando um código de pilha completa {#full-stack-code}

Um pipeline de código de pilha completa implanta simultaneamente compilações de código de back-end e front-end contendo um ou mais aplicativos de servidor do AEM, juntamente com a configuração HTTPD/Dispatcher.

>[!NOTE]
>
>Se um pipeline de código de pilha completa já existir para o ambiente selecionado, essa seleção ficará desativada.

**Para configurar um pipeline de código de pilha completa:**

1. Na guia **Código Source**, defina as seguintes opções.

   * **Repositório** - Define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte [Adicionar e gerenciar repositórios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Na lista suspensa, escolha de qual ramificação o pipeline deve compilar no repositório selecionado. O padrão é `main`. O pipeline usa a ramificação escolhida como origem para a compilação e a implantação. Se necessário, clique em **Atualizar** para atualizar a lista de ramificações disponíveis para o repositório selecionado. Use esta opção se uma ramificação criada recentemente não aparecer na lista.
   * **Estratégia de compilação**
      * **Compilação Completa** - Cria todos os módulos no repositório sempre
      * BETA **Compilação Inteligente** - Compila apenas módulos que foram alterados desde a última confirmação.<br>Saiba mais sobre [como usar o Smart Build em um pipeline de não produção](#about-smart-build-non-production-pipeline).

        >[!IMPORTANT]
        >
        >O Smart Build está disponível somente para pipelines de Qualidade do código e pipelines de implantação do Código de pilha completa de desenvolvimento.
   * **Ignorar configuração no nível da Web**: quando essa opção está marcada, o pipeline não implanta sua configuração no nível da Web.
   * **Pausar antes de implantar na Produção** - Pausa o pipeline antes de implantar na produção.
   * **Agendado** - Permite que o usuário habilite a implantação de produção agendada.

   ![Código de pilha completa](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Clique em **Continuar** para avançar para a guia **Auditoria de experiência**, na qual é possível definir os caminhos que devem ser sempre incluídos na Auditoria de experiência.

   ![Adicionar auditoria de experiência](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Forneça caminhos a serem incluídos na Auditoria de experiência.

   * Consulte [Teste de auditoria de experiência](/help/implementing/cloud-manager/reports/report-experience-audit.md#configuration) para obter detalhes.

1. Clique em **Salvar** para salvar o pipeline.

Quando o pipeline é executado, os caminhos configurados para a Auditoria de experiência são enviados e avaliados com base em desempenho, acessibilidade, SEO, práticas recomendadas e testes do PWA. Para obter mais detalhes, consulte [Noções básicas sobre os resultados da auditoria de experiência](/help/implementing/cloud-manager/reports/report-experience-audit.md).

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

### Estou usando a implantação direcionada {#targeted-deployment}

Uma implantação direcionada implanta o código somente para partes selecionadas do aplicativo AEM. Nessa implantação, você pode optar por **Incluir** um dos seguintes tipos de código:

* **Configuração** - Defina as configurações de vários recursos no seu ambiente do AEM.
   * Consulte [Uso dos Pipelines de Configuração](/help/operations/config-pipeline.md) para obter uma lista de configurações com suporte, que incluem encaminhamento de logs, tarefas de manutenção relacionadas à limpeza e várias configurações de CDN, além de gerenciá-las no repositório para que sejam implantadas corretamente.
   * Ao executar um pipeline de implantação direcionada, as configurações são implantadas, desde que sejam salvas no ambiente, repositório e ramificação definidos no pipeline.
   * Em um dado momento, somente pode haver um pipeline de configuração por ambiente.
* **Configurar pipeline de configuração do Edge Delivery Services** - Os Pipelines de Configuração do Edge Delivery não têm ambientes de desenvolvimento, preparo e produção separados. No AEM as a Cloud Service, as alterações percorrem níveis de desenvolvimento, preparo e produção. Por outro lado, um Pipeline de configuração do Edge Delivery aplica sua configuração diretamente a todos os domínios do Edge Delivery Sites registrados no Cloud Manager. Para saber mais, consulte [Adicionar um pipeline de Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).
* **Código de front-end** - Configure o JavaScript e o CSS para o front-end do seu aplicativo AEM.
   * Com os pipelines de front-end, é dada mais independência aos desenvolvedores de front-end e o processo de desenvolvimento pode ser acelerado.
   * Consulte o documento [Desenvolvimento de sites com o pipeline de front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber como esse processo funciona, além de algumas considerações a serem feitas para aproveitar ao máximo o potencial desse processo.
* **Configuração da Camada da Web** - Configure as propriedades do Dispatcher para armazenar, processar e entregar páginas da Web ao cliente.
   * Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) para obter mais detalhes.
   * Se existir um pipeline de código da Web para o ambiente selecionado, essa seleção será desabilitada.
   * Se você criar um pipeline de configuração no nível da Web para um ambiente com um pipeline de pilha completa existente, a configuração no pipeline de pilha completa será ignorada. Essa alteração afeta somente a configuração no nível da Web nesse ambiente.

>[!NOTE]
>
>Os pipelines de nível da Web e de configuração não são compatíveis com repositórios privados. Consulte [Adicionando repositórios privados no Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md) para obter detalhes e a lista completa de limitações.

**Para configurar um pipeline de implantação direcionada:**

1. Escolha o tipo de implantação necessário.

![Opções de implantação direcionada](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-targeted-deployment.png)

1. Defina os **Ambientes de implantação qualificados**.

   * Se o pipeline for um pipeline de implantação, você deverá selecionar em quais ambientes ele deve ser implantado.

1. Em **Source Code**, defina as seguintes opções:

   * **Repositório**: essa opção define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git**: essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e utilize o preenchimento automático deste campo. O recurso encontra as ramificações correspondentes que você pode selecionar.
   * **Localização do código** - Essa opção define o caminho na ramificação do repositório selecionado do qual o pipeline deve recuperar o código.
   * **Pausar antes de implantar na produção** - Essa opção pausa o pipeline antes de implantar na produção.
   * **Agendado** - Permite que o usuário habilite a implantação de produção agendada. Disponível somente para implantações direcionadas no nível da Web.

   ![Configurar pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. Clique em **Salvar**.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

## BETA: sobre o uso do Smart Build em um pipeline de produção{#about-smart-build-production-pipeline}

A **Compilação Inteligente** do Cloud Manager é uma estratégia de compilação otimizada para pipelines de produção. O Smart Build reduz os tempos de criação ao armazenar em cache módulos e recriar apenas os módulos que foram alterados desde a última execução bem-sucedida. Os módulos inalterados são reutilizados do cache, enquanto apenas os módulos modificados e suas dependências são recriados, melhorando a eficiência dos workflows de desenvolvimento iterativos.

>[!NOTE]
>
>Interessado nesse beta? Envie um email para [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) com sua ID organizacional e ID do programa da Adobe.

>[!IMPORTANT]
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
* Você pode voltar para a **Compilação completa** a qualquer momento editando o pipeline de produção.

Se você encontrar um comportamento de compilação inesperado, considere desabilitar o cache de módulos específicos ou alternar temporariamente sua estratégia de compilação para **Compilação Completa**.

### Solução de problemas do Smart Build{#smart-build-troubleshoot}

| Problema | Soluções sugeridas |
| --- | --- |
| Os resultados da build são inconsistentes | · Desativar o armazenamento em cache para os módulos afetados.<br>· Verificar comportamento do plug-in (especialmente `exec`/`antrun` plug-ins). |
| Sem melhoria de desempenho | · Garantir que várias execuções tenham ocorrido (aquecimento de cache).<br>· Verifique se a maioria dos módulos está mudando com frequência. |
| Artefatos inesperados ou alterações ausentes | · Analisar se as alterações estão fora do rastreamento de dependência do Maven.<br>· Use **Compilação Completa** para verificação. |

Consulte [Adicionar um pipeline de produção](#adding-production-pipeline) para habilitar o Smart Build.

## Ignorar pacotes do Dispatcher {#skip-dispatcher-packages}

Para criar pacotes do Dispatcher no pipeline sem publicá-los para criar armazenamento, você pode desativar a opção de publicação. Isso pode ajudar a reduzir o tempo de execução do pipeline.

A configuração a seguir para desabilitar a publicação de pacotes do Dispatcher deve ser adicionada por meio do arquivo de projeto `pom.xml`. Uma variável de ambiente serve como um sinalizador definido no contêiner de criação do Cloud Manager para determinar quando ignorar os pacotes do Dispatcher.

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>[!NOTE]rue</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
