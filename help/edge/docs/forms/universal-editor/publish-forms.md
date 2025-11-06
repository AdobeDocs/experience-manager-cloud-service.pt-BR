---
title: Publicar Forms adaptável com o Edge Delivery Services
description: Saiba como publicar, configurar e acessar o Adaptive Forms usando o Edge Delivery Services para uso de produção.
feature: Edge Delivery Services
role: Admin, Developer
level: Intermediate
keywords: publicar formulários, Edge Delivery Services, configuração de formulário, CORS, filtro referenciador
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 0%

---

# Publicar Forms adaptável com o Edge Delivery Services

A publicação de um Formulário adaptável o disponibiliza no Edge Delivery Services para que os usuários finais acessem e enviem. Esse processo envolve três fases principais: publicação do formulário, configuração das configurações de segurança e acesso ao formulário em tempo real.

**O que você realizará:**

- Publicar o formulário no Edge Delivery Services
- Definir configurações de segurança para envio de formulário
- Acesse e verifique seu formulário publicado
- Configurar o roteamento de URL adequado e as políticas do CORS

## Pré-requisitos

- Formulário adaptável criado usando o modelo Edge Delivery Services
- Formulário testado e pronto para uso de produção
- Permissões de autor do AEM Forms
- Acesso ao Cloud Manager (para configuração de produção)
- Acesso do desenvolvedor ao código de bloco do formulário (para configuração de envio)

## Visão geral do processo de publicação

A publicação de formulários no Edge Delivery Services segue uma abordagem de três fases:

- **Fase 1: Publicação de Formulário** - Publique seu formulário na CDN e verifique o status da publicação
- **Fase 2: Configuração de Segurança** - Configurar políticas do CORS e filtros de referenciador para envios seguros
- **Fase 3: Acesso e Validação** - Testar a funcionalidade do formulário e validar o fluxo de trabalho completo

Cada fase se baseia na anterior para garantir uma implantação segura e funcional.

### Fase 1: Publicar seu formulário

+++ Etapa 1: Iniciar publicação

1. **Acessar o formulário**: Abra o formulário adaptável no Editor Universal
2. **Iniciar publicação**: clique no ícone **Publicar** na barra de ferramentas

   ![Clique em Publicar](/help/edge/docs/forms/universal-editor/assets/publish-form-ue.png)

+++


+++ Etapa 2: revisar e confirmar

1. **Revisar ativos de publicação**: o sistema mostra todos os ativos que estão sendo publicados, incluindo o formulário

   ![Ao clicar em Publicar](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-review.png)

2. **Confirmar publicação**: Clique em **Publicar** para continuar
3. **Verificar êxito**: procure a mensagem de confirmação

   ![Êxito na publicação](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-success.png)

+++


+++ Etapa 3: Verificar status de publicação

**Verificar status**: clique no ícone **Publicar** novamente para exibir o status atual

![Status de publicação](/help/edge/docs/forms/universal-editor/assets/publish-form-ue-validate.png)

**Ponto de Verificação de Validação:**

- Formulário mostra o status &quot;Publicado&quot; no editor
- Nenhuma mensagem de erro durante o processo de publicação
- O formulário aparece na lista de ativos publicados

+++


+++ Gerenciamento de Forms publicados

**Para desfazer a publicação de um formulário:**

1. Abrir o formulário no editor
2. Clique no menu de três pontos () no canto superior direito
3. Selecione **Cancelar publicação**

![Cancelar publicação do formulário](/help/edge/docs/forms/universal-editor/assets/unpublish-ue.png)

+++


### Fase 2: Definir configurações de segurança

+++ Por que a configuração de segurança é obrigatória

Para habilitar envios seguros de formulários, você deve definir configurações de segurança que:

- Permitir que o Edge Delivery Services envie dados para o AEM
- Impedir acesso não autorizado à sua instância do AEM
- Ativar o CORS (Cross-Origin Resource Sharing) para envios de formulários
- Filtrar solicitações para permitir somente domínios legítimos do Edge Delivery

>[!IMPORTANT]
>
>**Obrigatório para Produção**: essas configurações são obrigatórias para que os envios de formulários funcionem em ambientes de produção.

+++



+++ Etapa 1: configurar o URL de envio do formulário

**Propósito**: envios diretos de formulários para sua instância do AEM

**Local do Arquivo**: `blocks/form/constant.js` em seu projeto do Edge Delivery Services

