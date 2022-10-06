---
title: Painel de licenças
description: O Cloud Manager fornece um painel para facilitar a visualização dos direitos de produto do AEMaaCS disponíveis para sua organização ou locatário.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: b5078c849c9fa088546f5df1fcbef1dec59f3cdb
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 3%

---

# Painel de licenças {#license-dashboard}

O Cloud Manager fornece um painel para facilitar a visualização dos direitos de produto do AEMaaCS disponíveis para sua organização ou locatário.

## Visão geral {#overview}

O Painel de Licenças do Cloud Manager fornece acesso fácil às seguintes informações:

1. Direitos da solução disponíveis para você em todos os seus programas, incluindo o que é usado e o que está disponível
1. Métricas de consumo de Solicitação de conteúdo com tendência mensal para a solução Sites

## Uso do Painel de Licenças {#using-dashboard}

Para acessar o painel de licenças, siga estas etapas.

>[!NOTE]
>
>Um usuário em **Proprietário da empresa** deve estar conectado para exibir o Painel de licenças.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Na página de visão geral dos produtos, alterne para a **Licença** guia .

![Painel de licenças](assets/license-dashboard.png)

O painel é dividido em três seções que mostram:

* **Soluções** - Esta seção resume quais soluções você licenciou, como Sites ou Ativos.
* **Complementos** - Esta seção resume quais complementos para suas soluções licenciadas você tem disponível.
* **Ambientes de sandbox e desenvolvimento** - Esta seção resume quais ambientes você tem disponíveis.

Cada seção resume o que está disponível e como está sendo usado no momento, se houver alguma. Atualmente, somente as soluções do Sites são exibidas mesmo se outras soluções existirem no locatário.

* O **Status** exibe o número de direitos não utilizados vs. total disponível para o locatário.
* O **Configurado em** indica os programas nos quais o direito da solução foi aplicado.
   * Um direito é considerado como usado somente quando um ambiente de produção foi criado ou se já existir, se um pipeline de atualização tiver sido executado nele.
* O **Uso** exibe as solicitações de conteúdo consumidas nos últimos 12 meses como um gráfico quando clicadas.

>[!TIP]
>
>Consulte [Visão geral do Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para saber como gerenciar os direitos de Adobe em toda a organização no Admin Console.

## Perguntas frequentes  {#faq}

### O que é uma solicitação de conteúdo? {#what-is-a-content-request}

Uma solicitação de conteúdo é uma solicitação que entra no AEM Sites ou em qualquer sistema de cache fornecido pelo cliente, como uma rede de entrega de conteúdo para fornecer conteúdo ou dados no formato HTML como uma exibição de página ou no formato JSON como uma chamada de API.

Uma solicitação de conteúdo é contada para cada exibição de página ou para cada cinco chamadas de API, medidas na entrada do primeiro sistema de cache a receber uma solicitação de conteúdo. As solicitações de conteúdo são contadas somente em ambientes de produção.

As Solicitações de conteúdo excluem solicitações ou atividades iniciadas pelo Adobe ou em seu nome com o único objetivo de fornecer produtos e serviços. O tráfego de agente de usuário identificado por Adobe de bots, crawlers e spiders relacionados a mecanismos de pesquisa comuns e serviços de mídia social também são excluídos.

### Como o Adobe Experience Manager avalia as solicitações de conteúdo? {#how-are-content-requests-measured}

As solicitações de conteúdo são rastreadas nos servidores de borda AEM as a Cloud Service. O tráfego de origem não conta para solicitações de conteúdo. A CDN incorporada AEM rastreia solicitações HTML e JSON válidas.

AEM também tem regras em vigor para excluir bots conhecidos, incluindo serviços conhecidos visitando o site regularmente para atualizar seu índice de pesquisa ou serviço.

### Por que meu relatório do Analytics mostra resultados diferentes das Solicitações de conteúdo AEM? {#why-are-reports-different}

As Solicitações de conteúdo terão variações com as ferramentas de relatório do Analytics de uma organização, conforme resumido nesta tabela.

| Motivo Da Variação | Explicação |
|---|---|
| Marcação com tags | Todas as páginas que são rastreadas como solicitações de conteúdo AEM podem ou não ser marcadas com o rastreamento do Analytics. Todas as chamadas de API que são rastreadas como solicitações de conteúdo AEM não serão marcadas pela ferramenta Analytics de uma organização.<br>As páginas ou chamadas de API podem ser marcadas para rastrear ações ou apenas exibições de página exclusivas, em vez de todas as exibições. |
| Regras do Tag Management | As configurações de regras do Tag Management podem resultar em várias configurações de coleta de dados em uma página, resultando em alguma combinação de discrepâncias com o rastreamento de solicitação de conteúdo. |
| Bots | Os bots desconhecidos que não foram pré-identificados e removidos pelo AEM podem causar discrepâncias no rastreamento. |
| Report Suites | As páginas que fazem parte da mesma instância e domínio de AEM podem enviar dados para conjuntos de relatórios do Analytics diferentes. |
| Ferramentas de segurança e monitoramento de terceiros | Ferramentas de varredura de monitoramento e segurança podem gerar solicitações de conteúdo para AEM que não são rastreadas nos relatórios do Analytics. |
| Buscar previamente solicitações | Usar um serviço de pré-busca para pré-carregar páginas para aumentar a velocidade pode causar um aumento significativo no tráfego de solicitação de conteúdo. |
| DDOS | Embora o Adobe faça todos os esforços para detectar e filtrar automaticamente o tráfego de ataques de DDOS, não há garantia de que todos os possíveis ataques de DDOS serão detectados |
| Bloqueadores de tráfego | O uso de um bloqueador de rastreadores em um navegador pode impedir que algumas solicitações sejam rastreadas. |
| Firewalls | Os firewalls podem bloquear o rastreamento do Analytics. Isso é mais frequente com firewalls corporativos. |

### E se eu quiser saber mais sobre o volume de solicitação de conteúdo? {#current-request-volumes}

Se você quiser obter insights adicionais sobre o volume de solicitação de conteúdo mostrado no Painel de licenças, a equipe do Adobe pode fornecer um relatório que mostra os principais drivers de volume das solicitações de conteúdo. Entre em contato com a equipe do Adobe ou com o Atendimento ao cliente do Adobe para solicitar um relatório de uso principal.

### E se eu estiver usando meu próprio CDN? {#using-own-cdn}

O Painel de Licenças mostrará apenas os dados rastreados pelo Cloud Service CDN.  Se optar por trazer seu próprio CDN (BYOCDN), você reportará o volume de solicitação de conteúdo de volta ao Adobe anualmente, conforme declarado em seu contrato.
