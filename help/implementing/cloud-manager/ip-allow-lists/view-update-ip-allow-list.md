---
title: Visualização e atualização - Listas de permissões de IP no Cloud Manager
description: Visualização e atualização - Listas de permissões de IP no Cloud Manager
exl-id: 9f9aebcd-b6d0-497a-b262-0a24b4938b45
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 2%

---

# Visualização e atualização de uma lista de permissões de IP {#view-update}

Você pode exibir e atualizar Listas de permissões de IP nos seguintes cenários:

* Para exibir e atualizar o menu para simplesmente exibir os detalhes de uma ou mais Listas de permissões de IP.
* Para editar um ou mais dos seguintes itens:
   * Intervalos de IP na definição do nome da regra
   * Nome amigável da regra de Lista de permissões IP

## Atualizar Lista de permissões IP {#update-ip-allow-lists}


Um usuário na função Proprietário comercial ou Gerente de implantação deve estar conectado para poder atualizar uma Lista de permissões de IP.

>[!NOTE]
>O assistente de Exibição e atualização exibirá o nome, os intervalos IP ou os intervalos IP que definem a regra. Além disso, ele exibirá os ambientes e o serviço em que a regra é aplicada.

Siga as etapas abaixo para atualizar uma Lista de permissões IP:

1. Navegue até o **LISTAS DE PERMISSÕES de IP** da página **Ambientes** tela.
1. Identifique a linha na qual a regra de Lista de permissões IP que você deseja visualizar/atualizar está listada.
1. Selecione o **...** na extremidade direita da linha.
1. Selecione o **Exibir e atualizar** opção.
1. Faça alterações no nome ou no IP e confirme o envio.

## Considerações importantes ao adicionar, atualizar ou remover Listas de permissões IP {#considerations}

* A adição de um novo intervalo IP à Lista de permissões IP o aplicará automaticamente a todos os serviços ambientais correspondentes.
* A remoção de um intervalo IP da Lista de permissões IP irá automaticamente Desaplicá-lo de todos os serviços ambientais correspondentes.
* Não é possível fazer atualizações em uma Lista de permissões IP enquanto uma atualização anterior estiver em andamento e não tiver sido concluída.
* Não é possível fazer atualizações em uma Lista de permissões IP se houver erros de uma atualização anterior. Qualquer erro deve ser eliminado tentando atualizar novamente.
Consulte [Verificando o status da Lista de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md) para saber mais.
