---
title: Programas de edição
description: Saiba como editar os programas de sandbox e produção para ajustar as opções depois de criá-las.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: ecb168e9261b3e3ed89e4cbe430b3da9f777a795
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 44%

---

# Programas de edição {#editing-programs}

Os usuários com as permissões necessárias podem editar [programas de produção criados em sua organização](creating-production-programs.md) e [programas de sandbox criados em sua organização.](creating-sandbox-programs.md) Ao editar um programa, você pode:

* Adicionar a solução Sites a um programa existente com Assets e vice-versa.
* Remover sites ou ativos de um programa existente usando o Sites e o Assets.
* Adicionar um segundo direito de solução não utilizado a um programa existente ou como um novo programa.
* Excluir programas de sandbox.

## Permissões {#permissions}

Você deve ser um membro com a função **Proprietário da empresa** para editar ou excluir programas de sandbox.

## Edição de um programa {#editing}

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa que deseja editar para exibir seus detalhes.

1. Clique no nome do programa no canto superior esquerdo da página e selecione **Editar programa**.

   ![Opção Editar programa](assets/edit-program-overview.png)

1. A página **Editar programa** será aberta. Na guia **Geral**, edite o nome e a descrição do programa.

   * Pelo menos uma solução deve ser selecionada para um programa.

   ![Guia Geral](assets/edit-program-prod1.png)

1. Na guia **Soluções e complementos**, modifique as soluções do programa.

   ![Selecionar soluções](assets/edit-prg.png)

1. Clique na divisa antes do nome da solução para exibir os complementos opcionais, como selecionar o **Commerce** opção complementar em **Sites**.

   ![Editar complementos](assets/edit-program-add-on.png)

1. Na guia **Configurações de publicação**, modifique a data de publicação planejada para o programa.

   ![Editar configurações de publicação](assets/edit-program-go-live.png)

   * Esta data é apenas para fins informativos. Ele aciona o widget de publicação na página de visão geral do programa. Por sua vez, ele fornece links para a documentação de práticas as a Cloud Service do Adobe Experience Manager (AEM) para alinhar-se à sua jornada, resultando em uma experiência de ativação bem-sucedida.
   * Esta guia não está disponível para programas de sandbox.

1. Se os direitos necessários estiverem disponíveis para o programa, a **Segurança** mostrará onde você pode modificar as opções de segurança do programa.

   ![Editar configurações de segurança](assets/edit-program-security.png)

   * O HIPAA não pode ser habilitado ou desabilitado após [criação do programa.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
      * [Saiba mais](https://www.adobe.com/go/hipaa-ready) sobre a solução de implementação pronta para HIPAA da Adobe.
   * Uma vez ativada, a proteção WAF-DDOS pode ser configurada configurando um [pipeline de não produção.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

   {{waf-limited-release}}

1. Clique em **Atualizar** para salvar as alterações no programa.

Sempre que um programa for editado, incluindo a adição ou remoção de uma solução ou complemento, essas alterações entrarão em vigor após a próxima implantação.

## Exclusão de programas de sandbox {#delete-sandbox-program}

A exclusão de um programa de sandbox remove todos os ambientes e pipelines associados a ele.

>[!TIP]
>
>Usuários com as funções **Proprietário da empresa** ou **Gerente de implantação** podem, como alternativa, excluir os ambientes de produção e preparo em vez de todo o programa de sandbox.

Para excluir um programa de sandbox, faça o seguinte.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa que deseja editar para exibir seus detalhes.

1. Clique no nome do programa no canto superior esquerdo da página e selecione **Excluir programa**.

   ![Opção Excluir programa](assets/delete-sandbox1.png)

Como alternativa, você pode clicar no botão de reticências no cartão do programa na página de visão geral do Cloud Manager e selecionar **Excluir programa**.

![Excluir sandbox do cartão de programa](assets/delete-sandbox2.png)

>[!NOTE]
>
>Somente programas de sandbox podem ser excluídos. Os programas de produção não podem ser excluídos.
