---
title: "[!DNL AEM Forms] Notas de versão as a Cloud Service"
description: "[!DNL AEM Forms] Notas de versão as a Cloud Service"
exl-id: 35950b81-6e45-4a75-bd27-8c28fd68e42e
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '2024'
ht-degree: 19%

---


# [!DNL Experience Manager Forms] Nota de versão as a Cloud Service {#overview}

Adobe Experience Manager [!DNL AEM Forms] A as a Cloud Service recebe melhorias continuamente. Para se manter atualizado com os desenvolvimentos mais recentes, visite esta página regularmente. Esta página fornece informações sobre:

- Novos recursos
- Melhorias
- Recursos de pré-lançamento
- Recursos beta
- Correções de erros
- Funcionalidade obsoleta
- Instruções especiais
- Futuros planos de alterações

>[!NOTE]
>
>Para obter as notas de versão de todos os outros componentes AEM versão as a Cloud Service, consulte [Notas de versão atuais](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

## 2021.10.0 {#sep-2021-10-0}

### Novidades do [!DNL Forms] {#what-is-new-forms-oct-2021}

- **Analytics para Adaptive Forms**: Agora é possível capturar e rastrear o comportamento de logon e não conectado (Anônimo) pelo Adobe Analytics para Adaptive Forms para coletar insights do usuário final. Ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário final.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms-oct-2021}

- **Externalizar dados do fluxo de trabalho do AEM para processamento seguro**: Você pode armazenar dados de fluxos de trabalho em andamento do AEM (dados de variáveis de fluxo de trabalho do AEM) que contêm elementos de Dados pessoais sensíveis (SPD) em um repositório gerenciado pelo cliente para processamento seguro. Os elementos de dados e as variáveis de fluxo de trabalho não são armazenados no repositório do AEM e são buscados sob demanda de um repositório gerenciado pelo cliente durante o processamento do fluxo de trabalho.

### Recursos beta de [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](aem-forms-cloud-service-communications.md) ajudam a combinar um modelo e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modos síncronos e em lote. As APIs permitem criar aplicativos que possibilitam a você:

   - Gerar documentos preenchendo arquivos de modelo (PDF e XDP) com dados XML.
   - Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.

Você pode escrever para [!DNL formscsbeta@adobe.com] para se inscrever no programa beta.

## 2021.9.0 {#sep-2021-09-0}

### Novidades do [!DNL Forms] {#what-is-new-forms-sep-2021}

- **Usar as funções do Adobe Sign em um formulário adaptável**: Os níveis de serviço Adobe Sign for business and enterprise têm a opção de expandir as funções para os recipients do Agreement, além apenas do Signer, para melhor corresponder aos seus requisitos de fluxo de trabalho. Agora você pode [permitir que cada recipient do contrato configure sua função em um formulário adaptável](working-with-adobe-sign.md#addsignerstoanadaptiveform), com o Signer sendo a função padrão.

- **Analytics para Adaptive Forms**: Agora você pode capturar e [rastrear o comportamento do usuário final via Adobe Analytics](integrate-aem-forms-with-adobe-analytics.md) para Adaptive Forms para coletar insights do usuário final. Ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário final.

- **Conecte facilmente o AEM Forms com o Microsoft Dynamics e o Salesforce**: O serviço fornece configuração de fonte de dados e modelos de dados prontos para uso para o Microsoft Dynamics e Salesforce, tornando-o [mais rápido e mais fácil para os desenvolvedores configurar o Microsoft Dynamics e o Salesforce como fontes de dados para um formulário adaptável](configure-msdynamics-salesforce.md).

- **Assinar um formulário adaptável por meio do DocuSign:** [Você pode usar o DocuSign para assinar automaticamente um formulário adaptável](integrate-docusign-adaptive-forms.md). O serviço fornece uma ação de envio personalizada para usar o DocuSign com um formulário adaptável.

### Recursos beta de [!DNL Forms] {#sep-what-is-new-forms-prerelease}

- **Conector de armazenamento unificado:** Use o Unified Storage Connector para externalizar dados em andamento em repositórios gerenciados pelo cliente. Por exemplo, você pode armazenar dados em andamento AEM Workflows (AEM dados de Variáveis de Fluxo de Trabalho) que contêm Dados Pessoais Sensíveis (SPD) em um repositório gerenciado pelo cliente.

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](aem-forms-cloud-service-communications.md) Ajudar a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modo síncrono. As APIs permitem criar aplicativos que possibilitam a você:
   - Gerar documentos preenchendo arquivos de modelo com dados XML.
   - Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
   - Gere arquivos PDF de impressão a partir de um PDF de formulário XFA e do Formulário Adobe Acrobat.

