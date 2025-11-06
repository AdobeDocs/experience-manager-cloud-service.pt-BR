---
title: Verificar status do registro DNS
description: Saiba como determinar se as configurações de DNS são resolvidas corretamente usando o Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 24%

---


# Verificar o status do registro DNS {#check-dns-record-status}

Saiba como determinar se as configurações de DNS são resolvidas corretamente usando o Cloud Manager.

## Status dos registros DNS {#status}

Um nome de domínio personalizado não pode veicular o tráfego direto até que o DNS seja resolvido corretamente. No Cloud Manager, você pode determinar se o nome de domínio é resolvido corretamente para o site da AEM as a Cloud Service.

## Requisitos {#requirements}

Atenda a esses requisitos antes de verificar o status de um registro DNS usando o Cloud Manager.

Você já deve ter definido as configurações de DNS para seu nome de domínio personalizado conforme descrito em [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Verificar o status do registro DNS {#how-to}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Clique em **Configurações do domínio** no menu do lado esquerdo.

1. Clique no ícone de **Status** do nome do domínio.

O Cloud Manager faz uma pesquisa de DNS pelo seu nome de domínio e exibe [o status atual](#statuses).

O Cloud Manager aciona automaticamente uma pesquisa de DNS quando o nome de domínio personalizado é verificado e implantado pela primeira vez com êxito. Para tentativas subsequentes, é necessário selecionar ativamente o ícone **Resolver novamente** ao lado do status.

## Status de DNS no Cloud Manager {#statuses}

Um domínio personalizado pode ter um dos seguintes status no Cloud Manager.

| Status | Descrição |
| --- | --- |
| Status do DNS não detectado | O status do DNS não é detectado até que o nome de domínio personalizado seja verificado e implantado com êxito. Esse status também é observado quando o nome de domínio personalizado está em processo de exclusão. |
| O DNS não foi resolvido corretamente | Esse status indica que a configuração dos registros DNS não foi resolvida ou está incorreta. Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para saber mais.<br>Quando estiver pronto, você deverá selecionar o ícone **Resolver Novamente** ao lado do status. |
| Resolução DNS em andamento | A resolução está em andamento. Normalmente, esse status é exibido depois de selecionar o ícone **Resolver novamente** ao lado do status. |
| O DNS foi resolvido corretamente | Suas configurações de DNS estão definidas corretamente. Seu site está atendendo visitantes. |

## Próximas etapas {#next-steps}

O domínio personalizado foi configurado com êxito para uso com o Cloud Manager. Consulte o documento [Gerenciar nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para obter detalhes sobre como gerenciar seus nomes de domínio personalizados usando o Cloud Manager.
