---
title: Noções básicas do Editor universal - Modo responsivo
description: Este artigo explica como visualizar formulários usando diferentes emuladores no Editor universal para visualizar sua aparência durante a criação.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 1%

---


# Modo responsivo na criação do WYSIWYG

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email de seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> com o nome da organização do GitHub e o nome do repositório. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>

## Introdução ao Responsive Forms

No mundo de vários dispositivos de hoje, seus formulários precisam ter ótima aparência e funcionar bem em telas de todos os tamanhos: de monitores de desktop a smartphones. O modo responsivo no Editor universal ajuda você a fazer isso permitindo visualizar e testar seus formulários em diferentes tamanhos de dispositivo durante o processo de criação.

O [Editor Universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) permite que você crie formulários que se adaptam automaticamente a diferentes tamanhos de tela, fornecendo uma experiência do usuário ideal independentemente do dispositivo que está sendo usado.

## Visualizar o Forms no modo responsivo para diferentes dispositivos

O Editor Universal fornece um ícone de **Emulador** localizado no canto superior direito da tela, que permite que você visualize páginas em diferentes tamanhos de dispositivo e teste o comportamento do seu design responsivo para obter uma melhor experiência do usuário.

Para visualizar um formulário no modo responsivo:

1. Abra o formulário no Universal Editor para edição.
2. Clique no ícone ![Emulador mostrando um símbolo de visualização de dispositivo](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} na barra de ferramentas.
3. Selecione um formato de dispositivo:
   - Área de trabalho (padrão)
   - Tablet
   - Dispositivos móveis
   - Personalizado (especificar largura e altura)

