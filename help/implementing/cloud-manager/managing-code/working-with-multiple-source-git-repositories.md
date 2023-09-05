---
title: Uso de vários repositórios
description: Saiba como gerenciar vários repositórios Git ao trabalhar com o Cloud Manager.
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '752'
ht-degree: 100%

---

# Uso de vários repositórios {#working-with-multiple-source-git-repos}

Saiba como gerenciar vários repositórios Git ao trabalhar com o Cloud Manager.

## Sincronização de repositórios Git gerenciados pelo Cliente {#syncing-customer-managed-git-repositories}

Em vez de trabalhar diretamente com o repositório Git do Cloud Manager, [os clientes podem trabalhar com seu próprio repositório Git](integrating-with-git.md), ou com vários deles. Nesses casos, um processo de sincronização automatizada deve ser configurado para garantir que o repositório Git do Cloud Manager esteja sempre atualizado.

Dependendo de onde o repositório Git do cliente estiver hospedado, uma ação do GitHub ou uma solução de integração contínua, como Jenkins, pode ser usada para configurar a automação. Com uma automação em vigor, cada push para um repositório Git de propriedade do cliente pode ser encaminhado automaticamente para o repositório Git do Cloud Manager.

Embora essa automação para um único repositório Git de propriedade do cliente seja direta, a configuração disso para vários repositórios requer uma configuração inicial. O conteúdo de vários repositórios Git precisa ser mapeado a diferentes diretórios no único repositório Git do Cloud Manager.  O repositório Git do Cloud Manager precisa ser provisionado com um Maven raiz `pom.xml`, listando os diferentes subprojetos na seção de módulos.

Veja a seguir um exemplo do arquivo `pom.xml` para dois repositórios Git de propriedade do cliente.

* O primeiro projeto será colocado no diretório chamado `project-a`.
* O segundo projeto será colocado no diretório chamado `project-b`.

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

A raiz `pom.xml` será enviada para uma ramificação no repositório Git do Cloud Manager. Em seguida, os dois projetos precisam ser configurados para encaminhar automaticamente as alterações ao repositório Git do Cloud Manager.

Uma solução possível seria a descrita a seguir.

1. Uma ação do GitHub pode ser acionada por push a uma ramificação no projeto A.
1. A ação verificará o projeto A e o repositório Git do Cloud Manager e copiará todo o conteúdo do projeto A para o diretório `project-a` no repositório Git do Cloud Manager.
1. Em seguida, a ação confirmará a alteração por push.

Por exemplo, uma alteração na ramificação principal do projeto A é automaticamente enviada para a ramificação principal no repositório Git do Cloud Manager. Obviamente, pode haver um mapeamento entre ramificações, como quando um push para uma ramificação chamada `dev` no projeto A é enviado para uma ramificação chamada `development` no repositório Git do Cloud Manager. Etapas semelhantes são necessárias para o projeto B.

Dependendo da estratégia de ramificação e dos fluxos de trabalho, a sincronização pode ser configurada para ramificações diferentes. Se o repositório Git usado não fornecer um conceito semelhante às ações do GitHub, também será possível fazer a integração por meio do Jenkins (ou semelhante). Nesse caso, um webhook aciona uma tarefa do Jenkins que faz o trabalho.

Siga estas etapas para adicionar um novo, uma terceira fonte ou um repositório.

1. Adicione uma nova ação do GitHub ao novo repositório, que envia as alterações desse repositório para o repositório Git do Cloud Manager.
1. Execute essa ação pelo menos uma vez para garantir que o código do projeto esteja no repositório Git do Cloud Manager.
1. Adicione uma referência ao novo diretório no `pom.xml` do Maven raiz no repositório Git do Cloud Manager.

## Exemplo de ação do GitHub {#sample-github-action}

Este é um exemplo de ação do GitHub acionada por push para a ramificação principal e, em seguida, por push a um subdiretório do repositório Git do Cloud Manager. As ações do GitHub precisam ser fornecidas com dois segredos, `MAIN_USER` e `MAIN_PASSWORD`, para poder se conectar e enviar por push para o repositório Git do Cloud Manager.

