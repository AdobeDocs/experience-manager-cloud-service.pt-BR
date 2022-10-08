---
title: Práticas recomendadas do MSM
description: Conheça as práticas recomendadas compiladas pelas equipes de engenharia e consultoria da Adobe para ajudar a começar a usar o Gerenciamento de vários sites do AEM.
feature: Multi Site Manager
role: Admin
exl-id: 61b8ded8-3b9e-423f-85a9-7280e1a721cc
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 97%

---

# Práticas recomendadas do MSM {#msm-best-practices}

## Geral {#general}

O MSM é uma estrutura configurável para automatizar a implantação de conteúdo. As implementações geralmente envolvem partes importantes de um site e abrangem organizações e regiões geográficas. Portanto, é altamente recomendável planejar as implementações do MSM com o cuidado necessário ao planejar seu site:

* Cuidadosamente **planeje a estrutura do plano e os fluxos de conteúdo** antes de iniciar a implementação.
* **Personalize o quanto for necessário, mas o mínimo possível.** Embora o MSM suporte um alto grau de personalização (por exemplo, configurações de implementação), a prática recomendada para o desempenho, confiabilidade e atualização de seu site é minimizar a personalização.
* Estabeleça um modelo de **governança** desde o início e treine os usuários adequadamente para garantir o sucesso. Uma prática recomendada do ponto de vista da governança é **minimizar a autoridade que os produtores de conteúdo locais têm** para alocar/conectar conteúdo a outros usuários locais e suas respectivas Live Copies. Isso ocorre porque heranças encadeadas e sem governança podem aumentar significativamente a complexidade de uma estrutura do MSM e comprometer seu desempenho e confiabilidade.
* Quando existir um plano para sua estrutura, fluxos de conteúdo, automação e governança, **crie um protótipo e teste completamente seu sistema** antes de iniciar uma implementação real.
* Lembre-se que a **Adobe Consulting e os principais integradores de sistema** têm ampla experiência em planejar e implementar a automação de conteúdo com o MSM, então eles podem ajudar você a começar o projeto do MSM e durante toda a implementação.

## Origens de Live Copy e configurações de blueprint {#live-copy-sources-and-blueprint-configurations}

