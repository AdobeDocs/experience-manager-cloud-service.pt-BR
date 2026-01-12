---
title: Como configurar a autenticação JWT (JSON Web Token)?
description: Saiba como configurar a autenticação JWT (JSON Web Token) para o Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
source-git-commit: d9eb9a93aba71a5ef5940c9d1d75cfd4e738c26b
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 3%

---


# Autenticação de servidor para servidor JWT (JSON Web Token)

A autenticação de servidor para servidor JWT no AEM Forms, especialmente para integrações do lado do servidor com o AEM as a Cloud Service, envolve um processo específico para interagir com segurança com os serviços da AEM. A autenticação de servidor para servidor JWT é compatível com o AEM Developer Console.

## Pré-requisitos

Antes de começar, verifique se os seguintes pré-requisitos foram atendidos:

* Verifique se você tem acesso ao [Adobe Cloud Manager](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html) específico do ambiente que usa.
* Atribua a função de [Administrador do Sistema ou Desenvolvedor para acessar o Adobe Cloud Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-manager/content/requirements/access-rights).

## Como gerar um token de acesso usando credenciais JWT?

Siga as etapas abaixo, que mostram como gerar um token de acesso a partir das credenciais JWT.

1. **Adobe Cloud Manager**

   1. Faça logon em sua [conta do Cloud Manager](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html).
   2. No programa selecionado, clique em **[!UICONTROL Visão Geral do Programa]**.

      ![Conta do Cloud Manager](/help/forms/assets/jwt-cloud-manager-landing.png)

   3. No seu programa, clique em três pontos e selecione **[!UICONTROL Developer Console]**.

      ![Console do desenvolvedor](/help/forms/assets/jwt-developer-console.png)

2. **AEM Developer Console**
   1. Fazer logon no AEM Developer Console
   2. Clique em **[!UICONTROL Integrações]**, localizado na barra de menu superior.

      ![Integrações](/help/forms/assets/jwt-integrations.png)

   3. Clique na opção para **[!UICONTROL Criar nova conta técnica]**.

      ![Criar nova conta técnica](/help/forms/assets/jwt-creae-new-tech-account.png)

   Depois de clicar em criar uma nova conta técnica, são geradas as informações necessárias para gerar o token de acesso, como ID do cliente e segredo do cliente, juntamente com outras informações técnicas da conta, incluindo chave privada, chave pública e data de expiração.

   ![Credenciais JWT](/help/forms/assets/jwt-credentials.png)


3. **Gerar e salvar credenciais**

   1. Registrar credenciais de API

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

4. **Geração de token de acesso**

   Gerar tokens programaticamente usando o comando cURL:

   **Credenciais necessárias:**

   * ID do cliente
   * Segredo do cliente
   * Escopos (normalmente: `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`)

   **Ponto de Extremidade do Token:**

   ```
   https://ims-na1.adobelogin.com/ims/token/v3
   ```

   **Solicitação de Exemplo (cURL):**

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


>[!NOTE]
>
> Para saber mais sobre as credenciais de serviço e como gerar um token de acesso usando a API do Adobe IMS, [clique aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials).

Agora você pode usar o token de acesso gerado para fazer uma chamada de API para ambientes de desenvolvimento, preparo ou produção.

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


