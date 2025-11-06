---
title: Conectar o AEM Forms com o Adobe Experience Platform (AEP) | Guia de integração de dados
description: Saiba como integrar o AEM Forms com o Adobe Experience Platform para aproveitar os perfis do cliente, enviar dados de formulário e criar experiências personalizadas. Guia passo a passo.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
exl-id: b0eb19d3-0297-4583-8471-edbb7257ded4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2047'
ht-degree: 1%

---

# Integração do AEM Forms com o Adobe Experience Platform (AEP) {#aem-forms-aep-integration}

<span class="preview"> A capacidade de conectar o Adaptive Forms (AEM Forms) ao Adobe Experience Platform (AEP) está no programa de acesso antecipado. Para solicitar acesso ao recurso, basta enviar um email de seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D). Você também pode visitar a página <a href="/help/forms/early-access-ea-features.md">Programa de Acesso Antecipado</a> para descobrir todas as inovações e recursos disponíveis. . </span>

## Visão geral {#overview}

Você pode conectar o AEM Forms com o Adobe Experience Platform para transformar suas experiências de formulário. Essa integração avançada permite que as organizações aproveitem perfis de clientes em tempo real para experiências de formulário personalizadas, simplifiquem o **envio de dados do AEM Forms para o Experience Platform** e criem registros unificados do cliente em todo o ecossistema da Adobe. Conectando seus formulários adaptáveis aos recursos robustos de gerenciamento de dados do Experience Platform, você pode criar experiências mais relevantes e melhorar as taxas de conversão, mantendo uma única fonte da verdade para os dados do cliente.

### O que é o AEM Forms Connector for Adobe Experience Platform (AEP)? {#what-is-connector}

O AEM Forms Connector for Adobe Experience Platform (AEP) é um conector pronto para uso (OOTB) fornecido pela AEM Forms que permite a integração perfeita entre o AEM Forms e o Adobe Experience Platform (AEP). Essa integração permite criar formulários usando esquemas XDM disponíveis no AEP e enviar dados de volta para o AEP para fins de personalização e hidratação de perfil.

## Por que conectar o AEM Forms ao Adobe Experience Platform (AEP)? {#benefits}

A conexão do Adaptive Forms com o Adobe Experience Platform oferece vantagens significativas para sua organização e seus clientes:

* **Perfis de clientes unificados** - Enriqueça os perfis de clientes com dados de envio de formulário, criando uma visão abrangente das interações e preferências do cliente
* **Experiências de formulário personalizadas** - Aproveite os dados de perfil existentes para preencher previamente campos e personalizar formulários com base em informações de clientes conhecidos
* **Coleta de dados simplificada** - Capture dados de formulário diretamente nos conjuntos de dados do AEP sem criar conectores personalizados ou código de integração
* **Ativação de dados em tempo real** - Envie dados de envio de formulário para outros aplicativos da Adobe por meio do Real-Time CDP para ativação imediata
* **Gerenciamento simplificado de conformidade** - gerencie políticas de consentimento e governança de dados de forma centralizada por meio da AEP
* **Tempo de desenvolvimento reduzido** - Elimine o trabalho de integração personalizada com um conector pré-criado que siga as práticas recomendadas
* **Enriquecimento do perfil do cliente com dados de formulário** - Atualize e aprimore automaticamente os perfis do cliente com cada envio de formulário, criando insights mais avançados do cliente

## Principais recursos {#key-features}

* Criar formulários usando esquemas XDM do AEP
* Enviar dados de formulário à AEP para personalização
* Suporte para assimilação de dados por transmissão
* Habilitar hidratação de perfil para experiências aprimoradas do usuário
* Integração com o sistema de perfis da AEP
* Integração do esquema XDM com formulários adaptáveis para uma coleta de dados padronizada
* Conexão de transmissão do AEP para formulários, permitindo o processamento de dados em tempo real

O vídeo abaixo fornece um guia passo a passo sobre os pré-requisitos (como criar um esquema, configurar dados e autenticação) e mostra como criar e conectar o Adaptive Forms ao Adobe Experience Platform (AEP)

