---
title: Variáveis de pipeline no Cloud Manager
description: Saiba como você pode usar variáveis de pipeline no Cloud Manager para gerenciar variáveis de configuração específicas para a sua build.
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ea85deb74f759f8e74d314df0ba081ea23cb5aab
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 14%

---

# Variáveis de pipeline no Cloud Manager {#configuring-pipeline-variables}

Seu processo de build pode depender de variáveis de configuração específicas que não devem ser armazenadas no repositório Git. Ou talvez seja necessário ajustá-los entre execuções de pipeline na mesma ramificação. O Cloud Manager permite gerenciar essas configurações como variáveis de pipeline.

## Sobre variáveis de pipeline {#pipeline-variables}

Com o Cloud Manager, você pode configurar variáveis de pipeline de várias maneiras diferentes.

* [Uso da interface do usuário do Cloud Manager](#ui)
* [Uso da CLI do Cloud Manager](#cli)
* [Usando a API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

As variáveis podem ser armazenadas como texto simples ou criptografadas em repouso. Em ambos os casos, as variáveis são disponibilizadas no ambiente de compilação como variáveis de ambiente que podem ser referenciadas no arquivo `pom.xml` ou em outros scripts de criação.

## Adicionar uma variável de pipeline por meio do Cloud Manager {#ui}

As variáveis de pipeline podem ser configuradas e gerenciadas pela interface do usuário do Cloud Manager. Eles ajudam a simplificar o gerenciamento de pipeline, especialmente quando configurações variáveis são necessárias em diferentes etapas.

Você deve ter permissões para editar o pipeline para adicionar, editar e excluir variáveis de pipeline.

Se um pipeline estiver em execução, o gerenciamento de variáveis será bloqueado.

**Para adicionar uma variável de pipeline por meio do Cloud Manager:**

1. Ao [gerenciar seus pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), clique em ![Reticências - Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) do pipeline para o qual você deseja criar variáveis de pipeline.

1. No menu suspenso, clique em **Exibir/Editar variáveis**.

   ![Exibir/Editar variáveis de pipeline](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Na caixa de diálogo **Configuração de Variáveis**, insira os detalhes na primeira linha da tabela.

   | Texto | Descrição |
   | --- | --- |
   | Nome | Um nome exclusivo da variável de configuração. Ela identifica a variável específica usada no pipeline. Ele deve seguir as seguintes convenções de nomenclatura:<ul><li>As variáveis só podem conter caracteres alfanuméricos e sublinhado (`_`).</li><li>Os nomes devem estar em maiúsculas.</li><li>Há um limite de 200 variáveis por pipeline.</li><li>Cada nome deve ter 100 caracteres ou menos.</li><li>Cada valor de variável `string` deve ter menos de 2048 caracteres.</li><li>Cada valor de tipo de variável `secretString` deve ter 500 caracteres ou menos.</li></ul> |
   | Valor | O valor que a variável contém. |
   | Etapa aplicada | Obrigatório. A etapa no pipeline à qual a variável se aplica:<ul><li>**Compilação** - A variável é aplicada durante o processo de compilação.</li><li>**Teste funcional** - A variável é usada durante a etapa de teste funcional.</li><li>**Teste de interface** - A variável é usada durante a fase de teste de interface.</li>&lt;li&lt;**Implantar** - A variável é usada durante a etapa de implantação. Por exemplo, use essa variável para pipelines do Edge Delivery Services.</li></ul> |
   | Tipo | Selecione se a variável for texto sem formatação ou criptografada como segredo. |

   ![Adicionar variável](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. Clique em **Adicionar**.

   Adicione mais variáveis, conforme necessário.

1. Clique em **Salvar**.

## Editar uma variável de pipeline {#edit-ui}

1. Ao [gerenciar seus pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), clique em ![Reticências - Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) do pipeline para o qual você deseja editar variáveis de pipeline.

1. No menu suspenso, clique em **Exibir/Editar variáveis**.

   ![Exibir/Editar variáveis de pipeline](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Na caixa de diálogo **Configuração de Variáveis**, clique em ![Reticências - Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) da variável que você deseja alterar.

1. No menu suspenso, clique em **Editar**.

   ![Editar variável](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. Atualize o valor da variável conforme necessário.

   Somente o valor da variável pode ser alterado.

1. Siga uma das seguintes opções:

   * Clique em ![Aplicar - Ícone de marca de seleção](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg) para aplicar a alteração.
   * Clique no ![ícone Desfazer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Undo_18_N.svg) para reverter a alteração.

1. Clique em **Salvar**.


## Excluir uma variável de pipeline {#delete-ui}

1. Ao [gerenciar seus pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), clique em ![Reticências - Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) do pipeline para o qual você deseja excluir variáveis de pipeline.

1. No menu suspenso, clique em **Exibir/Editar variáveis**.

   ![Exibir/Editar variáveis de pipeline](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Na caixa de diálogo **Configuração de Variáveis**, clique em ![Reticências - Mais ícones](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) da variável que você deseja remover e em **Excluir**.

## Definir variáveis de pipeline usando a CLI do Cloud Manager {#cli}

Esse comando na CLI (Command Line Interface, interface de linha de comando) define uma variável.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Esse comando lista variáveis.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Quando usado em um arquivo Maven `pom.xml`, geralmente é útil vincular essas variáveis às propriedades Maven usando uma sintaxe semelhante ao seguinte exemplo:

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
