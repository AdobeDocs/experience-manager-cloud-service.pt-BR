---
title: Jornada de criação rápida de site do AEM
description: Comece aqui uma jornada guiada através da ferramenta fácil de usar de Criação rápida de sites do AEM para simplificar o desenvolvimento de front-end do seu site e personalizá-lo rapidamente sem nenhum conhecimento de back-end no AEM.
exl-id: b8218232-0298-4b16-9dab-fa59be592a24
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 87%

---

# Jornada de criação rápida de site do AEM {#quick-site-creation-journey}

Comece aqui uma jornada guiada através da ferramenta fácil de usar de Criação rápida de sites do AEM para simplificar o desenvolvimento de front-end do seu site e personalizá-lo rapidamente sem nenhum conhecimento de back-end no AEM.

## Introdução {#introduction}

O AEM Sites é um avançado conjunto de ferramentas para criar e gerenciar experiências digitais. Autores de conteúdo podem criar experiências digitais facilmente usando o editor de sites e organizar o conteúdo usando o console Sites, tudo isso enquanto visualizam o conteúdo em tempo real conforme é entregue pelo AEM aos seus públicos entre canais.

A ferramenta de Criação rápida de sites do AEM permite que não desenvolvedores criem um novo site do zero rapidamente usando modelos. Depois de criada, a ferramenta de Criação rápida de sites também permite a personalização rápida do tema e estilo do site do AEM (JavaScript, CSS e recursos estáticos). Isso permite que o desenvolvedor de front-end, que não precisa ter nenhum conhecimento sobre o AEM, funcione separadamente e em paralelo aos criadores de conteúdo. O administrador do AEM simplesmente baixa o tema do site e o fornece ao desenvolvedor de front-end, que o personaliza usando suas ferramentas favoritas e, em seguida, confirma as alterações no repositório de código do AEM, que é então implantado.

Eliminando a necessidade de qualquer conhecimento de desenvolvedor para a criação de sites e dos requisitos de conhecimento do AEM para o desenvolvimento de front-end, e permitindo que o desenvolvimento de temas continue em paralelo à criação de conteúdo, a ferramenta de Criação rápida de sites do AEM acelera o rendimento do site e aumenta a agilidade da personalização e implantação.

## Visão geral do vídeo {#video-overview}

