---
title: Publique o AEM Forms para o Edge Delivery Services.
description: Publique seus formulários do Edge Delivery Services de forma rápida e contínua.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: e4a71d1a513bebed67b9571a483871dc16c36daa
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Publicar o formulário adaptável no Edge Delivery Services

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email com o nome da sua organização GitHub e o nome do repositório do seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>


Quando o formulário estiver finalizado e pronto para uso, você poderá publicá-lo para torná-lo acessível aos clientes para coleta e envio de dados. A publicação garante que o formulário esteja disponível no Edge Delivery, permitindo que os usuários interajam com ele facilmente. Esse processo permite que os clientes preencham e enviem o formulário em tempo real, garantindo uma captura de dados eficiente e processamento simplificado.

## Pré-requisitos

* Um formulário criado usando o **modelo de Edge Delivery Services**. [Saiba mais](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) sobre como criar um formulário baseado em EDS.

## Publicar o formulário

Você pode publicar qualquer **Formulário adaptável baseado em EDS** no Edge Delivery seguindo estas etapas:

<!--1. Select the **Adaptive Form** that you want to publish and click the **Edit** ![edit icon](/help/forms/assets/edit.svg) icon.
   ![Select EDS-Based Form](/help/forms/assets/select-eds-based-form.png)-->

1. Abra o formulário adaptável no editor e clique no ícone **Publicar** no painel superior.
   ![Clique em Publicar](/help/forms/assets/publish-icon-eds-form.png)

1. Quando você clica em **Publicar**, é exibida uma tela ou um pop-up que mostra os ativos da publicação, incluindo o título do formulário. Neste exemplo, o modelo **Wknd_Form** é usado.
   ![Ao clicar em Publicar](/help/forms/assets/on-click-publish.png)

1. Clique em **Publicar** novamente e uma janela pop-up de confirmação será exibida, indicando que o formulário foi publicado agora.
   ![Êxito na publicação](/help/forms/assets/publish-success.png)

1. Para verificar o status de publicação do formulário, clique em **Publicar** novamente.
   ![Status de publicação](/help/forms/assets/publish-status.png)

1. Para **desfazer a publicação** de um formulário, abra o formulário no editor, clique no menu de três pontos no canto superior direito e clique em **Desfazer publicação**.
   ![Cancelar publicação](/help/forms/assets/unpublish--form.png)

## Ativar o envio de formulários no Edge Delivery configurando um filtro de referenciador para o AEM Publisher

Para garantir o envio seguro do formulário, você precisa configurar um **Filtro de Referenciador** no AEM Publisher. Esse filtro garante que somente solicitações autorizadas do Edge Delivery possam executar operações de gravação (POST, PUT, DELETE, COPY, MOVE), evitando modificações não autorizadas. A seguir estão as etapas fornecidas para configurar um Filtro referenciador para o AEM Publisher:

### Atualizar o URL da instância do AEM no Edge Delivery

Modifique o `submitBaseUrl` no arquivo **constant.js** dentro do bloco de formulários para especificar a URL da instância do AEM:

**Para Configuração na Nuvem:**

```js
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';
```

**Para Desenvolvimento Local:**

```js
export const submitBaseUrl = 'http://localhost:4503';
```

### Modificar a configuração do CORS

Ajuste as **configurações do CORS** para permitir solicitações de envio de formulário de domínios do Edge Delivery. Consulte o [Guia de Configuração do CORS](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors) para obter detalhes.

**Exemplo de configuração do CORS:**

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Franklin Stage
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  

# Franklin Live
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

Para desenvolvimento local, consulte a [documentação](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter) para habilitar o CORS da sua **URL de host da interface de desenvolvimento**.

### Configurar o filtro referenciador

Configure o **Filtro do referenciador** no AEM Cloud Service via Cloud Manager. [Saiba mais](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) sobre como configurar o filtro referenciador em uma instância do AEM Cloud Service usando um gerenciador de nuvem.

**Configuração JSON para o Filtro Referenciador:**

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

Essa configuração especifica quais métodos HTTP são filtrados, quais referenciadores são permitidos e quais agentes de usuário são excluídos do filtro. Ao implementar essas configurações, os **envios de formulários via Edge Delivery** serão protegidos e restritos somente a fontes autorizadas.

### Acessar O Formulário Adaptável Publicado

O formulário adaptável agora pode ser acessado via **Edge Delivery** usando este formato de URL:

```
https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
```

Por exemplo, a URL para o **Formulário Wknd** é:

```
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form
```


## Consulte também:

{{universal-editor-see-also}}

