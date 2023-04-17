---
title: Centro de notificação
description: Utilize o centro de notificações para tomar ações apropriadas em caso de incidentes e para obter outras informações importantes
hidefromtoc: true
source-git-commit: 55ecd685afa28226974f3415b550bd2e8d05e2e6
workflow-type: ht
source-wordcount: '638'
ht-degree: 100%

---


# Centro de notificação {#notification-center}

>[!NOTE]
>Este recurso não foi lançado.

Depois de configurado, o AEM as a Cloud Service envia notificações sobre informações importantes para as quais os clientes devem tomar ações. Exemplos de notificações incluem uma fila bloqueada ou um conjunto de credenciais que está expirando. O conjunto completo de tipos de notificação pode ser observado na [tabela abaixo](#current-notification-types), e eles serão expandidos ao longo do tempo. As notificações são recebidas por email e como uma nova entrada no widget de notificação, que pode ser acessado clicando no ícone de sino no canto superior direito da Adobe Experience Cloud. As configurações de notificação podem ser definidas.

É possível clicar em uma notificação recebida para abrir o centro de notificações do AEM as a Cloud Service na forma de um pop-up, o qual exibe um contexto adicional explicando a ação recomendada para um cliente tomar.

Além de exibir informações sobre a notificação recém-clicada, o centro de notificações serve como um hub onde você pode visualizar e gerenciar o conjunto de notificações atuais e anteriores. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Há duas categorias de alto nível de notificações:

1. Incidentes: quando ocorre um evento que normalmente exige resolução imediata. Por exemplo, resolver o problema de uma fila bloqueada
1. Proativa: a Adobe tem uma recomendação para uma ação que um cliente deve tomar em breve. Por exemplo, para interromper a referência a uma interface obsoleta.

Consulte a [tabela abaixo](#current-notification-types) para ver as notificações compatíveis no momento.

Na tela Centro de notificações, é possível selecionar um programa e ambiente específicos, que atuam como um filtro nesse escopo.

## Configuração {#configuration}

Siga as etapas abaixo para configurar o recebimento de notificações:

1. Crie os seguintes perfis de produto (conforme descrito [neste artigo](/help/journey-onboarding/notification-profiles.md)) atribuindo as Adobe IDs apropriadas de sua organização a esses perfis.
1. Determine as configurações de notificação. [Nesta página](https://experience.adobe.com/preferences/notification-section), verifique se a assinatura do Experience Manager está ativada e se a caixa de seleção **Outros** está selecionada. Além disso, é recomendável que a seção Emails esteja definida como **Notificações instantâneas**, para que você receba notificações imediatamente após um incidente.

>[!NOTE]
>As assinaturas funcionam no nível da organização, para que os assinantes recebam notificações de todos os programas e ambientes desses programas.

## Fluxo detalhado do usuário {#detailed-user-flow}

Ao clicar no email, você será redirecionado para o Centro de notificações, com um pop-up que exibe o contexto da notificação em que você clicou e, em alguns casos, com links para informações adicionais descrevendo como tomar ações de correção.

![Detalhes do incidente](/help/operations/assets/incident-details.png)

Ao clicar em **Saiba mais**, o usuário é direcionado a este artigo, onde a notificação pode ser referenciada na tabela abaixo, que fornece orientação sobre qual ação tomar.

No Centro de notificações, você pode ver uma lista de outras notificações recentes. É recomendado reconhecer a existência de uma notificação, utilizando a lista Ações, para informar à Adobe que sua organização está ciente da tarefa, bem como “concluir” a notificação posteriormente, quando uma ação corretiva for tomada.

![Lista de notificações](/help/operations/assets/notification-list.png)

Na maioria dos casos, a notificação deve fornecer todo o contexto necessário para resolver o problema. No entanto, em caso de dúvidas relacionadas ao suporte da Adobe, clique no link **Entrar em contato com o suporte** no pop-up de notificação. Isso exibirá um formulário, no qual é possível descrever a pergunta e enviá-la para criar o tíquete de suporte, que também incluirá uma referência à notificação específica para que um engenheiro de suporte da Adobe tenha o contexto relevante.

![Entrar em contato com o suporte 1](/help/operations/assets/contact-support1.png)

![Entrar em contato com o suporte 2](/help/operations/assets/contact-support2.png)

Assim como todos os tíquetes de suporte, ele aparecerá na guia [Casos de suporte do Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/support-for-enterprise.html), onde é possível rastreá-lo e adicionar outros comentários.

![Suporte do Admin Console](/help/operations/assets/admin-console-support.png)

## Tipos de notificação atuais {#current-notification-types}

A tabela abaixo lista os tipos de notificação compatíveis no momento

| Tipo de notificação | Perfil de produto relacionado | Ação de correção |
|---|---|---|
| Fila de replicação bloqueada | Incidente | Desbloqueie a fila seguindo as instruções da [Documentação de replicação](/help/operations/replication.md#troubleshooting) |
| Certificado S2S a expirar | Proativa | Saiba como atualizar uma credencial na documentação [Geração de tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
