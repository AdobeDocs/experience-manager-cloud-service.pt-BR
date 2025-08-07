---
title: Introdução ao Edge Delivery Services para AEM Forms usando o Universal Editor
description: Saiba como criar e publicar formulários de alto desempenho usando o Edge Delivery Services com criação no WYSIWYG do Universal Editor.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 6400662cb1c7a504f69db7091091452e99dd6ce9
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 0%

---


# Introdução ao Edge Delivery Services para AEM Forms usando o Universal Editor

| Método de criação | Guia |
|---------------------------------|-----------------------------------------------------------------------|
| **Editor Universal (WYSIWYG)** | Este artigo |
| **Criação baseada em documento** | [Tutorial baseado em documento](/help/edge/docs/forms/tutorial.md) |

O Edge Delivery Services para AEM Forms combina entrega da Web de alto desempenho com criação do WYSIWYG no Universal Editor. Este guia aborda a criação, personalização e publicação de formulários de carregamento rápido.

## O que você realizará

Ao final deste tutorial, você irá:

- Configurar um repositório GitHub com o bloco adaptável do Forms
- Criar um site do AEM integrado ao Edge Delivery Services
- Criar e publicar formulários usando o Editor Universal
- Configurar ambiente de desenvolvimento local

## Escolha seu caminho

Selecione a abordagem que corresponde ao seu cenário:

