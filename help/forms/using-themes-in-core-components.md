---
title: Criação e uso de temas
description: É possível usar temas para estilizar e fornecer uma identidade visual a um Formulário adaptável usando componentes principais. Você pode compartilhar um tema em qualquer número de adaptadores Forms.
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 7%

---


# Introdução aos Temas do formulário adaptável usando os Componentes principais {#introduction-to-themes-for-af-using-core-components}

É possível criar e aplicar temas para estilizar um Formulário adaptável usando componentes principais. Um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de plano de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica um tema, o estilo especificado reflete nos componentes correspondentes. O tema é gerenciado de forma independente sem uma referência a um formulário adaptável.

Quando você [criar um formulário adaptável](/help/forms/creating-adaptive-form.md) usando os componentes principais, os temas prontos para uso são exibidos no **Estilo** guia . Por padrão, somente a variável **Tela** tema está disponível.

>[!NOTE]
>
>Um tema de Forma adaptável não deve ser confundido com [Modelos de formulário adaptável.](/help/forms/template-editor.md) Os temas de formulário adaptável contêm apenas as informações de estilo para um formulário adaptável. Os modelos de formulário adaptável definem a estrutura do formulário e o conteúdo inicial e contêm um tema para permitir a criação de novos [Formulário adaptável.](/help/forms/creating-adaptive-form.md)

## Utilização do tema Tela no Adaptive Forms com componentes principais {#using-theme-in-adaptive-form}

As etapas para aplicar o tema a um formulário adaptável são:

1. Faça logon na instância do autor do AEM Forms.

1. Toque **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**.

1. Clique em **Criar** > **Forms adaptável**. O assistente para criar o formulário adaptável é aberto.

1. Selecione o modelo do componente principal na **Origem** guia .

   >[!NOTE]
   >
   > Ao criar um Formulário adaptável com componentes principais, você verá o tema Tela na guia Estilo . Este é o único tema pronto para uso disponível agora. Mas você pode alterar o tema para sua preferência e salvá-lo para uso futuro configurando um pipeline de primeiro plano.

1. Selecione o tema Tela na **Estilo** guia .
1. Clique em **Criar**.

Os temas de formulário adaptável são usados como parte de um modelo de formulário adaptável para definir o estilo ao criar um formulário adaptável.

## Personalizar o tema {#customizing-theme}

Para personalizar um tema,

