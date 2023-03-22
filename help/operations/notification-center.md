---
title: Centro de notificação
description: Aproveite o centro de notificações para agir convenientemente sobre incidentes e outras informações importantes
hidefromtoc: true
source-git-commit: 55ecd685afa28226974f3415b550bd2e8d05e2e6
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Centro de notificação {#notification-center}

>[!NOTE]
>Este recurso não foi lançado.

Depois de configurado, o AEM como Cloud Service envia notificações sobre informações importantes para as quais os clientes devem tomar medidas. Os exemplos de notificações incluem uma fila bloqueada ou um conjunto de credenciais que está expirando. O conjunto completo de tipos de notificação pode ser visualizado no [tabela abaixo](#current-notification-types)e se expandirão ao longo do tempo. As notificações são recebidas por email e como uma nova entrada no widget de notificação, que é acessada clicando no ícone de sino no canto superior direito do Adobe Experience Cloud. As configurações de notificação podem ser definidas.

Quando uma notificação é recebida, ela pode ser clicada para abrir AEM Centro de notificações do as a Cloud Service com um pop-up que exibe o contexto adicional explicando a ação recomendada para um cliente tomar.

Além de exibir informações sobre a notificação recém-clicada, o Centro de Notificações serve como um hub onde você pode visualizar e gerenciar o conjunto de notificações atuais e anteriores. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Há duas categorias de alto nível de notificações:

1. Incidentes - um evento ocorreu, o que normalmente requer resolução imediata. Por exemplo, resolver uma fila bloqueada
1. Proativa - o Adobe tem uma recomendação para uma ação que um cliente deve tomar em breve. Por exemplo, para interromper a referência a uma interface do usuário obsoleta.

Consulte a [tabela abaixo](#current-notification-types) para as notificações atualmente suportadas.

Na tela Central de notificações, é possível selecionar um programa e ambiente específicos, que têm o efeito de filtrar esse escopo.

## Configuração {#configuration}

Siga as etapas abaixo para configurar o recebimento de notificações:

1. Crie os seguintes Perfis de produto, conforme descrito [neste artigo](/help/journey-onboarding/notification-profiles.md), atribuindo as IDs de Adobe apropriadas de sua organização a esses perfis.
1. Determine as configurações de notificação. [Nesta página](https://experience.adobe.com/preferences/notification-section), verifique se a Assinatura do Experience Manager está ativada e a variável **Outros** está marcada. Além disso, é recomendável que a seção Emails esteja definida como **Notificações instantâneas** para que você receba notificações imediatamente após um incidente.

>[!NOTE]
>As assinaturas funcionam no nível da organização para que os assinantes recebam notificações de todos os programas e ambientes nesses programas.

## Fluxo detalhado do usuário {#detailed-user-flow}

Ao clicar no email, você será redirecionado para a Central de notificações, com um pop-up mostrando o contexto da notificação em que você clicou e, em alguns casos, com links para informações adicionais descrevendo como tomar as ações corretivas.

![Detalhes do incidente](/help/operations/assets/incident-details.png)

Clicar no **Saiba mais** O link navega o usuário para este artigo, onde a notificação pode ser referenciada na tabela abaixo, que fornece orientação sobre qual ação tomar.

Na Central de notificações, você pode ver uma lista de outras notificações recentes. É recomendável que, usando a lista Ações, você reconheça uma notificação para avisar ao Adobe que sua organização está ciente da tarefa e resolver posteriormente a notificação quando uma ação corretiva for tomada.

![Lista de notificações](/help/operations/assets/notification-list.png)

Na maioria dos casos, a notificação deve fornecer todo o contexto necessário para resolver o problema. No entanto, em caso de dúvidas relacionadas ao suporte ao Adobe, clique no botão **Entre em contato com o suporte** no pop-up de notificação. Isso exibirá um formulário de onde você pode descrever a pergunta e enviá-la para criar o tíquete de suporte, que também incluirá uma referência à notificação específica para que um Engenheiro de suporte do Adobe tenha o contexto relevante.

![Entre em contato com o suporte 1](/help/operations/assets/contact-support1.png)

![Entre em contato com o suporte 2](/help/operations/assets/contact-support2.png)

Como todos os tíquetes de suporte, ele aparecerá no [Guia Casos de suporte do Adobe Admin Console](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html), onde é possível rastreá-lo e adicionar outros comentários.

![Suporte a Admin Console](/help/operations/assets/admin-console-support.png)

## Tipos de Notificação Atuais {#current-notification-types}

A tabela abaixo lista os Tipos de Notificação atualmente compatíveis

| Tipo de notificação | Perfil de produto relacionado | Ação Corretiva |
|---|---|---|
| Fila de replicação bloqueada | Incidente | Desbloqueie a fila seguindo as instruções em [Documentação de replicação](/help/operations/replication.md#troubleshooting) |
| Expirando certificado S2S | Proativa | Saiba como atualizar uma credencial no [Geração de tokens de acesso para a documentação de APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
