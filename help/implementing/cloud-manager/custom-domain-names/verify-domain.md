---
title: Verificando domínio
description: Verificando domínio
translation-type: tm+mt
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# Verificando Domínio {#verify-domain-name}

Um registro TXT DNS autoriza um Domínio a ser hospedado em um serviço CDN. O cliente deve criar um registro DNS TXT na zona que autoriza o Cloud Manager a implantar o serviço CDN com o domínio personalizado e associá-lo ao serviço de backend. Essa associação está totalmente sob o controle do cliente e autoriza o Cloud Manager a enviar conteúdo do serviço para um domínio. Essa autorização pode ser concedida e retirada. O registro TXT é específico para o domínio e o ambiente do Gerenciador de nuvem.

1. Efetue logon no Host de Domínio e visite a seção de registros DNS.
1. Copie e cole a entrada TXT na sua zona DNS onde seu domínio personalizado está localizado, exatamente como aparece. Se precisar de um &quot;nome&quot; para sua entrada, forneça `@`.

>[!NOTE]
>Várias ferramentas de pesquisa DNS, como [Ferramenta de pesquisa DNS](https://www.ultratools.com/tools/dnsLookup), o Google DoH pode ser usado para pesquisar entradas de registro TXT e identificar se o registro TXT está ausente ou errado.
