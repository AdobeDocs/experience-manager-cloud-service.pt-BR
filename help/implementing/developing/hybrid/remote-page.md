---
title: O componente RemotePage
description: O componente RemotePage é um componente de página personalizado para editar o React SPA remoto no AEM.
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
feature: Developing
role: Admin, Developer
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---


# O componente RemotePage {#remote-page-component}

Ao decidir [que nível de integração](/help/implementing/developing/headful-headless.md) você gostaria de ter entre seu SPA externo e o AEM, geralmente fica claro que você precisa exibir e editar o SPA no AEM. O componente RemotePage é um componente de página personalizado apenas para esta finalidade.

{{ue-over-spa}}

## Visão geral {#overview}

O componente RemotePage busca todos os ativos necessários do `asset-manifest.json` gerado pelo aplicativo e usa isso para renderizar o SPA no AEM.

* A RemotePage permite inserir os scripts e folhas de estilos de um SPA no corpo de um componente Página do AEM.
* Os Componentes de front-end virtuais permitem marcar seções como editáveis no AEM SPA Editor.
* Juntos, um SPA hospedado em um domínio diferente pode se tornar editável no AEM.

Consulte o artigo [Edição de um SPA externo no AEM](editing-external-spa.md) para obter mais detalhes sobre SPAs externos editáveis no AEM.

## Requisitos {#requirements}

* Ativar o CORS em desenvolvimento
* Configurar o URL remoto nas Propriedades da página
* Renderize o SPA no AEM
* O aplicativo Web deve usar um manifesto de ativo de pacote como um dos itens a seguir e expor um arquivo `asset-manifest.json` na raiz do domínio que lista em um `entrypoints property` todos os arquivos CSS e JS que devem ser carregados:
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
     ![exemplo de propriedade de pontos de entrada](assets/asset-manifest-entrypoints.png)
* O aplicativo deve ser capaz de inicializar em um `<div id="root"></div>` sob o elemento `body`. Se uma marcação diferente for esperada para o aplicativo instanciar, ela deverá ser ajustada adequadamente nos scripts HTL do componente proxy que tem um `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Limitações {#limitations}

* O componente RemotePage espera que a implementação forneça um manifesto de ativo como o [encontrado aqui](https://github.com/shellscape/webpack-manifest-plugin). No entanto, o componente RemotePage só foi testado para funcionar com a estrutura React (e o Next.js por meio do componente remote-page-next) e, portanto, não oferece suporte ao carregamento remoto de aplicativos de outras estruturas, como o Angular.
* O CSS interno definido no arquivo HTML raiz do aplicativo e o CSS em linha no nó DOM raiz não estarão disponíveis ao fazer renderização remota no AEM.

## Detalhes técnicos {#technical-details}

Como o restante do projeto SPA do AEM, o componente RemotePage é de código aberto. Para obter os detalhes técnicos completos do componente RemotePage, [consulte o repositório GitHub](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage).
