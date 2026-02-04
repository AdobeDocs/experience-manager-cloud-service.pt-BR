---
title: Chamar uma interface do usuário associada na instância de publicação
description: Saiba como integrar e chamar a interface do usuário do AEM Forms Associate em instâncias de Publicação para permitir que profissionais voltados para o cliente gerem comunicações interativas personalizadas em tempo real.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
hidefromtoc: true
source-git-commit: bfee883205f81012fea75cbd7dc5fddd7169fdbb
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 1%

---


# Gerar comunicações personalizadas com a interface do usuário associada

<span> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.</span>

A interface do usuário Associar pode ser invocada diretamente em instâncias de Publicação, permitindo que profissionais voltados para o cliente, como associados de campo e agentes de serviço, gerem comunicações personalizadas em tempo real durante as interações do cliente.

A tabela abaixo descreve os vários cenários do mundo real em que a Interface do usuário associada pode ser usada para enviar mensagens personalizadas aos clientes:

| Setor | Caso de uso |
|----------|----------|
| **Serviços financeiros** | Gerar cartas de confirmação de empréstimo em tempo real, extratos de conta e resumos de perfil de risco durante reuniões de clientes |
| **Seguros** | Produzir cartões de comprovação de seguro instantâneos e resumos de descarte de solicitações nos balcões de serviço |
| **Serviços de saúde** | Criar resumos do plano de tratamento do paciente com valores e cronogramas de pagamento calculados |
| **Governo** | Gerar relatórios de verificação policial, recibos de serviço ao cidadão e resumos de atualização de casos no local |

## Pré-requisitos

Antes de integrar a Interface do usuário do Associate ao seu aplicativo, verifique se você tem:

