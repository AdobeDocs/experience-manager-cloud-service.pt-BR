---
title: Introdução - Listas de permissões de IP no Cloud Manager
description: Introdução - Listas de permissões de IP no Cloud Manager
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 1875920ae5180074dcad98fb5c10242b6baa76c7
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 3%

---

# Introdução {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gerenciar Listas de permissões de IP"
>abstract="O AEM as a cloud service está aberto na Internet e a segurança é tratada por meio de autenticação e autorização do usuário. A lista de permissões de IP é um recurso no Cloud Manager usado para limitar e controlar o acesso somente a usuários confiáveis. Esse recurso permite que usuários com permissões criem listas de permissões de endereços IP confiáveis dos quais os usuários de sites podem acessar seus domínios AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Adicionar uma Lista de permissões IP"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="Exibir e atualizar uma Lista de permissões IP"

O AEM as a cloud service está aberto na Internet e a segurança é tratada por meio de autenticação e autorização do usuário. A lista de permissões de IP é um recurso no Cloud Manager usado para limitar e controlar o acesso somente a usuários confiáveis. Esse recurso permite que usuários com permissões criem listas de permissões de endereços IP confiáveis dos quais os usuários de sites podem acessar seus domínios AEM.

>[!NOTE]
>É possível adicionar no máximo 50 Listas de permissões IP ao seu programa e no máximo 50 endereços IP/CIDR podem ser adicionados a cada Lista de permissões IP.

LISTAS DE PERMISSÕES IP podem ser adicionadas uma vez e aplicadas/não aplicadas várias vezes como uma unidade ou entidade a um serviço Autor e/ou Editor em um ambiente.

>[!NOTE]
>Os nomes de Listas de permissões IP são compatíveis com o Cloud Manager para o serviço Autor e/ou Publicação em um ambiente.

Usando a página Lista de permissões de IP da interface do usuário do Cloud Manager ou a página Detalhes do ambiente , um usuário com permissões pode executar várias tarefas para gerenciar Listas de permissões de IP em seus ambientes, incluindo:

* [Adicionar uma lista de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
   >[!NOTE]
   > Você pode Adicionar uma vez e reutilizar ou aplicar a regra várias vezes em todos os serviços do ambiente no programa.
* [Visualização ou atualização de uma Lista de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
* [Aplicar ou desaplicar uma Lista de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
* [Excluir uma lista de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)
