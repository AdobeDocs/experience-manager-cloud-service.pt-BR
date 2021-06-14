---
title: Registrar players no Screens como um Cloud Service
description: Esta página descreve como registrar players no Screens como um Cloud Service.
hide: true
hidefromtoc: true
index: false
source-git-commit: c65eeaf74ddfd81d37eb7090b84c8bf6f876dc72
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---


# Registrando players no Screens como um Cloud Service {#registering-players-screens-cloud}

Depois de instalar e configurar players para o Screens como um Cloud Service, você deve registrar os players.

## Objetivo {#objective}

Este documento ajuda você a entender o registro de players no Provedor de serviços do Screens. Depois de ler, você deve:

* Entenda como registrar jogadores.
* Gerencie seus canais em um projeto do AEM Screens, em termos de escopo.

## Etapas para registrar um reprodutor do Screens {#register-players}

Depois de instalar seu player no Screens como um Cloud Service, você estará pronto para registrar seu player no Provedor de serviços do Screens.

Siga as etapas abaixo para registrar o player:

1. Faça logon no Provedor de serviços do Screens.

1. Navegue até **Códigos de Registro** em **Gerenciamento de Players** no painel de navegação esquerdo e clique em **Criar código**.

   >[!NOTE]
   >Se não existirem códigos válidos/não expirados, clique em criar código e insira um nome para o código e escolha as configurações de expiração de acordo com seus requisitos.

   ![imagem](/help/screens-cloud/assets/player/register-player1.png)

1. Preencha os seguintes campos na caixa de diálogo **Criar um código de registro**:

   ![imagem](/help/screens-cloud/assets/player/register-player2.png)

   1. **Nome** do código de registro: Nome do código de registro
   1. **Expiração** do código de registro: Prazo de validade do código de registro
   1. **Limitar uso**: Alterne o botão para desligar o limite de uso do código de registro. Por padrão, a opção Limitar uso está desativada por padrão.
   1. **Limite** de uso: Escolha o número do limite de uso

1. Clique em **Create** para criar o código de registro. Você verá o player com o código de registro na lista.

   ![imagem](/help/screens-cloud/assets/player/register-player3.png)

1. Clique no valor na coluna **REGISTRATION CODE** para copiar o valor para a área de transferência.

1. Cole esse valor no campo **Enter code** na guia **Player Registration** da interface de usuário do administrador do reprodutor do AEM Screens e clique em **Register**.

   ![imagem](/help/screens-cloud/assets/player/register-player4.png)


1. Após adicionar o código, você verá que o reprodutor agora está registrado na interface do usuário do administrador do reprodutor.

   ![imagem](/help/screens-cloud/assets/player/register-player5.png)

1. Esse reprodutor deve ser exibido em **Players** no painel de navegação esquerdo. O código exibido no Provedor de serviços do Screens corresponde ao painel **Informações do sistema** da interface do usuário do administrador, em Código do player.

   ![imagem](/help/screens-cloud/assets/player/register-player6.png)

