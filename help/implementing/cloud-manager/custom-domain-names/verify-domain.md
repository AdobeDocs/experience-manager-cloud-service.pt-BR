---
title: Verificar Domínio
description: Verificar Domínio
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# Verificar Domínio {#verify-domain-name}

Um registro TXT DNS autoriza um Domínio a ser hospedado em um serviço CDN. O cliente deve criar um registro TXT de DNS na zona que autoriza o Cloud Manager a implantar o Serviço CDN com o domínio personalizado e associá-lo ao serviço de back-end. Essa associação está totalmente sob o controle do cliente e autoriza o Cloud Manager a veicular conteúdo do serviço para um domínio. Essa autorização pode ser concedida e retirada. O registro TXT é específico para o domínio e o ambiente do Cloud Manager.

1. Faça logon no Host de domínio e visite a seção Registros DNS .
1. Copie e cole a entrada TXT em sua zona DNS, onde seu domínio personalizado está localizado, exatamente como aparece. Se precisar de um &quot;nome&quot; para a entrada, forneça-o `@`.

>[!NOTE]
>Várias ferramentas de pesquisa de DNS, como [Ferramenta de pesquisa DNS](https://www.ultratools.com/tools/dnsLookup), o Google DoH pode ser usado para pesquisar entradas de registro TXT e identificar se o registro TXT está ausente ou incorreto.
