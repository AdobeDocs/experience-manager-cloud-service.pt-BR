---
title: Como configurar a autenticação de servidor para servidor do OAuth?
description: Saiba como configurar a autenticação de servidor para servidor do OAuth para o Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: 6bd2e1698cceaf8fe47e19e0645d0782c916644a
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 2%

---


# Autenticação de servidor para servidor OAuth

A autenticação de servidor para servidor do OAuth permite acesso seguro e baseado em token às APIs de comunicações da AEM Forms sem exigir interação com o usuário. A autenticação de servidor para servidor OAuth é compatível com o Adobe Developer Console.

## Pré-requisitos

Antes de começar, verifique se os seguintes pré-requisitos foram atendidos:

* Verifique se você tem [acesso ao Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/access-rights) específico para o ambiente que usa.
* [Atribua a função de Administrador do Sistema ou Desenvolvedor no Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions) para habilitar o acesso ao Adobe Developer Console.

## Como gerar um token de acesso usando a autenticação de servidor para servidor do OAuth?

Siga as etapas abaixo para gerar um token de acesso do console do Adobe Developer e fazer sua primeira chamada de API por meio da autenticação de servidor para servidor OAuth.

### &#x200B;1. Configuração do projeto do Adobe Developer Console

1. Navegue até [Adobe Developer Console](https://developer.adobe.com/console)
2. Faça logon com sua Adobe ID

3. Criar novo projeto ou navegar até o projeto existente

>[!BEGINTABS]

>[!TAB Para criar um novo projeto]

1. Na seção **Início rápido**, clique em **Criar novo projeto**
2. Um novo projeto é criado com um nome padrão

   ![Criar projeto ADC](/help/forms/assets/adc-home.png)

3. Clique em **Editar projeto** no canto superior direito

   ![Editar Projeto](/help/forms/assets/adc-edit-project.png)

4. Forneça um nome significativo (por exemplo, &quot;formsproject&quot;)
5. Clique em **Salvar**

   ![Editar Nome do Projeto](/help/forms/assets/adc-edit-projectname.png)

>[!TAB Para navegar até o projeto existente]

1. Clique em **Todos os projetos** da Adobe Developer Console

   ![Pesquisar Projetos](/help/forms/assets/search-adc-project.png)

2. Localize o projeto e clique em para abri-lo.

   ![Localizar Projetos](/help/forms/assets/locate-adc-project.png)

>[!ENDTABS]

### &#x200B;2. Adicionar APIs do Forms

Adicione APIs do Forms com base no que você deseja fazer:

* **APIs de Comunicações do AEM Forms**: use quando precisar gerar, converter, reunir ou proteger documentos (PDF e formatos relacionados).
* **APIs Adaptive Forms Runtime** - use quando precisar renderizar, enviar ou processar o Adaptive Forms no tempo de execução.

>[!BEGINTABS]

>[!TAB Para APIs de comunicações do AEM Forms]

1. Clique em **Adicionar API**

   ![Adicionar API](/help/forms/assets/adc-add-api.png)

2. Selecione as **APIs de comunicação do Forms**
   1. Na caixa de diálogo _Adicionar API_, filtre por **Experience Cloud**
   2. Selecione **&quot;APIs de comunicação do Forms&quot;**

      ![Adicionar API de comunicação do Forms](/help/forms/assets/adc-add-forms-api.png)

   3. Clique em **Avançar**
   4. Selecione o método de autenticação **Servidor a Servidor do OAuth**

      ![Selecionar método de autenticação](/help/forms/assets/adc-add-authentication-method.png)

>[!TAB Para APIs Adaptive Forms Runtime]

1. **Clique em Adicionar API**

   ![Adicionar API](/help/forms/assets/adc-add-api.png)

2. **Selecionar API de Entrega e Tempo de Execução do AEM Forms**
   1. Na caixa de diálogo _Adicionar API_, filtre por **Experience Cloud**
   2. Selecione **&quot;API de Entrega e Tempo de Execução do AEM Forms&quot;**
      ![Adicionar API de comunicação do Forms](/help/forms/assets/adc-add-runtime-api.png)

   3. Clique em **Avançar**
   4. Selecione o método de autenticação **OAuth de servidor para servidor**.
      ![Selecionar método de autenticação](/help/forms/assets/adc-add-authentication-method.png)

>[!ENDTABS]

Você também pode adicionar a API e o método de autenticação ao seu projeto existente clicando em **Adicionar ao projeto** > **API**\
![Adicionar API ao projeto existente](/help/forms/assets/add-api-existing-project.png)

### &#x200B;3. Adicionar perfil de produto

O perfil de produto fornece permissões (ou autorização) para credenciais para acessar os recursos do AEM.

1. Selecione o **Perfil do Produto** que corresponda à URL da instância do AEM (`https://Service Type -Environment Type-Program XXX-Environment XXX.adobeaemcloud.com`).

   * **Tipo de Serviço** - especifica os serviços ou permissões associados à instância do AEM

   * **Tipo de ambiente** - especifica se o ambiente é para o serviço de Autor ou Publicação

   * **Programa XXX** - identifica a ID do programa Cloud Manager

   * **Ambiente XXX** - identifica a ID de ambiente específica dentro desse programa

   >[!NOTE]
   >
   > Os perfis de produto estão vinculados a uma instância específica do AEM (programa + ambiente). Sempre escolha o perfil que corresponde ao URL da instância.

2. Clique em **Salvar API configurada**. A API e o Perfil de produto são adicionados ao seu projeto

   ![Selecionar configuração do projeto](/help/forms/assets/adc-add-product-profile.png)

### &#x200B;4. Gerar e salvar credenciais

1. Navegar até o projeto no Adobe Developer Console
2. Clique na credencial **OAuth de servidor para servidor**
3. Exibir a seção **Detalhes da credencial**

   ![Exibir Credenciais](/help/forms/assets/adc-view-credential.png)

**Credenciais da API de registro**

```text
    API Credentials:
    ================
    Client ID: <your_client_id>
    Client Secret: <your_client_secret>
    Technical Account ID: <tech_account_id>
    Organization ID: <org_id>
    Scopes: AdobeID,openid,read_organizations
```

### &#x200B;5. Geração de token de acesso

Gere o token de acesso manual ou programaticamente:

>[!BEGINTABS]

>[!TAB Para Teste]

Gerar tokens de acesso manualmente no Adobe Developer Console:

1. **Navegar até o seu projeto**
   1. No Adobe Developer Console, abra o projeto
   2. Clique em **Servidor a servidor OAuth**

2. **Gerar token de acesso**
   1. Clique no botão **&quot;Gerar token de acesso&quot;** na seção API do projeto
   2. Copiar o token de acesso gerado

   ![Gerar token de acesso](/help/forms/assets/adc-access-token.png)

   >[!NOTE]
   >
   > O token de acesso é válido somente por **24 horas**

>[!TAB Para Produção]

Gerar tokens de forma programática usando a API do [Adobe IMS](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service):

**Credenciais necessárias:**

* ID do cliente
* Segredo do cliente
* Escopos (normalmente: `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`)

**Ponto de Extremidade do Token:**

```
https://ims-na1.adobelogin.com/ims/token/v3
```

**Solicitação de Exemplo (curl):**

```bash
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=client_credentials' \
-d 'client_id=<YOUR_CLIENT_ID>' \
-d 'client_secret=<YOUR_CLIENT_SECRET>' \
-d 'scope=AdobeID,openid,read_organizations'
```

**Resposta:**

```json
    {
    "access_token": "eyJhbGciOiJSUz...",
    "token_type": "bearer",
    "expires_in": 86399
    }
```

>[!ENDTABS]

Agora você pode usar o token de acesso gerado para fazer uma chamada de API para ambientes de desenvolvimento, preparo ou produção.

>
>
> Para saber mais sobre a implementação de servidor para servidor do OAuth para gerar token de acesso e fazer chamadas de API, [clique aqui](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation).

## Práticas recomendadas: gerenciamento de credenciais para desenvolvimento, armazenamento temporário e produção

* Sempre use credenciais separadas para desenvolvimento, armazenamento temporário e produção.

* Mapeie cada credencial para o URL de ambiente correto do AEM.

* Armazene segredos com segurança e nunca os confirme no controle de origem.

* Rastrear a validade do token de acesso, pois os tokens são válidos somente por 24 horas.

## Próximas etapas

Para saber como configurar o ambiente para APIs de comunicação síncrona do Forms, consulte [Processamento síncrono das comunicações do AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md).


## Artigos relacionados

Saiba como definir o ambiente para APIs de comunicações síncronas (sob demanda) e assíncronas (em lote) do Forms:

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="APIs síncronas" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="APIs síncronas"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="APIs de comunicações do AEM Forms - síncronas">APIs de Comunicações do AEM Forms - Síncronas</a>
                    </p>
                    <p class="is-size-6">Saiba como configurar um ambiente para APIs síncronas (sob demanda) de comunicações do Forms que geram ou processam documentos instantaneamente. </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="APIs de comunicações do AEM Forms - Assíncronas" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="APIs assíncronas"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="APIs assíncronas">APIs de Comunicações do AEM Forms - Assíncrono (Lote)</a>
                    </p>
                    <p class="is-size-6">Saiba como configurar um ambiente para APIs assíncronas (em lote) de comunicações do Forms que geram ou processam vários documentos de maneira programada.</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Saiba mais</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


