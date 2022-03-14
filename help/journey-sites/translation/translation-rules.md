---
title: Configurar regras de tradução
description: Saiba como definir regras de tradução para identificar o conteúdo para tradução.
index: true
hide: false
hidefromtoc: false
exl-id: 831009b8-8e09-4b0f-b0fd-4e21221c1455
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---

# Configurar regras de tradução {#configure-translation-rules}

Saiba como definir regras de tradução para identificar o conteúdo para tradução.

## A História Até Agora {#story-so-far}

No documento anterior da jornada de tradução do AEM Sites, [Configurar conector de tradução](configure-connector.md) você aprendeu a instalar e configurar seu conector de tradução e agora deve:

* Entenda os parâmetros importantes da Estrutura de integração de tradução no AEM.
* Pode configurar sua própria conexão com o serviço de tradução.

Agora que seu conector está configurado, este artigo o conduzirá até a próxima etapa de identificação do conteúdo que deve ser traduzido.

## Objetivo {#objective}

Este documento ajuda você a entender como usar AEM regras de tradução para identificar o conteúdo de tradução. Após ler este documento, você deve:

* Entenda o que as regras de tradução fazem.
* Pode definir suas próprias regras de tradução.

## Regras de tradução {#translation-rules}

As páginas do AEM Sites podem conter muitas informações. Dependendo das necessidades do seu projeto, é provável que nem todas as informações em uma página precisem ser traduzidas.

As regras de tradução identificam o conteúdo que está incluído ou excluído dos projetos de tradução. Quando o conteúdo é traduzido, AEM extrai ou obtém o conteúdo com base nessas regras. Dessa forma, somente o conteúdo que deve ser traduzido é enviado para o serviço de tradução.

As regras de tradução incluem as seguintes informações:

* O caminho do conteúdo ao qual a regra se aplica
   * A regra também se aplica aos descendentes do conteúdo
* Os nomes das propriedades que contêm o conteúdo a ser traduzido
   * A propriedade pode ser específica para um tipo de recurso específico ou para todos os tipos de recurso

AEM cria regras de tradução automaticamente para páginas de sites, mas como os requisitos de cada projeto são diferentes, é importante saber como revisar e adaptar as regras conforme necessário ao projeto.

## Criação de regras de tradução {#creating-rules}

Várias regras podem ser criadas para suportar requisitos complexos de tradução. Por exemplo, um projeto no qual você pode estar trabalhando exige que todas as informações da página sejam traduzidas, mas em outra página somente as descrições devem ser traduzidas, enquanto os títulos ficam sem tradução.

As regras de tradução são projetadas para lidar com tais cenários. No entanto, neste exemplo, ilustramos como criar regras com foco em uma configuração simples e única.

Existe um **Configuração de tradução** console disponível para configurar regras de tradução.

Para acessá-lo:

1. Navegar para **Ferramentas** -> **Geral**.
1. Toque ou clique **Configuração de tradução**.

AEM cria automaticamente regras de tradução para todo o conteúdo. Para exibir essas regras:

1. Selecione o `/content` e, em seguida, o **Editar** na barra de ferramentas.
1. O Editor de regras de tradução é aberto com as regras que AEM criadas automaticamente para o `/content` caminho.

   ![Editor de regras de tradução](assets/translation-rules-editor.png)

1. As propriedades de página que serão traduzidas estão localizadas na variável **Geral** da lista. Você pode adicionar ou atualizar nomes de propriedades existentes que deseja incluir explicitamente na tradução.
   1. Insira o nome da propriedade no **Nova propriedade** campo.
   1. As opções **Traduzir** e **Herdar** são marcadas automaticamente.
   1. Toque ou clique **Adicionar**.
   1. Repita essas etapas para todos os campos que devem ser traduzidos.
   1. Toque ou clique **Salvar**.

Agora você configurou suas regras de tradução.

>[!NOTE]
>
>AEM cria regras de tradução automaticamente. Para uma configuração de tradução simples ou para testar um fluxo de trabalho de tradução, não é necessário criar novas regras ou até mesmo modificar as regras existentes criadas automaticamente. Os detalhes dessas etapas são apresentados para explicar como as regras funcionam e contextualizar como o AEM processa traduções.

>[!TIP]
>
>Também é possível criar regras apenas para seu caminho ou projeto específico tocando ou clicando no botão **Adicionar contexto** no console Configuração de tradução. Isso está fora do escopo dessa jornada.

## Uso avançado {#advanced-usage}

Há várias propriedades adicionais que podem ser configuradas como parte das regras de tradução. Além disso, você pode especificar suas regras manualmente como XML, o que permite maior especificidade e flexibilidade.

Esses recursos geralmente não são necessários para começar a localizar seu conteúdo, mas você pode ler mais sobre eles na seção [Recursos adicionais](#additional-resources) se você estiver interessado.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de tradução do AEM Sites, deve:

* Entenda o que as regras de tradução fazem.
* Pode definir suas próprias regras de tradução.

Aproveite esse conhecimento e continue sua jornada de tradução do AEM Sites revisando o documento [Traduzir conteúdo](translate-content.md) onde você aprenderá como o conector e as regras funcionam juntos para traduzir conteúdo.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de tradução revisando o documento [Traduzir conteúdo,](translate-content.md) a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada.

* [Identificação de conteúdo a ser traduzido](/help/sites-cloud/administering/translation/rules.md) - Saiba como as regras de tradução identificam o conteúdo que precisa ser traduzido.
