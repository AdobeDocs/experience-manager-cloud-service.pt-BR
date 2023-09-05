---
title: Gerenciamento de listas de permissões de IP
description: Saiba como exibir, editar, excluir e verificar o status de suas listas de permissões de IP no Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
source-git-commit: 5311ba7f001201fc94c73fa52bc7033716c1ba78
workflow-type: ht
source-wordcount: '802'
ht-degree: 100%

---

# Gerenciamento de listas de permissões de IP {#manage-ip-allow-lists}

Saiba como exibir, editar, excluir e verificar o status de suas listas de permissões de IP no Cloud Manager.

## Exibição e atualização de listas de permissões de IP {#update-ip-allow-lists}

Um usuário com a função **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para exibir e atualizar uma lista de permissões de IP.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Acesse a página **Listas de permissão de IP** na tela **Ambientes**.
1. Identifique a linha das listas de permissões de IP que deseja exibir ou atualizar.
1. Clique no botão de reticências localizado na extremidade direita da linha.
1. Selecione a opção **Exibir e atualizar**.
1. O assistente **Exibir e atualizar** exibirá o nome, os endereços IP (ou intervalos) que definem a regra, juntamente com os ambientes e o serviço aos quais a regra é aplicada.
1. Altere o nome ou os endereços IP, conforme desejado, e confirme o envio.

A adição ou remoção de um novo intervalo IP em uma lista de permissões de IP automaticamente o aplicará/desaplicará a todos os ambientes/serviços correspondentes aos quais foram aplicados anteriormente.

Não é possível atualizar uma lista de permissões IP enquanto uma atualização anterior estiver em andamento e não tiver sido concluída.

## Verificação do status das listas de permissões de IP {#check-allow-list-status}

1. Faça logon no Cloud Manager em[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Clique no ícone **Status** para a lista de permissões de IP na tabela na tabela **Ambientes** e selecione a página **Lista de permissões de IP**.

1. O Cloud Manager exibirá o status da lista de permissões conforme descrito [na seção a seguir.](#status)

### Status de uma lista de permissões de IP {#status}

[Ao verificar o status das listas de permissões de IP,](#check-allow-list-status) pode haver um dos valores a seguir.

* **Aplicada** - A lista de permissões de IP foi aplicada com sucesso a um ou mais ambientes.

* **Em atualização**: uma atualização da lista de permissões de IP está em andamento, o que pode incluir uma ou mais aplicações ou cancelamento de aplicações na lista.

   * Cada aplicação/cancelamento de aplicação é listado junto com seu próprio status de **Não iniciado**, **Em andamento**, **Concluído** ou **Falha**.

* **Falha**: falha em um ou mais processos de aplicação ou de cancelamento de aplicação de uma atualização.
   * Cada aplicação e cancelamento de aplicação é listada com seu status.
      * O status é **Falha** se uma aplicação/cancelamento de aplicação na atualização falhar.
      * O status permanecerá como **Falha** até que todos os problemas sejam resolvidos.
         * Selecione o ícone de **Tentar novamente** ao lado do status para resolver a falha.
      * Não é possível atualizar ou excluir uma lista de permissões de IP com status de **Falha**.

* **Em exclusão**: uma exclusão de uma lista de permissões de IP está em andamento.
   * A exclusão envolve o cancelamento da aplicação da lista de todos os serviços.
   * Cada cancelamento de aplicação é listado com seu próprio status **Não iniciado**, **Em andamento**, **Concluído** ou **Falha**.
   * Quando a operação de exclusão for concluída, a lista de permissões de IP:
      * Não será mais exibida na tabela de lista de permissões de IP.
      * Não poderá mais ser aplicada a nenhum serviço no programa no Cloud Manager.

* **Falha ao excluir**: um ou mais cancelamentos de aplicação falharam durante uma operação de exclusão.

   * Cada cancelamento de aplicação é listado com o status **Concluído** ou **Falha**.
   * O status fica como **Falha ao excluir** se um cancelamento de aplicação falhar.
   * O status permanecerá como **Falha ao excluir** até que todos os problemas sejam resolvidos.
      * Selecione **Excluir** no menu de reticências, na extremidade direita da linha da tabela, para resolver qualquer falha.
   * Não será possível atualizar uma lista de permissões de IP enquanto seu status for **Falha**.

## Excluir uma lista de permissões de IP {#delete-allow-list}

Um usuário com a função **Proprietário da empresa** ou **Gerente de implantação** pode seguir essas etapas para exibir e atualizar uma lista de permissões de IP.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.
1. Acesse a tela **Ambientes** a partir da página **Visão geral**.
1. Acesse a página **Listas de permissão de IP** na tela **Ambientes**.
1. Identifique a linha da lista de permissões de IP que deseja excluir.
1. Selecione o menu de reticências na extremidade direita da linha.
1. Clique em **Excluir**.
1. Confirme seu envio.

A exclusão de uma lista de permissões de IP cancela automaticamente sua aplicação de todos os serviços e a exclui da tabela.

## Configurações pré-existentes de CDN {#pre-existing-cdn}

Se tiver uma configuração de CDN pré-existente para suas listas de permissões de IP, haverá uma mensagem informativa na página **Lista de permissões de IP**. A mensagem incentiva você a adicionar essas configurações por meio da interface, para que elas fiquem visíveis e possam ser definidas no Cloud Manager.

A mensagem desaparece assim que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário. Pode levar de 1 a 2 dias úteis para a mensagem desaparecer.

Consulte [Adicionar uma lista de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) para mais detalhes.

Uma mensagem semelhante também é fornecida nas páginas de **Certificados SSL** e de **Ambientes** para os ambientes que tenham configurações pré-existentes de CDN para certificados SSL ou nomes de domínio personalizados.
