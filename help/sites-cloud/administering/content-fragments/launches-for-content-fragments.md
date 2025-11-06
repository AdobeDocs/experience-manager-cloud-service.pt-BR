---
title: Lançamentos para fragmentos de conteúdo
description: Saiba como usar Inicializações para fragmentos de conteúdo no Adobe Experience Manager as a Cloud Service. Os lançamentos permitem desenvolver conteúdo com eficiência para uma versão futura, mantendo os fragmentos de conteúdo atuais.
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
exl-id: c0b9e571-3be5-42ab-8d56-d93e8ef4c2f7
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 1%

---

# Lançamentos para fragmentos de conteúdo {#launches-for-content-fragments}

No Adobe Experience Manager (AEM) as a Cloud Service, os Lançamentos permitem desenvolver conteúdo com eficiência para uma versão futura.

Uma *Inicialização* é criada para permitir que você faça alterações na preparação de uma publicação futura, ao mesmo tempo em que mantém o conteúdo atual. Para fragmentos de conteúdo, isso significa que você está editando duas versões ao mesmo tempo: o conteúdo que está publicado no momento e uma versão desse conteúdo que será publicada posteriormente. Depois que esse tempo chegar, você poderá substituir o conteúdo dos fragmentos de conteúdo originais e publicar as novas versões.

>[!NOTE]
>
>Lançamentos também estão disponíveis para Páginas. Os conceitos básicos são os mesmos, mas há diferenças em como gerenciá-los no AEM.
>
>Para obter detalhes completos, consulte [Inicializações para páginas](/help/sites-cloud/authoring/launches/overview.md).

Você cria uma *Inicialização* e, em seguida, edita e atualiza os fragmentos de conteúdo na *Inicialização*. Se forem feitas alterações nos fragmentos do *Source* durante esta fase, você poderá copiá-las para o *Launch* com a operação *Rebase*. Quando pronto, *Promover* duplica o conteúdo da inicialização de volta para a origem. Em seguida, você pode ativar os fragmentos de origem manual ou automaticamente (dependendo dos campos definidos ao criar e editar a inicialização). Você também pode especificar se os fragmentos referenciados devem ser incluídos nesse processo.

Por exemplo, os fragmentos de produto sazonais da loja online são atualizados trimestralmente para que os produtos em destaque se alinhem à temporada atual. Para se preparar para a próxima atualização trimestral, é possível criar uma inicialização dos fragmentos apropriados. Ao longo do trimestre, as seguintes alterações são acumuladas na cópia do lançamento:

* Edições realizadas diretamente nos fragmentos de lançamento como preparação para o próximo trimestre.
* Alterações nos Fragmentos de Conteúdo de origem que você transfere para as páginas de inicialização com *Rebase*.
* Você também pode navegar pelo conteúdo na ramificação de inicialização; adicionar ou remover fragmentos, conforme necessário.

Quando o próximo trimestre chegar, você promoverá as páginas de lançamento para poder publicar as páginas de origem (mantendo o conteúdo atualizado). É possível promover todos os fragmentos ou somente aqueles que você modificou.

![Visão geral das inicializações - Rebasear e Promover](/help/sites-cloud/administering/content-fragments/assets/cf-launches-overview.png)

Esta seção descreve como criar, editar, gerenciar, trocar base, promover e, se necessário, excluir inicializações do [Console de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md):

