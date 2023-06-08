---
title: Criação e uso de temas
description: Você pode usar temas para estilizar e fornecer uma identidade visual a um Formulário adaptável usando componentes principais. Você pode compartilhar um tema em qualquer número do Adaptive Forms.
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: f22554450d2eb1f4948f749ba00f78b568ee308f
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 5%

---

# Temas no Forms adaptável (Componentes principais) {#themes-for-af-using-core-components}

Você pode criar e aplicar temas para estilizar um Formulário adaptável usando os componentes principais. Um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica um tema, o estilo especificado é refletido nos componentes correspondentes. O tema é gerenciado de forma independente sem uma referência a um Formulário adaptável.

Quando você [criar um Formulário adaptável](/help/forms/creating-adaptive-form.md) usando os componentes principais, os temas prontos para uso aparecem no menu **Estilo** guia. Por padrão, somente a variável **Tela** tema está disponível.

>[!NOTE]
>
>Um tema de formulário adaptável não deve ser confundido com [Modelos de formulário adaptável.](/help/forms/template-editor.md) Os temas do Formulário adaptável contêm apenas as informações de estilo de um Formulário adaptável. Os modelos de formulário adaptável definem a estrutura do formulário e o conteúdo inicial, além de conter um tema para permitir a criação de novos [Formulário adaptável.](/help/forms/creating-adaptive-form.md)

## Uso do tema da Tela no Adaptive Forms usando componentes principais {#using-theme-in-adaptive-form}

As etapas para aplicar o tema a um Formulário adaptável são:

1. Faça logon na instância de autor do AEM Forms.

1. Toque **Adobe Experience Manager** > **Forms** > **Forms e documentos**.

1. Clique em **Criar** > **Forms adaptável**. O assistente para criação do Formulário adaptável é aberto.

1. Selecione o modelo do componente principal na **Origem** guia.

   >[!NOTE]
   >
   > Ao criar um Formulário adaptável com componentes principais, você vê o tema Tela de desenho na guia Estilo. Esse é o único tema pronto para uso disponível no momento. Mas você pode alterar o tema de seu gosto e salvá-lo para uso futuro configurando um pipeline de front-end.

1. Selecione o tema da Tela de Pintura na **Estilo** guia.
1. Clique em **Criar**.

Os temas do formulário adaptável são usados como parte de um modelo de formulário adaptável para definir o estilo ao criar um formulário adaptável.

## Personalizar o tema {#customizing-theme}

Para personalizar um tema,

