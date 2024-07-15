---
title: Registro de players no Screens as a Cloud Service
description: Esta página descreve como registrar players no Screens as a Cloud Service.
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# Registro de players no Screens as a Cloud Service {#registering-players-screens-cloud}

Depois de instalar e configurar reprodutores para o Screens as a Cloud Service, você deve registrá-los.

## Objetivo {#objective}

Este documento ajuda você a entender o registro de players no Screens Services Provider. Depois de ler, você deverá ser capaz de:

* entender como registrar players
* como concluir o processo de registro do Provedor de Serviços Screens

## Etapas para registrar um reprodutor do Screens {#register-players}

Depois de instalar o reprodutor no Screens as a Cloud Service, você estará pronto para registrá-lo no Provedor de serviços da Screens.

Siga as etapas abaixo para registrar seu reprodutor:

1. Faça logon no Provedor de Serviços Screens.

1. Navegue até **Códigos de registro** em **Gerenciamento de players** no painel de navegação esquerdo e clique em **Criar código**.

   >[!NOTE]
   >Se não houver códigos válidos/não expirados, clique em criar código, insira um nome para o código e escolha as configurações de expiração de acordo com seus requisitos.

   ![imagem](/help/screens-cloud/assets/player/register-player1.png)

1. Preencha os seguintes campos na caixa de diálogo **Criar um código de registro**:

   ![imagem](/help/screens-cloud/assets/player/register-player2.png)

   1. **Nome do Código de Registro**: Nome para seu código de registro
   1. **Expiração do código de registro**: data de expiração do código de registro
   1. **Limitar Uso**: Ative o botão para desativar o limite de uso do seu código de registro. Por padrão, a opção Limitar uso está desativada.
   1. **Limite de uso**: escolha o número para seu limite de uso

1. Clique em **Criar** para criar o código de registro. Você pode ver seu reprodutor com o código de registro na lista.

   ![imagem](/help/screens-cloud/assets/player/register-player3.png)

1. Clique no valor na coluna **CÓDIGO DE REGISTRO** para copiar o valor para a área de transferência.

1. Cole esse valor no campo **Inserir código** da guia **Registro do player** da interface do Administrador do reprodutor do AEM Screens e clique em **Registrar**.

   ![imagem](/help/screens-cloud/assets/player/register-player4.png)


1. Ao adicionar o código, você pode ver que o reprodutor agora está registrado na interface do usuário de administração do reprodutor.

   ![imagem](/help/screens-cloud/assets/player/register-player5.png)

1. Você deve ver este player agora em **Players** no painel de navegação esquerdo. O código exibido no Provedor de Serviços Screens corresponde ao painel **Informações do Sistema** da interface do usuário do Administrador em Código do player.

   ![imagem](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**Recomendação de práticas recomendadas de segurança ao usar o código de registro**
   >Como prática recomendada, você pode limitar o uso do código de registro. Se um código de registro for comprometido, mas tiver um limite de 100 registros, o invasor poderá registrar somente até esse número, mas não mais. Você sempre pode atualizar o limite de uso depois que o código de registro for criado e alguns dos players do cliente já tiverem sido registrados. Se o cliente observar uma atividade de registro incomum para um código de registro específico, ele poderá reduzir o limite em tempo real enquanto investiga e poderá aumentar o número de volta se for um alarme falso, sem afetar os players já registrados.


## O que vem a seguir {#whats-next}

Agora que você instalou e configurou o reprodutor no modo Nuvem, continue sua jornada do Screens as a Cloud Service revisando o documento, [Atribuindo o reprodutor a uma exibição no Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) do Provedor de Serviços Screens.
