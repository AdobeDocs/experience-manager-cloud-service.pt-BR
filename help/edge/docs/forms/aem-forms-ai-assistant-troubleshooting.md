---
title: Forms Experience Builder - Guia de solução de problemas
description: Guia abrangente de solução de problemas do Forms Experience Builder, abordando problemas comuns, soluções e técnicas de depuração para criação e gerenciamento de formulários.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 6a7810fd-2860-410b-867d-8d29afd5297d
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2282'
ht-degree: 0%

---


# Forms Experience Builder - Guia de solução de problemas

>[!NOTE]
>
> O Forms Experience Builder está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: este guia de solução de problemas está sendo testado no momento em relação ao produto e está sujeito a atualizações e revisões. Problemas, soluções e técnicas de depuração podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

Este abrangente guia de solução de problemas ajuda você a identificar, diagnosticar e resolver problemas comuns ao trabalhar com o Forms Experience Builder. O guia é organizado por categorias de problemas com correções rápidas e soluções detalhadas.

## Referência rápida - Problemas comuns

| Problema | Correção rápida |
|-------|-----------|
| **Interface não carregando** | Atualizar navegador, verificar conexão com a Internet e permissões de acesso antecipado |
| **Comandos não funcionando** | Experimente `/help` ou use linguagem natural em vez de comandos de barra |
| **@fieldName não reconhecido** | Verifique a ortografia, verifique se o campo existe primeiro, verifique a sintaxe do nome do campo |
| **Falha ao carregar o arquivo** | Use PDF/JPG/PNG com menos de 10 MB e verifique a compatibilidade do formato de arquivo |
| **Aparência incorreta do formulário** | Seja mais específico: &quot;Tornar compatível com dispositivos móveis&quot; em vez de &quot;corrigir layout&quot; |
| **Falha na integração** | Verifique as credenciais e permissões da API, verifique a disponibilidade do endpoint |
| **Formulário não enviado** | Verificar regras de validação e configuração da ação de envio |
| **Erros de validação não exibidos** | Verificar configurações de validação de campo e posicionamento de mensagem de erro |
| **Problemas de layout móvel** | Revisar configurações de design responsivo e dimensionamento de campo |
| **Campos que não aparecem** | Verificar lógica condicional e regras de visibilidade |
| **Falhas na importação** | Verificar a compatibilidade do formato de arquivo e os limites de tamanho |
| **Problemas de desempenho** | Otimizar a contagem de campos e remover validações desnecessárias |
| **Problemas de acessibilidade** | Revisar rótulos de campo, atributos ARIA e ordem de tabulação |

**Ainda precisa de ajuda?** Digite `/help` seguido de sua pergunta específica ou contate o administrador do sistema para obter assistência técnica.

## Problemas de acesso e autenticação

### Não é possível acessar o Forms Experience Builder

**Sintomas:**

- Interface do Forms Experience Builder não visível
- Mensagens de erro do tipo &quot;Acesso negado&quot; ou semelhantes
- Ícone ausente do Forms Experience Builder no editor

**Soluções:**

1. **Verificar Inscrição no Programa de Acesso Antecipado**
   - Confirmar se você foi aprovado para o programa de adoção antecipada
   - Verifique se sua solicitação foi enviada do email de trabalho oficial
   - Contate `aem-forms-ea@adobe.com` se o acesso ainda estiver pendente

2. **Verificar Configuração do Ambiente**
   - Verifique se o AEM Forms está ativado para o seu ambiente
   - Verifique se você está usando um navegador compatível (Chrome, Firefox, Safari, Edge)
   - Limpar cache do navegador e cookies
   - Desative as extensões do navegador que possam interferir

3. **Verificar Permissões de Usuário**
   - Confirme se você tem as funções e permissões de usuário apropriadas
   - Verifique com o administrador do sistema os direitos de acesso
   - Verifique se você está conectado com a conta correta

### Problemas de carregamento de interface

**Sintomas:**

- Interface em branco ou parcialmente carregada
- Rotação de indicadores de carregamento que não concluem
- Erros do JavaScript no console do navegador

**Soluções:**

1. **Solução de problemas do navegador**
   - Atualizar a página (Ctrl+F5 ou Cmd+Shift+R)
   - Tente usar um navegador diferente ou o modo incógnito/privado
   - Verificar atualizações do navegador e instalar, se disponível
   - Desative temporariamente bloqueadores de anúncios e extensões de privacidade

2. **Conectividade de Rede**
   - Verificar conexão estável com a Internet
   - Verificar se o firewall corporativo está bloqueando os domínios necessários
   - Testar com uma conexão de rede diferente, se possível
   - Entre em contato com o suporte de TI para solucionar problemas de configuração de rede

