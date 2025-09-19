---
title: Importação e conversão inteligentes
description: Saiba como transformar documentos, PDFs e imagens existentes em formulários digitais interativos usando os recursos inteligentes de importação e conversão do Forms Experience Builder.
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---


# Importação e conversão inteligentes

>[!NOTE]
>
> O Forms Experience Builder está disponível em um programa de acesso antecipado. Antes de começar, verifique se você solicitou e recebeu acesso.

O recurso de importação e conversão inteligente do Forms Experience Builder permite transformar documentos, PDFs e imagens existentes em formulários digitais modernos e interativos usando análise e conversão alimentadas por IA.

## Formatos de origem compatíveis

### Documentos do PDF

**PDFs AcroForm:**

- PDF forms interativo com campos de formulário
- PDFs estáticos com layouts semelhantes a formulários
- Documentos de várias páginas com conteúdo estruturado

**PDFs baseados em XFA:**

- Formulários herdados XFA (XML Forms Architecture)
- Formulários empresariais complexos com layouts avançados
- Formulários do governo e de empresas

**PDFs estáticos:**

- Documentos e formulários digitalizados
- Formulários prontos para impressão sem elementos interativos
- Documentos com estruturas semelhantes a formulários

### Arquivos de imagem

**Formatos com suporte:**

- PNG, JPG, JPEG, GIF
- Digitalizações de alta resolução de formulários em papel
- Capturas de tela de formulários digitais
- Desenhos à mão e esboços em arames

**Requisitos de qualidade de imagem:**

- Mínimo de 300 DPI para reconhecimento de texto
- Texto e elementos de formulário claros e legíveis
- Bom contraste entre texto e plano de fundo
- Orientação adequada (não girada)

### Arquivos de design

**Designs de figuras:**

- Modelos de formulários e protótipos
- Arquivos de design de UI/UX
- Layouts de formulário baseados em componente

**Outros formatos de design:**

- Arquivos do Adobe XD
- Desenhos do esboço
- Documentos em wireframe

## Como importar e converter

### Etapa 1: acessar o recurso de importação

1. Abrir o Forms Experience Builder
2. Clique no ícone de anexo na interface
3. Selecione a opção &quot;Importar e converter&quot;
4. Escolha seu arquivo de origem

### Etapa 2: Fazer upload do documento

**Para arquivos PDF:**

1. Selecione seu documento do PDF
2. Aguarde a análise da estrutura pela IA
3. Revisar os elementos de formulário detectados
4. Confirmar as configurações de conversão

**Para arquivos de imagem:**

1. Fazer upload da imagem (PNG, JPG etc.)
2. A IA analisará o layout e o texto
3. Revisar os campos de formulário detectados
4. Faça ajustes, se necessário

**Para arquivos de design:**

1. Fazer upload do arquivo de design
2. A IA extrairá componentes de formulário
3. Revisar os elementos convertidos
4. Personalizar a estrutura do formulário

### Etapa 3: revisar e personalizar

Após a conversão inicial:

1. **Revisar campos detectados**: verifique se todos os elementos do formulário estão identificados corretamente
2. **Ajustar tipos de campo**: modificar tipos de campo (texto, lista suspensa, caixa de seleção etc.)
3. **Adicionar validação**: configurar regras de validação de campo
4. **Personalizar estilo**: aplicar temas e marcas
5. **Funcionalidade de teste**: verificar comportamento e lógica do formulário

## Exemplos de conversão

### Conversão do formulário do PDF

**Formulário original do PDF:**

- Formulário de contato estático com campos de nome, email, telefone
- Seção de informações da empresa
- Área de comentários

**Formulário adaptável convertido:**

- Campos de texto interativo com validação
- Lista suspensa para tamanho da empresa
- Área de texto multilinha para comentários
- Botão Enviar com integração de email

### Conversão de imagem para formulário

**Imagem original:**

- Foto de um formulário de inscrição em papel
- Formulário manuscrito com caixas de seleção
- Várias seções para diferentes informações

**Formulário adaptável convertido:**

