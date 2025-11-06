---
title: Editor universal do Edge Delivery Services para Forms
description: Use o Universal Editor para Edge Delivery Services no Forms para criar o Adaptive Forms.
feature: Edge Delivery Services
role: Admin, Developer
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 3%

---


# Editor universal do Edge Delivery Services para Forms

O Editor universal revoluciona a criação de formulários para os Serviços de entrega de borda da Adobe, oferecendo uma interface simples, visual e intuitiva do What You See Is What You Get (WYSIWYG). Projetado para criadores de conteúdo e autores de formulários, ele elimina a complexidade dos processos tradicionais de criação de formulários, tornando-o acessível até mesmo para usuários não técnicos.

Com o Editor universal, você pode criar rapidamente formulários responsivos e interativos usando componentes pré-criados, como campos de texto, caixas de seleção e botões de opção. Seu conjunto de recursos robusto oferece suporte a regras dinâmicas, integração de dados contínua e personalização avançada, garantindo que cada formulário seja adaptado às suas necessidades.

Quer você esteja gerenciando uma renderização leve do lado do cliente, garantindo compatibilidade entre navegadores ou seguindo padrões de acessibilidade rigorosos, o Universal Editor oferece uma solução simplificada para criar e gerenciar formulários.

![Universal Editor](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}

## Principais recursos do Universal Editor para Edge Delivery Services para Forms



| ![Interface do WYSIWYG](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg) | ![Editor de regras](/help/edge/docs/forms/universal-editor/assets/rule-editor.svg) | ![Enviar Ações](/help/edge/docs/forms/universal-editor/assets/submit-actions.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Interface do WYSIWYG**](/help/edge/docs/forms/universal-editor/universal-editor-user-interface.md) | [**Editor de regras**](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) | [**Enviar Ações**](/help/edge/docs/forms/universal-editor/submit-action.md) |
| O Editor universal fornece uma interface do WYSIWYG para design de formulários com uma biblioteca de componentes pré-criada, design responsivo, criação baseada em modelo e modificações de campo em tempo real. | O editor de regras permite que os usuários criem interações de formulário dinâmicas usando regras orientadas por eventos, validação instantânea e tratamento de erros por meio do lightweight JavaScript e do JSON. | As ações enviar oferecem suporte à integração de back-end, lógica de envio condicional, endpoints seguros e pré-processadores, simplificando os fluxos de trabalho de envio. |

| ![Publicando/Desfazendo publicação](/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg) | ![Modo responsivo](/help/edge/docs/forms/universal-editor/assets/responsive.svg) | ![Componentes personalizados](/help/edge/docs/forms/universal-editor/assets/custom-components.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Publicando/Desfazendo publicação**](/help/edge/docs/forms/universal-editor/publish-forms.md) | [**Modo responsivo**](/help/edge/docs/forms/universal-editor/responsive-layout.md) | [**Componentes personalizados**](/help/edge/docs/forms/universal-editor/create-custom-component.md) |
| Controle facilmente a visibilidade de seus formulários — publique ou cancele a publicação diretamente do editor com apenas alguns cliques. | Crie formulários que se adaptam perfeitamente a todos os dispositivos (desktops, tablets e dispositivos móveis). Use o modo responsivo para visualizar e testar formulários para vários tamanhos de tela. | Os componentes personalizados permitem que os desenvolvedores estendam os recursos do formulário criando elementos exclusivos personalizados adaptados a casos de uso organizacional específicos. |

