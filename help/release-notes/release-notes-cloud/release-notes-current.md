---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
source-git-commit: b47901d749712384506cf4eb03c099027933e95f
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 23%

---


# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas de versão do recurso para a versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2021, 2022 e assim por diante.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a versão do recurso atual (2023.1.0) é 9 de fevereiro de 2023. A próxima versão de recurso (2023.2.0) está planejada para 6 de abril de 2023.

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de janeiro de 2023 que exibe um resumo dos recursos adicionados na versão 2023.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no pré-lançamento do [!DNL Sites] {#prerelease-features-sites}

* A API de entrega de conteúdo do GraphQL AEM agora é compatível com o GraphQL [Paginação](/help/headless/graphql-api/content-fragments.md#paging) e [Classificação](/help/headless/graphql-api/content-fragments.md#sorting), para tornar a busca e renderização de conjuntos de conteúdo grandes mais eficiente. A paginação do GraphQL permite melhorar o tempo de resposta da consulta, retornando resultados em subconjuntos, em vez de todos ao mesmo tempo. A classificação do GraphQL permite colocar conjuntos de conteúdo na ordem desejada, tornando mais fácil para um aplicativo cliente processar o conteúdo.  O tempo de resposta da consulta é aprimorado ainda mais com a Filtragem híbrida no mecanismo GraphQL AEM. O conteúdo agora é lido do JCR em conjuntos menores que correspondem aos filtros de consulta.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Os Relatórios de ativos agora incluem a capacidade dos administradores de [gerar relatórios de download de ativos](/help/assets/asset-reports.md) da implantação as a Cloud Service do Experience Manager Assets. Esses dados capacitam ainda mais os administradores a obter insights das principais métricas de sucesso para medir a adoção dos Ativos na empresa e pelos clientes.

   ![Representação de PDF para outros formatos](/help/release-notes/assets/choose_report.png)

* O Experience Manager Assets agora [é compatível com o token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) além da Chave de acesso para autenticação ao conectar-se à fonte de dados do Armazenamento de Blobs do Azure para assimilar ativos usando a ferramenta Importação em massa.

* Gerenciamento aprimorado de imagens CMYK no Asset compute, permitindo gerar Recorte inteligente e Tags inteligentes para imagens CMYK.

### Novos recursos no pré-lançamento do [!DNL Assets] {#prerelease-features-assets}

* O Experience Manager Assets agora é compatível [assimilação em grande escala de ativos da Google Cloud Platform](/help/assets/add-assets.md#asset-bulk-ingestor) usando a ferramenta Importação em massa .

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos disponíveis em [!DNL Forms] {#new-features-available-in-channel}

* **[Etapas de fluxo de trabalho para gerar documentos PDF não interativos e saída imprimível](/help/forms/aem-forms-workflow-step-reference.md)**: Automatize a criação de documentos PDF não interativos e a saída imprimível para seus processos de negócios com AEM etapas do fluxo de trabalho, simplificando o processo de geração de documentos e economizando tempo.
* **[Use notas de rodapé para fornecer citações ou informações adicionais no Adaptive Forms](/help/forms/footnotes-richtextsupport.md)**: Use as Notas de rodapé em um formulário adaptável para exibir as informações sobre como preencher ou usar um formulário. Você também pode usá-lo para fornecer informações parênteses, permissões de direitos autorais e outras informações úteis.

### Novos recursos no pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **[Use os componentes principais de captura de dados para criar o Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en)**: [Usar o editor adaptável do Forms](/help/forms/creating-adaptive-form-core-components.md) para criar formulários com base em componentes padronizados de captura de dados (Componentes principais). Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital.
* **[Suporte a pipeline de fronteira para o Forms adaptável baseado em componentes principais de estilo](/help/forms/using-themes-in-core-components.md)**: Utilize temas facilmente personalizáveis baseados em BEM para o Forms adaptável baseado em componentes principais, implantando-os com o pipeline de implantação do front-end para aprimorar a aparência de seus formulários.
* **[Gerar documento de registro para Forms adaptável baseado em componentes principais](/help/forms/generate-document-of-record-core-components.md)**: Crie um registro para o Formulário adaptativo baseado em componentes principais no envio para arquivamento de longo prazo, na impressão ou no formato do documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Enviar Forms adaptável para o Microsoft SharePoint e Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: Simplifique o envio de dados com a capacidade de enviar diretamente os dados do Formulário adaptável para o Microsoft SharePoint e o Microsoft OneDrive. Você pode enviar dados baseados em esquema e sem esquema. Essas ações de envio são adicionais às ações de envio já disponíveis.
* **[Criação eficiente de formulários com o recurso Salvar um formulário adaptável como modelo](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: Simplifique o processo de criação de formulários, salvando um formulário adaptável como modelo e reutilizando os modelos para o próximo formulário adaptável.
* **[Conectar o AEM Forms a bancos de dados compatíveis com JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: Conecte facilmente seu modelo de dados do AEM Forms a bancos de dados que suportam JDBC, permitindo ler e gravar dados perfeitamente.
* **[Integre com endpoints REST usando a API 3.0 aberta](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: Conecte os Modelos de dados de formulário as a Cloud Service do AEM Forms aos endpoints REST que oferecem suporte à especificação da API aberta versão 3.0, permitindo enviar e receber dados com facilidade.
* **[Compartilhar um formulário adaptável para revisão](/help/forms/create-reviews-forms.md)**: Use o mecanismo de revisão do Adaptive Forms para permitir que um ou mais revisores revisem o formulário.


## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Os autores podem enriquecer dinamicamente listas de produtos com Fragmentos de experiência (por exemplo: colocar banner entre as listas de produtos).
* O componente de lista agora oferece suporte às páginas de produto/categoria associadas para mostrar dinamicamente páginas relacionadas.
* Foi adicionado suporte para componentes do Peregrine 12.5.
* Foi adicionado suporte para o carregamento de preço no lado do cliente no teaser e no carrossel do produto.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* [Ambientes de desenvolvimento rápido](/help/implementing/developing/introduction/rapid-development-environments.md) - Os RDEs permitem que os desenvolvedores solucionem rapidamente os problemas e implantem novos recursos AEM as a Cloud Service.

   Os ambientes de desenvolvimento rápido são um novo tipo de Ambiente de nuvem destinado a uma maneira rápida, consistente e extensível de validar que o código funciona localmente também funciona conforme esperado na nuvem. Usando Ferramentas de Linha de Comando, rapidamente &quot;sincronize&quot; pacotes de conteúdo, pacotes, arquivos de conteúdo, configuração OSGI ou configuração do dispatcher para o RDE. Veja isso em ação no vídeo abaixo:

   >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

   Depois de validar o código com êxito no RDE, é recomendável implantar em um Ambiente de desenvolvimento da nuvem para usar as portas de qualidade do Cloud Manager, antes de implantar por meio de pipeline de produção em ambientes de preparo e produção.

   Cada programa inclui um RDE e, opcionalmente, mais pode ser licenciado.

   >[!NOTE]
   >
   >As RDE serão gradualmente implementadas nas próximas semanas; você pode enviar um email para aemcs-rde-support@adobe.com para pular para a frente da linha.

* [Suporte estendido para tokens de acesso de API do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) - Agora é possível gerar várias credenciais, o que é útil para cenários em que as APIs têm características diferentes. Também agora é possível revogar credenciais de maneira automatizada.

## Notas de versão de manutenção {#maintenance}

Você pode encontrar as notas da versão de manutenção mais recentes [here](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui.](/help/implementing/cloud-manager/release-notes/current.md)

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
