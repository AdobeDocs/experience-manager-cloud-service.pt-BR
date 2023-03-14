---
title: Crie um Forms envolvente usando componentes principais e headless
seo-title: Build Engaging Forms Using Core Components and Headless
description: Crie um Forms envolvente usando componentes principais e headless
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
source-git-commit: 8f3ffc72507be1d28bc437041579578d6a479e23
workflow-type: tm+mt
source-wordcount: '2453'
ht-degree: 1%

---


# Crie um Forms envolvente usando componentes principais e headless

## Visão geral do laboratório

Neste laboratório prático, você aprende:

Como usar o AEM Forms para criar facilmente formulários adaptáveis usando os componentes principais mais recentes, consistentes com o AEM Sites, habilitar experiências de captura de dados omnicanal fornecendo os formulários adaptáveis como formulários headless para a Web, dispositivos móveis e bate-papo. Você também aprende as práticas recomendadas em relação a estilo, personalizações e desenvolvimento de front-end.

## Principais pontos

* **Agilidade comercial**: Como usuário empresarial, posso criar experiência de formulário para vários canais facilmente.

* **Poder para o desenvolvedor de front-end**: como desenvolvedor de front-end, posso controlar a experiência do usuário final usando formulários headless.

* **Velocidade do desenvolvedor**: como desenvolvedor, posso personalizar de maneira fácil e consistente os componentes do Sites e do Forms.

## Pré-requisitos

AEM Forms como sandbox Cloud Service

## Lição 1

### Objetivo

Familiarize-se com o ambiente as a Cloud Service do AEM Forms.

### Contexto da lição

Nesta lição, você se familiariza com o ambiente as a Cloud Service do AEM Forms navegando na interface do usuário.

### Exercício

1. Abra o navegador e insira o URL do ambiente do autor do Cloud Service. Por exemplo:
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Faça logon no ambiente de autor do Cloud Service de acordo com as credenciais compartilhadas. Por exemplo: Nome de usuário: [L716+001@summitlab.us](mailto:L716%2B001@summitlab.us)
Senha: 
**Adobe 123!**

1. Depois de fazer logon, navegue até a interface do usuário do AEM Forms. Clique em **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. Clique em **Forms e documentos**. Ignore qualquer pop-up relacionado às preferências ou informações.

   ![](/help/forms/assets/screenshot2028113929.png)

   Todos os formulários disponíveis são exibidos.

   ![](/help/forms/assets/screenshot2028114029.png)

## Lição 2

### Objetivo

Crie um formulário adaptável usando os componentes principais mais recentes, configure e envie o formulário.

## Contexto da lição

Nesta lição, como usuário empresarial, você criará um formulário adaptável para vários canais, como Web, celular e bate-papo, usando a criação de formulários adaptáveis com componentes principais OOTB padronizados para captura de dados.

## Exercício

