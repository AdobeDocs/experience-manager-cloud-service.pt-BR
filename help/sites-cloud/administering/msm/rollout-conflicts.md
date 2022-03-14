---
title: Conflitos de implantação
description: Saiba como gerenciar e resolver conflitos de implementação do Multi Site Manager.
feature: Multi Site Manager
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 3%

---

# Conflitos de implantação {#msm-rollout-conflicts}

Conflitos podem ocorrer se novas páginas com o mesmo nome de página forem criadas na ramificação do blueprint e em uma ramificação dependente da Live Copy. Tais conflitos devem ser tratados e resolvidos aquando da sua implantação.

## Tratamento de conflitos {#conflict-handling}

Quando páginas conflitantes existem (nas ramificações do blueprint e Live Copy), o MSM permite definir como (ou mesmo se) elas devem ser tratadas.

Para garantir que a implantação não seja bloqueada, as possíveis definições podem incluir:

* Qual página (blueprint ou Live Copy) terá prioridade durante a implantação
* Quais páginas serão renomeadas (e como)
* Como isso afetará qualquer conteúdo publicado

O comportamento padrão AEM pronto para uso é que o conteúdo publicado não será afetado. Portanto, se uma página que foi criada manualmente na ramificação da Live Copy tiver sido publicada, esse conteúdo ainda será publicado após a manipulação e implantação do conflito.

Além da funcionalidade padrão, os manipuladores de conflito personalizados podem ser adicionados para implementar regras diferentes. Isso também pode permitir a publicação de ações como um processo individual.

### Exemplo de cenário {#example-scenario}

Nas seções a seguir, usamos o exemplo de uma nova página `b`, criado no blueprint e na ramificação Live Copy (criado manualmente), para ilustrar os vários métodos de resolução de conflitos:

* blueprint: `/b`

   Uma página principal com 1 página secundária, `bp-level-1`

* Live Copy: `/b`

   Uma página criada manualmente na ramificação Live Copy com 1 página secundária, `lc-level-1`

   * Ativado ao publicar como `/b`, junto com a página filho

#### Antes da implantação {#before-rollout}

|  | Blueprint antes da implantação | Live Copy antes da implantação | Publicar antes da implantação |
|---|---|---|---|
| Valor | `b` | `b` | `b` |
| Comentário | Criado na ramificação do blueprint, pronto para implantação | Criado manualmente na ramificação Live Copy | Contém o conteúdo da página `b` que foi criado manualmente na ramificação Live Copy |
| Valor | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentário |  | Criado manualmente na ramificação Live Copy | contém o conteúdo da página `child-level-1` que foi criado manualmente na ramificação Live Copy |

## Gerenciador de implementação e tratamento de conflito {#rollout-manager-and-conflict-handling}

O gerenciador de implementação permite ativar ou desativar o gerenciamento de conflitos.

Isso é feito usando [Configuração do OSGi](/help/implementing/deploying/configuring-osgi.md) de **Gerenciador de implementação do WCM CQ do dia**. Defina o valor **Lidar com conflito com páginas criadas manualmente** ( `rolloutmgr.conflicthandling.enabled`) como verdadeiro se o gerenciador de implementação deve lidar com conflitos de uma página criada na Live Copy com um nome que existe no blueprint.

