---
title: Manuseio da versão do projeto Maven
description: Manuseio da versão do projeto Maven - Cloud Services
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
source-git-commit: 21669a29fbfd1072b637f407f5220825c4d1edbb
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 5%

---

# Manuseio da versão do projeto Maven {#maven-project-version-handling}


## Noções básicas sobre o tratamento da versão do projeto Maven {#understanding-project-version}

Para implantações de estágio e produção, o Cloud Manager gera uma versão exclusiva que aumenta.

Essa versão é vista na página de detalhes de execução do pipeline, bem como na página de atividades. Quando uma build é executada, o projeto Maven é atualizado para usar esta versão e uma tag é criada no repositório Git com essa versão como seu nome.

Se a versão original do projeto atender a determinados critérios, a versão atualizada do projeto Maven mesclará a versão original do projeto e a versão gerada pelo Cloud Manager. No entanto, a tag sempre usa a versão gerada. Para que essa mesclagem ocorra, a versão original do projeto deve ser formada com exatamente três segmentos de versão, por exemplo, 1.0.0 ou 1.2.3, mas não 1.0 ou 1, e a versão original não deve terminar em -SNAPSHOT.

>[!NOTE]
>O valor da versão original do projeto deve ser definido estaticamente no elemento `<version>` do arquivo de nível superior `pom.xml` na ramificação do repositório Git.

Se a versão original atender a esses critérios, a versão gerada será anexada à versão original como um novo segmento de versão. A versão gerada também será ligeiramente modificada para incluir a classificação correta e o manuseio de versão. Por exemplo, pressupondo uma versão gerada de 2019.926.121356.0000020490:

| **Versão** | **versão em pom.xml** | **Comentário** |
|---|---|---|
| 1.0.0 | 1.0.0.2019_0926_121356_000020490 | Versão original corretamente formada |
| 1.0.0-SNAPSHOT | 2019.926.121356.000020490 | Versão do instantâneo, substituída |
| 1 | 2019.926.121356.000020490 | Versão incompleta, substituída |

>[!NOTE]
>
>Independentemente de a versão original ter ou não sido incorporada à versão inicializada do Cloud Manager, a versão original está disponível como uma propriedade Maven com o nome *cloudManagerOriginalVersion.*
