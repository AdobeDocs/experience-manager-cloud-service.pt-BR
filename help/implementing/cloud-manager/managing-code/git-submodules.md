---
title: Suporte ao submódulo Git
description: Saiba como você pode usar submódulos Git para mesclar o conteúdo de várias ramificações em repositórios Git no momento da criação.
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 24%

---

# Suporte ao submódulo Git para repositórios da Adobe {#git-submodule-support}

Os submódulos Git podem ser usados para mesclar o conteúdo de várias ramificações em repositórios Git no momento da criação.

Quando o processo de criação do Cloud Manager é executado, ele clona o repositório do pipeline e verifica a ramificação. Se um arquivo `.gitmodules` existir no diretório raiz da ramificação, o comando correspondente será executado.

O comando a seguir verifica cada submódulo no diretório apropriado.

```
$ git submodule update --init
```

Esta técnica oferece uma alternativa para a solução descrita em [Trabalhar com vários repositórios Git da Source](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md). É ideal para organizações familiarizadas com os submódulos do Git e que preferem não gerenciar um processo de mesclagem externo.

Por exemplo, suponha que haja três repositórios. Cada repositório contém uma única ramificação chamada `main`. No repositório principal, ou seja, aquele configurado nos pipelines, a ramificação `main` tem um arquivo `pom.xml` que declara os projetos contidos nos outros dois repositórios:

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

Em seguida, você adicionaria submódulos para os outros dois repositórios:

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

O resultado é um arquivo `.gitmodules` semelhante ao seguinte:

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

Consulte também o [Manual de referência do Git](https://git-scm.com/book/en/v2/Git-Tools-Submodules) para obter mais informações sobre os submódulos do Git.

## Notas de uso para repositórios Adobe {#usage-notes-recommendations-adobe-repos}

* O URL do Git deve seguir exatamente a sintaxe descrita na seção anterior.
* Somente há suporte aos submódulos na raiz da ramificação.
* Por motivos de segurança, não incorpore credenciais nas URLs do Git.
* A menos que seja necessário, a Adobe recomenda usar submódulos superficiais executando o seguinte:
  `git config -f .gitmodules submodule.<submodule path>.shallow true` para cada submódulo.
* As referências do submódulo Git são armazenadas em confirmações Git específicas. Como resultado, quando alterações no repositório do submódulo são feitas, a confirmação referenciada deve ser atualizada.
Por exemplo, usando o seguinte:

  `git submodule update --remote`

## Suporte ao submódulo Git para repositórios privados {#private-repositories}

O suporte para submódulos Git em [repositórios privados](private-repositories.md) geralmente é semelhante ao seu uso com repositórios Adobe.

No entanto, após configurar seu arquivo `pom.xml` e executar os comandos `git submodule`, você deve adicionar um arquivo `.gitmodules` ao diretório raiz do repositório agregador para que o Cloud Manager reconheça a configuração do submódulo.

![arquivo .gitmodules](assets/gitmodules.png)

![Agregador](assets/aggregator.png)

### Notas de uso {#usage-notes-recommendations-private-repos}

* Os URLs Git do submódulo podem estar no formato HTTPS ou SSH, mas devem apontar para um repositório GitHub.com. Não há suporte para a adição de um submódulo do repositório Adobe a um repositório agregador GitHub ou o inverso.
* Os submódulos do GitHub devem ser acessíveis pelo aplicativo GitHub da Adobe.
* [As limitações do uso de submódulos Git com repositórios gerenciados pela Adobe](#usage-notes-recommendations-adobe-repos) também se aplicam.
