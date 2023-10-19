---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.4.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.4.0.
exl-id: c34aedee-e45a-4e2a-ae7f-930bc0cc026f
source-git-commit: 0109cea1be85e647fb6c04dde4714b162bdc75a5
workflow-type: ht
source-wordcount: '1171'
ht-degree: 100%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2023.4.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2023.4.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2023.4.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é 7 de junho de 2023. O próximo lançamento de recursos (2023.6.0) está planejado para 29 de junho de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de abril de 2023 que exibe um resumo dos recursos adicionados na versão 2023.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Experience Manager Sites] {#sites-features}

* Exporte fragmentos de conteúdo do AEM as a Cloud Service para o Adobe Target no formato JSON e crie ofertas JSON correspondentes no Target.
* A compatibilidade com os recursos de paginação e classificação de GraphQL, juntamente com aprimoramentos internos de armazenamento em cache, agora ajudam a melhorar o desempenho de aplicativos clientes dissociados ao buscar grandes conjuntos de conteúdo do AEM usando consultas e filtros de GraphQL complexos.

### Novos recursos no pré-lançamento do [!DNL Experience Manager Sites] {#prerelease-sites}

* Os fragmentos de conteúdo e suas referências agora podem ser publicados no [Serviço de visualização do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=pt-BR#access-preview-service) usando o [Console de fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=pt-BR), permitindo a visualização da experiência final em um aplicativo separado antes da publicação.
* As imagens agora podem ser otimizadas dinamicamente para entrega na Web com cenários headless usando o AEM GraphQL. [Variáveis de consulta](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=pt-BR#query-variables) podem ser definidas em consultas de GraphQL para permitir que aplicativos clientes dissociados solicitem imagens otimizadas do AEM.
* As tags das [variações de fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=pt-BR) agora podem ser exportadas em JSON usando a API de entrega de conteúdo do AEM GraphQL.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Adição de suporte para imagens WebP para extrair metadados automaticamente e gerar miniaturas e representações personalizadas. Agora a funcionalidade de tags inteligentes também é compatível com esses arquivos. As funcionalidades do Dynamic Media não são compatíveis com WebP como formato de entrada.

* [Melhorias na experiência de pesquisa](/help/assets/search-assets.md#aftersearch): agora você pode executar rapidamente as seguintes operações nos ativos exibidos nos resultados da pesquisa:

   * Criar um fluxo de trabalho
   * Criar uma versão
   * Criar ou remover relação de ativos

     Não é necessário navegar até o local do ativo e exibir suas propriedades para executar essas operações.

* Melhorias na usabilidade das facetas da pesquisa de cores: o campo de entrada para valores de cor agora é editável e os resultados da pesquisa são atualizados somente quando você sai do seletor de cores.

* Lançamento de um novo suporte de protocolo (DASH, Dynamic Adaptive Streaming over HTTP) para a transmissão adaptável na entrega de vídeos do Dynamic Media (com CMAF habilitado):
   * A transmissão adaptável (DASH/HLS) garante uma melhor experiência de exibição de vídeos ao usuário final
   * DASH é o protocolo internacional padrão para transmissão de vídeo adaptável e é amplamente adotado no setor
   * Disponível em todas as regiões; deve ser habilitado pelo tíquete de suporte

* _Instantâneo_ do Dynamic Media: faça experimentos com imagens de teste ou URLs do Dynamic Media para ver o resultado de diferentes modificadores de imagem e avaliar o recurso de Imagem inteligente, que otimiza o tamanho do arquivo (com entrega de WebP e AVIF), a largura de banda da rede e a proporção de pixels do dispositivo. Consulte [Instantâneo do Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=pt-BR).

### Recurso no pré-lançamento do [!DNL Assets] {#prerelease-feature-assets}

* Dynamic Media: a interface foi atualizada para que alguns campos relacionados ao Corte inteligente de um perfil de imagem reflitam as diretrizes atuais de definição do Corte inteligente. Consulte [Opções de corte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=pt-BR#crop-options).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-channel}

* **[Enviar formulários adaptáveis para o Microsoft® SharePoint e Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: agilize o processo do usuário empresarial para lançar novos formulários rapidamente e armazenar dados enviados em ferramentas usadas diariamente, como o site do Microsoft® SharePoint ou a pasta do OneDrive.

### Recursos no pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* [Formulários adaptáveis no editor de páginas do AEM](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): agora você pode usar o editor de páginas do AEM para criar e adicionar rapidamente vários formulários às páginas dos sites. Essa funcionalidade permite que os autores de conteúdo criem uma experiência perfeita para a captura de dados nas páginas de sites, usando o potencial dos componentes de formulários adaptáveis, incluindo comportamento dinâmico, validações, integração de dados, geração de documentos de registro e automação de processos empresariais. É possível:

   * Criar um formulário adaptável arrastando e soltando componentes de formulário no componente de Container de formulários adaptáveis do editor de sites do AEM ou de fragmentos de experiência.
   * Usar o assistente de formulários adaptáveis no editor de sites do AEM para criar formulários independentes de qualquer página de site, o que oferece a liberdade de reutilizar esses formulários em várias páginas.
   * Adicionar vários formulários a uma página de site, simplificando a experiência do usuário e fornecendo maior flexibilidade.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions para órgãos governamentais](/help/forms/adobe-sign-integration-adaptive-forms.md): o AEM Forms agora se integra ao Adobe Acrobat Sign Solutions para órgãos governamentais. Essa integração oferece um nível avançado de conformidade e segurança para assinaturas eletrônicas com envios de formulários adaptáveis para contas associadas a órgãos governamentais (departamentos e agências governamentais).

  A integração com o Adobe Acrobat Sign para órgãos governamentais permite que parceiros da Adobe e clientes governamentais usem assinaturas eletrônicas em formulários adaptáveis para alguns dos ramos de negócios mais essenciais e confidenciais. Essa camada adicional de segurança garante que todas as assinaturas eletrônicas sejam totalmente compatíveis com o nível moderado de conformidade do FedRAMP, proporcionando tranquilidade aos clientes governamentais da Adobe.

* Tratamento de erros aprimorado com manipuladores de erros personalizados no editor de regras: agora é possível chamar uma função personalizada (usando a Biblioteca do cliente) em resposta a um erro retornado por um serviço externo e fornecer uma resposta personalizada aos usuários finais. Como alternativa, você pode realizar ações específicas para erros retornados por um serviço. Por exemplo, você pode acionar um fluxo de trabalho personalizado no back-end para códigos de erro específicos ou informar ao cliente que o serviço está inativo.

  Essa funcionalidade ajuda a melhorar a capacidade geral de tratamento de erros, por meio da adição de respostas baseadas em padrões que são compatíveis com versões anteriores de manipuladores de erro prontos para uso, o que oferece maior flexibilidade e controle.

### Programa de adoção antecipada de formulários adaptáveis headless {#forms-early-adopter}

Use formulários adaptáveis hedless para permitir que seus desenvolvedores criem, publiquem e gerenciem formulários interativos que podem ser acessados e manuseados por meio de APIs, em vez de utilizar uma interface gráfica tradicional. Os formulários adaptáveis headless ajudam a:

* criar formulários multicanal de alta qualidade na linguagem de programação de sua escolha
* integrar formulários nativamente a seus aplicativos móveis e de desktop, sites e aplicativos de bate-papo
* reutilizar os componentes de interface de sua propriedade com aplicativos de formulários
* aproveitar o potencial do Adobe Experience Manager Forms

Você pode enviar um email para `aem-forms-headless@adobe.com` utilizando sua ID de email oficial para participar do programa de adoção antecipada.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* Regiões de publicação adicionais: clientes do Sites podem licenciar até três regiões de publicação, além da região principal. O tráfego é roteado para farms de publicação adicionais, o que resulta na redução da latência de determinadas solicitações e no aumento da resistência em caso de interrupções regionais. Entre em contato com o gerente de conta da Adobe para obter informações sobre licenciamento de [regiões de publicação adicionais](/help/operations/additional-publish-regions.md) em seus programas.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui.](/help/implementing/cloud-manager/release-notes/current.md)

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
