---
title: Carregar opções de lista suspensa de um URL ou outra planilha do Edge Delivery Services para o AEM Forms as a Cloud Service
description: As opções da lista suspensa são incluídas em uma planilha distinta e, em seguida, importadas para a planilha principal por meio do URL fornecido.
feature: Edge Delivery Services
exl-id: 5b0bc1b6-6e33-41f3-b7c1-4d997787b6cd
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# Opções de um URL ou outra planilha do Edge Delivery Services para o AEM Forms as a Cloud Service

O Forms geralmente inclui menus suspensos para que os usuários selecionem entre as opções predefinidas. Normalmente, essas opções são definidas no próprio formulário, mas o gerenciamento de listas longas pode ser complicado. Este guia descreve como melhorar a criação de formulários carregando opções suspensas de uma planilha separada por meio de um URL.


Os benefícios de carregar opções suspensas em uma planilha separada são:

- Gerenciamento simplificado: mantenha as opções suspensas em um local centralizado para facilitar atualizações e adições.
- Maior eficiência: elimine a necessidade de adicionar manualmente longas listas de opções na definição do formulário.

![Opções suspensas](/help/forms/assets/drop-down-options.png)


No final deste artigo, você aprenderá a:

- [Definir opções em uma planilha separada](#define-options)
- [Adicionar URL para carregar opções da lista suspensa](#add-url)

## Definir opções em uma planilha separada {#define-options}

Definição de Opções em uma Planilha Separada

1. Criar uma planilha:
   1. Localize a pasta do projeto AEM no Microsoft® SharePoint ou Google Drive.
   1. Adicione uma nova planilha. Por exemplo, &quot;país compartilhado&quot;.
1. Definir Colunas de Opção:
Adicione duas colunas: &quot;Option&quot; e &quot;Value&quot;.
   - &quot;Option&quot; define o texto exibido no menu suspenso.
   - &quot;Value&quot; define o valor enviado quando um usuário seleciona a opção.

   >[!NOTE]
   >
   >Se a opção e o valor forem idênticos, somente a coluna &quot;Option&quot; será necessária.

1. Preencha a planilha:
Insira suas opções de país na coluna &quot;Option&quot; (e na coluna &quot;Value&quot;, se necessário).

   Consulte o exemplo abaixo para obter uma estrutura.

   ![Lista suspensa do país](/help/forms/assets/drop-down-country-options.png)

1. Visualize e publique a planilha `shared-country` usando o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   Por exemplo, se o repositório do seu projeto for chamado de &quot;wefinance&quot;, ele estará localizado sob o proprietário da conta &quot;wkndform&quot; e você estiver usando a ramificação &quot;main&quot;, a URL que mostra a planilha `shared-country`:
   `https://main--wefinance--wkndform.aem.live/enquiry.json?sheet=country`
   <!--(https://main--wefinance--wkndform.aem.live/enquiry.json?sheet=country)  -->

>[!NOTE]
>
> `?sheet=country` é um parâmetro de consulta anexado à URL. Este parâmetro indica o JSON filtrado com base na planilha `shared-country`. Ele redireciona para o arquivo JSON contendo informações relacionadas a diferentes países.

## Adicionar URL para carregar opções da lista suspensa{#add-url}

A propriedade `Options` de um campo `select` aceita uma URL. A URL retorna uma matriz JSON usada como opções para a lista suspensa `Destination`. Para adicionar as opções da lista suspensa URL to load:

1. Vá para a pasta do Projeto AEM no Microsoft® SharePoint ou Google Drive e abra a planilha. Você também pode criar uma nova planilha para um formulário.
1. Copie a URL da folha `shared-country` e cole-a na coluna `Options` do campo `Destination`.

   ![Planilha de consulta](/help/forms/assets/drop-down-enquiry.png)

1. Visualize e publique a planilha usando o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).


   ![Lista suspensa do país](/help/forms/assets/load-dropdown-options-form.png)

Você pode consultar a [planilha de consulta](/help/edge/assets/enquiry.xlsx) para adicionar a URL para carregar opções de listas suspensas.

Depois de integrar a URL à definição de formulário para carregar as opções da lista suspensa, as opções para a lista suspensa `Destination` começam a aparecer na URL.

Por exemplo, se o repositório do seu projeto for chamado &quot;wefinance&quot;, estiver localizado sob o proprietário da conta &quot;wkndform&quot; e você estiver usando a ramificação &quot;main&quot;, a URL abaixo exibirá o formulário `enquiry` exibindo as opções salvas na planilha separada:

`https://main--wefinance--wkndform.aem.live/enquiry-form`