* [Acessar e exibir inicializações no console de Fragmentos de conteúdo](#launches-in-the-content-fragment-console)
* [Criar um lançamento](#create-a-launch)
* [Editar conteúdo do lançamento](#edit-launch-content)
* [Gerenciar conteúdo em um lançamento](#manage-content-within-a-launch)
* [Comparar o Launch à origem](#compare-launch-to-source)
* [Rebasear uma inicialização do Source](#rebase-a-launch-from-source)
* [Promover uma inicialização para o Source](#promote-a-launch-to-source)
* [Excluir um lançamento](#delete-a-launch)

## Lançamentos no Console de fragmentos de conteúdo {#launches-in-the-content-fragment-console}

A guia **Inicializações** do console de Fragmentos de conteúdo permite criar inicializações, listar todas as inicializações existentes, ver as principais propriedades e realizar ações sobre elas.

Quando nenhuma inicialização é selecionada, você pode [criar uma nova inicialização](#create-a-launch).

![Guia Inicializações no console](/help/sites-cloud/administering/content-fragments/assets/cf-launches-tab.png)

Selecione o seu lançamento para mostrar:

* a barra de ferramentas, com as ações disponíveis
* o painel direito, mostrando propriedades e outras ações

![Iniciar a barra de ferramentas de ações no console](/help/sites-cloud/administering/content-fragments/assets/cf-launches-actions.png)

A barra de ferramentas permite:

* **[Abrir lançamento](#edit-launch-content)**
* **[Editar fontes](#manage-content-within-a-launch)**
* **[Comparar Inicialização com Source](#compare-launch-to-source)**
* **[Promover](#promote-a-launch-to-source)**
* **[Rebase](#promote-a-launch-to-source)**
* **[Excluir lançamento](#delete-a-launch)**

Embora o painel direito permita:

* Editar o **Título** de inicialização
* Editar a **Descrição** de Inicialização
* Atualize os detalhes de configuração que foram definidos quando você [criou a inicialização](#create-a-launch):

   * **Incluir referências**: crie a inicialização com ou sem, incluindo qualquer Fragmento de conteúdo referenciado. Por padrão, os fragmentos referenciados são incluídos.

      * Os fragmentos referenciados também são afetados quando você [adiciona ou remove fragmentos da inicialização](#manage-content-within-a-launch) em um estágio posterior.

     >[!NOTE]
     >
     >Consulte [Detalhes sobre referências incluídas](#details-concerning-included-references)

   * **Publicar pronto**; Habilitar essa opção publicará automaticamente os fragmentos quando a inicialização for promovida para a origem.

* E também definir:

   * A **Promover Data** e Hora: se a [inicialização for promovida automaticamente](#promote-automatically)

## Criar um lançamento {#create-a-launch}

Para criar seu lançamento:

1. Navegue até o Console de fragmentos de conteúdo.

1. Abra a guia **Inicializações**.

1. Selecione **Criar inicialização**.

1. Navegue até a pasta apropriada e selecione os fragmentos a serem incluídos no lançamento:

   ![Selecionar fragmentos de conteúdo para o novo lançamento](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-select-cfs.png)

1. Selecione **Próximo**.

1. Especifique os detalhes para configurar o lançamento:

   * **Título**
   * **Descrição**
   * **Incluir referências**: crie a inicialização com ou sem, incluindo qualquer Fragmento de conteúdo referenciado. Por padrão, os fragmentos referenciados são incluídos.

     >[!NOTE]
     >
     >Consulte [Detalhes sobre referências incluídas](#details-concerning-included-references)

   * **Publicar pronto**: habilitar essa opção publicará automaticamente os fragmentos quando a inicialização for promovida na origem.

   ![Detalhes da nova inicialização](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-launch-details.png)

1. **Salve** a configuração.

1. Você retornará à guia **Inicializações** do console de Fragmentos de conteúdo, onde:

   * seu novo lançamento está listado
   * uma mensagem é exibida para confirmar que a criação do lançamento foi iniciada:

      * **O trabalho iniciou a criação de uma nova inicialização, monitore o progresso no AEM e recarregue a página quando concluído.**

1. Selecione **Exibir**, na caixa de mensagem, para ver mais detalhes no console do AEM para [Operações em Segundo Plano](/help/operations/asynchronous-jobs.md).

   ![Nova inicialização no console](/help/sites-cloud/administering/content-fragments/assets/cf-launches-new-launch-in-console.png)

## Editar conteúdo do lançamento {#edit-launch-content}

Para editar os fragmentos de conteúdo no seu lançamento:

1. Navegue até o Console de fragmentos de conteúdo.

1. Abra a guia **Inicializações**.

1. Selecione o seu lançamento para mostrar as ações da barra de ferramentas.

1. Selecione **Abrir lançamento**.

   Seu lançamento será mostrado junto com os fragmentos que ele contém.

   ![Editar conteúdo da inicialização](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-launch-content.png)

1. Selecione **Editar** para o fragmento que deseja atualizar. Ele será aberto no [editor de fragmentos](/help/sites-cloud/administering/content-fragments/authoring.md) como de costume.

## Gerenciar conteúdo em um lançamento {#manage-content-within-a-launch}

Para gerenciar os fragmentos de conteúdo no seu lançamento e também editar o conteúdo:

1. Navegue até o Console de fragmentos de conteúdo.

1. Abra a guia **Inicializações**.

1. Selecione o seu lançamento.

1. Selecione **Editar fontes**.

   Os fragmentos de origem do seu lançamento serão mostrados.

   ![Editar Source](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-sources.png)

1. É possível:

   1. **Adicione fontes** para adicionar mais fragmentos à sua inicialização.

      * Se **Incluir referências** for verdadeiro para a inicialização, todos os Fragmentos de conteúdo referenciados também serão trazidos para a inicialização (se ainda não estiverem presentes).

   1. Selecione **Editar** para o fragmento de origem que você deseja atualizar. Ele será aberto no [editor de fragmentos](/help/sites-cloud/administering/content-fragments/authoring.md) como de costume.

   1. Selecione um fragmento e depois a ação **Excluir fontes** da barra de ferramentas para remover esse fragmento da inicialização.

      * Se **Incluir referências** for verdadeiro para a inicialização, todos os Fragmentos de conteúdo referenciados também serão removidos da inicialização, a menos que também sejam referenciados por outros Fragmentos de conteúdo ainda na inicialização.

   >[!NOTE]
   >
   >Consulte [Detalhes sobre referências incluídas](#details-concerning-included-references)

## Comparar o Launch à origem {#compare-launch-to-source}

É recomendável que, antes de qualquer ação Rebase ou Promover, você sempre compare a origem e o lançamento para confirmar as alterações e o impacto no conteúdo (ambas as ações substituem o conteúdo de destino):

1. Navegue até o Console de fragmentos de conteúdo.

1. Abra a guia **Inicializações**.

1. Selecione o seu lançamento.

1. Selecione **Comparar Inicialização com Source**.

   * Os fragmentos de origem e de inicialização são mostrados lado a lado para destacar as diferenças.
      * Os fragmentos do Source são exibidos à esquerda e os fragmentos do Launch são exibidos à direita.
      * As atualizações são destacadas:
         * Source: azul
         * Launch: rosa
         * Conflitos: amarelo
   * As ações [Promover](#promote-a-launch-to-source) e [Rebase](#rebase-a-launch-from-source) estão disponíveis na parte superior direita.
   * **Atualizações encontradas**: no canto superior esquerdo, um resumo de todas as atualizações é exibido. O número de atualizações de origem em azul, o número de atualizações do Launch em rosa e atualizações para ambos (conflitos) em amarelo.
      * Os ícones de olho permitem mostrar ou ocultar as atualizações de conteúdo reais para obter uma visão geral mais clara.
   * Os controles deslizantes **Incluir** permitem definir os Fragmentos de conteúdo a serem incluídos na operação subsequente de Promover ou Rebasear:
      * **Incluir tudo** na parte superior direita
      * **Incluir** acima de cada fragmento na inicialização

     >[!NOTE]
     >
     >Os controles deslizantes se aplicam apenas às ações Promover e Rebasear tiradas da tela Comparar.

   * O conteúdo do fragmento é exibido no nível do campo (elemento do fragmento de conteúdo/nível do tipo de dados); com realces indicando alterações.
   * Selecione **Exibir** para recalcular as diferenças.

   ![Comparar Source e Launch](/help/sites-cloud/administering/content-fragments/assets/cf-launches-compare.png)

## Trocar base de uma inicialização (do Source) {#rebase-a-launch-from-source}

Quando forem feitas atualizações nos fragmentos de origem e você quiser copiar essas alterações para o seu lançamento:

1. Navegue até o Console de fragmentos de conteúdo.

1. Abra a guia **Inicializações**.

1. Selecione o lançamento e os fragmentos.

1. Selecione **Rebase**.

>[!NOTE]
>
>Você também pode **Rebasear** um lançamento de **[Comparar o Launch com o Source](#compare-launch-to-source)**.

## Promover uma inicialização (para o Source) {#promote-a-launch-to-source}

Quando o lançamento estiver pronto para ser publicado, ele deverá ser copiado para a origem. Você pode fazer isso no console ou definir as configurações para que isso aconteça automaticamente em uma data e hora específicas.

### Promover manualmente {#promote-manually}

Quando o lançamento estiver pronto para ser publicado, ele poderá ser copiado para a origem com a ação explícita:

1. Navegue até o Console de fragmentos de conteúdo.

1. Abra a guia **Inicializações**.

1. Selecione o lançamento e os fragmentos.

1. Selecione **Promover**.

>[!NOTE]
>
>Você também pode **Promover** uma inicialização de **Comparar Inicialização com a Source**.

### Promover automaticamente {#promote-automatically}

Para que um lançamento seja promovido automaticamente em uma data e hora especificadas, é necessário:

1. Defina a **Data de Promoção** e a Hora no painel direito da [guia Inicializações](#launches-in-the-content-fragment-console).

1. Se o conteúdo puder ser publicado quando for promovido, defina **Publicar pronto** ao [criar a inicialização](#create-a-launch), ou no painel direito da [guia Inicializações](#launches-in-the-content-fragment-console).

## Excluir um lançamento {#delete-a-launch}

Depois de promover o lançamento ou decidir que não precisa mais dele, você pode excluí-lo:

1. Navegue até o Console de fragmentos de conteúdo.

1. Abra a guia **Inicializações**.

1. Selecione o seu lançamento.

1. Selecione **Excluir Inicialização**.

   Você será solicitado a confirmar a ação antes que a inicialização seja excluída.

## Detalhes relativos às referências incluídas {#details-concerning-included-references}

Para Inicializações, as seguintes referências de Fragmento de conteúdo são consideradas, dependendo do [tipo de dados](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types):

* O tipo de dados **Referência de fragmento**, aplicável a referências de fragmento único e a referências de fragmento de vários campos.
* Fragmentos referenciados dentro do tipo de dados **Texto de várias linhas** ao usar **Rich Text**.

Todos os pontos também são aplicáveis a fragmentos referenciados em variações

Os seguintes não são considerados:

* Fragmentos referenciados dentro de tipos de dados de referência de conteúdo, **Referência de Conteúdo** (baseada em caminho) e **Referência de Conteúdo (UUID)**.
* Fragmentos referenciados dentro do tipo de dados **Referência de Fragmento (UUID)**.
