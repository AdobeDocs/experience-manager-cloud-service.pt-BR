---
title: Gerenciamento de vários sites de resposta
description: Saiba mais sobre as práticas recomendadas de como configurar um projeto com sites multilíngues aproveitando uma única base de código de maneira imperceptível.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 02957fb8671d953a683ebd6e168979b11ad391c4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Gerenciamento de vários sites de resposta {#repoless-msm}

Este documento supõe que você já tenha criado um site base para o seu projeto chamado `my-aem-site` e deseja localizá-lo usando o recurso MSM do AEM.

Se você já configurou seu projeto para o caso de uso de resposta, a configuração de nuvem é atribuída no nível da página raiz, `/content/my-aem-site`. Para sites multilíngues, essa atribuição de configuração deve ser alterada para a raiz do idioma, como `/content/my-aem-site/language-master/de`.

