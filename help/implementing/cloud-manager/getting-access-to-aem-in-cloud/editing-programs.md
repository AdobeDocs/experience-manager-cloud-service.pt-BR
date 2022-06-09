---
title: Programas de edição
description: Saiba como editar a produção e os programas de sandbox para ajustar as opções depois de criá-las.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: d805ed744af0e5c95863a1c67439b384cc5d11b2
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Programas de edição {#editing-programs}

Os usuários com permissões necessárias podem editar [programas de produção criados em sua organização](creating-production-programs.md) bem como [programas sandbox criados em sua organização.](creating-sandbox-programs.md) Ao editar um programa, você pode:

* Adicionar a solução Sites a um programa existente com Ativos e vice-versa.
* Remova Sites ou Ativos de um programa existente com Sites e Ativos.
* Adicione um segundo direito de solução não utilizado a um programa existente ou como um novo Programa.
* Exclua programas de sandbox.

>[!NOTE]
>
>Você deve ser um membro do **Proprietário da empresa** função para editar programas ou excluir programas sandbox.

Siga estas etapas para editar um programa.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada.

1. Clique no programa que deseja editar para exibir seus detalhes.

1. Clique no nome do seu programa no canto superior esquerdo da página e selecione **Editar programa**.

   ![Opção Editar programa](assets/edit-program-overview.png)

1. O **Editar programa** será aberta. No **Geral** , edite o nome e a descrição do programa.

   * Pelo menos uma solução deve ser selecionada para um programa.

   ![Guia General](assets/edit-program-prod1.png)

1. No **Soluções e complementos** , modifique as soluções do programa.

   ![Selecionar soluções](assets/edit-prg.png)

1. Clique na divisa antes dos nomes da solução para exibir os complementos opcionais, como selecionar a **Comércio** opção complementar em **Sites**.

   ![Editar complementos](assets/edit-program-add-on.png)

1. No **Ativar configurações** , modifique a data de ativação planejada para o programa.

   ![Editar configurações dinâmicas](assets/edit-program-go-live.png)

   * Esta data é somente para uso informativo e aciona o widget Ir ao vivo na página de visão geral do programa para fornecer links no produto para AEM documentação de práticas recomendadas as a Cloud Service em tempo hábil para se alinhar com sua jornada, resultando em uma experiência de ativação bem-sucedida e suave.

1. Clique em **Atualizar** para salvar as alterações no programa.

Sempre que um programa for editado, incluindo a adição ou remoção de uma solução ou complemento, essas alterações entrarão em vigor após a próxima implantação.

## Exclusão de programas de sandbox {#delete-sandbox-program}

A exclusão de um programa sandbox removerá todos os ambientes e pipelines associados a ele.

>[!TIP]
>
>Usuários com a **Proprietário da empresa** ou **Gerenciador de implantação** as funções podem, alternativamente, excluir os ambientes de produção e preparo em vez do programa sandbox inteiro.

Siga estas etapas para excluir um programa sandbox.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada.

1. Clique no programa que deseja editar para exibir seus detalhes.

1. Clique no nome do seu programa no canto superior esquerdo da página e selecione **Excluir programa**.

   ![Opção Excluir programa](assets/delete-sandbox1.png)

Como alternativa, você pode clicar no botão de reticências no cartão do programa na página de visão geral do Cloud Manager e selecionar **Excluir programa**.

![Excluir sandbox do cartão de programa](assets/delete-sandbox2.png)

>[!NOTE]
>
>Somente programas de sandbox podem ser excluídos. Os programas de produção não podem ser excluídos.
