---
title: Configuração de pipeline de não produção
description: Saiba como configurar pipelines de não produção para testar a qualidade do código antes de implantar em ambientes de produção.
index: true
source-git-commit: 536740f8bb5e54a3a831a22f4e6d237863aea324
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 1%

---


# Configuração de pipeline de não produção {#configuring-non-production-pipelines}

Saiba como configurar pipelines de não produção para testar a qualidade do código antes de implantar em ambientes de produção.

## Pipelines de não produção {#non-production-pipelines}

Além de [gasodutos de produção](#configuring-production-pipelines.md) que é implantada em ambientes de preparo e produção, também é possível configurar pipelines não de produção para validar seu código.

Existem dois tipos de gasodutos não relacionados à produção:

* **Pipelines de qualidade do código** - Esses executam verificações de qualidade de código no código em uma ramificação git e executa as etapas de qualidade de código e criação.
* **Pipelines de implantação** - Além de executar as etapas de criação e qualidade do código, como os pipelines de qualidade do código, esses pipelines implantam o código em um ambiente não relacionado à produção.

>[!NOTE]
>
>Você pode [editar configurações de pipeline](managing-pipelines.md) após a configuração inicial.

## Adicionar um novo pipeline de não produção {#adding-non-production-pipeline}

Depois de configurar seu programa e ter pelo menos um ambiente usando a interface do usuário do Cloud Manager, você estará pronto para adicionar um pipeline de não produção seguindo essas etapas.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Acesse o **Pipelines** na tela inicial do Cloud Manager. Clique em **+Adicionar** e selecione **Adicionar pipeline de não-produção**.

   ![Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. No **Configuração** da guia **Adicionar pipeline de não-produção** , selecione o tipo de pipeline de não produção com o qual você deseja adicionar, **Pipeline de qualidade do código** ou **Pipeline de implantação**.

   ![Caixa de diálogo Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Forneça uma **Nome do pipeline de não produção** para identificar o pipeline junto com as seguintes informações adicionais.

   * **Acionador da implantação** - Você tem as seguintes opções ao definir os acionadores de implantação para iniciar o pipeline.

      * **Manual** - Use essa opção para iniciar manualmente o pipeline.
      * **Nas alterações no Git** - Essas opções iniciam o pipeline de CI/CD sempre que os commits são adicionados à ramificação git configurada. Com essa opção, ainda é possível iniciar o pipeline manualmente, conforme necessário.
   * **Comportamento de falhas importantes da métrica** - Durante a configuração ou edição do pipeline, a variável **Gerenciador de implantação** tem a opção de definir o comportamento do pipeline quando uma falha importante é encontrada em qualquer uma das portas de qualidade. Você tem as seguintes opções.

      * **Perguntar sempre** - Esta é a configuração padrão e requer intervenção manual em qualquer falha importante.
      * **Falhar imediatamente** - Se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que rejeita manualmente cada falha.
      * **Continuar imediatamente** - Se selecionado, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que aprova manualmente cada falha.


1. Clique em **Continuar**.

1. No **Código fonte** da guia **Adicionar pipeline de não-produção** , você deve selecionar o tipo de código que o pipeline deve processar.

   * **[Código de front-end](#front-end-code)**
   * **[Código de pilha completo](#full-stack-code)**
   * **[Configuração da camada da Web](#web-tier-config)**

As etapas para concluir a criação do pipeline de não produção variam de acordo com a opção para **Código fonte** você selecionou. Siga os links acima para ir até a próxima seção deste documento para concluir a configuração do pipeline.

### Código de front-end {#front-end-code}

Um pipeline de código front-end implanta compilações de código front-end contendo um ou mais aplicativos de interface do usuário do lado do cliente. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obter mais informações sobre esse tipo de pipeline.

Para concluir a configuração do pipeline de não produção do código front-end, siga estas etapas.

1. No **Código fonte** , você deve definir as seguintes opções.

   * **Ambientes de implantação qualificados** - Se o pipeline for um pipeline de implantação, você deve selecionar para quais ambientes ele deve implantar.
   * **Repositório** - Essa opção define de qual Git repo o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte o documento [Adicionar e gerenciar repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
   * **Localização do código** - Essa opção define o caminho na ramificação do acordo de recompra selecionado a partir do qual o pipeline deve recuperar o código.

   ![Gasoduto front-end](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. Clique em **Salvar**.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no **Pipelines** no cartão **Visão geral do programa** página.

### Código de pilha completo {#full-stack-code}

Um pipeline de código de pilha completa implanta simultaneamente builds de código back-end e front-end contendo um ou mais aplicativos de servidor AEM juntamente com a configuração HTTPD/Dispatcher. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) para obter mais informações sobre esse tipo de pipeline.

>[!NOTE]
>
>Se um pipeline de código de pilha completo já existir para o ambiente selecionado, essa seleção será desativada.

Para concluir a configuração do pipeline de não produção do código de pilha completo, siga estas etapas.

1. No **Código fonte** , você deve definir as seguintes opções.

   * **Ambientes de implantação qualificados** - Se o pipeline for um pipeline de implantação, você deve selecionar para quais ambientes ele deve implantar.
   * **Repositório** - Essas opções definem a partir de qual Git repo o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte o documento [Adicionar e gerenciar repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
   * **Ignorar configuração da camada da Web** -

   ![pipeline de pilha completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Clique em **Salvar**.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no **Pipelines** no cartão **Visão geral do programa** página.

### Configuração da camada da Web {#web-tier-config}

Um pipeline de configuração de camada da Web implanta configurações HTTPD/Dispatcher. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) para obter mais informações sobre esse tipo de pipeline.

>[!NOTE]
>
>Se um pipeline de código de camada da Web já existir para o ambiente selecionado, essa seleção será desativada.

Para concluir a configuração do pipeline de não produção do código de pilha completo, siga estas etapas.

1. No **Código fonte** , você deve definir as seguintes opções.

   * **Ambientes de implantação qualificados** - Se o pipeline for um pipeline de implantação, você deve selecionar para quais ambientes ele deve implantar.
   * **Repositório** - Essa opção define de qual Git repo o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte o documento [Adicionar e gerenciar repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
   * **Localização do código** - Essa opção define o caminho na ramificação do acordo de recompra selecionado a partir do qual o pipeline deve recuperar o código.
      * Para pipelines de configuração da camada da Web, esse é geralmente o caminho que contém `conf.d`, `conf.dispatcher.d`e `opt-in` diretórios.
      * Por exemplo, se a estrutura do projeto foi gerada da variável [Arquétipo de projeto AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) o caminho seria `/dispatcher/src`.

   ![pipeline de camada da Web](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. Clique em **Salvar**.

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
