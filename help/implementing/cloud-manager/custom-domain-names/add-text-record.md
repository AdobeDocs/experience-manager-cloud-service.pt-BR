---
title: Adicionando um registro TXT
description: Adicionando um nome de domínio personalizado
translation-type: tm+mt
source-git-commit: b76a22469f248dde316dcaa514a906fe4361afd1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Adicionando um registro TXT {#adding-txt}

Um registro TXT DNS autoriza um Domínio a ser hospedado em um serviço CDN. O cliente deve criar um registro DNS TXT na zona que autoriza o Cloud Manager a implantar o serviço CDN com o domínio personalizado e associá-lo ao serviço de backend. Essa associação está totalmente sob o controle do cliente e autoriza o Cloud Manager a enviar conteúdo do serviço para um domínio. Essa autorização pode ser concedida e retirada.

Você deve seguir as etapas abaixo antes de criar um registro TXT:

* Ter a capacidade de modificar os registros DNS para o domínio de sua organização ou entrar em contato com a pessoa adequada que puder.
* Identifique o host ou registrador do domínio se você já não souber.

Ao iniciar a verificação de domínio, o Cloud Manager fornece o nome e o valor TXT a serem usados para verificação. Adicione um registro TXT ao servidor DNS do seu domínio usando o Nome e o Valor especificados.

1. Efetue logon no Host de Domínio e visite a seção de registros DNS.
1. Adicione `_aemverification.[yourdomainname]` como o Nome e adicione o Valor TXT exatamente como ele aparece.
Consulte os exemplos na tabela abaixo.

| Domínio | Nome | Valor TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Exibida na interface do usuário do Cloud Manager e é específica do domínio e do ambiente do Cloud Manager |
| `test.example.com` | `_aemverification.test.example.com` | Exibida na interface do usuário do Cloud Manager e é específica do domínio e do ambiente do Cloud Manager |

Quando terminar, você pode verificar o resultado executando: `dig _aemverification.[yourdomainname] -t txt`.
O resultado esperado deve exibir o valor TXT fornecido na interface do usuário do Cloud Manager.

Por exemplo, se seu domínio for `example.com`, execute: `dig TXT _aemverification.example.com -t txt`.

>[!NOTE]
>Há também várias [ferramentas de pesquisa DNS](https://www.ultratools.com/tools/dnsLookup), o Google DoH pode ser usado para pesquisar entradas de registro TXT e identificar se o registro TXT está ausente ou errado.