3. **Problemas de cache e armazenamento**
   - Limpar o cache do navegador e o armazenamento local
   - Redefinir as configurações padrão do navegador
   - Verificar o espaço disponível em disco no dispositivo
   - Tente acessar de um dispositivo diferente

## Problemas de comando e interação

### Comandos de barras não funcionam

**Sintomas:**

- `/create-form` ou outros comandos de barra não reconhecidos
- Nenhuma sugestão de preenchimento automático é exibida
- Comandos resultam em mensagens de erro

**Soluções:**

1. **Verificação de Sintaxe de Comando**
   - Verifique se o formato do comando é adequado: `/command-name description`
   - Verificar erros de digitação em nomes de comando
   - Use a linguagem natural como alternativa: &quot;Criar um formulário de contato&quot;
   - Tente `/help` para verificar a disponibilidade do comando

2. **Comandos Específicos de Contexto**
   - Verifique se você está no contexto correto do editor (Editor universal vs Editor Forms adaptável)
   - Alguns comandos só funcionam em ambientes específicos
   - Verificar referência de comando para requisitos de contexto

3. **Abordagens Alternativas**
   - Usar linguagem natural em vez de comandos de barra
   - Dividir comandos complexos em solicitações menores e mais simples
   - Tente criar um formulário passo a passo em vez de um único comando complexo

### As Referências De Campo Não Funcionam

**Sintomas:**

- `@fieldName` referências não reconhecidas
- Mensagens de erro sobre campos desconhecidos
- Modificações de campo não aplicadas corretamente

**Soluções:**

1. **Verificação de nome de campo**
   - Verificar a ortografia exata dos nomes de campo (distinção entre maiúsculas e minúsculas)
   - Verifique se o campo existe antes de referenciá-lo
   - Usar o nome de campo exato como criado, não o rótulo de exibição
   - Verificar as convenções de nomenclatura do campo (camelCase, snake_case etc.)

2. **Sintaxe de referência de campo**
   - Usar a sintaxe `@fieldName` apropriada sem espaços
   - Evitar caracteres especiais nas referências de campo
   - Verifique se há caracteres invisíveis ou problemas de formatação
   - Tente recriar a referência de campo manualmente

3. **Depurando Referências de Campo**
   - Listar todos os campos existentes primeiro: &quot;Mostrar todos os campos de formulário atuais&quot;
   - Criar campos antes de fazer referência a eles nas regras
   - Usar nomes de campo simples sem caracteres complexos
   - O campo de teste faz referência a um de cada vez

## Problemas de criação e design do formulário

### O formulário não é criado conforme esperado

**Sintomas:**

- Formulário gerado sem campos solicitados
- Tipos ou layouts de campo incorretos
- A estrutura do formulário não corresponde à descrição

**Soluções:**

1. **Melhore A Especificidade Do Prompt**
   - Ser mais detalhado nas descrições do formulário
   - Especificar tipos de campos exatos e requisitos de validação
   - Incluir preferências de layout e requisitos de experiência do usuário
   - Divida formulários complexos em solicitações menores e incrementais

2. **Abordagem de desenvolvimento iterativa**
   - Começar com estrutura básica do formulário
   - Adicionar campos e recursos de forma incremental
   - Teste cada adição antes de continuar
   - Refinar por meio de conversa em vez de uma única solicitação complexa

3. **Exemplo de Prompts Melhores**

   Em vez de:

       Criar um formulário para clientes
   
   Uso:

       Criar um formulário de contato do cliente com:
       - Nome completo (campo de texto obrigatório)
       - Endereço de email (obrigatório com validação)
       - Número de telefone (opcional, formatado)
       - Mensagem (área de texto necessária, máximo de 500 caracteres)
       - Enviar notificação por e-mail
   
### Problemas de layout e estilo

**Sintomas:**

- O formulário parece corrompido em dispositivos móveis
- Espaçamento ou alinhamento inconsistente
- Os campos não são exibidos corretamente
- Hierarquia visual deficiente

**Soluções:**

1. **Capacidade de resposta móvel**
   - Solicitar otimizações específicas para dispositivos móveis: &quot;Tornar este formulário compatível com dispositivos móveis&quot;
   - Especificar requisitos de design responsivo
   - Testar em dispositivos móveis reais
   - Usar layouts de coluna única para dispositivos móveis

