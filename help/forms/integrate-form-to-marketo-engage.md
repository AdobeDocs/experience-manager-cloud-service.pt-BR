---
title: Como integrar o Marketo Engage com o AEM Forms?
description: Saiba como integrar sua instância do Marketo Engage ao AEM Forms.
keywords: Como conectar uma instância do Marketo com o formulário? , Conectar um formulário ao Marketo, Integrar um formulário ao Marketo Engage, Integrar um formulário adaptável a uma instância do Marketo.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 74cd25f9-1ee1-4f3f-8e02-8714071e7c86
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 3%

---

# Integrar o Marketo Engage com o AEM Forms

<span class="preview"> O recurso está disponível no programa dos primeiros usuários. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

Integrar o AEM Forms com o [Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home) permite que os usuários aproveitem os recursos do Marketo Engage para criar uma lógica de negócios a partir de dados capturados e automatizar fluxos de trabalho, incluindo campanhas inteligentes e automação de email. O formulário configurado pode enviar dados capturados para processamento pela Marketo Engage.

## Vantagens de integrar o Marketo Engage com formulários

Abaixo estão algumas vantagens de conectar um formulário do AEM com o Adobe Marketo Engage:

* **Integração simplificada**: a conexão de formulários com o Marketo Engage elimina a necessidade de criar um modelo de dados de formulário separado. O processo de integração é simples e fácil de usar.
* **Captura de dados automatizada**: ajuda a capturar automaticamente envios de formulários e armazená-los no Marketo, eliminando a entrada manual de dados e reduzindo erros.

* **Gerenciamento de clientes potenciais**: ele simplifica os processos de gerenciamento de clientes potenciais, integrando envios de formulários diretamente ao seu banco de dados de marketing, permitindo um melhor rastreamento e promoção de clientes potenciais.

* **Desempenho de campanha aprimorado**: ele usa dados de formulário para analisar e otimizar campanhas de marketing, aprimorando o desempenho geral e o retorno sobre o investimento (ROI).

* **Analytics e relatórios**: ajudam a obter acesso a ferramentas de análise e relatórios robustas, como o Munchkin, no Marketo para medir a eficácia de formulários e campanhas.

* **Automação de acompanhamento**: ajuda a automatizar emails de acompanhamento e fluxos de trabalho acionados por envios de formulários, garantindo a comunicação oportuna com clientes potenciais.

## Principais benefícios do uso do AEM Forms em relação às soluções de formulários alternativos

A tabela abaixo descreve os poucos motivos para escolher a AEM Forms em vez de outras soluções alternativas de formulários:

| **Recurso** | **AEM Forms** | **Outras Soluções de Formulário** |
|-------------------------------------|----------------------------------------------------------------------|-----------------------------------------------------------|
| **Personalizações** | Permite adicionar funções personalizadas específicas, ajustar ações de formulário e modificar comportamentos de campo para aprimorar interações de formulário, fluxos de trabalho complexos | Sem suporte para personalização |
| **Editor de regras** | Oferece suporte a um Editor de regras incorporado para adicionar lógica e condições. | Não há suporte para o Editor de regras |
| **Opções de layout** | Suporta várias opções de layout | Opções de layout limitadas |
| **Preencher Serviço** | Oferece um serviço de Preenchimento prévio para preencher automaticamente os dados do formulário. | Nenhum serviço de Preenchimento prévio disponível |
| **Incorporação no Sites** | Pode ser incorporado ao Sites usando o iFrame | Não pode ser incorporado ao Sites usando o iFrame |
| **Facilidade de Integração com Sites** | Não é necessário aprendizado adicional; o AEM Forms usa as mesmas habilidades do Sites | Aprendizado adicional pode ser necessário |
| **Envio de dados** | Pode enviar dados para várias plataformas e oferece vários conectores, como Conectar-se ao SharePoint, Conectar-se ao OneDrive, Conectar-se ao Salesforce e muito mais. | Podem enviar dados para conectores limitados, por exemplo, para o Salesforce |

## Considerações para a integração do Marketo Engage com formulários

Algumas considerações sobre a integração do Marketo Engage com o AEM Forms:

* O AEM só oferece suporte ao banco de dados People(Leads) entre os vários bancos de dados do Marketo.
* O Marketo permite a [criação de 10 objetos personalizados](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields) como objetos definidos pelo usuário para armazenar dados especializados além dos campos padrão em clientes potenciais, dando suporte a necessidades comerciais exclusivas.
* O AEM pode acessar objetos personalizados somente se eles estiverem associados ao banco de dados de clientes potenciais

## Pré-requisitos para integrar o Marketo Engage com formulários

Abaixo estão os pré-requisitos para conectar o Marketo Engage ao AEM Forms:

* Uma licença válida do Adobe Marketo Engage
* Uma instância de trabalho do Marketo Engage para [recuperar a ID do Cliente e o Segredo do Cliente](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api) para criar uma configuração de nuvem.

## Criar configuração do Cloud Service para conectar o AEM Forms (Adaptive Forms) ao Marketo Engage

![Fluxo de trabalho](/help/forms/assets/workflow-marketo-1.png)

>[!VIDEO](https://video.tv.adobe.com/v/3442865/engage-marketo-aem-forms-aem)

<span> Este vídeo se aplica somente aos Componentes principais. Para Componentes UE/Foundation, consulte o artigo.</span>

A configuração da nuvem conecta a instância do Experience Manager à instância do Adobe Marketo Engage. Execute as seguintes etapas para criar uma configuração da nuvem do Marketo Engage:

1. Vá para **Ferramentas** > **Serviços na Nuvem** > **Marketo Engage**.

   ![Marketo Engage](/help/forms/assets/marketo-engage.png)

1. Abra uma pasta para hospedar a configuração e clique em **Criar**. A janela **Criar configuração do Marketo Engage** é exibida.

   >[!NOTE]
   >
   > Você também pode [definir a pasta de configurações do serviço de nuvem](/help/forms/configure-data-sources.md#configure-folder-for-cloud-service-configurations).

1. Especifique o **Título** da configuração e as credenciais para se conectar ao serviço. Você pode recuperar as credenciais de autenticação do painel do Adobe Marketo Engage:

   * A **ID do Cliente** e o **Segredo do Cliente** estão disponíveis em **Admin** > **Integração** > **LaunchPoint** selecionando o serviço personalizado e clicando em **Exibir Detalhes**.
   * A **URL da Identidade** está disponível em **Admin** > **Integração** > **Serviços Web** como **Identidade** na seção **API REST**.

1. Clique em **Conectar**.  Em uma conexão bem-sucedida, a mensagem `Authentication Successful` é exibida.
1. Clique em **[!UICONTROL Criar]** para salvar as definições de configuração da nuvem.

![Configuração de nuvem do Marketo Engage](/help/forms/assets/marketo-engage-cloud-configuration.png)

Agora você pode usar a configuração do serviço de nuvem criado para conectar a fonte de dados do Marketo Engage a um Formulário adaptável.

## Próxima etapa

Você criou a configuração do Cloud Service para integrar o Adobe Marketo Engage ao AEM Forms. Agora, é possível integrar:

* [Novo formulário adaptável com o Marketo Engage](/help/forms/integrate-adaptive-form-with-marketo-engage.md)
* [Formulário adaptável existente com o Marketo Engage](/help/forms/use-marketo-engage-data-source-in-form.md)

## Artigos relacionados

{{af-submit-action}}

## Consulte também:

{{marketo-engage-see-also}}
