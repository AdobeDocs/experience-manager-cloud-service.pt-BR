---
title: Reutilizar fragmentos de conteúdo usando MSM e Live Copies
description: Saiba mais sobre como usar a funcionalidade de Live Copy do MSM para usar o mesmo conteúdo de fragmento de conteúdo, ou similar, em vários locais, enquanto sincroniza com o conteúdo original.
badgeSaas: label="AEM Sites" type="Positive" tooltip="Aplicável ao AEM Sites)."
feature: Content Fragments
role: User
solution: Experience Manager Sites
hide: true
hidefromtoc: true
index: false
source-git-commit: 85b72909597a95531aea51719c841bc5db9c1a21
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 3%

---

# Reutilizar fragmentos de conteúdo usando o MSM {#reuse-content-fragments-using-msm}

O Gerenciador de vários sites (MSM) e a funcionalidade de Live Copy permitem usar o mesmo conteúdo em vários locais, ao mesmo tempo em que são sincronizados com o conteúdo original.

<!-- CQDOC-23473 - feature is currently beta so page is hidden, see metadata -->
<!-- CQDOC-23473 - screenshots -->
<!-- CQDOC-23473 - only mentioned once in ToC, add entries -->
<!-- CQDOC-23473 - will work on folders -->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!CAUTION]
>
>O MSM do console de Fragmento de conteúdo é, atualmente, a funcionalidade do Beta e está disponível somente para clientes específicos.
>
>O MSM para fragmentos de conteúdo também está disponível ao usar fragmentos de conteúdo por meio do console **Assets**.

* Com as Live Copies do MSM é possível:
   * Criar conteúdo uma vez
   * Reutilizar este conteúdo em outras áreas do mesmo site, em outros sites ou em aplicativos.
* O MSM mantém os relacionamentos dinâmicos entre o conteúdo original e suas Live Copies, de modo que:
   * Quando você altera o conteúdo original, ele e as Live Copies são sincronizados.
   * É possível fazer ajustes somente no conteúdo das Live Copies, desconectando o relacionamento dinâmico de subfragmentos e/ou componentes individuais.

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

Para obter uma visão geral detalhada dos conceitos do MSM, consulte Reutilização de conteúdo: gerenciador de vários sites e Live Copy.

<!--
For a detailed overview of MSM concepts see [Reusing Content: Multi Site Manager and Live Copy](/help/sites-cloud/administering/msm/overview.md).
-->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>A funcionalidade do Gerenciador de vários sites (MSM) no Adobe Experience Manager permite que os usuários reutilizem o conteúdo criado uma vez e depois reutilizado em vários locais da Web.

<!--
>[!NOTE]
>
>[Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md) functionality in Adobe Experience Manager enables users to reuse content that is authored once and then reused across multiple web-locations. 
-->

Ao usar o MSM para fragmentos de conteúdo, você pode:

* Crie fragmentos de conteúdo uma vez e faça cópias (vinculadas) desses fragmentos para reutilizar em outras áreas do site ou aplicativo.
* Manter várias cópias sincronizadas atualizando a cópia de origem uma vez e, em seguida, enviando as alterações para as cópias (ativas).
* Fazer alterações locais temporariamente ou permanentemente, suspendendo o vínculo entre fragmentos pai e filho; completamente ou para suas variações ou campos.

O MSM para fragmentos de conteúdo, combinado com a funcionalidade no Editor de fragmento de conteúdo, permite quebrar e restaurar a herança no nível do campo.

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>Esta página aborda a funcionalidade do MSM ao usar o console **Fragmentos de conteúdo**.
>
>O MSM para fragmentos de conteúdo também está disponível ao usar fragmentos de conteúdo por meio do console **Assets**.

<!--
>[!NOTE]
>
>This page covers MSM functionality when using the **Content Fragments** console.
>
>MSM for Content Fragments is also available when using [Content Fragments via the **Assets** console](/help/assets/content-fragments/content-fragments-msm.md). 
-->

## Criar uma Live Copy {#create-a-live-copy}

<!-- CQDOC-23473 - exclude children or referenced content fragments? -->

Para criar uma Live Copy do fragmento de conteúdo:

1. No console de Fragmentos de conteúdo, navegue até o local do fragmento.
1. Selecione o fragmento.
1. Selecione **Criar Live Copy** na barra de ferramentas superior.
1. Na caixa de diálogo aberta, especifique o destino e continue com **Próximo**.
1. Especifique as propriedades. Você pode especificar o título, o nome e se a Live Copy deve excluir filhos (fragmentos aninhados).
1. Continuar com **Próximo**.
1. Selecione se você deseja que a Live Copy seja criada imediatamente (**Agora**) ou em uma data e hora **Posterior**.
1. Confirme com **Criar Live Copy**.

   <!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

   >[!CAUTION]
   >
   >Se você quiser usar o MSM para criar cópias de Fragmentos de conteúdo), qualquer restrição **única** deverá ser removida de qualquer Tipo de dados usado nos respectivos Modelos de fragmento de conteúdo.

   <!--
   >[!CAUTION]
   >
   >If you want to use MSM to create copies of Content Fragments), then any **Unique** constraints should be removed from any Data Types used in the respective [Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md).
   -->

