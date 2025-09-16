---
title: Form Analytics com Adobe Analytics e AEM Forms - Guia completo
seo-title: "Form Analytics: Track Performance, Boost Conversions with Adobe Analytics & AEM Forms"
description: Guia completo para análise de formulários com o Adobe Analytics e o AEM Forms. Acompanhe o desempenho do formulário, analise o comportamento do usuário, reduza o abandono e otimize as conversões.
keywords: análise de formulários, rastreamento de desempenho de formulários, análise de abandono de formulários, otimização de conversão, análise de comportamento do usuário, Adobe Analytics forms, AEM Forms analytics
exl-id: 0730432e-75b8-4b35-a377-ae4a2bee6c9f
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '7898'
ht-degree: 0%

---


# Form Analytics com Adobe Analytics e AEM Forms - Guia completo {#integrate-aem-forms-with-adobe-analytics}

## O que é o Form Analytics?

Análise de formulários é o processo de coletar, medir e analisar dados sobre como os usuários interagem com seus formulários. Ele fornece insights sobre o comportamento do usuário, identifica gargalos no processo de conclusão de formulários e ajuda a otimizar formulários para obter melhores taxas de conversão.

A análise de formulários vai além do simples rastreamento de envio para fornecer insights abrangentes sobre cada aspecto da experiência do usuário. Analisando como os usuários interagem com campos de formulário individuais, padrões de navegação e comportamentos de conclusão, as organizações podem fazer melhorias orientadas por dados que afetam significativamente os resultados dos negócios.

### Conceitos principais do Form Analytics

**Rastreamento de interação do usuário**
A análise de formulários captura informações detalhadas sobre como os usuários se envolvem com formulários, incluindo o tempo gasto em cada campo, movimentos do mouse, comportamento de rolagem e padrões de interação. Esses dados granulares ajudam a identificar problemas de usabilidade e oportunidades de otimização.

**Análise de Padrão Comportamental**
Ao analisar os padrões de comportamento do usuário em várias sessões de formulário, as organizações podem identificar jornadas comuns do usuário, pontos de abandono típicos e caminhos de conclusão bem-sucedidos. Essa análise permite melhorias direcionadas que atendem às necessidades reais do usuário.

**Avaliação de desempenho**
O Form Analytics fornece métricas quantitativas que medem a eficácia do formulário, incluindo taxas de conversão, tempos de conclusão, frequências de erro e indicadores de satisfação do usuário. Essas métricas permitem a avaliação objetiva do desempenho do formulário e do impacto da otimização.

### Por que o formulário Analytics é importante para os negócios

A análise de formulários transforma dados brutos de interação do usuário em insights comerciais acionáveis que promovem melhorias mensuráveis nas principais métricas de negócios:

**Otimização do Índice de Conversão**
O abandono de formulários é um desafio crítico para os negócios que afeta diretamente a receita e a geração de leads. Pesquisas mostram que 68% dos usuários abandonam formulários antes da conclusão, tornando a análise de formulários essencial para identificar pontos de interrupção. A análise de formulários permite estratégias de otimização de conversão direcionadas que podem aumentar significativamente o desempenho dos formulários. A otimização de conversão eficaz por meio da análise de formulários fornece melhorias mensuráveis na geração de leads e na aquisição de clientes.

**Aperfeiçoamento da Experiência do Usuário**
Entender as dificuldades do usuário e os pontos problemáticos permite que as organizações criem experiências de formulário mais suaves e intuitivas. Isso resulta em maior satisfação do cliente, custos de suporte reduzidos e melhor percepção da marca.

**Tomada de decisão orientada por dados**
Em vez de depender de suposições ou práticas recomendadas, a análise de formulários fornece dados concretos sobre a análise do comportamento do usuário. Isso permite uma otimização de conversão baseada em evidências que fornece resultados significativamente melhores do que as alterações baseadas em intuição. A análise do comportamento do usuário por meio do rastreamento do desempenho do formulário garante que os esforços de otimização se concentrem nas necessidades reais do usuário, em vez de em suposições.

**Medição e justificação do ROI**
A análise de formulários quantifica o impacto dos esforços de otimização, fornecendo métricas claras que demonstram o valor comercial. As empresas podem medir a correlação direta entre as melhorias de formulários e os resultados de negócios, como geração de leads, conversão de vendas e custos de aquisição de clientes.

**Vantagem competitiva**
Experiências de forma superiores se tornam um diferencial competitivo na aquisição de clientes. As organizações que usam a análise de formulários podem criar as melhores experiências do setor para o usuário, com desempenho superior ao dos concorrentes e impulsionando o crescimento da participação no mercado.

### Métricas principais do Form Analytics

A análise de formulários eficiente se concentra em métricas que afetam diretamente os resultados de negócios e fornecem insights acionáveis para otimização:

**Métricas Primárias de Sucesso**

- **Taxa de Conversão de Formulário**: a porcentagem de exibições de formulário que resultam em envios bem-sucedidos - a medida final da eficácia do formulário
- **Taxa de abandono de formulário**: onde e por que os usuários abandonam, fornecendo insight direto aos problemas de experiência do usuário
- **Hora de conclusão**: quanto tempo os usuários levam para preencher formulários, indicando complexidade e qualidade da experiência do usuário

**Indicadores de Desempenho Detalhados**

- **Análise em Nível de Campo**: quais campos específicos causam problemas, permitindo esforços de otimização direcionados
- **Análise de Taxa de Erro**: problemas de validação e erros do usuário que impedem o preenchimento bem-sucedido do formulário
- **Padrões de Uso da Ajuda**: quando e onde os usuários precisam de assistência, indicando áreas a serem aprimoradas

**Métricas Comportamentais Avançadas**

- **Análise de funil de conversão**: jornada de usuário em formulários de várias etapas, mostrando padrões de progressão e distribuição
- **Desempenho do dispositivo e do navegador**: fatores técnicos que afetam a conclusão em diferentes ambientes de usuário
- **Profundidade do Envolvimento do Usuário**: tempo gasto em formulários, padrões de interação de campo e indicadores de atenção do usuário

**Métricas de impacto nos negócios**

- **Correlação de Qualidade de Cliente Potencial**: como o comportamento de conclusão do formulário se relaciona com a conversão de cliente potencial e o valor do cliente
- **Tráfego Source Performance**: quais canais de marketing direcionam os envios de formulários de maior qualidade
- **Impacto de temporada e campanha**: como o desempenho do formulário varia com as atividades de marketing e fatores externos

## Benefícios comerciais do Form Analytics

A implementação da análise de formulários oferece valor comercial mensurável em várias dimensões. As organizações que utilizam análises de formulários normalmente veem melhorias significativas nas taxas de conversão, na satisfação do usuário e na eficiência operacional.

### &#x200B;1. Reduzir o abandono de formulários e aumentar as conversões

O abandono de formulários é um desafio crítico para os negócios que afeta diretamente a receita e a geração de leads:

- **Identificar pontos de devolução**: controle exatamente onde os usuários abandonam formulários para apontar campos ou seções problemáticas
- **Otimizar Fluxo de Formulário**: Reorganizar, simplificar ou remover campos que causam as taxas de abandono mais altas
- **Melhorias do teste A/B**: teste diferentes variações de formulário e meça seu impacto nas taxas de conclusão
- **Otimização móvel**: identificar problemas específicos de dispositivos móveis que impedem o preenchimento de formulários
- **Monitoramento em tempo real**: obtenha alertas imediatos quando o desempenho do formulário for degradado

**Impacto nos negócios**: normalmente, as empresas observam uma melhora significativa nas taxas de conversão de formulários após implementarem otimizações orientadas por análise.

### &#x200B;2. Melhorar a experiência do usuário e a satisfação

O Form Analytics fornece insights profundos do comportamento do usuário e pontos problemáticos:

- **Reduzir Tempo de Conclusão**: identifique campos que demoram muito para serem concluídos e simplifique o processo
- **Minimizar frustração do usuário**: controle padrões de erro e problemas de validação para melhorar a usabilidade do formulário
- **Otimizar Ordem de Campo**: organize os campos na sequência mais lógica e amigável
- **Melhorar Ajuda e Orientação**: identifique onde os usuários precisam de assistência e forneça ajuda direcionada
- **Experiência entre dispositivos**: garanta um desempenho consistente em dispositivos móveis, tablets e computadores desktop

**Impacto nos negócios**: a experiência aprimorada do usuário resulta em maiores pontuações de satisfação do cliente e maior fidelidade à marca.

### &#x200B;3. Faça melhorias nos formulários orientados por dados

Substitua o trabalho de adivinhação por dados concretos ao otimizar formulários:

- **Decisões baseadas em evidências**: use dados reais de comportamento do usuário em vez de suposições para guiar as melhorias
- **Impacto de Otimização de Medida**: quantifique os resultados das alterações de formulário com análises antes/depois
- **Priorizar melhorias**: concentre-se nas alterações que terão maior impacto nas métricas comerciais
- **Otimização contínua**: estabelecer ciclos de aprimoramento contínuos com base em dados de desempenho
- **Relatórios das partes interessadas**: forneça métricas concretas para demonstrar o desempenho do formulário e o ROI

**Impacto nos negócios**: a otimização orientada por dados geralmente oferece resultados significativamente melhores do que as alterações baseadas em intuição.

### &#x200B;4. Aumente a qualidade do lead e a eficiência das vendas

O Form Analytics ajuda a otimizar não apenas a quantidade, mas a qualidade dos envios de formulários:

