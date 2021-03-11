---
title: Implantar o código - Cloud Services
description: Implantar o código - Cloud Services
translation-type: tm+mt
source-git-commit: 533707b9073231ed16757884afeb968ace0785b3
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 1%

---


# Implantação do código {#deploy-your-code}

## Implantação do código com o Cloud Manager {#deploying-code-with-cloud-manager}

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
Consulte Teste da interface personalizada para obter mais detalhes.


   * **Auditoria** de experiência: Essa etapa no pipeline está sempre presente e não pode ser ignorada. Conforme um pipeline de produção é executado, uma etapa de auditoria de experiência é incluída após um teste funcional personalizado que executará as verificações. As páginas configuradas serão enviadas ao serviço e avaliadas. Os resultados são informativos e permitem que o usuário veja as pontuações e a alteração entre as pontuações atual e anterior. Esse insight é importante para determinar se há uma regressão que será introduzida com a implantação atual.
Consulte [Entendendo os resultados da auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

      ![](assets/stage-testing.png)





## Processo de implantação {#deployment-process}

A seção a seguir descreve como os pacotes de AEM e dispatcher são implantados na fase de estágio e na fase de produção.

O Cloud Manager carrega todos os arquivos target/*.zip produzidos pelo processo de compilação em um local de armazenamento.  Esses artefatos são recuperados desse local durante as fases de implantação do pipeline.

Quando o Cloud Manager é implantado em topologias que não são de produção, o objetivo é concluir a implantação o mais rápido possível e, portanto, os artefatos são implantados em todos os nós simultaneamente da seguinte maneira:

1. O Cloud Manager determina se cada artefato é um pacote de AEM ou dispatcher.
1. O Cloud Manager remove todos os dispatchers do Balanceador de Carga para isolar o ambiente durante a implantação.

   A menos que configurado de outra forma, você pode ignorar as Alterações no Balanceador de Carga nas Implantações de Desenvolvimento e Estágio, ou seja, desanexar e anexar etapas em pipelines não de produção, para ambientes de desenvolvimento e o pipeline de produção, para ambientes de preparo.

   >[!NOTE]
   >
   >Espera-se que esse recurso seja usado principalmente por clientes 1-1-1.

1. Cada artefato de AEM é implantado em cada instância AEM por meio de APIs do Gerenciador de Pacotes, com dependências de pacote determinando a ordem de implantação.

   Para saber mais sobre como usar pacotes para instalar novas funcionalidades, transferir conteúdo entre instâncias e fazer backup do conteúdo do repositório, consulte Como trabalhar com pacotes.

   >[!NOTE]
   >
   >Todos os artefatos AEM são implantados tanto no autor quanto nos editores. Os modos de execução devem ser aproveitados quando configurações específicas de nó são necessárias. Para saber mais sobre como os modos de Execução permitem ajustar a instância do AEM para uma finalidade específica, consulte Modos de execução.

1. O artefato do dispatcher é implantado em cada dispatcher da seguinte maneira:

   1. O backup das configurações atuais é feito e copiado para um local temporário
   1. Todas as configurações são excluídas, exceto os arquivos imutáveis. Consulte Gerenciar suas configurações do Dispatcher para obter mais detalhes. Isso limpa os diretórios para garantir que nenhum arquivo órfão seja deixado para trás.
   1. O artefato é extraído para o diretório `httpd`.  Arquivos imutáveis não são substituídos. Quaisquer alterações feitas em arquivos imutáveis no repositório Git serão ignoradas no momento da implantação.  Esses arquivos são fundamentais para a estrutura do AMS Dispatcher e não podem ser alterados.
   1. O Apache executa um teste de configuração. Se nenhum erro for encontrado, o serviço será recarregado. Se ocorrer um erro, as configurações serão restauradas a partir do backup, o serviço será recarregado e o erro será relatado ao Cloud Manager.
   1. Cada caminho especificado na configuração do pipeline é invalidado ou liberado do cache do dispatcher.

   >[!NOTE]
   >
   >O Cloud Manager espera que o artefato do dispatcher contenha o conjunto completo de arquivos.  Todos os arquivos de configuração do dispatcher devem estar presentes no repositório Git. Arquivos ou pastas ausentes resultarão em falha na implantação.

1. Após a implantação bem-sucedida de todos os pacotes de AEM e dispatcher em todos os nós, os dispatchers serão adicionados novamente ao balanceador de carga e a implantação será concluída.

   >[!NOTE]
   >
   >Você pode ignorar as alterações no balanceador de carga em implantações de desenvolvimento e estágio, ou seja, desanexar e anexar etapas em pipelines não de produção, para ambientes de desenvolvedor e no pipeline de produção, para ambientes de preparo.

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


