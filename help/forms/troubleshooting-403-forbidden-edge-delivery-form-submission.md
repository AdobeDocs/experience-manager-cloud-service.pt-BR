---
title: Solução de problemas de erros 403 proibidos no envio do formulário do Edge Delivery Services
description: Saiba como diagnosticar e resolver erros 403 proibidos ao enviar formulários do Edge Delivery Services para o AEM Publish. Este guia aborda causas comuns, incluindo CORS, regras do Dispatcher e problemas de Filtro de referenciador.
feature: Edge Delivery Services
role: Admin, Developer
exl-id: f397e059-f1b3-4afa-bd38-8f5fc591bb22
source-git-commit: d457bf9af377176222c2b96816fbbc4265e6b167
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 2%

---

# Solução de problemas de erros 403 proibidos no envio do formulário do Edge Delivery Services {#troubleshooting-403-forbidden-edge-delivery}

Ao enviar formulários do Edge Delivery Services para o AEM Publish, você pode encontrar um erro **403 Proibido**. Esse erro indica que o servidor está se recusando a processar a solicitação, normalmente devido a configurações de segurança. Este artigo ajuda a identificar e resolver as causas mais comuns desse problema.

## Descrição do problema

Os usuários recebem um erro **403 Proibido** ao enviar formulários do Edge Delivery Services para a Publicação do AEM. O erro aparece como:

- Código de status HTTP: 403
- Mensagem de erro: &quot;Proibido&quot; ou &quot;Acesso negado&quot;
- O envio do formulário falha sem chegar ao servlet de envio do AEM

Esse problema geralmente ocorre em integrações do Edge Delivery Services em que formulários hospedados em domínios do Edge (`.aem.live`, `.aem.page`, `.hlx.page`, `.hlx.live`) tentam enviar dados para instâncias de Publicação do AEM.

>[!IMPORTANT]
>
>Com configurações de resposta, vários sites podem ser hospedados usando o mesmo repositório. Cada domínio do site deve ser adicionado individualmente às listas de permissões para que os envios de formulários funcionem corretamente.
>
>**Exemplo:**
>
>- Repositório: `https://github.com/adobe/abc`
>- Site 1: `main--abc--adobe.aem.live`
>- Site 2: `main--abc1--adobe.aem.live`
>
>Incluir na lista de permissões Ambos os domínios precisam separar entradas para o envio de formulários de ambos os sites.

## Causas comuns e soluções

Um erro 403 Proibido no envio do formulário do Edge Delivery Services pode ter várias causas. Siga estas etapas de solução de problemas na ordem:

### &#x200B;1. Questões do CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens)

**Sintomas:**

- O console do navegador mostra mensagens de erro relacionadas ao CORS
- A guia Rede mostra a solicitação sendo bloqueada antes de acessar o servidor
- Mensagens de erro que mencionam &quot;Solicitação entre origens bloqueada&quot;

**Diagnóstico:**

1. Abrir Ferramentas do desenvolvedor do navegador (F12)
2. Verifique se há mensagens de erro do CORS na guia Console
3. Procurar mensagens como: `Access to fetch at 'https://publish-xxx.adobeaemcloud.com' from origin 'https://main--repo--owner.aem.live' has been blocked by CORS policy`

**Solução:**
Defina as configurações do CORS no AEM para permitir solicitações de domínios específicos do site do Edge Delivery:

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Sites - Add each site domain individually
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true

# Legacy Franklin domains (if still in use)
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>Substitua `main--abc--adobe.aem.live` e `main--abc1--adobe.aem.live` pelos domínios de site reais. Cada site hospedado no mesmo repositório requer uma entrada de configuração do CORS separada.

Para obter a configuração detalhada do CORS, consulte o [Guia de Configuração do CORS](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors).

### &#x200B;2. Regras do Dispatcher

**Sintomas:**

- O erro 403 ocorre sem mensagens CORS no console do navegador
- A solicitação chega ao servidor, mas é bloqueada pelo Dispatcher
- Erro antes de atingir a camada de aplicativo do AEM

