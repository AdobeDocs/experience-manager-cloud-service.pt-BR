---
title: Implantar seu código - Cloud Services
description: Implantar seu código - Cloud Services
translation-type: tm+mt
source-git-commit: 2fa0ef7893fd4f06896402e33bf45d525f0817a5
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 3%

---


# Implantação dor seu  código {#deploy-your-code}

## Implantação de código com o Cloud Manager {#deploying-code-with-cloud-manager}

Depois de configurar o **Pipeline** (repositório, ambiente e ambiente de teste), você estará pronto para implantar seu código.

1. Clique em **Implantar** no Gerenciador de nuvem para start do processo de implantação.

   ![](assets/deploy-code1.png)


1. A tela Execução **do pipeline** é exibida.

   Clique em **Criar** para start do processo.

   ![](assets/deploy-code2.png)

1. O processo de compilação completo implanta seu código.

   As etapas a seguir estão envolvidas no processo de construção:

   1. Implantação do estágio
   1. Teste de estágio
   1. Implantação de produção

   >[!NOTE]
   >
   >Além disso, você pode revisar as etapas de vários processos de implantação ao exibir registros ou revisar os resultados para os critérios de teste.

   A **Implantação do preparo** envolve estas etapas:

   * Validação: Essa etapa garante que o pipeline esteja configurado para usar os recursos disponíveis no momento, por exemplo, que a ramificação configurada exista, os ambientes estarão disponíveis.
   * Compilação e teste de unidade: Esta etapa executa um processo de criação contido. Consulte [Criar detalhes](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#build-environment-details) do Ambiente para obter detalhes sobre o ambiente de criação.
   * Digitalização de código: Esta etapa avalia a qualidade do código do aplicativo. Consulte Teste [de qualidade de](/help/implementing/developing/introduction/understand-test-results.md#code-quality-testing) código para obter detalhes sobre o processo de teste.
   * Criar imagens: Esta etapa tem um arquivo de log do processo usado para criar imagens. Esse processo é responsável por transformar os pacotes de conteúdo e despachante produzidos pela etapa de compilação em imagens Docker e configurações de Kubernetes.
   * Implantar no palco

      ![](assets/stage-deployment.png)
   O **Teste de preparo** envolve as seguintes etapas:

   * Teste funcional do produto: As execuções de pipeline do Gerenciador de nuvem oferecerão suporte à execução de testes executados em relação ao ambiente stage.
Consulte Teste [funcional do](/help/implementing/developing/introduction/understand-test-results.md#product-functional-testing) produto para obter mais detalhes.

   * Teste funcional personalizado: Esta etapa do pipeline está sempre presente e não pode ser ignorada. No entanto, se nenhum JAR de teste for produzido pela compilação, o teste será aprovado por padrão.\
      Consulte Teste [funcional](/help/implementing/developing/introduction/understand-test-results.md#custom-functional-testing) personalizado para obter mais detalhes.

   * Auditoria de conteúdo: Esta etapa do pipeline está sempre presente e não pode ser ignorada. Como um pipeline de produção é executado, uma etapa de auditoria de conteúdo é incluída após testes funcionais personalizados que executarão as verificações. As páginas configuradas serão enviadas ao serviço e avaliadas. Os resultados são informativos e permitem que o usuário veja as pontuações e a alteração entre as pontuações atual e anterior. Esse insight é importante para determinar se há uma regressão que será introduzida com a implantação atual.
Consulte [Compreensão dos resultados](/help/implementing/developing/introduction/understand-test-results.md#content-audit-testing) da auditoria de conteúdo para obter mais detalhes.

      ![](assets/testing-tab.png)





## Processo de implantação {#deployment-process}

A seção a seguir descreve como os pacotes AEM e dispatcher são implantados na fase de estágio e na fase de produção.

O Cloud Manager carrega todos os arquivos público alvo/*.zip produzidos pelo processo de compilação para um local do armazenamento.  Esses artefatos são recuperados desse local durante as fases de implantação do pipeline.

Quando o Cloud Manager é implantado em topologias que não sejam de produção, o objetivo é concluir a implantação o mais rápido possível e, portanto, os artefatos são implantados em todos os nós simultaneamente, da seguinte forma:

1. O Cloud Manager determina se cada artefato é um pacote AEM ou despachante.
1. O Cloud Manager remove todos os despachantes do Balanceador de carga para isolar o ambiente durante a implantação.

   A menos que configurado de outra forma, você pode ignorar as Alterações do Balanceador de Carga nas Implantações de Dev e Stage, ou seja, desanexar e anexar etapas em pipelines de não produção, para ambientes dev e o pipeline de produção, para ambientes de palco.

   >[!NOTE]
   >
   >Espera-se que esse recurso seja usado principalmente por clientes 1-1-1.

1. Cada artefato AEM é implantado em cada instância AEM por meio de APIs do Package Manager, com dependências de pacote determinando a ordem de implantação.

   Para saber mais sobre como usar pacotes para instalar novas funcionalidades, transferir conteúdo entre instâncias e fazer backup do conteúdo do repositório, consulte Como trabalhar com pacotes.

   >[!NOTE]
   >
   >Todos os artefatos AEM são implantados no autor e nos editores. Os modos de execução devem ser utilizados quando configurações específicas do nó forem necessárias. Para saber mais sobre como os modos de execução permitem que você ajuste sua instância de AEM para uma finalidade específica, consulte Modos de execução.

1. O artefato do dispatcher é implantado em cada dispatcher da seguinte maneira:

   1. O backup das configurações atuais é feito e copiado para um local temporário
   1. Todas as configurações são excluídas, exceto os arquivos imutáveis. Consulte Gerenciar configurações do Dispatcher para obter mais detalhes. Isso limpa os diretórios para garantir que nenhum arquivo órfão seja deixado para trás.
   1. O artefato é extraído para o diretório httpd.  Arquivos imutáveis não são substituídos. Quaisquer alterações feitas em arquivos imutáveis no repositório git serão ignoradas no momento da implantação.  Esses arquivos são fundamentais para a estrutura do despachante do AMS e não podem ser alterados.
   1. O Apache realiza um teste de configuração. Se nenhum erro for encontrado, o serviço será recarregado. Se ocorrer um erro, as configurações serão restauradas a partir do backup, o serviço será recarregado e o erro será reportado de volta ao Cloud Manager.
   1. Cada caminho especificado na configuração do pipeline é invalidado ou liberado do cache do dispatcher.

   >[!NOTE]
   >
   >O Cloud Manager espera que o artefato do dispatcher contenha o conjunto de arquivos completo.  Todos os arquivos de configuração do dispatcher devem estar presentes no repositório git. Arquivos ou pastas ausentes resultarão em falha de implantação.

1. Após a implantação bem-sucedida de todos os pacotes de AEM e despachante para todos os nós, os despachantes são adicionados de volta ao balanceador de carga e a implantação é concluída.

   >[!NOTE]
   >
   >Você pode ignorar as alterações no balanceador de carga nas implantações de desenvolvimento e estágio, ou seja, desanexar e anexar etapas em pipelines que não sejam de produção, para ambientes de desenvolvedor e pipeline de produção, para ambientes de estágio.

### Implantação para fase de produção {#deployment-production-phase}

O processo de implantação das topologias de produção difere um pouco para minimizar o impacto nos visitantes AEM Site.

As implantações de produção geralmente seguem as mesmas etapas acima, mas de maneira contínua:

1. Implante AEM pacotes para o autor.
1. Desconecte o dispatcher1 do balanceador de carga.
1. Implante AEM pacotes para publicar1 e o pacote do dispatcher para o dispatcher1, liberar o cache do dispatcher.
1. Recoloque o dispatcher1 no balanceador de carga.
1. Quando o dispatcher1 voltar a funcionar, desconecte o dispatcher2 do balanceador de carga.
1. Implante AEM pacotes para publicar2 e o pacote do dispatcher para o dispatcher2, liberar o cache do dispatcher.
1. Recoloque o dispatcher2 no balanceador de carga.
Esse processo continua até que a implantação tenha atingido todos os editores e despachantes na topologia.


