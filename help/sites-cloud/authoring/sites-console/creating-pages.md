---
title: Criação de páginas
description: Saiba como criar novas páginas para o seu site usando o console Sites.
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 64%

---


# Criação de páginas {#creating-pages}

Saiba como criar novas páginas para o seu site usando o **Sites** console.

>[!TIP]
>
>Antes de começar a criar novas páginas, familiarize-se [como suas páginas estão organizadas no AEM.](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

## Privilégios de Acesso {#access-privileges}

Sua conta precisa de direitos de acesso apropriados e permissões para criar páginas.

Caso encontre algum problema, sugerimos que você entre em contato com o administrador do sistema.

## Criar uma nova página {#creating-a-new-page}

A menos que todas as páginas tenham sido criadas antecipadamente para você, é necessário criar uma página antes de começar a criar o conteúdo:

1. Abertura [o **Sites** console.](/help/sites-cloud/authoring/sites-console/introduction.md)
1. Navegue até o local onde deseja criar a nova página.
1. Abra o seletor suspenso usando **Criar** na barra de ferramentas e selecione **Página** na lista:

   ![Criação de uma página](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. A partir do primeiro estágio do assistente, você pode:

   * Selecione o modelo que deseja usar para criar a nova página e selecione **Próxima** para continuar.

   * **Cancelar** para suspender o processo.

   ![Seleção de um modelo para uma nova página](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. A partir do último estágio do assistente, você pode:

   * Use as três guias para inserir a variável [propriedades da página](/help/sites-cloud/authoring/sites-console/page-properties.md) que deseja atribuir à nova página, selecione **Criar** para realmente criar a página.

   * Use **Voltar** para retornar à seleção do modelo.

   Os campos principais são:

   * **Título**:

      * Ele é exibido ao usuário e é obrigatório.

   * **Nome**:

      * Usado para gerar o URI. Se não especificado, o nome é derivado do título.
      * Se você fornecer uma página **Nome** ao criar uma página, AEM [valida o nome de acordo com as convenções](/help/implementing/developing/introduction/naming-conventions.md) impostos pelo AEM e pelo JCR.
      * **Não é possível inserir caracteres inválidos** no campo **Nome**. Quando o AEM detecta caracteres inválidos, o campo é destacado e uma mensagem explicativa é exibida para indicar os caracteres que precisam ser removidos/substituídos.

   >[!TIP]
   >
   >Consulte [Convenções de nomenclatura da página](#page-naming-conventions).

   As informações mínimas necessárias para criar uma página são **Título**.

   ![Fornecimento do título da página](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Use **Criar** para concluir o processo e criar a sua nova página. A caixa de diálogo de confirmação perguntará se você deseja **Abrir** a página imediatamente ou voltar para o console (**concluído**):

   ![Êxito na criação da página](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >Caso crie uma página usando um nome que já existe no local, o sistema vai gerar automaticamente uma variação do nome, ao anexar um número. Por exemplo, se `beach` já existir, uma nova página se tornará `beach1`.

1. Se você retornar ao console, poderá ver sua nova página:

   ![Nova página resultante](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>Assim que uma página tiver sido criada, seu modelo não poderá ser alterado, a menos que você [crie um lançamento com um novo modelo; ](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)porém, o conteúdo existente será perdido.