2. **Melhorias de layout**
   - Seja específico quanto aos requisitos de layout: &quot;Organizar campos de endereço em duas colunas&quot;
   - Solicitar estilo específico: &quot;Usar cores profissionais e tipografia limpa&quot;
   - Especificar necessidades de espaçamento e alinhamento
   - Solicitar conformidade de acessibilidade

3. **Consistência de marca**
   - Preparar as diretrizes de marca antes da criação do formulário
   - Incluir códigos de cor e fontes específicos nas solicitações
   - Usar estilo consistente em todos os formulários
   - Criar modelos de marca para reutilização

### Problemas de Lógica Condicional

**Sintomas:**

- Regras que não são acionadas conforme esperado
- Campos exibidos/ocultados incorretamente
- A lógica de validação não está funcionando
- Falha em regras de negócios complexas

**Soluções:**

1. **Simplificação de regras**
   - Quebre regras complexas em condições menores e mais simples
   - Teste cada regra individualmente antes de combinar
   - Use condições claras e específicas: &quot;Mostrar @spouseInfo quando @maritalStatus for igual a &quot;Casado&quot;&quot;
   - Evitar lógica aninhada ou excessivamente complexa inicialmente

2. **Teste e depuração de regras**
   - Testar todos os caminhos e cenários possíveis do usuário
   - Verificar nomes e valores de campo em condições
   - Verificar a diferenciação entre maiúsculas e minúsculas nas condições da regra
   - Usar o modo de depuração para rastrear a execução da regra

3. **Implementação da lógica de negócios**
   - Documente os requisitos de negócios claramente antes da implementação
   - Implementar regras de maneira incremental e testar cada etapa
   - Fornecer feedback claro do usuário quando as regras forem acionadas
   - Tratar casos de borda e cenários de exceção

## Problemas de importação e conversão de arquivo

### Falhas de importação do PDF

**Sintomas:**

- Arquivos do PDF que não estão sendo carregados ou processados
- Formulários convertidos sem campos ou conteúdo
- Mensagens de erro durante a conversão do PDF
- Reconhecimento de campo insatisfatório do PDF

**Soluções:**

1. **Formato e Tamanho do Arquivo**
   - Verifique se os arquivos do PDF têm menos de 10 MB
   - Usar PDFs de alta qualidade baseados em texto (não imagens digitalizadas)
   - Verificar se o PDF não está protegido por senha ou criptografado
   - Tente converter o PDF para o formato de imagem se a extração de texto falhar

2. **Otimização de qualidade do PDF**
   - Usar PDFs com campos de formulário claros e bem definidos
   - Garantir bom contraste e texto legível
   - Evitar layouts complexos ou elementos sobrepostos
   - Fornecer contexto adicional na solicitação de conversão

3. **Aprimoramento de conversão**
   - Descreva detalhadamente a estrutura do formulário esperado
   - Especificar tipos de campo e requisitos de validação
   - Solicitar melhorias específicas: &quot;Adicionar agilidade e validação móvel&quot;
   - Revisar e refinar formulários convertidos manualmente

### Problemas de conversão de imagem e captura de tela

**Sintomas:**

- Reconhecimento de campo insatisfatório de imagens
- Tipos ou layouts de campo incorretos
- Elementos de formulário ausentes
- Erros de conversão ou tempos limite

**Soluções:**

1. **Requisitos de qualidade de imagem**
   - Usar imagens de alta resolução (mínimo 300 DPI)
   - Garanta uma boa iluminação e contraste
   - Evite sombras, brilhos ou distorções
   - Cortar imagens para focalizar somente o conteúdo do formulário

2. **Formatos de imagem ideais**
   - Usar formatos PNG ou JPG para obter melhores resultados
   - Evite imagens GIF ou compactadas de baixa qualidade
   - Garantir que o texto seja claramente legível na imagem
   - Tente orientações de imagem diferentes, se necessário

3. **Diretrizes de conversão**
   - Fornecer descrições detalhadas da estrutura do formulário
   - Especificar explicitamente os tipos e requisitos de campo
   - Solicitar melhorias específicas durante a conversão
   - Esteja preparado para fazer ajustes manuais após a conversão

## Problemas de integração e envio

### Falhas no envio do formulário

**Sintomas:**

- O Forms não está enviando com sucesso
- Mensagens de erro durante o envio
- Dados que não alcançam os destinos pretendidos
- Erros de tempo limite durante o envio

**Soluções:**

1. **Configuração de ação de envio**
   - Verificar se a ação de envio está configurada corretamente
   - Verificar endpoints de API e credenciais de autenticação
   - Testar com envio de email simples primeiro
   - Validar requisitos de formato de dados

