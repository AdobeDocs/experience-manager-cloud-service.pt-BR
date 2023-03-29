---
title: Diferenças entre AEM 6.5 Forms e AEM Cloud Services
description: Você é um usuário do Experience Manager Forms e deseja atualizar para o Adobe Experience Manager Forms as a Cloud Service? Compare AEM 6.5 Forms e AEM Cloud Services e saiba mais sobre as alterações mais importantes antes de atualizar ou migrar para o Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 54a1ae1cc030030e44612b502b70c9b567144538
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 0%

---

# Alterações importantes para usuários existentes do Adobe Experience Manager 6.5 Forms  {#notable-changes-for-existing-AEM-Forms-users}

O Adobe Experience Manager Forms as a Cloud Service traz algumas alterações notáveis nos recursos existentes, em comparação com o Adobe Experience Manager Forms no local e [!DNL Adobe-Managed Service] ambientes . As principais diferenças estão listadas abaixo:

## Recursos nativos da nuvem

* O serviço tem uma arquitetura nativa em nuvem que permite o dimensionamento automático com base na carga, tempo de inatividade zero para atualizações, frequente e após a implantação de novos recursos e atualizações, e topologias otimizadas para obter o máximo em resiliência e eficiência.

* O serviço não inclui ações de envio que armazenam dados em instâncias do Adobe Experience Manager Cloud Service, tornando-o super seguro. Os dados capturados por meio de formulários são enviados diretamente para armazenamentos de dados configurados.

* Uma CDN gratuita (rede de entrega de conteúdo) também é incluída para ajudar você a fornecer e renderizar formulários a um ritmo mais rápido.


## Atualizações no fluxo de desenvolvimento

* O serviço fornece um SDK para desenvolver e testar código personalizado em um ambiente local (máquina local) antes de implantar o código em um Cloud Service. Os desenvolvedores desenvolvem e testam componentes personalizados, temas, aplicativos de fluxos de trabalho, configurações, modelos e muito mais usando o SDK em suas máquinas locais. Após testar o código personalizado em seu ambiente de desenvolvimento local, ele implanta o código personalizado em um [Ambiente de preparo ou desenvolvimento do Forms CS](/help/implementing/cloud-manager/deploy-code.md) para testes adicionais antes de promovê-lo para um ambiente de produção.

* Os desenvolvedores mantêm o código para o Cloud Service e o ambiente de desenvolvimento local em um [repositório git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). Um repositório Git, baseado AEM Arquétipo, é criado automaticamente na criação de um programa as a Cloud Service AEM.

   ![](/help/forms/assets/git-repo-local-and-forms-cs.png)

* O fluxo de desenvolvimento para o Forms as a Cloud Service se alinha ao Arquétipo de AEM para AEM Cloud Service. No entanto, há algumas alterações necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com o AEM Cloud Service. Em um nível alto, o AEM exige uma separação de conteúdo e código em subpacotes discretos para respeitar a divisão entre conteúdo mutável e imutável. Use o [Ferramenta Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) para reestruturar pacotes de projetos existentes separando o conteúdo e o código em pacotes discretos para serem compatíveis com a estrutura do projeto definida para o Adobe Experience Manager as a Cloud Service.

* Antes de usar seus pacotes de clientes com o Forms as a Cloud Service, recompile seu código personalizado com a versão mais recente do adobe-aemfd-docmanager.