- **Integração de Pontuação de Cliente Potencial**: correlacione o comportamento do formulário com a qualidade do cliente potencial e o potencial de conversão
- **Atribuição do Source**: entender quais fontes de tráfego geram os envios de formulários de maior qualidade
- **Progressive Profiling**: otimizar formulários de várias etapas para coletar clientes em potencial mais qualificados
- **Insights de segmentação**: identificar padrões em comportamento de formulário de cliente de alto valor
- **Otimização da Transferência de Vendas**: forneça às equipes de vendas o contexto sobre as interações de formulário de clientes potenciais

**Impacto nos negócios**: leads de maior qualidade resultam em melhores taxas de conversão de vendas e custos reduzidos de aquisição de clientes.

### &#x200B;5. Eficiência operacional e redução de custos

A análise de formulários promove melhorias operacionais em toda a organização:

- **Reduzir Tíquetes de Suporte**: Identifique e corrija problemas comuns de formulários que geram chamadas de atendimento ao cliente
- **Otimização Automática**: Configurar alertas automatizados e regras de otimização com base em limites de desempenho
- **Alocação de recursos**: concentre os recursos de desenvolvimento em formulários e campos com o maior impacto nos negócios
- **Monitoramento de conformidade**: controle o desempenho do formulário para conformidade normativa e de acessibilidade
- **Eficiência da Integração**: otimizar integrações de formulário para sistema com base nos padrões de envio

**Impacto nos negócios**: as melhorias operacionais podem reduzir significativamente os custos de suporte relacionados ao formulário.

### &#x200B;6. Vantagem Competitiva Através Da Forms Superior

A análise de formulários permite que as organizações criem as melhores experiências de formulário do setor:

- **Desempenho de benchmark**: compare o desempenho de formulários com os padrões do setor e da concorrência
- **Oportunidades de inovação**: identificar oportunidades de otimização exclusivas que os concorrentes possam perder
- **Retenção de clientes**: experiências de formulários superiores contribuem para a satisfação e retenção gerais do cliente
- **Diferenciação de Mercado**: Use os insights de análise de formulários para criar vantagens competitivas na experiência do usuário
- **Otimização Escalável**: Aplicar padrões de formulário bem-sucedidos em vários produtos e campanhas

**Impacto nos negócios**: experiências de formulários superiores podem se tornar um diferencial competitivo significativo na aquisição de clientes.

## Casos de uso e exemplos do Form Analytics

Entender como a análise de formulários se aplica a cenários do mundo real ajuda as organizações a identificar oportunidades de otimização e implementar estratégias de medição eficazes. Estes são casos de uso comuns em diferentes setores e tipos de formulário.

### Forms de comércio eletrônico e varejo

**Check-out e Forms de Pagamento**

- **Desafio**: o alto abandono do carrinho durante o processo de finalização afeta diretamente a receita
- **Solução de análise de formulário**: controle as taxas de conclusão campo a campo e o desempenho do formulário para identificar pontos de atrito
- **Descobertas Comuns**: campos de cartão de crédito, validação de endereço de remessa e etapas de criação de conta geralmente causam abandono de formulário
- **Resultados da Otimização de Conversão**: normalmente, os varejistas observam uma melhora significativa na conclusão do check-out após a otimização do desempenho do formulário orientado por análise
- **Análise de Comportamento do Usuário**: Rastreie os padrões de abandono do carrinho para entender quando e por que os clientes saem durante o check-out
- **Impacto nos negócios**: a redução do abandono de formulários se traduz diretamente no aumento da receita e na melhoria dos custos de aquisição do cliente

**Forms de Registro e Garantia do Produto**

- **Desafio**: baixas taxas de registro de produtos que afetam o suporte ao cliente e o marketing
- **Solução do Analytics**: monitore as taxas de conclusão e identifique o impacto de campo opcional versus necessário
- **Estratégia de otimização**: reduza os campos obrigatórios e melhore a experiência móvel
- **Impacto nos negócios**: taxas de registro mais altas melhoram o valor vitalício do cliente e a eficiência do suporte

### Geração de leads e Forms B2B

**Solicitação de demonstração e de contato para o Forms**

- **Desafio**: equilibrar a qualidade do lead com as taxas de conclusão do formulário e minimizar o abandono do formulário
- **Solução de análise de formulário**: controle a correlação entre desempenho de formulário, comprimento de formulário e qualidade de conversão de cliente potencial
- **Principais insights**: a definição progressiva de perfis geralmente supera o desempenho de formulários de página única longos para otimização de conversão
- **Análise de Comportamento do Usuário**: monitore como o comprimento do formulário afeta as taxas de conclusão e as pontuações de qualidade dos clientes potenciais
- **Resultados da Otimização de Conversão**: as empresas B2B veem melhorias significativas na geração de leads qualificados por meio da otimização do desempenho do formulário
- **Impacto nos negócios**: análises de formulários de melhor qualidade resultam em clientes potenciais de maior qualidade e melhores taxas de conversão de vendas

**Webinar e Registro de Evento**

- **Desafio**: maximizar a participação no evento enquanto coleta as informações necessárias
- **Solução do Analytics**: monitorar a conclusão do registro em relação às taxas de participação reais
- **Padrões Comuns**: formulários mais curtos aumentam os registros, mas podem reduzir a qualidade da presença
- **Prática recomendada**: use a análise para encontrar o equilíbrio ideal entre o comprimento do formulário e a qualidade do participante

### Forms de serviços financeiros

**Pedidos de Empréstimo e Crédito**

- **Desafio**: aplicativos complexos de várias etapas com altas taxas de abandono
- **Solução do Analytics**: controle as taxas de conclusão em cada etapa e identifique os pontos de devolução
- **Insights Críticos**: as etapas de carregamento de documentos e verificação de renda geralmente causam abandono
- **Estratégia de otimização**: fornecer indicadores de progresso claros e funcionalidade de salvar e retomar
- **Considerações sobre Normas**: a análise deve estar em conformidade com os requisitos de privacidade de dados financeiros

**Cotação e reclamações de seguro Forms**

- **Desafio**: coletar informações detalhadas enquanto mantém o engajamento do usuário
- **Solução do Analytics**: monitore o tempo de conclusão e o envolvimento em nível de campo
- **Principais descobertas**: o preenchimento automático e os padrões inteligentes melhoram significativamente as taxas de conclusão
- **Impacto nos negócios**: a conclusão aprimorada do formulário está diretamente correlacionada às taxas de conversão da política

### Assistência médica e Forms médico

**Forms de Registro e Entrada de Paciente**

- **Desafio**: coletar informações médicas abrangentes com eficiência
- **Solução de análise**: controle as taxas de conclusão em diferentes dados demográficos de pacientes
- **Foco de acessibilidade**: monitorar o desempenho em diferentes dispositivos e ferramentas de acessibilidade
- **Prioridade de Otimização**: otimização móvel crítica para satisfação do paciente
- **Requisitos de conformidade**: conformidade com a HIPAA essencial para todas as implementações de análise

**Forms de Agendamento de Compromissos**

- **Desafio**: reduzir o número de não apresentações ao simplificar o processo de reserva
- **Solução do Analytics**: correlacione o comportamento de conclusão do formulário com a presença no compromisso
- **Principais Insights**: as preferências de confirmação e lembrete afetam significativamente a presença
- **Oportunidade de Integração**: conectar a análise de formulários com os sistemas de gerenciamento de compromissos

### Instituição educacional Forms

**Forms de Aplicativo e Inscrição**

- **Desafio**: gerenciar aplicativos complexos de várias etapas com requisitos de documentos
- **Solução do Analytics**: controle as taxas de conclusão em diferentes estágios do aplicativo
- **Métricas críticas**: padrões de uso de tempo até a conclusão e salvar e retomar
- **Foco de otimização**: a experiência móvel é cada vez mais importante para os aplicativos dos alunos
- **Considerações sobre a estação**: o desempenho varia bastante durante os períodos de aplicação

**Inscrição no curso e Forms de feedback**

- **Desafio**: maximizar a participação dos alunos com processos administrativos
- **Solução do Analytics**: monitore as taxas de conclusão e identifique problemas de experiência do usuário
- **Principais insights**: a integração com portais de alunos melhora as taxas de conclusão
- **Aprimoramento contínuo**: a análise regular é essencial para a otimização de semestre a semestre

### Cenários comuns do Form Analytics

**Otimização de formulários em várias etapas**

Os formulários de várias etapas geralmente atingem taxas de conversão 86% mais altas do que os formulários de página única quando otimizados adequadamente:

- **Análise passo a passo**: controle as taxas de conclusão em cada etapa do formulário
- **Impacto do Indicador de Progresso**: meça como as barras de progresso afetam as taxas de conclusão
- **Uso de Salvar e Retomar**: monitore como a gravação de rascunho afeta a conclusão final
- **Desempenho móvel vs. desktop**: Comparar taxas de conclusão entre dispositivos

**Análise de Desempenho em Nível de Campo**

- **Campos Obrigatórios vs. Opcionais**: Analisar o impacto dos requisitos de campo na conclusão
- **Otimização de Ordem de Campo**: teste sequências de campo diferentes para fluxo ideal
- **Padrões de Erro de Validação**: identificar erros comuns de usuário e melhorar a validação
- **Eficácia do Texto de Ajuda**: medir o impacto da orientação de campo nas taxas de conclusão

**Desempenho de temporada e campanha**

- **Análise de tráfego do Source**: comparar o desempenho dos formulários entre canais de marketing
- **Variações sazonais**: controle como o desempenho dos formulários muda ao longo do ano
- **Integração de Campanha**: correlacionar análises de formulários com desempenho de campanhas de marketing
- **Integração de Teste A/B**: use a análise para medir variações de teste e otimizar continuamente

