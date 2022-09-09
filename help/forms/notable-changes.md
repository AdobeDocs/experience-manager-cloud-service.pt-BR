---
title: O que mudou entre AEM 6.5 Forms e AEM Cloud Services
description: Você é um usuário do Experience Manager Forms e deseja atualizar para o Adobe Experience Manager Forms as a Cloud Service? Saiba mais sobre as alterações mais importantes antes de atualizar ou migrar para o Cloud Service.
contentOwner: khsingh
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 3%

---

# Alterações importantes para usuários existentes do Adobe Experience Manager Forms  {#notable-changes-for-existing-AEM-Forms-users}

O Adobe Experience Manager Forms as a Cloud Service traz algumas alterações notáveis aos recursos existentes em comparação ao Adobe Experience Manager FormsOn-Premise e [!DNL Adobe-Managed Service] ambientes . As principais diferenças estão listadas abaixo:

* O serviço fornece um ambiente de desenvolvimento local e nativo de nuvem. Você pode usar um [ambiente de desenvolvimento local](setup-local-development-environment.md) para desenvolver e testar seu código personalizado, componentes, modelos, temas, Adaptive Forms, outros ativos antes de implantar esses ativos em um ambiente em nuvem. Ajuda a acelerar o processo de desenvolvimento.
* [!DNL AEM] como Cloud Service é enviado com um CDN integrado. Seu principal objetivo é reduzir a latência, fornecendo conteúdo que pode ser armazenado em cache a partir dos nós CDN na borda, perto do navegador. Ele é totalmente gerenciado e configurado para obter o desempenho ideal dos aplicativos AEM.
* Um ambiente nativo da nuvem não tem o console da Web (gerenciador de configuração). Você pode usar [[!DNL AEM Forms] SDK as a Cloud Service para gerar configurações](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) e pipeline de CI/CD para [implantar a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) para a instância do Cloud Service.

* A convenção de URL do Adaptive Forms localizado agora é compatível com a especificação de um local no URL. A nova convenção de URL permite o armazenamento em cache de formulários localizados em um Dispatcher ou CDN. No ambiente Cloud Service , use o formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. O Adobe recomenda usar o armazenamento em cache do Dispatcher ou CDN. Ajuda a melhorar a velocidade de renderização dos formulários pré-preenchidos.
* O serviço de preenchimento prévio mescla dados com um formulário adaptável em um cliente. Ajuda a melhorar o tempo necessário para preencher previamente um formulário adaptável. Você sempre pode configurar para executar a ação de mesclagem no Adobe Experience Manager FormsServer.
* Por padrão, o suporte a email é compatível somente com protocolos HTTP e HTTPs. [Entre em contato com a equipe de suporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) para habilitar as portas para enviar emails e habilitar o protocolo SMTP para seu ambiente.
* O Adobe Experience Manager Forms as a Cloud Service traz muitos novos recursos e possibilidades para seus Projetos AEM. No entanto, há algumas alterações necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com o AEM Cloud Service. Em um nível alto, o AEM exige uma separação de conteúdo e código em subpacotes discretos para respeitar a divisão entre conteúdo mutável e imutável. Use o [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) ferramenta para reestruturar pacotes de projetos existentes separando conteúdo e código em pacotes discretos para serem compatíveis com a estrutura do projeto definida para o Adobe Experience Manager as a Cloud Service.

<!--  If your Cloud Configuration contains a secret (password), create a separate Cloud Configuration for every Author instance (Developer, Stage, and Production). If a Cloud Configuration is also required on Publish instances, publish/replicate a separate Cloud Configuration for every Publish instance (Developer, Stage, and Production). 

* When you create a Cloud Configuration that contains a secret, each Cloud Service instance (Developer, Stage, and Production) uses its own encryption key to encrypt the password before storing it. So, manually create such Cloud Configuration for every Cloud Service instance (Developer, Stage, and Production). Also, do not store secrets used in a Cloud Configuration to your Cloud Manager Git repository.

