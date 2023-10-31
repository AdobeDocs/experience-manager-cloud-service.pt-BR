---
title: Como podemos criar e usar temas no Adaptive Forms?
description: Você pode usar temas para estilizar e fornecer uma identidade visual a um Formulário adaptável usando componentes principais. Você pode compartilhar um tema em qualquer número do Adaptive Forms.
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: 4cebcd58a0d6fd429cde3d739095c131cc76d9e5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Temas no Adaptive Forms {#themes-for-af-using-core-components}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components.html) |
| AEM as a Cloud Service | Este artigo |

É possível criar e aplicar temas para estilizar um Formulário adaptável. Um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Ao aplicar um tema, o estilo especificado é refletido nos componentes correspondentes. Um tema é gerenciado de forma independente sem uma referência a um Formulário adaptável e pode ser reutilizado em vários Forms adaptáveis.

## Temas disponíveis

O Forms as Cloud Service fornece os temas listados abaixo para o Adaptive Forms baseado em Componentes principais:

* [Tema Tela de desenho](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema CAVALETE](https://github.com/adobe/aem-forms-theme-easel)

## Compreender a estrutura dos temas

Um tema é um pacote que abrange o arquivo CSS, arquivos JavaScript e recursos (como ícones) que definem o estilo do Forms adaptável. Um tema do Formulário adaptável segue uma organização específica, consistindo nos seguintes componentes:

* `src/theme.scss`: essa pasta inclui o arquivo CSS que tem um amplo impacto sobre todo o tema. Ele serve como um local centralizado para definir e gerenciar o estilo e o comportamento do tema. Ao fazer edições nesse arquivo, você pode fazer alterações aplicadas universalmente no tema, influenciando a aparência e a funcionalidade das Páginas adaptáveis do Forms e do AEM Sites.

* `src/site`: esta pasta contém arquivos CSS que são aplicados à página inteira de um site AEM. Esses arquivos consistem em códigos e estilos que afetam a funcionalidade geral e o layout da página do seu site AEM. Quaisquer modificações feitas aqui serão refletidas em todas as páginas do site. [Quando usá-lo?]

* `src/components`: os arquivos CSS nesta pasta são projetados para componentes principais individuais do AEM. Cada pasta dedicada de um componente inclui uma `.scss` arquivo que estiliza esse componente específico em um Formulário adaptável. Por exemplo, o arquivo /src/components/accordion/_accordion.scss contém informações de estilo para o componente Adaptive Forms Accordion.

  ![estrutura de tema baseada em formulário adaptável](/help/forms/assets/theme_structure.png)

* `src/resources`: esta pasta contém arquivos estáticos, como ícones, logotipos e fontes. Esses recursos são usados para aprimorar os elementos visuais e o design geral do tema.

## Criar um tema

O Forms as Cloud Service fornece os temas listados abaixo para o Adaptive Forms baseado em Componentes principais.

* [Tema Tela de desenho](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema CAVALETE](https://github.com/adobe/aem-forms-theme-easel)

Você pode [personalizar qualquer um desses temas para criar um novo tema](#customize-a-theme-core-components).

![Fluxo de trabalho de personalização de tema](/help/forms/assets/workflow-of-customization-of-theme.png)

## Personalizar um tema {#customize-a-theme-core-components}

A personalização de um tema refere-se ao processo de modificação e personalização da aparência de um tema. Ao personalizar um tema, você altera seus elementos de design, layout, cores, tipografia e, às vezes, o código subjacente. Ele permite criar uma aparência exclusiva e personalizada para seu site ou aplicativo, mantendo a estrutura básica e a funcionalidade fornecidas pelo tema.

### Pré-requisitos {#prerequisites-to-customize}

* Familiarize-se com [configuração de um pipeline no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline) e ter conhecimento básico sobre como configurar um pipeline ajuda você a gerenciar e implantar com eficiência suas personalizações de tema.
* Saiba como [configurar um usuário com a função de colaborador](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html). Entender como configurar um usuário com a função de colaborador permite que você conceda as permissões necessárias para personalização de temas.
* Instale a versão mais recente do [Apache Maven.](https://maven.apache.org/download.cgi) O Apache Maven é uma ferramenta de automação de build comumente usada para projetos Java™. A instalação da versão mais recente garante que você tenha as dependências necessárias para a personalização de temas.
* Instale um editor de texto simples. Por exemplo, Microsoft® Visual Studio Code. O uso de um editor de texto simples, como o Microsoft® Visual Studio Code, fornece um ambiente amigável para a edição e modificação de arquivos de tema.

### Configurar o ambiente

* [Ativar os Componentes principais adaptáveis do Forms](/help/forms/enable-adaptive-forms-core-components.md)  para seu ambiente de desenvolvimento e Cloud Service local.
* Configurar [pipeline de implantação front-end](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html) para o ambiente de Cloud Service. Como alternativa, você pode configurar o pipeline posteriormente, fornecendo a flexibilidade para priorizar testes e refinar o tema antes de configurar o pipeline de implantação.

<!-- 
To deploy your themes to a Forms as a Cloud Service environment, first test theme on a local development environment to address any issues. Once the theme is tested, configure the front-end deployment pipeline, which is responsible for deploying the themes.

These themes are deployed to a Forms as a Cloud Service environment via the front-end pipeline. You can configure the pipeline later also, after testing the theme on a local development environment. 

-->

Depois de conhecer os pré-requisitos e configurar o ambiente de desenvolvimento, você estará bem preparado para começar a personalizar seu tema de acordo com suas necessidades específicas.

### Personalizar um tema {#steps-to-customize-a-theme-core-components}

A personalização de um tema é um processo de várias etapas. Para personalizar o tema, execute as etapas na ordem listada:

1. [Clonar um tema](#download-a-theme-core-components)
1. [Definir nome de um tema](#set-name-of-theme)
1. [Personalizar um tema](#customize-the-theme)
1. [Testar um tema](#test-the-theme)
1. [Implantar um tema](#deploy-the-theme)

Os exemplos fornecidos no documento são baseados no **Tela** tema, mas é importante observar que você pode clonar qualquer tema e personalizá-lo usando as mesmas instruções. Essas instruções se aplicam a qualquer tema, permitindo modificar temas de acordo com suas necessidades específicas.

#### 1. Clonar um tema {#download-a-theme-core-components}

Para clonar um tema para os Componentes principais com base no Adaptive Forms, escolha um dos seguintes temas:

* [Tema Tela de desenho](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema CAVALETE](https://github.com/adobe/aem-forms-theme-easel)

Para clonar um tema, execute as seguintes instruções:

1. Abra o prompt de comando ou a janela do terminal no ambiente de desenvolvimento local.

1. Execute o `git clone` comando para clonar um tema.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   Substitua o [Caminho do repositório Git do tema] com o URL real do Repositório Git correspondente do tema

   Por exemplo, para clonar o tema da Tela de Pintura, execute o seguinte comando:

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

   Depois de executar o comando com êxito, você terá uma cópia local do tema disponível em sua máquina na  `aem-forms-theme-canvas` pasta.


#### 2. Definir nome de um tema {#set-name-of-theme}

1. Abra a pasta de temas em um editor de texto simples. Por exemplo, para abrir a variável `aem-forms-theme-canvas` pasta no editor de código do Visual Studio.

1. Navegue até a `aem-forms-theme-canvas` pasta.

1. Execute o seguinte comando:

   ```
         code .
   ```

   ![Abrir a pasta de temas em um editor de texto simples](/help/forms/assets/aem-forms-theme-folder-in-vs-code.png)

   A pasta é aberta no Visual Studio Code.

1. Abra o `package.json` arquivo para edição.

1. Defina os valores para o `name` e `description` atributos.

   O atributo name é usado para identificar exclusivamente o tema, como &quot;aem-forms-wknd-theme&quot; e exibido no **Estilo** guia de **Assistente de criação de formulário**. O atributo de descrição fornece detalhes adicionais sobre o tema, incluindo a finalidade e os cenários para os quais ele foi projetado. Você também pode especificar a versão, a descrição e a licença do tema.

1. Salvar e fechar o arquivo.

![Imagem de alteração do nome do tema da tela de desenho](/help/forms/assets/changename_canvastheme.png)


#### 3. Personalizar um tema {#customize-the-theme}

Você pode personalizar componentes individuais ou fazer alterações no nível do tema usando variáveis globais de um tema. Quaisquer alterações feitas nas variáveis globais afetam todos os componentes individuais. Por exemplo, você pode usar variáveis Globais para alterar a cor da borda de todos os componentes de um Formulário adaptável e uma cor de preenchimento brilhante para definir CTA (Chamada para ação) usando o componente de botão:

* [Definir estilos de nível de tema](#theme-customization-global-level)

* [Definir estilos de nível de componente](#component-based-customization)

##### Definir estilos de nível de tema{#theme-customization-global-level}

A variável `variable.scss` arquivo contém as variáveis globais do tema. Ao atualizar essas variáveis, é possível fazer alterações relacionadas ao estilo no nível do tema. Para aplicar estilos de nível de tema, siga estas etapas:

1. Abra o `<your-theme-sources>/src/site/_variables.scss` arquivo para edição.
1. Altere o valor de qualquer propriedade. Por exemplo, a cor de erro padrão é `red`. Para alterar a cor do erro de `red` para `blue`, altere o código hexadecimal de cor do `$errorvariable`. Por exemplo, `$error: #196ee5`.
1. Salvar e fechar o arquivo.

   ![Editar tema](/help/forms/assets/edit_theme.png)

Da mesma forma, você pode usar o `variable.scss` arquivo para definir a família e o tipo de fonte, as cores do tema e da fonte, o tamanho da fonte, o espaçamento do tema, o ícone de erro, os estilos de borda do tema e mais as variáveis que afetam vários componentes do Formulário adaptável.

##### Definir estilos de nível de componente {#component-based-customization}

Você também pode alterar a fonte, a cor, o tamanho e outras propriedades CSS de um componente principal do Formulário adaptável específico. Por exemplo, botão, caixa de seleção, container, rodapé e muito mais. Você pode criar um botão de estilo ou uma caixa de seleção editando o arquivo CSS do componente específico para alinhá-lo ao estilo de sua organização. Para personalizar o estilo de um componente:

1. Abra o arquivo `<your-theme-sources>/src/components/<component>/<component.scss>` para edição. Por exemplo, para alterar a cor da fonte do componente de botão, abra a variável `<your-theme-sources>/src/components/button/button.scss`, arquivo .
1. Altere o valor de qualquer de acordo com suas necessidades. Por exemplo, para alterar a cor do componente Botão ao passar o mouse para `green`, altere o valor de `color: $white` propriedade na `cmp-adaptiveform-button__widget:hover` classe para código hexadecimal `#12B453` ou qualquer outro tom de `green`. O código final é semelhante ao seguinte:

   ```
   .cmp-adaptiveform-button__widget:hover {
   background: $dark-gray;
   color: #12B453;
   }
   ```

1. Salvar e fechar o arquivo.

   ![Editar CSS da caixa de texto](/help/forms/assets/edit_color_textbox.png)

   >
   >
   > Quando um estilo é definido no nível do tema e do componente, o estilo definido no nível do componente tem prioridade.

#### 4. Testar um tema personalizado {#test-the-theme}

Para visualizar e testar as alterações no ambiente local e personalizar o tema de acordo com os requisitos para diferentes componentes AEM, execute as seguintes etapas:

* 4.1 [Configurar o ambiente local para testes](#rename-env-file-theme-folder)
* 4.2 [Testar o tema usando o ambiente local](#start-a-local-proxy-server)

##### 4.1. Configurar o ambiente local para testes {#rename-env-file-theme-folder}

1. Abra a pasta de temas em um editor de texto simples. Por exemplo, abra `aem-forms-theme-canvas` pasta no editor de código do Visual Studio.
1. Renomeie o `env_template` arquivo para `.env` na pasta de temas e adicione os seguintes parâmetros:

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

   ![Estrutura do tema da tela de desenho](/help/forms/assets/env-file-canvas-theme.png)

##### 4.2 Testar o tema usando o ambiente local {#start-a-local-proxy-server}

1. Navegue até a raiz da pasta de temas. Nesse caso, o nome da pasta do tema é `aem-forms-theme-canvas`.
1. Abra o prompt de comando ou o terminal.
1. Executar `npm install` para instalar as dependências.
1. Executar `npm run live` para visualizar o formulário com o tema atualizado no navegador local.

   >[!NOTE]
   >
   > Se ocorrer um erro durante a execução do `npm run live` execute os seguintes comandos antes de `npm run live` comando:
   >
   > * `npm install parcel --save-dev`
   > * `npm i @parcel/transformer-sass`

Esta é uma implantação ativa. Assim, sempre que fizer alterações e salvar a variável `_variables.scss` e `button.scss` automaticamente as alterações e visualiza a saída mais recente. A linha `[Browsersync] File event [change]` significa que o servidor reconheceu as alterações mais recentes e está implantando as alterações no ambiente local.

![Browsersync de proxy](/help/forms/assets/browser_sync.png)

Após seguir os exemplos fornecidos no nível do tema e no nível do componente para personalizações de tema, as mensagens de erro de um Formulário adaptável são alteradas para a variável `blue` cor, enquanto a cor do rótulo para o componente de botão muda para `green` ao passar o cursor.

**Visualização do estilo do nível do tema**

![Exemplo: Cor de erro definida como azul](/help/forms/assets/theme-level-changes.png)

**Visualização do estilo de nível do componente**

![Exemplo: a cor de foco está definida como verde](/help/forms/assets/button-customization.png)

###### Testar o tema para formulários hospedados em um ambiente de Cloud Service

Você também pode testar o tema do Formulário adaptável hospedado em sua instância do AEM Forms as a Cloud Service. Para configurar e definir o ambiente local para o teste dos temas com o Forms adaptável hospedado na instância da nuvem, execute as seguintes etapas:

1. Abra a pasta de temas em um editor de texto simples. Por exemplo, abra `aem-forms-theme-canvas` pasta no editor de código do Visual Studio.
1. Renomeie o `env_template` arquivo para `.env` e adicione os seguintes parâmetros:

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
   > * Ir para **[!UICONTROL Página inicial do AEM]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]** .
   > * Certifique-se de que o usuário é membro do `forms-users` grupo.

1. Navegue até a raiz da pasta de temas. Nesse caso, o nome da pasta do tema é `aem-forms-theme-canvas`.
1. Executar `npm run live` e você for redirecionado a um navegador local.
1. Clique em `SIGN IN LOCALLY (ADMIN TASKS ONLY)` e faça logon usando as credenciais do usuário local.

Você pode visualizar o Formulário adaptável com as alterações mais recentes. Quando estiver satisfeito com as modificações feitas em uma pasta de tema, implante o tema no ambiente do AEM Cloud Service usando o pipeline de front-end.

#### 5. Implantar um tema {#deploy-the-theme}

Para implantar o tema no ambiente Cloud Service usando o pipeline de front-end:

* 5.1 [Criar um repositório para o tema](#create-a-new-theme-repo)
* 5.2 [Enviar as alterações para o repositório](#committing-the-changes)
* 5.3 [Executar o pipeline de front-end](#run-a-frontend-pipeline)

##### 5.1 Criar um repositório para o tema{#create-a-new-theme-repo}

Você precisa de um repositório para implantar o tema. Faça logon no [Repositório do AEM Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) e adicionar novo repositório para o tema.

1. Crie um novo repositório para o tema clicando no link **[!UICONTROL Repositórios]** > **[!UICONTROL Adicionar repositório]**.

   ![criar novo repositório de tema](/help/forms/assets/createrepo_canvastheme.png)


1. Especifique a **Nome do repositório** no **Adicionar repositório** caixa de diálogo. Por exemplo, o nome fornecido é `custom-canvas-theme-repo`.
1. Clique em **[!UICONTROL Salvar]**.

   ![Adicionar tema da tela de desenho ao repositório](/help/forms/assets/addcanvasthemerepo.png)

1. Clique em **[!UICONTROL Copiar URL de repositório]** para copiar o URL do repositório.

   ![URL do tema da tela](/help/forms/assets/copyurl_canvastheme.png)

   >[!NOTE]
   > 
   > * Você pode usar um único repositório para vários temas.
   > * Para implantar temas diferentes, é necessário criar pipelines de front-end separados.
   >* Por exemplo, você pode usar o mesmo repositório, como `custom-canvas-theme-repo`, para tema do Canvas, tema WKND e tema EASEL. No entanto, para implantar os temas, é necessário criar pipelines de front-end separados. Personalizações futuras para um tema específico são implantadas usando o pipeline de front-end correspondente.

##### 5.2. Enviar as alterações para o repositório {#committing-the-changes}

Agora, envie as alterações para o repositório de temas do seu Cloud Service AEM Forms. .

1. Navegue até a raiz da pasta de temas.  Nesse caso, o nome da pasta do tema é `aem-forms-theme-canvas`.
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

O tema é implantado usando o [pipeline de front-end.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html). Para implantar o tema, execute as seguintes etapas:

1. Faça logon no repositório do AEM Cloud Manager.
1. Clique em **[!UICONTROL Adicionar]** botão no **[!UICONTROL Pipelines]** seção.
1. Selecionar **[!UICONTROL Adicionar pipeline de não produção]** ou **[!UICONTROL Adicionar pipeline de produção]** com base no ambiente Cloud Service. Por exemplo, aqui a variável **[!UICONTROL Adicionar pipeline de produção]** for selecionada.
1. No **[!UICONTROL Adicionar pipeline de produção]** como parte da **[!UICONTROL Configuração]** etapas, especifique o nome do seu pipeline. Por exemplo, o nome do pipeline é `customcanvastheme`.
1. Clique em **[!UICONTROL Continuar]**.
1. Selecione o **[!UICONTROL Implantação direcionada]** > o **[!UICONTROL Código de front-end]** opções, na caixa **[!UICONTROL Código-fonte]** etapas.
1. Selecione o **[!UICONTROL Repositório]** e a variável **[!UICONTROL Ramificação Git]** que têm suas alterações mais recentes. Por exemplo, aqui o nome do repositório selecionado é `custom-canvas-theme-repo` e a ramificação Git é `main`.
1. Selecione o **[!UICONTROL Localização do código]** as `/`, se as alterações estiverem presentes na pasta raiz.
1. Clique em **[!UICONTROL Salvar]**.
   ![criar pipeline de front-end](/help/forms/assets/canvas-theme-frontendpipeline.gif)

   Após a conclusão da configuração do pipeline, o cartão de chamada para ação é atualizado.

1. Clique com o botão direito do mouse no pipeline criado.
1. Clique em **[!UICONTROL Executar]** .

   ![run-a-pipeline](/help/forms/assets/canvas-theme-run-pipeline.png)

Quando a criação for concluída, o tema ficará disponível na instância do autor para uso. Aparece sob o título **[!UICONTROL Estilo]** no assistente de criação do Formulário adaptável, ao criar um novo Formulário adaptável.

![tema personalizado disponível na guia estilo](/help/forms/assets/custom-theme-style-tab.png)

## Aplicar um tema a um formulário adaptável {#using-theme-in-adaptive-form}

As etapas para aplicar um tema a um Formulário adaptável são:

1. Faça logon na instância de autor do AEM Forms.

1. Toque **Adobe Experience Manager** > **Forms** > **Forms e documentos**.

1. Clique em **Criar** > **Forms adaptável**. O assistente para criação do Formulário adaptável é aberto.

1. Selecione o modelo do componente principal na **Origem** guia.
1. Selecione o tema no campo **Estilo** guia.
1. Clique em **Criar**.

Os temas do formulário adaptável são usados como parte de um modelo de formulário adaptável para definir o estilo ao criar um formulário adaptável.

## Práticas recomendadas {#best-practices}

* **Como evitar ativos de outro tema**

  Ao editar um tema, você pode procurar e adicionar ativos (como imagens) de outros temas. Por exemplo, você está editando o fundo de uma página. Por exemplo, ao selecionar **[!UICONTROL Página]** ![botão editar](assets/edit-button.png)> **[!UICONTROL Histórico]** > **[!UICONTROL Adicionar]** > **[!UICONTROL Imagem]**, você verá uma caixa de diálogo que permite navegar e adicionar imagens em outro tema.

  Você pode enfrentar problemas com seu tema atual se um ativo for adicionado de outro tema e o outro tema for movido ou excluído. É recomendável evitar a navegação e adicionar ativos de outros temas.

* **Alteração da largura do layout do painel de contêiner**

  Não é recomendável alterar a largura do layout do painel de contêiner. Quando você especifica a largura de um painel de contêiner, ele se torna estático e não se adapta a exibições diferentes.

* **Usar o editor de formulários ou de temas para trabalhar com cabeçalho e rodapé**

  Use o editor de temas se desejar estilizar o cabeçalho e o rodapé usando opções de estilo, como estilo da fonte, plano de fundo e transparência.
Se você quiser fornecer informações como uma imagem de logotipo, o nome da empresa no cabeçalho e informações de direitos autorais no rodapé, use as opções do editor de formulários.

## Perguntas frequentes {#faq}

**P:** Qual personalização tem prioridade ao fazer personalizações em uma pasta de tema no nível global e no nível do componente?

**Ans:** Quando as personalizações são feitas no nível global e no nível do componente, a personalização no nível do componente tem prioridade.

<!--

## See next

* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/features/responsive-layout.md)
* [Generate Document of Record for Adaptive Forms (Core Components](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Create an Adaptive Forms with Repeatable sections](/help/forms/create-forms-repeatable-sections.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)


>[!MORELIKETHIS]
>
>* [Enable Adaptive Forms Core Components on AEM Forms as a Cloud Service and local development environment](/help/forms/enable-adaptive-forms-core-components.md)

-->


## Consulte também {#see-also}

{{see-also}}
* [Definir layout de formulários para diferentes tamanhos de tela e tipos de dispositivo](/help/sites-cloud/authoring/features/responsive-layout.md)
* [Gerar documento de registro para o Forms adaptável (componentes principais)](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Criar um Forms adaptável com seções repetíveis](/help/forms/create-forms-repeatable-sections.md)
* [Modelos de temas de amostra e modelos de dados de formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
* [Habilitar os componentes principais de formulários adaptáveis no AEM Forms as a Cloud Service e no ambiente de desenvolvimento local](/help/forms/enable-adaptive-forms-core-components.md)