- Campos de texto digital correspondentes ao layout
- Caixas de seleção interativas e botões de opção
- Seções organizadas com espaçamento adequado
- Design responsivo para dispositivos móveis

### Conversão do arquivo de design

**Design original do Figma:**

- Modelo de interface do usuário moderna com componentes de formulário
- Estilos e cores de marca
- Layout complexo com vários painéis

**Formulário adaptável convertido:**

- A recriação perfeita do design para pixels
- Elementos de formulário interativos
- Comportamento responsivo entre dispositivos
- Estilo consistente com a marca

## Recursos avançados de conversão

### Detecção inteligente de campo

A IA detecta e converte automaticamente:

- **Campos de texto**: áreas de texto de linha única e de várias linhas
- **Campos de seleção**: menus suspensos, botões de opção, caixas de seleção
- **Campos de data**: seletores de data com formatação adequada
- **Campos de números**: entradas numéricas com validação
- **Carregamentos de arquivos**: áreas de carregamento de documentos e imagens

### Preservação de layout

A conversão mantém:

- **Estrutura original**: preserva o layout e a organização
- **Hierarquia visual**: mantém cabeçalhos e quebras de seção
- **Espaçamento e alinhamento**: mantém o espaçamento correto do formulário
- **Elementos de marca**: preserva logotipos e elementos de estilo

### Validação inteligente

Adiciona automaticamente a validação apropriada:

- **Campos de email**: validação do formato do email
- **Números de telefone**: validação do formato de número de telefone
- **Campos obrigatórios**: marca os campos obrigatórios óbvios
- **Intervalos de datas**: define restrições de data apropriadas

## Práticas recomendadas para importação e conversão

### Preparando documentos de origem

**Para arquivos PDF:**

- Garantir que o texto seja selecionável (não apenas imagens)
- Usar verificações de alta qualidade para PDFs estáticos
- Organizar conteúdo em seções lógicas
- Incluir rótulos de campos limpos

**Para imagens:**

- Usar imagens de alta resolução (mais de 300 DPI)
- Garanta um bom contraste e legibilidade
- Evite imagens giradas ou inclinadas
- Incluir todos os elementos de formulário na imagem

**Para arquivos de design:**

- Usar nomenclatura consistente para componentes de formulário
- Organizar camadas logicamente
- Incluir todos os elementos de formulário necessários
- Exportar em alta qualidade

### Otimização pós-conversão

**Revisão e teste:**

- Testar todos os campos de formulário e a validação
- Verificar a agilidade móvel
- Verificar conformidade de acessibilidade
- Testar funcionalidade de envio

**Personalizar e aprimorar:**

- Adicionar lógica de negócios e regras condicionais
- Implementar a manipulação adequada de erros
- Configurar pontos de extremidade de envio
- Aplicar estilo de marca e temas

## Solução de problemas de conversão

### Problemas comuns

**Detecção de campo ruim:**

- Melhorar a qualidade da imagem ou a clareza do texto do PDF
- Ajustar manualmente os tipos de campo após a conversão
- Usar mais rótulos de campo descritivos na origem

**Problemas de layout:**

- Ajustar o espaçamento e o alinhamento manualmente
- Usar princípios de design responsivo
- Testar em telas de tamanhos diferentes

**Elementos ausentes:**

- Adicionar campos ausentes manualmente
- Reimportar com melhor qualidade da origem
- Usar o método de conversão incremental

### Obtendo ajuda

Para problemas de conversão:

- Verifique as [Perguntas frequentes sobre o Forms Experience Builder](forms-experience-builder-frequently-asked-questions.md)
- Revise o [Guia de Introdução](forms-experience-builder-getting-started.md)
- Entre em contato com o administrador do sistema para obter assistência técnica

## Artigos relacionados

- [Visão geral do Forms Experience Builder](product-overview.md)
- [Introdução ao Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Implantar e configurar o Forms Experience Builder](deploy-forms-experience-builder.md)
- [Envio e integração de formulários](form-submission-integration.md)
- [Perguntas frequentes](forms-experience-builder-frequently-asked-questions.md)
