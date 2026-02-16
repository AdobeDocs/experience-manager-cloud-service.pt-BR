---
title: Integrar interface do usuário associada para comunicações interativas em tempo de execução
description: Saiba como integrar a interface do usuário do AEM Forms Associate ao seu aplicativo para permitir que profissionais voltados para o cliente gerem Comunicações interativas personalizadas em tempo real em instâncias de Publicação.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: f946ccea-86d0-4086-8208-9583b8206244
source-git-commit: 749ad181c7e9e59a0601e0eddd85b0bd0e761f08
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 1%

---

# Integrar a interface do usuário do Associate no seu aplicativo

<span> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.</span>

Este artigo explica como integrar a Interface do usuário do Associate ao seu aplicativo, permitindo que profissionais voltados para o cliente, como associados de campo e agentes de serviço, gerem Comunicações interativas personalizadas em tempo real em instâncias de Publicação.

## Pré-requisitos

Antes de integrar a Interface do usuário do Associate ao seu aplicativo, verifique se você tem:

- Comunicação interativa criada e publicada
- Navegador com suporte a pop-up ativado
- Os [usuários associados devem fazer parte do grupo ](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-roles#assign-a-role-to-users-and-groups) de forms-associates
- Autenticação configurada usando qualquer [mecanismo de autenticação com suporte do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/authentication) (por exemplo, SAML 2.0, OAuth ou manipuladores de autenticação personalizados)

>[!NOTE]
>
>- Este artigo demonstra a configuração de autenticação usando o SAML 2.0 com a [Microsoft Entra ID (Azure AD) como o Provedor de Identidade](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings).
>- Para Associar Interface, configurações SAML adicionais são necessárias além da configuração padrão explicada no artigo [Autenticação SAML 2.0](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0). Consulte a seção [Configurações SAML adicionais para interface do usuário associada](#additional-saml-configurations-for-associate-ui) para obter detalhes.

### Configurações SAML adicionais para Associar IU

Ao configurar a autenticação SAML 2.0 para a Interface de usuário associada, você deve aplicar as seguintes configurações específicas em seus arquivos de configuração OSGi.

#### Manipulador de autenticação SAML

O Manipulador de autenticação SAML é uma configuração de fábrica OSGi que permite várias configurações SAML para diferentes árvores de recursos. Isso permite implantações de AEM em vários sites e permite adicionar recursos de Interface do usuário Associada à configuração SAML existente.

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

O Sling Authenticator impõe autenticação para acessar recursos de interface do usuário associada em Publicar.

Atualizar o arquivo `org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json` em `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Filtro do Dispatcher

Adicione as seguintes regras para garantir que as APIs de comunicações interativas e a interface do usuário associada funcionem corretamente na instância de publicação.

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

Esta seção o orienta durante a inicialização da Interface do usuário do Associate a partir de seu próprio aplicativo. Siga estas etapas para começar rapidamente — começando com uma página de exemplo do HTML pronta para uso e configurando-a para o seu ambiente.

### Etapa 1: iniciar com a página de exemplo do HTML

Para testar e entender rapidamente como funciona a integração da Interface de usuário associada, use a seguinte página de exemplo do HTML. Copie esse código em um arquivo HTML e abra-o no navegador.

>[!NOTE]
>
> Este exemplo de HTML requer uma IC ID e um serviço de Preenchimento prévio. Você pode testá-lo usando sua ID de IC e o serviço de Preenchimento prévio de amostra &quot;FdmTestData&quot;.&quot;

A amostra do HTML fornece uma interface de formulário simples, onde você pode inserir seus detalhes de Comunicação interativa e iniciar a Interface do usuário Associada com um único clique.

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

### Etapa 2: configurar o URL da instância de publicação

Antes de iniciar a interface do usuário Associate, é necessário apontar a amostra para sua instância de publicação do AEM Forms Cloud Service.

No exemplo de HTML acima, localize a seguinte linha na seção `<script>`:

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

Substitua os valores de espaço reservado pelos detalhes do ambiente real:
- `{program-id}`: sua ID de programa do AEM Cloud Service
- `{env-id}`: Sua ID de ambiente

Por exemplo, se a ID do seu programa for `12345` e a ID do ambiente for `67890`, a URL se tornará:

```javascript
const AEM_URL = 'https://publish-p12345`-e67890.adobeaemcloud.com/libs/fd/associate/ui.html';
```

>[!NOTE]
>
> Por motivos de segurança, parâmetros como ID de comunicação interativa, serviço de preenchimento prévio e parâmetros de serviço não são transmitidos pelo URL. Em vez disso, esses parâmetros são transmitidos com segurança usando a API `postMessage` do JavaScript.

### Etapa 3: Entender a função de integração do JavaScript

O exemplo de HTML usa a seguinte função do JavaScript para iniciar a Interface do usuário associada. Esta função valida a ID de IC, constrói a carga de dados, abre a interface do usuário Associar em uma nova janela do navegador e envia os dados usando a API `postMessage` do navegador.

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

A função aceita quatro parâmetros: a ID da IC (obrigatória), o nome do serviço de preenchimento prévio, os parâmetros do serviço de preenchimento prévio e as opções adicionais. Esses parâmetros são estruturados na carga de dados conforme descrito abaixo.

### Etapa 4: Entender a estrutura da carga de dados

**Formato da Carga:**

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
| `prefill` | Opcional | Contém a configuração do serviço para preenchimento prévio de dados |
| `prefill.serviceName` | Opcional | Nome do serviço de modelo de dados de formulário a ser chamado para preencher dados previamente |
| `prefill.serviceParams` | Opcional | Pares de valor-chave passados para o serviço de preenchimento prévio |
| `options` | Opcional | Propriedades adicionais compatíveis com a renderização do PDF — locale, includeAttachments, embedFonts, makeAccessible |

#### Exemplos de carga de dados

**Carga mínima (somente IC ID)**

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

**Com Dados De Preenchimento Prévio**

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

**Com Opções de Renderização do PDF**

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
      "locale": "en_US",
      "includeAttachments": "true",
      "webOptimized": "false",
      "embedFonts": "false",
      "makeAccessible": "false"
  }
}
```

### Etapa 5: Insira a ID da IC e inicie a interface do usuário Associate

Agora você está pronto para iniciar a Interface do usuário do Associate usando a página de exemplo do HTML:

1. **Insira a ID de IC**: no campo **ID de IC**, insira o identificador da sua Comunicação Interativa publicada. Este é o único campo obrigatório.

1. **Configurar serviço de preenchimento prévio**: se quiser preencher previamente a IC com dados dinâmicos, insira o nome do serviço do Modelo de dados de formulário no campo **Serviço de preenchimento prévio**. Por exemplo, use `FdmTestData` para dados de exemplo.

   ![Exemplo de interface do HTML](/help/forms/assets/samplehtmlui.png)

1. **Clique em Iniciar Interface do Usuário Associada**: clique no botão **Iniciar Interface do Usuário Associada**. Uma nova janela do navegador é aberta com a Interface do usuário Associate, pré-carregada com sua Comunicação interativa.

Insira os dados e a Interface do usuário associada será exibida conforme mostrado abaixo:

![Associar interface](/help/forms/assets/associateui.png)

>[!NOTE]
>
> Se a janela não abrir, verifique se o navegador permite pop-ups para este site.


<!--**Add Service Parameters**: In the **Service Parameters (JSON)** field, enter a JSON object with the parameters your prefill service requires. For example:

   ```json
   {"customerId": "101", "accountNumber": "ACC-98765"}
   ```

  **Set PDF Options** (optional): In the **Options (JSON)** field, configure rendering options such as locale, attachments, or accessibility settings.-->

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
