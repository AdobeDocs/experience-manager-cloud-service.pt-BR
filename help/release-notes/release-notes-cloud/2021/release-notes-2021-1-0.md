---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2021.1.0.
description: '[!DNL Adobe Experience Manager] Notas de versão as a Cloud Service para 2021.1.0.'
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
source-git-commit: 44b24a68e2b9a9abd2a9d609c3a28f6b90e492fa
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 7%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento para [!DNL Adobe Experience Manager] O as a Cloud Service 2021.1.0 é 3 de fevereiro de 2021.
A seguinte versão (2021.2.0) será lançada em 25 de fevereiro de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP do fragmento de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md)**: Adicione a capacidade de adicionar/atualizar e excluir variações do Fragmento de conteúdo usando a API HTTP.

* **[API GraphQL para entrega de fragmento de conteúdo](/help/headless/graphql-api/content-fragments.md)**: Capacidade de consultar Fragmentos de conteúdo usando a sintaxe GraphQL e esquemas com base em modelos de Fragmento de conteúdo, para saída no formato JSON.

* **[Suporte de autenticação para solicitações de API GraphQL](/help/headless/security/authentication.md)**: Capacidade de autenticar solicitações de API GraphQL com tokens de acesso para APIs do lado do servidor.

* Saída JSON aprimorada da API GraphQL, incluindo a capacidade de produzir rich text no formato JSON e localidades.

* Suporte para aninhar modelos de Fragmento de conteúdo para permitir a criação de estruturas de Fragmento de conteúdo aninhadas, por meio de tipos de dados dedicados de Referência de fragmento de conteúdo ou referências de Fragmento de conteúdo embutidas em campos de texto de várias linhas.

* Regras de validação adicionais disponíveis nos tipos de dados do modelo de Fragmento de conteúdo , incluindo &quot;exclusivo&quot;, &quot;obrigatório&quot; e &quot;traduzível&quot;.

* Capacidade de marcar modelos de Fragmento de conteúdo e permitir a criação de Fragmento de conteúdo em uma pasta com políticas por tags ou caminhos.

* Aprimoramentos de usabilidade no editor de Fragmento de conteúdo, incluindo a ação de publicação e a exibição do modelo no qual um fragmento é baseado.

* Capacidade de visualizar a saída JSON diretamente no editor de Fragmento de conteúdo.


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] como [!DNL Cloud Service] estende a funcionalidade Tags inteligentes para suportar a identificação de palavras-chave e entidades em ativos baseados em texto. O texto é identificado, indexado e disponibilizado como metadados para melhorar a experiência de pesquisa sem a necessidade de qualquer configuração. Consulte [Tags inteligentes](/help/assets/smart-tags.md).

* O formato de arquivo MXF agora é compatível. Consulte [formatos de arquivo compatíveis](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Gerenciamento de experiência do produto: Nova guia de propriedades &quot;Comércio&quot; para Ativos e Fragmentos de experiência. Essa guia permite vincular produtos/categorias a Ativos e Fragmentos de experiência. A guia também mostra dados em tempo real para produtos/categorias vinculados e um link para mostrar detalhes no console do produto.

* Lançamento do site de referência CIF Venia - 2021.02.02, que inclui a versão mais recente dos Componentes principais CIF v1.7.0. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02) para obter mais detalhes.

* Lançamento de componentes principais CIF v1.7.0. Consulte [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.1.0 é 14 de janeiro de 2021.

### Correções de erros {#bug-fixes-cloud-manager}

* A instância Produção de ativos pode, ocasionalmente, mostrar o status do Brand Portal no **Ambientes** página de detalhes como *Pending* sem permitir que o usuário execute qualquer ação.

* Ao acionar uma deshibernação no Cloud Manager, às vezes uma mensagem de falha era exibida mesmo quando a desibernação era iniciada com êxito.

* Foram solucionados casos raros de falha encontrados na criação ou exclusão de ambientes.

## Ferramentas de refatoração de código {#code-refactoring-tools}

### Novidades do [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Nova versão do plug-in AIO-CLI lançada. A versão mais recente deste plug-in inclui correções de erros para o Conversor do Dispatcher AEM e o Repository Modernizer, além de oferecer suporte a um novo utilitário - Conversor de índice. Consulte [Experiência unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para saber mais sobre este plug-in.

* O Conversor de Índice é um utilitário que pode ser usado para transformar as Definições de Índice OAK Personalizado de um cliente em Definições de Índice OAK as a Cloud Service e compatíveis. Consulte [Conversor de índice](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obter mais detalhes.

* Novo recurso adicionado a [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que cria um pacote separado `ui.config` para conter todas as configurações do OSGi.

### Correções de erros {#crt-bug-fixes}

* Várias correções de erros feitas nas ferramentas AEM Dispatcher Converter e Repository Modernizer. Consulte [Conversor do Dispatcher do AEM](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## AEM fundação as a Cloud Service {#aem-as-a-cloud-service-foundation}

### Novidades {#what-is-new-foundation}

* Chamadas de API autenticadas de servidor para servidor - Gere os tokens de acesso apropriados para fazer chamadas de API autenticadas de servidor para servidor entre seus aplicativos externos e AEM ambientes as a Cloud Service. Saiba mais ao ler [a documentação](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) ou consultando [tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

### Analisadores de build do SDK {#sdk-build-analyzers}

O AEM plug-in Maven do Analisador de build do SDK as a Cloud Service detecta problemas em um projeto maven, incluindo dependências ausentes. Ela oferece aos desenvolvedores uma oportunidade de descobrir problemas durante o desenvolvimento local, bem antes de implantar em ambientes do Cloud com o Cloud Manager.

Dois novos analisadores foram adicionados para esta versão:

* analisador de repontas
* bundle-nativecode

Para obter mais informações, consulte a documentação [here](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR#developing).

## Ferramentas de transição para a nuvem {#code-transition-tools}

### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta Transferência de conteúdo v1.2.2 é 1 de fevereiro de 2021.

### Novidades do [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Novo recurso e interface do usuário adicionados à ferramenta Transferência de conteúdo - Ferramenta de mapeamento de usuário. Esse recurso mapeia automaticamente usuários e grupos existentes para suas IDs de sistema do Adobe Identity Management como parte da atividade de migração de conteúdo. Consulte [Usar a ferramenta Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obter mais detalhes.
* A ferramenta Transferência de conteúdo agora migra todos os grupos e usuários referenciados no conjunto de migração, incluindo filhos.
* Os usuários podem selecionar determinados caminhos em `/etc` ao criar conjuntos de migração.
