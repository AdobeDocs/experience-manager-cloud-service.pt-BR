---
title: Configurar pipeline de não produção
description: Siga esta página para saber mais sobre como configurar um pipeline de não produção no Cloud Manager
index: true
source-git-commit: 2ac65af4cf410491d1196b9e20f67647e0a1b4d1
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---


# Configurar pipeline de não produção {#configure-non-production-pipeline}

Além do principal pipeline que é implantado na fase e na produção, os clientes podem configurar pipelines adicionais, conhecidos como pipeline não relacionados à produção.

Há dois tipos de pipelines de não produção:

1. Qualidade do código: Executa verificações de qualidade de código no código na ramificação git. Esse pipeline executa as etapas de build e qualidade de código.
1. Implantação: Além de executar as etapas de criação e qualidade do código, esse pipeline implanta o código na não produção selecionada para AEM ambiente as a Cloud Service.

## Adicionar um novo pipeline de não produção {#adding-non-production-pipeline}

Na tela inicial, esses pipelines são listados em um novo cartão:

1. Acesse o **Pipelines** na tela inicial do Cloud Manager. Clique em **+Adicionar** e selecione **Adicionar pipeline de não-produção**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **Adicionar pipeline de não-produção**  será exibida. Selecione o tipo de pipeline que deseja criar, **Pipeline de qualidade do código** ou **Pipeline de implantação**.

   >[!NOTE]
   >Para pipelines de implantação, você deve selecionar o ambiente de implantação.

   Além disso, também é possível configurar **Acionador da implantação** e **Comportamento de falhas importantes da métrica** from **Opções de implantação**. Clique em **Continuar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

   Você pode definir os seguintes acionadores de implantação para iniciar o pipeline.

   * **Manual** - uso da interface do usuário para iniciar manualmente o pipeline.
   * **Nas alterações no Git** - inicia o pipeline de CI/CD sempre que há confirmações adicionadas à ramificação git configurada. Mesmo que você selecione essa opção, sempre poderá iniciar o pipeline manualmente.

      Durante a configuração ou edição do pipeline, o Gerenciador de implantação tem a opção de definir o comportamento do pipeline quando uma falha importante for encontrada em qualquer uma das portas de qualidade.

      Isso é útil para clientes que desejam processos mais automatizados. As opções disponíveis são:
   Você pode definir o comportamento importante das métricas de falha para iniciar o pipeline.

   * **Perguntar sempre** - Esta é a configuração padrão e requer intervenção manual em qualquer falha importante.
   * **Falhar imediatamente** - Se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que rejeita manualmente cada falha.
   * **Continuar imediatamente** - Se selecionado, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que aprova manualmente cada falha.


1. Selecionar **[Código de pilha completo](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)** ou **[Código de front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)**.

   Se você selecionou **Código de front-end**, você deve selecionar a variável **Repositório**, **Ramificação Git** e **Localização do código**, como mostrado na figura abaixo:

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-confignew1.png)

   Se você selecionou **Código de pilha completo**, você deve selecionar a variável **Repositório** e **Ramificação Git**, como indicado na figura:
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack1.png)

   >[!IMPORTANT]
   >Se um pipeline de Código de pilha completo já existir para o ambiente selecionado, essa seleção será desativada.

   >[!NOTE]
   >Antes de começar a configurar os pipelines do Front-End, consulte [AEM Jornada de criação rápida de site](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) para um fluxo de trabalho completo por meio da ferramenta de criação rápida de sites AEM fácil de usar. Este site de documentação ajudará você a simplificar o desenvolvimento de front-end do seu site de AEM e personalizar rapidamente seu site sem conhecimento AEM de back-end.

1. O pipeline de não produção recém-criado agora é exibido na variável **Pipelines** cartão.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack2.png)


   O pipeline é mostrado no cartão na tela inicial com quatro ações, conforme mostrado abaixo:

   * **Adicionar** - permite adicionar um novo pipeline.
   * **Mostrar tudo** - permite que o usuário visualize todos os pipelines.
   * **Acessar informações do repositório** - permite que o usuário obtenha as informações necessárias para acessar o repositório Git do Cloud Manager.
   * **Saiba mais** - navega para entender o recurso de documentação do pipeline de CI/CD.