---
title: Configurar regras de tradução
description: Saiba como definir regras de tradução para identificar o conteúdo para tradução.
index: false
hide: true
hidefromtoc: true
source-git-commit: 142c49b6b98dc78c3d36964dada1cfb900afee66
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 0%

---

# Configurar regras de tradução {#configure-translation-rules}

Saiba como definir regras de tradução para identificar o conteúdo para tradução.

## A História Até Agora {#story-so-far}

No documento anterior da jornada de tradução AEM sem cabeçalho, [Configure translation connector](configure-connector.md) você aprendeu a instalar e configurar seu conector de tradução e agora deve:

* Entenda os parâmetros importantes da Estrutura de integração de tradução no AEM.
* Pode configurar sua própria conexão com o serviço de tradução.

Agora que seu conector está configurado, este artigo o conduzirá até a próxima etapa de identificação do conteúdo que deve ser traduzido.

## Objetivo {#objective}

Este documento ajuda você a entender como usar AEM regras de tradução para identificar o conteúdo de tradução. Após ler este documento, você deve:

* Entenda o que as regras de tradução fazem.
* Pode definir suas próprias regras de tradução.

## Regras de tradução {#translation-rules}

Fragmentos de conteúdo, que representam o conteúdo sem periféricos, podem conter muitas informações organizadas por campos estruturados. Dependendo das necessidades do seu projeto, é provável que nem todos os campos em um Fragmento de conteúdo precisem ser traduzidos.

As regras de tradução identificam o conteúdo que está incluído ou excluído dos projetos de tradução. Quando o conteúdo é traduzido, AEM extrai ou obtém o conteúdo com base nessas regras. Dessa forma, somente o conteúdo que deve ser traduzido é enviado para o serviço de tradução.

As regras de tradução incluem as seguintes informações:

* O caminho do conteúdo ao qual a regra se aplica
   * A regra também se aplica aos descendentes do conteúdo
* Os nomes das propriedades que contêm o conteúdo a ser traduzido
   * A propriedade pode ser específica para um tipo de recurso específico ou para todos os tipos de recurso

Como os Modelos de fragmentos de conteúdo, que definem a estrutura dos Fragmentos de conteúdo, são exclusivos de seu próprio projeto, é vital configurar regras de tradução para que o AEM saiba quais elementos dos modelos de conteúdo devem ser traduzidos.

>[!TIP]
>
>Geralmente, o arquiteto de conteúdo fornece ao especialista de tradução o **Nome da propriedade** s de todos os campos necessários para a tradução. Esses nomes são necessários para configurar as regras de tradução. Como especialista em tradução, você [pode encontrar esses **Nome da propriedade** como ](getting-started.md#content-modlels) conforme descrito anteriormente nesta jornada.

## Criação de regras de tradução {#creating-rules}

Várias regras podem ser criadas para suportar requisitos complexos de tradução. Por exemplo, um projeto no qual você pode estar trabalhando requer que todos os campos do modelo sejam traduzidos, mas em outro apenas os campos de descrição devem ser traduzidos enquanto os títulos ficam não traduzidos.

As regras de tradução são projetadas para lidar com tais cenários. No entanto, neste exemplo, ilustramos como criar regras com foco em uma configuração simples e única.

Há um console **Configuração de tradução** disponível para configurar regras de tradução. Para acessá-lo:

1. Navegue até **Ferramentas** -> **Geral**.
1. Toque ou clique em **Configuração de Tradução**.

Na interface **Configuração de tradução**, há várias opções disponíveis para suas regras de tradução. Aqui destacamos as etapas mais necessárias e típicas necessárias para uma configuração básica de localização sem cabeçalho.

1. Toque ou clique em **Adicionar contexto**, o que permite adicionar um caminho. Esse é o caminho do conteúdo que deve ser afetado pela regra.
   ![Adicionar contexto](assets/add-translation-context.png)
1. Use o navegador de caminho para selecionar o caminho necessário e toque ou clique no botão **Confirm** para salvar. Lembre-se, os Fragmentos de conteúdo, que contêm conteúdo sem cabeçalho, geralmente estão localizados em `/content/dam/<your-project>`.
   ![Selecione o caminho](assets/select-context.png)
1. AEM salva a configuração.
1. Você deve selecionar o contexto que acabou de criar e tocar ou clicar em **Editar**. Isso abre o **Editor de regras de tradução** para configurar as propriedades.
   ![Editor de regras de tradução](assets/translation-rules-editor.png)
1. Por padrão, todas as configurações são herdadas do caminho pai, neste caso `/content/dam`. Desmarque a opção **Herdar de`/content/dam`** para adicionar campos adicionais à configuração.
1. Depois de desmarcado, na seção **Geral** da lista, adicione os nomes de propriedade dos Modelos de Fragmento de Conteúdo que você [anteriormente identificado como campos para tradução.](getting-started.md#content-models)
   1. Insira o nome da propriedade no campo **New Property**.
   1. As opções **Translate** e **Inherit** são marcadas automaticamente.
   1. Toque ou clique em **Adicionar**.
   1. Repita essas etapas para todos os campos que devem ser traduzidos.
   1. Toque ou clique em **Salvar**.
      ![Adicionar propriedade](assets/add-property.png)

Agora você configurou suas regras de tradução.

## Uso avançado {#advanced-usage}

Há várias propriedades adicionais que podem ser configuradas como parte das regras de tradução. Além disso, você pode especificar suas regras manualmente como XML, o que permite maior especificidade e flexibilidade.

Esses recursos geralmente não são necessários para começar a localizar seu conteúdo sem periféricos, mas você pode ler mais sobre eles na seção [Additional Resources](#additional-resources) se estiver interessado.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de tradução sem cabeçalho, é necessário:

* Entenda o que as regras de tradução fazem.
* Pode definir suas próprias regras de tradução.

Aproveite esse conhecimento e prossiga com sua jornada de tradução sem periféricos AEM revisando o documento [Traduzir conteúdo](translate-content.md), onde você aprenderá como seu conector e as regras trabalham juntos para traduzir conteúdo sem periféricos.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de tradução sem periféricos revisando o documento [Traduzir conteúdo,](translate-content.md) a seguir estão alguns recursos adicionais opcionais que fazem um mergulho mais profundo em alguns conceitos mencionados neste documento, mas eles não são solicitados a continuar com a jornada sem periféricos.

* [Identificação de conteúdo para traduzir](/help/sites-cloud/administering/translation/rules.md)  - saiba como as regras de tradução identificam o conteúdo que precisa ser traduzido.