2. **Rede e Conectividade**
   - Verifique a conectividade com a Internet e a estabilidade da rede
   - Verificar se as configurações de firewall permitem o envio de formulários
   - Testar de conexões de rede diferentes
   - Verificar se há restrições de segurança ou proxy corporativo

3. **Problemas de validação de dados**
   - Garantir que todos os campos obrigatórios sejam preenchidos
   - Verificar se os formatos de dados correspondem aos requisitos da API
   - Verifique se há caracteres especiais ou problemas de codificação
   - Testar primeiro com conjunto mínimo de dados

### Problemas de integração da API

**Sintomas:**

- Pontos de extremidade da REST API não respondem
- Falhas de autenticação
- Incompatibilidade de formato de dados
- Tempos limite ou erros de integração

**Soluções:**

1. **Verificação de configuração de API**
   - Verifique se os URLs do endpoint da API estão corretos e acessíveis
   - Verificar credenciais e permissões de autenticação
   - Teste os pontos de extremidade da API de maneira independente usando ferramentas como o Postman
   - Verificar se a API está aceitando o formato de dados correto (JSON, XML etc.)

2. **Problemas de Mapeamento de Dados**
   - Garantir que os nomes dos campos de formulário correspondam aos requisitos do parâmetro da API
   - Verifique os campos obrigatórios que podem estar ausentes
   - Verificar a compatibilidade do tipo de dados (cadeias de caracteres, números, datas)
   - Teste com dados de amostra para identificar problemas de mapeamento

3. **Tratamento e depuração de erros**
   - Habilitar o log de erros detalhado para chamadas de API
   - Verificar códigos de resposta da API e mensagens de erro
   - Implementar lógica de repetição para falhas temporárias
   - Fornecer opções de fallback para os usuários quando a API falhar

### Problemas de integração de email

**Sintomas:**

- Emails de confirmação não enviados
- Emails indo para pastas de spam
- Formatação de email incorreta
- Dados de formulário ausentes em emails

**Soluções:**

1. **Configuração de email**
   - Verifique se os endereços de email estão formatados corretamente
   - Verificar configurações e autenticação SMTP
   - Testar primeiro com endereços de email simples
   - Verificar permissões e cotas do servidor de email

2. **Otimização de Entrega de Email**
   - Usar cabeçalhos de email e informações do remetente apropriados
   - Evite palavras de acionamento de spam nas linhas de assunto
   - Incluir mecanismos adequados de cancelamento de inscrição
   - Testar a entrega de email para provedores diferentes

3. **Conteúdo e formatação**
   - Verificar se os dados do formulário estão formatados corretamente em emails
   - Verifique se há caracteres especiais ou problemas de codificação
   - Testar modelos de email com várias combinações de dados
   - Garantir que o conteúdo de e-mail esteja acessível e legível

## Problemas de desempenho e de carregamento

### Carregamento lento de formulário

**Sintomas:**

- O Forms leva muito tempo para carregar inicialmente
- Interações lentas do usuário
- Tempos limite durante operações de formulário
- Baixo desempenho em dispositivos móveis

**Soluções:**

1. **Otimização de formulários**
   - Reduza o número de campos e a complexidade
   - Implementar carregamento lento para seções não críticas
   - Otimizar imagens e ativos para entrega na Web
   - Remover regras ou lógicas de validação desnecessárias

2. **Otimização de Navegador e Dispositivo**
   - Limpar o cache do navegador e os arquivos temporários
   - Feche guias e aplicativos desnecessários do navegador
   - Verificar memória e armazenamento de dispositivo disponíveis
   - Use navegadores diferentes para comparar o desempenho

3. **Otimização de Rede**
   - Testar com conexões de rede diferentes
   - Verificar se há congestionamento de rede ou limitações de largura de banda
   - Usar conexão com fio em vez de WiFi, se possível
   - Entre em contato com o suporte de TI para solucionar problemas de desempenho de rede

### Problemas de Desempenho de Validação

**Sintomas:**

- Respostas de validação lentas
- Exibição de mensagem de erro atrasada
- Congelamento de formulários durante a validação
- Erros de tempo limite durante a validação de campo

**Soluções:**

1. **Otimização da validação**
   - Reduzir a frequência da validação em tempo real
   - Implementar desistências para chamadas de validação
   - Simplificar regras de validação complexas
   - Usar a validação do lado do cliente quando possível

2. **Simplificação de regras**
   - Divida a validação complexa em regras menores
   - Remover validações desnecessárias entre campos
   - Otimizar a lógica condicional para o desempenho
   - Armazenar em cache os resultados da validação quando apropriado

