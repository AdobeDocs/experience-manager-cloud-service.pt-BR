---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 45004db44af48301f0a9cbd9f574ac34c360275e
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 16%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Aqui, você pode navegar até as notas de versão de versões anteriores, como 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] A versão atual do recurso (2023.6.0) é 29 de junho de 2023. A próxima versão do recurso (2023.7.0) está planejada para 27 de julho de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo de Visão geral da versão de junho de 2023 para ver um resumo dos recursos adicionados na versão 2023.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Experience Manager Sites] {#sites-features}

* Fragmentos de conteúdo e suas referências agora podem ser publicados na [Serviço de visualização do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en#access-preview-service) usando o [Console de fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en), permitindo que os usuários visualizem a experiência final em um aplicativo de visualização dissociado antes de entrar em funcionamento.
* As imagens agora podem ser otimizadas dinamicamente para entrega na Web em cenários headless usando o AEM GraphQL. [Variáveis de consulta](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=en#query-variables) O pode ser definido em queries do GraphQL para permitir que aplicativos clientes dissociados solicitem imagens otimizadas de AEM.
* Tags ativadas [Variações do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=en) agora pode ser enviado para JSON usando a API de entrega de conteúdo AEM GraphQL.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

**Visualização Disponibilidade de novos ativos**

A variável [nova visualização de Ativos](/help/assets/assets-view-introduction.md) O agora está disponível no Experience Manager Assets. A Exibição de ativos fornece uma interface simplificada, o que facilita o gerenciamento, a descoberta e a distribuição de ativos digitais. A experiência é direcionada para criativos, consumidores de ativos somente leitura e usuários de DAM mais leves.

![Gerenciamento de tags](/help/assets/assets/my-workspace.png)

**Aprimoramentos na experiência de pesquisa**

O Experience Manager Assets agora capacita você a fazer mais na interface do usuário de resultados de pesquisa: agora é possível:

* [Executar pesquisa no local do repositório atual](/help/assets/search-assets.md) por padrão, em vez de pesquisar a palavra-chave no repositório inteiro.

* [Navegar até o local da pasta](/help/assets/search-assets.md#aftersearch) para ativos exibidos nos resultados da pesquisa.

**Visualizações de miniaturas para ativos 3D**

[!DNL Experience Manager Assets] agora gera [visualizações de miniaturas para formatos de arquivo 3D comuns](/help/assets/file-format-support.md) incluindo gLB, USDz, FBX, 3DS, OBJ e SBSAR. Quando esses arquivos são carregados, as miniaturas são geradas automaticamente por padrão.

**Configuração de compartilhamento de link**

Uma nova experiência aprimorada do usuário para [criação de compartilhamentos de links](/help/assets/share-assets.md) junto com um novo conjunto de configurações que permite que os administradores personalizem o comportamento padrão desse recurso para seus usuários.

![Gerenciamento de tags](/help/assets/assets/config-email-service.png)

**Dynamic Media: campos relacionados ao Corte inteligente atualizados no perfil de imagem**

A interface de alguns campos relacionados ao Corte inteligente em um Perfil de imagem agora é atualizada para refletir as diretrizes atuais para a definição de um Corte inteligente. Consulte [Opções de corte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=en#crop-options).

### Novos recursos na exibição do Assets {#assets-view-features}

**Marcação hierárquica de ativos para obter uma experiência de pesquisa mais rápida**

Listas planas de vocabulários controlados tornam-se incontroláveis com o tempo. A exibição de ativos agora é compatível [estrutura hierárquica de marcação](/help/assets/tagging-management-assets-view.md), que facilita a aplicação de metadados relevantes, a categorização de ativos, o suporte a pesquisas, a reutilização de tags, a melhoria da descoberta e assim por diante.

![Gerenciamento de tags](/help/assets/assets/tags-hierarchy.png)

**Fixar arquivos, pastas e coleções para acesso rápido**

Agora você pode [fixe arquivos, pastas e coleções para agilizar o acesso](/help/assets/my-workspace-assets-view.md) a esses itens quando você precisar deles mais tarde. Os itens fixados são exibidos na variável **Acesso rápido** seção do Meu espaço de trabalho. Você pode acessá-las usando Meu espaço de trabalho em vez de navegar até o local em que são salvas no repositório.

![Tarefas no Espaço de trabalho](/help/assets/assets/quick-access.png)

**Filtrar ativos na pasta Lixeira**

A visualização de ativos agora permite [filtrar ativos disponíveis na pasta Lixeira](/help/assets/navigate-assets-view.md). Você pode aplicar filtros padrão ou personalizados para pesquisar ativos apropriados na pasta Lixeira para restaurá-los ou excluí-los permanentemente.

**Visualizações de miniaturas para ativos 3D**

A visualização de ativos agora gera visualizações de miniaturas para formatos de arquivo 3D comuns, incluindo gLB, USDz, FBX, 3DS, OBJ e SBSAR. Quando esses arquivos são carregados para a visualização de Ativos, as miniaturas são geradas automaticamente pelo sistema, por padrão.

![Tarefas no Espaço de trabalho](/help/assets/assets/3d-preview.png)

**Exibir os principais termos pesquisados**

A exibição de ativos agora é compatível [exibindo os principais termos pesquisados na implantação](/help/assets/my-workspace-assets-view.md) usando o **Insights** seção do Meu espaço de trabalho. Você também pode navegar até os Insights detalhados para exibir as principais pesquisas durante os últimos 30 dias ou 12 meses.

![Tarefas no Espaço de trabalho](/help/assets/assets/insights-top-searches.png)

**Aprimoramentos no formulário de metadados**

A visualização de ativos agora permite [adicionar componentes de propriedade de texto de vários valores e lista suspensa](/help/assets/metadata-assets-view.md#property-components) aos formulários de metadados.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-channel}

* [Forms adaptável no editor de páginas AEM e no fragmento de experiência](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): Agora você pode usar o Editor de páginas AEM e o Fragmento de experiência para criar e adicionar rapidamente vários formulários às suas páginas do AEM Sites. Esse recurso permite que os autores de conteúdo criem experiências de captura de dados perfeitas nas páginas do Sites, usando o potencial dos componentes do Adaptive Forms, incluindo comportamento dinâmico, validações, integração de dados e geração de documentos de registro e automação de processos de negócios.

  >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Usar o Adobe Acrobat Sign Solutions para o governo (Reclamação HIPPA) com o AEM Forms](/help/forms/adobe-sign-integration-adaptive-forms.md): o AEM Forms agora se integra ao Adobe Acrobat Sign Solutions para o governo. Essa integração oferece um nível avançado de conformidade e segurança para assinaturas eletrônicas com envios de formulários adaptáveis para contas associadas ao governo (departamentos e agências governamentais).

  A integração com o Adobe Acrobat Sign Solutions para o governo permite que os parceiros do Adobe e os clientes do governo usem assinaturas eletrônicas no Adaptive Forms para algumas das linhas de negócios mais críticas e confidenciais. Essa camada adicional de segurança garante que todas as assinaturas eletrônicas sejam totalmente compatíveis com a conformidade Moderada do FedRAMP, proporcionando tranquilidade aos clientes governamentais Adobe.

* [Tratamento de erros aprimorado com manipuladores de erros personalizados no editor de regras](/help/forms/add-custom-error-handler-adaptive-forms.md): agora você pode chamar uma função personalizada (usando a Biblioteca do cliente) em resposta a um erro retornado por um serviço externo e fornecer uma resposta personalizada aos usuários finais. Ou você pode realizar ações específicas para erros retornados por um serviço. Por exemplo, você pode chamar um fluxo de trabalho personalizado no backend para códigos de erro específicos ou informar ao cliente que o serviço está inativo.

  Essa funcionalidade ajuda a melhorar a capacidade geral de tratamento de erros, introduzindo respostas de erro baseadas em padrões que são compatíveis com versões anteriores de manipuladores de erro OOTB, com maior flexibilidade e controle.

* [Métodos de autenticação aprimorados para o modelo de dados de formulário](/help/forms/configure-data-sources.md): Experimente maior segurança com a introdução da autenticação baseada em Credenciais do cliente para conectar o AEM Forms (Modelos de dados de formulário) a fontes de dados compatíveis. Esse aprimoramento elimina a necessidade de representação ou logon de usuário, reforçando a proteção de seus dados.

* [Criar Forms adaptável com seções que podem ser repetidas](/help/forms/create-forms-repeatable-sections.md): Agora você pode fazer [Acordeão](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html), [Assistente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html), [Painel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html), e [Guias Horizontais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html) componentes em um formulário adaptável baseado em Componentes principais para criar seções repetíveis.

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  Essas seções repetíveis permitem fornecer um número ilimitado de entradas sem uma contagem de campos fixa. É útil quando as instâncias de dados necessárias são desconhecidas antecipadamente. Os usuários do Forms podem adicionar ou remover seções facilmente, tornando os formulários adaptáveis a diferentes cenários de entrada de dados e simplificando a coleta de várias ocorrências dos mesmos dados.

* **[Enviar Forms adaptável ao Microsoft® SharePoint e Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: Agora você pode enviar dados do Adaptive Forms para ferramentas diárias como o Microsoft® SharePoint Site ou Microsoft® OneDrive.

### Programa de adoção antecipada de formulários adaptáveis headless {#forms-early-adopter}

Uso [Forms adaptável headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) para permitir que os desenvolvedores criem, publiquem e gerenciem formulários interativos que possam ser acessados e interagidos por meio de APIs, em vez de uma interface gráfica tradicional. Os formulários adaptáveis headless ajudam a:

* criar formulários multicanal de alta qualidade na linguagem de programação de sua escolha
* integrar formulários nativamente a seus aplicativos móveis e de desktop, sites e aplicativos de bate-papo
* reutilizar os componentes de interface de sua propriedade com aplicativos de formulários
* use o poder do Adobe Experience Manager Forms

Você pode enviar um email para `aem-forms-headless@adobe.com` do seu ID de e-mail oficial para participar do programa de adoção antecipada.


## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
