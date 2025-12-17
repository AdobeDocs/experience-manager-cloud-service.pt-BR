---
title: Agente de otimização de conteúdo
description: Saiba como usar o Agente de otimização de conteúdo para transformar como os usuários refinam e adaptam ativos aplicando instruções de linguagem natural para criar variações prontas para canal.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 3f44e74488fc73c406fefb6decc41782859d029b
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# Agente de otimização de conteúdo {#content-optimization-agent}

O Agente de otimização de conteúdo transforma o modo como os usuários refinam e adaptam ativos aplicando instruções de linguagem natural para criar variações prontas para canal. Seja gerando novas representações, ajustando propriedades visuais, alterando planos de fundo ou preparando ativos para canais digitais específicos, o agente interpreta a intenção do usuário e executa tarefas de edição complexas automaticamente. Ele funciona perfeitamente com o Discovery Agent, pegando os ativos encontrados e produzindo variações otimizadas usando o [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) que atendem aos requisitos de marca, canal e campanha sem esforço manual de design.

Alguns dos principais benefícios da otimização de conteúdo incluem:

* **Transformação sem esforço de ativos**: converte prompts simples e conversacionais em operações de imagem precisas, como redimensionamento, nitidez, espelhamento ou recoloração, eliminando a necessidade de ferramentas de edição especializadas.

* **Saídas otimizadas para canal**: produz rapidamente representações personalizadas para plataformas específicas, como Instagram Stories, banners da Web ou outros pontos de contato de marketing, garantindo que os ativos estejam prontos para uso imediato.

* **Aprimoramento do Creative em escala**: aplica ajustes visuais e aprimoramentos, como alterações no plano de fundo ou sobreposições gráficas, para oferecer suporte a fluxos de trabalho criativos de alto volume sem retardar as equipes.

* **[Colaboração perfeita com o Discovery Agent](/help/ai-in-aem/agents/discovery/overview.md)**: baseia-se nos ativos identificados pelo Discovery Agent, permitindo recuperação e otimização completas de ativos por meio de conversação natural.