Você pode escrever para [!DNL formscsbeta@adobe.com] para se inscrever no programa beta.

### Limitações           {#limitations}

- O Adobe Analytics pode rastrear métricas de formulário somente para usuários autenticados.

<!--

### New features available in [!DNL Forms] prerelease channel {#prerelease-features-forms-sep-2021}

* **Forms Portal:**  In a typical forms-centric portal deployment scenario, forms development and portal development are two disjoint activities. While Form Designers design and store forms in a repository, Web Developers create a web application to list forms and handle submission of forms. Forms are copied over to the web tier as there is no communication between the forms repository and the web application.

  Such scenarios often result in management issues and production delays. For example, if there is a newer version of a form available in the repository, you need to replace the form on the web tier, modify the web application, and redeploy the form on the public site. Redeploying the web application might cause some server downtime. Typically, the server downtime is a planned activity and therefore the changes cannot be pushed to the public site instantaneously.

  AEM Forms provides portal components that reduce management overheads and production delays. The components equip Web Developers to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM). The form portal components allow you to add the following functionality:

  * List forms in customized layouts. Out of the box, List view and Card view are provided.

  * List published adaptive forms on an AEM Sites page.

  * Enable searching of forms based on a various criteria, such as form properties, metadata, and tags.

  * Lists drafts and submissions related to Adaptive Form created by end user.

  -->

## 2021.8.0 {#aug-2021-08-0}

### Novidades do [!DNL Forms] {#what-is-new-forms-aug-2021}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

- AEM projeto do Arquétipo para o Forms as a Cloud Service agora inclui [modelos de dados de formulário para o Microsoft Dynamics e Salesforce](setup-local-development-environment.md).

- **Documento de registro baseado em formulário**: O AEM Forms as a Cloud Service oferece suporte ao uso do [Adobe Acrobat Form PDF (Acroform PDF)](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) como um modelo para o Documento de registro além do modelo de formulário baseado em XFA.

- **Conector do armazenamento de dados do Microsoft Azure**: Agora você pode [conectar o Modelo de Dados de Formulário ao Armazenamento do Microsoft Azure](configure-azure-storage.md). Ele permite recuperar e armazenar dados de formulário adaptáveis para o Microsoft Azure Storage como um BLOB.

### Recurso beta de [!DNL Forms] {#aug-what-is-new-forms-prerelease}

- **Conector de armazenamento unificado:** Use o Unified Storage Connector para externalizar dados em andamento em repositórios gerenciados pelo cliente. Por exemplo, você pode

   - Habilite a funcionalidade de salvar e retomar do Forms Portal e armazene rascunhos de formulários adaptáveis em um repositório de dados gerenciado pelo cliente.
   - Armazene dados de fluxos de trabalho AEM em andamento (dados AEM variáveis de fluxo de trabalho) que contêm dados confidenciais pessoais (SPD) em um repositório gerenciado pelo cliente.

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](aem-forms-cloud-service-communications.md) Ajudar a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modo síncrono. As APIs permitem criar aplicativos que possibilitam a você:
   - Gerar documentos preenchendo arquivos de modelo com dados XML.
   - Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
   - Gere arquivos PDF de impressão a partir de um PDF de formulário XFA e do Formulário Adobe Acrobat.

Você pode escrever para [!DNL formscsbeta@adobe.com] para se inscrever no programa beta.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms-aug-2021}

