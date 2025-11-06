---
title: Adicionar seções repetíveis a um formulário
description: Adicionar seções repetíveis a um formulário EDS
feature: Edge Delivery Services
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Adicionar seções repetíveis a um formulário

O bloco adaptável do Forms fornece a capacidade de adicionar ou fazer uma seção ou um componente de um formulário repetível. Isso permite que os usuários insiram informações várias vezes para o mesmo tipo de dados, facilitando a coleta de informações, como experiência de trabalho ou histórico educacional.

Por exemplo, considere um formulário usado para coletar informações sobre a experiência profissional de uma pessoa. Você pode ter uma seção repetível para capturar detalhes de cada tarefa anterior. A seção repetível normalmente contém campos como nome da empresa, título do cargo, datas de emprego e responsabilidades do cargo. O usuário pode adicionar várias instâncias da seção repetível para inserir informações sobre cada cargo que manteve.

No final deste artigo, você aprenderá a:

- [Criar uma seção repetível em um formulário](#add-repeatable-sections-to-a-form)
- [Definir o número mínimo ou máximo de repetições em um formulário](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## Criar uma seção repetível

A criação de uma seção repetível em um formulário oferece aos usuários a capacidade de inserir várias instâncias do mesmo conjunto de dados, permitindo a coleta eficiente de informações repetitivas. Para criar uma seção repetível em um formulário:

1. Vá para a pasta do projeto do Edge Deliver no Microsoft SharePoint ou Google Workspace e abra a planilha.

1. Adicionar um campo de formulário com a propriedade `type` definida como `fieldset`
1. Especifique `Name` do campo. A propriedade name é usada para criar uma seção repetível.
1. Habilite a repetibilidade definindo `repeatable` como `true`.
1. Especifique um `label` descritivo para o campo. Ele serve como o cabeçalho da seção repetível.

   Consulte a imagem abaixo para obter uma ilustração de uma seção de histórico de emprego em um formulário de requisição de cargo.

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. Para cada campo que você deseja incluir na seção, defina sua propriedade `Fieldset` com o mesmo nome que você escolheu na etapa 3.

   Por exemplo, designe `experience` na propriedade Fieldset de todos os campos relevantes a serem incluídos na seção `employment history`.

   ![exemplo de um campo de seção repetível e suas propriedades](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. Use o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar e publicar a planilha. A seção repetível é adicionada ao formulário.

   Abaixo da seção repetível, os usuários encontram um botão intuitivo **Adicionar**, que facilita a adição de várias seções com facilidade.

   ![seção repetível, botão Adicionar, para adicionar várias seções ](/help/edge/assets/repeatable-section-example.png)


## Definindo Repetições Mínimas e Máximas

No design do formulário, é benéfico definir repetições mínimas e máximas para seções repetíveis. Ao fazer isso, você estabelece controle e consistência e, ao mesmo tempo, orienta os usuários com eficiência. Para definir o número mínimo ou máximo de repetições:

1. Vá para a pasta do projeto do Edge Deliver no Microsoft SharePoint ou Google Workspace e abra a planilha.

1. Para um campo de `type` `fieldset` e propriedade `repeatable` definida como `true`:

   - defina a propriedade `min` para especificar o número mínimo de vezes que a seção pode ser repetida.

   - defina a propriedade `max` para especificar o número máximo de vezes que a seção pode ser repetida.

   ![Defina as propriedades min e max para especificar o número de vezes que a seção pode ser repetida](/help/edge/assets/repeatable-section-set-min-max.png)

1. Use o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar e publicar a planilha.

   Ao adicionar uma seção repetível, os usuários encontram um ícone intuitivo **Excluir**, facilitando a remoção de seções repetíveis. Depois de adicionadas, essas seções não podem ser diminuídas para menos instâncias do que o especificado pela propriedade `min`. Isso garante a adesão ao requisito mínimo definido para o preenchimento do formulário.