## Cenários de implementação do Real-World Form Analytics

A compreensão de cenários de implementação específicos ajuda as organizações a aplicar a análise de formulários de maneira eficaz em diferentes contextos de negócios. Esses exemplos reais demonstram como o rastreamento do desempenho do formulário e a otimização de conversão fornecem resultados comerciais mensuráveis.

### Otimização de saída de comércio eletrônico

**Cenário**: o retailer online enfrenta alto abandono de carrinho durante o check-out

- **Implementação do Form Analytics**: rastreie o abandono do carrinho no nível do formulário com análise campo a campo
- **Principais Achados**: o preenchimento do formulário de pagamento caiu significativamente na etapa de verificação do cartão de crédito
- **Estratégia de otimização de conversão**: formulário de pagamento simplificado, indicadores de progresso adicionados, experiência móvel otimizada
- **Resultados**: abandono de formulário substancialmente reduzido e aumento de receita
- **Análise de Comportamento do Usuário**: os usuários móveis identificados tiveram taxas de abandono mais altas, resultando em um novo design para dispositivos móveis

### Otimização do formulário de geração de leads

**Cenário**: empresa de software B2B lutando com clientes em potencial de baixa qualidade de formulários de contato

- **Desafio de desempenho de formulário**: altas taxas de conclusão de formulário, mas baixa conversão de cliente em cliente
- **Solução do Analytics**: correlacione o comportamento de conclusão do formulário com a qualidade do cliente potencial e os resultados de vendas
- **Abordagem de otimização**: implementação da criação progressiva de perfis e da integração de pontuação de clientes potenciais
- **Impacto nos negócios**: melhoria significativa na qualidade do lead e aumento nos leads qualificados pelas vendas
- **Otimização de Conversão**: abandono de formulário reduzido ao melhorar a qualificação de lead

### Otimização de registro e integração

**Cenário**: plataforma SaaS com alto abandono de inscrição durante o processo de integração

- **Análise de Comportamento do Usuário**: Rastreie as taxas de conclusão da inscrição e identifique gargalos de integração
- **Form Analytics Insights**: abandono significativo de usuário durante a etapa de verificação de conta
- **Estratégia de otimização**: processo de verificação simplificado, funcionalidade de salvar e retomar adicionada
- **Resultados**: aumento substancial na conclusão da inscrição e melhora nas taxas de ativação do usuário
- **Impacto a longo prazo**: melhor conclusão da integração correlacionada ao maior valor vitalício do cliente

## Recursos do Form Analytics no Adobe Analytics

O Adobe Analytics oferece recursos de rastreamento de formulários de nível empresarial que permitem que as organizações capturem insights detalhados sobre as interações do usuário com seus formulários. A integração perfeita com o AEM Forms oferece análises poderosas e opções sofisticadas de personalização prontas para uso que se ajustam às necessidades da empresa.

### Por que escolher o Adobe Analytics para o Form Analytics

**Desempenho em escala corporativa**
O Adobe Analytics lida com milhões de interações de formulários sem degradação do desempenho, tornando-o ideal para sites de alto tráfego e ambientes corporativos complexos. A infraestrutura robusta da plataforma garante uma coleta de dados confiável mesmo durante os períodos de pico de uso.

**Recursos avançados de segmentação**
Ao contrário das ferramentas básicas de análise de formulários, o Adobe Analytics permite a segmentação sofisticada do usuário com base em comportamento, demografia, fontes de tráfego e critérios comerciais personalizados. Isso permite estratégias de otimização direcionadas que abordam grupos de usuários e cenários específicos.

**Alertas e Insights em Tempo Real**
Monitore o desempenho dos formulários à medida que ele acontece, com painéis em tempo real e alertas automatizados. Identifique e responda imediatamente aos problemas, evitando possíveis perdas de receita devido a problemas de formulários ou degradação do desempenho.

### Recursos de rastreamento prontos para uso

O AEM Forms integra-se perfeitamente com o [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) para capturar e rastrear automaticamente as métricas de desempenho dos formulários publicados. Você pode monitorar o comportamento de usuários autenticados e anônimos sem configurações adicionais.

Antes de implementar a análise de formulários, verifique se o seu [ambiente do AEM Forms está configurado corretamente](/help/forms/setup-forms-cloud-service.md) e se você [criou seus formulários adaptáveis](/help/forms/creating-adaptive-form-core-components.md) usando os Componentes Principais ou os [Componentes de Base](/help/forms/creating-adaptive-form.md).

**Rastreamento Abrangente de Eventos de Formulário:**

O Adobe Analytics captura automaticamente uma imagem completa das interações de formulário do usuário:

- **Renderizações do formulário**: controle as impressões e as exibições do formulário para compreender o alcance e o envolvimento inicial
- **Envios de Formulário**: Monitore conclusões bem-sucedidas com contexto de envio detalhado e dados de jornada do usuário
- **Análise de Abandono de Formulário**: Capture pontos de abandono precisos com granularidade em nível de campo e contexto de sessão do usuário
- **Rastreamento de Erro de Validação**: registra tipos de erro, frequência e padrões de resolução para identificar problemas de usabilidade
- **Uso de Conteúdo da Ajuda**: monitorar quando os usuários acessam recursos de ajuda, indicando áreas de confusão ou complexidade
- **Interações em nível de campo**: controle o envolvimento individual de campo, o tempo gasto e os padrões de interação
- **Comportamento de Salvamento do Rascunho**: Compreenda a intenção do usuário e a complexidade do formulário por meio de padrões de uso de salvar e retomar
- **Rastreamento entre sessões**: siga usuários em várias sessões de formulário para entender as jornadas de conclusão

**Insights Comportamentais Avançados:**

- **Análise Time-on-Field**: meça quanto tempo os usuários gastam em cada campo de formulário para identificar problemas de complexidade
- **Padrões de Movimento do Mouse**: Rastreie a hesitação e o engajamento do usuário através da análise do comportamento do cursor
- **Rastreamento de profundidade de rolagem**: entenda como os usuários navegam por formulários longos e identificam o comprimento ideal do formulário
- **Padrões de Recuperação de Erros**: analise como os usuários respondem e se recuperam de erros de validação

### Rastreamento de evento personalizado

Além dos eventos de formulários padrão, o Adobe Analytics permite um rastreamento personalizado sofisticado:

- **Métricas específicas de negócios**: defina eventos personalizados usando o editor de regras para rastrear interações de formulários específicas da organização
- **Mapeamento de Jornada de usuário**: crie eventos personalizados para rastrear caminhos de usuário complexos através de formulários de várias etapas
- **Análise de funil de conversão**: configure eventos personalizados para medir pontos de conversão e estágios iniciais específicos
- **Eventos de Integração**: Rastrear interações de formulário com sistemas externos e APIs

### Recursos avançados de relatórios

A Adobe Analytics oferece recursos de geração de relatórios de nível empresarial para desempenho de formulários:

- **Painéis em tempo real**: monitore o desempenho dos formulários e as interações do usuário à medida que elas ocorrem
- **Análise de Segmentação**: analisar o desempenho do formulário em diferentes grupos de usuários, fontes de tráfego e dados demográficos
- **Visualização de funil**: visualize a progressão do usuário através de formulários de várias etapas e identifique oportunidades de otimização
- **Análise de coorte**: controle as melhorias de desempenho do formulário ao longo do tempo e meça o impacto da otimização
- **Rastreamento entre dispositivos**: entenda como os usuários interagem com formulários em diferentes dispositivos e sessões

### Vantagens da integração

A integração do Adobe Analytics e do AEM Forms oferece vantagens exclusivas:

- **Plataforma de Dados Unificada**: combine a análise de formulário com a análise mais ampla de site e marketing
- **Integração do Adobe Experience Cloud**: aproveitar as conexões com o Adobe Target, o Campaign e outras soluções da Experience Cloud
- **Segurança Corporativa**: conformidade interna com as regulamentações de privacidade de dados e os requisitos de segurança corporativa
- **Arquitetura escalável**: lidar com interações de formulário de alto volume sem impacto no desempenho
- **Suporte Profissional**: acesso aos serviços de otimização e suporte corporativo da Adobe

Depois de implementar as etapas de integração descritas neste artigo, você poderá configurar e exibir relatórios abrangentes no [!DNL Adobe Analytics], conforme demonstrado no vídeo a seguir:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

## Métricas principais do Form Analytics a serem rastreadas

A implementação bem-sucedida da análise de formulários requer o foco nas métricas que afetam diretamente os resultados dos negócios. Entender quais métricas priorizar ajuda as organizações a tomar decisões orientadas por dados e otimizar o desempenho dos formulários de maneira eficaz.

### Métricas de desempenho primárias

**Índice de conversão de formulários**

- **Definição**: porcentagem de exibições de formulário que resultam em envios bem-sucedidos
- **Cálculo**: (Envios de Formulários/Exibições de Formulário) × 100
- **Impacto nos negócios**: correlação direta com a geração de clientes potenciais e metas de receita
- **Destino de otimização**: varia de acordo com o setor e a complexidade do formulário

**Taxa de Abandono de Formulário**

- **Definição**: porcentagem de usuários que iniciam mas não concluem formulários
- **Cálculo**: (Inícios de Formulário - Conclusões de Formulário) / Inícios de Formulário × 100
- **Insights Críticos**: identifica problemas de experiência do usuário e oportunidades de otimização
- **Referencial**: altas taxas de abandono geralmente indicam problemas significativos de usabilidade

