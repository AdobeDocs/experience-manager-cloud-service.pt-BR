---
title: Adicionar um registro TXT
description: Saiba como adicionar um registro TXT para adicionar um nome de domínio personalizado no Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 491e710223c5878bfa81c4b0a57d18ec0ec29479
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 4%

---

# Adicionar um registro TXT {#adding-txt}

Um registro TXT DNS autoriza um domínio a ser hospedado em um serviço CDN. Você deve criar um registro TXT de DNS na zona que autoriza o Cloud Manager a implantar o Serviço CDN com o domínio personalizado e associá-lo ao serviço de back-end. Essa associação está totalmente sob seu controle e autoriza o Cloud Manager a veicular conteúdo do serviço em um domínio. Esta autorização pode ser concedida e retirada. O registro TXT é específico para o domínio e o ambiente do Cloud Manager.

Você deve atender a esses requisitos antes de adicionar um registro TXT.

* Você deve ter a capacidade de modificar os registros DNS do domínio de sua organização ou entrar em contato com a pessoa adequada que puder.
* Você deve identificar o host ou registrador do domínio se ainda não souber.

Ao iniciar a verificação de domínio, o Cloud Manager fornece o nome e o valor TXT a serem usados para verificação. Adicione um registro TXT ao servidor DNS do domínio usando o nome e o valor especificados.

1. Faça logon no host de domínio e localize a seção Registros DNS .
1. Adicionar `_aemverification.[yourdomainname]` como **Nome** e adicione o valor TXT exatamente como aparece.

Consulte os exemplos nesta tabela.

| Domínio | Nome | Valor TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Copie o valor inteiro exibido na interface do usuário do Cloud Manager. Isso é específico para o domínio e o ambiente . Por exemplo:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Copie o valor inteiro exibido na interface do usuário do Cloud Manager. Isso é específico para o domínio e o ambiente . Por exemplo:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

Quando terminar, você poderá verificar o resultado executando o seguinte comando

```shell
dig _aemverification.[yourdomainname] -t txt
```

O resultado esperado deve exibir o valor TXT fornecido na interface do usuário do Cloud Manager.

Por exemplo, se o domínio for `example.com`e, em seguida, execute:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Há vários [Ferramentas de pesquisa DNS](https://www.ultratools.com/tools/dnsLookup) disponível. O Google DoH pode ser usado para pesquisar entradas de registro TXT e identificar se o registro TXT está ausente ou incorreto.
