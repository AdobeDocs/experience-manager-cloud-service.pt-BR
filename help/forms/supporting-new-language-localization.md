---
title: Adicionar compatibilidade a novas localidades a um Formulário adaptável
seo-title: Learn to add support for new locales to your adaptive forms
description: O AEM Forms permite adicionar novas localidades para localizar formulários adaptáveis. Locais de inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR).
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. We support 10 locales out of the box curently, as  "en","fr","de","ja","pt-br","zh-cn","zh-tw","ko-kr","it","es".
exl-id: 4c7d6caa-1adb-4663-933f-b09129b9baef
source-git-commit: ca0c9f102488c38dbe8c969b54be7404748cbc00
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 1%

---

# Suporte a novos locais para a localização adaptável do Forms {#supporting-new-locales-for-adaptive-forms-localization}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-br) para [criação de um novo Forms adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/supporting-new-language-localization.html) |
| AEM as a Cloud Service | Este artigo |

O AEM Forms oferece suporte imediato para as localidades de inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR). Você também pode adicionar suporte para mais locais, como Hindi(hi_IN).

## Compreender dicionários de localidade {#about-locale-dictionaries}

A localização de formulários adaptáveis depende de dois tipos de dicionários de localidade:

* **Dicionário específico de formulário** Contém strings usadas em formulários adaptáveis. Por exemplo, rótulos, nomes de campos, mensagens de erro, descrições da ajuda. Ele é gerenciado como um conjunto de arquivos XLIFF para cada local e você pode acessá-lo em `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **Dicionários globais** Há dois dicionários globais, gerenciados como objetos JSON, na biblioteca do cliente AEM. Esses dicionários contêm mensagens de erro padrão, nomes de meses, símbolos de moeda, padrões de data e hora e assim por diante. Você pode encontrar esses dicionários em `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. Esses locais contêm pastas separadas para cada local. Como os dicionários globais não são atualizados com frequência, manter arquivos JavaScript separados para cada localidade permite que os navegadores os armazenem em cache e reduzam o uso da largura de banda da rede ao acessar diferentes formulários adaptáveis no mesmo servidor.

## Adicionar suporte para novas localidades {#add-support-for-new-locales}

Execute o seguinte para adicionar suporte a uma nova localidade:

