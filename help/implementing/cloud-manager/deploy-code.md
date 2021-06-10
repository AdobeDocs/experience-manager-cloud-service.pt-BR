---
title: Implantar o código - Cloud Services
description: Implantar o código - Cloud Services
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: 64023bbdccd8d173b15e3984d0af5bb59a2c1447
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

---

# Implantação do código {#deploy-your-code}

## Implantação do código com o Cloud Manager no AEM as a Cloud Service {#deploying-code-with-cloud-manager}

Depois de configurar o Pipeline de produção (repositório, ambiente e ambiente de teste), você estará pronto para implantar seu código.

1. Clique em **Implantar** no Cloud Manager para iniciar o processo de implantação.

   ![](assets/deploy-code1.png)


1. A tela **Pipeline Execution** é exibida.

   Clique em **Criar** para iniciar o processo.

   ![](assets/deploy-code2.png)

1. O processo de build completo implanta seu código.

   Os seguintes estágios estão envolvidos no processo de criação:

   1. Implantação do Estágio
   1. Teste de preparo
   1. Implantação de produção

   >[!NOTE]
   >
   >Além disso, você pode revisar as etapas de vários processos de implantação exibindo registros ou revisando resultados para os critérios de teste.

   A **Implantação do preparo** envolve estas etapas:

   * Validação: Essa etapa garante que o pipeline esteja configurado para usar os recursos disponíveis no momento, por exemplo, que a ramificação configurada exista, os ambientes estarão disponíveis.
   * Teste de compilação e unidade: Essa etapa executa um processo de criação contêiner. Consulte [Detalhes do ambiente de criação](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md) para obter detalhes sobre o ambiente de criação.
   * Verificação de código: Esta etapa avalia a qualidade do código de seu aplicativo. Consulte [Teste de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md) para obter detalhes sobre o processo de teste.
   * Criar imagens: Esta etapa tem um arquivo de log do processo usado para criar imagens. Esse processo é responsável por transformar os pacotes de conteúdo e dispatcher produzidos pela etapa de compilação em imagens Docker e configuração de Kubernetes.
   * Implantar no Estágio

      ![](assets/stage-deployment.png)
   O **Teste de preparo** envolve as seguintes etapas:

   * **Teste** funcional do produto: As execuções de pipeline do Cloud Manager oferecerão suporte à execução de testes que são executados no ambiente de preparo.
Consulte [Teste funcional do produto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) para obter mais detalhes.

   * **Teste** funcional personalizado: Essa etapa no pipeline está sempre presente e não pode ser ignorada. No entanto, se nenhum JAR de teste for produzido pela build, o teste será aprovado por padrão.\
      Consulte [Teste funcional personalizado](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) para obter mais detalhes.

   * **Teste** da interface personalizada: Esta etapa é um recurso opcional que permite que nossos clientes criem e executem automaticamente testes de interface para seus aplicativos. Os testes da interface do usuário são testes baseados em Selenium, compactados em uma imagem Docker, para permitir uma grande escolha na linguagem e estruturas (como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium).
Consulte [Teste de interface personalizada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/functional-testing.html?lang=en#custom-ui-testing) para obter mais detalhes.


   * **Auditoria** de experiência: Essa etapa no pipeline está sempre presente e não pode ser ignorada. Conforme um pipeline de produção é executado, uma etapa de auditoria de experiência é incluída após um teste funcional personalizado que executará as verificações. As páginas configuradas serão enviadas ao serviço e avaliadas. Os resultados são informativos e permitem que o usuário veja as pontuações e a alteração entre as pontuações atual e anterior. Esse insight é importante para determinar se há uma regressão que será introduzida com a implantação atual.
Consulte [Entendendo os resultados da auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

      ![](assets/stage-testing.png)





## Processo de implantação {#deployment-process}

Todas as implantações de Cloud Service seguem um processo contínuo para garantir tempo de inatividade zero. Consulte [Como as implantações em andamento funcionam](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#how-rolling-deployments-work) para saber mais.

### Implantação para Fase de Produção {#deployment-production-phase}

O processo de implantação das topologias de produção é um pouco diferente para minimizar o impacto para AEM visitantes do Site.

As implantações de produção geralmente seguem as mesmas etapas descritas acima, mas de maneira contínua:

1. Implantar pacotes de AEM para o autor.
1. Desanexar dispatcher1 do balanceador de carga.
1. Implante AEM pacotes para publish1 e o pacote do dispatcher para dispatcher1, libere o cache do dispatcher.
1. Coloque o dispatcher1 de volta no balanceador de carga.
1. Depois que o dispatcher1 estiver novamente em serviço, desconecte o dispatcher2 do balanceador de carga.
1. Implante AEM pacotes para publish2 e o pacote do dispatcher para dispatcher2, libere o cache do dispatcher.
1. Coloque o dispatcher2 de volta no balanceador de carga.
Esse processo continua até que a implantação tenha atingido todos os editores e dispatchers na topologia.
