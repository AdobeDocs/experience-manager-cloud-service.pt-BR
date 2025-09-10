---
title: Como configurar uma página de redirecionamento ou uma mensagem de agradecimento
description: Saiba como os usuários podem exibir uma mensagem de agradecimento ou ser redirecionados para uma página da Web que os autores de formulários podem configurar ao criar o formulário.
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
exl-id: cacd7b0a-aad0-4b5d-a6a0-e4bac4cb196d
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 0%

---

# Configurar mensagens de agradecimento e URLs de redirecionamento

As experiências pós-envio afetam significativamente a satisfação do usuário e as taxas de conclusão do formulário. O Editor universal do Adobe fornece opções abrangentes para configurar o que os usuários veem após enviar formulários, seja por meio de mensagens de agradecimento personalizadas ou redirecionamentos estratégicos para páginas específicas.

Este artigo fornece orientação detalhada sobre como implementar mensagens de agradecimento e URLs de redirecionamento, incluindo considerações técnicas, práticas recomendadas e diretrizes de experiência do usuário para maximizar a eficiência dos envios de formulários.

## Pré-requisitos

Antes de configurar as experiências pós-envio, verifique se você tem:

**Configuração técnica:**

- Acesso ao Universal Editor com permissões apropriadas
- Um formulário adaptável existente criado no Editor universal
- Noções básicas sobre os requisitos de URL de redirecionamento de sua organização

**Considerações sobre planejamento:**

- **Estratégia da mensagem**: defina o tom, o comprimento e as informações específicas a serem incluídas nas mensagens de agradecimento
- **Estratégia de redirecionamento**: identifique páginas de destino e verifique se elas estão otimizadas para experiências de conclusão pós-formulário
- **Integração do Analytics**: planeje como rastrear as interações do usuário com mensagens de agradecimento ou destinos de redirecionamento

## Configurar mensagens de agradecimento

As mensagens de agradecimento fornecem reconhecimento imediato do envio bem-sucedido do formulário e podem incluir conteúdo personalizado, próximas etapas ou informações importantes relevantes para o envio do usuário.

### Quando usar mensagens de agradecimento

As mensagens de agradecimento funcionam melhor quando:

- **Confirmação simples**: os usuários precisam de confirmação sem requisitos de navegação adicionais
- **Conteúdo de instrução**: você precisa fornecer as próximas etapas específicas ou informações importantes
- **Consistência da marca**: a mensagem pode ser trabalhada para se alinhar ao estilo de comunicação de sua organização
- **Experiência de página única**: os usuários devem permanecer na página atual para continuidade do fluxo de trabalho

### Etapas da implementação

**1. Acessar propriedades do formulário**

Abra o formulário adaptável no Universal Editor e clique no ícone **Editar propriedades do formulário** na barra de ferramentas. Isso abre a caixa de diálogo de propriedades do formulário abrangente.

![Ícone de propriedades do formulário](/help/forms/assets/ue-form-properties-icon.png)

**2. Navegue para agradecer a configuração**

Na caixa de diálogo Propriedades do formulário, selecione a guia **Obrigado** para acessar as opções de configuração pós-envio.

![Propriedades de Formulário do Editor Universal](/help/forms/assets/ue-form-properties.png)

**3. Configurar exibição de mensagem**

Selecione **Mostrar mensagem** nas opções disponíveis.

![obrigado](/help/edge/docs/forms/universal-editor/assets/thankyou-ue.png)

**4. Criar o conteúdo da sua mensagem**

No campo **Conteúdo da mensagem**, crie sua mensagem de agradecimento usando o editor de rich text. O editor oferece suporte a:

- **Formatação do texto**: opções de negrito, itálico, sublinhado e cor
- **Listas**: listas com marcadores e numeradas para informações de organização
- **Links**: links diretos para recursos relevantes ou próximas etapas
- **Edição em tela cheia**: clique no ícone de expansão para obter um espaço de trabalho de edição maior

### Considerações técnicas

**Comportamento de exibição da mensagem:**

- As mensagens são exibidas em uma sobreposição modal imediatamente após o envio do formulário
- O conteúdo é compatível com a formatação do HTML e mantém o design responsivo
- As mensagens podem ser descartadas pelos usuários ou configuradas com temporizadores de fechamento automático

**Diretrizes de conteúdo:**

- Mantenha as mensagens concisas enquanto fornece as informações necessárias
- Inclua etapas claras a seguir quando apropriado
- Considere incluir números de referência ou detalhes de confirmação
- Garantir a formatação móvel amigável

### Exemplo de implementação

    Obrigado por seu envio!
    
    Seu aplicativo foi recebido e recebeu o número de referência #REF-2024-001234.
    
    **O que acontece a seguir:**
    - Você receberá um email de confirmação em 15 minutos
    - Nossa equipe verificará seu envio em 2 dias úteis
    - Entraremos em contato diretamente se forem necessárias informações adicionais
    
    **Precisa de assistência?** Entre em contato com nossa equipe de suporte em support@example.com

## Configurar URLs de redirecionamento

Os URLs de redirecionamento navegam automaticamente os usuários para páginas específicas após o envio do formulário, permitindo uma integração perfeita com os fluxos de trabalho existentes ou direcionando os usuários para o conteúdo relevante.

### Quando usar URLs de redirecionamento

Os URLs de redirecionamento são ideais para:

- **Integração do fluxo de trabalho**: direcionar usuários para painéis, páginas de conta ou próximas etapas em um processo
- **Entrega de conteúdo**: mostrando produtos, serviços ou informações relevantes com base em respostas de formulário
- **Rastreamento do Analytics**: direcionar para páginas com implementações de rastreamento específicas
- **Processos de várias etapas**: movendo usuários para a próxima fase de fluxos de trabalho complexos

