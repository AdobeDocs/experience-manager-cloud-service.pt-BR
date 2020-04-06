---
title: Visão geral do sistema AEM
description: Visão geral do sistema AEM
translation-type: tm+mt
source-git-commit: aa6bb878ea4c58ba1e2fbf82d53effaa1a72d668

---


# Visão geral do sistema AEM {#aem-system}

Esta página descreve o AEM como um serviço em nuvem que fornece um novo recurso com uma arquitetura que é um aprimoramento significativo em relação às versões anteriores do AEM. A atualização para essa nova arquitetura requer um esforço significativo.

## Descrição {#background}

O meta-padrão ACRA é usado para identificar vários problemas relacionados às atualizações do AEM como um serviço em nuvem. Suporta vários tipos de informações de aviso por meio de uma combinação dos valores de *referência* e &quot;referenciadoBy&quot; do padrão e seu objeto de *contexto* . O valor do *tipo* no objeto de *contexto* determina o problema específico que foi detectado.

Espera - se que as questões de prontidão incluídas no padrão ACRA tenham relativamente poucas instâncias que causem o aconselhamento. Há outros problemas de prontidão relacionados ao AEM como um serviço de nuvem que podem ter muitas instâncias que precisam de atenção e que recebem seu próprio código de padrão. (Consulte Interface do usuário e URS.)

## Dados de padrão {#pattern-data}

Os seguintes objetos estão incluídos na representação JSON do padrão:

* **item.message**: O tipo de problema de prontidão. (Consulte abaixo.)
* **dados**: Um objeto JSON que contém os dados correspondentes ao tipo.

### Possíveis implicações e riscos {#possible-implications}

A ser decidido

### Soluções possíveis {#possible-solutions}

A ser decidido
