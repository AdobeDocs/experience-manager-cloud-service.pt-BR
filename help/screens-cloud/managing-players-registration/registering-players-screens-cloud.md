---
title: Registrando Players no Screens as a Cloud Service
description: Esta página descreve como registrar players no Screens as a Cloud Service.
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
source-git-commit: 489cc9963910ba9f94d30906127beb75f9ad37df
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

Depois de instalar seu reprodutor no Screens as a Cloud Service, você estará pronto para registrar seu reprodutor no Provedor de serviços do Screens.

Siga as etapas abaixo para registrar o player:

1. Faça logon no Provedor de serviços do Screens.

1. Navegar para **Códigos de registro** under **Gerenciamento de players** no painel de navegação esquerdo e clique em **Criar código**.

   >[!NOTE]
   >Se não existirem códigos válidos/não expirados, clique em criar código e insira um nome para o código e escolha as configurações de expiração de acordo com seus requisitos.

   ![imagem](/help/screens-cloud/assets/player/register-player1.png)

1. Preencha os seguintes campos em **Criar um código de registro** caixa de diálogo:

   ![imagem](/help/screens-cloud/assets/player/register-player2.png)

   1. **Nome do código de registro**: Nome do código de registro
   1. **Expiração do código de registro**: Prazo de validade do código de registro
   1. **Limitar uso**: Alterne o botão para desligar o limite de uso do código de registro. Por padrão, a opção Limitar uso está desativada por padrão.
   1. **Limite de uso**: Escolha o número do limite de uso

1. Clique em **Criar** para criar o código de registro. Você verá o player com o código de registro na lista.

   ![imagem](/help/screens-cloud/assets/player/register-player3.png)

1. Click on the value under the column **REGISTRATION CODE**  to copy the value to the clipboard.

1. Cole esse valor na **Inserir código** no campo **Registro do reprodutor** na interface do usuário do administrador do reprodutor do AEM Screens e clique em **Registrar**.

   ![imagem](/help/screens-cloud/assets/player/register-player4.png)


1. Após adicionar o código, você verá que o reprodutor agora está registrado na interface do usuário do administrador do reprodutor.

   ![imagem](/help/screens-cloud/assets/player/register-player5.png)

1. Você deve ver esse reprodutor aparecer no **Players** no painel de navegação esquerdo. O código exibido no Provedor de serviços do Screens corresponde ao **Informações do sistema** na interface do usuário do administrador, em Código do player.

   ![imagem](/help/screens-cloud/assets/player/register-player6.png)

>[!IMPORTANT]
>**Recomendação de práticas recomendadas de segurança ao usar o código de registro
>Como prática recomendada, é possível limitar o uso do código de registro. Se um código de registro estiver comprometido, mas tiver um limite de 100 registros, o invasor poderá se registrar apenas até esse número, mas não mais. Você sempre pode atualizar o limite de uso depois que o código de registro é criado e alguns dos players do cliente já foram registrados. If the customer observes unusual registration activity for a specific registration code, they can lower the limit in real-time while they investigate and can increase the number back if it was a false alarm, without impacting the already registered players.


## O que vem a seguir {#whats-next}

Now, that you have installed and configured the player to Cloud mode, you should continue your Screens as a Cloud Service journey by next reviewing the document, [Assigning Player to a Display in Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) from Screens Services Provider.
