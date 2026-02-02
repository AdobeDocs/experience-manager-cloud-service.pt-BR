---
title: Assets Prime
description: Saiba mais sobre os principais aspectos do Assets Prime, como benefícios principais, tipos de usuários e seus privilégios.
feature: Asset Management
role: User, Admin
exl-id: 012f94c5-b1c3-4799-8eaf-af68d06c036f
source-git-commit: 504464ed1277c1d9629ae1f96892ebaa5ef701c8
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 1%

---

# as a Cloud Service Prime [!DNL Assets]  {#assets-prime}

![Imagem do banner do AEM Assets Prime](/help/assets/assets/aem-assets-prime-package-banner.png)

O Assets as a Cloud Service Prime inclui um DAM leve que permite executar vários recursos principais, como:

* **Serviços de gerenciamento de ativos e bibliotecas**&#x200B;: ferramentas que permitem aos usuários assimilar, armazenar, catalogar, controlar, gerenciar e controlar os ativos digitais de uma marca em um repositório centralizado

* **Pesquisa, Descoberta e Collaboration**: ferramentas que permitem aos usuários navegar, descobrir, compartilhar e colaborar em ativos necessários para criar experiências de cliente avançadas.

* **Segurança e Rights Management**: ferramentas para gerenciar acesso, permissões, direitos e segurança para garantir conformidade, consistência e integridade da marca.

* **Conexões do Creative Cloud**: ferramentas que permitem que as equipes de marketing e criação colaborem com acesso simplificado, comentários, revisões e anotações para atualizar ou finalizar ativos digitais.

* **Conexões do Experience Cloud**: ferramentas para dar suporte ao acesso nativo a ativos digitais de outros aplicativos e serviços da Experience Cloud.

* **Experiência do Portal de Distribuição sem opções de extensibilidade (Content Hub)**: ferramentas para expandir o acesso aos ativos digitais aprovados de uma marca para participantes estendidos, a fim de garantir a consistência da marca e o uso.

* **Integrações**: integrações com outros aplicativos Adobe e não Adobe.

* **Dynamic Media (complemento)**: ferramentas para transformar e entregar imagens, vídeos e outros conteúdos emergentes para experiências multimídia avançadas e interativas para qualquer dispositivo em escala.

  >[!NOTE]
  >
  >O Dynamic Media com recursos de OpenAPI, que fornecem acesso a modificadores básicos de imagem como girar, cortar (manual apenas - sem recorte inteligente), virar, altura, largura, qualidade, formato e transmissão de vídeo adaptável, também está disponível com o Assets Prime. Entre em contato com a equipe de conta da Adobe para saber mais.

No entanto, à medida que suas necessidades de DAM aumentam e você precisa de mais recursos, como extensibilidade da interface, automação orientada por API e implantação de código personalizado, você deve considerar a atualização para o [Assets Ultimate](/help/assets/assets-ultimate-overview.md).

Este artigo fornece um fluxo de trabalho completo para habilitar o Assets as a Cloud Service Prime.

## Ativar o Assets as a Cloud Service Prime{#enable-assets-prime}

Ative o Assets Prime ao criar um novo programa usando o Cloud Manager. Execute as seguintes etapas:

1. Como administrador do sistema, faça logon no Cloud Manager. Certifique-se de selecionar a organização correta ao fazer logon.

   >[!NOTE]
   >
   >Verifique se você foi adicionado ao perfil de produto apropriado do Cloud Manager para adicionar um novo programa. Para obter mais informações, consulte [Permissões baseadas em função no Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions).

1. [Criar um novo programa](/help/journey-onboarding/create-program.md).

   Ao criar o novo programa, na guia **[!UICONTROL Soluções e Complementos]**, selecione **[!UICONTROL Assets Prime]**. Você também pode expandir o **[!UICONTROL Assets Prime]** e selecionar o **[!UICONTROL Content Hub]** para habilitar o [Content Hub](/help/assets/product-overview.md) para distribuição de ativos.

   ![AEM Assets Ultimate](assets/aem-assets-prime.png)


1. Clique em **[!UICONTROL Criar]** para criar o programa.

1. Clique no cartão do programa e em **[!UICONTROL Adicionar ambiente]**.

1. Especifique o nome do ambiente, defina uma região e clique em **[!UICONTROL Salvar]** para criar o ambiente.

   ![Adicionar ambiente ao Assets Prime](assets/aem-assets-prime-add-environment.png)

>[!NOTE]
>
>O Assets Prime só permite criar um ambiente de produção. A opção para Adicionar ambiente não está mais disponível depois que o ambiente de produção é criado com sucesso.

O Assets Prime agora está ativado para o Experience Manager Assets as a Cloud Service.

![O AEM Assets Prime está disponível](assets/aem-assets-prime-setup-complete.png)

