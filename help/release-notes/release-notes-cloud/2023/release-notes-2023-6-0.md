---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.6.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.6.0.
source-git-commit: 7d09cafc4f8518fee185d3f9efc76c33ec20f9a3
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 95%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2023.6.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2023.6.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2023.6.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é 29 de junho de 2023. O próximo lançamento de recursos (2023.7.0) está planejado para 27 de julho de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo de visão geral da versão de junho de 2023 para ver um resumo dos recursos adicionados na versão 2023.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Experience Manager Sites] {#sites-features}

* Os fragmentos de conteúdo e suas referências agora podem ser publicados no [Serviço de visualização do AEM](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) usando o [Console de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console), permitindo a visualização da experiência final em um aplicativo separado antes da publicação.

![Visualizar no Console de fragmentos de conteúdo](/help/assets/content-fragments-console-preview.png)

* As imagens agora podem ser otimizadas dinamicamente para entrega na Web com cenários headless usando o AEM GraphQL. [Variáveis de consulta](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=pt-BR#query-variables) podem ser definidas em consultas de GraphQL para permitir que aplicativos clientes dissociados solicitem imagens otimizadas do AEM.
* As tags das [variações de fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=pt-BR) agora podem ser exportadas em JSON usando a API de entrega de conteúdo do AEM GraphQL.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

**Disponibilidade da nova visualização de ativos**

Uma [nova visualização de ativos](/help/assets/assets-view-introduction.md) está disponível no Experience Manager Assets. Essa visualização de ativos fornece uma interface simplificada que facilita o gerenciamento, a descoberta e a distribuição de ativos digitais. A experiência é direcionada para consumidores de ativos criativos do tipo somente leitura e que não exigem muito do DAM.

![Gerenciamento de tags](/help/assets/assets/my-workspace.png)

**Aprimoramentos na experiência de pesquisa**

A interface de resultados de pesquisa do Experience Manager Assets agora fornece mais recursos, permitindo:

* [Executar uma pesquisa no local do repositório atual](/help/assets/search-assets.md) por padrão, em vez de pesquisar a palavra-chave no repositório inteiro.

* [Navegar até o local da pasta](/help/assets/search-assets.md#aftersearch) em que estão contidos os ativos exibidos nos resultados da pesquisa.

**Visualizações de miniaturas para ativos 3D**

O [!DNL Experience Manager Assets] agora gera [visualizações de miniaturas para formatos de arquivo 3D comuns](/help/assets/file-format-support.md) incluindo gLB, USDz, FBX, 3DS, OBJ e SBSAR. Quando esses arquivos são carregados, as miniaturas são geradas automaticamente por padrão.

**Configuração de compartilhamento de link**

Uma nova experiência de usuário aprimorada para [criar compartilhamentos de links](/help/assets/share-assets.md) e um novo conjunto de configurações que permite que admins personalizem o comportamento padrão desse recurso para seus usuários.

![Gerenciamento de tags](/help/assets/assets/config-email-service.png)

**Dynamic Media: atualização de campos relacionados ao Corte inteligente no perfil de imagem**

A interface foi atualizada para que alguns campos relacionados ao Corte inteligente de um perfil de imagem reflitam as diretrizes atuais de definição de um Corte inteligente. Consulte [Opções de corte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=pt-BR#crop-options).

### Novos recursos na visualização de ativos {#assets-view-features}

**Marcação hierárquica de ativos para uma experiência de pesquisa mais rápida**

Listas planas de vocabulários controlados tornam-se incontroláveis com o tempo. A visualização de ativos agora possui uma [estrutura hierárquica de marcação](/help/assets/tagging-management-assets-view.md), que facilita a aplicação de metadados relevantes, a categorização de ativos, o suporte a pesquisas, a reutilização de tags, a melhoria da descoberta e assim por diante.

![Gerenciamento de tags](/help/assets/assets/tags-hierarchy.png)

**Fixar arquivos, pastas e coleções para acesso rápido**

Agora você pode [fixar arquivos, pastas e coleções para agilizar o acesso](/help/assets/my-workspace-assets-view.md) a esses itens quando precisar deles mais tarde. Os itens fixados são exibidos na seção **Acesso rápido** do Meu espaço de trabalho. Você pode acessá-los usando o Meu espaço de trabalho em vez de navegar até o local em que foram salvos no repositório.

![Tarefas no espaço de trabalho](/help/assets/assets/quick-access.png)

**Filtrar ativos na pasta Lixeira**

A visualização de ativos agora permite [filtrar ativos disponíveis na pasta Lixeira](/help/assets/navigate-assets-view.md). Você pode aplicar filtros padrão ou personalizados para pesquisar ativos apropriados na pasta Lixeira e restaurá-los ou excluí-los permanentemente.

**Visualizações de miniaturas para ativos 3D**

A visualização de ativos agora gera visualizações de miniaturas para formatos de arquivo 3D comuns, incluindo gLB, USDz, FBX, 3DS, OBJ e SBSAR. Quando esses arquivos são carregados na visualização de ativos, as miniaturas são geradas automaticamente pelo sistema, por padrão.

![Tarefas no Espaço de trabalho](/help/assets/assets/3d-preview.png)

**Exibir os principais termos pesquisados**

A exibição de arquivos agora é compatível com a [visualização dos principais termos pesquisados na implantação](/help/assets/my-workspace-assets-view.md) usando a seção **Insights** do Meu espaço de trabalho. Também é possível navegar até os Insights detalhados para exibir as principais pesquisas durante os últimos 30 dias ou 12 meses.

![Tarefas no Espaço de trabalho](/help/assets/assets/insights-top-searches.png)

**Aprimoramentos no formulário de metadados**

A visualização de arquivos agora permite [adicionar componentes de propriedade de texto de vários valores e de lista suspensa](/help/assets/metadata-assets-view.md#property-components) aos formulários de metadados.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-channel}

* [Formulários adaptáveis no editor de páginas do AEM](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): agora você pode usar o editor de páginas do AEM para criar e adicionar rapidamente vários formulários às páginas dos sites. Essa funcionalidade permite que os autores de conteúdo criem uma experiência perfeita para a captura de dados nas páginas de sites, usando o potencial dos componentes de formulários adaptáveis, incluindo comportamento dinâmico, validações, integração de dados, geração de documentos de registro e automação de processos empresariais. É possível:

   * Criar um formulário adaptável arrastando e soltando componentes de formulário no componente de Container de formulários adaptáveis do editor de sites do AEM ou de fragmentos de experiência.
   * Usar o assistente de formulários adaptáveis no editor de sites do AEM para criar formulários independentes de qualquer página de site, o que oferece a liberdade de reutilizar esses formulários em várias páginas.
   * Adicionar vários formulários a uma página de site, simplificando a experiência do usuário e fornecendo maior flexibilidade.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions para órgãos governamentais](/help/forms/adobe-sign-integration-adaptive-forms.md): o AEM Forms agora se integra ao Adobe Acrobat Sign Solutions para órgãos governamentais. Essa integração oferece um nível avançado de conformidade e segurança para assinaturas eletrônicas com envios de formulários adaptáveis para contas associadas a órgãos governamentais (departamentos e agências governamentais).

  A integração com o Adobe Acrobat Sign Solutions para os órgãos governamentais permite que parceiros da Adobe e clientes governamentais usem assinaturas eletrônicas em formulários adaptáveis para alguns dos ramos de negócios mais críticos e sensíveis. Essa camada adicional de segurança garante que todas as assinaturas eletrônicas sejam totalmente compatíveis com o nível moderado de conformidade do FedRAMP, proporcionando tranquilidade aos clientes governamentais da Adobe.

* [Tratamento de erros aprimorado com manipuladores de erros personalizados no editor de regras](/help/forms/add-custom-error-handler-adaptive-forms.md): agora é possível chamar uma função personalizada (usando a Biblioteca do cliente) em resposta a um erro retornado por um serviço externo e fornecer uma resposta personalizada aos usuários finais. Como alternativa, você pode realizar ações específicas para erros retornados por um serviço. Por exemplo, você pode acionar um fluxo de trabalho personalizado no back-end para códigos de erro específicos ou informar ao cliente que o serviço está inativo.

  Essa funcionalidade ajuda a melhorar a capacidade geral de tratamento de erros, por meio da adição de respostas baseadas em padrões que são compatíveis com versões anteriores de manipuladores de erro prontos para uso, o que oferece maior flexibilidade e controle.

* [Métodos de autenticação aprimorados para o modelo de dados de formulário](/help/forms/configure-data-sources.md): Experimente maior segurança com a introdução da autenticação baseada em Credenciais do cliente para conectar o AEM Forms a fontes de dados compatíveis. Esse aprimoramento elimina a necessidade de representação ou logon de usuário, reforçando a proteção de seus dados.

* [Forms adaptável com seções que podem ser repetidas](/help/forms/create-forms-repeatable-sections.md): Agora você pode fazer [Acordeão](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=pt-BR), [Assistente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=pt-br), [Painel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html?lang=pt-br), e [Guias Horizontais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=pt-br) componentes em um formulário adaptável baseado em Componentes principais para criar seções repetíveis.

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  Essas seções repetíveis permitem fornecer um número ilimitado de entradas sem uma contagem de campo fixa. É útil quando as instâncias de dados necessárias são desconhecidas. Os usuários do Forms podem adicionar ou remover seções facilmente, tornando os formulários adaptáveis a diferentes cenários de entrada de dados e simplificando a coleta de várias ocorrências dos mesmos dados.

* **[Enviar formulários adaptáveis para o Microsoft® SharePoint e Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: agilize o processo do usuário empresarial para lançar novos formulários rapidamente e armazenar dados enviados em ferramentas usadas diariamente, como o site do Microsoft® SharePoint ou a pasta do OneDrive.

### Programa de adoção antecipada de formulários adaptáveis headless {#forms-early-adopter}

Use [Formulários adaptáveis Headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=pt-BR) para permitir que seus desenvolvedores criem, publiquem e gerenciem formulários interativos que podem ser acessados e manuseados por meio de APIs, em vez de utilizar uma interface gráfica tradicional. Os formulários adaptáveis headless ajudam a:

* criar formulários multicanal de alta qualidade na linguagem de programação de sua escolha
* integrar formulários nativamente a seus aplicativos móveis e de desktop, sites e aplicativos de bate-papo
* reutilizar os componentes de interface de sua propriedade com aplicativos de formulários
* aproveitar o potencial do Adobe Experience Manager Forms

Você pode enviar um email para `aem-forms-headless@adobe.com` utilizando sua ID de email oficial para participar do programa de adoção antecipada.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
