---
title: Notas de versão atuais para [!DNL Adobe Experience Manager] como um Cloud Service.
description: Notas de versão atuais para [!DNL Adobe Experience Manager] como um Cloud Service.
translation-type: tm+mt
source-git-commit: a93db92689928a900662a39b11bb5a7ea9724e62
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 4%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] como um Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] como Cloud Service 2021.2.0 é 25 de fevereiro de 2021.
A seguinte versão (2021.3.0) será lançada em 25 de março de 2021.

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

## Novidades em [!DNL Assets] {#what-is-new-assets}

* Em [!DNL Brand Portal], uma nova configuração de download é introduzida, permitindo que você crie uma pasta separada para cada ativo ao baixar pastas, coleção e assim por diante. consulte [configurações de download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  -->

## Correções de erros em [!DNL Assets] {#bug-fixes-assets}

* Quando uma nova versão de um ativo existente é criada após resolver o conflito de nomes, os metadados do ativo original são substituídos. (CQ-4313594)
* Quando um ativo com um texto de anotação longo é impresso, o texto da anotação é aparado, mesmo se houver espaço disponível. (CQ-4314101)
* Quando vários ativos são selecionados para atualizar as propriedades, às vezes ocorre um erro ou as propriedades de um ativo desmarcado são atualizadas. (CQ-4316532)
* Ao tentar abrir [!UICONTROL Painel de pesquisa do administrador do Assets], a página permanece em branco e clicar em [!UICONTROL Editar] > [!UICONTROL Definições] gera um erro. (CQ-4315079)

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2021.2.0 é 11 de fevereiro de 2021.

### Novidades {#what-is-new-cloud-manager}


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

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt}

A data de lançamento da Content Transfer Tool v1.2.4 é 10 de fevereiro de 2021.

### Correções de erros {#bug-fixes-ctt}

* Ao mapear vários usuários, algumas IDs IMS estavam sendo mapeadas incorretamente. Isso foi corrigido.

### Data de lançamento {#release-date-ctt-feb}

A data de lançamento da Content Transfer Tool v1.2.2 é 1 de fevereiro de 2021.

### Novidades da Ferramenta de transferência de conteúdo {#what-is-new-ctt}

* Novo recurso e interface adicionada à Ferramenta de transferência de conteúdo - Ferramenta de mapeamento do usuário. Esse recurso mapeia automaticamente usuários e grupos existentes para suas IDs de sistema Adobe Identity Management como parte da atividade de migração de conteúdo.
Consulte [Usando a ferramenta de mapeamento do usuário](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obter mais detalhes.
* A Ferramenta de transferência de conteúdo agora migra todos os grupos e usuários referenciados no conjunto de migração, incluindo filhos.
* Os usuários podem selecionar determinados caminhos em `/etc` ao criar conjuntos de migração.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Best Practices Analyzer v2.1.2 é 18 de fevereiro de 2021.

### Novidades do Analisador de práticas recomendadas {#what-is-new-bpa}

* Capacidade de detectar o uso da implementação do AEM Forms e AEM Forms e indicar áreas relevantes para migrar para o AEM Forms como Cloud Service.
* Capacidade de detectar e relatar sobre o uso e contagem de componentes e modelos personalizados.
* Capacidade de detectar o tipo de armazenamento de nó e armazenamento de dados usado.
* Capacidade de detectar o uso do Dynamic Media.
* Capacidade de detectar a versão do Java usada.

## Ferramentas de refatoração de código {#code-refactoring-tools}

### Novidades das Ferramentas de Refatoração de Código {#what-is-new-crt}

* Nova versão do plug-in AIO-CLI lançada. A versão mais recente deste plug-in inclui várias correções de erros para o Repository Modernizer.
Consulte [Experiência unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para saber mais sobre este plug-in.

### Correções de erros {#bug-fixes-crt}

* Várias correções de erros feitas no Repository Modernizer.
Consulte [Recurso GitHub: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obter mais detalhes.








