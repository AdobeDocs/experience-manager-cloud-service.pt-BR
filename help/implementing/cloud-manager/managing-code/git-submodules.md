---
title: Suporte ao submódulo Git
description: Aprenda como você pode usar submódulos Git para mesclar o conteúdo de várias ramificações em repositórios Git no momento da criação.
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 90%

---

# Suporte ao submódulo Git para repositórios da Adobe {#git-submodule-support}

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

Mais informações sobre os submódulos Git podem ser encontradas no [Manual de referência do Git](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

### Limitações e recomendações {#limitations-recommendations}

Ao usar submódulos do Git com repositórios gerenciados pelo Adobe, esteja ciente das limitações a seguir.

* A URL do Git deve seguir exatamente a sintaxe descrita na seção anterior.
* Somente há suporte aos submódulos na raiz da ramificação.
* Por motivos de segurança, não incorpore credenciais nas URLs do Git.
* A menos que seja necessário, é altamente recomendado usar submódulos superficiais.
   * Para fazer isso, execute `git config -f .gitmodules submodule.<submodule path>.shallow true` para cada submódulo.
* As referências do submódulo Git são armazenadas em confirmações Git específicas. Como resultado, quando alterações no repositório do submódulo são feitas, a confirmação referenciada deve ser atualizada.
   * Por exemplo, usando `git submodule update --remote`

## Suporte ao submódulo Git para repositórios privados {#private-repositories}

O suporte para submódulos git ao usar [repositórios privados](private-repositories.md) é basicamente o mesmo que usar repositórios da Adobe.

No entanto, após configurar o arquivo `pom.xml` e executar os comandos `git submodule`, é necessário adicionar um arquivo `.gitmodules` no diretório raiz do repositório agregador do Cloud Manager para detectar a configuração do submódulo.

![arquivo .gitmodules](assets/gitmodules.png)

![Agregador](assets/aggregator.png)

### Limitações e recomendações {#limitations-recommendations-private-repos}

Ao usar submódulos git com repositórios privados, esteja ciente das limitações a seguir.

* Os URLs do git para os submódulos podem estar no formato HTTPS ou SSH, mas devem estar vinculados a um repositório github.com
   * Adicionar um submódulo de repositório da Adobe a um repositório agregador do GitHub ou vice-versa não funcionará.
* Os submódulos do GitHub devem estar acessíveis ao aplicativo Adobe GitHub.
* [As limitações do uso de submódulos git com repositórios gerenciados pela Adobe](#limitations-recommendations) também se aplicam.
