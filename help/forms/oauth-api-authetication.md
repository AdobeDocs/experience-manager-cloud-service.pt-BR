---
title: Como configurar a autenticação de servidor para servidor do OAuth?
description: Saiba como configurar a autenticação de servidor para servidor do OAuth para o Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: fcc25eb44b485db69ec1c267f4cf8774c4279b24
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 2%

---


# Autenticação de servidor para servidor OAuth - recomendada

A autenticação de servidor para servidor do OAuth permite acesso seguro e baseado em token às APIs de comunicações da AEM Forms sem exigir interação com o usuário. Esse método é ideal para sistemas automatizados, serviços de back-end e integrações que precisam ser autenticadas de forma programática.

## Pré-requisitos

Antes de começar, verifique se os seguintes pré-requisitos foram atendidos:

* Verifique se você tem acesso ao [Adobe Developer Console](https://developer.adobe.com/console) específico do ambiente que usa.
* Atribua a função de Administrador do sistema ou Desenvolvedor no Adobe Admin Console para habilitar o acesso ao Adobe Developer Console.

## Como gerar um token de acesso usando a autenticação de servidor para servidor do OAuth?

Siga as etapas abaixo, que mostram como gerar um token de acesso do console do Adobe Developer e fazer sua primeira chamada de API por meio da autenticação de servidor para servidor OAuth.


1. Navegue até [Adobe Developer Console](https://developer.adobe.com/console)
2. Faça logon com sua Adobe ID

3. Criar novo projeto ou navegar até o projeto existente

   **Para criar um novo projeto:**

   1. Na seção **Início rápido**, clique em **Criar novo projeto**
   2. Um novo projeto é criado com um nome padrão

      ![Criar projeto ADC](/help/forms/assets/adc-home.png)

   3. Clique em **Editar projeto** no canto superior direito

      ![Editar Projeto](/help/forms/assets/adc-edit-project.png)

   4. Forneça um nome significativo (por exemplo, &quot;formsproject&quot;)
   5. Clique em **Salvar**

      ![Editar Nome do Projeto](/help/forms/assets/adc-edit-projectname.png)


   **Para navegar até o projeto existente:**

   1. Clique em **Todos os projetos** da Adobe Developer Console

      ![Pesquisar Projetos](/help/forms/assets/search-adc-project.png)

   2. Localize o projeto e clique em para abri-lo.

      ![Localizar Projetos](/help/forms/assets/locate-adc-project.png)


      >[!NOTE]
      >
      > Você pode adicionar a API e o método de autenticação ao seu projeto existente clicando em **Adicionar ao Projeto** > **API**\
      > ![Adicionar API ao projeto existente](/help/forms/assets/add-api-existing-project.png)
      > Para adicionar a API e o método de autenticação, execute as mesmas etapas descritas abaixo para o projeto existente.

4. Adicione diferentes APIs de comunicações do AEM Forms, dependendo de suas necessidades.

   **A Para APIs de Serviços de Documento**

   1. Clique em **Adicionar API**

      ![Adicionar API](/help/forms/assets/adc-add-api.png)

   2. Selecione as **APIs de comunicação do Forms**
      1. Na caixa de diálogo _Adicionar API_, filtre por **Experience Cloud**
      2. Selecione **&quot;APIs de comunicação do Forms&quot;**

         ![Adicionar API de comunicação do Forms](/help/forms/assets/adc-add-forms-api.png)


   3. Selecione o método de autenticação **Servidor a Servidor do OAuth**

      ![Selecionar método de autenticação](/help/forms/assets/adc-add-authentication-method.png)


   **B Para APIs Adaptive Forms Runtime**

   1. **Clique em Adicionar API**
No seu projeto, clique no botão **Adicionar API**

      ![Adicionar API](/help/forms/assets/adc-add-api.png)

   2. **Selecionar API de Entrega e Tempo de Execução do AEM Forms**
      1. Na caixa de diálogo _Adicionar API_, filtre por **Experience Cloud**
      2. Selecione **&quot;API de Entrega e Tempo de Execução do AEM Forms&quot;**
      3. Clique em **Avançar**

   3. **Método de Autenticação**
Selecione o método de autenticação **OAuth de servidor para servidor**.


      ![Selecionar método de autenticação](/help/forms/assets/adc-add-authentication-method.png)

5. **Adicionar Perfil de Produto**:

   1. Selecione o **Perfil de Produto** apropriado com base no nível de acesso necessário:

      | Tipo de acesso | Perfil do produto |
      |------------------|----------------------|
      | Acesso somente leitura | `AEM Users - author - Program XXX - Environment XXX` |
      | Acesso de leitura/gravação | `AEM Assets Collaborator Users - author - Program XXX - Environment XXX` |
      | Acesso administrativo completo | `AEM Administrators - author - Program XXX - Environment XXX` |

   2. Selecione o **Perfil do Produto** que corresponda à URL do Serviço do Autor (`https://author-pXXXXX-eYYYYY.adobeaemcloud.com`). Por exemplo: selecione `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`.

   3. Clique em **Salvar API configurada**. A API e o Perfil de produto são adicionados ao seu projeto

      ![Selecionar configuração do projeto](/help/forms/assets/adc-add-product-profile.png)

6. Gerar e salvar credenciais

   1. Navegar até o projeto no Adobe Developer Console
   2. Clique na credencial **OAuth de servidor para servidor**
   3. Exibir a seção **Detalhes da credencial**

      ![Exibir Credenciais](/help/forms/assets/adc-view-credential.png)

   4. Registrar credenciais de API

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

7. Geração de token de acesso

   **A Para Teste**

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

   **B Para produção**

   Gerar tokens programaticamente usando a API do Adobe IMS:

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

Agora você pode usar o token de acesso gerado para fazer uma chamada de API para ambientes de desenvolvimento, preparo ou produção.

>[!NOTE]
>
> Para saber mais sobre a implementação de servidor para servidor do OAuth para gerar token de acesso e fazer chamadas de API, [clique aqui](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation).

## Próximas etapas

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


