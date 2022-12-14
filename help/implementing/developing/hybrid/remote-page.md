---
title: O componente RemotePage
description: O Componente de página remota é um componente de página personalizado para editar o React SPA remoto no AEM.
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
source-git-commit: d213dd0788e66015237d241caf0f3b5737ce725c
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---

# O componente RemotePage {#remote-page-component}

Ao decidir [que nível de integração](/help/implementing/developing/headful-headless.md) você gostaria de ter entre seu SPA externo e o AEM, geralmente é claro que você precisa visualizar e editar o SPA dentro do AEM. O Componente RemotePage é um componente de página personalizado apenas para essa finalidade.

## Visão geral {#overview}

O componente RemotePage busca todos os ativos necessários do aplicativo gerado `asset-manifest.json` O e o usa para renderizar a SPA no AEM.

* A RemotePage permite inserir os scripts e as folhas de estilos de um SPA no corpo de um componente Página AEM.
* Os Componentes do Frente Virtual permitem marcar seções como editáveis AEM Editor de SPA.
* Juntos, um SPA hospedado em um domínio diferente pode ser editado no AEM.

Veja o artigo [Edição de um SPA externo no AEM](editing-external-spa.md) para obter mais detalhes sobre SPA editáveis e externos em AEM.

## Requisitos {#requirements}

* Habilitar CORS no desenvolvimento
* Configurar o URL remoto nas Propriedades da página
* Renderizar a SPA em AEM
* A aplicação Web deve usar um manifesto de ativo do pacote como um dos seguintes e expor um `asset-manifest.json` na raiz do domínio que lista em um `entrypoints property` todos os arquivos CSS e JS que devem ser carregados:
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
      ![exemplo da propriedade entrypoints](assets/asset-manifest-entrypoints.png)
* O aplicativo deve ser capaz de inicializar em um `<div id="root"></div>` abaixo do `body` elemento. Se uma marcação diferente for esperada para o aplicativo instanciar, isso deverá ser ajustado adequadamente nos scripts HTL do componente proxy que tem uma `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Limitações {#limitations}

* O componente RemotePage espera que a implementação forneça um manifesto de ativo como aquele [encontrado aqui.](https://github.com/shellscape/webpack-manifest-plugin) No entanto, o componente RemotePage só foi testado para funcionar com a estrutura React (e Next.js através do componente página remota seguinte) e, portanto, não suporta o carregamento remoto de aplicativos de outras estruturas, como o Angular.
* O CSS interno definido no arquivo HTML do aplicativo, bem como o CSS em linha no nó DOM raiz, não estará disponível ao fazer a renderização remota no AEM.

## Detalhes técnicos {#technical-details}

Como o resto do projeto de SPA de AEM, o Componente RemotePage é de código aberto. Para obter os detalhes técnicos completos do Componente de página remota, [consulte o repositório GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
