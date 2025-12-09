---
title: Serviço de envio de Forms para o Edge Delivery Services
description: Armazene envios de formulários diretamente em planilhas usando o Serviço de envio de Forms hospedado pela Adobe. Saiba mais sobre instalação, configuração e uso da API para integração do Google Sheets, OneDrive e SharePoint.
keywords: Serviço de envio do Forms, formulários do Edge Delivery Services, integração de planilhas, formulários do Google Sheets, formulários do OneDrive, formulários do SharePoint, coleção de dados de formulário
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner, Intermediate
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: 8056b17d390cb84a11de9d329f04f04927a35646
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 1%

---

# Serviço de envio de Forms para o Edge Delivery Services

O Serviço de envio da Forms é a solução hospedada da Adobe que armazena automaticamente os dados de envio de formulário diretamente em suas planilhas preferidas: Google Sheets, Microsoft OneDrive ou SharePoint. Isso elimina a necessidade de infraestruturas complexas de back-end e, ao mesmo tempo, fornece coleta e gerenciamento de dados em tempo real.

## Visão geral

![Serviço de envio do Forms](/help/forms/assets/form-submission-service.png)
*Figura: Fluxo de trabalho do Serviço de envio do Forms - do envio de formulários ao armazenamento de planilhas*

+++ Quem Deve Usar Este Serviço?

**Perfeito para:**

- **Criadores de conteúdo** criando formulários de coleção de dados simples
- **Pequenas empresas** que precisam de fluxos de trabalho rápidos de formulário para planilha
- **Equipes de marketing** coletando informações de clientes potenciais
- **Organizadores de eventos** gerenciando registros

**Considere alternativas para:**

- Fluxos de trabalho complexos que exigem lógica personalizada
- Integrações corporativas com bancos de dados
- Forms que precisa de validação ou processamento avançado

+++

+++ Casos de uso comuns

| Caso de uso | Exemplo | Benefício da Planilha |
|----------|---------|-------------------|
| **Contate a Forms** | Consultas ao site → Google Sheets | Fácil acompanhamento e importação de CRM |
| **Registro de evento** | Inscrições na conferência → Excel Online | Rastreamento de participante em tempo real |
| **Geração de leads** | Inscrições no informativo → SharePoint | Análise de campanha de marketing |
| **Coleção de Comentários** | Respostas da pesquisa → Google Sheets | Visualização rápida de dados |

+++

## Principais benefícios

O serviço de envio da Forms oferece várias vantagens para uma coleta de dados simplificada:

+++ Configuração simplificada

- **Nenhuma infraestrutura de back-end** necessária - o Adobe hospeda o ponto de extremidade de envio
- **Integração direta** com plataformas de planilha populares
- **Mapeamento automático de dados** de campos de formulário para colunas de planilha

+++


+++ Gerenciamento de dados em tempo real

- **Captura instantânea de dados** - os envios aparecem imediatamente em sua planilha
- **Armazenamento estruturado** - colunas organizadas para facilitar a análise
- **Colaboração ao vivo** - vários membros da equipe podem acessar e analisar dados

+++

+++ Segurança interna e controle de acesso

- **Aproveita permissões existentes** - use os controles de compartilhamento da sua plataforma de planilha
- **segurança gerenciada pela Adobe** - ponto de extremidade de envio seguro com proteção de nível empresarial
- **Propriedade dos dados** - seus dados permanecem na plataforma de planilha escolhida

+++

## Pré-requisitos

Antes de configurar o Serviço de envio do Forms, verifique se você tem:



+++ Requisitos técnicos

- **Repositório do GitHub** configurado para seu projeto do Edge Delivery Services com o Bloco Adaptive Forms mais recente instalado
- **Aprovação de acesso** - repositório adicionado ao incluo na lista de permissões

+++

+++ Configuração da plataforma de planilha


Escolha uma das plataformas compatíveis:

- **Google Sheets** - Conta da Google com permissões de criação de planilhas
- **Microsoft OneDrive** - Conta do Microsoft 365 com acesso ao Excel Online
- **SharePoint** - Acesso ao SharePoint com permissões de lista/biblioteca

