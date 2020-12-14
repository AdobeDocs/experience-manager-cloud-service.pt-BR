---
title: Design responsivo
description: Com o design responsivo, as mesmas experiências podem ser exibidas com eficiência em vários dispositivos em várias orientações
translation-type: tm+mt
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Design responsivo {#responsive-design}

Projete suas experiências para que elas se adaptem ao visor do cliente no qual são exibidas. Com o design responsivo, as mesmas páginas podem ser exibidas com eficiência em vários dispositivos em ambas as orientações. A imagem a seguir demonstra algumas maneiras pelas quais uma página pode responder às alterações no tamanho do visor:

* Layout: Use layouts de coluna única para visualizações menores e layouts de várias colunas para visualizações maiores.
* Tamanho do texto: Use um tamanho de texto maior (quando apropriado, como cabeçalhos) em visualizações maiores.
* Conteúdo: Inclua somente o conteúdo mais importante ao exibir em dispositivos menores.
* Navegação: Ferramentas específicas do dispositivo são fornecidas para acessar outras páginas.
* Imagens: Servindo representações de imagem apropriadas para o visor cliente de acordo com as dimensões da janela.

![Exemplos de design responsivo](assets/responsive-example.png)

Desenvolva aplicativos Adobe Experience Manager (AEM) que gerem HTML5 que se adaptem a vários tamanhos de janela e orientações. Por exemplo, os seguintes intervalos de larguras do visor correspondem a vários tipos de dispositivos e orientações

* Largura máxima de 480 pixels (telefone, retrato)
* Largura máxima de 767 pixels (telefone, paisagem)
* Largura entre 768 pixels e 979 pixels (tablet, retrato)
* Largura entre 980 pixels e 1199 pixels (tablet, paisagem)
* Largura de 1200px ou superior (desktop)

Consulte os seguintes tópicos para obter informações sobre como implementar o comportamento de design responsivo:

* [Query de mídia](#using-media-queries)
* [Grades fluidas](#developing-a-fluid-grid)
* [Imagens adaptativas](#using-adaptive-images)

Ao projetar, use a barra de ferramentas **Emulador** para pré-visualização das páginas para vários tamanhos de tela.

## Antes de desenvolver {#before-you-develop}

Antes de desenvolver o aplicativo AEM que suporta suas páginas da Web, várias decisões de design devem ser tomadas. Por exemplo, você precisa ter as seguintes informações:

* Os dispositivos direcionados
* Os tamanhos do visor do público alvo
* Os layouts de página para cada tamanho de visor direcionado

### Estrutura do aplicativo {#application-structure}

A estrutura típica do aplicativo AEM suporta todas as implementações responsivas de design:

* Os componentes da página ficam abaixo de `/apps/<application_name>/components`
* Os modelos residem abaixo de `/apps/<application_name>/templates`

## Usando Query de mídia {#using-media-queries}

Os query de mídia permitem o uso seletivo de estilos CSS para renderização de página. AEM ferramentas e recursos de desenvolvimento permitem implementar query de mídia em seus aplicativos de modo eficiente e eficiente.

O grupo W3C fornece a recomendação [Query de mídia](https://www.w3.org/TR/css3-mediaqueries/) que descreve esse recurso CSS3 e a sintaxe.

### Criação do arquivo CSS {#creating-the-css-file}

No arquivo CSS, defina query de mídia com base nas propriedades dos dispositivos que você está definindo como meta. A seguinte estratégia de implementação é eficaz para gerenciar estilos para cada query de mídia:

* Use uma [pasta Biblioteca do cliente](clientlibs.md) para definir o CSS que é montado quando a página é renderizada.
* Defina cada query de mídia e os estilos associados em arquivos CSS separados. É útil usar nomes de arquivos que representem os recursos do dispositivo do query de mídia.
* Defina estilos comuns a todos os dispositivos em um arquivo CSS separado.
* No arquivo css.txt da pasta Client Library, solicite os arquivos CSS de lista, conforme necessário, no arquivo CSS montado.

O tutorial [WKND](develop-wknd-tutorial.md) usa essa estratégia para definir estilos no design do site. O arquivo CSS usado pelo WKND está localizado em `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.
