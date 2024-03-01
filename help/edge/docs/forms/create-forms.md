---
title: Introdução ao Serviço de entrega de borda da AEM Forms. Crie um formulário.
description: Formas perfeitas de artesanato, rápido!  criação baseada em documentos do AEM Forms Edge Delivery = velocidade incrível e formulários compatíveis com SEO para usuários e mecanismos de pesquisa mais satisfeitos.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---


# Criar um formulário usando o bloco de formulário adaptável

Na era digital de hoje, criar formulários amigáveis é essencial para qualquer organização. O AEM Forms Edge Delivery permite criar formulários usando ferramentas familiares como o Word ou o Google Docs.

Esses formulários enviam dados diretamente para um arquivo do Microsoft Excel ou do Google Sheets, permitindo que você use um ecossistema vibrante e APIs robustas do Google Sheets, do Microsoft Excel e do Microsoft Sharepoint para processar facilmente os dados enviados ou iniciar um fluxo de trabalho de negócios existente.

O AEM Forms Edge Delivery fornece um bloco, conhecido como Bloco de formulário adaptável, para ajudar você a criar formulários facilmente para capturar e armazenar dados capturados. Você pode incluir o Bloco de formulário adaptável no projeto AEM EDS para começar a criar um formulário. Vamos começar:


## Pré-requisitos

Antes de começar, verifique se você concluiu as seguintes etapas:

