---
title: Adicionar o Google reCAPTCHA ao Forms no Editor universal
description: Guia para implementar a proteção do Google reCAPTCHA em formulários do Edge Delivery Services para impedir spam e ataques automatizados
feature: Edge Delivery Services
keywords: reCAPTCHA em formulários, Uso do reCAPTCHA no Universal Editor, Adição do reCAPTCHA em formulários, segurança de formulários, proteção contra spam
role: Developer, Admin
level: Intermediate
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---


# Adicionar o Google reCAPTCHA ao Forms no Editor universal

O Google reCAPTCHA ajuda a proteger formulários, diferenciando usuários humanos e bots automatizados. Este guia explica como implementar as versões Enterprise e Standard do reCAPTCHA no Universal Editor.

**Objetivos:**

- Selecione a solução reCAPTCHA apropriada
- Configurar o reCAPTCHA Enterprise ou Standard
- Adicionar reCAPTCHA aos seus formulários
- Validar e testar a implementação
- Monitorar e otimizar o desempenho

## Pré-requisitos

Antes de iniciar, verifique se você tem o seguinte:

### Requisitos de acesso

- Acesso de criação ao AEM as a Cloud Service
- Acesso ao Editor universal com permissões de edição de formulário

### Requisitos técnicos

- Conta ativa do Google
- Para corporações: projeto da Google Cloud Platform com faturamento ativado
- Para Standard: conta do Google reCAPTCHA
- Propriedade de domínio verificada para seus formulários

### Requisitos de conhecimento

- Noções básicas sobre o AEM Forms e o Universal Editor
- Familiaridade com configurações do Cloud Service
- Noções básicas sobre conceitos de segurança de formulário

## Por que usar o reCAPTCHA no seu Forms?

