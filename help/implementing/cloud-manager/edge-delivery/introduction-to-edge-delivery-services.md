---
title: Introdução aos Edge Delivery Services no Cloud Manager
description: Saiba como entregar projetos do Cloud Manager usando o Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0fb5476b4cff9e26971696bd8352181a71e7b3e4
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 3%

---


# Introdução aos Edge Delivery Services no Cloud Manager {#edge-delivery-services}

O Edge Delivery Services é um conjunto de serviços combináveis que permite um alto grau de flexibilidade na maneira como você cria conteúdo no seu site. Essa capacidade permite fazer o seguinte:

* Crie sites rápidos com um Lighthouse Score perfeito.
* Monitore continuamente o desempenho por meio do RUM (Monitoramento de uso real).
* Aumente a eficiência da criação desvinculando as fontes de conteúdo.

Você pode usar a gestão de conteúdo do AEM e a criação do WYSIWYG usando o Editor universal e a criação baseada em documentos.

O Cloud Manager no AEM as a Cloud Service permite que você ative o Serviço Edge Delivery para o seu projeto.

>[!TIP]
>
>Para obter detalhes sobre Edge Delivery Services e como ele pode ser usado com AEM, consulte a [visão geral sobre Edge Delivery Services](/help/edge/overview.md).

## Sobre o Edge Delivery Services no Cloud Manager {#edge-in-cloud-manager}

Se você tiver licenciado Edge Delivery Services como parte do Adobe Experience Manager Sites, poderá integrar seu site com Edge Delivery Services diretamente no Cloud Manager e ativar o [usando uma experiência guiada de autoatendimento](/help/implementing/cloud-manager/managing-code/private-repositories.md).

Além disso, você pode acessar uma experiência unificada para gerenciar todas as propriedades do AEM, garantindo a consistência entre os fluxos de trabalho principais. Esses workflows incluem gerenciamento de nome de domínio, gerenciamento de certificado SSL e mapeamentos CDN.

## Vantagens de usar o caminho recomendado para o Adobe para o Edge Delivery Services {#recommended-path-eds}

Maximize os benefícios do Adobe, acessando e consumindo sua licença do Edge Delivery Services por meio da Cloud Manager. Isso permite aproveitar vários benefícios principais.

* [Consuma sua licença no programa escolhido](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md), [atualize outros programas](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md) ou ambos.
* Aproveite os benefícios da [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) para executar operações CRUD (Create, Read, Update, Delete).
* [Acessar relatórios do SLA](/help/implementing/cloud-manager/sla-reporting.md) (*em breve*)
* [Obtenha acesso ao suporte para Adobe](/help/edge/overview.md#support-ticket) para seus programas de produção registrados.

Além disso, o uso do Cloud Manager permite usar o [CDN gerenciado por Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) para o site do Edge Delivery e aproveitar os principais benefícios, como o gerenciamento de CDN de autoatendimento, incluindo a configuração e a adição de certificados DV. Além disso, após a criação de um certificado DV, o Adobe o renova automaticamente a cada três meses, a menos que ele seja excluído. Se você não tiver uma licença de Edge Delivery Services com o Adobe e decidir ignorar esses benefícios, só poderá usar seu próprio CDN gerenciado automaticamente. Esta configuração deve estar na plataforma [`aem.live`](https://www.aem.live/docs/go-live-checklist#cdn-configuration).

## Sobre adicionar Edge Delivery Services a um programa de produção ou de sandbox

Um Edge Delivery Services pode ser adicionado de várias maneiras diferentes, dependendo de como você começou seu projeto.

| Caso de uso | Descrição |
| --- | --- |
| Quero adicionar Edge Delivery Services a um novo programa de produção. | Consulte [Criar programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>No assistente, na guia **Soluções e Complementos**, selecione **Edge Delivery Services**. |
| Quero adicionar Edge Delivery Services a um programa de produção existente. | Consulte [Editar programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>Na caixa de diálogo **Editar Programa**, na guia **Soluções e Complementos**, selecione **Edge Delivery Services**. |
| Quero adicionar um site do Edge Delivery ao Cloud Manager | Consulte [Adicionar um site do Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). |
| Quero adicionar Edge Delivery Services a um programa de sandbox novo ou existente. | Consulte [Criar programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>Ao criar um programa de sandbox, o Edge Delivery Services é adicionado ao programa por padrão; não é necessário selecioná-lo.<br>Os programas de sandbox existentes antes da disponibilização geral do Edge Delivery herdarão Edge Delivery Services automaticamente. |

>[!NOTE]
>
>* Para adicionar ou editar programas, você deve ser membro da função **Proprietário da empresa** ou receber permissão para fazer isso.
>* Sua organização deve ter uma licença de Edge Delivery Services não usada para que possa ser aplicada a um programa de produção.
>* Depois que a licença do Edge Delivery Services é aplicada ou removida de um programa, a alteração entra em vigor imediatamente, sem a necessidade de executar um pipeline.


## Sobre a lista de tarefas do Edge Delivery no Cloud Manager {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

A **lista de tarefas do Edge Delivery** no Cloud Manager é uma lista de verificação de tarefas de integração criada para orientá-lo na integração e no gerenciamento do seu site do Edge Delivery até a [Ativação](/help/journey-onboarding/go-live-checklist.md).

![Lista de tarefas do site do Edge Delivery no Cloud Manager](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | Tarefa | Descrição |
| --- | --- | --- |
| 1 | Associe-se ao canal de colaboração de produtos | Clicar em **Enviar solicitação agora** envia uma solicitação ao Adobe para criar um canal para sua empresa. Se o canal já existir, você será encaminhado para o canal de sua empresa. |
| 2 | Concluir pré-requisitos | Consulte o [Tutorial de introdução](https://www.aem.live/developer/tutorial). |
| 3 | Adicionar site do Edge Delivery | Consulte [Adicionar um site do Edge Delivery](#eds-add-site). |
| 4 | Adicionar domínio | Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 5 | Adicionar certificado SSL | Consulte [Adicionar certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 6 | Configurar o CDN do site do Edge Delivery | Consulte [Adicionar uma configuração de CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md). |
| 7 | Configurar validação por push | Consulte [Configurar validação por push para um site do Edge Delivery](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md). |
| 8 | Publicação | Consulte a [Lista de verificação de ativação](/help/edge/docs/go-live-checklist.md). |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## Registrar um tíquete de suporte {#eds-support-ticket}

{{support-ticket}}



