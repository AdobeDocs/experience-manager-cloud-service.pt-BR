---
title: Perguntas frequentes sobre o Dynamic Media com recursos OpenAPI
description: Perguntas frequentes sobre o Dynamic Media com recursos OpenAPI
role: User
exl-id: 3450e050-4b0b-4184-8e71-5e667d9ca721
source-git-commit: c3bac140c2e0b33cfc206cda7c0591fc75a47a1f
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# Perguntas frequentes sobre o Dynamic Media com recursos OpenAPI {#new-dynaminc-media-apis-frequently-asked-questions}

## Todos os ativos no repositório do Experience Manager Assets as a Cloud Service estão disponíveis para pesquisa e entrega usando o Dynamic Media com recursos OpenAPI? {#assets-available-for-search}

Não, apenas [as versões aprovadas e mais recentes dos ativos](/help/assets/approve-assets.md) estão disponíveis para pesquisa e entrega usando o Dynamic Media com recursos OpenAPI, garantindo a consistência da marca em todos os canais e aplicativos.


## Como os administradores podem marcar ativos novos e existentes adicionados a uma pasta como aprovados? {#add-assets-to-folder-as-approved}

O status de um ativo no Experience Manager Assets é regido pela propriedade `jcr:content/metadata/dam:status`. Os valores dessa propriedade podem ser:

* Aprovado

* Rejeitado

* Alterações solicitadas

O Experience Manager Assets distingue o status Aprovado usando um ícone de aprovado disponível no cartão de ativos, conforme representado nas imagens a seguir para as visualizações Administração e Ativo:

**Modo de exibição de administrador**

![Ativos aprovados no modo de exibição de Administrador](/help/assets/assets/approved-assets-thumbs-up.png)

**exibição do Assets**

![Ativos aprovados no modo de exibição do Assets](/help/assets/assets/approved-assets-thumbs-up-assets-view.png)


