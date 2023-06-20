---
title: Configuração de pipelines de produção
description: Saiba como configurar pipelines de produção para compilar e implantar seu código em ambientes de produção.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 91%

---


# Configuração de um pipeline de produção {#configure-production-pipeline}

Saiba como configurar pipelines de produção para compilar e implantar seu código em ambientes de produção. Um pipeline de produção primeiro implanta o código no ambiente de preparo e, após a aprovação, implanta o mesmo código no ambiente de produção.

Um usuário deve ter a função **[Gerente de implantação](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar pipelines de produção.

>[!NOTE]
>
>Um pipeline de produção somente poderá ser configurado quando a criação do programa for concluída, quando exista um repositório Git com pelo menos uma ramificação e após a criação de um conjunto de ambientes de produção e de preparo.

Antes de começar a implantar seu código, você deve definir as configurações de pipeline no [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Você poderá [editar as configurações do pipeline](managing-pipelines.md) após a configuração inicial.

## Adição de um novo pipeline de produção {#adding-production-pipeline}

Depois de configurar seu programa e ter pelo menos um ambiente usando a interface do usuário do [!UICONTROL Cloud Manager], você estará pronto para adicionar um pipeline de não produção seguindo essas etapas.

>[!TIP]
>
>Antes de configurar um pipeline de front-end, consulte a [jornada de Criação rápida de sites do AEM](/help/journey-sites/quick-site/overview.md) para obter um guia completo sobre a ferramenta simples de Criação rápida de sites do AEM. Essa jornada ajudará você a simplificar o desenvolvimento de front-end do seu site do AEM, permitindo personalizar rapidamente o site sem conhecimento de back-end no AEM.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até o cartão **Pipelines** na página **Visão geral do programa** e clique em **Adicionar** para selecionar **Adicionar pipeline de produção**.

   ![O cartão Pipelines na visão geral do Gerenciador de programas](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. A caixa de diálogo **Adicionar pipeline de produção** será exibida. Forneça um **Nome do pipeline** para identificar o pipeline junto com as opções a seguir. Clique em **Continuar**.

   **Acionador da implantação** - Você tem as seguintes opções ao definir os acionadores de implantação para iniciar o pipeline.

   * **Manual** - Use essa opção para iniciar manualmente o pipeline.
   * **Quando o Git é alterado** - Essas opções iniciam o pipeline de CI/CD sempre que confirmações são adicionadas à ramificação Git configurada. Com essa opção, ainda é possível iniciar o pipeline manualmente, conforme necessário.

   **Comportamento de falhas importantes da métrica** - Durante a configuração ou edição do pipeline, o **Gerente de implantação** tem a opção de definir o comportamento do pipeline quando uma falha importante é encontrada em qualquer um dos quality gates (portais de qualidade). As opções disponíveis são:

   * **Sempre perguntar** - Essa é a configuração padrão e requer intervenção manual em qualquer falha importante.
   * **Falha imediata** - Se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. É como emular um usuário que rejeita manualmente cada falha.
   * **Continuar imediatamente** - Se selecionado, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. É como emular um usuário que aprova manualmente cada falha.

   ![Configuração do pipeline de produção](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. Na guia **Código-fonte**, é necessário definir de onde o pipeline deve recuperar o código e o tipo de código.

   * **[Código de front-end](#front-end-code)**
   * **[Código de pilha completa](#full-stack-code)**
   * **[Configuração no nível da Web](#web-tier-config)**

As etapas para concluir a criação do pipeline de produção variam de acordo com a opção de **Código-fonte** que você selecionou. Siga os links acima para ir até a próxima seção deste documento para concluir a configuração do pipeline.

### Código de front-end {#front-end-code}

Um pipeline de código front-end implanta compilações de código de front-end contendo um ou mais aplicativos de interface do usuário do lado do cliente. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obter mais informações sobre esse tipo de pipeline.

Para concluir a configuração do pipeline de produção de front-end, siga estas etapas.

1. Na guia **Código-fonte**, você deve definir as opções a seguir.

   * **Repositório** - Essa opção define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte o documento [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e o recurso de preenchimento automático do campo localizará as ramificações correspondentes para ajudá-lo em sua seleção.
   * **Localização do código** - Essa opção define o caminho na ramificação do repositório selecionado do qual o pipeline deve recuperar o código.
   * **Pausar antes de implantar na produção** - Essa opção pausa o pipeline antes de implantar na produção.

   ![Código de front-end](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. Clique em **Salvar** para salvar o pipeline.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

### Código de pilha completa {#full-stack-code}

Um pipeline de código de pilha completa implanta simultaneamente compilações de código de back-end e front-end contendo um ou mais aplicativos de servidor do AEM, juntamente com a configuração HTTPD/Dispatcher. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) para obter mais informações sobre esse tipo de pipeline.

>[!NOTE]
>
>Se um pipeline de código de pilha completa já existir para o ambiente selecionado, essa seleção será desativada.

Para concluir a configuração do pipeline de produção com código de pilha completa, siga estas etapas.

1. Na guia **Código-fonte**, você deve definir as opções a seguir.

   * **Repositório** - Essa opção define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte o documento [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e o recurso de preenchimento automático do campo localizará as ramificações correspondentes para ajudá-lo em sua seleção.
   * **Localização do código** - Essa opção define o caminho na ramificação do repositório selecionado do qual o pipeline deve recuperar o código.
   * **Pausar antes de implantar na produção** - Essa opção pausa o pipeline antes de implantar na produção.
   * **Agendado** - Essa opção permite que o usuário habilite a implantação de produção agendada.

   ![Código de pilha completa](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Clique em **Continuar** para avançar para a guia **Auditoria de experiência**, na qual é possível definir os caminhos que devem ser sempre incluídos na Auditoria de experiência.

   ![Adicionar auditoria de experiência](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Forneça um caminho a ser incluído na Auditoria de experiência.

   * Os caminhos da página devem começar com `/`.
   * Por exemplo, se você deseja incluir `https://wknd.site/us/en/about-us.html` na Auditoria de experiência, insira o caminho `/us/en/about-us.html`.

   ![Definição de um caminho para a Auditoria de experiência](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. Clique em **Adicionar página** e o caminho é preenchido automaticamente com o endereço do ambiente e adicionado à tabela de caminhos.

   ![Caminho salvo na tabela](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. Continue a adicionar caminhos, conforme necessário, repetindo as duas etapas anteriores.

   * É possível adicionar no máximo 25 caminhos.
   * Se você não definir nenhum caminho, a página inicial do site será incluída na Auditoria de experiência por padrão.

1. Clique em **Salvar** para salvar o pipeline.

Os caminhos configurados para a Auditoria de experiência são enviados ao serviço e avaliados de acordo com os testes de desempenho, acessibilidade, SEO (Otimização do mecanismo de pesquisa), práticas recomendadas e PWA (Aplicativo Web Progressivo) quando o pipeline é executado. Consulte [Noções básicas sobre os resultados da Auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

### Configuração no nível da Web {#web-tier-config}

Um pipeline de configuração no nível da Web implanta configurações HTTPD/Dispatcher. Consulte o documento [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) para obter mais informações sobre esse tipo de pipeline.

Para concluir a configuração do pipeline de produção com código de pilha completa, siga estas etapas.

1. Na guia **Código-fonte**, você deve definir as opções a seguir.

   * **Repositório** - Essa opção define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte o documento [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e o recurso de preenchimento automático do campo localizará as ramificações correspondentes para ajudá-lo em sua seleção.
   * **Localização do código** - Essa opção define o caminho na ramificação do repositório selecionado do qual o pipeline deve recuperar o código.
      * Para pipelines de configuração no nível da Web, esse é geralmente o caminho que contém os diretórios `conf.d`, `conf.dispatcher.d` e `opt-in`.
      * Por exemplo, se a estrutura do projeto foi gerada a partir do [Arquétipo de projeto AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) o caminho seria `/dispatcher/src`.
   * **Pausar antes de implantar na produção** - Essa opção pausa o pipeline antes de implantar na produção.
   * **Agendado** - Essa opção permite que o usuário habilite a implantação de produção agendada.

   ![Código no nível da Web](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. Clique em **Salvar** para salvar o pipeline.

>[!NOTE]
>
>Se você tiver um pipeline de pilha completa existente implantando em um ambiente, a criação de um pipeline de configuração no nível da Web para o mesmo ambiente fará com que a configuração existente no pipeline de pilha completa seja ignorada.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

## Desenvolvimento de Sites com o pipeline front-end {#developing-with-front-end-pipeline}

Com os pipelines de front-end, é dada mais independência aos desenvolvedores de front-end e o processo de desenvolvimento pode ser acelerado.

Consulte o documento [Desenvolvimento de sites com o pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber como esse processo funciona, além de algumas considerações a serem feitas para aproveitar ao máximo o potencial desse processo.

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