| ![Estilo](/help/edge/docs/forms/universal-editor/assets/personalization.svg) | ![Serviços de preenchimento prévio](/help/edge/docs/forms/universal-editor/assets/prefill-services.svg) | ![Teste A/B](/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Estilo**](/help/edge/docs/forms/universal-editor/style-theme-forms.md) | **[Preencher formulários previamente](/help/edge/docs/forms/universal-editor/prefill-form.md)** | [**Teste A/B**](https://github.com/adobe/aem-experimentation/blob/main/documentation/experiments.md) |
| O estilo com CSS permite que os desenvolvedores personalizem a aparência dos elementos de formulário e criem um design visualmente atraente que se alinhe à estética do site. | Os serviços de pré-preenchimento preenchem automaticamente os campos de formulário com dados relevantes do usuário de várias fontes, reduzindo a entrada manual e aprimorando a experiência do usuário. | O teste A/B permite que as organizações experimentem diferentes designs de formulário, layouts e recursos para identificar as variantes com melhor desempenho. |

| ![Análise e Acompanhamento](/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg) | ![Fragmentos de formulário](/help/edge/docs/forms/universal-editor/assets/form-fragments.svg) | ![Associação de Dados](/help/edge/docs/forms/universal-editor/assets/data-binding.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Análise e Acompanhamento**](https://www.aem.live/developer/martech-integration) | **Fragmentos de formulário** (em breve) | [**Associação de Dados**](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) |
| Obtenha insights sobre o comportamento do usuário, as interações de formulário e as taxas de envio com análises e rastreamento integrados para permitir a otimização de formulários orientados por dados. | Os fragmentos de formulário permitem a reutilização, permitindo que as seções usadas com frequência sejam criadas uma vez e reutilizadas em vários formulários, garantindo a consistência e reduzindo o esforço de manutenção. | A vinculação de dados permite conexões diretas entre campos de formulário e fontes de dados de back-end, oferecendo suporte a atualizações em tempo real e mapeamento de dados avançado. |

| ![CAPTCHA](/help/edge/docs/forms/universal-editor/assets/captcha.svg) | ![Incorporando o Forms](/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg) | ![Obrigado pela Configuração](/help/edge/docs/forms/universal-editor/assets/thank-you.svg) |
|:-------------:|:-------------:|:-------------:|
| [**CAPTCHA**](/help/edge/docs/forms/universal-editor/recaptcha-forms.md) | **Incorporando o Forms** (Em Breve) | [**Obrigado pela Configuração**](/help/edge/docs/forms/universal-editor/submit-action.md#show-a-custom-thank-you-message-on-adaptive-form-submission-submit-action-message-ue) |
| Use o reCAPTCHA para proteger formulários de bots automatizados, garantindo uma coleta de dados segura e confiável. | Incorpore formulários diretamente nas páginas do Edge Delivery Services Sites usando o componente de incorporação integrado do Editor universal. | Personalize facilmente a mensagem ou página de confirmação exibida aos usuários após o envio bem-sucedido do formulário. |



## Componentes de formulário pré-construídos

O Editor universal fornece os seguintes componentes de formulário prontos para uso:

<table>
  <thead>
    <tr>
      <th></th> 
      <th>Componentes de formulários</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="Componentes de formulários" style="width: 100%;"></td> 
      <td><b>Acordeão</b></td>
      <td>Estrutura do painel flexível para organizar o conteúdo.</td>
    </tr>
    <tr>
      <td><b>Botão</b></td>
      <td>Adiciona elementos interativos para ações como navegação ou lógica personalizada.</td>
    </tr>
    <tr>
      <td><b>Captcha</b></td>
      <td>Evita spam exigindo que os usuários concluam uma tarefa de verificação humana usando o Google reCaptcha ou HCaptcha.</td>
    </tr>
    <tr>
      <td><b>Caixa de seleção</b></td>
      <td>Permite que os usuários configurem uma caixa de seleção.</td>
    </tr>
    <tr>
      <td><b>Grupos de caixa de seleção</b></td>
      <td>Permite aos usuários selecionar várias opções de um grupo.</td>
    </tr>
    <tr>
      <td><b>Seletor de datas</b></td>
      <td>Permite que os usuários selecionem uma data usando uma interface de calendário.</td>
    </tr>
    <tr>
      <td><b>Listas Suspensas</b></td>
      <td>Oferece opções de seleção única ou múltipla de uma lista predefinida.</td>
    </tr>
    <tr>
      <td><b>Email</b></td>
      <td>Captura endereços de email com validação básica de formato.</td>
    </tr>
    <tr>
      <td><b>Arquivo em anexo</b></td>
      <td>Permite o upload de documentos, imagens ou outros tipos de arquivos.</td>
    </tr>
    <tr>
      <td><b>Fragmentos de formulários</b></td>
      <td>Componentes de formulário reutilizáveis para seções como campos de endereço ou detalhes de contato.</td>
    </tr>
    <tr>
      <td><b>Imagem</b></td>
      <td>Suporta o upload e a exibição de imagens em formulários.</td>
    </tr>
    <tr>
      <td><b>Modal</b></td>
      <td>Exibe uma caixa de diálogo pop-up, geralmente usada para alertas, informações adicionais ou confirmação.</td>
    </tr>
    <tr>
      <td><b>Campo numérico</b></td>
      <td>Registra entrada numérica, permitindo a validação de números ou intervalos.</td>
    </tr>
    <tr>
      <td><b>Painel</b></td>
      <td>Organiza seções de formulário com painéis expansíveis/recolhíveis.</td>
    </tr>
    <tr>
      <td><b>Botões de opção</b></td>
      <td>Habilita a seleção de escolha única de um grupo de opções.</td>
    </tr>
    <tr>
      <td><b>Avaliação</b></td>
      <td>Permite que os usuários forneçam uma classificação baseada em estrelas.</td>
    </tr>
    <tr>
      <td><b>Botão de redefinir</b></td>
      <td>Redefine os campos de formulário para seu estado padrão.</td>
    </tr>
    <tr>
      <td><b>Botão de enviar</b></td>
      <td>Aciona o envio do formulário e inicia fluxos de trabalho definidos.</td>
    </tr>
    <tr>
      <td><b>Campo de número de telefone</b></td>
      <td>Registra números de telefone com formatação baseada no país.</td>
    </tr>
    <tr>
      <td><b>Texto</b></td>
      <td>Fornece uma seção dedicada para exibir termos legais e coletar contratos de usuário por meio de caixas de seleção.</td>
    </tr>
    <tr>
      <td><b>Campo de texto</b></td>
      <td>DCaptura a entrada de linha única, como nomes ou endereços de email.</td>
    </tr>
    <tr>
      <td><b>Assistente</b></td>
      <td>Orienta os usuários passo a passo por um processo de formulário de várias partes.</td>
    </tr>
  </tbody>
</table>

## Perguntas frequentes

**T. Quem pode usar o Editor universal?**
O Editor universal foi projetado para um amplo público-alvo, incluindo:

- Criadores de conteúdo que desejam criar formulários visualmente atraentes.
- Desenvolvedores que precisam de recursos avançados de personalização e integração.
- Organizações que buscam soluções de formulários escaláveis, seguras e compatíveis.

**P: Posso integrar formulários criados com o Editor Universal aos meus sistemas existentes?**
Absolutamente. O Editor universal oferece suporte à vinculação de dados contínua com sistemas de back-end, permitindo atualizações em tempo real e mapeamento de dados avançado. Ele também se integra a ferramentas como o Adobe Workfront para gerenciamento de tarefas e oferece suporte a endpoints seguros para workflows de envio de dados.

**P: É possível personalizar os componentes de formulário?**
Sim, o Editor universal permite que os desenvolvedores criem componentes personalizados adaptados às necessidades organizacionais específicas. Além disso, é possível estender a funcionalidade do editor por meio de extensões de interface do usuário e fluxos de trabalho personalizados.

**P: Que tipo de análise posso obter dos formulários?**
O Editor universal inclui ferramentas de análise e rastreamento integradas para monitorar interações do usuário, taxas de envio de formulário e métricas de conversão. Esses insights ajudam a otimizar seus formulários para obter melhor desempenho.

**P: Como o Editor Universal lida com a acessibilidade?**
O Editor universal foi projetado com a rigorosa observância dos padrões de acessibilidade, incluindo as WCAG (Web Content Accessibility Guidelines). Isso garante que os formulários possam ser usados por indivíduos com deficiência, fornecendo uma experiência inclusiva.






