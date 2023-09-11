---
title: Exibição e noções básicas dos relatórios de análise do Adaptive Forms
description: O Forms adaptável integra-se perfeitamente ao Adobe Analytics para capturar e rastrear métricas de desempenho para seus formulários e documentos publicados.
topic-tags: develop
feature: Adaptive Forms
role: User
level: Intermediate
source-git-commit: 96b3986f73ab71bad02b00ddc699aeecd498aebd
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---


# Exibição e noções básicas dos relatórios de análise do Adaptive Forms {#viewing-and-understanding-aem-forms-analytics-reports}

No cenário de rápida evolução da análise digital, manter-se atualizado com as tendências globais é fundamental para tomar decisões informadas e otimizar as experiências digitais. Para resolver isso, o Adaptive Forms integra-se perfeitamente ao Adobe Analytics para capturar e rastrear métricas de desempenho para seus formulários e documentos publicados. O objetivo por trás da análise dessas métricas é tomar decisões orientadas por dados, usando métricas e análises para melhorar a usabilidade e a eficácia dos formulários.

Ao capturar e rastrear os principais indicadores de desempenho, as empresas podem identificar áreas de aprimoramento, otimizar as experiências do usuário e, em última análise, gerar melhores resultados para criar experiências excepcionais para os clientes.

## Configurar Adobe Analytics para Forms adaptável {#setup-adobe-analytics-to-aem-forms}

Para o relatório do AEM Forms Analytics, primeiro você integra o Adobe Analytics ao AEM Forms por meio da Automação de configuração do Experience Cloud. A Automação de configuração do Experience Cloud no Adaptive Forms exige uma licença do Adobe Analytics, Coleção de dados (antigo Adobe Launch) para gerenciar scripts de rastreamento e integração com a API do Experience Platform Launch para agilizar a agregação de dados e a geração de insights. Visita [Ativar o Adobe Analytics para um formulário adaptável usando a automação de configuração do Experience Cloud](/help/forms/forms-experience-cloud-setup-automation.md) para obter informações completas sobre a configuração.

## Exibir o relatório adaptável do Forms Adobe Analytics {#view-adobe-analytics-report}

1. Na instância do AEM, acesse **[!UICONTROL Forms]** >> **[!UICONTROL Forms e Documento]**.
1. Selecione o formulário e veja que o Adobe Analytics está integrado, como mostrado à esquerda, à Forms ativada para o Adobe Analytics.

   ![Exibir Relatório](assets/activ-aa.png)

1. Clique em **Adobe Analytics** para exibir seu relatório e analisar dados de desempenho.

## Noções básicas sobre o relatório de análise adaptável do Forms {#understanding-aem-forms-analytics-reports}

O Adobe Analytics oferece uma ampla variedade de métricas de desempenho adaptáveis do Forms projetadas para fornecer insights valiosos sobre o uso do formulário. Essas métricas são:

### **Como está o desempenho do Adaptive Forms?** {#how-your-adaptive-form-is-performing}

Ele tem as métricas Representações de formulário, Envios de formulário, Erros de validação e Visitantes únicos, que permitem avaliar o uso e a eficácia de seus formulários:

* **Representações de formulário**: as representações de formulário revelam o número de vezes que o formulário foi renderizado ou aberto.

* **Envios de formulários**: os envios de formulário indicam o número de vezes que os formulários adaptáveis são concluídos com êxito e enviados pelos usuários.

* **Erros de validação**: Erro de validação exibe o número total de erros relacionados à validação que ocorreram nos campos dos formulários.

* **Visitantes únicos**: visitantes únicos representam o número de vezes que o formulário é renderizado por um visitante. Para obter mais informações sobre visitantes únicos, consulte [Visitantes únicos, Visitas e comportamento do cliente](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html).

  ![Desempenho do Forms](assets/forms-performance.png)

### **Visitantes de seus formulários** {#visitors-to-your-forms}

Ele ajuda a obter insights valiosos sobre a atividade de visitantes em seus formulários:

