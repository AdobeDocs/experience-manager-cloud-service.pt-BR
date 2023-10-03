---
title: Quais são as diferenças entre o AEM 6.5 Forms e o AEM Cloud Service?
description: Compare o AEM 6.5 Forms e o AEM Cloud Services e saiba mais sobre as mudanças mais importantes antes de atualizar ou migrar para o Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 7e3eb3426002408a90e08bee9c2a8b7a7bfebb61
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 1%

---

# Alterações importantes para usuários existentes do Adobe Experience Manager 6.5 Forms  {#notable-changes-for-existing-AEM-Forms-users}

O Adobe Experience Manager Forms as a Cloud Service traz algumas alterações notáveis para os recursos existentes em comparação com o Adobe Experience Manager Forms no local e [!DNL Adobe-Managed Service] ambientes. As principais diferenças estão listadas abaixo:

## Recursos nativos em nuvem

* O serviço tem uma arquitetura nativa em nuvem que permite o dimensionamento automático com base em carga, tempo de inatividade zero para atualizações, implantação frequente e posterior de novos recursos e atualizações e topologias otimizadas para máxima resiliência e eficiência.

* O serviço não inclui ações de envio que armazenem dados em instâncias do Adobe Experience Manager Cloud Service, tornando-o super seguro. Os dados capturados por meio de formulários são enviados diretamente para os armazenamentos de dados configurados.

* Uma CDN (Content Delivery Network) gratuita também está incluída para ajudar você a fornecer e renderizar formulários em um ritmo mais rápido.


## Atualizações no fluxo de desenvolvimento

* O serviço fornece um SDK para desenvolver e testar o código personalizado em um ambiente local (máquina local) antes de implantar o código em um Cloud Service. Os desenvolvedores desenvolvem e testam componentes personalizados, temas, aplicativos de fluxos de trabalho, configurações, modelos e muito mais usando o SDK em suas máquinas locais. Depois de testar o código personalizado no ambiente de desenvolvimento local, eles implantam o código personalizado em um [Desenvolvimento de ambiente Forms CS ou ambiente de preparo](/help/implementing/cloud-manager/deploy-code.md) para testes adicionais antes de promovê-lo para um ambiente de produção.

* Os desenvolvedores mantêm o código para o Cloud Service e o ambiente de desenvolvimento local em um [repositório Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). Um repositório Git, com base no Arquétipo AEM, é criado automaticamente na criação de um programa as a Cloud Service AEM.

  ![criação automática de repositório git no programa AEM as a cloud service](/help/forms/assets/git-repo-local-and-forms-cs.png)

* O fluxo de desenvolvimento do Forms as a Cloud Service está alinhado ao Arquétipo AEM do AEM Cloud Service. No entanto, há algumas alterações necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com o AEM Cloud Service. Em um alto nível, o AEM requer uma separação de conteúdo e código em subpacotes discretos para respeitar a divisão entre conteúdo mutável e imutável. Use o [Ferramenta Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) reestruturar pacotes de projetos existentes separando o conteúdo e o código em pacotes discretos para serem compatíveis com a estrutura do projeto definida para o Adobe Experience Manager as a Cloud Service.

* Antes de usar seus pacotes de clientes com o Forms as a Cloud Service, recompile seu código personalizado com a versão mais recente do adobe-aemfd-docmanager.

