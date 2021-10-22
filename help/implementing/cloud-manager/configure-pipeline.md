---
title: Configurar pipeline de CI/CD - Cloud Services
description: Configurar pipeline de CI/CD - Cloud Services
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: f3743451f7aeadae26e8a6814cfbed9667c4a242
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 0%

---

# Configurar seu pipeline de CI-CDConfiguração do seu pipeline CI-CD {#configure-ci-cd-pipeline}

No Cloud Manager, há dois tipos de pipeline:

* **Pipeline de produção**:

   Um pipeline de produção só pode ser adicionado depois que um conjunto de ambientes de produção e de estágio é criado.

   Consulte [Configuração do pipeline de produção](configure-pipeline.md#setting-up-the-pipeline) para obter mais detalhes.

* **Pipeline de não produção**:

   Um pipeline de não produção pode ser adicionado a partir do **Visão geral** na interface do usuário do Cloud Manager.

   Consulte [Pipelines somente para não-produção e qualidade de código](configure-pipeline.md#non-production-pipelines) para obter mais detalhes.

   >[!NOTE]
   >Para configurar o pipeline, você deve:
   > * defina o acionador que iniciará o pipeline.
   > * defina os parâmetros que controlam a implantação de produção.
   > * configure os parâmetros de teste de desempenho.


## Configuração do pipeline de produção {#setting-up-production-pipeline}

O Gerenciador de implantação é responsável pela configuração do pipeline de produção.

>[!NOTE]
>Um Pipeline de produção não pode ser configurado até que a criação de um programa seja concluída, o repositório Git tenha pelo menos uma ramificação e um conjunto de ambientes de Produção e Estágio seja criado.

Antes de começar a implantar seu código, você deve definir as configurações de pipeline do [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Você pode alterar as configurações do pipeline após a configuração inicial.

### Adicionar um novo pipeline de produção {#adding-production-pipeline}

Depois de configurar seu programa e ter pelo menos um ambiente usando [!UICONTROL Cloud Manager] Interface do usuário do , você está pronto para adicionar um pipeline de produção.

Siga estas etapas para configurar o comportamento e as preferências do pipeline de produção:

1. Navegue até o **Pipelines** do cartão **Visão geral do programa** página.
Clique em **+Adicionar** e selecione **Adicionar pipeline de produção**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **Adicionar pipeline de produção** será exibida. Insira o nome do pipeline.

   Além disso, também é possível configurar **Acionador da implantação** e **Comportamento de falhas importantes da métrica** from **Opções de implantação**. Clique em **Continuar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   Você pode definir os acionadores de implantação para iniciar o pipeline.

   * **Manual** - uso da interface do usuário para iniciar manualmente o pipeline.
   * **Nas alterações no Git** - inicia o pipeline de CI/CD sempre que há confirmações adicionadas à ramificação git configurada. Mesmo que você selecione essa opção, sempre poderá iniciar o pipeline manualmente.

      Durante a configuração ou edição do pipeline, o Gerenciador de implantação tem a opção de definir o comportamento do pipeline quando uma falha importante for encontrada em qualquer uma das portas de qualidade.

      Isso é útil para clientes que desejam processos mais automatizados. As opções disponíveis são:
   Você pode definir o comportamento importante das métricas de falha para iniciar o pipeline.

   * **Perguntar sempre** - Esta é a configuração padrão e requer intervenção manual em qualquer falha importante.
   * **Falhar imediatamente** - Se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que rejeita manualmente cada falha.
   * **Continuar imediatamente** - Se selecionado, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que aprova manualmente cada falha.


1. O **Adicionar pipeline de produção** caixa de diálogo inclui uma segunda guia rotulada como **Código fonte**. **Código de pilha completo** está selecionada. Você pode escolher a variável **Repositório** e **Ramificação Git**. Selecione as Opções de implantação de produção, conforme explicado abaixo. Clique em **Continuar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   Opções de implantação de produção:

   * **Pausar antes de implantar na produção**: Essa opção permite a interrupção da implantação antes da produção.
   * **Programado**: Essa opção permite que o usuário habilite a implantação de produção agendada.

1. O **Adicionar pipeline de produção** caixa de diálogo inclui uma terceira guia rotulada como **Auditoria de experiência**. Essa opção fornece uma tabela para os caminhos de URL que devem ser sempre incluídos na Auditoria de experiência.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >Você deve clicar em **Adicionar página** para definir seu próprio link personalizado. O caminho da página deve começar com `/`.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit2.png)


   Clique em **Adicionar nova página** para fornecer um caminho de URL a ser incluído na Auditoria de experiência.

   Por exemplo, se você deseja incluir `https://wknd.site/us/en/about-us.html` na Auditoria de experiência, insira o caminho `/us/en/about-us.html` neste campo e clique em **Salvar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

   O URL que aparece na tabela será:

   `https://publish-p12361-e112003.adobeaemcloud.com/us/en/about-us.html`

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

   É possível incluir no máximo 25 linhas. Se não houver páginas enviadas pelo usuário nesta seção, a página inicial do site será incluída na Auditoria de experiência por padrão.

   Consulte [Noções básicas dos resultados da auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

   >[!NOTE]
   > As páginas configuradas serão enviadas ao serviço e avaliadas de acordo com os testes de desempenho, acessibilidade, SEO (Search Engine Otimization), prática recomendada e PWA (Progressive Web App).

1. Clique em **Salvar**. O pipeline de produção recém-criado agora é exibido na variável **Pipelines** cartão.

   O pipeline é mostrado no cartão na tela inicial com três ações, conforme mostrado abaixo:

   * **Adicionar** - permite adicionar um novo pipeline.
   * **Acessar informações do repositório** - permite que o usuário obtenha as informações necessárias para acessar o repositório Git do Cloud Manager.
   * **Saiba mais** - navega para entender o recurso de documentação do pipeline de CI/CD.

### Edição de um pipeline de produção {#editing-prod-pipeline}

É possível editar as configurações de pipeline da variável **Visão geral do programa** página.

Siga as etapas abaixo para editar o pipeline configurado:

1. Navegar para **Pipelines** do cartão **Visão geral do programa** página.

1. Clique em **...** do **Pipelines** e clique em **Editar**, conforme mostrado na figura abaixo.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. O **Editar pipeline de produção** será exibida.

   1. O **Configuração** permite atualizar a guia **Nome do pipeline**, **Acionador da implantação** e **Comportamento de falha de métricas importantes**.

      >[!NOTE]
      >Consulte [Adicionar e gerenciar repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. O **Origem** fornece uma opção para marcar ou desmarcar **Pausar antes de implantar em produção** e **Programado** opções de **Opções de implantação de produção**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. O **Auditoria de experiência** permite atualizar ou adicionar novas páginas.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. Clique em **Atualizar** depois de concluir a edição do pipeline.

### Ações adicionais do pipeline de produção {#additional-prod-actions}

#### Execução de um pipeline de produção {#run-prod}

Você pode executar o pipeline de produção no cartão Pipelines :

1. Navegar para **Pipelines** do cartão **Visão geral do programa** página.

1. Clique em **...** do **Pipelines** e clique em **Executar**, conforme mostrado na figura abaixo.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

#### Exclusão de um pipeline de produção {#delete-prod}

Você pode excluir o pipeline de produção do cartão Pipelines:

1. Navegar para **Pipelines** do cartão **Visão geral do programa** página.

1. Clique em **...** do **Pipelines** e clique em **Excluir**, conforme mostrado na figura abaixo.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >Um usuário na função Gerenciador de implantação agora pode excluir o pipeline de Produção de maneira automatizada por meio do **Excluir** na placa Pipeline.


## Pipelines somente para não-produção e qualidade de código {#non-production-pipelines}

Além do principal pipeline que é implantado na fase e na produção, os clientes podem configurar pipelines adicionais, conhecidos como pipeline não relacionados à produção.
Existem dois tipos de gasodutos não relacionados à produção:

1. Qualidade do código: Executa verificações de qualidade de código no código na ramificação git. Esse pipeline executa as etapas de build e qualidade de código.
1. Implantação: Além de executar as etapas de criação e qualidade do código, esse pipeline implanta o código na não produção selecionada para AEM ambiente as a Cloud Service.

### Adicionar um novo pipeline de não produção {#adding-non-production-pipeline}

Na tela inicial, esses pipelines são listados em um novo cartão:

1. Acesse o **Pipelines** na tela inicial do Cloud Manager. Clique em **+Adicionar** e selecione **Adicionar pipeline de não-produção**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **Adicionar pipeline de não-produção**  será exibida. Selecione o tipo de pipeline que deseja criar, **Pipeline de qualidade do código** ou **Pipeline de implantação**.

   >[!NOTE]
   >Para pipelines de implantação, você deve selecionar o ambiente de implantação.

   Além disso, também é possível configurar **Acionador da implantação** e **Comportamento de falhas importantes da métrica** from **Opções de implantação**. Clique em **Continuar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. **Código de pilha completo** está selecionada. Você pode escolher a variável **Repositório** e **Ramificação Git**. Clique em **Salvar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. O pipeline de não produção recém-criado agora é exibido na variável **Pipelines** cartão.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   O pipeline é mostrado no cartão na tela inicial com três ações, conforme mostrado abaixo:

   * **Adicionar** - permite adicionar um novo pipeline.
   * **Acessar informações do repositório** - permite que o usuário obtenha as informações necessárias para acessar o repositório Git do Cloud Manager.
   * **Saiba mais** - navega para entender o recurso de documentação do pipeline de CI/CD.

### Edição de um pipeline de não produção {#editing-nonprod-pipeline}

É possível editar as configurações de pipeline da variável **Cartão de pipeline** from **Visão geral do programa** página.

Siga as etapas abaixo para editar o pipeline de não produção configurado:

1. Navegar para **Pipelines** do cartão **Visão geral do programa** página.

1. Selecione o pipeline de não produção e clique em **...**. Clique em **Editar**, conforme mostrado na figura abaixo.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. O **Editar pipeline de produção** será exibida.

   1. O **Configuração** permite atualizar a guia **Nome do pipeline**, **Acionador da implantação** e **Comportamento de falhas importantes da métrica**.

      >[!NOTE]
      >Consulte [Adicionar e gerenciar repositórios](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. O **Código fonte** fornece a atualização da guia **Repositório** e **Ramificação Git**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. Clique em **Atualizar** depois de concluir a edição do pipeline de não produção.

### Ações adicionais do pipeline de não produção {#additional-nonprod-actions}

#### Execução de um pipeline de não produção {#run-nonprod}

Você pode executar o pipeline de produção no cartão Pipelines :

1. Navegar para **Pipelines** do cartão **Visão geral do programa** página.

1. Clique em **...** do **Pipelines** e clique em **Executar**, conforme mostrado na figura abaixo.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### Excluindo um pipeline de não produção {#delete-nonprod}

Você pode excluir o pipeline de produção do cartão Pipelines:

1. Navegar para **Pipelines** do cartão **Visão geral do programa** página.

1. Clique em **...** do **Pipelines** e clique em **Excluir**, conforme mostrado na figura abaixo.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)


## Próximas etapas {#the-next-steps}

Depois de configurar o pipeline, é necessário implantar seu código.

Consulte [Implantar o código](deploy-code.md) para obter mais detalhes.
