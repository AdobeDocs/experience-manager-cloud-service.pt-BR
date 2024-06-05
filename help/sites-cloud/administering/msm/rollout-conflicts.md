---
title: Conflitos de implantação
description: Saiba como gerenciar e resolver conflitos de implementação do Multi Site Manager.
feature: Multi Site Manager
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 63%

---

# Conflitos de implantação {#msm-rollout-conflicts}

Conflitos podem ocorrer se novas páginas com o mesmo nome de página forem criadas na ramificação do blueprint e em uma ramificação dependente da Live Copy. Esses conflitos devem ser tratados e resolvidos na implantação.

## Tratamento de conflitos {#conflict-handling}

Quando páginas conflitantes existem (nas ramificações do blueprint e da Live Copy), o MSM permite definir como (ou mesmo se) elas devem ser tratadas.

Para garantir que a implantação não seja bloqueada, as possíveis definições podem incluir:

* Qual página (blueprint ou Live Copy) tem prioridade durante a implantação
* Quais páginas são renomeadas e como
* Como isso afeta qualquer conteúdo publicado

O comportamento padrão do Adobe Experience Manager (AEM) pronto para uso é que o conteúdo publicado não é afetado. Portanto, se uma página que foi criada manualmente na ramificação da Live Copy tiver sido publicada, esse conteúdo ainda será publicado após o tratamento do conflito e a implantação.

Além da funcionalidade padrão, os manipuladores de conflito personalizados podem ser adicionados para implementar regras diferentes. Eles também podem permitir a publicação de ações como um processo individual.

### Exemplo de cenário {#example-scenario}

Nas seções a seguir, há um exemplo de uma nova página `b` é usada, criada no blueprint e na ramificação da Live Copy (criada manualmente), para ilustrar os vários métodos de resolução de conflitos:

* blueprint: `/b`

  Uma página principal com uma página secundária, `bp-level-1`

* Live Copy: `/b`

  Uma página criada manualmente na ramificação da Live Copy com uma página secundária, `lc-level-1`

   * Ativado ao publicar como `/b`, junto com a página secundária

#### Antes da implantação {#before-rollout}

|  | Blueprint antes da implantação | Live Copy antes da implantação | Publicar antes da implantação |
|---|---|---|---|
| Valor | `b` | `b` | `b` |
| Comentar | Criado na ramificação do blueprint, pronto para implantação | Criado manualmente na ramificação da Live Copy | Contém o conteúdo da página `b` que foi criada manualmente na ramificação da Live Copy |
| Valor | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentar |  | Criado manualmente na ramificação da Live Copy | Contém o conteúdo da página `child-level-1` que foi criada manualmente na ramificação da Live Copy |

## Gerenciador de implantação e tratamento de conflito {#rollout-manager-and-conflict-handling}

O gerenciador de implantação permite ativar ou desativar o gerenciamento de conflitos.

Isso é feito usando a [configuração do OSGi](/help/implementing/deploying/configuring-osgi.md) do **Gerenciador de implantaçao Day CQ WCM**. Defina o valor **Manipular conflito com páginas criadas manualmente** ( `rolloutmgr.conflicthandling.enabled`) como verdadeiro se o gerenciador de implantação deve lidar com conflitos de uma página criada na Live Copy com um nome que existe no blueprint.

