---
title: Associar a interface no Editor de comunicação interativa
description: Descubra a interface do usuário associada no Editor de comunicação interativa, permitindo que o agente voltado para o cliente gere comunicações personalizadas e compatíveis.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="Aplicável ao AEM Forms)."
exl-id: 9ba58659-b14c-4ebc-a6d9-e56a4b6aa48b
source-git-commit: f889498f9ee5e71a4d3695dbfbe194d1bbb11488
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# Associar a interface no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

A **Interface do Usuário Associada** é uma interface simplificada e especializada criada sobre o editor de IC (Comunicações Interativas). Ele foi projetado para profissionais voltados para o cliente, como associados de campo e agentes de serviço, para gerar comunicações personalizadas, compatíveis e precisas em tempo real durante as interações em tempo real.

![Localizar IC Doc](/help/forms/interactive-communication/assets/associate-ui-preview.png)

## Associar interface do usuário

A Interface do usuário do Associate fornece um espaço de trabalho limpo de dois painéis que permite a geração de comunicação rápida e segura:

### Painel Esquerdo: Entrada de Dados

- Os associados inserem ou confirmam informações específicas do cliente.
- Validações, textos auxiliares e campos obrigatórios orientam a entrada precisa.

### Painel direito: Visualização em tempo real

- Exibe uma visualização instantânea do documento final.
- Atualiza automaticamente conforme o associado preenche os dados.

### Geração instantânea de documento

- Gerar ou baixar a comunicação finalizada.

## Personas e responsabilidades do usuário

A interface do usuário Associate é orientada por três funções principais, cada uma com responsabilidades distintas:

### &#x200B;1. Administrador

Responsável pela configuração do sistema, governança, integrações de back-end e acesso do usuário.

| Responsabilidade | Foco |
|---------------|-------|
| Configuração do sistema | Configura a infraestrutura principal, os grupos de usuários, os Modelos de dados de formulário (FDM) e a saída. |
| Governança e segurança | Gerencia permissões do usuário e garante a conformidade do sistema. |
| Gerenciamento de integração | Mantém integrações de back-end e conexões ativas de dados do cliente. |

### &#x200B;2. Autor

Projeta e gerencia a comunicação interativa e a configura para a interface do usuário Associar (incluindo a ativação da exibição Associar e do fluxo de trabalho opcional).

| Responsabilidade | Foco |
|---------------|-------|
| Criação e design da IC | Cria layout, marca e estrutura de documento compatível. |
| Configuração do campo | Mapeia campos de dados, define campos Editáveis, Obrigatórios e Somente Leitura. |
| Publicação e ativação | Publica a IC e compartilha o link para acesso associado. |

### &#x200B;3. Associar

Usa a Interface do usuário do Associate para auxiliar clientes, atualizar informações e gerar comunicações de conformidade.


| Responsabilidade | Foco |
|---------------|-------|
| Confirmação de dados | Preenche ou valida os dados do cliente por meio do painel de entrada esquerdo. |
| Visualização e validação | Garante a precisão usando o painel de visualização em tempo real. |
| Entrega | Gera a PDF/email e a envia por meio dos canais aprovados. |

>[!NOTE]
>
> Os associados devem fazer parte do grupo **forms-associates**. Para autores que também enviam da interface do usuário Associate na instância do Author, adicione-os a **workflow-users** também.

## Casos de uso dinâmico

A interface do usuário Associate oferece suporte à geração instantânea e personalizada de documentos, essencial para setores com necessidades de manutenção em tempo real.

| Setor | Exemplo de casos de uso |
|----------|-------------------|
| **Serviços financeiros** | Gerar cartas de confirmação de empréstimo em tempo real, resumos de perfil de risco e criação de conta. |
| **Seguros** | Produza cartões de prova de seguro instantâneos ou resumos de descarte de solicitações. |
| **Serviços de saúde** | Crie resumos do plano de tratamento do paciente com códigos e cronogramas calculados. |
| **Setor público** | Gerar relatórios de verificação policial, recibos de serviço ao cidadão, cartas de confirmação de reclamação e resumos de atualização de casos no local. |
| **Governo** | Crie resumos de status da requisição, cartas de aprovação de serviço e comunicação em tempo real para inscrições em esquemas de previdência. |

## Ativação da interface de usuário Associar

Os autores habilitam a Interface do Usuário Associada e, opcionalmente, configuram um fluxo de trabalho para envios em **Configurações de comunicação interativa**:

1. **Habilitar Modo de Exibição Associado** — Em **Associar Propriedades**, marque **Habilitar Edição de Modo de Exibição Associado**, clique em **Aplicar Alterações** e salve o documento.
2. **Configurar fluxo de trabalho (opcional)** — No **Fluxo de trabalho**, ative **Configurar Fluxo de Trabalho para Atualização**. Selecione um modelo de fluxo de trabalho e, opcionalmente, defina uma mensagem de sucesso e uma URL de redirecionamento.
3. **Configurar campos editáveis** — Habilite os campos associados para editar e definir validações.
4. **Publicar e compartilhar** — Publique a IC e compartilhe o link com os associados.

Para obter instruções passo a passo com capturas de tela e comportamento de envio/fluxo de trabalho (Autor em Autor vs. Associar em Publicar), consulte [Habilitar e configurar a Interface do Usuário para Comunicações Interativas](/help/forms/interactive-communication/enable-configure-associate-ui.md). Para criar um fluxo de trabalho que gera o PDF a partir de envios IC, consulte [Fluxo de trabalho de envio para Interface do usuário associada — IC Gerar saída PDF](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md).

A **Interface de usuário associada** preenche a lacuna entre a criação de conteúdo estruturado e o envolvimento do cliente em tempo real.\
Combinando design intuitivo, configuração de back-end robusta e controles de conformidade rigorosos, as organizações podem fornecer **comunicações rápidas, precisas e personalizadas** em escala.

## Consulte também:

- [Habilitar e configurar a Interface do Usuário Associada para Comunicações Interativas](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [Integrar a interface do usuário do Associate no seu aplicativo](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Fluxo de trabalho de envio para interface do usuário associada — IC Generate PDF Output](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md)
