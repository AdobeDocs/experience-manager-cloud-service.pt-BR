---
title: Criar e gerenciar revisões em formulários
seo-title: Creating and managing reviews in forms
description: Uma Revisão é um mecanismo que permite a um ou mais revisores comentar um ativo que está disponível em um formulário.
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
topic-tags: forms-manager
source-git-commit: 400e9fa0263b3e9bdae10dc80d524b291f99496d
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Criar e gerenciar revisões de ativos nos formulários{#creating-and-managing-reviews-for-assets-in-forms}

## Análise {#review}

Uma revisão é um mecanismo que permite a um ou mais revisores comentar um ativo que está disponível em um formulário.

## Configurar uma revisão {#setting-up-a-review}

1. Navegue até a guia Forms e selecione um formulário.
1. Se o Formulário não tiver uma revisão em andamento, uma revisão de Início ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) é exibido na barra Ação. Clique em Iniciar revisão ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) ícone .
1. Insira as seguintes informações:

   * Título: Obrigatório, Pode conter caracteres alfanuméricos, hífen ou sublinhado.
   * Descrição: Opcional, descrição da finalidade/conteúdo para revisão.
   * Prazo: Opcional, a data em que a revisão termina. Quando terminar o prazo, a tarefa aparecerá como &quot;Vencida&quot;.
   * Revisores: Um mínimo de um é obrigatório. A digitação de um nome de grupo ou de um nome de usuário lista todos os nomes correspondentes, exceto o grupo de usuários do serviço. selecione um nome e clique em Adicionar.

1. Clique em Start para iniciar uma revisão.

>[!NOTE]
>
>* O administrador pode acessar qualquer grupo associado aos usuários do Formulário .
>* O grupo Usuários do Serviço não está disponível para seleção para revisão.


### Ações que ocorrem quando uma revisão é configurada {#actions-that-occur-when-a-review-is-set-up}

Esta seção descreve o que acontece quando uma revisão é criada ou configurada.

1. Uma nova tarefa de revisão é criada e atribuída ao revisor selecionado.
1. Todos os revisores recebem uma tarefa de revisão. A tarefa é exibida na seção Notifications. Um revisor pode clicar em uma notificação ou ir para a Caixa de entrada para exibir a tarefa. Um revisor pode clicar em para abrir a tarefa de revisão, exibir o formulário e começar a adicionar comentários.

   ![Alerta de notificação do revisor](assets/review-notification-img.png)

   Alerta de notificação do revisor

1. A caixa de comentários está disponível para os revisores do Formulário. Outros podem exibir os comentários, mas não podem escrever comentários.

## Gerenciamento de uma revisão {#managing-a-review}

>[!NOTE]
>
>Somente as revisões em andamento podem ser modificadas. As revisões concluídas não podem ser modificadas.

1. Navegue até a guia Forms e selecione um formulário.

1. Se um ativo tiver uma revisão em andamento e você for o iniciador da revisão, uma Análise de gerenciamento ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) ícones é exibido na barra Ação. Somente o iniciador de revisão pode gerenciar (Atualizar/Fim) a revisão.

   Clique em Gerenciar revisão ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)ícone .

   Para outro usuário que não iniciador, o ícone Gerenciar Revisão está desativado.

1. Você recebe uma tela que exibe informações:

   * **Título**: Não pode ser editado.

   * **Descrição**: Disponível para edição.

   * **Prazo**: Disponível para edição. É possível modificar o prazo para qualquer data e hora além da data e hora atuais.

   * **Nome do revisor**: Disponível para edição. Você pode adicionar ou remover revisores. Se uma tarefa estiver vencida, você poderá adicionar revisores somente após estender o prazo além da data atual.

1. Edite os campos necessários e clique em Concluído.

   ![Rever o estado atualizado no Gerenciador de Tarefas](assets/manage-review-img.png)

   Rever o estado atualizado no Gerenciador de Tarefas

1. Para encerrar a revisão, clique em Finalizar revisão.

### Ações que ocorrem quando uma revisão é modificada {#actions-that-occur-when-a-review-is-modified}

Esta seção descreve o que acontece em Revisar atualização/fim:

1. Se a descrição Revisar for modificada, a tarefa correspondente dos revisores e o iniciador serão atualizados.
1. Se o prazo de Revisão for modificado, a tarefa correspondente dos revisores será atualizada com a nova data.

1. Se um revisor for removido:

   ![Remover um revisor](assets/removeduser.png)

   Remover um revisor

   1. Se estiver incompleta, a tarefa atribuída será encerrada.
   1. O revisor não pode mais comentar no formulário.

1. Se um revisor for adicionado:

   ![Adicionar um revisor](assets/addedreviewer.png)

   Adicionar um revisor

   1. Uma tarefa de revisão é criada e atribuída ao revisor recém-adicionado.
   1. O revisor recém-adicionado pode adicionar comentários sobre o formulário.

1. Quando uma revisão termina:

   1. **Revisores**: Para cada revisor, a tarefa incompleta relacionada à revisão é encerrada. A tarefa não é mais exibida como &quot;Pendente&quot; na seção Notificações do revisor.
   1. **Iniciador**: A tarefa atribuída ao iniciador Revisar está marcada como concluída. A tarefa é removida da seção Notification do iniciador de revisão.
   1. **Todos**: A revisão é exibida na seção Revisões anteriores . Não podem ser acrescentadas outras observações.
      ![revisão concluída](assets/review-complete-imgg.png)


