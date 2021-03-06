---
title: Repositórios do Cloud Manager
description: Saiba como criar, exibir e excluir repositórios git no Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---


# Repositórios do Cloud Manager {#cloud-manager-repos}

Saiba como criar, exibir e excluir repositórios git no Cloud Manager.

>[!NOTE]
>
>Há um limite de 300 repositórios em todos os programas em uma determinada empresa ou organização IMS.

## Adicionar e gerenciar repositórios {#add-manage-repos}

Siga estas etapas para visualizar e gerenciar repositórios no Cloud Manager.

1. No **Visão geral do programa** clique em **Repositórios** e navegue até a guia **Repositórios** página.

1. Clique em **Adicionar Repositório** para iniciar o assistente.

   ![Botão Adicionar repositório](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. Insira o nome e a descrição conforme solicitado e clique em **Salvar**.

   ![Caixa de diálogo Adicionar Repositório](/help/implementing/cloud-manager/assets/repos/repo-1.png)

Quando o assistente for fechado, seu novo repositório será exibido na tabela.

Você pode selecionar o repositório na tabela, clicar no botão de reticências e selecionar **Copiar URL do repositório**, **Exibir e atualizar** ou **Excluir**.

![Opções de repositório](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

Os repositórios criados no Cloud Manager também estarão disponíveis para você selecionar ao adicionar ou editar pipelines. Consulte o documento [Pipelines de CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para saber mais.

Há um único repositório principal ou uma ramificação para qualquer pipeline. Com [suporte ao submódulo git](#git-submodule-support), muitas ramificações secundárias podem ser incluídas no momento da criação.

>[!NOTE]
>
>Um usuário deve ter a função **Gerenciador de implantação** ou **Proprietário da empresa** para poder adicionar um repositório.

## Excluindo um Repositório {#delete-repo}

A exclusão de um repositório irá:

* Torne o nome do repositório excluído inutilizável para novos repositórios que podem ser criados no futuro.
   * A mensagem de erro `Repository name should be unique within organization.` serão mostrados nesses casos.
* Tornar o repositório excluído indisponível no Cloud Manager e indisponível para vinculação a um pipeline.

Siga estes procedimentos para excluir um repositório no Cloud Manager.

1. No **Visão geral do programa** clique em **Repositórios** e navegue até a guia **Repositórios** página.

1. Selecione o repositório, clique no botão de reticências e selecione **Excluir** para excluir o repositório.

   ![Excluir repositório](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Suporte ao Submódulo Git {#git-submodule-support}

Os submódulos Git podem ser usados para mesclar o conteúdo de várias ramificações entre repositórios Git no momento da criação.

Quando o processo de build do Cloud Manager é executado, depois que o repositório configurado para o pipeline é clonado e a ramificação configurada é desmarcada, se a ramificação contiver um `.gitmodules` no diretório raiz, o comando é executado.

O comando a seguir verificará cada submódulo no diretório apropriado.

```
$ git submodule update --init
```

Essa técnica é uma alternativa potencial à solução descrita no documento [Trabalhando com vários repositórios Git de origem](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) para organizações confortáveis com o uso de submódulos git e que não desejam gerenciar um processo de mesclagem externo.

Por exemplo, digamos que existam três repositórios, cada um contendo uma única ramificação chamada `main`. No repositório principal, ou seja, aquele configurado nos pipelines, a variável `main` ramificação `pom.xml` arquivo declarando os projetos contidos nos outros dois repositórios.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
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

Isso resulta em uma `.gitmodules` arquivo semelhante ao seguinte.

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

Mais informações sobre os submódulos git podem ser encontradas na seção [Manual De Referência Do Git.](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

### Limitações e Recommendations {#limitations-recommendations}

Ao usar submódulos git, esteja ciente das seguintes limitações.

* O URL do git deve estar exatamente na sintaxe descrita na seção anterior.
* Somente os submódulos na raiz da ramificação são suportados.
* Por motivos de segurança, não incorpore credenciais em URLs Git.
* A menos que seja necessário, é altamente recomendável usar submódulos superficiais.
   * Para fazer isso, execute `git config -f .gitmodules submodule.<submodule path>.shallow true` para cada submódulo.
* As referências do submódulo Git são armazenadas para confirmações Git específicas. Como resultado, quando alterações no repositório do submódulo são feitas, a confirmação referenciada precisa ser atualizada.
   * Por exemplo, usando `git submodule update --remote`
