---
title: Trabalhando com vários repositórios Git de origem
description: Trabalhar com vários repositórios Git de origem - Cloud Services
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: 21669a29fbfd1072b637f407f5220825c4d1edbb
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# Trabalhando com vários repositórios Git de origem {#working-with-multiple-source-git-repos}


## Sincronizando Repositórios Git Gerenciados pelo Cliente {#syncing-customer-managed-git-repositories}

Em vez de trabalhar diretamente com o repositório Git do Cloud Manager, os clientes podem trabalhar com seu próprio repositório Git ou vários repositórios Git próprios. Nesses casos, um processo de sincronização automatizada deve ser configurado para garantir que o repositório Git do Cloud Manager seja sempre atualizado. Dependendo de onde o repositório Git do cliente estiver hospedado, uma ação do GitHub ou uma solução de integração contínua como Jenkins podem ser usadas para configurar a automação. Com uma automação em vigor, cada push para um repositório Git de propriedade do cliente pode ser encaminhado automaticamente para o repositório Git do Cloud Manager.

Embora essa automação para um único repositório Git de propriedade de cliente seja direta, a configuração dessa configuração para vários repositórios requer uma configuração inicial. O conteúdo de vários repositórios Git precisa ser mapeado para diretórios diferentes no único repositório Git do Cloud Manager.  O repositório Git do Cloud Manager precisa ser provisionado com um pom Maven raiz, listando os diferentes subprojetos na seção de módulos

Abaixo está um exemplo de pom para dois Repositórios Git de propriedade do cliente: o primeiro projeto será colocado no diretório chamado `project-a`, o segundo projeto será colocado no diretório chamado `project-b`.

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

Esse pom raiz é enviado para uma ramificação no Repositório Git do Cloud Manager. Em seguida, os dois projetos precisam ser configurados para encaminhar automaticamente as alterações para o Repositório Git do Cloud Manager.

Por exemplo, uma ação do GitHub pode ser acionada por um push para uma ramificação no projeto A. A ação verificará o projeto A e o repositório Git do Cloud Manager e copiará todo o conteúdo do projeto A para o diretório `project-a` no repositório Git do Cloud Manager e enviará a alteração novamente. Por exemplo, uma alteração na ramificação principal do projeto A é automaticamente enviada para a ramificação principal no repositório Git do Cloud Manager. É claro que pode haver um mapeamento entre ramificações, como um push para uma ramificação chamada &quot;dev&quot; no projeto A, que é enviado para uma ramificação chamada &quot;development&quot; no repositório Git do Cloud Manager. Etapas semelhantes são necessárias para o Projeto B.

Dependendo da estratégia de ramificação e dos fluxos de trabalho, a sincronização pode ser configurada para ramificações diferentes. Se o repositório Git usado não fornecer um conceito semelhante às ações do GitHub, uma integração por meio de Jenkins (ou semelhante) também será possível. Nesse caso, um webhook aciona um emprego em Jenkins que faz o trabalho.

Siga as etapas abaixo para adicionar uma nova (terceira) fonte ou repositório:

1. Adicione uma nova ação do GitHub ao novo repositório, que envia as alterações desse Repositório para o Repositório Git do Cloud Manager.
1. Execute essa ação pelo menos uma vez para garantir que o código do projeto esteja no Repositório Git do Cloud Manager.
1. Adicione uma referência ao novo diretório no pom Maven raiz no Repositório Git do Cloud Manager.


## Exemplo de ação do GitHub {#sample-github-action}

Esta é uma amostra de ação do GitHub acionada por um push para a ramificação principal e, em seguida, por push em um subdiretório do Repositório Git do Cloud Manager. As ações do GitHub precisam ser fornecidas com dois segredos, `MAIN_USER` e `MAIN_PASSWORD`, para se conectar e enviar para o repositório Git do Cloud Manager.

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
          git clone -b ${MAIN_BRANCH} https://${{ secrets.PAT }}@github.com/${MAIN_REPOSITORY}.git main 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf main/${PROJECT_DIR} 
          mv sub main/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C main add -f ${PROJECT_DIR}
          git -C main commit -F ../commit.txt
          git -C main push
```

Como mostrado acima, usar uma ação do GitHub é muito flexível. Qualquer mapeamento entre ramificações dos repositórios Git pode ser executado, bem como qualquer mapeamento dos projetos Git separados no layout de diretório do projeto principal.

>[!NOTE]
>O script acima usa `git add` para atualizar o repositório, o que pressupõe que as remoções estejam incluídas - dependendo da configuração padrão do Git, isso precisa ser substituído por `git add --all`.

## Exemplo de trabalho do Jenkins {#sample-jenkins-job}

Este é um exemplo de script que pode ser usado em um trabalho do Jenkins ou similar. Ele é acionado por uma alteração em um Repositório Git. O trabalho do Jenkins verifica o estado mais recente desse projeto ou ramificação e então dispara esse script.

Esse script, por sua vez, verifica o Repositório Git do Cloud Manager e confirma o código do projeto em um subdiretório.

O trabalho do Jenkins precisa ser fornecido com dois segredos, `MAIN_USER` e `MAIN_PASSWORD`, para poder se conectar e enviar para o repositório Git do Cloud Manager.

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

Como mostrado acima, usar um emprego em Jenkins é muito flexível. Qualquer mapeamento entre ramificações dos Repositórios Git pode ser executado, bem como qualquer mapeamento dos projetos Git separados no layout de diretório do projeto principal.

>[!NOTE]
>O script acima usa `git add` para atualizar o repositório, o que pressupõe que as remoções estejam incluídas - dependendo da configuração padrão do Git, isso precisa ser substituído por `git add --all`.
