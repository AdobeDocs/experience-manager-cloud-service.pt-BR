---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service
description: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 1c5cbed1ea9e8beda14ed3c66f14a446941cd9cf
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 7%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2023 ou 2024.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2026.1.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 29 de janeiro de 2026. O próximo lançamento de recursos (2026.2.0) está planejado para sexta-feira, 26 de fevereiro de 2026.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## Programas do AEM Beta {#aem-beta-programs}

Os programas beta do Adobe Experience Manager (AEM) são uma maneira de os clientes obterem acesso a recursos e código de pré-lançamento, fornecerem feedback e guiarem o futuro do AEM.

>[!IMPORTANT]
>
>As versões do Beta podem conter defeitos e são fornecidas &quot;NO ESTADO EM QUE SE ENCONTRAM&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte (por meio dos Serviços de suporte da Adobe ou de outra forma) às versões beta. A Adobe recomenda que os clientes tenham cuidado e não dependam do funcionamento ou do desempenho correto das versões beta, nem de qualquer documentação ou material que as acompanhe. Os recursos e as APIs na versão beta estão sujeitos a alterações sem aviso prévio. Portanto, qualquer uso das versões beta é de inteira responsabilidade do cliente.

**Vantagens de participar**
Obter acesso antecipado aos recursos que a Adobe está desenvolvendo permite que clientes e parceiros forneçam feedback e modelem o desenvolvimento de produtos. Também os ajuda a se preparar para adotar novos recursos antes da disponibilidade geral.

**Programas beta atuais**
As seções a seguir listam os programas beta e Explorer ativos.

### Agentes no AEM (programa Explorer) {#agents-in-aem-beta-program}

Obter acesso antecipado a novos e eficientes recursos agenciais da AEM em produção, governança, otimização, descoberta e desenvolvimento. Seus comentários moldam diretamente o roteiro e os recursos finais do Adobe. Consulte [Visão geral dos agentes no AEM](/help/ai-in-aem/agents/overview.md) para saber mais.

Esse programa normalmente dura de 4 a 6 semanas, mas pode ser personalizado para ser flexível em relação à sua capacidade de participar ativamente.

Para participar deste programa, envie um email para [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) e inclua os seguintes detalhes na medida do possível:

* Nomes e membros da equipe da Adobe ID que usarão agentes ativamente.
* Liste os agentes específicos que você ou sua equipe desejarão usar. Ou simplesmente diga &quot;Todos os Agentes&quot;.

Os clientes selecionados para participação serão notificados diretamente pela Adobe. A participação está sujeita a considerações de qualificação, incluindo licenciamento de clientes e capacidade limitada do programa. Embora nem todas as solicitações possam ser acomodadas inicialmente, clientes adicionais podem ser considerados em ondas beta futuras.

### AEM Foundation (programas do Beta) {#aem-foundation-beta-programs}

