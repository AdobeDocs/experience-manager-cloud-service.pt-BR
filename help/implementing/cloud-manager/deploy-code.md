---
title: Implantação de código
description: Saiba como implantar seu código usando os pipelines do Cloud Manager no AEM as a Cloud Service.
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 94%

---


# Implantação de código {#deploy-your-code}

Saiba como implantar seu código em produção usando os pipelines do Cloud Manager no AEM as a Cloud Service.

![Diagrama de pipelines de produção](./assets/configure-pipeline/production-pipeline-diagram.png)

A implantação perfeita de código em preparo e, em seguida, em produção é feita por meio de um pipeline de produção. A execução do pipeline de produção é dividida em duas fases lógicas.

1. Implantação no ambiente de preparo
   * O código é compilado e implantado no ambiente de preparo para testes funcionais automatizados, testes de interface do usuário, auditoria de experiência e testes de aceitação de usuários (UAT).
1. Implantação no ambiente de produção
   * Depois que a compilação for validada em preparo e aprovada para promoção em produção, o mesmo artefato de compilação será implantado no ambiente de produção.

_Somente o tipo de pipeline de Código de pilha completa oferece suporte à verificação do código, testes de função, testes de interface do usuário e auditoria de experiência._

## Implantação de código com o Cloud Manager no AEM as a Cloud Service {#deploying-code-with-cloud-manager}

Depois de [configurar o Pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md), incluindo repositório, ambiente e ambiente de teste, você estará pronto para implantar seu código.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa no qual deseja implantar código.

1. Clique em **Implantar** na chamada à ação na tela **Visão geral** para iniciar o processo de implantação.

   ![CTA](assets/deploy-code1.png)

1. A tela **Execução de pipeline** será exibida. Clique em **Compilar** para iniciar o processo.

   ![Tela Execução de pipeline](assets/deploy-code2.png)

O processo de compilação implanta o código pelas três fases.

