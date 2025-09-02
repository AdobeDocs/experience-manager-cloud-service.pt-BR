---
title: Forms Experience Builder - Práticas recomendadas
description: Práticas recomendadas abrangentes para a criação de formulários eficazes com o Forms Experience Builder, abrangendo design, experiência do usuário, desempenho e consistência da marca.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 0%

---


# Forms Experience Builder - Práticas recomendadas

>[!NOTE]
>
> O Forms Experience Builder está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: este guia de práticas recomendadas está sendo testado no momento em relação ao produto e está sujeito a atualizações e revisões. As práticas recomendadas, as recomendações e os exemplos podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção inicial.

Este guia abrangente fornece práticas recomendadas comprovadas para a criação de formulários eficazes e fáceis de usar usando o Forms Experience Builder. Essas práticas são derivadas de implementações bem-sucedidas e do feedback do usuário em vários setores e casos de uso.

## Práticas recomendadas de design do formulário

### Mantenha a simplicidade

**Iniciar com Campos Essenciais**

- Comece apenas com as informações mais necessárias para reduzir a sobrecarga dos usuários
- Adicione complexidade gradualmente com base nas necessidades do usuário e nos requisitos de negócios
- Evite solicitar informações que você realmente não precisa ou usa
- Considerar o tempo do usuário e a carga cognitiva ao projetar formulários

**Usar rótulos claros e descritivos**

- Torne as finalidades do campo imediatamente óbvias com rótulos descritivos
- Evite jargões técnicos ou terminologias internas que os usuários não entenderão
- Use convenções consistentes de rotulagem em todos os formulários
- Fornecer contexto quando os requisitos de campo podem não ser óbvios

**Fornecer Orientação Útil**

- Incluir texto de ajuda para campos complexos com exemplos e requisitos de formatação
- Usar texto de espaço reservado para mostrar os formatos de entrada esperados
- Fornecer instruções claras para uploads de arquivo, incluindo formatos aceitos e limites de tamanho
- Orientar os usuários por meio de processos de várias etapas com indicadores de progresso

**Testar Completamente**

- Validar todos os caminhos e cenários de usuário antes da implantação
- Teste formulários com usuários reais do público-alvo
- Verifique se toda lógica condicional funciona como esperado
- Certifique-se de que o tratamento de erros forneça comentários claros e acionáveis

### Divulgação progressiva

**Mostrar Campos Relevantes com Base no Contexto**

- Exibir campos adicionais somente quando eles se tornarem relevantes para as seleções do usuário
- Usar lógica condicional para reduzir a carga cognitiva e o comprimento da forma
- Agrupar campos relacionados em seções lógicas
- Ocultar opções avançadas até que os usuários indiquem que precisam delas

**Exemplo de implementação:**

    Crie uma regra que mostre o painel @spouseInformation somente quando @maritalStatus for igual a &quot;Casado&quot;

**Limpar Navegação e Progresso**

- Ajudar os usuários a entender onde estão em formulários de várias etapas
- Fornecer uma navegação clara entre seções do formulário
- Mostrar indicadores de progresso para formulários mais longos
- Permitir que os usuários salvem o progresso e retornem posteriormente

## Práticas recomendadas de experiência do usuário

### Design móvel

**Otimização Responsiva de Layout**

- Crie formulários com usuários móveis como a principal consideração
- Usar layouts de coluna única para dispositivos móveis
- Garantir que os destinos de toque tenham o tamanho adequado (mínimo de 44 px)
- Testar formulários em vários tamanhos e orientações de dispositivos

**Interações compatíveis com toque**

- Implementar botões maiores e campos de entrada para interfaces de toque
- Use os tipos de entrada apropriados para acionar teclados móveis corretos
- Evite interações dependentes de focalização que não funcionam em dispositivos de toque
- Fornecer feedback visual claro para as interações do usuário

### Conformidade para acessibilidade

**Diretrizes da WCAG 2.1**

- Siga as Diretrizes de acessibilidade de conteúdo da Web para obter um design inclusivo
- Garantir taxas de contraste de cores adequadas (mínimo 4,5:1 para texto normal)
- Fornecer texto alternativo para todas as imagens e ícones
- Implementar a estrutura de cabeçalho adequada e o HTML semântico

**Navegação do Teclado**

- Verifique se todos os elementos de formulário estão acessíveis por meio da navegação pelo teclado
- Fornecer indicadores de foco claros para todos os elementos interativos
- Implementar a ordem lógica de guias por meio de campos de formulário
- Incluir links de navegação ignorados para formulários complexos

**Suporte ao Screen Reader**

