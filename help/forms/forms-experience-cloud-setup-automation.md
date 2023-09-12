---
title: Ativar o Adobe Analytics para um formulário adaptável usando a automação de configuração do Experience Cloud
description: A Automação de configuração do Experience Cloud ajuda a conectar o Adobe Analytics a um Formulário adaptável. Ele ajuda a rastrear e analisar a interação do usuário com um Formulário adaptável, oferecendo insights sobre as interações e o envolvimento do visitante.
source-git-commit: b44b54a88b87dc391dfeb51fb8b83095c274bd38
workflow-type: tm+mt
source-wordcount: '1030'
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

![Relatório do Analytics](assets/analytics-report.png)


Para obter informações detalhadas sobre cada métrica, visite [Visualização e noções básicas sobre relatórios do AEM Forms Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Pré-requisitos {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

A Automação de configuração do Experience Cloud no Adobe Experience Manager Forms requer um **Licença do Adobe Analytics**, **Coleta de dados (antigo Adobe Launch)** para gerenciar scripts de rastreamento e a integração com a **Experience Platform Launch (API)** para uma agregação de dados e geração de insights simplificadas.

Se você tiver uma licença ativa para a Automação de configuração do Experience Cloud, Adobe Analytics e API Experience Platform Launch, deverá verificar a disponibilidade delas no console do desenvolvedor.

Para verificar se os itens acima estão disponíveis para o seu ambiente as a Cloud Service do Forms, visite a [console do desenvolvedor](https://developer.adobe.com/console/projects), navegue até o projeto e pesquise seu projeto com a ID do programa, por exemplo, para o ambiente com o URL `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`, a id do programa é `p45913-e175111`. Verifique se Experience Cloud Setup Automation, Adobe Analytics e Experience Platform Launch API estão listados. Se estiverem listados, você poderá ativar o Adobe Analytics para o seu Forms adaptável.

![Integração de pré-requisito do Forms Analytics](assets/analytics-aem.png)

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

![Análise integrada do AEM](assets/analytics-aem-integrated.png)

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

   ![Exibir Relatório](assets/activ-aa.png)

1. Clique em **Adobe Analytics** para exibir seu relatório e analisar dados de desempenho.

Para conectar um formulário adaptável ao Adobe Analytics usando o método manual, visite [Integrar o AEM Forms com o Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md).
