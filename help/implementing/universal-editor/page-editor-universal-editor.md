---
title: Editor de páginas e Editor universal
description: O Editor de páginas permanece compatível com o Adobe, mas o Editor universal traz possibilidades interessantes para seus novos projetos.
feature: Developing
role: Admin, Architect, Developer
exl-id: 0a13fb52-623e-4aff-b254-186d8d117e4d
source-git-commit: 90c542bfc6ba6bcab34b640e3539971b8b89034c
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 3%

---

# Editor de páginas e Editor universal {#page-editor-universal-editor}

O Editor de páginas permanece compatível com o Adobe, mas o Editor universal traz possibilidades interessantes para seus novos projetos.

## Fundo {#background}

A Adobe apresentou o [Editor universal](/help/implementing/universal-editor/introduction.md) em 2024 como um editor simplificado que adota uma abordagem de desenvolvimento moderna baseada em Javascript. O Editor universal é a visão do Adobe para uma experiência de criação de conteúdo visual contínua e extensível.

Reconhecendo o conjunto de recursos avançados do [Editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md) e os inúmeros projetos que investem nele ao longo da longa história do AEM, a Adobe continua a oferecer suporte total ao Editor de páginas, embora a inovação se concentre no Editor universal.

## Recomendação {#recommendation}

Embora esteja restringindo rapidamente, ainda há uma lacuna de recursos entre o Editor Universal e o Editor de Páginas ([uma comparação de recursos pode ser encontrada na próxima seção](#feature-comparison)).

Como regra geral:

* **Novos projetos** devem usar o Editor Universal como padrão.
* **Projetos existentes** devem continuar usando o Editor de páginas e considerar o Editor universal ao iniciar os esforços do Edge Delivery ou do Headless.

**O editor escolhido deve ser totalmente orientado pelas necessidades do projeto individual.**

## Comparação de recursos {#feature-comparison}

Como a lacuna de recursos entre os dois editores está diminuindo constantemente, consulte as [notas de versão do Universal Editor](/help/release-notes/universal-editor/current.md) para obter os desenvolvimentos mais recentes.

### Entrega {#delivery}

|  | Editor de página | Notas | Editor universal | Notas |
|---|---|---|---|---|
| [Publicar Entrega](/help/sites-cloud/authoring/author-publish.md) | [!BADGE Disponível]{type=Positive} | Recomendado para uso com os Componentes principais e projetos tradicionais do AEM | [!BADGE Indisponível]{type=Negative} | As páginas tradicionais do AEM normalmente dependem de vários recursos específicos do Editor de páginas que são difíceis de replicar como estão com o Universal Editor. |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE Indisponível]{type=Negative} |  | [!BADGE Disponível]{type=Positive} |  |
| [Entrega headless](/help/headless/introduction.md) | [!BADGE Parcialmente Disponível]{type=Caution} | Somente com [o Editor de SPA](/help/implementing/developing/hybrid/introduction.md), que foi [descontinuado](/help/implementing/developing/hybrid/spa-editor-deprecation.md) em favor do Editor Universal | [!BADGE Disponível]{type=Positive} | O Editor universal permite que os desenvolvedores tragam seu próprio aplicativo web sem impor requisitos de estrutura específicos ou restrições de implementação. |

### Persistência {#persistence}

|  | Editor de página | Notas | Editor universal | Notas |
|---|---|---|---|---|
| Editar componentes da página | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} |  |
| Editando [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) | [!BADGE Indisponível]{type=Negative} |  | [!BADGE Disponível]{type=Positive} | Inclusão da inserção de fragmentos novos e de reordenação |

### Recursos {#capabilities}

