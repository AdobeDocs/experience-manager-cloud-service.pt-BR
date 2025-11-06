---
title: Design responsivo
description: Com um design responsivo, as mesmas experiências podem ser exibidas com eficiência em vários dispositivos em várias orientações.
exl-id: be645062-d6d6-45a2-97dc-d8aa235539b8
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---


# Design responsivo {#responsive-design}

Com um design responsivo, as mesmas experiências podem ser exibidas com eficiência em vários dispositivos em várias orientações.

>[!TIP]
>
>Este documento fornece uma visão geral do design responsivo para desenvolvedores e como os recursos são realizados no AEM. Recursos adicionais estão disponíveis:
>
>* Para autores de conteúdo, os detalhes de como usar recursos de design responsivo em uma página de conteúdo estão disponíveis no documento [Layout responsivo.](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
>* Para administradores de site, os detalhes sobre como configurar o contêiner de layout para seus sites estão descritos no documento [Configuração do Contêiner de Layout e do Modo de Layout.](/help/sites-cloud/administering/responsive-layout.md)

## Visão geral {#overview}

Projete suas experiências para que elas se adaptem à janela de visualização do cliente em que são exibidas. Com um design responsivo, as mesmas páginas podem ser exibidas efetivamente em vários dispositivos em ambas as orientações. A imagem a seguir demonstra algumas maneiras pelas quais uma página pode responder às alterações no tamanho da janela de visualização:

* Layout: use layouts de coluna única para visores menores e layouts de várias colunas para visores maiores.
* Tamanho do texto: use um tamanho de texto maior (quando apropriado, como cabeçalhos) em visores maiores.
* Conteúdo: inclua apenas o conteúdo mais importante ao exibir em dispositivos menores.
* Navegação: ferramentas específicas de dispositivos são fornecidas para acessar outras páginas.
* Imagens: exibe representações de imagens apropriadas para a janela de visualização do cliente de acordo com as dimensões da janela.

![Exemplos de design responsivo](assets/responsive-example.png)

Desenvolva aplicativos Adobe Experience Manager (AEM) que geram HTML5 que se adaptam a vários tamanhos de janela e orientações. Por exemplo, os seguintes intervalos de larguras de visor correspondem a vários tipos e orientações de dispositivo

* Largura máxima de 480 pixels (telefone, retrato)
* Largura máxima de 767 pixels (telefone, paisagem)
* Largura entre 768 pixels e 979 pixels (tablet, retrato)
* Largura entre 980 pixels e 1199 pixels (tablet, paisagem)
* Largura de 1200 px ou superior (desktop)

Consulte os seguintes tópicos para obter informações sobre como implementar um comportamento de design responsivo:

* [Consultas de mídia](#using-media-queries)
* [Grades fluídas](#developing-a-fluid-grid)
* [Imagens adaptáveis](#using-adaptive-images)

Conforme você cria, use a barra de ferramentas **Emulador** para visualizar suas páginas para vários tamanhos de tela.

## Antes de desenvolver {#before-you-develop}

Antes de desenvolver o aplicativo do AEM compatível com suas páginas da Web, várias decisões de design devem ser tomadas. Por exemplo, você precisa ter as seguintes informações:

* Os dispositivos que você está direcionando
* Os tamanhos das janelas de visualização de destino
* Os layouts de página para cada tamanho de visor direcionado

### Estrutura do aplicativo {#application-structure}

A estrutura de aplicativo típica do AEM é compatível com todas as implementações de design responsivas:

* Os componentes da página residem abaixo de `/apps/<application_name>/components`
* Os modelos residem abaixo de `/apps/<application_name>/templates`

## Uso de consultas de mídia {#using-media-queries}

As consultas de mídia permitem o uso seletivo de estilos CSS para renderização da página. As ferramentas e os recursos de desenvolvimento do AEM permitem que você implemente de forma eficaz e eficiente as consultas de mídia em seus aplicativos.

O grupo W3C fornece a recomendação [Consultas de Mídia](https://www.w3.org/TR/css3-mediaqueries/) que descreve esse recurso CSS3 e a sintaxe.

### Criação do arquivo CSS {#creating-the-css-file}

No arquivo CSS, defina consultas de mídia com base nas propriedades dos dispositivos que você está direcionando. A seguinte estratégia de implementação é eficaz para gerenciar estilos para cada consulta de mídia:

* Use uma [pasta da Biblioteca do Cliente](clientlibs.md) para definir o CSS que é montado quando a página é renderizada.
* Defina cada consulta de mídia e os estilos associados em arquivos CSS separados. É útil usar nomes de arquivo que representem os recursos do dispositivo da query de mídia.
* Defina estilos comuns a todos os dispositivos em um arquivo CSS separado.
* No arquivo css.txt da pasta Biblioteca do cliente, ordene os arquivos CSS da lista conforme necessário no arquivo CSS montado.

O [tutorial do WKND](develop-wknd-tutorial.md) usa essa estratégia para definir estilos no design do site. O arquivo CSS usado pela WKND está localizado em `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.

### Uso de consultas de mídia com páginas do AEM {#using-media-queries-with-aem-pages}

[O projeto de amostra WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) e o [Arquétipo de Projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) usam o [Componente principal de página](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/page.html), que inclui as clientlibs por meio da política de página.

Se o seu próprio componente de página não for baseado no Componente principal de página, você também poderá incluir a pasta da biblioteca do cliente no script HTL ou JSP dele. Isso gerará e referenciará o arquivo CSS com as consultas de mídia necessárias para que a grade responsiva funcione.

#### HTL {#htl}

```html
<sly data-sly-use.clientlib="${'/libs/granite/sightly/templates/clientlib.html'}">
<sly data-sly-call="${clientlib.all @ categories='apps.weretail.all'}"/>
```

#### JSP {#jsp}

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

O script JSP gera o seguinte código HTML que faz referência às folhas de estilos:

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Visualização de dispositivos específicos {#previewing-for-specific-devices}

O emulador permite visualizar as páginas em diferentes tamanhos de visor para testar o comportamento do design responsivo. Ao editar uma página no Console de sites, toque ou clique no ícone **Emulador** para revelar o emulador.

![O ícone de emulador na barra de ferramentas](assets/emulator-icon.png)

Na barra de ferramentas do emulador, toque ou clique no ícone **Dispositivos** para exibir um menu suspenso onde é possível selecionar um dispositivo. Ao selecionar um dispositivo, a página muda para se adaptar ao tamanho do visor.

![A barra de ferramentas do emulador](assets/emulator.png)

### Especificando Grupos de Dispositivos {#specifying-device-groups}

Para especificar os grupos de dispositivos que aparecem na lista **Dispositivos**, adicione uma propriedade `cq:deviceGroups` ao nó `jcr:content` da página de modelo do site. O valor da propriedade é uma matriz de caminhos para os nós do grupo de dispositivos.

Por exemplo, a página de modelo do site WKND é `/conf/wknd/settings/wcm/template-types/empty-page/structure`. E o nó `jcr:content` abaixo dele inclui a seguinte propriedade:

* Nome: `cq:deviceGroups`
* Tipo: `String[]`
* Valor: `mobile/groups/responsive`

Os nós do grupo de dispositivos estão na pasta `/etc/mobile/groups`.

## Imagens responsivas {#responsive-images}

Páginas responsivas se adaptarão dinamicamente ao dispositivo no qual são renderizadas, oferecendo uma melhor experiência para o usuário. No entanto, também é importante que os ativos sejam otimizados para o ponto de interrupção e o dispositivo para minimizar o tempo de carregamento da página.

[O Componente de Imagem do Componente Principal](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=pt-BR) apresenta recursos como seleção de imagem adaptável.

* Por padrão, o Componente de imagem usa o [Servlet de imagem adaptável](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/adaptive-image-servlet.html) para fornecer a representação adequada.
* A [Entrega de imagens otimizadas para a Web](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html?lang=pt-BR) também está disponível por meio de uma caixa de seleção simples em sua política, que fornece ativos de imagem do DAM em formato WebP e pode reduzir o tamanho de download de uma imagem em cerca de 25%, em média.

## O Contêiner de layout {#layout-container}

O Contêiner de layout do AEM permite implementar com eficiência e eficácia o layout responsivo para adaptar as dimensões da página à janela de visualização do cliente.

>[A documentação do GitHub](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) da grade responsiva é uma referência que pode ser fornecida para desenvolvedores front-end permitindo que usem a grade do AEM fora do AEM, por exemplo, ao criar modelos estáticos do HTML para um site futuro do AEM.

>[!TIP]
>
>Consulte o documento [Configuração do Contêiner de Layout e do Modo de Layout](/help/sites-cloud/administering/responsive-layout.md) para obter mais informações sobre como o Contêiner de Layout funciona e como habilitar layouts responsivos para o seu conteúdo.

## Grades Responsivas Aninhadas {#nested-responsive-grids}

Pode haver ocasiões em que você ache necessário aninhar grades responsivas para suportar as necessidades do seu projeto. No entanto, lembre-se de que a prática recomendada pela Adobe é manter a estrutura o mais plana possível.

Quando não for possível evitar o uso de grades responsivas aninhadas, verifique se:

* Todos os contêineres (contêineres, guias, acordeões, etc.) têm a propriedade `layout = responsiveGrid`.
* Não misture a propriedade `layout = simple` na hierarquia de contêiner.

Isso inclui todos os containers estruturais do modelo de página.

O número da coluna do contêiner interno nunca deve ser maior que o do contêiner externo. O exemplo a seguir satisfaz essa condição. Embora o número da coluna do contêiner externo seja 8 para a tela padrão (desktop), o número da coluna do contêiner interno é 4.

>[!BEGINTABS]

>[!TAB Exemplo de estrutura de nó]

```text
container
  @layout = responsiveGrid
  cq:responsive
    default
      @offset = 0
      @width = 8
  container
  @layout = responsiveGrid
    cq:responsive
      default
        @offset = 0
        @width = 4
    text
      @text =" Text Column 1"
```

>[!TAB Exemplo de HTML resultante]

```html
<div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--default--8 aem-GridColumn--offset--default--0">
  <div id="container-c9955c233c" class="cmp-container">
    <div class="aem-Grid aem-Grid--8 aem-Grid--default--8 ">
      <div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--offset--default--0 aem-GridColumn--default--4">
        <div id="container-8414e95866" class="cmp-container">
          <div class="aem-Grid aem-Grid--4 aem-Grid--default--4 ">
            <div class="text aem-GridColumn aem-GridColumn--default--4">
              <div data-cmp-data-layer="..." id="text-1234567890" class="cmp-text">
                <p>Text Column 1</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```

>[!ENDTABS]
