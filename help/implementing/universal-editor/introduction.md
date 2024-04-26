---
title: Introdução ao Editor universal
description: Saiba como o Editor universal habilita a edição "o que você vê é o que você obtém" (WYSIWYG) de qualquer experiência headless e headful. Entenda como ele pode ajudar criadores de conteúdo a entregar experiências excepcionais, aumentar a velocidade do conteúdo e como ele oferece uma experiência de desenvolvedor de última geração.
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
source-git-commit: bbcf44c585e98f75c558d06edc3c1c030adad2cf
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 63%

---


# Introdução ao Editor universal {#introduction}

O Universal Editor é um editor visual versátil que faz parte do Adobe Experience Manager Sites. Ele permite que os autores façam a edição &quot;o que você vê é o que você obtém&quot; (WYSIWYG) de qualquer experiência headless ou headful. Entenda como ele pode ajudar os autores de conteúdo a fornecer experiências excepcionais e como oferece liberdade inigualável para desenvolvedores.

## Segundo plano {#background}

O Editor universal fornece uma experiência de criação em contexto eficiente e intuitiva que requer treinamento mínimo. Com ele, os autores podem gerenciar o conteúdo diretamente no contexto da experiência online, exatamente como ele aparecerá para os visitantes. Por ser um verdadeiro editor como um serviço e, em geral, mais flexível, ele pretende eventualmente substituir o Editor de páginas.

Os autores se beneficiam da flexibilidade do Editor universal, pois ele oferece suporte à mesma edição visual consistente para todas as formas de conteúdo AEM: a edição no local e a composição de layout são possíveis também para fragmentos de conteúdo e componentes de página. As duas formas de conteúdo podem até ser editadas ao serem exibidas lado a lado em uma experiência da Web, sem que os autores precisem alternar o contexto. Essa é uma melhora tremenda em comparação aos editores anteriores no AEM que suportavam apenas um tipo de conteúdo.

Os desenvolvedores se beneficiam da versatilidade do Universal Editor, pois ele também oferece suporte à verdadeira dissociação da implementação. Ele permite que os desenvolvedores utilizem praticamente qualquer estrutura ou arquitetura de sua escolha, sem impor restrições de SDK ou tecnologia. Essa flexibilidade até facilita a instrumentação de aplicativos web existentes para o editor universal sem precisar rearquitetá-los.

## É realmente universal {#universal}

O Editor universal pode ser utilizado em qualquer implementação, para qualquer aspecto de qualquer conteúdo.

![Isso o torna universal](assets/universal.png)

### Qualquer implementação {#any-implementation}

Visto que é possível criar experiências de diferentes maneiras, qualquer implementação pode utilizar o Editor Universal para que os autores possam realizar edições com contexto.

Muitos usuários acreditam que uma implementação headless limita a edição de todo o conteúdo dos autores a uma interface baseada em formulários, mas isso não acontece no Editor Universal

Os requisitos para uma implementação utilizar o Editor Universal são bastante simples e são compatíveis com:

* **Qualquer arquitetura** - Renderização do lado do servidor, renderização da borda, renderização do lado do cliente e assim por diante.
* **Qualquer estrutura** - AEM Baunilla, ou qualquer estrutura de terceiros como React, Next.js, Angular e assim por diante.
* **Qualquer hospedagem**: é possível hospedar localmente no AEM ou em um domínio remoto

### Qualquer conteúdo {#any-content}

Um autor de conteúdo deve ter a mesma experiência avançada oferecida no editor de páginas do AEM. Mas o Editor universal permite que os autores editem **qualquer** conteúdo de forma visual e com contexto, o que abrange:

* **Estruturas de página do AEM**: `cq:Components` aninhados de `cq:Pages`, incluindo fragmentos de experiência.
* **Fragmentos de conteúdo do AEM**: é possível editar o conteúdo dos fragmentos de conteúdo conforme aparecem no contexto da experiência.
* **Documentos**: a prova de conceitos mostrou que os documentos do Word, Excel, Google Docs ou Markdown também podem ser editados da mesma maneira (trata-se do WIP).

### Qualquer aspecto {#any-aspect}

Para um autor, o conteúdo não envolve apenas as informações contidas, mas também a forma como elas são apresentadas e recebidas. O conteúdo vem com metadados e regras de instrumentação adicionais, que o Editor universal pode entender e editar, incluindo:

* **Aplicar layout e estilo** - Ao usar um sistema de estilos, o profissional de marketing e o autor de conteúdo podem aplicar estilos diferentes ao conteúdo e criar layouts diferentes para o conteúdo, como colunas, carrosséis, guias, acordeões e assim por diante.

## Valor {#value}

Ao separar a experiência de edição de conteúdo de qualquer sistema de entrega de conteúdo específico, o editor se torna realmente universal e flexível, permitindo que o autor de conteúdo entregue experiências excepcionais, aumente a velocidade do conteúdo e forneça uma experiência de desenvolvimento de última geração.

![O valor do Editor universal](assets/value.png)

* **Entrega de experiências excepcionais**: com o objetivo de habilitar os profissionais a criar um experiência atrativa para os visitantes, o Editor Universal permite a criação e a edição do conteúdo no contexto da visualização. Isso permite que eles criem um conteúdo que se ajuste ao design, possibilitando uma experiência significativa para os visitantes.
* **Aumento da velocidade do conteúdo**: para simplificar a administração do fluxo de trabalho, o Editor universal permite editar o conteúdo da visualização a fim de orientar os profissionais, mostrando apenas as opções que são relevantes para o contexto e tornando o fluxo de trabalho independente das fontes de conteúdo.
* **Experiência de desenvolvedor de última geração**: para se adequar ao atual cenário heterogêneo dos aplicativos, o Editor universal é completamente independente e não favorece tecnologias específicas, permitindo que os desenvolvedores utilizem sua tecnologia preferida para implementar a experiência.

## Editor universal e o editor de fragmento de conteúdo {#universal-editor-content-fragment-editor}

À primeira vista, pode parecer que o Editor universal e o Editor de fragmento de conteúdo fornecem recursos de edição semelhantes. No entanto, esses editores oferecem recursos muito diferentes e cuidam de tarefas distintas do profissional de marketing.

### Editor de fragmento de conteúdo {#content-fragment-editor}

Para um profissional de marketing que deseja criar conteúdo sem precisar se preocupar com o layout, de maneira que ele possa ser reutilizado em vários contextos da experiência.

* O foco é dimensionar a estratégia de conteúdo.

### Editor universal {#universal-editor}

Para um profissional de marketing que deseja criar um conteúdo adaptado ao layout de um contexto específico, a fim de fornecer uma experiência excepcional.

* O foco é estabelecer uma conexão convincente com os leitores.

## Recursos adicionais {#additional-resources}

Para saber mais sobre o Editor universal, consulte estes documentos.

* [Criação de conteúdo com o Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md): saiba como é fácil e intuitivo para os autores criarem conteúdo utilizando o Editor universal.
* [Publicar conteúdo com o editor universal](/help/sites-cloud/authoring/universal-editor/publishing.md) - Saiba como o Editor Universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.
* [Introdução ao Editor universal no AEM](getting-started.md): saiba como obter acesso ao Editor universal e começar a instrumentar seu primeiro aplicativo do AEM para utilizá-lo.
* [Arquitetura do Editor universal](architecture.md): saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.
* [Atributos e tipos](attributes-types.md): saiba mais sobre os atributos e tipos de dados exigidos pelo Editor universal.
* [Autenticação do Editor universal](authentication.md): saiba como funciona a autenticação do Editor universal.