Consulte [programas beta do AEM Foundation](#foundation-early-adopter).

### Cloud Manager (programas do Beta) {#cloud-manager-beta-programs}

Consulte [programas beta do Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Servidor MCP de conteúdo {#content-MCP}

O AEM Cloud Service agora inclui **Servidores MCP de conteúdo**, fornecendo uma maneira padronizada para experiências alimentadas por IA funcionarem com conteúdo do AEM por meio de ferramentas compatíveis com MCP.

Desenvolvedores e usuários avançados trabalhando em aplicativos de bate-papo e plataformas de agentes podem conectar o AEM a compilações e automações personalizadas, de modo que o trabalho de conteúdo se torne parte dos fluxos de trabalho comerciais completos.

A AEM fornece dois servidores:

1. **Servidor MCP de Conteúdo Somente Leitura** - para recuperar conteúdo com segurança
1. **Servidor MCP de Conteúdo de Leitura/Gravação** - para fazer alterações no conteúdo

Esses servidores MCP incluem ferramentas para trabalhar com **Páginas**, **Fragmentos de Conteúdo** e **Assets**, e podem ser usados a partir dos seguintes clientes MCP: **ChatGPT**, **Claude**, **Cursor** e **Microsoft Copilot Studio**.

Saiba mais em [Uso do MCP com o AEM Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md). Para perguntas ou comentários, envie um email para [aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Pesquisa com IA**

A pesquisa com IA apresenta uma experiência de pesquisa inteligente e com reconhecimento de contexto que vai além da correspondência tradicional de palavras-chave, entendendo o significado e a intenção por trás das consultas do usuário. Alimentado por IA e aprendizado de máquina, ele fornece resultados mais precisos mesmo quando as consultas são redigidas de forma diferente, contêm erros ortográficos, usam sinônimos ou são enviadas em idiomas diferentes, ajudando os usuários a encontrar conteúdo relevante mais rapidamente com menos esforço.

Para obter mais informações, consulte Pesquisa com IA em [modo de exibição do Assets](/help/assets/search-assets-view.md#ai-search) e [modo de exibição de Administrador](/help/assets/search-assets.md#ai-search).

**Versão 3.0.1 do Aplicativo de Desktop**

[Aplicativo de desktop 3.0.1 (20 de dezembro de 2025)](https://experienceleague.adobe.com/en/docs/experience-manager-desktop-app/using/release-notes) melhora a confiabilidade, o desempenho e a estabilidade em fluxos de trabalho importantes. Esta versão garante uma nomenclatura de pasta consistente, corrigindo problemas de sincronização com o AEM Author, permite o uso ininterrupto do aplicativo durante transferências ativas, melhora a capacidade de resposta da interface do usuário por meio de processamento assíncrono, otimiza transferências de arquivos grandes com paginação e resolve problemas de estabilidade, incluindo reinicializações e falhas do servidor do Author durante uploads e downloads de pastas grandes.

**Adobe Asset Link CEP versão 2026.01.0**

[O Adobe Asset Link CEP 2026.01.0](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) introduz uma nova opção para Vincular novamente os links ausentes no InDesign, que vincula automaticamente outros ativos ausentes da mesma pasta do AEM. O recurso corresponde a ativos com base no nome do arquivo, reduzindo significativamente o esforço manual ao restaurar links com falha.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

**Aprimoramentos no Espaço Reservado para Nota de Rodapé do Adaptive Forms (Componentes de Base)**

* Adição do [suporte a várias linhas com quebras de linha](/help/forms/footnotes-richtextsupport.md), permitindo uma apresentação mais clara e expressiva do conteúdo da nota de rodapé.
* As notas de rodapé agora permanecem persistentemente visíveis no espaço reservado para notas de rodapé, independentemente da visibilidade dos painéis associados, garantindo um acesso consistente às informações críticas.
  ![Descrição da Nota de Rodapé](/help/forms/assets/footnote-description.png){height=50%}

### Novos recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

**Recuperar valores de uma matriz JSON**

Recursos de função personalizada expandidos para [extrair valores de matrizes JSON](/help/forms/invoke-service-enhancements-rule-editor.md#retrieve-property-values-from-a-json-array), recebidos por meio de uma chamada de API, e vinculá-los diretamente aos campos de Formulário adaptável. Agora é possível desenvolver lógica e regras de negócios com mapeamento manual mínimo de dados.

**Executar a Interface do Usuário Associada em uma instância de Publicação**

Agora você pode executar a [Interface do Usuário para Associação](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md) diretamente nas instâncias de Publicação. Isso permite que seus agentes acessem a Interface do usuário do Associate e personalizem facilmente as comunicações com seus clientes.

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. 
-->

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Avisos importantes sobre a base [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation-notices}

#### Desaprovações da API Java {#java-api-deprecation}

As APIs obsoletas que direcionam a remoção de 26/02/2026 não devem mais ser usadas no código. Para evitar bloqueios de implantação, remova o uso da API antes de 26 de março de 2026. Datas importantes:

* **A partir de 26 de janeiro de 2026**: os emails de notificação da Central de Ações são enviados **semanalmente por ambiente** como um lembrete para remover o uso dessas APIs.
* **26 de fevereiro de 2026**: os pipelines do Cloud Manager que contêm código usando essas APIs **pausarão** durante a etapa **Qualidade do Código**. Um Gerente de implantação, Gerente de projeto ou Proprietário da empresa pode substituir o problema para permitir que o pipeline continue.
* **26 de março de 2026**: os pipelines de Cloud Manager que contêm código usando essas APIs **falharão** durante a etapa **Qualidade do Código**, **bloqueando implantações** de novos códigos até que o uso seja removido.
* **30 de abril de 2026**: os ambientes que ainda usam essas APIs podem **não receber mais atualizações críticas de versões do Adobe**.

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
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

#### Descontinuação do Java 11 Runtime {#java11-runtime-deprecation}

A Adobe atualizou os ambientes **Preparo** e **Produção** para o **tempo de execução do Java 21** de maior desempenho em 14 de outubro de 2025. A partir de **9 de fevereiro** (implantação gradual até 11 de fevereiro), o AEM Cloud Service SDK e qualquer ambiente de nuvem não funcionarão com o Java 11 runtime.

>[!NOTE]
>
> Para aproveitar as otimizações de desempenho e aprimoramentos de linguagem mais recentes, é recomendável criar com Java 17 ou Java 21 (preferencial). A construção com Java 8 e Java 11 permanece suportada por enquanto, mas será descontinuada em uma versão futura. Uma comunicação separada será emitida antes da desativação. Consulte a seção *requisitos de tempo de compilação* de [este artigo](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).
>

#### Aplicação da política de configuração de logs Java do AEM {#logconfig-policy}

Os registros Java da AEM devem seguir um formato padrão para garantir um monitoramento confiável em todos os ambientes do cliente. Configurações de log personalizadas — como alterações na formatação de log, arquivos de saída ou níveis de log padrão — não são mais suportadas. Os registros devem permanecer direcionados aos arquivos padrão e os níveis de registro padrão para o código de produto do AEM devem ser preservados. Veja todos os detalhes no [Artigo sobre log](/help/implementing/developing/introduction/logging.md#configuration-loggers).

Quaisquer substituições de log personalizado sem suporte *foram ignoradas*. A maioria dos clientes não foi afetada e a Adobe entrou em contato com clientes cuja configuração atual pode ser afetada.

Revise e atualize todos os processos downstream que dependem do comportamento de log personalizado. Por exemplo:

* Se o sistema de encaminhamento de registros esperar um formato de registro personalizado, talvez seja necessário ajustar as regras de assimilação.
* Se você tiver reduzido anteriormente a verbosidade dos registros alterando os níveis de registro, observe que reverter para os níveis padrão pode aumentar o volume de registro.

### Recursos do [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Early Adopter {#foundation-early-adopter}

#### Pausar Atualizações de Manutenção Automática {#pause-updates}

Dias de ativação, eventos ao vivo, pico de vendas — esses momentos não quebram. [Nossos novos recursos de autoatendimento](/help/implementing/deploying/quiet-hours-update-free-periods.md) interrompem as atualizações de manutenção automáticas quando é importante, para que suas equipes permaneçam focadas.

* Quiet Hours: bloqueia a manutenção automática durante os horários definidos a cada dia. Ideal para horas de trabalho, corridas noturnas ou cortes matinais.
* Período Livre de Atualização: Bloqueia a manutenção automática por uma semana inteira. Use-o para inicializações, promoções ou congelamentos anuais.

>[!NOTE]
>
>Disponível como um recurso de Disponibilidade limitada em 25 de setembro.
>Envie um email para [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) para ativá-lo em seus programas.
>

#### Funções do AEM Edge (Programa Beta) {#edge-functions}

As Funções do AEM Edge (referidas nas notas de versão anteriores como *Edge Computing*) permitem executar o JavaScript na camada CDN, aproximando o processamento de dados do usuário final. Isso reduz a latência e permite experiências responsivas e dinâmicas na borda.

Casos de uso comuns incluem:

* Personalização de conteúdo com base na geolocalização, tipo de dispositivo ou atributos do usuário
* Atuar como middleware entre a CDN e sua origem
* Reformatação de respostas de APIs de terceiros (e talvez agregação de várias respostas de API) antes de entregá-las ao navegador
* Compor e servir HTML renderizado pelo servidor na borda usando conteúdo compilado de vários back-ends
* Expor um servidor MCP para LLMs como ChatGPT e Claude para acessar ferramentas personalizadas

Temos um número limitado de oportunidades disponíveis para projetos do AEM Publish Delivery ou do Edge Delivery Services para sites de produção em tempo real. Se você estiver interessado em participar ou quiser saber mais, envie um email para [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com uma breve descrição do seu caso de uso.

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

#### Ferramentas de IA para IDEs para desenvolvimento em Java e Dispatcher do AEM (Programa Beta) {#ai-dev-beta}

As equipes de pilha em Java estão cada vez mais usando o desenvolvimento assistido por IA em ferramentas como Cursor, Claude Code, Visual Studio e IntelliJ para acelerar a entrega de recursos e melhorar a qualidade do código. Associe-se à versão beta para:

* Compartilhar experiências reais para ajudar a moldar futuros recursos de IA compatíveis com a Adobe
* Experimente as ferramentas do IDE que podem ser usadas pelos agentes de IA para gerar e depurar o código AEM e a configuração do Dispatcher

Envie um email para [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) para obter mais informações.

#### APM (Application Performance Monitoring, monitoramento do desempenho de aplicativos) expandido (programa Alpha) {#apm-alpha}

Para fins de observação, o AEM Cloud Service oferece suporte atualmente ao [New Relic One](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) fornecido pela Adobe e ao [Dynatrace](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace) gerenciado pelo cliente. À medida que exploramos o suporte para opções adicionais de APM, envie um email para [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) com seu fornecedor ou tecnologia de preferência, juntamente com casos de uso.

## Guias do [!DNL Experience Manager] {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente do Adobe Experience Manager Guides [aqui](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

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
