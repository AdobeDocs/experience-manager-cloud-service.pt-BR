---
title: Registro de players no Screens as a Cloud Service
description: Esta página descreve como registrar players no Screens as a Cloud Service.
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Registro de players no Screens as a Cloud Service {#registering-players-screens-cloud}

Depois de instalar e configurar reprodutores para o Screens as a Cloud Service, você deve registrar os reprodutores.

## Objetivo {#objective}

Este documento ajuda você a entender o registro de players no provedor de serviços do Screens. Depois de ler, você deverá ser capaz de:

* entender como registrar players
* como concluir o processo de registro do provedor de serviços Screens

## Etapas para registrar um reprodutor do Screens {#register-players}

Depois de instalar o reprodutor no Screens as a Cloud Service, você estará pronto para registrá-lo no provedor de serviços do Screens.

Siga as etapas abaixo para registrar seu reprodutor:

1. Faça logon no provedor de serviços do Screens.

1. Navegue até **Códigos de registro** em **Gerenciamento de players** no painel de navegação esquerdo e clique em **Criar código**.

   >[!NOTE]
   >Se não houver códigos válidos/não expirados, clique em criar código, insira um nome para o código e escolha as configurações de expiração de acordo com seus requisitos.

   ![imagem](/help/screens-cloud/assets/player/register-player1.png)

1. Preencha os seguintes campos em **Criar um código de registro** caixa de diálogo:

   ![imagem](/help/screens-cloud/assets/player/register-player2.png)

   1. **Nome do código de registro**: Nome do código de registro
   1. **Expiração do código de registro**: Data de expiração do código de registro
   1. **Limitar uso**: Alterne o botão para desativar o limite de uso do código de registro. Por padrão, a opção Limitar uso está desativada.
   1. **Limite de uso**: escolha o número para o seu limite de uso

1. Clique em **Criar** para criar o código de registro. Você pode ver seu reprodutor com o código de registro na lista.

   ![imagem](/help/screens-cloud/assets/player/register-player3.png)

1. Clique no valor abaixo da coluna **CÓDIGO DE REGISTRO**  para copiar o valor para a área de transferência.

1. Cole esse valor no **Inserir código** no campo **Registro do reprodutor** na interface de usuário do Administrador do reprodutor do AEM Screens e clique em **Registrar**.

   ![imagem](/help/screens-cloud/assets/player/register-player4.png)


1. Ao adicionar o código, você pode ver que o reprodutor agora está registrado na interface do usuário de administração do reprodutor.

   ![imagem](/help/screens-cloud/assets/player/register-player5.png)

1. Você deve ver este player agora aparecer em **Reprodutores** no painel de navegação esquerdo. O código exibido no Provedor de serviços do Screens corresponde ao **Informações do sistema** da interface do Administrador em Código do player.

   ![imagem](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**Recomendação de práticas recomendadas de segurança ao usar o código de registro**
   >Como prática recomendada, você pode limitar o uso do código de registro. Se um código de registro for comprometido, mas tiver um limite de 100 registros, o invasor poderá registrar somente até esse número, mas não mais. Você sempre pode atualizar o limite de uso depois que o código de registro for criado e alguns dos players do cliente já tiverem sido registrados. Se o cliente observar uma atividade de registro incomum para um código de registro específico, ele poderá reduzir o limite em tempo real enquanto investiga e poderá aumentar o número de volta se for um alarme falso, sem afetar os players já registrados.


## O que vem a seguir {#whats-next}

Agora que você instalou e configurou o reprodutor no modo Nuvem, continue sua jornada as a Cloud Service do Screens revisando o documento em seguida, [Atribuição do reprodutor a uma exibição no Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) do provedor de serviços Screens.
