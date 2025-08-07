---
title: Criar Forms responsivo com editor universal
description: Saiba como projetar, testar e otimizar formulários responsivos para todos os dispositivos usando o Universal Editor. Teste de dispositivo mestre, padrões de layout e técnicas de otimização para dispositivos móveis para AEM Forms com Edge Delivery Services.
keywords: formulários responsivos, formulários móveis, teste de dispositivo, editor universal, layout adaptável, otimização de formulário, design móvel, design responsivo, layouts de formulário, emulador de dispositivo
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: ccfb85da187e828b5f7e8b1a8bae3f483209368d
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 0%

---


# Criar Forms responsivo com editor universal

Os usuários acessam formulários em uma grande variedade de dispositivos, incluindo desktops, tablets e smartphones. A criação de formulários responsivos garante uma experiência ideal para todos os usuários, independentemente do dispositivo. Este guia explica como projetar, testar e otimizar formulários para qualquer tamanho de tela usando o Universal Editor.


A criação responsiva de formulários envolve duas atividades principais:

- **Teste responsivo:** Visualize e teste seus formulários em vários tamanhos de tela usando emuladores de dispositivo.
- **Design responsivo:** Selecione e implemente padrões de layout que se adaptem perfeitamente a diferentes dispositivos.

**Neste guia, você aprenderá a:**

- Testar formulários em dispositivos desktop, tablet e móveis
- Selecione os padrões de layout apropriados para o seu conteúdo
- Aplicar práticas recomendadas de design responsivo
- Solução de problemas comuns de formulários responsivos
- Otimizar formulários para desempenho móvel

## Por que o Forms responsivo é importante

**Impacto na experiência do usuário:**

- Mais de 60% dos usuários acessam formulários em dispositivos móveis
- Experiências móveis ruins resultam em uma taxa de abandono 67% maior
- Formulários responsivos podem aumentar as taxas de conclusão em até 25%

**Benefícios para os negócios:**

- Taxas mais altas de conclusão de formulários
- Maior satisfação do usuário
- Conformidade aprimorada com acessibilidade
- Reduzir os custos de desenvolvimento e manutenção

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

**Propósito:** Organiza o conteúdo relacionado em seções visualmente distintas que podem ser visualizadas simultaneamente.