```java
name: SYNC
env:
  # Username/email used to commit to Cloud Manager's Git repository
  USER_NAME: <NAME>
  USER_EMAIL: <EMAIL>
  # Directory within the Cloud Manager Git repository
  PROJECT_DIR: project-a
  # Cloud Manager's Git repository
  MAIN_REPOSITORY: https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
  # The branch in Cloud Manager's Git repository to push to
  MAIN_BRANCH : <BRANCH_NAME>
 
# Only run on a push to this branch
on:
  push:
     branches: [ main ]
 
jobs:
  build:
    runs-on: ubuntu-latest
 
    steps:
      # Checkout this project into a sub folder
      - uses: actions/checkout@v2
        with:
          path: sub
      # Cleanup sub project
      - name: Clean project
        run: |
          git -C sub log --format="%an : %s" -n 1 > commit.txt
          rm -rf sub/.git
          rm -rf sub/.github
      # Set global git configuration
      - name: Set git config
        run: |
          git config --global credential.helper cache
          git config --global user.email ${USER_EMAIL}
          git config --global user.name ${USER_NAME}
      # Checkout the main project
      - name: Checkout main project
        run:
          git clone -b ${MAIN_BRANCH} ${MAIN_REPOSITORY} ${MAIN_BRANCH} 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf ${MAIN_BRANCH}/${PROJECT_DIR} 
          mv sub ${MAIN_BRANCH}/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C ${MAIN_BRANCH} add -f ${PROJECT_DIR}
          git -C ${MAIN_BRANCH} commit -F ../commit.txt
          git -C ${MAIN_BRANCH} push
```

O uso de uma ação do GitHub é muito flexível. É possível executar qualquer mapeamento entre ramificações de repositórios Git, bem como qualquer mapeamento de projetos Git separados no layout de diretório do projeto principal.

>[!NOTE]
>
>O exemplo de script usa `git add` para atualizar o repositório. Isso pressupõe que as remoções estejam incluídas. Dependendo da configuração padrão do Git, talvez seja necessário substituí-lo por `git add --all`.

## Exemplo de tarefa do Jenkins {#sample-jenkins-job}

Este é um exemplo de script que pode ser usado em uma tarefa do Jenkins ou similar e tem o seguinte fluxo:

1. É acionado por uma alteração em um repositório Git.
1. A tarefa do Jenkins verifica o estado mais recente desse projeto ou ramificação.
1. A tarefa então aciona o script.
1. Esse script, por sua vez, verifica o repositório Git do Cloud Manager e confirma o código do projeto em um subdiretório.

A tarefa do Jenkins precisa de dois segredos, `MAIN_USER` e `MAIN_PASSWORD`, para poder se conectar e enviar para o repositório Git do Cloud Manager.

```java
# Username/email used to commit to Cloud Manager's Git repository
export USER_NAME=<NAME>
export USER_EMAIL=<EMAIL>
# Directory within the Cloud Manager Git repository
export PROJECT_DIR=project-a
# Cloud Manager's Git repository
export MAIN_REPOSITORY=https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
# The branch in Cloud Manager's Git repository to push to
export MAIN_BRANCH=<BRANCH_NAME>
 
# clean up and init
rm -rf target
mkdir target
 
# mv project to sub folder
mkdir target/sub
for f in .* *
do
    if [ "$f" != "." -a "$f" != ".." -a "$f" != "target" ]
    then
        mv "$f" target/sub
    fi
done
cd target
 
# capture log and remove git info
cd sub
git log --format="%an : %s" -n 1 > ../commit.txt
rm -rf .git
rm -rf .github
cd ..
 
# checkout main repository
git clone -b $MAIN_BRANCH $MAIN_REPOSITORY main
cd main
 
# configure main repository
git config credential.helper cache
git config user.email $USER_EMAIL
git config user.name $USER_NAME
 
# update project in main
rm -rf $PROJECT_DIR
mv ../sub $PROJECT_DIR
 
# commit changes to main
git add -f $PROJECT_DIR
git commit -F ../commit.txt
git push
```

O uso de uma tarefa do Jenkins é muito flexível. É possível executar qualquer mapeamento entre ramificações de repositórios Git, bem como qualquer mapeamento de projetos Git separados no layout de diretório do projeto principal.

>[!NOTE]
>
>O exemplo de script usa `git add` para atualizar o repositório. Isso pressupõe que as remoções estejam incluídas. Dependendo da configuração padrão do Git, talvez seja necessário substituí-lo por `git add --all`.
