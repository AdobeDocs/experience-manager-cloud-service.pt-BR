---
title: Repositórios do Cloud Manager
description: Saiba como criar, exibir e excluir repositórios Git no Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: af8ab1f741c658dcb47bdf0d37e403fcb180631a
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 96%

---


# Repositórios do Cloud Manager {#cloud-manager-repos}

Saiba como criar, exibir e excluir repositórios Git no Cloud Manager.

>[!NOTE]
>
>Há um limite de 300 repositórios em todos os programas em uma determinada empresa ou organização IMS.

## Adição e gerenciamento de repositórios {#add-manage-repos}

Siga estas etapas para exibir e gerenciar repositórios no Cloud Manager.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. No **Visão geral do programa** toque ou clique em **Repositórios** para alternar para a guia **Repositórios** página.

1. Clique em **Adicionar repositório**.

   ![Botão Adicionar repositório](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. Insira o nome e a descrição conforme solicitado e clique em **Salvar**.

   ![Caixa de diálogo Adicionar repositório](/help/implementing/cloud-manager/assets/repos/repo-1.png)

Quando o assistente for fechado, o novo repositório será exibido na tabela.

Você pode selecionar o repositório na tabela, clicar no botão de reticências e selecionar **Copiar URL do repositório**, **Exibir e atualizar** ou **Excluir**.

![Opções do repositório](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

Os repositórios criados no Cloud Manager também estarão disponíveis para seleção ao adicionar ou editar pipelines. Consulte [Pipelines de CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para saber mais.

Há um único repositório principal ou uma ramificação para um determinado pipeline. Com o [suporte ao submódulo Git](#git-submodule-support), várias ramificações secundárias podem ser incluídas no momento da compilação.

>[!NOTE]
>
>Um usuário deve ter a função **Gerente de implantação** ou **Proprietário da empresa** para poder adicionar um repositório.

## Exclusão de um repositório {#delete-repo}

A exclusão de um repositório:

* Tornará o nome do repositório excluído inutilizável para novos repositórios que podem ser criados no futuro.
   * A mensagem de erro `Repository name should be unique within organization.` será mostrada nesses casos.
* Tornará o repositório excluído indisponível no Cloud Manager e indisponível para vinculação a um pipeline.

Siga estas instruções para excluir um repositório no Cloud Manager.

1. Na página **Visão geral do programa**, clique na guia **Repositórios** e navegue até a página **Repositórios**.

1. Selecione o repositório, clique no botão de reticências e selecione **Excluir** para excluir o repositório.

   ![Excluir repositório](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Suporte a submódulos Git {#git-submodule-support}

Os submódulos Git podem ser usados para mesclar o conteúdo de várias ramificações entre repositórios Git no momento da compilação.

Quando o processo de compilação do Cloud Manager é executado, depois que o repositório configurado para o pipeline é clonado e a ramificação configurada é desmarcada, se a ramificação contiver um arquivo `.gitmodules` no diretório raiz, o comando será executado.

O comando a seguir verificará cada submódulo no diretório apropriado.

```
$ git submodule update --init
```

Essa técnica é uma possível alternativa à solução descrita no documento [Trabalho com vários repositórios Git de origem](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) para organizações familiarizadas com o uso de submódulos Git e que não desejam gerenciar um processo de mesclagem externo.

Por exemplo, digamos que existam três repositórios, cada um contendo uma única ramificação chamada `main`. No repositório principal, ou seja, aquele configurado nos pipelines, a ramificação `main` tem um arquivo `pom.xml` que declara os projetos contidos nos outros dois repositórios.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
   
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
   
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
   
</project>
```

Em seguida, você adicionaria submódulos para os outros dois repositórios.

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Isso resultaria em um arquivo `.gitmodules` semelhante ao mostrado a seguir.

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

Mais informações sobre os submódulos Git podem ser encontradas na seção [Manual de referência do Git.](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

### Limitações e recomendações {#limitations-recommendations}

Ao usar submódulos do Git, esteja ciente das limitações a seguir.

* A URL do Git deve seguir exatamente a sintaxe descrita na seção anterior.
* Somente há suporte aos submódulos na raiz da ramificação.
* Por motivos de segurança, não incorpore credenciais nas URLs do Git.
* A menos que seja necessário, é altamente recomendado usar submódulos superficiais.
   * Para fazer isso, execute `git config -f .gitmodules submodule.<submodule path>.shallow true` para cada submódulo.
* As referências do submódulo Git são armazenadas em confirmações Git específicas. Como resultado, quando são feitas alterações no repositório do submódulo, a confirmação referenciada precisa ser atualizada.
   * Por exemplo, usando `git submodule update --remote`
