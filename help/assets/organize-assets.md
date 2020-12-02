---
title: Organizar ativos digitais
description: Organize seus ativos digitais usando vários métodos fornecidos no Adobe Experience Manager Assets.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9c5dd93be316417014fc665cc813a0d83c3fac6f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# Organizar ativos digitais {#organize-digital-assets}

Todos os ativos digitais, metadados e conteúdo de documentos do Microsoft Office e PDF são extraídos e tornados pesquisáveis. A pesquisa permite a filtragem sofisticada de ativos e respeita totalmente as permissões adequadas. Os metadados são abordados detalhadamente em Metadados no Gerenciamento de ativos digitais.

A AEM Assets oferece suporte a várias maneiras de organizar o conteúdo. Você pode organizá-las de maneira hierárquica usando pastas ou pode organizá-las de maneira não ordenada e ad hoc, usando, por exemplo, tags. Os usuários podem editar tags no DAM Asset Editor, onde subativos, representações e metadados são exibidos.

## Criar pastas {#create-folders}

Ao organizar uma coleção de ativos, por exemplo, todas as imagens *Nature*, você pode criar pastas para mantê-las juntas. Você pode usar pastas para categorizar e organizar seus ativos. A AEM Assets não exige que você organize ativos em pastas para trabalhar melhor.

>[!NOTE]
>
>Não há suporte para o compartilhamento de uma pasta Assets (no Marketing Cloud) do tipo `sling:OrderedFolder`. Se quiser compartilhar uma pasta, não selecione Solicitado ao criar uma pasta.

1. Navegue até o local na pasta de ativos digitais onde deseja criar uma nova pasta.
1. No menu, clique em **[!UICONTROL Criar]**. Selecione **[!UICONTROL Nova pasta]**.
1. No campo **[!UICONTROL Title]**, forneça um nome de pasta. Por padrão, o DAM usa o título fornecido como o nome da pasta. Depois que a pasta for criada, você poderá substituir o padrão e especificar outro nome de pasta.
1. Clique em **[!UICONTROL Criar]**. Sua pasta é exibida na pasta de ativos digitais.

## Adicionar propriedades CUG a pastas {#add-cug-properties-to-folders}

Você pode limitar quem pode acessar determinadas pastas no Assets, tornando a pasta parte de um grupo de usuários fechado (CUG). Para tornar uma pasta parte de um CUG:

1. Em Ativos, clique com o botão direito do mouse na pasta para a qual deseja adicionar propriedades de grupo de usuários fechadas e selecione **Propriedades**.
1. Clique na guia **CUG**.
1. Marque a caixa de seleção **Ativado** para disponibilizar a pasta e seus ativos somente para um grupo de usuários fechado.
1. Navegue até a página de logon, se houver, para adicionar essas informações. Adicione grupos admitidos clicando em **Adicionar item**. Se necessário, adicione o realm. Clique em **OK** para salvar suas alterações.

## Usar tags para organizar ativos {#use-tags-to-organize-assets}

Você pode usar pastas ou tags ou ambas para organizar ativos. A adição de tags a ativos facilita sua recuperação durante uma pesquisa. Para adicionar tags a um ativo, siga estas etapas:

1. No Digital Asset Manager, clique com o duplo do mouse no ativo para abri-lo.
1. Na área **Tags**, abra o menu para revelar as tags disponíveis. Selecione as tags conforme apropriado. Para excluir uma tag, passe o ponteiro do mouse sobre ela e clique em `X` para excluí-la.
1. Clique em **Salvar** para salvar quaisquer tags adicionadas.
