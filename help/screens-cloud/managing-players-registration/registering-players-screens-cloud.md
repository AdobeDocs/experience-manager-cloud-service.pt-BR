---
title: Registrando Players no Screens as a Cloud Service
description: This page describes how to register players in Screens as a Cloud Service.
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
source-git-commit: fb82970154fa37e3b3d1591a2e25989853ec6b90
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# Registrando Players no Screens as a Cloud Service {#registering-players-screens-cloud}

Depois de instalar e configurar reprodutores para o Screens as a Cloud Service, você deve registrar os players.

## Objetivo {#objective}

Este documento ajuda você a entender o registro de players no Provedor de serviços do Screens. Após a leitura, você deve ser capaz de:

* entender como registrar jogadores
* como concluir o processo de registro do Provedor de serviços do Screens

## Etapas para registrar um player do Screens {#register-players}

Once you have installed your player to Screens as a Cloud Service, you are ready to register your player from Screens Services Provider.

Siga as etapas abaixo para registrar o player:

1. Faça logon no Provedor de serviços do Screens.

1. Navegar para **Códigos de registro** under **Gerenciamento de players** no painel de navegação esquerdo e clique em **Criar código**.

   >[!NOTE]
   >Se não existirem códigos válidos/não expirados, clique em criar código e insira um nome para o código e escolha as configurações de expiração de acordo com seus requisitos.

   ![imagem](/help/screens-cloud/assets/player/register-player1.png)

1. Preencha os seguintes campos em **Criar um código de registro** caixa de diálogo:

   ![imagem](/help/screens-cloud/assets/player/register-player2.png)

   1. **Registration Code Name**: Name for your registration code
   1. **Registration Code Expiry**: Date of expiry for your registration code
   1. **Limit Usage**: Toggle the button to switch off the usage limit of your registration code. By default, the Limit Usage option is off by default.
   1. **Limite de uso**: Escolha o número do limite de uso

1. Clique em **Criar** para criar o código de registro. Você verá o player com o código de registro na lista.

   ![imagem](/help/screens-cloud/assets/player/register-player3.png)

1. Clique no valor sob a coluna **CÓDIGO DE REGISTRO**  para copiar o valor para a área de transferência.

1. Cole esse valor na **Inserir código** no campo **Registro do reprodutor** na interface do usuário do administrador do reprodutor do AEM Screens e clique em **Registrar**.

   ![imagem](/help/screens-cloud/assets/player/register-player4.png)


1. Após adicionar o código, você verá que o reprodutor agora está registrado na interface do usuário do administrador do reprodutor.

   ![imagem](/help/screens-cloud/assets/player/register-player5.png)

1. Você deve ver esse reprodutor aparecer no **Players** no painel de navegação esquerdo. The code that displays in Screens Services Provider matches the **System Information** panel from the Admin UI under Player Code.

   ![imagem](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**Security Best Practices Recommendation while using Registration Code**
   >As a best practice, you can limit the registration code usage. Se um código de registro estiver comprometido, mas tiver um limite de 100 registros, o invasor poderá se registrar apenas até esse número, mas não mais. Você sempre pode atualizar o limite de uso depois que o código de registro é criado e alguns dos players do cliente já foram registrados. Se o cliente observar uma atividade de registro incomum para um código de registro específico, ele poderá reduzir o limite em tempo real enquanto investiga e aumentar o número novamente se for um alarme falso, sem afetar os players já registrados.


## O que vem a seguir {#whats-next}

Agora que você instalou e configurou o reprodutor para o modo Nuvem, deve continuar sua jornada as a Cloud Service do Screens ao próxima revisar o documento, [Atribuição do reprodutor a uma exibição no Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) do Provedor de serviços do Screens.