- Usar rótulos e descrições ARIA adequados para campos de formulário
- Fornecer mensagens de erro claras anunciadas aos leitores de tela
- Garantir que as alterações de conteúdo dinâmico sejam anunciadas corretamente
- Testar formulários com o software de leitor de tela real

### Otimização do desempenho

**Velocidade de carregamento**

- Otimizar os tempos de carregamento do formulário, minimizando o tamanho inicial do pacote
- Implementar carregamento lento para seções de formulário não críticas
- Otimizar imagens e ativos para entrega na Web
- Ativar estratégias apropriadas de armazenamento em cache para recursos estáticos

**Desempenho de Tempo de Execução**

- Usar o tempo de validação apropriado para equilibrar a experiência e o desempenho do usuário
- Implementar desativação para validação em tempo real para reduzir as solicitações do servidor
- Armazenar em cache os dados acessados com frequência e os resultados de validação
- Otimizar a execução da lógica condicional para formulários complexos

**Salvamento Automático e Proteção de Dados**

- Implementar o salvamento automático do progresso do formulário para evitar perda de dados
- Fornecer recurso offline sempre que possível para o preenchimento do formulário
- Incluir lógica de repetição para envios com falha
- Oferecer opções de exportação de dados como backup para os usuários

## Práticas recomendadas de consistência da marca

### Preparar o Brand Assets com antecedência

**Criar modelos de marca**

- Desenvolver modelos de formulário padronizados com a identidade visual de sua organização
- Incluir esquemas de cores consistentes, tipografia e padrões de layout
- Prepare componentes reutilizáveis que correspondam às diretrizes da sua marca
- Padrões de estilo de documento para implementação consistente em equipes

**Definir Diretrizes de Estilo**

- Estabelecer um estilo de campo consistente, designs de botão e padrões de espaçamento
- Criar um guia de estilo que inclua códigos de cor, especificações de fonte e regras de layout
- Definir padrões de interação e diretrizes de animação
- Preparar mensagens de erro específicas da marca e texto de ajuda

**Biblioteca de Componentes de Compilação**

- Crie componentes de formulário reutilizáveis que correspondam à identidade da sua marca
- Desenvolver padrões de navegação e elementos da interface de usuário consistentes
- Preparar ícones, logotipos e ativos visuais da marca para integração de formulários
- Estabelecer modelos para tipos comuns de formulários (contato, registro, feedback)

### Estratégias de implementação da marca

**Solicitações de Estilo para Consistência**