* Uso [Utilitário de migração as a Cloud Service do AEM Forms](/help/forms/migrate-to-forms-as-a-cloud-service.md) para preparar e migrar o Forms adaptável, temas, modelos e configurações de nuvem do <!-- AEM 6.3 Forms--> AEM 6.4 Forms no OSGi e AEM 6.5 Forms no OSGi para [!DNL AEM] as a Cloud Service. Use o [Repositório Git do seu programa](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para importar modelos de Formulário adaptável existentes.

* Por padrão, o email suporta apenas protocolos HTTP e HTTPs. [Contate a equipe de suporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) para permitir que as portas enviem emails e habilitem o protocolo SMTP para o seu ambiente.

## Localização

* A convenção de URL do Adaptive Forms localizado agora permite especificar um local no URL. A nova convenção de URL permite o armazenamento em cache de formulários localizados em um Dispatcher ou CDN. Em um ambiente de Cloud Service, use o formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um Formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* O Adobe recomenda usar o armazenamento em cache do Dispatcher ou CDN. Isso ajuda a melhorar a velocidade de renderização de formulários pré-preenchidos.


## Adaptive Forms

* **Editor de regras:** O AEM Forms as a Cloud Service oferece uma [Editor de regras](rule-editor.md#visual-rule-editor). O editor de código não está disponível no Forms as a Cloud Service.

  A variável [utilitário de migração](/help/forms/migrate-to-forms-as-a-cloud-service.md) O ajuda a migrar os formulários que têm regras personalizadas (criadas no editor de código). O utilitário converte essas regras em funções personalizadas compatíveis com o Forms as a Cloud Service. Você pode usar as funções reutilizáveis com o Editor de regras para continuar obtendo resultados obtidos com scripts de regras. A variável `onSubmitError` ou `onSubmitSuccess` As funções do agora estão disponíveis como ações no Editor de regras.

* **Preencher Serviço:** Por padrão, o serviço de preenchimento prévio mescla dados com um formulário adaptável no cliente em vez de mesclar dados no servidor no AEM 6.5 Forms. O recurso ajuda a melhorar o tempo necessário para preencher previamente um Formulário adaptável. Você sempre pode configurar o para executar a ação de mesclagem no servidor do Adobe Experience Manager Forms.

* **Enviar ações:** A variável **E-mail** ação enviar fornecer opções para enviar anexos e anexar Documento de registro (DoR) com o email. Você pode usá-lo no lugar da variável **Enviar por e-mail como PDF** ação disponível no AEM 6.5 Forms.

* **Serviço Automated forms conversion**: o serviço não fornece um metamodelo para o Automated forms conversion Service. Você pode [baixe-o na documentação do Automated forms conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **Forms adaptável baseado em XSD:** Você pode usar o modelo XDP para projetar um modelo para documento para registro. O serviço não é compatível com o Adaptive Forms baseado em XFA

* **Componentes**: o serviço não oferece suporte à experiência de assinatura no formulário e não inclui os componentes Resumo e Verificar para o Formulário adaptável.

* **Interface do assistente:** Você pode usar o [Interface do assistente](/help/forms/creating-adaptive-form-core-components.md) para configurar rapidamente as opções comuns e criar facilmente um Formulário adaptável.

## Portal do Forms

* O serviço não retém metadados para rascunhos e Forms adaptável enviado.

## Serviços de documento:

O Forms as a Cloud Service fornece APIs RESTful de geração e manipulação de documentos. Você pode usar essas APIs para gerar ou manipular documentos sob demanda ou em lotes, conforme necessário:

* **Serviços de documento: APIs de geração de documento (serviço de saída)**: em uma única chamada de API ou em um lote, você pode usar apenas um modelo com vários arquivos DATA XML. Não há suporte para o uso de vários modelos com vários arquivos de dados em uma única chamada de API.

* **APIs de Manipulação de Documentos (Serviço de Assembler)**:

   * As operações que dependem de serviços de documentos ou aplicativos não estão disponíveis. Por exemplo, Microsoft® Word para PDF, Microsoft® Excel para PDF e HTML para PDF, PostScript (PS) para PDF e XDP para PDF forms não são suportados. Essas operações dependem do Microsoft® Office, Adobe Acrobat, Adobe Distiller, Forms Document Service, respectivamente.

   * Converta documentos que não estejam no formato PDF em um formato PDF antes de usá-los com APIs de Manipulação de documentos de comunicações. Por exemplo, se seus documentos estiverem no formato Microsoft® Office, HTML, PostScript (PS), XDP, converta esses documentos no formato PDF antes de usá-los com documentos PDF. Você pode usar o [ConverterPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) serviço para essas conversões.

   * Você pode usar um ambiente de Forms AEM 6.5 para Assinatura digital, Criptografia, Extensão Reader, Enviar para impressora, Converter PDF e Serviço Forms com código de barras.


## Integração de dados (modelo de dados de formulário)

* O serviço também oferece suporte ao conector JDBC, Microsoft® Dynamics, SalesForce, serviços da Web baseados em SOAP e serviços que oferecem suporte a OData.

* Você também pode conectar o perfil de usuário AEM para recuperar e atualizar as informações do usuário.

* O modelo de dados do Forms é compatível apenas com endpoints HTTP e HTTPS para enviar dados. O serviço não oferece suporte a SSL mútuo para conector REST e autenticação baseada em certificado x509 para fontes de dados SOAP.

* O Forms as a Cloud Service permite usar o Microsoft® Azure Blob, Microsoft® Sharepoint, Microsoft® OneDrive e serviços que oferecem suporte a operações CRUD (Create, Read, Update, and Delete, Criar, Ler, Atualizar e Excluir) gerais como armazenamentos de dados. As especificações Open API 2.0 e Open API 3.0 são compatíveis.


## E-Sign

* O serviço fornece uma integração OOTB com o Adobe Sign e oferece suporte ao DocuSign para assinaturas eletrônicas.

* O serviço também oferece suporte a funções do Adobe Sign. É possível configurar as funções no editor Forms adaptável para usuários empresariais para configurar facilmente workflows de assinatura.


## Formulários HTML5

* Você pode usar um ambiente de Forms AEM 6.5 para:

   * renderize seus formulários baseados em XDP como HTML5 Forms. O serviço não oferece suporte ao HTML5 Forms.

   * capturar dados offline e sincronizá-los na próxima vez que você voltar online com o [Espaço de trabalho AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) aplicativo.

## Comunicações interativas

* Você pode usar APIs de comunicações para produzir documentos personalizados sob demanda ou em lotes no Forms as a Cloud Service. Você pode usar um ambiente de Forms AEM 6.5 para comunicações interativas e casos de uso da interface do agente.

## Ver Próximo

* [Migração de um AEM Forms (ambientes no local e AMS) para o AEM Forms as a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [Adicionar ou criar Forms adaptável à página do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Criar um formulário adaptável (componentes principais)](/help/forms/creating-adaptive-form-core-components.md)

## Informações adicionais

* [Introdução ao AEM Forms as a Cloud Service](/help/forms/home.md)
* [Configurar um ambiente de desenvolvimento local e um projeto de desenvolvimento inicial](/help/forms/setup-local-development-environment.md)
