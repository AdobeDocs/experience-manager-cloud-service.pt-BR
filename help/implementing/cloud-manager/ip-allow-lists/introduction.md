---
title: Introdução às listas de permissões de IP
description: Saiba como as listas de permissão de IP podem limitar de quais endereços os usuários podem acessar domínios no AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: ht
source-wordcount: '306'
ht-degree: 100%

---


# Introdução às listas de permissões de IP {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gerenciar listas de permissões de IP"
>abstract="O AEM as a Cloud Service pode ser acessado pela Internet e é protegido por meio da autenticação e da autorização do usuário. As listas de permissões de IP do Cloud Manager podem ser usadas para limitar e controlar o acesso apenas a endereços IP confiáveis. Usuários do Cloud Manager com as permissões apropriadas podem criar listas de permissões de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios do AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html?lang=pt-BR" text="Adicionar uma lista de permissões de IP"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists.html?lang=pt-BR" text="Exibir e atualizar uma lista de permissões de IP"

Por padrão, o AEM as a Cloud Service é acessível pela Internet. Embora a segurança seja tratada por meio da autenticação e autorização do usuário, a inclusão na lista de permissões de IP é uma maneira de limitar o acesso somente a endereços IP confiáveis.

As listas de permissões de IP do Cloud Manager podem ser usadas para limitar e controlar o acesso apenas a endereços IP confiáveis. Os usuários do Cloud Manager com as permissões apropriadas podem [criar listas de permissões](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) de endereços IP confiáveis a partir dos quais os usuários do site podem acessar os domínios do AEM.

Após adicionadas, as [listas de permissões de IP podem ser aplicadas/desaplicadas](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) várias vezes como uma unidade ou entidade a um serviço de autor e/ou editor em um ambiente.

>[!NOTE]
>
>Se nenhuma lista de permissões de IP for aplicada, por padrão, todos os endereços IP são permitidos. Quando uma lista de permissões de IP é aplicada, nenhum endereço IP é permitido, exceto os incluídos na lista.

## Limitações {#limitations}

As listas de permissões de IP possuem várias limitações que devem ser consideradas.

* É possível adicionar no máximo 50 listas de permissões de IP ao seu programa
* É possível adicionar no máximo 50 endereços IP/CIDR a cada lista de permissões de IP.
* Os nomes das listas de permissões de IP são compatíveis com o Cloud Manager para o serviço de criação ou publicação (ou ambos) de um ambiente.
