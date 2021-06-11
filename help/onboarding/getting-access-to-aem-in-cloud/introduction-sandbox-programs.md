---
title: 'Introdução aos programas de sandbox '
description: Introdução aos programas de sandbox
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 1ecadc0d2b45ee8c94af8d91b35dbd40b08e89b5
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Introdução aos programas de sandbox {#sandbox-programs}

## Introdução {#introduction}

Um programa de sandbox é um dos dois tipos de programas disponíveis no AEM Cloud Service, sendo o outro um programa de produção.

Um Sandbox é normalmente criado para servir aos propósitos de treinamento, execução de demonstrações, ativação ou Prova de Conceito (POCs). Não se destinam a transportar tráfego vivo. Eles não estão sujeitos ao AEM [como um Cloud Service Commitments](https://www.adobe.com/legal/service-commitments.html).

Os ambientes criados em um Sandbox não são configurados para dimensionamento automático. Portanto, esses ambientes não são adequados para teste de desempenho ou carga.

Os programas de sandbox incluem [!DNL Sites] e [!DNL Assets] e são preenchidos automaticamente com um repositório Git, um ambiente de desenvolvimento e um pipeline não relacionado à produção.  O repositório Git é preenchido com um projeto de amostra com base no arquétipo de projeto AEM.

Consulte [Noções básicas sobre programas e tipos de programas](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) para saber mais sobre os tipos de programas.

### Atributos dos programas de sandbox {#attributes-sandbox}

Os Programas do Sandbox têm os seguintes atributos:

1. **Criação de programas:** A criação do programa Sandbox inclui automaticamente:
   * configuração de projeto com código de amostra e conteúdo
   * criação de um ambiente de desenvolvimento
   * criação de pipeline de não produção implantando no ambiente de desenvolvimento (implantação de ramificação principal no ambiente de desenvolvimento)

1. **Soluções:** os programas de sandbox incluem AEM  [!DNL Sites] e  [!DNL Assets].

1. **AEM atualizações:** AEM atualizações podem ser aplicadas manualmente aos ambientes em um programa de sandbox e não são automaticamente enviadas.
Consulte [AEM Atualizações para ambientes de sandbox](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox) para obter mais detalhes.

1. **Hibernação:** os ambientes em um programa de sandbox hibernam automaticamente se nenhuma atividade for detectada por um determinado período. As sandboxes são colocadas no nó de hibernação após 8 horas de inatividade, após o que podem ser removidas da hibernação. Ambientes hibernados podem ser removidos manualmente da hibernação.
Consulte [Hibernando e removendo ambientes de sandbox](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md) para obter mais detalhes.

1. **Exclusão**: As sandboxes são excluídas depois de seis meses em modo de hibernação contínua, depois disso, podem ser recriadas.
