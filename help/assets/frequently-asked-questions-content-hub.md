---
title: Perguntas frequentes sobre o Content Hub
description: Obtenha respostas para algumas das perguntas mais frequentes do Content Hub.
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 0%

---

# Perguntas frequentes sobre o Content Hub {#content-hub-frequently-asked-questions}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Perguntas frequentes sobre a Content Hub](assets/content-hub-faqs.png)

>[!AVAILABILITY]
>
>O guia do Content Hub agora está disponível no formato PDF. Baixe o guia inteiro e use o Assistente de IA da Adobe Acrobat para responder às suas consultas.
>
>[!BADGE PDF do Guia do Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

## O que é o Content Hub? {#what-is-content-hub}

O Content Hub é um recurso do Adobe Experience Manager Assets as a Cloud Service.

O Content Hub permite que equipes maiores descubram facilmente ativos relevantes e aprovados por meio de um portal intuitivo e os adaptem rapidamente às suas necessidades.  Além disso, o Content Hub fornece um mecanismo de assimilação que permite que esses usuários realizem autoatendimento facilmente à medida que fazem upload de ativos para o DAM. Isso atende diretamente à necessidade que as organizações têm de maior velocidade de criação de conteúdo, preservando a consistência da marca e a conformidade com as salvaguardas apropriadas.

## Por que não posso ativar o Content Hub no meu programa/ambiente do Cloud Manager? {#cannot-enable-content-hub}

No momento, o Content Hub está disponível apenas nos programas de produção da AEM Cloud Manager, que incluem uma licença da Assets. Quando você clica em [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) para habilitá-lo, ele é implantado e associado ao ambiente de produção do AEM do autor nesse programa. Consulte [Implantar o Content Hub](/help/assets/deploy-content-hub.md) para obter detalhes e pré-requisitos.

Há um programa de acesso antecipado ao Content Hub em programas de sandbox/ambientes de produção de autores. Para obter mais informações, consulte [Introdução aos programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Para saber mais sobre o programa de acesso antecipado, entre em contato com a equipe de conta do Adobe.

O Content Hub não está disponível para ambientes não relacionados à produção (preparo, desenvolvimento e assim por diante) no momento.

## Eu ativei o Content Hub em meu programa/ambiente de produção. É possível desativá-lo? {#can-i-disable-content-hub}

Habilitar o Content Hub em um programa de produção o implanta como parte da infraestrutura de produção. A AEM Cloud Manager não permite remover ou desativar a infraestrutura de produção para minimizar o risco de uso da produção por erros humanos.

Se não quiser fornecer o Content Hub aos usuários após a implantação, não atribua nenhum usuário ao perfil de produto do Content Hub no Admin Console. Consulte [Implantar Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile) para obter detalhes.

## Como posso avaliar o Content Hub em minha organização, pois ele só está disponível para programas de produção/ambientes de criação de produção? {#how-can-i-evaluate-content-hub}

O Content Hub é um recurso que o Adobe fornece e mantém, e não tem nenhum código personalizado que exija validação típica via desenvolvimento/preparo/produção. Além disso, o acesso ao recurso para usuários é totalmente controlado pelo administrador, para que você possa avaliá-lo sem expô-lo a todos os usuários.

É possível avaliar o Content Hub sem afetar os usuários/conteúdos de produção gerenciados no AEM as a Cloud Service Assets. Um procedimento de avaliação pode ser semelhante a:

* [Habilitar o Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) no ambiente de produção (programa Cloud Manager)
* [Adicionar um usuário Administrador de AEM](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator) do autor de produção ao perfil de produto do Content Hub.
* O Administrador do AEM [configura o Content Hub](/help/assets/configure-content-hub-ui-options.md)
* O Administrador do AEM ou um Usuário do AEM no autor de produção do AEM [aprova vários ativos para o Content Hub](/help/assets/approve-assets-content-hub.md); se você não quiser alterar nenhum conteúdo de produção no DAM, poderá criar uma pasta de avaliação separada na instância do autor do AEM e carregar/marcar ou copiar alguns ativos do DAM para ela.
* O administrador do Admin Console adiciona [alguns usuários selecionados](/help/assets/deploy-content-hub.md#onboard-content-hub-users) ao perfil de produto do Content Hub, para que eles possam iniciar a avaliação.
* Após a conclusão da avaliação, os usuários do AEM na instância do autor podem remover a aprovação de ativos de teste, aprovar ativos de produção para o Content Hub e, em seguida, o administrador de Admin Console pode adicionar todos os usuários que precisam de acesso ao Content Hub e conteúdo aprovado. Parabéns, seu Content Hub está disponível agora.

O Adobe também oferece um programa de acesso antecipado ao Content Hub em ambientes de preparo - consulte a pergunta [Por que não posso habilitar o Content Hub no meu programa/ambiente do Cloud Manager?](#cannot-enable-content-hub) para obter detalhes.

## Por que não vejo nenhum ativo depois de fazer logon no Content Hub? {#no-assets-in-content-hub}

Os ativos marcados como aprovados no Assets as a Cloud Service são automaticamente disponibilizados no Content Hub. Se não conseguir ver nenhum ativo depois de fazer logon no Content Hub, aprove os ativos usando o ambiente de criação do AEM as a Cloud Service para disponibilizá-los no Content Hub. Para obter mais informações, consulte [Aprovar ativos para o Content Hub](/help/assets/approve-assets-content-hub.md).

## Por que não vejo meus ativos que carrego diretamente usando o Content Hub ou os importo de contas do Dropbox ou do OneDrive usando o Content Hub? {#no-assets-uploaded-from-content-hub}

A exibição de ativos carregados com o Content Hub depende de se você habilitou a opção [Aprovação automática](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub), disponível na interface do usuário de Configuração:

* Se a opção **Aprovação automática** estiver habilitada, os ativos carregados usando o Content Hub estarão automaticamente disponíveis.

* Se a opção **Aprovação automática** estiver desabilitada, os ativos carregados usando o Content Hub não serão exibidos automaticamente. Os ativos estão disponíveis na pasta `hydrated-assets` do seu ambiente as a Cloud Service do Assets. Navegue até a pasta e [edite em massa](/help/assets/approve-assets-content-hub.md) o status desses ativos para `Approved` para que eles sejam exibidos no Content Hub.

## Como localizar rapidamente ativos carregados usando o Content Hub no ambiente do AEM as a Cloud Service? {#find-uploaded-assets-on-aem-cloud}

Você pode encontrar rapidamente ativos carregados usando o Content Hub no ambiente do AEM as a Cloud Service ao:

1. Navegando até a pasta `hydrated-assets`.

1. Clicando em **[!UICONTROL Filtros]** e definindo **[!UICONTROL Sem status]** no campo **[!UICONTROL Status do ativo]**.

1. Classificando ativos usando o campo **[!UICONTROL Data de modificação]**.

## Por que não exibo a opção editar usando o Adobe Express no meu cartão de ativos para poder remixar ativos e criar novas variações? {#edit-using-express-not-available}

Para exibir a edição usando a opção Adobe Express no cartão de ativos, você deve ter direitos de Adobe Express além de privilégios para [usuários do Content Hub com direitos de remixar ativos para novas variações](#onboard-content-hub-users-add-assets). O Adobe Express deve ser implantado na mesma organização no Admin Console do Adobe em que o Adobe Experience Manager é implantado.

## Posso configurar o Content Hub para que as diretrizes de marca da minha organização sejam exibidas como um link na página inicial? {#content-hub-setup-brand-guidelines}

É possível adicionar links personalizados como guias separadas, além das guias padrão Todos os Assets, Coleções e Insights na página inicial do Content Hub. Para obter informações sobre como configurá-lo, consulte [Links Personalizados](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub).

## Há algum plano para migrar os clientes existentes do Brand Portal para o Content Hub? {#migration-brand-portal}

O Adobe oferece suporte à migração do Brand Portal para o Content Hub, que pode ser usado ao criar um tíquete de suporte ao Adobe.

## Por que não consigo ver a opção Configurações/configurações do produto no Content Hub? {#ui-configuration-option-missing}

Para acessar a [Interface do Usuário de Configuração](/help/assets/configure-content-hub-ui-options.md), você precisa ser um [Administrador do Content Hub](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator). Se você estiver atribuído ao perfil de produto Administradores do AEM na instância do autor de produção no Adobe Admin Console e ainda não conseguir ver a opção de configuração, verifique se o perfil de produto Administradores do AEM não é renomeado. Consulte [Perfis de produto e de equipe do AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) para obter mais detalhes.
