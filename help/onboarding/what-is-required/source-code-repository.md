---
title: Repositório de código fonte - Cloud Services
description: Repositório de código fonte - Cloud Services
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# Repositório de código-fonte {#source-code-repository}

O programa do Cloud Manager será provisionado automaticamente com seu próprio repositório git.

Para que um usuário acesse o repositório git do Cloud Manager, os usuários precisarão usar um cliente Git com uma ferramenta de linha de comando, um cliente Git visual independente ou o IDE do usuário, como Eclipse, IntelliJ e NetBeans.

Depois que um cliente Git é configurado, você pode gerenciar seu repositório git na interface do usuário do Cloud Manager. Para saber mais sobre como gerenciar o Git usando a interface do usuário do Cloud Manager, consulte [Acessando o Git](/help/implementing/cloud-manager/accessing-git.md).

Para começar a desenvolver o aplicativo AEM Cloud, é necessário fazer uma cópia local do código do aplicativo, fazendo o check-out do repositório do Cloud Manager para um local em seu computador local onde deseje criar seu repositório.

```java
$ git clone {URL}
```

>[!NOTE]
>
>Um usuário pode fazer check-out de uma cópia de seu código e fazer alterações no repositório de código local. Quando estiver pronto, o usuário poderá confirmar suas alterações de código de volta para o repositório de código remoto no Cloud Manager.
