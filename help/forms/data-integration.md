---
title: Como conectar um banco de dados ao  [!DNL AEM Forms] as a Cloud Service?
description: Recupere e salve dados em serviços Web RESTful, serviços Web baseados em SOAP e serviços OData de um Formulário adaptável ou de um Fluxo de trabalho do AEM.
feature: Adaptive Forms, Form Data Model
role: Admin, User
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 2%

---

# Conectar o AEM Forms a um banco de dados {#aem-forms-data-integration}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/data-integration.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |



![Integração de dados](do-not-localize/data-integeration.png)

As infraestruturas corporativas incluem sistemas back-end distintos ou fontes de dados como bancos de dados, serviços da Web, serviços REST, serviços OData e soluções de CRM. Juntas, elas fazem um sistema de informações que serve dados para aplicativos corporativos para realizar negócios diários. Por outro lado, os aplicativos capturam os dados e os enviam de volta para atualizar as fontes de dados.

Quando você conecta o Formulário adaptável a um Banco de dados, ele requer integração com fontes de dados para buscar dados do cliente ao renderizar formulários. Há casos de uso em que os dados são obtidos de fontes de dados com base nas entradas do usuário no Adaptive Forms. Além disso, ao enviar um Formulário adaptável para um banco de dados, os dados do Formulário adaptável enviado podem ser gravados de volta para atualizar as respectivas fontes de dados.

Embora um sistema modular e distribuído tenha seus próprios benefícios, o desafio está na integração e criação de associações de dados entre as fontes de dados. A integração de dados é a chave para uma infraestrutura empresarial funcional e eficiente, com diferentes fontes de dados conectadas a aplicativos para troca de dados de negócios.

## Visão geral da integração de dados {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

A Integração de Dados do [!DNL AEM Forms] permite configurar e conectar fontes de dados diferentes ao [!DNL AEM Forms]. Ele fornece uma interface de usuário intuitiva para criar um esquema de representação de dados unificada de entidades e serviços comerciais em fontes de dados conectadas. A representação unificada é conhecida como modelo de dados de formulário (FDM), uma extensão do esquema JSON. As entidades em um Modelo de dados de formulário (FDM) são chamadas de objetos de modelo de dados. Um Modelo de dados de formulário (FDM) permite:

* Acesse objetos de modelo de dados, propriedades e serviços a partir de fontes de dados conectadas.
* Criar objetos e propriedades de modelo de dados personalizados
* Crie associações entre objetos de modelo de dados em e entre fontes de dados.
* Invoque serviços de objeto de modelo de dados para consultar ou gravar dados de e para fontes de dados.

Depois de criar um modelo de dados de formulário (FDM), você pode usá-lo para:

* Criar Forms adaptável com base em um modelo de dados de formulário (FDM)
* Preencher previamente o Forms adaptável a partir de fontes de dados configuradas
* Chamar serviços/operações de fonte de dados usando regras do Formulário adaptável
* Gravar dados do Formulário adaptável enviados nas fontes de dados

## Aplicabilidade e casos de uso

### Seguros

## O AEM Forms pode ser usado para aplicações de apólices de seguro?

Sim. O AEM Forms pode ser usado para criar formulários de inscrição de seguro digital que coletam informações do candidato, validam entradas e se integram a sistemas de subscrições de back-end.

## O AEM Forms oferece suporte à subscrições de workflows?

Sim, com fluxos de trabalho e integrações. O AEM Forms oferece suporte a processos orientados por fluxo de trabalho e integrações de back-end que permitem que os dados do aplicativo fluam para sistemas de tomada firme e decisão.

## O AEM Forms pode se integrar a sistemas centrais de seguros?

Sim. O AEM Forms oferece suporte à integração usando as APIs REST e SOAP, permitindo que ele se conecte a sistemas de administração de políticas, sistemas de gerenciamento de solicitações e CRMs.

## A AEM Forms pode gravar dados de formulário nos sistemas de seguros?

Sim. O AEM Forms oferece suporte à gravação de dados em sistemas de back-end como parte do envio de formulários e da execução de fluxos de trabalho.

## Introdução à integração de dados {#get-started-with-data-integration}

A primeira etapa para implementar a integração de dados para enviar o Formulário adaptável a um banco de dados é identificar e configurar fontes de dados que armazenam informações que você deseja usar no Adaptive Forms. Em seguida, você cria um Modelo de dados de formulário (FDM) que usa objetos de modelo de dados, propriedades e serviços de uma ou mais fontes de dados. Você pode criar o Adaptive Forms com base em um Modelo de dados de formulário (FDM) em que os campos do Formulário adaptável estão vinculados às respectivas propriedades da fonte de dados.

O [!DNL AEM Forms] também permite criar um Modelo de Dados de Formulário (FDM) independente das fontes de dados e associar ou associar objetos e propriedades de modelo de dados no Modelo de Dados de Formulário (FDM) à fonte de dados posteriormente. Isso elimina quaisquer dependências nas fontes de dados enquanto você trabalha em um modelo de dados de formulário (FDM).

Revise o seguinte para começar, entender e implementar a integração de dados:

* [Configurar fontes de dados](configure-data-sources.md)
* [Criar modelo de dados de formulário (FDM)](create-form-data-models.md)
* [Trabalhar com o modelo de dados de formulário (FDM)](work-with-form-data-model.md)
* [Usar o modelo de dados de formulário (FDM)](using-form-data-model.md)

<!--

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] does not support relational database.

-->