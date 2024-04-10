---
title: Carregar opções de lista suspensa do URL
description: As opções da lista suspensa são incluídas em uma planilha distinta e, em seguida, importadas para a planilha principal por meio do URL fornecido.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# Carregar opções de lista suspensa do URL

Nos Edge Delivery Services, os usuários têm a opção de selecionar um valor em um conjunto predefinido de opções. Os autores do formulário usam o `select` elemento, que fornece uma lista de opções.
Por exemplo, a variável `enquiry` O formulário apresenta um menu suspenso para selecionar países, oferecendo aos usuários uma variedade de países predefinidos para escolher. Esta lista é composta por uma longa lista de países separados por vírgulas.

![Opções suspensas](/help/forms/assets/drop-down-options.png)

O gerenciamento de longas listas de opções para menus suspensos pode ser complicado ao adicioná-los diretamente à planilha que contém a definição do formulário. Criar uma planilha separada para armazenar essas opções suspensas pode simplificar e simplificar o processo. Essa planilha atua como um repositório centralizado para todas as opções suspensas, organizadas em um formato estruturado. Cada opção é listada em sua própria linha, facilitando o gerenciamento e as atualizações.

Vamos explorar a melhoria do processo de criação de formulários carregando a lista de opções de outra planilha por meio de um URL.

No final deste artigo, você aprenderá a:

* [Definir opções em uma planilha separada](#define-options)
* [Adicionar URL para carregar opções da lista suspensa](#add-url)

## Definir opções em uma planilha separada {#define-options}

Crie uma planilha com duas colunas:`Option` e `Value`, para definir as opções:

1. Vá para a pasta do Projeto AEM na Microsoft® SharePoint ou na pasta Google Drive.
2. Adicionar uma planilha com nome `shared-country` no site Microsoft® SharePoint ou na pasta Google Drive e adicione o seguinte:

   * **Opção**: representa os valores de exibição das opções no menu suspenso.
   * **Valor**: representa o valor enviado quando um usuário seleciona a opção.

   >[!NOTE]
   >
   > Se o valor e a opção de uma opção suspensa forem iguais, a planilha poderá conter somente o **Opção** coluna.

   Vamos adicionar uma nova planilha, [shared-country](/help/forms/assets/enquiry-options.xlsx) para as opções exibidas na guia `Destination` lista suspensa na `enquiry` formulário.

   Consulte a ilustração abaixo, que descreve o `shared-country` planilha:

   ![Lista suspensa para país](/help/forms/assets/drop-down-country-options.png)
3. Pré-visualizar e publicar o `shared-country` planilha usando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

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