* **Visitas e envios**: descreve a frequência de visitas aos seus formulários em um intervalo de datas e o número correspondente de envios de formulários, para obter mais informações sobre esse clique [Visitas](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html).
* **Visitantes únicos e seu total de visitas**: faz a distinção entre usuários novos e recorrentes. Por exemplo, um visitante pode chegar ao seu site todos os dias por um mês, mas ainda assim contam como um visitante único exclusivo. Visita [Visitantes únicos](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html) para obter informações detalhadas.

  ![Visitantes do Forms](assets/forms-visitors.png)

### **Tipo de dispositivo** {#device-type}

O tipo de dispositivo ajuda a identificar o tipo de dispositivo usado para acessar seus formulários. Ele categoriza o tipo de dispositivo como Tipo de dispositivo móvel. Por exemplo, nesse caso, é o Tipo de dispositivo móvel: Outro e Tipo de dispositivo móvel: Telefone celular. Os vários tipos de dispositivos móveis incluem celular, tablet, reprodutor de mídia, console de jogos e muito mais.

![Tipo de dispositivo](assets/device-type.png)

### **Discriminação geográfica** {#geographical-breakdown}

Ela mostra o local de onde as Forms são acessadas. Ela fornece informações específicas da região sobre usuários de formulário, por exemplo, você pode ver que as informações específicas da região sobre um usuário de formulário são da Índia, conforme mostrado na imagem.

![discriminação geográfica](assets/geographical-breakdown.png)

### **Principais fontes de tráfego e formulários populares** {#top-sources-of-traffic-and-popular-forms}

Isso ajuda a identificar a fonte primária ou o link de onde seus formulários são referenciados. Por exemplo, na imagem fornecida abaixo, você vê instâncias de pesquisa para seus formulários adaptáveis, onde 18,9% são **Digitado/Marcado**, 70,49% com base em **Mecanismos de pesquisa** e 24% são de **Outros sites**. Você pode definir itens de dimensão com base nos seus requisitos. Além disso, você pode classificar quais são os formulários mais visitados ou populares.

![Sites indicados](assets/referred-sites.png)

### **Atividade do usuário nos principais formulários** {#user-activity-on-top-forms}

Uma visualização abrangente do engajamento do usuário com visitas de campo, representações de formulário, erros de validação, formulários abandonados e envios de formulário fornece insights sobre os formulários que estão mais ativos. Na imagem apresentada abaixo, você vê que o Formulário de aplicação é o mais ativo baseado nas métricas do Evento de formulário.

![user-activity](assets/user-activity.png)

### **Linha do tempo gasto em formulários** {#timeline-for-time-spent-on-forms}

Os usuários gastam em seus formulários ao longo do tempo, o que ajuda a identificar os padrões de engajamento.

![tempo gasto com formulários](assets/time-spent-on-forms.png)

### **Áreas em que os visitantes precisam de assistência para preencher o formulário** {#areas-requiring-assistance}

Métricas como exibições de ajuda, erros de validação e visitas de campo revelam onde os usuários precisam de assistência ou como podemos rastrear erros em campos. Por exemplo, na imagem abaixo, é possível ver isso em um formulário com campos como **Nome completo**, **Número de telefone**, **DoB**. A variável **Nome completo** O campo tem 12 visitas, das 12 visitas, 8 visitas têm erro de validação e 1 clicou no ícone de ajuda para obter uma visualização da ajuda sobre este campo. É possível ver os dados de métricas de outros campos de formulário.

![áreas de assistência](assets/assisting-areas.png)

### **O último campo de formulário que os visitantes visualizaram antes de abandonarem o formulário** {#last-form-field-that-visitors-viewed}

Ele ajuda a analisar os campos de formulário nos quais os usuários passaram tempo antes de abandonar o formulário. Por exemplo, na imagem apresentada abaixo, de 5 formulários abandonados, 2 foram deixados no campo **Nome completo**, 2 à esquerda no campo **Número de telefone**, e 1 esquerda no campo **Entrada de texto**.

![visitantes de campo](assets/field-visitors.png)