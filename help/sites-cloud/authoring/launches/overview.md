---
title: Lançamentos
description: Lançamentos permitem que você desenvolva com eficiência o conteúdo para uma versão futura. Eles permitem que você faça alterações prontas para publicação futura, mantendo ao mesmo tempo suas páginas atuais
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '907'
ht-degree: 100%

---

# Lançamentos {#launches}

Lançamentos permitem que você desenvolva com eficiência o conteúdo para uma versão futura.

Um lançamento é criado para permitir que você faça modificações prontas para futuras publicações (mantendo suas páginas atuais). Após editar e atualizar suas páginas de lançamento, você as promove à origem e ativa as páginas de origem (nível superior). A promoção duplica o conteúdo do lançamento nas páginas de origem e pode ser feita manual ou automaticamente (dependendo dos campos definidos ao criar e editar o lançamento).

Por exemplo, as páginas de produtos sazonais da sua loja online são atualizadas trimestralmente, para que os produtos em destaque correspondam à estação atual. Para se preparar para a próxima atualização trimestral, você pode criar um lançamento das páginas da Web apropriadas. Ao longo do trimestre, as seguintes alterações são acumuladas na cópia de lançamento:

* Alterações nas páginas de origem que ocorrem como resultado de tarefas de manutenção normais. Essas alterações são duplicadas automaticamente nas páginas de lançamento.
* Edições realizadas diretamente nas páginas de lançamento, em preparação para o próximo trimestre.

Também é possível:

* Navegar pelo conteúdo na ramificação de lançamento; adicionar ou remover páginas, conforme necessário.
* Visualize como será o conteúdo publicado em uma data/hora específica no futuro.

Quando o próximo trimestre chegar, você promoverá as páginas de lançamento para poder publicar as páginas de origem (mantendo o conteúdo atualizado). É possível promover todas as páginas ou apenas aquelas que você modificou.

Lançamentos também podem ser:

* Criados para várias ramificações raiz. Embora você possa criar o lançamento para o site inteiro (e fazer as alterações lá), isso pode ser impraticável, pois todo o conteúdo precisa ser copiado. Quando centenas ou até milhares de páginas estão envolvidas, os requisitos e o desempenho do sistema são afetados pela ação de cópia e posteriormente pelas comparações necessárias para as tarefas de promoção.
* Aninhados (um lançamento dentro de outro), para dar a você a capacidade de criar um lançamento a partir de outro existente, de forma que os autores possam aproveitar as alterações já feitas, em vez de terem que fazer as mesmas alterações várias vezes em cada lançamento.

Esta seção descreve como criar, editar e promover (e, se necessário, [excluir](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)) as páginas de lançamento de dentro do console do Sites ou [do console de Lançamentos](#the-launches-console):

* [Criação de Lançamentos](/help/sites-cloud/authoring/launches/creating.md)
* [Edição de Lançamentos](/help/sites-cloud/authoring/launches/editing.md)
* [Gerenciamento de páginas dentro dos Lançamentos](/help/sites-cloud/authoring/launches/managing-pages.md)
* [Uso do Timewarp para visualizar seu conteúdo com base em Lançamentos](/help/sites-cloud/authoring/launches/preview.md)
* [Promoção de Lançamentos](/help/sites-cloud/authoring/launches/promoting.md)

## Lançamentos - a ordem dos eventos {#launches-the-order-of-events}

Lançamentos permitem que você desenvolva com eficiência o conteúdo para uma versão futura de uma ou mais páginas da Web ativadas.

Lançamentos permitem que você:

* Crie uma cópia das páginas de origem:
   * A cópia é sua inicialização.
   * As páginas de origem de nível superior são conhecidas como **Produção**.
      * As páginas de origem podem ser obtidas de várias ramificações (separadas).

   ![Ordem de funcionamento dos lançamentos](/help/sites-cloud/authoring/assets/launches-order.png)

* Edite a configuração do lançamento:
   * Adicione ou remova páginas e/ou ramificações ao/do lançamento.
   * Edite as propriedades do lançamento; como **Título**, **Data de Lançameto**, sinalizador **Pronto para produção**.
* Você pode promover e publicar o conteúdo manual ou automaticamente:
   * Manualmente:
      * Promova seu conteúdo de lançamento de volta ao **Destino** (páginas de origem) quando ele estiver pronto para ser publicado.
      * Publique o conteúdo das páginas de origem (após a promoção de volta).
      * Promova todas as páginas ou apenas as páginas modificadas.
   * Automaticamente - isso envolve o seguinte:
      * O campo **Data de lançamento** (**Data de ativação**):**** pode ser definida ao criar ou editar um lançamento.
      * O sinalizador de **Pronto para produção**: só pode ser definido ao editar um lançamento.
      * Se o sinalizador de **Pronto para produção** estiver definido, o lançamento será promovido automaticamente para as páginas de produção na **Data de lançamento** (**Data de ativação**)**especificada**. Após a promoção, as páginas de produção são publicadas automaticamente.\
         Se nenhuma data tiver sido definida, o sinalizador não terá efeito.
* Atualize suas páginas de origem e de lançamento em paralelo:
   * As alterações nas páginas de origem são implementadas automaticamente na cópia de lançamento (se configurada como herança, ou seja, como uma live copy).
   * As alterações na sua cópia de lançamento podem ser feitas sem interromper essas atualizações automáticas ou as páginas de origem.

   ![Ações paralelas](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [Crie um lançamento aninhado](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch) - um lançamento dentro de outro:
   * A origem é um lançamento existente.
   * Você pode [promover um lançamento ](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch)aninhado para qualquer destino. Esse destino pode ser um lançamento pai ou as páginas de origem de nível superior (Produção).

   ![Um lançamento aninhado](/help/sites-cloud/authoring/assets/launches-nested.png)

   >[!CAUTION]
   >
   >Excluir um lançamento removerá o próprio lançamento e qualquer lançamento descendente aninhado.

>[!NOTE]
>
>Criar e editar lançamentos requer direitos de acesso a `/content/launches`, bem como ao grupo padrão `content-authors`.
>
>Entre em contato com o administrador do sistema se você tiver algum problema.

## Lançamentos em Referências (console Sites) {#launches-in-references-sites-console}

1. No console **Sites**, navegue até a origem dos lançamentos.
1. Abra o painel **Referências** e selecione a página de origem.
1. Selecione **Lançamentos**. Os lançamentos existentes serão listados, juntamente com o acesso ao **console de Lançamentos**:

   ![Referências de lançamentos no console do Sites](/help/sites-cloud/authoring/assets/launches-references.png)

1. Toque/clique no lançamento apropriado. A lista de ações possíveis será exibida:

   ![Ações para executar em lançamentos no console do Sites](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## O console Lançamentos {#the-launches-console}

O console Lançamentos fornece uma visão geral dos seus lançamentos e permite que você realize ações naqueles listados. O console pode ser acessado das seguintes maneiras:

* No console de **Ferramentas**: **Ferramentas**, **Sites**, **Lançamentos**.

* **Console de Lançamentos**, na parte inferior da seção **Lançamentos** do painel **Referências** ao navegar pelo conteúdo de origem no console do Sites.

   ![Console de Lançamentos em Referências de lançamentos no console do Sites](/help/sites-cloud/authoring/assets/launches-references.png)

* O botão **Lançamentos**, na parte superior direita, ao navegar pelo conteúdo do lançamento no console do Sites:

   ![Opção Lançamentos, no console do Sites](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)

* Ou diretamente; por exemplo, com:
   `https://<host>:<port>/libs/launches/content/launches.html`