* Configure o projeto GitHub do Serviço de entrega de borda (EDS) usando a placa intermediária AEM e clone o repositório GitHub correspondente no computador local. Consulte [tutorial do desenvolvedor](https://www.aem.live/developer/tutorial) para obter detalhes. Neste documento, a pasta local do projeto do Serviço de entrega de borda (EDS) é chamada de `[EDS Project repository]` .
* Verifique se você tem acesso ao Google Sheets ou ao Microsoft SharePoint. Para configurar o Microsoft SharePoint como sua fonte de conteúdo, consulte [Como usar o Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint)



## Criar um formulário

+++ Etapa 1: adicione o bloco de formulário adaptável ao projeto do Serviço de entrega de borda (EDS).

O adaptável permite que os usuários criem formulários para um site do Serviço de entrega de borda. No entanto, esse bloco não está incluído na placa-padrão do AEM (usada para criar um projeto do Serviço de entrega de borda). Para integrar facilmente o bloco de formulário adaptável ao seu projeto do Serviço de entrega de borda:

1. **Clonar o repositório de blocos do formulário adaptável**: Clone o [Repositório de blocos do formulário adaptável](https://github.com/adobe/afb) no computador local. Ele contém o código para renderizar o formulário em uma página da Web EDS. Neste documento, a pasta local do seu repositório de blocos do Forms é chamada de `[Adaptive Form block repository]`.
1. **Localize o Repositório de blocos do formulário adaptável:** Acesse o [Repositório de blocos do formulário adaptável]pasta /blocks no computador local e copiar a pasta `form` pasta.
1. **Cole o bloco do formulário adaptável no projeto EDS:**
Navegue até a [Repositório de projetos do EDS]pasta /blocks/ no computador local e cole a pasta de formulários.
1. **Confirmar alterações no GitHub:** Verifique a pasta de formulário e seus arquivos subjacentes no projeto do Serviço de entrega de borda no GitHub.

Após concluir essas etapas, o bloco de formulário adaptável foi adicionado com êxito ao repositório do projeto do Edge Delivery Service(EDS) no GitHub. Agora é possível criar e adicionar formulários a uma página de Sites de EDS.


**Solução de problemas de build do GitHub**

Verifique se o processo de criação do GitHub está descomplicado, solucionando possíveis problemas:

* **Resolver erro de caminho de módulo:**
Se você encontrar o erro &quot;Não foi possível resolver o caminho para o módulo &quot;&#39;../../scripts/lib-franklin.js&#39;&quot;, navegue até o [Projeto EDS]arquivo /blocks/forms/form.js. Atualize a instrução de importação substituindo o arquivo lib-franklin.js pelo arquivo aem.js.

* **Manipular erros de impressão:**
Caso encontre erros de impressão, você pode ignorá-los. Abra o [Projeto EDS]/package.json e modifique o script &quot;lint&quot; de &quot;lint&quot;: &quot;npm run lint:js &amp;&amp; npm run lint:css&quot; para &quot;lint&quot;: &quot;echo &#39;skipping linting for now&#39;&quot;. Salve o arquivo e confirme as alterações no projeto GitHub.



+++

+++ Etapa 2: Crie um formulário usando o Microsoft Excel ou a Planilha do Google.

Em vez de navegar por processos complexos, é possível criar um formulário sem esforço usando uma planilha. Você pode começar adicionando as linhas e os cabeçalhos de coluna a uma planilha, onde cada linha representa um campo de formulário, enquanto cada cabeçalho de coluna define as propriedades do campo correspondente.

Por exemplo, considere a seguinte planilha em que as linhas delineiam campos para uma `enquiry` os cabeçalhos de formulário e coluna definem suas propriedades:

![Planilha de consulta](/help/edge/assets/enquiry-form-spreadsheet.png)

Para continuar com a criação do formulário:

1. Acesse sua pasta do projeto AEM Edge Delivery no Microsoft SharePoint ou Google Drive.

1. Crie uma Pasta de trabalho do Microsoft Excel ou uma Planilha do Google em qualquer lugar no diretório do projeto de Entrega da borda do AEM. Por exemplo, crie uma planilha chamada `enquiry` no diretório do projeto AEM Edge Delivery no Google Drive.

1. Verifique se a planilha está compartilhada com o usuário AEM apropriado (por exemplo, `helix@adobe.com`) [de acordo com as configurações especificadas para seu projeto](https://www.aem.live/docs/setup-customer-sharepoint). Conceda ao usuário permissão de edição para a planilha.

1. Abra a planilha criada e renomeie a planilha padrão como &quot;shared-default&quot;.

   ![renomear planilha padrão para &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-shared-default.png)

1. Para adicionar os campos de formulário, insira linhas e cabeçalhos de colunas na planilha &quot;shared-default&quot;. Cada linha deve representar um [campo de formulário](/help/edge/docs/forms/form-components.md), com cabeçalhos de coluna definindo o campo correspondente [propriedades](/help/edge/docs/forms/eds-form-field-properties).

   Para um início rápido, considere copiar o conteúdo do [Planilha de consulta](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0) na planilha. Depois de copiar o conteúdo, salve sua planilha.

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar a planilha.

   ![Usar AEM Sidekick para visualizar a planilha](/help/edge/assets/preview-form.png)

   Ao visualizar, novas guias do navegador exibem o conteúdo da planilha no formato JSON. Certifique-se de capturar a URL de visualização, pois ela é necessária para renderizar o formulário no próximo da seção. O formato do URL é o seguinte:


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` refere-se à ramificação do seu repositório GitHub.
   * `<repository>` indica seu repositório GitHub.
   * `<owner>` refere-se ao nome de usuário da sua conta GitHub que hospeda o repositório GitHub.

   Por exemplo, se o repositório do seu projeto for chamado de &quot;portal&quot;, estiver localizado na conta &quot;wkndforms&quot; e você estiver usando a ramificação &quot;main&quot;, o URL será semelhante ao seguinte:

   `https://main--portal--wkndforms.hlx.page/enquiry.json`


+++

+++ Etapa 3: visualize o formulário usando a página Serviço de entrega de borda (EDS).


Até agora, você adicionou o bloco de formulário adaptável ao projeto EDS e preparou a estrutura do formulário. Agora, para visualizar o formulário:

1. **Acessar o Diretório do Projeto:** Abra sua conta do Microsoft SharePoint ou Google Drive e navegue até o diretório do projeto do Delivery de borda do AEM.

1. **Incorporar o formulário em um documento:** Abra um arquivo de documento (por exemplo, arquivo de índice) para incorporar o formulário. Como alternativa, crie um novo documento.

1. **Navegue até o local desejado:** Mova para o local desejado no documento onde você pretende adicionar o formulário.

1. **Adicionar o bloco de formulário adaptável:** Insira um bloco chamado &quot;Formulário&quot; no arquivo, conforme ilustrado abaixo:

   | Formulário |
   |---|
   | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   Esse bloco serve como um espaço reservado em que o formulário é incorporado. Na segunda linha do bloco, adicione o URL de visualização do `<form>.json` arquivo como um hiperlink.

   >[!IMPORTANT]
   >
   >
   > Verifique se o URL está formatado como um hiperlink em vez de ser exibido como texto simples.


1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar o documento. A página agora exibe o formulário. Por exemplo, este é o formulário baseado na variável [planilha de consulta](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![Um exemplo de formulário EDS](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   Agora, preencha o formulário e clique no botão enviar, você enfrenta um erro, semelhante ao seguinte, porque a planilha ainda não está definida para aceitar os dados.

   ![erro no envio do formulário](/help/edge/assets/form-error.png)

+++


## Próxima etapa

[Preparar sua planilha](/help/edge/docs/forms/submit-forms.md) para começar a aceitar dados no envio do formulário.



## Veja mais

* [Componentes de formulários](/help/edge/docs/forms/form-components.md)
* [Propriedades do campo de formulário](/help/edge/docs/forms/eds-form-field-properties)
* [Criar e visualizar um formulário](/help/edge/docs/forms/create-forms.md)
* [Ativar formulário para enviar dados](/help/edge/docs/forms/submit-forms.md)
* [Publicar um formulário na página de sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Adicionar validações a campos de formulário](/help/edge/docs/forms/validate-forms.md)
* [Alterar temas e estilo de formulário](/help/edge/docs/forms/style-theme-forms.md)
