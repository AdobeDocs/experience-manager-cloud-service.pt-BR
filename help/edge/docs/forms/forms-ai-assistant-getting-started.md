---
title: Introdução ao Forms Experience Builder
description: Saiba como usar o Forms Experience Builder para criar e gerenciar formulários com divulgação progressiva para todos os tipos de usuários
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2013'
ht-degree: 0%

---


# Introdução ao Forms Experience Builder

>[!NOTE]
>
> O recurso Forms Experience Builder está disponível no **programa de acesso antecipado (EA)**. Se estiver interessado, envie um email rápido do seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso ao recurso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta documentação está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os recursos, comandos e exemplos podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa Acesso antecipado.

Este guia abrangente ajuda você a começar a criar e gerenciar formulários usando a tecnologia de IA de conversação. Seja você um iniciante procurando criar seu primeiro formulário ou um usuário avançado procurando aproveitar recursos sofisticados, você encontrará informações detalhadas e exemplos práticos para orientar sua jornada pelos recursos do Forms Experience Builder.

## Pré-requisitos e configuração

### &#x200B;1. Solicitar acesso

O Forms Experience Builder está disponível no momento como parte do programa de Acesso antecipado (EA). Para participar e obter acesso, você precisará das seguintes informações:

**Informações necessárias**

- **IMS Organization ID**: o identificador da sua organização da Adobe
- **ID do programa**: o identificador específico de seu programa no Adobe Experience Cloud
- **Detalhes do projeto**: linha do tempo, escopo e casos de uso pretendidos
- **Email Comercial Oficial**: associado à conta da Adobe da sua organização

**Como obter a ID da organização IMS e a ID do programa**

Para obter etapas detalhadas para localizar sua IMS Organization ID e ID do Programa, consulte:

- [Guia de configuração da organização da Adobe Experience Cloud](/help/onboarding/cloud-manager-introduction.md)
- [Gerenciamento de Programa e Ambiente](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

**Solicitar Acesso**

1. Obtenha a ID da organização IMS e a ID do programa usando os guias acima
2. Enviar um email para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) solicitando acesso
3. Inclua em sua solicitação:
   - Nome da organização e IMS Organization ID
   - ID do programa
   - Cronograma e escopo do projeto
   - Casos de uso pretendidos e objetivos de negócios

>[!IMPORTANT]
>
> **Programa de Disponibilidade Limitada**: o acesso ao Forms Experience Builder está sujeito à aprovação dos participantes internos. A Adobe analisará sua solicitação com base na capacidade do programa e no alinhamento com os critérios de acesso antecipado. A aprovação não é garantida e depende da disponibilidade atual do programa.

### &#x200B;2. Verifique se o Forms está ativado

Antes de usar o Forms Experience Builder, verifique se o [AEM Forms está habilitado para o seu ambiente](/help/forms/setup-forms-cloud-service.md).


### &#x200B;3. Configurar o ambiente


