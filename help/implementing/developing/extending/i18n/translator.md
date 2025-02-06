---
title: Internacionalizando strings de interface do usuário
description: O AEM fornece um console para gerenciar as várias traduções de textos usados na interface do usuário do componente.
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 14a6516872f842d099b902b9f633b1d6f984266d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Usar o Translator para gerenciar dicionários{#using-translator-to-manage-dictionaries}

O AEM fornece um console para gerenciar as várias traduções de textos usados na interface do usuário do componente. Esse console está disponível em:

`https://<hostname>:<port-number>/libs/cq/i18n/gui/translator.html`

Use a ferramenta de tradução para gerenciar cadeias de caracteres em inglês e suas traduções. Os dicionários são criados no repositório, por exemplo, `/apps/myproject/i18n`.

A ferramenta Tradutor e os dicionários gerenciados são usados para apresentar a interface do usuário do componente em diferentes idiomas. Se quiser traduzir páginas, consulte [Tradução de conteúdo para sites multilíngues](/help/sites-cloud/administering/translation/overview.md).

## Criando um dicionário {#creating-a-dictionary}

Os desenvolvedores podem criar dicionários i18n no AEM para gerenciar cadeias de caracteres de componentes localizadas. Dicionários normalmente fazem parte do código do componente em `/apps`. Veja a seguir um exemplo do código WKND AEM com um par de chave/valor usado em todos os componentes WKND.

```
{
  "&copy; {0} WKND Site Site. All rights reserved." : "&copy; {0} WKND Site Site. Tous droits réservés."
}
```

Os desenvolvedores podem criar dicionários adicionais adicionando um nó raiz (`sling:Folder`) para um novo dicionário manter as definições de idioma para cadeias de caracteres de componentes.

```shell
/apps/myProject/i18n [sling:Folder]
    - de.json [nt:file] [mix:language]
        + jcr:language = de
    - fr.json [nt:file] [mix:language]
        + jcr:language = fr
```

>[!NOTE]
>
>Esta é a estrutura do [módulo Sling i18n](https://sling.apache.org/site/internationalization-support.html).

Depois de criados em um repositório GitHub no AEM, os dicionários podem ser implantados por meio de um AEM [pipeline de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

## Localizações do dicionário {#dictionary-locations}

Os desenvolvedores podem criar livremente um dicionário do idioma de origem no `/apps` ou `/content/cq:i18n`. Iniciando com o código de amostra do arquétipo AEM, os dicionários iniciais normalmente ficam no caminho `/apps`. Se uma meta for armazenar cópias de idioma do dicionário correspondente também no `/apps`, essas cópias de idioma deverão ser criadas e mantidas manualmente pelos desenvolvedores no código do componente.

Como alternativa, o novo processo de tradução do tempo de execução do AEM para dicionários i18n criará dicionários traduzidos em `/content/cq:i18n/<projectName>`, independentemente se o dicionário de origem estiver armazenado em `/apps` ou `/content`.

As decisões sobre onde localizar os dicionários i18n, cópias de origem e idioma, devem ser tomadas usando os seguintes critérios:

* `/apps`
   * local padrão para dicionários com traduções de string de componentes, seguindo o arquétipo AEM e o código de amostra WKND
   * maior ordem de renderização, por Sling ([Hierarquias de Pesquisa de Conjunto de Recursos](https://sling.apache.org/documentation/bundles/internationalization-support-i18n.html#resourcebundle-hierarchies))
   * mas não é possível editar ou traduzir dicionários em tempo de execução, pois `/apps` é imutável em ambientes AEM as a Cloud Service

* `/content/cq:i18n`
   * local alternativo para dicionários i18n se
      * a tradução de dicionários em tempo de execução é obrigatória
      * é necessária a capacidade de editar um dicionário em tempo de execução
   * local padrão onde a tradução de dicionário em tempo de execução criará cópias de idioma.

Como `/apps` sempre substitui `/content` na ordem de renderização do Sling, é importante ter em mente que dicionários com pares chave/valor idênticos não devem existir simultaneamente em `/apps` e `/content/cq:i18n`, pois o dicionário em `/content/cq:i18n` nunca será usado para renderização. Se uma cópia de idioma do dicionário, ou seja, o destino da tradução, já existir em `/apps`, e o objetivo for torná-la traduzível em tempo de execução no AEM as a Cloud Service, a cópia de idioma do dicionário original em `/apps` deverá ser movida para `/content/cq:i18n` ou ser excluída em `/apps` e recriada automaticamente em `/content/cq:i18n` através da tradução do dicionário de origem. Este processo de tradução criará automaticamente as cópias de idioma no `/content/cq:i18n`.

## Criação automática de dicionário {#automatic-creation}

Para páginas AEM e fragmentos de experiência que contêm componentes principais de AEM, o novo processo de tradução de dicionário também verificará essas páginas ou fragmentos de experiência em busca de componentes e strings de componentes que devem ser traduzidos. O sistema criará automaticamente as novas cópias de idioma do dicionário correspondentes no `/content/cq:i18n`. Isso não se aplica aos fragmentos de conteúdo, pois eles são conteúdo puro e estruturado sem o uso de componentes principais do AEM.

## Exportar um dicionário {#exporting-a-dictionary}

Embora a tradução em tempo de execução dos dicionários i18n em `/apps` ou `/libs` locais não seja possível no AEM as a Cloud Service, pois esses locais são imutáveis, esses dicionários ainda podem ser exportados em tempo de execução para tradução assíncrona fora do AEM.

Para exportar as strings do idioma de origem de um dicionário para um arquivo XLIFF:

1. Abrir a ferramenta de Tradução `http://<host>:<port>/libs/cq/i18n/gui/translator.html`

   >[!NOTE]
   >
   >A ferramenta está disponível somente por meio desse URL e não pode ser acessada pela interface do usuário do produto AEM.

1. Use o menu suspenso Dicionários para selecionar o dicionário a ser exportado.
1. Clique em Exportar Tradução XLIFF e Exportar completo `<locale>` xliff.

## Importando um dicionário {#importing-a-dictionary}

Para importar um arquivo XLIFF em um dicionário para preencher o conteúdo do dicionário:

1. Abrir a ferramenta de Tradução `http://<host>:<port>/libs/cq/i18n/gui/translator.html`
1. Clique em Importar e depois em Traduções XLIFF.
1. Selecione o arquivo a ser importado e clique em OK.