1. [Adicionar suporte de localização para localidades sem suporte](#add-localization-support-for-non-supported-locales)
1. [Usar localidades adicionadas no Adaptive Forms](#use-added-locale-in-af)

### Adicionar suporte de localização para localidades sem suporte {#add-localization-support-for-non-supported-locales}

Atualmente, o AEM Forms oferece suporte à localização de conteúdo do Adaptive Forms em inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR).

Para adicionar suporte para um novo local no tempo de execução do Adaptive Forms:

1. [Clonar seu repositório](#clone-the-repository)
1. [Adicionar uma localidade ao serviço GuideLocalizationService](#add-a-locale-to-the-guide-localization-service)
1. [Adicionar pasta específica do nome da localidade](#add-locale-name-specific-folder)
1. [Adicionar suporte de localidade para o dicionário](#add-locale-support-for-the-dictionary)
1. [Confirmar as alterações no repositório e implantar o pipeline](#commit-changes-in-repo-deploy-pipeline)

#### 1. Clonar o repositório {#clone-the-repository}

1. Na linha de comando, navegue até o local em que deseja clonar o repositório Cloud Service do Forms.
1. Execute o comando que [recuperado do Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) É semelhante a `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. Use o nome de usuário e a senha do Git para clonar o repositório.
1. Abra a pasta clonada do repositório de Cloud Service do Forms no editor de sua preferência.

#### 2. Adicionar um local ao serviço de Localização do Guia {#add-a-locale-to-the-guide-localization-service}

1. Localize o `Guide Localization Service.cfg.json` e adicione o local que deseja adicionar à lista de locais suportados.

   >[!NOTE]
   >
   > Crie um arquivo com o nome como `Guide Localization Service.cfg.json` arquivo, se já não estiver presente.

#### 3. Adicionar biblioteca de cliente de pasta específica de nome de localidade {#add-locale-name-specific-folder}

1. Na pasta UI.content, crie `etc/clientlibs` pasta.
1. Além disso, crie uma pasta chamada como `locale-name` em `etc/clientlibs` para servir como contêiner de clientlibs xfa e af.

##### 3.1 Adicionar biblioteca do cliente XFA para um local na pasta de nome do local

Criar um nó chamado como `[locale-name]_xfa` e digite como `cq:ClientLibraryFolder` em `etc/clientlibs/locale_name`, com categoria `xfaforms.I18N.<locale>`e adicione os seguintes arquivos:

* **I18N.js** definindo `xfalib.locale.Strings` para o `<locale>` conforme definido em `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt** contendo o seguinte:
  */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2. Adicionar biblioteca do cliente Formulário adaptável para uma pasta de nome de localidade

1. Criar um nó chamado como `[locale-name]_af` e digite como `cq:ClientLibraryFolder` em `etc/clientlibs/locale_name`, com a categoria como `guides.I18N.<locale>` e dependências como `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`.
1. Criar uma pasta chamada como `javascript` e adicione os seguintes arquivos:

   * **i18n.js** definindo `guidelib.i18n`, com padrões de &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` para o `<locale>` de acordo com as especificações XFA descritas em [Especificação do conjunto de localidades](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **LogMessages.js** definindo `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` para o `<locale>` conforme definido em `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. Adicionar **js.txt** contendo o seguinte:

   ```
     i18n.js
     LogMessages.js
   ```

#### 4. Adicionar suporte local ao dicionário {#add-locale-support-for-the-dictionary}

Execute esta etapa somente se a variável `<locale>` você está adicionando não está entre `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Criar uma pasta `languages` em `etc`, se ainda não estiver presente.

1. Adicionar uma propriedade de cadeia de caracteres de vários valores `languages` ao nó, se ainda não estiver presente.
1. Adicione o `<locale-name>` valores de localidade padrão `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, se ainda não estiver presente.

1. Adicione o `<locale>` aos valores de `languages` propriedade de `/etc/languages`.
1. Adicione as pastas recém-criadas na `filter.xml` em etc/META-INF/[hierarquia de pastas] como:

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

Antes de confirmar as alterações no repositório Git do AEM, é necessário acessar [Informações do repositório Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

#### 5. Confirme as alterações no repositório e implante o pipeline {#commit-changes-in-repo-deploy-pipeline}

Confirme as alterações no repositório GIT após adicionar um novo suporte de localidade. Implante seu código usando o pipeline de pilha completa. Saiba mais [como configurar um pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) para adicionar novo suporte de local.
Quando o pipeline estiver concluído, o local recém-adicionado aparecerá no ambiente AEM.

### Usar local adicionado no Adaptive Forms {#use-added-locale-in-af}

Execute as seguintes etapas para usar e renderizar um Formulário adaptável usando um local recém-adicionado:

1. Faça logon na instância de autor do AEM.
1. Ir para **Forms** >  **Forms e documentos**.
1. Selecione um Formulário adaptável e clique em **Adicionar dicionário** e **Adicionar Dicionário Ao Projeto De Tradução** é exibido.
1. Especifique a **Título do projeto** e selecione o **Idiomas de destino** no menu suspenso da caixa **Adicionar Dicionário Ao Projeto De Tradução** assistente.
1. Clique em **Concluído** e execute o projeto de tradução criado.
1. Selecione um Formulário adaptável e clique em **Visualizar como HTML**.
1. Adicionar `&afAcceptLang=<locale-name>` no URL de um Formulário adaptável.
1. Atualizar a página e o Formulário adaptável é renderizado em um local especificado.

Há dois métodos para identificar o local de um Formulário adaptável. Quando um formulário adaptável é renderizado, ele identifica o local solicitado por:

* Recuperação de `[local]` no URL do formulário adaptável. O formato do URL é `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Usar `[local]` O seletor permite armazenar em cache um Formulário adaptável.

* Recuperação dos seguintes parâmetros na ordem listada:

   * Parâmetro de solicitação `afAcceptLang`
Para substituir a localidade do navegador dos usuários, você pode transmitir a `afAcceptLang` parâmetro de solicitação para forçar a localidade. Por exemplo, a URL a seguir força a renderização do formulário na localidade canadense-francesa:
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * A localidade do navegador definida para o usuário, que é especificada na solicitação usando o `Accept-Language` cabeçalho.

Se não existir uma biblioteca do cliente para a localidade solicitada, ela verificará se há uma biblioteca do cliente para o código de idioma presente na localidade. Por exemplo, se o local solicitado for `en_ZA` (inglês da África do Sul) e a biblioteca do cliente para `en_ZA` não existir, o formulário adaptável usará a biblioteca do cliente para `en` Idioma (inglês), se existir. No entanto, se nenhum deles existir, o Formulário adaptável usará o dicionário para `en` localidade.


Depois que a localidade é identificada, o Formulário adaptável escolhe o dicionário específico do formulário. Se o dicionário específico do formulário para a localidade solicitada não for encontrado, ele usará o dicionário do idioma no qual o Formulário adaptável foi criado.

Se nenhuma informação de local estiver presente, o Formulário adaptável será fornecido no idioma original do formulário. O idioma original é o idioma usado ao desenvolver o Formulário adaptável.

Obter [biblioteca cliente de exemplo](/help/forms/assets/locale-support-sample.zip) para adicionar suporte ao novo local. É necessário alterar o conteúdo da pasta no local necessário.

## Práticas recomendadas para oferecer suporte à nova localização {#best-practices}

* O Adobe recomenda criar um projeto de tradução após criar um Formulário adaptável.

* Quando novos campos são adicionados em um Formulário adaptável existente:
   * **Para tradução automática**: recrie o dicionário e execute o projeto de tradução. Os campos adicionados a um Formulário adaptável após a criação de um projeto de tradução permanecem não traduzidos.
   * **Para tradução humana**: Exportar o dicionário através do `[server:port]/libs/cq/i18n/gui/translator.html`. Atualize o dicionário para os campos recém-adicionados e faça upload dele.
