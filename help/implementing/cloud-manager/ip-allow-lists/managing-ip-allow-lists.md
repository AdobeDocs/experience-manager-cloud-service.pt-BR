---
title: Gerenciamento de listas de permissões de IP
description: Saiba como visualizar, editar, excluir e verificar o status de suas listas de permissões de IP no Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
source-git-commit: 3080427529bb65e27721e05069012b33579fdd73
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 2%

---

# Gerenciamento de listas de permissões de IP {#manage-ip-allow-lists}

Saiba como visualizar, editar, excluir e verificar o status de suas listas de permissões de IP no Cloud Manager.

## Exibindo e Atualizando Listas de permissões IP {#update-ip-allow-lists}

Um usuário na **Proprietário da empresa** ou **Gerenciador de implantação** pode seguir essas etapas para visualizar e atualizar uma lista de permissões IP.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. Navegar para **Ambientes** da tela **Visão geral** página.
1. Navegue até o **LISTAS DE PERMISSÕES de IP** da página **Ambientes** tela.
1. Identifique a linha para as listas de permissões IP que deseja visualizar ou atualizar.
1. Clique no botão de reticências na extremidade direita da linha.
1. Selecione o **Exibir e atualizar** opção.
1. O **Exibir e atualizar** O assistente exibirá o nome, os endereços IP (ou intervalos) que definem a regra junto com os ambientes e o serviço aos quais a regra é aplicada.
1. Faça alterações no nome ou endereços IP e confirme o envio.

A adição ou remoção de um novo intervalo IP a uma lista de permissões IP automaticamente o aplicará/desaplicará a todos os ambientes/serviços correspondentes aos quais foi aplicado anteriormente.

Não é possível fazer atualizações em uma lista de permissões IP enquanto uma atualização anterior estiver em andamento e não tiver sido concluída.

## Verificar o status das Listas de permissões IP {#check-allow-list-status}

Siga estas etapas para verificar o status das listas de permissões de IP.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegar para **Ambientes** da tela **Visão geral** página.

1. Clique no botão **Status** ícone para a lista de permissões IP na tabela na **Ambientes** e selecione o **LISTAS DE PERMISSÕES de IP** página.

1. O Cloud Manager exibirá o status da lista de permissões conforme descrito [na seção a seguir.](#status)

### Status de uma Lista de permissões IP {#status}

[Ao verificar o status das listas de permissões de IP,](#check-allow-list-status) eles podem ter um dos valores a seguir.

* **Aplicado** - A lista de permissões IP é aplicada com êxito a um ou mais ambientes.

* **Atualização** - Uma atualização da lista de permissões de IP está em andamento, o que pode incluir um ou mais aplicativos ou o cancelamento da aplicação da lista.

   * Cada aplicativo/não aplicativo é listado junto com seu próprio status de **Não iniciado**, **Em Andamento**, **Concluído** ou **Falha**.

* **Falha** - Falha em um ou mais processos de aplicativo ou de cancelamento de aplicativo de uma atualização.
   * Cada aplicativo e desaplicativo é listado junto com seu status.
      * O status é **Falha** se um aplicativo/desaplicativo na atualização falhar.
      * O status permanecerá como **Falha** até que todas as falhas sejam apagadas.
         * Você deve selecionar a variável **Tentar novamente** ícone ao lado do status para limpar a falha.
      * Não é possível atualizar ou excluir uma lista de permissões IP com uma **Falha** status.

* **Exclusão** - Uma exclusão de uma lista de permissões IP está em andamento.
   * A exclusão envolve a desaplicação da lista de todos os serviços.
   * Cada não aplicativo é listado junto com seu próprio status de **Não iniciado**, **Em Andamento**, **Concluído** ou **Falha**.
   * Quando a operação de exclusão for concluída, a lista de permissões de IP:
      * Não é mais exibido na tabela de lista de permissões de IP.
      * Não pode mais ser aplicado a nenhum serviço no programa no Cloud Manager.

* **Falha ao Excluir** - Um ou mais desaplicativos falharam durante uma operação de exclusão.

   * Cada não aplicativo é listado junto com o status **Concluído** ou **Falha**.
   * O status será **Falha ao Excluir** se um desaplicativo falhar.
   * O status permanecerá como **Falha ao Excluir** até que todas as falhas sejam apagadas.
      * Você deve selecionar **Excluir** no menu reticências, na extremidade direita da linha da tabela, para limpar qualquer falha.
   * Não é possível atualizar uma lista de permissões IP enquanto o status estiver **Falha**.

## Excluir uma lista de permissões de IP {#delete-allow-list}

Um usuário na **Proprietário da empresa** ou **Gerenciador de implantação** pode seguir essas etapas para visualizar e atualizar uma lista de permissões IP.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. Navegar para **Ambientes** da tela **Visão geral** página.
1. Navegue até o **LISTAS DE PERMISSÕES de IP** da página **Ambientes** tela.
1. Identifique a linha da lista de permissões IP que deseja excluir.
1. Selecione o menu de reticências na extremidade direita da linha.
1. Clique em **Excluir**.
1. Confirme seu envio.

A exclusão de uma lista de permissões IP a desaplica automaticamente de todos os serviços e a exclui da tabela.

## Configurações pré-existentes de CDN {#pre-existing-cdn}

Se você tiver uma configuração de CDN pré-existente para suas listas de permissões de IP, haverá uma mensagem informativa no **LISTA DE PERMISSÕES IP** , incentivando você a adicionar essas configurações por meio da interface do usuário, para que fiquem visíveis e configuráveis no Cloud Manager.

A mensagem desaparece assim que todas as configurações de ambiente pré-existentes são migradas usando a interface do usuário do . Pode levar de 1 a 2 dias úteis para a mensagem desaparecer.

Consulte o documento [Adicionar uma lista de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) para obter mais detalhes.

Uma mensagem semelhante também é fornecida no **Certificados SSL** e **Ambientes** páginas para ambientes que tenham configurações CDN pré-existentes para certificados SSL ou nomes de domínio personalizados.
