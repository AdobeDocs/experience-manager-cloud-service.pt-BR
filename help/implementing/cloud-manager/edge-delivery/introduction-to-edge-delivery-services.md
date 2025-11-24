---
title: Introdução ao Edge Delivery Services no Cloud Manager
description: Saiba como entregar seus projetos do Cloud Manager usando o Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 897f6376c594604527231f6f5a05a8b85d6858f3
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 3%

---


# Introdução ao Edge Delivery Services no Cloud Manager {#edge-delivery-services}

O Edge Delivery Services é um conjunto combinável de serviços que permite um alto grau de flexibilidade na maneira como você cria conteúdo no seu site. Essa capacidade permite fazer o seguinte:

* Crie sites rápidos com um Lighthouse Score perfeito.
* Monitore continuamente o desempenho por meio da Telemetria Operacional.
* Aumente a eficiência da criação desvinculando as fontes de conteúdo.

Você pode usar a gestão de conteúdo do AEM e a criação do WYSIWYG usando o Editor universal e a criação baseada em documento.

O Cloud Manager no AEM as a Cloud Service permite que você ative o Serviço Edge Delivery para o seu projeto.

>[!TIP]
>
>Para obter detalhes sobre o Edge Delivery Services e como ele pode ser usado com o AEM, consulte a [visão geral do Edge Delivery Services](/help/edge/overview.md).

## Sobre o Edge Delivery Services no Cloud Manager {#edge-in-cloud-manager}

Se você tiver licenciado o Edge Delivery Services como parte da Adobe Experience Manager Sites, poderá integrar seu site com o Edge Delivery Services diretamente na Cloud Manager e ativar o [usando uma experiência guiada de autoatendimento](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).

Além disso, você pode acessar uma experiência unificada para gerenciar todas as propriedades do AEM, garantindo a consistência entre os fluxos de trabalho principais. Esses workflows incluem gerenciamento de nome de domínio, gerenciamento de certificado SSL e mapeamentos CDN.

## Benefícios do uso do caminho recomendado pela Adobe para o Edge Delivery Services {#recommended-path-eds}

Maximize os benefícios do Adobe acessando e consumindo sua licença do Edge Delivery Services por meio da Cloud Manager. Isso permite aproveitar vários benefícios principais.

* [Consuma sua licença no programa escolhido](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md), [atualize outros programas](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md) ou ambos.
* Aproveite os benefícios da [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) para executar operações CRUD (Create, Read, Update, Delete).
* [Acessar relatórios do SLA](/help/implementing/cloud-manager/reports/report-sla.md)
* [Obtenha acesso ao suporte da Adobe](/help/edge/overview.md#support-ticket) para seus programas de produção registrados.

Se você tiver uma licença do Edge Delivery Services (EDS), poderá usar uma [CDN gerenciada pela Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) para seu site do Edge Delivery. Dessa forma, você habilita o gerenciamento de CDN de autoatendimento e certificados DV que são renovados automaticamente a cada três meses, a menos que você exclua o certificado.

Como alternativa, se você optar por usar sua CDN (ou seja, uma CDN não gerenciada pela Adobe), independentemente do licenciamento da Edge Delivery Services, será necessário configurá-la na plataforma `aem.live`. Consulte [Configuração da CDN BYO](https://www.aem.live/docs/byo-cdn-setup).


## Sobre adicionar o Edge Delivery Services a um programa de produção ou de sandbox

Uma Edge Delivery Services pode ser adicionada de várias maneiras diferentes, dependendo de como você começou o projeto ou quando deseja criar o site.

| Caso de uso | Descrição |
| --- | --- |
| Quero adicionar o Edge Delivery Services a um novo programa de produção. | Consulte [Criar programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>No assistente, na guia **Soluções e Complementos**, selecione **Edge Delivery Services**. |
| Quero adicionar o Edge Delivery Services a um programa de produção existente. | Consulte [Editar programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>Na caixa de diálogo **Editar Programa**, na guia **Soluções e Complementos**, selecione **Edge Delivery Services**. |
| Quero adicionar um site do Edge Delivery ao Cloud Manager | Consulte [Adicionar um site do Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). |
| Quero criar um site do Edge Delivery agora | Veja [Criar um site do Edge Delivery rapidamente no Cloud Manager com um clique de botão](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md). |
| Quero adicionar o Edge Delivery Services a um programa de sandbox novo ou existente. | Consulte [Criar programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>Ao criar um programa de sandbox, o Edge Delivery Services é adicionado ao programa por padrão; não é necessário selecioná-lo.<br>Os programas de sandbox existentes antes da disponibilização geral do Edge Delivery herdam o Edge Delivery Services automaticamente. |

>[!NOTE]
>
>* Para adicionar ou editar programas, você deve ser membro da função **Proprietário da empresa** ou receber permissão para fazer isso.
>* Sua organização deve ter uma licença do Edge Delivery Services não usada antes de ser aplicada a um programa de produção.
>* Depois que a licença do Edge Delivery Services é aplicada ou removida de um programa, a alteração entra em vigor imediatamente, sem a necessidade de executar um pipeline.


## Sobre a lista de tarefas do Edge Delivery no Cloud Manager {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

A **lista de tarefas do Edge Delivery** no Cloud Manager é uma lista de verificação de tarefas de integração criada para orientá-lo na integração e no gerenciamento do seu site do Edge Delivery até a [Ativação](/help/journey-onboarding/go-live-checklist.md).

![Lista de tarefas do site do Edge Delivery no Cloud Manager](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | Tarefa | Descrição |
| --- | --- | --- |
| 1 | Associe-se ao canal de colaboração de produtos | Clicar em **Enviar solicitação agora** envia uma solicitação à Adobe para criar um canal para sua empresa. Se o canal já existir, você será encaminhado para o canal de sua empresa. |
| 2 | Concluir pré-requisitos | Consulte o [Tutorial de introdução](https://www.aem.live/developer/tutorial). |
| 3 | Adicionar site do Edge Delivery OU <br>Criar um site agora | Consulte [Adicionar um site do Edge Delivery](#eds-add-site).<br>Consulte [Criar um site do Edge Delivery no Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md). |
| 4 | Configurar um site do Edge Delivery para usar um repositório Git externo | Consulte [Configurar um site do Edge Delivery para usar um repositório Git externo](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md). |
| 5 | Adicionar domínio | Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 6 | Adicionar certificado SSL | Consulte [Adicionar certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 7 | Configurar o CDN do site do Edge Delivery | Consulte [Adicionar um mapeamento de domínio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md). |
| 8 | Configurar validação por push | Consulte [Configurar validação por push para um site do Edge Delivery](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md). |
| 9 | Publicação | Consulte a [Lista de verificação de ativação](https://www.aem.live/docs/go-live-checklist). |

>[!VIDEO](https://video.tv.adobe.com/v/3441566?captions=por_br&learn=on)

## Registrar um tíquete de suporte {#eds-support-ticket}

{{support-ticket}}