>[!VIDEO](https://video.tv.adobe.com/v/3457850/)

<span> Este vídeo se aplica somente aos Componentes principais. Para Componentes UE/Foundation, consulte o artigo.</span>

## Pré-requisitos {#prerequisites}

Antes de configurar o Conector do AEP no AEM Forms, verifique se você concluiu o seguinte no Adobe Experience Platform:

1. Configuração do esquema
   * [Criar um esquema XDM](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/tutorials/create-schema-ui)
   * [Habilitar esquema para criação de perfil](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)
   * [Definir campo de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)

2. Configuração de dados
   * [Criar um conjunto de dados](https://experienceleague.adobe.com/pt-br/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-datasets)
   * [Configurar conexão de streaming](https://experienceleague.adobe.com/pt-br/docs/experience-platform/ingestion/tutorials/create-streaming-connection) (Você precisa da URL do ponto de extremidade de streaming mais tarde; anote-a agora.)

3. Autenticação
   * [Gerar credenciais de API](https://experienceleague.adobe.com/pt-br/docs/experience-platform/landing/platform-apis/api-authentication#generate-credentials) (ID do cliente e Segredo do cliente) da Adobe Developer Console


## Etapas da implementação

### &#x200B;1. Criar configuração de nuvem do AEP

1. Navegue até sua **instância do Adobe Experience Manager** > **Ferramentas** > **Cloud Services** > **Adobe Experience Platform**.
1. Selecione um **Contêiner de Configuração** para armazenar a configuração.
1. Clique em **Criar** para abrir o assistente de configuração do AEP
1. Insira os seguintes detalhes:
   * Título
   * ID do cliente (obtida do console do desenvolvedor)
   * Client Secret (obtido do console do desenvolvedor)
   * URL OAuth (há um URL padrão, mas ele também pode ser obtido no console do desenvolvedor)

   ![Configuração de nuvem do AEP](/help/forms/assets/aep-cloud-configuration.png)

1. Clique em **Conectar** para estabelecer a conexão. Depois de estabelecer a conexão, defina essas configurações adicionais:
   * URL base: platform.adobe.io (Este é um URL padrão e também pode ser obtido no console do desenvolvedor, o oauth e os URLs da plataforma assumem o padrão de prod URLs. Caso seja necessário se conectar ao estágio, os URLs de estágio devem ser usados.)
   * ID da organização (obtida no console do desenvolvedor junto com a ID/segredo do cliente)
   * Nome da sandbox (necessário para ambientes de desenvolvimento e produção)

### &#x200B;2. Criação de formulários com integração de esquema XDM {#form-creation}

>[!BEGINTABS]

>[!TAB Componente de base]

Execute as seguintes etapas para criar o Formulário adaptável com base nos Componentes de base com integração de esquema:

1. Acesse o assistente de criação de formulários:
   * Navegue até sua **instância do Adobe Experience Manager** > **Forms** > **Forms e Documentos**.
   * Clique em **Criar** > **Formulário adaptável**.
1. Na guia **origem**, selecione um modelo de base.
1. Na guia **Dados**, selecione a opção **Adobe Experience Platform**.
1. No painel de propriedades, selecione a configuração de nuvem.

   ![](/help/forms/assets/xdm-schema-integration.png)

   O sistema carrega todos os esquemas disponíveis do Adobe Experience Platform

   >[!NOTE]
   >
   >
   > * Somente esquemas ativados por perfil e não gerados pelo sistema são buscados.
   > * O carregamento inicial do esquema pode levar algum tempo na primeira configuração.

1. Selecione os campos apropriados/obrigatórios do esquema. (Consulte o vídeo para ver as etapas detalhadas)
1. Na guia de envio:
   * Selecione a ação de envio **Enviar para o Adobe Experience Platform**
   * Defina as configurações de envio de formulário para **o envio de dados do AEM Forms para o Experience Platform**
1. No painel de propriedades:
   * Adicione o URL de transmissão (obtido em Fontes do AEP > Conexão de transmissão)
   * Adicione a ID do fluxo de dados (encontrada em Fontes do AEP > Fluxo > Informações de uso da API)
1. Clique em **Salvar**. Forneça os detalhes do formulário:
   * Título
   * Nome
   * Caminho de armazenamento
1. Adicione o botão Submit ao formulário. Seu formulário está pronto para enviar dados para o AEP.

>[!TAB Componente principal]

Execute as seguintes etapas para criar o Formulário adaptável com base nos Componentes principais com Integração de esquema:

1. Acesse o assistente de criação de formulários:
   * Navegue até sua **instância do Adobe Experience Manager** > **Forms** > **Forms e Documentos**.
   * Clique em **Criar** > **Formulário adaptável**.
1. Na guia **origem**, selecione um modelo baseado em Componente principal.
1. Na guia **Dados**, selecione a opção **Adobe Experience Platform**.
1. No painel de propriedades, selecione a configuração de nuvem.

   ![](/help/forms/assets/xdm-schema-integration.png)

   O sistema carrega todos os esquemas disponíveis do Adobe Experience Platform

   >[!NOTE]
   >
   >
   > * Somente esquemas ativados por perfil e não gerados pelo sistema são buscados.
   > * O carregamento inicial do esquema pode levar algum tempo na primeira configuração.

1. Selecione os campos apropriados/obrigatórios do esquema. (Consulte o vídeo para ver as etapas detalhadas)
1. Na guia de envio:
   * Selecione a ação de envio **Enviar para o Adobe Experience Platform**
   * Defina as configurações de envio de formulário para **o envio de dados do AEM Forms para o Experience Platform**
1. No painel de propriedades:
   * Adicione o URL de transmissão (obtido em Fontes do AEP > Conexão de transmissão)
   * Adicione a ID do fluxo de dados (encontrada em Fontes do AEP > Fluxo > Informações de uso da API)
1. Clique em **Salvar**. Forneça os detalhes do formulário:
   * Título
   * Nome
   * Caminho de armazenamento
1. Adicione o botão Submit ao formulário. Seu formulário está pronto para enviar dados para o AEP.

>[!TAB Universal Editor]

Execute as seguintes etapas para criar o Formulário adaptável criado usando o Editor universal com integração de esquema:

1. Acesse o assistente de criação de formulários:
   * Navegue até sua **instância do Adobe Experience Manager** > **Forms** > **Forms e Documentos**.
   * Clique em **Criar** > **Formulário adaptável**.
1. Na guia **origem**, selecione o modelo baseado em Edge Delivery.
1. Na guia **Dados**, selecione a opção **Adobe Experience Platform**.
1. No painel de propriedades, selecione a configuração de nuvem.

   ![integração de esquema](/help/forms/assets/xdm-schema-integration.png)

   O sistema carrega todos os esquemas disponíveis do Adobe Experience Platform

   >[!NOTE]
   >
   >
   > * Somente esquemas ativados por perfil e não gerados pelo sistema são buscados.
   > * O carregamento inicial do esquema pode levar algum tempo na primeira configuração.

1. Selecione os campos apropriados/obrigatórios do esquema. (Consulte o vídeo para ver as etapas detalhadas)
1. Na guia de envio:
   * Selecione a ação de envio **Enviar para o Adobe Experience Platform**
   * Defina as configurações de envio de formulário para **o envio de dados do AEM Forms para o Experience Platform**

     >[!NOTE]
     >
     >* Se você não vir o ícone Fontes de dados na interface do Universal Editor ou a propriedade Associar referência no painel direito de propriedades, habilite a extensão **Fonte de dados** no Extension Manager.
     >* Se você não vir o ícone **Editar Propriedades do Formulário** na interface do Universal Editor, habilite a extensão **Editar Propriedades do Formulário** na Extension Manager.
     > 
     >* Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar ou desabilitar extensões no Universal Editor.

   No momento, não há suporte para o serviço de preenchimento prévio de formulários no Editor Universal.

1. No painel de propriedades:
   * Adicione o URL de transmissão (obtido em Fontes do AEP > Conexão de transmissão)
   * Adicione a ID do fluxo de dados (encontrada em Fontes do AEP > Fluxo > Informações de uso da API)
1. Clique em **Salvar**. Forneça os detalhes do formulário:
   * Título
   * Nome
   * Caminho de armazenamento
1. Adicione o botão Submit ao formulário. Seu formulário está pronto para enviar dados para o AEP.

>[!ENDTABS]

## Observações importantes {#important-notes}

* Os dados enviados por meio de formulários ficam visíveis no AEP após aproximadamente 10 a 15 minutos
* Por padrão, somente esquemas habilitados para perfil são listados
* Embora o envio de dados funcione para todos os esquemas, a funcionalidade de preenchimento prévio é limitada a esquemas habilitados para perfis
* Os dados em esquemas não habilitados para perfil não serão usados para a criação de perfis, mesmo que o esquema seja habilitado posteriormente para a criação de perfis
* **O enriquecimento do perfil do cliente com dados de formulário** requer a configuração adequada do campo de identidade no esquema XDM
* O **envio de dados do AEM Forms para o Experience Platform** usa a **conexão de streaming do AEP para formulários** para garantir o fluxo de dados em tempo real

## Práticas recomendadas {#best-practices}

1. Planeje sua estrutura de esquema com cuidado antes de ativar a criação de perfil
1. Considere os requisitos de dimensionamento do sistema e do volume de dados ao configurar a **conexão de streaming do AEP para formulários**
1. Teste a integração completamente antes da implantação em produção
1. Monitorar os processos de assimilação de dados e criação de perfis
1. Projete a integração do esquema XDM do **com formulários adaptáveis** para coletar apenas os dados necessários
1. Usar estrategicamente o **enriquecimento do perfil do cliente com dados de formulário** para aprimorar a personalização

## Considerações técnicas {#technical-considerations}

* O conector usa APIs de transmissão pública para envio de dados
* A criação do perfil é baseada no campo de identidade
* A unificação de dados ocorre automaticamente no AEP
* A integração oferece suporte à criação de novos formulários e à modificação de formulários existentes
* A integração do esquema XDM com formulários adaptáveis padroniza a estrutura de dados em diferentes pontos de contato
* A conexão de transmissão do AEP para formulários fornece recursos de assimilação de dados em tempo real

## Perguntas frequentes {#faq}

### Perguntas gerais {#general-questions}

**P: &quot;Este conector está disponível com várias ofertas do AEM Forms?**
R: Não, essa integração só está disponível para o AEM Forms as a Cloud Service e está no programa Acesso antecipado.

**P: Esse conector funciona com os Componentes principais adaptáveis do Forms e os Componentes de base?**
R: Esse conector funciona com os Componentes principais adaptáveis do Forms e os Componentes principais adaptáveis do Forms.

**P: Posso enviar dados para vários conjuntos de dados do AEP a partir de um único formulário?**
R: Atualmente, cada formulário pode enviar somente para um conjunto de dados.

**P: Há um limite para quantos envios de formulários podem ser processados?**
R: Os envios de formulários estão sujeitos à sua assimilação de streaming do AEP [cotas e limites de taxa](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/api/quota).

<!-- 
>
**Q: Can form attachments be sent to AEP?**
A: No, form attachments cannot be directly sent to AEP. You would need to store attachments separately and only send metadata to AEP. -->

### Perguntas sobre implementação {#implementation-questions}

**P: Como solucionar problemas de conexão entre o AEM Forms e o AEP?**
R: Verifique as configurações da nuvem, certifique-se de que as credenciais da API estão corretas e verifique se o URL do ponto de extremidade de transmissão está configurado corretamente.

**P: Posso usar esquemas XDM personalizados com essa integração?**
R: Sim, você pode usar qualquer esquema XDM personalizado, desde que esteja configurado corretamente no AEP e, para funcionalidade de preenchimento prévio, habilitado para perfis.

**P: Como habilitar o preenchimento prévio de formulário com dados de perfil do AEP?**
R: Certifique-se de que o esquema esteja habilitado para perfil e que o formulário esteja configurado para usar o mesmo campo de identidade definido no esquema.

**P: E se for necessário transformar dados antes de enviá-los para a AEP?**
R: Você pode usar regras de formulário ou funções personalizadas para transformar dados antes do envio. Para transformações complexas, considere usar uma ação de envio personalizada.

**P: Posso usar essa integração em um modelo de implantação híbrida?**
R: Não, essa integração é específica do AEM Forms as a Cloud Service.

## Resumo e próximas etapas {#summary-next-steps}

A integração do AEM Forms com o Adobe Experience Platform permite que as organizações criem um fluxo contínuo de dados entre formulários e o ecossistema mais amplo da Experience Platform. Essa integração permite criar experiências de formulário mais personalizadas, simplificar a coleta de dados e aprimorar os perfis do cliente com dados valiosos de envio de formulário.

Para começar a usar essa integração:

1. **Solicitar acesso** - Caso ainda não o tenha feito, ingresse no programa de Acesso Antecipado entrando em contato com [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D)
2. **Preparar seu ambiente** - Verifique se você tem as permissões e as configurações necessárias no AEM Forms e no Adobe Experience Platform
3. **Siga as etapas de implementação** - Use o guia acima para definir sua configuração de nuvem e criar seu primeiro formulário conectado à AEP com integração de esquema XDM
4. **Testar completamente** - Valide o envio de dados e os recursos de preenchimento prévio em um ambiente de desenvolvimento
5. **Planejar produção** - Trabalhe com a equipe de implementação para agendar a implantação do envio de dados do AEM Forms para a Experience Platform em produção

## Recursos relacionados {#related-resources}

* [Documentação do AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=pt-BR)
* [Documentação do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html?lang=pt-BR)
* [Visão geral do sistema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR)
* [Assimilação de streaming no Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=pt-BR)
* [Visão geral do Perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=pt-BR)
* [Recursos de acesso antecipado do AEM Forms](/help/forms/early-access-ea-features.md)
* [Criação de Forms adaptável com componentes principais](/help/forms/creating-adaptive-form-core-components.md)
* [Utilização de modelos de dados de formulário no AEM Forms](/help/forms/using-form-data-model.md)

<!--
Schema markup for technical documentation
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "Connect AEM Forms with Adobe Experience Platform (AEP) | Data Integration Guide",
  "description": "Learn how to integrate AEM Forms with Adobe Experience Platform to leverage customer profiles, submit form data, and create personalized experiences.",
  "datePublished": "2025-05-28",
  "author": {
    "@type": "Corporation",
    "name": "Adobe"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Adobe Experience League",
    "logo": {
      "@type": "ImageObject",
      "url": "https://experienceleague.adobe.com/assets/img/favicons/apple-touch-icon.png"
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/aem-forms-aep-connector.html"
  },
  "articleSection": "AEM Forms",
  "keywords": "AEM Forms, Adobe Experience Platform, XDM schema, data integration, form submission, customer profiles, personalization"
}
-->