1. [Implantação em preparo](#stage-deployment)
1. [Teste de preparo](#stage-testing)
1. [Implantação em produção](#production-deployment)

>[!TIP]
>
>Você pode revisar as etapas dos vários processos de implantação exibindo os registros ou revisando os resultados dos critérios de teste.

## Fase de implantação em preparo {#stage-deployment}

A fase de **Implantação em preparo** envolve estas etapas.

* **Validação** - Essa etapa garante que o pipeline esteja configurado para usar os recursos disponíveis no momento. por exemplo, testar se a ramificação configurada existe e se os ambientes estão disponíveis.
* **Teste de compilação e unidade** - Essa etapa executa um processo de compilação contido.
   * Consulte o documento [Detalhes do ambiente de compilação](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) para obter detalhes sobre o ambiente de compilação.
* **Verificação do código Scanning** - Essa etapa avalia a qualidade do código do seu aplicativo.
   * Consulte o documento [Teste de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md) para obter detalhes sobre o processo de teste.
* **Compilar imagens** - Esse processo é responsável por transformar os pacotes de conteúdo e dispatcher produzidos pela etapa de compilação em imagens do Docker e configurações Kubernetes.
* **Implantar em preparo** - A imagem é implantada no ambiente de preparo, como forme de preparação para a [Fase de teste de preparo.](#stage-testing)

![Implantação em preparo](assets/stage-deployment.png)

## Fase de teste de preparo {#stage-testing}

O **Teste de preparo** envolve essas etapas.

* **Teste funcional do produto** - O pipeline do Cloud Manager realiza testes que são executados no ambiente de preparo.
   * Consulte o documento [Teste funcional do produto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) para obter mais detalhes.

* **Teste funcional personalizado** - Essa etapa no pipeline é sempre executada e não pode ser ignorada. Se nenhum JAR de teste for produzido pela compilação, o teste será aprovado por padrão.
   * Consulte o documento [Teste funcional do produto](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) para obter mais detalhes.

* **Teste de interface do usuário personalizada** - Essa etapa é um recurso opcional que executa automaticamente testes de interface do usuário criados para aplicativos personalizados.
   * Os testes de interface do usuário são testes baseados em Selenium, compactados em uma imagem do Docker, para permitir uma variedade de opções de linguagens e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium).
   * Consulte o documento [Teste personalizado da interface do usuário](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) para obter mais detalhes.

* **Auditoria de experiência** - Essa etapa no pipeline é sempre executada e não pode ser ignorada. Conforme um pipeline de produção é executado, uma etapa de auditoria de experiência é incluída após o teste funcional personalizado que realizará as verificações.
   * As páginas configuradas são enviadas ao serviço e avaliadas.
   * Os resultados são informativos e mostram as pontuações e as alterações entre as pontuações atual e anterior.
   * Esse insight é importante para determinar se há uma regressão introduzida com a implantação atual.
   * Consulte o documento [Noções básicas sobre os resultados da auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

![Teste de preparo](assets/stage-testing.png)

## Fase de implantação em produção {#deployment-production}

O processo de implantação nas topologias de produção é um pouco diferente para minimizar o impacto dos visitantes em um site AEM.

As implantações em produção geralmente seguem as mesmas etapas descritas anteriormente, mas de maneira gradual.

1. Implante pacotes de AEM para o autor.
1. Desconecte dispatcher1 do balanceador de carga.
1. Implante os pacotes do AEM em publish1 e o pacote do dispatcher em dispatcher1; limpe o cache do dispatcher.
1. Coloque dispatcher1 de volta no balanceador de carga.
1. Quando dispatcher1 estiver novamente em serviço, desconecte dispatcher2 do balanceador de carga.
1. Implante os pacotes do AEM em publish2 e o pacote do dispatcher em dispatcher2; limpe o cache do dispatcher.
1. Coloque dispatcher2 de volta no balanceador de carga.

Esse processo continua até que a implantação tenha atingido todos os editores e dispatchers na topologia.

![Fase de implantação em produção](assets/production-deployment.png)

## Tempos limite {#timeouts}

As seguintes etapas atingirão o tempo limite se forem deixadas aguardando o feedback do usuário:

| Etapa | Tempo limite |
|--- |--- |
| Teste de qualidade do código | 14 dias |
| Teste de segurança | 14 dias |
| Teste de desempenho | 14 dias |
| Pedido de aprovação | 14 dias |
| Agendar implantação em produção | 14 dias |
| Suporte CSE | 14 dias |

## Processo de implantação {#deployment-process}

Todas as implantações do Cloud Service seguem um processo gradual para garantir tempo de inatividade zero. Consulte o documento [Como funcionam as implantações graduais](/help/implementing/deploying/overview.md#how-rolling-deployments-work) para saber mais.

>[!NOTE]
>
>O cache do Dispatcher é limpo em cada implantação. Em seguida, ele é aquecido antes que os novos nós de publicação aceitem o tráfego.

## Reexecutar uma implantação em produção {#Reexecute-Deployment}

A reexecução da etapa de implantação em produção é compatível com execuções em que a etapa de implantação em produção foi concluída. O tipo de conclusão não é importante – a implantação pode ser cancelada ou malsucedida. Dito isso, espera-se que o principal caso de uso seja aquele em que a etapa de implantação em produção falhou por motivos transitórios. A reexecução cria uma nova execução usando o mesmo pipeline. Essa nova execução consiste em três etapas:

1. A etapa de validação – é essencialmente a mesma validação que ocorre durante uma execução normal do pipeline.
1. A etapa de compilação – no contexto de uma reexecução, a etapa de compilação é a cópia dos artefatos, sem executar um novo processo de compilação.
1. A etapa de implantação em produção – usa a mesma configuração e as mesmas opções da etapa de implantação em produção de uma execução normal do pipeline.

A etapa de compilação pode ser rotulada de forma um pouco diferente na interface do usuário para refletir que está copiando artefatos, não os recompilando.

![Reimplantar](assets/Re-deploy.png)

Limitações:

* A reexecução da etapa de implantação em produção somente estará disponível na última execução.
* A reexecução não estará disponível para execuções de atualização por push. Se a última execução for uma execução de atualização por push, não será possível iniciar uma reexecução.
* Se a última execução for uma execução de atualização por push, não será possível iniciar uma reexecução.
* Se a última execução falhar em qualquer ponto antes da etapa de implantação em produção, não será possível iniciar uma reexecução.

### API de reexecução {#Reexecute-API}

### Como identificar a se uma reexecução foi iniciada

Para identificar se uma execução foi reexecutada, analise o campo do acionador. Seu valor é *RE_EXECUTAR*.

### Acionamento de uma nova execução

Para acionar uma reexecução, uma solicitação PUT precisa ser feita ao Link HAL &lt;(<https://ns.adobe.com/adobecloud/rel/pipeline/reExecute>)> o estado da etapa de implantação em produção. Se esse link estiver presente, a execução poderá ser reiniciada dessa etapa. Se estiver ausente, a execução não poderá ser reiniciada dessa etapa. Na versão inicial, esse link somente estará presente na etapa de implantação em produção, mas versões futuras poderão oferecer suporte para iniciar o pipeline a partir de outras etapas. Exemplo:

```Javascript
 {
  "_links": {
    "https://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/metrics",
      "templated": false
    },
    "self": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530",
      "templated": false
    }
  },
  "id": "6187842",
  "stepId": "2983530",
  "phaseId": "1575676",
  "action": "deploy",
  "environment": "weretail-global-b75-prod",
  "environmentType": "prod",
  "environmentId": "59254",
  "startedAt": "2022-01-20T14:47:41.247+0000",
  "finishedAt": "2022-01-20T15:06:19.885+0000",
  "updatedAt": "2022-01-20T15:06:20.803+0000",
  "details": {
  },
  "status": "FINISHED"
```


A sintaxe do valor _href_ do link HAL acima não deve ser usada como ponto de referência. O valor real sempre deve ser lido do link HAL, e não gerado.

Envio de um *PUT* solicitação para esse endpoint resulta em uma *201* se for bem-sucedido, e o corpo da resposta for a representação da nova execução. É semelhante a iniciar uma execução regular por meio da API.
