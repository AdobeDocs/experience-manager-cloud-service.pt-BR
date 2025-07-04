---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.1.0.
description: as a Cloud Service Notas de versão do [!DNL Adobe Experience Manager] para 2021.1.0.
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 21%

---


# Notas de versão para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de Versão gerais para [!DNL Experience Manager] as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] as a Cloud Service 2021.1.0 é 3 de fevereiro de 2021.
A versão seguinte (2021.2.0) será lançada em 25 de fevereiro de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP de fragmento de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md)**: adicione a capacidade de adicionar/atualizar e excluir variações de Fragmento de conteúdo usando a API HTTP.

* **[API do GraphQL para Entrega de fragmento de conteúdo](/help/headless/graphql-api/content-fragments.md)**: capacidade de consultar Fragmentos de conteúdo usando sintaxe GraphQL e esquemas com base em modelos de Fragmento de conteúdo para saída no formato JSON.

* **[Suporte de Autenticação para Solicitações da API do GraphQL](/help/headless/security/authentication.md)**: capacidade de autenticar solicitações da API do GraphQL com tokens de acesso para APIs do lado do servidor.

* Saída JSON aprimorada da API do GraphQL, incluindo a capacidade de produzir rich text no formato JSON e localidades.

* Suporte para aninhamento de modelos de fragmento de conteúdo para permitir a criação de estruturas aninhadas de fragmento de conteúdo por meio de tipos de dados dedicados de referência de fragmento de conteúdo ou referências de fragmento de conteúdo embutidas em campos de texto de várias linhas.

* Regras de validação adicionais disponíveis nos tipos de dados do modelo de Fragmento de conteúdo, incluindo &quot;exclusivo&quot;, &quot;obrigatório&quot; e &quot;traduzível&quot;.

* Capacidade de marcar modelos de Fragmento de conteúdo e permitir a criação de Fragmento de conteúdo em uma pasta com políticas por tags ou caminhos.

* Aprimoramentos de usabilidade no editor de Fragmento de conteúdo, incluindo ação de publicação e exibição do modelo no qual um fragmento é baseado.

* Capacidade de visualizar a saída JSON diretamente no editor de Fragmento de conteúdo.


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* O [!DNL Experience Manager] as a [!DNL Cloud Service] estende a funcionalidade de Tags inteligentes para oferecer suporte à identificação de palavras-chave e entidades em ativos baseados em texto. O texto é identificado, indexado e disponibilizado como metadados para melhorar a experiência de pesquisa sem a necessidade de qualquer configuração. Consulte [Tags inteligentes](/help/assets/smart-tags.md).

* O formato de arquivo MXF agora é compatível. Consulte [formatos de arquivo compatíveis](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Gerenciamento da experiência do produto: nova guia de propriedades &quot;Commerce&quot; para Assets e Fragmentos de experiência. Essa guia permite vincular produtos/categorias à Assets e aos Fragmentos de experiência. A guia também mostra dados em tempo real para produtos/categorias vinculados e um link para mostrar detalhes no console do produto.

* Lançamento do site de referência CIF Venia - 2021.02.02 que inclui a versão mais recente dos componentes principais CIF v1.7.0. Consulte [Site de referência de CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02) para obter mais detalhes.

* Lançamento de componentes principais de CIF v1.7.0. Consulte [Componentes principais do CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.1.0 é 14 de janeiro de 2021.

### Correções de erros {#bug-fixes-cloud-manager}

* A instância de Produção de ativos pode, ocasionalmente, mostrar o status do Portal da marca na página de detalhes do **Ambientes** como *Pendente*, sem permitir que o usuário execute uma ação.

* Ao cancelar uma hibernação no Cloud Manager, às vezes, uma mensagem de falha era exibida mesmo quando o processo era iniciado com êxito.

* Foram solucionados casos raros de falha na criação ou exclusão de ambientes.

## Ferramentas de refatoração de código {#code-refactoring-tools}

### Novidades do [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Nova versão do plug-in AIO-CLI lançada. A versão mais recente deste plug-in inclui correções de erros para o AEM Dispatcher Converter e o Repository Modernizer, além de oferecer suporte a um novo utilitário: Conversor de índice. Consulte [Experiência unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=pt-BR#benefits) para saber mais sobre este plug-in.

* O Conversor de índice é um utilitário que pode ser usado para transformar as Definições de índice OAK personalizadas de um cliente em Definições de índice OAK compatíveis com AEM as a Cloud Service. Consulte [Conversor de Índice](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obter mais detalhes.

* Novo recurso adicionado ao [Modernizador de repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que cria um pacote separado `ui.config` para conter todas as configurações OSGi.

### Correções de erros {#crt-bug-fixes}

* Várias correções de bugs feitas nas ferramentas AEM Dispatcher Converter e Repository Modernizer. Consulte [Conversor de Dispatcher do AEM](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Modernizador de repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## AEM as a Cloud Service Foundation {#aem-as-a-cloud-service-foundation}

### Novidades {#what-is-new-foundation}

* Chamadas de API autenticadas de servidor para servidor - gere os tokens de acesso apropriados para fazer chamadas de API autenticadas de servidor para servidor entre os aplicativos externos e os ambientes do AEM as a Cloud Service. Saiba mais lendo [a documentação](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) ou consultando o [tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=pt-BR#authentication).

### Analisadores de build do SDK {#sdk-build-analyzers}

O plug-in para Maven do Analisador de build do SDK do AEM as a Cloud Service detecta problemas em um projeto Maven, incluindo dependências ausentes. Ele oferece aos desenvolvedores uma oportunidade de descobrir problemas durante o desenvolvimento local, bem antes da implantação em ambientes da nuvem com o Cloud Manager.

Dois novos analisadores foram adicionados nesta versão:

* analisador repoinit
* bundle-nativecode

Para obter mais informações, consulte a documentação [aqui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR#developing).

## Ferramentas de transição para a nuvem {#code-transition-tools}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de transferência de conteúdo v1.2.2 é 1º de fevereiro de 2021.

### Novidades do [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Novo recurso e interface adicionados à Ferramenta de transferência de conteúdo - Ferramenta de mapeamento do usuário. Esse recurso mapeia automaticamente usuários e grupos existentes para suas IDs de sistema do Adobe Identity Management como parte da atividade de migração de conteúdo. Consulte [Usar a ferramenta de Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=pt-BR) para obter mais detalhes.
* A Ferramenta de transferência de conteúdo agora migra todos os grupos e usuários referenciados no conjunto de migração, incluindo filhos.
* Os usuários podem selecionar determinados caminhos em `/etc` ao criar conjuntos de migração.
