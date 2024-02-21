---
title: Introdução ao serviço de entrega de borda da AEM Forms
description: Formas perfeitas de artesanato, rápido!  criação baseada em documentos do AEM Forms Edge Delivery = velocidade incrível e formulários compatíveis com SEO para usuários e mecanismos de pesquisa mais satisfeitos.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: f37a99cd5cbfb745cb591e3be2a46a5f52139cb2
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Criar um formulário no Serviço de entrega de borda do AEM Forms

Na era digital de hoje, criar formulários amigáveis é essencial para qualquer organização. O AEM Forms Edge Delivery permite criar formulários usando ferramentas familiares como o Word ou o Google Docs.

Esses formulários enviam dados diretamente para um arquivo do Microsoft Excel ou do Google Sheets, permitindo que você use um ecossistema vibrante e APIs robustas do Google Sheets, do Microsoft Excel e do Microsoft Sharepoint para processar facilmente os dados enviados ou iniciar um fluxo de trabalho de negócios existente.

## Pré-requisitos

* Você tem uma conta do GitHub.
* Você tem acesso ao Google Sheets ou ao Microsoft SharePoint.
* Você entende as noções básicas de Git, HTML, CSS e JavaScript.
* Você tem o Nó e o NPM instalados para desenvolvimento local.

## Antes de começar

* Configure e clone seu projeto do Serviço de entrega de borda (EDS). Consulte [tutorial do desenvolvedor](https://www.aem.live/developer/tutorial) para obter detalhes.
* Clonar o [Repositório de blocos do Forms](https://github.com/adobe/afb). Inclui o bloco Form necessário para renderizar o formulário.

![Introdução ao Edge Delivery Forms](/help/edge/assets/getting-started-with-eds-forms.png)

## Adicionar o bloco de formulário ao projeto do Edge Delivery Service (EDS) {#add-forms-block-to-an-eds-project}

O AEM Forms Edge Delivery inclui um bloco de formulário para ajudá-lo a criar formulários facilmente para capturar e armazenar dados capturados. Para incluir o bloco de formulário ao projeto do Serviço de entrega de borda:

1. Navegue até a pasta do projeto do Serviço de entrega de borda (EDS) no ambiente de desenvolvimento local.


   ```Shell
   cd [EDS Project folder]
   ```

1. Crie uma pasta chamada `form` no diretório de projeto EDS. Por exemplo, no diretório do projeto EDS chamado `Portal`, crie uma pasta chamada `form`.

   ```Shell
   mkdir form
   ```


1. Adicione o [Bloco do Forms](https://github.com/adobe/afb/tree/main/blocks/form) para a pasta &#39;formulário&#39;.

   ```shell
   cp -R <source:path of the form block> <destination: path of the form folder created in the previous step>
   
   For example
   
   cp -R Documents/afb/blocks/form Documents/portal/blocks/
   ```

1. Faça check-in da pasta &quot;formulário&quot; e dos arquivos subjacentes no seu projeto do Serviço de entrega de borda no GitHub.

   ```Shell
   git add .
   git commit -m "Added form block"
   git push origin
   ```

   Agora você está pronto para renderizar um formulário EDS.

   >[!NOTE]
   >
   > * Se a criação do projeto de solicitação de pull/eds falhar e você encontrar um erro relacionado à importação do `franklin-lib.js` arquivo, atualize a declaração de importação para fazer referência à `aem.js` arquivo em vez de `franklin-lib.js` arquivo.
   > * Se encontrar algum erro de impressão, sinta-se à vontade para ignorá-los. Para ignorar as verificações de lista, navegue até o arquivo package.json e atualize o script &quot;lint&quot; de `"lint": "npm run lint:js && npm run lint:css"` para `"lint": "echo 'skipping linting for now'"`. Em seguida, confirme as alterações no arquivo package.json.

## Criar um formulário usando o Microsoft Excel ou o Google Sheet {#create-a-form-for-an-eds-project}

Permitir que os desenvolvedores de site criem formulários e escolham quais informações coletar dos visitantes do site pode ser útil. Em vez de processos complexos, os autores podem configurar facilmente um formulário usando uma planilha. Eles precisam adicionar os cabeçalhos de coluna corretos e, em seguida, usar um bloco de formulário para exibi-lo no site sem qualquer problema. Para criar um formulário:

1. Crie uma Pasta de trabalho do Microsoft Excel ou uma Planilha do Google em qualquer lugar no diretório do projeto de Entrega da borda do AEM no Microsoft SharePoint ou no Google Drive.

1. Verifique se o usuário AEM (por exemplo, `helix@adobe.com`) configurado para seu projeto tem permissões de edição para a planilha.

1. Abra a pasta de trabalho que você criou e altere o nome da planilha padrão para &quot;shared-default&quot;.

   ![renomear planilha padrão para &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-helix-default.png)

1. Copie o conteúdo de [entre em contato conosco](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) para sua própria planilha.

   ![entre em contato conosco](/help/edge/assets/contact-us-form-spreadsheet.png)

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar e publicar a planilha.

   Ao visualizar e publicar, o navegador abre novas guias que exibem o conteúdo da planilha no formato JSON. Anote a URL ativa, pois ela é necessária para renderizar o formulário posteriormente.

   O formato do URL é:

   ```shell
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

## Pré-visualize o formulário usando a página Serviço de entrega de borda (EDS) {#add-a-form-to-your-eds-page}

Até agora, você ativou o bloco de formulários do projeto EDS e preparou a estrutura do formulário. Agora, para incluir o formulário na sua página de EDS e renderizá-lo:

1. Vá para o diretório do projeto AEM Edge Delivery no Microsoft SharePoint ou Google Drive.

1. Para adicionar o formulário a uma página, abra o arquivo de documento correspondente. Por exemplo, abra o arquivo de índice.

1. Navegue até o local desejado no documento onde deseja adicionar o formulário.

1. Adicione um bloco chamado &#39;Formulário&#39; ao arquivo, semelhante ao exibido abaixo.

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   Na segunda linha, inclua o URL anotado na seção anterior como um hiperlink.

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar e publicar a página. O formulário é renderizado.

   Por exemplo, este é o formulário baseado na variável [entre em contato conosco](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link):


   ![fale conosco (formulário EDS)](/help/edge/assets/eds-form.png)

   O bloco de formulário renderiza o formulário, mas ainda não está pronto para aceitar os dados. Ao clicar no botão enviar, ocorre um erro semelhante ao seguinte:

   ![erro no envio do formulário](/help/edge/assets/form-error.png)

   [Preparar sua planilha para aceitar os dados](/help/edge/docs/forms/submit-forms.md). Você pode enviar os dados para a publicação da folha preparando-a para aceitar os dados.


## Veja mais

* [Criar e visualizar um formulário](/help/edge/docs/forms/create-forms.md)
* [Ativar formulário para enviar dados](/help/edge/docs/forms/submit-forms.md)
* [Publicar um formulário na página de sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Adicionar validações a campos de formulário](/help/edge/docs/forms/validate-forms.md)
* [Alterar temas e estilo de formulário](/help/edge/docs/forms/style-theme-forms.md)