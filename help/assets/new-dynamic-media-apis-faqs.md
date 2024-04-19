---
title: Perguntas frequentes sobre o Dynamic Media com recursos OpenAPI
description: Perguntas frequentes sobre o Dynamic Media com recursos OpenAPI
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# Perguntas frequentes sobre o Dynamic Media com recursos OpenAPI {#new-dynaminc-media-apis-frequently-asked-questions}

+++**Todos os ativos no repositório do Experience Manager Assets as a Cloud Service estão disponíveis para pesquisa e entrega usando o Dynamic Media com recursos OpenAPI?**

Não, apenas [aprovado e versão mais recente dos ativos](/help/assets/approved-assets.md) estão disponíveis para pesquisa e entrega usando o Dynamic Media com recursos OpenAPI, garantindo a consistência da marca em todos os canais e aplicativos.

+++

+++**Como os administradores podem marcar ativos novos e existentes adicionados a uma pasta como aprovados?**

O status de um ativo no Experience Manager Assets é regido por `jcr:content/metadata/dam:status` propriedade. Os valores dessa propriedade podem ser:

* Aprovado

* Rejeitado

* Alterações solicitadas

O Experience Manager Assets distingue o status Aprovado usando ![Aprovar ativos](assets/thumbs-up-icon.svg) disponível no cartão de ativos, conforme ilustrado na imagem a seguir:

![Ícone para ativos aprovados](/help/assets/assets/approved-assets-thumbs-up.png)

