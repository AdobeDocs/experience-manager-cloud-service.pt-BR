---
title: Utilização de Planilhas para Gerenciar Dados Tabulares
description: Saiba como usar planilhas para gerenciar dados tabulares para vários valores, como metadados e redirecionamentos para seu AEM com Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 26d4db90-3e4b-4957-bf21-343c76322cdc
role: Admin, Architect, Developer
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 1%

---


# Utilização de Planilhas para Gerenciar Dados Tabulares {#tabular-data}

Saiba como usar planilhas para gerenciar dados tabulares para vários valores, como metadados e redirecionamentos para seu AEM com Edge Delivery Services.

## Casos de uso {#use-cases}

Para qualquer AEM com um site de Edge Delivery Services, é necessário manter listas de dados tabulares, como para mapeamentos de valores-chave. Elas podem ser listas de vários valores diferentes, como metadados e redirecionamentos. O Edge Deliver Services permite manter essas listas tabulares usando uma ferramenta intuitiva: a planilha. O AEM traduz essas planilhas em arquivos JSON que podem ser facilmente consumidos pelo seu site ou aplicativo da Web.

Casos de uso comuns incluem:

* [Espaços reservados](/help/edge/docs/placeholders.md)
* [Metadados](/help/edge/docs/bulk-metadata.md)
* [Cabeçalhos](/help/edge/docs/custom-headers.md)
* [Redirecionamentos](/help/edge/docs/redirects.md)
* [Configurações](/help/edge/docs/setup-byo-cdn-push-invalidation.md), como para configurações CND

