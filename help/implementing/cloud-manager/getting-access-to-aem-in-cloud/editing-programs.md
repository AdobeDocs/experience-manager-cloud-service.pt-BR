---
title: Editar Programas
description: Saiba como editar os programas de sandbox e produção para ajustar as opções depois de criá-las.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 1c42dff8efb505d050583c8af2f150a7f862d8c9
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 8%

---


# Editar programas {#editing-programs}

Para gerenciar e editar programas, inicie no console [**Meus Programas**](/help/implementing/cloud-manager/navigation.md). A página **Meus Programas** fornece uma visão geral de todos os programas aos quais você tem acesso. Ao selecionar um programa individual, a página **Visão geral do programa** fornece uma visão geral dos detalhes do programa.

Na **Visão Geral do Programa**, os usuários com as permissões necessárias podem editar [programas de produção criados em sua organização](creating-production-programs.md) e [programas de sandbox criados em sua organização](creating-sandbox-programs.md). Ao editar um programa, você pode fazer o seguinte:

* Adicionar a solução Sites a um programa existente com o Assets e vice-versa.
* Remova o Sites ou o Assets de um programa existente que tenha o Sites e o Assets.
* Adicionar um direito de solução não utilizado a um programa existente ou criar um novo programa.
* Marcar programas de produção para exclusão.
* Excluir programas de sandbox.

## Permissões {#permissions}

Você deve ter a função **Proprietário da empresa** para editar programas, excluir programas de sandbox, marcar programas de produção para exclusão e acessar o Painel de Licenças.

## Editar um programa {#editing}

Sempre que um programa for editado, incluindo a adição ou remoção de uma solução ou complemento, essas alterações entrarão em vigor após a próxima implantação.

**Para editar um programa:**

1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
1. Na seção **Acesso rápido**, clique em **Experience Manager**.
1. No painel lateral esquerdo, clique em **Cloud Manager**.
1. Selecione a organização apropriada.
1. Na página **Meus Programas**, clique no programa que você deseja editar.
1. Próximo ao canto superior esquerdo da página, clique no nome do programa e selecione **Editar programa**.

   ![Opção Editar programa no menu suspenso do Programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/edit-program.png)

1. Na caixa de diálogo **Editar Programa**, use as guias para definir as várias opções desejadas.

   ![Guia Geral](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/edit-program-dialog-box.png)

   As opções disponíveis para editar o programa são as mesmas para a criação do programa.
   * Você pode configurar se um nível de publicação será provisionado para novos ambientes (Beta). Consulte [Nível de publicação flexível (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).
   * Consulte [Criar Programas de Produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) e [Criar Programas de Sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) para obter detalhes sobre as opções individuais.
   * [Opções adicionais](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options) podem estar disponíveis para o programa de produção, dependendo dos direitos da sua organização.

1. Clique em **Atualizar** para salvar as alterações.

## Marcar um programa de produção para exclusão {#delete-production-program}

A exclusão de um programa de produção é um processo de duas fases. Um Proprietário da empresa marca o programa para exclusão, o que aciona um período de validação e remoção. O programa é então removido permanentemente após o término do período de retirada.

Quando um programa de produção é marcado para exclusão, ocorre o seguinte:

* O crédito associado ao programa de produção é devolvido ao cliente.
* Todos os ambientes pertencentes ao programa de produção são removidos.

Antes de iniciar a marcação para exclusão, o sistema valida se o programa de produção é elegível para exclusão. Se a marcação falhar, o programa de produção será movido para um estado `Failed to mark for deletion`.

>[!NOTE]
>
>Os programas de sandbox não são afetados por esse processo. Para excluir um programa de sandbox, consulte [Excluir um programa de sandbox](#delete-sandbox-program).

**Para marcar um programa de produção para exclusão:**

1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
1. Na seção **Acesso rápido**, clique em **Experience Manager**.
1. No painel lateral esquerdo, clique em **Cloud Manager**.
1. Selecione a organização apropriada.
1. Na página **Meus Programas**, para o programa de produção que você deseja marcar para exclusão, clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e em **Excluir programa**.

   ![Selecionar Excluir Programa da lista suspensa de um programa de produção ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete1.png)*O exemplo de programa de produção visto acima serve apenas para fins ilustrativos.*

1. Na caixa de diálogo **Marcar programa de produção para exclusão**, revise o aviso que lista os recursos conectados ao seu programa, incluindo ambientes de produção, preparo e desenvolvimento.

   ![Caixa de diálogo Excluir Programa de Produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete2.png)


   >[!NOTE]
   >
   >Se o programa de produção tiver recursos de bloqueio, como ambientes que estão sendo atualizados no momento, o botão **Marcar para exclusão** será desabilitado. Aguarde até que todos os recursos do programa sejam desbloqueados antes de poder marcar o programa para exclusão.
   >
   >![A caixa de diálogo Marcar programa de produção para exclusão mostra que o programa não pode ser excluído porque tem recursos de bloqueio](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete2b.png)


1. Para confirmar, digite o nome do programa conforme exibido na caixa de diálogo e clique em **Marcar para exclusão**.

   Após a confirmação, o programa de produção mostra um status **Marcação para exclusão** enquanto o processo é executado.

   ![Marcando para status de exclusão](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete3.png)

   Quando concluído, o cartão do programa de produção é atualizado para **Marcado para exclusão** com um selo de Alerta associado.

   ![Marcado para status de exclusão com selo de alerta associado](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete4.png)

1. Clique no selo Alert no cartão do programa de produção para exibir a data programada de remoção permanente.

   ![Exibição da data de remoção permanente agendada do programa de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete5.png)

   Após o término do período de retirada, o programa é removido permanentemente e não pode ser restaurado.

### Desmarcar um programa de produção da exclusão {#unmark-from-deletion}

Você pode restaurar um programa de produção que foi *marcado* para exclusão, desde que a remoção permanente ainda não tenha ocorrido.

>[!IMPORTANT]
>
>Restaurar um programa de produção que foi marcado para exclusão requer que o cliente tenha créditos disponíveis.

**Para desmarcar um programa de produção da exclusão:**

1. Na página **Meus Programas**, localize o cartão de programa de produção que mostra **Marcado para exclusão**.

1. No cartão do programa de produção, clique no ícone ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e em **Desmarcar para exclusão**.

   ![Desmarcando a data de remoção permanente agendada do programa de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-unmarkfordelete6.png)

   O programa de produção não está marcado para exclusão.

## Excluir um programa de sandbox {#delete-sandbox-program}

A exclusão de um programa de sandbox remove todos os ambientes e pipelines associados a ele.

>[!TIP]
>
>Usuários com as funções **Proprietário da empresa** ou **Gerente de implantação** podem, como alternativa, excluir os ambientes de produção e preparo em vez de todo o programa de sandbox.

**Para excluir um programa de sandbox:**

1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
1. Na seção **Acesso rápido**, clique em **Experience Manager**.
1. No painel lateral esquerdo, clique em **Cloud Manager**.
1. Selecione a organização apropriada.

1. Na página **[Meus programas](#my-programs)**, clique no programa de sandbox que você deseja editar para exibir seus detalhes.

1. Clique no nome do programa de sandbox no canto superior esquerdo da página e selecione **Excluir programa**.

   ![Opção Excluir programa](assets/delete-sandbox1.png)

Como alternativa, você pode clicar em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no cartão do programa de sandbox na página de visão geral da Cloud Manager e selecionar **Excluir programa**.

![Excluir sandbox do cartão de programa](assets/delete-sandbox2.png)