**Tempo médio de conclusão**

- **Definição**: tempo médio que os usuários gastam concluindo formulários do início ao envio
- **Analysis Focus**: identifique formulários que demoram muito e podem frustrar os usuários
- **Meta de otimização**: equilibrar integridade com a eficiência da experiência do usuário
- **Segmentação**: comparar tempos de conclusão entre dispositivos, tipos de usuários e fontes de tráfego

### Análise de campo

**Taxas de abandono de campo**

- **Medição**: porcentagem de usuários que abandonam formulários em campos específicos
- **Valor de Otimização**: identifica campos problemáticos que precisam de simplificação ou remoção
- **Problemas comuns**: requisitos de validação complexos, instruções não claras ou problemas técnicos
- **Itens de ação**: priorizar esforços de otimização em campos com taxas de abandono mais altas

**Padrões de interação de campo**

- **Taxas de click-through**: porcentagem de usuários que se envolvem com campos de formulário específicos
- **Tempo no campo**: tempo médio que os usuários gastam em campos individuais
- **Taxas de Erro**: Frequência de erros de validação para campos específicos
- **Uso da Ajuda**: a frequência com que os usuários acessam o conteúdo da ajuda de campos específicos

**Taxas de conclusão do campo**

- **Análise Progressiva**: Rastreie as taxas de conclusão à medida que os usuários avançam pelos campos de formulário
- **Identificação de devolução**: identifique locais exatos onde os usuários abandonam formulários
- **Prioridade de Otimização**: concentre-se nas melhorias nos campos com reduções mais acentuadas na taxa de conclusão

### Métricas de experiência do usuário

**Análise de Taxa de Erros**

- **Erros de Validação**: Frequência e tipos de falhas de validação de formulário
- **Erros Técnicos**: problemas no nível do sistema que afetam a funcionalidade do formulário
- **Padrões de erro do usuário**: erros comuns que os usuários cometem ao preencher formulários
- **Controle de Resolução**: Monitore como as melhorias na taxa de erro afetam a conversão geral

**Desempenho móvel vs. desktop**

Os formulários móveis normalmente apresentam taxas de abandono 30% mais altas em comparação às versões de desktop, tornando a otimização específica do dispositivo essencial:

- **Taxas de Conversão Específicas do Dispositivo**: Comparar o desempenho de formulários entre tipos de dispositivos
- **Impacto Responsivo no Design**: meça como a otimização para dispositivos móveis afeta as taxas de conclusão
- **Usabilidade da interface de toque**: analisar padrões de interação específicos para dispositivos móveis
- **Jornada entre dispositivos**: controle usuários que iniciam formulários em um dispositivo e concluem em outro

**Métricas de Carregamento e Desempenho de Página**

O Forms que é carregado em menos de 3 segundos tem taxas de conclusão 70% mais altas do que formulários mais lentos:

- **Tempo de carregamento do formulário**: tempo necessário para que os formulários sejam totalmente renderizados e se tornem interativos
- **Tempo de Resposta do Campo**: latência entre entrada do usuário e resposta do sistema
- **Tempo de Processamento de Envio**: duração do envio do formulário até a confirmação
- **Impacto no desempenho**: correlação entre tempos de carregamento e taxas de abandono

### Métricas avançadas do Analytics

**Análise de segmentação de usuário**

- **Desempenho do Traffic Source**: Comparar taxas de conversão de formulários entre canais de marketing
- **Desempenho geográfico**: analisar taxas de conclusão de formulário por localização e idioma
- **Análise de Tipo de Usuário**: comparar o desempenho entre usuários novos e recorrentes
- **Insights Demográficos**: entender como diferentes grupos de usuários interagem com formulários

**Análise de funil de conversão**

- **Progressão de Formulário de Várias Etapas**: Rastrear o avanço do usuário por meio de formulários complexos
- **Conversão de etapa por etapa**: meça as taxas de conclusão em cada etapa do formulário
- **Otimização de Funil**: identificar e resolver gargalos na progressão do formulário
- **Integração de Teste A/B**: comparar o desempenho de funil entre variações de formulário

**Métricas de impacto nos negócios**

- **Pontuação de qualidade do lead**: correlacione o comportamento de conclusão do formulário com as taxas de conversão de lead
- **Atribuição de receita**: conectar os envios de formulários aos resultados reais de negócios
- **Valor vitalício do cliente**: analise o valor de longo prazo dos usuários adquiridos através de diferentes formulários
- **Custo por aquisição**: calcule a eficiência de marketing com base nos dados de desempenho do formulário

A figura a seguir ilustra as ações que você precisa executar antes de exibir relatórios em [!DNL Adobe Analytics]:

![Visão geral do Analytics](assets/analytics-workflow.png)

## Configuração do Form Analytics para AEM Forms

A implementação do Form Analytics com Adobe Analytics e AEM Forms requer configuração sistemática em vários componentes. Esta seção fornece orientação abrangente de configuração, pré-requisitos e práticas recomendadas para uma implementação bem-sucedida.

### Pré-requisitos e condições

Antes de iniciar a implementação do form Analytics, verifique se seu ambiente atende aos seguintes requisitos:

>[!NOTE]
>
>Se você encontrar problemas durante a instalação, consulte nosso abrangente [guia de solução de problemas do AEM Forms](/help/forms/troubleshooting-installation-and-configuration.md) para obter informações sobre problemas de instalação e configuração.

**Acesso ao Adobe Experience Cloud**

- Organização Adobe Experience Cloud válida com licenciamento da Adobe Analytics
- Acesso administrativo a ambientes Adobe Analytics e AEM Forms
- Acesso ao Adobe Launch (Coleção de dados) para gerenciamento e configuração de tags

**Ambiente AEM Forms**

