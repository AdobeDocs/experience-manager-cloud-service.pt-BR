---
title: Associar revisores de envio a um formulário
seo-title: Associating submission reviewers with a form
description: Saiba como associar revisores de envio a um formulário em [!DNL AEM Forms]. Os revisores associados revisam um formulário enviado pelo portal de formulários.
seo-description: Learn how to associate submission reviewers with a form in [!DNL AEM Forms]. Associated reviewers review a form submitted via forms portal.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Associar revisores de envio a um formulário {#associating-submission-reviewers-with-a-form}

Ao criar um formulário, você pode especificar usuários que revisam os envios do formulário por meio do portal de formulários e fornecer feedback. Sua organização pode coletar comentários e trabalhar novamente nos formulários enviados.

[!DNL AEM Forms] permite associar um grupo de revisores a um formulário. Os usuários adicionados a um grupo de revisão de um formulário visualizam os envios desse formulário e fornecem feedback.

Os grupos de revisores atribuídos a um formulário só podem revisar os envios do formulário especificado.

## Pré-requisitos {#prerequisite}

### Ativação da propriedade de grupos do revisor de envio para o Adaptive Forms usando o editor de esquema de metadados {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Para associar um grupo de revisores a um formulário, edite o esquema de metadados do Adaptive Forms. Por padrão, não é possível adicionar um grupo de revisores a um formulário enviado.

Para editar o esquema de metadados:

1. No modo de autor, em Experience Manager, clique em **Ferramentas** > **Ativos** > **Esquemas de metadados**.
1. Na página Schema Forms , navegue até **Forms** > **Forms Autorizado em AEM.**

   O URL da página é:

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Selecionar **Formulário adaptável** e clique em **Editar**.
1. Na página Editar formulário , clique em **Avançado**.
1. Na guia Avançado , arraste e solte a **Texto de linha única** componente disponível em Criar formulário.
1. Selecione o componente de texto adicionado para ver suas configurações.

   Em Configurações, digite `./jcr:content/metadata/form-submission-reviewer-group` no campo Mapear para propriedade .

   O campo de grupo do revisor de envio nas propriedades Avançadas do Formulário adaptável é ativado com o nome que você especifica em Rótulo do campo.

## Associar revisores de envio a um formulário {#associating-submission-reviewers-with-a-form-1}

Para associar revisores de envio a um Formulário adaptável, crie um grupo de revisores e adicione usuários a ele. Adicione o grupo de revisores criado no campo do revisor de envio de formulário nas propriedades avançadas do formulário.
Os grupos de usuários permitem associar diferentes conjuntos de revisores de envio com diferentes Forms adaptáveis. Esse recurso impede uma análise de envio de um usuário não autorizado.

Antes de executar as etapas a seguir, consulte [Pré-requisito](adding-reviewers-form.md#prerequisite).

Para criar um grupo e adicionar membros a ele, navegue até **Ferramentas** > **Operações** > **Segurança** > **Grupos**.
Para obter mais informações, consulte [Administração e serviços do usuário](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).
Certifique-se de adicionar o grupo criado como membro do grupo de usuários predefinido: **forms-submit-revisores**. Este grupo de usuários é enviado com [!DNL AEM Forms]e garante que os usuários sejam adicionados como revisores de envio.

Para associar grupos de usuários a um Formulário adaptável:

1. No modo de criação, navegue até **Forms** > **Forms &amp; Documents**.
1. Use a opção **Selecionar **para selecionar um formulário adaptável e clique em **Propriedades da exibição**.
1. Na janela Propriedades do formulário, clique em **Editar** e, em seguida, clique em **AVANÇADO**.
1. Insira o grupo no campo de grupo do revisor de envio e clique em **Concluído**.

   O campo de grupo do revisor de envio aparece com o nome especificado no esquema de metadados editado do Adaptive Forms.

>[!NOTE]
>
>Replicar usuários e formulários para garantir a disponibilidade dos usuários e formulários na implementação remota de [!DNL AEM Forms].
>
>Certifique-se de que todos os usuários sejam replicados como membros de revisão dos grupos de usuários na implementação remota.

