---
title: Carregar opções de lista suspensa de um URL ou outra planilha para o Edge Delivery Services para AEM Forms as a Cloud Service
description: As opções da lista suspensa são incluídas em uma planilha distinta e, em seguida, importadas para a planilha principal por meio do URL fornecido.
feature: Edge Delivery Services
exl-id: 5b0bc1b6-6e33-41f3-b7c1-4d997787b6cd
source-git-commit: 8730383d26c6f4fbe31a25a43d33bf314251d267
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---


# Opções de um URL ou outra planilha para o Edge Delivery Services para o AEM Forms as a Cloud Service

O Forms geralmente inclui menus suspensos para que os usuários selecionem entre as opções predefinidas. Normalmente, essas opções são definidas no próprio formulário, mas o gerenciamento de listas longas pode ser complicado. Este guia descreve como melhorar a criação de formulários carregando opções suspensas de uma planilha separada por meio de um URL.


Os benefícios de carregar opções suspensas em uma planilha separada são:

* Gerenciamento simplificado: mantenha as opções suspensas em um local centralizado para facilitar atualizações e adições.
* Maior eficiência: elimine a necessidade de adicionar manualmente longas listas de opções na definição do formulário.




![Opções suspensas](/help/forms/assets/drop-down-options.png)


No final deste artigo, você aprenderá a:

* [Definir opções em uma planilha separada](#define-options)
* [Adicionar URL para carregar opções da lista suspensa](#add-url)

## Definir opções em uma planilha separada {#define-options}

Definição de Opções em uma Planilha Separada

1. Criar uma planilha:
   1. Localize a pasta do projeto AEM no Microsoft® SharePoint ou Google Drive.
   1. Adicione uma nova planilha. Por exemplo, &quot;país compartilhado&quot;.
1. Definir colunas de opção: adicione duas colunas: &quot;Option&quot; e &quot;Value&quot;.
   * &quot;Option&quot; define o texto exibido no menu suspenso.
   * &quot;Value&quot; define o valor enviado quando um usuário seleciona a opção.

   >[!NOTE]
   >
   >Se a opção e o valor forem idênticos, somente a coluna &quot;Option&quot; será necessária.

1. Preencha a Planilha: Informe suas opções de país na coluna &quot;Opção&quot; (e na coluna &quot;Valor&quot;, se necessário).

   Consulte o exemplo abaixo para obter uma estrutura.

   ![Lista suspensa para país](/help/forms/assets/drop-down-country-options.png)

1. Pré-visualizar e publicar o `shared-country` planilha usando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   Consulte o URL que mostra a variável `shared-country` planilha: https://main--wefinance--wkndforms.hlx.live/enquiry.json?sheet=country

>[!NOTE]
>
> `?sheet=country` é um parâmetro de consulta anexado ao URL. Esse parâmetro indica o JSON filtrado com base no `shared-country` planilha. Ele redireciona para o arquivo JSON contendo informações relacionadas a diferentes países.

## Adicionar URL para carregar opções da lista suspensa{#add-url}

A variável `Options` propriedade de um `select` aceita um URL. O URL retorna uma matriz JSON usada como opções para a variável `Destination` lista suspensa. Para adicionar as opções da lista suspensa URL to load:

1. Vá para a pasta do Projeto AEM no Microsoft® SharePoint ou Google Drive e abra a planilha. Você também pode criar uma nova planilha para um formulário.
1. Copie o URL de `shared-country` planilha e cole-a na caixa `Options` coluna para a `Destination` campo.

   ![Planilha de consulta](/help/forms/assets/drop-down-enquiry.png)

1. Visualizar e publicar a planilha usando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).


   ![Lista suspensa para país](/help/forms/assets/load-dropdown-options-form.png)

Você pode consultar a [planilha de consulta](/help/forms/assets/enquiry-options.xlsx) para adicionar as opções da lista suspensa URL to load.

Depois de integrar a URL às opções da lista suspensa Definição de formulário a ser carregado, as opções para a `Destination` início da lista suspensa que aparece no URL.

Consulte o URL abaixo, que exibe a variável `enquiry` formulário exibindo as opções salvas na planilha separada:

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## Consulte também:

{{see-more-forms-eds}}


