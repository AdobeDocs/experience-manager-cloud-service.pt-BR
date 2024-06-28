---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 19b52f733a592c7e84ba2e9d83d37e5e181f21ab
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 10%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2022 ou 2023.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.6.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 27 de junho de 2024. O próximo lançamento de recursos (2024.7.0) está planejado para sexta-feira, 25 de julho de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!--  ## Release Video {#release-video}

Have a look at the June 2024 Release Overview video for a summary of the features added in the 2024.6.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar variações**

Aproveite a GenAI por meio do novo recurso do AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta do Adobe para consideração no programa.

**Navegação de ativos no Console de fragmentos de conteúdo**

Os autores de conteúdo agora podem navegar, visualizar e realizar ações em imagens e outros ativos sem precisar sair do Console de fragmentos de conteúdo.

![Navegação de ativos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Interessado em experimentar o recurso e compartilhar feedback? Envie um email para aemcs-headless-adopter@adobe.com a partir de sua ID de email oficial para saber mais sobre o programa dos participantes antecipados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no Experience Manager Assets {#new-features-assets}

**Content Hub**

O Content Hub está disponível como parte do Experience Manager Assets as a Cloud Service para democratizar o acesso a conteúdo sobre a marca para organizações e seus parceiros de negócios. Com o Content Hub, você pode encontrar e distribuir ativos facilmente, reutilizar e criar novas variações na marca e acelerar a ativação em escala.

![Interface do usuário do Content Hub](/help/release-notes/assets/content-hub-ui.png)

**Dynamic Media com recursos OpenAPI**

O Dynamic Media com recursos OpenAPI estende o DAM aos aplicativos de Adobe e de terceiros, permitindo o acesso a ativos digitais aprovados pela marca, em qualquer canal, por meio do Seletor de ativos ou da pilha de OpenAPI. Princípios principais - sem cópias binárias, os ativos são otimizados e transformados na borda para desempenho rápido, fornecem ativos públicos ou seguros.

![Novo diagrama de fluxo de dados do Dynamic Media](/help/assets/assets/dm-openapi-dfd.png)


### Novos recursos na visualização de ativos {#assets-view-new-features}

**Mais opções disponíveis no painel Assets Insights**

A Contagem de ativos por tipo e tamanho de ativo agora está disponível no painel do Assets Insights. Essas opções fornecem dados em tempo real no ambiente de visualização do Assets sobre a contagem e a porcentagem de ativos por intervalo de tamanho e tipo de ativo.

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Novos recursos no AEM Forms {#forms-new-prerelease-features}

#### Editor de regras visuais aprimorado para Forms adaptável baseado em componentes principais

Esta versão traz uma atualização significativa para o editor visual de regras para formulários adaptáveis com base em componentes principais. Agora você pode:

* Criar regras no editor de regras visuais para [substituir as mensagens padrão de sucesso/falha no envio do formulário](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* No Editor de regras do Forms adaptável, foi adicionada a capacidade de [selecionar diferentes tipos de campos para a operação WHEN](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* Um autor de formulário agora pode aplicar funções personalizadas a [pré-processar dados antes do envio](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Use o [**Salvar como rascunho**](/help/forms/save-core-component-based-form-as-draft.md) funcionalidade para salvar formulários parcialmente preenchidos para envio posterior. Isso é útil em cenários nos quais os usuários precisam interromper o preenchimento de um formulário e retornar a ele posteriormente.

### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado do AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de ponta antes de qualquer outra pessoa e ajudar a moldar seu desenvolvimento. O programa oferece acesso a várias inovações.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa das inovações disponíveis no âmbito do programa de acesso antecipado, consulte [Documentação do Programa de acesso antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Métodos aprimorados de proteção de bot

A AEM Forms aprimorou seus recursos de segurança adicionando suporte para duas soluções populares do CAPTCHA: Cloud Turnstile e hCaptcha. Isso adiciona ao já disponível Google reCAPTCHA, fornecendo aos usuários mais opções e flexibilidade na proteção de seus formulários contra bots e envios de spam.

* **Cilindro de nuvens**: esse CAPTCHA sem atrito verifica os usuários por meio de um desafio simples que não requer interação explícita. Ele se integra perfeitamente aos seus formulários, melhorando a experiência do usuário.
* **Captcha**: esse CAPTCHA com foco na privacidade oferece uma alternativa simples, com foco na privacidade de dados. O objetivo é obter um equilíbrio entre a segurança e a experiência do usuário.
* **Google reCAPTCHA**: a AEM Forms continua a oferecer suporte ao reCAPTCHA v2 e ao reCAPTCHA Enterprise, oferecendo uma solução confiável e bem estabelecida.

Ao oferecer várias opções de CAPTCHA, a AEM Forms capacitou você a selecionar a solução que melhor se alinha às suas necessidades específicas.

Pronto para integrar qualquer uma dessas soluções CAPTCHA ao Adaptive Forms? Nossa documentação fornece instruções detalhadas para cada: [Cilindro de nuvens](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [Captcha](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components), e [Google reCAPTCHA](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Serviço do Forms

O serviço Forms gera PDF forms interativos para a captura de dados. Ele também pode ser usado para importar ou exportar dados de e para um formulário PDF interativo existente e validar os dados enviados. Veja um detalhamento de suas funcionalidades:

* **Renderização do Forms**: gere um formulário PDF interativo a partir de um modelo criado usando o AEM Forms Designer e, opcionalmente, dados XML. Isso produz essencialmente um formulário PDF preenchível opcionalmente pré-preenchido com dados.
* **Extração e importação de dados**: importe dados para um formulário PDF existente, bem como extraia dados de um formulário PDF preenchido. Os formatos de dados XDP e XML são compatíveis, e a importação para PDF forms não XFA (também conhecida como AcroForms) também é compatível com dados FDF e XFDF.
* **Validação de dados**: valide os dados enviados, no formato XDP ou XML, em relação a um modelo criado usando o AEM Forms Designer.

>[!IMPORTANT]
>
> Se você estiver interessado em participar do nosso Programa de acesso antecipado para qualquer inovação de acesso antecipado, basta enviar um email do seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acesso. Você pode solicitar acesso a todas as inovações ou a qualquer inovação específica.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Programa de adoção antecipada de notificações do Centro de ações relacionadas à integridade do conteúdo {#actions-center-notifications}

[Centro de ações](/help/operations/actions-center.md) O envia notificações por email quando ocorrem incidentes importantes ou se observarmos algo sobre seu código ou configuração, onde você deve tomar medidas proativas. Agora introduzimos vários novos tipos de notificações associados à integridade do conteúdo. Isso está disponível por meio de um programa de adoção antecipada. Para participar, entre em contato com o Atendimento ao cliente do Adobe.

#### As páginas contêm um grande número de nós {#page-nodes}

Um grande número de nós pode degradar o desempenho da renderização e reduzir o tempo de carregamento da página. Receba uma notificação proativa pelo Centro de ações quando um grande número de nós for detectado em uma página, permitindo que você siga as etapas necessárias para reduzir o número total de nós em uma página.

#### Grande número de instâncias de fluxo de trabalho em execução {#running-workflows}

O desempenho do mecanismo de fluxo de trabalho é afetado quando há um grande número de fluxos de trabalho em execução no ambiente de criação. Receba uma notificação proativa pelo Centro de Ações quando um grande número de instâncias de fluxos de trabalho em execução for detectado, permitindo configurar um trabalho de limpeza para encerrar fluxos de trabalho em execução que não sejam necessários.

#### Usuários adicionados diretamente aos grupos personalizados {#users-customgroups}

Receba uma notificação proativa pelo Centro de ações quando os usuários forem adicionados diretamente a grupos personalizados, permitindo que você siga as práticas recomendadas do IMS para adicionar usuários a grupos IMS relevantes e, em seguida, adicionar os grupos IMS como membros de grupos AEM.

#### Conteúdo JCR ausente {#jcr-content}

Receba uma notificação proativa pelo Centro de Ações quando o conteúdo JCR ausente for detectado, permitindo que você adicione o conteúdo JCR ausente e evite a falha de determinados recursos do AEM Assets.

#### Fluxos de trabalho concluídos não removidos {#workflows}

Receba uma notificação proativa por meio do Centro de ações quando os workflows concluídos por mais de 90 dias não tiverem sido removidos, permitindo melhorar o desempenho do mecanismo do workflow, minimizando o número de instâncias de workflows.

#### Recurso Sling ausente {#sling-resource}

Receba uma notificação proativa pelo Centro de ações quando um recurso Sling ausente for detectado, permitindo adicionar o recurso Sling ausente e evitar a falha de determinados recursos do AEM Assets.

### Programas dos primeiros usuários relacionados à entrega de conteúdo {#foundation-early-adopter}

E-mail **<aemcs-cdn-config-adopter@adobe.com>**, indicando em qual dos programas de primeiros usuários abaixo você está interessado.

#### Autenticação básica na CDN (Early Adoter Program, programa de primeiros usuários) {#basicauth-cdn}

Protect determinados recursos de conteúdo, exibindo uma caixa de diálogo de autenticação básica que requer um nome de usuário e senha. Esse recurso destina-se principalmente a casos de uso de autenticação simples, como a análise de conteúdo pelas partes interessadas, e não como uma solução completa para os direitos de acesso do usuário final. A lista de nomes de usuário e senhas é gerenciada por meio de um arquivo de configuração no Git, que é implantado por meio do Pipeline de configuração, com uma referência às variáveis de ambiente do Cloud Manager do tipo secreto. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Limpar conteúdo na CDN com uma chave de API de autoatendimento (Early Adoter Program, Programa de adoção antecipada) {#purge-cdn}

Registre uma chave de API de limpeza de CDN de forma automatizada e use-a para invalidar o conteúdo na CDN, seja globalmente ou para um ou mais recursos. [Saiba mais](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Criação de autoatendimento do X-AEM-Edge-Key para CDN gerenciado pelo cliente (BYOCDN) (programa Early Adoter) {#byocdn-keys}

Anteriormente, um tíquete de suporte era necessário para gerar a X-AEM-Edge-Key necessária para a configuração de um CDN gerenciado pelo cliente. Isso agora pode ser feito de forma automatizada por meio de um arquivo de configuração implantado usando o pipeline de configuração, removendo qualquer atraso na integração de um novo ambiente. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Redirecionamentos do lado do cliente (programa de primeiros usuários) {#client-side-redirects-early-adopter}

Configure os redirecionamentos do lado do cliente 301/302 no controle do código-fonte e implante na CDN. [Saiba mais](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Observe que há vários outros recursos já disponíveis relacionados ao [Configuração da CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), incluindo transformações de solicitação e resposta, e roteamento de tráfego para sites fora do AEM.

#### Alertas de regras de filtro de tráfego (Programa de adoção antecipada) {#traffic-filter-rules-alerts-early-adopter}

O recém-lançado [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md), que incluem as regras opcionalmente licenciáveis do Web Application Firewall (WAF), permite configurar o tráfego que deve ser permitido ou negado.

Participe do programa de adoção antecipada para que você possa ser alertado sempre que as regras de filtro de tráfego forem acionadas. As notificações por email do Centro de ações manterão você informado quando ocorrerem determinadas condições de tráfego para que você possa tomar as medidas apropriadas.

#### Usuários empresariais podem declarar redirecionamentos fora do Git (Early Adoter Program, Programa de primeiros usuários) {#apache-rewritemaps-early-adopter}

Semelhante ao AEM 6.5, o Apache/Dispatcher assimilará mapas de regravação colocados em um local específico no repositório de publicação e os carregará, sem exigir uma execução de pipeline no nível da Web. Isso abre oportunidades para que um usuário empresarial declare redirecionamentos usando uma planilha ou uma interface do usuário, como a oferecida pelo ACS Commons Redirect Map Manager ou criada como parte de um aplicativo do cliente. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### O Edge Side Includes (ESI) para Carregar Conteúdo Dinâmico (Early Adoter Program) {#esi-early-adopter}

O CDN gerenciado por Adobe agora é compatível [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), uma linguagem de marcação para a montagem de conteúdo dinâmico da Web no nível da borda. Ao incluir trechos ESI, você pode armazenar em cache a página de HTML geral na CDN com TTLs mais altos, enquanto busca com mais frequência a partir da origem as seções menores que exigem atualizações de cadência mais altas (TTLs mais baixos). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] Guias {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente do Adobe Experience Manager Guides [aqui](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Notas de versão da Experience Cloud {#experience-cloud}

Você pode encontrar informações sobre lançamentos de outros aplicativos Experience Cloud [aqui](https://experienceleague.adobe.com/pt-br/docs/release-notes/experience-cloud/current).
Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine o [Atualização de produtos prioritários para o Adobe](https://www.adobe.com/subscription/priority-product-update.html).
