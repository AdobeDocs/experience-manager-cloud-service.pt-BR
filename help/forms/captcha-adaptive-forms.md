---
title: Utilização do reCAPTCHA no Adaptive Forms
description: Saiba como configurar o serviço Google reCAPTCHA no Adaptive Forms.
topic-tags: adaptive_forms, author
source-git-commit: b4665d0291ee1223e46c8ecf13ca13ea336107d3
workflow-type: tm+mt
source-wordcount: '1913'
ht-degree: 1%

---

# Usar reCAPTCHA no Adaptive Forms{#using-reCAPTCHA-in-adaptive-forms}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html) |
| AEM as a Cloud Service | Este artigo |

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-br) para [criação de um novo Forms adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) é um programa comumente usado em transações on-line para distinguir entre humanos e programas ou bots automatizados. Ele representa um desafio e avalia a resposta do usuário para determinar se é um humano ou um bot interagindo com o site. Ele impede que o usuário continue se o teste falhar e ajuda a tornar as transações online seguras, impedindo que os bots publiquem spam ou fins mal-intencionados.

[!DNL AEM Forms] suporte a reCAPTCHA no Adaptive Forms. Você pode usar o serviço reCAPTCHA pelo Google para implementar o CAPTCHA.

>[!NOTE]
>
>* [!DNL AEM Forms] suporte para reCaptcha v2 e reCaptcha Enterprise. Nenhuma outra versão é compatível.
>* O reCAPTCHA no Adaptive Forms não é compatível no modo offline no [!DNL AEM Forms] aplicativo.
>

## Configurar o serviço reCAPTCHA pelo Google {#google-reCAPTCHA}

Os autores de formulários podem usar o serviço reCAPTCHA pelo Google para implementar o reCAPTCHA no Adaptive Forms. Ele oferece recursos avançados de CAPTCHA para proteger o site. Para obter mais informações sobre como o reCAPTCHA funciona, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/). O serviço reCAPTCHA inclui [!DNL reCAPTCHA v2] e [!DNL reCAPTCHA Enterprise] que você pode integrar a [!DNL AEM Forms]. Com base em seu requisito, você pode configurar o serviço reCAPTCHA para habilitar:

![reCAPTCHA](/help/forms/assets/recaptcha_new.png)

