---
title: Verificar o status de um certificado SSL - Gerenciar certificados SSL
description: Verificar o status de um certificado SSL - Gerenciar certificados SSL
translation-type: tm+mt
source-git-commit: 0b04d43c8b5bb28286e616f0bd902c05ec56ec05
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# Verificando o status de um certificado SSL {#checking-status-an-ssl-certificate}

O status dos certificados SSL pode ser entendido rapidamente na página de certificado SSL.

Você pode identificar o status de um certificado SSL nos seguintes esquemas de cores:

* ****
VerdeIndica que o certificado é válido por, pelo menos, 60 dias no futuro.

* ****
LaranjaIndica que o certificado deve expirar em menos de 60 dias. É hora de garantir que você tenha um plano para renovar seu certificado e substituí-lo pela interface do usuário do Cloud Manager para evitar possíveis acessos ao site ou interrupções. O Cloud Manager enviará notificações regulares na interface do usuário para alertá-lo sobre uma expiração iminente de certificado.

* ****
VermelhoIndica que, apesar de várias notificações, seu certificado SSL expirou.

## Configurações de CDN pré-existentes para Listas de permissões IP {#pre-existing-cdn}

Os clientes com ambientes que incluem configurações de CDN pré-existentes para Listas de permissões de IP, certificados SSL ou Nomes de domínio personalizados verão a seguinte mensagem na página **Lista de permissões de IP** e **Ambiente** de detalhes. A mensagem exibida na interface do usuário desaparecerá assim que o cliente migrar totalmente todas as configurações de ambiente pré-existentes por meio da interface do usuário e talvez demore de 1 a 2 dias úteis para a mensagem desaparecer.

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>Para visualizar e gerenciar as configurações pré-existentes, elas devem ser adicionadas por meio da interface do usuário, como mostrado na figura abaixo.

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)