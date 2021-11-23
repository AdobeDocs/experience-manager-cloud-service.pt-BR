---
title: Adicionar um registro TXT
description: Adicionar um nome de domínio personalizado
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 12849a79975f70dafd59f4b6ebf4b4ff24145cbf
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Adicionar um registro TXT {#adding-txt}

Um registro TXT DNS autoriza um Domínio a ser hospedado em um serviço CDN. O cliente deve criar um registro TXT de DNS na zona que autoriza o Cloud Manager a implantar o Serviço CDN com o domínio personalizado e associá-lo ao serviço de back-end. Essa associação está totalmente sob o controle do cliente e autoriza o Cloud Manager a veicular conteúdo do serviço para um domínio. Essa autorização pode ser concedida e retirada.

Você deve seguir as etapas abaixo antes de criar um registro TXT:

* Ter a capacidade de modificar os registros DNS para o domínio de sua organização ou entrar em contato com a pessoa adequada que puder.
* Identifique o host ou registrador do domínio se ainda não souber.

Ao iniciar a verificação de domínio, o Cloud Manager fornece o nome e o valor TXT a serem usados para verificação. Adicione um registro TXT ao servidor DNS do domínio usando o Nome e o Valor especificados.

1. Faça logon no Host de domínio e visite a seção Registros DNS .
1. Adicionar `_aemverification.[yourdomainname]` como o Nome e adicione o Valor TXT exatamente como aparece.
Consulte os exemplos na tabela abaixo.

| Domínio | Nome | Valor TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Copie o valor inteiro exibido na interface do usuário do Cloud Manager. Isso é específico para o domínio e o ambiente . Exemplo:<br>*adobe-aem-verify=example.com/[programa]/[env]/..* |
| `www.example.com` | `_aemverification.www.example.com` | Copie o valor inteiro exibido na interface do usuário do Cloud Manager. Isso é específico para o domínio e o ambiente . Exemplo:<br>*adobe-aem-verify=www.example.com/[programa]/[env]/..* |

Quando terminar, você poderá verificar o resultado executando: `dig _aemverification.[yourdomainname] -t txt`.
O resultado esperado deve exibir o valor TXT fornecido na interface do usuário do Cloud Manager.

Por exemplo, se o domínio for `example.com`e, em seguida, execute: `dig TXT _aemverification.example.com -t txt`.

>[!NOTE]
>Há também vários [Ferramentas de pesquisa DNS](https://www.ultratools.com/tools/dnsLookup), o Google DoH pode ser usado para pesquisar entradas de registro TXT e identificar se o registro TXT está ausente ou incorreto.