* [configurar um pipeline no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* Configurar um usuário com o [função do colaborador](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* Você deve ter um [conhecimento básico do Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) e os repositórios Git do Cloud Service.

Para personalizar um tema da Tela de Pintura:

1. [Clonar o tema da tela de desenho](#1-download-canvas-theme-download-canvas-theme)
1. [Entender a estrutura do tema](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [Alterar nome em package.json e package_lock.json](#changename-packagelock-packagelockjson)
1. [Crie o ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [Iniciar o servidor proxy local](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [Personalizar o tema](#customize-the-theme-customizing-theme)
1. [Confirmar as alterações](#6-committing-the-changes-committing-the-changes)
1. [Implantar o pipeline](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1. Clone o tema da Tela de Pintura {#download-canvas-theme}

Abra o prompt de comando e execute o seguinte comando para clonar o tema da tela:

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> A guia Estilo do Assistente de criação de formulário exibe o mesmo nome de tema do arquivo package.json.

### 2. Compreender a estrutura do tema {#structure-of-canvas-theme}

Um tema de formulário adaptável é um pacote que contém o CSS, o JavaScript e os recursos estáticos que definem o estilo do seu formulário e está em conformidade com a estrutura de um tema de formulário adaptável. Um tema do formulário adaptável tem a seguinte estrutura típica de um projeto front-end:

* `src/components`: arquivos JavaScript e CSS específicos para componentes principais do AEM
* `src/resources`: arquivos estáticos como ícones, logotipos e fontes
* `src/site`: arquivos JavaScript e CSS que se aplicam a toda a página do AEM Sites
* `src/theme.ts`: o principal ponto de entrada do seu JavaScript e tema CSS
* `src\theme.scss`: arquivos JavaScript e CSS que se aplicam a todo o tema

A variável `src/components` A pasta tem arquivos JavaScript e CSS específicos para todos os componentes principais do AEM, como botão, caixa de seleção, contêiner, rodapé etc. Você pode estilizar o botão ou a caixa de seleção editando o arquivo CSS específico ao componente AEM.

![Edição do tema](/help/forms/assets/theme_structure.png)

Para personalizar o tema, você pode iniciar o servidor proxy local para ver as personalizações do tema em tempo real com base no conteúdo real do AEM.

### 3. Altere o nome em package.json e package_lock.json do tema da Tela {#changename-packagelock-packagelockjson}

Atualize o nome e a versão do tema da Tela de Pintura no `package.json` e `package_lock.json` arquivos.

>[!NOTE]
>
> Os nomes não devem ter `@aemforms` tag. Deve ser um texto simples como nome fornecido pelo usuário.

![Imagem do tema da tela de desenho](/help/forms/assets/changename_canvastheme.png)

### 4. Crie o arquivo .env em uma pasta de temas {#creating-env-file-theme-folder}

Criar um `.env` na pasta de temas e adicione os seguintes parâmetros:

* **URL do AEM**
AEM_URL=https://[author-instance]

* **Nome do site AEM**
AEM_ADAPTIVE_FORM=Nome_do_formulário

* **Porta de proxy AEM**
AEM_PROXY_PORT=7000


![Estrutura do tema da tela de desenho](/help/forms/assets/env-file-canvas-theme.png)

### 5. Iniciar um servidor proxy local {#starting-a-local-proxy-server}

1. Na linha de comando, navegue até a raiz do tema no computador local.
1. Execute `npm install` e o npm recupera dependências e instala o projeto.
1. Execute `npm run live` e o servidor proxy é iniciado.

   ![npm run live](/help/forms/assets/theme_proxy.png)


1. Toque ou clique **FAZER LOGON LOCALMENTE (SOMENTE TAREFAS DE ADMINISTRADOR)** e faça logon com as credenciais de usuário proxy fornecidas pelo administrador do AEM.

   ![Fazer logon localmente](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * Crie um usuário local para fazer logon localmente. Forneça a função de colaborador para o designer de tema.
   > * Se você especificar o URL do AEM como `http://localhost:[port]/` no `.env` arquivo do tema da Tela, você é redirecionado diretamente para o navegador.


1. Depois de fazer logon, altere o URL no navegador de modo que aponte o caminho para o conteúdo de amostra que o administrador do AEM forneceu.

   * Por exemplo, se o caminho fornecido foi `/content/formname.html?wcmmode=disabled`, altere o URL para `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![Conteúdo de amostra proxy](/help/forms/assets/sample_af.png)

Navegue até um Formulário adaptável para ver o tema da Tela de desenho aplicado a um Formulário adaptável.

### 6. Personalizar o tema {#customize-theme}

1. No editor, abra o arquivo `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > É possível estilizar todos os componentes do Formulário adaptável em um Site diretamente ao editar o `site/_variables.scss` arquivo.

1. Edite a variável para o `font colour` para `red`.

   ![Editar tema](/help/forms/assets/edit_theme.png)

   **Estilizar os diferentes componentes do AEM**

   Você pode estilizar os diferentes componentes de um Formulário adaptável alterando seu arquivo CSS no editor. Há diferentes pastas CSS para cada componente principal do Formulário adaptável na pasta do Tema da Tela.

   ![Componente principal](/help/forms/assets/theme-component.png)

   Para especificar estilos para um componente específico no editor de temas, edite o CSS em uma pasta de temas. Por exemplo, se você quiser alterar a cor da borda de um campo de caixa de texto, abra o arquivo CSS no editor e altere sua cor de borda.

   ![Editar CSS da caixa de texto](/help/forms/assets/edit_color_textbox.png)

1. Ao salvar o arquivo, o servidor proxy reconhece a alteração através da linha `[Browsersync] File event [change]`.

   ![Browsersync de proxy](/help/forms/assets/browser_sync.png)

1. Ao retornar ao navegador do servidor proxy local, a alteração fica visível imediatamente.

   ![alterar tema de AF](/help/forms/assets/edit_theme_af.png)

O designer do tema visualiza as alterações no servidor proxy local e personaliza o tema de acordo com os requisitos para diferentes componentes do AEM.

Antes de confirmar as alterações no repositório Git do AEM, é necessário acessar [Informações do repositório Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 7. Confirmar as alterações {#committing-the-changes}

Depois de fazer alterações no tema e testá-lo com um servidor proxy local, confirme as alterações no repositório Git do Cloud Service AEM Forms. Ele disponibiliza o tema personalizado em seu ambiente Forms Cloud Service para que os autores do Adaptive Forms usem o.

Antes de confirmar as alterações no repositório Git do Cloud Service AEM Forms, é necessário um clone do repositório no computador local. Para clonar o repositório:

1. Crie um novo repositório de temas clicando no ícone **[!UICONTROL Repositórios]** opção.

   ![criar novo repositório de tema](/help/forms/assets/createrepo_canvastheme.png)

1. Clique em **[!UICONTROL Adicionar repositório]** e especificar a **Nome do repositório** no **Adicionar repositório** caixa de diálogo. Clique em **[!UICONTROL Salvar]**.

   ![Adicionar tema da tela de desenho ao repositório](/help/forms/assets/addcanvasthemerepo.png)

1. Clique em **[!UICONTROL Copiar URL de repositório]** para copiar o URL do repositório criado.

   ![URL do tema da tela](/help/forms/assets/copyurl_canvastheme.png)

1. Abra o prompt de comando e clone o repositório na nuvem criado acima.

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. Mova os arquivos do repositório de temas que você está editando para o repositório na nuvem com um comando semelhante a
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
Por exemplo, use este comando 
`cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. No diretório do repositório da nuvem, confirme os arquivos de tema movidos para o com os seguintes comandos.

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. As personalizações são enviadas para o repositório Git.

   ![Alterações confirmadas](/help/forms/assets/cmd_git_push.png)

Suas personalizações agora estão armazenadas com segurança no repositório Git.


### 8. Executar o pipeline de front-end {#deploy-pipeline}

1. Crie o pipeline de front-end para implantar o tema personalizado. Saiba mais [como configurar um pipeline de linha de frente para implantar um tema personalizado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).
1. Execute o pipeline de front-end criado para implantar a pasta de tema personalizada no **[!UICONTROL Estilo]** de um assistente de criação de Formulário adaptável.

>[!NOTE]
>
>No futuro, se fizer modificações na pasta de temas da Tela de Pintura, será necessário executar novamente o pipeline acima. Portanto, é necessário lembrar o nome do pipeline.

## Exemplo para personalizar o tema {#example-to-customize-a-theme}

1. Faça logon na instância de autor do AEM Forms.
1. Abra um Formulário adaptável criado usando os componentes principais.
1. Inicie o servidor proxy local usando o prompt de comando e clique em **FAZER LOGON LOCALMENTE (SOMENTE TAREFAS DE ADMINISTRADOR)**.
1. Depois de fazer logon, você será redirecionado para o navegador e verá o tema aplicado.
1. Baixe o [Tema da tela de desenho](https://github.com/adobe/aem-forms-theme-canvas) e extraia a pasta zip baixada.
1. Abra a pasta zip extraída no editor de sua preferência.
1. Criar um `.env` arquivo na pasta de temas e adicionar parâmetros: **URL do AEM**, **AEM_ADAPTIVE_FORM** e **AEM_PROXY_PORT**.
1. Abra o arquivo CSS da caixa de texto na pasta de temas da Tela de Pintura e altere a cor da borda para `red` colorido e salve as alterações.
1. Abra o navegador novamente e você verá que as alterações são refletidas imediatamente em um Formulário adaptável.
1. Mova a pasta do tema da tela de desenho no repositório clonado.
1. Confirme as alterações e execute o pipeline de front-end.

Depois que o pipeline é executado, o tema fica disponível na guia Estilo.

## Práticas recomendadas {#best-practices}

* **Como evitar ativos de outro tema**

   Ao editar um tema, você pode procurar e adicionar ativos (como imagens) de outros temas. Por exemplo, você está editando o fundo de uma página. Por exemplo, ao selecionar **[!UICONTROL Página]** ![botão editar](assets/edit-button.png)> **[!UICONTROL Histórico]** > **[!UICONTROL Adicionar]** > **[!UICONTROL Imagem]**, você verá uma caixa de diálogo que permite navegar e adicionar imagens em outro tema.

   Você pode enfrentar problemas com seu tema atual se um ativo for adicionado de outro tema e o outro tema for movido ou excluído. É recomendável evitar a navegação e adicionar ativos de outros temas.

* **Alteração da largura do layout do painel de contêiner**

   Não é recomendável alterar a largura do layout do painel de contêiner. Quando você especifica a largura de um painel de contêiner, ele se torna estático e não se adapta a exibições diferentes.

* **Usar o editor de formulários ou de temas para trabalhar com cabeçalho e rodapé**

   Use o editor de temas se desejar estilizar o cabeçalho e o rodapé usando opções de estilo, como estilo da fonte, plano de fundo e transparência.
Se você quiser fornecer informações como uma imagem de logotipo, o nome da empresa no cabeçalho e informações de direitos autorais no rodapé, use as opções do editor de formulários.
