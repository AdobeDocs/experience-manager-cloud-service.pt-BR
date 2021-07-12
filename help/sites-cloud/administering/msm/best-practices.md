---
title: Práticas recomendadas do MSM
description: Conheça as práticas recomendadas compiladas pelas equipes de engenharia e consultoria de Adobe para ajudar a ativar e executar o AEM Multi Site Manager.
feature: Gerenciamento de vários sites
role: Admin
exl-id: 61b8ded8-3b9e-423f-85a9-7280e1a721cc
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 0%

---

# Práticas recomendadas do MSM {#msm-best-practices}

## Geral {#general}

O MSM é uma estrutura configurável para automatizar a implantação de conteúdo. As implementações geralmente envolvem partes importantes de um site, organizações de extensão e regiões geográficas. Portanto, é altamente recomendável planejar as implementações do MSM com o cuidado necessário ao planejar seu site:

* Cuidadosamente **planeje a estrutura e os fluxos de conteúdo** antes de iniciar a implementação.
* **Personalize o quanto for necessário, mas o mínimo possível.** Embora o MSM suporte um alto grau de personalização (por exemplo, configurações de implementação), a prática recomendada para o desempenho, confiabilidade e atualização de seu site é minimizar a personalização.
* Estabeleça um modelo de **governança** antecipadamente e treine os usuários de acordo, para garantir o sucesso. Uma prática recomendada do ponto de vista de governança é **minimizar a autoridade que os produtores de conteúdo local têm** para alocar/conectar conteúdo a outros usuários locais e suas respectivas Live Copies. Isso ocorre porque heranças encadeadas e não governadas podem aumentar significativamente a complexidade de uma estrutura MSM e comprometer seu desempenho e confiabilidade.
* Quando existir um plano para sua estrutura, fluxos de conteúdo, automação e governança, **protótipo e teste completamente seu sistema** antes de iniciar uma implementação ativa.
* Lembre-se de que **Adobe Consulting e os principais integradores de sistema** têm um planejamento de experiência profundo e implementam a automação de conteúdo com o MSM, para que eles possam ajudá-lo a começar a usar o projeto MSM e em toda a implementação.

## Fontes de Live Copy e configurações do Blueprint {#live-copy-sources-and-blueprint-configurations}