3. **Melhorias na experiência do usuário**
   - Fornecer feedback imediato para validações simples
   - Use a validação progressiva em vez do tempo real para regras complexas
   - Mostrar indicadores de carregamento durante processos de validação
   - Permitir que os usuários continuem enquanto a validação processa em segundo plano

## Solução avançada de problemas

### Modo de depuração e diagnósticos

**Habilitar Informações de Depuração**

Use estes prompts para obter informações mais detalhadas sobre problemas de formulário:

    Habilite o modo de depuração para identificar problemas com o envio do formulário e a validação do campo
    
    Analisar erros de formulário: verifique as regras de validação, as respostas da API e os padrões de entrada do usuário
    
    Mostrar informações detalhadas sobre a estrutura do formulário e a configuração do campo

### Técnicas de análise de erros

**Abordagem de depuração sistemática**

1. **Isolar o problema**
   - Testar com configuração mínima de formulário
   - Remover temporariamente recursos complexos
   - Testar componentes individuais separadamente
   - Usar o processo de eliminação para identificar a causa básica

2. **Coletar Informações De Diagnóstico**
   - Verifique se há erros de JavaScript no console do navegador
   - Revisar solicitações e respostas da rede
   - Documente as etapas exatas para reproduzir o problema
   - Coletar capturas de tela e mensagens de erro

3. **Testar Variáveis de Ambiente**
   - Experimente navegadores e dispositivos diferentes
   - Testar com contas e permissões de usuário diferentes
   - Verificar em ambientes de rede diferentes
   - Comparar com formulários de trabalho ou configurações

### Monitoramento e análise de registros

**Depuração do Console do Navegador**

1. Abrir ferramentas do desenvolvedor do navegador (F12)
2. Verifique se há erros no JavaScript na guia Console
3. Consulte a guia Rede para verificar se há solicitações com falha
4. Guia Monitorar desempenho para operações lentas

**Padrões de Erro Comuns**

- **Erros CORS**: problemas de solicitação entre origens com integrações de API
- **Falhas de Autenticação**: credenciais inválidas ou tokens expirados
- **Erros de Validação**: conflitos de regra de validação de campo ou erros de sintaxe
- **Limites de Tempo de Rede**: Conexões de rede lentas ou não confiáveis

## Como obter mais ajuda

### Recursos de autoatendimento

**Sistema de Ajuda Interno**

- Usar o comando `/help` seguido de perguntas específicas
- Acessar ajuda contextual na interface do Forms Experience Builder
- Revise as mensagens de erro cuidadosamente para obter orientação específica
- Verifique o [Guia de Introdução do Forms Experience Builder](forms-ai-assistant-getting-started.md)

**Recursos da Documentação**

- [Biblioteca de Prompts do Forms Experience Builder](ai-assistant-prompt-library.md)
- [Práticas recomendadas do Forms Experience Builder](aem-forms-ai-assistant-best-practices.md)
- [Documentação do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=pt-BR)

### Escalonamento e suporte

**Quando Entrar em Contato com o Suporte**

- Os problemas persistem após tentar soluções documentadas
- Problemas em todo o sistema que afetam vários usuários
- Questões de segurança ou integridade dos dados
- Problemas de integração que exigem configuração no nível do sistema

**Informações a Serem Fornecidas**

- Descrição detalhada do problema e etapas de reprodução
- Capturas de tela ou gravações de tela do problema
- Informações do navegador e do sistema
- Mensagens de erro e registros do console
- Detalhes de configuração e integração do formulário

**Métodos de contato**

- Administrador do sistema: para problemas de ambiente e acesso
- Suporte técnico: para problemas complexos de integração e configuração
- Programa de Acesso Antecipado: `aem-forms-ea@adobe.com` para problemas específicos do programa

### Comunidade e compartilhamento de conhecimento

**Práticas recomendadas para resolução de problemas**

- Soluções de documentos para referência futura
- Compartilhar abordagens de solução de problemas bem-sucedidas com membros da equipe
- Contribuir com a base de conhecimento organizacional
- Participar de comunidades e fóruns de usuários

**Aprimoramento Contínuo**

- Revisão regular de problemas e soluções comuns
- Atualizar procedimentos de solução de problemas com base em novos achados
- Sessões de treinamento e compartilhamento de conhecimento
- Feedback para a equipe de produtos sobre melhorias de recursos

Este guia de solução de problemas é atualizado continuamente com base nos comentários dos usuários e nos novos recursos do Forms Experience Builder. Para obter as informações mais recentes e os recursos adicionais, consulte a [documentação do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=pt-BR).
