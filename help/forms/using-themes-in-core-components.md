---
title: Como criar e usar temas no Adaptive Forms?
description: Você pode usar temas para estilizar e fornecer uma identidade visual a um formulário adaptável usando os Componentes principais. Você pode compartilhar um tema em qualquer número do Adaptive Forms.
keywords: temas do construtor de formulários, formulários adaptáveis com estilo dos componentes principais, construtor de temas de formulário, estilo do formulário adaptável, personalização de temas, criação de temas de formulário
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: c0e0a700e85563ff65c703d5d20e6d6c1ff0651c
workflow-type: tm+mt
source-wordcount: '2897'
ht-degree: 3%

---

# Usar temas para estilizar os Componentes principais com base no Forms adaptável{#themes-for-af-using-core-components}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

É possível criar e aplicar temas para estilizar um Formulário adaptável. Um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Ao aplicar um tema, o estilo especificado é refletido nos componentes correspondentes. Um tema é gerenciado de forma independente sem uma referência a um Formulário adaptável e pode ser reutilizado em vários Forms adaptáveis.

Neste artigo, entendemos como projetar buscas personalizadas para Forms adaptável com base em Componentes principais usando temas.

## Temas disponíveis para estilizar os Componentes principais

O Forms, conforme fornecido pelo Cloud Service, lista abaixo os temas dos Componentes principais com base no Adaptive Forms:

