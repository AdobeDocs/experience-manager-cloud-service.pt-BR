---
title: Configurar ações de envio para o AEM Forms com o Edge Delivery Services
description: Saiba como configurar ações de envio no AEM Forms usando o Edge Delivery Services. Escolha entre o Serviço de envio do Forms e a Ação de envio de publicação do AEM para lidar com os dados de formulário de maneira segura e eficiente.
feature: Edge Delivery Services
role: Admin, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 3%

---

# Configurar ações de envio para o AEM Forms

Configure o manuseio de envio de formulário para rotear dados para planilhas, emails ou sistemas de back-end usando o AEM Forms com o Edge Delivery Services.

## Guia de decisão rápida

Escolha seu método de envio:

| Método | Melhor para | Complexidade da configuração | Casos de uso |
|--------|----------|------------------|-----------|
| **Serviço de Envio do Forms** | Captura de dados simples | Baixa | Formulários de contato, pesquisas, coleta básica de dados |
| **Envio de publicação do AEM** | Fluxos de trabalho complexos | Alta | Integrações empresariais, processamento personalizado, fluxos de trabalho |

## Pré-requisitos

Antes de configurar ações de envio, verifique se você tem:

- Instância do AEM Forms as a Cloud Service
- Projeto do Edge Delivery Services configurado
- Formulário criado usando Criação de Documento ou Editor Universal
- Permissões necessárias para destinos de destino (planilhas, sistemas de email ou AEM)

+++ Método 1: Serviço de envio do Forms

O Serviço de envio da Forms é um terminal hospedado pela Adobe ideal para cenários simples de captura de dados.

### Destinos suportados

- **Planilhas**: Google Sheets, Microsoft Excel (OneDrive/SharePoint)
- **Email**: enviar dados de formulário para endereços de email especificados

### Etapas de configuração

1. **Configurar Acesso ao Destino**
   - Para planilhas: Conceder permissão de edição a `forms@adobe.com` na planilha de destino
   - Para email: verifique se os endereços de email dos recipients estão acessíveis

2. **Configurar Envio de Formulário**
   - Abrir o formulário no ambiente de criação
   - Definir a ação de envio como &quot;Serviço de envio do Forms&quot;
   - Especificar URL da planilha de destino ou endereços de email
   - Salvar e publicar o formulário

3. **Envio de teste**
   - Enviar dados de teste por meio do formulário
   - Verificar se os dados aparecem no destino
   - Verificar logs de erros se o envio falhar

### Observações importantes

- A conta de serviço `forms@adobe.com` requer acesso de edição para planilhas de destino
- As notificações por email são enviadas imediatamente após o envio do formulário
- A validação de dados ocorre no nível de serviço

![Fluxo do Serviço de Envio do Forms](/help/forms/assets/eds-fss.png)

+++

+++ Método 2: envio de publicação do AEM

Envie dados de formulário diretamente para a instância de publicação do AEM as a Cloud Service para processamento complexo.

### Quando usar a publicação do AEM

- Fluxos de trabalho personalizados do AEM necessários após envio
- Integração do Form Data Model (FDM) com bancos de dados
- Integrações de serviços de terceiros (Marketo, Power Automate, Workfront Fusion)
- Armazenamento Azure Blob ou bibliotecas de documentos do SharePoint
- Validação ou lógica de processamento complexa do lado do servidor

### Ações de envio disponíveis

