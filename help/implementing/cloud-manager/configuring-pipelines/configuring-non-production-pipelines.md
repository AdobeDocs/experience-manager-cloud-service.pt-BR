---
title: Configurar pipelines de não produção
description: Saiba como configurar pipelines de não produção para testar a qualidade do código antes de implantar em ambientes de produção.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: aac397310babe1aa1e950c176459beaf665b72ce
workflow-type: ht
source-wordcount: '1369'
ht-degree: 100%

---


# Configurar pipelines de não produção {#configuring-non-production-pipelines}

Saiba como configurar pipelines de não produção para testar a qualidade do código antes de implantar em ambientes de produção.

## Pipelines de não produção {#non-production-pipelines}

Além de [pipelines de produção](#configuring-production-pipelines.md), que são implantados em ambientes de preparo e produção, também é possível configurar pipelines de não produção para validar seu código.

Existem dois tipos de pipelines de não produção:

* **Pipelines de qualidade do código** - Esses executam verificações de qualidade do código em uma ramificação Git e executam as etapas de qualidade do código e compilação.
* **Pipelines de implantação** - Além de executar as etapas de compilação e qualidade do código como os pipelines de qualidade do código, esses pipelines implantam o código em um ambiente de não produção.

>[!NOTE]
>
>Você poderá [editar as configurações do pipeline](managing-pipelines.md) após a configuração inicial.

## Adicionar um novo pipeline de não produção {#adding-non-production-pipeline}

Depois de configurar seu programa e ter pelo menos um ambiente usando a interface do usuário do Cloud Manager, você estará pronto para adicionar um pipeline de não produção seguindo essas etapas.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse o cartão **Pipelines** na tela inicial do Cloud Manager. Clique em **+Adicionar** e selecione **Adicionar pipeline de não produção**.

   ![Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. Na guia **Configuração** da caixa de diálogo **Adicionar pipeline de não produção**, selecione o tipo de pipeline de não produção que você deseja adicionar.

   * **Pipeline de qualidade do código**: cria um pipeline que gera o seu código, executa testes de unidade e avalia a qualidade do código; porém, ele NÃO realiza implantações.
   * **Pipeline de implantação**: cria um pipeline que gera o seu código, executa testes de unidade, avalia a qualidade do código e implanta em um ambiente.

   ![Caixa de diálogo Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Forneça um **Nome do pipeline de não produção** para identificar o pipeline junto com as informações adicionais a seguir.

   * **Acionador da implantação** - Você tem as seguintes opções ao definir os acionadores de implantação para iniciar o pipeline.

      * **Manual** - Use essa opção para iniciar manualmente o pipeline.
      * **Quando o Git é alterado** - Essas opções iniciam o pipeline de CI/CD sempre que confirmações são adicionadas à ramificação Git configurada. Com essa opção, ainda é possível iniciar o pipeline manualmente, conforme necessário.

1. Se optar por criar um **Pipeline de implantação**, você também precisará definir a variável **Comportamento de falhas de métricas importantes**.

   * **Sempre perguntar** - Essa é a configuração padrão e requer intervenção manual em qualquer falha importante.
   * **Falhar imediatamente** - Se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. É como emular um usuário que rejeita manualmente cada falha.
   * **Continuar imediatamente** - Se selecionado, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. É como emular um usuário que aprova manualmente cada falha.

1. Clique em **Continuar**.

1. Na guia **Código fonte** da caixa de diálogo **Adicionar pipeline de não produção**, você deve selecionar o tipo de código que o pipeline deve processar.

   * **[Código de front-end](#front-end-code)**
   * **[Código de pilha completa](#full-stack-code)**
   * **[Configuração no nível da Web](#web-tier-config)**

As etapas para concluir a criação do pipeline de não produção variam de acordo com a opção de **Código-fonte** que você selecionou. Siga os links acima para ir até a próxima seção deste documento para concluir a configuração do pipeline.

### Código de front-end {#front-end-code}

Um pipeline de código front-end implanta compilações de código de front-end contendo um ou mais aplicativos de interface do usuário do lado do cliente. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obter mais informações sobre esse tipo de pipeline.

Para concluir a configuração do pipeline de não produção do código de front-end, siga estas etapas.

1. Na guia **Código-fonte**, você deve definir as opções a seguir.

   * **Ambientes de implantação qualificados** - Se o pipeline for um pipeline de implantação, você deve selecionar em quais ambientes ele deve ser implantado.
   * **Repositório** - Essa opção define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte o documento [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e o recurso de preenchimento automático do campo localizará as ramificações correspondentes para ajudá-lo em sua seleção.
   * **Localização do código** - Essa opção define o caminho na ramificação do repositório selecionado do qual o pipeline deve recuperar o código.

   ![Pipeline de front-end](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. Clique em **Salvar**.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

### Código de pilha completa {#full-stack-code}

Um pipeline de código de pilha completa implanta simultaneamente compilações de código de back-end e front-end contendo um ou mais aplicativos de servidor do AEM, juntamente com a configuração HTTPD/Dispatcher. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) para obter mais informações sobre esse tipo de pipeline.

>[!NOTE]
>
>Se um pipeline de código de pilha completa já existir para o ambiente selecionado, essa seleção será desativada.

Para concluir a configuração do pipeline de não produção do código de pilha completa, siga estas etapas.

1. Na guia **Código-fonte**, você deve definir as opções a seguir.

   * **Ambientes de implantação qualificados** - Se o pipeline for um pipeline de implantação, você deve selecionar em quais ambientes ele deve ser implantado.
   * **Repositório** - Essa opção define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte o documento [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e o recurso de preenchimento automático do campo localizará as ramificações correspondentes para ajudá-lo em sua seleção.
   * **Ignorar configuração no nível da Web** - Quando marcado, o pipeline não implantará sua configuração no nível da Web.

   * **Pipeline**: se um pipeline de implantação for utilizado, você pode optar por executar uma fase de teste. Marque as opções que deseja habilitar nesta fase. Se nenhuma das opções for selecionada, a fase de teste não será exibida durante a execução do pipeline.

      * **Teste funcional do produto**: executa [testes funcionais de produto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) no ambiente de desenvolvimento.
      * **Teste funcional personalizado**: executa [testes funcionais personalizados](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) no ambiente de desenvolvimento.
      * **Teste de interface personalizada**: executa [testes de interface personalizada](/help/implementing/cloud-manager/ui-testing.md) para aplicativos personalizados.

   ![Pipeline de pilha completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Clique em **Salvar**.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

### Configuração no nível da Web {#web-tier-config}

Um pipeline de configuração no nível da Web implanta configurações HTTPD/Dispatcher. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) para obter mais informações sobre esse tipo de pipeline.

>[!NOTE]
>
>Se um pipeline de código no nível da Web já existir para o ambiente selecionado, essa seleção será desativada.

Para concluir a configuração do pipeline de não produção no nível da Web, siga estas etapas.

1. Na guia **Código-fonte**, você deve definir as opções a seguir.

   * **Ambientes de implantação qualificados** - Se o pipeline for um pipeline de implantação, você deve selecionar em quais ambientes ele deve ser implantado.
   * **Repositório** - Essa opção define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte o documento [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
   * **Localização do código** - Essa opção define o caminho na ramificação do repositório selecionado do qual o pipeline deve recuperar o código.
      * Para pipelines de configuração no nível da Web, esse é geralmente o caminho que contém os diretórios `conf.d`, `conf.dispatcher.d` e `opt-in`.
      * Por exemplo, se a estrutura do projeto foi gerada a partir do [Arquétipo de projeto AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) o caminho seria `/dispatcher/src`.

   ![Pipeline no nível da Web](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. Clique em **Salvar**.

>[!NOTE]
>
>Se você tiver um pipeline de pilha completa existente implantando em um ambiente, a criação de um pipeline de configuração no nível da Web para o mesmo ambiente fará com que a configuração existente no pipeline de pilha completa seja ignorada.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

## Desenvolvimento de Sites com o pipeline front-end {#developing-with-front-end-pipeline}

Com os pipelines de front-end, é dada mais independência aos desenvolvedores de front-end e o processo de desenvolvimento pode ser acelerado.

Consulte o documento [Desenvolvimento de Sites com o pipeline de front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber como esse processo funciona, além de algumas considerações a serem feitas a fim de aproveitar ao máximo o potencial desse processo.

## Ignorar pacotes do Dispatcher {#skip-dispatcher-packages}

Se quiser que os pacotes do dispatcher sejam compilados como parte do pipeline, mas não quiser que eles sejam publicados para criar armazenamento, desative a publicação, o que pode reduzir a duração da execução do pipeline.

A configuração a seguir para desativar a publicação de pacotes do dispatcher deve ser adicionada por meio do arquivo de projeto `pom.xml`. Ela se baseia em uma variável de ambiente, que serve como um sinalizador que pode ser definido no contêiner de compilação do Cloud Manager para especificar quando os pacotes do dispatcher devem ser ignorados.

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