| ![Segurança](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![Proteção de bot](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![Experiência do usuário](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **Segurança aprimorada** | **Prevenção contra spam e bot** | **Experiência de usuário perfeita** |
| Proteger formulários contra atividades e ataques fraudulentos | Impedir que bots automatizados enviem formulários | O reCAPTCHA invisível não interrompe usuários legítimos |

**Conceito principal:** o reCAPTCHA usa o aprendizado de máquina para analisar o comportamento do usuário e atribui uma pontuação (0,0 a 1,0) indicando a probabilidade de interação humana. Pontuações mais altas indicam usuários humanos; pontuações mais baixas sugerem bots.

**Exemplo:** um formulário de cálculo de imposto que lida com dados confidenciais requer proteção contra ataques automatizados. O reCAPTCHA verifica se os envios são de usuários reais, não de bots.

## Escolha sua solução reCAPTCHA

O Edge Delivery Services Forms é compatível com duas opções de reCAPTCHA do Google. Use os critérios a seguir para selecionar a solução correta:

### Guia de decisão rápida

**Use o reCAPTCHA Enterprise se você tiver:**

- Formulários de alto tráfego (>10.000 solicitações/mês)
- Requisitos de conformidade rigorosos (GDPR, SOX, HIPAA)
- Necessidade de análises e relatórios avançados
- Orçamento para recursos de segurança premium
- Implantações complexas de vários domínios

**Use o reCAPTCHA Standard se você tiver:**

- Tráfego baixo a moderado (&lt;10.000 solicitações/mês)
- Necessidades básicas de segurança
- Orçamento limitado (nível gratuito)
- Configuração simples de domínio único
- São novos no reCAPTCHA

### Comparação detalhada

| **Recurso** | **reCAPTCHA Empresa** | **Padrão do reCAPTCHA** |
|-------------|--------------------------|------------------------|
| **Custo** | Pago (preço com base na utilização) | Gratuito |
| **Limite de Solicitações** | Ilimitado | 1 milhão de solicitações/mês |
| **Análises avançadas** | Relatórios detalhados | Somente estatísticas básicas |
| **Regras personalizadas** | Regras específicas da conta | Somente regras globais |
| **Suporte a vários domínios** | Gerenciamento avançado | Suporte básico |
| **SLA** | 99,9% de garantia de tempo de atividade | Melhor esforço |
| **Suporte** | Suporte Enterprise | Suporte da comunidade |
| **Conformidade** | Nível empresarial | Conformidade padrão |

**Ambas as soluções fornecem:**

- Detecção baseada em pontuação (escala de 0 a 1,0)
- Operação invisível (nenhuma interação do usuário é necessária)
- Detecção de bot habilitada para aprendizado de máquina
- Avaliação de riscos em tempo real

## Configurar o reCAPTCHA Enterprise


+++ Etapa 1: Preparar O Ambiente De Nuvem Do Google

**Requisitos:**

1. Projeto da Google Cloud com faturamento ativado
2. ID do projeto (do painel GCP)
3. Verificação de domínio para seus formulários
4. Acesso de administrador ao GCP e ao AEM

**Instalação:**

1. Criar ou selecionar um projeto da Google Cloud
   - Ir para o [Google Cloud Console](https://console.cloud.google.com/)
   - Criar um novo projeto ou selecionar um já existente
   - Anote a ID do projeto

2. Habilitar a API corporativa do reCAPTCHA
   - Acesse APIs e serviços > Biblioteca
   - Procure por &quot;reCAPTCHA Enterprise API&quot;
   - Clique em Ativar

3. Criar credenciais de API
   - Acesse APIs e serviços > Credenciais
   - Clique em Criar credenciais > Chave de API
   - Copie e armazene sua chave de API

4. Criar chave do site
   - Acesse Segurança > reCAPTCHA Enterprise
   - Clique em Criar chave
   - Escolher tipo de chave baseada em pontuação
   - Adicionar seu(s) domínio(s)
   - Definir pontuação de limite (recomendado: 0,5)

**Ponto de Verificação de Validação:** Verifique se você tem:

- ID do projeto
- Chave da API
- Chave do site
- Domínio verificado na Google Cloud

+++

+++ Etapa 2: definir o contêiner de configuração da nuvem do AEM

![Configuração de nuvem passo a passo](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)
*Figura: Habilitando configurações de nuvem para o contêiner de formulário*

**Instalação:**

1. Acessar navegador de configuração
   - Faça logon na instância de autor do AEM
   - Acesse Ferramentas > Geral > Navegador de configuração

2. Ativar configurações em nuvem
   - Localize o contêiner de configuração do formulário
   - Selecionar propriedades
   - Verificar configurações de nuvem
   - Clique em Salvar e fechar

3. Verificar configuração
   - Confirmar &quot;Configurações de nuvem&quot; aparece nas propriedades do container

**Ponto de Verificação de Validação:**

- Configurações de nuvem habilitadas para o seu contêiner
- O contêiner é exibido no Navegador de configuração
- As propriedades mostram &quot;Configurações de nuvem&quot; como ativadas

+++

+++ Etapa 3: configurar o Serviço corporativo reCAPTCHA no AEM

![tela de configuração corporativa do reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)
*Figura: interface de configuração do reCAPTCHA Enterprise no AEM*

**Configuração:**

1. Acessar a configuração do reCAPTCHA
   - Acesse Ferramentas > Serviços da nuvem > reCAPTCHA
   - Selecione o contêiner de configuração do seu formulário
   - Clique em Criar

2. Definir Configurações Corporativas
   - Título: nome descritivo (por exemplo, &quot;Production reCAPTCHA&quot;)
   - Nome: Nome do sistema (gerado automaticamente ou personalizado)
   - Versão: Selecione ReCAPTCHA Enterprise
   - ID do projeto: insira sua ID do projeto do Google Cloud
   - Chave do site: insira a chave do site na Google Cloud
   - Chave da API: insira sua chave da API da Google Cloud
   - Tipo de chave: selecione Chave do site com base em pontuação

3. Definir Limite de Segurança
   - Pontuação limite: Definida entre 0,0 e 1,0
   - Valores recomendados:
      - 0.7-0.9: Alta segurança (pode bloquear alguns usuários legítimos)
      - 0.5-0.7: Segurança equilibrada (recomendado)
      - 0.1-0.5: Segurança mais baixa (permite mais usuários)

4. Salvar e publicar
   - Clique em Criar para salvar a configuração
   - Clique em Publicar para disponibilizá-lo

**Ponto de Verificação de Validação:**

- Configuração salva com sucesso
- Todos os campos obrigatórios foram preenchidos
- Configuração publicada e visível
- Nenhuma mensagem de erro

+++

## Configurar o reCAPTCHA Standard

+++Etapa 1: Obter chaves de API do reCAPTCHA (consulte os detalhes)

>[!IMPORTANT]
>
> O Edge Delivery Services Forms é compatível apenas com o reCAPTCHA v2 (baseado em pontuação). Não use a versão da caixa de seleção.

**Geração de chave:**

1. Acessar o console reCAPTCHA do Google

   - Ir para o [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin)
   - Fazer logon com sua conta da Google

2. Criar novo site

   - Clique em + para adicionar um novo site
   - Label: digite um nome descritivo
   - Tipo de reCAPTCHA: selecione reCAPTCHA v2 > &quot;Não sou um robô&quot; Invisível
   - Domínios: adicione seu(s) domínio(s) de formulário
   - Aceite os termos e clique em Enviar

3. Colete suas chaves

   - Chave do site: copie a chave do site (chave pública)
   - Chave secreta: copie a chave secreta (chave privada)

**Ponto de Verificação de Validação:**

- Site criado no console do reCAPTCHA

- Chave do site obtida

- Chave secreta obtida

- Domínio(s) adicionado(s) e verificado(s)

+++

+++Etapa 2: definir o contêiner de configuração da nuvem do AEM (consulte os detalhes)

Siga o mesmo processo da Configuração do Enterprise:

1. Habilitar configurações de nuvem no navegador de configuração

2. Verificar configuração do contêiner

3. Confirmar se as configurações foram salvas

+++

+++Etapa 3: configurar o serviço padrão reCAPTCHA no AEM (consulte os detalhes)

![Tela de configuração padrão do reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)
*Figura: interface de configuração do reCAPTCHA Standard no AEM*

**Configuração:**

1. Acessar a configuração do reCAPTCHA

   - Acesse Ferramentas > Serviços da nuvem > reCAPTCHA
   - Selecione o contêiner de configuração do seu formulário
   - Clique em Criar

2. Definir Configurações Padrão

   - Título: nome descritivo (por exemplo, &quot;Standard reCAPTCHA&quot;)
   - Nome: Nome do sistema (gerado automaticamente ou personalizado)
   - Versão: Selecione ReCAPTCHA v2
   - Chave do site: insira sua chave do site Google reCAPTCHA
   - Chave secreta: insira sua chave secreta do Google reCAPTCHA

3. Salvar e publicar

   - Clique em Criar para salvar a configuração
   - Clique em Publicar para disponibilizá-lo

**Ponto de Verificação de Validação:**

- Configuração criada sem erros

- Ambas as chaves foram inseridas corretamente

- Configuração publicada com sucesso

- A configuração é exibida na lista

+++

## Adicionar reCAPTCHA ao formulário

Após configurar o serviço reCAPTCHA, adicione proteção ao formulário da seguinte maneira:

![Adicionando o componente reCAPTCHA a um formulário](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)
*Figura: Adicionando o componente Captcha Invisível ao formulário*

+++&#x200B;1. Abrir formulário no Universal Editor
Vá para o formulário no AEM Sites e clique em Editar para abri-lo no Universal Editor. Aguarde até que o editor seja carregado.

- Acesse seu formulário no AEM Sites
- Clique em Editar para abrir no Editor universal
- Aguardar o editor carregar
+++

+++&#x200B;2. Localize a estrutura do formulário
Na Árvore de conteúdo (painel esquerdo), encontre a seção Formulário adaptável e expanda a estrutura do formulário para ver os pontos de inserção.

- Na Árvore de conteúdo (painel esquerdo), encontre a seção Formulário adaptável
- Expanda a estrutura do formulário para ver pontos de inserção
+++

+++&#x200B;3. Adicionar componente reCAPTCHA
Adicione o componente Captcha (Invisível) ao formulário.

- Clique no ícone Adicionar (+) na seção do formulário
- Na lista de componentes, selecione Captcha (Invisível)
- Como alternativa, arraste e solte o componente do painel Componentes
+++

+++&#x200B;4. Configurar Componente (Opcional)
Selecione o componente captcha recém-adicionado e verifique se ele usa a configuração do reCAPTCHA.

- Selecione o componente captcha recém-adicionado
- No painel Propriedades, verifique se ele usa a configuração do reCAPTCHA
- Nenhuma configuração adicional é necessária para a configuração básica
+++

+++&#x200B;5. Publicar suas alterações
Publique suas alterações e verifique se não há erros.

- Clique em Publicar no Universal Editor
- Aguardar confirmação
- Verifique se nenhum erro é exibido
+++

### Verificar implementação

Seu formulário protegido agora está disponível em:

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/
<form-name>
```

**Exemplo de URL:**

```
https://main--my-forms--company.aem.live/content/forms/af/
contact-us-form
```