Para aprovar todos os ativos em uma pasta, consulte as instruções em [como aprovar ativos em massa em uma pasta](/help/assets/approved-assets.md#bulk-approve-assets). Há também um vídeo que mostra todo o processo.

Depois de configurar uma pasta para aprovação em massa, todos os novos ativos adicionados à pasta são aprovados automaticamente. Todos os ativos existentes são aprovados após o reprocessamento de ativos. Consulte [Reprocessamento de ativos digitais](/help/assets/reprocessing.md) para obter instruções sobre como reprocessar ativos. Se você copiar ou mover ativos não aprovados de qualquer outra pasta, será necessário [reprocessar os ativos](/help/assets/reprocessing.md).

O ativo está marcado como `Rejected`, se o administrador especificar `Rejected` ou `Changes requested` valores. O Experience Manager Assets distingue o status Rejeitado usando ![Rejeitar ativos](/help/assets/assets/do-not-localize/reject-assets.svg) disponível no cartão de ativos.

+++

+++**Como você pode fazer com que a ID de usuário ou grupo do Adobe IMS (Adobe Identity Management Services) seja usada para definir as funções em ativos no modo de exibição Experience Manager Admin para proteger a experiência de entrega e pesquisa?**

Os usuários que precisam de acesso ao ambiente de autor do Experience Manager são gerenciados como usuários do Adobe IMS no Adobe Admin Console. Para obter informações sobre o que são os usuários do Adobe IMS e como eles são acessados e gerenciados no Admin Console, consulte [Usuários do Adobe IMS](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en).

+++

+++**É possível aprovar vários ativos simultaneamente em uma pasta?**

Sim, você pode aprovar vários ativos em uma pasta simultaneamente.

Execute as seguintes etapas para aprovar vários ativos simultaneamente no [!DNL Experience Manager Assets]:

1. Selecione os ativos e clique em **[!UICONTROL Propriedades]**.
1. No **[!UICONTROL Básico]** , role para baixo até **[!UICONTROL Status da revisão]**.
1. Alterar o status da revisão para **[!UICONTROL Aprovado]**.
1. Clique em **[!UICONTROL Salvar e fechar]**.

+++

+++**Como posso proteger a entrega de ativos e pesquisar as Dynamic Media OpenAPIs?**

A governança de ativos centrais no Experience Manager permite que os administradores do DAM ou gerentes de marca gerenciem o acesso aos ativos. Eles podem restringir o acesso configurando funções para ativos aprovados no lado da criação, especificamente na instância de autor as a Cloud Service do AEM.

Os usuários finais que pesquisam ou utilizam URLs de entrega podem obter acesso a ativos restritos ao passar com êxito pelo processo de autorização.

Para obter mais informações, consulte [Restringir o acesso a ativos no Experience Manager](restrict-assets-delivery.md#authoring).

+++

+++**Como você pode obter permissões para editar o status de aprovação de um ativo?**

Como usuário do DAM, talvez você não tenha permissões para [aprovar ativos](approved-assets.md#approve-assets). Para obter as permissões para editar o status de aprovação de um ativo, os administradores podem editar o esquema de metadados padrão ou qualquer outro aplicado à pasta de ativos para fornecer permissões de edição ao **[!UICONTROL Status da revisão]** campo. Para obter mais informações, consulte [como desabilitar a edição para o Status de revisão](approved-assets.md#configuration) campo.

+++

+++**Quais são as diferenças entre o Dynamic Media com recursos OpenAPI e a solução da Dynamic Media?**

O Dynamic Media com recursos OpenAPI e o Dynamic Media representam soluções distintas, cada uma oferecendo seus recursos especializados de entrega. É fundamental analisar minuciosamente seus requisitos específicos para determinar a solução mais adequada que se alinha às suas necessidades.

Estas são algumas das principais diferenças entre o Dynamic Media com recursos OpenAPI e o Dynamic Media:

| Dynamic Media com recursos OpenAPI | Dynamic Media |
|---|---|
| [Disponível somente com Ativos as a Cloud Service](/help/assets/new-dynamic-media-overview.md#prerequisites-new-dynaminc-media-apis) | Também disponível com Managed Services no local ou Adobe com etapas adicionais de configuração e provisionamento. |
| [Conjunto limitado de modificadores de imagem compatíveis, como largura, altura, rotação, inversão, qualidade e formato](/help/assets/deliver-assets-apis.md) | Conjunto avançado de modificadores de imagem disponíveis |
| [Entrega de ativos restrita com base em usuários e funções](/help/assets/restrict-assets-delivery.md) | Os ativos publicados no Dynamic Media são acessíveis a todos os usuários |
| Suporta recorte inteligente de imagem | Oferece suporte a recorte inteligente de imagem e vídeo |
| Empilhe com base nas especificações da OpenAPI, com as quais a maioria dos desenvolvedores está familiarizada. A extensibilidade do AEM Assets fica muito simples ao usar [Seletor de ativos de front-end micro](/help/assets/asset-selector.md). | APIs baseadas em SOAP, que se tornam uma barreira ao desenvolver personalizações de integração. |
| Quaisquer alterações feitas em ativos aprovados no DAM, incluindo atualizações de versão e modificações de metadados, são refletidas automaticamente nos URLs de entrega. Com um valor curto de TTL (Time-to-Live) de 10 minutos configurado para o Dynamic Media com recursos OpenAPI via CDN, as atualizações ficam visíveis em todas as interfaces de criação e publicação em menos de 10 minutos. | TTL de CDN recomendado de 10 horas. Você pode substituir o valor TTL usando a ação de invalidação de cache. |
| Somente os ativos aprovados estão disponíveis para entrega de ativos em aplicativos downstream, permitindo ativos aprovados pela marca em experiências digitais. Os ativos entregues respeitam o status de expiração do ativo na instância do autor do repositório as a Cloud Service AEM. | As atualizações em um ativo publicado pela Dynamic Media são publicadas automaticamente sem nenhum fluxo de trabalho de aprovação, o que não garante ativos aprovados pela marca em experiências digitais. Nenhuma expiração de ativo inerente. Um ativo permanece público até ser excluído do repositório as a Cloud Service do AEM. |
| Relatórios de uso com base no número de ativos entregues. | Os relatórios de uso não estão disponíveis. |

+++

+++**Como o Dynamic Media com recursos OpenAPI lida com as limitações do recurso Connected Assets?**

A tabela abaixo descreve as principais diferenças entre as duas soluções:

| Dynamic Media com recursos OpenAPI | Connected Assets |
|---|---|
| Os ativos na implantação remota do DAM estão disponíveis no AEM as a Cloud Service. | Os ativos na implantação remota do DAM podem estar disponíveis no AEM as a Cloud Service ou no Adobe Managed Services. |
| Os binários de ativos não são copiados quando os ativos em uma implantação remota do DAM estão disponíveis em uma instância do AEM Sites. | Os binários de ativos são copiados quando os ativos em uma implantação remota do DAM estão disponíveis em uma instância do AEM Sites. |
| Suporte para todos os tipos de formato de ativos compatíveis com o AEM Assets. | Não há suporte para vídeos. |
| Suporta recorte inteligente de imagem. | Suporte para recortes inteligentes de imagens e predefinições de imagens do Dynamic Media. |
| Você pode usar o Dynamic Media na implantação local do Sites enquanto busca ativos da implantação remota do DAM. | A implantação do Dynamic Media no Sites local é somente leitura. |
| Nenhuma restrição no número de instâncias do AEM Sites conectadas a uma implantação remota do DAM. Você pode [restrinja o acesso a ativos na instância do Sites configurando funções](/help/assets/restrict-assets-delivery.md) para ativos aprovados no DAM remoto. | Restrição para conectar não mais do que quatro instâncias do AEM Sites à implantação remota do DAM. O aumento do número requer testes adicionais. |
| O Seletor de ativos e o Dynamic Media com recursos OpenAPI são extensíveis para permitir integrações personalizadas. | As APIs do Connected Assets não são extensíveis para permitir integrações personalizadas. |
| Quaisquer alterações feitas em ativos aprovados disponíveis na implantação remota do DAM, incluindo atualizações de versão e modificações de metadados, são refletidas automaticamente na instância do Sites em um valor curto de Tempo de vida (TTL) de 10 minutos. | As atualizações de ativos na implantação remota do DAM são tratadas por meio de eventos de ciclo de vida automaticamente, mas leva muito mais tempo do que o Dynamic Media com recursos OpenAPI. |
| Os metadados de ativos no DAM remoto também estão disponíveis na instância do AEM Sites. | Os metadados de ativos no DAM remoto não estão disponíveis na instância do AEM Sites. |

+++



