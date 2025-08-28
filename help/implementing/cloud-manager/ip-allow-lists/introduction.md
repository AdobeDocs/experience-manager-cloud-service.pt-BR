---
title: Introdução às listas de permissões de IP
description: Saiba como as Listas de permissões de IP podem limitar os endereços dos quais os usuários podem acessar domínios no AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fdd86b966f0480c00b7cd975d63a48b82fb1d027
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 21%

---


# Introdução às listas de permissões de IP {#introduction}

Saiba como as Listas de permissões de IP podem limitar os endereços dos quais os usuários podem acessar domínios no AEM as a Cloud Service.

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gerenciar listas de permissões de IP"
>abstract="O AEM as a Cloud Service pode ser acessado pela Internet e é protegido por meio da autenticação e da autorização do usuário. As listas de permissões de IP do Cloud Manager podem ser usadas para limitar e controlar o acesso somente a endereços IP confiáveis. Usuários do Cloud Manager com as permissões apropriadas podem criar listas de permissões de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios do AEM."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="Adicionar uma lista de permissões de IP"
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="Exibir e atualizar uma lista de permissões de IP"

## Visão geral {#overview}

O AEM as a cloud service é acessível por padrão pela Internet. Embora a segurança seja tratada por meio da autenticação e autorização do usuário, a inclusão na lista de permissões de IP é uma maneira de limitar o acesso somente a endereços IP confiáveis.

As Listas de permissões IP da Cloud Manager podem ser usadas para limitar e controlar o acesso somente a esses endereços IP confiáveis. Usuários do Cloud Manager com permissões apropriadas podem [criar e adicionar Listas de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) de endereços IP confiáveis a partir dos quais os usuários do site podem acessar seus domínios do AEM.

Após adicionar, [Listas de permissões de IP podem ser aplicadas ou desaplicadas](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) várias vezes como uma unidade ou entidade a um serviço de autoria, de editor ou ambos, em um ambiente.

>[!NOTE]
>
>Se nenhuma Lista de permissões IP for aplicada, por padrão, todos os endereços IP serão permitidos. Quando uma Lista de permissões IP é aplicada, nenhum endereço IP é permitido, exceto os endereços na Lista de permissões IP.

## Notas de uso {#usage-notes}

* É possível adicionar no máximo 50 Listas de permissões IP ao programa.
* É possível adicionar no máximo 50 endereços IP/CIDR a cada Lista de permissões IP.
* Os nomes de Lista de permissões de IP são suportados no Cloud Manager para o serviço de autoria, serviço de publicação ou ambos em um ambiente.

### Pipelines de front-end e Listas de permissões de IP {#front-end-pipeline}

Se você usa (ou pretende usar) o [pipeline de front-end para desenvolver sites](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md), a seguinte Lista de permissões de IP do Cloud Manager deve ser adicionada com antecedência.

Quando você [adicionar a Lista de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md#add-cm-allowlist), nomeie-a como *`Cloud Manager`*, copie a lista de endereços abaixo e cole-a na caixa de diálogo Lista de permissões de IP.

```text
52.254.106.192/28
20.186.185.181
52.254.106.240/28
52.254.107.128/28
52.254.105.192/28
52.254.106.176/28
20.186.185.227
52.254.106.144/28
52.254.107.64/28
20.186.185.239
20.22.83.112
52.254.107.80/28
52.254.107.144/28
52.254.106.224/28
20.14.241.153
52.254.107.0/28
52.254.107.32/28
52.254.106.208/28
40.70.154.136/29
52.254.106.160/28
52.254.107.16/28
52.254.106.0/28
4.152.211.251
```

Para evitar a interrupção da execução do pipeline de front-end, verifique se essa Lista de permissões IP do Cloud Manager foi adicionada. Em seguida, aplique a lista ao ambiente de Autor *antes* de habilitar o pipeline.

Consulte [Aplicar Lista de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) e [Habilitar pipeline de front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md) para obter mais informações.

### O Editor Universal e as Listas de permissões de IP {#universal-editor}

Se você pretende usar o Editor universal para criar seu conteúdo, é necessário adicionar os endereços IP que o Serviço do editor universal usa a uma Lista de permissões e aplicá-la.

1. Recupere os endereços IP usados pelo Universal Editor Service do seguinte ponto de extremidade de API: `http://universal-editor-service.adobe.io/ip-ranges`.
1. Crie uma lista de permissões com esses endereços IP, nomeando-a como `Universal Editor Service` ou similar.
1. Aplicar a lista de permissões `Universal Editor Service`.

A lista de endereços IP usados pelo Universal Editor Service está sujeita a alterações e você deve atualizar sua lista de permissões adequadamente.
