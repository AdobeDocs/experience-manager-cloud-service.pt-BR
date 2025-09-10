---
title: Criar Forms responsivo com editor universal
description: Saiba como projetar, testar e otimizar formulários responsivos para todos os dispositivos usando o Universal Editor. Teste de dispositivo mestre, padrões de layout e técnicas de otimização para dispositivos móveis para AEM Forms com Edge Delivery Services.
keywords: formulários responsivos, formulários móveis, teste de dispositivo, editor universal, layout adaptável, otimização de formulário, design móvel, design responsivo, layouts de formulário, emulador de dispositivo
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '2443'
ht-degree: 0%

---


# Criação de Forms responsivo com Universal Editor - Um guia completo

O cenário moderno da Web exige formulários que funcionem perfeitamente em um espectro cada vez maior de dispositivos e tamanhos de tela. De grandes monitores de desktop a telas de smartphone compactas, os usuários esperam experiências consistentes e intuitivas, independentemente do dispositivo escolhido. A criação de formulários responsivos não é mais opcional — é um requisito fundamental para o fornecimento de experiências digitais profissionais, acessíveis e otimizadas para conversão.

O Universal Editor fornece ferramentas e metodologias abrangentes para desenvolver formulários responsivos que se adaptem de forma inteligente a várias dimensões de tela, métodos de entrada e contextos de usuário. Este guia explora as bases técnicas, as estratégias de implementação e as técnicas de otimização necessárias para criar formulários que tenham desempenho excepcional em todos os dispositivos, mantendo a usabilidade, a acessibilidade e o apelo visual.

A criação responsiva de formulários envolve duas atividades principais:

- **Teste responsivo:** Visualize e teste seus formulários em vários tamanhos de tela usando emuladores de dispositivo.
- **Design responsivo:** Selecione e implemente padrões de layout que se adaptem perfeitamente a diferentes dispositivos.

**Neste guia, você aprenderá a:**

- Testar formulários em dispositivos desktop, tablet e móveis
- Selecione os padrões de layout apropriados para o seu conteúdo
- Aplicar práticas recomendadas de design responsivo
- Solução de problemas comuns de formulários responsivos
- Otimizar formulários para desempenho móvel

<!--
## Why Responsive Forms Are Important

**User Experience Impact:**

- Over 60% of users access forms on mobile devices
- Poor mobile experiences result in a 67% higher abandonment rate
- Responsive forms can increase completion rates by up to 25%

**Business Benefits:**

- Higher form completion rates
- Improved user satisfaction
- Enhanced accessibility compliance
- Lower development and maintenance costs-->

>[!TIP]
>
> **Primeira Abordagem para Dispositivos Móveis:** comece a criar para dispositivos móveis e, em seguida, melhore para telas maiores. Isso garante que a funcionalidade principal funcione no ambiente mais restrito.

## Parte 1: Testando o Forms em vários dispositivos

Testar seus formulários em diferentes dispositivos ajuda a identificar e resolver problemas responsivos antes que os usuários os encontrem. O Editor universal fornece um modo emulador para simular vários tamanhos e orientações de tela.

### Como testar seu Forms

**Etapa 1: Abrir o Emulador de Dispositivo**

1. Abra o formulário no Editor universal.
2. Clique no ícone ![Emulador](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} **Emulador** na barra de ferramentas.
3. O menu do seletor de dispositivos será exibido.

