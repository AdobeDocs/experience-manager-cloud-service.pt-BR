---
title: Navegar pela interface do editor universal para o AEM Forms
description: Domine a interface do Editor universal para criar AEM Forms com Edge Delivery Services. Conheça as ferramentas, os atalhos e os fluxos de trabalho essenciais para criar formulários de maneira eficiente com este abrangente guia de interface.
keywords: editor universal, AEM forms, edge delivery services, guia de interface, criação de formulários, editor do WYSIWYG, ferramentas do construtor de formulários, navegação da interface do usuário
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '2390'
ht-degree: 0%

---


# Navegar pela interface do editor universal para o AEM Forms

O [Editor Universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) fornece uma interface visual para criar AEM Forms com Edge Delivery Services. Ele oferece uma experiência do **What You See Is What You Get (WYSIWYG)** que mostra exatamente como seus formulários aparecerão para os usuários.

![Visão Geral da Interface do Editor Universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

Este guia ajuda você a entender a interface para criar formulários com eficiência. Quer você seja novo na criação de formulários ou um desenvolvedor experiente, este guia ajudará a:

**Conheça as habilidades essenciais:**

- Navegue pela interface com confiança e eficiência
- Usar as ferramentas apropriadas para as tarefas comuns de criação de formulários
- Aproveite os atalhos de teclado para aumentar a produtividade
- Solução de problemas comuns de interface

**Fluxos de Trabalho de Chave Mestra:**

- Configure seu espaço de trabalho para obter produtividade ideal
- Criar formulários do conceito à publicação
- Testar e visualizar formulários em vários dispositivos
- Colaborar com membros da equipe em projetos de formulário



## Introdução rapidamente

**Novos usuários:** Comece com as [Ferramentas essenciais](#essential-tools-for-form-building) para conhecer os recursos principais que você usará com mais frequência.

**Usuários experientes:** Use os [Recursos Avançados](#advanced-features-and-integrations) para obter ferramentas e integrações especializadas.

**Referência rápida:** Use as seções [Visão Geral da Interface](#interface-overview) e [Atalhos de Teclado](#keyboard-shortcuts) para pesquisas rápidas.

>[!NOTE]
>
> Novo na criação de formulários? Consulte [Introdução ao Edge Delivery Services para AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) para obter orientação passo a passo sobre a criação de formulários.

## Visão geral da interface

A interface do Editor universal é organizada em quatro áreas principais, cada uma projetada para tarefas específicas:

![Layout da Interface do Editor Universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

| **Área** | **Finalidade** | **Uso principal** |
|----------|-------------|----------------|
| **[A: Cabeçalho Do Experience Cloud](#experience-cloud-header)** | Navegação e gerenciamento de conta | Alternar entre ferramentas do Adobe, acessar ajuda, gerenciar notificações |
| **[B: Barra de Ferramentas do Editor Universal](#universal-editor-toolbar)** | Edição e publicação de formulários | Criar, editar, visualizar e publicar formulários |
| **[C: Painel Propriedades](#properties-panel)** | Configuração do componente | Configurar campos de formulário, gerenciar estrutura de conteúdo, acessar recursos avançados |
| **[D: Tela Do Editor](#editor-canvas)** | Criação visual do formulário | Adicione componentes, organize o layout, consulte visualização em tempo real |

**Fluxo de Interface:** A maioria dos usuários trabalha principalmente na **Tela do Editor** (D) e no **Painel de Propriedades** (C), usando a **Barra de Ferramentas** (B) para ações como visualizar e publicar.

## Ferramentas essenciais para a construção de formulários

Comece aqui se você é novo no Editor universal. Estas são as ferramentas principais que você usará para a maioria das tarefas de criação de formulários:

### **1. Tela do Editor - Seu Workspace principal**

A **Tela do Editor** é onde você constrói visualmente seus formulários. Ele mostra exatamente como o formulário será exibido para os usuários.

![Tela do Editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Ações principais:**

- **Adicionar componentes** clicando no botão **Adicionar** no Painel Propriedades
- **Selecione os elementos** clicando diretamente neles na tela
- **Ver alterações em tempo real** ao configurar componentes
- **Interações de teste** no modo de visualização

### **2. Painel Propriedades - Configurar Seus Componentes**

O **Painel de Propriedades** (lado direito) é onde você personaliza componentes selecionados e gerencia a estrutura do formulário.

![Painel de propriedades](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

**Recursos Essenciais:**

- **Modo de Propriedades** (atalho `d`) - Definir configurações do componente selecionado
- **Árvore de conteúdo** (atalho `f`) - Navegar pela estrutura do formulário
- **Adicionar componentes** (atalho `a`) - Inserir novos campos de formulário
- **Ações de componentes** - Duplicar ou excluir elementos selecionados

### **3. Toolbar Essentials - Visualizar e Publicar**

A **Barra de Ferramentas do Editor Universal** fornece ações-chave para testar e publicar seus formulários.

![Barra de Ferramentas do Editor Universal](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

**Ferramentas Obrigatórias:**

- **Modo de Visualização** (atalho `p`) - Teste o formulário como os usuários o verão
- **Modo responsivo** - Verifique a aparência do formulário em dispositivos móveis
- **Abrir página** (atalho `o`) - Exibir formulário em uma nova guia
- **Publicar** - Tornar o formulário disponível para os usuários

### **4. Fluxo de Trabalho de Início Rápido**

**Para o primeiro formulário:**

1. **Adicionar um componente de Formulário Adaptável** - Inserir o componente `Adaptive Form` em uma seção.
2. **Iniciar criação** - Adicionar componentes usando o botão **Adicionar** (`a`)
3. **Configurar campos** - Selecionar componentes e usar o **Modo de Propriedades** (`d`)
4. **Testar o formulário** - Use o **Modo de Visualização** (`p`) para interagir com o formulário
5. **Verificar exibição móvel** - Alternar para **Modo Responsivo** para teste móvel
6. **Ativar** - Clique em **Publicar** quando estiver pronto

>[!NOTE]
>
> Para saber as etapas detalhadas para criar formulários no Universal Editor, consulte [Criar e Publicar Forms Adaptável com Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md).

**Pontos de Verificação de Validação:**

- É possível adicionar e configurar campos de formulário?
- O modo de visualização funciona corretamente?
- Todos os campos obrigatórios estão configurados corretamente?
- O formulário é exibido bem em dispositivos móveis?

## Cabeçalho Experience Cloud

O **Cabeçalho do Experience Cloud** fornece ferramentas de navegação e gerenciamento de conta. A maioria dos construtores de formulários o usa ocasionalmente para alternar entre as ferramentas do Adobe ou acessar a ajuda.

![Cabeçalho do Experience Cloud](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

**Elementos-chave:**

| **Elemento** | **Finalidade** | **Quando usar** |
|-------------|-------------|----------------|
| **Adobe Experience Cloud** | Navegar até outras ferramentas do Adobe | Alternância entre Sites, Assets, Forms |
| **Organização** | Alternar entre organizações | Cenários de acesso de várias organizações |
| **Ajuda** | Acessar a documentação e o suporte | Quando precisar de orientação ou quiser enviar feedback |
| **Notificações** | Exibir tarefas atribuídas e alertas | Verificação do status do fluxo de trabalho |
| **Soluções** | Acesso rápido a outras soluções da Adobe | Transferência entre diferentes produtos da Adobe |
| **Perfil de usuário** | Configurações da conta e saída | Gerenciamento de conta ou alternância de usuários |

**Usos Mais Comuns:**

- **Obtendo Ajuda** - Clique no ícone Ajuda para obter documentação e suporte
- **Alternando Organizações** - Use a lista suspensa Organização se você tiver acesso para várias organizações

## Barra de ferramentas do editor universal

A **Barra de Ferramentas do Editor Universal** contém suas ferramentas primárias de edição e publicação de formulários. Elas são organizadas por frequência de uso e fluxo de trabalho típico.

![Barra de Ferramentas do Editor Universal](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

### **Ferramentas de Fluxo de Trabalho Diário**

**Estas ferramentas são usadas na maioria das sessões de criação de formulários:**

#### **Modo de Visualização** (atalho `p`)

**Finalidade:** testar seu formulário exatamente como os usuários irão experimentá-lo\
**Quando usar:** Antes de publicar, depois de fazer alterações, para testar a funcionalidade do formulário

![Modo de visualização](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

**Prática recomendada:** visualizar após cada grande alteração para capturar problemas antecipadamente.

#### **Modo responsivo**

**Finalidade:** Verifique como o formulário é exibido em dispositivos móveis\
**Quando usar:** Após criar o formulário, antes de publicar

![Modo responsivo](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

**Prática recomendada:** Sempre testar a exibição móvel - muitos usuários acessarão formulários em telefones.

#### **Abrir página** (`o` atalho)

**Propósito:** Exibir seu formulário em uma nova guia sem a interface do editor\
**Quando usar:** Para testes em tela inteira, compartilhar com as partes interessadas para revisão

![Abrir página](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

#### **Publicar**

**Finalidade:** Tornar o formulário ativo e acessível aos usuários\
**Quando usar:** Após testes completos nos modos Visualização e Responsivo

![Publicar](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

**Lista de Verificação de Validação Antes da Publicação:**

- Formulário testado no modo de visualização
- Capacidade de resposta remota verificada
- Todos os campos obrigatórios configurados
- As ações enviar estão funcionando corretamente

### **Ferramentas de Navegação**

#### **Botão da Página Inicial**

**Finalidade:** retornar à página inicial do Editor Universal\
**Quando usar:** Iniciando o trabalho em um formulário diferente

![Botão da Página Inicial](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

#### **Barra de Localização** (`l` atalho)

**Propósito:** Navegar diretamente para qualquer formulário por URL\
**Quando usar:** alternar rapidamente entre formulários específicos

![Barra de Localização](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

### **Ferramentas de Configuração Avançada**

**Estas ferramentas são usadas para cenários específicos ou configurações avançadas:**

#### **Propriedades do Formulário AEM**

**Propósito:** definir configurações no nível do formulário, como o Modelo de Dados de Formulário (FDM), configurar ações de envio e datas de publicação\
**Quando usar:** Configuração de integrações de dados, agendamento de publicação

![Propriedades do formulário](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

![Assistente de Propriedades do Formulário](/help/edge/docs/forms/universal-editor/assets/form-properties-ue.png)

O painel Propriedades do formulário inclui as seguintes seções:

- **Envio**: defina o que acontece depois que um usuário envia o formulário. Escolha entre várias ações de envio, como enviar dados por email, enviar para o SharePoint, usar um modelo de dados de formulário ou integrar a serviços como o Adobe Experience Platform ou o Microsoft Power Automate. Para obter uma lista completa das ações de envio suportadas, consulte o artigo [Ação de envio](/help/edge/docs/forms/universal-editor/submit-action.md).

- **Preenchimento prévio**: configure como os campos de formulário são preenchidos automaticamente antes que o usuário interaja com o formulário. Você pode se conectar a fontes de dados, como um Modelo de dados de formulário (FDM), ou usar parâmetros de URL para preencher campos previamente, aprimorando a experiência do usuário e reduzindo a entrada manual. Para saber mais, consulte o artigo [Serviço de preenchimento prévio](/help/edge/docs/forms/universal-editor/prefill-form.md).

- **Obrigado**: personalize o que os usuários verão depois de enviar o formulário. Você pode exibir uma mensagem de confirmação ou redirecioná-la para outra página da Web, garantindo uma experiência de conclusão perfeita e profissional. Para saber como configurar uma mensagem de agradecimento para formulários, consulte o artigo [Configurar Mensagem de Agradecimento](/help/edge/docs/forms/universal-editor/configure-thankyou-message.md).

#### **Editor de regras** (acesso antecipado)

**Propósito:** adicionar comportamentos dinâmicos, validações e lógica condicional\
**Quando usar:** Criar formulários interativos com lógica de negócios complexa

![Editor de regras](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

>[!IMPORTANT]
>
> **Recurso de Acesso Antecipado:** o Editor de Regras requer acesso especial. Contate [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para habilitar este recurso.
>
> **Saiba Mais:** Consulte o [Guia do Editor de Regras](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) para obter instruções detalhadas.

#### **Configurações do Cabeçalho de Autenticação**

**Propósito:** definir cabeçalhos de autenticação personalizados para teste de desenvolvimento\
**Quando usar:** Desenvolvimento local com formulários de autenticação obrigatória

![Cabeçalhos de autenticação](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

#### **Opções Adicionais** (Menu Reticências)

**Propósito:** Acessar ações menos comuns, como desfazer a publicação\
**Quando usar:** Colocando formulários offline, acessando opções avançadas

![Opções adicionais](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

## Painel Propriedades

O **Painel de Propriedades** (lado direito) é o seu centro de controle para criar e configurar formulários. Ele muda com base no que você seleciona e fornece ferramentas diferentes para tarefas diferentes.

![Painel de propriedades](/help/edge/docs/forms/universal-editor/assets/text-properties-ue.png)

### **Ferramentas de Criação de Formulários Principais**

**Estas ferramentas são essenciais para criar e organizar seus formulários:**

#### **Adicionar Componentes** (atalho `a`)

**Propósito:** inserir novos campos e elementos de formulário\
**Como funciona:** Mostra os componentes disponíveis para o contêiner selecionado

![Adicionar componentes](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

**Componentes comuns:**

- Entrada de texto, email, campos de telefone
- Lista suspensa, Botões de opção, Caixas de seleção
- Upload de arquivo, Seletor de data
- Painéis e seções para organização

#### **Modo de Propriedades** (`d` atalho)

**Propósito:** definir configurações para os componentes selecionados\
**Quando usar:** Depois de adicionar qualquer componente para personalizar seu comportamento

![Modo de Propriedades](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

**Configurações de Chave:**

- Rótulos de campo e texto de espaço reservado
- Regras de validação (obrigatório, formato, comprimento)
- Valores padrão e texto de ajuda
- Regras de visibilidade condicional

#### **Árvore de conteúdo** (`f` atalho)

**Propósito:** Navegar e organizar sua estrutura de formulário\
**Quando usar:** formulários complexos com várias seções, localizando componentes específicos

![Árvore de conteúdo](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

**Vantagens:**

- Navegação rápida para qualquer componente
- Hierarquia do formulário visual
- Fácil reorganização dos elementos

#### **Ações do componente**

**Propósito:** Gerenciar componentes existentes\
**Ações disponíveis:**

- **Duplicar** - Copiar componentes rapidamente ![Duplicar](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)
- **Excluir** - Remover componentes (sem prompt de confirmação) ![Excluir](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### **Integrações e recursos avançados**

**Estas ferramentas habilitam funcionalidade de formulário sofisticada:**

+++Integração de dados

#### **Source de dados**

**Finalidade:** conectar formulários a sistemas de dados de back-end\
**Quando usar:** Forms que precisam ler/gravar em bancos de dados ou serviços externos

![Source de dados](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

**Recursos:**

- Configuração do modelo de dados de formulário (FDM)
- População de dados dinâmicos
- Envio a sistemas externos

+++

+++Ferramentas alimentadas por IA

#### **Gerar variações**

**Finalidade:** usar a IA para criar diferentes versões do conteúdo do formulário\
**Quando usar:** Experimentar com texto, layouts ou abordagens diferentes

    ![Gerar variações](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

**Saiba Mais:** [Gerar Guia De Variações](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

#### **Rascunhos de Conteúdo**

**Finalidade:** criar e salvar versões de texto preliminares\
**Quando usar:** Iterando na cópia do formulário, salvando opções de texto alternativo

![Rascunhos de Conteúdo](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

+++

+++Teste e otimização

#### **Teste A/B**

**Propósito:** Comparar variações de formulário para otimizar o desempenho\
**Quando usar:** Otimizando as taxas de conversão, testando designs diferentes

![Teste A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

#### **Experimentação**

**Propósito:** executar testes controlados em designs de formulário\
**Quando usar:** otimização de formulário orientado por dados, teste de experiência do usuário

    ![Experimentação](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

+++

+++Ferramentas do Collaboration

#### **Gerenciamento de tarefas**

**Propósito:** organizar o fluxo de trabalho de equipe para projetos de formulário\
**Quando usar:** desenvolvimento de formulário multipessoa, rastreamento de projetos

![Gerenciamento de tarefas](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

#### **Personalização**

**Propósito:** conectar-se com a Adobe Experience Platform para obter experiências personalizadas\
**Quando usar:** Criar formulários personalizados com base nos dados do usuário

    ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

+++

## Tela do editor

A **Tela do Editor** é o seu espaço de trabalho principal onde você cria visualmente formulários. Ele mostra exatamente como o formulário será exibido para os usuários e fornece feedback em tempo real conforme você faz alterações.

![Tela do Editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Principais Recursos:**

- **edição de WYSIWYG** - Ver as alterações imediatamente à medida que forem feitas
- **Interação direta** - Clique em qualquer componente para selecioná-lo e editá-lo
- **Visualização em tempo real** - Alternar para o modo de visualização para testar a funcionalidade
- **Exibição responsiva** - Alternar exibições do dispositivo para verificar a compatibilidade móvel

**Práticas recomendadas:**

- **Iniciar com estrutura** - Adicionar seções principais antes de componentes detalhados
- **Testar com frequência** - Use o Modo de visualização regularmente para detectar problemas antecipadamente
- **Think mobile-first** - Verificar Modo Responsivo durante todo o processo de design

## Atalhos de teclado

Domine esses atalhos para criar formulários com mais rapidez e eficiência:

| **Atalho** | **Ação** | **Quando usar** |
|--------------|------------|----------------|
| `a` | Abrir lista de componentes | Adição de novos campos de formulário |
| `d` | Abrir propriedades do componente | Configuração dos elementos selecionados |
| `f` | Alternar árvore de conteúdo | Navegação em formulários complexos |
| `p` | Alternar modo de visualização | Teste da funcionalidade do formulário |
| `o` | Abrir formulário em nova guia | Teste de tela cheia |
| `l` | Barra de localização de foco | Alternar para diferentes formulários |

**Dica Profissional:** Use estes atalhos em combinação; por exemplo, selecione um componente, pressione `d` para configurá-lo e `p` para testar as alterações.

## Fluxos de trabalho comuns

### **Criando Seu Primeiro Formulário**

1. **Adicionar estrutura** - Use `a` para adicionar um Painel para seções de formulário
2. **Adicionar campos** - Inserir Entrada de Texto, Email e outros componentes
3. **Configurar propriedades** - Selecione cada campo e pressione `d` para definir rótulos e validação
4. **Testar funcionalidade** - Pressione `p` para visualizar e testar o formulário
5. **Verificar exibição móvel** - Use o Modo Responsivo para verificar a exibição móvel
6. **Publicar** - Clique em Publicar quando estiver pronto para entrar no ar

### **Editando Forms Existente**

1. **Navegar pela estrutura** - Use a Árvore de Conteúdo (`f`) para localizar componentes rapidamente
2. **Selecionar e modificar** - Clique diretamente nos componentes ou use a Árvore de Conteúdo
3. **Testar alterações** - Visualizar (`p`) após cada alteração significativa
4. **Validar fluxo de trabalho** - Testar o fluxo de formulários completo antes de republicar

### **Colaborando com Equipes**

1. **Usar Gerenciamento de Tarefas** - Atribuir seções de formulário específicas aos membros da equipe
2. **Compartilhar para revisão** - Use Abrir Página (`o`) para compartilhar visualizações limpas
3. **Testar juntos** - Use o Modo de Visualização para sessões de teste colaborativo
4. **Rastrear progresso** - Verificar notificações de atualizações de tarefa

## Solução de problemas comuns

### **Problemas de interface**

+++Elementos de interface não carregam

**Problema:** os botões da barra de ferramentas, o Painel de Propriedades ou outros elementos da interface não aparecem

**Soluções:**

- **Atualizar a página** - Uma simples atualização do navegador frequentemente resolve problemas de carregamento
- **Verificar compatibilidade do navegador** - Use Chrome, Firefox ou Safari
- **Limpar cache do navegador** - Remover arquivos em cache que possam estar desatualizados
- **Verificar permissões** - Verifique se você tem acesso adequado para editar formulários

+++

+++Componentes não respondem

**Problema:** Não é possível selecionar componentes ou o Painel Propriedades não é atualizado

**Soluções:**

- **Clique diretamente nos componentes** - Evite clicar em áreas vazias
- **Usar árvore de conteúdo** - Pressione `f` e selecione componentes da árvore
- **Verificar elementos sobrepostos** - Alguns componentes podem estar bloqueando outros
- **Recarregar o formulário** - Use a Barra de Localização (`l`) para recarregar o formulário atual

+++

+++Problemas do modo de visualização

**Problema:** o Modo de Visualização não funciona corretamente ou mostra erros

**Soluções:**

- **Verificar validação de formulário** - Garantir que todos os campos obrigatórios estejam configurados corretamente
- **Testar primeiro no Modo de Edição** - Verifique se os componentes funcionam antes de visualizar
- **Limpar cache do navegador** - Os scripts em cache podem interferir na visualização
- **Verifique a configuração do componente** - Verifique se há erros nas configurações do Modo de Propriedades

+++

## Práticas recomendadas para a construção eficiente de formulários

### **Dicas da Organização**

- **Usar nomes descritivos** - Componentes de rótulo claramente no Modo de Propriedades
- **Agrupar campos relacionados** - Use Painéis para organizar seções de formulário logicamente
- **Planejar antes de compilar** - Faça um esboço da estrutura do formulário antes de iniciar
- **Mantenha a simplicidade** - Evite sobrecarregar os usuários com muitos campos

### **Experiência do usuário**

- **Testar com frequência** - Usar Modo de Visualização após cada alteração importante
- **Pense como usuários** - Considere a experiência completa de preenchimento de formulário
- **Fornecer rótulos claros** - Tornar as finalidades de campo óbvias para os usuários
- **Adicionar texto útil** - Use texto de ajuda para campos complexos

### **Otimização do desempenho**

- **Minimizar componentes** - Use apenas os campos de formulário necessários
- **Otimizar imagens** - Compactar todas as imagens usadas em formulários
- **Testar em dispositivo móvel** - Garantir bom desempenho em conexões móveis mais lentas
- **Validar com antecedência** - Configurar a validação adequada para evitar erros de envio

## Próximas etapas

Agora que você entende a interface do Editor universal:

1. **Pratique com um formulário simples** - Comece com campos básicos para se familiarizar
2. **Explore recursos avançados** - Experimente ferramentas e integrações alimentadas por IA quando estiver pronto
3. **Saiba mais sobre criação de formulários** - Consulte o [Guia de Introdução](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
4. **Editor de regras mestres** - Adicionar comportamentos dinâmicos com o [Guia do Editor de Regras](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)

**Lembre-se:** o Editor Universal foi criado para tornar a criação de formulários intuitiva. Comece com o básico e explore gradualmente os recursos avançados à medida que suas necessidades aumentam.
