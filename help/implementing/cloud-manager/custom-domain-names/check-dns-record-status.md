---
title: Verificação de status do registro DNS
description: Saiba como determinar se as configurações de DNS são resolvidas corretamente usando o Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 06e961febd7cb2ea1d8fca00cb3dee7f7ca893c9
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 60%

---


# Verificação de status do registro DNS {#check-dns-record-status}

Saiba como determinar se as configurações de DNS são resolvidas corretamente usando o Cloud Manager.

## Status dos Registros DNS {#status}

Um nome de domínio personalizado não pode veicular o tráfego direto até que o DNS seja resolvido corretamente. No Cloud Manager, você pode determinar se o nome de domínio é resolvido corretamente para o seu site do AEM as a Cloud Service.

## Requisitos {#requirements}

Você deve atender a esses requisitos antes de verificar o status de um registro DNS usando o Cloud Manager.

* Você já deve ter definido as configurações de DNS para seu nome de domínio personalizado conforme descrito no documento [Definindo as Configurações de DNS.](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)

## Como verificar o status do registro DNS {#how-to}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Clique em **Configurações do domínio** no painel de navegação esquerdo.

1. Clique no ícone de **Status** do nome do domínio.

O Cloud Manager faz uma pesquisa de DNS pelo seu nome de domínio e exibe o [status atual.](#statuses)

O Cloud Manager acionará automaticamente uma consulta de DNS depois de o nome de domínio personalizado ter sido verificado e implantado com sucesso pela primeira vez. Para tentativas subsequentes, é necessário selecionar ativamente o ícone **Resolver novamente** ao lado do status.

## Status de DNS no Cloud Manager {#statuses}

Um domínio personalizado pode ter um dos seguintes status no Cloud Manager.

* **Status de DNS não detectado** - O status de DNS não será detectado até que o nome de domínio personalizado tenha sido verificado e implantado com êxito.

   * Esse status também é observado quando o nome de domínio personalizado está em processo de exclusão.

* **O DNS resolve incorretamente** - Indica que a configuração dos registros DNS não foi resolvida ou está incorreta.

   * Consulte [Definição das configurações de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para saber mais.
   * Quando estiver pronto, você deverá selecionar o ícone **Resolver novamente** ao lado do status.

* **Resolução DNS em andamento** - A resolução está em andamento.

   * Normalmente, esse status é exibido depois de selecionar o ícone **Resolver novamente** ao lado do status.

* **O DNS resolve corretamente** - Suas configurações de DNS estão configuradas corretamente.

   * Seu site está atendendo visitantes.

## Próximas etapas {#next-steps}

Parabéns! O domínio personalizado foi configurado com êxito para uso com o Cloud Manager. Consulte o documento [Gerenciando nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para obter detalhes sobre como gerenciar seus nomes de domínio personalizados usando o Cloud Manager.
