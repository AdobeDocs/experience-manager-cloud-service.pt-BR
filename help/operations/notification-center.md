---
title: Central de notificações
description: Aproveite a Central de notificações para agir de maneira conveniente em incidentes e outras informações importantes
hidefromtoc: true
source-git-commit: a5977c667d831c47d41cd86b68e9196fbe726899
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Central de notificações {#notification-center}

>[!NOTE]
>Este recurso não foi lançado.

Depois de configurado, o AEM as Cloud Service envia notificações sobre informações importantes para as quais os clientes devem tomar medidas. Exemplos de notificações incluem uma fila bloqueada ou um conjunto de credenciais com expiração. O conjunto completo de tipos de notificação pode ser exibido no [tabela abaixo](#current-notification-types), e se expandirão com o tempo. As notificações são recebidas por email e como uma nova entrada no widget de notificação, que é acessado clicando no ícone de sino no canto superior direito em toda a Adobe Experience Cloud. As configurações de notificação podem ser definidas.

Quando uma notificação é recebida, é possível clicar nela para abrir a Central de notificações do AEM as a Cloud Service com um pop-up que exibe um contexto adicional explicando a ação recomendada para um cliente tomar.

Além de exibir informações sobre a notificação recém-clicada, o Centro de notificações serve como um hub onde você pode visualizar e gerenciar o conjunto de notificações atuais e mais antigas. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Existem duas categorias de alto nível de notificações:

1. Incidentes - ocorreu um evento, que normalmente requer resolução imediata. Por exemplo, resolver uma fila bloqueada
1. Pró-ativo - o Adobe tem uma recomendação para uma ação que um cliente deve tomar no futuro próximo. Por exemplo, para parar de fazer referência a uma interface obsoleta.

Consulte a [tabela abaixo](#current-notification-types) para as notificações aceitas no momento.

Na tela Central de notificações, você pode selecionar um programa e um ambiente específicos, o que tem o efeito de filtrar esse escopo.

## Configuração {#configuration}

Você pode seguir as etapas abaixo para configurar o recebimento de notificações:

1. Crie os seguintes Perfis de produto, conforme descrito [neste artigo](/help/journey-onboarding/user-groups.md), atribuindo as IDs de Adobe apropriadas da sua organização a esses perfis.
1. Determine as configurações de notificação. [Nesta página](https://experience.adobe.com/preferences/notification-section), verifique se a Assinatura de Experience Manager está ativada e se **Outros** está marcada. Além disso, é recomendável que a seção Emails esteja definida como **Notificações instantâneas** portanto, você recebe notificações imediatamente após a ocorrência de um incidente.

>[!NOTE]
>As assinaturas funcionam no nível da organização para que os assinantes recebam notificações para todos os programas e ambientes nesses programas.

## Fluxo de usuário detalhado {#detailed-user-flow}

Ao clicar no e-mail, você será redirecionado para a Central de notificações, com um pop-up que mostra o contexto da notificação clicada e, em alguns casos, links para informações adicionais que descrevem como executar uma ação corretiva.

![Detalhes do incidente](/help/operations/assets/incident-details.png)

Clicar no **Saiba mais** link leva o usuário até este artigo, onde a notificação pode ser referenciada na tabela abaixo, que fornece orientação sobre qual ação tomar.

No Centro de notificações, você pode ver uma lista de outras notificações recentes. Recomenda-se que, usando a lista Ações, você reconheça uma notificação para sinalizar ao Adobe que sua organização está ciente da tarefa e para resolver posteriormente a notificação quando uma ação corretiva tiver sido tomada.

![Lista de notificações](/help/operations/assets/notification-list.png)

Na maioria dos casos, a notificação deve fornecer todo o contexto necessário para resolver o problema. No entanto, se houver dúvidas sobre o Suporte para Adobe, clique no link **Entrar em contato com o suporte** no pop-up de notificação. Isso exibirá um formulário de onde você pode descrever a pergunta e enviá-lo para criar o tíquete de suporte, que também incluirá uma referência à notificação específica para que um engenheiro de suporte do Adobe tenha o contexto relevante.

![Entrar em contato com o suporte 1](/help/operations/assets/contact-support1.png)

![Entrar em contato com o suporte 2](/help/operations/assets/contact-support2.png)

Como todos os tíquetes de suporte, ele aparecerá no [Guia Casos de suporte da Adobe Admin Console](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html), onde é possível rastreá-lo e adicionar comentários.

![Suporte para Admin Console](/help/operations/assets/admin-console-support.png)

## Tipos de Notificação Atuais {#current-notification-types}

A tabela abaixo lista os Tipos de Notificação aceitos no momento

| Tipo de notificação | Perfil de produto relacionado | Ação corretiva |
|---|---|---|
| Fila de replicação bloqueada | Incidente | Desbloqueie a fila seguindo as instruções na guia [Documentação de replicação](/help/operations/replication.md#troubleshooting) |
| Certificado S2S em expiração | Pró-ativo | Saiba como atualizar uma credencial no [Geração de tokens de acesso para a documentação de APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
