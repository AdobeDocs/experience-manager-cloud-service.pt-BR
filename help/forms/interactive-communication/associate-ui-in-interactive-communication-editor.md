---
title: Associar a interface no Editor de comunicação interativa
description: Descubra a interface do usuário associada no Editor de comunicação interativa, permitindo que o agente voltado para o cliente gere comunicações personalizadas e compatíveis.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 19270498fa60f860b31400ad40705ecd2f821cf8
workflow-type: tm+mt
source-wordcount: '594'
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

Projeta e gerencia a comunicação interativa usando a interface do usuário Associar. ß

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
> O associado deve fazer parte do grupo **forms-associates**.

## Casos de uso dinâmico

A interface do usuário Associate oferece suporte à geração instantânea e personalizada de documentos, essencial para setores com necessidades de manutenção em tempo real.

| Setor | Exemplo de casos de uso |
|----------|-------------------|
| **Serviços financeiros** | Gerar cartas de confirmação de empréstimo em tempo real, resumos de perfil de risco e criação de conta. |
| **Seguros** | Produza cartões de prova de seguro instantâneos ou resumos de descarte de solicitações. |
| **Serviços de saúde** | Crie resumos do plano de tratamento do paciente com códigos e cronogramas calculados. |
| **Setor público** | Gerar relatórios de verificação policial, recibos de serviço ao cidadão, cartas de confirmação de reclamação e resumos de atualização de casos no local. |
| **Governo** | Crie resumos de status da requisição, cartas de aprovação de serviço e comunicação em tempo real para inscrições em esquemas de previdência. |

## Ativação do fluxo de trabalho Associar interface

O autor pode seguir as etapas abaixo para configurar e publicar uma Comunicação interativa (IC) para acessar a interface do usuário associada:

>[!NOTE]
>
> Componentes compatíveis para associado: Campo de data, Campo numérico, Campo de texto.

### Criar a IC

Projete e configure a Comunicação interativa, garantindo que a identidade visual, os vínculos de dados, as regras de conformidade e as integrações sejam definidos corretamente.

### Habilitar a Interface do Usuário Associada

Na barra de ação superior, ative a opção Associate UI para disponibilizar a IC para orientada por associado.

### Habilitar a interface do usuário Associar no componente

### Configurar campos editáveis

Na seção de campos obrigatórios, ative os campos que os associados podem editar.
Defina validações para garantir uma entrada de dados precisa e controlada.

### Publicar a IC

Após finalizar todas as configurações, publique a Comunicação interativa para acesso seguro.

### Compartilhar a IC publicada com Associados

Fornecer o link IC publicado para o Associado, permitindo que eles se autentiquem, insiram informações específicas do cliente e gerem a comunicação final com entradas válidas.

A **Interface de usuário associada** preenche a lacuna entre a criação de conteúdo estruturado e o envolvimento do cliente em tempo real.\
Combinando design intuitivo, configuração de back-end robusta e controles de conformidade rigorosos, as organizações podem fornecer **comunicações rápidas, precisas e personalizadas** em escala.
