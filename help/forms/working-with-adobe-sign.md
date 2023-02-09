---
title: Como utilizar [!DNL Adobe Sign] em um formulário adaptável?
description: Você pode ativar a assinatura eletrônica ([!DNL Adobe Sign]) fluxos de trabalho para um formulário adaptável para automatizar fluxos de trabalho de assinatura, simplificar processos de assinatura única e múltipla e assinar eletronicamente formulários de dispositivos móveis.
topic-tags: develop
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: cde9523e-5409-4edd-af0f-2c2575cc22ea
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '3072'
ht-degree: 0%

---


# Usando [!DNL Adobe Sign] em um formulário adaptável {#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] habilita fluxos de trabalho de assinatura eletrônica para o Adaptive Forms. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e outras.

Em um [!DNL Adobe Sign] e Adaptive Forms , um usuário preenche um Formulário adaptável para se candidatar a um serviço que requer assinaturas de uma ou mais partes. Por exemplo, um pedido de hipoteca e de cartão de crédito requer assinaturas legais de todos os mutuários e co-requerentes. Para ativar workflows de assinatura eletrônica para cenários semelhantes, é possível integrar [!DNL Adobe Sign] com um formulário adaptável. Mais alguns exemplos são: você pode usar [!DNL Adobe Sign] para:

* Feche negócios de qualquer dispositivo com processos de proposta, cotação e contrato totalmente automatizados.
* Termine os processos de recurso humano mais rapidamente e dê aos seus funcionários as experiências digitais.
* Reduza mais rapidamente os tempos de ciclo do contrato e integre seus fornecedores.
* Crie workflows digitais que automatizam processos comuns.

[!DNL Adobe Sign] integração com [!DNL AEM Forms] suporta:

