---
title: Noções básicas sobre tipos de programas e programas
description: Noções básicas sobre tipos de programas e programas - Cloud Services
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---


# Noções básicas sobre programas e tipos de programas {#understanding-programs}

No Cloud Manager, você tem a entidade Locatário na parte superior, que pode ter vários programas. Cada Programa não pode conter mais de um ambiente de Produção e vários ambientes não relacionados à produção.

O diagrama a seguir mostra a hierarquia de entidades no Cloud Manager.

![imagem](assets/program-types1.png)

## Repositório de código-fonte {#source-code-repository}

O programa do Cloud Manager será provisionado automaticamente com seu próprio repositório Git.

Para um usuário acessar o repositório Git do Cloud Manager, os usuários precisarão usar um cliente Git com uma ferramenta de linha de comando, um cliente Git visual independente ou o IDE do usuário, como Eclipse, IntelliJ, NetBeans.

Depois que um cliente Git é configurado, você pode gerenciar seu repositório Git na interface do usuário do Cloud Manager. Para saber mais sobre como gerenciar o Git usando a interface do usuário do Cloud Manager, consulte [Acesso ao Git](/help/implementing/cloud-manager/accessing-git.md).

Para começar a desenvolver o aplicativo AEM Cloud, uma cópia local do código do aplicativo deve ser feita verificando-o do repositório do Cloud Manager para um local em seu computador local onde deseje criar seu repositório.

```java
$ git clone {URL}
```

>[!NOTE]
>Um usuário pode fazer check-out de uma cópia de seu código e fazer alterações no repositório de código local. Quando pronto, o usuário pode confirmar as alterações de código no repositório de código remoto no Cloud Manager.

## Tipos de programas {#program-types}

Um usuário pode criar um programa de **Sandbox** ou **Produção**.

* Um *Programa de produção* é criado para ativar o tráfego ao vivo no momento adequado no futuro.
Consulte [Introdução aos programas de produção](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md) para obter mais detalhes.


* Um *Programa de sandbox* normalmente é criado para servir os propósitos de treinamento, execução de demonstração, ativação, POC&#39;s ou documentação. Não se destina a transportar tráfego vivo e terá restrições que um programa de produção não irá. Ele incluirá Sites e Ativos e será fornecido automaticamente com uma ramificação Git que inclui código de amostra, um ambiente de desenvolvimento e um pipeline não relacionado à produção.
Consulte [Introdução aos programas de sandbox](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) para obter mais detalhes.