![Captura de tela do Editor Universal mostrando opções do modo responsivo para diferentes dispositivos](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

Você também pode usar o ícone **Rotador de Tela** para alternar entre as orientações retrato e paisagem ao visualizar em tablet ou dispositivos móveis.

O Editor universal fornece diferentes emuladores para visualizar formulários em vários dispositivos. A tabela abaixo lista os tipos de emulador disponíveis junto com suas representações de dispositivo correspondentes:

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">Tipo de emulador</th>
        <th style="width: 80%">Imagem do dispositivo</th>
    </tr>
    <tr>
        <td style="width: 20%">Desktop</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="Modo de exibição de desktop de um formulário mostrando layout de largura total" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Tablet</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="Exibição de tablet de um formulário mostrando layout de largura média com componentes ajustados" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivos móveis</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="Modo de exibição móvel de um formulário que mostra layout estreito com componentes empilhados" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo personalizado</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="Exibição de dispositivo personalizado de um formulário com dimensões especificadas pelo usuário" style="width: auto; height: auto"></td>
    </tr>
</table>

## Recursos de layout

O Universal Editor permite criar formulários fáceis de usar que oferecem experiências dinâmicas para os usuários finais. O layout de formulário controla como os itens ou componentes são exibidos em um formulário.

O Universal Editor é compatível com os seguintes tipos de layouts para formulários:

- [Layout do painel](#panel-layout)
- [Layout do assistente](#wizard-layout)
- [Layout do acordeão](#accordion-layout)

### Layout do painel

O layout do painel é útil para organizar campos relacionados de uma maneira que facilite a navegação e a localização do conteúdo correspondente. O layout do painel organiza os componentes do formulário em seções distintas ou painéis em formulários.

![Layout do painel mostrando várias seções distintas dentro de um formulário](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Exemplo:** Um formulário de aplicativo de trabalho pode usar painéis para separar &quot;Informações Pessoais&quot;, &quot;Educação&quot;, &quot;Experiência Profissional&quot; e &quot;Referências&quot; em seções distintas.

**Comportamento responsivo:** Em telas menores, os painéis normalmente são empilhados verticalmente, mantendo seus agrupamentos distintos enquanto ajustam para uma largura mais estreita.

Você pode usar o [componente do painel](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) para adicionar o layout do painel em um formulário. Para obter instruções detalhadas sobre como configurar várias propriedades do componente do painel, consulte o artigo [componente do painel](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

### Layout do assistente

O layout do assistente ajuda a simplificar um formulário complexo, dividindo-o em etapas distintas. Cada etapa representa uma parte diferente do processo, e os usuários navegam pelas etapas sequencialmente, geralmente com os botões **Avançar** e **Voltar**. Você pode usar o layout do assistente para criar um formulário que envolve várias seções ou etapas.

![Layout do assistente mostrando um formulário de várias etapas com controles de navegação](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Exemplo:** Um formulário de reclamação de seguro pode usar um assistente para orientar os usuários sobre como fornecer detalhes do incidente, carregar evidências, inserir informações pessoais e revisar o envio.

**Comportamento responsivo:** Em dispositivos móveis, o assistente mantém sua abordagem passo a passo, mas ajusta o conteúdo em cada etapa para caber na tela mais estreita, geralmente empilhando elementos que apareceriam lado a lado em telas maiores.

Você pode usar o [componente de assistente](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) para adicionar o layout de assistente em um formulário. Para obter instruções detalhadas sobre como configurar as várias propriedades do componente do assistente, consulte o artigo [componente do assistente](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

### Layout do acordeão

O layout do Accordion exibe o conteúdo em seções ou painéis que podem ser recolhidos em um Formulário adaptável. Quando uma seção é expandida, ela exibe o conteúdo em, enquanto outras seções permanecem recolhidas. Esse layout é ideal para exibir grandes quantidades de informações em um formato compacto.

![Layout do Accordion mostrando seções expansíveis em um formulário](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Exemplo:** um formulário de configuração de produto pode usar seções do Accordion para &quot;Opções Básicas&quot;, &quot;Recursos Avançados&quot;, &quot;Acessórios&quot; e &quot;Planos de Pagamento&quot;, permitindo que os usuários se concentrem em um aspecto de cada vez.

**Comportamento responsivo:** Os acordeões funcionam particularmente bem em dispositivos móveis, pois conservam naturalmente o espaço vertical ao mostrar somente a seção de conteúdo expandida, tornando-os ideais para telas menores.

Você pode usar o [componente Acordeão](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) para adicionar o layout acordeão em um formulário. Para obter instruções detalhadas sobre como configurar as várias propriedades do componente Acordeão, consulte o artigo [componente Acordeão](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

### Como escolher o layout correto?

É importante selecionar o layout correto para otimizar a experiência do usuário e a funcionalidade do formulário. A tabela ajuda você a entender as diferentes opções de layout disponíveis e orienta você a selecionar o layout mais adequado com base nas suas necessidades e casos de uso específicos:

| Destaque | Layout do painel | Layout do assistente | Layout do acordeão |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **Finalidade** | Agrupa conteúdo relacionado em seções distintas | Orienta os usuários por meio de um processo ou formulário de várias etapas | Organiza o conteúdo em seções que podem ser recolhidas |
| **Estrutura** | Seções distintas | Etapas/páginas sequenciais | Painéis/seções flexíveis |
| **Navegação** | Clique nos cabeçalhos do painel para navegar | - Avançar: botão &quot;Avançar&quot;<br>- Voltar: botão &quot;Voltar&quot;<br>- Etapas de ignorar opcionais | Clique em cabeçalhos para expandir/recolher seções |
| **Experiência do usuário** | Organiza grandes quantidades de conteúdo de maneira gerenciável | Orientação passo a passo, reduzindo a sobrecarga | Exibição compacta com seções expandidas/recolhidas |
| **Caso de uso** | Formulários complexos com seções categorizadas | Processos de configuração, formulários complexos | Perguntas frequentes, menus de configurações e seções detalhadas de conteúdo |
| **Melhor para dispositivos móveis** | Moderado - painéis empilhados verticalmente | Bom - mantém o foco somente na etapa atual | Excelente - preserva o espaço com seções que podem ser recolhidas |

## Práticas recomendadas para Forms responsivo

Para garantir que seus formulários forneçam a melhor experiência em todos os dispositivos, siga estas práticas recomendadas:

1. **Crie para dispositivos móveis primeiro:** comece criando seu formulário para dispositivos móveis e depois melhore para telas maiores. Essa abordagem garante que a funcionalidade principal funcione nas telas menores.

2. **Usar tipos de campo apropriados:** Escolha tipos de campo que funcionem bem em dispositivos de toque:
   - Use menus suspensos em vez de botões de opção quando houver muitas opções
   - Usar seletores de data projetados para entrada de toque
   - Verifique se os botões e os destinos de toque têm pelo menos 44px x 44px

3. **Simplificar para telas menores:**
   - Exibir menos campos por linha em dispositivos móveis
   - Considere ocultar campos opcionais atrás de uma opção &quot;Mostrar mais&quot;
   - Divida formulários complexos em mais etapas no dispositivo móvel

4. **Teste completamente:** sempre teste seus formulários em dispositivos reais ou usando o modo emulador no Universal Editor para garantir que eles funcionem corretamente em todos os tamanhos de tela.

5. **Considere carregar os tempos:** otimize os tamanhos das imagens e minimize os recursos necessários, especialmente para usuários móveis que possam ter conexões mais lentas.

## Solução de problemas do Responsive Forms

| Problema | Causa possível | Solução |
|-------|---------------|----------|
| O formulário aparece cortado em dispositivos móveis | Configurações de largura corrigidas ou problemas de estouro | Usar unidades relativas (%, rem) em vez de pixels e verificar se há propriedades overflow:hidden |
| Elementos de toque de difícil interação | Destinos de toque muito pequenos ou muito próximos | Aumente o tamanho do botão/entrada para pelo menos 44 px x 44 px e adicione mais espaço entre elementos interativos |
| Sobrecargas de conteúdo em telas pequenas | Nenhuma regra responsiva para janelas de visualização menores | Adicionar consultas de mídia ou classes responsivas para ajustar o layout para diferentes tamanhos de tela |
| Formulário muito lento em dispositivos móveis | Imagens grandes ou scripts em excesso | Otimizar imagens, minimizar o JavaScript e considerar o carregamento lento de elementos não críticos |
| Aparência diferente entre emulador e dispositivos reais | Renderização específica do navegador ou variações de dispositivo | Testar em dispositivos reais quando possível, não apenas em emuladores |

## Consulte também:

{#see-more-eds-forms}
