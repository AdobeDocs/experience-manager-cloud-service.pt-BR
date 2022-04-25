---
title: Implantação de código
description: Saiba como implantar seu código usando os pipelines do Cloud Manager AEM as a Cloud Service.
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: feee55b2d1814b14121030b2ec3c0cb286e87044
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 1%

---


# Implantação de código {#deploy-your-code}

Saiba como implantar seu código usando os pipelines do Cloud Manager AEM as a Cloud Service.

## Implantação do código com o Cloud Manager AEM as a Cloud Service {#deploying-code-with-cloud-manager}

Depois de [configuração do pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) incluindo repositório, ambiente e ambiente de teste, você está pronto para implantar seu código.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada.

1. Clique no programa para o qual deseja implantar o código.

1. Clique em **Implantar** do convite à ação no **Visão geral** para iniciar o processo de implantação.

   ![CTA](assets/deploy-code1.png)

1. O **Execução de pipeline** será exibida. Clique em **Criar** para iniciar o processo.

   ![Tela de execução do pipeline](assets/deploy-code2.png)

O processo de build implanta seu código em três fases.

1. [Implantação do Estágio](#stage-deployment)
1. [Teste de preparo](#stage-testing)
1. [Implantação de produção](#production-deployment)

>[!TIP]
>
>Você pode revisar as etapas de vários processos de implantação exibindo registros ou revisando resultados para os critérios de teste.

## Fase de implantação do estágio {#stage-deployment}

O **Implantação do Estágio** fase. envolve essas etapas.

* **Validação**  - Essa etapa garante que o pipeline esteja configurado para usar os recursos disponíveis no momento. Por exemplo, teste se a ramificação configurada existe e se os ambientes estão disponíveis.
* **Teste de compilação e unidade** - Essa etapa executa um processo de criação em contêiner.
   * Consulte o documento [Detalhes do ambiente de criação](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) para obter detalhes sobre o ambiente de criação.
* **Verificação de código** - Esta etapa avalia a qualidade do código do seu aplicativo.
   * Consulte o documento [Teste de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md) para obter detalhes sobre o processo de teste.
* **Criar imagens** - Esse processo é responsável por transformar os pacotes de conteúdo e dispatcher produzidos pela etapa de compilação em imagens Docker e configurações de Kubernetes.
* **Implantar no Estágio** - A imagem é implantada no ambiente de preparo temporário, em preparação para o [Fase de teste.](#stage-testing)

![Implantação do Estágio](assets/stage-deployment.png)

## Fase de teste de estágio {#stage-testing}

O **Teste de preparo** envolve essas etapas.

* **Teste funcional do produto** - O pipeline do Cloud Manager executa testes que são executados no ambiente de preparo.
   * Consulte o documento [Teste funcional do produto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) para obter mais detalhes.

* **Teste funcional personalizado** - Essa etapa no pipeline é sempre executada e não pode ser ignorada. Se nenhum JAR de teste for produzido pela criação, o teste será aprovado por padrão.
   * Consulte o documento [Teste funcional personalizado](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) para obter mais detalhes.

* **Teste de interface personalizada** - Esta etapa é um recurso opcional que executa automaticamente testes de interface criados para aplicativos personalizados.
   * Os testes da interface do usuário são testes baseados em Selenium compactados em uma imagem Docker para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia desenvolvida na Selenium).
   * Consulte o documento [Teste de interface personalizada](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) para obter mais detalhes.

* **Auditoria de experiência** - Essa etapa no pipeline é sempre executada e não pode ser ignorada. Conforme um pipeline de produção é executado, uma etapa de auditoria de experiência é incluída após um teste funcional personalizado que executará as verificações.
   * As páginas configuradas são enviadas ao serviço e avaliadas.
   * Os resultados são informativos e mostram as pontuações e a alteração entre as pontuações atual e anterior.
   * Esse insight é importante para determinar se há uma regressão que será introduzida com a implantação atual.
   * Consulte o documento [Compreender os resultados da auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

![Teste de preparo](assets/stage-testing.png)

## Fase de implantação da produção {#deployment-production}

O processo de implantação das topologias de produção é um pouco diferente para minimizar o impacto dos visitantes em um site de AEM.

As implantações de produção geralmente seguem as mesmas etapas descritas anteriormente, mas de maneira contínua.

1. Implantar pacotes de AEM para o autor.
1. Desanexar dispatcher1 do balanceador de carga.
1. Implante AEM pacotes para publish1 e o pacote do dispatcher para dispatcher1, libere o cache do dispatcher.
1. Coloque o dispatcher1 de volta no balanceador de carga.
1. Depois que o dispatcher1 estiver novamente em serviço, desconecte o dispatcher2 do balanceador de carga.
1. Implante AEM pacotes para publish2 e o pacote do dispatcher para dispatcher2, libere o cache do dispatcher.
1. Coloque o dispatcher2 de volta no balanceador de carga.

Esse processo continua até que a implantação tenha atingido todos os editores e dispatchers na topologia.

![Fase de implantação da produção](assets/production-deployment.png)

## Tempos limite {#timeouts}

As etapas a seguir atingirão o tempo limite se forem deixadas aguardando o feedback do usuário:

| Etapa | Tempo limite |
|--- |--- |
| Teste de qualidade do código | 14 dias |
| Teste de segurança | 14 dias |
| Teste de desempenho | 14 dias |
| Pedido de aprovação | 14 dias |
| Agendar implantação de produção | 14 dias |
| Suporte CSE | 14 dias |

## Processo de implantação {#deployment-process}

Todas as implantações de Cloud Service seguem um processo contínuo para garantir tempo de inatividade zero. Consulte o documento [Como funcionam as implantações em andamento](/help/implementing/deploying/overview.md#how-rolling-deployments-work) para saber mais.