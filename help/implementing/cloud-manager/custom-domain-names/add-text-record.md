---
title: Adicionar um registro TXT
description: Saiba como adicionar um registro TXT para adicionar um nome de domínio personalizado no Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 91%

---

# Adicionar um registro TXT {#adding-txt}

Um registro TXT de DNS autoriza um domínio a ser hospedado em um serviço CDN. Você deve criar um registro TXT de DNS na zona que autoriza o Cloud Manager a implantar o Serviço CDN no domínio personalizado e associá-lo ao serviço de back-end. Essa associação está totalmente sob seu controle e autoriza o Cloud Manager a veicular conteúdo do serviço em um domínio. Esta autorização pode ser concedida e retirada. O registro TXT é específico do domínio e do ambiente do Cloud Manager.

Você deve atender aos requisitos a seguir para adicionar um registro TXT.

* Você deve ser capaz de editar os registros DNS do domínio de sua organização ou entrar em contato com a pessoa apropriada que pode fazer isso.
* Você deve identificar o host ou o registrador do seu domínio, se não tiver essa informação.

Ao iniciar a verificação de domínio, o Cloud Manager fornece o nome e o valor TXT a serem usados para verificação. Adicione um registro TXT ao servidor DNS do domínio usando o nome e o valor especificados.

1. Faça logon no host do domínio e localize a seção Registros DNS.
1. Adicione `_aemverification.[yourdomainname]` como valor **Nome** e adicione o valor TXT exatamente como mostrado.

Consulte os exemplos nesta tabela.

| Domínio | Nome | Valor TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Copie todo o valor mostrado na interface do usuário do Cloud Manager. Isso é específico do domínio e do ambiente. Por exemplo:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Copie todo o valor mostrado na interface do usuário do Cloud Manager. Isso é específico do domínio e do ambiente. Por exemplo:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

Quando você terminar, poderá verificar o resultado executando o seguinte comando

```shell
dig _aemverification.[yourdomainname] -t txt
```

O resultado esperado deve mostrar o valor TXT fornecido na interface do usuário do Cloud Manager.

Por exemplo, se o domínio for `example.com`, execute:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Há vários [Ferramentas de pesquisa de DNS](https://www.ultratools.com/tools/dnsLookup) disponíveis. O Google DoH pode ser usado para pesquisar entradas no registro TXT e identificar se o registro TXT está ausente ou incorreto.