1. Crie um ponto de extremidade de envio para o formulário:

   1. Abertura <https://requestbin.com/> em uma nova guia do navegador.
      ![](/help/forms/assets/screenshot2028114329.png)

   1. Clique em **Criar um compartimento público** e copie o URL do endpoint.
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. Crie um formulário adaptável usando a interface do Assistente:

   1. Na guia do navegador usada na Lição 1, navegue até AEM Forms como interface da Web Cloud Service e navegue até Forms e Documentos.
      ![](/help/forms/assets/screenshot2028114029.png)

   1. Clique em **Criar** e selecione Formulário adaptável.
      ![](/help/forms/assets/screenshot2028114629.png)

   1. Selecione o **Em branco com Componentes principais** modelo na tela de seleção de modelo, conforme mostrado abaixo:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Clique em **Estilo** e selecione a guia **wknd-theme** tema conforme mostrado abaixo:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Clique em **Envio** e selecione a guia **Enviar para ponto de extremidade REST** e especifique o compartimento público no
      **URL da solicitação POST** conforme mostrado abaixo:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Clique em **Criar**. Especifique um nome e um título para o formulário. Por exemplo, **contactus**. Clique em **Criar**.
      ![](/help/forms/assets/screenshot2028123329.png)

   1. O editor de formulário adaptável é aberto. Ignore pop-ups ou caixas de diálogo para preferências ou informações. Clique no navegador de componentes no painel à esquerda e adicione o **Rodapé** na parte inferior do formulário em branco.
      ![](/help/forms/assets/screenshot2028121929.png)

   1. Adicione o **Cabeçalho** componente na parte superior do formulário.
      ![](/help/forms/assets/screenshot2028122029.png)

   1. Adicionar um **Título** componente no meio do formulário.
      ![](/help/forms/assets/screenshot2028122129.png)

   1. Adicionar um **Entrada de texto** componente após o componente de título.
      ![](/help/forms/assets/screenshot2028122329.png)

   1. Adicionar um **Entrada de número** componente.
      ![](/help/forms/assets/screenshot2028122429.png)

   1. Adicionar um **Botão Enviar** componente ao formulário.
      ![](/help/forms/assets/screenshot2028122529.png)

   1. Clique em **Título** para que **menu pop-up** é exibido. Clique em **Ícone Editar** no menu para editar o rótulo.
      ![](/help/forms/assets/screenshot2028122629.png)

   1. Enter `Contact Us` como o texto do título.
      ![](/help/forms/assets/screenshot2028122829.png)

   1. Clique em **Entrada de texto** para que o menu pop-up seja exibido. Clique em **Ícone Editar** no menu para editar o rótulo.
      ![](/help/forms/assets/screenshot2028122929.png)

   1. Enter **Nome completo** como rótulo de campo.
      ![](/help/forms/assets/screenshot2028123029.png)

   1. Clique em **Entrada de número** para que o menu pop-up seja exibido. Clique em **Ícone Editar** no menu para editar o rótulo.
      ![](/help/forms/assets/screenshot2028123129.png)

   1. Insira o **Número de telefone** como o rótulo do campo.
      ![](/help/forms/assets/screenshot2028123829.png)


1. Adicionar validações ao formulário:

   1. Clique em **Número de telefone** para que o menu pop-up seja exibido. Clique em **Ícone de chave inglesa** no menu para configurar o campo.
      ![](/help/forms/assets/screenshot2028123429.png)

   1. Abra o **guia validações**, marcar o campo **Obrigatório** e clique em **Concluído**. A mensagem de sucesso é exibida.
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. Clique em **Visualizar** para visualizar o formulário de uma perspectiva do usuário final.
      ![](/help/forms/assets/screenshot2028125529.png)

   1. Preencher o formulário com dados fictícios
      ![](/help/forms/assets/screenshot2028125629.png)

   1. Enviar o formulário
      ![](/help/forms/assets/screenshot2028125729.png)

   1. Na guia Bandeja de solicitações, verifique os dados enviados.
      ![](/help/forms/assets/screenshot2028125829.png)

Agora, para a finalidade do exercício restante, use um formulário de registro pré-criado.

1. Abra a interface de gerenciamento do AEM Forms, por exemplo, `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`e selecione o formulário de registro.

   ![](/help/forms/assets/screenshot2028115529.png)