- Comunicação interativa criada e publicada
- Navegador com suporte a pop-up ativado
- Os [usuários associados devem fazer parte do grupo &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-roles#assign-a-role-to-users-and-groups) de forms-associates
- Autenticação configurada usando qualquer [mecanismo de autenticação com suporte do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/authentication) (por exemplo, SAML 2.0, OAuth ou manipuladores de autenticação personalizados)

>[!NOTE]
>
>- Este artigo demonstra a configuração de autenticação usando o SAML 2.0 com a [Microsoft Entra ID (Azure AD) como o Provedor de Identidade](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings).
>- Para Associar Interface, configurações SAML adicionais são necessárias além da configuração padrão explicada no artigo [Autenticação SAML 2.0](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0). Consulte a seção [Configurações SAML adicionais para interface do usuário associada](#additional-saml-configurations-for-associate-ui) para obter detalhes.

### Configurações SAML adicionais para Associar IU

Ao configurar a autenticação SAML 2.0 para a Interface de usuário associada, você deve aplicar as seguintes configurações específicas em seus arquivos de configuração OSGi.

#### Manipulador de autenticação SAML

Criar o arquivo `com.adobe.granite.auth.saml.SamlAuthenticationHandler~saml.cfg.json` em `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
  {
    "path": ["/libs/fd/associate"],
    "serviceProviderEntityId": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com",
    "assertionConsumerServiceURL": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/saml_login"
    "idpUrl": "https://login.microsoftonline.com/{azure-tenant-id}/saml2",
    "idpCertAlias": "{your-certificate-alias}",
    "idpIdentifier": "https://sts.windows.net/{azure-tenant-id}/",
    "userIDAttribute": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",
    "createUser": true,
    "userIntermediatePath": "saml",
    "synchronizeAttributes": [
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname=profile/givenName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname=profile/familyName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress=profile/email"
      ],
      "addGroupMemberships": true,
      "defaultGroups": ["forms-associates"],
      "defaultRedirectUrl": "/libs/fd/associate/ui.html",
      "idpHttpRedirect": false,
      "service.ranking": 5002
  }
```

| Propriedade | Descrição |
|----------|-------------|
| `path` | Deve ser definido como `/libs/fd/associate` para Associar UI |
| `defaultGroups` | Defina como `forms-associates` para atribuir usuários automaticamente ao grupo necessário |
| `defaultRedirectUrl` | Redireciona usuários autenticados para a Interface do usuário associada |
| `idpHttpRedirect` | Deve ser `false` para o fluxo iniciado pela controladora |
| `idpCertAlias` | Deve corresponder exatamente ao alias do certificado no Armazenamento de Confiança (diferencia maiúsculas de minúsculas) |

#### Sling Authenticator

Atualizar o arquivo `org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json` em `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Filtro do Dispatcher

Se ainda não estiver presente, adicione as seguintes regras ao arquivo `dispatcher/src/conf.dispatcher.d/filters/filters.any`:

```json
  # Allow Interactive Communications APIs and Associate UI
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/adobe/communications" }
  /XXXX { /type "allow" /method '(GET|POST|OPTIONS)' /url "/adobe/communications/*" }
  /XXXX { /type "allow" /method "GET" /url "/content/dam/fd:fonts/*" }
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/libs/fd/associate/*" }
```

>[!NOTE]
>
> Substitua `XXXX` pela sequência numérica apropriada usada em seu arquivo `filters.any` existente.

## Chamar interface de usuário associada na instância de publicação

Para chamar a interface do usuário Associar do aplicativo, configure o URL da instância de Publicação, prepare a carga de dados e use a função de integração para iniciar a interface do usuário Associar em uma nova janela do navegador.

### Etapa 1: configurar o URL da instância de publicação

A interface do usuário Associate é acessada por meio de um endpoint específico na instância de publicação do AEM Forms Cloud Service:

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

Substitua `{program-id}` e `{env-id}` pelos valores reais do ambiente.

Por motivos de segurança, parâmetros como ID de comunicação interativa, serviço de preenchimento prévio e parâmetros de serviço não são transmitidos pelo URL. Em vez disso, esses parâmetros são transmitidos com segurança usando uma função do JavaScript que se comunica com a interface do usuário Associate por meio da API postMessage do navegador.

### Etapa 2: Preparar a carga de dados

Estruture sua carga de dados com o seguinte formato:

```javascript
const data = {
  id: "your-ic-id",              // Required: Interactive Communication ID
  prefill: {                      // Optional: Data to prefill the IC
    serviceName: "YourService",
    serviceParams: { key: "value" }
  },
  options: {}                     // Optional: Additional configuration options
};
```

**Componentes de carga:**

| Componente | Obrigatório | Descrição |
|-----------|----------|-------------|
| `id` | Sim | O identificador da comunicação interativa (IC) a ser carregada |
| `prefill` | Opcional | Contém a configuração do serviço para preenchimento prévio de dados. |
| `prefill.serviceName` | Opcional | Nome do serviço de modelo de dados de formulário a ser chamado para preencher dados previamente |
| `prefill.serviceParams` | Opcional | Pares de valor-chave passados para o serviço de preenchimento prévio |
| `options` | Opcional | Propriedades adicionais compatíveis com a renderização do PDF - locale, includeAttachments, embedFonts, makeAccessible |

### Etapa 3: Implementar a Função de Integração

Crie uma função do JavaScript para iniciar a Interface do usuário do Associate e lidar com a comunicação de mensagem:

```javascript
function launchAssociateUI(icId, prefillService, prefillParams, options) {
  if (!icId) {
    console.error('IC ID required');
    return;
  }
   
  const data = {
    id: icId,
    prefill: {
      serviceName: prefillService || '',
      serviceParams: prefillParams || {}
    },
    options: options || {}
  };
   
  const AEM_URL = 'https://your-aem.adobeaemcloud.com/libs/fd/associate/ui.html';
  const win = window.open(AEM_URL, '_blank');
   
  if (!win) {
    alert('Please enable pop-ups for this site');
    return;
  }
   
  const readyHandler = (event) => {
    if (event.data && event.data.type === 'READY' && event.data.source === 'APP') {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  };
   
  window.addEventListener('message', readyHandler);
   
  // Fallback timeout in case READY message is missed
  setTimeout(() => {
    if (win && !win.closed) {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  }, 1000);
}
```

### Etapa 4: Chame a função

Chame a função com parâmetros apropriados:

```javascript
// Basic invocation with IC ID only
launchAssociateUI('12345', '', {}, {});

// With prefill service
launchAssociateUI('12345', 'IC_FDM', 
  { customerId: '101'}, {});

// With all parameters
launchAssociateUI('12345', 'IC_FDM', 
  { customerId: "101" }, 
  { locale: 'en', includeAttachments: "true" });
```

## Página Testar sua integração com um exemplo de HTML

Para observar como a Interface do usuário do Associate aparece no front-end e testar a integração, veja um exemplo simples de HTML. Essa página de exemplo permite inserir a ID da IC, configurar parâmetros de serviço de preenchimento prévio, definir opções do PDF e iniciar a interface do usuário Associar na instância de Publicação.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Associate UI Integration</title>
  <style>
    body { 
      font-family: sans-serif; 
      max-width: 600px; 
      margin: 50px auto; 
      padding: 20px; 
    }
    .form-group { 
      margin: 20px 0; 
    }
    label { 
      display: block; 
      margin-bottom: 5px; 
      font-weight: bold; 
    }
    input, textarea { 
      width: 100%; 
      padding: 8px; 
      border: 1px solid #ccc; 
      border-radius: 4px; 
      box-sizing: border-box;
    }
    textarea { 
      height: 80px; 
      font-family: monospace; 
    }
    button { 
      padding: 10px 20px; 
      margin: 5px; 
      cursor: pointer; 
      border-radius: 4px;
    }
    .btn-primary { 
      background: #007bff; 
      color: white; 
      border: none; 
    }
    .btn-primary:hover {
      background: #0056b3;
    }
    .error { 
      color: red; 
      font-size: 12px; 
      display: none; 
    }
  </style>
</head>
<body>
  <h1>Launch Associate UI</h1>
  
  <form id="form">
    <div class="form-group">
      <label>IC ID *</label>
      <input type="text" id="icId" placeholder="Enter Interactive Communication ID" required>
    </div>
    
    <div class="form-group">
      <label>Prefill Service</label>
      <input type="text" id="serviceName" placeholder="e.g., CustomerDataService">
    </div>
    
    <div class="form-group">
      <label>Service Parameters (JSON)</label>
      <textarea id="serviceParams" placeholder='{"customerId": "12345"}'>{}</textarea>
      <span id="paramsError" class="error">Invalid JSON format</span>
    </div>
    
    <div class="form-group">
      <label>Options (JSON)</label>
      <textarea id="options" placeholder='{"mode": "edit", "locale": "en_US"}'>{}</textarea>
      <span id="optionsError" class="error">Invalid JSON format</span>
    </div>
    
    <button type="button" onclick="reset()">Reset</button>
    <button type="button" class="btn-primary" onclick="launch()">Launch Associate UI</button>
  </form>

  <script>
    // Replace with your AEM Publish instance URL
    const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
    
    function validateJSON(str, errorId) {
      const err = document.getElementById(errorId);
      try {
        const obj = JSON.parse(str || '{}');
        err.style.display = 'none';
        return obj;
      } catch (e) {
        err.style.display = 'block';
        return null;
      }
    }
    
    function launch() {
      const icId = document.getElementById('icId').value.trim();
      if (!icId) { 
        alert('IC ID is required'); 
        return; 
      }
      
      const params = validateJSON(document.getElementById('serviceParams').value, 'paramsError');
      const opts = validateJSON(document.getElementById('options').value, 'optionsError');
      
      if (!params || !opts) { 
        alert('Please fix JSON errors before launching'); 
        return; 
      }
      
      const data = {
        id: icId,
        prefill: {
          serviceName: document.getElementById('serviceName').value.trim(),
          serviceParams: params
        },
        options: opts
      };
      
      const win = window.open(AEM_URL, '_blank');
      if (!win) { 
        alert('Pop-up blocked. Please enable pop-ups for this site.'); 
        return; 
      }
      
      const handler = (e) => {
        if (e.data && e.data.type === 'READY' && e.data.source === 'APP') {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      };
      
      window.addEventListener('message', handler);
      
      // Fallback timeout in case READY message is missed
      setTimeout(() => {
        if (win && !win.closed) {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      }, 1000);
    }
    
    function reset() {
      document.getElementById('form').reset();
      document.getElementById('serviceParams').value = '{}';
      document.getElementById('options').value = '{}';
      document.getElementById('paramsError').style.display = 'none';
      document.getElementById('optionsError').style.display = 'none';
    }
  </script>
</body>
</html>
```

### Como a amostra funciona

1. **Campo de ID da IC**: insira o identificador de Comunicação Interativa (obrigatório)
2. **Serviço de Preenchimento Prévio**: especifique o nome do serviço do Modelo de Dados de Formulário para preencher dados previamente
3. **Parâmetros de Serviço**: insira o objeto JSON com parâmetros a serem transmitidos para o serviço de preenchimento prévio
4. **Opções**: insira as opções de configuração para o PDF, por exemplo, localidade, includeAttachments, embedFonts, makeAccessible
5. **Botão Iniciar**: abre a interface do usuário Associar em uma nova janela e envia os dados de inicialização

## Exemplos de carga de dados

### Carga mínima (somente IC)

Use isso quando nenhum dado de preenchimento prévio for necessário:

```json
{
  "id": "12345",
  "prefill": { 
    "serviceName": "", 
    "serviceParams": {} 
  },
  "options": {}
}
```

### Com dados de preenchimento prévio

Use isso para preencher dinamicamente a IC com os dados do cliente:

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": {}
}
```

### Com configuração de opções

Use isso para especificar opções adicionais de renderização:

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": { 
      locale: "en_US",
      includeAttachments: "true",
      webOptimized: "false",
      embedFonts: "false",
      makeAccessible: "false"
  }
}
```

## Resolução de problemas

### Pop-up Bloqueado

**Problema**: a janela Associar Interface do Usuário não abre.

**Solução**:
- Habilitar pop-ups para o seu domínio nas configurações do navegador
- Verifique se `window.open()` é chamado a partir de uma ação do usuário (por exemplo, clique de botão)
- Testar com navegadores diferentes para identificar o comportamento de bloqueio

### Dados não carregam

**Problema**: a comunicação interativa é aberta, mas os dados não são preenchidos.

**Solução**:
- Verifique se a ID da IC está correta e se a IC foi publicada
- Verifique se há erros de JavaScript no console do navegador
- Verifique se a estrutura `postMessage` corresponde exatamente à especificação
- Verificar se o serviço de modelo de dados de formulário está configurado corretamente

### Erro de autenticação

**Problema**: o usuário recebe um erro de autenticação quando a Interface do Usuário Associada é aberta.

**Solução**:
- Configurar a autenticação SAML 2.0 na instância de publicação
- Verifique se o usuário faz parte do grupo **forms-associates**
- Verificar configurações de tempo limite da sessão

### Erros do CORS

**Problema**: erros de Compartilhamento de Recursos entre Origens no console.

**Solução**:
- Para desenvolvimento: Use `'*'` como origem de destino em `postMessage`
- Para produção: especifique o URL de origem exato do aplicativo
- Verifique se as configurações de CORS da instância de publicação permitem o domínio do aplicativo

<!--## Best Practices

When implementing the Associate UI integration, follow these best practices:

1. **Validation**: Always validate the IC ID and JSON payload before sending
2. **Error Handling**: Implement proper error handling for `window.open()` failures
3. **User Experience**: Display a loading indicator while the Associate UI initializes
4. **Memory Management**: Remove event listeners after initialization to prevent memory leaks
5. **Testing**: Test the integration with popup blockers enabled to ensure graceful handling
6. **User Permissions**: Verify users have appropriate access to the forms-associates group-->

## Consulte também

- [Associar a interface no Editor de comunicação interativa](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Comunicações interativas na nuvem](/help/forms/early-access-ea-features.md#interactive-communications-on-cloud)
- [Recursos de acesso antecipado](/help/forms/early-access-ea-features.md)