* Fluxos de trabalho de assinatura de um e vários usuários
* Fluxos de trabalho de assinatura sequenciais e simultâneos
* Assinar formulários como um usuário anônimo ou conectado
* Processos de assinatura dinâmica (integração com [!DNL AEM Forms] Fluxo de trabalho)
* Autenticação por meio de uma base de conhecimento, telefone, perfis sociais e ID do governo
* Atribua funções a cada recipient de contrato. Os níveis de serviço da Adobe Sign para empresas e empresas têm a opção de expandir o [funções para recipients do contrato](#addsignerstoanadaptiveform).

<!-- * In-form and out-of-form signing experiences -->

## Pré-requisitos {#prerequisites}

Antes de usar [!DNL Adobe Sign] em um formulário adaptável:

* Certifique-se de que [!DNL AEM Forms] as a Cloud Service está configurado para usar o Adobe Sign. Para obter detalhes, consulte [Integrar o Adobe Sign com o [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
* Mantenha a lista de recipients pronta. Você precisa de pelo menos um endereço de email para cada recipient.

## Configurar [!DNL Adobe Sign] para um formulário adaptável {#configure-adobe-sign-for-an-adaptive-form}

Para configurar [!DNL Adobe Sign] para um formulário adaptável:

1. [Habilitar [!DNL Adobe Sign] para um formulário adaptável](#enableadobsignforanadaptiveform)
1. [Adicionar [!DNL Adobe Sign] campos em um formulário adaptável](#addadobesignfieldstoanadaptiveform)
1. [Selecionar [!DNL Adobe Sign] Cloud Service para um formulário adaptável](#select-adobe-sign-cloud-service-and-signing-order)

1. [Adicionar [!DNL Adobe Sign] recipient para um formulário adaptável](#addsignerstoanadaptiveform)
1. [Selecione Enviar ação para um formulário adaptável](#selectsubmitactionforanadaptiveform)

![Detalhes do destinatário](assets/signer_details_new.png)

### Habilitar [!DNL Adobe Sign] para um formulário adaptável  {#enableadobesign}

Você pode ativar [!DNL Adobe Sign] para um formulário adaptável existente ou criar um [!DNL Adobe Sign] formulário adaptável habilitado. Escolha uma das opções a seguir:

* [Crie um [!DNL Adobe Sign] formulário adaptável ativado](#create-an-adaptive-form-for-adobe-sign)
* [Habilitar [!DNL Adobe Sign] para um formulário adaptável existente](#editafsign).

#### Criar um formulário adaptável para o Adobe Sign {#create-an-adaptive-form-for-adobe-sign}

Para criar um formulário adaptável habilitado para assinatura:

1. Navegar para **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Toque **[!UICONTROL Criar]** e selecione **[!UICONTROL Formulário adaptável]**. Uma lista de modelos é exibida. Selecione um modelo e toque em **[!UICONTROL Próximo]**.
1. No **[!UICONTROL Básico]** guia :

   1. Especifique a **[!UICONTROL Nome]** e **[!UICONTROL Título]** para o formulário adaptável.

   1. Selecione o [contêiner de configuração](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) criado ao [integração [!DNL Adobe Sign] com [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
   O contêiner de configuração contém a variável [!DNL Adobe Sign] Cloud Services configurados para o seu ambiente. Esses serviços estão disponíveis para seleção no editor de formulário adaptável.

1. No **[!UICONTROL Modelo de formulário]** selecione uma das seguintes opções:

   * Se você tiver um modelo de formulário personalizado e exigir um Documento de registro com base no modelo de formulário, selecione o **[!UICONTROL Associar modelo de formulário como o modelo Documento de registro]** e selecione um modelo Document of Record . Ao usar a opção , os documentos enviados para assinatura exibem apenas os campos que se baseiam no modelo de formulário associado. Não exibe todos os campos do Formulário adaptável.

   * Se não tiver um modelo de formulário personalizado, selecione **[!UICONTROL Gerar Documento de Registro]** opção. Quando você usa a opção , o documento enviado para assinatura exibe todos os campos do Formulário adaptável.

1. Toque **[!UICONTROL Criar.]** É criado um formulário adaptável habilitado para assinatura. Você pode adicionar [!DNL Adobe Sign] campos para o formulário e enviá-lo para assinatura.

#### Habilitar [!DNL Adobe Sign] para um formulário adaptável {#editafsign}

Para usar [!DNL Adobe Sign] em um formulário adaptável existente:

1. Navegar para **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Selecione o formulário adaptável e toque em **[!UICONTROL Propriedades]**.
1. No **[!UICONTROL Básico]** selecione a guia [contêiner de configuração](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) criado ao integrar [!DNL Adobe Sign] com [!DNL AEM Forms].
1. No **[!UICONTROL Modo de formulário]** selecione uma das seguintes opções:

   * Se você tiver um modelo de formulário personalizado e exigir um Documento de registro com base no modelo de formulário, selecione o **[!UICONTROL Associar modelo de formulário como o modelo Documento de registro]** e selecione um modelo Document of Record . Ao usar a opção , os documentos enviados para assinatura exibem apenas os campos que se baseiam no modelo de formulário associado. Não exibe todos os campos do Formulário adaptável.

   * Se não tiver um modelo de formulário personalizado, selecione **[!UICONTROL Gerar Documento de Registro]** opção. Quando você usa a opção , o documento enviado para assinatura exibe todos os campos do Formulário adaptável.

1. Toque **[!UICONTROL Salvar e fechar]**. O formulário adaptável está ativado para [!DNL Adobe Sign]. Agora, você pode adicionar seu [!DNL Adobe Sign] campos para o formulário e enviá-lo para assinatura.

### Adicionar [!DNL Adobe Sign] campos em um formulário adaptável {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] O tem vários campos que podem ser colocados em um formulário adaptável. Esses campos aceitam vários tipos de dados, como assinaturas, iniciais, empresa ou título, e ajudam a coletar informações adicionais durante a assinatura, juntamente com as assinaturas. Você pode usar o [!DNL Adobe Sign] Bloquear componente a ser posicionado [!DNL Adobe Sign] campos em vários locais em um formulário adaptável.

Para adicionar campos a um Formulário adaptável e personalizar várias opções relacionadas a esses campos:

1. Arrastar e soltar **[!UICONTROL Bloco Adobe Sign]** do navegador de componentes para o Formulário adaptável. O [!DNL Adobe Sign] O componente Bloqueio tem todos os [!DNL Adobe Sign] campos. Por padrão, ele adiciona uma **[!UICONTROL Assinatura]** para o formulário adaptável.

   ![Bloco de assinatura](assets/sign_block_new.png)

   Por padrão, a variável [!DNL Adobe Sign] O bloco não está visível no Formulário adaptável publicado. Ela é visível somente nos documentos de assinatura. Você pode alterar a visibilidade de [!DNL Adobe Sign] Bloquear nas propriedades da [!DNL Adobe Sign] Bloquear componente.

   >[!NOTE]
   >
   >  * Usando [!DNL Adobe Sign] o bloco não é obrigatório para usar [!DNL Adobe Sign] em um formulário adaptável. Se não utilizar [!DNL Adobe Sign] bloqueie e adicione campos para os recipients, então o campo de assinatura padrão é exibido na parte inferior dos documentos de assinatura.
   >  * Use [!DNL Adobe Sign] bloquear somente para o Adaptive Forms que gera automaticamente o Documento de registro. Se estiver usando um XDP personalizado para gerar o Documento de registro ou um formulário baseado no Formulário adaptável, [!DNL Adobe Sign] não há suporte para bloqueio.



1. Selecione o **[!UICONTROL Bloco Adobe Sign]** e toque no **[!UICONTROL Editar]** ![Editar](assets/Smock_Edit_18_N.svg) ícone . Ele exibe opções para adicionar campos e formatar a aparência de um campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Selecionar e adicionar [!DNL Adobe Sign] campos. **B.** Expanda o [!DNL Adobe Sign] bloquear para exibição em tela cheia

1. Toque no **[!UICONTROL Adobe Sign]** Campo ![Adobe Sign](assets/adobesign.png) ícone . Ele exibe opções para selecionar e adicionar [!DNL Adobe Sign] campos.

   Expanda o **[!UICONTROL Tipo]** campo suspenso para selecionar uma [!DNL Adobe Sign] e toque em Concluído ![Salvar](assets/save_icon.svg) ícone para adicionar o campo selecionado ao [!DNL Adobe Sign] bloco. O **[!UICONTROL Tipo]** O campo suspenso inclui os tipos de campos Assinatura, Informações do destinatário e Dados . [!DNL Adobe Sign] integração com AEM [!DNL Forms] campos de suporte listados no [!UICONTROL Tipo] somente caixa suspensa. Para obter informações detalhadas sobre [!DNL Adobe Sign] campos, consulte [Documentação do Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   É obrigatório fornecer um nome exclusivo para um campo. Também é possível selecionar a opção obrigatória para marcar um campo como obrigatório. Além do **[!UICONTROL Nome]** e **[!UICONTROL Obrigatório]** opção, alguns [!DNL Adobe Sign] têm mais opções. Por exemplo, máscara e várias linhas. Além disso, especifique um nome exclusivo para cada [!DNL Adobe Sign] se os campos residem no mesmo campo ou em um campo diferente [!DNL Adobe Sign] blocos.

   Se você selecionar **[!UICONTROL Assinatura digital]** na lista suspensa, é possível aplicar assinaturas digitais ao Formulário adaptável:

   * Online usando assinaturas de nuvem para assinar com uma [ID digital](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) hospedado por um provedor de serviços de confiança.
   * Localmente, baixando o documento com o Adobe Acrobat ou Reader usando um cartão inteligente, um token USB ou uma ID digital baseada em arquivo.

### Habilitar [!DNL Adobe Sign] para um formulário adaptável {#enableadobsignforanadaptiveform}

Pronto para uso, [!DNL Adobe Sign] não está habilitado para um formulário adaptável. Para habilitá-lo:

1. No navegador Conteúdo, toque em **[!UICONTROL Contêiner de formulário]** e toque no **[!UICONTROL Configurar]** ![configure](assets/Smock_Wrench_18_N.svg) ícone . Ele abre o navegador de propriedades e exibe as propriedades do contêiner do Formulário adaptável.
1. No navegador de propriedades, expanda a **[!UICONTROL Assinatura eletrônica]** e selecione a opção **[!UICONTROL Ativar o Adobe Sign]** opção. Ela ativa [!DNL Adobe Sign] para um formulário adaptável.

### Selecionar [!DNL Adobe Sign] Cloud Service e ordem de assinatura {#select-adobe-sign-cloud-service-and-signing-order}

Você pode configurar vários [!DNL Adobe Sign] serviços para uma instância de AEM [!DNL Forms]. É aconselhável ter um conjunto separado de serviços para cada função (Recursos Humanos, Finanças e muito mais). Isso facilita o rastreamento e o relatório de documentos assinados. Por exemplo, um banco tem vários departamentos. Você pode ter uma configuração separada para cada departamento para melhorar o rastreamento dos documentos.

Um documento também pode ter vários destinatários. Por exemplo, um pedido de cartão de crédito pode ter vários candidatos. Um banco requer assinaturas de todos os candidatos antes de iniciar o processamento do pedido. Para cenários de vários recipients, você pode optar por assinar o documento em ordem sequencial ou simultânea.

Para selecionar um Cloud Service e a ordem de assinatura:

![Cloud-service](assets/cloud-service.png)

1. No navegador Conteúdo, toque em **[!UICONTROL Contêiner de formulário]** e toque no **[!UICONTROL Configurar]** ![configure](assets/Smock_Wrench_18_N.svg) ícone . Ele abre o navegador de propriedades e exibe as propriedades do contêiner do Formulário adaptável.
1. No navegador de propriedades, expanda a **[!UICONTROL Assinatura eletrônica]** e selecione a opção **[!UICONTROL Ativar o Adobe Sign]** opção. Ela ativa [!DNL Adobe Sign] para um formulário adaptável.
1. Selecione um Cloud Service na lista já configurada de [!DNL Adobe Sign] Cloud Services.

   Se a variável **[!UICONTROL Adobe Sign Cloud Service]** estiver vazia, siga o [Configurar [!DNL Adobe Sign] com [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) artigo para configurar o serviço.

   A lista suspensa lista os Cloud Services que existem na `global` em Ferramentas > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Além disso, a lista suspensa também lista os Cloud Services que existem na pasta selecionada na **[!UICONTROL Contêiner de configuração]** ao criar um formulário adaptável.

1. Selecione a ordem de assinatura no **[!UICONTROL Os recipients podem concluir]** caixa de diálogo. Os destinatários podem assinar um formulário adaptável **[!UICONTROL Sequencialmente]** - um após outro destinatário, ou **[!UICONTROL Simultaneamente]** - em qualquer ordem.

   Em ordem sequencial, um recipient recebe o contrato do Adobe Sign de cada vez. Depois que o recipient concluir a ação atribuída, o contrato é enviado para o próximo recipient e assim por diante.

   Em ordem simultânea, todos os recipients recebem o contrato do Adobe Sign e podem agir em paralelo.

1. Use o Campo ID do Acordo para associar uma referência de vínculo à ID do Acordo (agreementId). Ele adiciona a ID do Acordo à seção afBoundData do envio de dados para formulários baseados em esquema. A ID do contrato também é adicionada à seção afSubmissionInfo nos dados enviados para todos os formulários habilitados para Adobe Sign. Você pode usar a ID do contrato para rastrear o status do contrato usando o código personalizado (requer a implementação personalizada).

1. [Adicionar recipients a um formulário adaptável](working-with-adobe-sign.md#addsignerstoanadaptiveform) e toque em Concluído ![Salvar](assets/save_icon.svg) para salvar as alterações.

### Adicionar recipients a um formulário adaptável {#addsignerstoanadaptiveform}

Você pode ter um ou vários recipients para um contrato do Adobe Sign. Ao adicionar um recipient, você também pode configurar os detalhes de autenticação do recipient e selecionar se o usuário e o destinatário do formulário são a mesma pessoa. Execute as etapas a seguir para adicionar e fornecer vários detalhes sobre um recipient:

1. No navegador Conteúdo, toque em **[!UICONTROL Contêiner de formulário]** e toque no **[!UICONTROL Configurar]** ![configure](assets/Smock_Wrench_18_N.svg) ícone . Ele abre o navegador de propriedades com as propriedades do contêiner do Formulário adaptativo.
1. No navegador de propriedades, expanda a **[!UICONTROL Assinatura eletrônica]** e selecione a opção **[!UICONTROL Ativar o Adobe Sign]** opção. Ela ativa [!DNL Adobe Sign] para um formulário adaptável.
1. Toque **[!UICONTROL Adicionar destinatário]**. Ele adiciona um recipient ao formulário adaptável. É possível adicionar vários destinatários a um formulário adaptável. Todos os recipients recebem um contrato da Adobe Sign ao enviar o formulário adaptável.
   ![detalhes de telefone](assets/recipient-settings.png)

1. Clique no botão **[!UICONTROL Editar]** ![Editar](assets/Smock_Edit_18_N.svg) ícone para especificar as seguintes informações sobre o recipient:

   * **[!UICONTROL Título]:** Especifique um título para identificar exclusivamente um recipient.

   * **[!UICONTROL O recipient e quem preenche o formulário são a mesma pessoa?]:** Selecionar **[!UICONTROL Sim]**, se o usuário e o primeiro destinatário forem a mesma pessoa. <!-- If the option is set to **No,** then do not use the signature step component in the Adaptive Form. If the form contains a Signature Step component, then the field is automatically set to Yes. -->

   * **[!UICONTROL Função do destinatário]:** Selecione a função de um recipient. Os níveis de serviço da Adobe Sign para empresas e empresas têm a opção de expandir o [funções para recipients do contrato](https://helpx.adobe.com/sign/using/set-up-signer-approver-roles.html), além de **Assinante**, para corresponder melhor aos requisitos do fluxo de trabalho.

   * **[!UICONTROL Endereço de email do destinatário]:** Especifique o endereço de email do recipient. O destinatário recebe o contrato do Adobe Sign no endereço de email especificado. Você pode optar por usar um endereço de email fornecido em um campo de formulário, no perfil de Experience Manager do usuário conectado ou inserir manualmente um endereço de email. É uma etapa obrigatória.

      >[!NOTE]
      >
      >Certifique-se de que o endereço de email do primeiro recipient ou do único (se houver um único recipient) não seja idêntico a [!DNL Adobe Sign] conta usada para configurar os Serviços da nuvem AEM.

   * **[!UICONTROL Método de autenticação do destinatário]:** Especifique o método para autenticar um recipient antes de abrir o contrato do Adobe Sign. Você pode escolher entre telefone, base de conhecimento, autenticação baseada em identidade social e [ID do Governo](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html).
   >[!NOTE]
   >
   >    * Por padrão, a autenticação baseada em identidade social fornece uma opção para autenticação usando Facebook, Google e LinkedIn. Você pode entrar em contato [!DNL Adobe Sign] suporte para ativar outros provedores de autenticação social.


   * **[!DNL Adobe Sign]campos para preencher ou assinar:** Selecionar [!DNL Adobe Sign] campos para o recipient. Um formulário adaptável pode ter vários [!DNL Adobe Sign] campos. Você pode optar por ativar campos específicos para um recipient. O campo exibe todas as informações disponíveis [!DNL Adobe Sign] Blocos. Ao selecionar um bloco, todos os campos do bloco são selecionados. Você pode usar o ícone X para desmarcar um campo.

   ![recipient-details](assets/signer-details.png)

   A imagem acima tem dois exemplos [!DNL Adobe Sign] Blocos: Informações pessoais e detalhes do escritório

   Toque no ![Salvar](assets/save_icon.svg) ícone . O recipient é adicionado.

### Selecione Enviar ação para um formulário adaptável {#selectsubmitactionforanadaptiveform}

Depois de adicionar [!DNL Adobe Sign] para um formulário adaptável, ative [!DNL Adobe Sign] no contêiner do formulário, selecione [!DNL Adobe Sign] Cloud Service e adicione os recipients do contrato do Adobe Sign, selecione uma Ação de envio apropriada para o formulário adaptável. Para obter informações detalhadas sobre as Ações de envio adaptáveis do Forms, consulte [Configurar a ação de envio](configuring-submit-actions.md).

A assinatura e o envio de um formulário são independentes entre si. O envio do formulário adaptável ocorre assim que um contrato do Adobe Sign é criado após o usuário enviar um formulário. [!DNL AEM Forms] as a Cloud Service não espera que os recipients assinem ou concluam outras ações para enviar um formulário adaptável. Um formulário é enviado assim que um usuário clica no botão Enviar ou uma etapa de Resumo exibe o resumo do formulário.

Além disso, uma [!DNL Adobe Sign] ativado O formulário adaptável incorpora a ID do contrato do Adobe Sign para enviar dados. Você pode usar a ID do contrato para rastrear o status do contrato usando o código personalizado (requer a implementação personalizada).

A ID do contrato da Adobe Sign (agreementId) está incluída nos dados de envio do formulário adaptável. Por padrão, a ID do contrato está presente no `afSubmissionInfo` nó dos dados enviados.

```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <afData>
      <afUnboundData>
         <data>
            <textbox1613455050902>ff</textbox1613455050902>
         </data>
      </afUnboundData>
      <afBoundData>
         <data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" />
      </afBoundData>
      <afSubmissionInfo>
         <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].textbox1613455050902[0]</lastFocusItem>
         <stateOverrides />
         <signers>
            <signer0>
               <email />
            </signer0>
         </signers>
         <afPath>/content/dam/formsanddocuments/testsign</afPath>
         <afSubmissionTime>20210311031009</afSubmissionTime>
         <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
      </afSubmissionInfo>
   </afData>
```

Opcionalmente, também é possível associar uma referência de vínculo à ID do Acordo (agreementId). Ele adiciona a ID do contrato à seção afBoundData dos dados enviados. Por exemplo, nos dados enviados a seguir, a ID do Acordo está vinculada a `<userName>` nó:

```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <afData>
         <afUnboundData>
            <data />
         </afUnboundData>
         <afBoundData>
            <config xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
               <agreementID>3AAABLblqZhC2MWu7GFauKh45j_t2ih8mAtmbdIcNSl1HgQubhMJfDaDfylyN7NQiYRam_44ISKm45enIOafHqWZrdaxShf9r</agreementID>
               <dateOfBirth>0001-01-01</dateOfBirth>
            </config>
         </afBoundData>
         <afSubmissionInfo>
            <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].projectDetails[0]</lastFocusItem>
            <stateOverrides />
            <signers>
               <signer0>
                  <email />
               </signer0>
            </signers>
            <afPath>/content/dam/formsanddocuments/testathon2021-1/gaurav/xsd-based</afPath>
            <afSubmissionTime>20210311095211</afSubmissionTime>
            <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
         </afSubmissionInfo>
      </afData>
```

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the Adaptive Form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

Sua experiência de assinatura de formulário está pronta. É possível visualizar o formulário para verificar a experiência de assinatura. No formulário publicado, [!DNL Adobe Sign] Campos de bloco são exibidos quando um recipient recebe o formulário para assinatura por meio de um email. Quando a variável **[!UICONTROL Quando o destinatário e a pessoa que preenche o formulário são iguais?]** estiver marcada como sim e a condição for atendida, o usuário será redirecionado para o contrato do Adobe Sign depois dos envios e o usuário poderá assinar o documento imediatamente, em vez de esperar que o contrato seja exibido no email.

## Configurar assinaturas da nuvem para um formulário adaptável {#configure-cloud-signatures-for-an-adaptive-form}

Assinaturas digitais baseadas em nuvem ou assinaturas remotas são uma nova geração de assinaturas digitais que funcionam em computadores, dispositivos móveis e na Web — e atendem aos mais altos níveis de conformidade e garantia para autenticação de destinatários. Você pode assinar um formulário adaptável com assinaturas digitais baseadas em nuvem.

Depois [edição das propriedades do formulário adaptável para o Adobe Sign](working-with-adobe-sign.md#enableadobesign), execute as seguintes etapas para adicionar um campo de assinatura da nuvem a um Formulário adaptável:

1. Arrastar e soltar **[!UICONTROL Bloco Adobe Sign]** do navegador de componentes para o Formulário adaptável. O [!UICONTROL Bloco Adobe Sign] tem todos os [!DNL Adobe Sign] campos. Por padrão, ele adiciona uma **[!UICONTROL Assinatura]** para o formulário adaptável.

   ![Bloco de assinatura](assets/sign-block-new.png)

1. Selecione o **[!UICONTROL Bloco Adobe Sign]** e toque no **[!UICONTROL Editar]** ![Editar](assets/Smock_Edit_18_N.svg) ícone . Ele exibe opções para adicionar campos e formatar a aparência de um campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Selecionar e adicionar [!DNL Adobe Sign] campos. **B.** Expanda o [!DNL Adobe Sign] bloquear para exibição em tela cheia

1. Toque no **[!UICONTROL Campo Adobe Sign]** ![Adobe Sign](assets/adobesign.png) ícone . Ele exibe opções para selecionar e adicionar [!DNL Adobe Sign] campos.

   Expanda o **[!UICONTROL Tipo]** campo suspenso a ser selecionado **[!UICONTROL Assinatura digital]** e toque no **[!UICONTROL Concluído]** ícone para adicionar o campo selecionado ao [!DNL Adobe Sign] bloco.

   ![Assinaturas digitais](assets/digital_signatures_new.png)

   É obrigatório fornecer um nome exclusivo para um campo.

   Aplique assinaturas digitais ao formulário adaptável usando:

   * Assinaturas da nuvem: Assinar com um [ID digital](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) hospedado por um provedor de serviços de confiança.
   * Adobe Acrobat ou Reader: Baixe e abra o documento com Adobe Acrobat ou Reader para assinar usando um cartão inteligente, um token USB ou uma ID digital baseada em arquivo.

   Depois de adicionar o campo de assinatura da nuvem ao formulário adaptável, execute as seguintes etapas para concluir o processo de configuração:

   * [Ativar o Adobe Sign para um formulário adaptável](#enableadobsignforanadaptiveform)
   * [Selecione Adobe Sign Cloud Service para um formulário adaptável](#selectadobesigncloudserviceforanadaptiveform)
   * [Adicionar recipients a um formulário adaptável](#addsignerstoanadaptiveform)
   * [Selecione Enviar ação para um formulário adaptável](#selectsubmitactionforanadaptiveform)


### Configurar a página de agradecimento ou o componente da etapa de resumo {#configure-the-thank-you-page-or-summary-step-component}

O **[!UICONTROL Etapa de resumo]** O componente envia automaticamente o formulário, preenche as informações dentro da página Resumo personalizada e exibe o resumo do formulário enviado. O componente Etapa de resumo ocupa a largura total disponível para o formulário. É recomendável não ter nenhum outro componente na seção que contém o componente Etapa de resumo .

## Perguntas frequentes {#frequently-asked-questions}

**P:** É possível incorporar um formulário adaptável em outro formulário adaptável. O formulário adaptável incorporado pode ser [!DNL Adobe Sign] habilitado?
**Ans:** Não, a Experience Manager Forms não suporta o uso de um formulário adaptável que incorpora um [!DNL Adobe Sign] formulário adaptável ativado para assinatura

**P:** Quando eu crio um formulário adaptável usando o modelo avançado e o abro para edição, uma mensagem de erro &quot;Assinatura eletrônica ou destinatários não estão configurados corretamente&quot;. é exibido. Como resolver a mensagem de erro?
**Ans:** O formulário adaptável criado usando o modelo avançado está configurado para usar [!DNL Adobe Sign]. Para resolver o erro, crie e selecione um [!DNL Adobe Sign] configuração da nuvem e configuração de um [!DNL Adobe Sign] para o formulário adaptável.

**P:** Posso usar [!DNL Adobe Sign] tags de texto em um componente de texto estático de um formulário adaptável?
**Ans:** Sim, você pode usar tags de texto em um componente de texto para adicionar [!DNL Adobe Sign] campos para um Documento de registro (somente a opção Documento de registro gerado automaticamente) ativados Formulário adaptável. Para saber mais sobre o procedimento e as regras para criar uma tag de texto, consulte [Documentação do Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Além disso, observe que o Adaptive Forms tem suporte limitado para tags de texto. Você pode usar as tags de texto para criar apenas os campos que [Bloco Adobe Sign](working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) suporta.

## Solução de problemas {#troubleshoot}

### [!DNL Adobe Sign] falhas do acordo {#adobe-sign-agreement-failures}

**Problema**
When [!DNL Adobe Sign] estiver configurado para um formulário adaptável, o serviço não criará um [!DNL Adobe Sign] Contrato para o formulário adaptativo subjacente.

**Resolução**

* Verifique a [configuração do Adobe Sign Cloud Service](adobe-sign-integration-adaptive-forms.md) usado no formulário adaptável.
* Verifique se o aplicativo de API em [!DNL Adobe Sign] servidor usado para configurar [!DNL Adobe Sign] O Cloud Service tem as permissões necessárias.
* Se estiver usando vários [!DNL Adobe Sign] Cloud Services, aponte o **[!UICONTROL URL de oAuth]** de todos os serviços ao mesmo tempo **[!UICONTROL Adobe Sign Shard]**.

* Usar endereços de email separados para configurar [!DNL Adobe Sign] e para o primeiro ou único recipient. O endereço de email do primeiro recipient ou do único (se houver um único recipient) não pode ser idêntico a [!DNL Adobe Sign] conta usada para configurar os Serviços da nuvem AEM.

## Artigos relacionados {#related-articles}

* [Integrar [!DNL Adobe Sign] com [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)
* [Práticas recomendadas para usar [!DNL Adobe Sign] com o Adaptive Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
