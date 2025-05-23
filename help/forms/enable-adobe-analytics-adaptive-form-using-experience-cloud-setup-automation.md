---
title: Como habilitar o Adobe Analytics para uma análise de rastreamento rápido de um Formulário adaptável?
description: A Automação de configuração do Experience Cloud ajuda a conectar o Adobe Analytics a um formulário adaptável para obter uma análise de rastreamento rápida e insights sobre as interações e o envolvimento do visitante.
keywords: Ativar o Adobe Analytics para um formulário adaptável usando a Automação de configuração do Experience Cloud, Ativar o Adobe Analytics no Forms, Adobe Analytics no Adaptive Forms, integração do Forms Analytics, Forms e Adobe Analytics
feature: Adaptive Forms
role: Admin, User
exl-id: 0e1aa040-08b4-4c1a-b247-ad6fff410187
source-git-commit: a23576b5dc6d78a29fe19cd23f3c4788f2bee23e
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 2%

---

# Ativar o Adobe Analytics para um formulário adaptável usando a automação de configuração do Experience Cloud {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Este artigo |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html?lang=pt-BR) |

A Automação de configuração do Experience Cloud ajuda a conectar o Adobe Analytics ao Adaptive Forms, o que auxilia na análise rápida da interação do usuário com seus formulários e oferece insights sobre as interações e o envolvimento do visitante. A Automação de configuração do Experience Cloud também ajuda a monitorar o desempenho do formulário, o que envolve a avaliação de métricas como tempos de conclusão e pontos de devolução. Essa análise ajuda a otimizar formulários para obter uma melhor experiência do usuário, ao mesmo tempo em que distingue o comportamento do usuário com base no status de logon, por exemplo, usuários anônimos, para identificar tendências e padrões gerais.

## Vantagens da integração do Adobe Analytics com o Adaptive Forms {#advantages-of-integrating-adobe-analytics-with-aem-forms}

* **Insights sobre o comportamento do usuário final**: o Adobe Analytics ajuda a obter insights sobre o comportamento do usuário final, revela ações do usuário, quedas e taxas de conclusão, permitindo uma compreensão mais profunda de como os indivíduos se envolvem com formulários.
* **Permitir que usuários empresariais não técnicos obtenham insights**: a Adobe Analytics, por meio de sua interface fácil de usar, permite que até usuários não técnicos acessem e interpretem dados de uso de formulários, promovendo decisões orientadas por dados para aprimorar as experiências de inscrição.
* **Otimização da experiência de captura de dados com base no uso**: as organizações identificam facilmente pontos problemáticos na captura de dados, resultando em melhorias direcionadas que melhoram a usabilidade dos formulários e aumentam os envios bem-sucedidos.

## Escopo das métricas de uso adaptáveis do Forms {#scope-of-adaptive-forms-usage-metrics}

O Adobe Analytics oferece uma ampla variedade de métricas de desempenho Adaptive Forms projetadas para fornecer insights valiosos sobre o uso de formulários e oferece uma análise de rastreamento rápido. Essas métricas são:

* **Representações de formulário, envios de formulário, erros de validação e visitantes únicos**, permitindo que você avalie o uso e a eficácia de seus formulários.

* **Insights do visitante**, que incluem frequências de visita e envio, e contagens de visitantes únicos, oferecendo uma visão abrangente do público-alvo do seu formulário.

* Dados de **Tipo de dispositivo** que informam sobre os dispositivos que os usuários empregam para acessar seus formulários.

* **A análise geográfica** revela a distribuição regional dos usuários do formulário.

* As métricas **Fontes de tráfego** e **Formulários populares**, que consistem nos principais domínios de referência e formulários mais visitados, ajudam você a entender onde seu tráfego se origina e quais formulários são os mais populares.

* **A atividade de usuário nos principais formulários** fornece informações sobre visitas de campo, representações de formulários, erros de validação, formulários abandonados e envios de formulários, permitindo que você analise o comportamento do usuário.

* **Linha do tempo gasto em formulários** que oferece uma exibição da linha do tempo do engajamento do usuário com seus formulários.

* **Áreas que exigem assistência do visitante** métricas que incluem exibições de ajuda, instâncias de erro de validação e frequências de visita de campo, destacando onde os usuários podem precisar de assistência para preencher formulários.

