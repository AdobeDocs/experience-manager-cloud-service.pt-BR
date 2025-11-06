---
title: Introdução ao Editor universal
description: O Universal Editor é uma ferramenta de criação visual moderna projetada para capacitar sua organização de marketing a produzir experiências da Web impactantes.
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 11%

---


# Introdução ao Editor universal {#introduction}

O Universal Editor é uma ferramenta de criação visual moderna projetada para capacitar sua organização de marketing a produzir experiências da Web impactantes.

## Visão geral {#overview}

O Universal Editor é um editor visual versátil que faz parte do Adobe Experience Manager Sites. Ele permite que os autores executem a edição &quot;o que você vê é o que você obtém&quot; (WYSIWYG) de qualquer experiência headless ou headful. Ele oferece:

* **Edição instantânea**: os autores podem editar o conteúdo diretamente na experiência de visualização, eliminando a necessidade de localizar e navegar para fontes de conteúdo individuais.
* **Edição visual**: ao fazer alterações, os autores veem instantaneamente como elas afetam a experiência real do visitante, minimizando o atrito.
* **Opções detectáveis**: opções claramente rotuladas e uma interface intuitiva permitem aos autores configurar metadados e compor layouts com facilidade.
* **Não Técnico**: não é necessário um especialista especializado para fazer edições, enquanto as diretrizes de marca corporativa são aplicadas automaticamente, facilitando o dimensionamento de tarefas de conteúdo em toda a organização.
* **Integração e Extensibilidade**: totalmente integrado ao AEM, os [pontos de extensão](#extensibility) flexíveis do Editor Universal permitem que todas as ferramentas essenciais sejam unificadas em uma única interface coesa. De recursos alimentados por IA a extensões personalizadas adaptadas às suas necessidades comerciais exclusivas, ele permite que as equipes simplifiquem os fluxos de trabalho e melhorem a produtividade sem esforço.

Em resumo:

* **Os autores se beneficiam** da flexibilidade do Universal Editor, pois ele oferece suporte à mesma edição visual consistente para todas as formas de conteúdo do AEM.
* **Os desenvolvedores se beneficiam** da versatilidade do Universal Editor, pois ele oferece suporte à verdadeira dissociação da implementação.

Por ser um verdadeiro editor de como serviço e, no geral, ser mais flexível, o Editor universal pretende eventualmente substituir o [Editor de páginas.](/help/sites-cloud/authoring/page-editor/introduction.md)

## Arquiteturas compatíveis {#supported-architectures}

O Universal Editor é compatível com as duas configurações principais do AEM a seguir:

1. **[Edge Delivery Services](/help/edge/overview.md)**: esta é a abordagem preferida por sua simplicidade, tempo de implantação mais rápido e desempenho aprimorado.
1. **[Implementações headless](/help/headless/introduction.md)**: se você tiver um projeto headless existente ou requisitos específicos para renderização dissociada, o Editor universal permitirá edição visual de nível empresarial sem a necessidade de refatorar todo o projeto. Ele é compatível com praticamente qualquer arquitetura (SSR, CSR), estrutura da Web (Next.js, React, Astro, etc.) e modelos de hospedagem (&quot;traga seu próprio aplicativo&quot;).

>[!TIP]
>
>Consulte o documento [Casos de uso do editor universal e Caminhos de aprendizado](/help/implementing/universal-editor/use-cases.md) para obter mais detalhes sobre as arquiteturas compatíveis.

## Versões do AEM suportadas {#aem-versions}

O Editor Universal é compatível com:

* AEM as a Cloud Service (versão `2023.8.13099` ou superior)
* [AEM 6.5 LTS](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * Tanto no local quanto na hospedagem do AMS são compatíveis.
* [AEM 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * Tanto no local quanto na hospedagem do AMS são compatíveis.

Esta documentação é para usar o Editor universal com o AEM as a Cloud Service.

## Recursos {#features}

O Universal Editor oferece muitos recursos para oferecer suporte a uma grande variedade de casos de uso para um gerenciamento de conteúdo eficiente.

* **[WYSIWYG](/help/sites-cloud/authoring/universal-editor/authoring.md)**: faça edições &quot;o que você vê é o que você consegue&quot; de qualquer forma de conteúdo da Web, incluindo texto simples, rich text, mídia e metadados.
* **[Composição](/help/sites-cloud/authoring/universal-editor/authoring.md#editing-content)**: criar, editar, reordenar, aninhar ou excluir blocos de conteúdo de vários tipos (títulos, botões, teasers, seções, incorporação etc.).
* **[Layout](/help/sites-cloud/authoring/universal-editor/templates.md)**: utilizar modelos de página, aplicar estilos visuais e compor layouts com blocos como colunas, carrosséis e acordeões.
* **[Simulação de Dispositivo](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)**: Visualize e otimize o conteúdo para diferentes dispositivos de visitantes ao editar.
* **Omnichannel**: reutilize conteúdo estruturado e não estruturado em vários canais.
* **[Localização](/help/sites-cloud/authoring/universal-editor/inheritance.md)**: simplifique os fluxos de trabalho de tradução de conteúdo e lide com a herança de conteúdo localizada com eficiência com o Gerenciador de vários sites.
* **Consistência**: garanta a conformidade com as diretrizes da marca e mantenha a uniformidade em todo o conteúdo.
* **Segurança**: [Imponha o controle de acesso](/help/implementing/universal-editor/authentication.md), proteja a integridade do conteúdo e rastreie as alterações com o [controle de versão robusto.](/help/sites-cloud/authoring/sites-console/page-versions.md)
* **[Publicação](/help/sites-cloud/authoring/universal-editor/publishing.md)**: integre fluxos de trabalho de revisão, aprovação e publicação diretamente no editor.
* **Unificado**: integra-se totalmente com ferramentas do AEM, como o Console do [Sites,](/help/sites-cloud/authoring/sites-console/introduction.md) o [Editor de Fragmentos de Conteúdo,](/help/sites-cloud/administering/content-fragments/overview.md) e muito mais, proporcionando uma experiência de criação coesa.

## Extensibilidade {#extensibility}

O Universal Editor não é apenas muito capaz de pronto para uso, mas oferece uma série de possibilidades de extensão.

* **As extensões** são numerosas e prontas para atender aos requisitos, como dar suporte a fluxos de trabalho, gerar variações e habilitar a experimentação, para citar alguns.
* **Uma interface extensível** permite que você crie suas próprias extensões usando as mesmas estruturas subjacentes que as extensões prontas usam, permitindo flexibilidade máxima para se adaptar às necessidades do seu projeto.
* **Os Pontos de Extensão**, como blocos, tipos de dados personalizados e eventos, permitem a integração perfeita de requisitos comerciais personalizados além da interface do usuário.

>[!TIP]
>
>Para obter mais informações sobre a extensibilidade do Universal Editor, consulte o documento [Extensão do Universal Editor.](/help/implementing/universal-editor/extending.md)

## Editor universal e o editor de fragmento de conteúdo {#universal-editor-content-fragment-editor}

À primeira vista, pode parecer que o Editor universal e o Editor de fragmento de conteúdo fornecem recursos de edição semelhantes. No entanto, esses editores oferecem recursos muito diferentes e cuidam de tarefas distintas do profissional de marketing.

### Editor de fragmento de conteúdo {#content-fragment-editor}

Para um profissional de marketing que deseja criar conteúdo sem precisar se preocupar com o layout, de maneira que ele possa ser reutilizado em vários contextos da experiência.

* O foco é dimensionar a estratégia de conteúdo.

### Editor universal {#universal-editor}

Para um profissional de marketing que deseja criar um conteúdo adaptado ao layout de um contexto específico, a fim de fornecer uma experiência excepcional.

* O foco é estabelecer uma conexão convincente com os leitores.

## Limitações {#limitations}

Ao explorar o Editor universal e prosseguir com a implementação em seus próprios projetos, lembre-se das limitações a seguir.

* No máximo 25 recursos do AEM (Fragmentos de conteúdo, páginas, Fragmentos de experiência, Assets etc.) devem ser referenciados como instrumentação em uma única página.
* O AEM as a Cloud Service, o [AEM 6.5 LTS](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction) e o [AEM 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction) são os únicos back-end do AEM com suporte.
* A versão `2023.8.13099` ou superior é necessária para o AEM as a Cloud Service.
* Os autores de conteúdo devem ter suas próprias contas individuais do Experience Cloud.
* Como parte do AEM, o Editor Universal [oferece suporte aos mesmos navegadores de desktop que o AEM.](/help/overview/supported-platforms.md)
   * As versões móveis desses navegadores não são compatíveis.

{{ip-allow-lists-ue}}

## Próximas etapas {#next-steps}

Consulte o documento [Casos de uso do editor universal e Caminhos de aprendizado](/help/implementing/universal-editor/use-cases.md) para saber mais sobre casos de uso comuns do editor universal e descobrir os recursos de documentação corretos para apoiá-lo no seu projeto.
