---
title: Verificando o status da Lista de permissões de IP
description: Verificando o status da Lista de permissões de IP
translation-type: tm+mt
source-git-commit: 4635cb6360707d12cf512b0ee21f05169a153114
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Verificando o status da Lista de permissões de IP {#check-allow-list-status}

Siga as etapas abaixo para determinar o status das atualizações para sua Lista de permissões IP:

1. Clique no ícone Status da Lista de permissões IP na tabela da tela **Ambientes** e selecione **Listas de permissões IP**.

1. O Cloud Manager exibirá um dos seguintes status, conforme mencionado na seção abaixo.

## Status de uma Lista de permissões IP {#status}

Veja a seguir as definições de status que aparecerão em uma Lista de permissões de IP:

* **Aplicado**: A Lista de permissões IP foi aplicada com êxito em ambientes.  Os ambientes e o serviço podem ser vistos como mostrado na imagem abaixo.

* **Atualizando**: Está em andamento uma atualização da Lista de permissões IP que pode incluir uma ou mais aplicações ou cancelamento de aplicação. Cada Aplicar e Desaplicar será listado juntamente com Não iniciado/Em andamento/Concluído ou Com falha.

* **Falha**: Falha em um ou mais processos de aplicação ou cancelamento de aplicação em uma Atualização. Cada Aplicar e Desaplicar será listado juntamente com Concluído ou Falha.
   * O status falhará, mesmo se uma aplicação/desaplicação na atualização falhar.
   * O status permanecerá com falha até que todas as falhas sejam apagadas.O usuário deve selecionar o ícone de nova tentativa ao lado do status para limpar a falha.
   * O usuário não poderá atualizar ou excluir a Lista de permissões IP enquanto o status estiver com falha.

* **Excluindo**: A solicitação de exclusão está em andamento. Isto implica a não aplicação de todos os serviços. Cada Desaplicação será listada juntamente com Não iniciado/Em andamento/Concluído ou Com falha.
Quando a operação Excluir estiver concluída, a Lista de permissões IP:
   * Não é mais exibido na tabela Lista de permissões de IP * Não é mais aplicado a nenhum serviço no programa no Gerenciador de nuvem

* **Falha** na exclusão: Um ou mais processos de desaplicação em uma operação Excluir falharam. Cada Cancelamento de aplicação será listado juntamente com Concluído ou Falha.

   * O status será Excluir falha, mesmo se uma não aplicação falhar.
   * O status permanecerá Excluir falha até que todas as falhas sejam apagadas. O usuário deve selecionar Excluir de **...** na extremidade direita da linha na tabela para eliminar qualquer falha.
   * O usuário não poderá atualizar a Lista de permissões IP enquanto o status estiver com falha.