AEM [comportamento predefinido quando o gerenciamento de conflitos foi desativado.](#behavior-when-conflict-handling-deactivated)

## Manipuladores de conflito {#conflict-handlers}

O AEM usa manipuladores de conflitos para resolver quaisquer conflitos de página que existam ao implantar conteúdo de um blueprint em uma Live Copy. A renomeação de páginas é o método usual (não apenas) para resolver esses conflitos. Mais de um manipulador de conflitos pode ser operacional para permitir uma seleção de comportamentos diferentes.

AEM fornece:

* O [manipulador de conflitos padrão](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* A possibilidade de aplicar uma [manipulador personalizado](#customized-handlers)
* O mecanismo de classificação de serviço que permite definir a prioridade de cada manipulador individual
   * O serviço com a classificação mais alta é usado.

### Manipulador de conflito padrão {#default-conflict-handler}

O manipulador de conflitos padrão é `ResourceNameRolloutConflictHandler`

* Com esse manipulador, a página do blueprint recebe prioridade.
* A classificação de serviço para esse manipulador é definida como baixa, ou seja, abaixo do valor padrão para a variável `service.ranking` , como se supõe que os manipuladores personalizados precisarão de uma classificação mais alta. No entanto, a classificação não é o mínimo absoluto para garantir a flexibilidade quando necessário.

Esse manipulador de conflitos dá prioridade ao blueprint. Por exemplo, a página Live Copy `/b` é movido dentro da ramificação Live Copy para `/b_msm_moved`.

* Live Copy: `/b`

   É movido dentro da Live Copy para `/b_msm_moved`. Isso funciona como um backup e garante que nenhum conteúdo seja perdido.

   * `lc-level-1` não é movido.

* Blueprint: `/b`

   É implantado na página Live Copy `/b`.

   * `bp-level-1` é implantado na Live Copy.

#### Após a implantação {#after-rollout}

|  | Blueprint após implantação | Live Copy após implantação | Live Copy após implantação | Publicar após a implantação |
|---|---|---|---|---|
| Valor | `b` | `b` | `b_msm_moved` | `b` |
| Comentário |  | Tem o conteúdo da página do blueprint `b` que foi lançado | Possui o conteúdo da página `b` que foi criado manualmente na ramificação Live Copy | Sem alterações, contém o conteúdo da página original `b` que foi criado manualmente na ramificação Live Copy e agora é chamado de `b_msm_moved` |
| Valor | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentário |  |  | Sem alteração | Sem alteração |

### Manipuladores personalizados {#customized-handlers}

Os manipuladores de conflito personalizados permitem que você implemente suas próprias regras. Usando o mecanismo de classificação de serviço, você também pode definir como eles interagem com outros manipuladores.

Os manipuladores de conflitos personalizados podem:

* Seja nomeado de acordo com suas necessidades.
* Ser desenvolvido/configurado de acordo com suas necessidades.
   * Por exemplo, você pode desenvolver um manipulador para que a página de Live Copy tenha prioridade.
* Pode ser projetado para ser configurado usando o [Configuração do OSGi](/help/implementing/deploying/configuring-osgi.md). Em especial:
   * **Classificação do serviço** define a ordem relacionada a outros manipuladores de conflito ( `service.ranking`).
      * O valor padrão é `0`.

### Comportamento quando a manipulação de conflitos é desativada {#behavior-when-conflict-handling-deactivated}

Se você manualmente [desativar tratamento de conflitos,](#rollout-manager-and-conflict-handling) AEM não executa nenhuma ação em páginas em conflito. As páginas não conflitantes são implantadas conforme esperado.

>[!CAUTION]
>
>Quando a manipulação de conflitos é desativada, AEM não dá qualquer indicação de que os conflitos estão sendo ignorados. Como nesses casos, esse comportamento deve ser configurado explicitamente, assume-se que é o comportamento desejado.

Nesse caso, a Live Copy tem prioridade. A página do blueprint `/b` não é copiada e a página Live Copy `/b` é deixado intocado.

* Blueprint: `/b`

   Não é copiado, mas é ignorado.

* Live Copy: `/b`

   Fica igual.

#### Após a implantação {#after-rollout-no-conflict}

|  | Blueprint após implantação | Live Copy após implantação | Publicar após a implantação |
|---|---|---|---|
| Valor | `b` | `b` | `b` |
| Comentário |  | Sem alterações, tem o conteúdo da página `b` que foi criado manualmente na ramificação Live Copy | Sem alterações, contém o conteúdo da página `b` que foi criado manualmente na ramificação Live Copy |
| Valor | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentário |  | Sem alteração | Sem alteração |

### Classificações de serviço {#service-rankings}

O [OSGi](https://www.osgi.org/) a classificação de serviço pode ser usada para definir a prioridade de manipuladores de conflito individuais.
