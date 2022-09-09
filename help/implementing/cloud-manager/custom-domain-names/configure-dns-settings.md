---
title: Definição das configurações de DNS
description: Definição das configurações de DNS
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 60b496024b3d012033309632999851c08f43c5d7
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# Definição das configurações de DNS {#configure-dns}

Depois que seu nome de domínio personalizado for verificado e implantado com êxito, você estará pronto para atualizar os registros DNS para seu nome de domínio personalizado com seu provedor DNS. Isso permite que seu site forneça visitantes. Portanto, essa atividade normalmente é feita antes de entrar em funcionamento.

## O que são Configurações de DNS? {#dns-settings}

A `CNAME` ou Um registro, uma vez provisionado, roteará todo o tráfego da Internet do domínio para onde ele estiver apontando. Se esse local não for provisionado para veicular o tráfego, haverá uma interrupção. Se não tiver sido testado, pode haver erros no conteúdo. É por isso que essa etapa é sempre feita após a conclusão do teste e que você está pronto para entrar em funcionamento.

Para definir essas configurações, é necessário determinar se uma `CNAME` ou o registro Apex deve ser configurado para apontar seu nome de domínio personalizado para o nome de domínio do Cloud Manager. As seções a seguir ajudarão você a determinar qual tipo de registro é apropriado para sua configuração de DNS.

>[!NOTE]
>
>Você ou o indivíduo apropriado em sua organização devem ser capazes de fazer logon ou entrar em contato com seu provedor de DNS (a empresa da qual você comprou o domínio) e fazer atualizações nas configurações de DNS.

## Registro CNAME {#cname-record}

Um nome canônico ou registro CNAME é um tipo de registro DNS que mapeia um nome de alias para um nome de domínio verdadeiro ou canônico. Os registros CNAME normalmente são usados para mapear um subdomínio como `www.example.com` ao domínio que hospeda o conteúdo desse subdomínio.

Faça logon no registrador de domínios e crie um `CNAME` registre para apontar seu nome de domínio personalizado para o público-alvo, como na tabela a seguir.

| CNAME | Ponto de Nome de Domínio Personalizado para Destino |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## Registro APEX {#apex-record}

Um domínio anexado é um domínio personalizado que não contém um subdomínio, como `example.com`. Um domínio anexado é configurado com um `A` , `ALIAS` ou `ANAME` registre por meio do provedor DNS. Domínios anexados devem apontar para endereços IP específicos.

Adicione todos os itens a seguir `A` registra nas configurações DNS do domínio por meio do provedor de domínio.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
