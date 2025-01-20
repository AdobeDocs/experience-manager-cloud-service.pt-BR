---
title: Publicação do Forms para o Edge Delivery Services
description: Saiba como a publicação de formulários funciona com o Edge Delivery Services e como publicar formulários AEM com o Edge Delivery Services.
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---


# Publicação do Forms para o Edge Delivery Services

Este artigo orienta você pelo processo de publicação de formulários no AEM Edge Delivery Services.
Para publicar formulários no Edge Delivery Services, primeiro estabeleça uma conexão entre seu ambiente AEM e seu repositório GitHub. Depois de conectado, você pode criar os formulários usando o Editor universal, que segue uma abordagem do WYSIWYG (What You See Is What You Get) para obter uma experiência do usuário contínua e consistente com o Sites.

## Pré-requisitos

* Novo no Forms adaptável? Configure seu repositório GitHub seguindo o [tutorial](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) fornecido.
* Se você já estiver usando o Edge Delivery Services, adicione a versão mais recente do [bloco adaptável do Forms](/help/edge/docs/forms/tutorial.md#) ao repositório do GitHub.
* A instância do autor do AEM Forms inclui um modelo baseado em Edge Delivery Services. Verifique se a [versão mais recente dos Componentes principais](https://github.com/adobe/aem-core-forms-components) está instalada em seu ambiente.
* Mantenha o URL da sua instância as a Cloud Service do AEM Forms e do seu Repositório GitHub acessíveis.

## Publish Forms para Edge Delivery Services

Para publicar formulários para Edge Delivery Services, execute as etapas abaixo:

[1. Vincular repositório GitHub à instância AEM](#link-github-repository-to-aem-instance)

[2. Vincular instância do AEM ao repositório GitHub](#link-aem-instance-to-github-repository)

### Vincular repositório GitHub à instância AEM

Para vincular [seu projeto no Repositório GitHub](/help/edge/docs/forms/tutorial.md) à instância do autor do AEM Forms, execute as seguintes etapas:

1. Vá para o repositório GitHub que você criou ou configurou para os Edge Delivery Services.
1. Abra o arquivo `fstab.yaml` para edição.
1. Atualize o arquivo `fstab.yaml` no repositório do GitHub com a URL da instância as a Cloud Service do AEM Forms.

   ```javascript
    mountpoints:
    /:
        url: [author-instance-url]/bin/franklin.delivery/[Github owner]/[Github Repository]/[Github branch] 
        type: "markup"
        suffix: ".html"
   ```

   Por exemplo, se o repositório GitHub se chamar &quot;aemcrosswalk&quot;, se estiver localizado na conta &quot;wkndform&quot; e você estiver usando a ramificação &quot;main&quot;, o URL da instância do autor será semelhante ao seguinte:

   ```
        mountpoints:
            /:
            url: https://author-p133911-e1313554.adobeaemcloud.com/bin/franklin.delivery/wkndform/aemcrosswalk/main
            type: "markup"
            suffix: ".html"
   ```

1. Confirme as alterações no arquivo `fstab.yaml`.

### Vincular instância do AEM ao repositório GitHub

Para vincular a instância do autor do AEM Forms a [seu projeto no Repositório GitHub](/help/edge/docs/forms/tutorial.md), execute as seguintes etapas:

[1. Crie um formulário adaptável com base no modelo Edge Delivery Services](#1-create-an-adaptive-form-based-on-the-edge-delivery-services-template)

[2. Localize o contêiner de configuração do formulário na instância do autor do AEM](#2-locate-your-forms-configuration-container-in-aem-author-instance)

[3. Crie o formulário no Editor universal](#3-author-the-form-in-the-universal-editor)

[4. Publish e pré-visualização do formulário](#4-publish-and-preview-the-form)

#### 1. Crie um formulário adaptável com base no modelo Edge Delivery Services

1. Acesse a instância do as a Cloud Service do AEM Forms.
1. Selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O Assistente será aberto. Na guia Source, selecione um modelo de formulário baseado em Edge Delivery Services:

   ![Criar EDS Forms](/help/edge/assets/create-eds-forms.png){width=50%, align-center}

1. Clique em **[!UICONTROL Criar]** e o assistente **Criar formulário** será exibido.
1. Especifique a **URL do GitHub**. Por exemplo, se o repositório GitHub se chamar &quot;aemcrosswalk&quot;, ele estiver localizado na conta &quot;wkndform&quot;, o URL será:
   `https://github.com/wkndform/aemcrosswalk`
1. Clique em **[!UICONTROL Criar]**.

   ![Assistente de criação de formulário](/help/edge/assets/create-form-wizard.png){width=50%, align-center}

   Assim que você clicar em **[!UICONTROL Criar]**, o formulário será aberto no editor universal para criação.

   ![criar o formulário](/help/edge/assets/author-form.png){width=50%, align-center}

   >[!NOTE]
   >
   > A configuração de Edge Delivery Services para os formulários com base no modelo Edge Delivery Services é criada automaticamente no contêiner de configuração do formulário.

#### 2. Localize o contêiner de configuração do formulário na instância do autor do AEM

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service Edge Delivery Services]** > **[!UICONTROL Configuração]** na sua instância as a Cloud Service do AEM Forms.
1. Selecione a pasta que corresponde ao nome do formulário. Por exemplo, se seu formulário for chamado de &#39;contact-us&#39;, escolha a pasta `forms/contact-us`, selecione a configuração e publique-a:

   ![Configuração de Edge Delivery Services](/help/forms/assets/aem-instance-eds-configuration.png){width=50%, align-center}

1. Clique em **[!UICONTROL Propriedades]** para ver a configuração.\
   ![Configuração criada automaticamente](/help/edge/assets/aem-forms-create-configuration-github.png){width=50%, align-center}

   Você pode deixar a opção Host do Edge como está. O formulário seria publicado em ambientes de visualização (.page) e em tempo real (.live).

1. Clique em **[!UICONTROL Salvar e fechar]**. A configuração é salva.

#### 3. Crie o formulário no Editor universal

Ao clicar em **[!UICONTROL Criar]**, o formulário é aberto no Editor Universal para criação.

1. Abra o navegador Conteúdo e navegue até o componente **[!UICONTROL Formulário adaptável]** na **Árvore de conteúdo**.

   ![árvore de conteúdo](/help/edge/assets/content-tree.png){width=50%, align-center}

1. Clique no ícone **[!UICONTROL Adicionar]** e adicione os componentes desejados da lista **Componentes de Formulários Adaptáveis**.

   ![adicionar componente](/help/edge/assets/add-component.png){width=50%, align-center}

1. Selecione o componente de Formulário adaptável adicionado e atualize suas propriedades usando **[!UICONTROL Propriedades]**.

   ![abrir propriedades](/help/edge/assets/component-properties.png){width=50%, align-center}

   A captura de tela abaixo exibe o formulário simples &quot;Fale conosco&quot; criado no Editor universal:

   ![contate-nos a partir do formulário](/help/edge/assets/contact-us.png){width=50%, align-center}

#### 4. Publish e pré-visualização do formulário

Agora publique o formulário no Edge Delivery Services clicando no botão **[!UICONTROL Publish]** no canto superior direito do Editor Universal.

![publicar formulário](/help/edge/assets/publish-form.png){width=50%, align-center}


Veja como acessar o formulário em Edge Delivery Services:

* **Versão Preparada (para teste)**: a versão preparada exibe a versão não publicada e funcional do formulário para fins de teste. Use o seguinte formato de URL para visualizar o formulário antes que ele entre em vigor:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  Por exemplo, se o repositório do seu projeto for chamado de &quot;aemcrosswalk&quot;, estiver localizado na conta &quot;wkndform&quot; e você estiver usando a ramificação &quot;principal&quot; e o formulário como &quot;entre em contato conosco&quot;, o URL da versão preparada será semelhante ao seguinte:
https://main--aemcrosswalk--wkndform.aem.page/content/forms/af/contact-us

* **Versão ao Vivo (formulário publicado)**:   A versão ao vivo exibe a versão publicada mais recentemente do formulário, acessível aos usuários finais. Use o seguinte formato de URL para acessar a versão publicada e em tempo real do formulário:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  Por exemplo, se o repositório do seu projeto for chamado de &quot;aemcrosswalk&quot;, estiver localizado na conta &quot;wkndform&quot; e você estiver usando a ramificação &quot;principal&quot; e o formulário como &quot;entre em contato conosco&quot;, o URL da versão preparada será semelhante ao seguinte:
https://main--aemcrosswalk--wkndform.aem.live/content/forms/af/contact-us

A estrutura do URL permanece a mesma para as versões preparadas e ativas. No entanto, o conteúdo exibido é diferente com base no contexto:

![Exibir formulário publicado](/help/edge/assets/eds-view-publish-form.png){width=50%, align-center}

## Resolução de problemas

Está tendo problemas para carregar o formulário? Estes são alguns problemas comuns e como corrigi-los:

* **URL do formulário**: verifique se a URL do seu formulário não inclui a extensão &quot;.html&quot; no final. O Edge Deliver Service não exige essa extensão.

* **URL do Autor do AEM** L: verifique se a URL do Autor do AEM listada no arquivo `fstab.yaml` está formatada corretamente. Ele deve incluir os seguintes detalhes:

   * O proprietário correto do GitHub
   * O nome correto do repositório
   * A ramificação específica que você está usando para o Edge Delivery Services

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## Consulte também:

{{see-more-forms-eds}}