Além disso, você pode [criar planilhas](#own-spreadsheet) de qualquer estrutura para armazenar mapeamentos para fins próprios.

Este documento usa o exemplo de redirecionamentos para ilustrar como criar essas planilhas. Consulte os tópicos vinculados anteriormente na documentação do Edge Delivery Services para obter detalhes sobre cada caso de uso.

>[!TIP]
>
>Para obter mais informações sobre como as planilhas em geral funcionam com Edge Delivery Services, consulte o documento [Planilhas e JSON.](/help/edge/developer/spreadsheets.md)

>[!TIP]
>
>As planilhas devem ser usadas apenas para manter dados tabulares. Para armazenar dados estruturados, [confira os recursos headless do AEM.](/help/headless/introduction.md)

## Pré-requisitos {#prerequisites}

Para criar mapeamentos usando planilhas no projeto AEM com Edge Delivery Services, é necessário criar o site usando o modelo de site mais recente.

Consulte o documento [Guia de Introdução do Desenvolvedor para criação WYSIWYG com o Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) para obter mais informações.

## Criação de uma Planilha {#spreadsheet}

Neste exemplo, você criará uma planilha para gerenciar redirecionamentos do AEM com o site Edge Delivery Services. As mesmas etapas se aplicam a [outros tipos de planilha](#other) que você deseja criar.

1. Entre na sua instância de criação do AEM as a Cloud Service, vá para o console **Sites** e navegue até a raiz do site, que requer uma planilha. Toque ou clique em **Criar** -> **Página**.

   ![Criar página](assets/tabular-data/tabular-data-create-page.png)

1. Na guia **Modelo** do assistente de criação de página, toque ou clique no modelo **Redirecionamentos** para selecioná-lo e toque ou clique em **Avançar**.

   ![Selecionar modelo](assets/tabular-data/tabular-data-create-page-teamplate-redirects.png)

1. A guia **Propriedades** do assistente apresenta os valores padrão para a planilha de redirecionamentos. Toque ou clique em **Criar**.

   * **Título** - Deixar este valor como está.
   * **Colunas** - As colunas mínimas necessárias para redirecionamentos são preenchidas previamente.
      * **origem** - A página a ser redirecionada
      * **destino** - A página para redirecionar

   ![Propriedades da planilha](assets/tabular-data/tabular-data-create-page-properties-redirects.png)

1. Na caixa de diálogo **Êxito**, toque ou clique em **Abrir**.

   ![Caixa de diálogo de sucesso](assets/tabular-data/tabular-data-success.png)

1. Uma nova guia é aberta com a planilha carregada em um editor com as colunas **origem** e **destino** predefinidas. Para definir seus redirecionamentos, toque ou clique na linha vazia da coluna **origem**. As alterações são salvas automaticamente à medida que você edita a planilha.

   ![Editar planilha](assets/tabular-data/tabular-data-edit-redirects.png)

   * A **origem** é relativa ao domínio do seu site, portanto, contém apenas o caminho relativo.
   * O **destino** pode ser uma URL totalmente qualificada se você estiver redirecionando para um site diferente ou um caminho relativo se você estiver redirecionando dentro do seu próprio site.
   * Use a tecla tab para mover o foco para a próxima célula.
   * O editor adiciona novas linhas à planilha conforme necessário.
   * Para excluir ou mover uma linha, use o ícone **Excluir** no final de cada linha e as alças de arrastar no início de cada linha, respectivamente.

## Publicar uma planilha em paths.json {#paths-json}

Para que o AEM possa publicar os dados em sua planilha, você também precisa atualizar o arquivo `paths.json` do seu projeto.

1. Abra a raiz do seu projeto no GitHub.

1. Toque ou clique no arquivo `paths.json` para abrir seus detalhes e, em seguida, no ícone **Editar**.

   ![arquivo paths.json](assets/tabular-data/tabular-data-paths-json.png)

1. Adicione uma linha para mapear sua nova planilha para um recurso `redirects.json`.

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/redirects:/redirects.json"
     ]
   }
   ```

1. Clique em **Confirmar alterações...** para salvar as alterações em `main`.

   * Confirme com `main` ou crie uma solicitação pull de acordo com seu processo.

1. Quando terminar de definir os redirecionamentos e atualizar o mapeamento de caminho, retorne ao console **Sites**.

1. Toque ou clique para selecionar a planilha de redirecionamentos criada no console e toque ou clique em **Publish Rápido** na barra de ações para publicar a planilha.

   ![Selecione a planilha no console Sites](assets/tabular-data/tabular-data-select-publish.png)

1. Na caixa de diálogo **Publish Rápido**, toque ou clique em **Publish**.

   ![Confirmar publicação](assets/tabular-data/tabular-data-quick-publish.png)

1. Um banner confirma a publicação.

   ![Confirmação de banner da publicação](assets/tabular-data/tabular-data-publish-banner.png)

A planilha de redirecionamentos agora está publicada e acessível ao público.

## Outros Tipos de Planilha {#other}

Agora que você sabe como criar uma planilha de redirecionamentos, é possível criar qualquer outro tipo de planilha padrão:

* Espaços reservados
* Metadados
* Cabeçalhos
* Configuração

Basta seguir as mesmas etapas nas seções [Criar planilha](#spreadsheet) e [Atualizar caminhos.json](#paths-json) e escolher o modelo apropriado e atualizar o arquivo `paths.json` apropriadamente.

Para [Configuração](https://www.aem.live/docs/configuration), [Cabeçalhos](https://www.aem.live/docs/custom-headers) e [Metadados](https://www.aem.live/docs/bulk-metadata) adicione um mapeamento para publicá-los em seus locais padrão:

* Configuração: `/.helix/config.json`
* Cabeçalhos: `/.helix/headers.json`
* Metadados: `/metadata.json`

Além disso, você pode [criar sua própria planilha](#own-spreadsheet) com colunas arbitrárias para uso próprio.

>[!NOTE]
>
>Não é necessário criar uma planilha para gerenciar a indexação do AEM as a Cloud Service com projetos Edge Delivery Services.
>
>Se quiser criar seus próprios índices, [siga esta documentação](https://www.aem.live/developer/indexing#setting-up-more-index-configurations) para criar seu próprio arquivo `helix-query.yaml`.

## Criar Sua Própria Planilha {#own-spreadsheet}

1. Siga as mesmas etapas na seção [Criar Planilha.](#spreadsheet)

1. Ao selecionar o modelo, escolha **Planilha**.

1. Na guia **Propriedades** do assistente, você pode adicionar suas próprias colunas.

   ![Adicionar suas próprias colunas](assets/tabular-data/tabular-data-own-spreadsheet.png)

   * Na seção **Colunas**, toque ou clique em **Adicionar** para adicionar uma nova coluna.
   * Forneça um nome para a coluna.
   * Remova ou reorganize as colunas usando os ícones **Excluir** e arrastar alça, respectivamente.

1. Crie a planilha e publique de acordo com as instruções para a planilha de redirecionamentos.

1. Adicione um mapeamento ao arquivo `paths.json` de acordo com as instruções da planilha de redirecionamentos.

