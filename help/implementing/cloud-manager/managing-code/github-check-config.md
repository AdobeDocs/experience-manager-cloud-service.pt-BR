---
title: Configuração de verificação do GitHub para repositórios privados
description: Saiba como controlar os pipelines criados automaticamente para validar cada solicitação de pull para um repositório privado.
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 6eabf593a7566129d32d9a5888cc480117bef51f
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 63%

---

# Configuração de verificação do GitHub para repositórios privados {#github-check-config}

Saiba como controlar os pipelines criados automaticamente para validar cada solicitação de pull para um repositório privado.

## Configuração das verificações do GitHub {#configuration}

Ao usar [repositórios privados](private-repositories.md#using), um [pipeline de qualidade de código de pilha completa](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) será criado automaticamente. Esse pipeline é iniciado a cada atualização de solicitação de pull.

Você pode controlar essas verificações criando um arquivo `.cloudmanager/pr_pipelines.yml` na ramificação padrão do repositório privado.

```yaml
github:
  shouldDeletePreviousComment: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR 
    importantMetricsFailureBehavior: CONTINUE
```

| Parâmetro | Valores possíveis | Padrão | Descrição |
|---|---|---|---|
| `shouldDeletePreviousComment` | `true` ou `false` | `false` | Seja para manter apenas o último comentário com os resultados da verificação de código nesta solicitação pull do GitHub ou manter todos |
| `type` | `CI_CD` | n/a | Define o comportamento de um pipeline de CI/CD |
| `template.programID` | Número inteiro | Nenhuma variável de pipeline é reutilizada | Você pode usá-lo para reutilizar as [variáveis de pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) definidas em um pipeline existente criado automaticamente por cada solicitação pull. |
| `template.pipelineID` | Número inteiro | Nenhuma variável de pipeline é reutilizada | Você pode usá-lo para reutilizar as [variáveis de pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) definidas em um pipeline existente criado automaticamente por cada solicitação pull. |
| `namePrefix` | String | `Full Stack Code Quality Pipeline for PR` | Usado para definir o nome do pipeline criado automaticamente |
| `importantMetricsFailureBehavior` | `CONTINUE` ou `FAIL` ou `PAUSE` | `CONTINUE` | Define o comportamento de métrica importante do pipeline <br>`CONTINUE` = Se uma métrica importante falhar, o pipeline se move automaticamente <br>`FAIL` = O pipeline termina com um status FALHA se uma métrica importante falhar <br>`PAUSE` = A etapa de verificação de código recebe um status DE ESPERA quando uma métrica importante falha e deve ser retomada manualmente |
