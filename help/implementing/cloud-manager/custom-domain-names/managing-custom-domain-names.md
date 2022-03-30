---
title: Gerenciar nomes de domínio personalizados
description: Saiba como usar o Cloud Manager para exibir, atualizar, substituir e excluir nomes de domínio personalizados.
source-git-commit: 4604b5fad59524a05dc7addf16c70246a14cfea1
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 3%

---


# Gerenciar nomes de domínio personalizados {#managing-custom-domain-names}

O Cloud Manager permite exibir, atualizar, substituir e excluir nomes de domínio personalizados.

## Exibir e atualizar {#view-and-update}

Use o **Exibir e atualizar** para exibir os detalhes de qualquer um dos nomes de domínio personalizados.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o **Ambientes** da tela **Visão geral** página.

1. Identifique a linha do nome de domínio personalizado que deseja visualizar ou atualizar.

1. Clique no botão de reticências na extremidade direita da linha.

1. Selecione o **Exibir e atualizar** opção.

## Atualização do certificado SSL do nome de domínio personalizado {#update-cert}

Você pode seguir [as mesmas etapas para exibir e atualizar um nome de domínio personalizado](#view-and-update) para atualizar um certificado SSL de nome de domínio personalizado.

>[!NOTE]
>
>O certificado SSL deve ser válido, [já configurado,](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) e conter o nome de domínio personalizado que você está atualizando.

##  Excluir um nome de domínio personalizado {#deleting}

Um usuário com a **Proprietário da empresa** ou **Gerenciador de implantação** pode usar o Cloud Manager para excluir um nome de domínio personalizado.

### Excluindo um nome de domínio personalizado de todos os ambientes associados {#delete-cdn-all}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o **Ambientes** da tela **Visão geral** página.

1. Navegue até o **Configurações de domínio** da página **Ambientes** tela.

1. Identifique a linha do nome de domínio personalizado que deseja excluir.

1. Clique no botão de reticências na extremidade direita da linha.

1. Selecionar **Excluir**.
   ![](/help/implementing/cloud-manager/assets/cdn/cdn-delete.png)

1. Confirme seu envio.

### Excluindo um Nome de Domínio Personalizado de um Ambiente Específico {#delete-cdn-specific}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. Navegue até o **Ambientes** da tela **Visão geral** página.
1. No **Ambientes** navegue até a tela de detalhes do ambiente de interesse.
1. Na tabela de nomes de domínio, identifique a linha do nome de domínio personalizado que deseja excluir.
1. Clique no botão de reticências na extremidade direita da linha.
1. Selecionar **Excluir**.
1. Confirme seu envio.
