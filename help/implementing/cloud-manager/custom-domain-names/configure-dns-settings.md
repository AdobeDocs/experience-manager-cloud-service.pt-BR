---
title: Definição das configurações de DNS
description: Definição das configurações de DNS
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 87%

---

# Definição das configurações de DNS {#configure-dns}

Uma vez verificado e implantado com sucesso seu nome de domínio personalizado, você estará pronto para atualizar os registros DNS para seu nome de domínio personalizado junto ao seu provedor de DNS. Isso permite que seu site receba visitantes. Portanto, essa atividade normalmente é feita antes de entrar em produção.

## O que são configurações de DNS? {#dns-settings}

Um `CNAME` ou um registro, uma vez provisionado, encaminhará todo o tráfego de Internet do domínio para onde quer que esteja apontando. Se esse local não for provisionado para veicular o tráfego, haverá uma interrupção. Se não for testado, poderá haver erros no conteúdo. É por isso que essa etapa é sempre realizada após a conclusão dos testes, quando você está pronto para entrar em produção.

Para definir essas configurações, é necessário determinar se uma `CNAME` O registro apex deve ser configurado para apontar seu nome de domínio personalizado para o nome de domínio do Cloud Manager. As seções a seguir ajudarão você a determinar qual tipo de registro é apropriado para sua configuração de DNS.

>[!NOTE]
>
>Você ou o indivíduo apropriado em sua organização devem poder fazer logon ou entrar em contato com o provedor de DNS (a empresa da qual você comprou o domínio) e fazer atualizações nas configurações de DNS.

## Registro CNAME {#cname-record}

Um nome canônico ou registro CNAME é um tipo de registro DNS que mapeia um nome de alias a um nome de domínio verdadeiro ou canônico. Os registros CNAME normalmente são usados para mapear um subdomínio como `www.example.com` ao domínio que hospeda o conteúdo desse subdomínio.

Faça logon no registrador de domínios e crie um registro `CNAME` para apontar seu nome de domínio personalizado ao destino, como na tabela a seguir.

| CNAME | Nome de domínio personalizado aponta para o Target |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## Registro APEX {#apex-record}

Um domínio apex é um domínio personalizado que não contém um subdomínio, como `example.com`. Um domínio apex é configurado com um registro `A`, `ALIAS` ou `ANAME` por meio do provedor de DNS. Domínios apex devem apontar para endereços IP específicos.

Adicione todos os registros `A` a seguir nas configurações de DNS do domínio por meio do provedor de domínio.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
