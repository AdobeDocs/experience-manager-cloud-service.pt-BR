---
title: Verificando o status de um certificado SSL - Gerenciando certificados SSL
description: Verificando o status de um certificado SSL - Gerenciando certificados SSL
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Verificando o status de um certificado SSL {#checking-status-an-ssl-certificate}

O status dos certificados SSL pode ser entendido rapidamente na página de certificado SSL ou na página de detalhes do Ambiente.

Você pode identificar o status de um certificado SSL dos seguintes esquemas de cores:

* **Verde** Indica que seu certificado é válido por pelo menos 60 dias no futuro.

* **Laranja** Indica que seu certificado deve expirar em menos de 60 dias. É hora de garantir que você tenha um plano para renovar seu certificado e substituí-lo pela interface do usuário do Cloud Manager, a fim de evitar possíveis acessos ou interrupções no site. O Cloud Manager enviará notificações regulares na interface do usuário para alertá-lo sobre uma expiração iminente do certificado.

* **Vermelho** Indica que, apesar de várias notificações, seu certificado SSL expirou.