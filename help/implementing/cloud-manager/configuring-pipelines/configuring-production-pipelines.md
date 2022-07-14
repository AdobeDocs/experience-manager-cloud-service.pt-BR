---
title: Configuração de pipeline de produção
description: Saiba como configurar pipelines de produção para criar e implantar seu código em ambientes de produção.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---

# Configuração de um pipeline de produção {#configure-production-pipeline}

Saiba como configurar pipelines de produção para criar e implantar seu código em ambientes de produção. Um pipeline de Produção implanta o código primeiro no ambiente de Preparo e, após a aprovação, implanta o mesmo código no ambiente de Produção.

Um usuário deve ter a variável **[Gerenciador de implantação](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar pipelines de produção.

>[!NOTE]
>
>Um pipeline de produção não pode ser configurado até que a criação do programa seja concluída, um repositório Git tenha pelo menos uma ramificação e um conjunto de ambientes de produção e de preparo seja criado.

Antes de começar a implantar seu código, você deve definir as configurações de pipeline do [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Você pode [editar configurações de pipeline](managing-pipelines.md) após a configuração inicial.

## Adicionar um novo pipeline de produção {#adding-production-pipeline}

Depois de configurar seu programa e ter pelo menos um ambiente usando a variável [!UICONTROL Cloud Manager] Na interface do usuário, você está pronto para adicionar um pipeline de produção seguindo essas etapas.

>[!TIP]
>
>Antes de configurar um pipeline de front-end, consulte o [AEM Jornada de criação rápida de site](/help/journey-sites/quick-site/overview.md) para obter um guia completo com a ferramenta de criação rápida de sites AEM fácil de usar. Essa jornada ajudará você a simplificar o desenvolvimento de front-end do seu Site de AEM, permitindo que você personalize rapidamente seu site sem conhecimento AEM back-end.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o **Pipelines** do cartão **Visão geral do programa** e clique em **Adicionar** para selecionar **Adicionar pipeline de produção**.

   ![O cartão Pipelines na visão geral do Gerenciador de programas](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. O **Adicionar pipeline de produção** será exibida. Forneça uma **Nome do pipeline** para identificar o pipeline junto com as seguintes opções. Clique em **Continuar**.

   **Acionador da implantação** - Você tem as seguintes opções ao definir os acionadores de implantação para iniciar o pipeline.

   * **Manual** - Use essa opção para iniciar manualmente o pipeline.
   * **Nas alterações no Git** - Essas opções iniciam o pipeline de CI/CD sempre que os commits são adicionados à ramificação git configurada. Com essa opção, ainda é possível iniciar o pipeline manualmente, conforme necessário.

   **Comportamento de falhas importantes da métrica** - Durante a configuração ou edição do pipeline, a variável **Gerenciador de implantação** tem a opção de definir o comportamento do pipeline quando uma falha importante é encontrada em qualquer uma das portas de qualidade. As opções disponíveis são:

   * **Perguntar sempre** - Esta é a configuração padrão e requer intervenção manual em qualquer falha importante.
   * **Falhar imediatamente** - Se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que rejeita manualmente cada falha.
   * **Continuar imediatamente** - Se selecionado, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que aprova manualmente cada falha.

   ![Configuração do pipeline de produção](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. No **Código fonte** é necessário definir onde o pipeline deve recuperar seu código e o tipo de código que ele é.

   * **[Código de front-end](#front-end-code)**
   * **[Código de pilha completo](#full-stack-code)**
   * **[Configuração da camada da Web](#web-tier-config)**

As etapas para concluir a criação do pipeline de produção variam dependendo da opção para **Código fonte** você selecionou. Siga os links acima para ir até a próxima seção deste documento para concluir a configuração do pipeline.

### Código de front-end {#front-end-code}

Um pipeline de código front-end implanta compilações de código front-end contendo um ou mais aplicativos de interface do usuário do lado do cliente. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obter mais informações sobre esse tipo de pipeline.

Para concluir a configuração do pipeline de produção do código front-end, siga estas etapas.

1. No **Código fonte** , você deve definir as seguintes opções.

   * **Repositório** - Essa opção define de qual Git repo o pipeline deve recuperar o código.
   >[!TIP]
   > 
   >Consulte o documento [Adicionar e gerenciar repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e o recurso de preenchimento automático desse campo encontrará as ramificações correspondentes para ajudá-lo a selecionar.
   * **Localização do código** - Essa opção define o caminho na ramificação do acordo de recompra selecionado a partir do qual o pipeline deve recuperar o código.
   * **Pausar antes de implantar em produção** - Essa opção pausa o pipeline antes de implantar na produção.

   ![Código front-end](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. Clique em **Salvar** para salvar o pipeline.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no **Pipelines** no cartão **Visão geral do programa** página.

### Código de pilha completo {#full-stack-code}

Um pipeline de código de pilha completa implanta simultaneamente builds de código back-end e front-end contendo um ou mais aplicativos de servidor AEM juntamente com a configuração HTTPD/Dispatcher. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) para obter mais informações sobre esse tipo de pipeline.

>[!NOTE]
>
>Se um pipeline de código de pilha completo já existir para o ambiente selecionado, essa seleção será desativada.

Para concluir a configuração do pipeline de produção do código de pilha completo, siga estas etapas.

1. No **Código fonte** , você deve definir as seguintes opções.

   * **Repositório** - Essa opção define de qual Git repo o pipeline deve recuperar o código.
   >[!TIP]
   > 
   >Consulte o documento [Adicionar e gerenciar repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e o recurso de preenchimento automático desse campo encontrará as ramificações correspondentes para ajudá-lo a selecionar.
   * **Localização do código** - Essa opção define o caminho na ramificação do acordo de recompra selecionado a partir do qual o pipeline deve recuperar o código.
   * **Pausar antes de implantar em produção** - Essa opção pausa o pipeline antes de implantar na produção.
   * **Programado** - Essa opção permite que o usuário habilite a implantação de produção agendada.

   ![Código de pilha completo](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Clique em **Continuar** para avançar para a **Auditoria de experiência** , onde é possível definir os caminhos que devem ser sempre incluídos na Auditoria de experiência.

   ![Adicionar auditoria de experiência](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Forneça um caminho a ser incluído na Auditoria de experiência.

   * Os caminhos da página devem começar com `/`.
   * Por exemplo, se você deseja incluir `https://wknd.site/us/en/about-us.html` na Auditoria de experiência, insira o caminho `/us/en/about-us.html`.

   ![Definição de um caminho para a Auditoria de experiência](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. Clique em **Adicionar página** e o caminho será preenchido automaticamente com o endereço do ambiente e adicionado à tabela de caminhos.

   ![Salvar caminho para a tabela](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. Continue a adicionar caminhos, conforme necessário, repetindo as duas etapas anteriores.

   * É possível adicionar no máximo 25 caminhos.
   * Se você não definir nenhum caminho, a página inicial do site será incluída na Auditoria de experiência por padrão.

1. Clique em **Salvar** para salvar o pipeline.

Os caminhos configurados para a Auditoria de experiência serão submetidos ao serviço e avaliados de acordo com os testes de desempenho, acessibilidade, SEO (Otimização de mecanismo de pesquisa), prática recomendada e PWA (Aplicativo web progressivo) quando o pipeline for executado. Consulte [Noções básicas dos resultados da auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no **Pipelines** no cartão **Visão geral do programa** página.

### Configuração da camada da Web {#web-tier-config}

Um pipeline de configuração de camada da Web implanta configurações HTTPD/Dispatcher. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) para obter mais informações sobre esse tipo de pipeline.

Para concluir a configuração do pipeline de produção do código de pilha completo, siga estas etapas.

1. No **Código fonte** , você deve definir as seguintes opções.

   * **Repositório** - Essa opção define de qual Git repo o pipeline deve recuperar o código.
   >[!TIP]
   > 
   >Consulte o documento [Adicionar e gerenciar repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e o recurso de preenchimento automático desse campo encontrará as ramificações correspondentes para ajudá-lo a selecionar.
   * **Localização do código** - Essa opção define o caminho na ramificação do acordo de recompra selecionado a partir do qual o pipeline deve recuperar o código.
      * Para pipelines de configuração da camada da Web, esse é geralmente o caminho que contém `conf.d`, `conf.dispatcher.d`e `opt-in` diretórios.
      * Por exemplo, se a estrutura do projeto foi gerada da variável [Arquétipo de projeto AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) o caminho seria `/dispatcher/src`.
   * **Pausar antes de implantar em produção** - Essa opção pausa o pipeline antes de implantar na produção.
   * **Programado** - Essa opção permite que o usuário habilite a implantação de produção agendada.

   ![Código da camada da Web](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. Clique em **Salvar** para salvar o pipeline.

>[!NOTE]
>
>Se você tiver um pipeline de pilha completa existente implantando em um ambiente, criar um pipeline de configuração de camada da Web para o mesmo ambiente fará com que a configuração de camada da Web existente no pipeline de pilha completa seja ignorada.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no **Pipelines** no cartão **Visão geral do programa** página.

## Ignorar pacotes do Dispatcher {#skip-dispatcher-packages}

Se quiser que os pacotes do dispatcher sejam criados como parte do pipeline, mas não quiser que eles sejam publicados para criar armazenamento, desative a publicação, o que pode reduzir a duração da execução do pipeline.

A seguinte configuração para desativar a publicação de pacotes do dispatcher deve ser adicionada por meio do projeto `pom.xml` arquivo. É baseada em uma variável de ambiente, que serve como um sinalizador que pode ser definido no contêiner de build do Cloud Manager para definir quando os pacotes de dispatcher devem ser ignorados.

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
