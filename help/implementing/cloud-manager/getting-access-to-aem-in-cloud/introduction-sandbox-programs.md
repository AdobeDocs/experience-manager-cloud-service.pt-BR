---
title: 'Introdução aos programas de sandbox '
description: Introdução aos programas de sandbox
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 1892900ea3f365e1b5f7d31ffae64d45256d2a3a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Introdução aos programas de sandbox {#sandbox-programs}

## Introdução {#introduction}

Um programa de sandbox é um dos dois tipos de programas disponíveis no AEM Cloud Service, sendo o outro um programa de produção.

Um Sandbox é normalmente criado para servir aos propósitos de treinamento, execução de demonstrações, ativação ou Prova de Conceito (POCs). Não se destinam a transportar tráfego vivo. Eles não estão sujeitos à [AEM compromissos as a Cloud Service](https://www.adobe.com/legal/service-commitments.html).

Os ambientes criados em um Sandbox não são configurados para dimensionamento automático. Portanto, esses ambientes não são adequados para teste de desempenho ou carga.

Os programas de sandbox incluem [!DNL Sites] e [!DNL Assets] e são preenchidas automaticamente com um repositório Git, um ambiente de desenvolvimento e um pipeline de não produção.  O repositório Git é preenchido com um projeto de amostra com base no arquétipo de projeto AEM.

>[!IMPORTANT]
>Um programa de sandbox terá apenas um ambiente de desenvolvimento.

>[!NOTE]
>Domínios personalizados e Listas de permissões IP não estão disponíveis em programas sandbox.

Consulte [Noções básicas sobre programas e tipos de programas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html?lang=en) para saber mais sobre os Tipos de programa.

### Atributos dos programas de sandbox {#attributes-sandbox}

Os Programas do Sandbox têm os seguintes atributos:

1. **Criação do programa:** A criação do programa Sandbox inclui automaticamente:
   * configuração de projeto com código de amostra e conteúdo
   * criação de um ambiente de desenvolvimento
   * criação de pipeline de não produção implantando no ambiente de desenvolvimento (implantação de ramificação principal no ambiente de desenvolvimento)

1. **Soluções:** Os programas de sandbox incluem AEM [!DNL Sites] e [!DNL Assets].

1. **Atualizações de AEM:** AEM atualizações podem ser aplicadas manualmente a ambientes em um programa de sandbox e não são automaticamente enviadas.
Consulte [AEM atualizações para ambientes de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox) para obter mais detalhes.

1. **Hibernação:** Os ambientes em um programa de sandbox hibernam automaticamente se nenhuma atividade for detectada por um determinado período. As sandboxes são colocadas no nó de hibernação após 8 horas de inatividade, após o que podem ser removidas da hibernação. Ambientes hibernados podem ser removidos manualmente da hibernação.
Consulte [Hibernar e desibernar ambientes de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md) para obter mais detalhes.

1. **Exclusão**: As sandboxes são excluídas depois de seis meses em modo de hibernação contínua, depois disso, podem ser recriadas.
