---
title: Gerenciar nomes de domínio personalizados
description: Saiba como usar o Cloud Manager para exibir, atualizar, substituir e excluir nomes de domínio personalizados.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4e887b753eaf09e104c68484792f00dcb08ee304
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 54%

---


# Gerenciar nomes de domínio personalizados {#managing-custom-domain-names}

O Cloud Manager permite exibir, atualizar, substituir e excluir nomes de domínio personalizados.

## Exibir e atualizar um nome de domínio personalizado {#view-and-update}

Use o menu **Exibir e atualizar** para exibir os detalhes de qualquer um dos nomes de domínio personalizados.

**Para exibir e atualizar um nome de domínio personalizado:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Identifique a linha do nome de domínio personalizado que deseja exibir ou atualizar.

1. Clique no botão de reticências localizado na extremidade direita da linha.

1. Selecione a opção **Exibir e atualizar**.

## Atualizar um certificado SSL de nome de domínio personalizado {#update-cert}

Você pode seguir [as mesmas etapas para exibir e atualizar um nome de domínio personalizado](#view-and-update) para atualizar um certificado SSL.

>[!NOTE]
>
>O certificado SSL deve ser válido, [já configurado](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md), e conter o nome de domínio personalizado que você está atualizando.

## Excluir um nome de domínio personalizado {#deleting}

Um usuário com a função de **Proprietário da empresa** ou **Gerente de implantação** pode usar o Cloud Manager para excluir um nome de domínio personalizado.

### Excluir um nome de domínio personalizado de todos os ambientes associados {#delete-cdn-all}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até a página **Configurações de Domínio** a partir da tela **Visão Geral**.

1. Identifique a linha do nome de domínio personalizado que deseja excluir.

1. Clique no botão de reticências localizado na extremidade direita da linha.

1. Selecione **Excluir**.

1. Confirme seu envio.

### Excluir um nome de domínio personalizado de um ambiente específico {#delete-cdn-specific}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Na página **Ambientes**, navegue até uma tela de detalhes do ambiente de interesse.
1. Na tabela de nomes de domínio, identifique a linha do nome de domínio personalizado que deseja excluir.
1. Clique no botão de reticências localizado na extremidade direita da linha.
1. Selecione **Excluir**.
1. Confirme seu envio.
