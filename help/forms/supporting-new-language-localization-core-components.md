---
title: Como adicionar suporte para novas localidades a um formulário adaptável baseado em componentes principais?
description: Saiba como adicionar novas localidades para um Formulário adaptável.
feature: Adaptive Forms, Core Components
Role: Developer, Author
exl-id: bc06542b-84c8-4c6a-a305-effbd16d5630
role: User, Developer
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 2%

---

# Adicione uma localidade para o Forms adaptável com base nos Componentes principais {#supporting-new-locales-for-adaptive-forms-localization}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| Componentes de fundação | [Clique aqui](supporting-new-language-localization.md) |
| Componentes principais | Este artigo |

<span class="preview"> O recurso de suporte a idiomas da direita para a esquerda está disponível no programa dos primeiros usuários. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

O AEM Forms oferece suporte imediato para as localidades de inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR). Você também pode adicionar suporte para mais locais, como Hindi(hi_IN). Você também pode apresentar o Adaptive Forms em um idioma da Direita para a Esquerda (RTL), como árabe, persa e urdu, adicionando esses locais.

>[!VIDEO](https://video.tv.adobe.com/v/3433132/adaptive-forms-rtl--arabic-hebrew-farsi)

## Aplicabilidade e casos de uso

### Seguros

## O AEM Forms oferece suporte a casos de uso de seguros multilíngues?

Sim. O AEM Forms oferece suporte a experiências de formulário multilíngues, o que é importante para seguradoras que operam em regiões e idiomas.

## Como o AEM Forms determina a localidade de um formulário adaptável?

Entender como o AEM Forms seleciona o local para renderizar um Formulário adaptável é crucial para a localização adequada. Veja um detalhamento do processo de seleção:

### Seleção de localidade com base em prioridade

O AEM Forms prioriza os seguintes métodos para determinar a localidade de um Formulário adaptável:

1. **Seletor de Localidade da URL ([localidade])**:

   O sistema prioriza a localidade especificada na URL usando o seletor de [localidade]. Esse formato permite o armazenamento em cache para melhorar o desempenho.

   Formato: A URL segue este formato: http:/[URL do AEM Forms Server]/content/forms/af/[afName].[locale].html?wcmmode=disabled.

   Exemplo: https://[server]/content/forms/af/contact-us.hi.html renderiza o formulário em híndi.


1. **Parâmetro de Solicitação afAcceptLang**:

   Para substituir a localidade do navegador do usuário, você pode usar o parâmetro `afAcceptLang` na URL.

   Exemplo: https://[server]/forms/af/survey.ca-fr.html?afAcceptLang=ca-fr força o formulário a ser renderizado em francês canadense.

1. **Localidade do Navegador do Usuário (Cabeçalho Accept-Language)**:

   Se nenhuma outra localidade for especificada, a AEM Forms considerará a localidade do navegador do usuário enviada usando o cabeçalho `Accept-Language`.


### Mecanismo de fallback:


* Se uma biblioteca do cliente (processo para adicionar um novo local, explicado mais adiante neste documento) para o local solicitado não estiver disponível, o AEM Forms verificará se há uma biblioteca com base no código do idioma no local.

  Exemplo: se en_ZA (inglês da África do Sul) for solicitado e não houver uma biblioteca en_ZA, ela usará en (inglês), se disponível.

  Se nenhuma biblioteca de cliente adequada for encontrada, o dicionário padrão (principalmente `en`) para a linguagem de criação do formulário será usado.

  Na ausência de informações de local, o Formulário adaptável é exibido em seu idioma original usado durante o desenvolvimento.


## Pré-requisitos para adicionar um local

Antes de começar a adicionar um novo local para o Adaptive Forms, verifique se você tem o seguinte:

**Software:**

* Editor de texto sem formatação (IDE): embora qualquer editor de texto sem formatação possa funcionar, um IDE (Ambiente de Desenvolvimento Integrado) como o [Microsoft Visual Studio Code](https://code.visualstudio.com/download) oferece recursos avançados para facilitar a edição.

* Git: este sistema de controle de versão é necessário para gerenciar alterações de código. Se você não o instalou, baixe-o de [https://git-scm.com](https://git-scm.com).


**Repositório de Códigos:**

Clonar o repositório dos componentes principais adaptáveis do Forms: você precisa de uma biblioteca do cliente desse repositório para adicionar um local. Para clonar o repositório:

1. Abra a linha de comando ou a janela do terminal.

1. Navegue até o local desejado no computador onde deseja armazenar o repositório (por exemplo, /adaptive-forms-core-components).

1. Execute o seguinte comando para clonar o repositório:

   ```
   git clone https://github.com/adobe/aem-core-forms-components.git
   ```

   Este comando baixa o repositório e cria uma pasta chamada `aem-core-forms-components` no computador. Neste guia, nos referimos a essa pasta como `[Adaptive Forms Core Components repository]`.


## Adicionar uma localidade {#add-localization-support-for-non-supported-locales}

Para adicionar suporte a novos locais a um formulário adaptável com base em componentes principais, siga estas etapas:

### Clonar o repositório Git do AEM as a Cloud Service

1. Abra a linha de comando e escolha um diretório para armazenar seu repositório do AEM as a Cloud Service, como `/cloud-service-repository/`.

1. Execute o comando abaixo para clonar o repositório:

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<program id>/
   ```

   Para clonar o repositório Git, você precisa de algumas informações:

   * **Nome da organização**: isso identifica sua equipe ou projeto na Adobe Experience Manager as a Cloud Service (AEM as a Cloud Service).

   * **ID do programa**: especifica o programa associado ao seu repositório.

   * **Credenciais**: você precisa de um nome de usuário e senha (ou um token de acesso pessoal) para acessar o repositório com segurança.

   **Onde encontrar essas informações?**

   Para obter as instruções passo a passo sobre como localizar esses detalhes, consulte o artigo &quot;[Acessando o Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)&quot; da Adobe Experience League.

   **Seu projeto está pronto!**

   Quando o comando for concluído com sucesso, você verá uma nova pasta criada no diretório local. Essa pasta é nomeada com base no seu programa (por exemplo, id-do-programa). Esta pasta contém todos os arquivos e códigos baixados do repositório Git da AEM as a Cloud Service.

   Neste guia, nos referimos a essa pasta como `[AEMaaCS project directory]`.


### Adicionar a nova localidade ao Serviço de localização do guia

1. Abra a pasta do repositório em um editor.

   ![Pasta do repositório em um editor](/help/forms/assets/repository-folder-in-an-editor.png)

1. Localize o arquivo `Guide Localization Service.cfg.json`. Esse arquivo controla as localidades compatíveis com seu aplicativo AEM Forms. Você pode editar esse arquivo para adicionar um novo local.

   * **Arquivo existente**: se o arquivo já existir, localize-o no diretório do projeto do AEM Forms. A localização típica é:

     ```Shell
     [AEMaaCS project directory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config`. 
     ```

     Substitua `<appid>` pela ID do aplicativo específica do seu projeto. Você pode encontrar `<appid>` para seu Projeto AEM no arquivo `archetype.properties`.

     ![Propriedades do Arquétipo](/help/forms/assets/archetype-properties.png)

   * **Novo arquivo**: se o arquivo não existir, você precisará criá-lo no mesmo local mencionado acima. Não copie e cole o nome do arquivo deste documento. Em vez disso, digite manualmente o nome. O nome de arquivo `Guide Localization Service.cfg.json` inclui espaços. Isso é intencional e não um erro de digitação na documentação.

     Um arquivo de amostra com a lista de localidades com suporte para OOTB é:

     ```
         {
             "supportedLocales":[
             "en",
             "fr",
             "de",
             "ja",
             "pt-br",
             "zh-cn",
             "zh-tw",
             "ko-kr",
             "it",
             "es"
             ]
         }
     ```

1. Adicione o código de localidade do idioma desejado ao arquivo.
   1. Use a [Lista de códigos ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) para localizar o código de duas letras que representa o idioma desejado.

   1. Inclua o código de localidade no arquivo `Guide Localization Service.cfg.json`. Veja alguns exemplos:

      * Idiomas da esquerda para a direita:
         * Inglês (Estados Unidos): en-US
         * Espanhol (Espanha): es-ES
         * Francês (França): fr-FR
      * Idiomas da direita para a esquerda:
         * Árabe (Emirados Árabes Unidos): ar-ae
         * Hebraico: ele (ou iw para referência histórica)
         * Farsi: fa

1. Depois de fazer as alterações, verifique se o arquivo `Guide Localization Service.cfg.json` está formatado corretamente como um arquivo JSON válido. Erros na formatação JSON podem impedir que ela funcione corretamente. Salve o arquivo.



### Aproveite a biblioteca de exemplo do cliente para facilitar a adição de local

O AEM Forms fornece uma biblioteca de cliente de exemplo útil, `clientlib-it-custom-locale`, para simplificar a adição de novas localidades. Esta biblioteca faz parte do [Repositório dos Componentes principais do Forms Adaptive](https://github.com/adobe/aem-core-forms-components), disponível no GitHub.


Antes de começarmos, verifique se você tem uma cópia local do [Repositório dos Componentes principais do Forms Adaptive]. Caso contrário, você pode cloná-lo facilmente usando o Git com o seguinte comando:

```SHELL
git clone https://github.com/adobe/aem-core-forms-components.git
```

Esse comando baixa o repositório inteiro, incluindo a biblioteca clientlib-it-custom-locale, para um diretório chamado aem-core-forms-components na máquina.

![Diretório de repositório dos Componentes Principais do Forms Adaptive no computador local](/help/forms/assets/core-forms-components-repo-on-local-machine.png)

### Integrar a biblioteca de exemplo do cliente

Agora, vamos incorporar a biblioteca `clientlib-it-custom-locale` ao seu AEM as a Cloud Service, [diretório do projeto AEMaaCS]:

1. Localize a biblioteca de exemplo de cliente:

   Em sua cópia local do [repositório dos Componentes principais do Forms adaptável], navegue até o seguinte caminho:

   ```
       /aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs
   ```

1. Copie e cole a biblioteca:

   1. Copie a pasta `clientlib-it-custom-locale`.

      ![Copiando clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-copy.png)

   1. Navegue até o seguinte diretório no [diretório do projeto AEMaaCS]:

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib
      ```

      **Importante**: substitua `<app-id>` pela ID real do seu aplicativo.

   1. Cole a pasta `clientlib-it-custom-locale` copiada neste diretório.

      ![Colando clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-paste.png)

1. Atualizar caminho `aemLangUrl` em `languageinit.js`

   1. Navegue até o seguinte diretório no [diretório do projeto AEMaaCS]:

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib/clientlib-it-custom-locale/js
      ```

   1. Abra o arquivo `languageinit.js` no editor.
   1. Localize a seguinte linha no arquivo `languageinit.js`:

      `const aemLangUrl = /etc.clientlibs/forms-core-components-it/clientlibs/clientlib-it-custom-locale/resources/i18n/${lang}.json;`

   1. Substitua `forms-core-components-it` pela `<app-id>` (ID real do aplicativo) na linha acima.

      `const aemLangUrl = '/etc.clientlibs/<app-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/${lang}.json';`

      ![arquivo-inicialização-idioma](/help/forms/assets/language-init-name-change.png)

>[!NOTE]
>  
> Se você não substituir `forms-core-components-it` pelo nome do projeto ou `<app-id>`, o componente seletor de datas não será traduzido.

### Crie um arquivo para o novo local:

1. Navegue até o Diretório de Localidade:

   Em seu `[AEMaaCS project directory]`, navegue até o seguinte caminho:

   ```
       /ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/
   ```

   **Importante**: substitua `<program-id>` pela ID do aplicativo real.

1. Localize o arquivo de amostra no idioma inglês:

   O AEM Forms fornece um [arquivo de local em inglês de exemplo (.json) no GitHub](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json).

   O arquivo de idioma inglês inclui o conjunto padrão de cadeias de caracteres para referência. O arquivo específico de local deve imitar a estrutura do arquivo de idioma inglês.

   Para idiomas como árabe, hebraico e farsi, o texto é lido da direita para a esquerda (RTL) em vez da esquerda para a direita (LTR) como inglês. Para garantir que seus formulários sejam exibidos corretamente nesses idiomas, recomendamos usar nossos arquivos de localidade de amostra como guia. Esses arquivos fornecem uma referência sobre como formatar texto, datas e outros elementos para idiomas RTL. Você pode encontrar os arquivos de código do idioma de exemplo para:

   * [Árabe](/help/forms/assets/ar-ae.json)
   * [Hebraico](/help/forms/assets/he.json)
   * [Farsi](/help/forms/assets/fa.json)

   Ao aproveitar esses arquivos de amostra, você pode garantir que seus formulários forneçam uma experiência perfeita para usuários que trabalham em idiomas RTL.


1. Crie seu arquivo de local:

   1. Crie um novo arquivo .json no diretório `i18n`.
   1. Nomeie o arquivo usando o código de localidade apropriado para o idioma desejado (por exemplo, fr-FR.json para francês e ar-ae.json para árabe). A estrutura desse arquivo deve refletir o arquivo de localidade em inglês.


1. Estrutura e tradução:

   1. Abra o arquivo recém-criado em um editor de texto.

   1. Substitua os valores em inglês pelas traduções correspondentes para o seu idioma de destino.

   1. Depois de concluir a tradução das cadeias de caracteres, salve o arquivo.




### Adicionar suporte de localidade ao dicionário

Esta etapa se aplica somente às localidades diferentes das seguintes comumente suportadas: inglês (en), alemão (de), espanhol (es), francês (fr), italiano (it), português brasileiro (pt-br), chinês (simplificado - zh_cn), chinês (tradicional - zh_tw), japonês (ja) e coreano (ko_kr).

1. Localize a pasta de configuração:

   Navegue até o seguinte diretório no seu [diretório do projeto AEMaaCS]:

   ```
   /ui.content/src/main/content/jcr_root/etc
   ```

1. Crie as pastas necessárias (se estiverem ausentes):

   Se a pasta `etc` não existir na pasta `jcr_root`, crie-a. Dentro de `etc`, crie outra pasta chamada `languages`, se ela estiver ausente.

1. Crie o arquivo de configuração de local:

   Na pasta `languages`, crie um novo arquivo chamado `.content.xml`. Não copie e cole o nome do arquivo deste documento. Em vez disso, digite manualmente o nome.

   ![criar um novo arquivo chamado `.content.xml`](etc-content-xml.png)

   Abra este arquivo e cole o conteúdo a seguir, substituindo [LOCALE_CODE] pelo código de localidade real (Por exemplo, ar-ae para Árabe).


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
         jcr:primaryType="nt:unstructured"
         languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

   AVISO: não substitua a lista existente. Em vez disso, anexe o novo código de localidade entre colchetes, separados por vírgulas, desta forma (usando ar-ae como exemplo):

   ```XML
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi,ar-ae]"
   ```

1. Incluir as Novas Pastas em filter.xml:

   Navegue até o arquivo `/ui.content/src/main/content/meta-inf/vault/filter.xml` no seu [diretório do projeto AEMaaCS].

   Abra o arquivo e adicione a seguinte linha no final:

   ```
   <filter root="/etc/languages"/>
   ```

   ![Adicionar as pastas criadas em `filter.xml` em `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)

1. Salve o arquivo.

### Implante a localidade recém-criada no ambiente do AEM

Agora você está pronto para usar o novo local com sua Forms adaptável. Você pode

* Implante o AEM as a Cloud Service, [diretório do projeto AEMaaCS], no ambiente de desenvolvimento local para experimentar a nova configuração de localidade no computador local. Para implantar no ambiente de desenvolvimento local:

   1. Certifique-se de que o ambiente de desenvolvimento local esteja em funcionamento. Se você ainda não tiver configurado um ambiente de desenvolvimento local, consulte o manual em [Configurar ambiente de desenvolvimento local para o AEM Forms](/help/forms/setup-local-development-environment.md).

   1. Abra a janela do terminal ou o prompt de comando.

   1. Navegue até o [diretório do projeto AEMaaCS]

   1. Execute o seguinte comando:

      ```
      mvn -PautoInstallPackage clean install
      ```

* Implante o AEM as a Cloud Service, [diretório do projeto AEMaaCS], no seu ambiente Cloud Service. Para implantar no ambiente do Cloud Service:

   1. Confirme suas alterações:

      Depois de adicionar a nova configuração de localidade, confirme suas alterações com uma mensagem clara do Git descrevendo a adição da localidade (Por exemplo, &quot;Adicionado suporte para [Nome da localidade]&quot;).

   1. Implante o código atualizado:

      Acione uma implantação do seu código por meio do [pipeline de pilha completa existente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline). Isso cria e implanta automaticamente o código atualizado com o novo suporte de localidade.

      Se você ainda não tiver configurado um pipeline, consulte o manual sobre [como configurar um pipeline para o AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline).


## Visualizar um formulário adaptável com a localidade recém-adicionada

Essas etapas orientam você na pré-visualização de um Formulário adaptável com a localidade recém-adicionada:

1. Faça logon na sua instância do AEM Forms as a Cloud Service.
1. Ir para **Forms** > **Forms e Documentos**.
1. Selecione um formulário adaptável e clique em **Adicionar dicionário** e o assistente **Adicionar dicionário ao projeto de tradução** será exibido.
1. Especifique o **Título do Projeto** e selecione os **Idiomas de Destino** no menu suspenso do assistente **Adicionar Dicionário ao Projeto de Tradução**.
1. Clique em **Concluído** e execute o projeto de tradução criado.
1. Ir para **Forms** > **Forms e Documentos**.
1. Selecione o Formulário adaptável e escolha a opção **Visualizar como HTML**.
1. Anexe `&afAcceptLang=<locale-name>` à URL de visualização e pressione a tecla Return. Substitua `<locale-name>` pelo seu código de localidade atual. O formulário adaptável é exibido no local especificado.

## Práticas recomendadas para oferecer suporte à nova localização {#best-practices}

* A Adobe recomenda criar um projeto de tradução após criar um Formulário adaptável. Isso simplifica o processo de localização.
* Quando os componentes Caixa numérica e Seletor de data são convertidos em um local específico, podem ocorrer problemas de formatação. Para atenuar isso, uma opção **Idioma** foi incorporada à caixa de diálogo Configurar do [componente seletor de datas](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker#format-tab) e do [componente Caixa Numérica](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/numeric-box#formats-configure-tab).


* Tratamento de novos campos:

   * **Tradução Automática**: se estiver usando tradução automática, você precisará recriar o dicionário e executar novamente o projeto de tradução[ depois de adicionar novos campos a um Formulário Adaptável existente. ](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md) Os novos campos adicionados após o projeto de tradução inicial permanecem não traduzidos.

   * **Tradução humana**: para fluxos de trabalho de tradução humana, exporte o dicionário usando a interface do usuário em `[AEM Forms Server]/libs/cq/i18n/gui/translator.html`. Atualize o dicionário para os novos campos e faça upload da versão revisada.


## Consulte também {#see-also}

{{see-also}}

* [Gerar documento de registro para Forms adaptável](/help/forms/generate-document-of-record-core-components.md)
* [Adição de um formulário adaptável a uma página do AEM Sites ou a um fragmento de experiência](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

