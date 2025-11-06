---
title: Centro de ações
description: Aproveite o Centro de ações para agir de forma conveniente em incidentes e outras informações importantes
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
feature: Operations
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 45%

---

# Centro de ações {#actions-center}

O AEM as Cloud Service envia notificações por email do Centro de ações quando ocorrem incidentes críticos que exigem ação imediata, bem como recomendações de otimização proativas. Os exemplos incluem uma fila bloqueada ou um conjunto de credenciais que está expirando. O conjunto completo de tipos de notificação do Centro de ações pode ser visto na [tabela abaixo](#supported-notification-types), que será ampliada ao longo do tempo.

Quando uma notificação por email do Centro de ações for recebida, é possível clicar nela para abrir o Centro de ações da AEM as a Cloud Service, com um pop-up exibindo um contexto adicional explicando a ação que um cliente deve tomar.

Além de exibir informações sobre a notificação em que você clicou, o Centro de ações serve como um hub onde você pode visualizar e gerenciar as notificações atuais e anteriores. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

Há duas categorias de alto nível de notificações que aparecem no Centro de ações:

1. Incidentes Operacionais: quando ocorre um evento que normalmente exige resolução imediata. Por exemplo, resolver o problema de uma fila bloqueada.
1. Recomendações Proativas: a Adobe tem uma recomendação para uma ação que um cliente deve tomar em breve. Por exemplo, para interromper a referência a uma interface obsoleta.

Consulte a [tabela abaixo](#supported-notification-types) para ver as notificações atualmente compatíveis no Centro de ações.

No Centro de ações, é possível selecionar um programa e ambiente específicos, que atuam como um filtro nesse escopo.

## Configuração {#configuration}

Para configurar as notificações por email da Central de Ações de recebimento, crie os Perfis de Produto conforme descrito em [Perfis de Notificação](/help/journey-onboarding/notification-profiles.md), ou seja, Notificação de Incidente - Cloud Service e Notificação Proativa - Cloud Service. Além disso, atribua a esses perfis as Adobe IDs adequadas da sua organização. Isso permite que um administrador determine quais usuários se qualificam para receber essas notificações por email.

>[!NOTE]
>As notificações por email do Centro de ações funcionam no nível da organização para que os assinantes recebam notificações de todos os programas e dos ambientes incluídos nesses programas.

## Fluxo detalhado do usuário {#detailed-user-flow}

Ao clicar no e-mail, você será redirecionado para o Centro de Ações, com um pop-up mostrando o contexto da notificação clicada e, em alguns casos, links para informações adicionais descrevendo como executar uma ação corretiva. Você também pode acessar o Centro de Ações diretamente em [https://experience.adobe.com/aem/actions-center](https://experience.adobe.com/aem/actions-center/), onde você pode selecionar o programa e o ambiente relevantes.

![Detalhes do incidente](/help/operations/assets/incident-details.png)

O link **Saiba mais** direciona a este artigo, onde o tipo de notificação pode ser consultado abaixo na [tabela de tipos de notificação compatíveis](#supported-notification-types), que fornece orientação sobre a ação a ser realizada.

No Centro de ações, é possível ver uma lista de outras notificações recentes. É recomendado reconhecer a existência de uma notificação, utilizando a lista Ações, para informar à Adobe que sua organização está ciente da tarefa, bem como “concluir” a notificação posteriormente, quando uma ação corretiva for tomada.

![Lista de notificações](/help/operations/assets/notification-list.png)

Na maioria dos casos, a janela pop-up deve fornecer todo o contexto necessário para resolver o problema. No entanto, se houver dúvidas sobre o Suporte da Adobe, você poderá clicar no link **Contatar Suporte** na janela pop-up. Isso exibirá um formulário, no qual é possível descrever a dúvida e enviá-la para criar um tíquete de suporte, que também incluirá uma referência à notificação específica para que um engenheiro de suporte da Adobe tenha o contexto relevante.

![Entrar em contato com o suporte 1](/help/operations/assets/contact-support1.png)

![Entrar em contato com o suporte 2](/help/operations/assets/contact-support2.png)

Assim como todos os tíquetes de suporte, ele aparecerá na guia [Casos de suporte do Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/support-for-enterprise.html), onde é possível rastreá-lo e adicionar outros comentários.

![Suporte do Admin Console](/help/operations/assets/admin-console-support.png)

## Que notificações aparecem? {#which-notification}

O AEM as a Cloud Service possui vários tipos de notificações, mas apenas um subconjunto deles é exibido no Centro de ações, conforme ilustrado na tabela abaixo.

| Tipo de notificação | Descrição | Como configurar | Aparece no Centro de ações |
|---------------------------------|-----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| Incidentes operacionais | Incidentes críticos que exigem ação imediata | Usuário atribuído ao perfil de produto “Notificação de incidente - Cloud Service” | X |
| Recomendações proativas | Otimizações que devem ser planejadas | Usuário atribuído ao perfil de produto “Notificação proativa - Cloud Service” | X |
| Status do pipeline do Cloud Manager | Informações sobre o estado dos seus pipelines | Usuário com funções de Proprietário da empresa, Gerente de programas ou Gerente de implantação, caixa de seleção &quot;Outros&quot; marcada nas [Preferências da Experience Cloud](https://experience.adobe.com/preferences), consulte [Notificações](/help/implementing/cloud-manager/notifications.md). |                           |

## Tipos de notificação compatíveis {#supported-notification-types}

A tabela a seguir lista os tipos de notificação atualmente aceitos no Centro de Ações. Atualmente, as notificações estão limitadas a ambientes de produção.

| Tipo de notificação | Perfil de produto relacionado | Ação de correção |
|---------------------------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Fila de replicação bloqueada | Incidente | Desbloqueie a fila seguindo as instruções da [Documentação de replicação](/help/operations/replication.md#troubleshooting) |
| Consulta GraphQL persistente inválida | Incidente | Corrija a consulta inválida do GraphQL fazendo referência à [documentação de solução de problemas de consultas persistidas do GraphQL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/persisted-queries-troubleshoot.html?lang=pt-BR) |
| Pico de tráfego na origem | Incidente | Proteja sua origem configurando regras de filtro de tráfego de limite de taxa que acionam limites menores que o alerta de pico de tráfego padrão na origem.  Consulte a seção [Bloqueando ataques DeS e DeS usando regras de tráfego](/help/security/traffic-filter-rules-including-waf.md#blocking-dos-and-ddos-attacks-using-traffic-filter-rules) da documentação Regras de filtro de tráfego, que faz referência a um tutorial. |
| Regras de Filtros de Tráfego CDN acionadas | Incidente | Se a regra de filtro de tráfego correspondente refletir um ataque e seu site não estiver bloqueando esse tráfego, proteja seu site configurando uma regra de filtro de tráfego no modo de bloqueio. Consulte a seção [Protegendo sites com regras de filtro de tráfego (incluindo regras do WAF)](/help/security/traffic-filter-rules-including-waf.md#tutorial-protecting-websites) da documentação Regras de filtro de tráfego, que faz referência a um tutorial. |
| Erros de encaminhamento do log do Splunk | Incidente | Verifique se o endpoint do Splunk está funcionando e pode ser acessado no ambiente do AEM Cloud Service. Para obter mais informações sobre o encaminhamento de logs, consulte a [documentação de encaminhamento de logs do Splunk](/help/implementing/developing/introduction/logging.md#splunk-logs). Se precisar de ajuda para solucionar problemas ou de alterações na configuração de registro, crie um tíquete de suporte no Adobe. |
| As páginas contêm um grande número de nós | Proativa | Reduza o número total de nós em uma página. Consulte a [Documentação de complexidade da página](https://experienceleague.adobe.com/pt-br/docs/experience-manager-pattern-detection/table-of-contents/pcx) | |
| Grande número de instâncias de fluxo de trabalho em execução | Proativa | Encerre workflows em execução que não são mais necessários. Saiba como [configurar um trabalho de limpeza](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/operations/maintenance) |               |
| Certificado S2S a expirar | Proativa | Saiba como atualizar uma credencial na documentação [Geração de tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) | Contagem Alta de Conexões | Proativa | Saiba mais sobre o pool de conexões no [Pool de Conexões juntamente com a documentação avançada de rede](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking) |
| Mapeamento de usuário de serviço obsoleto | Proativa | Saiba como usar o formato de Mapeamento de usuário do Sling Service mais recente, conforme indicado em [Práticas recomendadas para o Mapeamento de usuário do Sling Service e Definição de usuário do serviço](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/security/best-practices-for-sling-service-user-mapping-and-service-user-definition) |
| Contagem Alta de Conexões | Proativa | Saiba mais sobre o pool de conexões na [Documentação avançada de rede](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking) |  |
| Usuários adicionados diretamente ao grupo personalizado | Proativa | Os usuários precisam ser adicionados aos Grupos IMS relevantes e esses grupos IMS precisam ser adicionados como membros de grupos AEM. Alinhar com as [Práticas recomendadas do IMS](/help/security/ims-support.md) | |
| Conteúdo JCR ausente | Proativa | Adicione o nó ausente Conteúdo JCR. Consulte a [documentação do Assets Content Validator](https://experienceleague.adobe.com/pt-br/docs/experience-manager-pattern-detection/table-of-contents/acv) | |
| Fluxos de trabalho concluídos não removidos | Proativa | Minimize o número de instâncias de fluxo de trabalho e melhore o desempenho removendo as instâncias de fluxo de trabalho que têm mais de 90 dias. Saiba como [configurar tarefas de manutenção](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/operations/maintenance) | |
| Tipo de recurso Sling ausente na página | Proativa | Adicione o nó ausente do tipo de recurso Sling. Consulte a [documentação do Assets Content Validator](https://experienceleague.adobe.com/pt-br/docs/experience-manager-pattern-detection/table-of-contents/acv) | |
| Consulta lenta | Proativa | Corrija consultas lentas definindo definições de índice corretas, conforme sugerido pela [Folha de características da consulta JCQ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/JCR_query_cheatsheet-v1.1.pdf?lang=pt-BR) | |
| Consulta sem Índice | Proativa | Evite executar uma consulta que não use um índice - [vincular à Documentação de indexação](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/operations/indexing) | |
| Alerta de biblioteca obsoleta | Proativa | Substitua os pacotes obsoletos por suas versões mais recentes recomendadas, conforme descrito no [artigo de Substituição](/help/release-notes/deprecated-removed-features.md), para manter o aplicativo seguro e com desempenho | |
| Alerta de configuração obsoleta | Proativa | Substitua as configurações obsoletas por suas versões mais recentes recomendadas, conforme descrito no [artigo de Substituição](/help/release-notes/deprecated-removed-features.md), para manter seu aplicativo seguro e com desempenho |