![Escolha seu Guia de Decisão de Caminho](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*Figura: Guia visual para ajudá-lo a escolher o caminho de implementação correto*

| **Caminho A: Novo Projeto** | **Caminho B: Projeto Existente** |
|----------------------------------------|-------------------------------------------|
| Comece com um modelo pré-configurado | Adicionar formulários ao projeto atual do AEM |
| **Recomendado para:** novas implementações | **Recomendado para:** AEM Sites existente |
| **O que você obtém:** Bloco de Forms pré-configurado | **O que você obtém:** o Forms foi adicionado ao site existente |
| **Etapas:** Modelo → Configuração → Forms | **Etapas:** Integração → Configuração → Forms |
| [Iniciar com Caminho A](#path-a-create-new-project-with-forms) | [Iniciar com Caminho B](#path-b-add-forms-to-existing-project) |

## Pré-requisitos

Antes de começar, verifique se você tem o seguinte:

### Acesso necessário

- **Conta do GitHub** com permissão para criar repositórios
- Acesso de criação ao **AEM as a Cloud Service**

### Requisitos técnicos

- **Noções básicas do Git**: operações de clonagem, confirmação e push
- **Tecnologias da Web**: fundamentos de HTML, CSS, JavaScript
- **Node.js** (recomenda-se a versão 16+) para desenvolvimento local
- **npm** ou **yarn** gerenciador de pacotes

### Conhecimento recomendado

- Noções básicas sobre os conceitos do AEM Sites
- Familiaridade com os princípios de design do formulário
- Experiência com editores do WYSIWYG

>[!TIP]
>
> Novo no AEM? Comece com o [Guia de Introdução do AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html).

## Caminho A: Criar novo projeto com o Forms

**Recomendado para:** novas implementações ou provas de conceito

O AEM Forms Boilerplate fornece um modelo pré-configurado com Bloco de Forms adaptável integrado.

### Visão geral das etapas

1. Configurar um repositório GitHub a partir do modelo
2. Instalar sincronização de código do AEM
3. Configurar conexão do projeto do AEM
4. Criar e publicar um site do AEM
5. Adicionar formulários usando o Editor Universal

Vamos analisar cada etapa:

+++Etapa 1: criar repositório GitHub a partir do modelo

1. **Acessar o modelo do AEM Forms Boilerplate**
   - Ir para [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)

   ![Modelo padronizado do AEM Forms](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *Figura: repositório padrão do AEM Forms com bloco Forms adaptável pré-configurado*

2. **Criar seu repositório**
   - Clique em **Usar este modelo** > **Criar um novo repositório**

   ![Criar Repositório a partir de Modelo](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *Figura: usando o modelo para criar um novo repositório*

3. **Definir configurações do repositório**
   - **Proprietário**: selecione sua conta ou organização do GitHub
   - **Nome do repositório**: escolha um nome descritivo (por exemplo, `my-forms-project`)
   - **Visibilidade**: Selecionar **Público** (recomendado para o Edge Delivery Services)
   - Clique em **Criar repositório**

   ![Configuração do repositório](/help/edge/docs/forms/assets/name-eds-repo.png)
   *Figura: configurando seu novo repositório com visibilidade pública*

**Validação:** confirme se você tem um novo repositório GitHub com base no modelo AEM Forms Boilerplate.

+++

+++Etapa 2: instalar sincronização de código do AEM

A sincronização de código do AEM sincroniza automaticamente as alterações de conteúdo entre o ambiente de criação do AEM e o repositório do GitHub.

1. **Instalar o aplicativo GitHub**
   - Ir para [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)

2. **Configurar permissões de acesso**
   - Selecionar **Selecionar apenas repositórios**
   - Escolha o repositório recém-criado
   - Clique em **Salvar**

   ![Instalação da Sincronização de Código do AEM](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *Figura: instalando a sincronização de código do AEM com permissões específicas do repositório*

**Ponto de verificação:** a Sincronização de código do AEM agora está instalada e tem acesso ao seu repositório.

+++

+++Etapa 3: configurar a integração do AEM

O arquivo `fstab.yaml` conecta seu repositório GitHub ao ambiente de criação do AEM para sincronização de conteúdo.

1. **Navegue até o repositório**
   - Acesse o repositório GitHub recém-criado
   - Você deve ver os arquivos de chapa do AEM Forms

2. **Criar o arquivo fstab.yaml**
   - Clique em **Adicionar arquivo** > **Criar novo arquivo** no diretório raiz
   - Nomeie o arquivo `fstab.yaml`

   ![Criando arquivo fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)
   *Figura: Criando o arquivo de configuração fstab.yaml*

3. **Adicionar detalhes da conexão com o AEM**

   Copie e cole a seguinte configuração, substituindo os espaços reservados:

   ```yaml
   mountpoints:
     /: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
   ```

   **Substituir:**
   - `<aem-author>`: Sua URL do autor do AEM as a Cloud Service (por exemplo, `author-p12345-e67890.adobeaemcloud.com`)
   - `<owner>`: seu nome de usuário ou organização do GitHub
   - `<repository>`: Seu nome de repositório

   **Exemplo:**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![Editando arquivo fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *Figura: configurando o ponto de montagem para a integração do AEM*

4. **Confirmar a configuração**
   - Adicione uma mensagem de confirmação: &quot;Adicionar configuração de integração do AEM&quot;
   - Clique em **Confirmar novo arquivo**

   ![Confirmando alterações de fstab](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *Figura: Confirmando a configuração fstab.yaml*

**Validação:** confirme a conexão do repositório GitHub com o AEM.

    >[!NOTE]
    >
    >Você está tendo problemas de build? Consulte [Solução de problemas de compilação do GitHub](#troubleshooting-github-build-issues).

+++

+++Etapa 4: criar um site do AEM conectado ao repositório do GitHub.

1. **Acessar o console do AEM Sites**
   - Faça logon na instância de criação do AEM as a Cloud Service
   - Navegar até **Sites**

   ![Console do AEM Sites](/help/edge/assets/select-sites.png)
   *Figura: acessando o console do AEM Sites*

2. **Iniciar criação de site**
   - Clique em **Criar** > **Site do modelo**

   ![Criar Opção de Site](/help/edge/docs/forms/assets/create-sites.png)
   *Figura: criando um novo site a partir do modelo*

3. **Selecione o modelo do Edge Delivery Services**
   - Escolha o modelo do **Site do Edge Delivery Services**
   - Clique em **Avançar**

   ![Seleção de Modelo de Site](/help/edge/docs/forms/assets/select-site-template.png)
   *Figura: seleção do modelo de site do Edge Delivery Services*

   >[!NOTE]
   >
   >**Modelo não disponível?** Se você não vir o modelo do Edge Delivery Services:
   >
   >1. Clique em **Importar** para carregar o modelo
   >2. Baixar modelos das [versões do GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)

4. **Configurar seu site**

   Insira as seguintes informações:

   | Texto | Valor | Exemplo |
   |-----------------|-----------------------------|-----------------------------------------|
   | **Título do site** | Nome descritivo do site | &quot;Meu projeto do Forms&quot; |
   | **Nome do Site** | Nome amigável de URL | &quot;my-forms-project&quot; |
   | **URL do GitHub** | O URL do seu repositório | `https://github.com/mycompany/my-forms-project` |

   ![Configuração do Site](/help/edge/docs/forms/assets/create-aem-site.png)
   *Figura: configurando seu novo site do AEM com a integração do GitHub*

5. **Concluir criação de site**
   - Revisar suas configurações
   - Clique em **Criar**

   ![Confirmar Criação de Site](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *Figura: confirmando a criação do site*

   **Sucesso!** Seu site do AEM foi criado e está conectado ao GitHub.

6. **Abrir no Editor Universal**
   - No console Sites, localize o novo site
   - Selecione a página `index`
   - Clique em **Editar**

   ![Editar Site no Editor Universal](/help/edge/docs/forms/assets/edit-site.png)
   *Figura: Abrindo seu site para edição*

   O Editor universal é aberto em uma nova guia, fornecendo recursos de criação do WYSIWYG.

   ![Interface de Editor Universal](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *Figura: seu site foi aberto no Editor Universal para edição no WYSIWYG*

**Validação:** Confirme se o site do AEM está pronto para a criação de formulários.

+++

+++Etapa 5: Publicar Seu Site

A publicação disponibiliza seu site no Edge Delivery Services para acesso global.

1. **Publicação rápida no console Sites**
   - Retorne ao console do AEM Sites
   - Selecionar as páginas do site (ou selecionar todas com Ctrl+A)
   - Clique em **Publicação rápida**

   ![Publicando Site do AEM](/help/edge/docs/forms/assets/publish-sites.png)
   *Figura: seleção de páginas para publicação rápida*

2. **Confirmar publicação**
   - No diálogo de confirmação, clique em **Publicar**

   ![Caixa de Diálogo de Publicação Rápida](/help/edge/docs/forms/assets/quick-publish.png)
   *Figura: Confirmando a ação de publicação*

   **Alternativa:** você também pode publicar diretamente do Editor Universal usando o botão Publicar.

   ![Publicar pelo Editor Universal](/help/edge/docs/forms/assets/qui.png)
   *Figura: Publicando diretamente do Editor Universal*

3. **Acessar seu site online**

   Seu site agora está ativo em:

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **Estrutura de URL Explicada:**
   - `<branch>`: ramificação GitHub (geralmente `main`)
   - `<repo>`: Seu nome de repositório
   - `<owner>`: seu nome de usuário ou organização do GitHub
   - `<site-name>`: O nome do seu site do AEM

   **Exemplo:**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

**Validação:** Confirme se seu site está ativo no Edge Delivery Services.

>[!TIP]
>
> **Padrões de URL:**
>
> - **Página inicial:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **Outras páginas:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**Próximo:** [Criar o primeiro formulário](#create-your-first-form)

+++

## Caminho B: Adicionar o Forms ao projeto existente

**Recomendado para:** AEM Sites existente com Edge Delivery Services

Se você já tiver um projeto do AEM usando o Edge Delivery Services, poderá adicionar recursos de formulário integrando o Bloco de Forms adaptável.

### Pré-requisitos para o Caminho B

- Projeto AEM existente compilado com [AEM Boilerplate XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk)
- Configuração do ambiente de desenvolvimento local
- Acesso Git ao repositório do projeto

**Usando o AEM Forms Boilerplate?** Se o seu projeto foi criado com o [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms), os formulários já estão integrados. Pule para [Criar o Primeiro Formulário](#create-your-first-form).

Vamos analisar cada etapa:

### Visão geral das etapas

1. Copiar arquivos de bloco adaptáveis do Forms
2. Atualizar configuração do projeto
3. Configurar regras do ESLint
4. Criar e confirmar alterações

+++Etapa 1: Copiar arquivos de bloqueio do Forms

1. **Navegar até o projeto local**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **Baixar os arquivos necessários do AEM Forms Boilerplate**

   Copie estes arquivos do [repositório do AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms):

   | Origem | Destino | Propósito |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | Funcionalidade de formulário principal |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | Integração do Editor universal |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | Estilo do editor |

3. **Suporte ao editor de atualizações**
   - Substitua o arquivo `/scripts/editor-support.js` pelo [editor-support.js da AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)

**Validação:** Confirme se os arquivos de bloco de formulário estão no seu projeto.

+++

+++Etapa 2: atualizar configuração do componente

1. **Atualizar modelo de seção**

   Abra `/models/_section.json` e adicione componentes de formulário aos filtros:

   ```json
   {
        "filters": [
        {
      "id": "section",
      "components": [
           "text",
           "image",
           "button",
        "form",
        "embed-adaptive-form"
      ]
       }
     ]
   }
   ```

   **O que isto faz:** Habilita componentes de formulário no seletor de componentes do Editor Universal.

**Validação:** a confirmação dos componentes do formulário aparece no Editor Universal.

+++

+++Etapa 3: configurar ESLint (Opcional)

**Por que esta etapa:** impede a listagem de erros de arquivos específicos do formulário e configura as regras de validação adequadas.

1. **Atualizar .eslintignore**

   Adicionar estas linhas a `/.eslintignore`:

   ```bash
   # Form block rule engine files
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

2. **Atualizar .eslintrc.js**

   Adicionar estas regras ao objeto `rules` em `/.eslintrc.js`:

   ```javascript
   {
     "rules": {
       // Existing rules...
   
       // Form component cell limits
    'xwalk/max-cells': ['error', {
         '*': 4, // default limit
      form: 15,
      wizard: 12,
      'form-button': 7,
      'checkbox-group': 20,
      checkbox: 19,
      'date-input': 21,
      'drop-down': 19,
      email: 22,
      'file-input': 20,
      'form-fragment': 15,
      'form-image': 7,
      'multiline-input': 23,
      'number-input': 22,
      panel: 17,
      'radio-group': 20,
      'form-reset-button': 7,
      'form-submit-button': 7,
      'telephone-input': 20,
      'text-input': 23,
      accordion: 14,
      modal: 11,
      rating: 18,
      password: 20,
         tnc: 12
       }],
   
       // Disable this rule for forms
       'xwalk/no-orphan-collapsible-fields': 'off'
     }
   }
   ```

**Validação:** Confirme se o ESLint funciona com componentes de formulário.

+++

+++Etapa 4: criar e implantar

1. **Instalar dependências e compilar**

   ```bash
   # Install any new dependencies
   npm install
   
   # Build component definitions
   npm run build:json
   ```

   **O que isto faz:**
   - Atualizações `component-definition.json` com componentes de formulário
   - Gera `component-models.json` com modelos de formulário
   - Cria `component-filters.json` com regras de filtragem

2. **Verificar arquivos gerados**

   Verifique se esses arquivos na raiz do projeto contêm objetos relacionados ao formulário:
   - `component-definition.json`
   - `component-models.json`
   - `component-filters.json`

3. **Confirmar e enviar alterações**

   ```bash
   git add .
   git commit -m "Add Adaptive Forms Block integration"
   git push origin main
   ```

**Validação:** confirme se o projeto inclui recursos de formulário.

+++

**Próximo:** [Criar Seu Primeiro Formulário](#create-your-first-form)

## Criar o primeiro formulário

**Aplica-se a:** usuários do Caminho A e Caminho B

Agora que seu projeto está configurado com recursos de formulário, vamos criar seu primeiro formulário usando a interface WYSIWYG do Universal Editor.

### Visão Geral do Processo de Criação de Formulário

1. **Adicionar bloco de formulário adaptável** à sua página
2. **Adicionar componentes de formulário** (entradas de texto, botões, etc.)
3. **Configurar propriedades do componente**
4. **Visualizar e testar** seu formulário
5. **Publicar** a página atualizada

Vamos analisar cada etapa:

+++Etapa 1: Adicionar bloco de formulário adaptável

1. **Abrir sua página no Editor Universal**
   - Navegue até o console **Sites** no AEM
   - Selecione a página à qual deseja adicionar um formulário (por exemplo, `index`)
   - Clique em **Editar**

   Sua página é aberta no Universal Editor para edição em WYSIWYG.

2. **Adicionar o componente de Formulário Adaptável**
   - Abra o painel **Árvore de conteúdo** (barra lateral esquerda)
   - Navegue até a seção onde deseja adicionar o formulário
   - Clique no ícone **Adicionar** (+)
   - Selecione **Formulário adaptável** na lista de componentes

   ![Adicionando Bloco de Formulário Adaptável](/help/edge/docs/forms/assets/add-adaptive-form-block.png)
   *Figura: adicionando um bloco de formulário adaptável à sua página*

**Validação:** Confirme se você tem um contêiner de formulário vazio.

+++

+++Etapa 2: Adicionar Componentes De Formulário

1. **Navegar até o bloco de formulários**
   - Na árvore de conteúdo, localize a seção Formulário adaptável recém-adicionada

   ![Bloco De Formulários Adaptáveis Adicionado](/help/edge/docs/forms/assets/adative-form-block.png)
   *Figura: bloco de formulário adaptável na árvore de conteúdo*

2. **Adicionar componentes de formulário**

   Você pode adicionar componentes de duas maneiras:

   **Método A: clique para adicionar**
   - Clique no ícone **Adicionar** (+) na seção do formulário
   - Selecione componentes na lista **Componentes de formulários adaptáveis**

   **Método B: arrastar e soltar**
   - Arraste os componentes diretamente do painel do componente para o formulário

   ![Adicionando componentes de formulário](/help/edge/docs/forms/assets/add-component.png)
   *Figura: adicionando componentes ao formulário*

   **Componentes iniciais recomendados:**
   - Entrada de texto (para nome, email)
   - Área de texto (para mensagens)
   - Botão de enviar

3. **Configurar propriedades do componente**
   - Selecionar qualquer componente de formulário
   - Use o painel **Propriedades** (barra lateral direita) para configurar:
      - Rótulos e espaços reservados
      - Regras de validação
      - Configurações de campo obrigatórias

   ![Painel de Propriedades do Componente](/help/edge/docs/forms/assets/component-properties.png)
   *Figura: configurando propriedades do componente*

4. **Visualizar o formulário**

   Seu formulário será semelhante a:

   ![Visualização de formulário concluída](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *Figura: Exemplo de formulário criado com o Editor Universal*

**Validação:** Confirme se o formulário está pronto para publicação.

>[!IMPORTANT]
>
> Lembre-se de publicar sua página depois de fazer alterações para ver as atualizações no navegador.

+++

+++Etapa 3: Publicar O Formulário

1. **Publicar pelo Editor Universal**
   - Clique no botão **Publicar** no Editor Universal

   ![Formulário de publicação](/help/edge/docs/forms/assets/publish-form.png)
   *Figura: Publicando seu formulário pelo Editor Universal*

2. **Confirmar publicação**
   - No diálogo de confirmação, clique em **Publicar**

   ![Confirmação de publicação](/help/edge/docs/forms/assets/publish-form1.png)
   *Figura: Confirmando a ação de publicação*

   Você verá uma mensagem de sucesso confirmando a publicação.

   ![Êxito na publicação](/help/edge/docs/forms/assets/publish-form2.png)
   *Figura: confirmação da publicação com êxito*

3. **Exibir seu formulário disponível**

   Seu formulário agora está disponível em:

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **Exemplo de URL:**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

   ![Página de formulário online](/help/edge/docs/forms/assets/publish-index-page.png)
   *Figura: sua página de formulário publicada no Edge Delivery Services*

**Parabéns!** Seu formulário agora está disponível e pronto para coletar envios.

+++

### Próximas etapas

Agora que você tem um formulário de trabalho, é possível:

- **Personalize o estilo** editando arquivos CSS e JavaScript
- **Adicionar recursos de formulário avançados** como regras de validação e lógica condicional
- **Configurar o desenvolvimento local** para iteração mais rápida
- **Criar formulários autônomos** para casos de uso específicos

>[!TIP]
>
> **Saiba mais:** [Criar formulários independentes no Editor Universal](/help/edge/docs/forms/universal-editor/create-forms.md)

## Configurar o ambiente de desenvolvimento local

**Recomendado para:** desenvolvedores que desejam personalizar o estilo e o comportamento do formulário

Um ambiente de desenvolvimento local permite fazer alterações e vê-las instantaneamente, sem passar pelo ciclo de publicação.

+++Configurar a CLI do AEM e o desenvolvimento local

1. **Instalar AEM CLI**

   A CLI do AEM simplifica as tarefas de desenvolvimento locais:

   ```bash
       npm install -g @adobe/aem-cli
   ```

2. **Clonar seu repositório**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   Substitua `<owner>` e `<repo>` pelos detalhes reais do GitHub.

3. **Iniciar o servidor de desenvolvimento local**

   ```bash
   aem up
   ```

   Isso inicia um servidor local com recursos de recarregamento a quente.

4. **Fazer personalizações**

   - Editar arquivos no diretório `blocks/form/` para estilo e comportamento do formulário
   - Modificar `form.css` para estilo
   - Atualizar `form.js` para comportamento

   **Ver alterações instantaneamente** no seu navegador em `http://localhost:3000`

5. **Implante suas alterações**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   Suas alterações estarão disponíveis em:
   - **Visualizar:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **Produção:** `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## Resolução de problemas

### Problemas comuns e soluções

+++Problemas de build do GitHub

**Problema:** falhas de compilação ou erros de listagem

**Solução 1: Manipular Erros de Linting**

Se encontrar erros de impressão:

1. Abrir `package.json` na raiz do projeto
2. Localizar o script `lint`:

   ```json
   "scripts": {
     "lint": "npm run lint:js && npm run lint:css"
   }
   ```

3. Desativar temporariamente a impressão:

   ```json
   "scripts": {
     "lint": "echo 'skipping linting for now'"
   }
   ```

4. Confirmar e enviar as alterações

**Solução 2: Erros de Caminho do Módulo**

Se você vir &quot;Não é possível resolver o caminho para o módulo &#39;/scripts/lib-franklin.js&#39;&quot;:

1. Navegue até `blocks/form/form.js`
2. Atualize o demonstrativo de importação:

   ```javascript
   // Change this:
   import { ... } from '/scripts/lib-franklin.js';
   
   // To this:
   import { ... } from '/scripts/aem.js';
   ```

+++

+++Problemas do editor universal

**Problema:** componentes de formulário não aparecem no Editor Universal

**Soluções:**

- Verifique se a sincronização de código do AEM está instalada e em execução
- Verifique se `fstab.yaml` tem a URL correta do autor do AEM
- Verifique se a instância do AEM tem acesso antecipado ativado
- Confirmar se `component-definition.json` inclui componentes de formulário

**Problema:** alterações não visíveis após a publicação

**Soluções:**

- Aguardar atualização do cache da CDN
- Verificar o cache do navegador (tentar modo incógnito/privado)
- Verifique se o formato correto de URL está sendo usado

+++

+++Problemas de funcionalidade de formulário

**Problema:** os envios de formulários não estão funcionando

**Soluções:**

- Verifique se você tem um componente de botão enviar
- Verificar a configuração da URL de ação do formulário
- Verificar regras de validação de formulário
- Testar primeiro no modo de visualização

**Problema:** problemas de estilo

**Soluções:**

- Verificar caminhos de arquivo CSS em `blocks/form/`
- Limpar cache do navegador
- Verificar sintaxe de CSS
- Testar no ambiente de desenvolvimento local

+++

