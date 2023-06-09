---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: d4d44f452406e452372e409c6594ef4a256b9682
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 31%

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

A data de lançamento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] A versão atual do recurso (2023.4.0) é 7 de junho de 2023. A próxima versão do recurso (2023.6.0) está planejada para 29 de junho de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de abril de 2023 que exibe um resumo dos recursos adicionados na versão 2023.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Experience Manager Sites] {#sites-features}

* Exporte fragmentos de conteúdo do AEM as a Cloud Service para o Adobe Target como ofertas JSON.
* O suporte para os recursos de paginação e classificação de GraphQL, juntamente com aprimoramentos internos de armazenamento em cache, agora ajuda a melhorar o desempenho de aplicativos clientes dissociados ao buscar grandes conjuntos de conteúdo do AEM usando consultas e filtros de GraphQL complexos.

### Novos recursos no [!DNL Experience Manager Sites] pré-arrendar {#prerelease-sites}

* Fragmentos de conteúdo e suas referências agora podem ser publicados na [Serviço de visualização do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en#access-preview-service) usando o [Console de fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en), permitindo que os usuários visualizem a experiência final em um aplicativo de visualização dissociado antes de entrar em funcionamento.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Adição de suporte para imagens WebP para extrair metadados automaticamente e gerar miniaturas e representações personalizadas. O recurso Tags inteligentes agora também é compatível com esses arquivos. Os recursos do Dynamic Media não são compatíveis com WebP como formato de entrada.

* [Aprimoramentos na experiência de pesquisa](/help/assets/search-assets.md#aftersearch) - Agora você pode executar rapidamente as seguintes operações nos ativos exibidos nos resultados da pesquisa:

   * Criar um workflow
   * Criar uma versão
   * Relacionar ou não relacionar ativos

     Não é necessário navegar até o local do ativo e visualizar suas propriedades para executar essas operações.

* Melhorias na usabilidade das facetas de Pesquisa de cores - O campo de entrada para valores de cor agora é editável e os resultados da pesquisa são atualizados somente quando você sai do seletor de cores.

* Novo suporte de protocolo iniciado (DASH - Dynamic Adaptive Streaming por HTTP) para transmissão adaptável na entrega de vídeo do Dynamic Media (com o CMAF ativado):
   * A transmissão adaptável (DASH/HLS) garante uma melhor experiência de exibição de vídeos ao usuário final
   * DASH é o protocolo internacional padrão para transmissão de vídeo adaptável e é amplamente adotado no setor
   * Disponível em todas as regiões, para ser ativado pelo tíquete de suporte

* Dynamic Media _Instantâneo_ - Experimente com imagens de teste ou URLs Dynamic Media, para ver a saída de diferentes modificadores de imagem e avaliar as otimizações de Imagem inteligente para o tamanho do arquivo (com entrega de WebP e AVIF), largura de banda da rede e Proporção de pixels do dispositivo. Consulte [Instantâneo do Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).

### Recurso no [!DNL Assets] pré-lançamento {#prerelease-feature-assets}

* Dynamic Media - A interface de alguns campos relacionados ao Corte inteligente em um Perfil de imagem agora é atualizada para refletir as diretrizes atuais para a definição de um Corte inteligente. Consulte [Opções de corte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=en#crop-options).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-channel}

* **[Enviar Forms adaptável ao Microsoft® SharePoint e Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: aumente a agilidade do usuário empresarial para que você possa iniciar novos formulários rapidamente e armazenar dados enviados em ferramentas diárias que eles usam, como o site do Microsoft® SharePoint ou a pasta do OneDrive.

### Recursos no pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* [Forms adaptável no editor de páginas AEM](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): Agora você pode usar o Editor de páginas AEM para criar e adicionar rapidamente vários formulários às páginas dos sites. Esse recurso permite que os autores de conteúdo criem experiências de captura de dados perfeitas nas páginas do Sites, usando o potencial dos componentes de formulários adaptáveis, incluindo comportamento dinâmico, validações, integração de dados, geração de documentos de registro e automação de processos de negócios. É possível:

   * Crie um formulário adaptável arrastando e soltando componentes de formulário no componente de Contêiner adaptável do Forms no editor do AEM Sites ou em Fragmentos de experiência.
   * Use o Assistente do Forms adaptável no editor do AEM Sites para criar formulários independentes de qualquer página do Sites, fornecendo a liberdade de reutilizar esses formulários em várias páginas.
   * Adicione vários formulários a uma página do Sites, simplificando a experiência do usuário e fornecendo maior flexibilidade.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Integração e conformidade aprimoradas com o Adobe Acrobat Sign](/help/forms/adobe-sign-integration-adaptive-forms.md): o AEM Forms agora se integra ao Adobe Acrobat Sign para o governo. Essa integração oferece um nível avançado de conformidade e segurança para assinaturas eletrônicas com envios de formulários adaptáveis para contas associadas ao governo (departamentos e agências governamentais).

  A integração com o Adobe Acrobat Sign para o governo permite que os parceiros do Adobe e os clientes do governo usem assinaturas eletrônicas no Adaptive Forms para algumas das linhas de negócios mais críticas e confidenciais. Essa camada adicional de segurança garante que todas as assinaturas eletrônicas sejam totalmente compatíveis com a conformidade Moderada do FedRAMP, proporcionando tranquilidade aos clientes governamentais Adobe.

* Tratamento de erros aprimorado com manipuladores de erros personalizados no editor de regras. Agora é possível chamar uma função personalizada (usando a Biblioteca do cliente) em resposta a um erro retornado por um serviço externo e fornecer uma resposta personalizada aos usuários finais. Ou você pode realizar ações específicas para erros retornados por um serviço. Por exemplo, você pode chamar um fluxo de trabalho personalizado no backend para códigos de erro específicos ou informar ao cliente que o serviço está inativo.

  Essa funcionalidade ajuda a melhorar a capacidade geral de tratamento de erros, introduzindo respostas de erro baseadas em padrões que são compatíveis com versões anteriores de manipuladores de erro OOTB, com maior flexibilidade e controle.

### Programa de adoção antecipada de formulários adaptáveis headless {#forms-early-adopter}

Use formulários adaptáveis hedless para permitir que seus desenvolvedores criem, publiquem e gerenciem formulários interativos que podem ser acessados e manuseados por meio de APIs, em vez de utilizar uma interface gráfica tradicional. Os formulários adaptáveis headless ajudam a:

* criar formulários multicanal de alta qualidade na linguagem de programação de sua escolha
* integrar formulários nativamente a seus aplicativos móveis e de desktop, sites e aplicativos de bate-papo
* reutilizar os componentes de interface de sua propriedade com aplicativos de formulários
* use o poder do Adobe Experience Manager Forms

Você pode enviar um email para `aem-forms-headless@adobe.com` do seu ID de e-mail oficial para participar do programa de adoção antecipada.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* Regiões de Publicação Adicionais: Os Clientes do Sites podem licenciar até três regiões de publicação, além da região principal. O tráfego é roteado para farms de publicação adicionais, o que resulta na redução da latência de determinadas solicitações e no aumento da resiliência contra interrupções regionais. Entre em contato com o Gerente de conta do Adobe para obter informações sobre licenciamento [Regiões de publicação adicionais](/help/operations/additional-publish-regions.md) para seus programas.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui.](/help/implementing/cloud-manager/release-notes/current.md)

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