Para aprovar todos os ativos em uma pasta, consulte as instruções em [como aprovar ativos em massa em uma pasta](/help/assets/approve-assets.md#bulk-approve-assets). Há também um vídeo que mostra todo o processo.

Depois de configurar uma pasta para aprovação em massa, todos os novos ativos adicionados à pasta são aprovados automaticamente. Todos os ativos existentes são aprovados após o reprocessamento de ativos. Consulte [Reprocessando ativos digitais](/help/assets/reprocessing.md) para obter instruções sobre como reprocessar ativos. Se você copiar ou mover ativos não aprovados de qualquer outra pasta, será necessário [reprocessar os ativos](/help/assets/reprocessing.md).

O ativo é marcado como `Rejected`, se o administrador especificar `Rejected` ou `Changes requested` valores. O Experience Manager Assets distingue o status Rejeitado usando ![Rejeitar Assets](/help/assets/assets/do-not-localize/reject-assets.svg) disponível no cartão de ativos na exibição de Administrador.

Da mesma forma, o Experience Manager Assets distingue o status Rejeitado na exibição do Assets usando o seguinte status Rejeitado no cartão de ativos:

![Ativos rejeitados no modo de exibição Assets](/help/assets/assets/rejected-assets-admin-view.png)


## Como você pode fazer com que a ID de usuário ou de grupo do Adobe IMS (Adobe Identity Management Services) seja usada para definir as funções em ativos na exibição de administrador do Experience Manager, para proteger a experiência de entrega e pesquisa? {#set-roles-secure-delivery-search}

Os usuários que exigem acesso ao ambiente do Experience Manager Author são gerenciados como usuários do Adobe IMS no Admin Console da Adobe. Para obter informações sobre o que são os usuários do Adobe IMS e como eles são acessados e gerenciados no Admin Console, consulte [Usuários do Adobe IMS](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=pt-BR).


## É possível aprovar vários ativos simultaneamente em uma pasta? {#approve-multiple-assets-in-folder}

Sim, você pode aprovar vários ativos em uma pasta simultaneamente.

Execute as seguintes etapas para aprovar vários ativos simultaneamente no [!DNL Experience Manager Assets Admin view]:

1. Selecione o(s) ativo(s) e clique em **[!UICONTROL Propriedades]**.
1. Na guia **[!UICONTROL Básico]**, role para baixo até **[!UICONTROL Status de Revisão]**.
1. Alterar o status da revisão para **[!UICONTROL Aprovado]**.
1. Clique em **[!UICONTROL Salvar e fechar]**.

Da mesma forma, para aprovar vários ativos simultaneamente em uma pasta na exibição do Assets:

1. Selecione o(s) ativo(s) e clique em **[!UICONTROL Editar metadados em massa]**.

1. Selecione **[!UICONTROL Aprovado]** no campo **[!UICONTROL Status]**, disponível na seção [!UICONTROL Propriedades] do painel direito.

1. Clique em **[!UICONTROL Salvar]**.


## Como posso proteger a entrega de ativos e pesquisar o Dynamic Media com OpenAPIs? {#secure-asset-delivery}

A governança de ativos centrais no Experience Manager permite que os administradores do DAM ou gerentes de marca gerenciem o acesso aos ativos. Eles podem restringir o acesso definindo funções ou definindo o tempo de ativação e desativação para ativos aprovados no lado da criação, especificamente na instância de autor do AEM as a Cloud Service.

Os usuários finais que pesquisam ou utilizam URLs de entrega podem obter acesso a ativos restritos ao passar com êxito pelo processo de autorização.

Para obter mais informações, consulte [Restringir o acesso aos ativos no Experience Manager](restrict-assets-delivery.md#authoring).


## Como você pode obter permissões para editar o status de aprovação de um ativo? {#permissions-edit-approval-status}

Como usuário do DAM, talvez você não tenha permissões para [aprovar ativos](approve-assets.md#approve-assets). Para obter as permissões para editar o status de aprovação de um ativo, os administradores podem editar o esquema padrão ou qualquer outro esquema de metadados aplicado à pasta de ativos para fornecer permissões de edição ao campo **[!UICONTROL Status da revisão]**. Para obter mais informações, consulte [como desabilitar a edição para o campo Status de Revisão](approve-assets.md#configuration).


## Qual é o tamanho de arquivo suportado para vídeos? {#supported-file-formats-videos}

O Dynamic Media com recursos OpenAPI é compatível com vídeos de forma longa. Os vídeos podem suportar até 50 GB e 2 horas.


## Como o Dynamic Media com recursos OpenAPI é diferente da solução Dynamic Media? {#dynamic-media-and-dynamic-media-with-openapi-differences}

O Dynamic Media com recursos OpenAPI e Dynamic Media representam soluções distintas, cada uma oferecendo seus recursos de delivery especializados. É fundamental analisar minuciosamente seus requisitos específicos para determinar a solução mais adequada que se alinha às suas necessidades.

A orientação geral da Adobe é aproveitar o Dynamic Media com a pilha OpenAPI para qualquer caso de uso de integração (aplicativos próprios ou de terceiros). Se já existir uma integração com a pilha do Dynamic Media, a recomendação é não alterá-la, pois os URLs da pilha de OpenAPI são diferentes na estrutura. Somente para qualquer novo caso de uso de integração, use a pilha de OpenAPI. Se o caso de uso exigir modificadores avançados não disponíveis com a pilha de OpenAPI, evite a pilha de OpenAPI até que o Adobe preencha a lacuna. Mesmo para entrega nativa básica do AEM Assets Cloud Services, a pilha de OpenAPI pode ser avaliada, desde que seu caso de uso seja coberto pelos modificadores disponíveis com a pilha de OpenAPI. Concluindo, o Dynamic Media e o Dynamic Media com pilha de OpenAPI podem coexistir, dependendo da natureza do caso de uso.

Estas são algumas das principais diferenças entre o Dynamic Media com recursos OpenAPI e o Dynamic Media:

| Dynamic Media com recursos OpenAPI | Dynamic Media |
|---|---|
| [Disponível somente com o Assets as a Cloud Service](/help/assets/dynamic-media-open-apis-overview.md#prerequisites-dynaminc-media-open-apis) | Também disponível com On-premise ou Adobe Managed Services com etapas adicionais de configuração e provisionamento. |
| [Conjunto avançado de modificadores de imagem com suporte, como largura, altura, rotação, inversão, qualidade e formato](/help/assets/deliver-assets-apis.md) | Conjunto avançado de modificadores de imagem disponíveis |
| [Entrega de ativos restrita com base em usuários, funções, data e hora](/help/assets/restrict-assets-delivery.md) | O Assets publicado no Dynamic Media é acessível a todos os usuários |
| A maioria dos desenvolvedores está familiarizada com as especificações da OpenAPI. A extensibilidade do AEM Assets fica muito simples ao usar o [Seletor de ativos de micro front-end](/help/assets/overview-asset-selector.md). | APIs baseadas em SOAP, que se tornam uma barreira ao desenvolver personalizações de integração. |
| Quaisquer alterações feitas em ativos aprovados no DAM, incluindo atualizações de versão e modificações de metadados, são refletidas automaticamente nos URLs de entrega. Com um valor curto de TTL (Time-to-Live) de 10 minutos configurado para o Dynamic Media com recursos OpenAPI por meio do CDN, as atualizações ficam visíveis em todas as interfaces de criação e publicação em menos de 10 minutos. | TTL de CDN recomendado de 10 horas. Você pode substituir o valor TTL usando a ação de invalidação de cache. |
| Somente os ativos aprovados estão disponíveis para entrega de ativos em aplicativos downstream, permitindo ativos aprovados pela marca em experiências digitais. | As atualizações em um ativo publicado do Dynamic Media são publicadas automaticamente sem nenhum fluxo de trabalho de aprovação, o que não garante ativos aprovados pela marca em experiências digitais. |
| Relatórios de uso com base no número de ativos entregues. Esse recurso estará disponível em breve. | Os relatórios de uso não estão disponíveis. Esse recurso estará disponível em breve. |
| O Assets marcado como Expirado no repositório do Assets as a Cloud Service não está mais disponível para aplicativos downstream. | Nenhuma expiração de ativo inerente. Um ativo permanece público até ser excluído do repositório do AEM as a Cloud Service. |
| Não suporta recursos de recorte inteligente de vídeo. | Suporta recursos de recorte inteligente de vídeo. |
| Codificações de vídeo dinâmico, que garantem que as melhores codificações sejam fornecidas com base no vídeo de entrada. Nenhuma configuração é necessária para a entrega de vídeo nativo. | O padrão 3 codifica independentemente do vídeo de entrada (pode afetar o desempenho da entrega de vídeo). Você precisa configurar manualmente diferentes códigos para taxas de bits de vídeo diferentes. |
| Permite URLs protegidos e ofuscados usando UIDs de ativos sem comprometer o SEO. | Ofuscação de URL disponível apenas para parâmetros de consulta de URL. As Assets IDs (nomes de ativos) em URLs são reconhecíveis. |


## Como o Dynamic Media com recursos OpenAPI aborda as limitações do recurso Connected Assets? {#dynamic-media-openapi-addresses-connected-assets-limitations}

A tabela abaixo descreve as principais diferenças entre as duas soluções:

| Dynamic Media com recursos OpenAPI | Connected Assets |
|---|---|
| O Assets na implantação remota do DAM está disponível no AEM as a Cloud Service. | O Assets na implantação remota do DAM pode estar disponível no AEM as a Cloud Service ou no Adobe Managed Services. |
| Os binários de ativos não são copiados quando os ativos em uma implantação remota do DAM estão disponíveis em uma instância do AEM Sites. | Os binários de ativos são copiados quando os ativos em uma implantação remota do DAM estão disponíveis em uma instância do AEM Sites. |
| Suporte para todos os tipos de formato de ativos compatíveis com o AEM Assets. | Não há suporte para vídeos. |
| Você pode usar o Dynamic Media na implantação local do Sites enquanto busca ativos da implantação remota do DAM. | A implantação do Dynamic Media no Sites local é somente leitura. |
| Nenhuma restrição no número de instâncias do AEM Sites conectadas a uma implantação remota do DAM. Você pode [restringir o acesso a ativos na instância do Sites, configurando funções](/help/assets/restrict-assets-delivery.md) para ativos aprovados no DAM remoto. | Restrição para conectar não mais do que quatro instâncias do AEM Sites à implantação remota do DAM. O aumento do número requer testes adicionais. |
| O Seletor de ativos e o Dynamic Media com recursos OpenAPI são extensíveis para permitir integrações personalizadas. | As APIs do Assets conectadas não são extensíveis para permitir integrações personalizadas. |
| Quaisquer alterações feitas em ativos aprovados disponíveis na implantação remota do DAM, incluindo atualizações de versão e modificações de metadados, são refletidas automaticamente na instância do Sites em um valor curto de Tempo de vida (TTL) de 10 minutos. | As atualizações de ativos na implantação remota do DAM são tratadas por meio de eventos de ciclo de vida automaticamente, mas leva muito mais tempo do que o Dynamic Media com recursos OpenAPI. |
| Os metadados de ativos no DAM remoto também estão disponíveis na instância do AEM Sites. | Os metadados de ativos no DAM remoto não estão disponíveis na instância do AEM Sites. |

## Alguns modificadores são marcados como Disponibilidade Limitada. Como posso começar a usá-los? {#use-limited-availability-modifiers}

Para habilitar o uso de produção de [modificadores em Disponibilidade Limitada](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) na sua conta:

1. [Crie um caso de Suporte do Adobe usando o Admin Console](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).

1. Mencione os seguintes detalhes no caso de suporte da Adobe:

   * IMS Org

   * Lista de modificadores a serem ativados


## Como testar modificadores experimentais? {#modifiers-not-generally-available}

Você pode testar qualquer modificador, que geralmente não está disponível por meio de APIs experimentais. Por exemplo, &lt;/adobe/experimental/advancemodifiers-expires-YYYMMDD/assets>
Clique aqui para saber mais sobre como usar as [APIs experimentais](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/#experimental-apis) e a [lista completa de modificadores](https://developer.adobe.com/experience-cloud/experience-manager-apis/).