O AEM tem [comportamentos predefinidos quando o gerenciamento de conflitos foi desativado.](#behavior-when-conflict-handling-deactivated)

## Manipuladores de conflito {#conflict-handlers}

O AEM usa manipuladores de conflitos para resolver quaisquer conflitos de página que existam ao implantar conteúdo de um blueprint em uma Live Copy. A renomeação de páginas é o método usual (não único) para resolver esses conflitos. Mais de um manipulador de conflitos pode estar operacional para permitir uma seleção de comportamentos diferentes.

O AEM fornece:

* O [manipulador de conflitos padrão](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* A possibilidade de implementar um [manipulador personalizado](#customized-handlers)
* O mecanismo de classificação de serviço que permite definir a prioridade de cada manipulador individual
   * O serviço com a classificação mais alta é usado.

### Manipulador de conflito padrão {#default-conflict-handler}

O manipulador de conflito padrão é o `ResourceNameRolloutConflictHandler`

* Com esse manipulador, a página do blueprint recebe prioridade.
* A classificação de serviço para este manipulador está baixa. Ou seja, abaixo do valor padrão para o `service.ranking` propriedade porque se presume que os manipuladores personalizados precisam de uma classificação mais alta. No entanto, a classificação não é o mínimo absoluto para garantir flexibilidade quando necessária.

Esse manipulador de conflitos dá prioridade ao blueprint. Por exemplo, a página Live Copy `/b` é movido dentro da ramificação da Live Copy para `/b_msm_moved`.

* Live Copy: `/b`

  É movido dentro da Live Copy para `/b_msm_moved`. Isso funciona como um backup e garante que nenhum conteúdo seja perdido.

   * `lc-level-1` não é movido.

* Blueprint: `/b`

  É implantado na página da Live Copy `/b`.

   * `bp-level-1` é implantado na Live Copy.

#### Após a implantação {#after-rollout}

|  | Blueprint após implantação | Live Copy após implantação | Live Copy após implantação | Publicar após a implantação |
|---|---|---|---|---|
| Valor | `b` | `b` | `b_msm_moved` | `b` |
| Comentar |  | Tem o conteúdo da página do blueprint `b` que foi implantado | Tem o conteúdo da página `b` que foi criado manualmente na ramificação da Live Copy | Sem alterações; contém o conteúdo da página original `b` que foi criado manualmente na ramificação da Live Copy e agora é chamado de `b_msm_moved` |
| Valor | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentar |  |  | Sem alterações | Sem alterações |

### Manipuladores personalizados {#customized-handlers}

Os manipuladores de conflito personalizados permitem que você implemente suas próprias regras. Usando o mecanismo de classificação de serviço, você também pode definir como eles interagem com outros manipuladores.

Os manipuladores de conflito personalizados podem:

* Ser nomeados de acordo com suas necessidades.
* Ser desenvolvidos/configurados de acordo com suas necessidades.
   * Por exemplo, é possível desenvolver um manipulador para que a página da Live Copy tenha prioridade.
* Ela pode ser configurada usando o [Configuração OSGi](/help/implementing/deploying/configuring-osgi.md). Em especial:
   * A **Classificação do serviço** define a ordem relacionada a outros manipuladores de conflito ( `service.ranking`).
      * O valor padrão é `0`.

### Comportamento quando o manuseio de conflitos é desativado {#behavior-when-conflict-handling-deactivated}

Se você [desativar o manuseio de conflitos manualmente,](#rollout-manager-and-conflict-handling) o AEM não executa nenhuma ação em páginas em conflito. As páginas não conflitantes são implantadas conforme esperado.

>[!CAUTION]
>
>Quando o manuseio de conflitos é desativado, o AEM não dá qualquer indicação de que os conflitos estão sendo ignorados. Como nesses casos, esse comportamento deve ser configurado explicitamente, assume-se que é o comportamento desejado.

Nesse caso, a Live Copy tem prioridade efetiva. A página do blueprint `/b` não é copiada e a página da Live Copy `/b` é deixada intocada.

* Blueprint: `/b`

  Ela não é copiada, mas é ignorada.

* Live Copy: `/b`

  Fica igual.

#### Após a implantação {#after-rollout-no-conflict}

|  | Blueprint após implantação | Live Copy após implantação | Publicar após a implantação |
|---|---|---|---|
| Valor | `b` | `b` | `b` |
| Comentar |  | Sem alterações; tem o conteúdo da página `b` que foi criado manualmente na ramificação da Live Copy | Sem alterações; contém o conteúdo da página `b` que foi criado manualmente na ramificação da Live Copy |
| Valor | `/bp-level-1,` | `/lc-level-1` | `/lc-level-1` |
| Comentar |  | Sem alterações | Sem alterações |

### Classificações de serviço {#service-rankings}

A classificação de serviço do [OSGi](https://www.osgi.org/) pode ser usada para definir a prioridade de manipuladores de conflito individuais.
