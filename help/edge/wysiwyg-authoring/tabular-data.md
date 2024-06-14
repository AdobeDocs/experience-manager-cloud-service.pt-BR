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
* [Configurações](/help/edge/docs/setup-byo-cdn-push-invalidation.md) como para configurações de CND

Além disso, você pode [criar planilhas](#own-spreadsheet) de qualquer estrutura para armazenar mapeamentos para fins próprios.

Este documento usa o exemplo de redirecionamentos para ilustrar como criar essas planilhas. Consulte os tópicos vinculados anteriormente na documentação do Edge Delivery Services para obter detalhes sobre cada caso de uso.

>[!TIP]
>
>Para obter mais informações sobre como as planilhas em geral funcionam com os Edge Delivery Services, consulte o documento [Planilhas e JSON.](/help/edge/developer/spreadsheets.md)

>[!TIP]
>
>As planilhas devem ser usadas apenas para manter dados tabulares. Para armazenar dados estruturados, [confira os recursos headless do AEM.](/help/headless/introduction.md)

## Pré-requisitos {#prerequisites}

Para criar mapeamentos usando planilhas no projeto AEM com Edge Delivery Services, é necessário criar o site usando o modelo de site mais recente.

Consulte o documento [Guia de introdução do desenvolvedor para criação WYSIWYG com o Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) para obter mais informações.

## Criação de uma Planilha {#spreadsheet}

Neste exemplo, você criará uma planilha para gerenciar redirecionamentos do AEM com o site Edge Delivery Services. As mesmas etapas se aplicam a [outros tipos de planilhas](#other) que deseja criar.

1. Faça logon na sua instância de criação do AEM as a Cloud Service, acesse o **Sites** e navegue até a raiz do site que requer uma planilha. Toque ou clique **Criar** -> **Página**.

   ![Criar página](assets/tabular-data/tabular-data-create-page.png)

1. No **Modelo** do assistente criar página, toque ou clique na guia **Redirecionamentos** modelo para selecioná-lo e toque ou clique **Próxima**.

   ![Selecionar modelo](assets/tabular-data/tabular-data-create-page-teamplate-redirects.png)

1. A variável **Propriedades** do assistente apresenta os valores padrão para a planilha de redirecionamentos. Toque ou clique em **Criar**.

   * **Título** - Deixe esse valor como está.
   * **Colunas** - As colunas mínimas necessárias para redirecionamentos são pré-preenchidas.
      * **origem** - A página a ser redirecionada
      * **destino** - A página para redirecionar para

   ![Propriedades da planilha](assets/tabular-data/tabular-data-create-page-properties-redirects.png)

1. No **Sucesso** toque ou clique em **Abertura**.

   ![Caixa de diálogo de sucesso](assets/tabular-data/tabular-data-success.png)

1. Uma nova guia é aberta com a planilha carregada em um editor com a tag **origem** e **destino** colunas. Para definir seus redirecionamentos, toque ou clique na linha vazia do **origem** coluna. As alterações são salvas automaticamente à medida que você edita a planilha.

   ![Editar planilha](assets/tabular-data/tabular-data-edit-redirects.png)

   * A variável **origem** é relativo ao domínio do seu site, portanto, contém apenas o caminho relativo.
   * A variável **destino** pode ser um URL totalmente qualificado se você estiver redirecionando para um site diferente ou pode ser um caminho relativo se você estiver redirecionando dentro do seu próprio site.
   * Use a tecla tab para mover o foco para a próxima célula.
   * O editor adiciona novas linhas à planilha conforme necessário.
   * Para excluir ou mover uma linha, use o **Excluir** ícone no final de cada linha e as alças de arrastar no início de cada linha, respectivamente.

## Publicar uma planilha em paths.json {#paths-json}

Para que o AEM possa publicar os dados em sua planilha, você também precisa atualizar o `paths.json` arquivo do seu projeto.

1. Abra a raiz do seu projeto no GitHub.

1. Toque ou clique no `paths.json` para abrir os detalhes e depois o **Editar** ícone.

   ![arquivo paths.json](assets/tabular-data/tabular-data-paths-json.png)

1. Adicione uma linha para mapear sua nova planilha em uma `redirects.json` recurso.

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/redirects:/redirects.json"
     ]
   }
   ```

1. Clique em **Confirmar alterações...** para salvar as alterações em `main`.

   * Confirme em `main` ou criar uma solicitação de pull de acordo com seu processo.

1. Quando terminar de definir os redirecionamentos e atualizar o mapeamento de caminho, retorne ao **Sites** console.

1. Toque ou clique para selecionar a planilha de redirecionamentos criada no console e toque ou clique **Publicação rápida** na barra de ações para publicar a planilha.

   ![Selecione a planilha no console Sites](assets/tabular-data/tabular-data-select-publish.png)

1. No **Publicação rápida** toque ou clique em **Publish**.

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

Basta seguir as mesmas etapas nas seções [Criar planilha](#spreadsheet) e [Atualizar paths.json](#paths-json) e escolha o modelo apropriado e atualize o `paths.json` arquivo adequadamente.

Para [Configuração](https://www.aem.live/docs/configuration), [Cabeçalhos](https://www.aem.live/docs/custom-headers) e [Metadados](https://www.aem.live/docs/bulk-metadata) adicione um mapeamento para publicá-los em seus locais padrão:

* Configuração: `/.helix/config.json`
* Cabeçalhos: `/.helix/headers.json`
* Metadados: `/metadata.json`

Além disso, você pode [criar sua própria planilha](#own-spreadsheet) com colunas arbitrárias para seu próprio uso.

>[!NOTE]
>
>Não é necessário criar uma planilha para gerenciar a indexação para AEM as a Cloud Service com projetos Edge Delivery Services.
>
>Se quiser criar seus próprios índices, [siga esta documentação](https://www.aem.live/developer/indexing#setting-up-more-index-configurations) para criar o seu próprio `helix-query.yaml` arquivo.

## Criar Sua Própria Planilha {#own-spreadsheet}

1. Siga o mesmo procedimento na seção [Criar planilha.](#spreadsheet)

1. Ao selecionar o modelo, escolha **Planilha**.

1. No **Propriedades** do assistente, você pode adicionar suas próprias colunas.

   ![Adicionar suas próprias colunas](assets/tabular-data/tabular-data-own-spreadsheet.png)

   * No **Colunas** toque ou clique em **Adicionar** para adicionar uma nova coluna.
   * Forneça um nome para a coluna.
   * Remova ou reorganize as colunas usando o **Excluir** e arraste os ícones de alça, respectivamente.

1. Crie a planilha e publique de acordo com as instruções para a planilha de redirecionamentos.

1. Adicione um mapeamento à `paths.json` arquivo de acordo com as instruções para a planilha de redirecionamentos.

