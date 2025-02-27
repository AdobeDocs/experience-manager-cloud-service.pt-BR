---
title: Noções básicas do Editor universal - Modo responsivo
description: Este artigo explica como visualizar formulários usando diferentes emuladores no Editor universal para visualizar sua aparência durante a criação.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 8f5b4d863ab469c44b4c221eab1fb128706b45c7
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 2%

---

# Modo responsivo na criação do WYSIWYG

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email de seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> com o nome da organização do GitHub e o nome do repositório. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>


O [Editor Universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) permite que você visualize o Edge Delivery Services Forms com diferentes emuladores para ver a aparência do formulário durante a criação.

O modo responsivo permite que os desenvolvedores criem layouts que se adaptam automaticamente a diferentes tamanhos de tela, incluindo desktops, tablets e dispositivos móveis. O Editor universal oferece suporte a emuladores para desktop, tablet e dispositivos móveis. Você pode definir a altura e a largura de acordo com o tamanho da tela e executar as seguintes ações:

* Definir a orientação
* Especificar largura e altura
* Alterar a orientação

## Visualizar o Forms no modo responsivo para diferentes dispositivos

O Editor Universal fornece um ícone de **Emulador** localizado no canto superior direito da tela, que permite que você visualize páginas em diferentes tamanhos de dispositivo e teste o comportamento do seu design responsivo para obter uma melhor experiência do usuário.

Para ver como o Editor universal renderiza formulários em diferentes tamanhos de tela, execute as seguintes etapas:

1. Abra o formulário no Universal Editor para edição.
1. Selecione o ![Ícone do emulador](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} disponível na Barra de Ferramentas do Universal Editor e clique no ícone do emulador para exibir a opção.

   ![Modo responsivo](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

1. Selecione uma opção para emular um formulário no Universal Editor em um dispositivo selecionado: desktop, tablet, celular.

   ![Modo responsivo](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=40%,height=40%}

   Por padrão, o editor é aberto em um layout de desktop, com a altura e a largura determinadas automaticamente pelo navegador. Como alternativa, você pode emular um formulário em um dispositivo móvel ou tablet. Você também pode personalizar a largura e a altura da tela para dispositivos personalizados.

O Editor universal fornece diferentes emuladores para visualizar formulários em vários dispositivos. A tabela abaixo lista os tipos de emulador disponíveis junto com suas representações de dispositivo correspondentes:

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">Tipo de emulador</th>
        <th style="width: 80%">Imagem do dispositivo</th>
    </tr>
    <tr>
        <td style="width: 20%">Desktop</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="Emulador de desktop" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Tablet</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="Emulador de tablet" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivos móveis</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="Emulador móvel" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo personalizado</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="Emulador de dispositivo personalizado" style="width: auto; height: auto"></td>
    </tr>
</table>

Você pode usar o ícone **Rotador de Tela** para alternar entre as orientações retrato e paisagem ao visualizar um formulário em diferentes dispositivos. Ele ajuda os desenvolvedores a testar como o design responsivo se adapta às rotações de tela em vários dispositivos.

O Universal Editor é compatível com vários layouts de formulário. Para explorar o layout diferente, consulte a seção [Recursos de Layout](#layout-capabilities).

## Recursos de layout

O Universal Editor permite criar formulários fáceis de usar que oferecem experiências dinâmicas para os usuários finais. O layout de formulário controla como os itens ou componentes são exibidos em um formulário.

O Universal Editor é compatível com os seguintes tipos de layouts para formulários:
* [Layout do painel](#panel-layout)
* [Layout do assistente](#wizard-layout)
* [Layout do acordeão](#accordion-layout)

### Layout do painel

O layout do painel é útil para organizar campos relacionados de uma maneira que facilite a navegação e a localização do conteúdo correspondente. O layout do painel organiza os componentes do formulário em seções ou painéis distintos em formulários.

![Layout do painel](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

Você pode usar o [componente do painel](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) para adicionar o layout do painel em um formulário. Para obter instruções detalhadas sobre como configurar várias propriedades do componente do painel, consulte o artigo [componente do painel](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

### Layout do assistente


O layout do assistente ajuda a simplificar um formulário complexo, dividindo-o em etapas distintas. Cada etapa representa uma parte diferente do processo, e os usuários navegam pelas etapas sequencialmente, geralmente com os botões **Avançar** e **Voltar**. Você pode usar o layout do assistente para criar um formulário que envolve várias seções ou etapas.

![Layout do Assistente](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

Você pode usar o [componente de assistente](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) para adicionar o layout de assistente em um formulário. Para obter instruções detalhadas sobre como configurar as várias propriedades do componente do assistente, consulte o artigo [componente do assistente](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

### Layout do acordeão

O layout do Accordion exibe o conteúdo em seções ou painéis que podem ser recolhidos em um Formulário adaptável. Quando uma seção é expandida, ela exibe o conteúdo em, enquanto outras seções permanecem recolhidas. Esse layout é ideal para exibir grandes quantidades de informações em um formato compacto.

![Layout da opção](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

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

## Consulte também:

{{universal-editor-see-also}}
