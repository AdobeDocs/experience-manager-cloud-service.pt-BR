---
title: Introdução aos Edge Delivery Services no Cloud Manager
description: Saiba como entregar projetos do Cloud Manager usando o Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 2%

---

# Introdução aos Edge Delivery Services no Cloud Manager {#edge-delivery-services}

O Edge Delivery Services é um conjunto de serviços combináveis que permite um alto grau de flexibilidade na maneira como você cria conteúdo no seu site. Essa capacidade permite fazer o seguinte:

* Crie sites rápidos com um Lighthouse Score perfeito.
* Monitore continuamente o desempenho por meio do RUM (Monitoramento de uso real).
* Aumente a eficiência da criação desvinculando as fontes de conteúdo.

Você pode usar a gestão de conteúdo AEM e a criação WYSIWYG usando o Editor universal e a criação baseada em documento.

O Cloud Manager no AEM as a Cloud Service permite que você ative o Serviço Edge Delivery para o seu projeto.

>[!TIP]
>
>Para obter detalhes sobre Edge Delivery Services e como ele pode ser usado com AEM, consulte [visão geral sobre Edge Delivery Services](/help/edge/overview.md).

<!-- RELEASED TO GA SEPTEMBER 5, 2024
>[!NOTE]
>
>This feature is only available to [the early adopter program](/help/implementing/cloud-manager/release-notes/current.md#early-adoption). -->


## Sobre o Edge Delivery Services no Cloud Manager {#edge-in-cloud-manager}

Se você tiver licenciado Edge Delivery Services como parte do Adobe Experience Manager Sites, poderá integrar seu site com Edge Delivery Services diretamente no Cloud Manager e ativar o [usando uma experiência guiada de autoatendimento](/help/implementing/cloud-manager/managing-code/private-repositories.md).

Além disso, você pode acessar uma experiência unificada para gerenciar todas as propriedades do AEM, garantindo a consistência entre os fluxos de trabalho principais. Isso inclui gerenciamento de nome de domínio, gerenciamento de certificado SSL e mapeamentos de CDN.

## Adicionar Edge Delivery Services a um programa de produção ou de sandbox

Para adicionar ou editar programas, você deve ser membro da função **Proprietário da empresa** ou receber permissão para fazer isso.

Sua organização deve ter uma licença de Edge Delivery Services não usada para que possa ser aplicada a um programa de produção.

>[!NOTE]
>
>Depois que a licença do Edge Delivery Services é aplicada ou removida de um programa, a alteração entra em vigor imediatamente, sem a necessidade de executar um pipeline. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

Dependendo do caso de uso, siga um destes procedimentos:

| Caso de uso | Descrição |
| --- | --- |
| Quero adicionar Edge Delivery Services a um novo programa de produção. | Consulte [Criar programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>No assistente, na guia **Soluções e Complementos**, selecione **Edge Delivery Services**. |
| Quero adicionar Edge Delivery Services a um programa de produção existente. | Consulte [Editar programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>Na caixa de diálogo **Editar Programa**, na guia **Soluções e Complementos**, selecione **Edge Delivery Services**. |
| Quero adicionar um site do Edge Delivery ao Cloud Manager | Consulte [Adicionar um site do Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). |
| Quero adicionar Edge Delivery Services a um programa de sandbox novo ou existente. | Consulte [Criar programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>Ao criar um programa de sandbox, o Edge Delivery Services é adicionado ao programa por padrão; não é necessário selecioná-lo.<br>Os programas de sandbox existentes antes da disponibilização geral do Edge Delivery herdarão Edge Delivery Services automaticamente. |

## Caminho recomendado de Adobe para clientes contratados {#recommended-path-eds}

Como cliente contratado, maximize seus benefícios do Adobe acessando e consumindo sua licença do Edge Delivery Services por meio da Cloud Manager. Essa abordagem permite usar a [CDN gerenciada por Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) e aproveitar os principais benefícios, como o gerenciamento de CDN de autoatendimento, incluindo a configuração e a adição de certificados DV. Além disso, após a criação de um certificado DV, o Adobe o renova automaticamente a cada três meses, a menos que ele seja excluído. Se você não tiver uma licença de Edge Delivery Services com o Adobe e decidir ignorar esses benefícios, poderá usar somente uma CDN gerenciada pelo cliente. Esta configuração deve estar na plataforma `aem.live`.

Se você tiver sido contratado com licenças do AEM as a Cloud Service Sites Edge Delivery Services, faça logon no Cloud Manager para garantir que você possa fazer o seguinte:

* Consuma sua licença no programa escolhido.
* Aproveite os benefícios da [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) para executar operações CRUD (Create, Read, Update, Delete).
<!-- REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+Self-service+access+to+Edge+Delivery+Services+and+Adobe+Managed+CDN * Access to license dashboard and reporting -->
* Acesse os relatórios do SLA (*em breve*) <!-- ADD LINK TO IT WHEN FINALLY ADDED -->
* Obtenha suporte para Adobe. Certifique-se de que seus sites de Edge Delivery Services estejam registrados por meio de um programa de Produção no Cloud Manager para o reconhecimento e suporte adequados do Adobe.


## Sobre a lista de tarefas do Edge Delivery {#ed-todo-list}

A **Lista de tarefas do Edge Delivery** é uma lista de verificação de tarefas de integração destinada a orientá-lo pela integração, gerenciando seu site do Edge Delivery até o [Início da atividade](/help/journey-onboarding/go-live-checklist.md).

![Lista de tarefas do site Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|  | Tarefa | Descrição |
| --- | --- | --- |
| 1 | Associe-se ao canal de colaboração de produtos | Clicar em **Enviar solicitação agora** envia uma solicitação ao Adobe para criar um canal para sua empresa. Se o canal já existir, você será encaminhado para o canal de sua empresa. |
| 2 | Concluir pré-requisitos | Clicar em **Exibir tutorial da Introdução** direciona você para o [Introdução - Tutorial do desenvolvedor](https://www.aem.live/developer/tutorial). |
| 3 | Adicionar site do Edge Delivery | Consulte [Adicionar um site do Edge Delivery](#eds-add-site). |
| 4 | Adicionar domínio | Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 5 | Adicionar certificado SSL | Consulte [Adicionar certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 6 | Configurar o CDN do site do Edge Delivery | Consulte [Adicionar uma configuração de CDN](#add-cdn). |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

<!--
Edge Delivery Services can be enabled when adding a new production program or editing an existing one.

![Add production program with Edge Delivery Services](assets/add-production-program-with-edge.png)

For more information about adding programs, see the following:

* [Create Production programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Create Sandbox programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) -->