* [configurar um pipeline no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* Configure um usuário com a [função de contribuidor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* Você deveria ter um [conhecimento básico do Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) Repositórios e Cloud Service Git.

Para personalizar um tema de Tela:
1. [Clonar o tema Tela](#1-download-canvas-theme-download-canvas-theme)
1. [Compreender a estrutura do tema](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [Crie o ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [Iniciar o servidor proxy local](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [Personalizar o tema](#customize-the-theme-customizing-theme)
1. [Confirmar as alterações](#6-committing-the-changes-committing-the-changes)
1. [Implantar o pipeline](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1. Clonar o tema Tela {#download-canvas-theme}

Abra o prompt de comando e execute o seguinte comando para clonar o tema da tela:

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> A guia Estilo do Assistente de criação de formulário exibe o mesmo nome de tema como package.json .

### 2. Compreender a estrutura do tema {#structure-of-canvas-theme}

Um tema de Formulário adaptável é um pacote que contém os recursos de CSS, JavaScript e estáticos que definem o estilo de seu formulário e estão em conformidade com a estrutura de um tema de Formulário adaptável. Um tema de formulário adaptável tem a seguinte estrutura típica de um projeto front-end:

* `src/components`: Arquivos JavaScript e CSS específicos AEM componentes principais
* `src/resources`: arquivos estáticos como ícones, logotipos e fontes
* `src/site`: Arquivos JavaScript e CSS aplicáveis a toda a página do AEM Sites
* `src/theme.ts`: O principal ponto de entrada de seu tema JavaScript e CSS
* `src\theme.scss`: Arquivos JavaScript e CSS aplicáveis a todo o tema

O `src/components` tem arquivos JavaScript e CSS específicos para todos os componentes principais AEM como botão, caixa de seleção, contêiner, rodapé etc. É possível criar um botão de estilo ou uma caixa de seleção ao editar o arquivo CSS específico para o componente AEM.

![Edição do tema](/help/forms/assets/theme_structure.png)

Para personalizar o tema, você pode iniciar o servidor proxy local para ver as personalizações do tema em tempo real com base no conteúdo real do AEM.

### 3. Crie o arquivo .env em uma pasta de tema {#creating-env-file-theme-folder}

Crie um `.env` na pasta de temas e adicione os seguintes parâmetros:

* **URL de AEM**
AEM_URL=https://[author-instance] ou http://localhost:[porta]/

* **Nome do site AEM**
AEM_ADAPTIVE_FORM=Form_name

* **AEM porta proxy**
AEM_PROXY_PORT=7000


![Estrutura de Tema da Tela](/help/forms/assets/env-file-canvas-theme.png)

### 4. Iniciar um servidor proxy local {#starting-a-local-proxy-server}

1. Na linha de comando, navegue até a raiz do tema no computador local.
1. Execute `npm install` e o npm recupera dependências e instala o projeto.
1. Execute `npm run live` e o servidor proxy é iniciado.

   ![npm run live](/help/forms/assets/theme_proxy.png)

1. Quando o servidor proxy é iniciado, ele abre automaticamente um navegador para `http://localhost:[port]/`.
1. Toque ou clique **FAZER LOGON LOCALMENTE (SOMENTE TAREFAS DE ADMINISTRADOR)** e faça logon com as credenciais do usuário proxy fornecidas pelo administrador do AEM.

   ![Fazer logon localmente](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * Crie um usuário local para fazer logon localmente. Forneça a função de contribuidor para o designer de temas.
   > * Se você especificar o URL AEM como `http://localhost:[port]/` no `.env` do tema Tela, você é redirecionado diretamente para o navegador.


1. Depois de fazer logon, altere o URL no navegador de modo que aponte o caminho para o conteúdo de amostra que o administrador do AEM forneceu.

   * Por exemplo, se o caminho fornecido foi `/content/formname.html?wcmmode=disabled`, altere o URL para `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![Conteúdo de amostra proxy](/help/forms/assets/sample_af.png)

Navegue até um formulário adaptável para ver o tema Tela aplicado a um formulário adaptável.

### 5. Personalizar o tema {#customize-theme}

1. No editor, abra o arquivo `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > Você pode criar um estilo para todos os componentes do Formulário adaptativo em um site diretamente editando o `site/_variables.scss` arquivo.

1. Edite a variável para o `font colour` para `red`.

   ![Editar tema](/help/forms/assets/edit_theme.png)

   **Estilo dos diferentes componentes de AEM**

   É possível criar um estilo para os diferentes componentes de um formulário adaptável, alterando seu arquivo CSS no editor. Existem diferentes pastas CSS para cada componente principal do Formulário adaptável na pasta Tema da tela.

   ![Componente principal](/help/forms/assets/theme-component.png)

   Para especificar estilos para um componente específico no editor de temas, você pode editar o CSS em uma pasta de temas. Por exemplo, se você quiser alterar a cor da borda de um campo de caixa de texto, abra o arquivo CSS no editor e altere a cor da borda.

   ![Editar CSS da Caixa de Texto](/help/forms/assets/edit_color_textbox.png)

1. Ao salvar o arquivo, o servidor proxy reconhece a alteração por meio da linha `[Browsersync] File event [change]`.

   ![Browsersync de proxy](/help/forms/assets/browser_sync.png)

1. Ao retornar ao navegador do servidor proxy local, a alteração fica imediatamente visível.

   ![Alterar tema AF](/help/forms/assets/edit_theme_af.png)

O designer de temas visualiza as alterações no servidor proxy local e personaliza o tema de acordo com os requisitos de diferentes componentes de AEM.

Antes de confirmar as alterações no repositório Git do AEM, é necessário acessar o [Informações do repositório Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 6. Confirmar as alterações {#committing-the-changes}

Depois de fazer alterações no tema e testá-lo com um servidor proxy local, confira as alterações no repositório Git do seu Cloud Service AEM Forms. Ela disponibiliza o tema personalizado no ambiente do Cloud Service Forms para que os autores do Adaptive Forms possam usá-lo.

Antes de confirmar as alterações no repositório Git do seu Cloud Service AEM Forms, é necessário um clone do repositório no computador local. Para clonar o repositório:

1. Abra o prompt de comando e execute o comando abaixo após substituir [my-org] e [my-program] com valores fornecidos pelo administrador do AEM. Você também pode encontrar detalhes na sua [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git):

   ```
   git clone https://git.cloudmanager.adobe.com/[my-org]/[my-org]/
   ```
1. Mova o projeto de tema que você estava editando para o repositório clonado com um comando semelhante a `mv <theme-sources> <cloned-repo>`.
1. Faça as alterações desejadas nas pastas do componente de tema modificando seu arquivo CSS.
1. No diretório do repositório clonado, confira os arquivos de tema que você acabou de mover com os seguintes comandos.

   ```text
   git add <theme-file-name>
   git commit -m "Adding theme sources"
   git push
   ```

1. As personalizações são enviadas para o repositório Git.

   ![Alterações confirmadas](/help/forms/assets/cmd_git_push.png)

Suas personalizações agora são armazenadas com segurança no repositório Git.


### 7. Implantar o pipeline de frontend {#deploy-pipeline}

Implante seu tema personalizado usando o pipeline de front-end. Saiba mais [como configurar um pipeline de linha de frente para implantar tema personalizado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).


>[!NOTE]
>
>Futuramente, se você fizer modificações na pasta de temas Canvas , precisará executar o pipeline acima novamente. Por conseguinte, é necessário lembrar o nome do gasoduto.

## Exemplo para personalizar o tema {#example-to-customize-a-theme}

1. Faça logon na instância do autor do AEM Forms.
1. Abra um formulário adaptável criado usando componentes principais.
1. Inicie o servidor proxy local usando o prompt de comando e clique em **FAZER LOGON LOCALMENTE (SOMENTE TAREFAS DE ADMINISTRADOR)**.
1. Depois de fazer logon, você será redirecionado para o navegador e verá o tema aplicado.
1. Baixe o tema Canvas e extraia a pasta zip baixada.
1. Abra a pasta zip extraída no editor preferencial.
1. Crie um `.env` na pasta de temas e adicione parâmetros: **URL AEM**, **AEM_ADAPTIVE_FORM** e **AEM_PROXY_PORT**.
1. Abra o arquivo CSS da caixa de texto na pasta de tema Tela e altere a cor da borda para dizer `red` e salve as alterações.
1. Reabra o navegador novamente e veja que as alterações são refletidas imediatamente em um formulário adaptável.
1. Mova a pasta de tema da tela em seu repositório clonado.
1. Confirme as alterações e implante o pipeline de front-end.

Depois que o pipeline for executado, o tema estará disponível na guia Style .

## Práticas recomendadas {#best-practices}

* **Evitar ativos de outro tema**

   Ao editar um tema, você pode procurar e adicionar ativos (como imagens) de outros temas. Por exemplo, você está editando o plano de fundo de uma página. Por exemplo, ao selecionar **[!UICONTROL Página]** ![botão editar](assets/edit-button.png)> **[!UICONTROL Histórico]** > **[!UICONTROL Adicionar]** > **[!UICONTROL Imagem]**, você verá uma caixa de diálogo que permite navegar e adicionar imagens em outro tema.

   Você pode enfrentar problemas com seu tema atual se um ativo for adicionado de outro tema e o outro tema for movido ou excluído. É recomendável evitar navegar e adicionar ativos de outros temas.

* **Alteração da largura do layout do painel do contêiner**

   Não é recomendável alterar a largura do layout do painel do contêiner. Quando você especifica a largura de um painel de contêiner, ele se torna estático e não se adapta a exibições diferentes.

* **Uso do editor de formulário ou do editor de temas para trabalhar com o cabeçalho e o rodapé**

   Use o editor de temas se desejar criar um estilo de cabeçalho e rodapé usando opções de estilo, como estilo de fonte, plano de fundo e transparência.
Se desejar fornecer informações como uma imagem de logotipo, nome da empresa no cabeçalho e informações de direitos autorais no rodapé, use as opções do editor de formulário.
