---
title: AEM Jornada de criação rápida de site
description: Comece aqui para obter uma jornada guiada através da ferramenta de criação rápida de sites AEM fácil de usar para simplificar o desenvolvimento front-end do seu site AEM e personalizar rapidamente seu site sem conhecimento AEM de back-end.
source-git-commit: 3f1e6153c7f8b94865d10b5ce0f86b37c1f5cfe7
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 1%

---


# AEM Jornada de criação rápida de site {#quick-site-creation-journey}

Comece aqui para obter uma jornada guiada através da ferramenta de criação rápida de sites AEM fácil de usar para simplificar o desenvolvimento front-end do seu site AEM e personalizar rapidamente seu site sem conhecimento AEM de back-end.

>[!CAUTION]
>
>No momento, a ferramenta Criação rápida de site é uma visualização técnica. É disponibilizado para fins de ensaio e avaliação e não se destina à utilização da produção, a menos que acordado com o apoio ao Adobe.

## Introdução {#introduction}

O AEM Sites é um poderoso conjunto de ferramentas para criar e gerenciar experiências digitais. Os autores de conteúdo podem criar experiências digitais facilmente usando o editor de sites e organizar o conteúdo usando o console sites, tudo enquanto podem ver o conteúdo ao vivo, conforme será entregue pelo AEM aos seus públicos-alvo através de canais.

A ferramenta Criação de site rápido AEM permite que não desenvolvedores criem rapidamente um novo site do zero usando modelos de site. Depois de criada, a ferramenta Criação rápida de site também permite a rápida personalização do tema e estilo do site AEM (JavaScript, CSS e recursos estáticos). Isso permite que o desenvolvedor de front-end, que precisa de conhecimento zero sobre AEM, funcione separadamente e em paralelo aos criadores de conteúdo. O administrador do AEM simplesmente baixa o tema do site e o fornece ao desenvolvedor front-end que o personaliza usando suas ferramentas favoritas e, em seguida, confirma as alterações no repositório de código AEM, que é implantado.

Eliminando qualquer conhecimento do desenvolvedor para a criação do site, eliminando AEM requisitos de conhecimento para o desenvolvimento front-end e permitindo que o desenvolvimento de temas continue em paralelo com a criação de conteúdo, a ferramenta AEM Quick Site Creation acelera muito o tempo de implantação do site e aumenta a agilidade de personalização e implantação do site.

## Visão geral do vídeo {#video-overview}

