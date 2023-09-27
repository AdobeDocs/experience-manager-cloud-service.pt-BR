---
title: Ativar o Adobe Analytics para um formulário adaptável
description: A Automação de configuração do Experience Cloud ajuda a conectar o Adobe Analytics a um Formulário adaptável para rastrear insights sobre as interações e o envolvimento do visitante.
source-git-commit: 4fc6d29cd008b04ad97ceb17201c1f8d0e72439e
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 0%

---


# Ativar o Adobe Analytics para um formulário adaptável usando a automação de configuração do Experience Cloud {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

<span class="preview"> Esse é um recurso de pré-lançamento acessível por meio de nossa [canal de pré-lançamento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

A Automação de configuração do Experience Cloud ajuda a conectar o Adobe Analytics ao Adaptive Forms, o que ajuda a rastrear e analisar a interação do usuário com seus formulários e oferecer insights sobre as interações e o envolvimento do visitante. A Automação de configuração do Experience Cloud também ajuda a monitorar o desempenho do formulário, o que envolve a avaliação de métricas como tempo de conclusão e pontos de devolução. Essa análise ajuda a otimizar formulários para obter uma melhor experiência do usuário, ao mesmo tempo em que distingue o comportamento do usuário com base no status de logon, por exemplo, usuários anônimos, para identificar tendências e padrões gerais.


## Vantagens da integração do Adobe Analytics com o Adaptive Forms {#advantages-of-integrating-adobe-analytics-with-aem-forms}

* **Insights sobre o comportamento do usuário final**: o Adobe Analytics ajuda a obter insights sobre o comportamento do usuário final, revela ações do usuário, quedas e taxas de conclusão, permitindo uma compreensão mais profunda de como os indivíduos se envolvem com formulários.
* **Permitir que usuários não técnicos de negócios obtenham insights**: o Adobe Analytics, por meio de sua interface fácil de usar, permite que até usuários não técnicos acessem e interpretem dados de uso de formulário, promovendo decisões orientadas por dados para melhorar as experiências de inscrição.
* **Otimização da experiência de captura de dados com base no uso**: as organizações identificam facilmente os pontos problemáticos na captura de dados, resultando em melhorias direcionadas que melhoram a usabilidade dos formulários e aumentam os envios bem-sucedidos.

## Escopo das métricas de uso adaptáveis do Forms {#scope-of-adaptive-forms-usage-metrics}

O Adobe Analytics oferece uma ampla variedade de métricas de desempenho adaptáveis do Forms projetadas para fornecer insights valiosos sobre o uso do formulário. Essas métricas são:

* **Representações de formulário, Envios de formulário, Erros de validação e Visitantes únicos**, permitindo avaliar o uso e a eficácia dos formulários.

* **Insights do visitante** que incluem frequências de visita e envio e contagens de visitantes únicos, oferecendo uma visão abrangente do público-alvo do formulário.

* **Tipo de dispositivo** dados que informam sobre os dispositivos que os usuários utilizam para acessar seus formulários.

* **Discriminação geográfica** revela a distribuição regional dos usuários do formulário.

* **Fontes de tráfego** e **Formulários populares** as métricas que consistem nos principais domínios de referência e formulários mais visitados ajudam você a entender onde seu tráfego se origina e quais formulários são os mais populares.

* **Atividade do usuário nos principais formulários** O fornece insights sobre visitas de campo, representações de formulário, erros de validação, formulários abandonados e envios de formulário, permitindo analisar o comportamento do usuário.

* **Linha do tempo gasto em formulários** que oferece uma visualização do engajamento do usuário com seus formulários baseada em linha do tempo.

* **Áreas que exigem assistência do visitante** métricas que incluem exibições de ajuda, instâncias de erro de validação e frequências de visita de campo, destacando onde os usuários podem precisar de assistência para preencher formulários.

![Relatório do Analytics](assets/analytics-report.png){width="100%"}


Para obter informações detalhadas sobre cada métrica, visite [Visualização e noções básicas sobre relatórios do AEM Forms Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Pré-requisitos {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

A Automação de configuração do Experience Cloud requer um **Licença do Adobe Analytics**, **Coleta de dados (antigo Adobe Launch)** para gerenciar scripts de rastreamento e **Licença do Experience Manager Forms** para uma agregação de dados e geração de insights simplificadas.

Se você tiver uma licença ativa para **Adobe Analytics** e **Experience Manager Forms**, e você terá integração com **Coleta de dados (antigo Adobe Launch)**, você deve verificar a disponibilidade deles no console do desenvolvedor.

Para verificar se os itens acima estão disponíveis para o seu ambiente as a Cloud Service do Forms, visite a [console do desenvolvedor](https://developer.adobe.com/console/projects), navegue até o projeto e pesquise seu projeto com a id do programa - id de ambiente, por exemplo, para o ambiente com o URL `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`, id do programa - a id do ambiente é `p45913-e175111`. Verifique se Experience Cloud Setup Automation, Adobe Analytics e Experience Platform Launch API estão listados. Se estiverem listados, você poderá ativar o Adobe Analytics para o seu Forms adaptável.

![Integração de pré-requisito do Forms Analytics](assets/analytics-aem.png){width="100%"}

<!-- 
>[!NOTE]
> If you have an active licenses for Experience Cloud Setup Automation, Adobe Analytics, and Experience Platform Launch API, you should verify their availability within your developer console.
-->

<!-- For more information about your available integrations, see [troubleshooting Adaptive Forms with Analytics Integration](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html)
-->

## Configurar Adobe Analytics {#configure-adobe-analytics}

Execute as etapas listadas abaixo para ativar e configurar o Adobe Analytics para sua Forms adaptável:

* [Ativar o Adobe Analytics para Forms adaptável com base nos componentes de base](#integrate-adobe-analytics-with-aem-forms-for-foundation-component)
* [Ativar o Adobe Analytics para Forms adaptável com base nos Componentes principais](#integrate-adobe-analytics-with-aem-forms-for-core-components)

>[!VIDEO](https://video.tv.adobe.com/v/3424577/recaptcha-google-adaptive-forms/?quality=12&learn=on)


<!--
>[!NOTE]
>
> This is the demo video for **Foundation Component**. In **Core Component** you are required to perform similar steps but the container is not chosen for forms.
-->

### Habilitar o Adobe Analytics com o componente Adaptive Forms for Foundation {#integrate-adobe-analytics-with-aem-forms-for-foundation-component}

1. Criar um contêiner de configuração para os serviços em nuvem:
   1. Ir para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**.
   1. Selecione ou crie um Contêiner de configuração e ative a pasta para **[!UICONTROL Configurações da nuvem]**.
   1. Toque **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair do diálogo.
1. Na instância do AEM, acesse **[Forms]** >> **[Forms e Documento]**.
1. Selecione o **[!UICONTROL Formulário]** >> **[!UICONTROL Propriedades]**, No **[!UICONTROL Contêiner de configuração]**, selecione o container de configuração que você criou ou selecionou na **[!UICONTROL Navegador de configuração]** na Etapa 1.
1. Selecione o Painel de tarefas no painel esquerdo e clique em **Configurar o Analytics** e **Ativar Adobe Analytics**.
1. Forneça o nome de sua preferência para o conjunto de relatórios, clique em **[!UICONTROL Próxima]** e **[!UICONTROL Salvar]**.
1. Depois de salvar o projeto, a configuração será executada por algum tempo até a integração do Adobe Analytics com o seu Formulário adaptável. Você também pode verificar o **status da integração**.

   >[!NOTE]
   >
   >Se a configuração demorar mais de 15 minutos, tente habilitar novamente a análise para seus formulários.

1. Na instância do AEM, acesse **[!UICONTROL Forms]** >> **[Forms e Documento]** e selecione o **[!UICONTROL Formulário]**, você verá que o Adobe Analytics está integrado ao seu formulário, como mostrado na imagem abaixo.
1. Agora você pode visualizar seu [Relatório do Adobe Analytics do formulário adaptável](#view-adobe-analytics-report).

![Análise integrada do AEM](assets/analytics-aem-integrated.png){width="100%"}


### Ativar o Adobe Analytics com Forms adaptável para componentes principais {#integrate-adobe-analytics-with-aem-forms-for-core-components}

1. Na instância do AEM, acesse **[!UICONTROL Forms]** >> **[!UICONTROL Forms e Documento]** e selecione o **[!UICONTROL Formulário]**.
1. Selecione o Painel de tarefas à esquerda e clique em **Configurar o Analytics** e **Ativar Adobe Analytics**.
1. Forneça o nome de sua preferência para o conjunto de relatórios, clique em **[!UICONTROL Próxima]** e **[!UICONTROL Salvar]**.
1. Depois de salvar o projeto, a configuração será executada por algum tempo até a integração do Adobe Analytics com o seu Formulário adaptável. Você também pode verificar o **status da integração**.

   >[!NOTE]
   >
   >Se a configuração demorar mais de 15 minutos, tente habilitar novamente a análise para seus formulários.

1. Na instância do AEM, acesse **[!UICONTROL Forms]** >> **[!UICONTROL Forms e Documento]** e selecione o **[!UICONTROL Formulário]**, você verá que o Adobe Analytics está integrado ao seu formulário.
1. Agora você pode visualizar seu [Relatório do Adobe Analytics do formulário adaptável](#view-adobe-analytics-report).

## Exibir o relatório adaptável do Forms Adobe Analytics {#view-adobe-analytics-report}

1. Na instância do AEM, acesse **[!UICONTROL Forms]** >> **[!UICONTROL Forms e Documento]**.
1. Selecione o formulário e veja que o Adobe Analytics está integrado, como mostrado à esquerda, à Forms ativada para o Adobe Analytics.

   ![Exibir Relatório](assets/activ-aa.png){width="100%"}

1. Clique em **Adobe Analytics** para exibir seu relatório e analisar dados de desempenho.

Para conectar um formulário adaptável ao Adobe Analytics usando o método manual, visite [Integrar o AEM Forms com o Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md).

## Ativar o Analytics para o Forms adaptável no Sites {#Connect-Analytics-to-Adaptive-Forms-in-Sites}

Configurar análises para o formulário adaptável no AEM Sites ajuda a rastrear as interações do usuário e os envios de formulários no formulário na página Sites. Ao integrar facilmente a análise ao seu Forms do Sites, você obtém informações valiosas sobre o comportamento do usuário, taxas de conversão e áreas para melhoria no seu formulário.

### Pré-requisitos {#Prerequisites-to-connect-forms-analytics-to-sites}

Para conectar e habilitar o Analytics no Adaptive Forms para AEM Sites, você deve garantir que seu AEM Sites tenha um Adobe Analytics ativo.

### Conectar o Adaptive Forms no Sites para ativar o Analytics {#Connect-analytics-to-adaptive-forms}

Para conectar o Formulário adaptável em uma página do AEM Sites para ativar o Analytics, inclua a `customfooterlibs` biblioteca do cliente para a página do AEM Sites usando o Arquétipo AEM/Repositório Git e pipeline de implantação.

1. Abra o [Arquétipo do AEM Forms ou repositório Git clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) em um editor de texto. Por exemplo, Visual Studio Code.

1. Navegue até a página dos sites, onde o formulário adaptável existe. Por exemplo, neste projeto de demonstração, temos `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.

1. Copie o valor de `sling:resourceSuperType`. Por exemplo, o valor é `core/wcm/components/page/v3/page`.

   ![recurso sling](/help/forms/assets/slingresource.png){width="100%"}

1. Criar a estrutura semelhante no local `ui.apps/src/main/content/jcr_root/apps` igual a `core/wcm/components/page/v3/page`.

   ![estrutura de sobreposição](/help/forms/assets/overlaystructure.png){width="100%"}

1. Adicionar um `customfooterlibs.html` arquivo.

       &quot;
       // customheaderlibs.html
       &lt;sly data-sly-use.page=&quot;com.adobe.cq.wcm.core.components.models.Page&quot;>
       &lt;sly data-sly-test=&quot;${page.data &amp;&amp; page.dataLayerClientlibIncluded}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.commons.v1.datalayer&amp;#39;, async=true}&quot;>&lt;/sly>
       &lt;/sly>
       
       &quot;
   
   A variável `customfooterlibs.html` é usado para JavaScript.

1. [Executar o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) para implantar as alterações.

### Ativar regras do Form Analytics para o Forms no Sites {#bind-forms-analytics-rules-to-forms-in-sites}

1. Visite o **Coleta de dados do Adobe Experience Platform**.
1. Clique em **Tags** localizado no lado esquerdo.
1. Pesquise seu projeto com a ID do programa conforme mostrado na imagem abaixo, por exemplo, para o ambiente com URL `https://author-p45921-e175111-cmstg.adobeaemcloud.com/index.html`, a id do programa é `45921`.

   ![Pesquisar formulário na coleção de dados](/help/forms/assets/aep-data-collection.png){width="100%"}

1. Adicionar configuração para **Regras de formulário** e **Elementos de dados** conforme indicado a seguir:

#### Adicionar regras de formulário {#form-rules}

1. Selecione seu formulário e adicione **Nova propriedade** localizado no canto superior direito ou clique no formulário.
1. Na página de propriedades, clique em **Regras** e selecione eventos para o seu formulário. No exemplo de imagem abaixo, é **Eventos de formulário**.

   ![Pesquisar formulário na coleção de dados](/help/forms/assets/aep-form-event-properties.png){width="100%"}

1. Selecione todos os eventos do seu formulário e **copiar** que está localizado no painel superior direito.
1. Depois de copiar, um **Copiar regra** aparece onde você pesquisa a página Sites com a ID do projeto, para colar as Regras de formulário.

   ![Copiar-formulário-regras](/help/forms/assets/copy-form-rules.png){width="100%"}

1. Clique em **copiar** para colar as regras de formulário na página Sites.

#### Adicionar elementos de dados {#data-elements}

1. Selecione seu formulário e adicione **Nova propriedade** localizado no canto superior direito ou clique no formulário.
1. Na página de propriedades, clique em **Elementos de dados** e selecione eventos para o formulário.
1. Selecione todos os eventos do seu formulário e **copiar** localizado no painel superior direito.
1. Depois de copiar, um **Copiar regra** aparece onde você pesquisa a página Sites com a ID do projeto, para colar as Regras de formulário.
1. Clique em **copiar** para colar as regras de formulário na página Sites.

   ![Elementos de dados de formulário](/help/forms/assets/form-data-elements.png){width="100%"}

Depois de vincular as regras de Formulário e Sites por meio das etapas acima, execute as seguintes etapas para habilitar o Analytics para o seu Formulário adaptável na página Sites:

1. Clique em **Fluxo de publicação** à esquerda.
1. Clique em **Adicionar biblioteca** e digite o nome de sua preferência.
1. No **Ambiente** à direita, selecione **desenvolvimento**.
1. Clique em **Adicionar todos os recursos alterados**.
1. Clique em **Salvar e criar no desenvolvimento**.

![publicação para desenvolvimento](/help/forms/assets/publish-to-dev.png){width="100%"}


<!--

## Best Practices

1.	Verify that Adobe Analytics is enabled on all the forms activated for Adobe Analytics.

1.	Check the Adobe Analytics report periodically to gain insights into user behavior and form performance. For instance, you may set the cadence to 15 days or the period you prefer to choose for report analysis. This enables you to improve the forms enrollment experience.

1.	Enable Analytics for all or most of your forms for tracking and analyzing user interaction with your forms and to gain insights into visitor interactions and engagement.

1. Check your forms performance after you update your form fields or components.

1.	Share Analytics report with your peer groups for review, you can schedule your report for a later time.

-->