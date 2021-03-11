---
title: Noções básicas sobre tipos de programas e programas
description: Noções básicas sobre tipos de programas e programas - Cloud Services
translation-type: tm+mt
source-git-commit: 5a4353cb31337882a1c13b0ed830ea64f617181a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 3%

---


# Noções básicas sobre programas e tipos de programas {#understanding-programs}

No Cloud Manager, você tem a entidade Locatário na parte superior, que pode ter vários programas. Cada Programa não pode conter mais de um ambiente de Produção e vários ambientes não relacionados à produção.

O diagrama a seguir mostra a hierarquia de entidades no Cloud Manager.

![imagem](assets/program-types1.png)

## Tipos de programas {#program-types}

Um usuário pode criar um programa de **Sandbox** ou **Produção**.

* Um *Programa de produção* é criado para ativar o tráfego ao vivo no momento adequado no futuro.
Consulte [Introdução aos programas de produção](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md) para obter mais detalhes.


* Um *Programa de sandbox* normalmente é criado para servir os propósitos de treinamento, execução de demonstração, ativação, POC&#39;s ou documentação. Não se destina a transportar tráfego vivo e terá restrições que um programa de produção não irá. Ele incluirá Sites e Ativos e será fornecido automaticamente com uma ramificação Git que inclui código de amostra, um ambiente de desenvolvimento e um pipeline não relacionado à produção.
Consulte [Introdução aos programas de sandbox](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) para obter mais detalhes.

