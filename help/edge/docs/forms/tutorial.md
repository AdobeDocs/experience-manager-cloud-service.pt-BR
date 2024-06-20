---
title: Introdução ao AEM Forms Edge Delivery Services - Tutorial do desenvolvedor
description: Este tutorial ajuda você a começar a usar um novo projeto do Adobe Experience Manager Forms (AEM). Em dez a vinte minutos, você terá criado seus próprios formulários.
feature: Edge Delivery Services
exl-id: bb7e93ee-0575-44e1-9c5e-023284c19490
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 0%

---

# Introdução - Tutorial do desenvolvedor

Na era digital de hoje, criar formulários amigáveis é essencial para qualquer organização. O AEM Forms Edge Delivery Services (EDS) permite criar formulários usando ferramentas familiares como o Google Docs e o Microsoft Office.

Esses formulários enviam dados diretamente para um arquivo do Microsoft Excel ou do Google Sheets, permitindo que você use um ecossistema vibrante e APIs robustas do Google Sheets, do Microsoft Excel e do Microsoft SharePoint para processar facilmente os dados enviados ou iniciar um fluxo de trabalho de negócios existente.

O AEM Forms fornece um bloco, conhecido como Bloco adaptável do Forms, para ajudar você a criar formulários facilmente para capturar e armazenar dados capturados. Você pode [criar um novo projeto AEM pré-configurado com o Adaptive Forms Block](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) ou [adicionar o bloco adaptável do Forms a um projeto AEM existente](#add-adaptive-forms-block-to-your-existing-aem-project).

Este tutorial do AEM Forms orienta você na criação, visualização e publicação de seu próprio formulário personalizado com um novo projeto do Adobe Experience Manager (AEM) Forms.

## Pré-requisitos

* Você tem uma conta GitHub e compreende as noções básicas sobre Git.
* Você tem uma conta do Google ou do Microsoft SharePoint.
* Você entende as noções básicas do HTML, CSS e JavaScript.
* Você tem o Node/npm instalado para desenvolvimento local.

**Atenção!** Este tutorial usa macOS, Chrome e Visual Studio Code. Embora as etapas possam ser adaptadas para outras configurações, as capturas de tela e os elementos específicos da interface do usuário podem ser diferentes com base no sistema operacional, no navegador e no editor de código escolhidos.


## Criar um novo projeto AEM pré-configurado com o Bloco Forms adaptável

O modelo AEM Forms Boilerplate permite iniciar rapidamente com um projeto AEM pré-configurado com o Bloco de Forms adaptável. É a maneira mais rápida e fácil de seguir as práticas recomendadas para AEM e começar a criar seus formulários.

### Introdução ao modelo de repositório padronizado do AEM Forms

1. Crie um repositório GitHub para seu projeto AEM. Para criar um repositório:
   1. Ir para [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms Boilerplate](/help/edge/assets/aem-forms-boilerplate.png)
   1. Clique em **Usar este modelo** e selecione a opção **Criar um novo repositório** opção. A tela criar um novo repositório é aberta.

      ![Criar novo repositório usando o AEM Forms Boilerplate](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. Na tela criar um novo repositório, selecione a **proprietário** e especifique **Nome do repositório** . O Adobe recomenda que o repositório esteja definido como **Público**. Então, selecione o **público** e clique em **Criar repositório**.

   ![Definir o repositório como público](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. Instale o aplicativo GitHub de sincronização de código AEM em seu repositório. Para instalar:
   1. Ir para [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. Na tela Instalar sincronização do código AEM, selecione a **Selecionar apenas repositórios** e selecione o repositório recém-criado. Clique em Salvar.

   ![Definir o repositório como público](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > Se você estiver usando o GitHub Enterprise com filtragem de IP, é possível adicionar o seguinte IP à inclui na lista de permissões: 3.227.118.73

   Parabéns! Você tem um novo site em execução `https://<branch>--<repo>--<owner>.hlx.page/`.

   * `<branch>` refere-se à ramificação do seu repositório GitHub.
   * `<repository>` indica seu repositório GitHub.
   * `<owner>` refere-se ao nome de usuário da sua conta GitHub que hospeda o repositório GitHub.

   Por exemplo, se o nome da ramificação for `main`, o repositório é `wefinance`, e o proprietário for `wkndforms`, o site estaria funcionando em [https://main--wefinance--wkndforms.hlx.page/](https://main--wefinance--wkndforms.hlx.page/).



### Vincular sua própria fonte de conteúdo

Seu repositório GitHub recém-criado aponta para [exemplo de conteúdo armazenado em uma pasta Google Drive](https://drive.google.com/drive/folders/1bvjfi6TqpYA7DvbX6kKc-m7FgHuJ4RUQ). Esse conteúdo somente leitura fornece um excelente ponto de partida para seus formulários. Sinta-se à vontade para copiá-lo em seu próprio Google Drive e personalizá-lo para atender às suas necessidades.

![Conteúdo de exemplo no Google Drive](/help/edge/assets/folder-with-sample-content.png)

Para copiar o conteúdo de amostra para sua própria pasta de conteúdo e apontar seu repositório GitHub para sua própria pasta de conteúdo:

1. Crie uma nova pasta especificamente para o conteúdo do AEM no Google Drive ou no Microsoft SharePoint. Este documento usa uma pasta criada no Microsoft SharePoint.

1. Compartilhe a pasta com o usuário do Adobe Experience Manager (helix@adobe.com).

   ![Use a opção Gerenciar acesso para compartilhar a pasta com o usuário AEM - SharePoint](/help/edge/assets/share-folder-with-aem-user.png)

   ![Use a opção Gerenciar acesso para compartilhar a pasta com o usuário AEM - Google Drive](/help/edge/assets/share-google-drive-folder.png)


   Certifique-se de ter fornecido direitos de edição na pasta ao usuário do Adobe Experience Manager.

   ![Compartilhar pasta com usuário AEM, fornecer direitos de edição-SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png)

   ![Compartilhe a pasta com o usuário AEM, forneça direitos de edição - Google Drive](/help/edge/assets/add-aem-user-google-folder.png)

1. Copie o [exemplo de conteúdo armazenado na pasta Google Drive](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_) na sua pasta. Para copiar:

   1. Baixe os arquivos juntos ou baixe arquivos individuais.

      ![Baixar conteúdo de amostra](/help/edge/assets/download-sample-content.png)

      A variável `nav` e `footer` os arquivos definem o layout básico de suas páginas e raramente são alterados em um projeto. Eles também têm uma estrutura específica diferente da maioria dos outros arquivos de conteúdo. Ao examinar esses arquivos, você terá uma ideia de como o conteúdo é organizado em projetos AEM.


   1. Faça upload desses arquivos para a pasta Microsoft SharePoint ou Google Drive.

      ![Conteúdo de exemplo no Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      Certifique-se de copiar a variável  `enquiry` do conteúdo de amostra para sua pasta no Google Drive ou no Microsoft SharePoint. Ele contém a estrutura de um formulário de amostra.

1. Agora que sua pasta de conteúdo está configurada, é hora de vinculá-la ao seu projeto no GitHub que você criou usando o AEM Forms Boilerplate anteriormente. Para conectar:

   1. Vá para o repositório GitHub criado anteriormente usando a Matriz do AEM Forms.
   1. Abra o `fstab.yaml` para edição.
   1. Substitua a referência existente pelo caminho para a pasta que você compartilhou com o usuário AEM (helix@adobe.com).

      ![Conteúdo de exemplo no Google Drive](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      Se você usar o Microsoft SharePoint, o caminho da pasta usará o seguinte formato:

      ```HTML
      https://<tenant>.SharePoint.com/sites/<sp-site>/Shared%20Documents/<folder-name>
      ```

      Por exemplo,

      ```HTML
      https://adobe.SharePoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      Para obter mais informações sobre o gerenciamento de arquivos com o Microsoft SharePoint, consulte [Como usar o Adobe SharePoint](https://www.aem.live/docs/setup-customer-sharepoint).


   1. Confirmar o atualizado `fsatb.yaml` após atualizar a referência e tudo ficará bem. Se encontrar problemas de build, consulte [Solução de problemas de build do GitHub](#troubleshooting-github-build-issues).



      ![Confirmar arquivo fsatab.yaml atualizado](/help/edge/assets/commit-updated-fstab-yaml.png)

      Isso conecta sua pasta de conteúdo ao seu site. Depois de atualizar a referência, você pode enfrentar os erros &quot;404 Não encontrado&quot; inicialmente. Isso ocorre porque seu conteúdo ainda não foi visualizado. A próxima seção explica como começar a criar e visualizar seu conteúdo.



### Pré-visualizar e publicar seu conteúdo

Após concluir a última etapa, a nova fonte de conteúdo não ficará vazia, mas não estará visível no site até que seja promovida para a pré-visualização ou estágios ao vivo. No momento, isso pode causar erros 404.

Para visualizar conteúdo não publicado:

1. Instale a extensão do Chrome chamada [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo).

   ![Instalar o AEM Sidekick](/help/edge/assets/install-aem-sidekick.png)

   Depois de instalar a extensão no Chrome, não se esqueça de fixá-la, isso facilita a localização.

   ![Fixar AEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. Para configurar a extensão do Sidekick Chrome, vá para a pasta Google Drive ou Microsoft SharePoint compartilhada anteriormente e clique com o botão direito do mouse no ícone de extensão na barra de ferramentas do navegador e selecione `Add this project`.

   ![AEM Sidekick - Adicionar um projeto](/help/edge/assets/aem-sidekick-add-a-project.png)

   Quando a extensão for instalada e seu projeto for adicionado, você estará pronto para visualizar e publicar seu conteúdo do Google Drive.

1. Selecione todos os documentos na pasta Microsoft SharePoint ou Google Drive. Você pode escolher vários documentos mantendo pressionada a tecla Ctrl (Windows/Linux) ou a tecla Cmd (Mac) enquanto clica em.

   ![Selecionar todos os arquivos](/help/edge/assets/select-all-files.png)

1. Clique no ícone de AEM Sidekick fixado à barra de extensão do Chrome. Uma barra de ferramentas é exibida na tela. Você pode optar por visualizar ou publicar seu conteúdo.

   Se você tiver copiado `index`, `nav`, `footer` e `enquiry` arquivos, todos eles são documentos separados com seus próprios ciclos de visualização e publicação, portanto, visualize (e publique) todos eles.

   Ao visualizar os arquivos, novas guias do navegador exibem os documentos. Para visualizar o formulário de amostra, vá para o seguinte URL:


   ```HTML
   https://<branch>--<repository>--<owner>.hlx.live
   ```

   * `<branch>` refere-se à ramificação do seu repositório GitHub.
   * `<repository>` indica seu repositório GitHub.
   * `<owner>` refere-se ao nome de usuário da sua conta GitHub que hospeda o repositório GitHub.


   `https://<branch>--<repo>--<owner>.hlx.page/enquiry` URL.

   Por exemplo, se o repositório do seu projeto for chamado de &quot;wefinance&quot;, estiver localizado sob o proprietário da conta &quot;wkndforms&quot; e você estiver usando a ramificação &quot;main&quot;, o URL será:

   [https://main--wefinance--wkndforms.hlx.page](https://main--wefinance--wkndforms.hlx.page).

### Criar um formulário

O conteúdo de amostra inclui uma folha de &quot;consulta&quot; que serve como modelo para o formulário &quot;consulta&quot;. Cada linha da planilha representa um [campo de formulário](/help/edge/docs/forms/form-components.md#available-components)e os cabeçalhos de coluna definem a variável [propriedades do campo](/help/edge/docs/forms/form-components.md#available-components). Este formulário de amostra oferece uma vantagem inicial na criação do formulário.

![Formulário de consulta](/help/edge/docs/forms/assets/enquiry-form-microsoft-sharepoint.png)

Vamos começar com a atualização de um rótulo de campo. Abra a planilha &quot;consulta&quot; para edição, altere o rótulo do botão enviar para `Let's Chat` e use o AEM Sidekick para visualizar e publicar o arquivo.

![Formulário de consulta](/help/edge/assets/enquiry-form-preview-publish.png)

Ao visualizar ou publicar o arquivo, uma versão JSON do arquivo é exibida em uma nova guia. Copie o URL de visualização (.hlx.page) ou publicação (.hlx.live) do arquivo.

![JSON da planilha de formulário](/help/edge/assets//preview-and-publish-enquiry-form.png)

Abra o `enquiry` e substitua o URL no bloco de formulário pelo URL do arquivo copiado na etapa anterior. Certifique-se de que o URL seja um hiperlink.

![Arquivo de consulta com o URL .json do URL da planilha](/help/edge/assets/enquiry-doc-to-embed-form.png)

Use o AEM Sidekick para visualizar e publicar o documento de consulta.

![Arquivo de consulta com o URL .json do URL da planilha](/help/edge/assets/preview-and-publish-enquiry-document.png)


Para visualizar o formulário de consulta atualizado, vá para o seguinte URL:


```HTML
    https://<branch>--<repository>--<owner>.hlx.page/enquiry
       
```

O rótulo do botão de envio é atualizado para `Let's Chat`.

![Formulário de consulta](/help/edge/assets/updated-form.png)

Para obter informações detalhadas sobre como criar e publicar um novo formulário, vá para a [criar um formulário](/help/edge/docs/forms/create-forms.md) guia.

### Começar a desenvolver estilo e funcionalidade


Para começar a usar rapidamente um ambiente de desenvolvimento local de AEM:

1. Instalar a CLI do AEM: a CLI do AEM simplifica as tarefas de desenvolvimento. Vamos instalá-lo globalmente usando npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. Clonar o projeto do GitHub: clone o repositório de projetos do GitHub usando o comando a seguir, substituindo <owner> com o proprietário do repositório e <repo> com o nome do repositório:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. Inicie o ambiente local: navegue até o diretório do projeto e acione a instância local do AEM com um único comando:

   ```
   cd <repo>
   aem up
   ```

O bloco adaptável do Forms `blocks/form` A pasta é o seu playground para o estilo e o código de seus formulários! Editar qualquer `.css` ou `.js` nesse diretório, e você verá as alterações refletidas instantaneamente em seu navegador.

Pronto para apresentar sua criação? Use o Git para confirmar e enviar suas alterações. Isso atualiza seus ambientes de visualização e produção acessíveis nesses URLs (substitua espaços reservados pelos detalhes do projeto):

Visualizar: `https://<branch>--<repo>--<owner>.hlx.page/`
Produção: `https://<branch>--<repo>--<owner>.hlx.live/`

Parabéns! Você configurou seu ambiente de desenvolvimento local com êxito e implantou suas alterações.



## Adicionar bloco adaptável do Forms ao projeto AEM existente


>[!VIDEO](https://video.tv.adobe.com/v/3427789)

Se você tiver um projeto AEM existente, é possível integrar o Bloco de Forms adaptável ao seu projeto atual para começar a criar formulários.

>[!NOTE]
>
>
> Esta etapa se aplica a projetos criados com o [AEM Boilerplate](https://github.com/adobe/aem-boilerplate). Se você criou seu projeto AEM usando o [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms), você pode ignorar esta etapa.

Para Integrar O:

1. Clonar o repositório de blocos do Adaptive Forms: [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) ao computador.

1. Na pasta baixada, localize o `blocks/form` pasta. Copiar esta pasta. Agora, navegue até o local do seu projeto AEM `blocks` e cole a pasta de formulário copiada aqui.

1. Confirme e envie essas alterações para seu projeto AEM no GitHub.


Pronto! O bloco adaptável do Forms agora faz parte do projeto AEM. Você pode começar a criar e adicionar formulários às páginas AEM.


## Solução de problemas de build do GitHub

Verifique se o processo de criação do GitHub está descomplicado, solucionando possíveis problemas:

* **Resolver erro de caminho de módulo:**
Se você encontrar o erro &quot;Não foi possível resolver o caminho para o módulo &quot;&#39;../../scripts/lib-franklin.js&#39;&quot;, navegue até o [Projeto EDS]arquivo /blocks/forms/form.js. Atualize a instrução de importação substituindo o arquivo lib-franklin.js pelo arquivo aem.js.

* **Manipular erros de impressão:**
Caso encontre erros de impressão, você pode ignorá-los. Abra o [Projeto EDS]/package.json e modifique o script &quot;lint&quot; de `"lint": "npm run lint:js && npm run lint:css"` para `"lint": "echo 'skipping linting for now'"`. Salve o arquivo e confirme as alterações no projeto GitHub.


## Consulte também:

{{see-more-forms-eds}}
