---
title: Adicionar suporte para novas localidades a um formulário adaptável
seo-title: Learn to add support for new locales to your adaptive forms
description: O AEM Forms permite adicionar novas localidades para localizar formulários adaptáveis. Inglês (en), Espanhol (es), Francês (fr), Italiano (it), Alemão (de), Japonês (ja), Português-Brasileiro (pt-BR), Chinês (zh-CN), Chinês-Taiwan (zh-TW) e Coreano (ko-KR).
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. We support 10 locales out of the box curently, as  "en","fr","de","ja","pt-br","zh-cn","zh-tw","ko-kr","it","es".
source-git-commit: 00fcdb3530a441bde2f7f91515aaaec341615a3f
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Suporte a novas localidades para a localização do Adaptive Forms {#supporting-new-locales-for-adaptive-forms-localization}

A AEM Forms fornece suporte pronto para uso para localidades Inglês (en), Espanhol (es), Francês (fr), Italiano (it), Alemão (de), Japonês (ja), Português-Brasileiro (pt-BR), Chinês (zh-CN), Chinês-Taiwan (zh-TW) e Coreano (KKR). Você também pode adicionar suporte para mais localidades, como Hindi(hi_IN).

## Como entender dicionários de localidades {#about-locale-dictionaries}

A localização de formulários adaptáveis depende de dois tipos de dicionários de localidade:

* **Dicionário específico do formulário** Contém strings usadas em formulários adaptáveis. Por exemplo, rótulos, nomes de campo, mensagens de erro, descrições de ajuda. Ele é gerenciado como um conjunto de arquivos XLIFF para cada localidade e você pode acessá-lo em `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **Dicionários globais** Há dois dicionários globais, gerenciados como objetos JSON, em AEM biblioteca do cliente. Esses dicionários contêm mensagens de erro padrão, nomes de mês, símbolos de moeda, padrões de data e hora e assim por diante. Você pode encontrar esses dicionários em `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. Esses locais contêm pastas separadas para cada localidade. Como os dicionários globais não são atualizados com frequência, manter arquivos JavaScript separados para cada localidade permite que os navegadores os armazenem em cache e reduzam o uso da largura de banda da rede ao acessar diferentes formulários adaptáveis no mesmo servidor.

## Adicionar suporte para novas localidades {#add-support-for-new-locales}

Siga as etapas abaixo para adicionar suporte a uma nova localidade:

1. [Adicionar suporte de localização para localidades não suportadas](#add-localization-support-for-non-supported-locales)
1. [Usar localidades adicionadas no Adaptive Forms](#use-added-locale-in-af)

### Adicionar suporte de localização para localidades não suportadas {#add-localization-support-for-non-supported-locales}

Atualmente, o AEM Forms oferece suporte para a localização do conteúdo do Adaptive Forms em inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR).

Para adicionar suporte para um novo local no tempo de execução do Adaptive Forms:

1. [Clonar o repositório](#clone-the-repository)
1. [Adicionar uma localidade ao serviço GuideLocalizationService](#add-a-locale-to-the-guide-localization-service)
1. [Adicionar pasta específica do nome da localidade](#add-locale-name-specific-folder)
1. [Adicionar suporte de local ao dicionário](#add-locale-support-for-the-dictionary)
1. [Confirme as alterações no repositório e implante o pipeline](#commit-changes-in-repo-deploy-pipeline)

#### 1. Clonar o repositório {#clone-the-repository}

1. Na linha de comando, navegue até o local em que deseja clonar o repositório do Forms Cloud Service.
1. Execute o comando que você [recuperado do Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) É semelhante a `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. Use o nome de usuário e a senha do git para clonar o repositório.
1. Abra a pasta do repositório do Forms Cloud Service no editor preferencial.

#### 2. Adicione um local ao serviço de localização do Guia {#add-a-locale-to-the-guide-localization-service}

1. Localize a variável `Guide Localization Service.cfg.json` e adicione a localidade que deseja adicionar à lista de localidades suportadas.

   >[!NOTE]
   >
   > Crie um arquivo com o nome como `Guide Localization Service.cfg.json` , se já não estiver presente.

#### 3. Adicionar biblioteca cliente de pasta específica do nome da localidade {#add-locale-name-specific-folder}

1. Na pasta UI.content, crie `etc/clientlibs` pasta.
1. Crie uma pasta chamada como `locale-name` under `etc/clientlibs` para servir como container para xfa e af clientlibs.

##### 3.1 Adicionar biblioteca do cliente XFA para um local na pasta de nome do local

Criar um nó chamado como `[locale-name]_xfa` e digite como `cq:ClientLibraryFolder` under `etc/clientlibs/locale_name`, com categoria `xfaforms.I18N.<locale>`e adicione os seguintes arquivos:

* **I18N.js** definição `xfalib.locale.Strings` para `<locale>` conforme definido em `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt** Contendo o seguinte:
   */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2. Adicionar a biblioteca do cliente de Formulário adaptável para uma pasta de nome de localidade

1. Criar um nó chamado como `[locale-name]_af` e digite como `cq:ClientLibraryFolder` under `etc/clientlibs/locale_name`, com categoria como `guides.I18N.<locale>` e dependências como `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`.
1. Crie uma pasta chamada como `javascript` e adicione os seguintes arquivos:

   * **i18n.js** definição `guidelib.i18n`, com padrões de &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` para `<locale>` de acordo com as especificações XFA descritas em [Especificação do conjunto de localidades](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **LogMessages.js** definição `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` para `<locale>` conforme definido em `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. Adicionar **js.txt** Contendo o seguinte:

   ```
     i18n.js
     LogMessages.js
   ```

#### 4. Adicionar suporte de local ao dicionário {#add-locale-support-for-the-dictionary}

Execute esta etapa somente se a variável `<locale>` você está adicionando que não está entre `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Criar uma pasta `languages` under `etc`, se ainda não estiver presente.

1. Adicionar uma propriedade de string com vários valores `languages` ao nó , se ainda não estiver presente.
1. Adicione o `<locale-name>` valores de localidade padrão `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, se ainda não estiver presente.

1. Adicione o `<locale>` aos valores da `languages` propriedade de `/etc/languages`.
1. Adicione as pastas recém-criadas na `filter.xml` em etc/META-INF/[hierarquia de pastas] como:

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

Antes de confirmar as alterações no repositório Git do AEM, é necessário acessar o [Informações do repositório Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

#### 5. Confirme as alterações no repositório e implante o pipeline {#commit-changes-in-repo-deploy-pipeline}

Confirme as alterações no repositório GIT após adicionar um novo suporte de local. Implante seu código usando o pipeline de pilha completo. Saiba mais [como configurar um pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) para adicionar novo suporte à localidade.
Quando o pipeline estiver concluído, a localidade recém-adicionada aparecerá no ambiente de AEM.

### Usar localidade adicionada no Adaptive Forms {#use-added-locale-in-af}

Execute as seguintes etapas para usar e renderizar um formulário adaptável usando um local recém-adicionado:

1. Faça logon na instância do autor do AEM.
1. Ir para **Forms** >  **Forms e documentos**.
1. Selecione um formulário adaptável e clique em **Adicionar dicionário** e **Adicionar dicionário ao projeto de tradução** é exibido.
1. Especifique a **Título do projeto** e selecione o **Idiomas de destino** no menu suspenso no **Adicionar dicionário ao projeto de tradução** assistente.
1. Clique em **Concluído** e executar o projeto de tradução criado.
1. Selecione um formulário adaptável e clique em **Visualizar como HTML**.
1. Adicionar `&afAcceptLang=<locale-name>` no URL de um formulário adaptável.
1. Atualize a página e o Formulário adaptativo é renderizado em um local especificado.

Há dois métodos para identificar a localidade de um formulário adaptável. Quando um formulário adaptável é renderizado, ele identifica a localidade solicitada ao:

* Recuperação de `[local]` no URL do formulário adaptável. O formato do URL é `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Usando `[local]` permite armazenar em cache um formulário adaptável.

* Recuperando os seguintes parâmetros na ordem listada:

   * Parâmetro de solicitação `afAcceptLang`
Para substituir a localidade do navegador de usuários, você pode passar a variável 
`afAcceptLang` solicitar parâmetro para forçar a localidade. Por exemplo, o URL a seguir força a renderização do formulário na localidade franco-canadense:
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * A localidade do navegador definida para o usuário, que é especificada na solicitação usando o `Accept-Language` cabeçalho.

Se uma biblioteca do cliente para o local solicitado não existir, ela verificará se há uma biblioteca do cliente para o código de idioma presente no local. Por exemplo, se a localidade solicitada for `en_ZA` (inglês da África do Sul) e a biblioteca do cliente para `en_ZA` não existe, o formulário adaptável usa a biblioteca do cliente para `en` (Inglês), se existir. No entanto, se nenhum deles existir, o formulário adaptável usará o dicionário para `en` localidade.


Depois que a localidade é identificada, o Formulário adaptável escolhe o dicionário específico do formulário. Se o dicionário específico do formulário para a localidade solicitada não for encontrado, ele usará o dicionário para o idioma em que o formulário adaptável foi criado.

Se nenhuma informação de local estiver presente, o Formulário adaptável será fornecido no idioma original do formulário. O idioma original é o idioma usado durante o desenvolvimento do formulário adaptável.

Get [exemplo de biblioteca do cliente](/help/forms/assets/locale-support-sample.zip) para adicionar suporte a novo local. Você precisa alterar o conteúdo da pasta no local desejado.

## Práticas recomendadas para oferecer suporte à nova localização {#best-practices}

* O Adobe recomenda criar um projeto de tradução após a criação de um Formulário adaptável.

* Quando novos campos são adicionados em um Formulário adaptável existente:
   * **Para tradução automática**: Recrie o dicionário e execute o projeto de tradução. Os campos adicionados a um formulário adaptável após a criação de um projeto de tradução permanecem sem tradução.
   * **Para tradução humana**: Exporte o dicionário por `[server:port]/libs/cq/i18n/gui/translator.html`. Atualize o dicionário dos campos recém-adicionados e faça upload dele.