![Interface de Teste Responsiva do Editor Universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

**Etapa 2: Selecionar um dispositivo para teste**

- **Área de trabalho** (largura superior a 1200 px): modo de exibição de edição padrão
- **Tablet** (largura de 768px-1199px): teste de tela do Medium
- **Dispositivo móvel** (largura de 320px-767px): teste de tela pequena
- **Personalizado**: especifique dimensões exatas para dispositivos específicos

**Etapa 3: Testar orientações do dispositivo**

Use o ícone **Rotador de telas** para testar:

- **Modo retrato**: orientação móvel padrão
- **Modo paisagem**: exibição de tablet ou telefone girada

### Resultados do teste de dispositivo

Cada tipo de dispositivo revela comportamentos responsivos exclusivos:

| **Tipo de dispositivo** | **Largura da tela** | **O que Verificar** | **Problemas comuns** |
|-----------------|------------------|-------------------|-------------------|
| **Área de Trabalho** | 1200px+ | Layout completo, todos os recursos visíveis | Excesso de espaços em branco, layouts muito largos |
| **Tablet** | 768px-1199px | Empilhamento de componentes, usabilidade de navegação | Dimensionamento estranho, problemas de direcionamento por toque |
| **Móvel** | 320px-767px | Layout de coluna única, navegação em miniatura | Texto pequeno, botões próximos ao espaçamento |
| **Personalizado** | Definido pelo usuário | Requisitos específicos do dispositivo | Casos de borda de ponto de interrupção |

### Exemplos visuais por dispositivo

**Modo de Exibição de Área de Trabalho (1200px+):**
![Modo de exibição de formulário da área de trabalho](/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png)
*Layout de largura total com campos de formulário lado a lado.*

**Exibição do tablet (768px-1199px):**
![Modo de exibição de formulário do tablet](/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png)
*Layout de largura de Medium com espaçamento de componente ajustado.*

**Exibição do Mobile (320px-767px):**
![Exibição de formulário móvel](/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png)
*Layout de coluna única com componentes empilhados.*

**Modo de Exibição de Dispositivo Personalizado:**
![Exibição de dispositivo personalizada](/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png)
*Dimensões especificadas pelo usuário para testes direcionados.*

### Testar fluxo de trabalho

**Para o Novo Forms:**

1. **Compilação na exibição da área de trabalho:** Inicie com funcionalidade completa.
2. **Teste no tablet:** Verifique as adaptações para telas médias.
3. **Validar em dispositivos móveis:** garanta a usabilidade em telas pequenas.
4. **Corrigir problemas responsivos:** Ajuste layouts conforme necessário.
5. **Retestar todos os dispositivos:** Confirme as correções em todos os tamanhos.

**Para Forms Existente:**

1. **Verificação rápida de celular:** o formulário funciona em telefones?
2. **Identificar áreas com problemas:** Problemas de layout de observação e usabilidade.
3. **Teste sistemático:** teste completamente cada tamanho de dispositivo.
4. **Problemas de documento:** Acompanhe o que precisa ser corrigido.
5. **Implementar correções:** Resolver problemas metodicamente.

## Parte 2: Seleção de padrões de layout responsivos

Os padrões de layout determinam como o conteúdo do formulário se adapta a diferentes tamanhos de tela. O padrão correto melhora a experiência do usuário e o desempenho móvel.

### Visão geral do padrão de layout

| **Tipo de layout** | **Melhor para** | **Desempenho móvel** | **Complexidade** |
|---------------------|-------------------------------------------|------------------------|----------------|
| **Layout do painel** | Conteúdo categorizado, formulários de estilo de painel | Bom | Baixa |
| **Layout do Assistente** | Processos em várias etapas, fluxos de trabalho complexos | Excelente | Média |
| **Layout da opção** | Conteúdo no estilo das perguntas frequentes, seções opcionais | Excelente | Baixa |

### Guia de decisão rápida

**Usar Layout do Painel quando:**

- Seu conteúdo é dividido em categorias distintas
- Os usuários precisam visualizar várias seções de uma só vez
- O conteúdo é relativamente simples

**Usar Layout do Assistente quando:**

- O formulário tem várias etapas lógicas
- Você quer reduzir a carga cognitiva
- Os usuários móveis são o público principal

**Usar Layout Acordeão quando:**

- O formulário tem conteúdo opcional ou secundário
- A conservação do espaço é importante
- O conteúdo pode ser agrupado logicamente

### Layout do painel

O Layout do painel organiza o conteúdo relacionado em seções visualmente distintas, permitindo que os usuários visualizem várias seções de uma só vez. Esse layout é ideal para formulários com informações categorizadas que se beneficiam de uma apresentação lado a lado em telas maiores.

![Exemplo de layout do painel](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Comportamento responsivo**

- **Área de Trabalho (1200px e superior):** Painéis são exibidos lado a lado ou em uma grade para máxima visibilidade.
- **Tablet (768px-1199px):** os painéis são empilhados verticalmente com espaçamento apropriado para manter a clareza.
- **Dispositivo móvel (320px-767px):** os painéis são apresentados em um layout de coluna única, com separação clara entre seções para facilitar a navegação.

**Como implementar**

1. Adicione o [Componente de Painel](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) ao formulário.
2. Agrupe campos relacionados em cada painel para manter a organização lógica.
3. Atribua cabeçalhos claros e descritivos a cada seção do painel.
4. Verifique se há espaçamento suficiente entre os painéis para evitar desordem visual.

**Práticas recomendadas**

- Limite o número de painéis para 3 ou 4 no desktop para evitar sobrecarregar os usuários.
- Use títulos concisos e descritivos para cada painel para auxiliar a compreensão do usuário.
- Organize campos dentro de painéis logicamente para minimizar a carga cognitiva.
- Teste a navegação do painel em dispositivos de toque para garantir a usabilidade em todas as plataformas.

**Casos de uso comuns**

- **Aplicativo de Trabalho:** Seções para Informações Pessoais, Educação, Experiência e Referências.
- **Registro do Produto:** Painéis para Detalhes Básicos, Especificações Técnicas e Informações de Garantia.
- **Forms de Pesquisa:** Agrupamentos para Demografia, Preferências, Comentários e Informações de Contato.

### Layout do assistente

O Layout do assistente orienta os usuários por um processo de várias etapas, apresentando uma seção de cada vez. Esse layout é especialmente eficaz para formulários complexos, pois reduz a carga cognitiva e aumenta as taxas de conclusão quebrando o processo em etapas controláveis.

![Exemplo de layout do assistente](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Comportamento responsivo**

- **Todos os Dispositivos:** Mantém o foco em uma única etapa, o que é ideal para usuários móveis.
- **Conteúdo da Etapa:** cada etapa se adapta com agilidade, empilhando campos ou organizando-os lado a lado conforme apropriado para o tamanho da tela.
- **Navegação:** apresenta botões de toque com espaçamento adequado para facilitar a interação.
- **Indicador de progresso:** Barras de progresso ou indicadores de etapa são dimensionados adequadamente para dispositivos diferentes, fornecendo feedback claro sobre o status de conclusão.

**Como implementar**

1. Insira o [Componente de Assistente](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) no formulário.
2. Divida o formulário em etapas lógicas, idealmente entre 3 e 7, para manter cada etapa focalizada e gerenciável.
3. Adicione indicadores de progresso para ajudar os usuários a entender sua posição no processo.
4. Forneça controles de navegação claros, como os botões Próximo, Voltar e Salvar.

**Dicas de Otimização Móvel**

- Use destinos de toque grande (pelo menos 44 px de altura) para controles de navegação para melhorar a acessibilidade.
- Verifique se os indicadores de etapa estão visíveis e legíveis em telas pequenas.
- Limite o número de campos por etapa para minimizar a rolagem e melhorar o foco.
- Ative a funcionalidade de salvamento automático para impedir a perda de dados se os usuários deixarem o formulário.

**Práticas recomendadas**

- Etapas de design para seguir uma progressão lógica, com cada etapa tendo como base a anterior.
- Use títulos claros e descritivos para cada etapa para definir as expectativas do usuário.
- Valide a entrada do usuário em cada etapa para detectar erros antecipadamente e reduzir a frustração.
- Permite que os usuários naveguem para trás para revisar ou editar informações anteriores sem perder dados.

**Casos de uso comuns**

- **Reivindicações de Seguro:** Etapas para Detalhes do Incidente, Envio de Evidências, Informações Pessoais e Revisão.
- **Configuração de Conta:** Estágios para Informações Básicas, Preferências, Configurações de Segurança e Confirmação.
- **Processo do pedido:** Etapas para seleção de produto, informações de envio, detalhes de pagamento e resumo do pedido.

### Layout do acordeão

O Layout do Acordeão economiza espaço organizando o conteúdo em seções que podem ser recolhidas, tornando-o ideal para informações opcionais ou secundárias. Esse layout é particularmente eficiente para formulários com conteúdo que pode ser agrupado logicamente e não precisa ser exibido de uma só vez.

![Exemplo de layout do acordeão](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Comportamento responsivo**

- **Desempenho móvel:** somente a seção relevante é expandida, reduzindo a necessidade de rolagem e melhorando os tempos de carregamento.
- **Cabeçalhos otimizados para toque:** os cabeçalhos de seção são fáceis de tocar e expandir, oferecendo suporte a gestos naturais em dispositivos móveis.
- **Animações Suaves:** Expandir e recolher seções fornece comentários visuais para as interações do usuário.
- **Eficiência de Espaço:** as seções recolhidas minimizam o espaço vertical, tornando o formulário mais fácil de navegar em todos os dispositivos.

**Como implementar**

1. Adicione o [Componente Acordeão](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) ao seu formulário.
2. Agrupe o conteúdo opcional ou secundário relacionado em cada seção do acordeão.
3. Use cabeçalhos claros e descritivos para cada seção para ajudar os usuários a entender quais informações estão contidas em.
4. Defina os estados de abertura ou fechamento padrão apropriados para cada seção com base na importância e nas necessidades do usuário.

**Vantagens móveis**

- Reduz a rolagem ao recolher seções não usadas, permitindo que os usuários se concentrem em uma seção por vez.
- A interação amigável ao toque suporta gestos de expansão/recolhimento naturais.
- Carregamento mais rápido, pois somente o conteúdo ativo está visível.
- Foco aprimorado, já que os usuários veem somente as informações de que precisam em um determinado momento.

**Práticas recomendadas**

- Use limpar cabeçalhos de seção para que os usuários saibam o que esperar antes de expandir uma seção.
- Agrupe o conteúdo relacionado logicamente em cada seção para auxiliar na compreensão.
- Defina seções importantes para começar a expandir se for necessária atenção imediata.
- Forneça visualizações de seção resumidas ou resumos para ajudar os usuários a decidir quais seções expandir.

**Casos de uso comuns**

- **Configuração do Produto:** Seções de Opções Básicas, Configurações Avançadas, Acessórios e Suporte.
- **Perguntas frequentes sobre Forms:** Agrupamentos para perguntas sobre Conta, Faturamento, Técnico e Geral.
- **Configurações Forms:** Seções para opções de Privacidade, Notificações, Aparência e Avançadas.


## Parte 3: Práticas recomendadas de design responsivo

### Práticas recomendadas por tipo de dispositivo

+++Otimização móvel (320px-767px)

**Layout e interação:**

- Use um layout de coluna única para todo o conteúdo do formulário para maximizar a legibilidade e a facilidade de uso.
- Verifique se todos os botões e elementos interativos têm pelo menos 44 px de altura para uma interação de toque confiável.
- Fornece navegação clara e simples com botões de voltar e próximo visíveis.
- Minimize a necessidade de rolagem em cada seção separando formulários longos.
- Focalize automaticamente no primeiro campo de entrada para avisar o teclado móvel.

**Diretrizes de Campo:**

- Os campos de texto devem abranger a largura total da tela com preenchimento suficiente para entrada por toque.
- Use a lista suspensa nativa/selecione elementos para obter a usabilidade móvel ideal.
- Implemente seletores de data nativos para obter experiência móvel consistente.
- Torne grandes as áreas de upload de arquivos e claramente rotuladas para facilitar o acesso.

+++

+++Otimização do tablet (768px-1199px)

**Layout e Usabilidade:**

- Use layouts de duas colunas para campos relacionados a fim de aproveitar o espaço aumentado da tela.
- Teste a aparência do formulário e a usabilidade nas orientações de retrato e paisagem.
- Design para entrada de toque e mouse, garantindo que todos os controles sejam facilmente acessíveis.
- Aumente o tamanho da área de conteúdo mantendo uma hierarquia visual clara e a legibilidade.

+++

+++Otimização para desktop (1200px+)

**Layout e Recursos Avançados:**

- Use layouts de várias colunas para usar o espaço horizontal com eficiência e reduzir a rolagem vertical.
- Forneça atalhos de teclado para ações frequentes de suporte a usuários avançados.
- Implemente estados de focalização e feedback visual para elementos interativos.
- Ofereça validação avançada com mensagens de erro claras e detalhadas para formulários complexos.

+++

## Configurar layouts personalizados com pontos de interrupção de consulta de mídia

Ao criar layouts personalizados para componentes no Forms Adaptável usando o **Editor Universal**, você deve definir o comportamento responsivo usando os **pontos de interrupção de consulta de mídia CSS**. Isso garante que os formulários sejam renderizados corretamente em diferentes dispositivos e tamanhos de tela.

**Pontos de interrupção recomendados (com base nos Componentes principais do AEM)**

| **Tipo de dispositivo** | **Ponto de interrupção recomendado** |
|-----------------|---------------------------|
| **Área de Trabalho** | `min-width: 1200px` |
| **Tablet** | `min-width: 768px and max-width: 1199px` |
| **Móvel** | `max-width: 767px` |

**Pontos principais**

- Use esses pontos de interrupção para controlar como os componentes são redimensionados, empilhados ou ocultados em dispositivos diferentes.
- Siga as diretrizes de design responsivo da organização para obter um UX consistente.
- Teste layouts em vários dispositivos e orientações para garantir a usabilidade e a acessibilidade.

```css
/* Example: Stack form fields on smaller screens */
@media (max-width: 767px) {
  .custom-form-container {
    display: flex;
    flex-direction: column;
  }
}
```

>[!NOTE]
>
> O Editor Universal não fornece uma interface para definir o comportamento responsivo. Toda a personalização de layout deve ser feita por meio de CSS.



## Resolução de problemas

### Problemas de layout

+++Quebras de layout de formulário em dispositivos móveis

**Causas possíveis:**

- Elementos de largura fixa que não se adaptam a telas menores
- CSS do primeiro desktop que substitui estilos móveis
- Imagens ou conteúdo que transborda seus contêineres

**Como Corrigir:**

- Verifique se todas as imagens e contêineres usam dimensionamento relativo ou baseado em porcentagem.
- Comece com uma abordagem CSS móvel e crie camadas de aprimoramentos para telas maiores.
- Teste formulários usando emuladores de dispositivo e dispositivos reais.
- Evite dimensões fixas; use layouts flexíveis.

+++

+++Destinos de toque muito pequenos

**Causas possíveis:**

- Botões ou links menores que 44px por 44px
- Elementos interativos posicionados muito próximos
- CSS personalizado reduzindo o tamanho de destino de toque padrão

**Como Corrigir:**

- Verifique se cada elemento interativo tem no mínimo 44px por 44px.
- Adicione um espaçamento adequado entre botões, links e outros controles.
- Teste com dispositivos de toque reais, não apenas com um mouse.
- Expanda as áreas de destino de toque conforme necessário para acessibilidade.

+++

+++Problemas de estouro de conteúdo

**Causas possíveis:**

- Texto longo ou rótulos que não quebram automaticamente
- Contêineres com larguras fixas
- Imagens que não são dimensionadas responsivamente

**Como Corrigir:**

- Ativar quebra automática de texto para todos os rótulos e conteúdo.
- Use imagens responsivas que são dimensionadas com o container.
- Criar layouts flexíveis que se adaptam a tamanhos variáveis de conteúdo.
- Teste o conteúdo curto e o conteúdo longo para garantir a adaptabilidade.

+++

### Problemas de desempenho

+++Carregamento lento em dispositivos móveis

**Causas possíveis:**

- Imagens grandes, não otimizadas
- JavaScript pesado ou excessivo
- Muitos campos de formulário carregando simultaneamente

**Como Corrigir:**

- Otimizar imagens para dispositivos móveis e usar formatos de arquivo apropriados.
- Adiar ou carregar lentamente conteúdo não crítico.
- Minimize o uso de scripts e widgets de terceiros.
- Simplifique os campos de formulário para carregar somente o que é necessário.

+++

### Problemas de teste e validação

+++Diferenças entre o emulador e o dispositivo real

**Causas possíveis:**

- Diferenças nos mecanismos de renderização do navegador
- Interação de toque não simulada com precisão pelo mouse
- Discrepâncias de velocidade da rede

**Como Corrigir:**

- Sempre testar em dispositivos reais além de emuladores.
- Use vários navegadores e dispositivos para testes abrangentes.
- Simular várias velocidades de rede para identificar gargalos de desempenho.
- Obtenha feedback de usuários reais no seu público-alvo.

+++

## Métricas de sucesso para o Responsive Forms

+++Indicadores-chave de desempenho

**Experiência do Usuário:**

- **Taxa de conclusão de formulário:** Objetivo para 85% ou mais em dispositivos móveis.
- **Tempo para concluir:** usuários móveis devem concluir formulários dentro de 20% do tempo de conclusão da área de trabalho.
- **Taxa de erros:** Mantenha os erros de validação abaixo de 5%.
- **Pontos de abandono:** identifique e encaminhe as etapas nas quais os usuários são liberados.

**Desempenho Técnico:**

- **Tempo de carregamento da página:** Menos de 3 segundos em uma conexão 3G.
- **Web Vitals Principais:** Atenda ou exceda os limites recomendados pela Google.
- **Acessibilidade:** atenda à conformidade WCAG 2.1 AA.
- **Compatibilidade do navegador:** verifique a funcionalidade de mais de 98% em todos os principais navegadores.

+++

+++Lista de verificação de teste

**Lista de Verificação de Pré-Publicação:**

- Teste o formulário em dispositivos móveis reais (não apenas emuladores).
- Verifique se todos os destinos de toque têm pelo menos 44px × 44px.
- Verifique a legibilidade do texto em todos os tamanhos de tela compatíveis.
- Confirme se a validação de formulário funciona de maneira consistente em dispositivos e navegadores.
- Verifique se o tempo de carregamento do dispositivo móvel está abaixo de 3 segundos.
- Verifique se todos os elementos interativos podem ser acessados pelo teclado e pelos leitores de tela.
- Teste o envio de formulário em todos os dispositivos compatíveis.


+++

## Próximas etapas

**Ações imediatas:**

1. **Faça a auditoria dos formulários atuais:** Teste formulários existentes usando o emulador de dispositivo.
2. **Identifique ganhos rápidos:** corrija primeiro problemas óbvios de usabilidade móvel.
3. **Priorizar formulários de alto tráfego:** Concentre-se nos formulários com maior impacto para o usuário.
4. **Implemente uma abordagem móvel:** comece com o menor design de tela.

**Otimização avançada:**

- **Monitoramento de desempenho**: configure análises para rastrear métricas de formulário.
- **Teste A/B:** experimente com diferentes layouts e abordagens.
- **Coleção de comentários do usuário:** Obtenha insights de usuários reais.
- **Aperfeiçoamento contínuo:** examine e otimize formulários regularmente.