- [Enviar para endpoint REST](/help/forms/configure-submit-action-restpoint.md)
- [Enviar email por meio dos serviços de email da AEM](/help/forms/configure-submit-action-send-email.md)
- [Enviar usando modelo de dados de formulário](/help/forms/configure-data-sources.md)
- [Chamar fluxo de trabalho de AEM](/help/forms/aem-forms-workflow-step-reference.md)
- [Enviar para o SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [Enviar para o OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [Enviar para o Armazenamento de blob do Azure](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Enviar para o Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [Enviar para o Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Enviar para o Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![Fluxo de envio de publicação do AEM](/help/forms/assets/eds-aem-publish.png)

### Requisitos de configuração

#### &#x200B;1. Atualizar o URL da instância do AEM no Edge Delivery

Atualize a URL da instância do AEM Cloud Service no arquivo `constant.js` no bloco `form` em `submitBaseUrl`. Você pode configurar o URL com base em seu ambiente:

**Para a instância do Cloud Service**

```js
export const submitBaseUrl = '<aem-publish-instance-URL>';
```

**Para desenvolvimento local**

```js
export const submitBaseUrl = 'http://localhost:<port-number>';
```

#### &#x200B;2. Filtro referenciador OSGi

Configure o Filtro referenciador para permitir domínios de site específicos do Edge Delivery:

1. Criar ou atualizar o arquivo de configuração OSGi: `org.apache.sling.security.impl.ReferrerFilter.cfg.json`

2. Adicione a seguinte configuração com os domínios específicos do site:

   ```json
   {
     "allow.empty": false,
     "allow.hosts": [
       "main--abc--adobe.aem.live",
       "main--abc1--adobe.aem.live"
     ],
     "allow.hosts.regexp": [
       "https://.*\\.aem\\.live:443",
       "https://.*\\.aem\\.page:443",
       "https://.*\\.hlx\\.page:443",
       "https://.*\\.hlx\\.live:443"
     ],
     "filter.methods": [
       "POST",
       "PUT",
       "DELETE",
       "COPY",
       "MOVE"
     ],
     "exclude.agents.regexp": [
       ""
     ]
   }
   ```

3. Implantar a configuração por meio do Cloud Manager

Para obter a configuração detalhada do Filtro referenciador OSGi, consulte o Guia do [Filtro referenciador](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter).

#### &#x200B;3. Questões do CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens)

Defina as configurações do CORS no AEM para permitir solicitações de domínios específicos do site do Edge Delivery:

**Localhost do Desenvolvedor**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true
```

**Sites do Edge Delivery - Adicionar cada domínio de site individualmente**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true
```

**Domínios herdados do Franklin (se ainda estiverem em uso)**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>Substitua `main--abc--adobe.aem.live` e `main--abc1--adobe.aem.live` pelos domínios de site reais. Cada site hospedado no mesmo repositório requer uma entrada de configuração do CORS separada.

Para obter a configuração detalhada do CORS, consulte o [Guia de Configuração do CORS](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors).


Para habilitar o CORS para o seu ambiente de desenvolvimento local, consulte o artigo [Entender o CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing).

<!--
#### 4. CDN Redirect Rules

Configure your Edge Delivery CDN to route submissions:

- Route requests from `/adobe/forms/af/submit/...` to your AEM Publish instance
- Implementation varies by CDN provider (Fastly, Akamai, Cloudflare)-->

#### &#x200B;4. Configuração do formulário

1. Criar formulário no Editor Universal
2. Configurar ação de envio para ação do AEM Forms de destino
3. Especificar caminho de ponto de extremidade de envio
4. Publicar formulário no site do Edge Delivery

+++
<!--
+++ Form Embedding

Embed forms created in one location into different web pages or sites.

### Use Cases

- Reuse standard forms across multiple landing pages
- Include specialized forms in Document-Authored content
- Maintain single form across multiple EDS projects

### CORS Configuration

Configure Cross-Origin Resource Sharing on the form source:

1. **Add CORS Headers** to form source responses:
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`  
   - `Access-Control-Allow-Headers: Content-Type`

2. **Example Configuration**:

        # Configuration for site hosting the form
        headers:
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS

### Embedding Steps

1. **Create and Publish Form**
   - Build form using Document Authoring or Universal Editor
   - Configure submission method (FSS or AEM Publish)
   - Publish to standalone URL

2. **Configure CORS**
   - Set up CORS headers on form source site
   - Allow host page domain to fetch form

3. **Embed in Host Page**
   - Add form embedding block to host page
   - Point block to published form URL
   - Publish host page

![Embedded Form Architecture](/help/forms/assets/eds-embedded-form.png)

+++-->

+++ Problemas comuns

| Problema | Solução |
|-------|----------|
| **Falha no envio do formulário** | Verifique os erros do console, verifique o URL do endpoint e confirme as permissões |
| **Formulário inserido não aparece** | Configure os cabeçalhos CORS na origem do formulário e verifique o URL do formulário |
| Erros **403/401 com o AEM** | Atualize o filtro do referenciador Sling, verifique as configurações de autenticação |
| **Dados não atingindo a planilha** | Verificar se `forms@adobe.com` tem acesso de edição, verificar URL da planilha |
| **Erros do CORS** | Adicionar cabeçalhos `Access-Control-Allow-Origin` adequados à origem do formulário |

+++

## Exemplos de configuração

+++ Formulário Baseado em Documento com Envio de Planilha

1. Criar estrutura de formulário no Google Docs/Sheets
2. Configurar ponto de extremidade do Serviço de envio do Forms
3. Conceder acesso de edição `forms@adobe.com` à planilha de destino
4. Publicar documento no site do Edge Delivery
5. Testar envio de formulário e fluxo de dados

+++

+++ Formulário do editor universal com fluxo de trabalho do AEM

1. Criar formulário no Editor Universal
2. Configurar a ação de envio para &quot;Chamar fluxo de trabalho do AEM&quot;
3. Configurar o Dispatcher e o filtro de referenciador no AEM Publish
4. Configurar regras de roteamento CDN
5. Publicar formulário e testar a execução do fluxo de trabalho

+++

## Práticas recomendadas

- **Use o Serviço de Envio do Forms** para cenários simples de captura de dados
- **Escolha Publicar no AEM** quando um processamento complexo ou integrações forem necessários
- **Testar completamente** no ambiente de preparo antes da implantação de produção
- **Monitorar envios** usando logs do AEM e erros de console
- **Implementar a manipulação adequada de erros** para envios com falha
- **Validar dados** nos níveis de cliente e servidor
- **Usar HTTPS** para todos os envios de formulários e transmissão de dados

## Tópicos relacionados

- [Criação baseada em documento com o EDS Forms](/help/edge/docs/forms/tutorial.md)
- [Editor universal com EDS Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [Serviço de envio de AEM Forms](/help/forms/forms-submission-service.md)
- [Configurar fontes de dados](/help/forms/configure-data-sources.md)
- [Referência do fluxo de trabalho do AEM Forms](/help/forms/aem-forms-workflow-step-reference.md)