![Exemplo de layout do painel](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Comportamento responsivo:**

- **Área de Trabalho (1200px+):** Painéis exibidos lado a lado ou em uma grade
- **Tablet (768px-1199px):** Painéis empilhados verticalmente com espaçamento
- **Dispositivo móvel (320px-767px):** Layout de coluna única com quebras de seção claras

**Etapas de implementação:**

1. Use o [Componente de Painel](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).
2. Agrupar campos relacionados em cada painel.
3. Adicione cabeçalhos claros para cada seção.
4. Assegure um espaçamento adequado entre os painéis.

**Práticas recomendadas:**

- Limite de 3 a 4 painéis no desktop para evitar sobrecarregar os usuários.
- Use títulos descritivos para cada painel.
- Agrupar campos relacionados logicamente para reduzir a carga cognitiva.
- Teste a navegação do painel em dispositivos de toque.

**Exemplo de casos de uso:**

- **Aplicativo de Trabalho:** Informações Pessoais, Educação, Experiência, Referências
- **Registro do Produto:** Detalhes Básicos, Especificações Técnicas, Informações de Garantia
- **Forms de Pesquisa:** Demografia, Preferências, Comentários, Contato

### Layout do assistente

**Propósito:** orienta os usuários sobre processos complexos passo a passo, reduzindo a carga cognitiva e melhorando as taxas de conclusão.

![Exemplo de layout do assistente](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Comportamento responsivo:**

- **Todos os Dispositivos:** mantém o foco de etapa única para obter a experiência móvel ideal.
- **Conteúdo da Etapa:** Adapta-se dentro de cada etapa (empilhamento ou lado a lado).
- **Navegação:** botões de toque simples com espaçamento suficiente.
- **Indicador de Progresso:** Dimensionado adequadamente para o tamanho da tela.

**Etapas de implementação:**

1. Use o [Componente de Assistente](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).
2. Divida formulários complexos em etapas lógicas (3 a 7 etapas são ideais).
3. Incluir indicadores de progresso para orientação do usuário.
4. Forneça controles de navegação claros (Próximo, Voltar, Salvar).

**Otimização móvel:**

- Use destinos de toque grande (mínimo de 44px) para botões de navegação.
- Verifique se os indicadores de etapa estão claros e visíveis em telas pequenas.
- Limite o número de campos por etapa para reduzir a rolagem.
- Ative o salvamento automático para evitar perda de dados.

**Práticas recomendadas:**

- Assegurar a progressão lógica da etapa — cada etapa deve se basear na anterior.
- Use títulos de etapas claras para que os usuários saibam o que esperar.
- Valide a entrada em cada etapa para detectar erros antecipadamente.
- Permite que os usuários recuem para revisar ou editar informações.

**Exemplo de casos de uso:**

- **Reivindicações de Seguro:** Incidente → Evidência → Pessoal → Revisão
- **Configuração da Conta:** Informações Básicas → Preferências → Segurança → Confirmação
- **Processo do pedido:** Produtos → Envio → Pagamento → Resumo

### Layout do acordeão

**Propósito:** economiza espaço organizando o conteúdo em seções que podem ser recolhidas, ideal para informações opcionais ou secundárias.

![Exemplo de layout do acordeão](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Comportamento responsivo:**

- **Excelente desempenho móvel:** somente conteúdo relevante é exibido.
- **Cabeçalhos otimizados para toque:** Fáceis de tocar e expandir seções.
- **Animações suaves:** fornece feedback visual para interações.
- **Eficiência de espaço:** minimiza a rolagem em todos os dispositivos.

**Etapas de implementação:**

1. Use o [Componente Acordeão](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).
2. Agrupe o conteúdo opcional relacionado em cada seção.
3. Use cabeçalhos de seção descritiva.
4. Defina os estados de abertura/fechamento padrão apropriados.

**Vantagens móveis:**

- Reduz a rolagem recolhendo seções não usadas.
- Interação amigável ao toque com gestos de expansão/colapso naturais.
- Carregamento mais rápido — somente o conteúdo ativo fica visível.
- Foco aprimorado — os usuários veem somente o que precisam.

**Práticas recomendadas:**

- Use cabeçalhos de seção limpa para que os usuários saibam o que há dentro antes de expandir.
- Agrupe o conteúdo relacionado logicamente em cada seção.
- Defina seções importantes para iniciar a expansão, se necessário.
- Forneça breves visualizações de seção para ajudar os usuários a decidir o que expandir.

**Exemplo de casos de uso:**

- **Configuração do produto:** Básico → Avançado → Acessórios → Suporte
- **Perguntas frequentes Forms:** Conta → Faturamento → Técnico → Geral
- **Configurações Forms:** Privacidade → Notificações → Aparência → Avançado

## Parte 3: Práticas recomendadas de design responsivo

### Práticas recomendadas por tipo de dispositivo

+++Otimização móvel (320px-767px)

**Práticas essenciais:**

- Use um layout de coluna única para todo o conteúdo.
- Oferece botões grandes e sensíveis ao toque (altura mínima de 44 px).
- Simplifique a navegação com opções claras de voltar/avançar.
- Minimize a rolagem em cada seção.
- Foco automático no primeiro campo para exibir o teclado.

**Diretrizes Específicas de Campo:**

- **Entradas de texto:** Largura total com preenchimento de amostra.
- **Menus suspensos:** use elementos nativos selecionados para obter uma melhor experiência de toque.
- **Seletores de data:** use entradas de data nativas para compatibilidade móvel.
- **Carregamentos de arquivos:** forneça áreas de carregamento grandes e claras.

+++

+++Otimização do tablet (768px-1199px)

**Estratégias de layout:**

- Use layouts de duas colunas para campos relacionados.
- Teste as orientações retrato e paisagem.
- São compatíveis com interações com toque e mouse.
- Fornecer áreas de conteúdo maiores, mantendo a legibilidade.

+++

+++Otimização de desktop (1200px+)

**Recursos Avançados:**

- Use layouts de várias colunas para um uso eficiente do espaço.
- Ofereça atalhos de teclado para usuários avançados.
- Implemente estados de focalização para feedback interativo.
- Fornecer validação avançada com mensagens de erro detalhadas.

+++

## Solução de problemas abrangente

### Problemas de layout

+++Quebras de layout de formulário em dispositivos móveis

**Causas Comuns:**

- Elementos de largura fixa que não são dimensionados
- CSS projetado para layouts de desktop
- Imagens ou conteúdo que excedem seus contêineres

**Soluções:**

- Verifique se as imagens e os contêineres são dimensionados de acordo com o tamanho da tela.
- Use um design móvel com aprimoramento progressivo.
- Teste com emuladores de dispositivo e dispositivos reais.
- Use dimensionamento flexível em vez de dimensões fixas.

+++

+++Destinos de toque muito pequenos

**Causas Comuns:**

- Botões menores que 44px × 44px
- Elementos interativos posicionados muito próximos
- Substituição de padrões amigáveis ao toque por CSS personalizado

**Soluções:**

- Verifique se todos os elementos interativos estão no mínimo em 44px × 44px.
- Adicionar espaçamento entre botões e links.
- Teste a interação com os dedos reais, não apenas com o mouse.
- Aumente as áreas de destino de toque para facilitar o toque.

+++

+++Problemas de estouro de conteúdo

**Causas Comuns:**

- Texto longo ou rótulos que não quebram automaticamente
- Contêineres de largura fixa
- Imagens que não são dimensionadas corretamente

**Soluções:**

- Ativar quebra de texto para conteúdo longo.
- Use imagens responsivas que sejam dimensionadas adequadamente.
- Implementar layouts flexíveis que se adaptam ao conteúdo.
- Teste com vários comprimentos de conteúdo.

+++

### Problemas de desempenho

+++Carregamento lento em dispositivos móveis

**Causas Comuns:**

- Imagens grandes não otimizadas para dispositivos móveis
- Execução excessiva do JavaScript
- Muitos campos de formulário carregando de uma vez

**Soluções:**

- Otimizar imagens para tamanhos de tela diferentes.
- Carregue conteúdo não crítico somente quando necessário.
- Use técnicas para acelerar o carregamento móvel.
- Minimize scripts e widgets de terceiros.

+++

### Problemas de teste e validação

+++Emulador vs. Diferenças reais do dispositivo

**Causas Comuns:**

- Diferenças de renderização específicas do navegador
- Diferenças de interação entre toque e mouse
- Variações de velocidade da rede

**Soluções:**

- Testar em dispositivos reais sempre que possível.
- Use vários navegadores para testes de emulador.
- Simular velocidades de rede diferentes durante o teste.
- Validar com usuários reais em ambientes de destino.

+++

## Métricas de sucesso para o Responsive Forms

+++Indicadores-chave de desempenho

**Métricas de experiência do usuário:**

- **Taxa de conclusão de formulário:** Target 85%+ em dispositivos móveis
- **Tempo para concluir:** o tempo de conclusão móvel deve estar dentro de 20% da área de trabalho
- **Taxa de erros:** Menos de 5% de erros de validação
- **Pontos de abandono:** identifique onde os usuários caem

**Desempenho Técnico:**

- **Tempo de carregamento da página:** Em 3 segundos em redes 3G
- **Web Vitals Principais:** Aprovados em todos os benchmarks de desempenho da Google
- **Pontuação de acessibilidade:** Conformidade com a WCAG 2.1 AA
- **Compatibilidade entre navegadores:** Funcionalidade 98%+ nos principais navegadores

+++

+++Lista de verificação de teste

**Antes de publicar:**

- Teste o formulário em dispositivos móveis reais.
- Verifique se todos os destinos de toque têm pelo menos 44px × 44px.
- Verifique a legibilidade do texto em todos os tamanhos de tela.
- Confirmar se a validação de formulário funciona em todos os dispositivos.
- Verifique se o tempo de carregamento está abaixo de 3 segundos no dispositivo móvel.
- Verifique se todos os elementos interativos estão acessíveis.
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


