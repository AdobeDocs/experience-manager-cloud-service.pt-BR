---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.2.0.
description: as a Cloud Service Notas de versão do [!DNL Adobe Experience Manager] para 2021.2.0.
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 33%

---


# Notas de versão para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de Versão gerais para [!DNL Experience Manager] as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 é 25 de fevereiro de 2021.
A versão seguinte (2021.3.0) será lançada em 25 de março de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Gerenciamento de conteúdo headless {#headless}

* **[API do GraphQL para Entrega de fragmento de conteúdo](/help/headless/graphql-api/content-fragments.md)**: capacidade de consultar Fragmentos de conteúdo usando sintaxe GraphQL e esquemas com base em modelos de Fragmento de conteúdo para saída no formato JSON.

* **[Suporte de Autenticação para Solicitações da API do GraphQL](/help/headless/security/authentication.md)**: capacidade de autenticar solicitações da API do GraphQL com tokens de acesso para APIs do lado do servidor.

* **[O componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)**: adição de suporte para exibição e edição de SPA externo no AEM.

* **[Edição de um SPA externo no AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: adição da capacidade de carregar um aplicativo independente de página única em uma instância do AEM, adicionar seções editáveis de conteúdo e habilitar a criação.

* Saída JSON aprimorada da API do GraphQL, incluindo a capacidade de produzir rich text no formato JSON e localidades.

* Suporte para aninhamento de modelos de fragmento de conteúdo para permitir a criação de estruturas aninhadas de fragmento de conteúdo por meio de tipos de dados dedicados de referência de fragmento de conteúdo ou referências de fragmento de conteúdo embutidas em campos de texto de várias linhas.

* Regras de validação adicionais disponíveis nos tipos de dados do modelo de Fragmento de conteúdo, incluindo &quot;exclusivo&quot;, &quot;obrigatório&quot; e &quot;traduzível&quot;.

* Capacidade de marcar modelos de Fragmento de conteúdo e permitir a criação de Fragmento de conteúdo em uma pasta com políticas por tags ou caminhos.

* Aprimoramentos de usabilidade no editor de Fragmento de conteúdo, incluindo ação de publicação e exibição do modelo no qual um fragmento é baseado.

* Capacidade de visualizar a saída JSON diretamente no editor de Fragmento de conteúdo.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/sites-console/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## Novidades do [!DNL Assets] {#what-is-new-assets}

* O Assets pode ser originado usando [!DNL Experience Manager Assets Brand Portal]. Ele ajuda a obter ativos dos usuários da agência para novas campanhas de marketing, sessões de fotos e projetos.

* [!DNL Experience Manager Assets] como [!DNL Cloud Service] está qualificado para ter uma instância [!DNL Brand Portal] pré-configurada. O usuário [!DNL Cloud Manager] pode ativar [!DNL Brand Portal] em [!DNL Experience Manager Assets] como [!DNL Cloud Service]. Consulte [ativar Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=pt-BR).

* Agora, as empresas podem adquirir ativos usando o [!DNL Brand Portal]. O recurso de fornecimento de ativos usa o [!DNL Brand Portal] para ajudar os clientes a se envolver com usuários de agências a fim de obter ativos para novas campanhas de marketing, sessões de fotos e projetos. Consulte [origem do ativo em [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=pt-BR).

* O relatório de uso [!DNL Brand Portal] agora exibe somente os usuários ativos. Os usuários inativos não são exibidos agora. Os usuários ativos são aqueles cujas contas estão atribuídas a um perfil de produto no [!DNL Admin Console]. Consulte [[!DNL Brand Portal] relatórios](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html?lang=pt-BR).

* No [!DNL Brand Portal], é introduzida uma nova configuração de download que permite criar uma pasta separada para cada ativo ao baixar pastas, coleções e assim por diante. Consulte [configurações de download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=pt-BR).

## Correções de erros em [!DNL Assets] {#bug-fixes-assets}

* Quando vários ativos são selecionados para atualizar as propriedades, às vezes ocorre um erro ou as propriedades de um ativo desmarcado são atualizadas. (CQ-4316532)
* Ao tentar abrir o [!UICONTROL Painel de Pesquisa do Administrador do Assets], a página permanece em branco e um clique em [!UICONTROL Editar] > [!UICONTROL Configurações] gera um erro. (CQ-4315079)
* Quando uma nova versão de um ativo existente é criada após resolver o conflito de nomenclatura, os metadados do ativo original são substituídos. (CQ-4313594)
* Quando um ativo com texto de anotação longa é impresso, o texto da anotação é cortado, mesmo se houver espaço disponível. (CQ-4314101)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Gerenciamento de experiência do produto: enriqueça as páginas do catálogo de produtos individualmente com Fragmentos de experiência.

* Propriedades do console do produto estendido para mostrar Assets vinculados e Fragmentos de experiência, incluindo ações para navegar rapidamente até o conteúdo associado.

* Lançamento do site de referência CIF Venia - 24/02/2021 que inclui a versão mais recente dos componentes principais CIF v1.8.0. Consulte [Site de referência de CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) para obter mais detalhes.

* Lançamento de componentes principais de CIF v1.8.0. Consulte [Componentes principais do CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.2.0 é 11 de fevereiro de 2021.

### Novidades {#what-is-new-cloud-manager}


* Os clientes do Assets agora poderão escolher quando e onde implantar sua instância do Portal da marca de forma automatizada por meio da interface do usuário do Cloud Manager. Para um programa normal (que não é uma sandbox) que utiliza o Assets, o Brand Portal agora pode ser provisionado no ambiente de produção. O provisionamento pode ser feito apenas uma vez no ambiente de produção.

* O Arquétipo de Projetos AEM usado na criação do projeto e da sandbox foi atualizado para a versão 25.

* A lista de APIs descontinuadas identificadas durante a verificação de código foi refinada para incluir mais classes e métodos descontinuados nas versões mais recentes do SDK do Cloud Service.

* O perfil do SonarQube para o Cloud Manager foi atualizado para remover a regra do Sonar squid:S2142. Assim, não haverá mais conflito com as verificações de Interrupção de threads.

* A interface do usuário do Cloud Manager informará o usuário de que, temporariamente, talvez não possa adicionar/atualizar o nome de domínio porque o ambiente associado tem um pipeline em execução anexado a ele ou que está aguardando a etapa de aprovação.

* As propriedades definidas nos arquivos `pom.xml` do cliente com o prefixo “sonar” agora são removidas de maneira dinâmica para evitar falhas de build e de verificação de qualidade.

* A interface do usuário do Cloud Manager informará o usuário de que, temporariamente, talvez não possa selecionar um certificado SSL se ele estiver sendo usado por um nome de domínio em processo de implantação.

* Foram adicionadas Regras de qualidade do código adicionais para abordar problemas de compatibilidade do Cloud Service.

### Correções de erros {#bug-fixes-cloud-manager}

* A correspondência do certificado SSL com um nome de domínio não diferencia mais maiúsculas de minúsculas.

* A interface do usuário do Cloud Manager agora informará ao usuário se as chaves privadas do certificado não cumprirem o limite de 2048 bits com uma mensagem de erro apropriada.

* A interface do usuário do Cloud Manager informará o usuário de que, temporariamente, talvez não possa selecionar um certificado SSL se ele estiver sendo usado por um nome de domínio em processo de implantação.

* Em alguns casos, um problema interno pode causar a interrupção de uma exclusão do ambiente.

* Algumas falhas de pipeline foram relatadas incorretamente como erros de pipeline.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de transferência de conteúdo v1.2.4 é 10 de fevereiro de 2021.

### Correções de erros {#bug-fixes-ctt}

* Ao mapear vários usuários, as IDs IMS de alguns usuários eram mapeadas incorretamente. Isso foi corrigido.

### Data de lançamento {#release-date-ctt-feb}

A data de lançamento da ferramenta de transferência de conteúdo v1.2.2 é 1º de fevereiro de 2021.

### Novidades da Ferramenta de transferência de conteúdo {#what-is-new-ctt}

* Novo recurso e interface adicionados à Ferramenta de transferência de conteúdo - Ferramenta de mapeamento do usuário. Esse recurso mapeia automaticamente usuários e grupos existentes para suas IDs de sistema do Adobe Identity Management como parte da atividade de migração de conteúdo.
Consulte [Usar a ferramenta de Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=pt-BR) para obter mais detalhes.
* A Ferramenta de transferência de conteúdo agora migra todos os grupos e usuários referenciados no conjunto de migração, incluindo filhos.
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

### Novidades das Ferramentas de refatoração de código {#what-is-new-crt}

* Nova versão do plug-in AIO-CLI lançada. A versão mais recente deste plug-in inclui várias correções de erros para o Repository Modernizer.
Consulte [Experiência unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=pt-BR#benefits) para saber mais sobre este plug-in.

### Correções de erros {#bug-fixes-crt}

* Várias correções de erros feitas no Repository Modernizer.
Consulte [Recurso do GitHub: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obter mais detalhes.
