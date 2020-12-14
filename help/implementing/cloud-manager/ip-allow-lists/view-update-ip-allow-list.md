---
title: Exibição e atualização - Listas de permissões de IP no Cloud Manager
description: Exibição e atualização - Listas de permissões de IP no Cloud Manager
translation-type: tm+mt
source-git-commit: 7fdfa626147a72f3d7fb98b89a19a871fc7a13ca
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Exibindo e Atualizando uma Lista de permissões IP {#view-update}

Você pode visualização e atualizar Listas de permissões IP nos seguintes cenários:

* Para Visualização e o menu Atualizar para simplesmente visualização os detalhes de uma ou mais Listas de permissões IP.
* Para editar um ou mais dos seguintes:
   * Intervalos de IP na definição do nome da regra
   * Nome amigável da regra de Lista de permissões IP

## Atualizar Lista de permissões IP {#update-ip-allow-lists}


Um usuário na função Proprietário da empresa ou Gerenciador de implantação deve estar conectado para poder atualizar uma Lista de permissões de IP.

>[!NOTE]
>O assistente de Visualização e atualização exibirá o nome, os IPs ou os intervalos IP que definem a regra. Além disso, exibirá os ambientes e o serviço nos quais a regra é aplicada.

Siga as etapas abaixo para atualizar uma Lista de permissões IP:

1. Navegue até a página **Listas de permissões IP** a partir da tela **Ambientes**.
1. Identifique a linha na qual a regra de Lista de permissões IP que você deseja que seja visualização/atualização está listada.
1. Selecione **...** na extremidade direita da linha.
1. Selecione a opção **Visualização e atualização**.
1. Faça alterações no nome ou no IP e confirme sua submissão.

## Considerações importantes ao adicionar, atualizar ou remover Listas de permissões IP {#considerations}

* A adição de um novo intervalo IP à Lista de permissões IP automaticamente a aplicará a todos os serviços de ambiente correspondentes.
* A remoção de um intervalo IP da Lista de permissões IP automaticamente Desaplicará-o de todos os serviços de ambiente correspondentes.
* As atualizações não podem ser feitas em uma Lista de permissões IP enquanto uma atualização anterior estiver em andamento e não tiver sido concluída.
* As atualizações não podem ser feitas em uma Lista de permissões IP se houver erros em uma atualização anterior. Qualquer erro deve ser apagado ao tentar repetir a atualização.
Consulte [Verificando o status da Lista de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md) para saber mais.