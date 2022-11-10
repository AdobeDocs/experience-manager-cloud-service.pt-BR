---
title: Introdução às Listas de permissões de IP
description: Saiba como as listas de permissões de IP podem limitar de quais endereços os usuários podem acessar seus domínios as a Cloud Service AEM.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 18ecf3394ff575213756fced84a3b08795188240
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# Introdução às Listas de permissões de IP {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gerenciar Listas de permissões de IP"
>abstract="O AEM as a cloud service é acessível pela Internet e é protegido por meio de autenticação e autorização do usuário. As listas de permissões IP do Cloud Manager podem ser usadas para limitar e controlar o acesso somente a endereços IP confiáveis. Usuários do Cloud Manager com permissões apropriadas podem criar listas de permissões de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Adicionar uma Lista de permissões IP"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="Exibir e atualizar uma Lista de permissões IP"

Por padrão, o AEM as a cloud service é acessível pela Internet. Embora a segurança seja tratada por meio da autenticação e autorização do usuário, a lista de permissões de IP é uma maneira de limitar o acesso somente a endereços IP confiáveis.

As listas de permissões IP do Cloud Manager podem ser usadas para limitar e controlar o acesso somente a esses endereços IP confiáveis. Usuários do Cloud Manager com permissões apropriadas podem [criar listas de permissões](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) de endereços IP confiáveis dos quais os usuários do site podem acessar seus domínios AEM.

Depois de adicionado, [LISTAS DE PERMISSÕES de IP podem ser aplicadas/não aplicadas](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) várias vezes como uma unidade ou entidade para um serviço de autor e/ou editor em um ambiente.

>[!NOTE]
>
>Se nenhuma lista de permissões IP for aplicada, por padrão, todos os endereços IP serão permitidos. Assim que uma lista de permissões de IP for aplicada, nenhum endereço IP será permitido, exceto aqueles na lista de permissões de IP.

## Limitações           {#limitations}

Existem várias limitações para listas de permissões de IP que devem ser levadas em conta.

* É possível adicionar no máximo 50 listas de permissões IP ao seu programa
* É possível adicionar no máximo 50 endereços IP/CIDR a cada lista de permissões de IP.
* Os nomes de listas de permissões IP são aceitos no Cloud Manager para o serviço de criação e/ou publicação em um ambiente.