- **Para Edge Delivery Services (EDS):**

   - [Configurar ambiente para o Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
   - [Criar um novo formulário usando o modelo do Edge Delivery Forms](/help/edge/docs/forms/universal-editor/create-forms.md)

- **Para formulários baseados em Componentes Principais:**

   - Na sua instância do Adobe Experience Manager, acessei Forms > Forms e Documentos
   - [Criar uma nova página usando o modelo dos Componentes principais](/help/forms/creating-adaptive-form-core-components.md)


## Início rápido

### Acessar o Forms Experience Builder

O Forms Experience Builder está disponível na interface do usuário do Forms Management, no Editor universal e no Editor Forms adaptável. Você pode usar qualquer um destes métodos para acessar o formulário:

**Interface do usuário do Forms Management (para Componentes Principais)**

1. **Navegue até o Forms**: Vá até AEM > Forms > Forms e Documentos
1. Clique no ícone do Forms Experience Builder na barra de ferramentas. Está próximo ao canto superior esquerdo da interface do usuário.
   ![Ícone do Assistente de IA*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}
1. Comece a criação do seu formulário de conversação


**Editor Forms adaptável (para Componentes Principais)**

1. Acesse AEM > Forms > Forms e documentos
2. [Criar um novo formulário usando o modelo dos Componentes principais](/help/forms/creating-adaptive-form-core-components.md)
3. Abra o formulário para edição
4. Clique no ícone do Forms Experience Builder na barra de ferramentas do editor
   ![Ícone do Assistente de IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

5. Comece a criação do seu formulário de conversação


**Editor Universal (para Forms do Edge Delivery Services)**

1. Siga o [guia de configuração do Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) para criar sua página de EDS
1. Navegue até a página de EDS no Editor universal
1. Procure o ícone Forms Experience Builder no painel direito
1. Clique para abrir a interface conversacional



### Seu primeiro formulário

| Exemplo de conversa |   |
|--------------------------------------------------------------------------------------------------------------------------------------------|---|
| **Tente esta conversa para criar um formulário de contato abrangente (com base na demonstração do Summit):**<br><br>**Você:** &quot;Crie um formulário de contato para capturar informações pessoais, incluindo nome completo, endereço de email, número de telefone, nome da empresa, cargo e um campo de mensagem para consultas&quot;<br><br>**IA:** Selecione um modelo<br>    Uma lista suspensa para selecionar um modelo <br><br>**IA:** Selecione um tema<br>    Uma lista suspensa para selecionar um tema <br><br>**IA:** Criar formulário | ![Seu Primeiro Formulário](/help/edge/docs/forms/assets/create-form.png) |
| <br>**IA:** Abrir formulário criado | </br> O formulário é criado e aberto no editor |


### Comandos Essenciais

| Símbolo | Propósito | Exemplo de uso |
|--------|---------|---------------|
| `/` | Ações rápidas e atalhos | `/create-form contact form`, `/help validation rules`, `/update-layout wizard` |
| `@` | Fazer referência a campos de formulário existentes | `@email`, `@firstName`, `Make @phoneNumber required` |
| Texto sem formatação | Conversação natural | &quot;Adicionar um campo de número de telefone obrigatório&quot;, &quot;Criar validação para email&quot; |

**Exemplos de Comandos Específicos:**

- `/create-form customer survey` - Cria um novo formulário de pesquisa de cliente
- `/add-field @email validation` - Adiciona validação ao campo de email existente
- `/create-rule show @spouse if @maritalStatus equals married` - Cria uma lógica condicional
- `/configure-submit to email support@company.com` - Configura o envio de email
- `/help multi-step forms` - Obtém ajuda sobre a criação de formulário em várias etapas

### Dicas para se dar bem

- **Seja específico**: &quot;Adicionar um campo de email necessário com validação&quot; funciona melhor do que &quot;adicionar email&quot;
- **Fazer referência a campos existentes**: usar `@fieldName` ao modificar formulários
- **Solicitar ajuda**: Digite `/help` seguido da sua pergunta
- **Iterar**: fazer uma alteração de cada vez para obter melhores resultados


## Maneiras de começar a criar um Formulário

### &#x200B;1. Comece com prompts de linguagem natural

Descreva os requisitos de formulário em linguagem natural, e o Forms Experience Builder gera a estrutura completa do formulário:

**Exemplos:**

- &quot;Crie um formulário de solicitação de empréstimo com informações pessoais, detalhes financeiros e uploads de documentos&quot;
- &quot;Crie um formulário de feedback do cliente com classificações, comentários e categorias do produto&quot;
- &quot;Preciso de um formulário de inscrição em várias etapas para uma conferência com processamento de pagamento&quot;

### &#x200B;2. Importar e converter

Transforme formulários e documentos existentes em experiências modernas e interativas:

**Fontes com Suporte:**

- **PDF forms**: carregue PDFs estáticos para convertê-los em formulários digitais interativos com validações.
- **Capturas de tela ou Imagens**: carregue fotos de formulários em papel para gerar versões digitais funcionais
- **XFA Forms**: converter formulários herdados baseados em XFA em formulários responsivos modernos

**Como importar:**

1. Clique no ícone de anexo na interface do Forms Experience Builder
2. Faça upload do seu arquivo (PDF, imagem, design de imagem etc.)
3. Descreva suas necessidades:
   - &quot;Converter este formulário do PDF em uma versão digital&quot;
   - &quot;Criar um formulário correspondente a este layout de captura de tela&quot;
   - &quot;Criar este formulário a partir do meu design do Figma&quot;

**Tipos de Arquivos com Suporte:**

- **Imagens** (PNG, JPG, GIF): layouts de formulário, modelos de interface do usuário, formulários digitalizados, rascunhos à mão
- **Arquivos PDF**: formulários, especificações, documentos, Acroforms, formulários XFA existentes
- **Capturas de tela**: capturas de tela de aplicativos móveis/da área de trabalho, fotos de formulários em papel, rascunhos de quadro de comunicações
- **Rascunhos desenhados à mão**: Rascunhos de guardanapo, wireframes, desenhos conceituais (fotografados)

### Interações principais

#### Adição de elementos de formulário

**Adições básicas:**

    👤 Você: &quot;Adicionar uma seção para informações pessoais&quot;
    👤 Você: &quot;Incluir um carregamento de arquivo para retomada&quot;
    👤 Você: &quot;Adicionar uma lista suspensa para seleção de país&quot;

**Especificações detalhadas:**

    👤 Você: &quot;Adicionar um painel de informações pessoais com campos para nome completo, data de nascimento, número de telefone e endereço de email&quot;
    👤 Você: &quot;Incluir um componente de carregamento de arquivo seguro para documentos, limitado a arquivos PDF com menos de 5 MB&quot;
    👤 Você: &quot;Adicionar uma lista suspensa de país com opções para EUA, Canadá, Reino Unido e Alemanha&quot;

#### Criar comportamento dinâmico

**Lógica simples:**

    👤 Você: &quot;Mostrar campos adicionais quando &#39;Outro&#39; for selecionado&quot;
    🤖 IA: &quot;Criou uma regra condicional que mostra campos adicionais quando &#39;Outro&#39; for escolhido&quot;
    
    👤 Você: &quot;Tornar o campo de email necessário&quot;
    🤖 IA: &quot;Atualizou o campo de email a ser exigido com validação&quot;
    
    👤 Você: &quot;Calcular o total automaticamente&quot;
    🤖 IA: &quot;Adicionou lógica de cálculo para calcular totais automaticamente&quot;

**Regras de negócio complexas:**

    👤 Você: &quot;Mostrar os campos de informações do cônjuge somente quando o estado civil estiver definido como &#39;Casado&#39;&quot;
    🤖 IA: &quot;Criou uma regra condicional que exibe os campos do cônjuge com base no estado civil&quot;
    
    👤 Você: &quot;Calcular o custo total multiplicando quantidade e preço e adicionar imposto de 10%&quot;
    🤖 IA: &quot;Adição da lógica de cálculo com cálculo de quantidade, preço e imposto&quot;
    
    👤 Você: &quot;Habilitar o botão Enviar somente quando todos os campos obrigatórios estiverem concluídos e os termos forem aceitos&quot;
    🤖 IA: &quot;Lógica de validação criada que habilita o envio somente quando todas as condições forem atendidas&quot;

#### Layout e design do formulário

**Alterações de layout:**

    👤 Você: &quot;Transformar em formulário de várias etapas&quot;
    🤖 AI: &quot;Converter formulário em layout progressivo com navegação&quot;
    
    👤 Você: &quot;Organizar campos em duas colunas&quot;
    🤖 AI: &quot;Atualizar o layout para exibir campos em uma organização de duas colunas&quot;
    
    👤 Você: &quot;Converter em layout de acordeão&quot;
    🤖 AI: &quot;Transformar o formulário para usar seções de estilo acordeão&quot;

**Melhorias de design:**

    👤 Você: &quot;Criar um formulário de estilo assistente com 3 etapas: informações pessoais, preferências e revisão&quot;
    🤖 IA: &quot;Criar um formulário de assistente com três etapas e navegação distintas&quot;
    
    👤 Você: &quot;Organizar os campos de endereço em um layout compacto de duas colunas&quot;
    🤖 IA: &quot;Organizar campos de endereço em um formato compacto de duas colunas&quot;
    
    👤 Você: &quot;Atualizar o layout para corresponder ao wireframe anexado&quot;
    🤖 IA: &quot;Modificar o layout para corresponder à referência de design fornecida&quot;

### Enviar configuração

O Forms Experience Builder pode configurar vários endpoints de envio para conectar seus formulários a sistemas e serviços externos:

| Enviar Tipo de Ação | Comando de configuração | Caso de uso |
|------------------|---------------|----------|
| **Email** | &quot;Enviar formulário para email&quot; | Notificações e confirmações para envios de formulários |
| **REST API** | &quot;Enviar para endpoint REST&quot; | Aplicativos personalizados e sistemas de terceiros |
| **Armazenamento na nuvem** | &quot;Salvar no Azure/SharePoint&quot; | Armazenamento de documentos e gerenciamento de arquivos |
| **Fluxo de trabalho** | &quot;Conexão com o Power Automate&quot; | Automação e aprovações de processos de negócios |
| **Marketing** | &quot;Integrar ao Marketo&quot; | Gerenciamento de clientes potenciais e automação de marketing |

**Exemplos avançados de configuração de envio:**

    👤 Você: &quot;Enviar envios de formulários para hr@company.com e criar um caso em nosso sistema CRM&quot;
    🤖 IA: &quot;Envio de email configurado e ação de envio do CRM&quot;
    
    👤 Você: &quot;Enviar dados para nosso ponto de extremidade da API REST e acionar o novo fluxo de trabalho do cliente&quot;
    🤖 IA: &quot;Configurar o envio da API REST com acionadores de fluxo de trabalho&quot;
    
    👤 Você: &quot;Enviar respostas por email para a equipe de vendas e adicionar o cliente potencial à nossa plataforma de automação de marketing&quot;
    🤖 IA: &quot;Envio multicanal configurado com automação de email e marketing&quot;





## Operações avançadas de formulários


### Criação de regra complexa

Crie validação sofisticada e lógica de negócios que responda às interações do usuário e garanta a integridade dos dados:

    👤 Você: &quot;Mostrar a seção de endereço somente se o usuário selecionar &#39;Enviar para um endereço diferente&#39;&quot;
    🤖 IA: &quot;Criou uma regra condicional que mostra/oculta o painel de endereços com base na seleção da caixa de seleção&quot;

### Criação de formulário de várias etapas

    👤 Você: &quot;Criar um formulário progressivo com 3 etapas: informações pessoais, preferências, confirmação&quot;
    🤖 IA: &quot;Criado um formulário progressivo com navegação entre etapas e validação em cada estágio&quot;

### Tipos de campo avançados

- Upload de arquivo com restrições de validação e tamanho para gerenciamento de documentos
- Seletores de data com restrições e regras de negócios para agendamento
- Menus suspensos com opções dinâmicas que mudam com base nas seleções do usuário
- Botões de opção com lógica condicional para árvores de decisão complexas


### Conversão do PDF em formulário

    👤 Você: &quot;Converter este PDF em um formulário interativo&quot;
    🤖 IA: &quot;Analisou o PDF e criou um formulário com tipos de campo e validação apropriados&quot;





## Ajuda e aprendizado do produto

O Forms Experience Builder também pode ensiná-lo sobre os recursos do AEM Forms:

### Faça Perguntas Como:

- &quot;Como criar um formulário de várias etapas?&quot;
- &quot;Qual é a diferença entre painéis e seções?&quot;
- &quot;Como configurar notificações por email?&quot;
- &quot;Quais são as práticas recomendadas para formulários móveis?&quot;
- &quot;Como aplicar temas às minhas formas?&quot;

### Obter Ajuda Sobre:

- Conceitos e terminologia do AEM Forms
- Instruções passo a passo para recursos complexos
- Práticas recomendadas
- Solução de problemas comuns

## Práticas recomendadas

### Design do formulário

- **Mantenha a simplicidade**: comece com campos essenciais e adicione complexidade somente quando necessário para evitar sobrecarga de usuários
- **Usar rótulos claros**: torne as finalidades de campo óbvias com rótulos descritivos que orientam os usuários pelo formulário
- **Fornecer texto de ajuda**: orientar os usuários sobre campos complexos com ajuda contextual e exemplos
- **Teste completamente**: valide todos os caminhos de usuário para garantir que os formulários funcionem corretamente em todos os cenários

### Experiência do usuário

- **Divulgação progressiva**: mostra campos relevantes com base no contexto para reduzir a carga cognitiva e melhorar as taxas de conclusão
- **Limpar navegação**: ajude os usuários a entenderem onde eles estão no formulário e quais etapas permanecem
- **Design responsivo**: garanta que os formulários funcionem em todos os dispositivos e tamanhos de tela para acessibilidade máxima
- **Acessibilidade**: siga as diretrizes da WCAG para tornar os formulários utilizáveis por pessoas com deficiência

### Desempenho

- **Otimizar contagem de campos**: solicite apenas as informações necessárias para reduzir o abandono de formulário e melhorar as taxas de conclusão
- **Usar validação apropriada**: evite erros antes do envio para fornecer feedback e orientação imediatos
- **Taxas de conclusão de teste**: monitorar e melhorar a eficácia do formulário por meio de análises e comentários de usuários
- **Atualizações regulares**: mantenha os formulários atualizados com as necessidades dos negócios e as expectativas dos usuários para um desempenho ideal

### Consistência da marca

- **Criar modelos de marca**: prepare modelos de formulários com marcas com as cores, fontes e estilos de sua organização antes de iniciar a criação do formulário
- **Definir padrões de estilo**: estabelecer estilos de botão, layouts de campo e diretrizes de espaçamento consistentes que possam ser referenciados em prompts
- **Usar ativos da marca**: prepare logotipos, códigos de cores e diretrizes de marca para facilitar a referência ao criar formulários
- **Biblioteca de modelos**: crie uma coleção de modelos de formulário com marca para casos de uso comuns (contato, registro, feedback)
- **Prompts de estilo**: inclua instruções específicas da marca: &quot;Use azul da empresa (#1234AB) para botões e fontes corporativas Helvetica&quot;



## Resolução de problemas

| Problema | Correção rápida |
|-------|-----------|
| **Interface não carregando** | Atualize o navegador, verifique a conexão com a Internet |
| **Comandos não funcionando** | Experimente `/help` ou use uma linguagem natural |
| **@fieldName não reconhecido** | Verifique a ortografia, certifique-se de que o campo existe primeiro |
| **Falha ao carregar o arquivo** | Usar PDF/JPG/PNG com menos de 10 MB |
| **Aparência incorreta do formulário** | Seja mais específico: &quot;Torná-lo compatível com dispositivos móveis&quot; |
| **Falha ao enviar configuração** | Verificar credenciais e permissões de API |

**Ainda precisa de ajuda?** Digite `/help` seguido da pergunta específica ou contate o administrador do sistema.

Para obter suporte adicional, consulte a [Biblioteca de Prompts do Forms Experience Builder](ai-assistant-prompt-library.md) principal ou entre em contato com o administrador do sistema para obter assistência técnica.