**Exemplos de Configuração:**

```javascript
// Production Environment
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';

// Local Development Environment  
export const submitBaseUrl = 'http://localhost:4503';

// Staging Environment
export const submitBaseUrl = 'https://publish-staging-p120-e12.adobeaemcloud.com';
```

**Ponto de Verificação de Validação:**

- `constant.js` arquivo atualizado com a URL de publicação correta do AEM
- O URL corresponde ao seu ambiente (produção, preparo ou local)
- Nenhuma barra à direita no URL

+++



+++ Etapa 2: definir configurações do CORS

**Propósito**: permitir solicitações de envio de formulário de domínios do Edge Delivery Services

**Implementação**: adicionar a configuração do CORS ao Dispatcher do AEM ou à configuração do Apache

```apache
# Local Development Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Services - Preview/Stage Environment  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true

# Edge Delivery Services - Production Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

**Ponto de Verificação de Validação:**

- Regras do CORS aplicadas à configuração do dispatcher
- Todos os domínios necessários (localhost, hlx.page, hlx.live) estão incluídos
- Configuração implantada no ambiente de destino

**Documentação de referência:**

- [Guia de Configuração do CORS](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [Documentação de Filtro do Referenciador](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)

+++



+++ Etapa 3: configurar o filtro de referenciador

**Propósito**: restringir operações de gravação a domínios autorizados do Edge Delivery Services

**Método de implementação**: configurar via Cloud Manager no AEM as a Cloud Service

**Arquivo de configuração**: adicione à configuração OSGi do seu projeto

```json
{
  "allow.empty": false,
  "allow.hosts": [],
  "allow.hosts.regexp": [
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

**Detalhamento da Configuração:**

- **`allow.empty`**: rejeita solicitações sem cabeçalhos do referenciador
- **`allow.hosts.regexp`**: permite solicitações de domínios do Edge Delivery Services
- **`filter.methods`**: Aplica filtragem a esses métodos HTTP
- **`exclude.agents.regexp`**: Agentes do usuário excluídos da filtragem

**Ponto de Verificação de Validação:**

- Configuração de filtro referenciador implantada via Cloud Manager
- Configuração ativa na instância de publicação do AEM
- O envio do formulário de teste funciona no domínio Edge Delivery Services
- Domínios não autorizados estão impedidos de enviar formulários

**Documentação de referência:**

- [Configurar Filtro Referenciador via Cloud Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)

+++


### Fase 3: Acessar o formulário publicado



+++ Estrutura de URL do Edge Delivery Services

**Formato de URL Padrão:**

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
```

**Componentes da URL:**

- **`<branch>`**: Nome da ramificação Git (normalmente `main`)
- **`<repo>`**: Nome do repositório
- **`<owner>`**: Organização ou nome de usuário do GitHub
- **`<form_name>`**: Nome do seu formulário (minúsculas, hifenizadas)

**URLs Específicas do Ambiente:**

```
# Production Environment (.aem.live)
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form

# Preview Environment (.aem.page) 
https://main--universaleditor--wkndforms.aem.page/content/forms/af/wknd-form
```

+++



+++ Etapas finais de validação

**Verificar Acessibilidade de Formulário:**

1. **Testar carregamento do formulário**: visite a URL do formulário e confirme se ele é carregado corretamente
2. **Enviar formulário de teste**: preencha e envie o formulário para verificar o processamento de dados
3. **Verificar design responsivo**: Testar formulário em diferentes dispositivos e tamanhos de tela
4. **Validar segurança**: verifique se o CORS e o filtro de referenciador estão funcionando corretamente

**Resultados esperados:**

- Carregamentos de formulário sem erros
- Todos os campos de formulário são renderizados corretamente
- Processos de envio de formulário com sucesso
- Os dados aparecem no destino configurado (planilha, email etc.)
- Nenhum erro de console relacionado ao CORS ou às políticas de segurança

+++


## Próximas etapas


- [Configurar ações de envio de formulário](/help/edge/docs/forms/universal-editor/submit-action.md)
- [Estilo e tema de seus formulários](/help/edge/docs/forms/universal-editor/style-theme-forms.md)
- [Criar layouts de formulário responsivos](/help/edge/docs/forms/universal-editor/responsive-layout.md)
- [Adicionar proteção reCAPTCHA](/help/edge/docs/forms/universal-editor/recaptcha-forms.md)



