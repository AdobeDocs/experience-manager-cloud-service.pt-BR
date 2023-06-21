---
title: Introdução às listas de permissões de IP
description: Saiba como as listas de permissões de IP podem limitar a partir de quais endereços os usuários podem acessar domínios no AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 18%

---


# Introdução às listas de permissões de IP {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gerenciar listas de permissões IP"
>abstract="O AEM as a cloud service pode ser acessado pela Internet e é protegido por meio de autenticação e autorização do usuário. As listas de permissões IP do Cloud Manager podem ser usadas para limitar e controlar o acesso somente a endereços IP confiáveis. Lista de permissões Usuários do Cloud Manager com permissões apropriadas podem criar notificações de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios de AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Adicionar uma lista de permissões de IP"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists.html" text="Exibir e atualizar uma lista de permissões de IP"

Por padrão, o AEM as a Cloud Service é acessível pela Internet. Embora a segurança seja tratada por meio da autenticação e autorização do usuário, a inclusão na lista de permissões de IP é uma maneira de limitar o acesso somente a endereços IP confiáveis.

As listas de permissões IP do Cloud Manager podem ser usadas para limitar e controlar o acesso somente a esses endereços IP confiáveis. Usuários do Cloud Manager com permissões apropriadas podem [criar incluis na lista de permissões](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios AEM.

Depois de adicionar, [As listas de permissões IP podem ser aplicadas/desaplicadas](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) várias vezes como uma unidade ou entidade para um serviço de autoria e/ou edição em um ambiente.

>[!NOTE]
>
>Se nenhuma inclui na lista de permissões de IP for aplicada, por padrão, todos os endereços IP serão permitidos. Quando uma inclui na lista de permissões IP é aplicada, nenhum endereço IP é permitido, exceto para endereços no incluo na lista de permissões IP.

## Limitações {#limitations}

Existem várias limitações para as listas de permissões de IP que devem ser consideradas.

* Um máximo de 50 incluis na lista de permissões de IPs podem ser adicionadas ao seu programa
* É possível adicionar no máximo 50 endereços IP/CIDR a cada inclui na lista de permissões de IP.
* Os nomes de incluis na lista de permissões IP são suportados no Cloud Manager para o serviço de criação ou publicação, ou ambos, em um ambiente.