![Relatório do Analytics](assets/analytics-report.png){width="100%"}


Para obter informações detalhadas sobre cada métrica, visite [Exibir e entender os relatórios do AEM Forms Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Pré-requisitos {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

A Automação de Instalação do Experience Cloud exige uma **licença do Adobe Analytics**, **coleta de dados (antigo Adobe Launch)** para gerenciar scripts de rastreamento, e **licença do Experience Manager Forms** para agregação de dados simplificada e geração de insight.

Se você tiver uma licença ativa para o **Adobe Analytics** e o **Experience Manager Forms** e integração com a **Coleção de dados (antigo Adobe Launch)**, deverá verificar a disponibilidade no console do desenvolvedor.

Para verificar se os itens mencionados acima estão disponíveis para o seu ambiente do Forms as a Cloud Service, visite o [console do desenvolvedor](https://developer.adobe.com/console/projects), navegue até o projeto e pesquise seu projeto com a ID do programa - ID do ambiente, por exemplo, para o ambiente com a URL `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`, a ID do programa - ID do ambiente é `p45913-e175111`. Verifique se a Automação de configuração do Experience Cloud, o Adobe Analytics e a API do Experience Platform Launch estão listados. Se estiverem listados, você poderá ativar o Adobe Analytics para obter uma análise de rastreamento rápido do seu Forms adaptável.

![Integração de Pré-requisito do Forms Analytics](assets/analytics-aem.png){width="100%"}

<!-- 
>[!NOTE]
> If you have an active licenses for Experience Cloud Setup Automation, Adobe Analytics, and Experience Platform Launch API, you should verify their availability within your developer console.
-->

<!-- For more information about your available integrations, see [troubleshooting Adaptive Forms with Analytics Integration](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html?lang=pt-BR)
-->

## Configurar Adobe Analytics {#configure-adobe-analytics}

Execute as etapas listadas abaixo para habilitar e configurar o Adobe Analytics para uma análise de rastreamento rápido do seu Forms adaptável:

* [Ativar o Adobe Analytics para Forms adaptável com base nos componentes de base](#integrate-adobe-analytics-with-aem-forms-for-foundation-component)
* [Ativar o Adobe Analytics para Forms adaptável com base nos Componentes principais](#integrate-adobe-analytics-with-aem-forms-for-core-components)

>[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)


<!--
>[!NOTE]
>
> This is the demo video for **Foundation Component**. In **Core Component** you are required to perform similar steps but the container is not chosen for forms.
-->

### Habilitar o Adobe Analytics com o componente Adaptive Forms for Foundation {#integrate-adobe-analytics-with-aem-forms-for-foundation-component}

1. Criar um contêiner de configuração para os serviços em nuvem:
   1. Vá para **[!UICONTROL Ferramentas > Geral > Navegador de Configuração]**.
   1. Selecione ou crie um Contêiner de Configuração e habilite a pasta para **[!UICONTROL Configurações de Nuvem]**.
   1. Selecione **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.
1. Na sua instância do AEM, vá para **[Forms]** >> **[Forms e Documento]**.
1. Selecione o **[!UICONTROL Formulário]** >> **[!UICONTROL Propriedades]**, No **[!UICONTROL Contêiner de Configuração]**, selecione o contêiner de configuração que você criou ou selecionou no **[!UICONTROL Navegador de Configuração]** na Etapa 1.
1. Selecione o Painel de Tarefas no Painel à Esquerda e clique em **Configurar Analytics** e **Ativar Adobe Analytics**.
1. Forneça o nome de sua preferência para o conjunto de relatórios, Clique em **[!UICONTROL Avançar]** e **[!UICONTROL Salvar]**.
1. Depois que você salvar o projeto, a configuração será executada por algum tempo até a integração do Adobe Analytics com o seu Formulário adaptável. Você também pode verificar o **status da integração**.

   >[!NOTE]
   >
   >Se a configuração demorar mais de 15 minutos, tente habilitar novamente a análise para seus formulários.

1. Na sua instância do AEM, vá para **[!UICONTROL Forms]** >> **[Forms e Documento]** e selecione seu **[!UICONTROL Formulário]**. Você verá que o Adobe Analytics está integrado ao seu formulário conforme mostrado na imagem abaixo.
1. Agora você pode exibir seu [relatório de Adobe Analytics do formulário adaptável](#view-adobe-analytics-report).

![AEM Analytics Integrado](assets/analytics-aem-integrated.png){width="100%"}


### Ativar o Adobe Analytics com Forms adaptável para componentes principais {#integrate-adobe-analytics-with-aem-forms-for-core-components}

1. Na sua instância do AEM, vá para **[!UICONTROL Forms]** >> **[!UICONTROL Forms e Documento]** e selecione seu **[!UICONTROL Formulário]**.
1. Selecione o Painel de Tarefas à esquerda e clique em **Configurar Analytics** e **Ativar Adobe Analytics**.
1. Forneça o nome de sua preferência para o conjunto de relatórios, Clique em **[!UICONTROL Avançar]** e **[!UICONTROL Salvar]**.
1. Depois que você salvar o projeto, a configuração será executada por algum tempo até a integração do Adobe Analytics com o seu Formulário adaptável. Você também pode verificar o **status da integração**.

   >[!NOTE]
   >
   >Se a configuração demorar mais de 15 minutos, tente habilitar novamente a análise para seus formulários.

1. Na sua instância do AEM, vá para **[!UICONTROL Forms]** >> **[!UICONTROL Forms e Documento]** e selecione seu **[!UICONTROL Formulário]**. Você verá que o Adobe Analytics está integrado ao seu formulário.
1. Agora você pode exibir seu [relatório de Adobe Analytics do formulário adaptável](#view-adobe-analytics-report).

## Exibir o relatório adaptável do Forms Adobe Analytics {#view-adobe-analytics-report}

1. Na sua instância do AEM, vá para **[!UICONTROL Forms]** >> **[!UICONTROL Forms e Documento]**.
1. Selecione o formulário e veja que o Adobe Analytics está integrado, como mostrado à esquerda, à Forms ativada para o Adobe Analytics.

   ![Exibir Relatório](assets/activ-aa.png){width="100%"}

1. Clique em **Adobe Analytics** para exibir seu relatório e analisar os dados de desempenho.

Para conectar um Formulário adaptável ao Adobe Analytics usando o método manual, visite [Integrar o AEM Forms ao Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md).

## Ativar o Analytics para o Forms adaptável no Sites {#Connect-Analytics-to-Adaptive-Forms-in-Sites}

Configurar análises de rastreamento rápido para o Formulário adaptável no AEM Sites ajuda a rastrear as interações do usuário e os envios de formulários na página Formulário no Sites. Ao integrar facilmente a análise ao seu Forms do Sites, você obtém informações valiosas sobre o comportamento do usuário, taxas de conversão e áreas para melhoria no seu formulário.

### Pré-requisitos {#Prerequisites-to-connect-forms-analytics-to-sites}

Para conectar e habilitar o Analytics no Adaptive Forms para AEM Sites, você deve garantir que seu AEM Sites tenha um Adobe Analytics ativo.

### Conectar o Adaptive Forms no Sites para ativar o Analytics {#Connect-analytics-to-adaptive-forms}

Para conectar o Formulário adaptável em uma página do AEM Sites e habilitar o Analytics para análises de rastreamento rápido, inclua a biblioteca do cliente `customfooterlibs` na página do AEM Sites usando o Arquétipo AEM/Repositório Git e o pipeline de implantação.

1. Abra o projeto [Arquétipo do AEM Forms ou Repositório Git Clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) em um editor de texto. Por exemplo, Visual Studio Code.

1. Navegue até a página dos sites onde o formulário adaptável existe, por exemplo, Neste projeto de demonstração, temos `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.

1. Copie o valor de `sling:resourceSuperType`. Por exemplo, o valor é `core/wcm/components/page/v3/page`.

   ![recurso de sling](/help/forms/assets/slingresource.png){width="100%"}

1. Criar a estrutura semelhante no local `ui.apps/src/main/content/jcr_root/apps` igual a `core/wcm/components/page/v3/page`.

   ![estrutura de sobreposição](/help/forms/assets/overlaystructure.png){width="100%"}

1. Adicione um arquivo `customfooterlibs.html`.

   ```
   // customheaderlibs.html
   <sly data-sly-use.page="com.adobe.cq.wcm.core.components.models.Page">
   <sly data-sly-test="${page.data && page.dataLayerClientlibIncluded}" data-sly-call="${clientlib.js @ categories='core.forms.components.commons.v1.datalayer', async=true}"></sly>
   </sly>
   ```

   O `customfooterlibs.html` é usado para o JavaScript.

1. [Execute o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=pt-BR) para implantar as alterações.

### Ativar regras do Form Analytics para o Forms no Sites {#bind-forms-analytics-rules-to-forms-in-sites}

1. Visite a **Coleção de dados da Adobe Experience Platform**.
1. Clique em **Marcas**, localizado no lado esquerdo.
1. Pesquise seu projeto com a ID do programa conforme mostrado na imagem abaixo, por exemplo, para o ambiente com URL `https://author-p45921-e175111-cmstg.adobeaemcloud.com/index.html`, a ID do programa é `45921`.

   ![Pesquisar-seu-formulário-na-coleção-de-dados](/help/forms/assets/aep-data-collection.png){width="100%"}

1. Adicione a configuração para **Regras de formulário** e **Elementos de dados** conforme fornecido abaixo:

#### Adicionar regras de formulário {#form-rules}

1. Selecione o formulário e adicione a **Nova propriedade**, localizada no canto superior direito, ou clique no formulário.
1. Na página de propriedades, clique em **Regras** e selecione eventos para o formulário. Na imagem de exemplo abaixo, é **Eventos de Formulário**.

   ![Pesquisar-seu-formulário-na-coleção-de-dados](/help/forms/assets/aep-form-event-properties.png){width="100%"}

1. Selecione todos os eventos do seu formulário e **copie** que estão localizados no painel superior direito.
1. Depois de copiar, um pop-up **Copiar regra** é exibido onde você pesquisa a página Sites com a ID do projeto para colar as Regras de formulário.

   ![Regras de forma de cópia](/help/forms/assets/copy-form-rules.png){width="100%"}

1. Clique em **copiar** para colar as regras de formulário na página Sites.

#### Adicionar elementos de dados {#data-elements}

1. Selecione o formulário e adicione a **Nova propriedade**, localizada no canto superior direito, ou clique no formulário.
1. Na página de propriedades, clique em **Elementos de Dados** e selecione eventos para o formulário.
1. Selecione todos os eventos do formulário e da **cópia** localizados no painel superior direito.
1. Depois de copiar, um pop-up **Copiar regra** é exibido onde você pesquisa a página Sites com a ID do projeto para colar as Regras de formulário.
1. Clique em **copiar** para colar as regras de formulário na página Sites.

   ![Elementos-dados-formulário](/help/forms/assets/form-data-elements.png){width="100%"}

Depois de vincular as regras de Formulário e Sites por meio das etapas acima, execute as seguintes etapas para habilitar o Analytics para o seu Formulário adaptável na página Sites:

1. Clique em **Fluxo de publicação** à esquerda.
1. Clique em **Adicionar biblioteca** e digite o nome que você preferir.
1. No menu suspenso **Ambiente** à direita, selecione **desenvolvimento**.
1. Clique Em **Adicionar Todos Os Recursos Alterados**.
1. Clique em **Salvar e criar no desenvolvimento**.

![publicar para desenvolvimento](/help/forms/assets/publish-to-dev.png){width="100%"}


<!--

## Best Practices

1.    Verify that Adobe Analytics is enabled on all the forms activated for Adobe Analytics.

1.    Check the Adobe Analytics report periodically to gain insights into user behavior and form performance. For instance, you may set the cadence to 15 days or the period you prefer to choose for report analysis. This enables you to improve the forms enrollment experience.

1.    Enable Analytics for all or most of your forms for tracking and analyzing user interaction with your forms and to gain insights into visitor interactions and engagement.

1. Check your forms performance after you update your form fields or components.

1.    Share Analytics report with your peer groups for review, you can schedule your report for a later time.

-->

## Consulte também {#see-also}

* [Exibir e entender relatórios de análise do Adaptive Forms](/help/forms/view-understand-aem-forms-analytics-reports.md)
* [Adição de um formulário adaptável a uma página do AEM Sites ou a um fragmento de experiência](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Integrar o AEM Forms com o Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)
