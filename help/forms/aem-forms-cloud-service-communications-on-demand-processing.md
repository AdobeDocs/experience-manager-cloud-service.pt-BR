---
title: Como configurar APIs síncronas de comunicações interativas?
description: Configurar ambiente de desenvolvimento para APIs síncronas de comunicações interativas para o Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: 9401d96bcf5375dc20c33055343a5b895b4e9107
workflow-type: tm+mt
source-wordcount: '2573'
ht-degree: 1%

---


# Processamento de APIs síncronas das comunicações do AEM Forms as a Cloud Service

Este guia fornece instruções abrangentes para configurar e usar as APIs síncronas de comunicações da AEM Forms.

Saiba como configurar seu ambiente do AEM as a Cloud Service, habilitar o acesso à API e chamar APIs de comunicação usando a autenticação de servidor para servidor OAuth.

## Pré-requisitos

Para configurar um ambiente para executar e testar as APIs de comunicações do AEM Forms, verifique se você tem o seguinte:

### Acesso e permissões

Verifique se você tem os direitos de acesso e as permissões necessários antes de começar a configurar as APIs de comunicações.

**Permissões de usuário e função**

- Adobe ID criado em [https://account.adobe.com/](https://account.adobe.com/)
- Adobe ID associado ao email de sua organização
- Contexto de produto do Adobe Managed Services atribuído
- Função de desenvolvedor atribuída na Adobe Admin Console
- Permissão para criar projetos no Adobe Developer Console

>[!NOTE]
>
> Para saber mais sobre atribuição de funções e concessão de acesso a usuários, consulte o artigo [Adicionar usuários e funções](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles).

**Acesso ao Cloud Manager**

- Credenciais de logon para [Cloud Manager](https://my.cloudmanager.adobe.com)
- Acesso para visualizar e gerenciar os ambientes do seu programa
- Permissão para criar e executar pipelines de CI/CD
- Acesso aos detalhes e à configuração do ambiente

**Acesso ao Repositório Git**

- Acesso ao repositório Git do Cloud Manager
- Credenciais do Git para clonagem e envio de alterações

### Ferramentas de desenvolvimento

- **Node.js** para executar aplicativos de exemplo
- Última versão do **Git**
- Acesso a **Terminal/Linha de comando**
- **Editor de texto ou IDE** para editar arquivos de configuração (Código VS, IntelliJ etc.)
- **Postman** ou ferramenta semelhante para teste de API

>[!NOTE]
>
> Isso é uma vez por processo de ambiente que deve ser concluído antes de prosseguir com a configuração das APIs de comunicações do AEM Forms.

Agora vamos entender cada etapa em detalhes.

### Etapa 1: atualizar instância do AEM

Para atualizar a instância do AEM:

1. **Faça logon no Adobe Cloud Manager**
   1. Navegue até [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
   2. Faça logon com sua Adobe ID

2. **Navegue até a Visão Geral do Programa**
   1. Selecione seu programa na lista. Você será redirecionado para a página Visão geral do programa

3. **Localizar Detalhes do Ambiente**
   1. Selecione o ícone `ellipsis`(...) ao lado do nome do ambiente e clique em **Atualizar**
   2. Clique no botão **Enviar** e execute o pipeline de pilha completa sugerido.

      ![Atualizar ambiente](/help/forms/assets/update-env.png)

### Etapa 2: clonar repositório Git

Clonar o Repositório Git do Cloud Manager para gerenciar os arquivos de configuração da API.

1. **Localizar a Seção Repositório**
   1. Na página **Visão geral do programa**, clique na guia **Repositórios**
   2. Localize o nome do repositório e clique no menu de reticências (...)
   3. Copiar o URL do repositório

      >[!NOTE]
      >
      > Normalmente, o formato da URL é `https://git.cloudmanager.adobe.com/<org>/<program>/`

2. **Clonar Usando o Comando Git**

   1. Abra o prompt de comando ou o terminal
   2. Execute o comando `git clone` para clonar o repositório Git.

      ```bash
      git clone [repository-url]
      ```

      >[!NOTE]
      >
      > Para clonar o repositório Git, use as credenciais fornecidas pelo Adobe Cloud Manager.

      Por exemplo, para clonar o repositório Git, execute o seguinte comando:

      ```bash
      https://git.cloudmanager.adobe.com/formsinternal01/AEMFormsInternal-ReleaseSanity-p43162-uk59167/
      ```

      ![Clonagem do Repositório Git](/help/forms/assets/repo-clone.png)


**Opções de Integração do Repositório Git**

O Adobe Cloud Manager é compatível com ambas as opções de repositório:

- **Uso direto do Repositório Git da Cloud Manager**
   - Usar o repositório Git nativo do Cloud Manager
   - Integração integrada com pipelines

- **Integração com o Repositório Git gerenciado pelo cliente**
   - Conecte seu próprio repositório Git (GitHub, GitLab, Bitbucket etc.)
   - Configurar sincronização com o Adobe Cloud Manager

Para saber mais sobre como integrar o Adobe Cloud Manager e o Adobe Cloud Manager, consulte [Documentação de integração do Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/git-integration.html).

### Etapa 3: Acessar o ambiente do AEM Cloud Service e o terminal AEM Forms

Acesse os detalhes do ambiente do AEM Cloud Service para obter os URLs e os identificadores necessários para a configuração da API.

1. **Faça logon no Adobe Cloud Manager**
   1. Navegue até [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
   2. Faça logon com sua Adobe ID

2. **Navegue até a Visão Geral do Programa**
Selecione seu programa na lista. Você será redirecionado para a página Visão geral do programa

3. **Acessar e exibir o ambiente do AEM Cloud Service**

   Você pode visualizar ou acessar os detalhes do Ambiente do AEM Cloud Service usando uma das duas opções:

   - **Opção 1: Na Página Visão Geral**

      1. Na página **Visão geral do programa**
      2. Clique em **&quot;Ambientes&quot;** no menu do lado esquerdo.  É possível ver uma lista de todos os ambientes

         ![Exibir todos os ambientes](/help/forms/assets/all-env.png)

      3. Clique no nome do ambiente específico para exibir os detalhes

         ![Detalhes de Ambiente da Opção1](/help/forms/assets/option1-env.png)

   - **Opção 2: Da Seção Ambientes**

      1. Na página Visão geral do programa
      2. Localize a seção **Ambientes**
      3. Clique em **&quot;Mostrar tudo&quot;** para exibir todos os ambientes
      4. Clique no menu de reticências **(...)** ao lado do ambiente
         ![Detalhes de Ambiente da Opção1](/help/forms/assets/option2-env-details.png)
      5. Selecione **&quot;Exibir Detalhes&quot;**

         ![Detalhes de Ambiente da Opção1](/help/forms/assets/option1-env.png)

4. **Localizar seu Ponto de Extremidade do AEM Forms**

   Na página de detalhes do **Ambiente**, observe os seguintes detalhes:

   **URL de Serviço do Autor**

   - URL: `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`
   - Balde: author-pXXXXX-eYYYY
Exemplo: `https://author-p43162-e177398.adobeaemcloud.com`

   **URL do Serviço de Publicação**

   - URL: `https://publish-pXXXXX-eYYYYY.adobeaemcloud.com`
   - Compartimento: publish-pXXXXX-eYYYY
Exemplo: `https://publish-p43162-e177398.adobeaemcloud.com`

>[!NOTE]
>
> Para ver como acessar o Ambiente de acesso do AEM Cloud Service e o Ponto de extremidade do AEM Forms, consulte [Documentação de gerenciamento de ambientes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html).

### Etapa 4: configuração de acesso à API

Execute as seguintes etapas para configurar as APIs de comunicações do AEM Forms:

#### 4.1 Configuração de projeto do Adobe Developer Console

1. **Acessar o Adobe Developer Console**
   1. Navegue até [Adobe Developer Console](https://developer.adobe.com/console)
   2. Faça logon com sua Adobe ID

2. **Criar novo projeto**
   1. Na seção **Início rápido**, clique em **Criar novo projeto**
   2. Um novo projeto é criado com um nome padrão

      ![Criar projeto ADC](/help/forms/assets/adc-home.png)

   3. Clique em **Editar projeto** no canto superior direito

      ![Editar Projeto](/help/forms/assets/adc-edit-project.png)

   4. Forneça um nome significativo (por exemplo, &quot;formsproject&quot;)
   5. Clique em **Salvar**

      ![Editar Nome do Projeto](/help/forms/assets/adc-edit-projectname.png)

#### 4.2 Adicionar APIs de comunicação do Forms

É possível adicionar diferentes APIs de comunicações do AEM Forms, dependendo de suas necessidades.

**A Para APIs de Serviços de Documento**

1. Clique em **Adicionar API**

   ![Adicionar API](/help/forms/assets/adc-add-api.png)

2. Selecione as **APIs de comunicação do Forms**
   1. Na caixa de diálogo _Adicionar API_, filtre por **Experience Cloud**
   2. Selecione **&quot;APIs de comunicação do Forms&quot;**

   ![Adicionar API de comunicação do Forms](/help/forms/assets/adc-add-forms-api.png)


3. Selecione o método de autenticação **Servidor a Servidor do OAuth**

   ![Selecionar método de autenticação](/help/forms/assets/adc-add-authentication-method.png)

**B Para APIs do Forms Runtime**

1. **Clique em Adicionar API**
   - No seu projeto, clique no botão **Adicionar API**

   ![Adicionar API](/help/forms/assets/adc-add-api.png)

2. **Selecionar API de Entrega e Tempo de Execução do AEM Forms**
   - Na caixa de diálogo _Adicionar API_, filtre por **Experience Cloud**
   - Selecione **&quot;API de Entrega e Tempo de Execução do AEM Forms&quot;**
   - Clique em **Avançar**

   ![Adicionar API de tempo de execução](/help/forms/assets/add-runtime-api.png)


3. **Método de Autenticação**
   - Selecione o método de autenticação **OAuth de servidor para servidor**.


   ![Selecionar método de autenticação](/help/forms/assets/add-authentication-for-runtime-apis.png)

#### 4.3 Adicionar perfil de produto

Siga estas etapas para adicionar o Perfil do produto:

1. Selecione o **Perfil de Produto** apropriado com base no nível de acesso necessário:

   | Tipo de acesso | Perfil do produto |
   |------------------|----------------------|
   | Acesso somente leitura | `AEM Users - author - Program XXX - Environment XXX` |
   | Acesso de leitura/gravação | `AEM Assets Collaborator Users - author - Program XXX - Environment XXX` |
   | Acesso administrativo completo | `AEM Administrators - author - Program XXX - Environment XXX` |

2. Selecione o **Perfil do Produto** que corresponda à URL do Serviço do Autor (`https://author-pXXXXX-eYYYYY.adobeaemcloud.com`). Por exemplo: selecione `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`.

3. Clique em **Salvar API configurada**. A API e o Perfil de produto são adicionados ao seu projeto

   ![Selecionar configuração do projeto](/help/forms/assets/adc-add-product-profile.png)

#### 4.4 Gerar e salvar credenciais

1. **Acessar Suas Credenciais**

   1. Navegar até o projeto no Adobe Developer Console
   2. Clique na credencial **OAuth de servidor para servidor**
   3. Exibir a seção **Detalhes da credencial**

   ![Exibir Credenciais](/help/forms/assets/adc-view-credential.png)

2. **Credenciais da API de registro**

   ```text
   API Credentials:
   ================
   Client ID: <your_client_id>
   Client Secret: <your_client_secret>
   Technical Account ID: <tech_account_id>
   Organization ID: <org_id>
   Scopes: AdobeID,openid,read_organizations
   ```

#### 4.5 Geração de token de acesso

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
   > O token de acesso é válido por **24 horas**

**B Para produção**

Gerar tokens programaticamente usando o comando cURL:

**Credenciais necessárias:**

- ID do cliente
- Segredo do cliente
- Escopos (normalmente: `AdobeID,openid,read_organizations`)

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

#### 4.6 Registrar ID do cliente no ambiente do AEM

Para permitir que a ID do cliente do projeto ADC se comunique com a instância do AEM, registre-a usando um arquivo de configuração YAML e implante-a por meio de um Pipeline de configuração.

1. **Localizar ou Criar Diretório de Configuração**

   1. Navegue até o repositório clonado do Projeto AEM e navegue até a pasta `config`
   2. Se ele não existir, crie-o no nível raiz do projeto:

   ```bash
   mkdir config
   ```

2. Crie um novo arquivo chamado `api.yaml` no diretório `config`:

   ```bash
   touch config/api.yaml
   ```

3. Adicionar o seguinte código no arquivo `api.yaml`:

   ```yaml
   kind: "API"
   version: "1"
   metadata:
   envTypes: ["dev"]  # or ["prod", "stage"] for production environments
   data:
   allowedClientIDs:
       author:
       - "<your_client_id>"
       publish:
       - "<your_client_id>"
       preview:
       - "<your_client_id>"
   ```

   Veja a seguir uma explicação sobre os parâmetros de configuração:

   - **kind**: sempre definido como `"API"` (identifica como uma configuração de API)
   - **versão**: versão da API, normalmente `"1"` ou `"1.0"`
   - **envTypes**: matriz de tipos de ambiente à qual esta configuração se aplica
      - `["dev"]` - Somente ambientes de desenvolvimento
      - `["stage"]` - Somente ambientes de preparo
      - `["prod"]` - Somente ambientes de produção
   - **allowedClientIDs**: IDs do cliente com permissão para acessar sua instância do AEM
      - **author**: IDs de Cliente para a camada de autor
      - **publicar**: IDs de cliente para camada de publicação
      - **visualização**: IDs de cliente para camada de visualização

   Por exemplo, adicione o `allowedClientIDs` como `6bc4589785e246eda29a545d3ca55980` e envTypes como `dev`:

   ![Adicionando arquivo de configuração](/help/forms/assets/create-api-yaml-file.png)

4. **Confirmar e enviar alterações**

   1. Navegue até a pasta raiz do repositório clonado e execute os comandos abaixo:


   ```bash
       git add config/api.yaml
       git commit -m "Whitelist client id for api invocation"
       git push origin <your-branch>
   ```

   ![Enviar alterações do Git](/help/forms/assets/push-yaml-changes-in-git.png)


5. **Pipeline de configuração de instalação**

   1. **Fazer logon no Cloud Manager**
      1. Navegue até [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
      2. Faça logon com sua Adobe ID

   2. **Navegar até o seu programa**
Selecione seu programa na lista e você será redirecionado na página Visão geral do programa

   3. **Localizar o Cartão Pipelines**
      1. Localize o cartão **Pipelines** na página Visão geral do programa
      1. Clique no botão **&quot;Adicionar&quot;**

   4. **Selecionar tipo de pipeline**

      - **Para Ambientes De Desenvolvimento**: Selecione **&quot;Adicionar Pipeline De Não Produção&quot;**. Os pipelines de não produção são para ambientes de desenvolvimento e preparo

      - **Para Ambientes De Produção**: Selecione **&quot;Adicionar Pipeline De Produção&quot;**. Pipelines de produção exigem aprovações adicionais

        >[!NOTE]
        >
        > Nesse caso, crie um pipeline de não produção, pois um ambiente de desenvolvimento está disponível.

   5. **Configurar Pipeline - Guia Configuração**

      Na guia **Configuração**:

      a. **Tipo de pipeline**
      - Selecionar **&quot;Pipeline de Implantação&quot;**

      b. **Nome do pipeline**
      - Forneça um nome descritivo. Por exemplo, nomeie o pipeline como `api-config-pipieline`

      c. **Acionador da implantação**
      - **Manual**: implantar somente quando acionado manualmente (recomendado para configuração inicial)
      - **Sobre Alterações do Git**: implantação automática quando as alterações são enviadas para a ramificação

      d. **Comportamento de Falhas de Métricas Importantes**
      - **Perguntar sempre**: solicitar ação em caso de falhas (padrão)
      - **Falha imediata**: falha automática no pipeline em falhas de métrica
      - **Continuar imediatamente**: continuar apesar das falhas

      e. Clique em **&quot;Continuar&quot;** para prosseguir para a guia **Código Source**

      ![Pipeline de configuração](/help/forms/assets/add-config-pipeline.png)

   6. **Configurar Pipeline - Guia Código Source**

      Na guia **Source Code**:

      a. **Tipo de implantação**
      - Selecione **&quot;Implantação direcionada&quot;**

      b. **Opções de implantação**
      - Selecione **&quot;Config&quot;** (implantar somente arquivos de configuração). Informa ao Cloud Manager que é uma implantação de configuração.

      c. **Selecionar Ambiente de Implantação Elegível**
      - Escolha o ambiente em que deseja implantar a configuração. Nesse caso, é um ambiente `dev`.

      d. **Definir Detalhes do Código Source**

      - **Repositório**: selecione o repositório que contém seu arquivo `api.yaml`. Por exemplo, selecione o repositório `AEMFormsInternal-ReleaseSanity-p43162-uk59167`.
      - **Ramificação Git**: selecione sua ramificação. Por exemplo, nesse caso nosso código é implantado na ramificação `main`.
      - **Localização do Código**: Insira o caminho para o diretório `config`. Como o `api.yaml` está na pasta `config` da raiz, digite `/config`

      e. Clique em **&quot;Salvar&quot;** para criar o pipeline

      ![Pipeline de configuração](/help/forms/assets/confirm-pipeline-1.png)

6. **Implantar configuração**

   Agora que o pipeline foi criado, implante sua configuração `api.yaml`:

   1. **Da Visão Geral dos Pipelines**
      1. Na página Visão geral do programa, localize o cartão **Pipelines**
      2. Navegue até o pipeline de configuração recém-criado na lista. Por exemplo, procure o nome do pipeline criado (por exemplo, &quot;api-config-pipeline&quot;). Você pode ver detalhes do pipeline, incluindo o status e a última execução.

   2. **Iniciar a Implantação**
      1. Clique no botão **&quot;Compilação&quot;** (ou reproduza o ícone ▶) ao lado do seu pipeline
      2. Confirme a implantação, se solicitado, e a execução do pipeline começa

      ![executar o pipeline](/help/forms/assets/run-config-pipeline.png)

   3. **Verificar Implantação Bem-sucedida**
      - Aguarde a conclusão do pipeline.
         - Se for bem-sucedido, o status mudará para &quot;Sucesso&quot; (marca de seleção verde ✓).
         - Se falhar, o status mudará para &quot;Fail&quot; (vermelho ✗). Clique em **Baixar logs** para exibir os detalhes do erro.

           ![Êxito do pipeline](/help/forms/assets/pipeline-suceess.png)

      Agora, você pode começar a testar as APIs de comunicações do Forms. Para fins de teste, você pode usar o Postman, o curl ou qualquer outro cliente REST para chamar as APIs.

### Etapa 5: Especificações da API e testes

Agora que seu ambiente está configurado, você pode começar a testar as APIs de comunicação do AEM Forms usando a [interface do usuário do Swagger](#a-using-swagger-ui-for-api-testing) ou de forma programática desenvolvendo o aplicativo NodeJS.

Neste exemplo, vamos gerar uma PDF usando as APIs de serviços de documento com o modelo e o arquivo XDP.

#### A. Utilização da interface do usuário do Swagger para testes de API

A interface do Swagger fornece uma interface interativa para APIs de teste sem gravar código. Use o recurso **Experimentar** para invocar e testar a API de Serviço de Documento [gerar PDF](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm).

1. Navegue até a documentação da API
   - API Forms: [Referência da API Forms](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)
   - Serviços de documento: [Referência da API de serviços de documento](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)
Abra a documentação das [APIs de serviços de documento](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document) em seu navegador.
2. Expanda a seção **Geração de Documento** e selecione [Gera um formulário do PDF preenchível a partir de um modelo XDP ou PDF, opcionalmente com a mesclagem de dados](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm).
3. No painel direito, clique em **Experimente**.

   ![Teste do Swagger para a API](/help/forms/assets/api-doc-generation.png)
4. Insira os seguintes valores:

   | **Seção** | **Parâmetro** | **Valor** |
   |--------------|---------------|------------|
   | balde | Instância do AEM | Nome da instância do AEM sem o nome de domínio do Adobe (`.adobeaemcloud.com`) Por exemplo, use `p43162-e177398` como bucket. |
   | Segurança | Token de portador | Usar o token de acesso da credencial OAuth Server-to-Server do projeto do Adobe Developer Console |
   | Corpo | modelo | Carregue um XDP para gerar o formulário do PDF. Por exemplo, você pode usar [este XDP](/help/forms/assets/ClosingForm.xdp) para gerar um PDF. |
   | Corpo | dados | Um arquivo XML opcional que contém os dados a serem mesclados com o modelo para gerar um formulário PDF pré-preenchido. Por exemplo, você pode usar [este XML](/help/forms/assets/ClosingForm.xml) para gerar um PDF. |
   | Parâmetros | X-Adobe-Accept-Experimental | 1 |

5. Clique em **Enviar** para invocar a API

   ![Enviar API](/help/forms/assets/api-send.png)

6. Verifique a resposta na guia **Resposta**:
   - Se o código de resposta for `200`, significa que o PDF foi criado com êxito.
   - Se o código de resposta for `400`, significa que os parâmetros da solicitação são inválidos ou malformados.
   - Se o código de resposta for `500`, significa que há um erro interno do servidor.

   Nesse caso, o código de resposta é `200`, isso significa que o PDF foi gerado com êxito:

   ![Resposta da Revisão](/help/forms/assets/api-success.png)

   Agora você pode baixar o [PDF](/help/forms/assets/create-pdf.pdf) criado usando o botão **Baixar** e exibi-lo no visualizador do PDF:

   ![Exibir PDF](/help/forms/assets/create-pdf.png)

>[!NOTE]
>
> Para fins de teste, você também pode usar o [Postman](https://www.postman.com/), [curl](https://curl.se/) ou qualquer outro cliente REST para invocar as APIs do AEM.

#### B. Programaticamente desenvolvendo o aplicativo NodeJS

Desenvolva um aplicativo Node.js para gerar um formulário do PDF preenchível a partir de um modelo **XDP** e um arquivo de dados **XML** usando a **API de Serviços de Documento**

##### Pré-requisitos

- Node.js instalado em seu sistema
- Instância ativa do AEM as a Cloud Service
- Token de portador para autenticação de API do Adobe Developer Console
- Arquivo XDP de Exemplo: [ClosingForm.xdp](/help/forms/assets/ClosingForm.xdp)
- Arquivo XML de Exemplo: [ClosingForm.xml](/help/forms/assets/ClosingForm.xml)

Para desenvolver o aplicativo Node.js, siga o passo a passo do desenvolvimento:

##### Etapa 1: criar um novo projeto Node.js

Abra o cmd/terminal e execute os comandos abaixo:

```bash
# Create a new directory
mkdir demo-nodejs-generate-pdf
cd demo-nodejs-generate-pdf

##### Initialize Node.js project
npm init -y
```

![Criar novo projeto de nó js](/help/forms/assets/api-1.png)

##### Etapa 2: Instalar Dependências Necessárias

Instale as bibliotecas **node-fetch**, **dotenv** e **form-data** para fazer solicitações HTTP, ler variáveis de ambiente e manipular dados de formulário, respectivamente.

```bash
npm install node-fetch
npm install dotenv
npm install form-data
```

![instalar dependências npm](/help/forms/assets/api-2.png)

##### Etapa 3: atualizar package.json

1. Abra o cmd/terminal e execute o comando:

   ```bash
   code .
   ```

   ![abrir projeto no editor](/help/forms/assets/api-3.png)

   Ele abre o projeto no editor de código.

2. Atualize o arquivo `package.json` para adicionar `type` a `module`.

   ```bash
   {
   "name": "demo-nodejs-generate-pdf",
   "version": "1.0.0",
   "type": "module",
   "main": "index.js",
   }
   ```

   ![atualizar arquivo de pacote](/help/forms/assets/api-4.png)

##### Etapa 4: criar um arquivo .env

1. Criar arquivo .env no nível raiz de um projeto
2. Adicione a configuração a seguir e substitua os espaços reservados pelos valores reais da credencial servidor a servidor OAuth do projeto ADC.

   ```bash
   CLIENT_ID=<ADC Project OAuth Server-to-Server credential ClientID>
   CLIENT_SECRET=<ADC Project OAuth Server-to-Server credential Client Secret>
   SCOPES=<ADC Project OAuth Server-to-Server credential Scopes>
   ```

   ![criar arquivo de ambiente](/help/forms/assets/api-5.png)

   >[!NOTE]
   >
   > Você pode copiar o `CLIENT_ID`, `CLIENT_SECRET` e `SCOPES` do projeto do Adobe Developer Console.

##### Etapa 5: Criar src/index.js

1. Criar arquivo `index.js` no nível raiz do projeto
2. Adicione o código a seguir e substitua os espaços reservados pelos valores reais:

```javascript
// Import the dotenv configuration to load environment variables from the .env file
import "dotenv/config";

// Import fetch for making HTTP requests
import fetch from "node-fetch";
import fs from "fs";
import FormData from "form-data";

// REPLACE THE FOLLOWING VALUE WITH YOUR OWN
const bucket = <bucket-value>; // Your AEM Cloud Service Bucket name
const xdpFilePath = <xdp-file>;
const xmlFilePath = <xml-file>;

// Load environment variables
const clientId = process.env.CLIENT_ID;
const clientSecret = process.env.CLIENT_SECRET;
const scopes = process.env.SCOPES;

// Adobe IMS endpoint for obtaining an access token
const adobeIMSV3TokenEndpointURL = "https://ims-na1.adobelogin.com/ims/token/v3";

// Function to get an access token
const getAccessToken = async () => {
    console.log("Getting access token from IMS...");

    const options = {
        method: "POST",
        headers: {
            "Content-Type": "application/x-www-form-urlencoded",
        },
        body: `grant_type=client_credentials&client_id=${clientId}&client_secret=${clientSecret}&scope=${scopes}`,
    };

    const response = await fetch(adobeIMSV3TokenEndpointURL, options);
    const responseJSON = await response.json();

    console.log("Access token received.");
    return responseJSON.access_token;
};

// Function to generate PDF form from XDP and XML
const generatePDF = async () => {
    const accessToken = await getAccessToken();

    console.log("Generating PDF form from XDP and XML...");

    // Read XDP and XML files
    const xdpFile = fs.readFileSync(xdpFilePath);
    const xmlFile = fs.readFileSync(xmlFilePath);

    const url = `https://${bucket}.adobeaemcloud.com/adobe/document/generate/pdfform`;

    const formData = new FormData();
    formData.append("template", xdpFile, {
        filename: "form.xdp",
        contentType: "application/vnd.adobe.xdp+xml"
    });
    formData.append("data", xmlFile, {
        filename: "data.xml",
        contentType: "application/xml"
    });

    const response = await fetch(url, {
        method: "POST",
        headers: {
            Authorization: `Bearer ${accessToken}`,
            "X-Api-Key": clientId,
            "X-Adobe-Accept-Experimental": "1",
            ...formData.getHeaders()
        },
        body: formData,
    });

    if (response.ok) {
        const arrayBuffer = await response.arrayBuffer();
        fs.writeFileSync("generatedForm.pdf", Buffer.from(arrayBuffer));
        console.log("✅ PDF form generated successfully (saved as generatedForm.pdf)");
    } else {
        console.error("❌ Failed to generate PDF. Status:", response.status);
        console.error(await response.text());
    }
};

// Run the PDF generation function
generatePDF();
```

![criar index.js](/help/forms/assets/api-6.png)

##### Etapa 6: Executar o aplicativo

```bash
node src/index.js
```

![executar aplicativo](/help/forms/assets/api-7.png)

O PDF é criado na pasta `demo-nodejs-generate-pdf`. Navegue até a pasta para localizar o arquivo gerado chamado `generatedForm.pdf`.

![exibir pdf criado](/help/forms/assets/api-8.png)

Você pode abrir o [PDF](/help/forms/assets/create-pdf.png) gerado para exibi-lo.

## Resolução de problemas

### Problemas comuns e possíveis causas

#### Problema 1: Erro 403 proibido

**Sintomas:**

- As solicitações de API retornam `403 Forbidden`
- Mensagem de erro: *Acesso negado* ou *Permissões insuficientes*
- Ocorre mesmo com um token de acesso válido

**Causas possíveis:**

- Permissões insuficientes no Perfil de produto vinculado à credencial OAuth de servidor para servidor
- O grupo de usuários de serviço no AEM Author não tem as permissões necessárias nos caminhos de conteúdo necessários

#### Problema 2: Erro 401 não autorizado

**Sintomas:**

- As solicitações de API retornam `401 Unauthorized`
- Mensagem de erro: *Token inválido ou expirado*

**Causas possíveis:**

- Token de acesso expirado (válido por apenas 24 horas)
- ID do cliente e segredo do cliente incorretos ou incompatíveis
- Cabeçalhos de autenticação ausentes ou malformados na solicitação de API

#### Problema 3: Erro 404 não encontrado

**Sintomas:**

- As solicitações de API retornam `404 Not Found`
- Mensagem de erro: *Recurso não encontrado* ou *Ponto de extremidade de API não encontrado*

**Causas possíveis:**

- ID do cliente não registrada na configuração `api.yaml` da instância do AEM
- Parâmetro de bucket incorreto (não corresponde ao identificador de instância do AEM)
- ID de recurso inválida ou inexistente (formulário ou ativo)

#### Problema 4: Opção de autenticação de servidor para servidor não disponível

**Sintomas:**

- A opção OAuth Server-to-Server está ausente ou desabilitada no Adobe Developer Console

**Causa possível:**

- O usuário que está criando a integração não foi adicionado como um **Desenvolvedor** no Perfil de Produto associado

#### Problema 5: Falha na implantação do pipeline

**Sintomas:**

- Falha na execução do Pipeline de configuração
- Os logs de implantação mostram erros relacionados a `api.yaml`

**Causas possíveis:**

- Sintaxe YAML inválida (problemas de recuo, aspas ou formato de matriz)
- `api.yaml` foi colocado no diretório incorreto
- ID do cliente malformada ou incorreta na configuração


## Artigos relacionados

Para saber como configurar o ambiente para Batch (APIs assíncronas), consulte [Processamento em Lote das Comunicações do AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-batch-processing.md).