- [AEM Forms as a Cloud Service](/help/forms/setup-forms-cloud-service.md) ou AEM Forms 6.5+ (instalações locais/AMS)
- Recursos de criação e publicação do Forms habilitados
- Verifique se a [opção Forms está disponível](/help/forms/troubleshooting-installation-and-configuration.md#forms-option-is-unavailable) em seu ambiente AEM
- [Componentes principais adaptáveis do Forms](/help/forms/creating-adaptive-form-core-components.md) ou [Componentes de base](/help/forms/creating-adaptive-form.md) disponíveis

**Requisitos técnicos**

- Navegadores da Web modernos com JavaScript ativado para rastreamento de análise de formulário
- Implementação do protocolo HTTPS para transmissão segura de dados
- Configurações apropriadas de firewall e rede para a coleta de dados do Adobe Analytics

**Permissões e Acesso**

- Função de administrador do Adobe Analytics para configuração de conjunto de relatórios
- Permissões de autor do AEM Forms para configuração e publicação de formulários
- Acesso do desenvolvedor do Adobe Launch para implementação de tags e criação de regras

### Guia de implementação passo a passo

#### &#x200B;1. Configurar o Adobe Analytics {#Configure-adobe-analytics}

Antes de configurar [!DNL Adobe Analytics], crie:

- Uma Adobe ID para fazer logon no [Adobe Experience Cloud](https://experience.adobe.com/#/home).
- Um [conjunto de relatórios](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### Instalar o AEM Forms e as extensões do [!DNL Adobe Analytics] {#install-extensions}

Execute as seguintes etapas para configurar o AEM Forms e as extensões do [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html):

1. Faça logon no Adobe Experience Cloud e selecione um nome apropriado para a empresa.

1. Selecione **[!UICONTROL Iniciar/Coleção de Dados]** e **[!UICONTROL Ir para Iniciar/Coleção de Dados]**.

1. Selecione **[!UICONTROL Nova propriedade]** e especifique um nome para a configuração.

1. Especifique um nome de domínio e selecione **[!UICONTROL Salvar]** para salvar a propriedade.

1. Selecione o nome da configuração disponível na lista de Propriedades da tag.

1. Na seção **[!UICONTROL Criação]**, selecione **[!UICONTROL Extensões]**.

1. Selecione **[!UICONTROL Catálogo]** e **[!UICONTROL Instalar]** para a extensão **[!UICONTROL Adobe Experience Manager Forms]**. O **[!UICONTROL Adobe Experience Manager Forms]** é exibido na lista de extensões instaladas disponíveis na guia **Instalado**.

1. Selecione **[!UICONTROL Instalar]** para a extensão **[!UICONTROL Adobe Analytics]**.
1. Selecione o nome do conjunto de relatórios nas listas suspensas **[!UICONTROL Conjuntos de relatórios de desenvolvimento]**, **[!UICONTROL Conjuntos de relatórios de preparo]** e **[!UICONTROL Conjuntos de relatórios de produto]** e selecione **[!UICONTROL Salvar]** para salvar a extensão.

### Configurar elementos de dados {#configure-data-elements}

Você pode selecionar qualquer um dos elementos de dados configurados em uma regra criada para um evento. Quando ocorre um evento em um formulário adaptável, o AEM Forms envia esses elementos de dados para [!DNL Adobe Analytics].

Após instalar a extensão **[!UICONTROL Adobe Experience Manager Forms]**, você pode criar os seguintes elementos de dados:

<table>
 <tbody>
  <tr>
   <td>NomeCampo</th>
   <td>TítuloDoCampo</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>TítuloFormulário<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>URLdaPágina<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>Tempo gasto</td>
  </tr>
 </tbody>
</table>

Execute as seguintes etapas para configurar elementos de dados:

1. Na seção **[!UICONTROL Criação]**, selecione **[!UICONTROL Elementos de Dados]**.

1. Selecione **[!UICONTROL Criar Novo Elemento De Dados]**.

1. Especifique um nome para o Elemento de dados. Por exemplo, Título do formulário para o tipo de elemento de dados FormTitle.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como o nome da Extensão.

1. Selecione o **[!UICONTROL Tipo de Elemento de Dados]**.

1. Selecione **[!UICONTROL Salvar]** para salvar o elemento de dados.

>[!VIDEO](https://video.tv.adobe.com/v/337472)

### Configurar regras {#configure-rules}

Execute as seguintes etapas para criar regras com base na extensão **[!UICONTROL Adobe Experience Manager Forms]**:

1. Na seção **[!UICONTROL Criação]**, selecione **[!UICONTROL Regras]**.

1. Selecione **[!UICONTROL Criar Nova Regra]**.

1. Especifique um nome para a Regra. Por exemplo, Envio de formulário para registrar envios de formulário.

1. Na seção **[!UICONTROL Eventos]**, selecione **[!UICONTROL Adicionar]**.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como o nome da Extensão.

1. Selecione o tipo de evento. A entrada para o campo **[!UICONTROL Nome]** é preenchida automaticamente com base no tipo de evento selecionado.

1. Selecione **[!UICONTROL Manter alterações]** para salvar o evento.

1. Na seção **[!UICONTROL Actions]**, selecione **[!UICONTROL Add]**.

1. Especifique **[!UICONTROL Adobe Analytics]** como o nome da Extensão.

1. Selecione **[!UICONTROL Definir variáveis]** como o Tipo de ação. As opções disponíveis na lista suspensa incluem:

   - **[!UICONTROL Definir Variáveis]**: use este tipo de ação para definir o tipo de evento para o qual os elementos de dados selecionados são enviados do AEM Forms para [!DNL Adobe Analytics].

   - **[!UICONTROL Enviar sinal]**: use este tipo de ação para enviar dados do AEM Forms para [!DNL Adobe Analytics].

   - **[!UICONTROL Limpar Variáveis]**: use este tipo de ação para limpar a trilha de dados de forma que o evento seja registrado apenas uma vez em [!DNL Adobe Analytics].

     A abordagem recomendada é usar o tipo de ação **[!UICONTROL Definir Variáveis]** para configurar o evento e os elementos de dados, usar **[!UICONTROL Enviar Beacon]** para enviar dados e usar **[!UICONTROL Limpar Variáveis]** para limpar a trilha de dados.

1. Na seção **[!UICONTROL Props]**, mapeie as opções do conjunto de relatórios disponíveis na lista suspensa com os elementos de dados definidos com o uso de [Configurar elementos de dados](#configure-data-elements).

   Por exemplo, para enviar o elemento de dados **Título do formulário** do AEM Forms para [!DNL Adobe Analytics] quando você enviar um formulário:
   1. Na seção **[!UICONTROL Props]**, selecione uma prop para o Título do Formulário disponível no conjunto de relatórios e, em seguida, selecione ![Ícone do Banco de Dados](assets/database-icon.svg) para mapeá-lo para o Título do Formulário criado em [Configurar elementos de dados](#configure-data-elements).

      ![define-props](assets/define-props.png)

   1. Selecione **[!UICONTROL Adicionar Outro]** para adicionar mais elementos de dados à lista.

1. Na seção **[!UICONTROL Eventos]**, selecione um evento dentre as opções disponíveis no conjunto de relatórios e selecione **[!UICONTROL Manter alterações]**.

1. Na seção **[!UICONTROL Actions]**, selecione + e especifique **[!UICONTROL Adobe Analytics]** como o nome da Extensão.

1. Selecione **[!UICONTROL Enviar sinal]** como o Tipo de ação. No painel direito, selecione **[!UICONTROL s.t()]** para enviar dados a [!DNL Adobe Analytics] e tratá-los como um modo de exibição de página ou **[!UICONTROL s.tl()]** para enviar dados a [!DNL Adobe Analytics] e não tratá-los como um modo de exibição de página. Selecione **[!UICONTROL Manter alterações]**.

1. Na seção **[!UICONTROL Actions]**, selecione + e especifique **[!UICONTROL Adobe Analytics]** como o nome da Extensão.

1. Selecione **[!UICONTROL Limpar Variáveis]** como o Tipo de Ação. Selecione **[!UICONTROL Manter alterações]**. Depois de executar essas etapas, a seção **[!UICONTROL Ações]** é exibida como:
   ![Configuração de ações](assets/actions-config.png)

   Personalize a seção **[!UICONTROL Ações]** de acordo com suas necessidades. Por exemplo, você pode definir duas etapas **Enviar Beacon** em um Fluxo de ação para enviar dados para [!DNL Adobe Analytics] e tratá-los como uma exibição de página em uma etapa e enviar dados para [!DNL Adobe Analytics] e não tratá-los como uma exibição de página na segunda etapa.

   ![Configuração de ações](assets/actions-config-2.png)

1. Selecione **[!UICONTROL Salvar]** para salvar a regra.

   Você pode criar regras para todos os tipos de evento, como Abandonar, Erro, Visita de campo, Ajuda, Renderizar, Salvar e Enviar.

>[!VIDEO](https://video.tv.adobe.com/v/337425)


### Fluxos de publicação {#publish-flow}

Depois de criar os elementos de dados e usá-los nas regras, publique a configuração para coletar dados de formulário no [!DNL Adobe Analytics].

Execute as seguintes etapas para publicar a configuração:

1. Na seção **[!UICONTROL Publicação]**, selecione **[!UICONTROL Fluxo de Publicação]**.

1. Selecione **[!UICONTROL Adicionar biblioteca]**, especifique um nome e selecione o ambiente para a biblioteca.

1. Selecione **[!UICONTROL Adicionar todos os recursos alterados]** e selecione **[!UICONTROL Salvar e criar no desenvolvimento]**.

1. Na seção **[!UICONTROL Desenvolvimento]**, selecione ![Mais opções](assets/more-options-icon.svg) e **[!UICONTROL Aprovar e publicar para produção]**.

1. Confirme se as alterações e o fluxo de publicação serão exibidos em breve na seção **[!UICONTROL Publicado]**.

![Fluxo de publicação](assets/publish-flow.png)

## &#x200B;2. Configurar o AEM Forms {#configure-aem-forms}

Antes de criar uma configuração do Adobe Launch, crie uma [Configuração do Adobe IMS usando o Adobe Launch como a Solução da nuvem](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### Criar configuração do Adobe Launch {#create-adobe-launch-configuration}

Execute as seguintes etapas para criar uma configuração do Adobe Launch:

1. Na instância do Autor do AEM Forms, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Configurações do Adobe Launch]**.

1. Selecione uma pasta para criar a configuração e selecione **[!UICONTROL Criar]**.

1. Especifique um título para a configuração no campo **[!UICONTROL Título]**.

1. Selecione a [configuração IMS da Adobe associada](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. Selecione o nome da empresa usada durante a [configuração do Adobe Analytics](#Configure-adobe-analytics).

1. Selecione o nome da propriedade criada durante a [configuração do Adobe Analytics](#install-extensions).

1. Selecione **[!UICONTROL Salvar e fechar]**.

1. Publique a configuração.

### Habilitar [!DNL Adobe Analytics] para um formulário adaptável {#enable-analytics-adaptive-form}

Para usar a configuração [!DNL Adobe Launch] em um Formulário adaptável existente:

1. Na instância do Autor do AEM Forms, navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione o Formulário adaptável e selecione **[!UICONTROL Propriedades]**.
1. Na guia **[!UICONTROL Básico]**, selecione o [contêiner de configuração](#create-adobe-launch-configuration) usado ao criar a configuração do Adobe Launch.
1. Selecione **[!UICONTROL Salvar e fechar]**. O Formulário adaptável está habilitado para [!DNL Adobe Analytics].
1. Publique o formulário.

Depois de habilitar [!DNL Adobe Analytics] para um formulário adaptável, você poderá [validar](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) se houver um fluxo de eventos de dados apropriado entre o AEM Forms e o [!DNL Adobe Analytics]. A integração do AEM Forms com o Adobe Analytics está concluída. Agora você pode [configurar e exibir relatórios no Adobe Analytics](#view-reports-adobe-analytics).

### Criar regras para capturar eventos personalizados (Opcional) {#capture-custom-events}

Crie regras em campos específicos de um formulário adaptável usando um editor de regras para enviar dados do Analytics de um formulário adaptável para [!DNL Adobe Analytics].

Em um processo de dois estágios, você define uma regra em um campo em um formulário adaptável. A regra despacha um evento. O nome do evento é mapeado para um evento de captura personalizado no Adobe Launch.

Para criar regras usando um editor de regras em um formulário adaptável:

1. Selecione o campo e selecione ![Editor de regras](assets/rule-editor-icon.svg) para abrir a página do editor de regras.
1. Defina uma condição na seção [!UICONTROL When] da regra.
1. Na seção [!UICONTROL Then] da regra, selecione **[!UICONTROL Evento de Despacho]** na lista suspensa **[!UICONTROL Selecionar Ação]**.
1. Especifique o nome do evento no campo **[!UICONTROL Digitar Nome do Evento]**.

Por exemplo, se a data de nascimento for anterior a uma determinada data, a AEM Forms enviará o evento **Segurança**.

![Evento de expedição](assets/security-event.png)

Para mapear o evento para um evento de captura personalizado em [!DNL Adobe Analytics]:

1. [Criar uma regra](#configure-rules).

1. Na seção **[!UICONTROL Eventos]**, selecione **[!UICONTROL Adicionar]**.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como o nome da Extensão.

1. Selecione **[!UICONTROL Capturar evento personalizado]** na lista suspensa **[!UICONTROL Tipo de evento]**.

1. Especifique o nome do evento especificado na etapa 4 ao criar uma regra usando o editor de regras.

1. Selecione **Manter Alterações** e execute o restante das ações especificadas em [Configurar Regras](#configure-rules).

## &#x200B;3. Configurar e exibir relatórios em [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

Depois de configurar um formulário adaptável para enviar dados do evento para o [!DNL Adobe Analytics], você pode começar a exibir relatórios em [!DNL Adobe Analytics]:

1. Selecione ![Selecionar Produto](assets/select-analytics.png) e **[!UICONTROL Analytics]**.

1. Selecione **[!UICONTROL Criar projeto]** e selecione **[!UICONTROL Projeto em branco]**.

1. Selecione o nome do conjunto de relatórios na lista suspensa na parte superior direita da forma livre.

1. Especifique o **Título do formulário** no texto dos **[!UICONTROL itens de dimensão de Pesquisa]** para exibir todos os títulos de formulário.

1. Solte o título do formulário adaptável para a caixa de texto **[!UICONTROL Solte um segmento aqui (ou qualquer outro componente)]**.

1. Na seção **[!UICONTROL Métricas]**, solte os eventos a serem rastreados na caixa de texto **[!UICONTROL Solte uma métrica aqui (ou qualquer outro componente)]**.

1. Selecione ![Visualizações](assets/visualization-icon.svg) e solte um tipo de gráfico na seção de Forma livre. Da mesma forma, você pode adicionar vários tipos de gráfico à seção Forma livre.

1. Selecione as teclas Ctrl + S e especifique um nome para salvar o projeto.

<!--

## Add AEM Forms and Adobe Analytics integration specific rules to Dispatcher {#forms-specific-rules-to-dispatcher}

Add AEM Forms and Adobe Analytics integration specific rules to filter the data traffic that is sent to the backend.

Perform the following steps to add AEM Forms and Adobe Analytics integration specific rules to Dispatcher for Experience Manager Forms as a Cloud Service:

1. Open your AEM Project and navigate to `\src\conf.dispatcher.d\filters`.
1. Open `filters.any` file for editing and add the following rule at the end of the file:

     ```json
     /00XX { /type "allow" /path "/content/forms/af/*" /method "POST" /selectors '(analyticsconfigparser)' /extension '(jsp|json)' }
     ```

1. Save and close the file.
1. Compile and deploy the project to your [!DNL AEM Forms] as a Cloud Service environment.



## Limitations {#limitations}

* Adobe Analytics can track form metrics only for authenticated users.

-->

## Configuração avançada do Form Analytics

Além da configuração básica, o Adobe Analytics oferece opções avançadas de configuração que permitem recursos sofisticados de rastreamento e análise de formulários. Esses recursos avançados ajudam as organizações a obter insights mais profundos e implementar cenários de análise complexos.

### Eventos personalizados e rastreamento

**Criando Eventos de Formulário Personalizados**

Os eventos personalizados permitem rastrear interações específicas de negócios que vão além da análise de formulário padrão:

- **Eventos de Processo Comercial**: Rastreie interações de formulário que se alinham a fluxos de trabalho comerciais específicos
- **Eventos de Envolvimento do Usuário**: meça comportamentos de usuário avançados, como pré-visualização de formulário, uso da ajuda de campo ou conclusão de seção
- **Eventos de Integração**: Monitorar as interações de formulário com sistemas externos, APIs ou serviços de terceiros
- **Eventos de Desempenho**: Acompanhe as métricas de desempenho personalizadas, como tempos de carregamento de formulário ou taxas de resposta de campo

**Abordagem da implementação**

1. **Definir Requisitos Comerciais**: identificar interações de formulário específicas que forneçam valor comercial
2. **Criar variáveis personalizadas**: configure eVars e props personalizadas no Adobe Analytics para dados específicos de negócios
3. **Configurar Editor de Regras**: use o editor de regras do AEM Forms para acionar eventos personalizados com base em interações de formulário
4. **Mapear para Eventos do Analytics**: conectar eventos de formulário personalizados ao rastreamento de eventos do Adobe Analytics
5. **Validar implementação**: teste eventos personalizados para garantir coleta e relatórios de dados precisos

### Configuração avançada de relatórios

**Configuração de Análise Multidimensional**

- **Análise entre formulários**: compare o desempenho entre diferentes tipos de formulários e processos comerciais
- **Mapeamento da Jornada do usuário**: controle as interações do usuário em vários formulários e pontos de contato
- **Modelagem de atribuição**: entenda como os diferentes canais de marketing contribuem para a conclusão de formulários
- **Análise de coorte**: analisar as melhorias de desempenho do formulário ao longo do tempo e dos segmentos de usuário

**Configuração de relatório em tempo real**

- **Configuração do Live Dashboard**: configurar o monitoramento do desempenho do formulário em tempo real
- **Configuração de Alerta**: Configurar alertas automatizados para problemas ou anomalias no desempenho do formulário
- **Limites de Desempenho**: Defina intervalos de desempenho aceitáveis e gatilhos de monitoramento
- **Relatórios de Partes Interessadas**: crie relatórios automatizados para diferentes funções e responsabilidades organizacionais

### Integração com outras ferramentas do Adobe

**Integração do Adobe Target**

- **Teste A/B de formulário**: teste diferentes variações de formulário e meça o impacto no desempenho
- **Personalization**: fornecer experiências de formulário personalizadas com base no comportamento do usuário e nos dados de análise
- **Otimização**: use os insights de análise para informar as estratégias de otimização do Target
- **Otimização de conversão**: combinar análise de formulários com esforços de otimização de conversão mais amplos

**Integração do Adobe Campaign**

- **Orientação de clientes potenciais**: use dados de análise de formulários para informar sobre marketing por email e campanhas de orientação de clientes potenciais
- **Segmentação**: crie segmentos de usuários com base no comportamento de preenchimento de formulários e nos padrões de envolvimento
- **Atribuição de campanha**: controle como as campanhas de marketing influenciam as taxas de desempenho e conclusão do formulário
- **Marketing de ciclo de vida**: integre a análise de formulários às estratégias mais amplas de marketing de ciclo de vida do cliente

## Relatórios e insights do Form Analytics

Entender como interpretar e agir nos dados de análise de formulário é fundamental para uma otimização bem-sucedida. Esta seção aborda os principais relatórios, a configuração do painel e a extração de insights acionáveis.

### Noções básicas do painel do Analytics

**Painel de KPIs (Indicadores-chave de desempenho)**

- **Funil de conversão de formulário**: visualizar a progressão do usuário através do processo de conclusão do formulário
- **Análise de Abandono**: identificar pontos específicos em que os usuários deixam formulários incompletos
- **Tendências de Desempenho**: controle as alterações de desempenho do formulário ao longo do tempo e identifique padrões
- **Análise Comparativa**: comparar o desempenho em diferentes formulários, períodos e segmentos de usuário

**Painel de Métricas Operacionais**

- **Atividade de formulário em tempo real**: monitorar as taxas atuais de uso e conclusão do formulário
- **Monitoramento da Taxa de Erro**: Rastrear erros de validação e problemas técnicos que afetam o desempenho do formulário
- **Desempenho do dispositivo e do navegador**: analisar o desempenho do formulário em diferentes ambientes técnicos
- **Desempenho geográfico**: entenda como o desempenho do formulário varia de acordo com a localização e o idioma

### Principais relatórios a serem monitorados

**Relatórios de Desempenho Diário**

- **Resumo da conclusão do formulário**: visão geral diária dos envios de formulários, taxas de abandono e métricas de conversão
- **Análise de erro**: rastreamento diário de erros de formulário, problemas de validação e problemas técnicos
- **Desempenho do Traffic Source**: análise de como diferentes canais de marketing orientam a conclusão de formulários
- **Desempenho móvel vs. desktop**: análise comparativa do desempenho de formulários entre tipos de dispositivos

**Análise de tendência semanal**

- **Identificação da Tendência de Desempenho**: análise semanal de melhorias ou reduções no desempenho do formulário
- **Padrões de Comportamento do Usuário**: análise semanal de padrões de interação do usuário e tendências de engajamento
- **Medida de Impacto de Otimização**: avaliação de como as alterações de formulário afetam as métricas de desempenho
- **Benchmarking Competitivo**: Comparação do desempenho de formulários com padrões e benchmarks do setor

**Relatórios Estratégicos Mensais**

- **Análise do ROI**: avaliação mensal do impacto da análise de formulários nos resultados e na receita dos negócios
- **User Experience Insights**: análise abrangente das melhorias na experiência do usuário e oportunidades de otimização
- **Desempenho da Integração**: análise de como a integração da análise de formulários afeta processos comerciais e de marketing mais amplos
- **Recomendações estratégicas**: recomendações orientadas por dados para otimização de formulários e melhorias no processo comercial

### Extração de insights acionáveis

**Insights de Otimização de Desempenho**

- **Otimização no Nível de Campo**: Identifique campos de formulário específicos que precisam ser melhorados ou removidos
- **Aprimoramento da Experiência do Usuário**: descubra problemas de experiência do usuário e implemente melhorias direcionadas
- **Otimização da Taxa de Conversão**: use dados de análise para implementar alterações que melhorem as taxas de conclusão de formulários
- **Otimização do Desempenho Técnico**: Resolva problemas técnicos que afetam o desempenho de carregamento e envio do formulário

**Insights de processos comerciais**

- **Análise de Qualidade de Cliente Potencial**: Entenda como o comportamento de conclusão de formulário se correlaciona com a qualidade e a conversão de cliente potencial
- **Atribuição de marketing**: identifique quais canais e campanhas de marketing direcionam os envios de formulários de maior qualidade
- **Otimização da Jornada do cliente**: use a análise de formulários para melhorar os processos mais amplos de aquisição e retenção de clientes
- **Alocação de recursos**: tome decisões orientadas por dados sobre onde investir os recursos de otimização de formulários

## Solução de problemas do Form Analytics

Mesmo com uma implementação cuidadosa, as configurações de análise de formulário podem encontrar problemas que afetam a coleta de dados e a precisão dos relatórios. Esta seção fornece orientação sistemática de solução de problemas comuns.

### Problemas comuns de configuração

**Problemas de coleta de dados**

- **Dados de formulário ausentes**: verifique a configuração do Adobe Launch e garanta a implantação adequada da tag
- **Rastreamento de Eventos Incompleto**: verifique a configuração da regra e se todos os eventos de formulário estão mapeados corretamente
- **Latência de Dados**: Entenda os atrasos normais de processamento de dados e identifique atrasos anormais de relatórios
- **Rastreamento entre domínios**: resolva problemas com a análise de formulários em diferentes domínios ou subdomínios

>[!TIP]
>
>Para obter orientações adicionais sobre solução de problemas, consulte nossos guias [coleção de solução de problemas do AEM Forms](/help/forms/troubleshooting-installation-and-configuration.md) e [solução de problemas de criação de formulários](/help/forms/form-creation-failing.md).

**Problemas de configuração**

- **Mapeamento do Conjunto de Relatórios**: verifique se os formulários estão enviando dados para o conjunto de relatórios correto do Adobe Analytics
- **Configuração de variável**: verifique se as variáveis personalizadas (eVars, props) estão configuradas e mapeadas corretamente
- **Problemas de Lógica de Regra**: depurar regras do Adobe Launch que talvez não estejam sendo acionadas corretamente
- **Problemas de permissão**: resolver problemas de acesso que impedem a configuração ou a exibição de dados adequadas

### Resolução de discrepância de dados

**Discrepâncias do Analytics vs. Sistema de Formulários**

- **Diferenças na Contagem de Envio**: reconcilie as diferenças entre as contagens de envio do Adobe Analytics e do AEM Forms
- **Rastreamento de Comportamento do Usuário**: discrepâncias de endereço no rastreamento de interação do usuário entre sistemas
- **Problemas de Fuso Horário e Data**: Resolva as discrepâncias de relatório causadas pelas diferenças de configuração de fuso horário
- **Amostragem de dados**: entenda quando e como a amostragem de dados do Adobe Analytics afeta a precisão da análise do formulário

**Consistência de dados entre plataformas**

- **Rastreamento móvel vs. desktop**: garanta uma coleta de dados consistente em diferentes tipos de dispositivos e plataformas
- **Compatibilidade de Navegador**: resolver problemas de rastreamento específicos de determinados navegadores ou versões de navegadores
- **Integração de terceiros**: resolver problemas de consistência de dados com sistemas e integrações externos
- **Dados em Tempo Real vs. Dados Históricos**: compreenda e resolva as diferenças entre os dados históricos processados e em tempo real

### Otimização do desempenho

**Impacto no desempenho do Analytics**

- **Desempenho do carregamento da página**: minimize o impacto do rastreamento de análise sobre os tempos de carregamento do formulário
- **Eficiência da Coleta de Dados**: otimize a coleta de dados para reduzir o uso da largura de banda e melhorar a experiência do usuário
- **Processamento em tempo real**: configurar o processamento de análise em tempo real para as necessidades de análise de formulários com detecção de tempo
- **Considerações sobre escalabilidade**: verifique se a configuração do Analytics pode lidar com o uso de formulários de alto volume sem degradação do desempenho

**Desempenho de Integração do Sistema**

- **Desempenho da API**: otimize as integrações entre o AEM Forms e o Adobe Analytics para melhorar o desempenho
- **Eficiência de Processamento de Dados**: Melhore os fluxos de trabalho de processamento de dados para reduzir a latência e melhorar a pontualidade dos relatórios
- **Utilização de Recursos**: Monitore e otimize o uso de recursos do sistema para coleta e processamento de dados de análise
- **Otimização de Rede**: definir configurações de rede para otimizar a transmissão de dados entre sistemas

## Práticas recomendadas do Form Analytics

A implementação bem-sucedida do Form Analytics requer o cumprimento de práticas recomendadas estabelecidas que garantam uma coleta de dados precisa, insights significativos e processos de otimização sustentáveis.

>[!TIP]
>
>Antes de implementar o Analytics, verifique se seus formulários estão configurados corretamente usando as [práticas recomendadas do AEM Forms](/help/forms/introduction-forms-authoring.md) e as [ações de envio](/help/forms/configuring-submit-actions.md) apropriadas.

### Diretrizes de implementação

**Planejamento Estratégico**

- **Alinhamento do Objetivo de Negócios**: Garantir que a implementação da análise de formulário se alinhe às metas de negócios e KPIs específicos
- **Envolvimento das partes interessadas**: envolva as principais partes interessadas no planejamento para garantir que a análise atenda às necessidades organizacionais
- **Implementação em fases**: implemente a análise de formulários em fases para gerenciar a complexidade e garantir uma implantação bem-sucedida
- **Definição de Métricas de Sucesso**: defina claramente a aparência do sucesso e como ele será medido

**Implementação técnica**

- **Documentação de configuração**: mantenha uma documentação abrangente da configuração de análise para referência futura e solução de problemas
- **Protocolos de teste**: implemente procedimentos de teste completos para garantir uma coleta de dados precisa antes da implantação de produção
- **Controle de versão**: use o controle de versão para alterações de configuração de análise e habilite a reversão se surgirem problemas
- **Monitoramento de desempenho**: monitore continuamente o desempenho da implementação de análises e o impacto na funcionalidade de formulários

### Considerações sobre privacidade

**Conformidade com a Privacidade de Dados**

- **Conformidade com o GDPR**: garantir que a implementação da análise de formulários esteja em conformidade com as regulamentações europeias de proteção de dados
- **Conformidade com a CCPA**: implementar os requisitos da Lei de Privacidade do Consumidor da Califórnia para a coleta de dados de formulários e direitos de usuário
- **Regulamentos específicos do setor**: Atenda aos requisitos de saúde (HIPAA), financeiro (PCI DSS) e outros requisitos de privacidade específicos do setor
- **Gerenciamento de consentimento do usuário**: implementar mecanismos de consentimento adequados para coleta e processamento de dados de análise

**Segurança de dados**

- **Criptografia de Dados**: verifique se todos os dados de análise de formulário estão criptografados em trânsito e em repouso
- **Controles de Acesso**: Implementar os controles de acesso apropriados para dados e relatórios de análise
- **Retenção de Dados**: Estabelecer e aplicar políticas apropriadas de retenção de dados para informações de análise de formulários
- **Trilhas de auditoria**: manter trilhas de auditoria para acesso a dados de análise e alterações de configuração

### Estratégias de otimização

**Processo de aprimoramento contínuo**

- **Revisão de desempenho regular**: estabeleça ciclos de revisão regulares para avaliar o desempenho da análise de formulários e identificar oportunidades de otimização
- **Integração de teste A/B**: use dados de análise de formulário para informar estratégias de teste A/B e medir o impacto da otimização
- **Integração de Comentários do Usuário**: combine dados de análise quantitativos com comentários qualitativos do usuário para obter insights abrangentes de otimização
- **Cross-Functional Collaboration**: promova a colaboração entre as equipes de marketing, UX, desenvolvimento e análise para otimização integral

**Utilização de Análise Avançada**

- **Análise preditiva**: use dados de análise de formulário históricos para prever o comportamento do usuário e otimizar as experiências de formulário de forma proativa
- **Integração do Machine Learning**: aproveite os recursos de aprendizado de máquina para identificar padrões e oportunidades de otimização em dados de análise de formulário
- **Otimização em tempo real**: implementar a otimização de formulários em tempo real com base no desempenho atual da análise e no comportamento do usuário
- **Integração entre canais**: integre a análise de formulários à análise mais ampla de jornada do cliente para uma otimização abrangente da experiência do usuário

## Perguntas frequentes

Esta seção abrangente de perguntas frequentes aborda perguntas comuns sobre a implementação, a solução de problemas e a otimização do Form Analytics para ajudar os usuários em todos os níveis de experiência.

### Perguntas de introdução

**P: Qual é a diferença entre a análise de formulário e a análise geral de sites?**

R: A análise de formulários foca especificamente nas interações do usuário nos formulários, fornecendo insights detalhados sobre o comportamento no nível de campo, padrões de preenchimento e pontos de abandono. Enquanto a análise geral de sites rastreia exibições de página e jornadas gerais do usuário, a análise de formulários oferece dados granulares sobre experiências do usuário específicas do formulário, erros de validação, tempos de conclusão de campo e análise de funil de conversão nos próprios formulários.

**P: Preciso de conhecimento técnico para implementar a análise de formulários com o Adobe Analytics?**

R: A implementação básica pode ser realizada com conhecimento técnico moderado, mas as configurações avançadas se beneficiam da experiência técnica. O Adobe fornece opções de configuração automatizadas por meio da Automação de configuração do Experience Cloud para implementações mais simples. Para implantações corporativas complexas com eventos personalizados e relatórios avançados, recomenda-se a colaboração com desenvolvedores ou consultores da Adobe.

**P: Quanto tempo leva para ver dados significativos da análise de formulários?**

R: Os dados iniciais aparecem dentro de 24 a 48 horas após a implementação, mas insights significativos normalmente exigem de 2 a 4 semanas de coleta de dados para identificar padrões e tendências. Para obter significância estatística em decisões de teste A/B e otimização, permita de 4 a 6 semanas de coleta de dados, dependendo do volume de tráfego do formulário.

**P: Qual é o volume de tráfego mínimo necessário para uma análise de formulários eficaz?**

R: A análise de formulários pode fornecer valor em qualquer nível de tráfego, mas a significância estatística para decisões de otimização normalmente requer pelo menos 100 envios de formulários por semana. Para testes A/B e análises avançadas, mais de 500 envios semanais fornecem insights mais confiáveis. Os formulários de tráfego mais baixo ainda podem se beneficiar de insights qualitativos sobre padrões de comportamento do usuário e identificação de erros.

### Perguntas sobre implementação e configuração

**P: Posso rastrear formulários em vários domínios ou subdomínios?**

R: Sim, o Adobe Analytics oferece suporte ao rastreamento de formulários entre domínios por meio da configuração adequada do código de rastreamento do Adobe Analytics e da implementação do Adobe Launch. Garanta uma configuração consistente do conjunto de relatórios e o rastreamento entre domínios para manter a integridade dos dados em domínios diferentes.

**P: Como faço para manipular formulários de análise de formulários de várias etapas ou de estilo de assistente?**

R: Formulários de várias etapas exigem configuração especial para rastrear o progresso em cada etapa. Implemente eventos personalizados para conclusão de etapa, configure a análise de funil para visualizar os pontos de interrupção entre etapas e use variáveis personalizadas para rastrear os caminhos do usuário no assistente de formulário. O Adobe Analytics fornece orientação específica para o rastreamento de formulários de várias páginas.

**P: O que acontece com os dados de análise se um usuário preencher um formulário offline ou com o JavaScript desabilitado?**

R: O Adobe Analytics exige o JavaScript para a coleta de dados, portanto, os usuários com o JavaScript desativado não serão rastreados. Para cenários offline, implemente mecanismos de rastreamento de fallback ou a coleção de análises do lado do servidor. Considere o impacto na integridade dos dados e implemente métodos alternativos de rastreamento para processos de negócios críticos.

**P: Como rastrear o desempenho do formulário em diferentes dispositivos e navegadores?**

R: O Adobe Analytics captura automaticamente informações do dispositivo e do navegador com dados de análise de formulário. Configure relatórios personalizados para analisar o desempenho do formulário por tipo de dispositivo, navegador, sistema operacional e resolução de tela. Use esses dados para identificar oportunidades de otimização específicas para dispositivos e garantir experiências de formulário consistentes em todas as plataformas.

### Perguntas sobre análise e otimização de dados

**P: Qual taxa de abandono de formulário devo considerar problemática?**

R: As taxas de abandono de formulário variam significativamente de acordo com o setor e a complexidade do formulário. Os formulários de contato simples normalmente têm taxas de abandono mais baixas, enquanto os formulários de várias etapas complexos e os processos de finalização de comércio eletrônico tendem a ter taxas mais altas. Taxas de abandono excepcionalmente altas para seu tipo de formulário específico e setor indicam oportunidades de otimização.

**P: Como identificar quais campos de formulário causam mais abandono?**

R: Use o rastreamento em nível de campo do Adobe Analytics para analisar as taxas de conclusão de cada campo de formulário. Procure quedas significativas em campos específicos, tempo maior que a média gasto em campos específicos e altas taxas de erro para determinados tipos de campo. O mapeamento de calor e as gravações de sessão do usuário podem fornecer contexto adicional para a otimização em nível de campo.

**P: Devo otimizar a velocidade ou a integridade do preenchimento de formulários?**

R: O equilíbrio depende de suas metas comerciais. Para geração de leads, otimize para conclusão enquanto mantém a qualidade do lead. Para obter a coleção de dados detalhada (pesquisas, aplicativos), concentre-se nas melhorias de experiência do usuário que reduzem o atrito sem sacrificar a qualidade dos dados. Use o teste A/B para encontrar o equilíbrio ideal para seu caso de uso específico.

**P: Como meço o ROI da implementação da análise de formulários?**

R: Calcule o ROI medindo as melhorias nas taxas de conversão, na qualidade do lead e na eficiência operacional. Monitoramento de métricas como: taxas de preenchimento de formulários maiores, tíquetes de suporte reduzidos relacionados a problemas de formulário, taxas de conversão de lead para cliente melhores e custos de aquisição de cliente menores. Quantifique essas melhorias em relação ao custo da implementação de análises e aos esforços de otimização contínuos.

### Perguntas técnicas e de solução de problemas

**P: Por que vejo discrepâncias entre o Adobe Analytics e minhas contagens de envio do sistema de formulários?**

R: Causas comuns: erros do JavaScript que impedem o rastreamento do Analytics, usuários que enviam formulários várias vezes, tráfego de bot que afeta um sistema, mas não o outro, diferenças de fuso horário nos relatórios e atrasos no processamento de dados. Implemente regras de validação, filtragem de bot e garanta configurações consistentes de fuso horário em todos os sistemas.

**P: Como faço para lidar com a análise de formulários para aplicativos de página única (SPAs)?**

R: Os SPAs exigem configuração especial para a análise de formulários, pois os eventos tradicionais de carregamento de página não ocorrem. Implemente o rastreamento de eventos personalizado para interações de formulário, use os recursos de rastreamento SPA do Adobe Analytics, configure exibições de página virtuais para etapas de formulário e garanta o acionamento adequado do evento para elementos de formulário dinâmicos.

**P: O que devo fazer se a análise de formulários estiver afetando o desempenho do carregamento de páginas?**

R: Otimize a implementação do Analytics carregando scripts de análise de forma assíncrona, implementando o carregamento lento para rastreamento não crítico, reduzindo o número de variáveis e eventos personalizados, usando configurações de regras eficientes no Adobe Launch e monitorando os Componentes principais da Web para garantir que a análise não afete negativamente a experiência do usuário.

**P: Como garantir a conformidade do form Analytics com as regras de privacidade?**

R: Implementar a conformidade com a privacidade ao: obter o consentimento adequado do usuário para rastreamento de análise, tornar os dados pessoais anônimos ou pseudônimos, implementar políticas de retenção de dados, fornecer mecanismos de recusa, garantir a conformidade com o GDPR/CCPA na coleta e no processamento de dados e trabalhar com as equipes legais para garantir a conformidade regulamentar.

### Perguntas sobre implementação avançada

**P: Posso integrar a análise de formulários com outras soluções da Adobe Experience Cloud?**

R: Sim, o Adobe Analytics integra-se perfeitamente com outras soluções da Experience Cloud. Conecte-se com o Adobe Target para testes e personalização A/B de formulário, integre-se ao Adobe Campaign para obter orientação com base no comportamento do formulário, use o Adobe Audience Manager para segmentação avançada e utilize o Adobe Experience Platform para obter uma análise abrangente da jornada do cliente.

**P: Como configurar análises preditivas para abandono de formulário?**

R: Implemente a análise preditiva coletando dados abrangentes sobre o comportamento do usuário, usando os recursos de aprendizado de máquina do Adobe Analytics, implementando modelos de pontuação em tempo real, configurando intervenções automatizadas para cenários de abandono de alto risco e refinando continuamente os modelos com base em dados de desempenho.

**P: Qual é a melhor abordagem para rastrear análises de formulário em um aplicativo para dispositivos móveis?**

R: As análises de formulários de aplicativos para dispositivos móveis exigem a implementação do Adobe Analytics Mobile SDK. Configure eventos e variáveis específicos para dispositivos móveis, implemente a coleta e a sincronização de dados offline, rastreie interações específicas para dispositivos móveis (eventos de toque, orientação do dispositivo) e garanta a atribuição adequada em sessões de aplicativo e interações na Web.

**P: Como criar painéis personalizados para diferentes participantes?**

R: Crie painéis de controle específicos por função ao: identificar métricas principais para cada grupo de partes interessadas (executivos, profissionais de marketing, desenvolvedores), usar o Adobe Analytics Workspace para criar visualizações personalizadas, implementar agendamentos automatizados de relatórios, criar recursos de detalhamento para análise detalhada e fornecer treinamento sobre a interpretação e o uso do painel de controle.

### Solução de problemas de correções rápidas

**Problemas Comuns e Soluções:**

| Problema | Correção rápida | Solução detalhada |
|-------|-----------|-------------------|
| Nenhum dado exibido | Verificar implantação do Adobe Launch | Verificar a implementação de tags e a configuração de regras |
| Contagens de envio incorretas | Validar disparo de evento | Revisar lógica da regra e mapeamento do elemento de dados |
| Dados em nível de campo ausentes | Configurar o rastreamento de campo | Configurar variáveis personalizadas para interações de campo |
| Problemas entre domínios | Atualizar configuração de rastreamento | Implementar a configuração adequada do rastreamento entre domínios |
| Problemas de rastreamento móvel | Verificar implementação móvel | Verificar design responsivo e eventos específicos para dispositivos móveis |
| Impacto no desempenho | Otimizar estratégia de carregamento | Implementar carregamento assíncrono e regras eficientes |

>[!MORELIKETHIS]
>
>*[Habilitar o Adobe Analytics para um Formulário Adaptável](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)
