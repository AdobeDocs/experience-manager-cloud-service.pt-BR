---
title: Centro de ações
description: Aproveite o Centro de ações para executar ações convenientemente em incidentes e outras informações importantes
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: ca7cad567a5f83cd1edc14def6d961b8ba3b7f1f
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 32%

---

# Centro de ações {#actions-center}

>[!NOTE]
>Este recurso não foi lançado.

O AEM as Cloud Service envia notificações por email do Centro de Ações quando ocorrem incidentes críticos que exigem ação imediata, bem como recomendações proativas para otimizações. Os exemplos incluem uma fila bloqueada ou um conjunto de credenciais expirando; o conjunto completo de tipos de notificação da Central de Ações pode ser exibido na [tabela abaixo](#supported-notification-types), que se expandirá com o tempo.

Quando uma notificação por email do Centro de ações for recebida, é possível clicar nela para abrir o Centro de ações do AEM as a Cloud Service com um pop-up que exibe um contexto adicional explicando a ação que um cliente deve tomar.

Além de exibir informações sobre a notificação por email recém-clicada, o Centro de Ações serve como um hub onde você pode visualizar e gerenciar o conjunto de notificações atuais e mais antigas. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Há duas categorias de alto nível de notificações que aparecem no Centro de Ações:

1. Incidentes Operacionais: quando ocorre um evento que normalmente exige resolução imediata. Por exemplo, resolver o problema de uma fila bloqueada.
1. Recomendações Proativas: a Adobe tem uma recomendação para uma ação que um cliente deve tomar em breve. Por exemplo, para interromper a referência a uma interface obsoleta.

Consulte a [tabela abaixo](#supported-notification-types) para as notificações atualmente aceitas no Centro de Ações.

No Centro de Ações, é possível selecionar um programa e um ambiente específicos, o que tem o efeito de filtrar esse escopo.

## Configuração {#configuration}

Para configurar as notificações por email do Centro de ações de recebimento, crie os Perfis de produto descritos [neste artigo](/help/journey-onboarding/notification-profiles.md), a saber, Notificação de incidente - Cloud Service e Notificação proativa - Cloud Service. Também atribua as IDs de Adobe da organização apropriadas a esses perfis. Isso permite que um administrador determine quais usuários se qualificam para receber essas notificações por email.

>[!NOTE]
>As notificações por email do Centro de Ações funcionam no nível da organização para que os assinantes recebam notificações para todos os programas e ambientes dentro desses programas.

## Fluxo detalhado do usuário {#detailed-user-flow}

Ao clicar no e-mail, você será redirecionado para a Central de Alertas, com um pop-up mostrando o contexto da notificação clicada e, em alguns casos, links para informações adicionais que descrevem como executar uma ação corretiva.

![Detalhes do incidente](/help/operations/assets/incident-details.png)

Clicar no **Saiba mais** navegue pelo usuário até este artigo, onde o tipo de notificação pode ser referenciado na variável [tabela de tipos de notificação compatíveis](#supported-notification-types) abaixo, que fornece orientações sobre as medidas a serem tomadas.

No Centro de Ações, você pode ver uma lista de outras notificações recentes. É recomendado reconhecer a existência de uma notificação, utilizando a lista Ações, para informar à Adobe que sua organização está ciente da tarefa, bem como “concluir” a notificação posteriormente, quando uma ação corretiva for tomada.

![Lista de notificações](/help/operations/assets/notification-list.png)

Na maioria dos casos, o pop-up deve fornecer todo o contexto necessário para resolver o problema. No entanto, se houver dúvidas sobre o Suporte para Adobe, clique no link **Entrar em contato com o suporte** no pop-up. Isso exibirá um formulário de onde você pode descrever a pergunta e enviá-lo para criar um tíquete de suporte, que também incluirá uma referência à notificação específica para que um engenheiro de suporte do Adobe tenha o contexto relevante.

![Entrar em contato com o suporte 1](/help/operations/assets/contact-support1.png)

![Entrar em contato com o suporte 2](/help/operations/assets/contact-support2.png)

Assim como todos os tíquetes de suporte, ele aparecerá na guia [Casos de suporte do Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/support-for-enterprise.html), onde é possível rastreá-lo e adicionar outros comentários.

![Suporte do Admin Console](/help/operations/assets/admin-console-support.png)

## Que notificações aparecem? {#which-notification}

O AEM as a Cloud Service tem vários tipos de notificações, mas apenas um subconjunto é exibido no Centro de Ações, conforme ilustrado na tabela abaixo.

| Tipo de notificação | Descrição | Como configurar | Aparece na Central de Alertas |
|---|---|---|---|
| Incidentes operacionais | Incidentes críticos que exigem ação imediata | Usuário atribuído ao perfil de produto &quot;Notificação de incidente - Cloud Service&quot; | X |
| Recomendações proativas | Otimizações que devem ser planejadas | Usuário atribuído ao perfil de produto &quot;Notificação proativa - Cloud Service&quot; | X |
| Status do pipeline do Cloud Manager | Informações sobre o estado dos seus pipelines | Usuário com funções de Proprietário da empresa, Gerente de Programas ou Gerente de implantação, caixa de seleção &quot;Outros&quot; selecionada em [Preferências da Experience Cloud](https://experience.adobe.com/preferences), como [descrito aqui](/help/implementing/cloud-manager/notifications.md). |  |

## Tipos de notificação compatíveis {#supported-notification-types}

A tabela a seguir lista os tipos de notificação atualmente aceitos no Centro de Ações.

| Tipo de notificação | Perfil de produto relacionado | Ação de correção |
|---|---|---|
| Fila de replicação bloqueada | Incidente | Desbloqueie a fila seguindo as instruções da [Documentação de replicação](/help/operations/replication.md#troubleshooting) |
| Certificado S2S a expirar | Proativa | Saiba como atualizar uma credencial na documentação [Geração de tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |

