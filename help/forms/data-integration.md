---
title: Como conectar um banco de dados ao [!DNL AEM Forms] as a Cloud Service?
seo-title: AEM Forms Data Integration
description: Você pode recuperar e salvar dados em serviços Web RESTful, serviços Web baseados em SOAP e serviços OData de [!DNL AEM Forms] as a Cloud Service. O serviço fornece uma ferramenta dedicada para recuperar, testar, validar e enviar dados para vários tipos de fontes de dados.
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: b6dcb6308d1f4af7a002671f797db766e5cfe9b5
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 3%

---

# Conectar suas fontes de dados ao Cloud Service {#aem-forms-data-integration}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/data-integration.html) |
| AEM as a Cloud Service | Este artigo |


![Integração de dados](do-not-localize/data-integeration.png)

As infraestruturas corporativas incluem sistemas back-end distintos ou fontes de dados como bancos de dados, serviços da Web, serviços REST, serviços OData e soluções de CRM. Juntas, elas fazem um sistema de informações que serve dados para aplicativos corporativos para realizar negócios diários. Por outro lado, os aplicativos capturam os dados e os enviam de volta para atualizar as fontes de dados.

[!DNL AEM Forms] aplicativos como o Adaptive Forms e as comunicações interativas exigem integração com fontes de dados para buscar dados do cliente e, ao mesmo tempo, renderizar formulários e criar comunicações interativas. Há casos de uso em que os dados são obtidos de fontes de dados com base nas entradas do usuário no Adaptive Forms. Além disso, os dados do Formulário adaptável enviado podem ser regravados para atualizar as respectivas fontes de dados.

Embora um sistema modular e distribuído tenha seus próprios benefícios, o desafio está na integração e criação de associações de dados entre as fontes de dados. A integração de dados é a chave para uma infraestrutura empresarial funcional e eficiente, com diferentes fontes de dados conectadas a aplicativos para troca de dados de negócios.

## Visão geral da integração de dados {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] A Integração de dados permite configurar e conectar diferentes fontes de dados com o [!DNL AEM Forms]. Ele fornece uma interface de usuário intuitiva para criar um esquema de representação de dados unificada de entidades e serviços comerciais em fontes de dados conectadas. A representação unificada é conhecida como modelo de dados de formulário, uma extensão do esquema JSON. As entidades em um Modelo de dados de formulário são chamadas de objetos de modelo de dados. Um modelo de dados de formulário permite:

* Acesse objetos de modelo de dados, propriedades e serviços a partir de fontes de dados conectadas.
* Criar objetos e propriedades de modelo de dados personalizados
* Crie associações entre objetos de modelo de dados em e entre fontes de dados.
* Invoque serviços de objeto de modelo de dados para consultar ou gravar dados de e para fontes de dados.

Depois de criar um modelo de dados de formulário, você pode usá-lo em vários formulários adaptáveis e workflows de comunicações interativas, como:

* Crie comunicações interativas e Forms adaptáveis com base no modelo de dados de formulário
* Preencher previamente o Forms adaptável e as comunicações interativas de fontes de dados configuradas
* Chamar serviços/operações de fonte de dados usando regras do Formulário adaptável
* Gravar dados do Formulário adaptável enviados nas fontes de dados

## Introdução à integração de dados {#get-started-with-data-integration}

A primeira etapa para implementar a integração de dados é identificar e configurar as fontes de dados que armazenam as informações que você deseja usar nos casos de uso do Adaptive Forms e das comunicações interativas. Em seguida, você cria um Modelo de dados de formulário que usa objetos de modelo de dados, propriedades e serviços de uma ou mais fontes de dados. Você pode criar comunicações adaptáveis do Forms e interativas com base em um Modelo de dados de formulário em que os campos ou espaços reservados do Formulário adaptável em comunicações interativas são vinculados às respectivas propriedades da fonte de dados.

[!DNL AEM Forms] O também permite criar um modelo de dados de formulário independente das fontes de dados e associar ou vincular objetos de modelo de dados e propriedades no modelo de dados de formulário à fonte de dados posteriormente. Ele elimina qualquer dependência em fontes de dados enquanto você trabalha em um modelo de dados de formulário.

Analise o seguinte para começar, entender e implementar a integração de dados.

* [Configurar fontes de dados](configure-data-sources.md)
* [Criar modelo de dados de formulário](create-form-data-models.md)
* [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md)
* [Usar modelo de dados de formulário](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] não dá suporte a banco de dados relacional.
