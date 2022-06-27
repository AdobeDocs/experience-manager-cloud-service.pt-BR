---
title: Variáveis de ambiente do Cloud Manager
description: As variáveis de ambiente padrão podem ser configuradas e gerenciadas por meio do Cloud Manager e fornecidas para o ambiente de tempo de execução, a ser usado na configuração do OSGi.
exl-id: 5cdd5532-11fe-47a3-beb2-21967b0e43c6
source-git-commit: 7f8d6afdb5e3aecc90fdeb870eaaa0a5c5d29ca9
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---


# Variáveis de ambiente do Cloud Manager {#environment-variables}

As variáveis de ambiente padrão podem ser configuradas e gerenciadas pelo Cloud Manager. Eles são fornecidos para o ambiente de tempo de execução e podem ser usados em configurações do OSGi. As variáveis de ambiente podem ser valores específicos do ambiente ou segredos de ambiente, com base no que está sendo alterado.

## Visão geral {#overview}

As variáveis de ambiente oferecem vários benefícios aos usuários de AEM as a Cloud Service:

* Eles permitem que o comportamento do código e do aplicativo varie com base no contexto e no ambiente. Por exemplo, eles podem ser usados para permitir configurações diferentes no ambiente de desenvolvimento em comparação aos ambientes de produção ou de preparo para evitar erros dispendiosos.
* Eles só precisam ser configurados e configurados uma vez, e podem ser atualizados e excluídos quando necessário.
* Seus valores podem ser atualizados a qualquer momento e têm efeito imediatamente, sem a necessidade de alterações ou implantações de código.
* Eles podem separar o código da configuração e remover a necessidade de incluir informações confidenciais no controle de versão.
* Eles melhoram a segurança do aplicativo as a Cloud Service AEM, pois vivem fora do código.

Casos de uso típicos para o uso de variáveis de ambiente incluem:

* Conectar seu aplicativo de AEM com diferentes endpoints externos
* Uso de uma referência ao armazenar senhas em vez de diretamente na base de código
* Quando existem vários ambientes de desenvolvimento em um programa e algumas configurações diferem de um ambiente para outro

## Adição de variáveis de ambiente {#add-variables}

1. Faça logon no Adobe Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. O Cloud Manager lista os vários programas disponíveis. Selecione aquele que deseja gerenciar.
1. Selecione o **Ambientes** para o programa escolhido, selecione o ambiente para o qual deseja criar uma variável de ambiente no painel de navegação esquerdo.
1. Nos detalhes do ambiente, selecione a variável **Configuração** e selecione **Adicionar** para abrir o **Configuração do ambiente** caixa de diálogo.
   * Se estiver adicionando uma variável de ambiente pela primeira vez, você verá um **Adicionar configuração** no centro da página. Você pode usar esse botão ou **Adicionar** para abrir o **Configuração do ambiente** caixa de diálogo.

   ![Guia Configuração](assets/configuration-tab.png)

1. Insira os detalhes da variável.
   * **Nome**
   * **Valor**
   * **Serviço Aplicado** - Define o serviço (Autor/Publicação/Visualização) ao qual a variável se aplica ou se se aplica a todos os serviços
   * **Tipo** - Define se a variável é uma variável normal ou um segredo

   ![Adição de uma variável](assets/add-variable.png)

1. Depois de inserir a nova variável, é necessário selecionar **Adicionar** na última coluna da linha que contém a nova variável.
   * É possível inserir várias variáveis de uma só vez, inserindo uma nova linha e selecionando **Adicionar**.

   ![Salvar variáveis](assets/save-variables.png)

1. Selecionar **Salvar** para manter suas variáveis.

Um indicador com o status **Atualização** é mostrada na parte superior da tabela e ao lado da variável recém-adicionada para indicar que o ambiente está sendo atualizado com a configuração. Uma vez concluída, a nova variável de ambiente estará visível na tabela.

![Atualização de variáveis](assets/updating-variables.png)

>[!TIP]
>
>Se desejar adicionar várias variáveis, é recomendável adicionar a primeira variável e, em seguida, usar a variável **Adicionar** no botão **Configuração do ambiente** para adicionar as variáveis adicionais. Dessa forma, você pode adicioná-las com uma atualização ao ambiente.

## Atualização das variáveis de ambiente {#update-variables}

Depois de criar as variáveis de ambiente, você pode atualizá-las usando o **Adicionar/atualizar** botão para iniciar o **Configuração do ambiente** caixa de diálogo.

1. Faça logon no Adobe Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. O Cloud Manager lista os vários programas disponíveis. Selecione aquele que deseja gerenciar.
1. Selecione o **Ambientes** para o programa escolhido, selecione o ambiente para o qual deseja criar uma variável de ambiente no painel de navegação esquerdo.
1. Nos detalhes do ambiente, selecione a variável **Configuração** e selecione **Adicionar/atualizar** no canto superior direito para abrir o **Configuração do ambiente** caixa de diálogo.

   ![Botão Adicionar/Atualizar para variáveis](assets/add-update-variables.png)

1. Usando o botão de reticências na última coluna da linha da variável que deseja modificar, selecione **Editar** ou **Excluir**.

   ![Editar ou excluir variável](assets/edit-delete-variable.png)

1. Edite a variável de ambiente conforme necessário.
   * Ao editar, o botão de reticências será alterado para opções para reverter para o valor original ou confirmar a alteração.
   * Ao editar segredos, os valores só podem ser atualizados, não visualizados.

   ![Editar variável](assets/edit-variable.png)

1. Depois de fazer todas as alterações necessárias na configuração, selecione **Salvar**.

[Como ao adicionar variáveis,](#add-variables) um indicador com o status **Atualização** é mostrada na parte superior da tabela e ao lado das variáveis recém-atualizadas para indicar que o ambiente está sendo atualizado com a configuração. Uma vez concluída, as variáveis de ambiente atualizadas estarão visíveis na tabela.

>[!TIP]
>
>Se desejar atualizar várias variáveis, é recomendável usar a variável **Configuração do ambiente** para atualizar todas as variáveis necessárias de uma vez antes de tocar ou clicar em **Salvar**. Dessa forma, você pode adicioná-las com uma atualização ao ambiente.

## Uso de variáveis de ambiente {#using}

As variáveis de ambiente podem tornar seu `pom.xml` configurações mais seguras e flexíveis. Por exemplo, senhas não precisam ser codificadas e sua configuração pode se adaptar com base nos valores nas variáveis de ambiente.

Você pode acessar variáveis e segredos de ambiente, respectivamente, por meio de XML, como segue.

* `${env.VARIABLE_NAME}`
* `${secret.SECRET_NAME}`

Consulte o documento [Configurando o projeto](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repository-support-password-protected-maven-repositories) para obter um exemplo de como usar os dois tipos de variáveis em um `pom.xml` arquivo.
