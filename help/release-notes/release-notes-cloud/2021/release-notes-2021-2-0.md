---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.2.0.
description: "[!DNL Adobe Experience Manager] Notas de versão as a Cloud Service para 2021.2.0."
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 8%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento para [!DNL Adobe Experience Manager] O as a Cloud Service 2021.2.0 é 25 de fevereiro de 2021.
A seguinte versão (2021.3.0) será lançada em 25 de março de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Gerenciamento de conteúdo sem periféricos {#headless}

* **[API GraphQL para entrega de fragmento de conteúdo](/help/headless/graphql-api/content-fragments.md)**: Capacidade de consultar Fragmentos de conteúdo usando a sintaxe GraphQL e esquemas com base em modelos de Fragmento de conteúdo, para saída no formato JSON.

* **[Suporte de autenticação para solicitações de API GraphQL](/help/headless/security/authentication.md)**: Capacidade de autenticar solicitações de API GraphQL com tokens de acesso para APIs do lado do servidor.

* **[O componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)**: Adição de suporte para visualizar e editar SPA externos no AEM usando o .

* **[Edição de um SPA externo no AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: Adição da capacidade de carregar um aplicativo de página única independente em uma instância do AEM, adicionar seções editáveis de conteúdo e ativar a criação.

* Saída JSON aprimorada da API GraphQL, incluindo a capacidade de produzir rich text no formato JSON e localidades.

* Suporte para aninhar modelos de Fragmento de conteúdo para permitir a criação de estruturas de Fragmento de conteúdo aninhadas, por meio de tipos de dados dedicados de Referência de fragmento de conteúdo ou referências de Fragmento de conteúdo embutidas em campos de texto de várias linhas.

* Regras de validação adicionais disponíveis nos tipos de dados do modelo de Fragmento de conteúdo , incluindo &quot;exclusivo&quot;, &quot;obrigatório&quot; e &quot;traduzível&quot;.

* Capacidade de marcar modelos de Fragmento de conteúdo e permitir a criação de Fragmento de conteúdo em uma pasta com políticas por tags ou caminhos.

* Aprimoramentos de usabilidade no editor de Fragmento de conteúdo, incluindo a ação de publicação e a exibição do modelo no qual um fragmento é baseado.

* Capacidade de visualizar a saída JSON diretamente no editor de Fragmento de conteúdo.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## Novidades do [!DNL Assets] {#what-is-new-assets}

* Os ativos podem ser obtidos usando [!DNL Experience Manager Assets Brand Portal]. Ajuda a obter ativos dos usuários da agência para novas campanhas de marketing, fotografias e projetos.

* [!DNL Experience Manager Assets] como [!DNL Cloud Service] tem direito a uma pré-configuração [!DNL Brand Portal] instância. O [!DNL Cloud Manager] o usuário pode ativar [!DNL Brand Portal] on [!DNL Experience Manager Assets] como [!DNL Cloud Service]. Consulte [ativar o Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=pt-BR).

* Agora, as empresas podem adquirir ativos usando [!DNL Brand Portal]. Recursos de fornecimento de ativos aproveitam [!DNL Brand Portal] para ajudar os clientes a se envolverem com usuários de agências para obter ativos para novas campanhas de marketing, fotografias e projetos. Consulte [origem de ativos em [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=pt-BR).

* O [!DNL Brand Portal] relatório de uso agora exibe somente os usuários ativos. Os usuários inativos não são exibidos agora. Os usuários ativos são aqueles cuja conta está atribuída a um perfil de produto no [!DNL Admin Console]. Consulte [[!DNL Brand Portal] relatórios](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* Em [!DNL Brand Portal], uma nova configuração de download é introduzida, permitindo criar uma pasta separada para cada ativo ao baixar pastas, coleção e assim por diante. Consulte [configurações de download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

## Correções de erros no [!DNL Assets] {#bug-fixes-assets}

* Quando vários ativos são selecionados para atualizar as propriedades, às vezes ocorre um erro ou as propriedades de um ativo desmarcado são atualizadas. (CQ-4316532)
* Ao tentar abrir [!UICONTROL Painel de pesquisa do administrador de ativos], a página permanece em branco e ao clicar em [!UICONTROL Editar] > [!UICONTROL Configurações] gera um erro. (CQ-4315079)
* Quando uma nova versão de um ativo existente é criada após resolver o conflito de nomes, os metadados do ativo original são substituídos. (CQ-4313594)
* Quando um ativo com texto de anotação longo é impresso, o texto da anotação é cortado, mesmo se espaço estiver disponível. (CQ-4314101)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Gerenciamento de experiência do produto: Enriqueça as páginas do catálogo de produtos individualmente com Fragmentos de experiência.

* Propriedades do console do produto estendido para mostrar Ativos vinculados e Fragmentos de experiência, incluindo ações para navegar rapidamente para o conteúdo associado.

* Lançamento do site de referência CIF Venia - 2021.02.24, que inclui a versão mais recente dos Componentes principais CIF v1.8.0. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) para obter mais detalhes.

* Lançamento de componentes principais CIF v1.8.0. Consulte [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.2.0 é 11 de fevereiro de 2021.

### Novidades {#what-is-new-cloud-manager}


* Os clientes do Assets agora poderão escolher quando e onde implantar sua instância do Brand Portal de forma automatizada por meio da interface do usuário do Cloud Manager. Para um programa regular (não sandbox) com a solução Assets, a Brand Portal agora pode ser provisionada no ambiente de produção. O provisionamento pode ser feito apenas uma vez no ambiente de Produção.

* O Arquétipo de projeto AEM usado na Criação de projeto e sandbox foi atualizado para a versão 25.

* A lista de APIs obsoletas identificadas durante a verificação de código foi refinada para incluir classes e métodos adicionais obsoletos nas versões mais recentes do SDK do Cloud Service.

* O perfil do SonarQube para o Cloud Manager foi atualizado para remover a regra do Sonar squid:S2142. Isso não entrará mais em conflito com as verificações de Interrupção de encadeamento.

* A interface do usuário do Cloud Manager informará o usuário que pode não ser temporariamente capaz de adicionar/atualizar o nome de domínio porque o ambiente associado tem um pipeline em execução anexado a ele ou que está aguardando a etapa de aprovação.

* Propriedades definidas no cliente `pom.xml` Os arquivos com o prefixo sonar agora serão removidos dinamicamente para evitar falhas de build e de verificação de qualidade.

* A interface do usuário do Cloud Manager informará o usuário que pode não ser temporariamente capaz de selecionar um certificado SSL se ele estiver sendo usado por um nome de domínio que está sendo implantado no momento.

* Foram adicionadas Regras de qualidade de código adicionais para cobrir problemas de compatibilidade de Cloud Service.

### Correções de erros {#bug-fixes-cloud-manager}

* A correspondência do certificado SSL com um nome de domínio não diferencia maiúsculas de minúsculas.

* A interface do usuário do Cloud Manager agora informará um usuário se as chaves privadas do certificado não atenderem ao limite de 2048 bits com uma mensagem de erro apropriada.

* A interface do usuário do Cloud Manager informará o usuário que pode não ser temporariamente capaz de selecionar um certificado SSL se ele estiver sendo usado por um nome de domínio que está sendo implantado no momento.

* Em alguns casos, um problema interno pode causar a interrupção da exclusão do ambiente.

* Algumas falhas de pipeline eram relatadas incorretamente como erros de pipeline.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt}

A data de lançamento da Ferramenta de transferência de conteúdo v1.2.4 é 10 de fevereiro de 2021.

### Correções de erros {#bug-fixes-ctt}

* Ao mapear vários usuários, as IDs IMS de alguns estavam sendo mapeadas incorretamente. Isso foi corrigido.

### Data de lançamento {#release-date-ctt-feb}

A data de lançamento da Ferramenta de transferência de conteúdo v1.2.2 é 01 de fevereiro de 2021.

### Novidades da ferramenta Transferência de conteúdo {#what-is-new-ctt}

* Novo recurso e interface do usuário adicionados à ferramenta Transferência de conteúdo - Ferramenta de mapeamento de usuário. Esse recurso mapeia automaticamente usuários e grupos existentes para suas IDs de sistema do Adobe Identity Management como parte da atividade de migração de conteúdo.
Consulte [Usar a ferramenta Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obter mais detalhes.
* A ferramenta Transferência de conteúdo agora migra todos os grupos e usuários referenciados no conjunto de migração, incluindo filhos.
* Os usuários podem selecionar determinados caminhos em `/etc` ao criar conjuntos de migração.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.2 é 18 de fevereiro de 2021.

### Novidades do Analisador de práticas recomendadas {#what-is-new-bpa}

* Capacidade de detectar o uso da implementação do AEM Forms e do AEM Forms e indicar áreas relevantes para a migração para o AEM Forms as a Cloud Service.
* Capacidade de detectar e relatar o uso e a contagem de componentes e modelos personalizados.
* Capacidade de detectar o tipo de armazenamento de nó e armazenamento de dados usado.
* Capacidade de detectar o uso do Dynamic Media.
* Capacidade de detectar a versão do Java usada.

## Ferramentas de refatoração de código {#code-refactoring-tools}

### Novidades nas Ferramentas de refatoração de código {#what-is-new-crt}

* Nova versão do plug-in AIO-CLI lançada. A versão mais recente deste plug-in inclui várias correções de erros para o Repository Modernizer.
Consulte [Experiência unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para saber mais sobre este plug-in.

### Correções de erros {#bug-fixes-crt}

* Várias correções de erros feitas no Repository Modernizer.
Consulte [Recurso do GitHub: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obter mais detalhes.