Lembre-se de que uma Live Copy pode ser criada usando [páginas regulares](creating-live-copies.md#creating-a-live-copy-of-a-page) ou [configuração do blueprint](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Ambos são casos de uso válidos.

Os benefícios adicionais do uso de uma configuração do blueprint são:

* Permita que o autor use a opção **Rollout** em um blueprint para enviar explicitamente modificações às Live Copies que herdam deste blueprint.
* Permitir que o autor use **Criar Site** para selecionar idiomas facilmente e configurar a estrutura da Live Copy.
* Defina uma configuração de implementação padrão para Live Copies que tenham uma relação com o blueprint.

No caso de uma configuração do blueprint não ser mencionada, as implantações só podem ser iniciadas a partir das próprias Live Copies, obtendo essencialmente conteúdo da origem.

Ao criar um novo site com o Live Copy, é vantajoso criar configurações de blueprint para garantir a disponibilidade do conjunto completo de recursos do MSM.

>[!NOTE]
>
> Observe que os CUGs na guia Permissões não podem ser implantados em Live Copies de Blueprints. Planeje isso ao configurar a Live Copy.

## Sincronização de componentes e contêineres {#components-and-container-synchronization}

Em geral, a regra de implantação no MSM em relação à sincronização de componentes é:

* Os componentes são implementados sincronizando os recursos contidos no blueprint.
* Os contêineres sincronizam somente o recurso atual.

Isso significa que os componentes são tratados como um agregado e, em uma implementação, o próprio componente e todos os seus filhos são substituídos por aqueles nos blueprints. Isso significa que, se um recurso for adicionado localmente a esse componente, ele será perdido no conteúdo do blueprint na implantação.

Para suportar o aninhamento de componentes de modo que os componentes adicionados localmente sejam mantidos em uma implantação, o componente deve ser declarado como um contêiner.

>[!NOTE]
>
>Adicione a propriedade `cq:isContainer` ao componente para designá-la como um container.

## Criar site {#create-site}

Observe que AEM tem duas abordagens principais para a criação de Live Copies:

* Ao [criar uma Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page) - Isso pode ser considerado a abordagem mais genérica, permitindo que você crie Live Copies de qualquer página. A estrutura de conteúdo de uma Live Copy corresponde exatamente à fonte.

* Ao [criar um Site](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) - Essa é uma abordagem mais especializada, principalmente para criar sites com uma estrutura multilíngue.

Estas são algumas considerações que devem ser levadas em conta ao criar um site:

* Para criar um novo site, você precisa de uma [configuração do blueprint](creating-live-copies.md#managing-blueprint-configurations).
* Para permitir a seleção de caminhos de idioma para criar em um novo site, as raízes de idioma correspondentes devem existir no blueprint (fonte).
* Depois que um [novo site tiver sido criado como uma Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (usando **Criar**, em seguida **Site**), os dois primeiros níveis desta Live Copy serão *Shallow*. Os filhos da página não pertencem ao relacionamento ao vivo, mas uma implantação ainda descerá se um relacionamento ao vivo que corresponda ao acionador for encontrado.

É útil evitar:

* Adicionar idiomas manualmente no blueprint (abaixo do primeiro nível).
* Adicionar manualmente o conteúdo diretamente abaixo da raiz do idioma, pois isso não resulta no carregamento automático desse novo conteúdo para a Live Copy na implantação.

## MSM e sites multilíngues {#msm-and-multilingual-websites}

O MSM pode ajudar na criação de sites multilíngues de duas maneiras:

Ao criar mestres em linguagem, lembre-se do seguinte:

* Embora o próprio MSM **não forneça tradução de conteúdo**, ele pode ser integrado a conectores de tradução de terceiros que fornecem. Observe que:
   * O MSM permite cancelar a herança no nível da página e/ou do componente. Isso ajuda a impedir a substituição do conteúdo traduzido (de uma Live Copy, com conteúdo ainda não traduzido de um blueprint) na próxima implantação.
      * Alguns conectores de tradução de terceiros automatizam esse gerenciamento de heranças do MSM.
      * Consulte seu provedor de serviços de tradução para obter mais informações.
      * Uma abordagem alternativa para criar e traduzir mestres de linguagem é usar cópias de idioma juntamente com AEM estrutura de integração de tradução pronta para uso.

Para obter mais informações, consulte [Tradução de conteúdo para sites multilíngues](/help/sites-cloud/administering/translation/overview.md) e [Práticas recomendadas de tradução.](/help/sites-cloud/administering/translation/best-practices.md)

## Alterações na estrutura e implantações {#structure-changes-and-rollouts}

As modificações na estrutura de conteúdo em um blueprint/árvore de origem são refletidas de forma diferente em uma Live Copy. Depende do tipo de modificação:

* **** A criação de novas páginas em um blueprint resultará na criação de páginas correspondentes em Live Copies após a implantação com a configuração padrão de implementação.
* **** A exclusão de páginas em um blueprint resultará na exclusão de páginas correspondentes de Live Copies após a implantação com a configuração padrão de implementação.
* **** Mover páginas em um blueprint  **** não resultará na movimentação das páginas correspondentes em Live Copies após a implantação com a configuração padrão de implementação:
   * O motivo para esse comportamento é que uma movimentação de página inclui implicitamente uma exclusão de página. Isso pode levar a um comportamento inesperado na publicação, já que a exclusão de páginas no autor desativa automaticamente o conteúdo correspondente na publicação. Isso também pode ter um efeito adicional em itens relacionados, como links, marcadores e outros.
      * A herança de conteúdo nas respectivas páginas de Live Copy é atualizada para refletir o novo local de suas fontes no blueprint.
      * Para realizar totalmente uma movimentação de página de um blueprint para Live Copies, considere as [práticas recomendadas de movimentação de página.](#page-move)

### Práticas recomendadas de movimentação de página {#page-move}

Ao considerar mover páginas em uma Live Copy, considere a seguinte prática recomendada.

>[!NOTE]
>
>O seguinte funcionará somente com o acionador [Na implantação](live-copy-sync-config.md#rollout-triggers).

1. Crie uma configuração de implementação personalizada.
   * Essa nova configuração deve incluir a ação `PageMoveAction`.
   * Não adicione outras ações a essa configuração.
1. Posicione a nova configuração.
   * Para implantar totalmente a movimentação da página, ao excluir as respectivas páginas em seu local antigo na Live Copy:
      * Posicione a configuração recém-criada antes da configuração de implementação padrão. A configuração de implementação padrão cuidará da exclusão das páginas em seus locais antigos.
      * Para implantar a movimentação da página, mantendo as respectivas páginas em seus locais antigos nas Live Copies (essencialmente duplicando o conteúdo):
         * Posicione a configuração recém-criada após a configuração padrão de implementação. Isso garantirá que nenhum conteúdo seja excluído na Live Copy ou desativado da publicação.

## Personalização de implantações {#customizing-rollouts}

As configurações de implementação do MSM são altamente personalizáveis. Você deve estar ciente de que a automatização de implantações pode ter consequências de longo alcance. Como prática recomendada, você deve planejar com muito cuidado antes de realizar as seguintes atividades:

* Automatizar implantações como com [onModify acionadores](#onmodify)
* Personalizando [tipos de nó/propriedades](#node-types-properties)
* Iniciando workflows subsequentes
* Ativação de conteúdo como parte das implantações

### onModify {#onmodify}

Ao usar o [acionador de implementação](live-copy-sync-config.md#rollout-triggers) `onModify`, considere que:

* A automatização de implantações com `onModify` acionadores pode ter um impacto negativo no desempenho da criação à medida que acionam implantações após cada modificação de página.
* O resultado da implantação pode diferir do esperado como:
   * Não é possível especificar a ordem dos eventos de modificação resultantes.
   * A arquitetura baseada em eventos não pode garantir a sequência dos eventos transmitidos para o Gerenciador de implementação.
* O uso dessa configuração de implementação pode gerar conflitos se ocorrerem atualizações simultâneas do mesmo recurso.

Portanto, é recomendável usar somente `onModify` acionadores se os benefícios da iniciação de implementação automática compensarem quaisquer possíveis problemas de desempenho.

### Tipos/propriedades de nós {#node-types-properties}

Além de personalizar as ações de implantação, o MSM também permite personalizar as propriedades do nó que estão sendo implantadas. A configuração [MSM OSGi permite excluir os tipos de nó](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) de serem copiados da origem para a Live Copy.

## Informações adicionais {#further-information}

Consulte os seguintes artigos para obter mais detalhes sobre o MSM e Live Copy.

* [Criação e sincronização de cópias em tempo real](creating-live-copies.md)
* [Console de Visão Geral da Live Copy](live-copy-overview.md)
* [Configurar a sincronização da Live Copy](live-copy-sync-config.md)
* [Conflitos de implementação do MSM](rollout-conflicts.md)
