---
title: Adicionar compatibilidade a novas localidades a um Formulário adaptável
description: O AEM Forms permite adicionar novas localidades para localizar formulários adaptáveis. Locais de inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR).
exl-id: 4c7d6caa-1adb-4663-933f-b09129b9baef
source-git-commit: 9a1bb716256b5e820723911f4e78a6a4c69d940c
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 1%

---

# Adicione uma localidade para o Forms adaptável com base nos Componentes principais {#supporting-new-locales-for-adaptive-forms-localization}


| Versão | Link do artigo |
| -------- | ---------------------------- |
| Componentes de base | [Clique aqui](supporting-new-language-localization.md) |
| Componentes principais | Este artigo |

O AEM Forms oferece suporte imediato para as localidades de inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR). Você também pode adicionar suporte para mais locais, como Hindi(hi_IN).

## Compreender dicionários de localidade {#about-locale-dictionaries}

A localização de formulários adaptáveis depende de dois tipos de dicionários de localidade:

* **Dicionário específico de formulário** Contém strings usadas em formulários adaptáveis. Por exemplo, rótulos, nomes de campos, mensagens de erro, descrições da ajuda. Ele é gerenciado como um conjunto de arquivos XLIFF para cada local e você pode acessá-lo em `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **Dicionários globais** Há dois dicionários globais, gerenciados como objetos JSON, na biblioteca do cliente AEM. Esses dicionários contêm mensagens de erro padrão, nomes de meses, símbolos de moeda, padrões de data e hora e assim por diante. Você pode encontrar esses dicionários em `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. Esses locais contêm pastas separadas para cada local. Como os dicionários globais não são atualizados com frequência, manter arquivos JavaScript separados para cada localidade permite que os navegadores os armazenem em cache e reduzam o uso da largura de banda da rede ao acessar diferentes formulários adaptáveis no mesmo servidor.

## Pré-requisitos {#prerequistes}

Antes de começar a adicionar suporte para um novo local,

* Instale um editor de texto simples (IDE) para facilitar a edição. Os exemplos neste documento são baseados no Microsoft VS Code.
* Clonar o repositório dos Componentes principais adaptáveis do Forms. Para clonar o repositório:
   1. Abra a linha de comando ou a janela de terminal e navegue até um local para armazenar o repositório. Por exemplo `/adaptive-forms-core-components`
   1. Execute o seguinte comando para clonar o repositório:

      ```SHELL
          git clone https://github.com/adobe/aem-core-forms-components.git
      ```

  O repositório inclui uma biblioteca do cliente necessária para adicionar um local.


## Adicionar uma localidade {#add-localization-support-for-non-supported-locales}

Atualmente, o AEM Forms oferece suporte à localização de conteúdo do Adaptive Forms em inglês (en), espanhol (es), francês (fr), italiano (it), alemão (de), japonês (ja), português-brasileiro (pt-BR), chinês (zh-CN), chinês-Taiwan (zh-TW) e coreano (ko-KR). Para adicionar suporte para um novo local no tempo de execução do Adaptive Forms, siga estas etapas:

![Adicionar um local a um repositório](add-a-locale-adaptive-form-core-components.png)

### 1. Clonar o repositório Git as a Cloud Service do AEM {#clone-the-repository}

1. Abra a linha de comando e escolha um diretório para armazenar o repositório, como `/cloud-service-repository/`.

