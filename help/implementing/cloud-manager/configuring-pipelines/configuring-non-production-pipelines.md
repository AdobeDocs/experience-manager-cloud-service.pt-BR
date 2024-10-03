---
title: Adicionar um pipeline de não produção
description: Saiba como adicionar um pipeline de não produção para testar a qualidade do seu código antes de implantar em ambientes de produção.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: a5e9b29a8108d5c012d402fda8ff7544e02ca911
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 72%

---


# Adicionar um pipeline de não produção {#configuring-non-production-pipelines}

Saiba como configurar pipelines de não produção para testar a qualidade do código antes de implantar em ambientes de produção.

Um usuário deve ter a função **[Gerente de Implantação](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar pipelines de não produção.

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

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Acesse o cartão **Pipelines** na tela inicial do Cloud Manager. Clique em **+Adicionar** e selecione **Adicionar pipeline de não produção**.

   ![Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. Na guia **Configuração** da caixa de diálogo **Adicionar pipeline de não produção**, selecione o tipo de pipeline de não produção que você deseja adicionar.

   * **Pipeline de qualidade do código**: cria um pipeline que gera o seu código, executa testes de unidade e avalia a qualidade do código; porém, ele NÃO realiza implantações.
   * **Pipeline de implantação**: cria um pipeline que gera o seu código, executa testes de unidade, avalia a qualidade do código e implanta em um ambiente.

   ![Caixa de diálogo Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Forneça um **Nome do pipeline de não produção** para identificar o pipeline junto com as informações adicionais a seguir.

   * **Acionador da implantação** - Você tem as seguintes opções ao definir os acionadores de implantação para iniciar o pipeline.

      * **Manual** - Use essa opção para iniciar manualmente o pipeline.
      * **Quando o Git é alterado**: essa opção inicia o pipeline de CI/CD sempre que confirmações são adicionadas à ramificação Git configurada. Com essa opção, ainda é possível iniciar o pipeline manualmente, conforme necessário.

1. Se optar por criar um **pipeline de implantação**, você também precisará definir o **comportamento de falha para métricas importantes**.

   * **Perguntar sempre**: esse comportamento é a configuração padrão e exige intervenção manual em qualquer falha importante.
   * **Falhar imediatamente**: se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. É como emular um usuário que rejeita manualmente cada falha.
   * **Continuar imediatamente**: se essa opção for selecionada, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. É como emular um usuário que aprova manualmente cada falha.

1. Clique em **Continuar**.

1. Na guia **Código fonte** da caixa de diálogo **Adicionar pipeline de não produção**, você deve selecionar o tipo de código que o pipeline deve processar.

   * **[Código de pilha completa](#full-stack-code)**
   * **[Implantação direcionada](#targeted-deployment)**

Consulte [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obter mais informações sobre os tipos de pipelines.

As etapas para concluir a criação do pipeline de não produção variam de acordo com o tipo de código-fonte selecionado. Siga os links acima para acessar a próxima seção deste documento e concluir a configuração do pipeline.

### Código de pilha completa {#full-stack-code}

Um pipeline de código de pilha completa implanta simultaneamente compilações de código de back-end e front-end contendo um ou mais aplicativos de servidor AEM, juntamente com a configuração HTTPD/Dispatcher.

>[!NOTE]
>
>Se um pipeline de código de pilha completa já existir para o ambiente selecionado, essa seleção será desabilitada.

Para concluir a configuração do pipeline de não produção do código de pilha completa, siga estas etapas.

1. Na guia **Código-fonte**, você deve definir as opções a seguir.

   * **Ambientes de implantação qualificados** - Se o pipeline for um pipeline de implantação, você deve selecionar em quais ambientes ele deve ser implantado.
   * **Repositório**: essa opção define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git**: essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e utilize o preenchimento automático deste campo. Ela ajuda a encontrar as ramificações correspondentes que você pode selecionar.
   * **Ignorar configuração no nível da Web**: quando essa opção está marcada, o pipeline não implanta sua configuração no nível da Web.
   * **Pipeline**: se um pipeline de implantação for utilizado, você pode optar por executar uma fase de teste. Marque as opções que deseja habilitar nesta fase. Se nenhuma das opções for selecionada, a fase de teste não será exibida durante a execução do pipeline.

      * **Teste funcional do produto**: executa [testes funcionais de produto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) no ambiente de desenvolvimento.
      * **Teste funcional personalizado**: executa [testes funcionais personalizados](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) no ambiente de desenvolvimento.
      * **Teste de interface personalizada**: executa [testes de interface personalizada](/help/implementing/cloud-manager/ui-testing.md) para aplicativos personalizados.
      * **Auditoria de Experiência** - Executar [Auditoria de Experiência](/help/implementing/cloud-manager/experience-audit-dashboard.md)

   ![Pipeline de pilha completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Clique em **Salvar**.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

### Implantação direcionada {#targeted-deployment}

Uma implantação direcionada implanta o código somente em partes selecionadas do aplicativo AEM. Nessa implantação, você pode optar por **Incluir** um dos seguintes tipos de código:

* **Configuração** - Define as configurações de vários recursos no seu ambiente AEM.
   * Consulte [Uso dos Pipelines de Configuração](/help/operations/config-pipeline.md) para obter uma lista de configurações com suporte, que inclui encaminhamento de logs, tarefas de manutenção relacionadas à limpeza e várias configurações de CDN, além de gerenciá-las no repositório para que sejam implantadas corretamente.
   * Ao executar um pipeline de implantação direcionada, as configurações serão implantadas, desde que sejam salvas no ambiente, repositório e ramificação definidos no pipeline.
   * Em um dado momento, somente pode haver um pipeline de configuração por ambiente.
* **Código de front-end** - Configure o JavaScript e o CSS para o front-end do aplicativo AEM.
   * Com os pipelines de front-end, é dada mais independência aos desenvolvedores de front-end e o processo de desenvolvimento pode ser acelerado.
   * Consulte o documento [Desenvolvimento de sites com o pipeline de front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber como esse processo funciona, além de algumas considerações a serem feitas para aproveitar ao máximo o potencial desse processo.
* **Configuração da Camada da Web** - Configure as propriedades do Dispatcher para armazenar, processar e entregar páginas da Web ao cliente.
   * Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) para obter mais detalhes.
   * Se existir um pipeline de código da Web para o ambiente selecionado, essa seleção será desabilitada.
   * Se você tiver um pipeline de pilha completa existente implantando em um ambiente, a criação de um pipeline de configuração no nível da Web para o mesmo ambiente fará com que a configuração existente no pipeline de pilha completa seja ignorada.

>[!NOTE]
>
>Os pipelines de nível da Web e de configuração não são compatíveis com repositórios privados. Consulte o documento [Adição de repositórios privados no Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md) para obter detalhes e a lista completa de limitações.

As etapas para concluir a criação do pipeline de implantação de destino e não produção são as mesmas depois de escolher um tipo de implantação.

1. Escolha o tipo de implantação necessário.

![Opções de implantação direcionada](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

1. Defina os **Ambientes de implantação qualificados**.

   * Se o pipeline for um pipeline de implantação, você deverá selecionar em quais ambientes ele deve ser implantado.

1. Em **Source Code**, defina as seguintes opções:

   * **Repositório**: essa opção define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git**: essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e utilize o preenchimento automático deste campo. O recurso encontra as ramificações correspondentes que você pode selecionar.
   * **Localização do código**: essa opção define o caminho na ramificação do repositório selecionado do qual o pipeline deve recuperar o código.
   * **Pipeline** - Para pipelines de não produção de front-end, você tem a opção de habilitar a **[Auditoria de experiência](/help/implementing/cloud-manager/experience-audit-dashboard.md)**.

   ![Configurar pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)

1. Se você habilitou a Auditoria de experiência, toque ou clique em **Continuar** para avançar para a guia **Auditoria de experiência**, onde é possível definir os caminhos que sempre devem ser incluídos na Auditoria de experiência.

   * Se você habilitou a **Auditoria de experiência**, consulte o documento [Auditoria de experiência](/help/implementing/cloud-manager/experience-audit-dashboard.md) para obter detalhes sobre como configurar.
   * Caso contrário, pule esta etapa.

1. Toque ou clique em **Salvar** para salvar o pipeline.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

## Ignorar pacotes do Dispatcher {#skip-dispatcher-packages}

Se deseja que os pacotes do Dispatcher sejam criados como parte de seu pipeline, mas não que sejam publicados para criar um armazenamento, é possível desabilitar a publicação deles, o que pode reduzir a duração da execução do pipeline.

A configuração a seguir para desabilitar a publicação de pacotes do Dispatcher deve ser adicionada por meio do arquivo de projeto `pom.xml`. Ela se baseia em uma variável de ambiente, que serve como um sinalizador que pode ser definido no container de compilação do Cloud Manager para especificar quando os pacotes do Dispatcher devem ser ignorados.

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