Lembre-se de que uma Live Copy pode ser criada usando [páginas normais](creating-live-copies.md#creating-a-live-copy-of-a-page) ou uma [configuração de blueprint](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Ambos são casos de uso válidos.

Os benefícios adicionais de usar configurações de blueprint são que elas:

* Permitem que o autor use a opção de **Implantação** em um blueprint para enviar modificações explicitamente para as Live Copies que herdam deste blueprint.
* Permitem que o autor use a funcionalidade **Criar Site** para selecionar idiomas facilmente e configurar a estrutura da Live Copy.
* Definir uma configuração de implantação padrão para Live Copies que tenham uma relação com o blueprint.

No caso de uma configuração de blueprint não ser mencionada, as implantações só podem ser iniciadas a partir das próprias Live Copies, essencialmente obtendo conteúdo na origem.

Ao criar um novo site com a Live Copy, é vantajoso criar configurações de blueprint para garantir a disponibilidade do conjunto completo de recursos do MSM.

>[!NOTE]
>
> Observe que os CUGs na guia Permissões não podem ser implantados em Live Copies de blueprints. Planeje isso ao configurar a Live Copy.

## Sincronização de componentes e contêineres {#components-and-container-synchronization}

Em geral, a regra de implantação no MSM em relação à sincronização de componentes é:

* Os componentes são implementados sincronizando os recursos contidos no blueprint.
* Os contêineres sincronizam somente o recurso atual.

Isso significa que os componentes são tratados como um agregado e, em uma implantação, o próprio componente e todos os seus componentes secundários são substituídos por aqueles nos blueprints. Isso significa que, se um recurso for adicionado localmente a esse componente, ele será perdido no conteúdo do blueprint durante a implantação.

Para suportar o aninhamento de componentes de modo que os componentes adicionados localmente sejam mantidos em uma implantação, o componente deve ser declarado como um contêiner.

>[!NOTE]
>
>Adicione a propriedade `cq:isContainer` ao componente para designá-lo como um contêiner.

## Criar site {#create-site}

Observe que o AEM tem duas abordagens principais para a criação de Live Copies:

* Ao [criar uma Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page) — essa pode ser considerada a abordagem mais genérica, permitindo que você crie Live Copies de qualquer página. A estrutura de conteúdo de uma Live Copy corresponde exatamente à origem.

* Ao [criar um site](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) — esta é uma abordagem mais especializada, principalmente para criar sites com uma estrutura multilíngue.

Estas são algumas considerações que devem ser levadas em conta ao criar um site:

* Para criar um novo site, você precisa de uma [configuração de blueprint](creating-live-copies.md#managing-blueprint-configurations).
* Para permitir a seleção de caminhos de idioma para criar em um novo site, as raízes de idioma correspondentes devem existir no blueprint (origem).
* Uma vez que um [novo site foi criado como uma Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (usando **Criar** e, em seguida, **Site**), os dois primeiros níveis desta Live Copy são *superficiais*. Os filhos da página não pertencem ao relacionamento dinâmico, mas uma implantação ainda descerá se um relacionamento dinâmico que corresponda ao acionador for encontrado.

É útil evitar:

* Adicionar idiomas manualmente no blueprint (abaixo do primeiro nível).
* Adicionar manualmente o conteúdo diretamente abaixo da raiz do idioma, pois isso não resulta no carregamento automático desse novo conteúdo para a Live Copy na implantação.

## MSM e sites multilíngues {#msm-and-multilingual-websites}

O MSM pode ajudar na criação de sites multilíngues de duas maneiras:

Ao criar matrizes de idioma, lembre-se do seguinte:

* Embora o MSM em si **não forneça a tradução de conteúdo**, ele pode ser integrado a conectores de tradução de terceiros que o fazem. Observe que:
   * O MSM permite cancelar a herança no nível da página e/ou do componente. Isso ajuda a impedir a substituição do conteúdo traduzido (de uma Live Copy, com conteúdo ainda não traduzido de um blueprint) na próxima implantação.
      * Alguns conectores de tradução de terceiros automatizam esse gerenciamento de heranças do MSM.
      * Consulte seu provedor de serviços de tradução para obter mais informações.
      * Uma abordagem alternativa para criar e traduzir matrizes de idioma é usar cópias de idioma juntamente com a estrutura de integração de tradução pronta para uso do AEM.

Para obter mais informações, consulte [Tradução de conteúdo para sites multilíngues](/help/sites-cloud/administering/translation/overview.md) e as [Práticas recomendadas de tradução.](/help/sites-cloud/administering/translation/best-practices.md)

## Alterações de estrutura e implantações {#structure-changes-and-rollouts}

As modificações na estrutura de conteúdo em um blueprint/árvore de origem são refletidas de forma diferente em uma Live Copy. Isso depende do tipo de modificação:

* **Criar** novas páginas em um blueprint resultará na criação de páginas correspondentes em Live Copies após a implantação com a configuração padrão de implantação.
* **Excluir** as páginas em um blueprint resultará na exclusão das páginas correspondentes das Live Copies após a implantação com a configuração padrão de implantação.
* **Movimentar** as páginas em um blueprint **não** resultará em páginas correspondentes sendo movidas em Live Copies após a implantação com a configuração padrão de implantação:
   * O motivo para esse comportamento é que uma movimentação de página inclui implicitamente uma exclusão de página. Isso pode levar a um comportamento inesperado na publicação, já que a exclusão de páginas na criação desativa automaticamente o conteúdo correspondente na publicação. Isso também pode ter um efeito adicional em itens relacionados, como links, marcadores e outros.
      * A herança de conteúdo nas respectivas páginas de Live Copy é atualizada para refletir o novo local de suas origens no blueprint.
      * Para concluir uma movimentação de página de um blueprint para Live Copies, considere ver as [práticas recomendadas de movimentação de página.](#page-move)

### Práticas recomendadas de movimentação de página {#page-move}

Ao considerar mover páginas em uma Live Copy, considere a seguinte prática recomendada.

>[!NOTE]
>
>O seguinte funcionará somente com o [Acionador de implantação](live-copy-sync-config.md#rollout-triggers).

1. Crie uma configuração de implantação personalizada.
   * Essa nova configuração deve incluir a ação `PageMoveAction`.
   * Não adicione outras ações a essa configuração.
1. Posicione a nova configuração.
   * Para implantar totalmente a movimentação de página, ao excluir as respectivas páginas em seu local antigo na Live Copy:
      * Posicione a configuração recém-criada antes da configuração de implantação padrão. A configuração de implantação padrão cuidará da exclusão das páginas em seus locais antigos.
      * Para implantar a movimentação da página, mantendo as respectivas páginas em seus locais antigos nas Live Copies (essencialmente duplicando o conteúdo):
         * Posicione a configuração recém-criada após a configuração padrão de implantação. Isso garantirá que nenhum conteúdo seja excluído na Live Copy ou desativado na publicação.

## Personalização de implantações {#customizing-rollouts}

As configurações de implantação do MSM são altamente personalizáveis. Você deve estar ciente de que a automatização de implantações pode ter consequências abrangentes. Como prática recomendada, você deve planejar com muito cuidado antes de realizar as seguintes atividades:

* A automatização de implantações, como com [Acionadores onModify](#onmodify)
* A personalização de [tipos/propriedades de nós](#node-types-properties)
* A inicialização de fluxos de trabalho subsequentes
* A ativação de conteúdo como parte das implantações

### onModify {#onmodify}

Ao usar o [acionador de implantação](live-copy-sync-config.md#rollout-triggers) `onModify`, você deve considerar que:

* A automatização de implantações com `onModify` acionadores pode ter um impacto negativo no desempenho da criação, pois ela aciona implantações após cada modificação de página.
* O resultado da implantação pode diferir do esperado, uma vez que:
   * Não é possível especificar a ordem dos eventos de modificação resultantes.
   * A arquitetura baseada em eventos não pode garantir a sequência dos eventos transmitidos para o Gerenciador de implantação.
* O uso dessa configuração de implantação pode gerar conflitos se ocorrerem atualizações simultâneas do mesmo recurso.

Portanto, recomenda-se apenas utilizar `onModify` acionadores se os benefícios da iniciação automática de implantação forem maiores do que quaisquer possíveis problemas de desempenho.

### Tipos/propriedades de nós {#node-types-properties}

Além de personalizar as ações de implantação, o MSM também permite personalizar as propriedades do nó que estão sendo implantadas. A [configuração OSGi do MGM permite excluir tipos de nó](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) de serem copiados da origem para a Live Copy.

## Informações adicionais {#further-information}

Consulte os seguintes artigos para obter mais detalhes sobre MSM e Live Copies.

* [Criação e sincronização de Live Copies](creating-live-copies.md)
* [Visão geral do console da Live Copy](live-copy-overview.md)
* [Configurar a sincronização da Live Copy](live-copy-sync-config.md)
* [Conflitos de implantação do MSM](rollout-conflicts.md)
