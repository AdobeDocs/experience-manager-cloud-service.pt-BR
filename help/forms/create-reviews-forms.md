---
title: Como criar e gerenciar revisões em formulários?
description: Use o mecanismo de revisão para adicionar revisores e permitir que os revisores comentem em um formulário.
topic-tags: forms-manager
feature: Adaptive Forms, Foundation Components
exl-id: 378049f8-bf21-4595-819d-ba5fba7023c0
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 2%

---

# Criar e gerenciar revisões em formulários{#creating-and-managing-reviews-to-forms}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve uma abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/create-reviews-forms.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

## Revisar {#review}

Uma revisão é um mecanismo que permite que um ou mais revisores comentem formulários.

## Configurar uma revisão {#setting-up-a-review}

1. Navegue até o navegador de formulários e selecione um formulário para revisão.
1. Se o Formulário não tiver uma revisão em andamento, um ícone **Iniciar Revisão** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) será exibido na barra de Ações. Clique no ícone **Iniciar revisão** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png).
1. Insira as seguintes informações:

   * **Título**: obrigatório, pode conter caracteres alfanuméricos, hífen e sublinhado.
   * **Descrição**: opcional, descrição da finalidade/conteúdo para revisão.
   * **Prazo**: opcional, a data em que a revisão termina. Quando ultrapassado o prazo, a tarefa aparece como &#39;Vencida&#39;.
   * **Nome do Revisor**: no mínimo um é obrigatório. Use a caixa de combinação para adicionar revisores, digitando uma lista de nomes com todos os nomes correspondentes; selecione um nome e clique em **Adicionar**. Na próxima seção da guia **Revisores**, os nomes de todos os revisores serão exibidos.

1. Clique em **Iniciar** para iniciar uma revisão.

   >[!NOTE]
   >
   >* O administrador pode acessar qualquer grupo associado aos usuários do formulário.
   >* O grupo Usuários de Serviço não está disponível para seleção para revisão.

### Ações que ocorrem quando uma revisão é configurada {#actions-that-occur-when-a-review-is-set-up}

Esta seção descreve o que acontece quando uma revisão é criada ou configurada.

1. Uma nova tarefa de revisão é criada e atribuída ao revisor selecionado.
1. Todos os revisores recebem uma tarefa de revisão. A tarefa é exibida na seção Notificações. Um revisor pode clicar em uma notificação ou ir para a Caixa de entrada para exibir a tarefa. Um revisor pode clicar em para abrir a tarefa de revisão, exibir o formulário e começar a adicionar comentários.

   ![Alerta de Notificação do Revisor](assets/review-notification-img.png)

   Alerta de notificação do revisor

1. A caixa comment está disponível para os revisores do formulário. Outras pessoas podem ler os comentários, mas não podem adicionar os seus próprios.

## Gerenciamento de uma revisão {#managing-a-review}

>[!NOTE]
>
>* Somente as revisões em andamento podem ser modificadas.
>* As revisões concluídas não podem ser modificadas.

1. Navegue até a guia formulários e selecione um formulário.

1. Se um formulário tiver uma revisão em andamento e você for o iniciador da revisão, um ícone **Gerenciar revisão** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) aparecerá na barra de ações. Somente o iniciador da revisão pode gerenciar (Atualizar/Encerrar) a revisão.

   Clique no ícone **Gerenciar revisão** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png).

   Para usuários diferentes do iniciador, o ícone Gerenciar revisão está desativado.

1. Agora você obtém uma tela que exibe informações:

   * **Nome da revisão**: não pode ser editado.

   * **Descrição da revisão**: disponível para edição.

   * **Prazo da revisão**: disponível para edição. É possível modificar o prazo para qualquer data e hora além da data e hora atuais.

   * **Revisores**: disponíveis para edição. É possível adicionar ou remover revisores. Se uma tarefa estiver vencida, você poderá adicionar revisores somente depois de estender o prazo além da data atual.

1. Para encerrar a revisão, clique em **Fim**.

### Ações que ocorrem quando uma revisão é modificada {#actions-that-occur-when-a-review-is-modified}

Esta seção descreve o que acontece em **Atualização/Fim da Revisão**:

1. Se a descrição da revisão for modificada, a tarefa correspondente dos revisores e do iniciador será atualizada.
1. Se o prazo da revisão for modificado, a tarefa correspondente para os revisores será atualizada com a nova data.

1. Se um revisor for removido:

   ![Removendo um revisor](assets/removeduser.png)

   Remover um revisor

   1. Se estiver incompleta, a tarefa atribuída será encerrada.
   1. O revisor não pode mais comentar no formulário.

1. Se um revisor for adicionado:

   ![Adicionando um revisor](assets/addedreviewer.png)

   Adicionar um revisor

   1. Uma tarefa de revisão é criada e atribuída ao revisor recém-adicionado.
   1. O revisor recém-adicionado pode adicionar comentários sobre o formulário.

1. Quando uma revisão termina:

   1. **Revisores**: para cada revisor, a tarefa incompleta relacionada à revisão é encerrada. A tarefa não aparece mais como &#39;Pendente&#39; na seção Notificações do revisor.
   1. **Iniciador**: a tarefa atribuída ao iniciador da revisão está marcada como concluída. A tarefa é removida da seção Notificação do iniciador da revisão.
   1. **Todos**: a revisão aparece na seção Análises Anteriores. Nenhum comentário adicional pode ser adicionado.

   ![revisão concluída](assets/review-complete-imgg.png)


## Consulte também {#see-also}

{{see-also}}


<!--

>[!MORELIKETHIS]
>
>* [Associating submission reviewers with a form](/help/forms/adding-reviewers-form.md)

-->