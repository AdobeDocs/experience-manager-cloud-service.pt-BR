---
title: Configurar ações de envio para o AEM Forms com o Edge Delivery Services
description: Saiba como configurar ações de envio no AEM Forms usando o Edge Delivery Services. Escolha entre o Serviço de envio do Forms e a Ação de envio de publicação do AEM para lidar com os dados de formulário de maneira segura e eficiente.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: bca160763fdd1e96f1350ac74eb76ff7c26ac00b
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 0%

---


# Configuração dos envios de formulários: para onde vão seus dados?

Depois que um usuário clicar em **enviar** no seu formulário, você precisará informar à Edge Delivery Services o que fazer com esses dados. Você tem duas opções principais:

## Método 1: usar o serviço de envio do AEM Forms (simplificado)

Esse serviço é ideal para ações comuns e diretas, como enviar dados para uma planilha ou um email.

**O que é e como ele pode ajudá-lo?**

O [Serviço de Envio do Forms](/help/forms/forms-submission-service.md) é um ponto de extremidade hospedado pela Adobe. Quando o formulário envia dados para ele, esse serviço assume o controle e executa uma ação pré-configurada. Ele foi projetado para ser fácil de configurar. Você Pode Configurar: Enviando para Planilhas ou E-mail:

* **Enviar para Planilha:** Adicione automaticamente os dados do formulário enviado como uma nova linha em uma Planilha do Google ou em um arquivo do Microsoft Excel (armazenado no OneDrive ou no SharePoint).
* **Enviar Email:** Enviar um email contendo os dados de formulário para um ou mais endereços de email que você especificar.

#### Importante: requisitos de configuração

* **Acesso à Planilha:** Para enviar dados a uma Planilha do Google ou a um arquivo do Excel no OneDrive/SharePoint, a conta de serviço da Adobe (geralmente `forms@adobe.com`) geralmente precisa de **permissão de edição** nessa planilha específica.
* **Programa de Acesso Antecipado** Alguns recursos deste serviço, especialmente para planilhas, podem fazer parte de um programa de acesso antecipado. Talvez seja necessário solicitar acesso enviando um email para `aem-forms-ea@adobe.com` ou preenchendo um formulário específico do Adobe com os detalhes do projeto. Sempre verifique a documentação mais recente do Adobe.

**Fluxograma do Serviço de Envio do Forms**
<!--
```mermaid
    graph TD
    UserForm[User Submits Form on Your EDS Site] >|Data Sent| FormSubmissionService[AEM Forms Submission Service]
    FormSubmissionService -- "If configured for Google Sheets" > GoogleSheet[Data written to Google Sheet]
    FormSubmissionService -- "If configured for Excel (OneDrive or SharePoint)" > ExcelSheet[Data written to Excel]
    FormSubmissionService -- "If configured for Email" > Email[Email with data is sent]

    style UserForm fill:#ccf,stroke:#333
    style FormSubmissionService fill:#fca,stroke:#333
    style GoogleSheet fill:#90ee90,stroke:#333
    style ExcelSheet fill:#90ee90,stroke:#333
    style Email fill:#add8e6,stroke:#333
```-->

![Envio de Forms](/help/forms/assets/eds-fss.png)

Este fluxograma mostra como o Serviço de Envio do Forms pega os dados enviados e os envia para uma planilha ou email configurado.

## Método 2: enviar para sua instância de publicação do AEM (avançado)

Para necessidades mais complexas, os [formulários (especialmente aqueles criados com o Universal Editor) podem enviar dados diretamente para sua instância de Publicação do AEM as a Cloud Service](/help/forms/configure-submit-actions-core-components.md). Isso libera toda a capacidade de back-end do AEM.

**Quando Você Precisa Enviar para o AEM Publish?**