* [reCAPTCHA Enterprise no AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [reCAPTCHA v2 no AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)


### Configurar o reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Criar ou selecionar um [Projeto do Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) e habilitar [API corporativa do reCAPTCHA](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. Obtenha o [ID do projeto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) e criar um [Chave de API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) e uma [chave do site para sites](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Criar contêiner de configuração para serviços em nuvem.

   1. Ir para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**.
   1. Selecione uma pasta ou crie uma pasta e ative a pasta para configurações de nuvem seguindo estas etapas:
      1. No Navegador de configuração, selecione a pasta e toque em **[!UICONTROL Propriedades]**.
      1. Na caixa de diálogo Propriedades de configuração, ative **[!UICONTROL Configurações da nuvem]**.
      1. Toque **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair do diálogo.

1. Configurar o serviço em nuvem para [!DNL reCAPTCHA Enterprise].

   1. Na instância do autor do Experience Manager, acesse ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. Toque **[!UICONTROL reCAPTCHA]**. A página Configurações é aberta. Selecione o contêiner de configuração criado e toque em **[!UICONTROL Criar]**.
   1. Selecionar versão como [!DNL reCAPTCHA Enterprise] e especifique Nome, ID do projeto, Chave do site e Chave de API (Obtida na Etapa 2) para o serviço reCAPTCHA Enterprise.
   1. Selecione o tipo de chave, o tipo de chave deve ser o mesmo que a chave do site que você configurou no [Projeto do Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin), por exemplo, **Chave do site da caixa de seleção** ou **Chave do site com base em pontuação**.
   1. Especificar um [pontuação de limite no intervalo de 0 a 1](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores). Pontuações maiores ou iguais às pontuações de limite identificam a interação humana, caso contrário, são consideradas interação de bot.
   1. Toque **[!UICONTROL Criar]** para criar a configuração do cloud service.

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Tap **[!UICONTROL Save Settings]** and then tap **[!UICONTROL OK]** to complete the configuration.
-->

Quando o serviço reCAPTCHA Enterprise estiver ativado, ele estará disponível para uso em formulários adaptáveis. Consulte [uso de CAPTCHA em formulários adaptáveis](#using-reCAPTCHA).

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->

### Configurar o Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Obter [Par de chaves da API do reCAPTCHA](https://www.google.com/recaptcha/admin) do Google. Inclui uma **chave do site** e uma **chave secreta**.
1. Criar contêiner de configuração para serviços em nuvem.
   1. Ir para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**.
   1. Selecione uma pasta ou crie uma pasta e ative a pasta para configurações de nuvem seguindo estas etapas:
      1. No Navegador de configuração, selecione a pasta e toque em **[!UICONTROL Propriedades]**.
      1. Na caixa de diálogo Propriedades de configuração, ative **[!UICONTROL Configurações da nuvem]**.
      1. Toque **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair do diálogo.

1. Configure o serviço de nuvem para o reCAPTCHA v2.

   1. Na instância do autor do AEM, acesse ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Toque **[!UICONTROL reCAPTCHA]**. A página Configurações é aberta. Selecione o contêiner de configuração criado e toque em **[!UICONTROL Criar]**.
   1. Selecionar versão como [!DNL reCAPTCHA v2] , especifique Nome, Chave do site e Chave secreta para o serviço reCAPTCHA (Obtido na Etapa 1) e toque em **[!UICONTROL Criar]** para criar a configuração do cloud service.
   1. Na caixa de diálogo Editar componente, especifique o site e as chaves secretas obtidas na etapa 1. Toque **[!UICONTROL Salvar configurações]** e toque em **OK** para concluir a configuração.

   Depois que o serviço reCAPTCHA é configurado, ele é disponibilizado para uso em formulários adaptáveis. Para obter mais informações, consulte [uso de CAPTCHA em formulários adaptáveis](#using-reCAPTCHA).

<!--![reCAPTCHA v2](/help/forms/assets/recaptcha-v2.png)-->


## Usar reCAPTCHA em formulários adaptáveis {#using-reCAPTCHA}

Para usar o reCAPTCHA em formulários adaptáveis:

1. Abra um formulário adaptável no modo de edição.

   >[!NOTE]
   >
   >Verifique se o contêiner de configuração selecionado ao criar o formulário adaptável contém o serviço de nuvem reCAPTCHA. Também é possível editar propriedades do formulário adaptável para alterar o contêiner de configuração associado ao formulário.

1. No navegador de componentes, arraste e solte a **Captcha** no formulário adaptável.

   >[!NOTE]
   >
   >* Não há suporte para o uso de mais de um componente Captcha em um formulário adaptável. Além disso, não é recomendável usar CAPTCHA em um painel marcado para carregamento lento ou em um fragmento.
   >* O reCaptcha é sensível ao tempo e expira em cerca de dois minutos. Portanto, é recomendável colocar o componente Captcha antes do botão Enviar no formulário adaptável.

1. Selecione o componente Captcha que você adicionou e toque em ![cmppr](assets/cmppr.png) para editar suas propriedades.
1. Especifique um título para o widget CAPTCHA. O valor padrão é **Captcha**. Selecionar **Ocultar título** se não quiser que o título seja exibido.
1. No **Serviço de captcha** selecione **reCAPTCHA** para ativar o serviço reCAPTCHA se você o tiver configurado conforme descrito em [Serviço reCAPTCHA da Google](#google-reCAPTCHA).
1. Selecione uma configuração na lista suspensa Configurações para **reCAPTCHA Enterprise** ou **reCAPTCHA v2**
   1. Se você selecionar **reCAPTCHA Enterprise** versão, o tipo de chave pode ser de **caixa de seleção** ou **baseado em pontuação**, Baseia-se na sua seleção ao configurar [chave do site para sites](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key):

   >[!NOTE]
   >
   >* Na configuração da nuvem com **tipo de chave** as **caixa de seleção**, a mensagem de erro personalizada será exibida como uma mensagem em linha se a validação do captcha falhar.
   >* Na configuração da nuvem com **tipo de chave** as **baseado em pontuação**, a mensagem de erro personalizada será exibida como uma mensagem pop-up se a validação do captcha falhar.

   1. Você pode selecionar o tamanho como **[!UICONTROL Normal]** e **[!UICONTROL Compacto]**.
   1. É possível selecionar um **[!UICONTROL Referência de vinculação]**, Em **[!UICONTROL Referência de vinculação]** os dados enviados são dados vinculados, caso contrário, são dados desvinculados. Abaixo estão exemplos XML de dados não vinculados e dados vinculados (com referência de vinculação como SSN), respectivamente, quando um formulário é enviado.

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

   Se você selecionar **reCAPTCHA v2** versão:
   1. Você pode selecionar o tamanho como **[!UICONTROL Normal]** ou **[!UICONTROL Compacto]** para o widget reCAPTCHA.
   1. É possível selecionar a variável **[!UICONTROL Invisível]** opção para mostrar o desafio de CAPTCHA somente no caso de uma atividade suspeita.

   O serviço reCAPTCHA é ativado no formulário adaptável. Você pode visualizar o formulário e ver o CAPTCHA funcionando. A variável **protegido pelo reCAPTCHA** exibido abaixo, é exibido nos formulários protegidos.
   ![Google protegido pelo selo reCAPTCHA](/help/forms/assets/google-recaptcha-v2.png)

1. Salve as propriedades.

>[!NOTE]
> 
> Não selecionar **[!UICONTROL Padrão]** no menu suspenso do serviço Captcha, quando o serviço AEM CAPTCHA padrão é descontinuado.

>[!VIDEO](https://video.tv.adobe.com/v/3422641/recaptcha-google-adaptive-forms/?quality=12&learn=on)

### Mostrar ou ocultar o componente CAPTCHA com base em regras {#show-hide-captcha}

É possível optar por mostrar ou ocultar o componente CAPTCHA com base nas regras aplicadas em um componente de um Formulário adaptável. Toque no componente e selecione ![editar regras](assets/edit-rules-icon.svg)e toque em **[!UICONTROL Criar]** para criar uma regra. Para obter mais informações sobre como criar regras, consulte [Editor de regras](rule-editor.md).

Por exemplo, o componente CAPTCHA deve ser exibido em um formulário adaptável somente se o campo Valor da moeda no formulário tiver um valor maior que 25000.

Toque no **[!UICONTROL Valor da moeda]** no formulário e crie as seguintes regras:

![Mostrar ou ocultar regras](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> Quando você seleciona uma configuração reCAPTCHA v2 e o tamanho é definido como [!UICONTROL Invisível], a opção mostrar/ocultar permanece desativada.

### Validar CAPTCHA {#validate-captcha}

É possível validar CAPTCHA em um Formulário adaptável ao enviar o formulário ou basear a validação CAPTCHA em ações e condições do usuário.

#### Validar CAPTCHA no envio do formulário {#validation-form-submission}

Para validar um CAPTCHA automaticamente ao enviar um Formulário adaptável:

1. Toque no componente CAPTCHA e selecione ![cmppr](assets/configure-icon.svg) para visualizar as propriedades do componente.
1. No **[!UICONTROL Validar CAPTCHA]** , selecione **[!UICONTROL Validar CAPTCHA no envio do formulário]**.
1. Toque ![Concluído](assets/save_icon.svg) para salvar as propriedades do componente.

#### Validar CAPTCHA em ações e condições do usuário {#validate-captcha-user-action}

Para validar um CAPTCHA com base nas condições e ações do usuário:

1. Toque no componente CAPTCHA e selecione ![cmppr](assets/configure-icon.svg) para visualizar as propriedades do componente.
1. No **[!UICONTROL Validar CAPTCHA]** , selecione **[!UICONTROL Validar CAPTCHA em uma ação do usuário]**.
1. Toque ![Concluído](assets/save_icon.svg) para salvar as propriedades do componente.

[!DNL Experience Manager Forms] fornece `ValidateCAPTCHA` API para validar CAPTCHA usando condições predefinidas. Você pode chamar a API usando uma Ação enviar personalizada ou definindo regras em componentes em um Formulário adaptável.

Veja a seguir um exemplo de `ValidateCAPTCHA` API para validar CAPTCHA usando condições predefinidas:

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

O exemplo significa que a variável `ValidateCAPTCHA` A API valida o CAPTCHA no formulário somente se o número de dígitos na caixa numérica especificada pelo usuário durante o preenchimento do formulário for maior que 5.

**Opção 1: uso [!DNL Experience Manager Forms] Validar a API CAPTCHA para validar CAPTCHA usando uma ação enviar personalizada**

Execute as seguintes etapas para usar o `ValidateCAPTCHA` API para validar CAPTCHA usando uma Ação enviar personalizada:

1. Adicione o script que inclui a variável `ValidateCAPTCHA` API para ação enviar personalizada. Para obter mais informações sobre ações enviar personalizadas, consulte [Criar uma ação enviar personalizada para o Forms adaptável](custom-submit-action-form.md).
1. Selecione o nome da Ação de envio personalizada na **[!UICONTROL Ação de envio]** lista suspensa no **[!UICONTROL Envio]** propriedades de um Formulário adaptável.
1. Toque **[!UICONTROL Enviar]**. O CAPTCHA é validado com base nas condições definidas no `ValidateCAPTCHA` API da Ação de envio personalizada.

**Opção 2: uso [!DNL Experience Manager Forms] Validar API CAPTCHA para validar CAPTCHA em uma ação do usuário antes de enviar o formulário**

Você também pode invocar `ValidateCAPTCHA` ao aplicar regras em um componente em um Formulário adaptável.

Por exemplo, você adiciona um **[!UICONTROL Validar CAPTCHA]** em um Formulário adaptável e crie uma regra para chamar um serviço com o clique de um botão.

A figura a seguir ilustra como você pode chamar um serviço com um clique de **[!UICONTROL Validar CAPTCHA]** botão:

![Validar CAPTCHA](assets/captcha-validation1.gif)

Você pode chamar o servlet personalizado que inclui `ValidateCAPTCHA` API usando o editor de regras e ativar ou desativar o botão enviar do Formulário adaptável com base no resultado da validação.

Da mesma forma, você pode usar o editor de regras para incluir um método personalizado para validar CAPTCHA em um Formulário adaptável.

### Adicionar serviços personalizados de CAPTCHA {#add-custom-captcha-service}

[!DNL Experience Manager Forms] O fornece o reCAPTCHA como o serviço CAPTCHA. No entanto, é possível adicionar um serviço personalizado para exibir na **[!UICONTROL Serviço CAPTCHA]** lista suspensa.

Este é um exemplo de implementação da interface para adicionar outro serviço CAPTCHA ao formulário adaptável:

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

`captchaPropertyNodePath` refere-se ao caminho do recurso do componente CAPTCHA no repositório Sling. Use essa propriedade para incluir detalhes específicos do componente CAPTCHA. Por exemplo, `captchaPropertyNodePath` inclui informações para a configuração de nuvem do reCAPTCHA configurada no componente CAPTCHA. As informações de configuração da nuvem fornecem **[!UICONTROL Chave do site]** e **[!UICONTROL Chave secreta]** configurações para implementar o serviço reCAPTCHA.

`userResponseToken` refere-se à `g_recaptcha_response` que é gerado após resolver um CAPTCHA em um formulário.

### Editar domínio do serviço reCAPTCHA {#reCAPTCHA-service-domain}

O serviço reCAPTCHA usa `https://www.recaptcha.net/` como o domínio padrão. Você pode modificar as configurações para definir `https://www.google.com/` ou qualquer nome de domínio personalizado para carregar, processar e validar o serviço reCAPTCHA.

Defina o **[!UICONTROL af.cloudservices.recaptcha.domain]** propriedade do **[!UICONTROL Configuração do canal da Web do formulário adaptável e da comunicação interativa]** configuração a ser especificada `https://www.google.com/` ou qualquer outro nome de domínio personalizado. O seguinte arquivo JSON exibe uma amostra:

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

Para definir valores de uma configuração, [Gerar configurações de OSGi usando o SDK do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart), e [implantar a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) para a instância do Cloud Service.
