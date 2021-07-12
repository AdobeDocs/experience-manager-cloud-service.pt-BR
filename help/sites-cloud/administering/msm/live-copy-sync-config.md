---
title: Configurar a sincronização da Live Copy
description: Saiba mais sobre as poderosas opções de sincronização da Live Copy disponíveis e como você pode configurá-las e personalizá-las para atender às necessidades do seu projeto.
feature: Gerenciamento de vários sites
role: Admin
exl-id: 0c97652c-edac-436e-9b5b-58000bccf534
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 30%

---

# Configurar a sincronização da Live Copy {#configuring-live-copy-synchronization}

O Adobe Experience Manager fornece várias configurações de sincronização prontas para uso. Antes de usar as Live Copies, você deve considerar o seguinte para definir como e quando as Live Copies são sincronizadas com o conteúdo de origem.

1. Decida se as configurações de implementação existentes atendem aos seus requisitos
1. Se as configurações de implementação existentes não o fizerem, decida se é necessário criar as suas próprias configurações.
1. Especifique as configurações de implementação a serem usadas para suas Live Copies.

## Configurações instaladas e personalizadas de implementação {#installed-and-custom-rollout-configurations}

Esta seção fornece informações sobre as configurações de implementação instaladas e as ações de sincronização que elas usam, além de como criar configurações personalizadas, se necessário.

>[!CAUTION]
>
>Atualizar ou alterar uma configuração de implementação predefinida é **não** recomendado. Se houver um requisito para uma ação ativa personalizada, ela deverá ser adicionada em uma configuração de implementação personalizada.

### Acionadores de implementação {#rollout-triggers}

Cada configuração de implementação usa um acionador de implementação que faz com que a implementação ocorra. As configurações de implementação podem usar um dos seguintes acionadores:

* **Na implantação**: O comando  **** Rolloutcommand é usado na página de impressão azul, ou o comando  **** Synchronizececmand é usado na página Live Copy.
* **Em modificação**: a página de origem é modificada.
* **Em ativação**: a página de origem é ativada.
* **Em desativação**: a página de origem é desativada.