1. Clique em **Publicar**.

   ![](/help/forms/assets/screenshot2028115629.png)

   A mensagem de sucesso é exibida.

   ![](/help/forms/assets/screenshot2028115729.png)

   A URL de publicação do formulário seria semelhante a `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. Para visualizar o formulário publicado, substitua a ID do programa (pXXXXXX) e a ID do ambiente (eXXXXXX) no URL acima pelas IDs do seu ambiente.

## Lição 3

### Objetivo

Atualizar estilos usando práticas recomendadas de desenvolvimento de front-end.

### Contexto da lição

Nesta lição, como desenvolvedor front-end, você aprenderá como atualizar facilmente o estilo do formulário adaptável criado anteriormente.

### Exercício

Configurar repositório local do tema:

1. Abra o prompt de comando ou o shell com direitos de administrador:

   ![](/help/forms/assets/screenshot2028115829.png)

1. No Prompt de Comando, use o seguinte comando para navegar até **c:\git** pasta

   ```Shell
   cd c:\git
   ```

1. Use o seguinte comando para clonar o código de front-end do tema:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Use o seguinte comando na ordem listada para navegar até a **aem-forms-theme-canvas** e abra o Visual Studio Code.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. Selecionar **Confiar nos autores de todos os arquivos da pasta pai** e clique em **Sim, eu confio nos autores**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. Para renderizar o formulário hospedado no ambiente de publicação do Cloud Service, renomeie o `env_template` arquivo.  Para renomear o arquivo, clique com o botão direito do mouse no **env_template** e selecione o **Renomear** opção.

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. Defina os seguintes valores para as variáveis no arquivo .env e salve o arquivo:

   * **AEM_URL**: especifique o ambiente de publicação do Cloud Service. Por exemplo, `https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**: especifique o caminho do formulário. Por exemplo, se o caminho do formulário for `/content/forms/af/registration`, o valor dessa variável seria `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)

   ![](/help/forms/assets/screenshot20228116569.png)


1. Na janela Prompt de comando, execute o seguinte comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Se você receber uma mensagem solicitando a atualização do npm por meio do `npm notice Run npm nstall -g npm@9.6.0`ignorar a mensagem.
   > * Não execute outros comandos npm, a menos que instruído na pasta de trabalho.


1. Agora execute o seguinte comando para visualizar o formulário.

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   Depois que o comando acima for executado, aguarde o `webpack compiled` mensagem. O formulário é exibido em uma guia do navegador.

   >[!NOTE]
   >
   >Se você encontrar uma tela em branco no navegador após executar o `npm run live` comando, alterar `localhost` no URL do navegador para 127.0.0.1 e na ocorrência **Enter**.



   ![](/help/forms/assets/screenshot2028115129.png)


1. No Visual Studio Code, abra o `PROJECT\src\site\_variables.scss` arquivo. Observe a `$error` A cor é um tom de VERMELHO.

   ![](/help/forms/assets/screenshot2028120729.png)

1. No navegador, envie o formulário para ver a cor Vermelha no **Nome** campo.

   ![](/help/forms/assets/screenshot2028120829.png)

1. Defina o **$error** cor para **#5736eb** e salve o arquivo.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Atualize o navegador e envie o formulário. A cor do erro de aviso no campo de nome foi alterada de acordo.

   ![](/help/forms/assets/screenshot2028121129.png)

1. No Prompt de comando, pressione **CTRL+C**, insira **Y** e pressione **Enter** chave para finalizar o processo npm. É importante interromper o servidor npm para que ele não entre em conflito com o próximo conjunto de exercícios.
1. Feche as janelas Código Visual Studio e Prompt de Comando.

## Lição 4

### Objetivo

Renderize o formulário para Web/dispositivos móveis e outras interfaces como um formulário headless.

### Contexto da lição

Nesta lição, como desenvolvedor de front-end, você aprenderá a renderizar o formulário adaptável criado anteriormente como um formulário headless usando a estrutura de design do espectro do react.

### Exercício

Configure o repositório local usando o projeto inicial do react:

1. Abra o prompt de comando usando direitos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)

1. No Prompt de Comando, use o seguinte comando para navegar até **c:\git** pasta

   ```Shell
   cd c:\git
   ```

1. Use o seguinte comando para clonar o projeto inicial do Formulário adaptável do react:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. Use os seguintes comandos na ordem listada para navegar até o **react-starter-kit-aem-headless-forms** e abra o Visual Studio Code.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   A janela Visual Studio Code é aberta.

   ![](/help/forms/assets/screenshot2028117429.png)

Para renderizar o formulário hospedado no ambiente de publicação do Cloud Service:

1. Renomeie o arquivo env_template para o arquivo .env. Para renomear, clique com o botão direito do mouse no **env_template** e selecione o **Renomear** opção.

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. Defina os seguintes valores para as variáveis no arquivo .env. Depois de atualizar as variáveis, salve o arquivo.

   * **AEM_URL**: especifique a URL do ambiente de publicação do Cloud Service. Por exemplo, `https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**: especifique o caminho do formulário adaptável criado na lição anterior. Por exemplo, `/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Abra a janela de comando, verifique se você está no diretório react-starter-kit-aem-headless-forms e execute o seguinte comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. Na janela Prompt de comando, execute o seguinte comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   O comando acima inicia um servidor de desenvolvimento local que renderizaria a definição do formulário obtido do AEM de forma headless usando a biblioteca de front-end do espectro do react.

   >[!NOTE]
   >
   >Se você encontrar uma tela em branco no navegador após executar o `npm start` comando, alterar `localhost` no URL do navegador para 127.0.0.1 e na ocorrência **Enter**.

   ![](/help/forms/assets/screenshot2028118229.png)

Vamos verificar a execução das regras neste formato headless:

1. Selecione o **Marque a caixa para receber 5% de desconto** opção. A opção subsequente para aplicar cartão de crédito está desativada.

   ![](/help/forms/assets/screenshot2028126229.png)

1. Desmarcar **Marque a caixa para receber 5% de desconto** para ativar a opção de cartão de crédito.

   ![](/help/forms/assets/screenshot2028126329.png)

Vamos fazer alterações no formulário no servidor como um usuário empresarial e visualizar as alterações refletidas no formulário headless automaticamente.

1. Abra a interface de gerenciamento do AEM Forms no navegador. Por exemplo, [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. Selecione o **registro** e clique em **Editar.** Ele abre o formulário no editor de formulários adaptáveis.

   ![](/help/forms/assets/screenshot2028118529.png)

1. Selecione o **Número de telefone** e clique no botão **Ícone Editar (ícone de Lápis)** na barra de ferramentas. Se você não conseguir ver a barra de ferramentas pop-up, alterne para o modo de Edição clicando em **Editar** no canto superior direito, da esquerda para **Visualizar** botão.

   ![](/help/forms/assets/screenshot2028119629.png)

1. Altere o rótulo para Número de celular. Clique em qualquer espaço vazio no formulário e as alterações feitas no formulário serão salvas.

   ![](/help/forms/assets/screenshot2028119729.png)

Vamos publicar o formulário atualizado para propagar as alterações no ambiente de publicação.

1. Na guia AEM Forms management interface, selecione o formulário de registro e clique em **Cancelar publicação**. Se você não vir a variável **Cancelar publicação** , pule para a etapa 3 para publicar as alterações diretamente.

   ![](/help/forms/assets/screenshot2028119829.png)

1. Clique em **Cancelar publicação**. Clique em **Fechar** no respectivo diálogo.

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. Depois que o navegador for atualizado, selecione o formulário de registro e clique em **Publish**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. Clique em **Publicar**. Clique em **Fechar** no respectivo diálogo.

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. Atualize a guia do navegador com o formulário headless exibido. Aviso: o rótulo Número de telefone mudou para Número de celular.

   ![](/help/forms/assets/screenshot2028120529.png)

1. Abra a janela do prompt de comando que é usada para iniciar o **react-starter-kit-aem-headless-forms** projeto, pressione **CTRL+C** e, em seguida, insira **Y** e pressione a tecla Enter para encerrar o processo npm. É importante interromper o servidor npm para que ele não entre em conflito com o próximo conjunto de exercícios.

1. Feche as janelas Código Visual Studio e Prompt de Comando.


## Lição 5

### Objetivo

Renderize o formulário como um formulário headless usando a interface do usuário de materiais do Google

### Contexto da lição

Nesta lição, como desenvolvedor front-end, você aprenderá a renderizar o formulário adaptável criado anteriormente como um formulário headless usando a interface do usuário do Google Material.

### Exercício

Configure o repositório local usando o projeto inicial da interface do usuário do Material:

1. Abra o prompt de comando usando direitos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)


1. No Prompt de Comando, use o seguinte comando para navegar até **c:\git** pasta:

   ```Shell
   cd c:\git
   ```

1. Execute os seguintes comandos na ordem listada para criar uma pasta chamada mui e navegar até a pasta mui usando os seguintes comandos:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Use o seguinte comando para clonar o projeto inicial do Formulário adaptável do react:

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. Use o seguinte comando na ordem listada para navegar até a **react-starter-kit-aem-headless-forms** e abra o código no Visual Studio Code:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

Para renderizar o formulário hospedado no ambiente de publicação do Cloud Service:

1. Renomeie o **env_template** arquivo para **.env** arquivo. Para renomear, clique com o botão direito do mouse no **env_template** arquivo e selecione **Renomear**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. Defina os seguintes valores para as variáveis no arquivo .env. Depois de atualizar as variáveis, salve o arquivo. Use o **CTRL + S** alternar para salvar o arquivo.

   * **AEM_URL**: especifique a URL do ambiente de publicação do Cloud Service. Por exemplo, [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**: especifique o caminho do formulário adaptável criado na lição anterior. Por exemplo, /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. Abra a janela de comando e verifique se você está no estado **react-starter-kit-aem-headless-forms** e execute o seguinte comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. Na janela Prompt de comando, execute o seguinte comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   O comando inicia um servidor de desenvolvimento local e renderiza a definição do formulário obtido do AEM de forma headless, usando a biblioteca de front-end da interface do usuário de materiais do Google.

   >[!NOTE]
   >
   >Se você encontrar uma tela em branco no navegador após executar o `npm start` comando, alterar `localhost` no URL do navegador para 127.0.0.1 e na ocorrência **Enter**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. Para avaliar a execução da mesma lógica de negócios nesta representação de formulário:

   Selecionar **Marque a caixa para receber 5% de desconto**. A opção subsequente **Gostaria de solicitar o formulário de cartão de crédito corporativo We.Finance?** é desativado.

   ![](/help/forms/assets/screenshot2028127329.png)

## Lição 6

### Objetivo

Crie uma aparência alternativa do formulário headless usando variações de componentes da interface do usuário do material

### Contexto da lição

Nesta lição, como desenvolvedor de front-end, você aprenderá a criar uma representação alternativa de diferentes componentes usando a Interface do usuário do material para o formulário adaptável criado anteriormente pelo usuário empresarial.

### Exercício

Atualize a variação de componentes no projeto headless. Para alterar a variante do componente de entrada de texto da interface do usuário de material para `OutlinedInput`:

1. No Visual Code, navegue até o componente de entrada de texto abrindo o `index.tsx` arquivo em `src/components/textinput/index.tsx`.

1. Adicionar `//` no início da linha de código 103. Ele converte a linha em um comentário.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Adicione o seguinte na linha 104 para usar uma variante diferente de componente e salvar o arquivo. Use o **CTRL + S** alternar para salvar o arquivo.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   É essencial usar capitalização correta para a variante &quot;OutlineInput&quot;, caso contrário, a compilação falharia. A compilação do ambiente de desenvolvimento local começa automaticamente no Prompt de comando. Aguarde até ver a seguinte mensagem

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Atualize o navegador, se ele não for atualizado automaticamente, para ver o componente de entrada de texto usar uma variante diferente.

   ![](/help/forms/assets/screenshot2028127729.png)


   Essa alteração ocorre para os usuários finais sem nenhuma alteração na definição do formulário no AEM Forms Server e é específica para o canal headless em consideração. Por exemplo, canal da Web neste laboratório.

   ![](/help/forms/assets/screenshot2028127529.png)


