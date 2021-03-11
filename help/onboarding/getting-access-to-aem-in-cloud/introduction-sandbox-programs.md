---
title: 'Introdução aos programas de sandbox '
description: 'Introdução aos programas de sandbox '
translation-type: tm+mt
source-git-commit: d98e3ba930690627bfbe9b90ce5cb93328c30503
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Introdução aos programas de sandbox {#sandbox-programs}

## Introdução {#introduction}

Um programa de sandbox é um dos dois tipos de programas disponíveis no AEM Cloud Service, sendo o outro um programa de produção.

Um Sandbox é normalmente criado para servir aos propósitos de treinamento, execução de demonstrações, ativação ou Prova de Conceito (POCs). Não se destinam a transportar tráfego vivo. Eles não estão sujeitos ao AEM [como um Cloud Service Commitments](https://www.adobe.com/legal/service-commitments.html).

Os ambientes criados em um Sandbox não são configurados para dimensionamento automático. Portanto, esses ambientes não são adequados para teste de desempenho ou carga.

Os programas de sandbox incluem Sites e Ativos e são preenchidos automaticamente com um repositório Git, um ambiente de desenvolvimento e um pipeline não relacionado à produção.  O repositório Git é preenchido com um projeto de amostra com base no arquétipo de projeto AEM.

Consulte [Noções básicas sobre programas e tipos de programas](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) para saber mais sobre os tipos de programas.

### Atributos dos programas de sandbox {#attributes-sandbox}

Os Programas do Sandbox têm os seguintes atributos:

1. **Criação de programas:** A criação do programa Sandbox inclui automaticamente:
   * configuração de projeto com código de amostra e conteúdo
   * criação de um ambiente de desenvolvimento
   * criação de pipeline de não produção implantando no ambiente de desenvolvimento (implantação de ramificação principal no ambiente de desenvolvimento)

1. **Soluções:** os programas de sandbox incluem AEM Sites e Assets.

1. **AEM atualizações:** AEM atualizações podem ser aplicadas manualmente aos ambientes em um programa de sandbox e não são automaticamente enviadas.
Consulte [AEM Atualizações para ambientes de sandbox](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox) para obter mais detalhes.

1. **Hibernação:** os ambientes em um programa de sandbox hibernam automaticamente se nenhuma atividade for detectada por um determinado período. Ambientes hibernados podem ser removidos manualmente da hibernação.
Consulte [Hibernando e removendo ambientes de sandbox](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md) para obter mais detalhes.