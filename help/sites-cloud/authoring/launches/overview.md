---
title: Lançamentos para páginas
description: Saiba como usar Inicializações para páginas no Adobe Experience Manager as a Cloud Service. Os lançamentos permitem desenvolver conteúdo com eficiência para uma versão futura, mantendo as páginas atuais.
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
solution: Experience Manager Sites
feature: Authoring, Launches
role: User
source-git-commit: 20ad1d468ac0d8ec3933477f954120debe4e9240
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 72%

---

# Lançamentos para páginas {#launches-for-pages}

No Adobe Experience Manager (AEM) as a Cloud Service, os Lançamentos permitem desenvolver conteúdo com eficiência para uma versão futura.

Uma *Inicialização* é criada para permitir que você faça alterações na preparação de uma publicação futura, ao mesmo tempo em que mantém o conteúdo atual. Para páginas do AEM, isso significa que você está editando duas versões ao mesmo tempo: páginas publicadas no momento e uma versão dessas páginas a serem publicadas posteriormente. Quando essa hora chegar, você poderá substituir as páginas originais e publicar as novas versões.

>[!NOTE]
>
>As inicializações também estão disponíveis para Fragmentos de conteúdo. Os conceitos básicos são os mesmos, mas há diferenças em como gerenciá-los no AEM.
>
>Para obter detalhes completos, consulte [Inicializações para fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md).

Você cria uma *Inicialização* e, depois de editar e atualizar as páginas da *Inicialização*, *promove* de volta para a *Source*. Você pode então ativar estas *páginas do Source* (nível superior). A promoção duplica o conteúdo do lançamento de volta às páginas de origem e pode ser feita manual ou automaticamente (dependendo dos campos definidos ao criar e editar o lançamento).

Por exemplo, as páginas do produtos sazonais da loja online são atualizadas trimestralmente para que os produtos em destaque se alinhem à temporada atual. Para se preparar para a próxima atualização trimestral, é possível criar um lançamento das páginas da Web apropriadas. Ao longo do trimestre, as seguintes alterações são acumuladas na cópia do lançamento:

* Alterações nas páginas de origem que ocorrem como resultado de tarefas de manutenção normais. Essas alterações são duplicadas automaticamente nas páginas de lançamento.
* Edições realizadas diretamente nas páginas de lançamento como preparação para o próximo trimestre.

Também é possível:

* Navegar pelo conteúdo na ramificação de lançamento; adicionar ou remover páginas, conforme necessário.
* Visualize como será o conteúdo publicado em uma data específica no futuro.

Quando o próximo trimestre chegar, você promoverá as páginas de lançamento para poder publicar as páginas de origem (mantendo o conteúdo atualizado). É possível promover todas as páginas ou apenas aquelas que você modificou.

Os lançamentos também podem ser:

* Criados para várias ramificações raiz. Embora você possa criar o lançamento para todo o site (e fazer as alterações lá), isso pode ser impraticável, pois todo o site deve ser copiado. Quando centenas ou até milhares de páginas estão envolvidas, os requisitos e o desempenho do sistema seriam afetados pela ação de cópia e, posteriormente, pelas comparações necessárias para as tarefas de promoção.
* Aninhados (um lançamento dentro de outro) para oferecer a capacidade de criar um lançamento a partir de outro já existente, de modo que os autores possam aproveitar as alterações já feitas em vez de precisar fazer as mesmas alterações várias vezes para cada lançamento.

