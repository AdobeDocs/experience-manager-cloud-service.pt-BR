---
title: Design responsivo
description: Com um design responsivo, as mesmas experiências podem ser exibidas eficientemente em vários dispositivos em várias orientações
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Design responsivo {#responsive-design}

Projete suas experiências para que elas se adaptem à janela de visualização do cliente em que são exibidas. Com o design responsivo, as mesmas páginas podem ser exibidas efetivamente em vários dispositivos em ambas as orientações. A imagem a seguir demonstra algumas maneiras pelas quais uma página pode responder às alterações no tamanho da janela de visualização:

* Layout: Use layouts de coluna única para visores menores e layouts de várias colunas para visores maiores.
* Tamanho do texto: Use um tamanho de texto maior (quando apropriado, como cabeçalhos) em visores maiores.
* Conteúdo: Inclua apenas o conteúdo mais importante ao exibir em dispositivos menores.
* Navegação: Ferramentas específicas de dispositivo são fornecidas para acessar outras páginas.
* Imagens: Exibição de representações de imagem apropriadas para o visor do cliente de acordo com as dimensões da janela.

![Exemplos de design responsivo](assets/responsive-example.png)

Desenvolva aplicativos Adobe Experience Manager (AEM) que geram o HTML5 que se adapta a vários tamanhos e orientações de janela. Por exemplo, os seguintes intervalos de larguras do visor correspondem a vários tipos de dispositivo e orientações

* Largura máxima de 480 pixels (telefone, retrato)
* Largura máxima de 767 pixels (telefone, paisagem)
* Largura entre 768 pixels e 979 pixels (tablet, retrato)
* Largura entre 980 pixels e 1199 pixels (tablet, paisagem)
* Largura de 1200px ou superior (desktop)

Consulte os tópicos a seguir para obter informações sobre como implementar o comportamento de design responsivo:

* [Consultas de mídia](#using-media-queries)
* [Grades de fluidos](#developing-a-fluid-grid)
* [Imagens adaptativas](#using-adaptive-images)

Conforme você projeta, use o **Emulador** barra de ferramentas para visualizar suas páginas para vários tamanhos de tela.

## Antes de desenvolver {#before-you-develop}

Antes de desenvolver o aplicativo AEM que suporta suas páginas da Web, várias decisões de design devem ser tomadas. Por exemplo, você precisa ter as seguintes informações:

* Os dispositivos que você está direcionando
* Os tamanhos do visor de destino
* Os layouts de página para cada tamanho de visor direcionado

### Estrutura do aplicativo {#application-structure}

A estrutura típica do aplicativo de AEM suporta todas as implementações de design responsivas:

* Os componentes da página ficam abaixo `/apps/<application_name>/components`
* Os modelos residem abaixo `/apps/<application_name>/templates`

## Uso de consultas de mídia {#using-media-queries}

As consultas de mídia permitem o uso seletivo de estilos CSS para renderização de página. AEM ferramentas e recursos de desenvolvimento permitem que você implemente consultas de mídia de maneira eficaz e eficiente em seus aplicativos.

O grupo W3C fornece a variável [Consultas de mídia](https://www.w3.org/TR/css3-mediaqueries/) recomendação que descreve esse recurso CSS3 e a sintaxe.

### Criação do arquivo CSS {#creating-the-css-file}

No arquivo CSS, defina consultas de mídia com base nas propriedades dos dispositivos que você está direcionando. A seguinte estratégia de implementação é eficaz para gerenciar estilos para cada query de mídia:

* Use um [Pasta Biblioteca do cliente](clientlibs.md) para definir o CSS montado quando a página é renderizada.
* Defina cada consulta de mídia e os estilos associados em arquivos CSS separados. É útil usar nomes de arquivo que representem os recursos do dispositivo da consulta de mídia.
* Defina estilos comuns a todos os dispositivos em um arquivo CSS separado.
* No arquivo css.txt da pasta Biblioteca do cliente, solicite os arquivos CSS da lista, conforme necessário no arquivo CSS montado.

O [Tutorial WKND](develop-wknd-tutorial.md) O usa essa estratégia para definir estilos no design do site. O arquivo CSS usado pela WKND está localizado em `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.
