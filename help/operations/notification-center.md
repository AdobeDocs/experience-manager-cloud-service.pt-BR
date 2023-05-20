---
title: Centro de notificação
description: Utilize o centro de notificações para tomar ações apropriadas em caso de incidentes e para obter outras informações importantes
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: 3aa753fb5cc5130ced7e9baafde63e8825394dce
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 35%

---

# Centro de notificação {#notification-center}

>[!NOTE]
>Este recurso não foi lançado.

O AEM as Cloud Service envia notificações quando ocorrem incidentes críticos que exigem ação imediata, bem como recomendações proativas para otimizações. Os exemplos incluem uma fila bloqueada ou um conjunto expirando de credenciais; o conjunto completo de tipos de notificação pode ser exibido no [tabela abaixo](#supported-notification-types), que se expandirá com o tempo.

Essas notificações podem ser configuradas para serem recebidas por email e no widget de notificação, que é acessado clicando no ícone de sino no canto superior direito em toda a Adobe Experience Cloud.

Quando uma notificação é recebida, é possível clicar nela para abrir a Central de notificações do AEM as a Cloud Service com um pop-up que exibe um contexto adicional explicando a ação que um cliente deve tomar.

Além de exibir informações sobre a notificação recém-clicada, o Centro de notificações serve como um hub onde você pode visualizar e gerenciar o conjunto de notificações atuais e mais antigas. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Existem duas categorias de alto nível de notificações que aparecem na Central de notificações:

1. Incidentes operacionais - ocorreu um evento, que normalmente requer uma resolução imediata. Por exemplo, resolver o problema de uma fila bloqueada.
1. Recomendações proativas - o Adobe tem uma recomendação para uma ação que um cliente deve tomar em breve. Por exemplo, para interromper a referência a uma interface obsoleta.

Consulte a [tabela abaixo](#supported-notification-types) para ver as notificações compatíveis no momento.

Na Central de notificações, você pode selecionar um programa e um ambiente específicos, o que tem o efeito de filtrar esse escopo.

## Configuração {#configuration}

Siga as etapas abaixo para configurar o recebimento de notificações:

1. Crie os seguintes Perfis de produto, conforme descrito [neste artigo](/help/journey-onboarding/notification-profiles.md), também atribuindo as IDs de Adobe apropriadas da sua organização para esses perfis. Isso permite que um administrador determine quais usuários se qualificam para receber essas notificações.
1. Cada usuário atribuído na etapa anterior pode configurar como gostaria de receber as notificações. No [página de preferências do Experience Cloud](https://experience.adobe.com/preferences/notification-section), verifique se a assinatura do Experience Manager está ativada e se **Incidentes operacionais** e **Recomendações proativas** as caixas de seleção estão marcadas para as colunas no aplicativo e de email (consulte a imagem abaixo). Além disso, é recomendável que a seção Emails esteja definida como **Notificações instantâneas** portanto, as notificações são recebidas imediatamente quando ocorre um incidente.

![Configurar assinaturas](/help/operations/assets/configure-subscriptions.png)

>[!NOTE]
>As notificações funcionam no nível da organização para que os assinantes recebam notificações para todos os programas e ambientes nesses programas.

## Fluxo detalhado do usuário {#detailed-user-flow}

Ao clicar no email, você será redirecionado para o Centro de notificações, com um pop-up que exibe o contexto da notificação em que você clicou e, em alguns casos, com links para informações adicionais descrevendo como tomar ações de correção.

![Detalhes do incidente](/help/operations/assets/incident-details.png)

Ao clicar em **Saiba mais**, o usuário é direcionado a este artigo, onde a notificação pode ser referenciada na tabela abaixo, que fornece orientação sobre qual ação tomar.

No Centro de notificações, você pode ver uma lista de outras notificações recentes. É recomendado reconhecer a existência de uma notificação, utilizando a lista Ações, para informar à Adobe que sua organização está ciente da tarefa, bem como “concluir” a notificação posteriormente, quando uma ação corretiva for tomada.

![Lista de notificações](/help/operations/assets/notification-list.png)

Na maioria dos casos, a notificação deve fornecer todo o contexto necessário para resolver o problema. No entanto, em caso de dúvidas relacionadas ao suporte da Adobe, clique no link **Entrar em contato com o suporte** no pop-up de notificação. Isso exibirá um formulário de onde você pode descrever a pergunta e enviá-lo para criar o tíquete de suporte, que também incluirá uma referência à notificação específica para que um engenheiro de suporte do Adobe tenha o contexto relevante.

![Entrar em contato com o suporte 1](/help/operations/assets/contact-support1.png)

![Entrar em contato com o suporte 2](/help/operations/assets/contact-support2.png)

Assim como todos os tíquetes de suporte, ele aparecerá na guia [Casos de suporte do Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/support-for-enterprise.html), onde é possível rastreá-lo e adicionar outros comentários.

![Suporte do Admin Console](/help/operations/assets/admin-console-support.png)

## Quais Notificações São Exibidas? {#which-notification}

O AEM as a Cloud Service tem vários tipos de notificações, mas apenas um subconjunto é exibido na Central de notificações, conforme ilustrado na tabela abaixo.

| Tipo de notificação | Descrição | Como configurar | Aparece na Central de notificações |
|---|---|---|---|
| Incidentes operacionais | Incidentes críticos que exigem uma ação imediata | Usuário atribuído ao perfil de produto &quot;Notificação de incidente - Cloud Service&quot;, caixa de seleção &quot;Incidentes operacionais&quot; selecionada em [Preferências de Experience Cloud](https://experience.adobe.com/preferences) | X |
| Recomendações proativas | Otimizações que devem ser planejadas | Usuário atribuído ao perfil de produto &quot;Notificação proativa - Cloud Service&quot;, caixa de seleção &quot;Recomendações proativas&quot; selecionada em [Preferências de Experience Cloud](https://experience.adobe.com/preferences) | X |
| Status de pipeline do Cloud Manager | Informações sobre o estado dos seus pipelines | Usuário com funções de Proprietário da empresa, Gerente de programas ou Gerente de implantação; caixa de seleção &quot;Outros&quot; marcada em [Preferências de Experience Cloud](https://experience.adobe.com/preferences) |  |

## Tipos de notificação suportados {#supported-notification-types}

A tabela a seguir lista os tipos de notificação aceitos no momento.

| Tipo de notificação | Perfil de produto relacionado | Ação de correção |
|---|---|---|
| Fila de replicação bloqueada | Incidente | Desbloqueie a fila seguindo as instruções da [Documentação de replicação](/help/operations/replication.md#troubleshooting) |
| Certificado S2S a expirar | Proativa | Saiba como atualizar uma credencial na documentação [Geração de tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |

