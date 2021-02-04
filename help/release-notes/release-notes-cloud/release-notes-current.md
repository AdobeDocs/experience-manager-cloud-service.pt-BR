---
title: Notas de versão atuais para [!DNL Adobe Experience Manager] como um Cloud Service.
description: Notas de versão atuais para [!DNL Adobe Experience Manager] como um Cloud Service.
translation-type: tm+mt
source-git-commit: 5901bdd97c8c94f6baf04eab8da1d7fc3f3f89da
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 5%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] como um Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] como Cloud Service 2021.1.0 é 3 de fevereiro de 2021.
A seguinte versão (2021.2.0) será lançada em 25 de fevereiro de 2021.

## [!DNL Adobe Experience Manager Sites] como um Cloud Service  {#sites}

### Gerenciamento de conteúdo sem periféricos {#headless}

* **[API GraphQL para o Delivery](/help/assets/content-fragments/graphql-api-content-fragments.md)** de fragmento do conteúdo: Capacidade de query de Fragmentos de Conteúdo usando a sintaxe GraphQL e schemas com base em modelos de Fragmento de Conteúdo, para saída no formato JSON.

* **[Suporte de autenticação para solicitações](/help/assets/content-fragments/graphql-authentication-content-fragments.md)** da API GraphQL: Capacidade de autenticar solicitações de API GraphQL com tokens de acesso para APIs do lado do servidor.

* [O ](/help/implementing/developing/hybrid/remote-page.md) componente RemotePage oferece suporte para exibição e edição de SPA externos em AEM usando.

* Saída JSON aprimorada da API GraphQL, incluindo a capacidade de produzir rich text no formato JSON e localidades.

* Suporte para aninhamento de modelos de Fragmento de conteúdo para permitir a criação de estruturas aninhadas de Fragmento de conteúdo, por meio de tipos de dados dedicados de Referência de fragmento de conteúdo ou referências de fragmento de conteúdo embutidas em campos de texto de várias linhas.

* Regras de validação adicionais disponíveis nos tipos de dados do modelo de Fragmento de conteúdo, incluindo &quot;exclusivo&quot;, &quot;obrigatório&quot; e &quot;traduzível&quot;.

* Capacidade de marcar modelos de Fragmento de conteúdo e permitir a criação de Fragmento de conteúdo em uma pasta com políticas por tags ou caminhos.

* Aprimoramentos de usabilidade no editor de Fragmento de conteúdo, incluindo ação de publicação e exibição do modelo no qual um fragmento é baseado.

* Capacidade de pré-visualização da saída JSON diretamente no editor de fragmento de conteúdo.

### Aplicativos Web progressivos (PWA) {#pwa}

* [Uma versão de aplicativo da Web progressivo (PWA) de um ](/help/sites-cloud/authoring/features/enable-pwa.md)  sitecan agora pode ser ativada no nível do projeto por meio de uma configuração simples.

## [!DNL Adobe Experience Manager Assets] como uma  [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] como um recurso,  [!DNL Cloud Service] amplia a funcionalidade Tags inteligentes para suportar a identificação de palavras-chave e entidades em ativos baseados em texto. O texto é identificado, indexado e disponibilizado como metadados para melhorar a experiência de pesquisa sem a necessidade de qualquer configuração. Consulte [Tags inteligentes](/help/assets/smart-tags.md).

* O formato de arquivo MXF agora é compatível. Consulte [formatos de arquivo suportados](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Gerenciamento da experiência do produto: Nova guia de propriedades &#39;Comércio&#39; para Ativos e Fragmentos de experiência. Esta guia permite que você vincule produtos / categorias a ativos e fragmentos de experiência. A guia também mostra dados em tempo real para produtos/categorias vinculados e um link para mostrar detalhes no console do produto.

* Lançamento do site de referência CIF Venia - 2021.02.02 que inclui a versão mais recente dos componentes principais CIF v1.7.0. Consulte [CIF Site de Referência de Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02) para obter mais detalhes.

* Componentes principais CIF lançados v1.7.0. Consulte [CIF Componentes principais](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2021.1.0 é 14 de janeiro de 2021.

### Correções de erros {#bug-fixes-cloud-manager}

* A instância Produção de ativos pode, ocasionalmente, mostrar o status do Portal de marcas na página de detalhes **Ambientes** como *Pendente* sem permitir que o usuário execute nenhuma ação.

* Ao disparar uma hibernação do Gerenciador de nuvem, às vezes uma mensagem de falha era exibida mesmo quando a hibernação era iniciada com êxito.

* Casos raros de falha encontrados na criação ou exclusão de ambientes foram abordados.

## AEM como um Cloud Service Foundation {#aem-as-a-cloud-service-foundation}

### Novidades {#what-is-new-foundation}

* Chamadas de API autenticadas de servidor para servidor - Gere os tokens de acesso apropriados para fazer chamadas de API autenticadas de servidor para servidor entre seus aplicativos externos e AEM como ambientes Cloud Service. Saiba mais lendo [a documentação](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) ou consultando o [tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

### Analisadores de compilação do SDK {#sdk-build-analyzers}

O AEM como um plug-in Maven do Cloud Service SDK Build Analyzer detecta problemas em um projeto maven, incluindo dependências ausentes. Ele oferece aos desenvolvedores uma oportunidade de descobrir problemas durante o desenvolvimento local, bem antes de implantar ambientes da Cloud com o Cloud Manager.

Dois novos analisadores foram adicionados para esta versão:

* analisador de repontas
* bundle-nativecode

Para obter mais informações, consulte a documentação [here](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing).

## Ferramentas de transição para a nuvem {#code-transition-tools}

### Data de lançamento {#release-date-ctt}

A data de lançamento da Content Transfer Tool v1.2.2 é 1 de fevereiro de 2021.

### Novidades em [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Novo recurso e interface adicionada à Ferramenta de transferência de conteúdo - Ferramenta de mapeamento do usuário. Esse recurso mapeia automaticamente usuários e grupos existentes para suas IDs de sistema Adobe Identity Management como parte da atividade de migração de conteúdo. Consulte [Usando a ferramenta de mapeamento do usuário](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obter mais detalhes.
* A Ferramenta de transferência de conteúdo agora migra todos os grupos e usuários referenciados no conjunto de migração, incluindo filhos.
* Os usuários podem selecionar determinados caminhos em `/etc` ao criar conjuntos de migração.
