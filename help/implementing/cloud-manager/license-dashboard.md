---
title: Painel de licenças
description: O Cloud Manager fornece um painel para facilitar a visualização dos direitos de produto do AEMaaCS disponíveis para sua organização ou locatário.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: d5e0ca924dee50d7dd4f9057010b1a39780b4352
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 100%

---

# Painel de licenças {#license-dashboard}

O Cloud Manager fornece um painel para facilitar a visualização dos direitos de produto do AEMaaCS disponíveis para sua organização ou locatário.

## Visão geral {#overview}

O Painel de licenças do Cloud Manager fornece acesso fácil às seguintes informações:

1. Direitos da solução disponíveis para você em todos os seus programas, incluindo o que é usado e o que está disponível
1. Métricas de consumo de Solicitação de conteúdo com tendência mensal para a solução Sites

## Uso do Painel de dispositivos {#using-dashboard}

Para acessar o painel de licenças, siga estas etapas.

>[!NOTE]
>
>Um usuário com a função **Proprietário da empresa** deve estar conectado para exibir o Painel de licenças.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Na página de visão geral dos produtos, alterne para a guia **Licença**.

![Painel de licenças](assets/license-dashboard.png)

O painel é dividido em três seções que mostram:

* **Soluções** - Essa seção resume quais soluções você licenciou, como Sites ou Assets.
* **Complementos** - Essa seção resume quais complementos estão disponíveis para suas soluções licenciadas.
* **Ambientes de sandbox e desenvolvimento** - Essa seção resume quais ambientes estão disponíveis para você.

Cada seção resume o que está disponível e como é usado no momento, se for o caso. Atualmente, somente as soluções do Sites são exibidas, mesmo se outras soluções existirem no locatário.

* A coluna **Status** exibe o número de direitos não utilizados em relação ao total disponível para o locatário.
* A coluna **Configurado em** indica os programas nos quais o direito da solução foi aplicado.
   * Um direito será considerado usado somente quando um ambiente de produção for criado ou, se o ambiente já existir, quando um pipeline de atualização for executado nele.
* A coluna **Uso** exibe as solicitações de conteúdo consumidas nos últimos 12 meses na forma de um gráfico quando clicadas.

>[!TIP]
>
>Consulte [Visão geral do Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para saber como gerenciar seus direitos da Adobe para toda a organização no Admin Console.

## Perguntas frequentes {#faq}

### O que é uma solicitação de conteúdo? {#what-is-a-content-request}

Uma solicitação de conteúdo é uma solicitação recebida no AEM Sites ou em qualquer sistema de cache fornecido pelo cliente, como por exemplo, uma rede de entrega de conteúdo, para fornecer conteúdo ou dados no formato HTML como uma exibição de página ou no formato JSON como uma chamada de API.

Uma solicitação de conteúdo é contabilizada para cada exibição de página ou para cada cinco chamadas de API, medidas na entrada do primeiro sistema de cache a receber uma solicitação de conteúdo. As solicitações de conteúdo são contabilizadas somente em ambientes de produção.

As solicitações de conteúdo excluem solicitações ou atividades iniciadas pela Adobe, ou em nome dela, com o único objetivo de fornecer produtos e serviços. O tráfego de agente de usuário identificado pela Adobe como bots, crawlers e spiders relacionados a mecanismos de pesquisa comuns e serviços de redes sociais também são excluídos.

### Como o Adobe Experience Manager mede as solicitações de conteúdo? {#how-are-content-requests-measured}

As solicitações de conteúdo são rastreadas nos servidores de borda do AEM as a Cloud Service. O tráfego de origem não é contabilizado nas solicitações de conteúdo. O CDN incorporado ao AEM as a Cloud Service rastreia solicitações HTML e JSON válidas.

O AEM também tem regras em vigor para excluir bots conhecidos, incluindo serviços conhecidos que acessam o site regularmente para atualizar seu índice de pesquisa ou serviço.

### Por que meu relatório de Analytics mostra resultados diferentes das solicitações de conteúdo do AEM? {#why-are-reports-different}

As solicitações de conteúdo terão variações entre as ferramentas de relatório de Analytics de uma organização, conforme resumido nesta tabela.

| Motivo da variação | Explicação |
|---|---|
| Marcação com tags | Todas as páginas que são rastreadas como solicitações de conteúdo do AEM podem ou não ser marcadas com o rastreamento de Analytics. Todas as chamadas de API que são rastreadas como solicitações de conteúdo do AEM não serão marcadas pela ferramenta de Analytics de uma organização.<br>As páginas ou chamadas de API podem ser marcadas para rastrear ações ou apenas exibições de página exclusivas, em vez de todas as exibições. |
| Regras de gerenciamento de tags | As configurações das regras de gerenciamento de tags podem resultar em várias configurações de coleta de dados em uma página, o que gera uma combinação de discrepâncias com o rastreamento de solicitação de conteúdo. |
| Bots | Os bots desconhecidos que não foram pré-identificados e removidos pelo AEM podem causar discrepâncias no rastreamento. |
| Report Suites | As páginas que fazem parte de uma mesma instância e domínio do AEM podem enviar dados para diferentes conjuntos de relatórios de Analytics. |
| Ferramentas de segurança e monitoramento de terceiros | Ferramentas de verificação para monitoramento e segurança podem gerar solicitações de conteúdo para o AEM que não são rastreadas nos relatórios de Analytics. |
| Solicitações de pré-busca | Usar um serviço de pré-busca para pré-carregar páginas a fim de aumentar a velocidade pode causar um aumento significativo no tráfego de solicitações de conteúdo. |
| DDOS | Apesar de todos os esforços da Adobe para detectar e filtrar automaticamente o tráfego de ataques de DDOS, não há garantia de que todos os possíveis ataques de DDOS serão detectados. |
| Bloqueadores de tráfego | O uso de um bloqueador de rastreadores em um navegador pode impedir o rastreamento de algumas solicitações. |
| Firewalls | Os firewalls podem bloquear o rastreamento do Analytics. Isso é mais frequente com firewalls corporativos. |

### E se eu quiser saber mais sobre o volume de solicitação de conteúdo? {#current-request-volumes}

Se você quiser obter insights adicionais sobre o volume de solicitação de conteúdo mostrado no Painel de licenças, a equipe da Adobe pode fornecer um relatório que mostra os principais responsáveis pelo volume das solicitações de conteúdo. Entre em contato com a equipe da Adobe ou com o Atendimento ao cliente da Adobe para solicitar um relatório de uso principal.

### E se eu estiver usando meu próprio CDN? {#using-own-cdn}

O Painel de Licenças mostrará apenas os dados rastreados pelo CDN do Cloud Service.  Se optar por trazer seu próprio CDN (BYOCDN), você precisará relatar o volume de solicitações de conteúdo à Adobe anualmente, conforme declarado em seu contrato.