### Etapas da implementação

**1. Acessar propriedades do formulário**

Abra o formulário adaptável no Universal Editor e clique no ícone **Editar propriedades do formulário** para abrir a caixa de diálogo de configuração do formulário.

![Ícone de propriedades do formulário](/help/forms/assets/ue-form-properties-icon.png)

**2. Navegue para agradecer a configuração**

Selecione a guia **Obrigado** na caixa de diálogo Propriedades do formulário para acessar as opções de configuração de redirecionamento.

![Propriedades de Formulário do Editor Universal](/help/forms/assets/ue-form-properties.png)

**3. Habilitar funcionalidade de redirecionamento**

Escolha **Redirecionar para URL** nas opções pós-envio disponíveis.

![redirecionar](/help/edge/docs/forms/universal-editor/assets/redirect-ue.png)

**4. Configurar URL de destino**

Digite seu URL de destino no campo fornecido. O sistema é compatível com vários formatos de URL para implementação flexível.

### Opções de configuração de URL

**URLs absolutas**

Endereços da Web completos, incluindo protocolo e domínio:

    https://www.example.com/thank-you
    https://dashboard.example.com/user/profile

**Caminhos relativos**

Caminhos relativos ao seu domínio atual:

    /obrigado
    /painel/perfil-usuário
    ../confirmation-page.html

**Referências de página do AEM Sites**

Referências a outras páginas na implementação do AEM Sites:

    /content/mysite/en/thank-you
    /content/mysite/en/next-steps

### Considerações técnicas

**Comportamento de redirecionamento:**

- Os redirecionamentos ocorrem imediatamente após o envio bem-sucedido do formulário
- O histórico do navegador inclui o redirecionamento para a funcionalidade adequada do botão traseiro
- O tempo de redirecionamento pode ser configurado com atrasos opcionais

**Validação de URL:**

- O sistema valida o formato do URL antes de permitir a configuração
- URLs relativos são resolvidos em relação ao domínio atual
- Os URLs externos exigem a configuração adequada do CORS, se necessário

## Práticas recomendadas

### Diretrizes de experiência do usuário

**Otimização da mensagem:**

- **Clareza primeiro**: verifique se os usuários entenderam imediatamente que o envio foi bem-sucedido
- **Valor adicionado**: forneça informações que ajudem os usuários com as próximas etapas
- **Marca consistente**: mantenha a voz e o estilo visual de sua organização
- **Consideração móvel**: testar mensagens em vários tamanhos de tela

**Otimização de redirecionamento:**

- **Otimização da página**: certifique-se de que os destinos de redirecionamento estejam otimizados para visitantes pós-formulário
- **Desempenho de carregamento**: verifique se as páginas de redirecionamento carregam rapidamente para manter a experiência do usuário
- **Relevância de conteúdo**: verifique se o conteúdo de redirecionamento é relevante para o contexto do formulário

### Considerações sobre segurança

**Validação de URL:**

- Implemente a validação adequada para URLs de redirecionamento para impedir redirecionamentos mal-intencionados
- Considerar abordagens da lista de permissões para domínios de redirecionamento permitidos
- Monitorar padrões de redirecionamento para atividades incomuns

**Segurança de conteúdo:**

- Limpar conteúdo da mensagem de agradecimento para evitar a injeção de scripts
- Implementar políticas apropriadas de segurança de conteúdo para conteúdo rich text
- Revisões de segurança regulares de destinos de redirecionamento

### Analytics e rastreamento

**Considerações de implementação:**

- **Rastreamento de metas**: configurar metas de análise para exibições de mensagens de agradecimento e conclusões de redirecionamento
- **Mapeamento da jornada do usuário**: controle a forma como os usuários interagem com as experiências após o envio
- **Otimização de conversão**: teste A/B diferente para mensagens de agradecimento e destinos de redirecionamento

**Estratégias de medição:**

- Monitorar o tempo gasto nas mensagens de agradecimento antes da demissão
- Rastrear as taxas de click-through para links nas mensagens de agradecimento
- Analisar o comportamento do usuário nas páginas de destino de redirecionamento

## Pontos de verificação de validação

Após configurar sua experiência pós-envio:

**Verificação de configuração:**

- As propriedades do formulário mostram corretamente a opção de agradecimento selecionada
- O conteúdo da mensagem é exibido corretamente no modo de visualização
- Os URLs de redirecionamento estão formatados e acessíveis corretamente
- Todos os links nas mensagens funcionam corretamente

**Teste de experiência do usuário:**

- Envie formulários de teste para verificar a exibição adequada da mensagem de agradecimento
- Testar a funcionalidade de redirecionamento em navegadores diferentes
- Verificar a agilidade móvel das mensagens de agradecimento
- Confirmar se os destinos de redirecionamento são carregados corretamente

**Configuração do Analytics:**

- Códigos de rastreamento implementados corretamente para mensagens de agradecimento
- Rastreamento de destino de redirecionamento configurado
- Eventos de conclusão de meta acionados corretamente

## Próximas etapas

Após configurar com êxito sua experiência pós-envio:

- **Monitorar desempenho**: analise as análises para entender o engajamento do usuário com mensagens de agradecimento ou redirecione páginas
- **Iterar e melhorar**: use o feedback do usuário e os insights de dados para refinar sua estratégia pós-envio
- **Implementação de escala**: aplique padrões bem-sucedidos em outros formulários em sua organização

**Documentação relacionada:**

- [Guia de configuração de envio de formulário](submit-action.md)
- [Práticas recomendadas de experiência do usuário](responsive-layout.md)
