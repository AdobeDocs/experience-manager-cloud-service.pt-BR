---
title: Conceder acesso ao desenvolvedor front-end
description: Integram os desenvolvedores de front-end no Cloud Manager para que eles tenham acesso ao repositório e pipeline de Git do site de AEM.
source-git-commit: 5e1a89743c5ac36635a139ada690849507813c30
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---


# Conceder acesso ao desenvolvedor front-end {#grant-fed-access}

Integram os desenvolvedores de front-end no Cloud Manager para que eles tenham acesso ao repositório e pipeline de Git do site de AEM.

## A História Até Agora {#story-so-far}

No documento anterior da jornada de Criação AEM de Site Rápido, [Configurar o pipeline,](pipeline-setup.md) você aprendeu a criar um pipeline front-end para gerenciar a personalização do tema do seu site e agora deve:

* Entenda o que é um pipeline front-end.
* Saiba como configurar um pipeline de front-end no Cloud Manager.

Agora é necessário conceder acesso de desenvolvedor de front-end ao Cloud Manager por meio do processo de integração para que o desenvolvedor de front-end possa acessar o repositório Git de AEM e o pipeline criado.

## Objetivo {#objective}

O processo de conceder acesso ao Cloud Manager e atribuir funções de usuário aos usuários é chamado de integração. Este documento fornecerá uma visão geral das etapas mais importantes para a integração de um desenvolvedor front-end e, após a leitura, você saberá:

* Como adicionar um desenvolvedor de front-end como usuário.
* Como conceder as funções necessárias ao desenvolvedor de front-end.

>[!TIP]
>
>Há uma jornada de documentação inteira dedicada à integração de sua equipe ao AEM as a Cloud Service, vinculada ao [Seção Recursos adicionais](#additional-resources) deste documento, se precisar de detalhes adicionais sobre o processo.

## Função responsável {#responsible-role}

Essa parte da jornada se aplica ao administrador do Cloud Manager.

## Requisitos {#requirements}

* Você precisa ser membro de **Proprietário da empresa** no Cloud Manager.
* Você precisa ser um **Administrador de Sys** no Cloud Manager.
* Você precisa ter acesso ao Admin Console.

## Adicionar o desenvolvedor de front-end como usuário {#add-fed-user}

Primeiro, é necessário adicionar o desenvolvedor de front-end como usuário usando o Admin Console.

1. Entrar no Admin Console [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).

1. Depois de fazer logon, você verá uma página de visão geral semelhante à imagem a seguir.

   ![Visão geral do Admin Console](assets/admin-console.png)

1. Certifique-se de estar na organização apropriada, marcando o nome da organização no canto superior direito da tela.

   ![Verificar nome da organização](assets/correct-org.png)

1. Selecionar **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

   ![Selecione AEMaaCS](assets/select-aemaacs.png)

1. Você verá a lista de perfis de produto pré-configurados do Cloud Manager. Caso não veja esses perfis, entre em contato com o administrador do Cloud Manager, pois talvez você não tenha as permissões corretas em sua organização.

   ![Perfis de produto](assets/product-profiles.png)

1. Para atribuir o desenvolvedor de front-end aos perfis corretos, toque ou clique no botão **Usuários** e depois a guia **Adicionar usuário** botão.

   ![Adicionar usuário](assets/add-user.png)

1. No **Adicionar usuários à equipe** digite a ID de email do usuário que deseja adicionar. Para o Tipo de ID, selecione Adobe ID, se o Federated ID para os membros da equipe ainda não tiver sido configurado.

   ![Adicionar usuário à equipe](assets/add-to-team.png)

1. No **Produto** , toque ou clique no sinal de mais e selecione **Adobe Experience Manager as a Cloud Service** e atribua o **Gerenciador de implantação** e **Desenvolvedor** perfis de produto para o usuário.

   ![Atribuir perfis de equipe](assets/assign-team.png)

1. Toque ou clique **Salvar** e um email de boas-vindas é enviado ao desenvolvedor front-end que você adicionou como usuário.

O desenvolvedor front-end convidado pode acessar o Cloud Manager clicando no link do email de boas-vindas e fazendo logon usando sua Adobe ID.

## Transmissão para desenvolvedor front-end {#handover}

Com um convite feito por email para o Cloud Manager a caminho do desenvolvedor de front-end, você e o administrador de AEM agora podem fornecer ao desenvolvedor de front-end as informações necessárias restantes para iniciar a personalização.

* A [caminho para o conteúdo típico](#example-page)
* A fonte do tema que [você baixou](#download-theme)
* O [credenciais do usuário proxy](#proxy-user)
* O nome do programa ou o URL para ele [copiado do Cloud Manager](pipeline-setup.md#login)
* Requisitos de concepção de front-end

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de Criação de Site Rápido de AEM você deve saber:

* Como adicionar um desenvolvedor de front-end como usuário.
* Como conceder as funções necessárias ao desenvolvedor de front-end.

Crie com base nesse conhecimento e prossiga sua jornada de Criação de Site Rápido de AEM revisando o documento [Recuperar informações de acesso do repositório Git,](retrieve-access.md) que alterna a perspectiva exclusivamente para o desenvolvedor de front-end e explica como os usuários de desenvolvedor de front-end do Cloud Manager acessam as informações do repositório de git.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de Criação Rápida de Site revisando o documento [Recuperar credenciais do desenvolvedor front-end,](retrieve-access.md) a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada.

* [Jornada de integração](/help/journey-onboarding/home.md) - Este guia serve como ponto de partida para garantir que suas equipes estejam configuradas e tenham acesso a AEM as a Cloud Service.


