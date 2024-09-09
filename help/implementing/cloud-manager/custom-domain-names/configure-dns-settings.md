---
title: Definição das configurações de DNS
description: Saiba como definir configurações de DNS para seus nomes de domínio personalizados permite que seu site receba visitantes.
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 49%

---


# Definição das configurações de DNS {#configure-dns}

Depois que o nome de domínio personalizado for [verificado e implantado com êxito](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md), você estará pronto para atualizar os registros DNS para o nome de domínio personalizado com o provedor de DNS. Isso permite que seu site receba visitantes. Portanto, essa atividade normalmente é feita antes de entrar em produção.

## O que são configurações de DNS? {#dns-settings}

Um registro `CNAME` ou A, uma vez provisionado, encaminhará todo o tráfego de Internet do domínio para onde quer que esteja apontando. Se esse local não for provisionado para veicular o tráfego, haverá uma interrupção. Se não for testado, poderá haver erros no conteúdo. É por isso que essa etapa é sempre realizada após a conclusão dos testes, quando você está pronto para entrar em produção.

Para definir essas configurações, você precisa determinar se um registro `CNAME` ou apex deve ser configurado para apontar seu nome de domínio personalizado para o nome de domínio do Cloud Manager. As seções a seguir deste documento ajudarão você a determinar qual tipo de registro é apropriado para sua configuração de DNS.

## Requisitos {#requirements}

Você deve atender a esses requisitos antes de configurar seus registros DNS.

* Você deve identificar o host ou o registrador do seu domínio, se não tiver essa informação.
* Você deve ser capaz de editar os registros DNS do domínio de sua organização ou entrar em contato com a pessoa apropriada que pode fazer isso.
* Você já deve ter verificado o nome de domínio personalizado configurado, conforme descrito no documento [Verificando o Status do Nome de Domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Registro CNAME {#cname-record}

Um nome canônico ou registro CNAME é um tipo de registro DNS que mapeia um nome de alias a um nome de domínio verdadeiro ou canônico. Os registros CNAME normalmente são usados para mapear um subdomínio como `www.example.com` ao domínio que hospeda o conteúdo desse subdomínio.

Faça logon no registrador de domínios e crie um registro `CNAME` para apontar seu nome de domínio personalizado ao destino, como na tabela a seguir.

| CNAME | Nome de domínio personalizado aponta para o Target |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## Registro APEX {#apex-record}

Um domínio apex é um domínio personalizado que não contém um subdomínio, como `example.com`. Um domínio apex é configurado com um registro `A`, `ALIAS` ou `ANAME` por meio do provedor de DNS. Domínios apex devem apontar para endereços IP específicos.

Adicione os seguintes registros `A` às configurações de DNS do domínio por meio do provedor de domínio.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

## Próximas etapas {#next-steps}

Depois de configurar os registros DNS para o nome de domínio personalizado, será necessário verificar essas configurações no Cloud Manager. Prossiga para o documento [Verificando o Status do Registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) para finalizar seu nome de domínio personalizado.
