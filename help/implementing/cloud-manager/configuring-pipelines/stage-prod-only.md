---
title: Pipelines somente de preparo e somente de produção
description: Saiba como dividir implantações de preparo e produção usando pipelines dedicados.
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 88%

---


# Pipelines somente de preparo e somente de produção {#stage-prod-only}

Saiba como dividir implantações de preparo e produção usando pipelines dedicados.

>[!NOTE]
>
>Este recurso só está disponível por meio do [programa de adoção antecipada](/help/implementing/cloud-manager/release-notes/current.md#early-adoption).

## Visão geral {#overview}

Os ambientes de preparo e produção são totalmente combinados. Por padrão, as implantações para eles estão vinculadas a um único pipeline. É um pipeline de implantação inserido nos ambientes de preparo e produção desse programa. Embora esse acoplamento seja normalmente adequado, há certos casos de uso em que há desvantagens:

* Se quiser implantar somente em preparo, você só poderá fazer isso rejeitando a etapa **Promover para produção** no pipeline. No entanto, a execução será marcada como cancelada.
* Se você quiser implantar o código mais recente em um ambiente de preparo para produção, será necessário reimplantar todo o pipeline, incluindo a implantação de preparo, mesmo que nenhum código tenha sido alterado lá.
* Como os ambientes não podem ser atualizados durante as implantações, se você quiser pausar e testar o ambiente de preparo por vários dias antes de promover para produção, não será possível atualizar o ambiente de produção. Isso torna tarefas não dependentes, como a atualização de [variáveis de ambiente](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#environment-variables), impossíveis.

Os pipelines somente de preparo e somente de produção oferecem soluções para esses casos de uso fornecendo opções de implantação dedicadas.

* Os **Pipelines de implantação somente de preparo** implantam somente em um ambiente de preparo e a execução termina quando a implantação e os testes são concluídos.
   * Um pipeline somente de preparo se comporta de forma idêntica ao pipeline de produção de empilhamento completo acoplado padrão, mas sem as etapas de implantação de produção (aprovação, agendamento, implantação).
* Os **Pipelines de implantação somente de produção** implantam somente em um ambiente de produção com a opção de selecionar uma execução concluída e validada com sucesso no preparo e implantar seus artefatos na produção.
   * Os pipelines somente de produção reutilizarão os artefatos das implantações de preparo, ignorando a fase de compilação.

Os pipelines somente de preparo e somente de produção não serão executados enquanto um pipeline de produção de pilha completa estiver em execução e vice-versa. Se o pipeline de produção somente de preparo e o pipeline de pilha completa tiverem o acionador **Em alterações do Git** configurado e estiverem apontando para a mesma ramificação e repositório, apenas o pipeline somente de preparo será iniciado automaticamente. Os pipelines somente de produção não são iniciados **Em alterações do Git** já que não estão diretamente vinculados a um repositório.

Esses pipelines dedicados oferecem mais flexibilidade, mas observe os seguintes detalhes de operação e recomendações.

## Limitações {#limitations}

Os pipelines somente de produção sempre usarão os artefatos do pipeline somente de preparo, independentemente do que possa ter sido implantado no preparo por meio do pipeline de produção acoplado padrão nesse meio tempo.

* Isso pode levar a reversões de código indesejadas.
* A Adobe recomenda parar de usar o pipeline de produção acoplada padrão assim que você começar a usar os pipelines somente de produção e somente de preparo.
* Se você ainda decidir executar os pipelines acoplados padrão junto com os pipelines somente de preparo/produção, lembre-se da reutilização de artefatos para evitar reversões de código.

## Problemas conhecidos {#known-issues}

Observe também os seguintes problemas conhecidos antes de começar a testar esse recurso.

* Depois de usar pipelines somente de produção, você pode não se beneficiar das atualizações mais recentes do AEM
   * Em alguns casos, o processo de atualização do AEM pode reverter seu código para o código que foi implantado pela última vez por meio do pipeline de pilha completa.
* Você não poderá solicitar uma [restauração do ambiente](/help/operations/restore.md#offsite-backup) se usar pipelines somente de produção ou somente de preparo.

## Criação de pipeline {#pipeline-creation}

Os pipelines somente de produção e somente de preparo são criados de maneira semelhante aos [pipelines de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e [pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) acoplados padrão. Consulte esses documentos para obter detalhes.

1. Na janela **Pipelines**, clique em **Adicionar pipeline**.

   * Selecione **Adicionar pipeline de não produção** para criar um pipeline somente de preparo.
   * Selecione **Adicionar pipeline somente de produção** para criar um pipeline somente de produção.

   ![Criação de um pipeline somente de produção/preparo](assets/prod-stage-pipelines.png)

>[!NOTE]
>
>Determinadas opções podem estar esmaecidas se os pipelines correspondentes já existirem.
>
>* A opção **Adicionar pipeline somente de produção** não estará disponível se um pipeline somente de preparo ainda não existir.
>* A opção **Adicionar pipeline de produção** não estará disponível se um pipeline acoplado padrão já existir.
>* Apenas um pipeline somente de produção e um pipeline somente de preparo são permitidos por programa.

### Pipelines somente de preparo {#stage-only}

1. Depois de selecionar a opção **Adicionar pipeline de não produção**, a caixa de diálogo **Adicionar pipeline de não produção** é exibida.
1. Para criar um pipeline somente de preparo, selecione o ambiente de preparo no campo **Ambientes de implantação elegíveis** para o seu pipeline. Preencha os campos restantes e clique em **Continuar**.

   ![Criação de um pipeline somente de preparo](assets/stage-only.png)

1. Na guia **Teste de preparo**, será possível definir testes que devem ser executados no ambiente de preparo. Toque ou clique em **Salvar** para salvar o novo pipeline.

### Pipelines somente de produção {#prod-only}

1. Ao selecionar a opção **Adicionar pipeline somente de produção**, a caixa de diálogo **Adicionar pipeline somente de produção** é aberta.
1. Forneça um **Nome do pipeline**. As opções e funcionalidades restantes da caixa de diálogo funcionam da mesma forma que as da caixa de diálogo de criação de pipeline acoplado padrão. Clique em **Salvar** para salvar o pipeline.

## Execução de pipelines somente de produção e somente de preparo {#running}

Os pipelines somente de produção e somente de preparo são executados da mesma maneira que [todos os outros pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines). Consulte a documentação para obter mais detalhes.

Além disso, uma execução de pipeline somente de produção pode ser acionada diretamente dos detalhes de execução de um pipeline somente de preparo.

### Pipelines somente de preparo {#stage-only-run}

Um pipeline somente de preparo é executado quase da mesma maneira que os pipelines acoplados padrão. No entanto, no final da execução, após as etapas de teste, um botão **Promover build** permite iniciar uma execução de pipeline somente de produção que usa os artefatos implantados no preparo por esta execução e os implanta na produção.

![Execução de pipeline somente de preparo](assets/stage-only-pipeline-run.png)

O botão **Promover build** só será exibido se você estiver na última execução de pipeline somente de preparo bem-sucedida. Quando clicado, ele solicita que você confirme a execução do pipeline somente de produção ou crie um pipeline somente de produção, se um ainda não existir.

### Pipelines somente de produção {#prod-only-run}

Para pipelines somente de produção, é importante identificar os artefatos de origem que devem ser implantados na produção. Esses detalhes podem ser encontrados na etapa **Preparação de artefato**. É possível navegar até essas execuções para obter mais detalhes e logs.

![Detalhes do artefato](assets/prod-only-pipeline-run.png)
