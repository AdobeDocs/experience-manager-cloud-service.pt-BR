---
title: Práticas recomendadas de tradução
description: Saiba mais sobre as práticas recomendadas compiladas pelas equipes de engenharia de Adobe e consultoria para ajudá-lo a trabalhar com projetos de tradução.
feature: Language Copy
role: Admin
exl-id: 51b98c24-5566-4088-9010-bd39841a1633
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 1%

---

# Práticas recomendadas de tradução {#translation-best-practices}

>[!TIP]
>
>Se você é novo em traduzir conteúdo, consulte nosso [Jornada de tradução de sites,](/help/journey-sites/translation/overview.md) que é o caminho orientado pela tradução do conteúdo do AEM Sites usando as ferramentas de tradução avançadas do AEM, ideais para aqueles sem experiência de AEM ou tradução.

## Geral {#general}

Criar ou expandir uma presença global na Web pode ser um processo complexo, mas com boas AEM de previsão e planejamento pode simplificar seus esforços e apoiar suas metas globais de negócios.

* **Plano de expansão global** antes de implementar seu primeiro site. Adaptar um site existente para cobertura global quando o site foi implementado em um curto prazo normalmente é mais difícil do que planejar a expansão global no início:
   * Avalie o estado atual da maturidade de localização da sua organização. Determine se você tem a variável **ferramentas**, **processos** e **recursos** em vigor para suportar a expansão global.
   * Esteja ciente de **regulamentos globais** e **preferências de língua regional**. Projete estruturas e processos de conteúdo flexíveis que possam acomodar um ambiente de negócios global em constante mudança.
* Determine um **governança** modelo que suporta seus negócios globais e usa mecanismos AEM como MSM e permissões de usuário para impor seu modelo escolhido. Por exemplo, determine se o conteúdo será criado centralmente e &quot;enviado&quot; ou &quot;enviado&quot; para regiões/países. Determine qual conteúdo pode ser desbloqueado e alterado nas regiões geográficas. Determine quem é responsável por iniciar e gerenciar traduções.
* Se os recursos permitirem, é melhor gerenciar a atividade de tradução de uma equipe central que pode desenvolver conhecimento especializado nas ferramentas, processos e relacionamentos de fornecedores necessários.
* **Plano**, **protótipo** e **teste** sua estrutura e processos globais para garantir que eles suportem os negócios e que você tenha o suporte necessário das partes interessadas nas regiões geográficas.

## Estrutura do site  {#site-structure}

* Ao projetar a estrutura do site, comece examinando o conteúdo e determine onde e em qual idioma o conteúdo é criado. Esse local deve ser o nível superior do site.
* A prática recomendada é uma **estrutura baseada em idiomas** com até três níveis entre a criação de nível superior e os sites de países.
* Use uma convenção de nomenclatura de site de idioma/país que segue **[Padrões W3C.](/help/sites-cloud/authoring/fundamentals/accessible-content.md)**
* Determine como o conteúdo é distribuído por regiões e países. Considere quais países compartilham idiomas. É recomendável criar matrizes de idioma, uma camada de páginas não ativadas, em que o conteúdo traduzido pode ser revisado e modificado, depois enviado ou extraído para um site do país que compartilha esse idioma.
* Há duas abordagens para a criação de mestres em linguagem: usando cópias de idioma e cópias ativas do MSM/Live.
   * A abordagem de cópia de idioma é a utilizada AEM estrutura de integração de tradução pronta para uso, e portanto é a maneira mais fácil de começar. A estrutura fornece uma interface de usuário que facilita inicialmente a propagação e tradução de alterações de conteúdo do idioma principal (por exemplo, inglês) principal para o domínio do idioma. No entanto, à medida que o projeto cresce, a automação do fluxo de trabalho torna-se cada vez mais necessária para gerenciar a tradução do maior número de páginas e/ou idiomas.
   * A abordagem MSM/live copy pode ser uma alternativa para casos de uso avançados, em que os sites são maiores e mais complexos. Governança forte e automação de fluxo de trabalho são necessárias desde o início para lidar com os complexos relacionamentos de herança entre os mestres em inglês e idioma, e para reduzir o risco de sobreposição de traduções existentes. Essa manipulação pode ser realizada com a ajuda de alguns conectores de tradução. Consulte [MSM e sites multilíngues](/help/sites-cloud/administering/msm/best-practices.md#msm-and-multilingual-websites) para obter mais informações.
* Se seu idioma principal tiver variações globais, uma opção é usar o MSM para criar uma live copy a partir do principal global para usar na tradução. Por exemplo, se a criação global for realizada em um principal de inglês dos EUA, crie um principal de inglês internacional como uma live copy e base para a tradução para outros idiomas.
* Use o MSM para criar sites de países a partir dos mestres de idioma traduzido e implantar conteúdo em sites que compartilhem o mesmo idioma. Por exemplo, o idioma francês principal pode ser distribuído para sites da França, Bélgica e Suíça.
* Planejar, protótipo e testar primeiro, antes de iniciar a implementação.

## Processos e métodos de tradução {#translation-processes-and-methods}

* Envolver um **provedor de serviços de localização (LSP)** com conhecimentos especializados em tradução e atividades de localização relacionadas. Os LSPs podem ajudar a ampliar seus negócios globais fornecendo uma ampla variedade de recursos e tecnologias para melhorar a eficiência e economizar custos de tradução:
   * Alguns LSPs são provedores de serviços e tecnologia. Há também provedores independentes de tecnologia que permitem que muitos LSPs participem de suas plataformas de tradução.
   * O **Estrutura de tradução AEM** O apoia a integração com uma variedade de fornecedores de tecnologia de tradução para tradução automática e humana.
   * Saiba como [integrar conectores LSP ao seu sistema de AEM](integration-framework.md) para automatizar a tradução de conteúdo ou como criar, exportar e importar manualmente Projetos de tradução para testes e nos casos em que não há LSP ou provedor de tecnologia de tradução.
* Escolha um **método de tradução** que melhor se adapta ao conteúdo.
   * **Tradução humana** O é mais adequado para conteúdo em que as mensagens e as expectativas de qualidade são altas e o conteúdo permanecerá por algum tempo no site, como as páginas de Marketing.
   * **Tradução da máquina** pode ser uma boa escolha para volumes em massa de tradução quando o tempo para publicar é crítico, as expectativas de qualidade estão atenuadas ou os custos de tradução humana são proibitivos. A base de conhecimento de suporte e o conteúdo gerado pelo usuário geralmente são traduzidos por máquina.
* Conte com a experiência dos provedores de serviços de localização, da Adobe Consulting e dos Integradores de sistemas para planejar, protótipo e testar sua estrutura multilíngue do site.
