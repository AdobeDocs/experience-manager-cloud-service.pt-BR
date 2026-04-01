---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service
description: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 9820b642af32960c532b238e00267cb4d880535f
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 6%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2023 ou 2024.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2026.3.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 26 de março de 2026. O próximo lançamento de recursos (2026.4.0) está planejado para sexta-feira, 30 de abril de 2026.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

&lt;## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de março de 2026 que exibe um resumo dos recursos adicionados na versão 2026.3.0:

>[!VIDEO](https://video.tv.adobe.com/v/3483060/?quality=12)

## Programas do AEM Beta {#aem-beta-programs}

Os programas beta do Adobe Experience Manager (AEM) são uma maneira de os clientes obterem acesso a recursos e código de pré-lançamento, fornecerem feedback e guiarem o futuro do AEM.

>[!IMPORTANT]
>
>As versões do Beta podem conter defeitos e são fornecidas &quot;NO ESTADO EM QUE SE ENCONTRAM&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte (por meio dos Serviços de suporte da Adobe ou de outra forma) às versões beta. A Adobe recomenda que os clientes tenham cuidado e não dependam do funcionamento ou do desempenho correto das versões beta, nem de qualquer documentação ou material que as acompanhe. Os recursos e as APIs na versão beta estão sujeitos a alterações sem aviso prévio. Portanto, qualquer uso das versões beta é de inteira responsabilidade do cliente.

**Vantagens de participar**

Obter acesso antecipado aos recursos que a Adobe está desenvolvendo permite que clientes e parceiros forneçam feedback e modelem o desenvolvimento de produtos. Também os ajuda a se preparar para adotar novos recursos antes da disponibilidade geral.

**Programas beta atuais**

As seções a seguir listam os programas beta ativos.

### Agentes no AEM {#agents-in-aem}

Se você quiser explorar os novos e poderosos recursos do AEM em produção, governança, otimização, descoberta e desenvolvimento, [saiba mais sobre como acessá-los aqui.](/help/ai-in-aem/agents/overview.md)

<!--
### Agents in AEM (Explorer program) {#agents-in-aem-beta-program}

Gain early access to powerful, new AEM agentic capabilities across production, governance, optimization, discovery, and development. Your feedback directly shapes Adobe's roadmap and final features. See [Overview of Agents in AEM](/help/ai-in-aem/agents/overview.md) to learn more.

This program typically lasts 4-6 weeks, but can be tailored to be flexible around your ability to actively participate. 

To opt in to participate in this program, email [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) and include the following details to the extent possible:

* Names and Adobe ID's of team members who will actively use agents.
* List Specific agents that you or your team will want to use. Or simply say "All Agents."

Customers selected for participation will be notified directly by Adobe. Participation is subject to eligibility considerations, including customer licensing and limited program capacity. While not all requests can be accommodated initially, additional customers may be considered in future beta waves.
-->

### AEM Foundation (programas do Beta) {#aem-foundation-beta-programs}

Consulte [programas beta do AEM Foundation](#foundation-early-adopter).

### Cloud Manager (programas do Beta) {#cloud-manager-beta-programs}

Consulte [programas beta do Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Check-out/Entrada do fragmento de conteúdo {#cf-checkout-in}

Para melhorar a paridade com a interface para toque do AEM, agora é possível fazer check-out e check-in dos fragmentos de conteúdo usando também a nova interface para administração de fragmentos de conteúdo. A funcionalidade de check-out permanece inalterada, bloqueando efetivamente um fragmento de conteúdo com check-out e impedindo que ele seja editado no Editor de fragmentos de conteúdo por outros usuários. Os usuários que possuem um fragmento de conteúdo e os administradores podem fazer check-out e check-in do fragmento. A verificação de um fragmento não afeta fragmentos ou ativos secundários referenciados.

### Fragmento do conteúdo inicia o painel Trabalhos {#cf-launches-jobs}

Os trabalhos assíncronos para inicializações de fragmentos de conteúdo agora podem ser exibidos no painel de propriedades da interface do administrador de inicializações de fragmento de conteúdo para observar seu status: se um trabalho ainda estiver em execução, tiver sido concluído ou tiver sido anulado, juntamente com informações detalhadas relevantes sobre o trabalho.

### Atualização do RTE do Editor de fragmento de conteúdo {#cf-rte-update}

O editor de rich text (RTE) do editor de fragmento de conteúdo foi migrado do TinyMCE para o TipTap. Essa mudança traz uma série de benefícios.

* O Editor universal e o Editor de fragmento de conteúdo agora usam a mesma pilha de tecnologia RTE.
   * Isso significa que ambos os editores agora produzem o mesmo HTML.
   * As extensões agora podem ser reutilizáveis.
   * As mesmas funções e métodos agora estão disponíveis usando ambos os editores (em casos de uso headless).
   * O objetivo final é que uma configuração leve a uma experiência unificada em ambos os editores.
* O Editor de conteúdo agora tem uma nova aparência no estilo do Spectrum 2.
* Uma nova funcionalidade está disponível no Editor de fragmento de conteúdo, incluindo localizar e substituir, e ter o content advisor pronto.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Supervisor de Conteúdo no AEM Sites**

O Supervisor de conteúdo agora está disponível no AEM Sites, introduzindo a detecção inteligente de ativos diretamente da AEM Assets. Ele permite que os usuários descubram, naveguem e reutilizem facilmente os ativos mais relevantes diretamente no fluxo de trabalho, eliminando a necessidade de alternar contextos.

O Supervisor de conteúdo fornece recursos inteligentes para ativos, como sugestões baseadas em resumo da campanha, sugestões contextuais, acesso a representações do Dynamic Media e metadados de ativos detalhados.

Em breve — suporte do Supervisor de conteúdo para aplicativos B2C da Adobe Workfront e AJO, incluindo a capacidade de detectar fragmentos de conteúdo

### Novos recursos no Dynamic Media {#dynamic-media-new-features}

#### Atualizações do Editor de modelos do Dynamic Media {#dynamic-media-template-editor-updates}

**Melhorias no gerenciamento de camadas**

* Reorganização da camada de arrastar e soltar: agora as camadas podem ser reordenadas diretamente no painel Camadas ao arrastar, fornecendo uma maneira mais rápida e intuitiva de organizar a ordem de empilhamento da camada além das ações Avançar ou Recuar existentes.
* Copiar, Colar e Duplicar: suporte completo para copiar, colar e duplicar camadas usando atalhos de teclado (Cmd/Ctrl+C, V, D) ou o menu de contexto, com suporte para seleções de várias camadas.
* Botão Propriedades de camada separadas: adição do botão Propriedades de camada dedicado para facilitar a navegação até as configurações de camada, com o suporte de clique duplo em camadas para acesso rápido.

**Recursos de Formatação de Texto**

* Controle de espaçamento entre linhas: o novo controle deslizante de espaçamento entre linhas permite um controle preciso sobre a altura da linha em camadas de texto, com suporte completo de ponta a ponta, incluindo desfazer/refazer e salvar/carregar modelos.
* Formatação de Todas as Maiúsculas: as camadas de texto agora oferecem suporte à opção de formatação de Todas as Maiúsculas na barra de ferramentas Estilo da Fonte ao lado de Negrito, Itálico e Sublinhado.
* Opções de alinhamento vertical: adição de controles de alinhamento vertical para camadas de texto, fornecendo um posicionamento de texto mais preciso nas caixas de texto.

**Controles de Tamanho e Dimension**

* Desbloqueio da taxa de proporção: os usuários agora podem desbloquear a taxa de proporção ao ajustar as propriedades de tamanho, permitindo ajustes independentes de largura e altura para um dimensionamento de camada mais flexível.
* Configuração de Linhas de Ajuste de Texto: Adição de suporte para configurações de `copyfitlines` e `copyfitmaxlines` em propriedades de ajuste de texto de texto, fornecendo controle mais fino sobre o comportamento de ajuste de texto.

**Visual Polonês**

* Ícones atualizados para Camadas de timer e forma com ícones refinados do sistema de design do Spectrum 2 (S2).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Recursos de acesso antecipado no AEM Forms {#forms-early-access-features}

**Exibir rótulos para a lista suspensa de várias seleções no PDF de Envio**
Os componentes de seleção múltipla suspensos no Adaptive Forms agora renderizam seus rótulos de exibição selecionados na [PDF de envio gerada](/help/forms/generate-document-of-record-core-components.md), garantindo que o documento reflita com precisão o que os usuários veem no formulário.

**Acessibilidade aprimorada para componentes de caixa de seleção, botão de opção e painel**
Os Componentes principais adaptáveis do Forms apresentam marcação semântica compatível com WCAG 2.2 para [grupos de caixas de seleção(v2)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group), [grupos de botões de opção(v2)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button) e o [componente de Painel](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel). Esses componentes usam os elementos do HTML `<fieldset>` e `<legend>` para estabelecer relações significativas entre os rótulos de grupo e suas opções, permitindo a interpretação precisa por leitores de tela e outras tecnologias de assistência.

**Suporte ao controle de versão no Forms Manager**
O Forms Manager agora [oferece suporte ao controle de versão do Adaptive Forms (Componentes principais e Componentes de base)](/help/forms/manage-form-versions-forms-manager.md), fragmentos de formulário, temas, modelos XDP e ativos binários. Crie versões, visualize o histórico completo de versões e restaure estados anteriores dos ativos de formulário diretamente do console Forms e Documentos.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Novos recursos {#foundation-new}

#### Gerenciamento simplificado de índice {#simplified-index-management}

[O Gerenciamento simplificado de índice](https://oak-indexing.github.io/oakTools/simplified.html) fornece uma maneira mais simples de definir índices personalizados e personalizar índices prontos para uso (OOTB) usando um arquivo JSON, sem copiar definições completas ou gerenciar versões manualmente. As personalizações são mescladas com o índice OOTB mais recente e uma nova versão do índice é criada quando necessário.

#### Cloud Manager MCP Server {#cm-mcp-server}

>[!VIDEO](https://video.tv.adobe.com/v/3480347/?captions=por_br&quality=12)

IDEs modernos usam o protocolo de contexto de modelo (MCP) para permitir que modelos de linguagem grandes (LLMs) chamem ferramentas expostas por servidores MCP. Em vez de integrar diretamente com especificações de API de baixo nível, os desenvolvedores podem simplesmente descrever sua intenção em linguagem natural.

O Cloud Manager MCP Server permite que você interaja com as APIs do Cloud Manager diretamente do IDE usando prompts. Os cenários compatíveis incluem a execução de pipelines, a verificação do status do ambiente e muito mais.

Saiba mais sobre [Servidores MCP do AEM](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

### Avisos importantes sobre a base [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation-notices}

#### Desaprovações da API Java {#java-api-deprecation}

As APIs obsoletas que direcionam a remoção de 26/02/2026 não devem mais ser usadas no código. Para evitar bloqueios de implantação, remova o uso da API antes de **30 de março de 2026**. Datas importantes:

* **A partir de 26 de janeiro de 2026**: os emails de notificação da Central de Ações são enviados como um lembrete para remover o uso dessas APIs.
* **26 de fevereiro de 2026**: os pipelines do Cloud Manager que contêm código usando essas APIs **pausarão** durante a etapa **Qualidade do Código**. Um Gerente de implantação, Gerente de projeto ou Proprietário da empresa pode substituir o problema para permitir que o pipeline continue. *Isso pode retardar sua capacidade de validar e liberar alterações no código.*
* **30 de março de 2026**: os pipelines do Cloud Manager que contêm código usando essas APIs **falharão** durante a etapa **Qualidade do código**. As implantações serão bloqueadas até que o uso da API obsoleta seja removido. *Isso pode impedir que você libere atualizações com prazo determinado e pode afetar suas operações comerciais.*
* **4 de maio de 2026**: os ambientes que ainda usam APIs obsoletas **não receberão atualizações críticas de versões do Adobe** e não estão sujeitos aos compromissos padrão da Adobe sobre desempenho e disponibilidade. Como resultado, você não receberá novos recursos ou correções de erros, a estabilidade e o tempo de atividade do aplicativo podem ser afetados negativamente e a exposição ao risco de segurança pode aumentar ainda mais.

Consulte o [artigo de descontinuação](/help/release-notes/deprecated-removed-features.md#aem-apis) para obter detalhes completos, mas, para conveniência, essas APIs estão listadas abaixo:

+++ Expanda para ver as descontinuações da API Java

* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

### Recursos do [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Early Adopter {#foundation-early-adopter}

#### Ferramentas de IA do IDE para desenvolvimento em Java e Dispatcher do AEM (Programa Beta público) {#ai-dev-beta}

As equipes de pilha em Java estão cada vez mais usando o desenvolvimento assistido por IA em ferramentas como Cursor, Claude Code, Visual Studio e IntelliJ para acelerar a entrega de recursos e melhorar a qualidade do código.

Participe do beta público (sem necessidade de inscrição) para experimentar as ferramentas do IDE que podem ser usadas pelos agentes de codificação para gerar e depurar o código AEM e a configuração do Dispatcher.

Saiba mais na [documentação beta de Desenvolvimento local com ferramentas de IA](/help/ai-in-aem/local-development-with-ai-tools.md) e envie um email para [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) com perguntas ou comentários.

#### Funções do AEM Edge (Programa Beta) {#edge-functions}

O AEM Edge Functions permite executar o JavaScript na camada CDN, aproximando o processamento de dados do usuário final. Isso reduz a latência e permite experiências responsivas e dinâmicas na borda.

Casos de uso comuns incluem:

* Personalização de conteúdo com base na geolocalização, tipo de dispositivo ou atributos do usuário
* Atuar como middleware entre a CDN e sua origem
* Reformatação de respostas de APIs de terceiros (e talvez agregação de várias respostas de API) antes de entregá-las ao navegador
* Compor e servir HTML renderizado pelo servidor na borda usando conteúdo compilado de vários back-ends
* Expor um servidor MCP para LLMs como ChatGPT e Claude para acessar ferramentas personalizadas

Temos um número limitado de oportunidades disponíveis para projetos do AEM Publish Delivery ou do Edge Delivery Services para sites de produção em tempo real. Se você estiver interessado em participar ou quiser saber mais, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do seu caso de uso.

#### Solução de problemas do pipeline de configuração no nível da Web com o agente de desenvolvimento (Programa Beta) {#devagent-webtier}

Os recursos de [solução de problemas de pipeline](/help/ai-in-aem/agents/brand-experience/development/development.md) do Agente de Desenvolvimento ajudam os desenvolvedores a diagnosticar e resolver problemas de forma eficiente nas implantações do AEM as a Cloud Service. Além de oferecer suporte a pipelines de Empilhamento completo (Implantação e Qualidade de Código), o Agente de Desenvolvimento agora oferece suporte à solução de problemas do **Pipeline de configuração no nível da Web** como parte de um programa beta.

Para solicitar acesso ao beta, envie um email para [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com). É necessário acesso pré-existente aos Agentes no AEM.

#### Ferramentas de IA do IDE para AEM 6.5 para migração do AEM Cloud Service (Programa Alpha) {#cm-ide-migration}

Acelere sua migração do AEM 6.5 para o AEM as a Cloud Service (pilha Java) usando as ferramentas de IA do IDE para agir de acordo com as recomendações do [Relatório do Analisador de práticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

Envie um email para [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) para obter mais informações.

#### Autenticação do Edge para Edge Delivery Services (Programa Beta) {#edge-authentication}

A autenticação da Edge permite restringir o acesso às páginas do Edge Delivery Services somente àqueles que se autenticaram com seu provedor de identidade (IdP). Isso é feito implantando um arquivo YAML de configuração do OpenID Connect (OIDC).

Se estiver interessado, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do caso de uso e suas dúvidas.

#### Implantações de produção canária para testar o código antes de aceitar o tráfego direto (programa Beta) {#canary-beta}

Valide uma build de produção com tráfego de teste somente interno antes de expô-la aos usuários finais. Entregar para produção, rotear apenas tráfego canário (usando um cabeçalho especial), monitorar o comportamento e promover para tráfego ativo ou reverter, sem afetar os clientes.

Implante as versões de código para produção, mas restrinja-as somente ao tráfego de teste interno antes de decidir se aceita o tráfego ativo ou não.

Envie um email [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) para solicitar acesso e compartilhar feedback.

#### Instantâneos para RDEs (Programa Beta) {#rde-snapshot-program}

Na versão beta, os ambientes de desenvolvimento rápido (RDEs) agora oferecem suporte a um recurso para obter um instantâneo do estado atual do código e do conteúdo, que pode ser restaurado posteriormente. Isso pode ser útil ao sincronizar código que pode precisar ser revertido ou ao alternar entre o desenvolvimento de diferentes recursos. Também é possível restaurar apenas o conteúdo mutável como um ponto de partida conhecido para testes.

Envie um email para [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) se houver interesse em usar e fornecer feedback sobre este recurso.

#### APM (Application Performance Monitoring, monitoramento do desempenho de aplicativos) expandido (programa Alpha) {#apm-alpha}

Para fins de observação, o AEM Cloud Service oferece suporte atualmente ao [New Relic One](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) fornecido pela Adobe e ao [Dynatrace](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace) gerenciado pelo cliente. À medida que exploramos o suporte para opções adicionais de APM, envie um email para [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) com seu fornecedor ou tecnologia de preferência, juntamente com casos de uso.

## Guias do [!DNL Experience Manager] {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente do Adobe Experience Manager Guides [aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universal {#universal-editor}

Você pode encontrar uma lista completa de versões do Universal Editor [aqui](/help/release-notes/universal-editor/current.md).

## Gerar variações {#generate-variations}

Você pode encontrar uma lista completa de versões de Gerar Variações [aqui](/help/generative-ai/release-notes-generate-variations.md).

## Notas de versão da Experience Cloud {#experience-cloud}

Você pode encontrar informações sobre versões de outros aplicativos da Experience Cloud [aqui](https://experienceleague.adobe.com/pt-br/docs/release-notes/experience-cloud/current).
