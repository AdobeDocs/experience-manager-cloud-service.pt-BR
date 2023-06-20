---
title: Promoção de inicializações
description: É necessário promover as páginas de inicialização para mover o conteúdo de volta para a origem (produção) antes de publicar.
exl-id: 5f5ed17c-43db-4ef6-ab79-c491326fa01c
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 38%

---

# Promoção de inicializações {#promoting-launches}

É necessário promover as páginas de inicialização para mover o conteúdo de volta para a origem (produção) antes de publicar. Quando uma página de inicialização é promovida, a página correspondente das páginas de origem é substituída pelo conteúdo da página promovida. As seguintes opções estão disponíveis ao promover uma página de inicialização:

* Se deve promover somente a página atual ou toda a inicialização.
* Se as páginas secundárias da página atual devem ser promovidas.
* Se deve promover a inicialização completa ou somente as páginas que foram alteradas.
* Se o lançamento deve ser excluído após ser promovido.

>[!NOTE]
>
>Depois de promover as páginas de inicialização ao target (**Produção**), você pode ativar a variável **Produção** páginas como uma entidade (para tornar o processo mais rápido). Adicione as páginas a um pacote de fluxo de trabalho e use-o como a carga de um fluxo de trabalho que ativa um pacote de páginas. É necessário criar o pacote de workflow antes de promover a inicialização. Consulte [Processamento de páginas promovidas usando o fluxo de trabalho do AEM](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>Um único lançamento não pode ser promovido simultaneamente. Isso significa que duas ações de promoção simultâneas em uma mesma inicialização podem resultar em um erro - `Launch could not be promoted` (juntamente com erros de conflito no log).

>[!CAUTION]
>
>Ao promover inicializações para *modificado* páginas, modificações nas ramificações de origem e de inicialização são consideradas.

## Promover páginas de lançamento {#promoting-launch-pages}

>[!NOTE]
>
>Isso abrange a ação manual de promover páginas de inicialização quando há apenas um nível de inicialização. Consulte:
>
>* [Promover uma inicialização aninhada](#promoting-a-nested-launch) quando houver mais de uma inicialização na estrutura.
>* [Inicializações - a ordem dos eventos](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) para obter mais detalhes sobre promoção e publicação automáticas.
>

É possível promover inicializações a partir do **Sites** console ou o **Lançamentos** console:

1. Abrir:
   * O console do **Sites** ao navegar pelas páginas de origem:
      1. Abra o [painel de referências](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) e selecione a página de origem desejada usando o [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md) (ou selecione e abra o painel de referências; a ordem não é importante). Todas as referências são mostradas.
      1. Selecione **Lançamentos** (por exemplo, Lançamentos [1]) para exibir uma lista de lançamentos específica.
      1. Selecione a inicialização específica para mostrar as ações disponíveis.
      1. Selecione **Promover lançamento** para abrir o assistente.
   * O console do **Sites** ao navegar pelas páginas de inicialização:
      1. Selecione a página de inicialização necessária usando o [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md).
      1. A variável **Promover** ação está disponível na barra de ferramentas.
   * O console de **Inicializações**:
      1. Selecione o seu lançamento (toque/clique na miniatura).
      1. Selecionar **Promover**.
1. Na primeira etapa, é possível especificar:
   * **Target**
      * **Excluir inicialização após promoção**
   * **Escopo**
      * **Promover lançamento completo**
      * **Divulgar as páginas modificadas**
      * **Promover páginas aprovadas** - Dependente do fluxo de trabalho de aprovação da inicialização
      * **Divulgar a página atual**
      * **Divulgar página atual e subpáginas**

     Por exemplo, ao selecionar para promover somente as páginas modificadas:

     ![Promover inicialização](/help/sites-cloud/authoring/assets/launches-promote.png)

     >[!NOTE]
     >
     >Isso abrange uma única inicialização, se você tiver inicializações aninhadas, consulte [Promover uma inicialização aninhada](#promoting-a-nested-launch).
1. Selecionar **Próxima** para continuar.
1. É possível analisar as páginas a serem promovidas; isso dependerá do intervalo de páginas escolhido:

   ![Analisar promoção](/help/sites-cloud/authoring/assets/launches-promote-review.png)

1. Selecionar **Promover**.

## Promover páginas de lançamento ao editar {#promoting-launch-pages-when-editing}

Ao editar uma página de inicialização, a variável **Promover lançamento** a ação também está disponível em **Informações da página**. Isso abrirá o assistente para coletar as informações necessárias.

![Promover inicialização a partir das informações do site](/help/sites-cloud/authoring/assets/launches-promote-page-info.png)

>[!NOTE]
>
>Ele está disponível para single e [inicializações aninhadas](#promoting-a-nested-launch).

## Promover uma inicialização aninhada {#promoting-a-nested-launch}

Depois de criar uma inicialização aninhada, você pode promovê-la de volta para qualquer uma das origens, incluindo a origem raiz (produção).

![Uma inicialização aninhada](/help/sites-cloud/authoring/assets/launches-promoting-nested.png)

1. Da mesma forma que ao Criar um lançamento aninhado, navegue e selecione o lançamento necessário no console **Lançamentos** ou no painel **Referências**.
1. Selecione **Promover lançamento** para abrir o assistente.
1. Insira os detalhes necessários:
   * **Target**
      * **Destino da promoção** - É possível promover para qualquer uma das origens.
      * **Excluir inicialização após promoção** - Após a promoção, a inicialização selecionada e qualquer inicialização aninhada dentro dela será excluída.
   * **Escopo** - Aqui é possível promover toda a inicialização ou somente as páginas que foram editadas. No último caso, você pode optar por incluir/excluir subpáginas. A configuração padrão é promover alterações de página somente para a página atual:
      * **Promover lançamento completo**
      * **Divulgar as páginas modificadas**
      * **Promover páginas aprovadas** - Dependente do fluxo de trabalho de aprovação da inicialização
      * **Divulgar a página atual**
      * **Divulgar página atual e subpáginas**

   ![Promover configurações de inicialização](/help/sites-cloud/authoring/assets/launches-promote-settings.png)

1. Selecione **Próximo**.
1. Revise os detalhes da promoção antes que selecionar **Promover**:

   ![Revisar configurações da promoção](/help/sites-cloud/authoring/assets/launches-promote-review-2.png)

   >[!NOTE]
   >
   >As páginas listadas dependerão do tipo de **Escopo** e possivelmente as páginas que foram editadas.

1. Suas alterações são promovidas e refletidas no **Lançamentos** console:

   ![No console de inicializações](/help/sites-cloud/authoring/assets/launches-console.png)

## Processamento de Páginas promovidas usando o fluxo de trabalho do AEM {#processing-promoted-pages-using-aem-workflow}

Usar modelos de fluxo de trabalho para executar o processamento em massa das páginas de inicializações promovidas:

1. Crie um pacote de fluxo de trabalho.
1. Quando os autores promovem as páginas do Launch, eles as armazenam no pacote de fluxo de trabalho.
1. Inicie um modelo de fluxo de trabalho usando o pacote como a carga.

Para iniciar um fluxo de trabalho automaticamente quando as páginas forem promovidas, configure um ativador de fluxo de trabalho para o nó do pacote. <!--To start a workflow automatically when pages are promoted, [configure a workflow launcher](/help/sites-administering/workflows-starting.md#workflows-launchers) for the package node.-->

Por exemplo, você pode gerar automaticamente solicitações de ativação de página quando os autores promovem páginas de Lançamentos. Configure um iniciador de fluxo de trabalho para iniciar o fluxo de trabalho Ativação de solicitação quando o nó do pacote for modificado.

![Fluxo de trabalho de promoção](/help/sites-cloud/authoring/assets/launches-create-workflow.png)
