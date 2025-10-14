---
title: Introdução ao AEM Forms as a Cloud Service
description: Descubra os recursos do AEM Forms para criar formulários adaptáveis, automatizar fluxos de trabalho e gerenciar documentos digitais. Plataforma completa para processos de negócios orientados por formulários.
landing-page-description: Entenda como usar o AEM Forms as a Cloud Service para criar formulários adaptáveis, processar documentos e automatizar fluxos de trabalho de negócios.
keywords: AEM Forms, formulários adaptáveis, construtor de formulários, formulários digitais, automação de fluxo de trabalho, serviços de documentos, modelo de dados de formulário
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
exl-id: 50d7ce19-7d76-4ea1-a54c-8ca0e5379982
source-git-commit: eca09e1bf2ba4466f54e915e01218cc89cf5b116
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 0%

---

# Introdução ao AEM Forms as a Cloud Service {#introduction}



O Adobe Experience Manager Forms as a Cloud Service fornece uma plataforma abrangente para criar, gerenciar e otimizar experiências de formulários digitais. As empresas usam o AEM Forms para digitalizar processos em papel, criar formulários Web responsivos, automatizar fluxos de trabalho de documentos e fornecer comunicações personalizadas em escala.

A plataforma combina recursos de criação de formulários com serviços robustos de back-end, permitindo que você crie tudo, desde formulários de contato simples até aplicativos comerciais complexos de várias etapas. Com a arquitetura nativa em nuvem, você obtém atualizações automáticas, dimensionamento elástico e segurança de nível empresarial sem gerenciar a infraestrutura.

Este guia apresenta os principais recursos organizados em torno de todo o ciclo de vida do formulário, desde o design inicial até a otimização contínua.

## Novidades do AEM Forms {#whats-new}

**Destaques da última versão:**

- **Componente de Entrada de Data e Hora** - Entrada de usuário aprimorada com interface de calendário e relógio para seleção precisa de data e hora
- **Segurança aprimorada de carregamento de arquivo** - Validação automática e verificação do tipo de conteúdo para evitar formatos de arquivo sem suporte
- **Tratamento de erros aprimorado** - Melhor depuração com códigos de erro específicos para ações de envio personalizadas
- **Aprimoramentos do Documento de Registro** - Opção de excluir campos ocultos para geração de documentos mais limpos

**Recursos de pré-lançamento:**

- **Suporte para o Formato AFP** - Recursos de impressão de nível empresarial com APIs de Comunicação
- **Aprimoramentos do Editor de regras** - Suporte moderno para JavaScript, variáveis dinâmicas e regras do painel com reconhecimento de contexto
- **Métodos de validação aprimorados** - Validação de painel, campo e nível de formulário com maior flexibilidade

