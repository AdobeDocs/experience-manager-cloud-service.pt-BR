---
title: Introdução ao serviço de entrega de borda da AEM Forms
description: Formas perfeitas de artesanato, rápido!  criação baseada em documentos do AEM Forms Edge Delivery = velocidade incrível e formulários compatíveis com SEO para usuários e mecanismos de pesquisa mais satisfeitos.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 7b497791c70fd588b7e8c9a94caa218189d3153a
workflow-type: tm+mt
source-wordcount: '891'
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
* Clonar o [Repositório de blocos do Forms](https://github.com/adobe/afb).

  ![Introdução ao Edge Delivery Forms](/help/edge/assets/getting-started-with-eds-forms.png)


## Criar um formulário


+++ Etapa 1: adicione o bloco de formulário ao projeto do Serviço de entrega de borda (EDS).

O AEM Forms Edge Delivery inclui um bloco de formulário para ajudá-lo a criar formulários facilmente para capturar e armazenar dados capturados. Para incluir o bloco de formulário ao projeto do Serviço de entrega de borda:

1. Navegue até `[cloned Forms Block repository folder]`/blocks/.

1. Copie o `forms` pasta para `[Cloned EDS Project repository folder]\blocks` pasta.

1. Verifique a pasta &quot;formulário&quot; e os arquivos subjacentes do seu projeto do Serviço de entrega de borda no GitHub.

   ```Shell
   cd ..
   git add .
   git commit -m "Added form block"
   git push origin
   ```

   O bloco Formulário é adicionado ao projeto EDS. Agora você pode criar um formulário e adicioná-lo ao site.

   >[!NOTE]
   >
   > * Se você encontrar um erro &quot;Não foi possível resolver o caminho para o módulo &quot;&#39;../../scripts/lib-franklin.js&#39;&quot;, abra o `[EDS Project]/blocks/forms/form.js` arquivo. Na declaração de importação, substitua a variável `lib-franklin.js` arquivo com o `aem.js` arquivo.
   > * Se encontrar algum erro de impressão, sinta-se à vontade para ignorá-los. Para ignorar as verificações de listagem, abra o `[EDS Project]\package.json` arquivo e atualize o script &quot;lint&quot; de `"lint": "npm run lint:js && npm run lint:css"` para `"lint": "echo 'skipping linting for now'"`. Salve o arquivo e confirme-o no projeto GitHub.

+++

+++ Etapa 2: Criar um formulário usando o Microsoft Excel ou a Planilha do Google


Em vez de processos complexos, você pode criar facilmente um formulário usando uma planilha. Você pode começar adicionando as linhas e os cabeçalhos de coluna a uma planilha, onde cada linha define um campo de formulário e cada cabeçalho de coluna define as propriedades dos campos de formulário correspondentes.

Por exemplo, na planilha a seguir, as linhas definem os campos para uma `contact us` o cabeçalho do formulário e da coluna define as propriedades dos campos correspondentes.

![entre em contato conosco](/help/edge/assets/contact-us-form-spreadsheet.png)

Para criar um formulário:

1. Abra a pasta do projeto AEM Edge Delivery no Microsoft SharePoint ou Google Drive.

1. Crie uma Pasta de trabalho do Microsoft Excel ou uma Planilha do Google em qualquer lugar no diretório do projeto de Entrega da borda do AEM. Por exemplo, crie uma planilha chamada `contact-us` no diretório do projeto AEM Edge Delivery no Google Drive.

1. Verifique se a planilha está compartilhada com o usuário AEM (por exemplo, `helix@adobe.com`) [configurado para o seu projeto](https://www.aem.live/docs/setup-customer-sharepoint) e o usuário tem permissões de edição para a planilha.

1. Abra a planilha criada e altere o nome da planilha padrão para &quot;shared-default&quot;.

   ![renomear planilha padrão para &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-shared-default.png)

1. Para adicionar os campos do formulário, adicione as linhas e os cabeçalhos das colunas à `shared-default` planilha, onde cada linha define um campo de formulário e cada cabeçalho de coluna define o [propriedades](/help/edge/docs/forms/eds-form-field-properties)) dos campos de formulário correspondentes.

   Para iniciar rapidamente, é possível copiar o conteúdo do [entre em contato conosco](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) à sua planilha.

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar e publicar a planilha.

   ![Use o AEM Sidekick para visualizar e publicar a planilha](/help/edge/assets/preview-form.png)

   Ao visualizar e publicar, o navegador abre novas guias que exibem o conteúdo da planilha no formato JSON. Anote a URL ativa, pois ela é necessária para renderizar o formulário posteriormente.

   O formato do URL é:

   ```JSON
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

+++

+++ Etapa 3: visualizar o formulário usando a página Serviço de entrega de borda (EDS)


Até agora, você ativou o bloco de formulários do projeto EDS e preparou a estrutura do formulário. Agora, para visualizar o formulário:

1. Vá para sua conta do Microsoft SharePoint ou Google Drive e abra o diretório do projeto Delivery do AEM Edge.

1. Abra um arquivo doc para incorporar o formulário a ele. Por exemplo, abra o arquivo de índice. Você também pode criar um novo arquivo.

1. Navegue até o local desejado no documento onde deseja adicionar o formulário.

1. Adicione um bloco chamado &#39;Formulário&#39; ao arquivo, semelhante ao exibido abaixo.

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   Na segunda linha, inclua o URL anotado na seção anterior como um hiperlink. Você pode usar o URL de visualização (URL .page) ou o URL de publicação (.live). A URL de pré-visualização pode ser usada ao criar ou testar o formulário e publicar a URL para produção.

   >[!IMPORTANT]
   >
   >
   > Certifique-se de que o URL não seja mencionado como um texto simples. Ele deve ser adicionado como um hiperlink.

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar a página. A página agora exibe o formulário. Por exemplo, este é o formulário baseado na variável [entre em contato conosco](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link):


   ![Um exemplo de formulário EDS](/help/edge/assets/eds-form.png)

   Agora, preencha o formulário e clique no botão enviar, você enfrenta um erro, semelhante ao seguinte, porque a planilha ainda não está definida para aceitar os dados.

   ![erro no envio do formulário](/help/edge/assets/form-error.png)

+++


## Próxima etapa

O próximo passo é [preparar sua planilha para aceitar dados](/help/edge/docs/forms/submit-forms.md).



## Veja mais

* [Propriedades do campo de formulário](/help/edge/docs/forms/eds-form-field-properties)
* [Criar e visualizar um formulário](/help/edge/docs/forms/create-forms.md)
* [Ativar formulário para enviar dados](/help/edge/docs/forms/submit-forms.md)
* [Publicar um formulário na página de sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Adicionar validações a campos de formulário](/help/edge/docs/forms/validate-forms.md)
* [Alterar temas e estilo de formulário](/help/edge/docs/forms/style-theme-forms.md)
