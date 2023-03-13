---
title: Introdução às listas de permissões de IP
description: Saiba como as listas de permissões de IP podem limitar os endereços dos quais os usuários podem acessar domínios do AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 286bc8e206b7a54cc1869e3965e55852cf62946d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 100%

---


# Introdução às listas de permissões de IP {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gerenciar listas de permissões de IP"
>abstract="O AEM as a cloud service pode ser acessado pela Internet e é protegido por meio de autenticação e autorização do usuário. As listas de permissões IP do Cloud Manager podem ser usadas para limitar e controlar o acesso somente a endereços IP confiáveis. Usuários do Cloud Manager com permissões apropriadas podem criar listas de permissões de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios do AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html?lang=pt-BR" text="Adicionar uma lista de permissões de IP"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html?lang=pt-BR" text="Exibir e atualizar uma lista de permissões de IP"

Por padrão, o AEM as a Cloud Service é acessível pela Internet. Embora a segurança seja tratada por meio da autenticação e autorização do usuário, a inclusão na lista de permissões de IP é uma maneira de limitar o acesso somente a endereços IP confiáveis.

As listas de permissão de IP do gerenciador de nuvem podem ser usadas para limitar e controlar o acesso somente a esses endereços IP confiáveis. Usuários do gerenciador de nuvem com permissões apropriadas podem [criar listas de permissões](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios do AEM.

Depois de adicionadas, [Listas de permissões de IP podem ser aplicadas/desaplicadas](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) várias vezes como uma unidade ou entidade a um serviço de autoria e/ou edição em um ambiente.

>[!NOTE]
>
>Se nenhuma lista de permissões IP for aplicada, por padrão, todos os endereços IP serão permitidos. Assim que uma lista de permissões de IP for aplicada, nenhum endereço IP será permitido, exceto os que constam na lista de permissões de IP.

## Limitações {#limitations}

Existem várias limitações para as listas de permissões de IP que devem ser consideradas.

* É possível adicionar no máximo 50 listas de permissões de IP ao seu programa.
* É possível adicionar no máximo 50 endereços IP/CIDR a cada lista de permissões de IP.
* O Cloud Manager oferece suporte a nomes de listas de permissões de IP para o serviço de autoria e/ou edição em um ambiente.