Para obter uma visão geral rápida desse recurso em ação, [assista a esta introdução de cinco minutos.](https://www.youtube.com/watch?v=NQeQ1jZ7ZBw)

Essa jornada de documentação o conduzirá através de todos os recursos no vídeo passo a passo e em detalhes para que você entenda o fluxo de trabalho e possa recriar o processo no seu próprio ambiente.

## Jornadas de documentação do AEM {#documentation-journeys}

[Uma Jornada de documentação](/help/journey-documentation/documentation-journeys.md) une vários tópicos e recursos diferentes e talvez complicados, fornecendo uma narrativa que ajuda o leitor, que pode ser novo no AEM, a entender e resolver um problema da empresa do começo ao fim, assumindo o mínimo de conhecimento prévio do tópico ou do AEM.

As Jornadas de documentação foram projetadas com princípios de práticas recomendadas, informadas pela última pesquisa da Adobe, experiência comprovada de implementação dos consultores da Adobe e feedback de projetos de clientes.

Se quiser saber como a Adobe recomenda resolver casos de negócios de sites com o AEM, as jornadas do AEM Sites são um ótimo ponto de partida.

## Público {#audience}

Esta jornada apresenta os requisitos, as etapas e a abordagem para personalizar temas do AEM Sites. Seu público principal é o desenvolvedor de front-end, que não precisa de conhecimento do AEM. No entanto, para ilustrar todo o processo, a jornada envolve administradores que devem ter conhecimento básico sobre o AEM Sites e o Cloud Manager. Na prática, várias pessoas podem desempenhar várias funções e essa jornada considera as perspectivas de administradores e desenvolvedores de front-end.

| Perfil | Descrição | Função na jornada |
|---|---|---|
| Desenvolvedor front-end | Personaliza o tema do site | Pega o tema fornecido pelo administrador do AEM e o personaliza para que possa ser implantado no site do AEM. |
| Autor de conteúdo | Cria e gerencia conteúdo que é entregue como site | Os autores de conteúdo criam conteúdo no AEM que é renderizado com o tema personalizado pelo desenvolvedor de front-end. |
| Administrador do AEM | Cria um novo site do AEM | O administrador do AEM cria um novo site com base em um modelo e, em seguida, fornece ao desenvolvedor de front-end um tema para personalizar. |
| Administrador do Cloud Manager | Cria pipelines e concede acesso | O administrador do Cloud Manager cria o pipeline de front-end e concede acesso ao desenvolvedor de front-end para poder confirmar personalizações no repositório Git do AEM. |

## Jornada de Criação rápida de sites do AEM {#the-journey}

Muitos tópicos serão explorados nesta jornada. Os artigos a seguir fornecem conhecimentos fundamentais sobre criação e personalização do AEM Sites usando a ferramenta de Criação rápida de sites, além de oferecer links para documentação técnica detalhada.

| # | Artigo | Descrição | Função de responsabilidade |
|---|---|---|--|
| 0 | Jornada de criação rápida de site do AEM | Este documento | Administradores do AEM e Cloud Manager |
| 1 | [Entenda o Cloud Manager e o fluxo de trabalho de Criação rápida de sites](cloud-manager.md) | Saiba mais sobre o Cloud Manager e como ele se vincula ao novo processo de criação rápida de sites. | Administrador do AEM |
| 2 | [Criar site a partir de modelo](create-site.md) | Saiba como criar rapidamente um novo site do AEM usando um modelo de site. | Administrador do AEM |
| 3 | [Configurar o seu pipeline](pipeline-setup.md) | Crie um pipeline de front-end para gerenciar a personalização do tema do seu site. | Administrador do Cloud Manager |
| 4 | [Conceder acesso ao desenvolvedor de front-end](grant-access.md) | Integre os desenvolvedores de front-end no Cloud Manager para que eles tenham acesso ao repositório do Git e pipeline de site do AEM. | Administrador do Cloud Manager |
| 5 | [Recuperar informações de acesso do repositório Git](retrieve-access.md) | Saiba como o desenvolvedor de front-end usa o Cloud Manager para acessar informações do repositório Git. | Desenvolvedor front-end |
| 6 | [Personalizar o tema do site](customize-theme.md) | Saiba como um tema de site é criado, como personalizá-lo e como testá-lo usando conteúdo dinâmico de AEM. | Desenvolvedor front-end |
| 7 | [Implantar o tema personalizado](deploy-theme.md) | Saiba como implantar o tema do site usando o pipeline. | Desenvolvedor front-end |

## O que vem a seguir {#what-is-next}

Agora você está pronto para começar a usar a jornada de Criação rápida de sites da Adobe.

* Se você for um administrador do AEM ou do Cloud Manager; se ocupa ambas as funções de desenvolvedor de front-end e de administrador; ou se quiser apenas entender o processo do AEM de ponta a ponta, comece no início da jornada com [Entender o Cloud Manager](cloud-manager.md) conforme estabelecido a seguir.
* Se você for responsável apenas pelo desenvolvimento de front-end e vai interagir com os administradores do AEM e do Cloud Manager, pule diretamente para [Recupere informações de acesso do repositório Git](retrieve-access.md) para obter acesso ao repositório Git do AEM e começar a personalizar.
* Se você já entende que o AEM Sites e o Cloud Manager trabalham juntos e quer começar diretamente com a configuração, pode [pular diretamente para a criação de um novo site a partir de um modelo.](create-site.md)

## Recursos adicionais {#additional-resources}

Confira estes recursos adicionais para obter mais informações sobre como os recursos avançados do AEM trabalham juntos.

* [Documentação técnica do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=pt-BR) - Se já tiver um conhecimento profundo do AEM, poderá consultar diretamente os documentos técnicos aprofundados.
* [Documentação de administração do site](/help/sites-cloud/administering/site-creation/create-site.md) - Consulte os documentos técnicos sobre a criação de sites para obter mais detalhes sobre os recursos da ferramenta de Criação rápida de sites.