O administrador do sistema é automaticamente qualificado como administrador do AEM e recebe um email para navegar até o Admin Console e gerenciar perfis de produto.


A instância do AEM as a Cloud Service no Admin Console inclui os seguintes perfis de produto:

* Administradores do AEM

* Usuários do AEM

* [Usuários do AEM Assets Collaborator](#onboard-collaborator-users)

* [Usuários avançados do AEM Assets](#onboard-power-users)


![Perfis de produto do AEM Assets](assets/aem-assets-product-profiles.png)

Você pode começar a adicionar usuários ou grupos de usuários aos perfis de produtos Usuários do AEM Assets Collaborator e Usuários Avançados do AEM Assets. Para obter mais informações, consulte [Integrar usuários do AEM Assets Collaborator](#onboard-collaborator-users) e [Integrar usuários avançados do AEM Assets](#onboard-power-users).

Se você habilitou o Content Hub para o Assets as a Cloud Service, há uma nova instância criada no AEM Assets as a Cloud Service no Admin Console com `delivery` como sufixo:

![Nova instância para o Content Hub](assets/new-instance-content-hub.png)

>[!NOTE]
>
>Se você tiver provisionado o Content Hub antes de 14 de agosto de 2024, a nova instância será criada com `contenthub` como sufixo.

Observe que não há `author` ou `publish` no nome da instância do Content Hub.

Clique no nome da instância para exibir o perfil de produto do Content Hub `AEM Assets Limited Users`.

![Perfil de produto do Content Hub](assets/content-hub-product-profile.png)

Você pode começar a adicionar usuários ou grupos de usuários a esse perfil de produto para fornecer a eles acesso ao Content Hub.

>[!NOTE]
>
>Se você tiver provisionado o Content Hub antes de 14 de agosto de 2024, o perfil de produto do Content Hub terá `contenthub` mencionado depois de `Limited Users` em vez de `delivery`.

## Integrar usuários do AEM Assets Collaborator {#onboard-collaborator-users}

Os usuários do AEM Assets Collaborator podem trabalhar com ativos do Experience Manager por meio de integrações da Assets disponíveis para sua organização em outros produtos da Adobe e aplicativos que não sejam da Adobe, criar e editar ativos usando o Adobe Express e o Firefly integrados, aproveitando modelos, kits de marca, ativos da Adobe Stock e assim por diante projetados profissionalmente, e acessar e aproveitar ativos aprovados de sua organização usando o portal AEM Assets Content Hub.

Para integrar usuários do Collaborator:

1. Acesse os perfis de produto do Experience Manager Assets clicando no nome de produto do AEM as a Cloud Service na lista de produtos do Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

1. Clique no perfil de produto Usuários do Collaborators e clique em **[!UICONTROL Adicionar usuários]** para adicionar o usuário ao perfil de produto.
   ![Perfil de produto do usuário](assets/aem-assets-collaborator-user-permissions.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

Você também pode acessar e exibir os serviços atribuídos aos usuários do Collaborator, conforme mostrado na imagem a seguir:

![Serviços para usuários do Collaborator](assets/aem-assets-collaborator-users.png)

Os serviços `Adobe Express` e `AEM Assets Collaborator Users` estão habilitados por padrão. Você pode desativar e ativar o, de acordo com seus requisitos. No entanto, a Adobe recomenda usar os serviços padrão ativados para os perfis de produto.

## Integração de usuários avançados do AEM Assets {#onboard-power-users}

Os usuários avançados da AEM Assets podem acessar todos os recursos da AEM Assets, incluindo o gerenciamento de ativos, permissões, metadados e a governança e automação geral em torno de ativos digitais, trabalhar com ativos do Experience Manager por meio de integrações da Assets disponíveis para sua organização em outros aplicativos da Adobe e que não sejam da Adobe, criar e editar ativos usando o Adobe Express e o Firefly integrados, aproveitando modelos projetados profissionalmente, kits de marca, ativos da Adobe Stock e assim por diante, e acessar e aproveitar os ativos aprovados da sua organização usando o portal AEM Assets da Content Hub da.

Para integrar Usuários avançados:

1. Acesse os perfis de produto do Experience Manager Assets clicando no nome de produto do AEM as a Cloud Service na lista de produtos do Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

1. Clique no perfil de produto Usuários avançados e em **[!UICONTROL Adicionar usuários]** para adicionar o usuário ao perfil de produto.
   ![Perfil de produto do usuário](assets/aem-assets-power-user-permissions.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

Você também pode acessar e visualizar os serviços atribuídos aos usuários avançados, conforme ilustrado na imagem a seguir:

![Serviços para usuários avançados](assets/aem-assets-power-users.png)

Os serviços `Adobe Express` e `AEM Assets Power Users` estão habilitados por padrão. Você pode desativar e ativar o, de acordo com seus requisitos. No entanto, a Adobe recomenda usar os serviços padrão ativados para os perfis de produto.
