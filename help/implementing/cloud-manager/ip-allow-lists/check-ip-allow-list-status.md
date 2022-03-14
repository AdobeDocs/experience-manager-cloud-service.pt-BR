---
title: Verificando o status da Lista de permissões de IP
description: Verificando o status da Lista de permissões de IP
exl-id: 5ddea04f-3720-4663-90a8-9399019bfcbe
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Verificando o status da Lista de permissões de IP {#check-allow-list-status}

Siga as etapas abaixo para determinar o status das atualizações na sua Lista de permissões de IP:

1. Clique no ícone Status da Lista de permissões IP na tabela **Ambientes** e selecione **LISTAS DE PERMISSÕES de IP** página.

1. O Cloud Manager exibirá um dos seguintes status, conforme mencionado na seção abaixo.

## Status de uma Lista de permissões IP {#status}

Estas são as definições de status que aparecerão em uma Lista de permissões de IP:

* **Aplicado**: A Lista de permissões de IP é aplicada com êxito em ambientes.  Os ambientes e o serviço podem ser vistos como mostrado na imagem abaixo.

* **Atualização**: Está em andamento uma atualização da Lista de permissões IP que pode incluir uma ou mais aplicações ou não aplicação. Cada Aplicar e Desaplicar será listado juntamente com Não Iniciado/Em Andamento/Concluído ou Falha.

* **Falha**: Um ou mais processos de aplicação ou cancelamento de aplicação em uma Atualização falharam. Cada Aplicar e Desaplicar será listado juntamente com Concluído ou Falha.
   * O status será Failed, mesmo se um apply/unapply na atualização falhar.
   * O status permanecerá com Falha até que todas as falhas sejam apagadas. O usuário deve selecionar o ícone de nova tentativa ao lado do status para limpar a falha.
   * O usuário não poderá atualizar ou excluir a Lista de permissões IP enquanto o status for Failed.

* **Exclusão**: A solicitação de exclusão está em andamento. Isto implica a não aplicação de todos os serviços. Cada Desaplicação será listada juntamente com Não Iniciado/Em Andamento/Concluído ou Falha.
Quando a operação Delete for concluída, a Lista de permissões IP irá:
   * Não é mais exibido na tabela de Lista de permissões de IP.
   * Não pode mais ser aplicado a nenhum serviço no programa no Cloud Manager.

* **Falha ao Excluir**: Falha em um ou mais processos de desaplicação em uma operação de exclusão. Cada Desaplicação será listada juntamente com Concluído ou Falha.

   * O status será Delete Failed (Falha na exclusão), mesmo se uma não aplicação falhar.
   * O status permanecerá Delete Failed até que todas as falhas sejam apagadas. O usuário deve selecionar Excluir no **...** na extremidade direita da linha da tabela para limpar qualquer falha.
   * O usuário não poderá atualizar a Lista de permissões de IP enquanto o status for Failed.

## Configurações de CDN pré-existentes para Listas de permissões IP {#pre-existing-cdn}

Os clientes com ambientes que incluem configurações de CDN pré-existentes para Listas de permissões de IP, certificados SSL ou nomes de domínio personalizados verão a seguinte mensagem na **LISTA DE PERMISSÕES IP** e **Ambiente** página de detalhes. A mensagem exibida na interface do usuário desaparecerá assim que o cliente migrar totalmente todas as configurações de ambiente pré-existentes por meio da interface do usuário e talvez demore de 1 a 2 dias úteis para a mensagem desaparecer.

>[!NOTE]
>Para visualizar e gerenciar as configurações pré-existentes, elas devem ser adicionadas por meio da interface do usuário. Consulte [Adicionar uma Lista de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) para obter mais detalhes.

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
