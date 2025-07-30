---
title: Introdução ao Edge Delivery Services para AEM Forms no Universal Editor - Tutorial do desenvolvedor
description: Este tutorial ajuda você a começar a usar um novo projeto do Adobe Experience Manager Forms (AEM). Dentro de dez a vinte minutos, você terá criado seu próprio Edge Delivery Services Forms no Universal Editor.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 0e7375adb146c370a189127838d736290d1860ad
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Introdução ao Edge Delivery Services para AEM Forms usando o Universal Editor (WYSIWYG)

| Versão | Link do artigo |
| -------- | ---------------------------- |
| Criação com base no Editor universal | Este artigo |
| Criação baseada em documento | [Clique aqui](/help/edge/docs/forms/tutorial.md) |


<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email de seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> com o nome da organização do GitHub e o nome do repositório. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>

Na era digital de hoje, formulários amigáveis são essenciais para todas as organizações. O Edge Delivery Services Forms é criado usando o Editor universal, que oferece recursos do WYSIWYG (what-you-see-is-what-you-get, o que você vê é o que você obtém). Ele fornece uma interface moderna e intuitiva para a criação eficiente de formulários.

O AEM Forms fornece um bloco, conhecido como Bloco adaptável do Forms, para ajudar você a criar facilmente o Edge Delivery Services Forms para capturar e armazenar dados. Você pode [criar um novo Projeto do AEM pré-configurado com o Bloco do Adaptive Forms](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) ou [adicionar o Bloco do Adaptive Forms a um Projeto do AEM existente](#add-adaptive-forms-block-to-your-existing-aem-project).

![Fluxo De Trabalho Do Repositório Github](/help/edge/assets/repo-workflow.png){width=auto}

Este tutorial o orienta por meio da criação, visualização e publicação de seu próprio formulário com um projeto do Adobe Experience Manager Site novo ou existente usando a criação do WYSIWYG no Universal Editor.

## Pré-requisitos

* Você tem uma conta GitHub e compreende as noções básicas sobre Git.
* Você entende as noções básicas do HTML, CSS e JavaScript.
* Você tem o Node/npm instalado para desenvolvimento local.

## Criar um novo projeto do AEM pré-configurado com o Bloco Adaptive Forms

O modelo do AEM Forms Boilerplate inicia rapidamente com um projeto do AEM pré-configurado com o Bloco de Forms adaptável. É a maneira mais rápida e fácil de seguir as práticas recomendadas da AEM e começar a criar formulários.

### Introdução ao modelo de repositório padronizado do AEM Forms

1. Crie um repositório GitHub para seu projeto do AEM. Para criar um repositório:
   1. Ir para [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![Modelo do AEM Forms](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. Clique na opção **Usar este modelo** e selecione a opção **Criar um novo repositório**.

      ![Criar novo repositório usando o Modelo do AEM Forms](/help/edge/docs/forms/assets/use-eds-form-template.png)

      A tela **Criar um novo repositório** é aberta.

   1. Na tela **Criar um novo repositório**, selecione o **proprietário** e especifique o **Nome do repositório**. A Adobe recomenda definir o repositório como **Público**. Então, selecione a opção **pública** e clique em **Criar Repositório**.

      ![Definir o repositório como público](/help/edge/docs/forms/assets/name-eds-repo.png)

1. Instale o aplicativo GitHub de sincronização de código da AEM em seu repositório. Para instalar:
   1. Ir para [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. Na tela **Instalar sincronização de código do AEM**, selecione a opção **Selecionar apenas repositórios** e selecione o repositório recém-criado. Clique em **Salvar**.

   ![Definir o repositório como público](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. Agora vincule o repositório GitHub criado por meio do AEM Forms Boilerplate ao ambiente de criação do AEM Project. Para conectar:

   1. Vá para o repositório GitHub criado anteriormente usando a Matriz do AEM Forms.
   1. Adicione o arquivo **fstab.yaml** à pasta raiz.

      ![abrir arquivo fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)

   1. Adicione o ponto de montagem do seu projeto ao arquivo **fstab.yaml**. Adicione o URL da instância de criação do AEM as a Cloud Service.

      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![editar arquivo fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. Confirme o arquivo **fstab.yaml** depois de adicionar a referência e tudo ficará bem.

      ![confirmar as alterações](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      Se você encontrar problemas de compilação, consulte [Solução de problemas de compilação do GitHub](#troubleshooting-github-build-issues).

### Criar um novo projeto do AEM

Agora que você tem um projeto GitHub, pode prosseguir para criar e publicar um novo projeto do AEM na instância de criação do AEM as a Cloud Service.

1. Para criar um novo projeto do AEM:

   1. Faça logon na instância de criação do AEM as a Cloud Service e selecione **Sites**.

      ![selecionar sites](/help/edge/assets/select-sites.png)

   1. Clique em **Criar** > **Site do modelo**.

      ![criar-sites](/help/edge/docs/forms/assets/create-sites.png)

   1. Selecione o modelo de Site do Edge Delivery Services e clique em **Próximo**.

      ![selecionar-modelo-site](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * Se o modelo de site do Edge Delivery Services não estiver disponível na instância de criação, clique no botão Importar para fazer upload do modelo.
      > * Você pode baixar os modelos de site do Edge Delivery Services no [GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases).

   1. Insira os seguintes detalhes para criar um novo projeto do AEM:
      * **Título do site** - Adicione um título descritivo para o site.
      * **Título do site** - Use o `site-name` que você definiu na etapa anterior.
      * **URL do GitHub** - Use a URL do projeto GitHub criado na etapa anterior.

      ![criar Site do AEM](/help/edge/docs/forms/assets/create-aem-site.png)

   1. A caixa de diálogo **Criar Site** é exibida. Clique em **OK**.

      ![clique em OK](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      Em apenas alguns minutos, o novo projeto do AEM será criado.

   1. Navegue até o projeto do AEM recém-criado no console Sites e clique em **Editar**.
Nesse caso, a página `index.html` é usada para ilustração.

      ![editar site do AEM](/help/edge/docs/forms/assets/edit-site.png)

      O Projeto AEM é aberto no Editor universal em uma nova guia, permitindo a criação no WYSIWYG. Agora você pode editar seu projeto do AEM.

      ![Aberturas de site no Editor Universal](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. Publicar o projeto criado no AEM

   Depois de concluir a edição do projeto do AEM, publique-o. Para publicar:

   1. No console Sites, selecione todas as páginas do Projeto do AEM e clique em **Publicação rápida**.

      ![publicar Projeto do AEM Sites](/help/edge/docs/forms/assets/publish-sites.png)

   1. A caixa de diálogo de confirmação **Publicação rápida** é exibida. Clique em **Publicar** para iniciar o processo de publicação.

      ![Caixa de diálogo de confirmação de Publicação Rápida](/help/edge/docs/forms/assets/quick-publish.png)

      Como alternativa, você pode publicar as páginas do Projeto do AEM diretamente da interface do usuário do Universal Editor.

      ![Caixa de diálogo de confirmação de Publicação Rápida](/help/edge/docs/forms/assets/qui.png)

   Parabéns! Você tem um novo site em execução em `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   * `<branch>` refere-se à ramificação do seu repositório GitHub.
   * `<repository>` indica seu repositório GitHub.
   * `<owner>` refere-se ao nome de usuário da sua conta GitHub que hospeda seu repositório GitHub.
   * `<site-name>` refere-se ao nome do site criado.

   Por exemplo, se o nome da ramificação for `main`, o repositório for `edsforms`, o proprietário for `wkndforms` e o `site-name` for `eds-forms`, o site estará funcionando a `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   >[!NOTE]
   >
   > * Para exibir a página `index.html` do Projeto do AEM, use a URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * Para exibir páginas diferentes da `index page` do Projeto AEM, use a URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

Agora, você pode começar a [criar e adicionar formulários ao seu Projeto do AEM](#add-edge-delivery-services-forms-to-aem-project).

## Adicionar bloco adaptável do Forms ao seu projeto existente do AEM

Se você tiver um projeto do AEM existente, é possível integrar o Bloco de Forms adaptável ao seu projeto atual para começar a criar formulários.

>[!NOTE]
>
>
> Esta etapa se aplica aos projetos compilados com o [AEM Boilerplate XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk). Se você criou seu projeto do AEM usando o [Modelo do AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms), ignore esta etapa.

Para integrar:

1. Navegue até a pasta do repositório do Projeto AEM no sistema local.

1. Copie e cole as seguintes pastas e arquivos do [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms) no seu projeto do AEM:

   * Pasta [bloco de formulários](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form)
   * [arquivo form-editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js)
   * Arquivo [form-editor-support.css](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css)
1. Navegue até o arquivo `/scripts/editor-support.js` no seu projeto do AEM e atualize-o com o arquivo [editor-support.js no Modelo do AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)
1. Navegue até `/models/_section.json` no seu projeto do AEM e anexe &quot;formulário&quot; e &quot;formulário-incorporado-adaptável-formulário&quot; à matriz de componentes do objeto `filters`:

   ```
       "filters": [
       {
     "id": "section",
     "components": [
       .
       .
       .
       "form",
       "embed-adaptive-form"
     ]
    }]
   ```

1. (Opcional) Navegue até `/.eslintignore` no seu projeto do AEM e adicione abaixo das linhas de código:

   ```
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

1. (Opcional) Navegue até `/.eslintrc.js` no seu projeto do AEM e adicione abaixo das linhas de código no objeto `rules`:

   ```
   'xwalk/max-cells': ['error', {
     '*': 4, // default limit for all models
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
     tnc: 12,
   }],
   'xwalk/no-orphan-collapsible-fields': 'off', // Disable until enhancement is done for Forms properties
   ```

1. Abra o terminal e execute os comandos abaixo:

   ```
   npm i
   npm run build:json
   ```

   >[!NOTE]
   >
   > Antes de enviar as alterações para o repositório do Projeto AEM no GitHub, verifique se os arquivos `component-definition.json`, `component-models.json` e `component-filters.json` localizados no nível raiz do projeto AEM estão atualizados com os objetos relacionados ao formulário.

1. Confirme e envie essas alterações para o repositório de projetos do AEM no GitHub.

   <!--
    1. **Update ESLint configuration file**
    2. Navigate to the `../.eslintignore` file in your AEM Project and add the following line of codes to prevent errors related to the Form Block rule engine:
        
            blocks/form/rules/formula/*
            blocks/form/rules/model/*
       * [form-common](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-common)  folder
       * [form-components](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-components) folder
    
     3. **Update component definitions and models files**
       1. Navigate to the `../models/_component-definition.json` file in your AEM Project and update it with the changes from the [_component-definition.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-definition.json#L39-L48).
    
    3. Navigate to the `../models/_component-models.json` file in your AEM Project and update it with the changes from the [_component-models.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-models.json#L24-L26) -->

Pronto! O bloco adaptável do Forms agora faz parte do projeto do AEM. Você pode [começar a criar e adicionar formulários ao seu projeto do AEM](#add-edge-delivery-services-forms-to-aem-site-project).

## Criar Forms usando o WYSIWYG

É possível abrir o projeto do AEM no Editor universal para criação no WYSIWYG, onde você pode editar o projeto e adicionar a seção Formulário adaptável para incluir formulários do Edge Delivery Services nas páginas do projeto do AEM.

1. Adicione a seção Formulário adaptável à página Projeto do AEM. Para adicionar:
   1. Navegue até o projeto do AEM no console Sites, selecione a página do site que deseja editar e clique em **Editar**. A página do projeto AEM é aberta no Editor universal para edição.
Nesse caso, a página `index.html` é usada para ilustração.
   1. Abra a árvore Conteúdo e navegue até uma seção onde deseja adicionar a seção Formulário adaptável.
   1. Clique no ícone **[!UICONTROL Adicionar]** e selecione o componente **[!UICONTROL Formulário adaptável]** na lista de componentes.

   ![árvore de conteúdo](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   A seção Formulário adaptável é adicionada. Agora é possível começar a adicionar componentes de formulário à página Projeto do AEM.

1. Adicionar componentes de formulário à seção Formulário adaptável adicionada. Para adicionar componentes de formulário:
   1. Navegue até a seção Formulário adaptável adicionada na árvore Conteúdo.

      ![bloco de formulários adaptáveis adicionado](/help/edge/docs/forms/assets/adative-form-block.png)


   1. Clique no ícone **[!UICONTROL Adicionar]** e adicione os componentes desejados da lista **Componentes de Formulários Adaptáveis**.

      ![adicionar componente](/help/edge/docs/forms/assets/add-component.png)

      Você também pode arrastar e soltar os componentes necessários do Adaptive Forms, já que o Editor universal oferece um recurso intuitivo de arrastar e soltar.

   1. Selecione o componente de Formulário adaptável adicionado para atualizar suas propriedades usando **[!UICONTROL Propriedades]**.

      ![abrir propriedades](/help/edge/docs/forms/assets/component-properties.png)

   1. Visualize o formulário.
A captura de tela abaixo exibe o formulário criado no projeto do AEM usando a criação do WYSIWYG:

      ![formulário adicionado](/help/edge/docs/forms/assets/added-form-aem-sites.png)

      Depois de satisfeito com a pré-visualização, o usuário pode prosseguir para publicar a página.

      >[!NOTE]
      >
      > É importante publicar a página do Projeto do AEM novamente depois de fazer as alterações; caso contrário, as atualizações não estarão visíveis no navegador.

1. Publique novamente a página do Projeto do AEM.

   1. Clique em **Publicar** para publicar a página do Projeto do AEM novamente depois de adicionar o formulário.

      ![formulário de publicação](/help/edge/docs/forms/assets/publish-form.png)

   1. A caixa de diálogo de confirmação **Publicar** aparece na tela. Clique em **Publicar** para iniciar a publicação.

      ![publicar formulário1](/help/edge/docs/forms/assets/publish-form1.png)

      Depois de clicar no botão **Publicar**, a mensagem `Publish started successfully` será exibida.

      ![publicar formulário2](/help/edge/docs/forms/assets/publish-form2.png)

   Agora você pode exibir a página Projeto do AEM com o formulário do Edge Delivery Services adicionado no seguinte URL:
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   Por exemplo, se o nome da ramificação for `main`, o repositório for `edsforms`, o proprietário for `wkndforms` e o nome do site for `eds-forms`, a URL será:
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![página de índice](/help/edge/docs/forms/assets/publish-index-page.png)

Você pode estilizar o Forms do Edge Delivery Services editando os arquivos `.css` e `.js` no Bloco de Forms Adaptável e [configurando um ambiente de desenvolvimento do AEM local](#set-up-local-aem-development-environment) para exibir as alterações instantaneamente em seu navegador.

>[!NOTE]
>
> Você também pode [criar um formulário independente no Universal Editor e publicá-lo no Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md).

## Configurar ambiente de desenvolvimento do AEM local

Você pode configurar um ambiente de desenvolvimento do AEM local para desenvolver estilos e componentes personalizados localmente. Para começar a usar um ambiente de desenvolvimento do AEM local:

1. **Instalar a CLI do AEM**: a CLI do AEM simplifica as tarefas de desenvolvimento. Vamos instalá-lo globalmente usando npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **Clonar seu projeto do GitHub**: clone seu repositório de projetos do AEM do GitHub usando o seguinte comando, substituindo &lt;owner> com o proprietário do repositório e &lt;repo> com o nome do repositório:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. **Iniciar o Ambiente Local**: Navegue até o diretório do projeto e inicie a instância do AEM local com um único comando:

   ```
   cd <repo>
   aem up
   ```

Você pode fazer alterações locais na pasta Bloco de Forms Adaptável `blocks/form` para estilizar e codificar seus formulários! Edite os arquivos `.css` ou `.js` nesse diretório e você poderá ver que as alterações foram refletidas instantaneamente em seu navegador.

Depois de concluir as alterações, use os comandos do Git para confirmá-las e enviá-las por push. Isso atualiza seus ambientes de visualização e produção, acessíveis nos seguintes URLs (substitua espaços reservados pelos detalhes do projeto):

Visualização: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`

Produção: `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## Solução de problemas de build do GitHub

Verifique se o processo de criação do GitHub está descomplicado, solucionando possíveis problemas:

* **Manipular Erros de Linting:**
Caso encontre erros de impressão, você pode ignorá-los. Abra o arquivo [Projeto EDS]/package.json e modifique o script &quot;lint&quot; de `"lint": "npm run lint:js && npm run lint:css"` para `"lint": "echo 'skipping linting for now'"`. Salve o arquivo e confirme as alterações no projeto GitHub.

* **Resolver Erro de Caminho do Módulo:**
Se você encontrar o erro &quot;Não é possível resolver o caminho para o módulo &quot;&#39;/scripts/lib-franklin.js&#39;&quot;, navegue até o arquivo [EDS Project]/blocks/forms/form.js. Atualize a instrução de importação substituindo o arquivo lib-franklin.js pelo arquivo aem.js.

## Consulte também:

{{universal-editor-see-also}}