* Use [Utilitário de migração as a Cloud Service AEM Forms](/help/forms/migrate-to-forms-as-a-cloud-service.md) para preparar e migrar suas configurações adaptativas de Forms, temas, modelos e nuvem da <!-- AEM 6.3 Forms--> AEM 6.4 Forms em OSGi e AEM 6.5 Forms em OSGi para [!DNL AEM] as a Cloud Service. Use [Repositório Git do seu programa](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para importar os modelos de formulário adaptável existentes.

* Por padrão, o email oferece suporte somente a protocolos HTTP e HTTPs. [Entre em contato com a equipe de suporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) para habilitar as portas para enviar emails e habilitar o protocolo SMTP para seu ambiente.

## Localização

* A convenção de URL do Adaptive Forms localizado agora é compatível com a especificação de um local no URL. A nova convenção de URL permite o armazenamento em cache de formulários localizados em um Dispatcher ou CDN. Em um ambiente Cloud Service, use o formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* O Adobe recomenda usar o armazenamento em cache do Dispatcher ou CDN. Ajuda a melhorar a velocidade de renderização dos formulários pré-preenchidos.


## Adaptive Forms

* **Editor de regras:** O AEM Forms as a Cloud Service oferece uma [Editor de regras](rule-editor.md#visual-rule-editor). O editor de código não está disponível no Forms as a Cloud Service.

   O [utilitário de migração](/help/forms/migrate-to-forms-as-a-cloud-service.md) O ajuda a migrar os formulários que têm regras personalizadas (criadas no editor de códigos). O utilitário converte essas regras em funções personalizadas compatíveis com o Forms as a Cloud Service. Você pode usar as funções reutilizáveis com o Editor de regras para continuar obtendo resultados obtidos com scripts de regras. O `onSubmitError` ou `onSubmitSuccess` agora estão disponíveis como ações no Editor de regras.

* **Serviço de preenchimento prévio:** Por padrão, o serviço de preenchimento prévio mescla dados com um formulário adaptável no cliente em vez de mesclar dados no servidor no AEM 6.5 Forms. O recurso ajuda a melhorar o tempo necessário para preencher previamente um formulário adaptável. Você sempre pode configurar para executar a ação de mesclagem no Adobe Experience Manager Forms Server.

* **Enviar ações:** O **Email** a ação enviar fornece opções para enviar anexos e anexar Documento de registro (DoR) com email. Você pode usá-lo no lugar da variável **Enviar email como PDF** ação disponível no AEM 6.5 Forms.

* **Serviço Automated forms conversion**: O serviço não fornece metamodelo para o Automated forms conversion Service. Você pode [baixe-o na documentação do Automated forms conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **Forms adaptável baseado em XSD:** Você pode usar o modelo XDP para criar um modelo para Documento para Registro. O serviço não oferece suporte ao Forms adaptável baseado em XFA

* **Componentes**: Você pode usar [Componentes principais adaptáveis do Forms](/help/forms/creating-adaptive-form-core-components.md) para projetar seus formulários. Esses componentes são baseados nos Componentes principais do WCM, seguem os padrões do BEM e podem ser facilmente personalizados. O serviço não oferece suporte à experiência de assinatura no formulário e não inclui os componentes Resumo e Verificação para o formulário adaptável

## Portal do Forms

* Você pode usar os componentes Pesquisar e lister, Rascunhos e Envio e Vincular do Forms Portal para listar formulários para usuários conectados. O suporte para uso anônimo do Forms Portal não está disponível para uso imediato (OOTB). Você pode personalizar o Portal do Forms para permitir a exibição de formulários para usuários não conectados.

* O serviço não retém metadados para rascunhos e Forms adaptável enviado.

## Serviços de documento:

O Forms as a Cloud Service fornece APIs RESTful de Geração de documentos e Manipulação de documentos. Você pode usar essas APIs para gerar ou manipular documentos sob demanda ou em lotes, conforme necessário:

* **Serviços de documento: APIs de geração de documento (Serviço de saída)**: Em uma única chamada de API ou lote, você pode usar apenas um modelo com vários arquivos XML DE DADOS. Não é possível usar vários modelos com vários arquivos de dados em uma única chamada de API.

* **APIs de Manipulação de Documento (Serviço Assembler)**:

   * As operações que dependem de serviços de documento ou aplicativos não estão disponíveis. Por exemplo, Microsoft Word para PDF, Microsoft Excel para PDF e HTML para PDF, PostScript (PS) para PDF, XDP para PDF forms não são compatíveis. Essas operações dependem do Microsoft Office, Adobe Acrobat, Adobe Distiller, Forms Document Service, respectivamente.

   * Converta documentos que estão em um formato não PDF em um formato PDF antes de usar aqueles com APIs de Manipulação de Documento de Comunicações. Por exemplo, se seus documentos estão no Microsoft Office, HTML, PostScript (PS), formato XDP, converta-os no formato PDF antes de usar aqueles com documentos PDF. Você pode usar o [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) para essas conversões.

* Você pode usar um ambiente Forms AEM 6.5 para Assinatura digital, Criptografia, Extensão Reader, Enviar para impressora, Converter PDF e Serviço Forms com código de barras.


## Integração de dados (Modelo de dados de formulário)

* O serviço também oferece suporte para o conector JDBC, Microsoft Dynamics, SalesForce, serviços da Web baseados em SOAP e serviços que oferecem suporte a OData.

* Também é possível conectar AEM perfil do usuário para recuperar e atualizar as informações do usuário.

* O modelo de dados Forms suporta apenas pontos de extremidade HTTP e HTTPS para enviar dados. O serviço não oferece suporte para SSL Mútuo para conector REST e autenticação baseada em certificado x509 para fontes de dados SOAP.

* O Forms as a Cloud Service permite usar o Microsoft Azure Blob, o Microsoft Sharepoint, o Microsoft OneDrive e serviços compatíveis com operações CRUD gerais (Criar, Ler, Atualizar e Excluir) como armazenamentos de dados. As especificações da API aberta 2.0 e da API aberta 3.0 são compatíveis.


## Assinatura eletrônica

* O serviço fornece uma integração OOTB com o Adobe Sign e oferece suporte ao DocuSign para assinaturas eletrônicas.

* O serviço também oferece suporte a funções Adobe Sign. Você pode configurar as funções no editor Adaptive Forms para usuários empresariais a fim de configurar facilmente os fluxos de trabalho de assinatura.


## Formulários HTML5

* Você pode usar um ambiente AEM 6.5 Forms para:

   * renderize seus formulários baseados em XDP como HTML5 Forms. O serviço não é compatível com o HTML5 Forms (Mobile Forms).

   * capturar dados offline e sincronizá-los na próxima vez que você voltar online com [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) aplicativo.

## Comunicações interativas

* Você pode usar as APIs de comunicações para produzir documentos personalizados sob demanda ou em lotes no Forms as a Cloud Service. Você pode usar um ambiente Forms AEM 6.5 para casos de uso de Comunicações interativas e interface do usuário do agente.