Inclua instruções específicas da marca em seus prompts:

    Crie um formulário de contato profissional usando:
    - Azul corporativo (#003366) para botões e cabeçalhos principais
    - Família de fontes Sans abertas para todos os elementos de texto
    - Tamanho de fonte mínimo de 16px para conformidade com a acessibilidade
    - Espaçamento consistente de 24px entre seções de formulário
    - Logotipo da empresa no cabeçalho com posicionamento adequado da marca

**Gerenciamento da Biblioteca de Modelos**

- Manter uma coleção de modelos de formulário com marca para casos de uso comuns
- Controle de versão dos modelos da sua marca para garantir a consistência
- Fornecer uma documentação clara para o uso e a personalização do modelo
- Revisão e atualização regulares dos ativos da marca para manter os padrões atuais

>[!NOTE]
>
>**Componentes personalizados**: coordene com sua equipe de desenvolvimento sobre como usar componentes específicos da organização e sua compatibilidade com o Forms Experience Builder antes de implementar elementos de marca personalizados.

## Práticas recomendadas de conteúdo e comunicação

### Abordagens de criação de formulários

**Dois Métodos Primários**

Escolha o método de criação mais apropriado às suas necessidades:

1. **Criar do Zero**: Recomendado para novos formulários com requisitos específicos
2. **Importar e Converter**: ideal para modernizar formulários e documentos existentes

**Solicitações de linguagem natural**

- Ser específico e detalhado nas descrições do formulário
- Use uma linguagem clara, voltada para os negócios, em vez de termos técnicos
- Fornecer contexto sobre a finalidade do formulário e o público-alvo
- Incluir requisitos de validação e regra de negócios nos prompts iniciais

### Estratégia de desenvolvimento incremental

**Comece Simples, Crie Complexidade**

- Comece com a estrutura básica do formulário e os campos essenciais
- Adicionar regras de validação e lógica de negócios de forma incremental
- Teste cada adição antes de prosseguir para o próximo aprimoramento
- Coletar feedback do usuário em cada estágio do desenvolvimento

**Exemplo de Abordagem Incremental:**

    Etapa 1: &quot;Criar um formulário de contato básico com campos de nome, email e mensagem&quot;
    Etapa 2: &quot;Tornar campos obrigatórios @name e @email com validação apropriada&quot;
    Etapa 3: &quot;Adicionar texto de espaço reservado e texto de ajuda para orientação do usuário&quot;
    Etapa 4: &quot;Adicionar lógica condicional baseada no tipo de consulta&quot;

### Práticas recomendadas de referência de campo

**Convenções de nomenclatura consistentes**

- Use nomes de campo claros e descritivos que correspondam à sua finalidade
- Manter padrões de nomenclatura consistentes em todos os formulários
- Use camelCase ou snake_case de forma consistente em todos os formulários
- Convenções de nomenclatura de campo de documento para consistência da equipe

**Referências de campo em vigor**

- Usar a sintaxe `@fieldName` ao modificar campos existentes
- Ser específico sobre quais campos você está referenciando em formulários complexos
- Agrupar modificações de campo relacionadas em solicitações únicas
- Verificar nomes de campo antes de usá-los na lógica condicional

## Práticas recomendadas de integração e envio

### Estratégia de envio de vários canais

**Ações Primárias e Secundárias**

- Configurar os principais endpoints de envio para os principais processos de negócios
- Configurar ações secundárias para notificações, confirmações e backup de dados
- Implementar manipulação de erros e lógica de repetição para envios com falha
- Fornecer feedback do usuário para todos os estados de envio (sucesso, falha, processamento)

**Planejamento de integração**

- Comece com a configuração básica de envio e adicione integrações de forma incremental
- Teste cada integração separadamente antes de combinar vários endpoints
- Requisitos da API de documentos e métodos de autenticação
- Planejar os requisitos de transformação e mapeamento de dados

### Tratamento e recuperação de erros

**Mensagens de Erro Amigáveis ao Usuário**

- Fornecer mensagens de erro claras e acionáveis que ajudem os usuários a resolver problemas
- Evite códigos de erro técnico ou mensagens do sistema em conteúdo voltado para o usuário
- Oferecer ações alternativas quando o envio principal falhar
- Incluir informações de contato para usuários que precisam de ajuda adicional

**Proteção e recuperação de dados**

- Implementar o salvamento de dados locais para recuperação de formulários após erros
- Fornecer opções para que os usuários baixem os dados de formulário como backup
- Configurar monitoramento e alertas de falhas de envio
- Planejar procedimentos de recuperação para paralisações ou manutenção do sistema

## Práticas recomendadas de desempenho e análise

### Monitoramento e otimização

**Métricas Principais de Desempenho**

- Rastrear as taxas de conclusão do formulário e os pontos de abandono
- Monitorar tempos de carregamento e padrões de interação do usuário
- Medir a eficácia da validação e as taxas de erro
- Analisar as pontuações de feedback e satisfação do usuário

**Aprimoramento Contínuo**

- Revisão regular da análise de formulários para identificar oportunidades de otimização
- Teste A/B de diferentes designs de formulário e fluxos de usuário
- Coleta e análise de feedback do usuário para melhorias iterativas
- Comparação de desempenho com os padrões do setor

### Qualidade e validação dos dados

**Estratégias de validação inteligente**

- Implementar validação em tempo real para feedback imediato do usuário
- Use a validação progressiva para orientar os usuários sobre requisitos complexos
- Fornecer mensagens de validação claras que expliquem como corrigir erros
- Rigor na validação de equilíbrio com considerações sobre a experiência do usuário

**Integridade dos dados**

- Implementar validação entre campos para manter a consistência dos dados
- Usar tipos e restrições de entrada apropriados para evitar dados inválidos
- Fornecer exemplos de formato de dados e orientação para campos complexos
- Auditoria regular da qualidade dos dados enviados e da eficácia da validação

## Práticas recomendadas de segurança e conformidade

### Proteção de dados

**Privacidade por design**

- Colete apenas os dados mínimos necessários para o seu objetivo comercial
- Implementar políticas apropriadas de retenção e exclusão de dados
- Fornecer avisos de privacidade e mecanismos de consentimento claros
- Garantir a conformidade com as normas relevantes de proteção de dados (GDPR, CCPA etc.)

**Implementação de segurança**

- Usar criptografia HTTPS para todos os envios de formulários e transmissão de dados
- Implementar a validação e a limpeza adequadas dos dados de entrada
- Configurar o upload seguro de arquivos com as restrições apropriadas e a análise de vírus
- Auditorias regulares de segurança e avaliações de vulnerabilidades

### Considerações sobre conformidade

**Requisitos normativos**

- Compreender e implementar os requisitos de conformidade específicos do setor
- Medidas de conformidade dos documentos para fins de auditoria
- Revisão regular das alterações regulamentares e seu impacto nos formulários
- Treinamento da equipe em requisitos de conformidade e implementação

**Conformidade de Acessibilidade**

- Siga as diretrizes AA da WCAG 2.1 para acessibilidade
- Testes regulares de acessibilidade com tecnologias assistivas
- Teste de usuários com pessoas portadoras de deficiências
- Documentação dos recursos de acessibilidade e das medidas de conformidade

## Práticas recomendadas do Team Collaboration

### Compartilhamento de conhecimento e documentação

**Documentação do formulário**

- Manter documentação clara de finalidades do formulário, requisitos e regras de negócios
- Endpoints de integração de documentos, fluxos de dados e dependências
- Manter histórico de versões e logs de alterações para atualizações de formulários
- Compartilhar práticas recomendadas e lições aprendidas em equipes

**Treinamento e adoção**

- Fornecer treinamento para membros da equipe sobre os recursos do Forms Experience Builder
- Estabelecer diretrizes para a criação consistente de formulários em toda a organização
- Sessões regulares de compartilhamento de conhecimento para novos recursos e práticas recomendadas
- Programas de orientação para novos usuários da plataforma

### Controle de qualidade

**Processos de revisão**

- Implementar processos de revisão por pares para projeto e implementação de formulários
- Estabelecer protocolos de teste para a funcionalidade do formulário e a experiência do usuário
- Auditorias regulares de formulários existentes para oportunidades de otimização
- Coleção de comentários de usuários internos e usuários finais

**Padrões e Diretrizes**

- Desenvolver padrões organizacionais para o design e a implementação de formulários
- Criar modelos e diretrizes para tipos de formulários comuns
- Estabelecer processos de aprovação para novos formulários e grandes alterações
- Revisão e atualização periódicas das normas organizacionais

## Práticas recomendadas avançadas

### Campos inteligentes aprimorados com LLM

**Aproveitando o conhecimento sobre IA**

- Use o conhecimento integrado da IA para opções de campo abrangentes
- Solicitar campos inteligentes para dados geográficos, classificações comerciais e padrões do setor
- Implementar população de campo inteligente para melhorar a experiência do usuário
- Teste a precisão e a integridade do campo inteligente para seus casos de uso específicos

**Exemplos de Campos Inteligentes**

    &quot;Adicionar um campo de aeroporto de partida com todos os principais aeroportos do mundo inteiro, incluindo códigos IATA&quot;
    &quot;Criar um campo do setor abrangente usando a classificação NAICS padrão&quot;
    &quot;Incluir uma lista suspensa de certificação profissional que se adapta com base no campo de trabalho&quot;

### Lógica de formulário avançada

**Regras de Negócios Complexas**

- Divida a complexa lógica de negócios em componentes menores e testáveis
- Documentar os requisitos da regra de negócios claramente antes da implementação
- Testar detalhadamente casos de borda e cenários de exceção
- Fornecer feedback claro do usuário para violações de regras de negócios

**Comportamento do formulário dinâmico**

- Usar a divulgação progressiva para mostrar campos relevantes com base na entrada do usuário
- Implementar padrões inteligentes que podem ser substituídos pelos usuários
- Criar formulários adaptáveis que se ajustam com base no comportamento e nas preferências do usuário
- Equilibre a automação com controle e transparência do usuário

## Validação e teste

### Estratégia abrangente de testes

**Teste de Vários Níveis**

- Teste de unidade para componentes de formulário individuais e regras de validação
- Teste de integração para endpoints de envio e fluxos de dados
- Teste de aceitação do usuário com grupos representativos de usuários
- Ensaio de desempenho em várias condições de carga

**Validação entre plataformas**

- Testar formulários em diferentes navegadores e versões
- Validar experiência móvel em vários dispositivos e tamanhos de tela
- Teste de acessibilidade com diferentes tecnologias assistivas
- Teste de condição de rede para várias velocidades de conexão

### Métricas de qualidade

**Indicadores de sucesso**

- Taxas de conclusão de formulários acima dos benchmarks do setor
- Baixas taxas de erro e altas pontuações de satisfação do usuário
- Carregamento rápido e interações responsivas do usuário
- Integração bem-sucedida com sistemas e processos de back-end

**Monitoramento contínuo**

- Revisão regular das métricas de desempenho do formulário e feedback do usuário
- Identificação e resolução proativas de problemas
- Análise de tendências para uso e eficácia de formulários
- Avaliação comparativa com padrões do setor e práticas recomendadas

Para obter orientação adicional e exemplos detalhados, consulte o [Guia de Introdução do Forms Experience Builder](forms-ai-assistant-getting-started.md) e a [Biblioteca de Prompts do Forms Experience Builder](ai-assistant-prompt-library.md).
