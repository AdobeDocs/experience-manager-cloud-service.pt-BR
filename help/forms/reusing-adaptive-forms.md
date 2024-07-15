---
title: Como reutilizar as propriedades de metadados de um formulário adaptável?
description: Descubra a redefinição de objetivo de um Formulário adaptável existente para criar um novo.
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
feature: Adaptive Forms, Foundation Components
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 3%

---

# Reutilizar propriedades de metadados de um Formulário adaptável {#reusing-adaptive-forms}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/reusing-adaptive-forms.html) |
| AEM as a Cloud Service | Este artigo |

Se você quiser usar algumas das propriedades de um Formulário adaptável existente para gerar um novo, basta usar a funcionalidade copiar e colar. Além disso, você pode colar o novo Formulário adaptável no caminho da pasta desejada. Todas as propriedades de metadados são replicadas e o XFA e os XSDs para o Adaptive Forms baseado em XFA e XSD também são copiados.

>[!NOTE]
>
>O status e os detalhes da revisão não são copiados. Por exemplo, se o formulário adaptável for publicado e depois for copiado, o formulário adaptável colado ficará no estado não publicado. Da mesma forma, se um ativo copiado estiver em revisão, o ativo colado não estará na mesma revisão.

## Copiar um formulário adaptável {#copy-an-adaptive-form}

Copie um formulário adaptável usando uma das seguintes abordagens:

1. Clique no ícone copiar ![aem6forms_copy](assets/aem6forms_copy.png) de Ações rápidas.

   >[!NOTE]
   >
   >As ações rápidas são itens de ação exibidos ao passar o mouse sobre uma miniatura.

1. Selecione o Formulário adaptável. O processo de seleção é diferente para diferentes exibições.

   Se você estiver na exibição de cartão, vá para o modo de seleção clicando no ícone de seleção ![aem6forms_check-circle](assets/aem6forms_check-circle.png) e clique em todas as Forms adaptáveis que deseja copiar.

   Se você estiver na exibição em lista, clique nas caixas de seleção de todas as Forms adaptáveis para selecioná-las.

   >[!NOTE]
   >
   >Todos os ativos selecionados devem ser do Adaptive Forms, pois a funcionalidade de copiar e colar é compatível somente com o Adaptive Forms, e todos os ativos selecionados devem estar presentes na mesma pasta.

   Depois de selecionar os ativos, clique no ícone copiar ![aem6forms_copy](assets/aem6forms_copy.png) presente na barra de ferramentas para copiar o formulário adaptável selecionado.

## Colar um formulário adaptável {#paste-an-adaptive-form}

Clicar na ação de cópia sai automaticamente do modo de seleção e torna visível o ícone Colar ![Colar](assets/Smock_Paste_18_N.svg). Agora vá para o caminho de pasta desejado e clique no ícone Colar ![Colar](assets/Smock_Paste_18_N.svg) para colar o Formulário adaptável copiado.

Se você estiver colando na mesma pasta ou se outro arquivo com o mesmo nome de nó (com o qual ele é armazenado no repositório do CRX) existir nessa pasta de destino, 1 será anexado ao sufixo (por exemplo, myaf torna-se myaf1 e se myaf1 existe no mesmo local, myaf torna-se myaf2. Todas as outras propriedades permanecem iguais ao Formulário adaptável original.

Depois de clicar no ícone Colar ![Colar](assets/Smock_Paste_18_N.svg), ele ficará oculto novamente. De uma só vez, só é possível colar uma vez. Para criar uma cópia do mesmo ativo novamente, copie-a novamente.

## Alterar conteúdo do novo Formulário adaptável {#change-contents-of-new-adaptive-form}

O conteúdo de um Forms adaptável colado pode ser alterado usando as seguintes abordagens para torná-lo diferente do formulário copiado:

1. **Alterar propriedades de metadados:**

   É possível alterar as propriedades de metadados do Formulário adaptável, por exemplo, título e descrição. Para obter mais detalhes sobre as propriedades dos metadados e como eles podem ser alterados, consulte [Gerenciando Metadados de Formulário](manage-form-metadata.md)

1. **Alterar XFA/XSD para Forms adaptável baseado em XFA/XSD:**

   Você pode alterar o XFA/XSD usado no Adaptive Forms. Para saber como essas Forms adaptáveis podem ser alteradas, consulte [Gerenciamento de metadados de formulário](manage-form-metadata.md)

1. **Republicar:**

   O ativo colado é diferente do copiado. Você pode publicá-lo como um novo ativo para disponibilizá-lo para os usuários finais. Para saber como publicar um ativo, <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->


## Consulte também {#see-also}

{{see-also}}