>[!IMPORTANT]
>
>As respostas geradas por IA podem ser imprecisas ou enganosas. Verifique as correções e respostas sugeridas.
>
>Consulte também [Diretrizes de usuário da IA gerativa da Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Pré-requisitos {#prerequisites-content-optimization-agent}

Para gerar variações ou otimizações para ativos de imagem. Você deve ter:

* Uma licença válida do Dynamic Media

* Dynamic Media com OpenAPI ativada no ambiente do AEM as a Cloud Service.

* Os ativos no [estado aprovado](/help/assets/manage-organize-assets-view.md#manage-asset-status) em seu ambiente do AEM as a Cloud Service.


## Habilidades {#skills-content-optimization-agent}

O Agente de otimização de conteúdo oferece as seguintes habilidades:

* **Entender a intenção através da linguagem natural**

  O Agente de otimização de conteúdo interpreta a intenção do usuário a partir de prompts em linguagem natural, contabilizando o canal, a campanha e o contexto de público-alvo para determinar as ações de otimização mais relevantes.

* **Gera variantes de conteúdo dinâmico**

  O Agente de otimização de conteúdo cria variantes otimizadas como URLs dinâmicos ajustados para diferentes canais e tipos de formato.

* **Otimiza o conteúdo da imagem**

  O Agente de otimização de conteúdo aplica aprimoramentos como conversão de formato, ajustes de resolução, recorte e nitidez para melhorar a qualidade da imagem.

* **Otimização de ativos de várias variantes**

  O Content Otimization Agent pode gerar várias variações de imagem otimizadas a partir dos ativos retornados pelo Discovery Agent usando um único prompt de linguagem natural, permitindo que os usuários produzam representações prontas para canal de maneira rápida e eficiente.

## Personas {#personas-content-optimization-agent}

Os profissionais de marketing de canal, principal persona do Agente de otimização de conteúdo, podem selecionar o conteúdo original de alta resolução correto e solicitar formatos otimizados personalizados para seus canais e segmentos de público-alvo.

Profissionais de marketing regionais e funcionários de agências também podem usar o agente de otimização de conteúdo para gerar rapidamente variações de imagem prontas para canais que oferecem suporte à produção de conteúdo mais rápida e consistente.

## Como acessar o Agente de otimização de conteúdo? {#access-content-optimization-agent}

Você pode acessar os Agentes no AEM por meio do Assistente de IA. Faça logon em experience.adobe.com e você pode começar a interagir com o Assistente de IA especificando seu prompt em linguagem natural usando o campo `Ask AI Assistant anything`:

![Agente de Descoberta de Acesso](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

## Casos de uso comuns e prompts de amostra {#use-cases-prompts}

Use os prompts de Otimização de Conteúdo procurando os ativos corretos por meio do [Discovery Agent](/help/ai-in-aem/agents/discovery/overview.md). Depois que as imagens relevantes forem exibidas, os usuários poderão gerar variantes otimizadas ou específicas de canal para um ou vários ativos diretamente dos resultados da pesquisa. Esse fluxo de trabalho garante entradas de alta qualidade e resultados de otimização consistentemente melhores. [Consulte a lista completa de otimizações disponíveis](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/).

* **Criação de representação de alta resolução**

  O agente pode gerar novas representações de um ativo em uma resolução e um nível de qualidade especificados, facilitando a preparação de variações prontas para canais sem edição manual.


  Exemplo de prompt:

  Crie uma representação `2000px` como `JPEG` com qualidade `80%`.

  Pesquise o ativo correto usando o [Agente de descoberta](/help/ai-in-aem/agents/discovery/overview.md) e use os seguintes prompts no caso de vários resultados de pesquisa:

  Para o terceiro resultado da pesquisa, crie uma representação `2000px` como `JPEG` com qualidade `80%`.

  OU

  Para `Asset ID`, gere uma representação 2000px como `JPEG` com qualidade `80%`

* **Aprimoramento da imagem**

  O agente pode aplicar melhorias visuais — como nitidez — para garantir que os ativos tenham aparência nítida e bem definida antes de serem usados em campanhas.

  Exemplo de prompt:

  Nitidez da imagem.


* **Ajustes de cor de fundo**

  O agente pode atualizar ou substituir cores de fundo em ativos transparentes, suportando esquemas de cores específicos da marca ou temas visuais orientados por campanha.

  Exemplo de prompt:

  Alterar a cor de fundo de `PNG` para `#ff8932`.

* **Transformações de orientação**

  O agente pode virar ou espelhar visuais para se alinhar às necessidades de layout ou direção criativa, sem precisar de ferramentas de edição externas.

  Exemplo de prompt:

  Espelhe a imagem horizontalmente.

* **Representações otimizadas por canal**

  O agente pode produzir representações personalizadas para requisitos específicos da plataforma, como o Instagram Stories, garantindo que os ativos atendam automaticamente às diretrizes de formato, taxa e qualidade.

  Exemplo de prompt:

  Crie uma representação para uma história `Instagram`.

* **Sobreposições de marca e geração composta**

  O agente pode aplicar gráficos promocionais, sobreposições ou selos aos ativos existentes com posicionamento preciso, apoiando a criação rápida de compostos prontos para campanha.

  Exemplo de prompt:

  Sobreponha a imagem com `30%` gráficos de desconto sobre o banner promocional, colocando-a `100px` a partir do centro.

  >[!NOTE]
  >
  >As posições de sobreposição podem não ser precisas.


## Resultados da Otimização {#content-optimization-agent-results}

Quando você especifica um prompt de otimização, o Agente de otimização de conteúdo retorna o ativo aprimorado juntamente com opções de acesso convenientes com base no tipo de ativo:

* **Imagens**: a resposta inclui uma visualização em miniatura e opções para abrir a URL do Dynamic Media ou baixar a imagem otimizada.

* **Documentos do PDF**: a resposta inclui uma visualização em miniatura e opções para abrir a URL do Dynamic Media ou baixar o arquivo otimizado.

* **Vídeos**: a resposta fornece opções para abrir a URL do Dynamic Media ou baixar o vídeo otimizado.

![Resultados da Otimização de Conteúdo](/help/ai-in-aem/agents/content-optimization/assets/download-content-optimization.png)

Esses resultados facilitam a análise da saída otimizada e o seu uso imediato em canais ou workflows downstream.


## Limitações {#limitations-content-optimization}

* No momento, o Agente de otimização de conteúdo não oferece suporte a ativos PNG.

* Não há suporte para a configuração da cor do plano de fundo.

<!--


## Prompting best Practices {#prompting-best-practices-content-optimization-agent}

The following are some of the prompting best practices:

* Be explicit about the enhancement you want the Content Optimization Agent to apply. Clearly state the transformation or adjustment you expect. Precise instructions help the agent produce accurate and predictable results. For example, Instead of `Make it good quality`, specify `Create a JPEG image with 90% quality`.

* Provide detailed parameters whenever possible. The more context you give, such as dimensions, format, quality, placement, or color values, the more tailored the output is.

-->