>[!NOTE]
>
>O uso do acionador **Em modificação** pode afetar o desempenho. Consulte [Práticas recomendadas do MSM](best-practices.md#onmodify) para obter mais informações.

### Configurações de implementação {#rollout-configurations}

A tabela a seguir lista as configurações de implementação fornecidas com AEM prontas para uso. A tabela inclui as ações de acionador e de sincronização de cada configuração de implementação.

<!--
If the installed rollout configuration actions do not meet your requirements, you can [create a new rollout configuration](#creating-a-rollout-configuration).
-->

| Nome | Descrição | Acionar | [Ações de sincronização](#synchronization-actions) |
|---|---|---|---|
| Configuração de implantação padrão | A configuração de implementação padrão que permite que o processo de implementação comece com estímulos de implementação e executa as ações: criar, atualizar, excluir conteúdo e ordenar os nós filhos | Na implantação | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`productUpdate`<br>`orderChildren` |
| Acionar com a ativação do blueprint | Publica a Live Copy quando a fonte é publicada | No modo de ativação | `targetActivate` |
| Desligar com a desativação do blueprint | Desativa a Live Copy quando a origem é desativada | Na desativação | `targetDeactivate` |
| Forçar modificação | Força o conteúdo para a Live Copy quando a origem é modificada<br>Use essa configuração de implementação com moderação, pois usa o acionador Em modificação . | Em modificação | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren` |
| Forçar modificação (superficial) | Força o conteúdo para a Live Copy quando a página do blueprint é modificada, sem atualizar referências (por exemplo, para cópias superficiais)<br>Use essa configuração de implementação com moderação, pois usa o acionador Em modificação. | Em modificação | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`orderChildren` |
| Promover lançamento | Configuração de implementação padrão para a promoção de páginas de inicialização. | Na implantação | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren`<br>`markLiveRelationship` |

### Ações de sincronização {#synchronization-actions}

A tabela a seguir lista as ações de sincronização fornecidas com AEM prontas para uso.

<!--If the installed actions do not meet your requirements, you can [Create a New Synchronization Action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).-->

| Nome da ação | Descrição | Propriedades |
|---|---|---|
| `contentCopy` | Quando os nós da origem não existem na Live Copy, essa ação copia os nós para a Live Copy. [Configure o Serviço de cópia de conteúdo MSM  **CQ** ](#excluding-properties-and-node-types-from-synchronization) para especificar os tipos de nó, itens de parágrafo e propriedades de página a serem excluídos. |  |
| `contentDelete` | Essa ação exclui os nós da Live Copy que não existem na origem. [Configure o Serviço de exclusão de conteúdo MSM  **CQ** ](#excluding-properties-and-node-types-from-synchronization) para especificar os tipos de nó, itens de parágrafo e propriedades de página a serem excluídos. |  |
| `contentUpdate` | Esta ação atualiza o conteúdo da Live Copy com as alterações da origem. [Configure o Serviço de atualização de conteúdo MSM  **CQ** ](#excluding-properties-and-node-types-from-synchronization) para especificar os tipos de nó, itens de parágrafo e propriedades de página a serem excluídos. |  |
| `editProperties` | Essa ação edita as propriedades da Live Copy. A propriedade `editMap` determina quais propriedades são editadas e seu valor. O valor da propriedade `editMap` deve usar o seguinte formato:<br>`[property_name_n]#[current_value]#[new_value]`<br>`current_value` e `new_value` são expressões regulares e `n` é um número inteiro incrementado.<br>Por exemplo, considere o seguinte valor para  `editMap`:<br>`sling:resourceType#/(contentpage` `homepage)#/mobilecontentpage,cq:template#/contentpage#/mobilecontentpage`<br>Este valor edita as propriedades dos nós da Live Copy da seguinte maneira:<br>As  `sling:resourceType` propriedades que estão definidas como  `contentpage` ou como  `homepage` estão definidas como  `mobilecontentpage`.<br>As  `cq:template` propriedades definidas como  `contentpage` são definidas como  `mobilecontentpage`. | `editMap: (String)` identifica a propriedade, o valor atual e o novo valor. Consulte a descrição para obter mais informações. |
| `notify` | Essa ação envia um evento de página que a página foi distribuída. Para ser notificado, é necessário primeiro assinar eventos de distribuição. |  |
| `orderChildren` | Essa ação ordena os nós filhos com base na ordem no blueprint. |  |
| `referencesUpdate` | Esta ação de sincronização atualiza referências na Live Copy.<br>Ele pesquisa caminhos nas páginas da Live Copy que apontam para um recurso dentro do blueprint. Quando encontrado, ele atualiza o caminho para apontar para o recurso relacionado dentro da Live Copy. As referências que têm destinos fora do blueprint não são alteradas. <br>[Configure o Serviço de atualização de referências MSM  **** ](#excluding-properties-and-node-types-from-synchronization) CQ para especificar os tipos de nó, itens de parágrafo e propriedades de página a serem excluídos. |  |
| `targetVersion` | Esta ação cria uma versão da Live Copy.<br>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação. |  |
| `targetActivate` | Essa ação ativa a Live Copy.<br>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação. |  |
| `targetDeactivate` | Essa ação desativa a Live Copy.<br>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação. |  |
| `workflow` | Essa ação inicia o fluxo de trabalho definido pela propriedade de destino (somente para páginas) e assume a Live Copy como carga útil.<br>O caminho de destino é o caminho do nó do modelo. | `target: (String)` é o caminho para o modelo de fluxo de trabalho. |
| `mandatory` | Essa ação define a permissão de várias ACLs na página Live Copy como somente leitura para um grupo de usuários específico. As seguintes ACLs estão configuradas:<br>`ActionSet.ACTION_NAME_REMOVE`<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>Use esta ação somente para páginas. | `target: (String)` é a ID do grupo para o qual você está definindo permissões. |
| `mandatoryContent` | Essa ação define a permissão de várias ACLs na página Live Copy como somente leitura para um grupo de usuários específico. As seguintes ACLs estão configuradas:<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>Use esta ação somente para páginas. | `target: (String)` é a ID do grupo para o qual você está definindo permissões. |
| `mandatoryStructure` | Essa ação define a permissão da ACL `ActionSet.ACTION_NAME_REMOVE` na página Live Copy como somente leitura para um grupo de usuários específico.<br>Use esta ação somente para páginas. | `target: (String)` é a ID do grupo para o qual você está definindo permissões. |
| `VersionCopyAction` | Se o blueprint/página de origem tiver sido publicado pelo menos uma vez, essa ação criará uma página de Live Copy usando a versão publicada. Observação: esta ação só está disponível para criar uma página Live Copy com base em uma página de origem publicada, não para atualizar uma página Live Copy existente. |  |
| `PageMoveAction` | O `PageMoveAction` se aplica quando uma página foi movida no blueprint.<br>A ação copia em vez de mover a página Live Copy (relacionada) do local antes de mover para o local depois.<br>O  `PageMoveAction` não altera a página da Live Copy no local antes da movimentação. Portanto, para configurações de implementação consecutivas, ele tem o status de uma relação ao vivo sem um blueprint.<br>[**** Configure o serviço de Ação de movimentação de página MSM CQ](#excluding-properties-and-node-types-from-synchronization) para especificar os tipos de nó, itens de parágrafo e propriedades de página a serem excluídos.<br>Essa ação deve ser a única ação de sincronização incluída em uma configuração de implementação. | Defina `prop_referenceUpdate: (Boolean)` como true (padrão) para atualizar referências. |
| `markLiveRelationship` | Esta ação Indica que existe uma relação ativa para o conteúdo criado na inicialização. |  |

<!--
### Creating a Rollout Configuration {#creating-a-rollout-configuration}

You can [create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) when the installed rollout configurations do not meet your application requirements by performing the following steps.

1. [Create the rollout configuration](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
1. [Add synchronization actions to the rollout configuration](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

The new rollout configuration is then available to you when configuring rollout configurations on a blueprint or Live Copy page.
-->

### Excluir propriedades e tipos de nó da sincronização {#excluding-properties-and-node-types-from-synchronization}

Você pode configurar vários serviços OSGi que suportam ações de sincronização correspondentes para que eles não afetem tipos de nó e propriedades específicos. Por exemplo, muitas propriedades e subnós relacionados ao funcionamento interno de AEM não devem ser incluídos em uma Live Copy. Somente o conteúdo relevante para o usuário da página deve ser copiado.

Ao trabalhar com AEM, há vários métodos de gerenciamento das configurações desses serviços. Consulte [Configuração do OSGi](/help/implementing/deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

A tabela a seguir lista as ações de sincronização para as quais você pode especificar os nós a serem excluídos. A tabela fornece os nomes dos serviços a serem configurados usando o Console na Web e o PID para configurar o usando um nó de repositório.

| Ação de sincronização | Nome do serviço no Console da Web | PID do serviço |
|---|---|---|
| `contentCopy` | Ação de cópia de conteúdo MSM CQ | `com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory` |
| `contentDelete` | Ação de exclusão de conteúdo MSM CQ | `com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory` |
| `contentUpdate` | Ação de atualização de conteúdo do MSM CQ | `com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory` |
| `PageMoveAction` | Ação de movimentação de página MSM CQ | `com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory` |
| `referencesUpdate` | Ação de atualização de referências do MSM CQ | `com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory` |

A tabela a seguir descreve as propriedades que você pode configurar:

| Propriedade do Console da Web | Propriedade OSGi | Descrição |
|---|---|---|
| Tipos de nó excluídos | `cq.wcm.msm.action.excludednodetypes` | Uma expressão regular que corresponde aos tipos de nó a serem excluídos da ação de sincronização |
| Itens de parágrafo excluídos | `cq.wcm.msm.action.excludedparagraphitems` | Uma expressão regular que corresponde aos itens de parágrafo que serão excluídos da ação de sincronização |
| Propriedades da página excluída | `cq.wcm.msm.action.excludedprops` | Uma expressão regular que corresponde às propriedades de página que serão excluídas da ação de sincronização |
| Tipos de nó Mixin ignorados | `cq.wcm.msm.action.ignoredMixin` | Uma expressão regular que corresponde aos nomes dos tipos de nó mixin a serem excluídos da ação de sincronização (disponível somente para a ação `contentUpdate`) |

#### Ação de atualização de conteúdo do MSM CQ - Exclusões {#cq-msm-content-update-action-exclusions}

Várias propriedades e tipos de nó são excluídas por padrão, elas são definidas na configuração OSGi da **Ação de atualização de conteúdo do MSM CQ**, em **Propriedades de página excluídas**.

Por padrão, as propriedades que correspondentes às seguintes expressões comuns são excluídas (ou seja, não é atualizada) na implementação:

![Regexes de exclusão da Live Copy](../assets/live-copy-exclude.png)

É possível alterar as expressões definindo a lista de exclusões conforme necessário.

Por exemplo, se você quiser que o **Título** da página seja incluído nas alterações consideradas para implementação, remova `jcr:title` das exclusões. Por exemplo, com o regex:

`jcr:(?!(title)$).*`

### Configurar sincronização para atualizar referências {#configuring-synchronization-for-updating-references}

Você pode configurar vários serviços OSGi que oferecem suporte às ações de sincronização correspondentes relacionadas à atualização de referências.

Ao trabalhar com AEM, há vários métodos de gerenciamento das configurações desses serviços. Consulte [Configuração do OSGi](/help/implementing/deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

A tabela a seguir lista as ações de sincronização para as quais você pode especificar a atualização de referência. A tabela fornece os nomes dos serviços a serem configurados usando o Console na Web e o PID para configurar o usando um nó de repositório.

| Propriedade do Console da Web | Propriedade OSGi | Descrição |
|---|---|---|
| Atualizar referência entre LiveCopies aninhados | `cq.wcm.msm.impl.action.referencesupdate.prop_updateNested` | Selecione essa opção no console da Web ou defina essa propriedade booleana como `true` usando a configuração do repositório para substituir referências que direcionam qualquer recurso que esteja na ramificação da Live Copy mais alta. Disponível somente para a ação `referencesUpdate`. |
| Atualizar páginas de referência | `cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate` | Selecione essa opção no console da Web ou defina essa propriedade booleana como `true` usando a configuração do repositório para atualizar quaisquer referências para usar a página original para fazer referência à página Live Copy. Disponível somente para `PageMoveAction`. |

## Especificar as configurações de implementação a serem usadas {#specifying-the-rollout-configurations-to-use}

O MSM permite que você especifique conjuntos de configurações de implementação que são usadas geralmente e, quando necessário, você pode substituí-los por Live Copies específicos. O MSM fornece vários locais para especificar as configurações de implementação a serem usadas. O local determina se a configuração se aplica a uma Live Copy específica.

A seguinte lista de locais onde você pode especificar as configurações de implementação a serem usadas descreve como o MSM determina quais configurações de implementação usar para uma Live Copy:

* **[Propriedades da página de Live Copy](live-copy-sync-config.md#setting-the-rollout-configurations-for-a-live-copy-page):** quando uma página de Live Copy é configurada para usar uma ou mais configurações de implementação, o MSM usa essas configurações.
* **[Propriedades da página do blueprint](live-copy-sync-config.md#setting-the-rollout-configuration-for-a-blueprint-page):** quando uma Live Copy é baseada em um blueprint e a página Live Copy não está configurada com uma configuração de implementação, a configuração de implementação associada à página de origem do blueprint é usada.
* **Propriedades da página pai da Live Copy:** quando nem a página Live Copy nem a página de origem do blueprint são configuradas com uma configuração de implementação, a configuração que se aplica à página pai da página Live Copy é usada.
* **[Padrão do sistema](live-copy-sync-config.md#setting-the-system-default-rollout-configuration):** Quando a configuração de implementação da página pai da Live Copy não pode ser determinada, a configuração de implementação padrão do sistema é usada.

Por exemplo, um blueprint usa o site [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) como conteúdo de origem. Um site é criado a partir do blueprint. Cada item da lista a seguir descreve um cenário diferente sobre o uso de configurações de implementação:

* Nenhuma das páginas do blueprint ou da Live Copy é configurada para usar uma configuração de implementação. O MSM usa a configuração de implementação padrão do sistema para todas as páginas da Live Copy.
* A página raiz do site WKND é configurada com várias configurações de implementação. O MSM usa essas configurações de implementação para todas as páginas da Live Copy.
* A página raiz do site WKND é configurada com várias configurações de implementação, e a página raiz do site Live Copy é configurada com um conjunto diferente de configurações de implementação. O MSM usa as configurações de implementação configuradas na página raiz do site Live Copy.

### Definir as configurações de implementação de uma página de Live Copy {#setting-the-rollout-configurations-for-a-live-copy-page}

Configure uma página de Live Copy com as configurações de implementação a serem usadas quando a página de origem for distribuída. As páginas secundárias herdam a configuração por padrão. Ao configurar a configuração de implementação a ser usada, você está substituindo a configuração que a página Live Copy herda de seu pai.

Você também pode configurar as configurações de implementação para uma página de Live Copy quando [criar a Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page).

1. Use o console **Sites** para selecionar a página Live Copy.
1. Selecione **Propriedades** na barra de ferramentas.
1. Abra a guia **Live Copy**.

   A seção **Configuração** mostra as configurações de implementação que a página herda.

   ![Herança da Live Copy da página principal](../assets/live-copy-inherit.png)

1. Se necessário, ajuste o sinalizador de **Herança da Live Copy**. Se marcada, a configuração da Live Copy entrará em vigor em todos os filhos.

1. Desmarque a propriedade **Herdar configuração de implementação do Pai** e selecione uma ou mais configurações de implementação na lista.

   As configurações de implementação selecionadas aparecem abaixo da lista suspensa.

   ![Substituição da herança de configuração da Live Copy](../assets/live-copy-inherit-override.png)

1. Clique ou toque em **Salvar e fechar**.

### Definir a configuração de implementação de uma página do blueprint {#setting-the-rollout-configuration-for-a-blueprint-page}

Configure uma página do blueprint com as configurações de implementação a serem usadas quando a página do blueprint for distribuída.

Observe que as páginas secundárias da página do blueprint herdam a configuração. Ao definir a configuração de implementação a ser usada, você pode estar substituindo a configuração que a página herda de seu pai.

1. Use o console **Sites** para selecionar a página raiz do blueprint.
1. Selecione **Propriedades** na barra de ferramentas.
1. Abra a guia **Blueprint.**
1. Selecione uma ou mais **configurações de implementação** usando o seletor suspenso.
1. Mantenha suas atualizações com **Salvar**.

### Definir a configuração de implementação padrão do sistema {#setting-the-system-default-rollout-configuration}

Para especificar uma configuração de implementação a ser usada como padrão do sistema, configure o seguinte serviço OSGi.

* **Day CQ WCM Live Relationship** Manager com o PID de serviço  `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

Configure o serviço usando o [console da Web](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou um [nó do repositório](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* No console da Web, o nome da propriedade a ser configurada é **Default rollout config**.
* Usando um nó de repositório, o nome da propriedade a ser configurada é `liverelationshipmgr.relationsconfig.default`.

Defina esse valor de propriedade como o caminho da configuração de implementação a ser usada como padrão do sistema. O valor padrão é `/libs/msm/wcm/rolloutconfigs/default`, que é a **Configuração de implementação padrão**.
