---
title: Gerenciar listas de permissões de IP
description: Saiba como exibir, editar, excluir e verificar o status de Listas de permissões de IP no Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 43%

---

# Gerenciar listas de permissões de IP {#manage-ip-allow-lists}

Saiba como exibir, editar, excluir e verificar o status de Listas de permissões de IP no Cloud Manager.

## Exibir e atualizar Listas de permissões de IP {#update-ip-allow-lists}

Um usuário com a função **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para exibir e atualizar uma Lista de permissões de IP.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Acesse a página **Listas de permissão de IP** na tela **Ambientes**.
1. Identifique a linha das Listas de permissões IP que deseja exibir ou atualizar.
1. Clique no botão de reticências localizado na extremidade direita da linha.
1. Selecione a opção **Exibir e atualizar**.
1. O assistente **Exibir e atualizar** exibe o nome, os endereços IP (ou intervalos) que definem a regra, juntamente com os ambientes e serviços aos quais a regra é aplicada.
1. Altere o nome ou os endereços IP, conforme desejado, e confirme o envio.

A adição ou remoção de um novo intervalo IP em uma Lista de permissões IP automaticamente o aplica/desaplica a todos os ambientes/serviços correspondentes aos quais foram aplicados anteriormente.

Não é possível atualizar uma Lista de permissões IP enquanto uma atualização anterior estiver em andamento e não tiver sido concluída.

## Verificar o status das Listas de permissões de IP {#check-allow-list-status}

1. Faça logon no Cloud Manager em[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Clique no ícone **Status** da Lista de permissões IP a partir da tabela na tela **Ambientes** e selecione a página **Listas de permissões IP**.

1. O Cloud Manager exibe o status da Lista de permissões conforme descrito [na seguinte seção](#status).

### Status de uma lista de permissões de IP {#status}

[Ao verificar o status das Listas de permissões de IP](#check-allow-list-status), pode haver um dos valores a seguir.

* **Aplicado** - A Lista de permissões IP foi aplicada com êxito a um ou mais ambientes.

* **Atualizando** - Uma atualização da Lista de permissões IP está em andamento, o que pode incluir um ou mais aplicativos ou o cancelamento da aplicação da lista.

   * Cada aplicação/cancelamento de aplicação é listado junto com seu próprio status de **Não iniciado**, **Em andamento**, **Concluído** ou **Falha**.

* **Falha**: falha em um ou mais processos de aplicação ou de cancelamento de aplicação de uma atualização.
   * Cada aplicação e cancelamento de aplicação é listada com seu status.
      * O status é **Falha** se uma aplicação/cancelamento de aplicação na atualização falhar.
      * O status permanecerá como **Falha** até que todos os problemas sejam resolvidos.
         * Selecione o ícone de **Tentar novamente** ao lado do status para resolver a falha.
      * Não é possível atualizar ou excluir uma Lista de permissões IP com status **Falha**.

* **Excluindo** - Uma exclusão de uma Lista de permissões IP está em andamento.
   * A exclusão envolve o cancelamento da aplicação da lista de todos os serviços.
   * Cada cancelamento de aplicação é listado com seu próprio status **Não iniciado**, **Em andamento**, **Concluído** ou **Falha**.
   * Quando a operação de exclusão for concluída:
      * A Lista de permissões de IP não aparece na tabela de Listas de permissões de IP.
      * A Lista de permissões IP não é aplicada em nenhum serviço no programa no Cloud Manager.

* **Falha ao excluir**: um ou mais cancelamentos de aplicação falharam durante uma operação de exclusão.

   * Cada cancelamento de aplicação é listado com o status **Concluído** ou **Falha**.
   * O status fica como **Falha ao excluir** se um cancelamento de aplicação falhar.
   * O status permanece como **Falha ao excluir** até que todas as falhas sejam resolvidas. Na extremidade direita da linha da tabela, clique no menu de reticências e em **Excluir** para resolver qualquer falha.
   * Não é possível atualizar uma Lista de permissões IP enquanto o status for **Falha**.

## Excluir uma Lista de permissões IP {#delete-allow-list}

Um usuário com a função **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para exibir e atualizar uma Lista de permissões de IP.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Acesse a página **Listas de permissão de IP** na tela **Ambientes**.
1. Identifique a linha da Lista de permissões IP que deseja excluir.
1. Selecione o menu de reticências na extremidade direita da linha.
1. Clique em **Excluir**.
1. Confirme seu envio.

A exclusão de uma Lista de permissões IP a desaplica automaticamente de todos os serviços e a exclui da tabela.

## Configurações de CDN pré-existentes {#pre-existing-cdn}

Se você tiver uma configuração de CDN (Content Delivery Network) pré-existente para suas Listas de permissões de IP, há uma mensagem informativa na página **Lista de permissões de IP**. A mensagem incentiva você a adicionar essas configurações por meio da interface, para que elas fiquem visíveis e possam ser definidas no Cloud Manager.

A mensagem desaparece assim que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário. Pode levar de 1 a 2 dias úteis para a mensagem desaparecer.

Consulte [Adicionar uma Lista de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) para obter mais detalhes.

Uma mensagem semelhante também é fornecida nas páginas de **Certificados SSL** e de **Ambientes** para os ambientes que tenham configurações pré-existentes de CDN para certificados SSL ou nomes de domínio personalizados.