1. Execute o seguinte comando para clonar o repositório:

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/
   ```

   Substituir `<my-org>` e `<my-program>` no URL acima, com o nome da organização e o nome do programa. Para obter instruções detalhadas sobre como obter o nome da organização, o nome do programa ou o caminho completo do repositório Git e as credenciais necessárias para cloná-lo, consulte a [Acesso ao Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) artigo.

   Após a conclusão bem-sucedida do comando, uma pasta `<my-program>` é criado. Ele contém o conteúdo clonado do repositório Git. No restante do artigo, a pasta é chamada de, `[AEM Forms as a Cloud Service Git repostory]`.


### 2. Adicione o novo local ao Serviço de localização do guia {#add-a-locale-to-the-guide-localization-service}

1. Abra a pasta do repositório, clonada na seção anterior, em um editor de texto simples.
1. Navegue até a `[AEM Forms as a Cloud Service Git repostory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config` pasta. Você pode encontrar o `<appid>` no `archetype.properties` arquivos do projeto.
1. Abra o `[AEM Forms as a Cloud Service Git repostory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config/Guide Localization Service.cfg.json` arquivo para edição. Crie o arquivo, caso ele não exista. Um arquivo de amostra com localidades suportadas é semelhante ao seguinte:

   ![Um exemplo de Guia de localização Service.cfg.json](locales.png)

1. Adicione o [código de localidade do idioma](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) você deseja adicionar, por exemplo, adicionar &#39;hi&#39; para hindi.
1. Salvar e fechar o arquivo.

### 3. Crie uma Biblioteca do cliente para adicionar um local

O AEM Forms fornece um exemplo de biblioteca de cliente para ajudá-lo a adicionar novas localidades facilmente. Você pode baixar e adicionar o `clientlib-it-custom-locale` biblioteca do cliente do repositório dos Componentes principais do Forms adaptável no GitHub para o repositório as a Cloud Service do Forms. Para adicionar a biblioteca do cliente, siga estas etapas:

1. Abra o repositório dos Componentes principais do Forms adaptável no editor de texto simples. Se você não tiver o repositório clonado, consulte [Pré-requisitos](#prerequistes) para obter instruções sobre como clonar o repositório.
1. Navegue até a `/aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs` diretório.
1. Copie o `clientlib-it-custom-locale` diretório.
1. Navegue até `[AEM Forms as a Cloud Service Git repostory]/ui.apps/src/main/content/jcr_root/apps/moonlightprodprogram/clientlibs` e cole a variável `clientlib-it-custom-locale` diretório.


### 4. Criar um arquivo específico de local {#locale-specific-file}

1. Vá até `[AEM Forms as a Cloud Service Git repostory]/ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/`
1. Localize o [Inglês locale .json file on GitHub](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json), que contém o conjunto mais recente de strings padrão incluídas no produto.
1. Crie um novo arquivo .json para o local específico.
1. No arquivo .json recém-criado, espelhe a estrutura do arquivo de localidade em inglês.
1. Substitua as strings do idioma inglês no arquivo .json pelas strings localizadas correspondentes para o seu idioma.
1. Salve e feche o arquivo.


### 4. Adicionar suporte local ao dicionário {#add-locale-support-for-the-dictionary}

Execute esta etapa somente se a variável `<locale>` você está adicionando não está entre `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Navegue até a `[AEM Forms as a Cloud Service Git repostory]/ui.content/src/main/content/jcr_root/etc/` pasta.

1. Criar um `etc` pasta sob o `jcr_root` pasta, se ainda não estiver presente.

1. Criar uma pasta `languages` no `etc` pasta, se ainda não estiver presente.

   ![Texto alternativo](etc-content-xml.png)

1. Criar um `.content.xml` arquivo sob o `languages` pasta. Adicione o seguinte conteúdo ao arquivo:

   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
   jcr:primaryType="nt:unstructured"
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr]"/>
   ```

1. Adicione o código de localidade à `languages` propriedade. Por exemplo, hi adicionou para hindi ao código de exemplo a seguir.


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
   jcr:primaryType="nt:unstructured"
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

1. Adicione as pastas recém-criadas na `filter.xml` em `/ui.content/src/main/content/meta-inf/vault/filter.xml` como:

   ```
   <filter root="/etc/languages"/>
   ```

   ![Adicione as pastas recém-criadas na `filter.xml` em `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)

### 5. Confirme as alterações e implante o pipeline {#commit-changes-in-repo-deploy-pipeline}

Confirme as alterações no repositório GIT após adicionar um novo suporte de localidade. Implante seu código usando o pipeline de pilha completa. Saiba mais [como configurar um pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) para adicionar novo suporte de local.
Quando o pipeline estiver concluído, o local recém-adicionado aparecerá no ambiente AEM.

## Usar local adicionado no Adaptive Forms {#use-added-locale-in-af}

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


Depois que a localidade é identificada, o Formulário adaptável escolhe o dicionário específico do formulário. Se o dicionário específico do formulário para a localidade solicitada não for encontrado, ele usará o dicionário para o idioma no qual o Formulário adaptável foi criado.

Se não houver informações de local disponíveis, o Formulário adaptável será exibido em seu idioma original, que é o idioma usado durante seu desenvolvimento.

Obter [biblioteca cliente de exemplo](/help/forms/assets/locale-support-sample.zip) para adicionar suporte ao novo local. É necessário alterar o conteúdo da pasta no local necessário.

## Práticas recomendadas para oferecer suporte à nova localização {#best-practices}

* O Adobe recomenda criar um projeto de tradução após criar um Formulário adaptável.

* Quando novos campos são adicionados em um Formulário adaptável existente:
   * **Para tradução automática**: recrie o dicionário e execute o projeto de tradução. Os campos adicionados a um Formulário adaptável após a criação de um projeto de tradução permanecem não traduzidos.
   * **Para tradução humana**: Exportar o dicionário através do `[server:port]/libs/cq/i18n/gui/translator.html`. Atualize o dicionário para os campos recém-adicionados e faça upload dele.
