---
title: Manuseio da versão do projeto Maven
description: Para implantações de preparo e produção do AEM as a Cloud Service, o Cloud Manager gera uma versão exclusiva com incremento numérico.
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 100%

---


# Manuseio da versão do projeto Maven {#maven-project-version-handling}

Para implantações de preparo e produção do AEM as a Cloud Service, o Cloud Manager gera uma versão exclusiva com incremento numérico

Essa versão é exibida na [página de detalhes de execução do pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) e na página de atividades. Quando uma compilação é executada, o projeto Maven é atualizado para usar a versão e uma tag é criada no repositório Git levando essa versão em seu nome.

Se a versão original do projeto atender a determinados critérios, a versão atualizada do projeto Maven mesclará a versão original do projeto e a versão gerada pelo Cloud Manager. No entanto, a tag sempre usará a versão gerada. Para que essa mesclagem ocorra, a versão original do projeto deve ser formada com exatamente três segmentos de versão, por exemplo, `1.0.0` ou `1.2.3`, mas não `1.0` ou `1`, e a versão original não deve terminar em `-SNAPSHOT`.

>[!IMPORTANT]
>
>O valor da versão original do projeto deve ser definido de forma estática no elemento `<version>` do arquivo principal `pom.xml` na ramificação do repositório Git.

Se a versão original atender a esses critérios, a versão gerada será anexada à versão original como um novo segmento de versão. A versão gerada também será ligeiramente modificada para incluir a classificação correta e o manuseio de versão. Por exemplo, assumindo uma versão gerada de `2019.926.121356.0000020490`, os resultados a seguir seriam obtidos.

| Versão | Versão em `pom.xml` | Comentar |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | Versão original corretamente formada |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | Versão de instantâneo, substituída |
| `1` | `2019.926.121356.0000020490` | Versão incompleta, substituída |

>[!NOTE]
>
>Independentemente de a versão original ter ou não sido incorporada à versão inicializada pelo Cloud Manager, a versão original estará disponível como uma propriedade do Maven com o nome `cloudManagerOriginalVersion`.
