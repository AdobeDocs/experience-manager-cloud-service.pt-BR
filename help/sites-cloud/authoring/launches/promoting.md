---
title: Promoção de inicializações
description: É necessário promover as páginas de lançamento para mover o conteúdo de volta para a origem (produção) antes de publicar.
exl-id: 5f5ed17c-43db-4ef6-ab79-c491326fa01c
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 98%

---

# Promoção de inicializações {#promoting-launches}

É necessário promover as páginas de lançamento para mover o conteúdo de volta para a origem (produção) antes de publicar. Quando uma página de lançamento é promovida, a página de origem correspondente é substituída pelo conteúdo da página promovida. As seguintes opções estão disponíveis ao promover uma página de lançamento:

* Promover somente a página atual ou todo o lançamento.
* Promover as páginas secundárias da página atual.
* Promover o lançamento completo ou somente as páginas alteradas.
* Excluir o lançamento após promovê-lo.

>[!NOTE]
>
>Após promover as páginas de lançamento para o destino (**Produção**), você pode ativar as páginas de **produção** como uma entidade (para tornar o processo mais rápido). Adicione as páginas a um pacote de fluxo de trabalho e use-o como o conteúdo de um fluxo de trabalho que ativa um pacote de páginas. É necessário criar o pacote de fluxo de trabalho antes de promover o lançamento. Consulte [Processamento de páginas promovidas usando o fluxo de trabalho do AEM](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>Um único lançamento não pode ser promovido simultaneamente. Isso significa que duas ações de promoção simultâneas em uma mesma inicialização podem resultar em um erro - `Launch could not be promoted` (juntamente com erros de conflito no log).

>[!CAUTION]
>
>Ao promover lançamentos para páginas *modificadas*, as modificações nas ramificações de origem e de lançamento são consideradas.

## Promover páginas de lançamento {#promoting-launch-pages}

>[!NOTE]
>
>Isso abrange a ação manual de promover páginas de lançamento quando há apenas um nível de lançamento. Consulte:
>
>* [Promover um lançamento aninhado](#promoting-a-nested-launch), quando houver mais de um lançamento na estrutura.
>* [Lançamentos - a ordem dos eventos](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) para obter mais detalhes sobre promoção e publicação automáticas.
>

É possível promover lançamentos a partir do console **Sites** ou do console **Lançamentos**:

1. Abrir:
   * O console do **Sites** ao navegar pelas páginas de origem:
      1. Abra o [painel de referências](/help/sites-cloud/authoring/sites-console/console-side-panel.md#references) e selecione a página de origem desejada usando o [modo de seleção](/help/sites-cloud/authoring/basic-handling.md) (ou selecione e abra o painel de referências; a ordem não é importante). Todas as referências são mostradas.
      1. Selecione **Lançamentos** (por exemplo, Lançamentos [1]) para exibir uma lista de lançamentos específica.
      1. Selecione um lançamento específico para mostrar as ações disponíveis.
      1. Selecione **Promover lançamento** para abrir o assistente.
   * O console do **Sites** ao navegar pelas páginas de inicialização:
      1. Selecione a página de inicialização necessária usando o [modo de seleção](/help/sites-cloud/authoring/basic-handling.md).
      1. A ação **Promover** estará disponível na barra de ferramentas.
   * O console de **Inicializações**:
      1. Selecione o seu lançamento (selecione a miniatura).
      1. Selecione **Promover**.
1. Na primeira etapa, é possível especificar:
   * **Target**
      * **Excluir lançamento após a promoção**
   * **Escopo**
      * **Promover lançamento completo**
      * **Promover as páginas modificadas**
      * **Promover páginas aprovadas** - Dependente do fluxo de trabalho de aprovação da inicialização
      * **Promover a página atual**
      * **Promover página atual e subpáginas**

     Por exemplo, ao selecionar para promover somente as páginas modificadas:

     ![Promover inicialização](/help/sites-cloud/authoring/assets/launches-promote.png)

     >[!NOTE]
     >
     >Isso abrange um único lançamento, se você tiver lançamentos aninhados, consulte [Promover um lançamento aninhado](#promoting-a-nested-launch).
1. Selecione **Próximo** para continuar.
1. É possível analisar as páginas a serem promovidas; isso dependerá do intervalo de páginas escolhido:

   ![Analisar promoção](/help/sites-cloud/authoring/assets/launches-promote-review.png)

1. Selecione **Promover**.

## Promover páginas de lançamento ao editar {#promoting-launch-pages-when-editing}

Ao editar uma página de lançamento, a ação **Promover lançamento** também está disponível em **Informações da página**. Isso abre o assistente para coletar as informações necessárias.

![Promover inicialização a partir das informações do site](/help/sites-cloud/authoring/assets/launches-promote-page-info.png)

>[!NOTE]
>
>Está disponível para [lançamentos aninhados](#promoting-a-nested-launch) e individuais.

## Promover um lançamento aninhado {#promoting-a-nested-launch}

Após criar um lançamento aninhado, você pode promovê-lo de volta para qualquer uma das origens, incluindo a raiz (produção).

![Uma inicialização aninhada](/help/sites-cloud/authoring/assets/launches-promoting-nested.png)

1. Da mesma forma que ao Criar um lançamento aninhado, navegue e selecione o lançamento necessário no console **Lançamentos** ou no painel **Referências**.
1. Selecione **Promover lançamento** para abrir o assistente.
1. Insira os detalhes necessários:
   * **Target**
      * **Destino da promoção** - É possível promover para qualquer uma das origens.
      * **Excluir o lançamento após a promoção**: após a promoção, o lançamento selecionado e qualquer lançamento aninhado nele será excluído.
   * **Escopo** - Aqui é possível promover toda a inicialização ou somente as páginas que foram editadas. Neste último caso, você pode optar por incluir/excluir subpáginas. A configuração padrão é promover alterações de página somente para a página atual:
      * **Promover lançamento completo**
      * **Promover as páginas modificadas**
      * **Promover páginas aprovadas** - Dependente do fluxo de trabalho de aprovação da inicialização
      * **Promover a página atual**
      * **Promover página atual e subpáginas**

   ![Promover configurações de inicialização](/help/sites-cloud/authoring/assets/launches-promote-settings.png)

1. Selecione **Próximo**.
1. Revise os detalhes da promoção antes que selecionar **Promover**:

   ![Revisar configurações da promoção](/help/sites-cloud/authoring/assets/launches-promote-review-2.png)

   >[!NOTE]
   >
   >As páginas listadas dependerão do tipo de **escopo** definido e, possivelmente, das páginas editadas.

1. Suas alterações são promovidas e refletidas no console **Lançamentos**:

   ![No console de inicializações](/help/sites-cloud/authoring/assets/launches-console.png)

## Processamento de Páginas promovidas usando o fluxo de trabalho do AEM {#processing-promoted-pages-using-aem-workflow}

Use modelos de fluxo de trabalho para executar o processamento em massa das páginas de lançamento promovidas:

1. Crie um pacote de fluxo de trabalho.
1. Quando autores(as) promovem as páginas de lançamento, elas são armazenadas no pacote de fluxo de trabalho.
1. Inicie um modelo de fluxo de trabalho usando o pacote como o conteúdo.

Para iniciar um fluxo de trabalho automaticamente quando as páginas forem promovidas, configure um ativador de fluxo de trabalho para o nó do pacote. <!--To start a workflow automatically when pages are promoted, [configure a workflow launcher](/help/sites-administering/workflows-starting.md#workflows-launchers) for the package node.-->

Por exemplo, você pode gerar solicitações de ativação de página automaticamente quando autores(as) promoverem páginas de lançamento. Configure um iniciador de fluxo de trabalho para iniciar o fluxo de trabalho Solicitar ativação quando o nó do pacote for modificado.

![Fluxo de trabalho de promoção](/help/sites-cloud/authoring/assets/launches-create-workflow.png)
