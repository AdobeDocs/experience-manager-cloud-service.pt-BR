---
title: Configuração de pipelines de produção
description: Saiba como configurar pipelines de produção para compilar e implantar seu código em ambientes de produção.
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 79%

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

1. Navegue até a **Pipelines** do **Visão geral do programa** e clique em **Adicionar** para selecionar **Adicionar pipeline de produção**.

   ![O cartão Pipelines na visão geral do Gerenciador de programas](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. A caixa de diálogo **Adicionar pipeline de produção** será exibida. Forneça um **Nome do pipeline** para identificar o pipeline junto com as opções a seguir. Clique em **Continuar**.

   **Acionador da implantação** - Você tem as seguintes opções ao definir os acionadores de implantação para iniciar o pipeline.

   * **Manual** - Use essa opção para iniciar manualmente o pipeline.
   * **Quando o Git é alterado** - Essas opções iniciam o pipeline de CI/CD sempre que confirmações são adicionadas à ramificação Git configurada. Com essa opção, ainda é possível iniciar o pipeline manualmente, conforme necessário.

   **Comportamento de falhas importantes da métrica** - Durante a configuração ou edição do pipeline, o **Gerente de implantação** tem a opção de definir o comportamento do pipeline quando uma falha importante é encontrada em qualquer um dos quality gates (portais de qualidade). As opções disponíveis são:

   * **Sempre perguntar** - Essa é a configuração padrão e requer intervenção manual em qualquer falha importante.
   * **Falhar imediatamente** - Se selecionada, o pipeline é cancelado sempre que ocorrer uma falha importante. É como emular um usuário que rejeita manualmente cada falha.
   * **Continuar imediatamente** - Se selecionado, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. É como emular um usuário que aprova manualmente cada falha.

   ![Configuração do pipeline de produção](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. No **Código-fonte** guia, é necessário selecionar o tipo de código que o pipeline deve processar.

   * **[Código de pilha completa](#full-stack-code)**
   * **[Implantação direcionada](#targeted-deployment)**

Consulte [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obter mais informações sobre os tipos de pipelines.

As etapas para concluir a criação do pipeline de produção variam de acordo com o tipo de código-fonte selecionado. Siga os links acima para acessar a próxima seção deste documento e concluir a configuração do pipeline.

### Código de pilha completa {#full-stack-code}

Um pipeline de código de pilha completa implanta simultaneamente compilações de código de back-end e front-end contendo um ou mais aplicativos de servidor do AEM, juntamente com a configuração HTTPD/Dispatcher.

>[!NOTE]
>
>Se um pipeline de código de pilha completa já existir para o ambiente selecionado, essa seleção ficará desativada.

Para concluir a configuração do pipeline de produção com código de pilha completa, siga estas etapas.

1. Na guia **Código-fonte**, você deve definir as opções a seguir.

   * **Repositório** - Essa opção define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte o documento [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e o recurso de preenchimento automático do campo localizará as ramificações correspondentes para ajudá-lo em sua seleção.
   * **Ignorar configuração no nível da Web**: quando essa opção está marcada, o pipeline não implanta sua configuração no nível da Web.
   * **Pausar antes de implantar na produção** - Essa opção pausa o pipeline antes de implantar na produção.
   * **Agendado** - Essa opção permite que o usuário habilite a implantação de produção agendada.

   ![Código de pilha completa](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. Clique em **Continuar** para avançar para a guia **Auditoria de experiência**, na qual é possível definir os caminhos que devem ser sempre incluídos na Auditoria de experiência.

   ![Adicionar auditoria de experiência](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. Forneça um caminho a ser incluído na Auditoria de experiência.

   * Os caminhos da página devem começar com `/`.
   * Por exemplo, se você deseja incluir `https://wknd.site/us/en/about-us.html` na Auditoria de experiência, insira o caminho `/us/en/about-us.html`.

   ![Definição de um caminho para a Auditoria de experiência](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. Clique em **Adicionar página** e o caminho será preenchido automaticamente com o endereço do ambiente e adicionado à tabela de caminhos.

   ![Caminho salvo na tabela](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. Continue a adicionar caminhos, conforme necessário, repetindo as duas etapas anteriores.

   * É possível adicionar no máximo 25 caminhos.
   * Se você não definir nenhum caminho, a página inicial do site será incluída na Auditoria de experiência por padrão.

1. Clique em **Salvar** para salvar o pipeline.

Os caminhos configurados para a Auditoria de experiência serão enviados ao serviço e avaliados conforme os testes de desempenho, acessibilidade, Otimização do Mecanismo de Pesquisa (SEO), práticas recomendadas e Aplicativo Web Progressivo (PWA) quando o pipeline for executado. Consulte [Noções básicas sobre os resultados da Auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

### Implantação direcionada {#targeted-deployment}

Uma implantação direcionada implanta o código somente em partes selecionadas do aplicativo AEM. Nessa implantação, você pode optar por **Incluir** Um dos seguintes tipos de código:

* **[Configuração](#config)** - Defina as configurações no ambiente AEM, tarefas de manutenção, regras CDN e muito mais.
   * Consulte o documento [Regras de filtro de tráfego incluindo regras WAF](/help/security/traffic-filter-rules-including-waf.md) para saber como gerenciar as configurações no repositório para que sejam implantadas corretamente.
* **[Código de front-end](#front-end-code)** - Configurar JavaScript e CSS para o front-end do aplicativo AEM.
   * Com os pipelines de front-end, é dada mais independência aos desenvolvedores de front-end e o processo de desenvolvimento pode ser acelerado.
   * Consulte o documento [Desenvolvimento de sites com o pipeline de front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber como esse processo funciona, além de algumas considerações a serem feitas para aproveitar ao máximo o potencial desse processo.
* **[Configuração no nível da Web](#web-tier-config)** - Configurar propriedades do dispatcher para armazenar, processar e entregar páginas da Web ao cliente.

>[!NOTE]
>
>* Se existir um pipeline de código da Web para o ambiente selecionado, essa seleção será desabilitada.
>* Se você tiver um pipeline de pilha completa existente implantando em um ambiente, a criação de um pipeline de configuração no nível da Web para o mesmo ambiente fará com que a configuração existente no pipeline de pilha completa seja ignorada.
> * Em um dado momento, somente pode haver um pipeline de configuração por ambiente.

As etapas para concluir a criação do pipeline de implantação de produção direcionada são as mesmas depois de escolher um tipo de implantação.

1. Escolha o tipo de implantação necessário.

![Opções de implantação direcionada](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-targeted-deployment.png)

1. Defina o **Ambientes de implantação qualificados**.

   * Se o pipeline for um pipeline de implantação, você deverá selecionar em quais ambientes ele deve ser implantado.

1. Em **Código-fonte**, defina as seguintes opções:

   * **Repositório**: essa opção define de qual repositório Git o pipeline deve recuperar o código.

   >[!TIP]
   > 
   >Consulte [Adição e gerenciamento de repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git**: essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e utilize o preenchimento automático deste campo. O recurso encontra as ramificações correspondentes que você pode selecionar.
   * **Localização do código** - Essa opção define o caminho na ramificação do repositório selecionado do qual o pipeline deve recuperar o código.
   * **Pausar antes de implantar na produção** - Essa opção pausa o pipeline antes de implantar na produção.
   * **Agendado** - Essa opção permite que o usuário habilite a implantação de produção agendada. Disponível somente para implantações direcionadas no nível da Web.

   ![Configurar pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-config-deployment.png)

1. Clique em **Salvar**.

O pipeline é salvo e agora você pode [gerenciar seus pipelines](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa**.

Ao executar um pipeline de implantação direcionado, as configurações [como as configurações WAF](/help/security/traffic-filter-rules-including-waf.md) serão implantados, desde que sejam salvos no ambiente, repositório e ramificação definidos no pipeline.

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
