---
title: Introdução ao Edge Delivery Services para AEM Forms no Universal Editor - Tutorial do desenvolvedor
description: Este tutorial ajuda você a começar a usar um novo projeto do Adobe Experience Manager Forms (AEM). Dentro de dez a vinte minutos, você terá criado seu próprio Edge Delivery Services Forms no Universal Editor.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: c27b8e413c060de601a72a669d86c4add2a4167d
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---


# Introdução ao Edge Delivery Services para AEM Forms usando o Universal Editor (WYSIWYG)

Na era digital de hoje, formulários amigáveis são essenciais para todas as organizações. Os Edge Delivery Services Forms são criados usando o Editor universal, que oferece recursos do WYSIWYG (what-you-see-is-what-you-get, o que você vê é o que você obtém). Ele fornece uma interface moderna e intuitiva para a criação eficiente de formulários.

O AEM Forms fornece um bloco, conhecido como Bloco adaptável do Forms, para ajudar você a criar facilmente o Edge Delivery Services Forms para capturar e armazenar dados. Você pode [criar um novo projeto AEM pré-configurado com o Bloco Forms Adaptável](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) ou [adicionar o Bloco Forms AEM Adaptável a um projeto existente](#add-adaptive-forms-block-to-your-existing-aem-project).

Este tutorial o orienta por meio da criação, visualização e publicação de seu próprio formulário com um projeto do Adobe Experience Manager Site novo ou existente usando a criação do WYSIWYG no Universal Editor.


## Pré-requisitos

* Você tem uma conta GitHub e compreende as noções básicas sobre Git.
* Você tem uma conta do Google ou do Microsoft SharePoint.
* Você entende as noções básicas do HTML, CSS e JavaScript.
* Você tem o Node/npm instalado para desenvolvimento local.

## Criar um novo projeto AEM pré-configurado com o Bloco Forms adaptável

O modelo AEM Forms Boilerplate permite iniciar rapidamente com um projeto AEM pré-configurado com o Bloco de Forms adaptável. É a maneira mais rápida e fácil de seguir as práticas recomendadas do AEM e começar a criar seus formulários.

### Introdução ao modelo de repositório padronizado do AEM Forms

1. Crie um repositório GitHub para seu projeto AEM. Para criar um repositório:
   1. Ir para [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![Modelo do AEM Forms](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. Clique na opção **Usar este modelo** e selecione a opção **Criar um novo repositório**.

      ![Criar novo repositório usando o Modelo do AEM Forms](/help/edge/docs/forms/assets/use-eds-form-template.png)

      A tela **Criar um novo repositório** é aberta.

   1. Na tela **Criar um novo repositório**, selecione o **proprietário** e especifique o **Nome do repositório**. A Adobe recomenda definir o repositório como **Público**. Então, selecione a opção **pública** e clique em **Criar Repositório**.

      ![Definir o repositório como público](/help/edge/docs/forms/assets/name-eds-repo.png)

1. Instale o aplicativo GitHub de sincronização de código AEM em seu repositório. Para instalar:
   1. Ir para [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. Na tela **Instalar Sincronização de Código AEM**, selecione a opção **Somente selecionar Repositórios** e selecione o repositório recém-criado. Clique em **Salvar**.

   ![Definir o repositório como público](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. Agora vincule o repositório GitHub criado por meio do AEM Forms Boilerplate ao ambiente de criação do Projeto AEM. Para conectar:

   1. Vá para o repositório GitHub criado anteriormente usando a Matriz do AEM Forms.
   1. Abra o arquivo **fstab.yaml** para edição.

      ![abrir arquivo fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)

   1. Edite o arquivo **fstab.yaml** para atualizar o ponto de montagem do seu projeto. Substitua o URL pelo URL da sua instância de criação do AEM as a Cloud Service.
      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![editar arquivo fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. Confirme o arquivo **fstab.yaml** atualizado, depois de atualizar a referência e tudo ficará bem.

      ![confirmar as alterações](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      Se você encontrar problemas de compilação, consulte [Solução de problemas de compilação do GitHub](#troubleshooting-github-build-issues).

### Criar um novo projeto AEM

Agora que você tem um projeto GitHub, pode prosseguir para criar e publicar um novo projeto AEM na instância de criação do AEM as a Cloud Service.
1. Para criar um novo projeto AEM:

   1. Faça logon na instância de criação do AEM as a Cloud Service e selecione **Sites**.

      ![selecionar sites](/help/edge/assets/select-sites.png)

   1. Clique em **Criar** > **Site do modelo**.

      ![criar-sites](/help/edge/docs/forms/assets/create-sites.png)

   1. Selecione o modelo de Site do Edge Delivery Services e clique em **Avançar**.

      ![selecionar-modelo-site](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * Se o modelo de site do Edge Delivery Services não estiver disponível na instância de criação, clique no botão Importar para fazer upload do modelo.
      > * Você pode baixar os modelos de site do Edge Delivery Services em [GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases).

   1. Insira os seguintes detalhes para criar um novo projeto AEM:
      * **Título do site** - Adicione um título descritivo para o site.
      * **Título do site** - Use o `site-name` que você definiu na etapa anterior.
      * **URL do GitHub** - Use a URL do projeto GitHub criado na etapa anterior.

      ![criar site de AEM](/help/edge/docs/forms/assets/create-aem-site.png)

   1. A caixa de diálogo **Criar Site** é exibida. Clique em **OK**.

      ![clique em OK](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      Em apenas alguns minutos, seu novo projeto AEM será criado.

   1. Navegue até o projeto AEM recém-criado no console Sites e clique em **Editar**.
Nesse caso, a página `index.html` é usada para ilustração.

      ![editar Site AEM](/help/edge/docs/forms/assets/edit-site.png)

      O projeto AEM é aberto no Editor universal em uma nova guia, permitindo a criação no WYSIWYG. Agora você pode editar seu projeto AEM.

      ![Aberturas de site no Editor Universal](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. Publish seu projeto AEM criado

   Quando terminar de editar o projeto AEM, publique-o. Para publicar:

   1. No console Sites, selecione todas as páginas do Projeto AEM e clique em **Quick Publish**.

      ![publicar Projeto do AEM Sites](/help/edge/docs/forms/assets/publish-sites.png)

   1. A caixa de diálogo de confirmação **Publish Rápido** é exibida. Clique em **Publish** para iniciar o processo de publicação.

      ![Caixa de diálogo de confirmação do Quick Publish](/help/edge/docs/forms/assets/quick-publish.png)

      Como alternativa, você pode publicar as páginas do projeto AEM diretamente na interface do usuário do Universal Editor.

      ![Caixa de diálogo de confirmação do Quick Publish](/help/edge/docs/forms/assets/qui.png)

   Parabéns! Você tem um novo site em execução em `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   * `<branch>` refere-se à ramificação do seu repositório GitHub.
   * `<repository>` indica seu repositório GitHub.
   * `<owner>` refere-se ao nome de usuário da sua conta GitHub que hospeda seu repositório GitHub.
   * `<site-name>` refere-se ao nome do site criado.

   Por exemplo, se o nome da ramificação for `main`, o repositório for `edsforms`, o proprietário for `wkndforms` e o `site-name` for `eds-forms`, o site estará funcionando a `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   >[!NOTE]
   >
   > * Para exibir a página `index.html` do Projeto AEM, use a URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * Para exibir páginas diferentes da `index page` do Projeto AEM, use a URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

Agora, você pode começar a [criar e adicionar formulários ao seu Projeto AEM](#add-edge-delivery-services-forms-to-aem-project).

## Adicionar bloco adaptável do Forms ao seu projeto AEM existente

Se você tiver um projeto AEM existente, é possível integrar o Bloco de Forms adaptável ao seu projeto atual para começar a criar formulários.

>[!NOTE]
>
>
> Esta etapa se aplica aos projetos compilados com a [Estrutura AEM](https://github.com/adobe-rnd/aem-boilerplate-xwalk). Se você criou seu projeto AEM usando o [Modelo do AEM Forms](https://github.com/adobe-rnd/aem-boilerplate-forms), ignore esta etapa.

Para Integrar O:

1. Clonar o repositório GitHub de Bloqueio Adaptável do Forms: [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) no computador.
1. Dentro da pasta baixada, localize a pasta `blocks/form` e copie esta pasta.
1. Clonar o repositório GitHub do projeto AEM no computador.
1. Agora, navegue até a pasta `blocks` no repositório local do Projeto AEM e cole a pasta do formulário copiado lá.
1. Confirme e envie essas alterações para o repositório do projeto AEM no GitHub.

Pronto! O bloco adaptável do Forms agora faz parte do projeto AEM. Você pode [começar a criar e adicionar formulários ao seu projeto AEM](#add-edge-delivery-services-forms-to-aem-site-project).

## Criar AEM Forms usando o WYSIWYG

Você pode abrir o projeto AEM no Editor universal para criação no WYSIWYG, onde é possível editar o projeto e adicionar a seção Formulário adaptável para incluir Edge Delivery Services AEM formulários nas páginas do projeto.

1. Adicione a seção Formulário adaptável à página Projeto AEM. Para adicionar:
   1. Navegue até o Projeto AEM no console Sites e clique em **Editar**. A página Projeto AEM é aberta no Editor universal para edição.
Nesse caso, a página `index.html` é usada para ilustração.
   1. Abra a árvore Conteúdo e navegue até o local em que deseja adicionar a seção Formulário adaptável.
   1. Clique no ícone **[!UICONTROL Adicionar]** e selecione o componente **[!UICONTROL Formulário adaptável]** na lista de componentes.

   ![árvore de conteúdo](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   A seção Formulário adaptável é adicionada no local especificado. Agora você pode começar a adicionar componentes de formulário à página Projeto AEM.

1. Adicionar componentes de formulário à seção Formulário adaptável adicionada. Para adicionar componentes de formulário:
   1. Navegue até a seção Formulário adaptável adicionada na árvore Conteúdo.

      ![bloco de formulários adaptáveis adicionado](/help/edge/docs/forms/assets/adative-form-block.png)


   1. Clique no ícone **[!UICONTROL Adicionar]** e adicione os componentes desejados da lista **Componentes de Formulários Adaptáveis**.

      ![adicionar componente](/help/edge/docs/forms/assets/add-component.png)

      Você também pode arrastar e soltar os componentes necessários do Adaptive Forms, já que o Editor universal oferece um recurso intuitivo de arrastar e soltar.

   1. Selecione o componente de Formulário adaptável adicionado para atualizar suas propriedades usando **[!UICONTROL Propriedades]**.

      ![abrir propriedades](/help/edge/docs/forms/assets/component-properties.png)

      A captura de tela abaixo exibe o formulário criado no projeto AEM usando a criação do WYSIWYG:

      ![formulário adicionado](/help/edge/docs/forms/assets/added-form-aem-sites.png)

   >[!NOTE]
   >
   > É importante publicar a página do Projeto AEM novamente depois de fazer as alterações; caso contrário, as atualizações não estarão visíveis no navegador.

1. Publique novamente a página do Projeto AEM.

   1. Clique em **Publish** para publicar a página Projeto AEM novamente depois de adicionar o formulário.

      ![formulário de publicação](/help/edge/docs/forms/assets/publish-form.png)

   1. A caixa de diálogo de confirmação **Publish** aparece na tela. Clique em **Publish** para iniciar a publicação.

      ![publicar formulário1](/help/edge/docs/forms/assets/publish-form1.png)

      Depois de clicar no botão **Publish**, a mensagem `Publish started successfully` será exibida.

      ![publicar formulário2](/help/edge/docs/forms/assets/publish-form2.png)

   Agora você pode visualizar a página do Projeto AEM com o Formulário Edge Delivery Services adicionado no seguinte URL:
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   Por exemplo, se o nome da ramificação for `main`, o repositório for `edsforms`, o proprietário for `wkndforms` e o nome do site for `eds-forms`, a URL será:
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![página de índice](/help/edge/docs/forms/assets/publish-index-page.png)

Você pode estilizar o Forms do Edge Delivery Services editando os arquivos `.css` e `.js` no Bloco de Forms AEM Adaptável e [configurando um ambiente de desenvolvimento local do](#set-up-local-aem-development-environment) para exibir as alterações instantaneamente em seu navegador.

## Configurar um ambiente de desenvolvimento do AEM local

Você pode configurar um ambiente de desenvolvimento local do AEM para desenvolver localmente estilos e componentes personalizados. Para começar a usar um ambiente de desenvolvimento local de AEM:

1. **Instalar a CLI do AEM**: a CLI do AEM simplifica as tarefas de desenvolvimento. Vamos instalá-lo globalmente usando npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **Clonar seu projeto do GitHub**: clone seu repositório de projetos do AEM do GitHub usando o seguinte comando, substituindo <owner> com o proprietário do repositório e <repo> com o nome do repositório:

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

<!-- * **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file. -->
