---
title: Referência de temas, modelos e modelos de dados de formulário
seo-title: Reference Themes, Templates, and Form Data models
description: A AEM Forms fornece temas de formulários adaptáveis, modelos e modelos de dados de formulários que você pode obter da Distribuição de software
seo-description: AEM Forms provides adaptive forms themes, templates, and form data models that you can get from Software Distribution
source-git-commit: 196a2f221c637d58ea6642177f530f158888efe0
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# Referência de temas, modelos e modelos de dados de formulário {#reference-themes-templates-and-data-models}

O AEM Forms as a Cloud Service fornece vários temas de referência, modelos e modelos de dados de formulário para ajudá-lo a começar rapidamente a criar o Adaptive Forms. Você pode baixar o [pacote de conteúdo de referência do portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) e use o [Gerenciador de pacotes](/help/implementing/developing/tools/package-manager.md) para instalar o [pacote de conteúdo de referência](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) no ambiente de produção, desenvolvimento ou desenvolvimento local para obter esses ativos de referência para o ambiente.

Os temas, modelos e modelos de dados de formulário incluídos no pacote de conteúdo de referência são:


| Temas | Modelos | Modelos de dados de formulário |
---------|----------|---------
| Tela 3.0 | Básico | Microsoft Dynamics 365 |
| Tranquilo | Em branco | Salesforce |
| Urbane |  |  |
| Ultramarina |  |  |
| Beril |  |  |
| Cuidados médicos |  |  |
| FSI |  |  |

## Temas de Referência {#reference-themes}

[Temas](/help/forms/themes.md) permite criar estilos em seus formulários sem conhecimento profundo de CSS. Você pode obter os seguintes temas instalando o [Pacote de conteúdo de referência](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Beril
* Tela 3.0
* Tranquilo
* Urbane
* Ultramarina
* Cuidados médicos
* FSI (Serviços financeiros e seguros)

Cada tema contém um estilo exclusivo e elegante que pode ser usado para criar formulários adaptáveis encantadores para os usuários. Ele contém um estilo exclusivo para seletores como painel, caixa de texto, caixa numérica, botão de opção, tabela e switch. As estilos nesses temas baseiam-se em requisitos. Por exemplo, em um cenário específico, você precisa de um tema minimalista com fontes limpas. O tema da liberdade permite-nos alcançar esse aspecto.

![Temas de Referência](assets/ref-themes.png)

Os temas incluídos neste pacote são responsivos e o estilo nesses temas é definido para exibições móveis e para desktop. A maioria dos navegadores modernos em vários dispositivos pode renderizar formulários aplicados com um desses temas sem complicações.

Para obter mais informações sobre como instalar o pacote, consulte [Como trabalhar com pacotes](/help/implementing/developing/tools/package-manager.md).

## Beril {#beryl}

O tema Beryl enfatiza o uso de imagem de fundo, transparência e ícones grandes e planos. Na captura de tela abaixo, você pode ver a aparência do tema Beryl e como ele pode melhorar o estilo de seu formulário.

![Tema de berilo](assets/beryl.png)

## Tela 3.0 {#canvas}

O Canvas 3.0 é o tema padrão do Adaptive Forms e enfatiza o uso de cores básicas, transparência e ícones simples. Na captura de tela abaixo, você pode ver a aparência do tema Canvas 3.0.

![Tema de berilo](assets/canvas.png)


## Tranquilo {#tranquil}

O tema tranquilo fornece tons claros e escuros do esquema de cor Tranquilo para destacar diferentes componentes de um formulário. Por exemplo, botões de opção, painéis e guias recebem um tom diferente de verde.

![Tema do tranquilo](assets/tranquil.png)


## Urbane {#urbane}

O tema Urbane enfatiza uma aparência minimalista e funcional para seu formulário. Ao aplicar o tema Urbane ao seu formulário, você pode ver que os componentes são planos. Os painéis obtêm contornos finos para criar uma aparência moderna.

![Tema de Urbana](assets/urbane.png)


## Ultramarina {#ultramarine}

O tema ultramarine usa tons azuis profundos para realçar componentes como guias, painéis, caixas de texto e botões.

![Tema ultramarino](assets/ultramarine.png)

## Cuidados médicos {#healthcare}

O tema de assistência médica utiliza tons verdes profundos para realçar componentes como guias, painéis, caixas de texto e botões.

![Tema FSI](assets/healthcare.png)


## FSI (Serviços financeiros e seguros)

O tema FSI enfatiza uma aparência minimalista e funcional para seu formulário. Ao aplicar o tema FSI ao formulário, é possível ver que os componentes do painel são amarelos.

![Tema FSI](assets/fsi.png)

## Modelos de referência {#reference-templates}


[Modelos](/help/forms/themes.md) permitem definir a estrutura, o conteúdo e as ações iniciais dos formulários. Você pode obter os seguintes modelos instalando o [Pacote de conteúdo de referência](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Básico
* Em branco

O modelo básico ajuda você a criar rapidamente um formulário de inscrição. Também é possível usá-lo para visualizar a funcionalidade dos componentes básicos do Adaptive Forms. Ele fornece um layout de assistente para a apresentação seção por seção dos dados. Use o modelo em branco para começar a criar um formulário adaptável em uma tela em branco.


## Modelos de dados do formulário de referência {#reference-models}

O Adaptive Forms pode então interagir com os servidores Microsoft Dynamics 365 e Salesforce para permitir fluxos de trabalho de negócios. Por exemplo:

* Grave dados no Microsoft Dynamics 365 e no Salesforce no envio do formulário adaptável.
* Escreva dados no Microsoft Dynamics 365 e no Salesforce por meio de entidades personalizadas definidas no Modelo de dados de formulário e vice-versa.
* Consulte o servidor Microsoft Dynamics 365 e Salesforce para obter dados e pré-preencher o Adaptive Forms.
* Leia dados do servidor Microsoft Dynamics 365 e Salesforce.

Você pode obter os seguintes Modelos de dados de formulário instalando o [Pacote de conteúdo de referência](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Microsoft® Dynamics 365
* Salesforce

Para obter informações sobre como usar esses modelos, consulte [Configurar os serviços em nuvem do Microsoft Dynamics 365 e Salesforce](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en#configure-dynamics-cloud-service)






