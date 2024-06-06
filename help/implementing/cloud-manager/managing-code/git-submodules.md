---
title: Suporte a submódulos Git
description: Saiba como você pode usar os submódulos do Git para mesclar o conteúdo de várias ramificações entre repositórios Git no momento da compilação.
source-git-commit: 34c96940f91d42d622d50e85e9a9d6f75f3fb483
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 57%

---


# Suporte a submódulos Git para repositórios Adobe {#git-submodule-support}

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

Ao usar submódulos do Git com repositórios gerenciados pelo Adobe, esteja ciente das limitações a seguir.

* A URL do Git deve seguir exatamente a sintaxe descrita na seção anterior.
* Somente há suporte aos submódulos na raiz da ramificação.
* Por motivos de segurança, não incorpore credenciais nas URLs do Git.
* A menos que seja necessário, é altamente recomendado usar submódulos superficiais.
   * Para fazer isso, execute `git config -f .gitmodules submodule.<submodule path>.shallow true` para cada submódulo.
* As referências do submódulo Git são armazenadas em confirmações Git específicas. Como resultado, quando alterações no repositório do submódulo são feitas, a confirmação referenciada deve ser atualizada.
   * Por exemplo, usando `git submodule update --remote`

## Suporte a submódulos Git para repositórios privados {#private-repositories}

Suporte para submódulos Git ao usar [repositórios privados](private-repositories.md) é basicamente o mesmo que usar repositórios de Adobe.

No entanto, após configurar o seu `pom.xml` arquivo e executando o `git submodule` comandos, é necessário adicionar um `.gitmodules` para o diretório raiz do repositório agregador do Cloud Manager para detectar a configuração do submódulo.

![arquivo .gitmodules](assets/gitmodules.png)

![Agregador](assets/aggregator.png)

### Limitações e recomendações {#limitations-recommendations-private-repos}

Ao usar submódulos do Git com repositórios privados, esteja ciente das limitações a seguir.

* Os URLs do Git para os submódulos podem estar no formato HTTPS ou SSH, mas devem vincular a um repositório github.com
   * Adicionar um submódulo do repositório de Adobe a um repositório agregador GitHub ou vice-versa não funcionará.
* Os submódulos do GitHub devem ser acessíveis para o aplicativo GitHub do Adobe.
* [As limitações do uso de submódulos Git com repositórios gerenciados pelo Adobe](#limitations-recommendations) também se aplicam.
