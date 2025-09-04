---
title: Verificações de solicitação de pull para repositórios privados
description: Saiba como controlar os pipelines criados automaticamente para validar cada solicitação de pull para um repositório privado.
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0ec47218d598aad6b225a9d5d8faeab20e606716
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 28%

---

# Verificações de solicitação de pull para repositórios privados {#github-check-config}

Saiba como controlar os pipelines criados automaticamente para validar cada solicitação de pull para um repositório privado.

## Configuração de verificações de repositório privado {#configuration}

Ao usar [repositórios privados](private-repositories.md#using), um [pipeline de qualidade de código de pilha completa](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) será criado automaticamente. Esse pipeline é iniciado a cada atualização de solicitação de pull.

Você pode controlar essas verificações criando um arquivo de configuração `.cloudmanager/pr_pipelines.yml` na ramificação padrão do repositório privado.

```yaml
pullRequest:
  shouldDeletePreviousComment: false
  shouldSkipCheckAnnotations: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR
    importantMetricsFailureBehavior: CONTINUE
```

| Parâmetro | Valores possíveis | Padrão | Descrição |
| --- | --- | --- | --- |
| `shouldDeletePreviousComment` | `true` ou `false` | `false` | Se deseja manter somente o último comentário com os resultados da verificação de código nesta solicitação de pull do GitHub ou manter todos. Configurar como `false` (padrão) significa que os comentários anteriores não serão excluídos. |
| `shouldSkipCheckAnnotations` | `true` ou `false` | `false` | Se anotações adicionais devem estar presentes na verificação de solicitação de pull do GitHub ou não. Configurar como `false` (padrão) significa que as anotações de verificação não são ignoradas e são incluídas no feedback. |
| `type` | `CI_CD` | n/d | Define o comportamento das configurações de pipeline de CI/CD (Integração contínua/Implantação contínua). |
| `template.programId` | Número inteiro | Nenhuma variável de pipeline é reutilizada | Você pode usá-lo para reutilizar as [variáveis de pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) definidas em um pipeline existente criado automaticamente por cada solicitação pull. |
| `template.pipelineId` | Número inteiro | Nenhuma variável de pipeline é reutilizada | Você pode usá-lo para reutilizar as [variáveis de pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) definidas em um pipeline existente criado automaticamente por cada solicitação pull. |
| `namePrefix` | String | `Full Stack Code Quality Pipeline for PR` | Usado para definir o prefixo do nome do pipeline que é criado automaticamente. |
| `importantMetricsFailureBehavior` | `CONTINUE` ou `FAIL` ou `PAUSE` | `CONTINUE` | Define o comportamento de métrica importante do pipeline <br>`CONTINUE` = Se uma métrica importante falhar, o pipeline se move automaticamente <br>`FAIL` = O pipeline termina com um status FALHA se uma métrica importante falhar <br>`PAUSE` = A etapa de verificação de código recebe um status DE ESPERA quando uma métrica importante falha e deve ser retomada manualmente |




