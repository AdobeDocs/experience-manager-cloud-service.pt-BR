---
title: Organizar ativos digitais
description: Organize seus ativos digitais usando vários métodos fornecidos no Adobe Experience Manager Assets.
contentOwner: AG
feature: Gerenciamento de ativos, Marcação, Distribuição de ativos
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 568c25d77eb42f7d5fd3c84d71333e083759712d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# Organizar ativos digitais {#organize-digital-assets}

Todos os ativos digitais, metadados e conteúdo de documentos do Microsoft Office e PDF são extraídos e podem ser pesquisados. A pesquisa permite uma filtragem sofisticada em ativos e respeita completamente as permissões apropriadas. Os metadados são abordados detalhadamente em Metadados no Gerenciamento de ativos digitais.

O Experience Manager Assets é compatível com várias maneiras de organizar o conteúdo. Você pode organizá-las de maneira hierárquica usando pastas ou pode organizá-las de maneira não ordenada e adhoc, usando, por exemplo, tags . Os usuários podem editar tags no Editor de ativos DAM, onde os ativos secundários, as representações e os metadados são exibidos.

## Criar pastas {#create-folders}

Ao organizar uma coleção de ativos, por exemplo, todas as imagens *Nature*, você pode criar pastas para mantê-las juntas. Você pode usar pastas para categorizar e organizar seus ativos. [!DNL Assets] não exige que você organize ativos em pastas para funcionar melhor.

>[!NOTE]
>
>Não há suporte para o compartilhamento de uma pasta de Ativos (no Marketing Cloud) do tipo `sling:OrderedFolder`. Se quiser compartilhar uma pasta, não selecione Solicitado ao criar uma pasta.

1. Navegue até o local na pasta de ativos digitais onde deseja criar uma nova pasta.
1. No menu, clique em **[!UICONTROL Create]**. Selecione **[!UICONTROL Nova Pasta]**.
1. No campo **[!UICONTROL Title]**, forneça um nome de pasta. Por padrão, o DAM usa o título fornecido como o nome da pasta. Depois que a pasta for criada, é possível substituir o padrão e especificar outro nome de pasta.
1. Clique em **[!UICONTROL Criar]**. Sua pasta é exibida na pasta de ativos digitais.

## Adicionar propriedades CUG a pastas {#add-cug-properties-to-folders}

É possível limitar quem pode acessar determinadas pastas no Assets, tornando a pasta parte de um grupo de usuários fechado (CUG). Para fazer uma pasta parte de um CUG:

1. No Assets, clique com o botão direito do mouse na pasta para a qual deseja adicionar propriedades de grupo de usuários fechado e selecione **Properties**.
1. Clique na guia **CUG**.
1. Marque a caixa de seleção **Enabled** para disponibilizar a pasta e seus ativos somente para um grupo de usuários fechado.
1. Navegue até a página de logon, se houver, para adicionar essas informações. Adicione grupos admitidos clicando em **Adicionar item**. Se necessário, adicione o realm. Clique em **OK** para salvar suas alterações.

## Usar tags para organizar ativos {#use-tags-to-organize-assets}

Você pode usar pastas ou tags ou ambas para organizar ativos. Adicionar tags a ativos facilita sua recuperação durante uma pesquisa. Para adicionar tags a um ativo, siga estas etapas:

1. No Digital Asset Manager, clique duas vezes no ativo para abri-lo.
1. Na área **Tags**, abra o menu para revelar as tags disponíveis. Selecione as tags conforme apropriado. Para excluir uma tag, passe o ponteiro do mouse sobre ela e clique em `X` para excluí-la.
1. Clique em **Salvar** para salvar quaisquer tags adicionadas.
