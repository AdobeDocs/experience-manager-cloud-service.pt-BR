---
title: Notas de versão atuais para [!DNL Adobe Experience Manager] como um Cloud Service.
description: Notas de versão atuais para [!DNL Adobe Experience Manager] como um Cloud Service.
translation-type: tm+mt
source-git-commit: 968775b24441457143f497c2cfb1f9ece392d475
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 4%

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

* **[O componente](/help/implementing/developing/hybrid/remote-page.md)** RemotePage: Adição de suporte para exibição e edição de SPA externos em AEM usando.

* **[Edição de um SPA externo em AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: Foi adicionada a capacidade de carregar um aplicativo independente de página única em uma instância AEM, adicionar seções editáveis de conteúdo e ativar a criação.

* Saída JSON aprimorada da API GraphQL, incluindo a capacidade de produzir rich text no formato JSON e localidades.

* Suporte para aninhamento de modelos de Fragmento de conteúdo para permitir a criação de estruturas aninhadas de Fragmento de conteúdo, por meio de tipos de dados dedicados de Referência de fragmento de conteúdo ou referências de fragmento de conteúdo embutidas em campos de texto de várias linhas.

* Regras de validação adicionais disponíveis nos tipos de dados do modelo de Fragmento de conteúdo, incluindo &quot;exclusivo&quot;, &quot;obrigatório&quot; e &quot;traduzível&quot;.

* Capacidade de marcar modelos de Fragmento de conteúdo e permitir a criação de Fragmento de conteúdo em uma pasta com políticas por tags ou caminhos.

* Aprimoramentos de usabilidade no editor de Fragmento de conteúdo, incluindo ação de publicação e exibição do modelo no qual um fragmento é baseado.

* Capacidade de pré-visualização da saída JSON diretamente no editor de fragmento de conteúdo.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

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

A data de lançamento do Cloud Manager no AEM como Cloud Service 2021.2.0 é 11 de fevereiro de 2021.

### Novidades {#what-is-new-cloud-manager}

* O pipeline de produção do Cloud Manager agora inclui o recurso de teste de interface personalizada.

* Os clientes do Assets agora poderão escolher quando e onde implantar sua instância do Brand Portal de forma automática por meio da interface do usuário do Cloud Manager. Para um programa regular (não caixa de proteção) com a solução Assets, o Portal de marcas agora pode ser provisionado no ambiente Production. O provisionamento pode ser feito somente uma vez no Production ambiente.

* O AEM Project Archetype usado em Projeto e criação de caixa de proteção foi atualizado para a versão 25.

* A lista de APIs obsoletas identificadas durante a digitalização de código foi refinada para incluir classes e métodos adicionais obsoletos nas versões mais recentes do Cloud Service SDK.

* O perfil SonarQube para o Gerenciador de nuvem foi atualizado para remover o Lula de regra Sonar:S2142. Isso não entrará em conflito com as verificações de Interrupção de Thread.

* A interface do usuário do Gerenciador de nuvem informará o usuário que pode não ser capaz de adicionar/atualizar temporariamente o nome do domínio porque o ambiente associado tem um pipeline em execução conectado a ele ou que está aguardando a etapa de aprovação.

* As propriedades definidas nos arquivos `pom.xml` do cliente prefixados com o sonar agora serão removidas dinamicamente para evitar falhas de compilação e verificação de qualidade.

* A interface do usuário do Gerenciador de nuvem informará o usuário que não pode selecionar temporariamente um certificado SSL se ele estiver sendo usado por um nome de Domínio que está sendo implantado no momento.

* Regras adicionais de qualidade de código foram adicionadas para cobrir problemas de compatibilidade de Cloud Service.

### Correções de erros {#bug-fixes-cloud-manager}

* A correspondência do certificado SSL com um nome de domínio não faz mais distinção entre maiúsculas e minúsculas.

* A interface do usuário do Cloud Manager agora informará um usuário se as chaves privadas do certificado não atenderem ao limite de 2048 bits com uma mensagem de erro apropriada.

* A interface do usuário do Gerenciador de nuvem informará o usuário que não pode selecionar temporariamente um certificado SSL se ele estiver sendo usado por um nome de Domínio que está sendo implantado no momento.

* Em alguns casos, um problema interno pode fazer com que a exclusão de ambientes fique travada.

* Algumas falhas de pipeline foram relatadas incorretamente como erros de pipeline.

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
