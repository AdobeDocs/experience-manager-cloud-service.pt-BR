---
title: Adicionar um registro TXT
description: Saiba como adicionar um registro TXT para verificar a propriedade de um domínio personalizado para uso com o Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 28%

---


# Adicionar um registro TXT {#adding-txt}

Saiba como adicionar um registro TXT para verificar a propriedade de um domínio personalizado para uso com o Cloud Manager.

## O que é um registro TXT? {#what-is}

Um registro de texto (também conhecido como registro TXT) é um tipo de registro de recurso no Sistema de nomes de domínio (DNS). Ele oferece a capacidade de associar texto arbitrário a um nome de host, como informações legíveis sobre um nome de host, como informações de servidor ou de rede.

O Cloud Manager usa um registro TXT específico para autorizar que um domínio seja hospedado em um serviço CDN. Você deve criar um registro TXT de DNS na zona que autoriza o Cloud Manager a implantar o serviço CDN no domínio personalizado e associá-lo ao serviço de back-end. Essa associação está totalmente sob seu controle e autoriza o Cloud Manager a veicular conteúdo do serviço em um domínio. Esta autorização pode ser concedida e retirada. O registro TXT é específico do domínio e do ambiente Cloud Manager.

## Requisitos {#requirements}

Você deve atender aos requisitos a seguir para adicionar um registro TXT.

* Você deve identificar o host ou o registrador do seu domínio, se não tiver essa informação.
* Você deve ser capaz de editar os registros DNS do domínio de sua organização ou entrar em contato com a pessoa apropriada que pode fazer isso.
* Primeiro, adicione um nome de domínio personalizado conforme descrito no documento [Adicionando um Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Adicionar um registro TXT para verificação {#verification}

Um registro TXT é adicionado como parte da verificação de um nome de domínio personalizado a ser usado com o Cloud Manager.

1. Primeiro, adicione um nome de domínio personalizado conforme descrito no documento [Adicionando um Nome de Domínio Personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Na guia **Verificação** da caixa de diálogo **Adicionar nome de domínio**, o Cloud Manager exibe o nome e o valor TXT a serem usados para verificação. Copie este valor.

   ![Verificação do nome de domínio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

1. Faça logon no host do domínio e localize a seção Registros DNS.

1. Adicione `_aemverification.[yourdomainname]` como o **Nome** do valor e adicione o valor TXT exatamente como ele aparece na caixa de diálogo **Adicionar Nome de Domínio**.

   * Veja os [exemplos na seção a seguir](#examples).

1. Salve o registro TXT no host do domínio.

## Exemplos de registro TXT {#examples}

| Domínio | Nome | Valor TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Copie todo o valor mostrado na interface do usuário do Cloud Manager. Isso é específico do domínio e do ambiente. Por exemplo:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Copie todo o valor mostrado na interface do usuário do Cloud Manager. Isso é específico do domínio e do ambiente. Por exemplo:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

## Verificar registro TXT {#verify}

Quando terminar, você poderá verificar o resultado executando o comando a seguir.

```shell
dig _aemverification.[yourdomainname] -t txt
```

O resultado esperado deve exibir o valor TXT fornecido na guia **Verificação** da caixa de diálogo **Adicionar nome de domínio** da interface do usuário do Cloud Manager.

Por exemplo, se o domínio for `example.com`, execute:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Há várias [ferramentas de pesquisa de DNS](https://www.ultratools.com/tools/dnsLookup) disponíveis. O Google DoH pode ser usado para pesquisar entradas no registro TXT e identificar se o registro TXT está ausente ou incorreto.

>[!NOTE]
>
>A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.
>
>O Cloud Manager verificará a propriedade e atualizará o status que pode ser visto na Tabela de configurações do domínio. Consulte [Verificar o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.

## Próximas etapas {#next-steps}

Agora que você criou a entrada TXT, é possível verificar o status do nome de domínio. Prossiga para o documento [Verificando o Status do Nome de Domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para continuar configurando seu nome de domínio personalizado.

>[!TIP]
>
>A entrada TXT e o registro CNAME ou A podem ser definidos simultaneamente no servidor DNS regulador, economizando tempo.
>
>Se desejar fazer isso, primeiro revise todo o processo de configuração de um nome de domínio personalizado, conforme detalhado no documento [Introdução a nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md), tomando uma observação especial do documento [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) e atualize suas configurações de DNS adequadamente.