## Exibir propriedades e status {#view-properties-and-status}

Para exibir as propriedades e o status da origem e da Live Copy:

1. No console de Fragmentos de conteúdo, navegue até o local do fragmento.
1. Selecione o fragmento.
1. Selecione o ícone Informações (i) na coluna **Título** do fragmento.
O painel de informações direito será aberto.
1. Selecione a guia para **Detalhes da Live Copy**.

   ![Informações em uma Live Copy](/help/sites-cloud/administering/content-fragments/assets/cf-msm-information.png)

## Propagar modificações {#propagate-modifications}

Para propagar modificações entre a origem e a Live Copy.

### Sincronizar {#synchronize}

Para acionar uma sincronização que puxa as atualizações de conteúdo da Live Copy para a origem:

1. No console de Fragmentos de conteúdo, navegue até o local de origem do fragmento.
1. Selecione o fragmento.
1. Selecione **Sincronizar** na barra de ferramentas.
1. Confirme **Sincronizar** na caixa de diálogo.

### Implantação {#rollout}

Para acionar uma implantação que envia as atualizações de origem para a Live Copy:

1. No console de Fragmentos de conteúdo, navegue até o local da Live Copy do fragmento.
1. Selecione o fragmento.
1. Selecione **Implantação** na barra de ferramentas. O assistente será aberto para orientá-lo pelo processo.
1. Selecione as Live Copies a serem incluídas na implantação e **Continuar**.
1. Agende a implantação para imediatamente (**Agora**) ou **Depois**.
1. **Continuar** conforme apropriado.

<!-- CQDOC-23473 - feature is beta, is in authoring so remove here when GA -->

## Cancelar e reverter para herança no editor {#cancel-and-revert-to-inheritance-in-the-editor}

Herança é o mecanismo em que o conteúdo pode ser enviado automaticamente de um fragmento para outro. Campos herdados e variações podem ser o produto do Gerenciamento de vários sites.

Você pode cancelar (e depois reverter para) a herança no editor de fragmentos de conteúdo. Dependendo do contexto, isso pode estar disponível para uma variação ou um campo individual, se o fragmento fizer parte de uma live copy.

Por exemplo:

* Cancelar herança

  ![Ícone Cancelar herança](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-cancel-inheritance.png)

* Reverter para herança (se a herança já estiver cancelada)

  ![Ícone Reverter para herança](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-revert-to-inheritance.png)

<!-- CQDOC-23473 - feature is currently beta reinstate Note for GA -->

<!--
## Cancel, and revert to, inheritance {#cancel-and-reinstate-inheritance}

Inheritance is the mechanism where content can be automatically pushed from one fragment to another. Inherited fields, and variations, can be the product of Multi-Site Management.

You can cancel (then revert) the inheritance. Depending on the context, this can be available for a variation, or an individual field, if the fragment is part of a live copy.
-->

<!--
>[!NOTE]
>
>For more details see [Cancel, and revert to, inheritance in the editor](/help/sites-cloud/administering/content-fragments/authoring.md#cancel-and-revert-to-inheritance).
-->

## Comparar o MSM para fragmentos de conteúdo e páginas do Sites {#compare-msm-for-content-fragments-and-sites-pages}

<!-- CQDOC-23473 - needs a detailed review -->

Na maioria dos cenários, o MSM para fragmentos de conteúdo corresponde ao comportamento do MSM para a funcionalidade de páginas do Sites. Algumas diferenças importantes a serem observadas são:

* O blueprint no MSM para páginas do Sites é chamado de origem de Live Copy no MSM para fragmentos de conteúdo.
* Para páginas do Sites, você pode comparar um blueprint e sua live copy, mas não é possível para Fragmentos de conteúdo comparar uma origem à sua live copy.
* Não é possível editar uma live copy no Console de fragmentos de conteúdo.
* As páginas do Sites geralmente têm filhos, mas os fragmentos de conteúdo não, embora possam ter fragmentos referenciados. A opção de incluir ou excluir filhos se refere a esses fragmentos referenciados.
* A remoção da etapa de capítulos no assistente de criação de site não é compatível com o MSM para fragmentos de conteúdo.
* A configuração de bloqueios do MSM nas propriedades da página não é compatível com o MSM para fragmentos de conteúdo.
* Para o MSM para fragmentos de conteúdo, use somente a **configuração de implantação padrão**. Outras configurações de implantação não estão disponíveis para o MSM para fragmentos de conteúdo.

>[!NOTE]
>
>Lembre-se de que o MSM para fragmentos de conteúdo acessados por meio do console de Fragmentos de conteúdo é baseado na funcionalidade do Assets; isso ocorre porque eles são armazenados como Assets (embora considerados um recurso do Sites).

## Limitações {#limitations}

* Os acionadores durante a modificação e a configuração de implantação associada não existem para Fragmentos de conteúdo.
