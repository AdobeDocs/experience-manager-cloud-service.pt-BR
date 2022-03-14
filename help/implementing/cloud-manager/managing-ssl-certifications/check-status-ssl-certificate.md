---
title: Verificar o status de um certificado SSL - Gerenciar certificados SSL
description: Verificar o status de um certificado SSL - Gerenciar certificados SSL
exl-id: 59d81356-2fa9-43db-bfa5-c2896c530eaa
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---

# Verificação de status de um certificado SSL {#checking-status-an-ssl-certificate}

O status dos certificados SSL pode ser entendido rapidamente na página de certificado SSL.

Você pode identificar o status de um certificado SSL nos seguintes esquemas de cores:

* **Verde**
Indica que o certificado é válido por, pelo menos, 60 dias no futuro.

* **Laranja**
Indica que o certificado deve expirar em menos de 60 dias. É hora de garantir que você tenha um plano para renovar seu certificado e substituí-lo pela interface do usuário do Cloud Manager para evitar possíveis acessos ao site ou interrupções. O Cloud Manager enviará notificações regulares na interface do usuário para alertá-lo sobre uma expiração iminente de certificado.

* **Vermelho**
Indica que, apesar de várias notificações, seu certificado SSL expirou.

## Configurações pré-existentes da CDN {#pre-existing-cdn}

Os clientes com ambientes que incluem configurações de CDN pré-existentes para Listas de permissões de IP, certificados SSL ou nomes de domínio personalizados verão a seguinte mensagem na **LISTA DE PERMISSÕES IP** e **Ambiente** página de detalhes. A mensagem exibida na interface do usuário desaparecerá assim que o cliente migrar totalmente todas as configurações de ambiente pré-existentes por meio da interface do usuário e talvez demore de 1 a 2 dias úteis para a mensagem desaparecer.

>[!NOTE]
>Para visualizar e gerenciar as configurações pré-existentes, elas devem ser adicionadas por meio da interface do usuário. Consulte [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obter mais detalhes.

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
