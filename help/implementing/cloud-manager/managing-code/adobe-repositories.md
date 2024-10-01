---
title: Adicionar um repositório de Adobe no Cloud Manager
description: Saiba como adicionar um repositório gerenciado por Adobe no Cloud Manager.
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f2364de6237ca9f0285815b581bcf3881488188d
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 7%

---

# Adicionar um repositório Adobe no Cloud Manager {#adobe-repositories}

Saiba como adicionar um repositório gerenciado por Adobe no Cloud Manager.

A página **Repositórios** facilita a adição de repositórios gerenciados por Adobe adicionais a um programa selecionado.

**Para adicionar um repositório de Adobe no Cloud Manager:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada e o programa ao qual você deseja adicionar um repositório gerenciado por Adobe.

1. Na página **Visão geral do programa**, no menu lateral, clique em ![ícone de Pasta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **guia Repositórios**.

1. Na página **Repositórios**, próximo ao canto superior direito, clique em **Adicionar Repositório**.

   ![Botão Adicionar repositório](assets/add-repository.png)

1. Na caixa de diálogo **Adicionar repositório**, verifique se **Repositório Adobe** está selecionado como o tipo de repositório.

1. Nos respectivos campos de texto, insira o seguinte:

   * **Nome do repositório** - Um nome expressivo para o novo repositório.
   * **Visualização da URL do repositório** - Não é necessário inserir um caminho de URL ou editar o caminho existente, pois a infraestrutura do repositório já está em vigor e é totalmente integrada e gerenciada pelo Adobe.
   * **Descrição (opcional)** - Uma descrição detalhada do repositório.

   ![Caixa de diálogo Adicionar Repositório](assets/add-adobe-repository.png)

1. Clique em **Salvar**.
O novo repositório é exibido na tabela da página **Repositórios**.

Agora você pode associar um [pipeline de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) ou gerenciá-lo na [**página Repositórios**](managing-repositories.md).

>[!TIP]
>
>Também é possível adicionar repositórios GitHub que você mesmo gerencia como [repositórios privados](private-repositories.md).
