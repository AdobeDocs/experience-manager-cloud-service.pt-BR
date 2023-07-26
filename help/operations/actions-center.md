---
title: Centro de ações
description: Use o Centro de ações para tomar as medidas apropriadas em caso de incidentes e obter outras informações importantes
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: 083aa4b893b58102b3a0bf68c4dd3b4c003b48f6
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 90%

---

# Centro de ações {#actions-center}

>[!NOTE]
>Este recurso não foi lançado.

O AEM as Cloud Service envia notificações por email do Centro de Ações quando ocorrem incidentes críticos que exigem ação imediata e recomendações proativas para otimizações. Os exemplos incluem uma fila bloqueada ou um conjunto de credenciais que está expirando. O conjunto completo de tipos de notificação do Centro de ações pode ser visto na [tabela abaixo](#supported-notification-types), que será ampliada ao longo do tempo.

Ao receber uma notificação do Centro de ações, você pode clicar nela para abrir o Centro de ações do AEM as a Cloud Service na forma de um pop-up, que exibe um contexto adicional explicando a ação a ser realizada.

Além de exibir informações sobre a notificação em que você clicou, o Centro de ações serve como um hub onde você pode visualizar e gerenciar as notificações atuais e anteriores. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

Há duas categorias de alto nível de notificações que aparecem no Centro de ações:

1. Incidentes Operacionais: quando ocorre um evento que normalmente exige resolução imediata. Por exemplo, resolver o problema de uma fila bloqueada.
1. Recomendações Proativas: a Adobe tem uma recomendação para uma ação que um cliente deve tomar em breve. Por exemplo, para interromper a referência a uma interface obsoleta.

Consulte a [tabela abaixo](#supported-notification-types) para ver as notificações atualmente compatíveis no Centro de ações.

No Centro de ações, é possível selecionar um programa e ambiente específicos, que atuam como um filtro nesse escopo.

## Configuração {#configuration}

Para configurar o recebimento de notificações por email do Centro de ações, crie os perfis de produto descritos [neste artigo](/help/journey-onboarding/notification-profiles.md), mais especificamente a Notificação de incidente - Cloud Service e Notificação proativa - Cloud Service. Além disso, atribua a esses perfis as Adobe IDs adequadas da sua organização. Isso permite que um administrador determine quais usuários se qualificam para receber essas notificações por email.

>[!NOTE]
>As notificações por email do Centro de ações funcionam no nível da organização para que os assinantes recebam notificações de todos os programas e dos ambientes incluídos nesses programas.

## Fluxo detalhado do usuário {#detailed-user-flow}

Ao clicar no email, você será redirecionado para o Centro de ações, onde um pop-up será exibido com o contexto da notificação em que você clicou e, em alguns casos, com links para informações adicionais que descrevem como realizar ações de correção.

![Detalhes do incidente](/help/operations/assets/incident-details.png)

O link **Saiba mais** direciona a este artigo, onde o tipo de notificação pode ser consultado abaixo na [tabela de tipos de notificação compatíveis](#supported-notification-types), que fornece orientação sobre a ação a ser realizada.

No Centro de ações, é possível ver uma lista de outras notificações recentes. Recomenda-se que, usando a lista Ações, você reconheça uma notificação para sinalizar ao Adobe que sua organização está ciente da tarefa e para resolver posteriormente a notificação quando uma ação corretiva tiver sido tomada.

![Lista de notificações](/help/operations/assets/notification-list.png)

Na maioria dos casos, o pop-up deve fornecer todo o contexto necessário para resolver o problema. No entanto, se tiver perguntas para o suporte da Adobe, clique no link **Entrar em contato com o suporte** no pop-up. Isso exibirá um formulário, no qual é possível descrever a dúvida e enviá-la para criar um tíquete de suporte, que também incluirá uma referência à notificação específica para que um engenheiro de suporte da Adobe tenha o contexto relevante.

![Entrar em contato com o suporte 1](/help/operations/assets/contact-support1.png)

![Entrar em contato com o suporte 2](/help/operations/assets/contact-support2.png)

Assim como todos os tíquetes de suporte, ele aparecerá na guia [Casos de suporte do Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/support-for-enterprise.html), onde é possível rastreá-lo e adicionar outros comentários.

![Suporte do Admin Console](/help/operations/assets/admin-console-support.png)

## Que notificações aparecem? {#which-notification}

O AEM as a Cloud Service possui vários tipos de notificações, mas apenas um subconjunto deles é exibido no Centro de ações, conforme ilustrado na tabela abaixo.

| Tipo de notificação | Descrição | Como configurar | Aparece no Centro de ações |
|---|---|---|---|
| Incidentes operacionais | Incidentes críticos que exigem ação imediata | Usuário atribuído ao perfil de produto “Notificação de incidente - Cloud Service” | X |
| Recomendações proativas | Otimizações que devem ser planejadas | Usuário atribuído ao perfil de produto “Notificação proativa - Cloud Service” | X |
| Status do pipeline do Cloud Manager | Informações sobre o estado dos seus pipelines | Usuário com funções de Proprietário da empresa, Gerente de Programas ou Gerente de implantação, caixa de seleção &quot;Outros&quot; selecionada em [Preferências da Experience Cloud](https://experience.adobe.com/preferences), conforme [descrito aqui](/help/implementing/cloud-manager/notifications.md). |   |

## Tipos de notificação compatíveis {#supported-notification-types}

A tabela a seguir lista os tipos de notificação atualmente compatíveis no Centro de ações. Atualmente, as notificações estão limitadas a ambientes de produção.

| Tipo de notificação | Perfil de produto relacionado | Ação de correção |
|---|---|---|
| Fila de replicação bloqueada | Incidente | Desbloqueie a fila seguindo as instruções da [Documentação de replicação](/help/operations/replication.md#troubleshooting) |
| Certificado S2S a expirar | Proativa | Saiba como atualizar uma credencial na documentação [Geração de tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |

