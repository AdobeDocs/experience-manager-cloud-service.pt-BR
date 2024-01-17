---
title: Aplicação e remoção de listas de permissões de IP
description: Saiba como aplicar e cancelar a aplicação de listas de permissões de IP a ambientes.
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 81%

---


# Aplicação e remoção de listas de permissões de IP {#apply-allow-list}

Ao aplicar uma lista de permissões de IP, todos os intervalos de IP incluídos na definição da lista são associados a um serviço de criação ou publicação em um ambiente. Cancelar a aplicação de uma lista é o processo inverso.

## Aplicação de uma lista de permissões de IP {#applying}

Um usuário com a função **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para aplicar uma lista de permissões de IP.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No **[Meus programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** selecione o programa.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Acesse a página de detalhes do ambiente específico na tela **Ambientes** e navegue até a tabela **Lista de permissões de IP**.
1. Use os campos de entrada na parte superior da tabela para poder selecionar a lista de permissões IP e o serviço de autoria ou publicação ao qual deseja aplicá-la.
   * A lista de permissões de IP deve existir no Cloud Manager para ser aplicada.
1. Clique em **Aplicar** e confirme o envio.

## Desaplicar listas de permissões {#un-applying}

Um usuário com a função **Proprietário da empresa** ou **Gerente de implantação** pode seguir estas etapas para cancelar a aplicação de uma lista de permissões de IP.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Acesse a página de detalhes do ambiente específico na tela **Ambientes** e navegue até a tabela **Lista de permissões de IP**.
1. Identifique a linha da lista de permissões IP que deseja desaplicar.
1. Selecione o botão de reticências na extremidade direita da linha.
1. Selecione a opção **Desaplicar** e confirme o envio.