* [Tema Tela de desenho](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema do CAVALETE](https://github.com/adobe/aem-forms-theme-easel)

## Compreender a estrutura dos temas

Um tema é um pacote que inclui componentes de estilo, como arquivo CSS, arquivos JavaScript e recursos (como ícones) que definem o estilo do seu Forms adaptável. Um tema do Formulário adaptável segue uma organização específica, consistindo nos seguintes componentes:

* `src/theme.scss`: esta pasta inclui o arquivo CSS que tem um amplo impacto sobre todo o tema. Ele serve como um local centralizado para definir e gerenciar o estilo e o comportamento do tema. Ao fazer edições nesse arquivo, você pode fazer alterações aplicadas universalmente no tema, influenciando a aparência e a funcionalidade das Páginas adaptáveis do Forms e do AEM Sites.

* `src/site`: esta pasta contém arquivos CSS que são aplicados a uma página inteira do Site do AEM. Esses arquivos consistem em códigos e estilos que afetam a funcionalidade geral e o layout da página do seu site do AEM. Quaisquer modificações feitas aqui serão refletidas em todas as páginas do site. [Quando usá-lo?]

* `src/components`: os arquivos CSS nesta pasta são criados para componentes principais individuais do AEM. Cada pasta dedicada de um componente inclui um arquivo `.scss` que estimula esse componente específico em um Formulário adaptável. Por exemplo, o arquivo /src/components/accordion/_accordion.scss contém informações de estilo para o componente Adaptive Forms Accordion.

  ![estrutura de tema baseada em formulário adaptável](/help/forms/assets/theme_structure.png)

* `src/resources`: esta pasta contém arquivos estáticos, como ícones, logotipos e fontes. Esses recursos são usados para aprimorar os elementos visuais e o design geral do tema.

## Criar um tema

O Forms as Cloud Service fornecem, os temas de estilo do Formulário adaptável listados abaixo para Componentes principais baseados no Adaptive Forms.

* [Tema Tela de desenho](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema do CAVALETE](https://github.com/adobe/aem-forms-theme-easel)

Você pode [personalizar qualquer um desses temas para criar um novo tema](#customize-a-theme-core-components).

![Fluxo de trabalho de personalização de tema](/help/forms/assets/workflow-of-customization-of-theme.png)

## Personalizar um tema {#customize-a-theme-core-components}

A personalização de um tema refere-se ao processo de modificação, estilo e personalização da aparência de um tema. Ao personalizar um tema, você altera seus elementos de design, layout, cores, tipografia e, às vezes, o código subjacente. Ele permite criar uma aparência exclusiva e personalizada para seu site ou aplicativo, mantendo a estrutura básica e a funcionalidade fornecidas pelo tema.

### Pré-requisitos {#prerequisites-to-customize}

* Familiarize-se com a [configuração de um pipeline no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=pt-BR#setup-pipeline) e ter conhecimento básico sobre como configurar um pipeline ajuda a gerenciar e implantar com eficiência suas personalizações de tema.
* Saiba como [configurar um usuário com a função de colaborador](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html?lang=pt-BR). Entender como configurar um usuário com a função de colaborador permite que você conceda as permissões necessárias para personalização de temas.
* Instale a última versão do [Apache Maven](https://maven.apache.org/download.cgi). O Apache Maven é uma ferramenta de automação de build comumente usada para projetos Java™. A instalação da versão mais recente garante que você tenha as dependências necessárias para a personalização de temas.
* Instale um editor de texto simples. Por exemplo, Microsoft® Visual Studio Code. O uso de um editor de texto simples, como o Microsoft® Visual Studio Code, fornece um ambiente amigável para a edição e modificação de arquivos de tema.

### Configurar o ambiente

* Instale os componentes principais adaptáveis do Forms mais recentes até o momento para ativar o ambiente do AEM Cloud Service.
* Configure um [pipeline de implantação front-end](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html?lang=pt-BR) para seu ambiente do Cloud Service. Como alternativa, você pode configurar o pipeline posteriormente, fornecendo a flexibilidade para priorizar testes e refinar o tema antes de configurar o pipeline de implantação.

<!-- 
To deploy your themes to a Forms as a Cloud Service environment, first test theme on a local development environment to address any issues. Once the theme is tested, configure the front-end deployment pipeline, which is responsible for deploying the themes.

These themes are deployed to a Forms as a Cloud Service environment via the front-end pipeline. You can configure the pipeline later also, after testing the theme on a local development environment. 

-->

Depois de aprender os pré-requisitos e configurar o ambiente de desenvolvimento, você estará bem preparado para começar a personalizar ou estilizar seu tema de acordo com seus requisitos específicos.

### Personalizar um tema {#steps-to-customize-a-theme-core-components}

A personalização de um tema é um processo de várias etapas. Para personalizar o tema, execute as etapas na ordem listada:

1. [Clonar um tema](#download-a-theme-core-components)
1. [Definir nome de um tema](#set-name-of-theme)
1. [Personalizar um tema](#customize-the-theme)
1. [Testar um tema](#test-the-theme)
1. [Implantar um tema](#deploy-the-theme)

Os exemplos fornecidos no documento são baseados no tema **Tela**, mas é importante observar que você pode clonar qualquer tema e personalizá-lo usando as mesmas instruções. Essas instruções se aplicam a qualquer tema, permitindo modificar temas de acordo com suas necessidades específicas.

Vamos começar com um processo para criar uma experiência com marca para seu Forms adaptável baseado em componentes principais usando temas?

#### &#x200B;1. Clonar um tema {#download-a-theme-core-components}

Para clonar um tema para os Componentes principais com base no Adaptive Forms, escolha um dos seguintes temas:

* [Tema Tela de desenho](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema do CAVALETE](https://github.com/adobe/aem-forms-theme-easel)

Para clonar um tema, execute as seguintes instruções:

1. Abra o prompt de comando ou a janela do terminal no ambiente de desenvolvimento local.

1. Execute o comando `git clone` para clonar um tema.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   Substituir o [Caminho do Repositório Git do tema] pela URL real do Repositório Git correspondente do tema

   Por exemplo, para clonar o tema da Tela de Pintura, execute o seguinte comando:

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

   Depois de executar o comando com êxito, você terá uma cópia local do tema disponível em sua máquina na pasta `aem-forms-theme-canvas`.


#### &#x200B;2. Definir nome de um tema {#set-name-of-theme}

1. Abra a pasta de temas no IDE. Por exemplo, para abrir a pasta `aem-forms-theme-canvas` no editor de código do Visual Studio.

1. Navegue até a pasta `aem-forms-theme-canvas`.

1. Execute o seguinte comando:

   ```
      code .
   ```

   ![Abrir a pasta de temas em um editor de texto simples](/help/forms/assets/aem-forms-theme-folder-in-vs-code.png)

   A pasta é aberta no Visual Studio Code.

1. Abra o arquivo `package.json` para edição.

1. Defina os valores para os atributos `name` e `version`.

   ![Imagem de alteração do nome do Tema da Tela](/help/forms/assets/changename_canvastheme.png)

   >[!NOTE]
   >
   > * O atributo de nome é usado para identificar exclusivamente o tema, e o nome especificado é exibido na guia **Estilo** do **Assistente de Criação de Formulário**.
   > * Você tem a opção de selecionar um nome para o tema de acordo com sua escolha, por exemplo, `mytheme` ou `customtheme`. No entanto, neste caso, especificamos o nome como `aem-forms-wknd-theme`.

1. Abra o arquivo `package-lock.json` para edição.
1. Defina os valores para os atributos `name` e `version`. Verifique se os valores dos atributos `name` e `version` no arquivo `Package-lock`.json correspondem àqueles no arquivo `Package.json`.

   ![Imagem de alteração do nome do Tema da Tela](/help/forms/assets/changename_canvastheme-package-lock.png)

1. (Opcional) Abra o arquivo `ReadMe` para editar e atualizar o nome do tema.

   ![Imagem de alteração do nome do Tema da Tela](/help/forms/assets/changename_canvastheme-readme-file.png)

1. Salve e feche os arquivos.

**Considerações ao definir o nome do tema**

* É obrigatório remover o `@aemforms` do nome do tema no arquivo `Package.json` e no arquivo `Package-lock.json`. Caso você não consiga remover `@aemforms` do nome de tema personalizado, isso resultará na falha do pipeline de front-end durante a implantação do tema.
* É recomendável atualizar o tema `version` no arquivo `Package.json` e no arquivo `Package-lock.json` para refletir com precisão as alterações e aprimoramentos ao longo do tempo para o seu tema.
* Para obter informações importantes sobre o uso, instruções de instalação e outros detalhes relevantes, é recomendável atualizar o nome do tema no arquivo `ReadMe`.

#### &#x200B;3. Personalizar um tema {#customize-the-theme}

Você pode personalizar componentes individuais ou fazer alterações no nível do tema usando variáveis globais de um tema. Quaisquer alterações feitas nas variáveis globais afetam todos os componentes individuais. Por exemplo, você pode usar variáveis Globais para alterar a cor da borda de todos os componentes de um Formulário adaptável e uma cor de preenchimento brilhante para definir o CTA (Call to action) usando o componente de botão:

* [Definir estilos de nível de tema](#theme-customization-global-level)

* [Definir estilos de nível de componente](#component-based-customization)

##### Definir estilos de nível de tema{#theme-customization-global-level}

O arquivo `variable.scss` contém as variáveis globais do tema. Ao atualizar essas variáveis, é possível fazer alterações relacionadas ao estilo no nível do tema. Para aplicar estilos de nível de tema, siga estas etapas:

1. Abra o arquivo `<your-theme-sources>/src/site/_variables.scss` para edição.
1. Altere o valor de qualquer propriedade. Por exemplo, a cor de erro padrão é `red`. Para alterar a cor do erro de `red` para `blue`, altere o código hexadecimal da cor de `$errorvariable`. Por exemplo, `$error: #196ee5`.
1. Salvar e fechar o arquivo.

   ![Editar tema](/help/forms/assets/edit_theme.png)

Da mesma forma, você pode usar o arquivo `variable.scss` para definir a família e o tipo de fonte, as cores do tema e da fonte, o tamanho da fonte, o espaçamento do tema, o ícone de erro, os estilos de borda do tema e mais variáveis que afetam vários componentes do Formulário adaptável.

##### Definir estilos de nível de componente {#component-based-customization}

Você também pode alterar a fonte, a cor, o tamanho e outras propriedades CSS de um componente principal do Formulário adaptável específico. Por exemplo, botão, caixa de seleção, container, rodapé e muito mais. Você pode estilizar um botão ou caixa de seleção editando o arquivo CSS do componente específico para alinhá-lo ao estilo de sua organização. Para personalizar o estilo de um componente:

1. Abra o arquivo `<your-theme-sources>/src/components/<component>/<component.scss>` para edição. Por exemplo, para alterar a cor da fonte do componente de botão, abra o arquivo `<your-theme-sources>/src/components/button/button.scss`.
1. Altere o valor de qualquer de acordo com suas necessidades. Por exemplo, para alterar a cor do componente de botão ao passar o mouse para `green`, altere o valor da propriedade `color: $white` na classe `cmp-adaptiveform-button__widget:hover` para o código hexadecimal `#12B453` ou qualquer outra sombra de `green`. O código final é semelhante ao seguinte:

   ```
   .cmp-adaptiveform-button__widget:hover {
   background: $dark-gray;
   color: #12B453;
   }
   ```

1. Salvar e fechar o arquivo.

   ![Editar CSS da Caixa de Texto](/help/forms/assets/edit_color_textbox.png)

   >[!NOTE]
   >
   > Quando um estilo é definido no nível do tema e do componente, o estilo definido no nível do componente tem prioridade.

#### &#x200B;4. Testar um tema personalizado {#test-the-theme}

Para visualizar e testar as alterações no ambiente local e personalizar o tema de acordo com os requisitos para diferentes componentes do AEM, execute as seguintes etapas:

* 4.1 [Configurar um ambiente local para teste](#rename-env-file-theme-folder)
* 4.2 [Testar o tema usando o ambiente local](#start-a-local-proxy-server)

##### 4.1. Configurar um ambiente local para testes {#rename-env-file-theme-folder}

1. Abra a pasta de temas no IDE. Por exemplo, abra a pasta `aem-forms-theme-canvas` no editor de código do Visual Studio.
1. Renomeie o arquivo `env_template` para o arquivo `.env` na pasta de temas e adicione os seguintes parâmetros:

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   Por exemplo, a URL do formulário é `http://localhost:4502/editor.html/content/forms/af/contactusform.html`. Portanto, os valores de:

   * AEM_URL = `http://localhost:4502/`
   * AEM_ADAPTIVE_FORM = `contactusform`

1. Salve o arquivo.

   ![Estrutura de Tema da Tela](/help/forms/assets/env-file-canvas-theme.png)

##### 4.2 Testar o tema usando um ambiente local {#start-a-local-proxy-server}

1. Navegue até a raiz da pasta de temas. Nesse caso, o nome da pasta de temas é `aem-forms-theme-canvas`.
1. Abra o prompt de comando ou o terminal.
1. Execute `npm install` para instalar as dependências.
1. Execute `npm run live` para visualizar o formulário com o tema atualizado em seu navegador local.

   >[!NOTE]
   >
   > Se ocorrer um erro durante a execução do comando `npm run live`, execute os seguintes comandos antes do comando `npm run live`:
   >
   > * `npm install parcel --save-dev`
   > * `npm i @parcel/transformer-sass`

Esta é uma implantação ativa. Assim, sempre que você fizer alterações e salvar os arquivos `_variables.scss` e `button.scss`, o servidor selecionará automaticamente as alterações e visualizará a saída mais recente. A linha `[Browsersync] File event [change]` significa que o servidor reconheceu as alterações mais recentes e está implantando as alterações no ambiente local.

![Browsersync de proxy](/help/forms/assets/browser_sync.png)

Após seguir os exemplos de estilo de um Formulário adaptável (componentes principais) no nível do tema e no nível do componente para personalizações de tema, as mensagens de erro de um Formulário adaptável são alteradas para a cor `blue`, enquanto a cor do rótulo do componente de botão é alterada para `green` ao passar o mouse.

**Visualizando estilo de nível de tema**

![Exemplo: Cor do erro definida para azul](/help/forms/assets/theme-level-changes.png)

**Visualizando estilo de nível de componente**

![Exemplo: a cor de foco está definida como verde](/help/forms/assets/button-customization.png)

A personalização de um tema ajuda a projetar as pesquisas personalizadas para o Forms adaptável baseado em Componentes principais de acordo com os requisitos organizacionais.

###### Testar o tema para formulários hospedados em um ambiente do Cloud Service

Você também pode testar o tema do Formulário adaptável hospedado em sua instância do AEM Forms as a Cloud Service. Para configurar e definir o ambiente local para o teste dos temas com o Forms adaptável hospedado na instância da nuvem, execute as seguintes etapas:

1. Abra a pasta de temas no IDE. Por exemplo, abra a pasta `aem-forms-theme-canvas` no editor de código do Visual Studio.
1. Renomeie o arquivo `env_template` para o arquivo `.env` e adicione os seguintes parâmetros:

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   Por exemplo, a URL do formulário no ambiente de nuvem é `https://author-XXXX.adobeaemcloud.com/editor.html/content/forms/af/contactusform.html`. Portanto, os valores de:

   * AEM_URL = `https://author-XXXX-cmstg.adobeaemcloud.com/`
   * AEM_ADAPTIVE_FORM = `contactusform`
1. Salve o arquivo.
1. Crie um usuário local.

   >[!NOTE]
   >
   > Para criar um usuário local:
   >
   > * Vá para **[!UICONTROL AEM Home]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
   > * Certifique-se de que o usuário é membro do grupo `forms-users`.

1. Navegue até a raiz da pasta de temas. Nesse caso, o nome da pasta de temas é `aem-forms-theme-canvas`.
1. Execute `npm run live` e você será redirecionado a um navegador local.
1. Clique em `SIGN IN LOCALLY (ADMIN TASKS ONLY)` e faça logon usando as credenciais do usuário local.

Você pode visualizar o Formulário adaptável com as alterações mais recentes. Quando estiver satisfeito com as modificações feitas em uma pasta de tema, implante o tema no ambiente do AEM Cloud Service usando o pipeline de front-end.

#### &#x200B;5. Implantar um tema {#deploy-the-theme}

Para implantar o tema no ambiente do Cloud Service usando o pipeline de front-end:

* 5.1 [Criar um repositório para o tema](#create-a-new-theme-repo)
* 5.2 [Enviar as alterações para o repositório](#committing-the-changes)
* 5.3 [Executar o pipeline de front-end](#run-a-frontend-pipeline)

##### 5.1 Criar um repositório para o tema{#create-a-new-theme-repo}

Você precisa de um repositório para implantar o tema. Faça logon no [repositório do AEM Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=pt-BR#accessing-git) e adicione um novo repositório para o tema.

1. Crie um novo repositório para um tema clicando em **[!UICONTROL Repositórios]** > **[!UICONTROL Adicionar repositório]**.

   ![criar novo repositório de temas](/help/forms/assets/createrepo_canvastheme.png)


1. Especifique o **Nome do Repositório** na caixa de diálogo **Adicionar Repositório**. Por exemplo, o nome fornecido é `custom-canvas-theme-repo`.
1. Clique em **[!UICONTROL Salvar]**.

   ![Adicionar tema da tela Repo](/help/forms/assets/addcanvasthemerepo.png)

1. Clique em **[!UICONTROL Copiar URL do Repositório]** para copiar a URL do repositório.

   ![URL do tema da tela](/help/forms/assets/copyurl_canvastheme.png)

   >[!NOTE]
   > 
   >* Você pode usar um único repositório para vários temas.
   >* Para implantar temas diferentes, é necessário criar pipelines de front-end separados.
   >* Por exemplo, você pode usar o mesmo repositório, como `custom-canvas-theme-repo`, para o tema da Tela, o tema da WKND e o tema do EASEL. No entanto, para implantar os temas, é necessário criar pipelines de front-end separados. Personalizações futuras para um tema específico são implantadas usando o pipeline de front-end correspondente.

##### 5.2. Enviar as alterações para o repositório {#committing-the-changes}

Agora, envie as alterações para o repositório de temas do AEM Forms Cloud Service.

1. Navegue até a raiz da pasta de temas.  Nesse caso, o nome da pasta de temas é `aem-forms-theme-canvas`.
1. Abra o prompt de comando ou o terminal.
1. Execute o seguinte comando na ordem listada:

   ```
   git remote add [alias-name-for-repository] [URL of repository]
   git add .
   git commit
   git push [name-for-createdrepository]
   ```

   Por exemplo:

   ```
   git remote add canvascloudthemerepo https://git.cloudmanager.adobe.com/stage-aemformsdev/customcanvastheme/
   git add .
   git commit
   git push canvascloudthemerepo 
   ```

   ![Alterações confirmadas](/help/forms/assets/cmd_git_push.png)



##### 5.3 Executar o pipeline de front-end {#run-a-frontend-pipeline}

O tema é implantado usando o [pipeline de front-end](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html?lang=pt-BR). Para implantar o tema, execute as seguintes etapas:

1. Faça logon no repositório do AEM Cloud Manager.
1. Clique no botão **[!UICONTROL Adicionar]** da seção **[!UICONTROL Pipelines]**.
1. Selecione **[!UICONTROL Adicionar pipeline de não produção]** ou **[!UICONTROL Adicionar pipeline de produção]** com base no ambiente do Cloud Service. Por exemplo, aqui a opção **[!UICONTROL Adicionar pipeline de produção]** está selecionada.
1. Na caixa de diálogo **[!UICONTROL Adicionar pipeline de produção]** como parte das etapas **[!UICONTROL Configuração]**, especifique o nome do pipeline. Por exemplo, o nome do pipeline é `customcanvastheme`.
1. Clique em **[!UICONTROL Continuar]**.
1. Selecione as opções **[!UICONTROL Implantação direcionada]** > **[!UICONTROL Código de front-end]**, em
as etapas **[!UICONTROL Código Source]**.
1. Selecione os valores de **[!UICONTROL Repositório]** e **[!UICONTROL Ramificação Git]** que têm as alterações mais recentes. Por exemplo, aqui o nome do repositório selecionado é `custom-canvas-theme-repo` e a ramificação Git é `main`.
1. Selecione o **[!UICONTROL Local do Código]** como `/`, se suas alterações estiverem presentes na pasta raiz.
1. Clique em **[!UICONTROL Salvar]**.
   ![criar pipeline de front-end](/help/forms/assets/canvas-theme-frontendpipeline.gif)

   Após a conclusão da configuração do pipeline, o cartão call-to-action é atualizado.

   >[!NOTE]
   >
   > Para garantir que seu pipeline de front-end não falhe no Cloud Manager, [defina a versão do Node.js para 20](#set-the-nodejs-vesrion-to-20).

1. Clique com o botão direito do mouse no pipeline criado.
1. Clique em **[!UICONTROL Executar]**.

   ![executar-um-pipeline](/help/forms/assets/canvas-theme-run-pipeline.png)

Quando a criação for concluída, o tema ficará disponível na instância do autor para uso. Ele aparece na guia **[!UICONTROL Style]** do assistente de criação do Formulário adaptável ao criar um Formulário adaptável.

![tema personalizado disponível na guia de estilo](/help/forms/assets/custom-theme-style-tab.png)

O tema personalizado ajuda a criar uma experiência com a marca para o Forms adaptável baseado nos Componentes principais.

## Aplicar um tema a um formulário adaptável {#using-theme-in-adaptive-form}

As etapas para aplicar um tema a um Formulário adaptável são:

1. Faça logon na instância de autor do AEM Forms.

1. Selecione **Adobe Experience Manager** > **Forms** > **Forms e Documentos**.

1. Clique em **Criar** > **Forms Adaptável**. O assistente para criação do Formulário adaptável é aberto.

1. Selecione o modelo do componente principal na guia **Source**.
1. Selecione o tema na guia **Style**.
1. Clique em **Criar**.

Os temas do formulário adaptável são usados como parte de um modelo de formulário adaptável para definir o estilo ao criar um formulário adaptável.

## Defina a versão do Node.js para 20

Para definir a versão do Node.js para 20 usando a configuração de pipeline:

1. Vá para a seção **Pipelines** e localize seu pipeline de front-end.
2. No lado direito do pipeline, clique no menu de três pontos **&#x200B;**&#x200B;e, na lista suspensa, selecione **Exibir/Editar variáveis**.
3. Na caixa de diálogo **Configuração de variáveis**, preencha os campos da seguinte maneira:
   * **NOME** - NODE_VERSION
   * **VALOR** - 20
   * **ETAPA APLICADA** - Build
   * **TIPO** - Variável
4. Clique em **Salvar** para aplicar a configuração.

![configuração de pipeline](/help/forms/assets/pipeline-config.png)

## Práticas recomendadas {#best-practices}

* **Evitando ativos de outro tema**

  Ao editar um tema, você pode procurar e adicionar ativos (como imagens) de outros temas. Por exemplo, você está editando o fundo de uma página. Por exemplo, ao selecionar **[!UICONTROL Página]** ![botão de edição](assets/edit-button.png)> **[!UICONTROL Plano de fundo]** > **[!UICONTROL Adicionar]** > **[!UICONTROL Imagem]**, você verá uma caixa de diálogo que permite navegar e adicionar imagens em outro tema.

  Você pode enfrentar problemas com seu tema atual se um ativo for adicionado de outro tema e o outro tema for movido ou excluído. É recomendável evitar a navegação e adicionar ativos de outros temas.

* **Alterando a largura do layout do painel de contêiner**

  Não é recomendável alterar a largura do layout do painel de contêiner. Quando você especifica a largura de um painel de contêiner, ele se torna estático e não se adapta a exibições diferentes.

## Perguntas frequentes {#faq}

**P:** Qual personalização tem prioridade ao fazer personalizações em uma pasta de tema no nível global e no nível do componente?

**Ans:** Quando as personalizações são feitas no nível global e no nível do componente, a personalização no nível do componente tem prioridade.

<!--

## See next

* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [Generate Document of Record for Adaptive Forms (Core Components](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Create an Adaptive Forms with Repeatable sections](/help/forms/create-forms-repeatable-sections.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=pt-BR)

-->


## Consulte também {#see-also}

{{see-also}}

* [Definir layout de formulários para diferentes tamanhos de tela e tipos de dispositivo](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [Gerar documento de registro para o Forms adaptável (componentes principais)](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Criar um Forms adaptável com seções repetíveis](/help/forms/create-forms-repeatable-sections.md)
* [Modelos de temas de exemplo e modelos de dados de formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=pt-BR)