**Diagnóstico:**

1. Verifique se o URL da solicitação corresponde a qualquer regra de filtro do Dispatcher
2. Revise a configuração do Dispatcher para `/filter` regras que podem bloquear solicitações POST
3. Verifique se o ponto de extremidade de envio do formulário é permitido na configuração do Dispatcher

**Solução:**
Atualize a configuração do Dispatcher para permitir solicitações de envio de formulário:

1. Verifique se as solicitações POST para pontos de extremidade de envio de formulário são permitidas
2. Adicionar regras de filtro apropriadas para domínios do Edge Delivery
3. Verifique se o caminho do servlet de envio não está bloqueado

Exemplo de configuração do filtro Dispatcher:

```apache
/filter {
  # Allow POST requests to form submission servlet
  /0100 { /type "allow" /method "POST" /url "/content/forms/af/*" }
  /0101 { /type "allow" /method "POST" /url "/adobe/forms/af/submit/*" }
  /0102 { /type "allow" /method "POST" /url "/content/forms/portal/submit/adaptiveform" }
}
```

### &#x200B;3. Problemas de Filtro referenciador

**Sintomas:**

- Erro 403 sem problemas com o CORS no console do navegador
- A solicitação chega ao AEM, mas é rejeitada pelo Filtro referenciador Sling
- Erro na camada de aplicativo do AEM

**Diagnóstico:**
Verifique os logs de erros do AEM quanto às mensagens de rejeição do Filtro referenciador:

1. [Acessar logs do AEM Cloud Service por meio da Cloud Manager](/help/implementing/cloud-manager/manage-logs.md)
2. Procurar entradas em `aemerror.log` que contenham:
   - &quot;Filtro referenciador rejeitado&quot;
   - &quot;org.apache.sling.security.impl.ReferrerFilter&quot;
   - Mensagens indicando falhas de validação do referenciador

**Exemplo de entrada de log:**

```
[ERROR] org.apache.sling.security.impl.ReferrerFilter Referrer filter rejected request with referrer 'https://main--abc--adobe.aem.live' for POST /content/forms/af/submit
```

**Solução:**
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

>[!IMPORTANT]
>
>**Para configurações de resposta:** Adicione cada domínio de site individualmente à matriz `allow.hosts`. Usar somente padrões de regex pode não ser suficiente para todos os cenários. Inclua domínios específicos e padrões de regex para uma cobertura abrangente.

>[!WARNING]
>
>O filtro referenciador não é uma fábrica de configurações OSGi, o que significa que apenas uma configuração pode ser ativada em um serviço do AEM de cada vez. Quando possível, evite adicionar configurações personalizadas de Filtro referenciador, pois isso substituirá as configurações nativas do AEM e poderá prejudicar a funcionalidade do produto.

## Etapas de diagnóstico

Siga estas etapas para identificar a causa específica do erro 403:

### Etapa 1: verifique o console do navegador

1. Abrir Ferramentas do desenvolvedor do navegador (F12)
2. Acesse a guia Console
3. Tentativa de envio de formulário
4. Procurar mensagens de erro relacionadas ao CORS

**Se houver erros de CORS:** Siga a solução de CORS acima.
**Se nenhum erro do CORS:**, vá para a Etapa 2.

### Etapa 2: Guia Verificar Rede

1. Abrir Ferramentas do desenvolvedor do navegador (F12)
2. Navegue até a guia Rede
3. Tentativa de envio de formulário
4. Verifique os detalhes da solicitação com falha
5. Observar cabeçalhos e status de resposta

**Se a solicitação não alcançar o servidor:** Provavelmente é um problema do Dispatcher.
**Se a solicitação atingir o servidor, mas falhar:** Provavelmente um problema de Filtro do Referenciador.

### Etapa 3: verificar logs do AEM

