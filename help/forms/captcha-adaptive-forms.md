---
title: Como usar CAPTCHA no Adaptive Forms?
description: Saiba como configurar o serviço Google reCAPTCHA para um Formulário adaptável.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 5%

---

# Usar reCAPTCHA no Adaptive Forms {#using-reCAPTCHA-in-adaptive-forms}

>[!NOTE]
>
> A Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adicionar o Adaptive Forms às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base.


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |
| Aplica-se a | Formulário adaptável baseado em Componentes de base. <br> Para o formulário adaptável baseado em Componentes principais, [Clique aqui](/help/forms/captcha-adaptive-forms-core-components.md). |


O CAPTCHA (um teste de Turing público e completamente automatizado para diferenciar computadores e humanos) é um programa comumente usado em transações online para distinguir entre humanos e programas ou bots automatizados. O recurso apresenta um desafio e avalia a resposta do usuário para determinar se é um humano ou um bot interagindo com o site. O CAPTCHA impede que o usuário prossiga se o teste falhar e ajuda a tornar as transações online seguras, evitando que bots publiquem spam ou outro conteúdo mal-intencionado.

O AEM Forms as a Cloud Service é compatível com as seguintes soluções CAPTCHA:

* [Google reCAPTCHA](#configure-recaptcha-service-by-google)
* [Cilindro de nuvens](/help/forms/integrate-adaptive-forms-turnstile.md)
* [Captcha](/help/forms/integrate-adaptive-forms-hcaptcha.md)

## Configurar o serviço reCAPTCHA pelo Google {#google-reCAPTCHA}

Os autores de formulários podem usar o serviço reCAPTCHA pelo Google para implementar o reCAPTCHA no Adaptive Forms. Ele oferece recursos avançados de CAPTCHA para proteger o site. Para obter mais informações sobre como o reCAPTCHA funciona, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/). O AEM Forms oferece suporte a [!DNL reCAPTCHA v2] e [!DNL reCAPTCHA Enterprise]. Nenhuma outra versão é compatível. Observe também que o reCAPTCHA no Adaptive Forms não é compatível no modo offline no aplicativo [!DNL AEM Forms]. Com base em seu requisito, você pode configurar o serviço reCAPTCHA para habilitar:

![reCAPTCHA](/help/forms/assets/recaptcha_new.png)

