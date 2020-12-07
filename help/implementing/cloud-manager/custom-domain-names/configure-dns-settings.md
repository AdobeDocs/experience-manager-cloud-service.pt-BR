---
title: 'Configuração de configurações DNS '
description: Configuração de configurações DNS
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Configuração de configurações DNS {#configure-dns}

Depois que seu nome de domínio personalizado for verificado e implantado com êxito, você estará pronto para atualizar os registros de DNS para seu nome de domínio personalizado com seu provedor DNS. Isso permite que seu site sirva visitantes. Esta atividade é, portanto, tipicamente feita antes do Go-live.

>[!NOTE]
>Você ou o indivíduo apropriado em sua organização deve poder fazer logon ou entrar em contato com seu provedor DNS (a empresa da qual você adquiriu o domínio) e fazer atualizações nas configurações de DNS.

Para fazer isso, você deve determinar se deve configurar suas configurações de DNS para um `CNAME` ou registro Apex apontando seu nome de domínio personalizado para o nome de domínio do Cloud Manager. Um registro `CNAME` ou A, uma vez provisionado, roteará todo o tráfego da Internet do domínio para onde ele estiver apontando. Se esse local não for provisionado para servir o tráfego, haverá uma interrupção. Se não tiver sido testado, pode haver erros no conteúdo. É por isso que essa etapa é sempre realizada depois que o teste é concluído e o cliente está pronto para o Go-live.

## Registro CNAME {#cname-record}

As seções a seguir ajudarão você a determinar que tipo de registro é apropriado para sua configuração de DNS.

Um registro Canonical Name ou `CNAME` é um tipo de registro DNS que mapeia um nome de alias para um nome de domínio verdadeiro ou canônico. Os registros CNAME são normalmente usados para mapear um subdomínio como `www.example.com` para o domínio que hospeda o conteúdo desse subdomínio.

Faça logon no Registrador de domínio e crie um registro CNAME para apontar seu nome de domínio personalizado para o público alvo, como mostrado abaixo:

| CNAME | Ponto de nome de domínio personalizado para Público alvo |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## Registro APEX {#apex-record}

Um domínio de ápice é um domínio personalizado que não contém um subdomínio, como example.com. Um domínio de ápice está configurado com um registro `A`, `ALIAS` ou `ANAME` através do seu provedor DNS. Os domínios Apex devem apontar para endereços IP específicos.

Adicione todos os seguintes registros A às configurações de DNS do Domínio por meio do provedor de domínio:

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
