---
title: Anotações de verificação do GitHub
description: Saiba como o GitHub verifica as PRs de anotação de seus repositórios privados para fornecer feedback útil.
exl-id: 15178de8-8a8a-4300-8510-88875ad0fc8c
source-git-commit: f7348d388918a31d255babcfb64b3dc547153d62
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Anotações de verificação do GitHub {#github-annotations}

Saiba como o GitHub verifica as PRs de anotação de seus repositórios privados para fornecer feedback útil.

## Visão geral {#overview}

Se você estiver usando [repositórios privados](private-repositories.md) para seu programa do Cloud Manager, as verificações no GitHub são executadas automaticamente para cada solicitação de pull. Eles são anotados com informações úteis para ajudar você a entender quaisquer problemas com seu código o mais rápido possível.

![Exemplo de anotações de verificação do GitHub](assets/github-check-annotations.png)

[Qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md) problemas detectados por [SonarQube](/help/implementing/cloud-manager/custom-code-quality-rules.md) estão claramente listados.

![Exemplo de anotação de problema de código](assets/github-check-annotations-example.png)

A linha exata de código com o problema é fornecida e você pode clicar nela para mostrar o código relevante. Essas anotações são fornecidas para todos os problemas de código, não apenas aqueles alterados na solicitação de pull.

![Exemplo de anotação de problema de código](assets/github-check-annotations-example-code.png)

Todas as linhas anotadas são agregadas no **Arquivos alterados** na solicitação de pull do GitHub. As anotações de arquivos que não foram alterados na solicitação de pull aparecem em sua própria seção.

![Exemplo de anotações na guia de arquivos alterados](assets/github-check-annotations-files-changed.png)

## Pipelines de qualidade de código {#code-quality-pipelines}

A variável [qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md) Os resultados também estão visíveis no pipeline, que é acionado automaticamente pelo Cloud Manager na parte inferior do **Verificações** guia. Também é acessível a partir do **Detalhes** da verificação da solicitação de pull.

![Exemplo de anotações](assets/github-check-annotations-code-quality.png)

![Exemplo de anotações](assets/github-check-annotations-code-quality-2.png)

Você também pode visualizar os problemas no formato de um CSV. Isto pode ser recuperado por [exibir os detalhes da execução do pipeline no Cloud Manager.](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)