1. Feche as janelas Código do Visual Studio e Prompt de Comando.

## Perguntas frequentes

+++ O assistente de Formulário adaptável está disponível publicamente?

Sim, está disponível com o AEM Forms como Cloud Service.

+++


+++ Os Componentes principais estão disponíveis publicamente?

Sim, os componentes principais do Adaptive Forms estão disponíveis com o AEM Forms como Cloud Service.

+++

+++ Os formulários headless estão disponíveis publicamente?

Sim, os formulários headless estão disponíveis com o AEM Forms como Cloud Service.

+++

+++ Os formulários headless exigem uma licença separada?

Não, os formulários headless usam a mesma métrica de valor de licenciamento, número de envios de formulários.

+++

+++ Os componentes principais e os formulários headless estão disponíveis com o AEM 6.5 Forms?

Sim, os componentes principais dos formulários adaptáveis e os formulários headless estão disponíveis com o AEM Forms 6.5 Service Pack 16 e posteriores.

+++


## Próximas etapas

Agora que você aprendeu a criar formulários adaptáveis e entregá-los a vários canais usando formulários headless, você deve tentar colocar suas novas habilidades em ação. Divirta-se e prossiga criando e fornecendo experiências excepcionais de captura de dados para seus usuários finais, onde eles estiverem, em escala!

## Recursos

* [Introdução aos componentes principais do formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [Criar formulário adaptável usando componentes principais](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [Atualizar estilo para AF com base em componentes principais](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [Formulários adaptáveis headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [Uso do kit inicial Headless do React](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


