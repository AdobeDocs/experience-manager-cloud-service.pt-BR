---
title: Notas de versão do [!DNL Adobe Experience Manager]  as a Cloud Service 2023.1.0.
description: Notas de versão do [!DNL Adobe Experience Manager]  as a Cloud Service 2023.1.0.
exl-id: f134fdbc-224b-404c-b20f-44cae8bad681
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '976'
ht-degree: 100%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2023.1.0 {#release-notes}

A seção a seguir descreve as notas de versão de recursos do [!DNL Experience Manager] as a Cloud Service 2023.1.0.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão anteriores; por exemplo, as de 2021, 2022 e assim por diante.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento dos recursos do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 2023.1.0 é 9 de fevereiro de 2023. O próximo lançamento de recursos (2023.2.0) está planejado para 12 de abril de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo de Visão geral da versão de janeiro de 2023 que exibe um resumo dos recursos adicionados na versão 2023.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no pré-lançamento do [!DNL Sites] {#prerelease-features-sites}

* A API de entrega de conteúdo GraphQL do AEM agora é compatível com a [paginação](/help/headless/graphql-api/content-fragments.md#paging) e [classificação](/help/headless/graphql-api/content-fragments.md#sorting) de GraphQL, para tornar mais eficiente a busca e a renderização de grandes conjuntos de conteúdo. A paginação de GraphQL permite melhorar o tempo de resposta da consulta, retornando os resultados em subconjuntos, ao invés de todos de uma vez. A classificação de GraphQL permite colocar conjuntos de conteúdo em uma ordem desejada, facilitando o processamento do conteúdo por um aplicativo cliente.  O tempo de resposta da consulta é aprimorado ainda mais com a Filtragem híbrida no mecanismo GraphQL do AEM. O conteúdo agora é lido do JCR em conjuntos menores que correspondem aos filtros de consulta.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Os relatórios de ativos agora permitem que os administradores [gerem relatórios de download de ativos](/help/assets/asset-reports.md) por meio da implantação do Experience Manager Assets as a Cloud Service. Esses dados capacitam ainda mais os(as) admins a obter insights sobre as principais métricas de sucesso e medir a adoção de ativos em sua empresa e pelos clientes.

  ![Representação de PDF para outros formatos](/help/release-notes/assets/choose_report.png)

* O Experience Manager Assets agora [é compatível com o token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) além da chave de acesso para autenticação ao conectar-se à fonte de dados do Armazenamento do Azure Blob para assimilar ativos usando a ferramenta Importação em massa.

* Gerenciamento aprimorado de imagens CMYK no Asset Compute, permitindo gerar cortes e tags inteligentes para imagens CMYK.

### Novos recursos no pré-lançamento do [!DNL Assets] {#prerelease-features-assets}

* O Experience Manager Assets agora é compatível com a [assimilação em grande escala de ativos da Google Cloud Platform](/help/assets/add-assets.md#asset-bulk-ingestor) usando a ferramenta Importação em massa.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-channel}

* **[Etapas do fluxo de trabalho de geração de documentos PDF não interativos e saída imprimível](/help/forms/aem-forms-workflow-step-reference.md)**: automatize a criação de documentos PDF não interativos e saída imprimível para seus processos comerciais com as etapas do fluxo de trabalho do AEM, simplificando seu processo de geração de documentos e economizando tempo.
* **[Use notas de rodapé para fornecer citações ou informações adicionais nos formulários adaptáveis](/help/forms/footnotes-richtextsupport.md)**: as notas de rodapé de um formulário adaptável podem ser usadas para exibir informações sobre como preencher ou usar um formulário. Você também pode usá-las para fornecer informações entre parênteses, permissões de direitos autorais e outras informações úteis.

### Novos recursos no pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **[Use componentes principais de captura de dados para criar formulários adaptáveis](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR)**: o [editor de formulários adaptáveis](/help/forms/creating-adaptive-form-core-components.md) pode ser usado para criar formulários com base em componentes de captura de dados padronizados (componentes principais). Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital.
* **[Suporte a pipeline de front-end para estilizar formulários adaptáveis baseados em componentes principais](/help/forms/using-themes-in-core-components.md)**: utilize temas facilmente personalizáveis baseados em BEM para formulários adaptáveis baseados em componentes principais, implantando-os com o pipeline de implantação de front-end para aprimorar a aparência de seus formulários.
* **[Gerar documento de registro para formulários adaptáveis baseados em componentes principais](/help/forms/generate-document-of-record-core-components.md)**: crie um registro ao enviar o formulário adaptável baseado em componentes principais para um arquivamento de longo prazo, seja em formato impresso ou de documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Enviar formulários adaptáveis para o Microsoft SharePoint e Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: agilize o envio de dados com a capacidade de enviar dados de formulários adaptáveis diretamente para o Microsoft SharePoint e o Microsoft OneDrive. Você pode enviar dados baseados em esquema e sem esquema. Essas ações de envio são um complemento das ações de envio já disponíveis.
* **[Criação eficiente de formulários com o recurso Salvar um formulário adaptável como modelo](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: simplifique o processo de criação de formulários salvando um formulário adaptável como modelo e reutilizando esses modelos no próximo formulário adaptável.
* **[Conectar o AEM Forms a bancos de dados compatíveis com JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: conecte facilmente seu modelo de dados do AEM Forms a bancos de dados que oferecem suporte a JDBC, permitindo ler e gravar dados de maneira contínua.
* **[Integrar a pontos de acesso REST usando a Open API 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: conecte os modelos de dados de formulário do AEM Forms as a Cloud Service aos pontos de acesso REST que são compatíveis com a especificação da Open API versão 3.0, permitindo enviar e receber dados com facilidade.
* **[Compartilhar um formulário adaptável para revisão](/help/forms/create-reviews-forms.md)**: use o mecanismo de revisão de formulários adaptáveis para permitir que um ou mais revisores revisem o formulário.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* [Ambientes de desenvolvimento rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md): os RDEs permitem que os desenvolvedores solucionem problemas e implantem novos recursos no AEM as a Cloud Service rapidamente.

  Os ambientes de desenvolvimento rápido são um novo tipo de ambiente de nuvem criado como uma maneira rápida, consistente e extensível de validar se o código que funciona localmente também funciona conforme esperado na nuvem. Usando as ferramentas de linha de comando, “sincronize” rapidamente os pacotes de conteúdo, pacotes, arquivos de conteúdo, a configuração OSGI ou a configuração do Dispatcher com o RDE. Veja esse processo em ação no vídeo abaixo:

  >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

  Depois de validar o código com sucesso no RDE, é recomendável implantar em um ambiente de desenvolvimento da nuvem para testar as portas de qualidade do Cloud Manager, antes de implantar por meio do pipeline de produção em ambientes de preparo e produção.

  Cada programa inclui um RDE e é possível licenciar outros.

  >[!NOTE]
  >
  >Os RDEs serão lançados gradualmente nas próximas semanas; você pode enviar um email para aemcs-rde-support@adobe.com para obter prioridade na fila de espera.

* [Suporte estendido para tokens de acesso de API do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md): agora é possível gerar várias credenciais, o que é útil para cenários em que as APIs têm características diferentes. Agora também é possível revogar credenciais por meio do autoatendimento.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
