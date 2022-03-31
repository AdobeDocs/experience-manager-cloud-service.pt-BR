---
title: Introdução às Listas de permissões de IP
description: Saiba como as listas de permissões de IP podem limitar de quais endereços os usuários podem acessar seus domínios as a Cloud Service AEM.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 8d1680fa8dbaaefa297cf8c6698097b3c7acc48d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Introdução às Listas de permissões de IP {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gerenciar Listas de permissões de IP"
>abstract="O AEM as a cloud service é acessível pela Internet e é protegido por meio de autenticação e autorização do usuário. As listas de permissões IP do Cloud Manager podem ser usadas para limitar e controlar o acesso somente a endereços IP confiáveis. Usuários do Cloud Manager com permissões apropriadas podem criar listas de permissões de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Adicionar uma Lista de permissões IP"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="Exibir e atualizar uma Lista de permissões IP"

O AEM as a cloud service é acessível pela Internet e é protegido por meio de autenticação e autorização do usuário. As listas de permissões IP do Cloud Manager podem ser usadas para limitar e controlar o acesso somente a endereços IP confiáveis. Usuários do Cloud Manager com permissões apropriadas podem criar listas de permissões de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios AEM.

LISTAS DE PERMISSÕES IP podem ser adicionadas uma vez e aplicadas/não aplicadas várias vezes como uma unidade ou entidade a um serviço de autor e/ou editor em um ambiente.

## Limitações           {#limitations}

Existem várias limitações para listas de permissões de IP que devem ser levadas em conta.

* É possível adicionar no máximo 50 listas de permissões IP ao seu programa
* É possível adicionar no máximo 50 endereços IP/CIDR a cada lista de permissões de IP.
* Os nomes de listas de permissões IP são aceitos no Cloud Manager para o serviço de criação e/ou publicação em um ambiente.
