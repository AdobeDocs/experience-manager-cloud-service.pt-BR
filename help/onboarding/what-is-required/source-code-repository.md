---
title: Repositório de código-fonte - Cloud Services
description: Repositório de código-fonte - Cloud Services
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# Repositório de código-fonte {#source-code-repository}

O programa do Cloud Manager será provisionado automaticamente com seu próprio repositório Git.

Para um usuário acessar o repositório Git do Cloud Manager, os usuários precisarão usar um cliente Git com uma ferramenta de linha de comando, um cliente Git visual independente ou o IDE do usuário, como Eclipse, IntelliJ, NetBeans.

Depois que um cliente Git é configurado, você pode gerenciar seu repositório Git na interface do usuário do Cloud Manager. Para saber mais sobre como gerenciar o Git usando a interface do usuário do Cloud Manager, consulte [Acesso ao Git](/help/implementing/cloud-manager/accessing-git.md).

Para começar a desenvolver o aplicativo AEM Cloud, uma cópia local do código do aplicativo deve ser feita verificando-o do repositório do Cloud Manager para um local em seu computador local onde deseje criar seu repositório.

```java
$ git clone {URL}
```

>[!NOTE]
>
>Um usuário pode fazer check-out de uma cópia de seu código e fazer alterações no repositório de código local. Quando pronto, o usuário pode confirmar as alterações de código no repositório de código remoto no Cloud Manager.