Esta seção descreve como criar, editar e promover (e, se necessário, [excluir](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)) as páginas de lançamento de dentro do console do Sites ou [do console de Lançamentos](#the-launches-console):

* [Criação de Lançamentos](/help/sites-cloud/authoring/launches/creating.md)
* [Edição de Lançamentos](/help/sites-cloud/authoring/launches/editing.md)
* [Gerenciamento de páginas dentro dos Lançamentos](/help/sites-cloud/authoring/launches/managing-pages.md)
* [Uso do Timewarp para visualizar seu conteúdo com base em Lançamentos](/help/sites-cloud/authoring/launches/preview.md)
* [Promoção de Lançamentos](/help/sites-cloud/authoring/launches/promoting.md)

## Lançamentos - a Ordem dos eventos {#launches-the-order-of-events}

Os lançamentos permitem desenvolver com eficiência o conteúdo de uma versão futura de uma ou mais páginas da Web ativadas.

Eles permitem:

* Crie uma cópia das páginas de origem:
   * A cópia é sua inicialização.
   * As páginas de origem de nível superior são conhecidas como **Produção**.
      * As páginas de origem podem ser obtidas de várias ramificações (separadas).

  ![Ordem de funcionamento dos lançamentos](/help/sites-cloud/authoring/assets/launches-order.png)

* Edite a configuração do lançamento:
   * Adicionar ou remover páginas e/ou ramificações do/ao lançamento.
   * Edite as propriedades do lançamento; como **Título**, **Data de Lançameto**, sinalizador **Pronto para produção**.
* É possível promover e publicar o conteúdo manual ou automaticamente:
   * Manualmente:
      * Promover o conteúdo do seu lançamento de volta para o **Destino** (páginas de origem) quando estiver pronto para ser publicado.
      * Publicar o conteúdo das páginas de origem (após promover de volta).
      * Promover todas as páginas ou somente as páginas modificadas.
   * Automaticamente - isso envolve o seguinte:
      * O campo **Data de lançamento** (**Data de ativação**):**** pode ser definida ao criar ou editar um lançamento.
      * O sinalizador **Pronto para produção** : só pode ser definido ao editar um lançamento.
      * Se o sinalizador **Pronto para produção** estiver definido, a inicialização será executada automaticamente nas páginas de produção na **Data** do **Lançamento**(**Data de ativação**) especificada. Após a promoção, as páginas de produção são publicadas automaticamente.\
        Se nenhuma data tiver sido definida, o sinalizador não terá efeito.
* Atualize suas páginas de origem e de lançamento em paralelo:
   * As alterações nas páginas de origem são implementadas automaticamente na cópia do lançamento (se configurada como herança, ou seja, como uma live copy).
   * As alterações na sua cópia de lançamento podem ser feitas sem interromper essas atualizações automáticas ou as páginas de origem.

  ![Ações paralelas](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [Criar uma inicialização aninhada](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch) - um lançamento dentro de outro:
   * A origem é um lançamento já existente.
   * É possível [promover um lançamento aninhado](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch) para qualquer destino. Pode ser um lançamento principal ou as páginas de origem de nível superior (Produção).

  ![Um lançamento aninhado](/help/sites-cloud/authoring/assets/launches-nested.png)

  >[!CAUTION]
  >
  >Excluir um lançamento removerá o próprio lançamento e qualquer lançamento descendente aninhado.

>[!NOTE]
>
>Criar e editar lançamentos requer direitos de acesso a `/content/launches`, bem como ao grupo padrão `content-authors`.
>
>Entre em contato com o administrador do sistema se tiver algum problema.

## Lançamentos em referências (console do Sites) {#launches-in-references-sites-console}

1. No console do **Sites** navegue até a origem do(s) lançamento(s).
1. Abra o painel **Referências** e selecione a página de origem.
1. Selecione **Lançamentos**, os lançamentos já existentes serão listados, juntamente com o acesso ao **Console de lançamentos**:

   ![Referências de lançamentos no console do Sites](/help/sites-cloud/authoring/assets/launches-references.png)

1. Selecione a inicialização apropriada. A lista de ações possíveis será exibida:

   ![Ações para executar em lançamentos no console do Sites](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## O console de lançamentos {#the-launches-console}

>[!NOTE]
>
>Este console é somente para Inicializações de páginas.
>
>Para gerenciar os fragmentos de conteúdo, consulte [Inicializações para fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md).

O console Lançamentos fornece uma visão geral dos lançamentos e permite que você atue de acordo com os listados.

![Console Lançamento — Gerenciar conteúdo](/help/sites-cloud/authoring/assets/launches-navigate-launches-console.png)

O console pode ser acessado das seguintes maneiras:

* O Console **Ferramentas**: **Ferramentas**, **Geral**, **Inicializações**.

* **Console de Lançamentos**, na parte inferior da seção **Lançamentos** do painel **Referências** ao navegar pelo conteúdo de origem no console do Sites.

  ![Console de Lançamentos em Referências de lançamentos no console do Sites](/help/sites-cloud/authoring/assets/launches-references.png)

* O botão **Lançamentos**, na parte superior direita, ao navegar pelo conteúdo do lançamento no console do Sites:

  ![Opção Lançamentos, no console do Sites](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)