* Use [!DNL Cloud Manager] [APIs to convert and provide your passwords as secrets](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#setting-values-via-api). Do not store plain text password or secrets on your environments. -->

* Uso de configurações específicas do ambiente para valores de configuração OSGi secretos, como senhas, chaves de API privadas ou quaisquer outros valores. Eles não podem ser armazenados no Git por motivos de segurança. [Use configurações secretas específicas do ambiente para armazenar o valor de segredos em todos os ambientes do Adobe Experience Manager as a Cloud Service, incluindo Preparo e Produção](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#when-to-use-secret-environment-specific-configuration-values).

Para obter uma lista abrangente de alterações no Adobe Experience Manager as a Cloud Service, consulte [Novidades e diferenças](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html).

<!-- ## Feature comparison {#comparison}

[!DNL AEM Forms] as a Cloud Service and Experience Manager 6.5 Forms share a common set of features: Adaptive Forms, data integration, integration with [!DNL Adobe Sign], themes, templates, and forms management interface are identical. You can easily port your existing Adaptive Forms from an Experience Manager 6.5 Forms or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of AEM 6.5 Forms and [!DNL AEM Forms] as a Cloud Service {#feature-comparison}

The following table lists the major features of Experience Manager 6.5 Forms and provides information about whether the feature is partially or fully supported in [!DNL AEM Forms] as a Cloud Service, with a link to more information about the feature. The table also lists extra features available in [!DNL AEM Forms] as a Cloud Service.


| Feature/Capability | AEM 6.5 Forms | [!DNL AEM Forms] as a Cloud Service |
| - | - | - |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611;(With some changes) |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with Adobe Sign | &#x2611; | &#x2611;(With some changes) |
| Themes and Templates | &#x2611; | &#x2611; ([With some changes](themes.md#difference-in-themes))|
| Rule editor | &#x2611; | &#x2611; (With some changes) |
| Forms Portal | &#x2611; | --- |
| Integration with Adobe Analytics | &#x2611; | &#x2612; |
| Document Security | &#x2611; | &#x2612; | -->

<!-- ## New features {#comparison} -->



## Principais melhorias {#whats-new}

<!-- [!DNL AEM Forms] as a Cloud Service offers benefits like auto-scaling, cost-effectiveness, zero downtime for upgrades, and cloud-native development environment and more. The list does not stop here. The following features are are start and are available only for [!DNL AEM Forms] as a Cloud Service: -->

Os seguintes recursos e aprimoramentos estão disponíveis somente em [!DNL AEM Forms] as a Cloud Service:

**Editor de regras visuais aprimorado**
O serviço oferece [Editor de regras visuais](rule-editor.md#visual-rule-editor). O serviço adicionou os seguintes recursos ao editor de regras do Visual para ajudar você a escrever regras capazes:

* [Novos eventos de envio](working-with-adobe-sign.md#available-operator-types-and-events-in-rule-editor): `Navigation`, `Step Completion`, `Successful Submission`e `Error`

* [Novo tipo de dados `scope`](rule-editor.md#custom-functions). Você pode usar o `scope` tipo de dados em uma função personalizada para passar todo o escopo de um formulário.

* Capacidade de usar [@this para especificar um JSDoc em uma função personalizada](rule-editor.md#custom-functions). Ela permite invocar uma função personalizada usando @this em um componente ativo.

* Capacidade de adicionar condições para regras baseadas em propriedade.

**Componentes principais**
O [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) são um conjunto de componentes padronizados do Web Content Management (WCM) para AEM a fim de acelerar o tempo de desenvolvimento e reduzir o custo de manutenção. [!DNL AEM Forms] Suporte as a Cloud Service **[!UICONTROL Contêiner AEM Forms]** Componente principal. Você pode usar o componente para incorporar um formulário adaptável a uma página do AEM Sites.

**Arquétipo de AEM para Forms as a Cloud Service**
[Arquétipo de AEM](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) ajuda você a começar a desenvolver o [!DNL AEM Forms] as a Cloud Service. Você pode usar o Archetype versão 27 ou posterior para criar um modelo de projeto compatível com o [!DNL AEM Forms] Ambiente as a Cloud Service. O Arquétipo também inclui alguns temas e modelos de amostra para ajudar você a começar rapidamente.

**Fluxo de informações seguro e aprimorado entre formulários e Sign**
[Integração adaptável Forms e Adobe Sign](working-with-adobe-sign.md) no Cloud Service oferecem envio simultâneo de dados e atividade de assinatura. Ele torna o envio de formulário independente do status de assinatura uma maneira de enviar envios mais rápidos. Além disso, o serviço não salva dados em instâncias do Cloud Service, tornando o processo de assinatura super seguro.

**Ferramenta Analisador de práticas recomendadas e migração**
O Analisador de práticas recomendadas fornece uma avaliação da implementação de AEM atual. Execute a ferramenta antes de [migração para o Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md). Ele avalia a prontidão para migrar de uma implantação do Adobe Experience Manager (AEM) existente para AEM as a Cloud Service.

O serviço também fornece uma [experiência de migração aprimorada](migrate-to-forms-as-a-cloud-service.md) para ajudá-lo a migrar facilmente da [!DNL AEM 6.4 Forms] e [!DNL AEM 6.5 Forms] para [!DNL AEM Forms] as a Cloud Service.

**Representações de formulário mais rápidas e validações mais rápidas no lado do servidor**
O serviço usa o armazenamento em cache do CDN e do Dispatcher para fornecer representações mais rápidas e validações do lado do servidor para o Adaptive Forms.

**CAPTCHA aprimorado**
Agora você pode [validar CAPTCHA](captcha-adaptive-forms.md) no envio do formulário adaptativo ou em uma lógica comercial. Você também pode adicionar condições para validar CAPTCHA em uma ação do usuário e mostrar ou ocultar o componente CAPTCHA em um Formulário adaptável com base em regras.

O componente CAPTCHA fornece uma integração pronta para uso com o Google reCAPTCHA. Você também pode configurar mais serviços CAPTCHA para o componente, se necessário.

**Várias páginas principais para o Documento de registro**
Agora é possível usar uma página principal diferente para cada página de um Documento de registro e controlar o posicionamento de um painel Formulário adaptável em um Documento de registro com opções de paginação.

**Adicionar colunas a tabelas sem cabeçalho**
É possível adicionar e excluir colunas em tabelas sem cabeçalhos. Cabeçalhos ocultos são adicionados a essas tabelas para ajudá-lo a adicionar e excluir colunas. Esses cabeçalhos são visíveis durante a criação, mas permanecem ocultos no formulário publicado. Tabelas sem cabeçalhos são encontradas no Adaptive Forms criado usando o Automated forms conversion Service.

**Ações de envio aprimoradas**
Você pode usar o [Enviar Email](configuring-submit-actions.md#send-email#send-email) Enviar ação para enviar um PDF doR (Document of Record) como anexo.

**Agrupar email para fluxo de trabalho**
Você pode optar por [enviar emails de notificação](aem-forms-workflow-step-reference.md#assign-task-step) na etapa Atribuir tarefa a uma única pessoa ou grupo.

**Etapa de modelo de dados de formulário de chamada aprimorada**
Agora é possível especificar o caminho da pasta para a opção Relativo a Carga dos argumentos do serviço de entrada em uma etapa Invocar Modelo de Dados de Formulário . Ajuda a mapear um arquivo presente na pasta especificada para o argumento de serviço sem especificar o nome de arquivo exato.

**Aprimoramento da legibilidade dos arquivos de tradução**
No Forms as a Cloud Service, a ordem de leitura dos campos e painéis de um Formulário adaptável e das chaves de mensagem dos arquivos de tradução correspondentes (arquivos .XLIFF) tem estrutura semelhante. Ajuda a melhorar as velocidades de tradução manual.

<!-- ## Feature comparison {#feature-comparison}

[!DNL AEM Forms] as a Cloud Service and [!DNL AEM 6.5 Forms] share some features like Adaptive Forms, Data Integration, and Forms Portal. You can easily port your existing Adaptive Forms from an [!DNL AEM 6.5 Forms] or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of [!DNL AEM 6.5 Forms] and [!DNL AEM Forms] as a Cloud Service {#aem-6.5-vs-aem-forms-as-a-cloud-service}

The following table lists the major features of [!DNL AEM 6.5 Forms] and provides information about the features coming soon to [!DNL AEM Forms] as a Cloud Service:

| Feature/Capability | AEM 6.5 Forms  | [!DNL AEM Forms] as a Cloud Service |
|---|---|---|
| Cloud-native architecture | &#x2612; | &#x2611;  |
| Auto-scaling based on load | &#x2612; | &#x2611;  |
| Zero downtime for upgrades | &#x2612; | &#x2611;  |
| Feature roll-out frequency | Quarterly | Agile*  |
| CDN (content delivery network) included | &#x2612; | &#x2611;  |
| Topologies optimized for maximum resilience and efficiency | &#x2612; | &#x2611;  |
| Cloud-native development environment | &#x2612; | &#x2611;  |
| Self-Service via Cloud Manager | &#x2612; | &#x2611;  |
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD)| &#x2611; | &#x2611;  |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611; |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; |
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; |
| Enhanced Visual Rule editor | &#x2612; | &#x2611; |
| Forms Portal | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Analytics] | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Target] | &#x2611; | Coming Soon |
| Document Security | &#x2611; | &#x2612; |

`*` New features every month and bug fix updates on daily basis.

For a comprehensive list of changes in AEM as a Cloud Service, See [What is New and What is Different](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/overview/what-is-new-and-different.html) and [Notable changes in [!DNL AEM Forms] as a Cloud Service](notable-changes.md) -->