|  | Editor de página | Notas | Editor universal | Notas |
|---|---|---|---|---|
| Modelos de páginas | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} | O Editor Universal é agnóstico em relação ao sistema de modelo usado. No entanto, o padrão de implementação típico favorece modelos definidos pelo desenvolvedor, já que as ferramentas de front-end modernas facilitam muito a definição e a manutenção da lógica do modelo diretamente no código. |
| Edição do WYSIWYG | [!BADGE Disponível]{type=Positive} | Limitado a páginas | [!BADGE Disponível]{type=Positive} | Páginas de suporte e fragmentos de conteúdo |
| [Gerar variações](/help/generative-ai/generate-variations.md) | [!BADGE Indisponível]{type=Negative} |  | [!BADGE Disponível]{type=Positive} | [Disponível como uma extensão](/help/implementing/universal-editor/extending.md) |
| Inserir novo bloco | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} |  |
| Reordenar bloco | [!BADGE Disponível]{type=Positive} | Possível com arrastar e soltar no contexto, mas não no painel lateral &quot;exibição em árvore&quot; | [!BADGE Disponível]{type=Positive} | Possível por meio do arrastar e soltar no painel lateral &quot;exibição em árvore&quot;, mas ainda não no contexto (planejado) |
| Recortar/Copiar-Colar bloco | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} |  |
| Aplicar estilos | [!BADGE Disponível]{type=Positive} | Os estilos podem ser aplicados a componentes usando o [Sistema de Estilos.](/help/sites-cloud/authoring/page-editor/style-system.md) | [!BADGE Disponível]{type=Positive} | Os estilos podem ser aplicados usando propriedades regulares de componente (ou Fragmento de conteúdo). O mesmo seletor de estilo não está disponível no Editor universal, no entanto, usar um widget de multisseleção para um UX muito semelhante pode ser obtido. |
| Aplicar layout | [!BADGE Disponível]{type=Positive} | Os sites devem implementar a [Grade responsiva do AEM](/help/implementing/developing/introduction/responsive-design.md) para permitir que os autores redimensionem componentes em três pontos de interrupção predefinidos. | [!BADGE Disponível]{type=Positive} | Os layouts podem ser aplicados usando propriedades regulares de componente (ou Fragmento de conteúdo). No entanto, a Grade responsiva não é compatível. |
| Desfazer-Refazer | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} |  |
| Publicar (também para visualização) | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} |  |
| [Iniciar fluxo de trabalho](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} | Disponível como uma extensão |
| Comentando | [!BADGE Disponível]{type=Positive} | Usando [anotações](/help/sites-cloud/authoring/page-editor/annotations.md) | [!BADGE Indisponível]{type=Negative} | Planejado |
| Integração com o Workfront | [!BADGE Indisponível]{type=Negative} |  | [!BADGE Disponível]{type=Positive} | Disponível como uma extensão |
| [MSM e inicializações](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} | Disponível para páginas como uma extensão |
| Experimentação e personalização | [!BADGE Disponível]{type=Positive} | Usando o [Modo de destino](/help/sites-cloud/authoring/personalization/targeted-content.md) | [!BADGE Disponível]{type=Positive} | Disponível como uma extensão para o Edge Delivery Services |
| Árvore de conteúdo | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} | Também permite reordenar dentro da árvore |
| Simulação de dispositivo | [!BADGE Disponível]{type=Positive} | [Dispositivos configurados podem ser simulados](/help/sites-cloud/administering/responsive-layout.md), mas o usuário não pode inserir manualmente dimensões de tela diferentes para simular. | [!BADGE Disponível]{type=Positive} | [Qualquer dimensão de tela a ser simulada pode ser inserida manualmente](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator), mas os pontos de interrupção padrão não podem ser configurados. |
| [Bloqueio de páginas](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} | Respeita o status de bloqueio definido no Console Sites com a extensão disponível para bloquear/desbloquear páginas do editor |
| [Propriedades da página](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} | Disponível pelo Administrador do site, com extensão para também acessar as propriedades das páginas do editor |
| Propriedades de vários campos | [!BADGE Disponível]{type=Positive} |  | [!BADGE Indisponível]{type=Negative} | Planejado |
| [DAM remoto](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} |  |
| [Controle de versão da página](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} |  |
| [TimeWarp](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp) e [Exibição de comparação](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE Disponível]{type=Positive} |  | [!BADGE Indisponível]{type=Negative} | Planejado |
| Exibir no admin | [!BADGE Disponível]{type=Positive} |  | [!BADGE Disponível]{type=Positive} | Disponível como uma extensão para páginas |
| Exibir status da página | [!BADGE Disponível]{type=Positive} |  | [!BADGE Indisponível]{type=Negative} | Disponível no console Sites |
| Extensibilidade | [!BADGE Disponível]{type=Positive} | Como sobreposições do AEM | [!BADGE Disponível]{type=Positive} | Como pontos de extensão claramente definidos usando o App Builder e muito pouco conhecimento específico do AEM |

## Adoção do Editor universal {#adopt-ue}

O Editor Universal oferece muitas vantagens, tornando-se uma ótima solução para novos projetos.

* **Edição visual:** assim como no Editor de páginas, os autores podem editar o conteúdo diretamente na visualização e ver instantaneamente como suas alterações afetam a experiência do visitante.
* **Prova futura:** o roteiro do AEM prioriza o Editor universal como editor visual. A sua adoção garante o acesso às mais recentes inovações e melhorias.
* **Integração mais simples**: nenhuma SDK específica do AEM é necessária para usar o Editor Universal, reduzindo o bloqueio da pilha técnica.
* **Traga Seu Próprio Aplicativo:** O Universal Editor oferece suporte a qualquer estrutura ou arquitetura da Web, permitindo a adoção sem a necessidade de refatoração complexa.
* **Extensibilidade:** o Editor Universal se beneficia de uma [estrutura de extensão](/help/implementing/universal-editor/extending.md) robusta, que inclui integrações com GenAI, Workfront e muito mais.

### Migração para o Editor universal {#migrate-ue}

Não há caminho de migração direto do Editor de páginas para o Editor universal. Isso se deve a diferenças fundamentais nas duas tecnologias.

* O Editor universal não reintroduz recursos como o Editor de modelo, o Sistema de estilos ou a Grade responsiva.
   * Esses casos de uso agora podem ser tratados com mais eficiência com CSS de front-end enxuto e JavaScript em projetos do Edge Delivery Services ou headless.
* Como o Editor universal é um editor como um serviço, ele não pode permitir que os implementadores injetem CSS ou JS nas caixas de diálogo do componente.
   * Isso impede a conversão automática das caixas de diálogo do componente no Editor de páginas.
   * Isso afeta muitas áreas das caixas de diálogo, como widgets personalizados, validação de campo, regras de mostrar/ocultar e personalizações baseadas em modelo.
      * Embora esses recursos ainda sejam possíveis, o Editor universal os resolve por meio de configuração, em vez de implantar JavaScript personalizado em caixas de diálogo.

Embora o Editor universal possa tecnicamente habilitar a edição de páginas para projetos tradicionais do AEM (por exemplo, criados com os Componentes principais), esses sites normalmente dependem de vários recursos específicos do Editor de páginas, como o Sistema de estilos, Grade responsiva, Modelos editáveis e Javascript personalizado nas caixas de diálogo.

Como o Editor universal segue uma abordagem mais simplificada e moderna que não oferece suporte a esses recursos herdados, a migração desses sites exigiria uma refatoração significativa. Por esse motivo, **migrar sites do Editor de páginas para o Editor universal é recomendado somente para projetos em transição para o Edge Delivery Services.**
