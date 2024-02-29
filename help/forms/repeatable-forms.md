---
description: Este tutorial inclui instruções para tornar uma seção de um formulário repetível
title: Seções repetíveis no Edge Delivery Services
feature: Edge Delivery Services
source-git-commit: 3b24d0cd4099e0b8eb48c977f460b25c168af220
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Seções repetíveis na entrega de borda

Uma seção repetível é um componente de um formulário que é duplicado ou replicado várias vezes para coletar informações de várias ocorrências dos mesmos dados.

Por exemplo, considere um formulário usado para coletar informações de usuários que solicitam um empréstimo. O formulário permite que os usuários forneçam informações pessoais, incluindo detalhes dos coemprestadores. Os usuários podem inserir detalhes para cocandidatos, sendo que esta seção pode ser repetida.

![Seções repetíveis em formulários](/help/forms/assets/eds-repeatable.png)

## Pré-requisitos

Configure o projeto Github do Serviço de entrega de borda (EDS) usando a placa intermediária AEM e clone o repositório Github correspondente no computador local. Consulte [tutorial do desenvolvedor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/build/tutorial.html) para obter detalhes.

## Seções repetíveis na entrega de borda

Vamos ver um exemplo de um formulário de pedido de empréstimo. O formulário permite que os usuários enviem informações pessoais. É possível incluir detalhes do cocandidato usando seções repetíveis, com a opção de adicionar no mínimo e no máximo três seções de cocandidatos.

>[!NOTE]
>
> * Você pode criar um Excel do Microsoft em seu site do SharePoint ou na Unidade de Google para fazer com que os conjuntos de campos possam ser repetidos em um formulário.
> * Nesse caso, estamos tomando o exemplo de um Microsoft SharePoint. Para tornar sua pasta do SharePoint a fonte de conteúdo, siga as etapas conforme explicado em [Como usar o Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint).


Para adicionar seções repetíveis no Edge Delivery:

1. [Criar um formulário usando o Microsoft Excel](#author-form)
2. [Pré-visualizar e publicar o formulário](#preview-form)

### Criar um formulário usando o Microsoft Excel {#author-form}

1. Vá para sua conta do Microsoft SharePoint e abra ou crie o diretório do projeto AEM Edge Delivery.
2. Abra um arquivo existente do Microsoft Excel ou crie um novo.
Neste exemplo, estamos usando uma planilha do Excel chamada `loan-application.xlsx` criado no site Microsoft SharePoint.
3. Adicionar novas colunas rotuladas como `Repeatable`, `Min`, e `Max` no arquivo do Microsoft Excel.
4. Especifique o valor para o `Repeatable` coluna como `True` para o conjunto de campos que você deseja tornar repetível.
5. Especifique os valores para o `Min` e `Max` colunas. A variável `Min` representa o número mínimo de ocorrências para as quais o painel se repete, enquanto o valor `Max` valor representa o número máximo de ocorrências para as quais o painel se repete.
6. Salve o arquivo do Microsoft Excel.

>[!NOTE]
>
> Aqui está o [Pedido de empréstimo](/help/forms/assets/loan-application.xlsx) planilha do excel para sua referência.

### Pré-visualizar/publicar o formulário usando seu Serviço de entrega de borda

1. Abra ou crie um novo arquivo de documento em um site do Microsoft SharePoint para incorporar a planilha do Excel usando um `Form Block`. Por exemplo, abra `index` arquivo e adicionar um `Form Block`.
2. Abra o prompt de comando, navegue até o diretório do projeto AEM Edge Delivery no computador local e execute o comando como `aem up`.

O formulário pode ser acessado em `https://localhost:3000`, onde se clica em `Add` O botão adiciona nova seção repetível para inserir detalhes do cocandidato. Você também pode excluir a seção que pode ser repetida clicando no `Delete` botão.

>[!NOTE]
>
> Se você encontrar um erro &quot;Página não encontrada&quot; ao acessar seu formulário no localhost, adicione o nome do diretório do site do Microsoft SharePoint na frente da URL em que seu formulário está localizado. Por exemplo, `http://localhost:3000/<dir-name>/`




