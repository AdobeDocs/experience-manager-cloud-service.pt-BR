---
title: Introdução ao Editor Visual Universal
description: Saiba como o Editor Visual Universal (também conhecido como Editor Universal) permite a edição do que você vê é o que você obtém (WYSIWYG) de qualquer experiência headless e headful. Entenda como ele pode ajudar os autores de conteúdo a entregar experiências excepcionais, aumentar a velocidade do conteúdo e como ele oferece uma experiência de desenvolvedor avançada.
source-git-commit: f242abbd7f53c523667d1d56a0f5b913bb26dee0
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 0%

---


# Introdução ao Editor Visual Universal {#introduction}

Saiba como o Editor Visual Universal (também conhecido como Editor Universal) permite a edição do que você vê é o que você obtém (WYSIWYG) de qualquer experiência headless e headful. Entenda como ele pode ajudar os autores de conteúdo a entregar experiências excepcionais, aumentar a velocidade do conteúdo e como ele oferece uma experiência de desenvolvedor avançada.

## Segundo plano {#background}

A ferramenta mais poderosa para o autor de conteúdo AEM foi o editor de páginas. O editor de páginas oferece uma experiência de criação WYSIWYG intuitiva e visual no contexto, que requer um treinamento mínimo e mostra aos autores exatamente como o conteúdo será exibido.

No entanto, o editor de páginas só pode editar AEM conteúdo da página, estrutura e os componentes contidos nela. O conteúdo atual, no entanto, raramente é proveniente de um local. O Editor universal oferece a mesma experiência de edição no local que o editor de página, mas para qualquer aspecto de conteúdo em qualquer implementação.

## Verdadeiramente Universal {#universal}

O Editor universal pode ser instrumentado para qualquer implementação, para qualquer conteúdo e para qualquer aspecto do conteúdo.

![O que torna universal](assets/universal.png)

### Qualquer implementação {#any-implementation}

Como as experiências podem ser criadas de várias maneiras diferentes, qualquer implementação pode aproveitar o Editor universal para que os autores possam realizar a edição no contexto.

Os usuários geralmente acham que uma implementação sem cabeçalho limita os autores a editar todo o conteúdo em uma interface do usuário baseada em formulário, mas isso não é verdade com o Editor Universal

Os requisitos para uma implementação aproveitar o Editor Universal são muito diretos e são compatíveis:

* **Qualquer arquitetura** - Renderização do lado do servidor, renderização do lado da borda, renderização do lado do cliente etc.
* **Qualquer estrutura** - Vanilla AEM ou qualquer estrutura de terceiros como React, Next.js, Angular etc.
* **Qualquer hospedagem** - Pode ser hospedado localmente para AEM ou em um domínio remoto

### Qualquer conteúdo {#any-content}

Um autor de conteúdo deve ter a mesma experiência de edição avançada anteriormente oferecida pelo editor de página de AEM. Mas o Editor universal permite que os autores de conteúdo editem **any** conteúdo visualmente e em contexto e suporte:

* **AEM Estruturas de Página** - Aninhado `cq:Components` de `cq:Pages`, incluindo Fragmentos de experiência
* **Fragmentos de conteúdo do AEM** - Edite o conteúdo dos Fragmentos de conteúdo conforme eles aparecem no contexto da experiência.
* **Documentos** - A prova de conceitos mostrou que também os documentos do Word, Excel, Google Docs ou Markdown também podem ser editados da mesma maneira (trata-se do WIP).

### Qualquer aspecto {#any-aspect}

Para um autor de conteúdo, o conteúdo não é apenas sobre as informações contidas, mas sobre como é renderizado e recebido. O conteúdo vem com metadados e regras de instrumentação adicionais, que o Editor Universal pode entender e editar, incluindo:

* **Aplicar layout e estilo** - Ao usar um sistema de estilos, o profissional de marketing e o autor de conteúdo podem aplicar estilos diferentes ao conteúdo e criar layouts diferentes para o conteúdo, como colunas, carrosséis, guias, acordeões etc.

## Valor {#value}

Ao dissociar a experiência de edição de conteúdo de qualquer sistema de entrega de conteúdo específico, o editor se torna realmente universal e flexível, permitindo que o autor de conteúdo forneça experiências excepcionais, aumente a velocidade do conteúdo e forneça uma experiência de desenvolvedor de última geração.

![O valor do Editor Universal](assets/value.png)

* **Fornecer experiências excepcionais** - Para permitir que os profissionais criem uma experiência atraente para os visitantes, o Editor Universal permite que os profissionais criem e editem o conteúdo no contexto da visualização. Isso permite que eles criem conteúdo que se ajuste ao design da experiência e que constitua uma jornada significativa para os visitantes.
* **Aumentar a velocidade do conteúdo** - Para simplificar o fluxo de trabalho de gerenciamento dos profissionais, o Editor Universal permite que o conteúdo de edição na pré-visualização seja exibido para os profissionais de guia, mostrando apenas as opções relevantes para esse contexto e tornando o fluxo de trabalho independente das fontes de conteúdo.
* **Experiência de desenvolvedor avançada** - Para oferecer suporte ao cenário de aplicativos heterogêneos do mundo real, o Editor Universal é completamente dissociado e independente da tecnologia, permitindo que os desenvolvedores usem sua pilha de tecnologia preferida para implementar a experiência.

## Editor visual universal e o editor de fragmento de conteúdo {#universal-editor-content-fragment-editor}

À primeira vista, pode parecer que o Editor visual universal e o Editor de fragmento de conteúdo fornecem recursos de edição semelhantes. No entanto, esses editores oferecem recursos muito diferentes e realizam trabalhos diferentes do profissional de marketing.

### Editor de fragmento de conteúdo {#content-fragment-editor}

Um profissional de marketing deseja criar conteúdo sem precisar se preocupar com seu layout, para que ele possa ser reutilizado em vários contextos da experiência.

* O trabalho subjacente a ser realizado é dimensionar a estratégia de conteúdo.

### Editor visual universal {#universal-editor}

Um profissional de marketing deseja criar conteúdo adaptado ao layout de um contexto específico para fornecer uma experiência excepcional.

* O trabalho subjacente a realizar é estabelecer uma conexão convincente com os leitores.

## Roteiro {#road-map}

É importante observar que o Universal Editor é um trabalho em andamento e alguns dos recursos apresentados neste documento são uma visão do editor final e não necessariamente representativa de suas capacidades atuais.

Fale com o seu Adobe para obter detalhes sobre os recursos futuros planejados para o Universal Editor.

## Recursos adicionais {#additional-resources}

Para saber mais sobre o Universal Editor, consulte estes documentos.

* [Criação de conteúdo com o editor universal](authoring.md) - Saiba como é fácil e intuitivo para os autores de conteúdo criar conteúdo usando o Editor Universal.
* [Introdução ao Editor universal no AEM](getting-started.md) - Saiba como obter acesso ao Universal Editor e como começar a instrumentar seu primeiro aplicativo AEM para usá-lo.
* [Arquitetura do editor universal](architecture.md) - Saiba mais sobre a arquitetura do Editor Universal e como os dados fluem entre seus serviços e camadas.
* [Atributos e tipos](attributes-types.md) - Saiba mais sobre os atributos e tipos de dados exigidos pelo Editor Universal.
* [Autenticação do editor universal](authentication.md) - Saiba como o Editor Universal se autentica.
