---
title: Reutilizar propriedades de metadados de um Formulário adaptável
seo-title: Reuse metadata properties of an Adaptive Form
description: É possível reutilizar um formulário adaptável existente para criar um novo Forms adaptável.
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 2%

---

# Reutilizar propriedades de metadados de um Formulário adaptável {#reusing-adaptive-forms}

Se você quiser usar algumas das propriedades de um formulário adaptável existente para gerar um novo formulário, basta usar a funcionalidade copiar e colar. Além disso, é possível colar o novo Formulário adaptável no caminho de pasta desejado. Todas as propriedades de metadados são replicadas e os XFA e os XSDs para o Forms adaptável baseado em XFA e XSD também são copiados.

>[!NOTE]
>
>O status e os detalhes da revisão não são copiados. Por exemplo, se o seu formulário adaptativo for publicado e, ao copiá-lo, o formulário adaptável colado estará no estado não publicado. Da mesma forma, se um ativo copiado estiver sob revisão, o ativo colado não estará sob a mesma revisão.

## Copiar um formulário adaptável {#copy-an-adaptive-form}

Copie um formulário adaptável usando uma das seguintes abordagens:

1. Clique em copiar ![aem6forms_copy](assets/aem6forms_copy.png) ícone das Ações rápidas.

   >[!NOTE]
   >
   >As ações rápidas são itens de ação exibidos em uma miniatura ao passar o mouse.

1. Selecione o formulário adaptável. O processo de seleção é diferente para diferentes exibições.

   Se você estiver na exibição de cartão, vá para o modo de seleção clicando na seleção ![aem6forms_check-círculo](assets/aem6forms_check-circle.png) e clique em todos os adaptadores Forms que deseja copiar.

   Se você estiver na exibição em lista, clique nas caixas de seleção de todos os adaptadores Forms para selecioná-los.

   >[!NOTE]
   >
   >Todos os ativos selecionados devem ser do Adaptive Forms, pois a funcionalidade de copiar e colar é compatível somente com o Adaptive Forms e todos os ativos selecionados devem estar presentes na mesma pasta.

   Depois de selecionar os ativos, clique no botão copiar ![aem6forms_copy](assets/aem6forms_copy.png) ícone presente na barra de ferramentas para copiar o formulário adaptável selecionado.

## Colar um formulário adaptável {#paste-an-adaptive-form}

Clicar na ação de cópia sai automaticamente do modo de seleção e faz com que a colagem ![Colar](assets/Smock_Paste_18_N.svg) ícone visível. Agora vá para o caminho da pasta desejada e clique no botão colar ![Colar](assets/Smock_Paste_18_N.svg) ícone para colar o formulário adaptável copiado.

Se você estiver colando na mesma pasta ou em outro arquivo com o mesmo nome de nó (com o qual está armazenado no repositório CRX) existir nessa pasta de destino, 1 será anexado ao sufixo (por exemplo, myaf se torna myaf1 e se myaf1 existir no mesmo local, myaf se torna myaf2. Todas as outras propriedades permanecem iguais ao formulário adaptável original.

Depois de clicar no botão colar ![Colar](assets/Smock_Paste_18_N.svg) ícone , ele ficará novamente oculto. De uma vez, você só pode colar uma vez. Para criar novamente uma cópia do mesmo ativo, copie-o novamente.

## Alterar o conteúdo do novo formulário adaptável {#change-contents-of-new-adaptive-form}

O conteúdo de um Adaptive Forms colado pode ser alterado com as seguintes abordagens para torná-lo diferente do formulário copiado:

1. **Alterar propriedades de metadados:**

   É possível alterar as propriedades de metadados do Formulário adaptável, por exemplo, título e descrição. Para obter mais detalhes sobre as propriedades de metadados e como eles podem ser alterados, consulte [Gerenciamento de metadados de formulário](manage-form-metadata.md)

1. **Altere o XFA/XSD para o Forms adaptável baseado em XFA/XSD:**

   Você pode alterar o XFA/XSD usado no Adaptive Forms. Para saber como essas Forms adaptáveis podem ser alteradas, consulte [Gerenciamento de metadados de formulário](manage-form-metadata.md)

1. **Publicar novamente:**

   O ativo colado é diferente do copiado. Você pode publicá-lo como um novo ativo para torná-lo disponível para os usuários finais. Para saber como publicar um ativo, <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->