1. Acessar o Cloud Manager
2. Navegue até Ambientes → Seu ambiente → Logs
3. Baixar ou exibir `aemerror.log`
4. Procurar entradas no momento do envio do formulário
5. Procure por Filtro referenciador ou mensagens relacionadas à segurança

## Prevenção e práticas recomendadas

### &#x200B;1. Configuração Adequada Durante A Instalação

- Definir as configurações de CORS, Dispatcher e Filtro referenciador durante a configuração inicial do Edge Delivery Services
- incluir na lista de permissões **Para cada novo site:** Adicione o domínio específico a todas as perguntas (CORS, Filtro de Referenciador)
- Testar envios de formulários no ambiente de desenvolvimento antes de entrar em funcionamento

### &#x200B;2. Configurações específicas do ambiente

- Usar configurações diferentes para ambientes de desenvolvimento, de preparo e de produção
- Incluir domínios de host local para teste de desenvolvimento local
- incluir na lista de permissões **Documentar todos os domínios de site** que precisam de acesso de pesquisa para o seu repositório

### &#x200B;3. Monitoramento e registro

- Configurar monitoramento de log para rejeições de Filtro referenciador
- Implementar a manipulação adequada de erros no código de envio do formulário
- Usar ferramentas de desenvolvedor do navegador durante os testes

### &#x200B;4. Documentação e conhecimento da equipe

- **Manter um Registro** de todos os domínios de site usando o mesmo repositório
- Treinar a equipe de desenvolvimento nas etapas de solução de problemas
- Manter uma lista de verificação para configuração de formulário do Edge Delivery Services
- **Atualizar listas de permissões** sempre que novos sites forem criados a partir de repositórios existentes

## Gerenciamento de Domínio do Site para Configurações de Resposta

Com as arquiteturas Helix-5 e repless, siga estas diretrizes:

### Ao criar novos sites

1. **Identificar o domínio do site** (por exemplo, `main--newsite--adobe.aem.live`)
2. **Atualize a configuração do CORS** para incluir o novo domínio
3. **Atualize o Filtro do Referenciador** para incluir o novo domínio em `allow.hosts`
4. **Envio de formulário de teste** do novo site
5. **Documentar o novo domínio** no Registro do site

### Padrões de nomeação de domínio

- Padrão: `{branch}--{site}--{owner}.aem.live`
- Cada site recebe um domínio exclusivo mesmo ao compartilhar o mesmo repositório
- Domínios `.aem.live` e `.aem.page` podem ser usados

### Gerenciamento de configurações

- Usar entradas de domínio específicas em `allow.hosts` para melhorar a segurança
- Suplemente com padrões de regex para uma cobertura mais ampla
- Auditoria e atualização regulares de incluis na lista de permissões conforme os sites são adicionados ou removidos

## Recursos adicionais

- [Configuração de filtro referenciador com AEM Headless](/help/headless/deployment/referrer-filter.md)
- [Guia de Configuração do CORS](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [Noções Básicas Sobre Compartilhamento De Recursos Entre Origens](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)
- [Documentação do Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/publish-forms.md)

## Tópicos relacionados

- [Configurar ações de envio](/help/forms/configuring-submit-actions.md)
- [Serviço de envio de Forms](/help/forms/forms-submission-service.md)
- [Visão geral do Edge Delivery Services](/help/edge/overview.md)


**Precisa de ajuda adicional?** Se continuar com problemas após seguir estas etapas de solução de problemas, entre em contato com o Suporte ao Cliente da Adobe com:

- Suas mensagens de erro específicas
- Detalhes do ambiente do AEM Cloud Service
- **Todos os domínios de site do Edge Delivery Services** que precisam de acesso para envio de formulários
- Entradas de log relevantes a partir do momento do erro

**Precisa de ajuda adicional?** Se continuar com problemas após seguir estas etapas de solução de problemas, entre em contato com o Suporte ao Cliente da Adobe com:

- Suas mensagens de erro específicas
- Detalhes do ambiente do AEM Cloud Service
- Informações de domínio do Edge Delivery Services
- Entradas de log relevantes a partir do momento do erro