* Para acionar Workflows personalizados do AEM após o envio.
* Usar o Modelo de dados de formulário (FDM) do AEM para integrar-se a bancos de dados ou outros sistemas corporativos.
* Para conectar-se a serviços de terceiros, como Marketo, Microsoft Power Automate ou Adobe Workfront Fusion.
* Para armazenar dados em locais específicos, como o Armazenamento de blobs do Azure ou bibliotecas de listas/documentos do SharePoint (não apenas planilhas simples).
* Quando você tem validação complexa do lado do servidor ou lógica de processamento de dados no AEM.

**Ações de Envio Disponíveis (Envios de Publicação do AEM)**

* [Enviar para um terminal REST](/help/forms/configure-submit-action-restpoint.md)
* [Enviar e-mail (usando os serviços de e-mail da AEM)](/help/forms/configure-submit-action-send-email.md)
* [Enviar usando o Modelo de dados de formulário (FDM)](/help/forms/configure-data-sources.md)
* [Chamar um fluxo de trabalho do AEM](/help/forms/aem-forms-workflow-step-reference.md)
* [Enviar para o SharePoint (como itens de lista ou documentos)](/help/forms/configure-submit-action-sharepoint.md)
* [Enviar para o OneDrive (como documentos)](/help/forms/configure-submit-action-onedrive.md)
* [Enviar para o Armazenamento de blob do Azure](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Enviar para o Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Enviar para o Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Enviar para o Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

>[!NOTE]
>
> Mesmo direcionando uma Planilha/Excel do AEM Publish para o Google, isso envolve etapas de configuração diferentes do Serviço de envio direto do Forms.

**Fluxograma de Envio de Publicação do AEM**

<!--```mermaid
    graph TD
    UEForm[User Submits Universal Editor Form on EDS Site] >|Data sent to AEM Publish URL - example: /adobe/forms/af/submit/...| AEMPublish[AEM Publish Instance]
    AEMPublish -- Configured to run AEM Workflow > AEMWorkflow[AEM Workflow is Triggered]
    AEMPublish -- Configured to use Form Data Model > FDM[FDM updates Backend System or Database]
    AEMPublish -- Configured for Marketo > Marketo[Data sent to Marketo Engage]
    AEMPublish -- Other configured actions... > OtherIntegrations[...]

    style UEForm fill:#ccf,stroke:#333
    style AEMPublish fill:#fca,stroke:#333
    style AEMWorkflow fill:#add8e6,stroke:#333
    style FDM fill:#add8e6,stroke:#333
    style Marketo fill:#add8e6,stroke:#333
```-->

![Fluxograma de Envio de Publicação do AEM](/help/forms/assets/eds-aem-publish.png)
Este fluxograma mostra um formulário sendo enviado para o AEM Publish, que então lida com tarefas complexas de backend.

### Envio do serviço de envio do Forms versus envio de publicação do AEM

| Destaque | Serviço de envio de Forms | Envios de publicação do AEM |
| :- | :- | :-- |
| **Melhor para** | Captura de dados simples em planilhas, notificações por email | Fluxos de trabalho complexos, integrações empresariais, lógica personalizada |
| **Criação de formulário** | Bom para baseado em documento; ok para formulários UE simples | Melhor para formulários criados pelo Universal Editor |
| **Esforço de instalação** | Baixa (geralmente configuração simples) | Mais alto (precisa da configuração do AEM Publish, Dispatcher, OSGi, CDN) |
| **Sistema de back-end** | Serviço hospedado pela Adobe | Sua instância de publicação do AEM as a Cloud Service |
| **Flexibilidade** | Limitado a Planilha/Email | Uma gama completa e muito flexível de ações do AEM Forms |
| **Exemplo** | Entrar em contato com dados de formulário para uma planilha do Google | Aplicativo de empréstimo acionando um fluxo de trabalho de aprovação do AEM |

## Como incorporar o Forms em diferentes sites ou páginas

Às vezes, você deseja exibir um formulário criado e gerenciado em um local (por exemplo, um &quot;site de formulários&quot; central) em uma página da Web ou site diferente.

### Por que você incorporaria um formulário?

* Você tem um formulário padrão &quot;Fale conosco&quot; criado com o Universal Editor que precisa aparecer em várias páginas de aterrissagem criadas com a Criação baseada em documento.
* O conteúdo principal do site está no Document Authoring (DA) e você precisa incluir um formulário especializado.
* Você deseja reutilizar um formulário único e bem mantido em vários projetos diferentes de EDS.

### Como funciona tecnicamente a incorporação de formulários

A página onde você deseja que o formulário apareça (vamos chamá-la de &quot;Página de host&quot;) conterá algum código (geralmente um bloco ou script especial). Quando um usuário visita a página do host, esse código faz uma solicitação para o URL onde o formulário real está hospedado (vamos chamá-lo de &quot;Form Source&quot;). O Form Source envia de volta sua HTML, que a Página do host injeta e exibe.

**Arquitetura de Formulário Inserida**

<!--```mermaid
   graph LR
    User[User] >|Visits| HostPage[Host Page - for example: your-site.com/landing-page]
    HostPage >|Contains code to embed form| FetchForm{Host Page Requests Form HTML}
    FetchForm >|HTTP GET request to the form URL| FormSource[Form Source - for example: forms-repo.hlx.page/my-form]
    FormSource >|Returns form HTML| FetchForm
    FetchForm >|Injects form HTML into page| HostPage
    HostPage >|Displays full page with embedded form| User

    subgraph Submission ["Form Submission from Host Page"]
        HostPage_Form[Embedded form on the host page] >|User submits| TargetEndpoint[Submission endpoint - FSS or AEM Publish]
    end

    style HostPage fill:#e6f3ff,stroke:#333
    style FormSource fill:#ffe6e6,stroke:#333
    style FetchForm fill:#fff2cc,stroke:#333
    style Submission fill:#f0fff0,stroke:#333
```-->

![Arquitetura de Formulário Inserida](/help/forms/assets/eds-embedded-form.png)
Este diagrama mostra a Página de host que busca o formulário HTML no Form Source e o exibe. O envio usa o ponto de extremidade configurado do formulário original.

## Configuração do CORS para Forms incorporado

[O CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) é um recurso de segurança do navegador. Se sua Página de Host (por exemplo, `site-a.com`) tentar buscar um formulário de um domínio diferente (por exemplo, `forms-site-b.com`), o navegador a bloqueará, a menos que `forms-site-b.com` permita explicitamente por meio de cabeçalhos CORS.

Sem os cabeçalhos CORS corretos no **servidor do Form Source**, o navegador impede que a Página de Host carregue o formulário, e seu formulário inserido não seria exibido.

### Como configurar o CORS no site que atende ao seu formulário?

Você precisa configurar o servidor que hospeda o **Form Source** para enviar cabeçalhos HTTP específicos em sua resposta. O método exato depende da configuração do EDS (por exemplo, para projetos do Franklin, isso geralmente é feito em um `helix-config.yaml` ou em um arquivo de configuração semelhante no repositório do GitHub que controla o comportamento do CDN ou a lógica do trabalhador de borda).
Cabeçalhos principais a serem adicionados às respostas do Form Source:

* `Access-Control-Allow-Origin: <URL_of_Host_Page>` (por exemplo, `https://your-site.com`). Para testes, você pode usar `*`, mas para produção, especifique os domínios exatos.
* `Access-Control-Allow-Methods: GET, OPTIONS` (Talvez seja necessário `POST` se o envio do formulário também tiver origem cruzada, mas os envios normalmente têm uma origem diferente ou um ponto de extremidade configurado especificamente).
* `Access-Control-Allow-Headers: Content-Type` (e quaisquer outros cabeçalhos personalizados que sua busca de formulários possa usar).

**Exemplo (conceitual para um arquivo de configuração):**

```yaml
        # In the configuration for the site HOSTING THE FORM (Form Source)
        headers:
          # Apply to paths where your forms are served, e.g., /forms/**
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-page-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS
```

## Considerações adicionais: CDNs e bases de código múltiplas (Helix 4)

* **Regras de CDN:** seu CDN pode oferecer maneiras de solicitações de proxy. Por exemplo, uma solicitação para `host-page.com/embedded-form` pode ser roteada internamente pela CDN para buscar conteúdo de `form-source.com/actual-form`, fazendo com que apareça a mesma origem para o navegador. A configuração pode ser complexa.
* **Várias bases de código (Helix 4):** Se a sua página de host e o Form Source estiverem em repositórios GitHub diferentes (comum nas configurações do Helix 4), verifique se qualquer &quot;Bloco de formulários&quot; do JavaScript necessário para renderizar ou gerenciar o formulário está disponível na base de código da página de host, ou se o formulário que o HTML buscou no Form Source está independente de toda a sua JavaScript necessária. Os documentos originais mencionam que para &quot;helix4 com bases de código diferentes, então você precisa adicionar o bloco Form em ambas as bases de código.&quot;

### Etapas comuns de configuração e configuração da arquitetura

Estas são algumas maneiras comuns de configurar seus formulários, combinando métodos de criação com estratégias de envio, juntamente com pontos principais de configuração.

#### Formulário Baseado em Documento com Envio de Planilha/Email

Esta é a configuração mais simples. Você cria seu formulário no Word/Google Docs e ele envia dados para uma planilha ou email por meio do Serviço de envio do Forms.

1. Defina o formulário em um Documento/Folha do Word/Google usando a estrutura de tabela ou o bloco de formulário especificado.
1. No documento (ou na configuração relacionada), especifique o URL da planilha de destino ou o endereço de email do Serviço de envio do Forms.
1. Verifique se `forms@adobe.com` (ou a conta de serviço relevante) tem acesso de edição à planilha de destino.
1. Publique seu documento no site do Edge Delivery.

**Baseado em Documento + Arquitetura do Forms Submissions Service**
<!--
```mermaid
    graph TD
        User[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User] >|Fills Out| EDS_Page_DocBased[EDS Page with Document-Based Form]
        EDS_Page_DocBased >|Submits Data| FSS[AEM Forms Submission Service]
        FSS > Target[<img src='https://img.icons8.com/color/48/000000/google-sheets.png' width='30' /> Data to Spreadsheet / <img src='https://img.icons8.com/color/48/000000/filled-sent.png' width='30' /> Email Notification]

        Authoring[Form defined in Google Doc/Sheet] >|EDS Syncs & Renders| EDS_Page_DocBased

        style EDS_Page_DocBased fill:#ccf,stroke:#333
        style FSS fill:#fca,stroke:#333
        style Target fill:#90ee90,stroke:#333
        style Authoring fill:#e6ffe6,stroke:#333
```-->

![Baseado em Documento + Arquitetura do Forms Submissions Service](/help/forms/assets/eds-doc-fss.png)

#### Formulário do Editor Universal com Envio de Planilha/Email

Você usa o editor universal visual para criar o formulário, mas ainda usa o serviço simples de envio do Forms para captura de dados.

1. Crie o formulário usando o Editor universal no AEM.
1. Configure a ação de envio do formulário no UE para usar a opção &quot;Enviar para o serviço de envio do Forms&quot;.
1. Especifique o URL da planilha de destino ou o endereço de email.
1. Se estiver usando planilhas, verifique se `forms@adobe.com` tem acesso de edição.
1. Publique sua página contendo o formulário do AEM no site do Edge Delivery.

   **Editor Universal + Arquitetura do Serviço de Envio do Forms**

   ![Editor Universal + Arquitetura do Serviço de Envio do Forms](/help/forms/assets/eds-ue-fss.png)

   <!--```mermaid
    graph TD
    User[User] >|Fills Out| EDS_Page_UE[EDS Page with Universal Editor Form]
    EDS_Page_UE >|Submits Data| FSS[AEM Forms Submission Service]
    FSS > Target[Data sent to Google Sheet and Email Notification]
    AuthoringUE[Form built in Universal Editor - AEM] >|AEM Publishes to EDS| EDS_Page_UE
    style EDS_Page_UE fill:#ccf,stroke:#333
    style FSS fill:#fca,stroke:#333
    style Target fill:#90ee90,stroke:#333
    style AuthoringUE fill:#e6f3ff,stroke:#333
    ```
    -->

#### Formulário do Editor universal com envio de publicação do AEM (avançado)

Essa configuração usa o Editor universal para a criação de formulários e a instância de publicação do AEM para um processamento avançado de back-end (workflows, FDM etc.). Isso requer mais configuração.

1. **Criar Formulário no UE:** Crie seu formulário no Editor Universal. Configure sua ação de envio para apontar para uma ação do AEM Forms (por exemplo, &quot;Chamar um fluxo de trabalho do AEM&quot;, &quot;Enviar usando o modelo de dados de formulário&quot;).
1. **Configuração do AEM Dispatcher (na sua camada de Publicação do AEM):**
   * **Nenhum redirecionamento:** verifique se as regras do Dispatcher fazem *não* solicitações de redirecionamento feitas para caminhos `/adobe/forms/af/submit/...`.
   * **Permitir envios:** modifique seus filtros do Dispatcher (por exemplo, em `filters.any`) para `allow` explicitamente solicitações POST para `/adobe/forms/af/submit/...` do domínio ou endereços IP de seu site do Edge Delivery.
1. **Filtro Referenciador OSGi no AEM (na sua camada de Publicação do AEM):**
   * No console OSGi do AEM (`/system/console/configMgr`), localize e configure o &quot;Filtro referenciador do Apache Sling&quot;.
   * Adicione o(s) domínio(s) do site do Edge Delivery (por exemplo, `https://your-eds-domain.hlx.page`, `https://your-custom-eds-domain.com`) à lista &quot;Permitir hosts&quot; ou &quot;Permitir hosts RegExp&quot;. Isso instrui o AEM a aceitar envios originados de seu site EDS.
1. **Regra de Redirecionamento da CDN (na sua CDN do Edge Delivery):**
   * Seu site do Edge Delivery (por exemplo, `your-eds-domain.hlx.page`) precisa rotear corretamente as solicitações de envio para sua instância de Publicação do AEM.
   * Quando o formulário na sua página de EDS for enviado, ele poderá ter como alvo um caminho relativo como `/adobe/forms/af/submit/...`. Você precisa de uma regra na CDN (ou trabalhador de borda) do Edge Delivery que diga: &quot;Se uma solicitação chegar a `your-eds-domain.hlx.page/adobe/forms/af/submit/...`, encaminhe (proxy ou redirecione) para `your-aem-publish-instance.com/adobe/forms/af/submit/...`.&quot;
   * A implementação exata depende do seu provedor de CDN (por exemplo, Fastly VCL, Akamai Property Manager, Cloudflare Workers).
1. **(Opcional) `constants.js` para Desenvolvimento (na base de código do projeto EDS):**
   * Para desenvolvimento local ou se os scripts de formulário do lado do cliente precisarem saber a URL completa de publicação do AEM, você poderá configurá-la em um `constants.js` ou em um arquivo de configuração semelhante no repositório GitHub do projeto do Edge Delivery. Exemplo:

   ```javascript
       // in your-eds-project/scripts/constants.js
       export const AEM_PUBLISH_URL = 'https://publish-p123-e456.adobeaemcloud.com';
            // Your form submission script might then construct the submit URL:
           // const submitUrl = `${AEM_PUBLISH_URL}/adobe/forms/af/submit/...`;
   ```

1. **Publicar:** publique a página do formulário do AEM no EDS e verifique se todas as configurações do AEM estão ativas na sua instância de Publicação do AEM.

   **Editor Universal + Arquitetura de Publicação do AEM**

![Editor Universal + Arquitetura de Publicação do AEM](/help/forms/assets/eds-aem-publish.png)

Isso mostra o fluxo: o usuário envia no site do EDS, o CDN roteia para o AEM Dispatcher e, em seguida, o AEM Publish a processa.

#### Incorporação de um formulário a uma página de Criação de documento (DA)

O conteúdo principal do site é criado no Document Authoring (DA). Você cria o formulário usando a Criação baseada em documento ou o Editor universal separadamente e, em seguida, incorpora-o à página do DA.

1. **Criar e Publicar o Formulário:**
   * Use a Criação baseada em documento OU o Editor universal para criar o formulário.
   * Configurar o método de envio (para o Serviço de envio do Forms ou para a Publicação do AEM, conforme Configuração 1, 2 ou 3).
   * Publique este formulário para que ele esteja disponível em sua própria URL do Edge Delivery (por exemplo, `.../forms/my-special-form`).
1. **Configurar o CORS:** No site/projeto do Edge Delivery que hospeda este formulário independente, verifique se os cabeçalhos do CORS estão configurados para permitir que o domínio do site de Criação de Documentos o busque.
1. **Criar página no DA:** Crie ou edite sua página no Document Authoring.
1. **Inserir bloco de formulário:** Use o bloco apropriado no DA para inserir uma URL externa. Aponte esse bloco para o URL do formulário publicado independente.
1. **Publicar página do DA:** Publique sua página do DA. Agora ele buscará e exibirá o formulário.

   **Forms Incorporado na Arquitetura DA**

   ![Forms Incorporado na Arquitetura DA](/help/forms/assets/eds-forms-embedd-da.png)

   Isso mostra uma página do DA que puxa um formulário de outro local do EDS. O formulário incorporado lida com seu próprio envio.

## Resolução de problemas

* **O envio do meu formulário não está funcionando.**
   * **Verificar Erros do Console:** Abra o console do desenvolvedor do navegador (geralmente F12) e procure erros na guia Rede ou na guia Console ao enviar.
   * **Verificar URL de Envio:** O formulário está tentando enviar para o ponto de extremidade correto (URL do Serviço de Envio do Forms ou caminho de Publicação do AEM)?
   * **Serviço de Envio do Forms:** Se estiver enviando para uma planilha, `forms@adobe.com` recebeu acesso de edição? O URL da planilha está correto?
   * **Envios de Publicação do AEM:**
      * O seu Dispatcher está permitindo o envio de POST para `/adobe/forms/af/submit/...`?
      * O Filtro referenciador Sling na publicação do AEM está configurado para permitir o domínio EDS?
      * Suas regras de redirecionamento CDN para `/adobe/forms/af/submit/...` estão funcionando corretamente?

* **Meu formulário inserido não está aparecendo.**

   * **CORS!** Este é o motivo mais comum. Verifique se há erros de CORS no console do navegador. Verifique se o site *hospedagem* do formulário tem os cabeçalhos `Access-Control-Allow-Origin` corretos.
   * **URL do formulário correto?** O código de inserção na página do host aponta para a URL ativa correta do formulário?
   * **Blocos JavaScript:** Se o formulário depender de um &quot;Bloco de formulário&quot; JavaScript específico para renderização, o código desse bloco estará disponível na página do host?

* **Recebo um &quot;403 Proibido&quot; ou &quot;401 Não Autorizado&quot; ao enviar para a Publicação do AEM.**

   * Isso geralmente aponta para o Sling Referrer Filter na publicação do AEM, impedindo solicitações do seu domínio EDS. Verifique novamente a configuração.
   * Também pode ser um problema de autenticação/autorização se o terminal de envio do AEM exigir, embora os envios de formulários padrão geralmente sejam anônimos.

## Próximas etapas

Este guia fornece uma visão geral do uso de formulários com o AEM Edge Delivery Services. Para obter instruções passo a passo mais detalhadas sobre configurações específicas, consulte a documentação oficial do Adobe Experience Manager:

* [Criação baseada em documento com o Edge Delivery Services Forms](/help/edge/docs/forms/tutorial.md)
* [Editor universal com o Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Criação de Documentos (DA) e Incorporação de Conteúdo](https://www.aem.live/developer/da-tutorial)
* [Serviço de envio de AEM Forms](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)