* [reCAPTCHA Enterprise no AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [reCAPTCHA v2 no AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)


### Configurar o reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Crie ou selecione um [projeto do Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) e habilite a [API corporativa do reCAPTCHA](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. Obtenha a [ID do Projeto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) e crie uma [chave de API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) e uma [chave de site para sites](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Criar contêiner de configuração para serviços em nuvem.

   1. Vá para **[!UICONTROL Ferramentas > Geral > Navegador de Configuração]**.
   1. Selecione uma pasta ou crie uma pasta e ative a pasta para configurações de nuvem seguindo estas etapas:
      1. No Navegador de Configuração, selecione a pasta e selecione **[!UICONTROL Propriedades]**.
      1. Na caixa de diálogo Propriedades de Configuração, habilite **[!UICONTROL Configurações de Nuvem]**.
      1. Selecione **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.

1. Configure o serviço de nuvem para [!DNL reCAPTCHA Enterprise].

   1. Na instância do autor do Experience Manager, vá para ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**.
   1. Selecione **[!UICONTROL reCAPTCHA]**. A página Configurações é aberta. Selecione o contêiner de configuração criado e selecione **[!UICONTROL Criar]**.
   1. Selecione a versão como [!DNL reCAPTCHA Enterprise] e especifique o Nome, a ID do Projeto, a Chave do Site e a Chave da API (Obtida na Etapa 2) para o serviço reCAPTCHA Enterprise.
   1. Selecione o tipo de chave; o tipo de chave deve ser igual à chave do site que você configurou no [projeto do Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin), por exemplo, **Chave do site da caixa de seleção** ou **Chave do site com base em pontuação**.
   1. Especifique uma pontuação de limite [&#x200B; no intervalo de 0 a 1](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores). Pontuações maiores ou iguais às pontuações de limite identificam a interação humana, caso contrário, são consideradas interação de bot.
   1. Selecione **[!UICONTROL Criar]** para criar a configuração do serviço de nuvem.

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Select **[!UICONTROL Save Settings]** and then select **[!UICONTROL OK]** to complete the configuration.
-->

Quando o serviço reCAPTCHA Enterprise estiver ativado, ele estará disponível para uso em formulários adaptáveis. Consulte [usando CAPTCHA em formulários adaptáveis](#using-reCAPTCHA).

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->

### Configurar o Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Obtenha o [par de chaves da API do reCAPTCHA](https://www.google.com/recaptcha/admin) da Google. Inclui uma **chave do site** e uma **chave secreta**.
1. Criar contêiner de configuração para serviços em nuvem.
   1. Vá para **[!UICONTROL Ferramentas > Geral > Navegador de Configuração]**.
   1. Selecione uma pasta ou crie uma pasta e ative a pasta para configurações de nuvem seguindo estas etapas:
      1. No Navegador de Configuração, selecione a pasta e selecione **[!UICONTROL Propriedades]**.
      1. Na caixa de diálogo Propriedades de Configuração, habilite **[!UICONTROL Configurações de Nuvem]**.
      1. Selecione **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.

1. Configure o serviço de nuvem para o reCAPTCHA v2.

   1. Na instância do autor AEM, vá para ![tools-1](assets/tools-1.png) > **Cloud Service**.
   1. Selecione **[!UICONTROL reCAPTCHA]**. A página Configurações é aberta. Selecione o contêiner de configuração criado e selecione **[!UICONTROL Criar]**.
   1. Selecione a versão como [!DNL reCAPTCHA v2], especifique o Nome, a Chave do Site e a Chave Secreta para o serviço reCAPTCHA (Obtido na Etapa 1) e selecione **[!UICONTROL Criar]** para criar a configuração do serviço de nuvem.
   1. Na caixa de diálogo Editar componente, especifique o site e as chaves secretas obtidas na etapa 1. Selecione **[!UICONTROL Salvar configurações]** e **OK** para concluir a configuração.

   Depois que o serviço reCAPTCHA é configurado, ele é disponibilizado para uso em formulários adaptáveis. Para obter mais informações, consulte [usando CAPTCHA em formulários adaptáveis](#using-reCAPTCHA).

<!--![reCAPTCHA v2](/help/forms/assets/recaptcha-v2.png)-->


## Usar o Google reCAPTCHA em formulários adaptáveis {#using-reCAPTCHA}

Para usar o Google reCAPTCHA em um formulário adaptável:

1. Abra um formulário adaptável no modo de edição.

   >[!NOTE]
   >
   >Verifique se o contêiner de configuração selecionado ao criar o formulário adaptável contém o serviço de nuvem reCAPTCHA. Também é possível editar propriedades do formulário adaptável para alterar o contêiner de configuração associado ao formulário.

1. No navegador de componentes, arraste e solte o componente **Captcha** no formulário adaptável.

   >[!NOTE]
   >
   >* Não há suporte para o uso de mais de um componente Captcha em um formulário adaptável. Além disso, não é recomendável usar CAPTCHA em um painel marcado para carregamento lento ou em um fragmento.
   >* O reCaptcha é sensível ao tempo e expira em cerca de dois minutos. Portanto, é recomendável colocar o componente Captcha antes do botão Enviar no formulário adaptável.

1. Selecione o componente Captcha adicionado e selecione ![cmppr](assets/cmppr.png) para editar suas propriedades.
1. Especifique um título para o widget CAPTCHA. O valor padrão é **Captcha**. Selecione **Ocultar título** se não quiser que o título seja exibido.
1. No menu suspenso do **serviço Captcha**, selecione **reCAPTCHA** para habilitar o serviço reCAPTCHA se você o tiver configurado conforme descrito no serviço [reCAPTCHA do Google](#google-reCAPTCHA).
1. Selecione uma configuração na lista suspensa Configurações para **reCAPTCHA Enterprise** ou **reCAPTCHA v2**
   1. Se você selecionar a versão **reCAPTCHA Enterprise**, o tipo de chave poderá ser **caixa de seleção** ou **com base na pontuação**. Ela será baseada na sua seleção ao configurar a [chave do site para sites](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key):

   >[!NOTE]
   >
   >* Na configuração da nuvem com **tipo de chave** como **caixa de seleção**, a mensagem de erro personalizada será exibida como uma mensagem embutida se a validação de captcha falhar.
   >* Na configuração da nuvem com **tipo de chave** como **baseado em pontuação**, a mensagem de erro personalizada será exibida como uma mensagem pop-up se a validação de captcha falhar.

   1. Você pode selecionar o tamanho como **[!UICONTROL Normal]** e **[!UICONTROL Compacto]**.
   1. Você pode selecionar uma **[!UICONTROL Referência de Ligação]**. Em **[!UICONTROL Referência de Ligação]**, os dados enviados são dados associados, caso contrário, são dados não associados. Abaixo estão exemplos XML de dados não vinculados e dados vinculados (com referência de vinculação como SSN), respectivamente, quando um formulário é enviado.

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data>
                   <captcha16820607953761>
                       <captchaType>reCaptchaEnterprise</captchaType>
                       <captchaScore>0.9</captchaScore>
                   </captcha16820607953761>
               </data>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>371237912</SSN>
                       <FirstName>Sarah </FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608034928</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data/>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>
                           <captchaType>reCaptchaEnterprise</captchaType>
                           <captchaScore>0.9</captchaScore>
                       </SSN>
                       <FirstName>Sarah</FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608035111</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   Se você selecionar a versão **reCAPTCHA v2**:
   1. Você pode selecionar o tamanho como **[!UICONTROL Normal]** ou **[!UICONTROL Compacto]** para o widget re do reCAPTCHA.
   1. Você pode selecionar a opção **[!UICONTROL Invisível]** para mostrar o desafio de CAPTCHA somente no caso de uma atividade suspeita.

   O serviço reCAPTCHA é ativado no formulário adaptável. Você pode visualizar o formulário e ver o CAPTCHA funcionando. O símbolo **protegido pelo reCAPTCHA**, exibido abaixo, é exibido nos formulários protegidos.
   ![Google protegido pelo selo reCAPTCHA](/help/forms/assets/google-recaptcha-v2.png)

1. Salve as propriedades.

>[!NOTE]
> 
> Não selecione **[!UICONTROL Padrão]** no menu suspenso do serviço Captcha, pois o serviço AEM CAPTCHA padrão está obsoleto.

>[!VIDEO](https://video.tv.adobe.com/v/3422641/recaptcha-google-adaptive-forms/?quality=12&learn=on)

### Mostrar ou ocultar o componente CAPTCHA com base em regras {#show-hide-captcha}

É possível optar por mostrar ou ocultar o componente CAPTCHA com base nas regras aplicadas em um componente de um Formulário adaptável. Selecione o componente, selecione ![editar regras](assets/edit-rules-icon.svg) e selecione **[!UICONTROL Criar]** para criar uma regra. Para obter mais informações sobre como criar regras, consulte [Editor de regras](rule-editor.md).

Por exemplo, o componente CAPTCHA deve ser exibido em um formulário adaptável somente se o campo Valor da moeda no formulário tiver um valor maior que 25000.

Selecione o campo **[!UICONTROL Valor da Moeda]** no formulário e crie as seguintes regras:

![Mostrar ou ocultar regras](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> Ao selecionar uma configuração do reCAPTCHA v2 e o tamanho estiver definido como [!UICONTROL Invisível], a opção mostrar/ocultar permanecerá desabilitada.

### Validar CAPTCHA {#validate-captcha}

É possível validar CAPTCHA em um Formulário adaptável ao enviar o formulário ou basear a validação CAPTCHA em ações e condições do usuário.

#### Validar CAPTCHA no envio do formulário {#validation-form-submission}

Para validar um CAPTCHA automaticamente ao enviar um Formulário adaptável:

1. Selecione o componente CAPTCHA e selecione ![cmppr](assets/configure-icon.svg) para exibir as propriedades do componente.
1. Na seção **[!UICONTROL Validar CAPTCHA]**, selecione **[!UICONTROL Validar CAPTCHA no envio do formulário]**.
1. Selecione ![Concluído](assets/save_icon.svg) para salvar as propriedades do componente.

#### Validar CAPTCHA em ações e condições do usuário {#validate-captcha-user-action}

Para validar um CAPTCHA com base nas condições e ações do usuário:

1. Selecione o componente CAPTCHA e selecione ![cmppr](assets/configure-icon.svg) para exibir as propriedades do componente.
1. Na seção **[!UICONTROL Validar CAPTCHA]**, selecione **[!UICONTROL Validar CAPTCHA em uma ação do usuário]**.
1. Selecione ![Concluído](assets/save_icon.svg) para salvar as propriedades do componente.

[!DNL Experience Manager Forms] fornece a API `ValidateCAPTCHA` para validar CAPTCHA usando condições predefinidas. Você pode chamar a API usando uma Ação enviar personalizada ou definindo regras em componentes em um Formulário adaptável.

Este é um exemplo de uma API `ValidateCAPTCHA` para validar CAPTCHA usando condições predefinidas:

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
     GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

O exemplo significa que a API `ValidateCAPTCHA` valida o CAPTCHA no formulário somente se o número de dígitos na caixa numérica especificada pelo usuário durante o preenchimento do formulário for maior que 5.

**Opção 1: Use a API ValidateCAPTCHA [!DNL Experience Manager Forms] para validar CAPTCHA usando uma Ação de Envio personalizada**

Execute as seguintes etapas para usar a API `ValidateCAPTCHA` para validar CAPTCHA usando uma Ação de envio personalizada:

1. Adicione o script que inclui a API `ValidateCAPTCHA` para personalizar a Ação de Envio. Para obter mais informações sobre Ações de Envio personalizadas, consulte [Criar uma Ação de Envio personalizada para o Forms Adaptável](custom-submit-action-form.md).
1. Selecione o nome da Ação de Envio personalizada na lista suspensa **[!UICONTROL Ação de Envio]** nas propriedades **[!UICONTROL Envio]** de um Formulário adaptável.
1. Selecione **[!UICONTROL Enviar]**. O CAPTCHA é validado com base nas condições definidas na API `ValidateCAPTCHA` da Ação de Envio personalizada.

**Opção 2: Use a API [!DNL Experience Manager Forms] ValidateCAPTCHA para validar CAPTCHA em uma ação do usuário antes de enviar o formulário**

Você também pode invocar a API `ValidateCAPTCHA` aplicando regras em um componente em um Formulário adaptável.

Por exemplo, você adiciona um botão **[!UICONTROL Validar CAPTCHA]** em um Formulário adaptável e cria uma regra para chamar um serviço com o clique de um botão.

A figura a seguir ilustra como você pode chamar um serviço clicando em um botão **[!UICONTROL Validar CAPTCHA]**:

![Validar CAPTCHA](assets/captcha-validation1.gif)

Você pode chamar o servlet personalizado que inclui a API `ValidateCAPTCHA` usando o editor de regras e habilitar ou desabilitar o botão enviar do Formulário adaptável com base no resultado da validação.

Da mesma forma, você pode usar o editor de regras para incluir um método personalizado para validar CAPTCHA em um Formulário adaptável.

<!--

### Add custom CAPTCHA services {#add-custom-captcha-service}

[!DNL Experience Manager Forms] provides reCAPTCHA as the CAPTCHA service. However, you can add a custom service to display in the **[!UICONTROL CAPTCHA Service]** drop-down list.  

The following is a sample implementation of the interface to add additional CAPTCHA service to your Adaptive Form:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` refers to the resource path of the CAPTCHA component in the Sling repository. Use this property to include details specific to the CAPTCHA component. For example, `captchaPropertyNodePath` includes information for the reCAPTCHA cloud configuration configured on the CAPTCHA component. The cloud configuration information provides **[!UICONTROL Site Key]** and **[!UICONTROL Secret Key]** settings for implementing the reCAPTCHA service.

`userResponseToken` refers to the `g_recaptcha_response` that gets generated after solving a CAPTCHA in a form. -->

### Editar domínio do serviço reCAPTCHA {#reCAPTCHA-service-domain}

O serviço reCAPTCHA usa `https://www.recaptcha.net/` como o domínio padrão. Você pode modificar as configurações para definir `https://www.google.com/` ou qualquer nome de domínio personalizado para carregar, renderizar e validar o serviço reCAPTCHA.

Defina a propriedade **[!UICONTROL af.cloudservices.recaptcha.domain]** da configuração **[!UICONTROL Configuração do Canal da Web de Formulário Adaptável e Comunicação Interativa]** para especificar `https://www.google.com/` ou qualquer outro nome de domínio personalizado. O seguinte arquivo JSON exibe uma amostra:

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

Para definir valores de uma configuração, [Gere Configurações OSGi usando o AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=pt-BR#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [implante a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=pt-BR#deployment-process) na sua instância Cloud Service.

## Consulte também {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Reference Themes, Templates, and Form Data models for Adaptive Forms](/help/forms/reference-themes-templates-data-models.md)

-->
