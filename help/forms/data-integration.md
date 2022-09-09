---
title: Como conectar um banco de dados a [!DNL AEM Forms] as a Cloud Service?
seo-title: AEM Forms Data Integration
description: Você pode recuperar e salvar dados em serviços da Web RESTful, serviços da Web baseados em SOAP e serviços OData de [!DNL AEM Forms] as a Cloud Service. O serviço fornece uma ferramenta dedicada para recuperar, testar, validar e enviar dados para vários tipos de fontes de dados.
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---

# Conectar suas fontes de dados ao Cloud Service {#aem-forms-data-integration}

![Integração de dados](do-not-localize/data-integeration.png)

As infraestruturas empresariais incluem sistemas de back-end ou fontes de dados diferentes, como bancos de dados, serviços da Web, serviços REST, serviços OData e soluções CRM. Juntos, eles fazem um sistema de informações que fornece dados para aplicativos corporativos para executar negócios diários. Por outro lado, os aplicativos capturam dados e os enviam de volta para atualizar fontes de dados.

[!DNL AEM Forms] aplicativos como o Adaptive Forms e comunicações interativas exigem integração com fontes de dados para buscar dados do cliente enquanto renderiza formulários e cria comunicações interativas. Há casos de uso em que os dados são obtidos de fontes de dados com base nas entradas do usuário no Adaptive Forms. Além disso, os dados enviados do Formulário adaptativo podem ser gravados novamente para atualizar as respectivas fontes de dados.

Embora um sistema modular distribuído tenha seus próprios benefícios, o desafio é integrar e criar associações de dados em todas as fontes de dados. A integração de dados é a chave para uma infraestrutura empresarial funcional e eficiente, com diferentes fontes de dados conectadas a aplicativos para troca de dados comerciais.

## Visão geral da integração de dados {#data-integration-overview}

![aem-forms-data-integeration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] A integração de dados permite configurar e conectar diferentes fontes de dados com [!DNL AEM Forms]. Ele fornece uma interface de usuário intuitiva para criar um esquema de representação de dados unificado de entidades e serviços de negócios em fontes de dados conectadas. A representação unificada é conhecida como um modelo de dados de formulário, uma extensão do esquema JSON. As entidades em um Modelo de dados de formulário são chamadas de objetos de modelo de dados. Um Modelo de dados de formulário permite:

* Acesse objetos, propriedades e serviços do modelo de dados de fontes de dados conectadas.
* Criar objetos e propriedades personalizados do modelo de dados
* Criar associações entre objetos de modelo de dados dentro e entre fontes de dados.
* Chame os serviços de objeto do modelo de dados para consultar ou gravar dados de e para fontes de dados.

Depois de criar um modelo de dados de formulário, você pode usá-lo em vários fluxos de trabalho de Adaptive Form e de comunicações interativas, como:

* Criar Forms adaptável e comunicações interativas com base no modelo de dados de formulário
* Preencher previamente o Adaptive Forms e as comunicações interativas a partir de fontes de dados configuradas
* Chamar serviços/operações de fonte de dados usando regras de formulário adaptável
* Gravar dados do formulário adaptativo enviados em fontes de dados

## Introdução à integração de dados {#get-started-with-data-integration}

A primeira etapa para implementar a integração de dados é identificar e configurar fontes de dados que armazenam informações que você deseja aproveitar no Adaptive Forms e em casos de uso de comunicações interativas. Em seguida, crie um Modelo de dados de formulário que use objetos, propriedades e serviços do modelo de dados de uma ou mais fontes de dados. É possível criar comunicações adaptativas e interativas com base em um Modelo de dados de formulário em que os campos do Formulário adaptável ou os espaços reservados em comunicações interativas estão vinculados às respectivas propriedades de fonte de dados.

[!DNL AEM Forms] O também permite criar um Modelo de dados de formulário independente das fontes de dados e associar ou vincular objetos e propriedades do modelo de dados no Modelo de dados de formulário com a fonte de dados posteriormente. Ele elimina qualquer dependência das fontes de dados enquanto você trabalha em um modelo de dados de formulário.

Analise o seguinte para começar, entender e implementar a integração de dados.

* [Configurar fontes de dados](configure-data-sources.md)
* [Criar modelo de dados de formulário](create-form-data-models.md)
* [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md)
* [Usar modelo de dados de formulário](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] não suporta banco de dados relacional.
