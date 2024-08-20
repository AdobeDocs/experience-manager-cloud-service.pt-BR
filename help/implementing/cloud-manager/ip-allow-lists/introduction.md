---
title: Introdução às listas de permissões de IP
description: Saiba como as Listas de permissões de IP podem limitar os endereços dos quais os usuários podem acessar domínios no AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 20%

---


# Introdução às listas de permissões de IP {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gerenciar listas de permissões de IP"
>abstract="O AEM as a Cloud Service pode ser acessado pela Internet e é protegido por meio de autenticação e autorização do usuário. As Listas de permissões IP da Cloud Manager podem ser usadas para limitar e controlar o acesso somente a endereços IP confiáveis. Usuários do Cloud Manager com as permissões apropriadas podem criar listas de permissões de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios do AEM."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="Adicionar uma lista de permissões de IP"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="Exibir e atualizar uma Lista de permissões de IP"

O AEM as a cloud service é acessível por padrão pela Internet. Embora a segurança seja tratada por meio da autenticação e autorização do usuário, a inclusão na lista de permissões de IP é uma maneira de limitar o acesso somente a endereços IP confiáveis.

As Listas de permissões IP da Cloud Manager podem ser usadas para limitar e controlar o acesso somente a esses endereços IP confiáveis. Os usuários do Cloud Manager com permissões apropriadas podem [criar Listas de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios do AEM.

Após adicionar, [Listas de permissões de IP podem ser aplicadas ou desaplicadas](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) várias vezes como uma unidade ou entidade a um serviço de autoria, de editor ou ambos, em um ambiente.

>[!NOTE]
>
>Se nenhuma Lista de permissões IP for aplicada, por padrão, todos os endereços IP serão permitidos. Quando uma Lista de permissões IP é aplicada, nenhum endereço IP é permitido, exceto os endereços na Lista de permissões IP.

## Limitações {#limitations}

Existem várias limitações para as Listas de permissões de IP que devem ser consideradas.

* É possível adicionar no máximo 50 Listas de permissões IP ao seu programa.
* É possível adicionar no máximo 50 endereços IP/CIDR a cada Lista de permissões IP.
* Os nomes de Lista de permissões de IP são suportados no Cloud Manager para o serviço de autoria, serviço de publicação ou ambos em um ambiente.