[Visualizar notas de versão completas →](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## Programa de acesso antecipado {#early-access}

Obtenha acesso exclusivo a inovações de última geração da AEM Forms antes que elas estejam disponíveis no mercado.

**Recursos Atuais de Acesso Antecipado:**

- **Assistente de IA do AEM Forms** - IA gerativa para recomendações de criação automatizada de formulários, geração de painéis e otimização
- **Componente de Assinatura Escrita** - Captura de assinatura direta dentro de formulários usando mouse, caneta ou tela sensível ao toque
- **Integração direta da API** - Conecte-se às APIs no Editor de regras sem exigir a configuração do modelo de dados de formulário
- **Otimização do Forms** - Análise de desempenho baseada em IA e sugestões de melhoria da taxa de conversão

**Ingressar no Programa:**
Seja um dos primeiros a acessar inovações e ajudar a moldar o futuro do AEM Forms.

[Solicitar acesso →](mailto:aem-forms-ea@adobe.com) | [Saiba mais →](/help/forms/early-access-ea-features.md)


## Principais recursos {#core-capabilities}

O AEM Forms oferece suporte à jornada completa de formulários digitais, desde a criação inicial até a otimização contínua. Cada fase se baseia na anterior, criando uma plataforma abrangente para processos de negócios orientados por formulários.

**Jornada de Fluxo de Trabalho do AEM Forms:**

    CRIAR → GOVERNAR → PUBLICAR → CAPTURAR → PROCESSO → INTEGRAR → RASTREAR → ARQUIVAR → MELHORAR
            ↓        ↓         ↓         ↓         ↓          ↓       ↓        ↓
    Design   Revisão   Implantar   Coletar   Alça   Conectar   Monitorar armazenamento   Otimizar
    ^                                                                              ↓
     Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda Esquerda ESQUERDA ESQUERDA ESQUERDA ESQUERDA ESTE ESQUERDA ESTE ESTE ESQUERDA ESQUERDA ESTE ESTE ESTE ESTE ESTE ESTE ESTE ESQUERDA ESTE

### Criar: Design e desenvolvimento de formulários {#create}

Crie formulários adaptáveis usando várias abordagens de criação personalizadas para diferentes necessidades e requisitos técnicos.

**Construtor de Formulários Visuais**
Crie formulários responsivos por meio de interfaces de arrastar e soltar usando [Componentes principais](/help/forms/creating-adaptive-form-core-components.md), [Componentes de base](/help/forms/creating-adaptive-form.md) ou [Edge Delivery Services](/help/edge/docs/forms/overview.md). O editor visual fornece feedback imediato enquanto mantém uma marcação semântica limpa que funciona em dispositivos e tecnologias assistivas.

**Criação Baseada em Documento**
Crie formulários usando ferramentas familiares, como o Microsoft Excel por meio do [Edge Delivery Services](/help/edge/docs/forms/overview.md). Essa abordagem permite que os autores de conteúdo criem formulários de alto desempenho sem conhecimento técnico e, ao mesmo tempo, atinjam pontuações excepcionais no Google Lighthouse.

**Modelos e Temas**
Acelere a criação de formulários usando os [modelos](/help/forms/template-editor-core-components.md) pré-criados que definem a estrutura e o conteúdo inicial. Aplique uma identidade visual consistente com [temas](/help/forms/using-themes-in-core-components.md) que controlam o estilo visual em vários formulários, garantindo a consistência do design e reduzindo o tempo de desenvolvimento.

**Integrações de dados**
Conectar formulários aos sistemas de back-end durante a fase de design. O [Modelo de Dados de Formulário](/help/forms/create-form-data-models.md) fornece uma interface unificada para várias fontes de dados, permitindo [pré-população](/help/forms/prepopulate-adaptive-form-fields.md), [regras de validação](/help/forms/rule-editor-core-components.md) e fluxo de dados contínuo entre formulários e sistemas empresariais.

**Validações e Lógica Condicional**
Implemente a [lógica condicional](/help/forms/rule-editor-core-components.md), a divulgação progressiva e a validação adaptável para orientar os usuários por processos complexos. [A funcionalidade Salvar e retomar](/help/forms/save-core-component-based-form-as-draft.md) permite que os usuários preencham formulários em várias sessões.

**HTML5 Forms**
Renderize formulários baseados em XFA como [formulários HTML5](/help/forms/introductionhtml5.md) para dispositivos móveis e navegadores herdados. O HTML5 Forms fornece experiência nativa em dispositivos móveis sem plug-ins, mantendo a lógica e a validação de formulários a partir de modelos XDP originais.

**Comunicações interativas**
Crie comunicações centradas em documentos como demonstrativos, faturas e avisos usando um editor visual. [Comunicações interativas](/help/forms/interactive-communication/create-interactive-communication.md) combina conteúdo estático com dados dinâmicos para gerar comunicações personalizadas entre canais digitais e de impressão.

### Controlar: análise e conformidade {#govern}

Estabeleça processos de supervisão e aprovação para garantir que os formulários atendam aos padrões organizacionais e requisitos normativos.

**Aprovações baseadas em fluxo de trabalho**
Rotear designs de formulário por meio de processos de revisão em várias etapas, com atribuições baseadas em funções. As partes interessadas podem [revisar](/help/forms/create-reviews-forms.md), [comentar](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) e aprovar formulários antes da publicação, mantendo o controle de qualidade e a supervisão de conformidade usando os [fluxos de trabalho do AEM](/help/forms/aem-forms-workflow.md).

**Gerenciamento de Versões**
Rastreie versões de formulários e mantenha trilhas de auditoria para conformidade normativa. O [controle de versão](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) integrado garante que você possa reverter alterações, comparar iterações e manter registros históricos para auditorias de conformidade.

**Controle de acesso e permissões**
Defina permissões granulares para criação, edição e publicação de formulários. O [acesso com base em função](/help/forms/forms-groups-privileges-tasks.md) garante que somente usuários autorizados possam modificar formulários, mantendo a separação de tarefas para processos comerciais confidenciais.

### Publicar: Distribuição multicanal {#publish}

Implante formulários em vários canais e pontos de contato para alcançar os usuários onde quer que eles estejam.

**Publicação Omnichannel**
Publicar formulários no [AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md), em páginas da Web autônomas, em aplicativos móveis ou em [incorporados a sistemas de terceiros](/help/forms/embed-adaptive-form-core-components-external-web-page.md). A publicação de uma única fonte garante consistência enquanto se adapta a diferentes requisitos de canal.

**Localização e Personalization**
Enviar formulários em vários idiomas usando os [fluxos de trabalho de tradução do AEM](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md), com suporte para [idiomas da esquerda para a direita e da direita para a esquerda](/help/forms/right-left-languages.md). Integre com o Adobe Target para personalizar experiências de formulário com base em segmentos de usuário, comportamento ou dados contextuais.

**Otimização do desempenho**
Aproveite o Edge Delivery Services para carregar formulários com velocidade surpreendente e otimizar o desempenho de SEO. As redes de entrega de conteúdo garantem acessibilidade global com latência mínima.

**Portal do Forms**
Crie repositórios de formulários centralizados onde os usuários possam descobrir, acessar e gerenciar formulários. O [Forms Portal](/help/forms/configure-forms-portal.md) fornece recursos de pesquisa, categorização de formulários, gerenciamento de rascunhos e rastreamento de envio em uma interface unificada para melhorar a experiência do usuário.

### Capturar: experiência do usuário e coleção de dados {#capture}

Otimize a experiência de preenchimento de formulário para maximizar as taxas de conclusão e a qualidade dos dados.

**Design responsivo**
O Forms se adapta automaticamente a diferentes tamanhos de tela e métodos de entrada. Os controles otimizados para toque, a navegação pelo teclado e a compatibilidade com o leitor de tela garantem a [acessibilidade](/help/forms/creating-accessible-adaptive-forms.md) em todos os tipos de usuário.

**Assinaturas Digitais**
Integre o [Adobe Sign](/help/forms/working-with-adobe-sign.md) para obter assinaturas eletrônicas com vínculo legal dentro da experiência do formulário. Os usuários podem assinar documentos sem sair do formulário, simplificando os processos de aprovação e reduzindo o abandono.

**Enviar Ações**
Configure [ações de envio](/help/forms/configure-submit-actions-core-components.md) para definir o que acontece quando os usuários concluem e enviam formulários. Direcione dados para email, bancos de dados, workflows ou sistemas externos enquanto fornece feedback e confirmação imediatos aos usuários.

### Processo: Controle e Roteamento de Submissão {#process}

Lide com envios de formulários com recursos robustos de processamento, validação e roteamento.

**Validação e processamento de dados**
Garanta a integridade dos dados por meio da validação no lado do servidor e das regras de processamento automatizadas. Transformar, validar e rotear os dados enviados ao gerar recebimentos, confirmações ou material de acompanhamento para os usuários.

**APIs de comunicação**
Gerar, manipular e proteger documentos de forma programática por meio de [RESTful APIs](/help/forms/aem-forms-cloud-service-communications-introduction.md). Crie PDFs, formatos prontos para impressão, monte documentos, aplique assinaturas digitais e processe [operações em lote](/help/forms/aem-forms-cloud-service-communications-batch-processing.md) de grande volume para fluxos de trabalho de documentos de escala empresarial.

**Documento de registro**
Gerar automaticamente registros PDF de envios de formulários para conformidade e confirmação do usuário. O [Documento de Registro](/help/forms/generate-document-of-record-core-components.md) cria versões formatadas e imprimíveis de formulários preenchidos com dados enviados, fornecendo documentação oficial para transações e requisitos normativos.

**Orquestração de Fluxo de Trabalho**
Acione processos de negócios complexos com base em envios de formulários. Direcione dados por meio de cadeias de aprovação, atribua tarefas a usuários específicos e automatize operações de rotina mantendo trilhas de auditoria.

**Tratamento e Recuperação de Erros**
Os mecanismos de repetição e o processamento de fallback integrados garantem que nenhum envio seja perdido. O registro abrangente ajuda a solucionar problemas e a manter os contratos de nível de serviço.

### Integrar: conectividade de back-end {#integrate}

Conecte formulários aos sistemas de negócios e fontes de dados existentes para obter um fluxo de informações perfeito.

**Conectores Pré-Criados**
Integração nativa com soluções do [Salesforce](/help/forms/configure-salesforce.md), [Microsoft Dynamics](/help/forms/configure-msdynamics.md), [SharePoint](/help/forms/connect-forms-to-sharepoint-document-library.md) e Adobe Experience Cloud. Conectores pré-construídos reduzem o tempo de desenvolvimento enquanto garantem a sincronização de dados confiável.

**Integração da API RESTful**
Conecte-se a qualquer serviço acessível pela Web por meio de APIs RESTful via [enviar ações](/help/forms/configure-submit-action-restpoint.md) ou [integração de dados](/help/forms/data-integration.md). O modelo de dados de formulário abstrai a complexidade da integração, fornecendo uma interface consistente independentemente da arquitetura do sistema subjacente.

**Troca de Dados em Tempo Real**
Permita o fluxo de dados bidirecional entre formulários e sistemas de negócios. Preencha previamente os formulários a partir dos registros existentes, valide em relação aos dados em tempo real e atualize vários sistemas simultaneamente após o envio por meio da [integração de dados](/help/forms/data-integration.md) abrangente.

### Track: Analytics e monitoramento de desempenho {#track}

Entenda o desempenho do formulário e o comportamento do usuário por meio de análises e monitoramento abrangentes.

**Análise de formulários**
Rastreie taxas de conclusão, padrões de abandono e interações em nível de campo por meio da [integração com o Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md). Identifique pontos de atrito, meça funis de conversão e entenda o comportamento do usuário em diferentes segmentos.

**Monitoramento de Desempenho**
Monitore os tempos de carregamento dos formulários, as taxas de sucesso dos envios e o desempenho do sistema. Os painéis em tempo real fornecem insights sobre saúde técnica e métricas de experiência do usuário.

**Business Intelligence**
Gerar relatórios sobre uso de formulário, volumes de envio e eficiência de processo. O Analytics informa o planejamento de capacidade, a otimização da experiência do usuário e as melhorias no processo de negócios.

**Relatórios de transação**
Monitore o uso da API, os volumes de geração de documentos e as [transações faturáveis](/help/forms/transaction-reports-billable-apis.md) em sua implantação do AEM Forms. Acompanhe os padrões de consumo, otimize a alocação de recursos e mantenha a conformidade com os requisitos de licenciamento com base no uso.

### Arquivamento: gerenciamento e conformidade de documentos {#archive}

Armazene e gerencie com segurança os envios de formulários e os documentos gerados para retenção e conformidade a longo prazo.

**Armazenamento de Documentos**
Armazene documentos gerados e envios de formulários no sistema de Gerenciamento de Ativos Digitais da AEM ou integre-os a repositórios de documentos externos como o [SharePoint](/help/forms/configure-submit-action-sharepoint.md), o [OneDrive](/help/forms/configure-submit-action-onedrive.md) ou o [Armazenamento de Blobs do Azure](/help/forms/configure-submit-action-azure-blob-storage.md).

**Conformidade e Retenção**
Implemente políticas de retenção de dados que estejam em conformidade com os requisitos normativos, incluindo GDPR, CCPA e HIPAA. [Os &#x200B;](/help/forms/aem-forms-cloud-service-communications-batch-processing.md) processos de arquivamento automatizados garantem que os documentos sejam retidos por períodos obrigatórios e descartados com segurança quando apropriado.

**Segurança e Controle de Acesso**
Aplique criptografia, assinaturas digitais e [controles de acesso com base em função](/help/forms/forms-groups-privileges-tasks.md) aos documentos arquivados. As trilhas de auditoria controlam o acesso aos documentos e as modificações para a emissão de relatórios de conformidade e a supervisão da segurança.

### Melhorar: otimização e aprimoramento {#improve}

Otimize continuamente o desempenho do formulário e a experiência do usuário por meio de insights e testes orientados por dados.

**Integração de teste A/B**
Use o Adobe Target para testar diferentes layouts de formulário, disposições de campo e fluxos de usuário. A análise estatística ajuda a identificar as abordagens mais eficazes para diferentes segmentos de usuários e casos de uso.

**Otimização Orientada Por Análise**
Analise os dados de comportamento do usuário para identificar oportunidades de melhoria. [Visualize e entenda relatórios de análise](/help/forms/view-understand-aem-forms-analytics-reports.md) para mapeamento de calor, análise de interação de campo e reconhecimento de padrão de abandono para informar melhorias de design iterativo.

**Aprimoramento iterativo**
Implemente processos de melhoria contínua com base no feedback dos usuários, nas métricas de desempenho e nos requisitos de negócios. Os recursos de [Controle de versão](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) e reversão permitem experimentação segura e iteração rápida.

## Introdução {#getting-started}

A abordagem que você adota depende de suas necessidades imediatas e objetivos de longo prazo.

### Início rápido: Forms simples {#quick-start}

Escolha a abordagem de criação de sua preferência com base na sua experiência técnica e nos requisitos de desempenho:

**Criação de Formulários Visuais:**

1. **[Crie formulários adaptáveis com os Componentes principais](/help/forms/creating-adaptive-form-core-components.md)** para formulários modernos e responsivos
2. **[Configurar ações de envio](/help/forms/configure-submit-actions-core-components.md)** para manipular dados de formulário
3. **[Incorporar formulários no AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)** ou compartilhar via links diretos

**Criação Baseada em Documento:**

1. **[Criar formulários usando o Excel](/help/edge/docs/forms/create-forms.md)** com o Edge Delivery Services para formulários de alto desempenho
2. **[Publicar no Edge Delivery](/help/edge/docs/forms/publish-forms.md)** para obter as melhores velocidades de carregamento e SEO

**Suporte a Formulários Herdados:**

- **[HTML5 Forms](/help/forms/introductionhtml5.md)** para renderização de formulário XFA otimizado para dispositivos móveis

### Implementação avançada: processos de negócios {#advanced-implementation}

Para requisitos complexos envolvendo vários sistemas, geração de documentos e fluxos de trabalho de aprovação:

**Integração de dados e fluxos de trabalho:**

1. **[Configurar Modelos de Dados de Formulário](/help/forms/create-form-data-models.md)** para conectar sistemas back-end
2. **[Criar processos de fluxo de trabalho](/help/forms/aem-forms-workflow.md)** para aprovação e roteamento
3. **[Configurar a análise](/help/forms/integrate-aem-forms-with-adobe-analytics.md)** para medir o desempenho

**Comunicações e Serviços de Documentos:**

1. **[Implementar APIs de comunicação](/help/forms/aem-forms-cloud-service-communications-introduction.md)** para geração automatizada de documentos
2. **[Criar comunicações interativas](/help/forms/interactive-communication/create-interactive-communication.md)** para instruções e avisos personalizados
3. **[Configurar o Forms Portal](/help/forms/configure-forms-portal.md)** para gerenciamento centralizado de formulários

### Implantação empresarial: dimensionamento e governança {#enterprise-deployment}

Para implantações em toda a organização que exigem governança, conformidade e monitoramento:

**Arquitetura e governança:**

1. **[Revise os padrões de arquitetura](/help/forms/aem-forms-cloud-service-architecture.md)** para implantação escalável
2. **[Configurar o gerenciamento de usuários](/help/forms/forms-groups-privileges-tasks.md)** e os controles de acesso
3. **[Configurar fluxos de trabalho de desenvolvimento](/help/forms/setup-local-development-environment.md)** para colaboração em equipe

**Migração e monitoramento:**

1. **[Planejar estratégias de migração](/help/forms/migrate-to-forms-as-a-cloud-service.md)** de sistemas existentes
2. **[Implementar monitoramento de transações](/help/forms/transaction-reports-billable-apis.md)** para controle de uso e conformidade

<details>
<summary><strong>❓ Perguntas Frequentes</strong></summary>

**O que é um construtor de formulários?**
Um construtor de formulários é uma ferramenta que permite criar formulários digitais sem codificação. Você pode criar formulários usando interfaces de arrastar e soltar, adicionar campos como caixas de texto e listas suspensas e publicá-los online para coletar dados dos usuários.

**Como faço para criar um formulário online?**
Com o AEM Forms, você pode criar formulários adaptáveis usando os Componentes principais por meio de um editor visual de arrastar e soltar, criar formulários de alto desempenho com o Edge Delivery Services ou usar os Componentes de base para fluxos de trabalho estabelecidos. Comece selecionando um modelo, adicione campos de formulário, configure conexões de dados e publique em vários canais.

**O que faz um bom formulário online?**
Bons formulários online são responsivos para dispositivos móveis, carregam rapidamente, têm rótulos claros, usam ordenação de campo lógico, incluem validação para evitar erros e fornecem feedback imediato aos usuários no envio.

**É possível integrar formulários a outros sistemas de negócios?**
Sim, os modernos construtores de formulários oferecem amplos recursos de integração. Você pode conectar formulários a sistemas CRM, plataformas de marketing por email, bancos de dados, armazenamento na nuvem e ferramentas de automação de fluxo de trabalho para simplificar seus processos comerciais.

**Os formulários online são seguros?**
Os construtores profissionais de formulários incluem recursos de segurança de nível empresarial, como criptografia de dados, transmissão segura de dados, controles de acesso e conformidade com normas como GDPR, HIPAA e CCPA para proteger informações confidenciais.

**Como adicionar assinaturas eletrônicas aos meus formulários?**
As assinaturas digitais podem ser integradas diretamente em formulários usando o Adobe Sign ou outros provedores de assinatura eletrônica. Isso permite que os usuários assinem documentos dentro da experiência do formulário, eliminando a necessidade de fluxos de trabalho de assinatura separados e reduzindo o abandono de formulários.

**Os formulários podem gerar documentos do PDF automaticamente?**
Sim, as plataformas de formulário modernas podem gerar automaticamente recibos, confirmações ou documentos de registro do PDF quando os formulários são enviados. Isso é essencial para conformidade, manutenção de registros e fornecimento de confirmação imediata aos usuários.

**Como rastrear o desempenho e a análise dos formulários?**
A análise de formulários ajuda você a entender as taxas de conclusão, os padrões de abandono e o comportamento do usuário. A integração com plataformas de análise como o Adobe Analytics fornece insights sobre quais campos causam atrito e como otimizar as taxas de conversão.

**O que é automação de fluxo de trabalho de formulário?**
A automação do fluxo de trabalho de formulário encaminha os envios por meio de processos de aprovação, atribui tarefas a membros da equipe e aciona ações em outros sistemas de negócios. Isso elimina o processamento manual e garante o tratamento consistente dos dados de formulário.

**Como faço para tornar os formulários acessíveis para usuários portadores de deficiência?**
[Formulários acessíveis](/help/forms/creating-accessible-adaptive-forms.md) incluem rotulagem adequada, navegação pelo teclado, compatibilidade com leitores de tela e conformidade com as diretrizes da WCAG. Isso garante que todos os usuários possam preencher formulários independentemente de suas habilidades ou tecnologias assistivas.

**Quanto custam os construtores de formulários?**
Os preços do AEM Forms as a Cloud Service dependem dos requisitos específicos, do volume de uso e das necessidades de recursos. Para obter informações detalhadas sobre preços e discutir uma solução personalizada para sua organização, entre em contato com o setor de vendas da Adobe ou com seu representante da Adobe.

</details>

## Próximas etapas {#next-steps}

Explore os recursos que correspondem às suas prioridades atuais:

- **[Crie seu primeiro formulário](/help/forms/creating-adaptive-form-core-components.md)** para experimentar o ambiente de criação
- **[Revise as opções de arquitetura](/help/forms/aem-forms-cloud-service-architecture.md)** para o planejamento da implantação
- **[Configure seu ambiente de desenvolvimento](/help/forms/setup-local-development-environment.md)** para colaboração em equipe
- **[Explore as opções de integração](/help/forms/data-integration.md)** para conectar sistemas existentes

Para obter orientação abrangente sobre a implementação, considere o Adobe Professional Services para acelerar sua implantação e garantir as práticas recomendadas desde o início.