- **Usar as funções do Adobe Sign em um formulário adaptável**: Os níveis de serviço Adobe Sign for business and enterprise têm a opção de expandir as funções para os recipients do Agreement, além apenas do Signer, para melhor corresponder aos seus requisitos de fluxo de trabalho. Agora você pode [permitir que cada recipient do contrato configure sua função em um formulário adaptável](working-with-adobe-sign.md#addsignerstoanadaptiveform), com o Signer sendo a função padrão.

- **Analytics para Adaptive Forms**: Agora é possível capturar e rastrear o comportamento do usuário final por meio do Adobe Analytics para o Adaptive Forms para coletar insights do usuário final. Ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário final.

- **Conecte facilmente o AEM Forms com o Microsoft Dynamics e o Salesforce**: O serviço fornece configuração de fonte de dados e modelos de dados prontos para uso para o Microsoft Dynamics e Salesforce, tornando-o [mais rápido e mais fácil para os desenvolvedores configurar o Microsoft Dynamics e o Salesforce como fontes de dados para um formulário adaptável](configure-msdynamics-salesforce.md).

## 2021.7.0 {#july-2021-07-0}

### Novidades do [!DNL Forms] {#july-what-is-new-forms}

- Agora você pode usar o serviço Automated forms conversion para [converter PDF forms em francês, alemão e espanhol](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) para formulários adaptáveis.
- Adição de um painel separado ao editor de modelo para exibir erros relacionados aos componentes de formulário adaptáveis. Ele ajuda a consolidar todos os erros de formulário adaptável em um local e a reduzir o tempo de resolução.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#july-prerelease-features-forms}

- **Documento de registro baseado em formulário**: Você também pode [usar o Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) como um modelo para o Documento de registro além do modelo de formulário baseado em XFA.

- **Conector do armazenamento de dados do Microsoft Azure**: Agora você pode [conectar o Modelo de Dados de Formulário ao Armazenamento do Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Ele permite recuperar e armazenar dados de formulário adaptáveis para o Microsoft Azure Storage como um BLOB.

- **Externalizador de dados de variáveis**: Você pode salvar dados de variáveis de Fluxo de trabalho AEM em um sistema de armazenamento externo gerenciado por sua organização.

### Recurso beta de [!DNL Forms] {#july-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](aem-forms-cloud-service-communications.md) Ajudar a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modo síncrono. As APIs permitem criar aplicativos que possibilitam a você:
   - Gerar documentos preenchendo arquivos de modelo com dados XML.
   - Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
   - Gere arquivos PDF de impressão a partir de um PDF de formulário XFA e do Formulário Adobe Acrobat.

## 2021.6.0 {#july-2021-06-0}

### Novidades do [!DNL Forms] {#june-what-is-new-forms}

- Adição da capacidade de filtrar colunas personalizadas AEM Caixa de entrada.
- Adição da capacidade de usar o editor de temas e a camada de estilo do editor de formulário adaptável para criar estilo no componente captcha.
- Melhoria na velocidade e precisão para detectar automaticamente seções lógicas nos PDF forms de origem e convertê-las em painéis de formulário adaptáveis correspondentes.
- Adição da ação de mover para mover um arquivo PDF ou XDP de uma pasta para outra.

### Recurso beta de [!DNL Forms] {#june-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: As APIs de comunicação ajudam a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modo síncrono. As APIs permitem criar aplicativos que possibilitam a você:

   - Gere documentos de formulário finais preenchendo arquivos de modelo com dados XML.
   - Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
   - Gere PDF de impressão a partir de um PDF de formulário XFA e Formulário Adobe Acrobat (AcroForm).

- **Externalizador de dados de variáveis**: Você pode salvar dados de variáveis de Fluxo de trabalho AEM em um sistema de armazenamento externo gerenciado por sua organização.

Você pode escrever para [!DNL formscsbeta@adobe.com] para se inscrever no programa beta.

### Erros corrigidos em [!DNL Forms] {#june-forms-bugs-fixed}

- Quando um campo é validado antes de enviar dados para o serviço de backend por meio do FDM (Form Data Model), as validações são bem-sucedidas, mas o serviço do Modelo de dados de formulário não consegue invocar a validação posterior.
- Às vezes, ao enviar um formulário contendo um campo de carregamento HTML padrão de um dispositivo Apple iOS, o conteúdo do arquivo não é enviado e um arquivo de 0 bytes é recebido na outra extremidade. O Apple iOS 15.1 fornece uma correção para o problema.

## 2021.5.0 {#may-2021-05-0}

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#may-what-is-new-forms}

- **Ajuda contextual**: Adição de ajuda contextual para o editor de formulários adaptáveis, editor de modelos e editor de temas para ajudar os autores a entender melhor vários recursos dos editores.
- **Mensagens de erro no navegador Propriedades**: Adicionadas mensagens de erro para cada propriedade no navegador Adaptive Forms Properties. Essas mensagens ajudam a entender os valores permitidos para um campo.

### Futuro recurso beta de [!DNL Forms] {#may-what-is-new-forms-prerelease}

Saída como um serviço da nuvem: O serviço de saída ajuda a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos no modo de lote síncrono e assíncrono. O serviço de saída permite criar aplicativos que permitem:

- Gere documentos de formulário finais preenchendo arquivos de modelo com dados XML.
- Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
- Gerar PDFs de impressão a partir de PDFs de formulário XFA.

Você pode gravar em formscsbeta@adobe.com para se inscrever no programa beta.

### Erros corrigidos em [!DNL Forms] {#may-forms-bugs-fixed}

- Em uma etapa Atribuir tarefa dos fluxos de trabalho do AEM Forms, ao substituir o ícone padrão dos botões de ação por um ícone de coral, o fluxo de trabalho para de funcionar e registra uma exceção. O fluxo de trabalho é executado conforme esperado quando os ícones padrão são usados.
- Na camada de layout, ao alterar o número de colunas, abrir a camada de edição e arrastar alguns componentes em um painel, caixas azuis quadradas começam a aparecer na área de conteúdo do editor de formulários adaptáveis e o editor fica sem resposta.
- A mensagem de erro de uma opção do editor de regras relacionada ao fornecimento de URL de um ativo adaptável ou externo é muito longa e não é amigável para o usuário.

## 2021.4.0 {#april-2021-04-0}

### Novidades do [!DNL Forms] {#april-what-is-new-forms}

- **Usar o método de autenticação de identidade do Governo no Adobe Sign Adaptive Forms habilitado**

   Alimentado por algoritmos avançados de aprendizado de máquina, o processo de ID do governo da Adobe Sign capacita empresas em todo o mundo com a capacidade de garantir uma autenticação de alta qualidade da identidade do destinatário. Agora, você pode usar o método de autenticação de identidade do Governo no Adobe Sign Adaptive Forms habilitado.

   ID do governo é um método de autenticação de identidade premium que instrui o recipient a [Fazer upload da imagem de um documento de identidade emitido pelo Estado (carta de condução, identificação nacional, passaporte)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)e, em seguida, avalia esse documento para certificar-se de que ele é autêntico.

- **Suporte para usar a experiência de assinatura no formulário para envios assíncronos de formulários adaptáveis**

   Agora é possível usar a experiência de assinatura no formulário para envios assíncronos de formulários adaptáveis. Também é possível incorporar um formulário adaptável em um [!DNL Experience Manager Sites] e use a experiência de assinatura no formulário para enviar formulários adaptáveis.

- **Suporte para usar uma variável para especificar um anexo ao preencher previamente um Formulário adaptável para uma etapa Atribuir tarefa**

   Ao pré-preencher um formulário adaptável para uma etapa Atribuir tarefa , agora é possível usar uma variável do tipo de documento para selecionar um anexo de entrada para o formulário adaptável.

- **Suporte para usar a opção literal para definir valor para uma variável do tipo JSON**

   Você pode usar a opção literal para definir um valor para uma variável do tipo JSON na etapa Definir variável de um fluxo de trabalho AEM. A opção literal permite especificar um JSON no formato de uma string.

- **Usar o ambiente de desenvolvimento local para criar Documento de registro (DoR)**

   Você pode usar um XDP como modelo de Documento de registro em instâncias do Cloud Service e no SDK as a Cloud Service do AEM Forms (ambiente de desenvolvimento local). Anteriormente, o suporte estava limitado apenas a instâncias Cloud Service.

### Correções de erros no [!DNL Forms] {#april-bug-fixes-forms}

- Quando um Formulário adaptável configurado para não gerar Documento de registro é enviado a um Fluxo de trabalho AEM configurado para gerar Documento de registro, nenhuma mensagem de erro é exibida e a tarefa não é enviada.
