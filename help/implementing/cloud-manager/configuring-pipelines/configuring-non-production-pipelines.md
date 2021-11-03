---
title: Configurar pipeline de não produção
description: Siga esta página para saber mais sobre como configurar um pipeline de não produção no Cloud Manager
index: false
source-git-commit: fe3bd08e32cef20403d3d2799d027b3ed03e6d36
workflow-type: tm+mt
source-wordcount: '340'
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

1. Selecionar **[Código de pilha completo](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)** ou **[Código de front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)**. Você pode escolher a variável **Repositório** e **Ramificação Git**. Clique em **Salvar**.

   >[!IMPORTANT]
   >Se um pipeline de Código de pilha completo já existir para o ambiente selecionado, essa seleção será desativada.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

   >[!NOTE]
   >Antes de começar a configurar os pipelines do Front-End, consulte AEM Quick Site Creation Jornada para um workflow completo por meio da ferramenta fácil de usar AEM Quick Site Creation. Este site de documentação ajudará você a simplificar o desenvolvimento de front-end do seu site de AEM e personalizar rapidamente seu site sem conhecimento AEM de back-end.

1. O pipeline de não produção recém-criado agora é exibido na variável **Pipelines** cartão.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   O pipeline é mostrado no cartão na tela inicial com três ações, conforme mostrado abaixo:

   * **Adicionar** - permite adicionar um novo pipeline.
   * **Acessar informações do repositório** - permite que o usuário obtenha as informações necessárias para acessar o repositório Git do Cloud Manager.
   * **Saiba mais** - navega para entender o recurso de documentação do pipeline de CI/CD.