+++

+++ Permissões e acesso

- **Editar permissões** para a planilha de destino
- **Compartilhando recursos** para conceder acesso a `forms@adobe.com`
- **Permissões de geração de link** para a plataforma escolhida

+++

>[!TIP]
>
>**Novo no Edge Delivery Services?** Comece com o [Tutorial de introdução](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial) para configurar a base do seu projeto.

## Métodos de configuração

O Serviço de envio da Forms oferece duas abordagens de configuração. Escolha o método que melhor se adapta ao seu fluxo de trabalho:


+++ Escolha seu método de configuração

| Método | Melhor para | Tempo necessário | Nível técnico |
|--------|----------|---------------|-----------------|
| **[Configuração Manual](#manual-configuration)** | Criadores de conteúdo, configuração única | 10-15 minutos | Iniciante |
| **[Configuração de API](#api-configuration)** | Desenvolvedores, fluxos de trabalho automatizados | 5-10 minutos | Intermediário |

+++

+++ Configuração do projeto

Antes de configurar qualquer método, verifique se a base do projeto do AEM está pronta:

1. **Crie ou atualize seu projeto do AEM** com o Bloco Adaptive Forms mais recente ([Tutorial de Introdução](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial))

2. **Atualize`fstab.yaml`** na raiz do seu projeto:

   ```yaml
   # Replace with the path to your shared folder
   mountpoints:
     /: https://drive.google.com/drive/folders/your-shared-folder-id
   ```


3. **Compartilhar a pasta do projeto** com `forms@adobe.com` (são necessárias permissões de edição)

+++

## Configuração Manual

![Fluxo de trabalho do serviço de envio de formulários](/help/forms/assets/forms-submission-service-workflow.png)
*Figura: Concluir fluxo de trabalho para configuração manual do Serviço de Envio do Forms*

Siga estas instruções passo a passo para configurar seu formulário com o envio da planilha:



+++ Etapa 1: Criar A Definição Do Formulário

Crie a estrutura do formulário usando o Google Sheets ou o Microsoft Excel.

**Etapas de Criação do Formulário:**

1. **Abra a plataforma de planilha** (Google Sheets ou Microsoft Excel)
2. **Criar uma nova planilha** para o projeto de formulário
3. **Nomeie sua planilha** (deve ser `helix-default` ou `shared-aem`)
4. **Defina sua estrutura de formulário** usando o [guia de criação de formulário](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)

![Definição de Formulário](/help/forms/assets/form-submission-definition.png)
*Exemplo: definição de formulário com tipos de campo, rótulos e regras de validação*

>[!IMPORTANT]
>
>**Requisitos de nomenclatura da planilha**
>
>A folha de definição de formulário deve ser nomeada como:
>
>- `helix-default` (recomendado para formulários únicos)
>- `shared-aem` (para projetos de vários formulários)
>
>Outros nomes de planilha não serão reconhecidos pelo sistema.

**Ponto de Verificação de Validação:**

- A estrutura do formulário está completa com todos os campos obrigatórios
- A planilha está nomeada corretamente (`helix-default` ou `shared-aem`)
- Os tipos de campos e as regras de validação estão configurados corretamente

+++

+++ Etapa 2: Criar a Folha de Coleta de Dados

Configure uma planilha dedicada para receber dados de envio do formulário.

**Configuração de Folha de Dados:**

1. **Adicionar uma nova planilha** à planilha existente
2. **Nomeie a planilha exatamente`incoming`** (diferencia maiúsculas de minúsculas)
3. **Configurar cabeçalhos de coluna** que correspondam aos seus campos de formulário
4. **Salve a planilha** para garantir que as alterações sejam preservadas

![Planilha de entrada](/help/forms/assets/form-submission-incoming-sheet.png)
*Exemplo: planilha de entrada com cabeçalhos de coluna correspondentes aos campos de formulário*

>[!WARNING]
>
>**Requisito Crítico**
>
>A planilha deve ser nomeada exatamente `incoming` (minúsculas). Sem esta planilha:
>
>- Os envios de formulários serão rejeitados
>- Nenhum dado será armazenado
>- Os usuários verão erros de envio

**Ponto de Verificação de Validação:**

- `incoming` planilha existe em sua planilha
- Os cabeçalhos de coluna correspondem aos nomes dos campos de formulário
- A planilha é salva e acessível corretamente

>[!TIP]
>
>**Dica profissional:** copie os nomes de campos exatos da sua definição de formulário para garantir a correspondência perfeita entre campos de formulário e colunas da planilha.

+++

+++ Etapa 3: Compartilhar planilha com o serviço Adobe

Conceda acesso ao Adobe Forms Submission Service para sua planilha.

**Processo de Compartilhamento:**

1. **Clique no botão Compartilhar** no canto superior direito da planilha
2. **Adicionar a conta de serviço da Adobe:**

   - Email: `forms@adobe.com`
   - Nível de permissão: **Editor** (necessário para gravação de dados)

3. **Enviar o convite de compartilhamento**
4. **Copie o link da planilha** para a próxima etapa

   ![Compartilhar planilha de entrada](/help/forms/assets/form-submission-share-incoming.png)
   *Processo de compartilhamento passo a passo para conceder acesso ao serviço da Adobe*

**Instruções específicas da plataforma:**

**Planilhas Google:**

- Adicionar `forms@adobe.com` como editor
- Verifique se &quot;Qualquer pessoa com o link pode visualizar&quot; está ativado
- Copiar o link compartilhável

**Microsoft Excel (OneDrive/SharePoint):**

- Adicionar `forms@adobe.com` com permissões de edição
- Defina o compartilhamento de link como &quot;Qualquer pessoa com o link pode editar&quot;
- Copiar o URL de compartilhamento

  ![Copiar link da planilha de entrada](/help/forms/assets/form-submission-copy-link.png)
  *Exemplo: Copiando o link compartilhável para a configuração de formulário*

**Ponto de Verificação de Validação:**

- `forms@adobe.com` tem acesso de Editor à sua planilha
- O link da planilha foi copiado e está pronto para uso
- Permissões de compartilhamento permitem acesso externo

+++

+++ Etapa 4: Conectar Formulário à Planilha

Vincule a definição do formulário à planilha de envio.

**Conexão de Planilha de Formulário:**

1. **Abra a planilha de definição de formulário** (aquela com a planilha `helix-default` ou `shared-aem`)
2. **Localize a linha de campo Enviar** na definição do formulário
3. **Cole o link da planilha copiada** na coluna **Ação** para o campo Enviar
4. **Salve as alterações** na definição do formulário

   ![Vincular uma planilha](/help/forms/assets/form-submission-sheet-linking.png)

*Exemplo: Conectando a ação de envio à sua planilha de coleta de dados*

**Publicando Seu Formulário:**

1. **Abra o AEM Sidekick** no navegador
2. **Visualize seu formulário** para testar a configuração
3. **Publicar o formulário** para ativá-lo

**Validação Final:**

- O link da planilha é adicionado corretamente à ação Enviar campo
- A definição de formulário é salva e publicada
- A visualização do formulário mostra todos os campos corretamente
- O botão Enviar está configurado corretamente

>[!SUCCESS]
>
>**Instalação concluída!** Seu formulário agora está conectado ao Serviço de Envio do Forms. Teste enviando dados de amostra e verificando sua planilha `incoming`.

**Materiais de Referência:**

- [Planilha de exemplo completa](/help/forms/assets/spreadsheet.xlsx) com configuração adequada
- [documentação do AEM Sidekick](https://www.aem.live/docs/sidekick) para orientação de publicação

+++

## Configuração da API

O método da API permite que os desenvolvedores enviem dados de forma programática para o Serviço de envio do Forms, ideal para fluxos de trabalho automatizados e integrações personalizadas.


+++ Quando usar a API

**Perfeito para:**

- Sistemas automatizados de coleta de dados
- Implementações de formulário personalizado
- Integração com aplicativos existentes
- Fluxos de trabalho de envio de dados em massa

+++

+++ Pré-requisitos da API

Antes de usar a API, verifique se você tem:

- **Configuração da planilha** concluída (incluindo a planilha `incoming`)
- **Acesso ao serviço da Adobe** concedido a `forms@adobe.com`
- **ID do formulário** do seu formulário publicado
- **Informações do repositório** (organização e nome do site)

>[!IMPORTANT]
>
>**Etapas de Instalação Necessárias**
>
>A API exige a mesma configuração de planilha que a configuração manual:
>
>- A planilha `incoming` deve existir
>- `forms@adobe.com` deve ter acesso de Editor
>- A planilha deve ser publicada por meio do AEM Sidekick

+++

+++ Endpoint e autenticação de API

**URL Base:** `https://forms.adobe.com/adobe/forms/af/submit/{id}`

**Cabeçalhos obrigatórios:**

- `Content-Type: application/json`
- `x-adobe-routing: tier=live,bucket=main--[repository]--[organization]`

**Documentação da API:** [Referência completa da API](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)

+++

+++ Utilização do Postman

O Postman fornece uma interface simples para testar os envios de API.

**Instruções de Instalação:**

1. **Criar uma nova solicitação POST** no Postman
2. **Configurar o ponto de extremidade:** `https://forms.adobe.com/adobe/forms/af/submit/{id}`
3. **Substituir espaços reservados:**
   - `{id}` → Sua ID de formulário real
   - `[repository]` → Seu nome de repositório no GitHub
   - `[organization]` → Sua organização/nome de usuário do GitHub

**Solicitar configuração:**

```json
POST https://forms.adobe.com/adobe/forms/af/submit/your-form-id

Headers:
Content-Type: application/json
x-adobe-routing: tier=live,bucket=main--your-repo--your-org

Body (JSON):
{
        "data": {
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Mary",
            "age": "35",
            "subscribe": null,
            "email": "mary@gmail.com"
                }
}
```

**Resposta esperada:**

- **Código de Status:** `201 Created`
- **Os dados aparecem** na planilha `incoming` imediatamente

![tela do carteiro](/help/forms/assets/postman-api.png)
*Exemplo: envio bem-sucedido da API usando a interface do Postman*

+++

+++ Usando Linha de Comando (curl)

Para desenvolvedores que preferem prompt de terminal/comando, use curl para enviar dados programaticamente.

**Configuração da Linha de Comando:**

Substitua os seguintes espaços reservados nos comandos abaixo:

- `{id}` → Sua ID de formulário real
- `[repository]` → Seu nome de repositório no GitHub
- `[organization]` → Sua organização/nome de usuário do GitHub

>[!BEGINTABS]

>[!TAB macOS/Linux]

```bash
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" \
    --header "Content-Type: application/json" \
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" \
    --data '{
        "data": {
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Joe",
            "age": "35",
            "subscribe": null,
      "email": "joe@example.com"
                }
            }'
```

>[!TAB Prompt de Comando do Windows]

```cmd
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" ^
    --header "Content-Type: application/json" ^
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" ^
  --data "{\"data\": {\"startDate\": \"2025-01-10\", \"endDate\": \"2025-01-25\", \"destination\": \"Australia\", \"class\": \"First Class\", \"budget\": \"2000\", \"amount\": \"1000000\", \"name\": \"Joe\", \"age\": \"35\", \"subscribe\": null, \"email\": \"joe@example.com\"}}"
```

>[!TAB Windows PowerShell]

```powershell
$body = @{
  data = @{
    startDate = "2025-01-10"
    endDate = "2025-01-25"
    destination = "Australia"
    class = "First Class"
    budget = "2000"
    amount = "1000000"
    name = "Joe"
    age = "35"
    subscribe = $null
    email = "joe@example.com"
  }
} | ConvertTo-Json -Depth 3

Invoke-RestMethod -Uri "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" `
  -Method POST `
  -Headers @{"Content-Type"="application/json"; "x-adobe-routing"="tier=live,bucket=main--your-repo--your-org"} `
  -Body $body
```

>[!ENDTABS]

+++

+++ Resposta e verificação da API

**Resposta Bem-sucedida:**

```http
HTTP/1.1 201 Created
Connection: keep-alive
Content-Length: 0
X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
Date: Fri, 10 Jan 2025 13:06:10 GMT
Access-Control-Allow-Origin: *
```

**Verificação de dados:**

Após um envio bem-sucedido, verifique se os dados aparecem em sua planilha:

![planilha atualizada](/help/forms/assets/updated-sheet.png)
*Exemplo: dados gravados com êxito na folha de entrada via API*

**Validação de Resposta:**

- **Status HTTP:** `201 Created` indica envio bem-sucedido
- **X-Request-Id:** Identificador exclusivo para rastrear o envio
- **Os dados aparecem** na sua planilha `incoming` em segundos
- **Todos os campos de formulário** estão mapeados corretamente para colunas da planilha

+++

## Resolução de problemas



+++ Problemas comuns e soluções

**Problema: 403 Erro Proibido**

```
Causes: Missing or incorrect access permissions
Solutions:
- Verify forms@adobe.com has Editor access to your spreadsheet
- Check that your repository is added to the allowlist
- Confirm the x-adobe-routing header format
```

**Problema: 404 Erro Não Encontrado**

```
Causes: Incorrect Form ID or endpoint URL
Solutions:  
- Verify your Form ID is correct
- Check the API endpoint URL format
- Ensure your form is published and live
```


**Problema: Dados Não Aparecem na Planilha**

```
Causes: Missing 'incoming' sheet or permission issues
Solutions:
- Confirm 'incoming' sheet exists (case-sensitive)
- Verify column headers match form field names exactly
- Check forms@adobe.com has edit permissions
- Ensure spreadsheet is shared properly
```


**Problema: Erro de Formato JSON Inválido**

```
Causes: Malformed request body
Solutions:
- Validate JSON syntax using online JSON validators
- Ensure proper escaping of special characters
- Check quote marks and brackets are balanced
```


+++

+++ Obtendo ajuda

**Canais de suporte:**

- **Documentação da API:** [Referência do desenvolvedor](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)
- **Suporte da comunidade:** [Comunidade da Adobe Experience League](https://experienceleaguecommunities.adobe.com/?profile.language=pt)

+++

## Próximas etapas

Agora que você tem o Serviço de envio do Forms configurado, explore estes tópicos relacionados:


+++ Aprimorar seu Forms

- **[Criar Forms Avançado](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)** - Adicionar validação, lógica condicional e estilo personalizado
- **[Guia de Componentes de Formulário](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-components)** - Explorar tipos de campos de formulário disponíveis

+++

+++ Métodos de envio alternativos

- **[Envios de Publicação do AEM](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)** - Para fluxos de trabalho complexos e integrações corporativas
- **[Ações de Envio Personalizadas](/help/forms/configure-submit-actions-core-components.md)** - Manuseio de envio avançado

+++

+++ Gerenciamento de dados

- **[Form Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)** - Rastrear o desempenho e o uso do formulário
- **[Integração de Dados](/help/forms/configure-data-sources.md)** - Conectar formulários a bancos de dados e sistemas CRM

+++

## Resumo

O Serviço de envio do Forms fornece uma solução poderosa sem código para coletar dados de formulário diretamente em planilhas. Os principais benefícios incluem:

- **Configuração rápida** - Nenhuma infraestrutura de back-end necessária
- **Dados em tempo real** - Captura de envio imediata
- **Plataformas flexíveis** - Google Sheets, OneDrive ou SharePoint
- **Acesso à API** - Recursos de envio programático
- **Segurança corporativa** - pontos de extremidade gerenciados pela Adobe com controles de acesso

**Pronto para começar?** Siga o guia de [configuração manual](#manual-configuration) para obter uma configuração visual ou vá para [configuração de API](#api-configuration) para obter integração programática.
