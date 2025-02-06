---
title: Criação de páginas
description: Saiba como criar novas páginas para o seu site usando o console Sites.
exl-id: 77264562-e76a-40c8-9878-847a8878fb8e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 26%

---


# Criação de páginas {#creating-pages}

Saiba como criar novas páginas para o seu site usando o console **Sites**.

>[!TIP]
>
>Antes de começar a criar novas páginas, familiarize-se com [como suas páginas estão organizadas no AEM](/help/sites-cloud/authoring/sites-console/organizing-pages.md).

## Privilégios de Acesso {#access-privileges}

Sua conta precisa de direitos de acesso apropriados e permissões para criar páginas.

Se você encontrar algum problema, entre em contato com o administrador do sistema.

## Criar uma nova página {#creating-a-new-page}

A menos que todas as páginas tenham sido criadas antecipadamente para você, é necessário criar uma página antes de começar a criar o conteúdo:

1. Abra [o console **Sites**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Navegue até o local onde deseja criar a nova página.
1. Abra o seletor suspenso usando **Criar** na barra de ferramentas e selecione **Página** na lista:

   ![Criação de uma página](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. A partir do primeiro estágio do assistente, é possível:

   * Selecione o modelo que deseja usar para criar a nova página e selecione **Avançar** para continuar ou **Cancelar** para suspender o processo.
   * Os modelos têm suporte no [Editor de Páginas](/help/sites-cloud/authoring/page-editor/introduction.md) e no [Editor Universal](/help/sites-cloud/authoring/universal-editor/templates.md).

   ![Seleção de um modelo para uma nova página](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. A partir do último estágio do assistente, é possível:

   * Use as três guias para inserir as [propriedades de página](/help/sites-cloud/authoring/sites-console/page-properties.md) que você deseja atribuir à nova página, em seguida, selecione **Criar** para realmente criar a página.

   * Use **Voltar** para retornar à seleção do modelo.

   Os campos principais são:

   * **Título**:

      * Ele é exibido ao usuário e é obrigatório.

   * **Nome**:

      * Usado para gerar o URI. Se não especificado, o nome é derivado do título.
      * Se você fornecer uma página **Nome** ao criar uma página, o AEM [validará o nome de acordo com as convenções](/help/implementing/developing/introduction/naming-conventions.md) impostas pelo AEM e JCR.
      * **Não é possível inserir caracteres inválidos** no campo **Nome**. Quando o AEM detecta caracteres inválidos, o campo é realçado e uma mensagem explicativa é exibida para indicar os caracteres que precisam ser removidos/substituídos.

   >[!TIP]
   >
   >Consulte [Convenções de nomenclatura da página](#page-naming-conventions).

   As informações mínimas necessárias para criar uma página são o **Título**.

   ![Fornecimento do título da página](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Toque ou clique em **Criar** para concluir o processo e criar sua nova página. A caixa de diálogo de confirmação pergunta se você deseja **Abrir** a página imediatamente ou retornar ao console (**Concluído**). Selecione uma para encerrar o processo de criação de página.

   ![Êxito na criação da página](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   * Se você escolher **Abrir**, o console **Sites** abrirá o editor apropriado com base no modelo da nova página:
      * [O editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md)
      * [O Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md)

Se você retornar ao console, poderá ver sua nova página:

![Nova página resultante](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!NOTE]
>
>Se você criar uma página usando um nome que já existe no mesmo local, o AEM cria a página com uma variação do nome especificado ao anexar um número. Por exemplo, se `beach` já existir, a nova página se tornará `beach1`.

>[!CAUTION]
>
>Após a criação de uma página, seu modelo não poderá ser alterado, a menos que você [crie uma inicialização com um novo modelo](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), embora o conteúdo existente seja perdido.