Para obter uma visão geral rápida desse recurso em ação, [podem ver esta introdução de cinco minutos.](https://www.youtube.com/watch?v=NQeQ1jZ7ZBw)

Essa jornada da documentação o levará a todos os recursos do vídeo passo a passo e em detalhes para que você entenda o fluxo de trabalho e possa recriar o processo no seu próprio ambiente.

## jornadas de documentação de AEM {#documentation-journeys}

[Uma Jornada de documentação](/help/journey-documentation/home.md) une vários tópicos e recursos diferentes e talvez complicados ao fornecer uma narrativa que ajude o leitor, que pode ser novo a AEM, compreender e resolver um problema de negócios do início ao fim, assumindo o mínimo de tópico ou conhecimento AEM.

As Jornadas de documentação foram projetadas com princípios de práticas recomendadas, informadas pela última pesquisa Adobe, experiência comprovada de implementação de consultores de Adobe e feedback de projetos de clientes.

Se você quiser saber como o Adobe recomenda como resolver casos de negócios de sites com AEM, o AEM Sites Jornada é o local de início.

## Público {#audience}

Esta jornada apresenta os requisitos, as etapas e a abordagem para personalizar temas da AEM Sites. Seu público-alvo principal é o desenvolvedor front-end, que não precisa de conhecimento de AEM. No entanto, para ilustrar todo o processo, a jornada envolve administradores que devem ter conhecimento básico sobre o AEM Sites e o Cloud Manager. Na prática, várias pessoas podem desempenhar várias funções e essa jornada oferece suporte a perspectivas de administradores e desenvolvedores front-end.

| Persona | Descrição | Função no Jornada |
|---|---|---|
| Desenvolvedor front-end | Personaliza o tema do site | Pega o tema fornecido pelo administrador do AEM e o personaliza para que possa ser implantado no site do AEM. |
| Autor do conteúdo | Cria e gerencia conteúdo que é fornecido como sites | Os Autores de conteúdo criam conteúdo em AEM que é renderizado com o tema personalizado pelo desenvolvedor front-end. |
| Administrador do AEM | Cria um novo site AEM | O administrador do AEM cria um novo site com base em um modelo e, em seguida, fornece ao desenvolvedor de front-end um tema para personalizar. |
| Administrador do Cloud Manager | Cria pipelines e concede acesso | O Administrador do Cloud Manager cria o pipeline de front-end e concede acesso ao desenvolvedor de front-end para poder confirmar personalizações no repositório Git de AEM. |

## A Jornada de Criação de Site Rápido AEM {#the-journey}

Você explorará muitos tópicos nesta jornada. Os artigos a seguir fornecem conhecimento fundamental da criação e personalização de sites AEM usando a ferramenta de Criação rápida de sites e vinculam a documentação técnica detalhada.

|#|Artigo|Descrição|Função responsável| |—|—|—|— |0|AEM Jornada de Criação Rápida de Site|Este documento|Administradores do AEM &amp; Cloud Manager| |1|[Entender o Cloud Manager e o fluxo de trabalho de criação rápida de sites](cloud-manager.md)|Saiba mais sobre o Cloud Manager e como ele se vincula ao novo processo de Criação rápida de sites.|AEM Administrador| |2|[Criar site a partir do modelo](create-site.md)|Saiba como criar rapidamente um novo site AEM usando um modelo de site.|AEM Administrador| |3|[Configurar o pipeline](pipeline-setup.md)|Crie um pipeline de front-end para gerenciar a personalização do tema do site.|Administrador do Cloud Manager| |4|[Conceder acesso ao desenvolvedor de front-end](grant-access.md)|Integrar os desenvolvedores de front-end no Cloud Manager para que eles tenham acesso ao repositório e pipeline de git do site AEM.|Administrador do Cloud Manager| |5|[Recuperar informações de acesso do repositório Git](retrieve-access.md)|Saiba como o desenvolvedor de front-end usa o Cloud Manager para acessar informações de repositório Git.|Desenvolvedor front-end| |6|[Personalizar o tema do site](customize-theme.md)|Saiba como um tema de site é criado, como personalizá-lo e como testá-lo usando conteúdo de AEM ao vivo.|Desenvolvedor front-end| |7|[Implantar o tema personalizado](deploy-theme.md)|Saiba como implantar o tema do site usando o pipeline.|Desenvolvedor front-end|

## O que vem a seguir {#what-is-next}

Agora você está pronto para começar a usar a jornada de criação de site rápido do Adobe.

* Se você for um administrador do AEM ou do Cloud Manager, ou se atender às funções de desenvolvedor front-end e de administrador, ou se quiser apenas entender o processo completo no AEM, comece no início da jornada com [Entender o Cloud Manager](cloud-manager.md) conforme estabelecido abaixo.
* Se você for responsável apenas pelo desenvolvimento de front-end e interagir com os administradores do AEM e do Cloud Manager, pule diretamente para [Recuperar informações de acesso do repositório Git](retrieve-access.md) para obter acesso ao repositório Git AEM e começar a personalizar.
* Se você já entende que o AEM Sites e o Cloud Manager trabalham juntos e querem começar diretamente com a configuração, você pode [pule diretamente para criar um novo site a partir de um modelo.](create-site.md)

## Recursos adicionais {#additional-resources}

Confira estes recursos adicionais para obter mais informações sobre como AEM recursos avançados trabalham juntos.

* [AEM documentação técnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=pt-BR) - Se já tiver um conhecimento profundo da AEM, poderá consultar diretamente os documentos técnicos aprofundados.
* [Documentação de administração do site](/help/sites-cloud/administering/site-creation/create-site.md) - Consulte os documentos técnicos sobre a criação do site para obter mais detalhes sobre os recursos da ferramenta de Criação rápida de sites.
