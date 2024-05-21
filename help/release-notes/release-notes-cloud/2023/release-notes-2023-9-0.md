---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.9.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.9.0.
exl-id: d747f58b-8d6c-418d-9d2b-ec3ae4b6dc03
source-git-commit: 02ad83eb9fa9ed3bf06cf7fe0ef10fd9577f66a9
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 21%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2023.9.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2023.9.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2023.9.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 28 de setembro de 2023. O próximo lançamento de recursos (2023.10.0) está planejado para sexta-feira, 26 de outubro de 2023.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de setembro de 2023 que exibe um resumo dos recursos adicionados na versão 2023.9.0:

>[!VIDEO](https://video.tv.adobe.com/v/3424826/?quality=12)

## AEM Edge Delivery Services {#edge-delivery}

O Edge Delivery é um novo conjunto de serviços de composição voltados para maximizar o impacto do conteúdo e gerar resultados mensuráveis para os negócios no ponto de interação com o cliente.

Saiba mais sobre os Edge Delivery Services no artigo [aqui](/help/edge/overview.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na visualização de ativos {#assets-view-features}

**Atribuir formulário de metadados a uma pasta**

Agora você pode atribuir o formulário de metadados a uma pasta específica na implantação. Com isso, todos os ativos contidos nas pastas e subpastas exibem as propriedades definidas no formulário de metadados atribuído.

![Atribuir formulário de metadados a uma pasta](/help/release-notes/assets/assign-to-folder.png)

### Novos recursos na exibição do Administrador {#admin-view-features}

* **Integrar o AEM Assets as a Cloud Service com a criação baseada em documentos para Edge Delivery Services**: integre o AEM Assets à Criação baseada em documentos para que o Edge Delivery Services permita que os autores de sites [usar imagens disponíveis em repositórios do AEM Assets ao criar documentos no Microsoft Word ou Google Docs](/help/edge/using.md#integrate-assets-edge).

* **Extrair arquivos ZIP**: Capacidade de selecionar arquivos ZIP gerenciados no Experience Manager e [extração de arquivos diretamente no Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) sem baixá-los.

  ![Fixação de itens para grupos](/help/release-notes/assets/extract-archive.png)

### Recursos de pré-lançamento disponíveis em [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Suporte a várias legendas e trilhas de áudio para vídeos no Dynamic Media](/help/assets/dynamic-media/video.md#about-msma)—Agora é possível adicionar facilmente várias legendas e faixas de áudio a um vídeo principal. Esse recurso significa que os vídeos estão acessíveis em um público-alvo global. Você pode personalizar um único vídeo principal publicado para um público-alvo global em vários idiomas e seguir as diretrizes de acessibilidade para diferentes regiões geográficas. Os autores também podem gerenciar as legendas e faixas de áudio em uma única guia na interface do usuário do.

  ![Guia Legendas e faixas de áudio na página Propriedades de um ativo de vídeo selecionado.](/help/release-notes/assets/msma-aem-cs.png)*Guia Legendas e faixas de áudio na página Propriedades de um ativo de vídeo selecionado.*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no [!DNL Experience Manager Forms] {#forms-features}

* [**Suporte corporativo ao Google reCAPTCHA**](/help/forms/captcha-adaptive-forms-core-components.md): use o Google reCAPTCHA Enterprise em um formulário adaptável para fornecer proteção aprimorada contra atividades fraudulentas e spam, proporcionando uma experiência mais segura ao usuário. Com a análise de risco avançada e a integração perfeita, os usuários genuínos podem enviar formulários facilmente, enquanto os bots são bloqueados de maneira eficaz.

* [**Adobe Analytics com automação de configuração do Experience Cloud para Forms**](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md): Agora você pode ativar o Adobe Analytics com a Automação de configuração do Experience Cloud girando alguns botões. Ele permite conectar o AEM Forms as a Cloud Service com tags Experience Platform e o Adobe Analytics para capturar e rastrear métricas de desempenho para seus formulários publicados.

  >[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)

* [**Modelo de relatório do Adobe Analytics para o Adaptive Forms**](/help/forms/view-understand-aem-forms-analytics-reports.md): o Forms as a Cloud Service agora fornece um relatório do Adobe Analytics OOTB. Ele ajuda você a entender facilmente o desempenho de seus formulários. As métricas no nível do formulário fornecem um insight sobre o desempenho do formulário em vários indicadores principais de desempenho (KPIs), como representações, visitantes, envios e tempo médio de preenchimento. Ao rastrear o comportamento do usuário e o feedback, você pode identificar áreas do formulário que estão causando confusão e orientar melhorias no design e na funcionalidade do formulário.

  ![Relatório de engajamento do usuário no formulário adaptável do adobe analytics](/help/forms/assets/forms-analytics-report.png)

* **[Fragmento de formulário no Forms adaptável com base nos Componentes principais](/help/forms/adaptive-form-fragments-core-components.md)**: diga adeus à duplicação, otimize seu inventário digital e melhore a colaboração à medida que você eleva sua experiência de criação de formulários com Fragmentos de formulário. Esses componentes reutilizáveis se integram perfeitamente em vários formulários, simplificando a criação de formulários consistentes e com aparência profissional. Os fragmentos de formulário garantem a reutilização, a padronização e a consistência da marca por meio da funcionalidade &quot;alterar uma vez e refletir em todos os lugares&quot;. Experimente maior capacidade de manutenção e eficiência, já que as atualizações feitas em um local são propagadas automaticamente em todos os formulários que utilizam esses fragmentos.

* **[Etapa de fluxo de trabalho aprimorada do Adobe Sign](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: a etapa Fluxo de trabalho do Adobe Sign foi aprimorada para incluir o seguinte:
   * **Autenticação com base em ID do governo para o Adobe Sign**: a autenticação baseada em ID do governo da Adobe Acrobat Sign oferece uma camada adicional de verificação, permitindo que os usuários autentiquem sua identidade usando IDs emitidas pelo governo (CNH, identificação nacional, passaporte). Ao usar documentos de identificação confiáveis, esse aprimoramento adiciona um nível extra de confiança ao processo de assinatura, tornando-o ideal para cenários que exigem maior segurança, conformidade e validação do usuário.

   * **Trilha de auditoria para documentos do Adobe Sign**: use o recurso Trilha de auditoria para obter insights detalhados sobre o ciclo de vida dos documentos do Adobe Sign. Com a Trilha de auditoria, agora é possível manter um registro abrangente de todas as ações e interações relacionadas aos documentos. Isso inclui detalhes como quem visualizou, editou ou assinou o documento, além de carimbos de data e hora para cada evento. Esse aprimoramento é fundamental para manter a conformidade, resolver disputas e garantir a integridade de seus contratos digitais.

   * **Novas funções para destinatários do Contrato além do Signatário**: a Adobe Acrobat Sign tem a opção de expandir as funções dos recipients do Contrato além apenas do Signatário para melhor corresponder aos requisitos de fluxo de trabalho. Quando habilitado, cada recipient em um Contrato tem sua função configurável individualmente, sendo que Signatário é o padrão.

* **Suporte à contagem de páginas em APIs de comunicação**: Agora, juntamente com a recuperação do documento por meio das APIs de comunicação, você também pode receber as informações valiosas sobre o número de páginas contidas no documento.

* **[Tratamento de erros com manipuladores de erros personalizados no editor de regras](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: agora você pode chamar uma função personalizada em resposta a um erro retornado por um serviço externo e fornecer uma resposta personalizada para os usuários finais. Por exemplo, você pode acionar um fluxo de trabalho personalizado no back-end para códigos de erro específicos ou informar ao cliente que o serviço está inativo.

* **[Versão de 64 bits do AEM Forms Designer](/help/forms/installing-configuring-designer.md)**: A versão de 64 bits do AEM Forms Designer oferece desempenho, escalabilidade e gerenciamento de memória aprimorados para potencializar a experiência de criação de formulários. Com a arquitetura de 64 bits, você pode executar projetos ainda maiores e mais complexos com facilidade, garantindo fluxos de trabalho de design ininterruptos e eficiência otimizada. Aumente os recursos de design de formulário e abrace o futuro do AEM Forms Designer com esta versão de última geração.

### Programa de adoção antecipada {#forms-early-adopter}

* **[Protect seus documentos com as APIs DocAssurance (Parte das APIs de comunicação)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: As APIs do DocAssurance permitem proteger informações confidenciais, assinando e criptografando os documentos. Por meio da criptografia, o conteúdo de um documento é transformado em um formato ilegível, garantindo que somente usuários autorizados possam ter acesso. Essa camada fortificada de proteção não apenas protege dados valiosos de olhos não autorizados, mas também proporciona tranquilidade. As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos.

  Você pode escrever para `aem-forms-ea@adobe.com` do seu id de email oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso.

* **[Forms adaptável headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=pt-BR)**: use o Headless Adaptive Forms para permitir que os desenvolvedores criem, publiquem e gerenciem formulários interativos que podem ser acessados e interagidos por meio de APIs, em vez de uma interface gráfica tradicional. Os formulários adaptáveis headless ajudam a:

   * criar formulários multicanal de alta qualidade na linguagem de programação de sua escolha
   * integrar formulários nativamente a seus aplicativos móveis e de desktop, sites e aplicativos de bate-papo
   * reutilizar os componentes de interface de sua propriedade com aplicativos de formulários
   * aproveitar o potencial do Adobe Experience Manager Forms

  Você pode enviar um email para `aem-forms-headless@adobe.com` utilizando sua ID de email oficial para participar do programa de adoção antecipada.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novo comportamento do armazenamento em cache do CDN para parâmetros de URL relacionados à campanha {#cache-url-params}

Para novos ambientes, a CDN removerá os parâmetros de consulta relacionados a marketing por padrão para aumentar o desempenho da campanha de marketing e as taxas de ocorrência do cache. Os ambientes existentes não são afetados. [Saiba mais.](/help/implementing/dispatcher/caching.md#marketing-parameters)

### Regras de filtro de tráfego (incluindo regras do WAF) do programa de adoção antecipada {#waf-early-adopter}

Filtrar o tráfego na CDN com base em:

* cabeçalhos e propriedades de solicitação (por exemplo, endereço IP)
* padrões de tráfego conhecidos por estarem associados a tráfego mal-intencionado

Interessado em experimentar o recurso e compartilhar feedback? Enviar um email para **aemcs-waf-adopter@adobe.com** da sua ID de e-mail oficial para saber mais sobre o programa dos participantes antecipados. O espaço é limitado.

Saiba mais sobre o recurso no artigo [aqui](/help/security/traffic-filter-rules-including-waf.md).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
