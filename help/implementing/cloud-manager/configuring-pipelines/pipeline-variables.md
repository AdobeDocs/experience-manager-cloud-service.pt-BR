---
title: Configuração de variáveis de pipeline
description: Saiba como você pode usar variáveis de pipeline no Cloud Manager para gerenciar variáveis de configuração específicas para a sua build.
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 20%

---

# Configuração de variáveis de pipeline {#configuring-pipeline-variables}

Seu processo de compilação pode depender de variáveis de configuração específicas que seriam inadequadas para colocar no repositório Git, ou você pode precisar variá-las entre as execuções de pipeline que usam a mesma ramificação. O Cloud Manager permite gerenciar esses dados como variáveis de pipeline.

## Variáveis de pipeline {#pipeline-variables}

Com o Cloud Manager, você pode configurar variáveis de pipeline de várias maneiras diferentes.

* [Pela interface do usuário do Cloud Manager](#ui)
* [Uso da CLI do Cloud Manager](#cli)
* [Usando a API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

As variáveis podem ser armazenadas como texto simples ou criptografadas em repouso. Em ambos os casos, as variáveis são disponibilizadas no ambiente de compilação como variáveis de ambiente que podem ser referenciadas no arquivo `pom.xml` ou em outros scripts de compilação.

### Convenções de nomenclatura de variáveis de pipeline {#naming-conventions}

Os nomes das variáveis devem observar as convenções a seguir.

* As variáveis podem conter somente caracteres alfanuméricos e sublinhado (`_`).
* Os nomes devem estar em maiúsculas.
* Há um limite de 200 variáveis por pipeline.
* Cada nome deve ter 100 caracteres ou menos.
* Cada valor de variável `string` deve ter menos de 2048 caracteres.
* Cada valor de tipo de variável `secretString` deve ter 500 caracteres ou menos.

## Pela interface do usuário do Cloud Manager {#ui}

As variáveis de pipeline podem ser configuradas e gerenciadas por meio da interface do Cloud Manager. Você deve ter permissões para editar o pipeline a fim de adicionar, editar e excluir variáveis de pipeline.

Se um pipeline estiver em execução, o gerenciamento de variáveis será bloqueado.

### Adição de variáveis de pipeline {#add-ui}

1. Ao [gerenciar seus pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), toque ou clique no botão de reticências do pipeline para o qual deseja criar variáveis de pipeline e selecione **Exibir/editar variáveis** no menu de contexto.

   ![Exibir/editar variáveis de pipeline](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. A janela **Configuração de variáveis** é aberta. Insira os detalhes da variável na primeira linha da tabela e toque ou clique em **Adicionar**.

   * **O Nome da Configuração** é um identificador exclusivo para sua variável, que deve chefiar [convenções de nomenclatura de variáveis de pipeline](#naming-conventions).
   * **Valor** é o valor que a variável contém.
   * **Etapa Aplicada** é a etapa no pipeline à qual a variável se aplica. É obrigatório.
      * **Compilação**
      * **Teste funcional**
      * **Testes de interface**
   * **Type** define se a variável é texto simples ou criptografada como um segredo.

   ![Adicionar variável](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. O é adicionado à tabela. Adicione mais variáveis conforme necessário e toque ou clique em **Salvar** para salvar as variáveis adicionadas ao pipeline.

### Edição de variáveis de pipeline {#edit-ui}

1. Ao [gerenciar seus pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), toque ou clique no botão de reticências do pipeline para o qual deseja criar variáveis de pipeline e selecione **Exibir/editar variáveis** no menu de contexto.

   ![Exibir/editar variáveis de pipeline](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. A janela **Configuração de variáveis** é aberta. Toque ou clique no botão de reticências da variável que deseja editar e selecione **Editar**.

   ![Editar variável](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. Atualize o valor da variável conforme necessário e toque ou clique em **Aplicar** (a marca de seleção no final da linha) para aplicar a alteração ou em **Descartar** (a seta para trás) para reverter a alteração.

   * Somente o valor da variável pode ser editado.

   ![Editando uma variável](/help/implementing/cloud-manager/assets/pipeline-variables-edit-save.png)

1. Toque ou clique em **Salvar** para salvar as alterações feitas nas variáveis no pipeline.

Se você deseja excluir uma variável, selecione **Excluir** em vez de **Editar** no menu de reticências da variável de pipeline na janela **Configuração de variáveis**.

## Uso da CLI do Cloud Manager {#cli}

Esse comando da CLI define uma variável.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Esse comando lista variáveis.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Quando usado em um arquivo `pom.xml` do Maven, normalmente é útil mapear essas variáveis às propriedades do Maven usando uma sintaxe semelhante a esta.

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```
