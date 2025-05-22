---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.6.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.6.0.
feature: Release Information
role: Admin
exl-id: 4033abf4-7094-4ce4-ba93-c936062667e3
source-git-commit: 0f5fc5469034139a45ec0fe7e30319012af97301
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 10%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2024.6.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2024.6.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2022 ou 2023.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.6.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 27 de junho de 2024. O próximo lançamento de recursos (2024.7.0) está planejado para sexta-feira, 25 de julho de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo de visão geral da versão de junho de 2024 para ver um resumo dos recursos adicionados na versão 2024.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/3430779?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novo recurso no Experience Manager Sites {#new-feature-sites}

**Serviço de Dados de Telemetria Operacional** {#real-use-monitoring}

O [Serviço de Telemetria Operacional](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) agora está disponível, permitindo a coleta de dados do lado do cliente para o AEM as a Cloud Service. Esse serviço oferece um reflexo mais preciso das interações do usuário, garantindo uma medida confiável do engajamento do site. Ele oferece aos clientes insights avançados sobre o tráfego e o desempenho da página, apresentando uma oportunidade valiosa para entender e aprimorar o desempenho da página.

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar Variações**

Aproveite a GenAI por meio do novo recurso do AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta da Adobe para consideração no programa.

**Navegação de ativos no Console de Fragmentos de Conteúdo**

Os autores de conteúdo agora podem navegar, visualizar e realizar ações em imagens e outros ativos sem precisar sair do Console de fragmentos de conteúdo.

![Navegação de ativos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Interessado em experimentar o recurso e compartilhar feedback? Envie um email para aemcs-headless-adopter@adobe.com a partir de sua ID de email oficial para saber mais sobre o programa dos participantes antecipados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no Experience Manager Assets {#new-features-assets}



**Centro de conteúdo**

O Content Hub está disponível como parte do Experience Manager Assets as a Cloud Service para democratizar o acesso a conteúdo sobre a marca para organizações e seus parceiros de negócios. Com o Content Hub, você pode encontrar e distribuir ativos facilmente, reutilizar e criar novas variações na marca e acelerar a ativação em escala.

![Interface de usuário do Content Hub](/help/release-notes/assets/content-hub-ui.png)

**Dynamic Media com recursos OpenAPI**

O Dynamic Media com recursos de OpenAPI estende o DAM a aplicativos da Adobe e de terceiros, permitindo o acesso a ativos digitais aprovados pela marca, em qualquer canal, por meio do Seletor de ativos ou da pilha de OpenAPI. Princípios principais - sem cópias binárias, os ativos são otimizados e transformados na borda para desempenho rápido, fornecem ativos públicos ou seguros.

![Novo diagrama de fluxo de dados do Dynamic Media](/help/assets/assets/dm-openapi-dfd.png)


### Novos recursos na visualização de ativos {#assets-view-new-features}

**Mais opções estão disponíveis no painel do Assets Insights**

A Contagem de ativos por tipo e tamanho de ativo agora está disponível no painel do Assets Insights. Essas opções fornecem dados em tempo real no ambiente de visualização do Assets. Eles detalham a contagem e a porcentagem de ativos por intervalo de tamanho e tipo de ativo.

**Atualizações para o editor Adobe Express inserido**

* Experiência do usuário aprimorada para salvar como um novo ativo em vez de salvar como uma nova versão.

* Exportação de documentos do Express de várias páginas (anteriormente, apenas uma página era suportada) nos formatos PDF de várias páginas e imagem. A seleção de formatos de imagem salva cada página como um ativo distinto no DAM para distribuição downstream.

* Suporte para adicionar metadados na caixa de diálogo Salvar ao salvar um ativo.

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

Esta versão traz uma atualização significativa ao Editor de regras visuais para formulários adaptáveis com base em componentes principais. Agora você pode:

* Crie regras no Editor de Regras Visuais para [substituir as mensagens de êxito/falha do envio de formulário padrão](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* No Editor de regras do Forms adaptável, foi adicionada a capacidade de [selecionar diferentes tipos de campos para a operação WHEN](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* Um autor de formulário agora pode aplicar funções personalizadas a [pré-processar dados antes do envio](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Use a funcionalidade [**Salvar como Rascunho**](/help/forms/save-core-component-based-form-as-draft.md) para salvar formulários parcialmente concluídos para envio posterior. Essa funcionalidade é útil em cenários em que os usuários precisam interromper o preenchimento de um formulário e retornar a ele posteriormente.

### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado do AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de ponta antes de qualquer outra pessoa e ajudar a moldar seu desenvolvimento. O programa oferece acesso a várias inovações.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Métodos aprimorados de proteção de bot

A AEM Forms aprimorou seus recursos de segurança adicionando suporte para duas soluções populares do CAPTCHA: Cloud Turnstile e hCaptcha. Essa funcionalidade complementa o Google reCAPTCHA existente, oferecendo aos usuários opções adicionais. Ele aumenta a flexibilidade na proteção de seus formulários contra bots e envios de spam.

* **Borboleta da Nuvem**: este CAPTCHA sem atrito verifica os usuários através de um desafio simples que não requer interação explícita. Ele se integra perfeitamente aos seus formulários, melhorando a experiência do usuário.
* **hCaptcha**: este CAPTCHA com foco na privacidade oferece uma alternativa simples com foco na privacidade de dados. O objetivo é obter um equilíbrio entre a segurança e a experiência do usuário.
* **Google reCAPTCHA**: a AEM Forms continua a oferecer suporte ao reCAPTCHA v2 e ao reCAPTCHA Enterprise, oferecendo uma solução confiável e bem estabelecida.

Ao oferecer várias opções de CAPTCHA, a AEM Forms capacitou você a selecionar a solução que melhor se alinha às suas necessidades específicas.

Pronto para integrar qualquer uma dessas soluções CAPTCHA ao Adaptive Forms? A documentação do Adobe fornece instruções detalhadas para cada: [Turnstile de Cloudflare](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [hCaptcha](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components) e [Google reCAPTCHA](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Serviço do Forms

O serviço do Forms gera PDF forms interativo para captura de dados. Ele também pode ser usado para importar ou exportar dados de e para um formulário interativo existente do PDF e validar os dados enviados. Veja um detalhamento de suas funcionalidades:

* **Renderização do Forms**: gere um formulário interativo do PDF a partir de um modelo criado com o AEM Forms Designer e, opcionalmente, dados XML. Essa funcionalidade produz um formulário do PDF preenchível opcionalmente pré-preenchido com dados.
* **Extração e Importação de Dados**: importe dados para um formulário existente do PDF, bem como extraia dados de um formulário preenchido do PDF. Os formatos de dados XDP e XML são compatíveis, e a importação para PDF forms não XFA (também conhecida como AcroForms) também é compatível com dados FDF e XFDF.
* **Validação de Dados**: valide os dados enviados, no formato XDP ou XML, em relação a um modelo criado com o AEM Forms Designer.

>[!IMPORTANT]
>
> Se você estiver interessado em participar do Programa de Acesso Antecipado da Adobe para qualquer inovação de acesso antecipado, basta enviar um email de seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acesso. Você pode solicitar acesso a todas as inovações ou a qualquer inovação específica.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Programa de adoção antecipada de notificações do Centro de ações relacionadas à integridade do conteúdo {#actions-center-notifications}

A [Central de Ações](/help/operations/actions-center.md) envia notificações por email quando ocorrem incidentes importantes, ou se algo for notado sobre seu código ou configuração, onde você deve tomar medidas pró-ativas. O Adobe agora introduziu vários novos tipos de notificações associados à integridade do conteúdo. Esse recurso está disponível por meio de um programa de adoção antecipada. Para participar, entre em contato com o Atendimento ao cliente da Adobe.

#### As páginas contêm um grande número de nós {#page-nodes}

Um grande número de nós pode degradar o desempenho da renderização e reduzir o tempo de carregamento da página. Receba uma notificação proativa pelo Centro de ações quando um grande número de nós for detectado em uma página, permitindo que você siga as etapas necessárias para reduzir o número total de nós em uma página.

#### Grande número de instâncias de fluxo de trabalho em execução {#running-workflows}

O desempenho do mecanismo de fluxo de trabalho é afetado quando há um grande número de fluxos de trabalho em execução no ambiente de criação. Você recebe uma notificação proativa por meio do Centro de ações quando um grande número de instâncias de fluxo de trabalho em execução é detectado. Esse processo permite configurar um trabalho de limpeza para encerrar fluxos de trabalho em execução desnecessários.

#### Usuários adicionados diretamente aos grupos personalizados {#users-customgroups}

Você recebe uma notificação proativa por meio do Centro de ações quando os usuários são adicionados diretamente aos grupos personalizados. Esse processo permite seguir as práticas recomendadas do IMS adicionando usuários aos grupos IMS relevantes e, em seguida, incluindo esses grupos IMS como membros de grupos AEM.

#### Conteúdo JCR ausente {#jcr-content}

O Centro de ações o notifica proativamente quando conteúdo JCR ausente é detectado. Essa abordagem permite adicionar o conteúdo ausente e evitar a falha de determinados recursos do AEM Assets.

#### Fluxos de trabalho concluídos não removidos {#workflows}

O Centro de ações notifica proativamente quando workflows concluídos há mais de 90 dias não foram removidos. Essa abordagem ajuda a melhorar o desempenho do mecanismo de fluxo de trabalho, reduzindo o número de instâncias de fluxo de trabalho.

#### Recurso Sling ausente {#sling-resource}

O Centro de ações envia uma notificação proativa quando um recurso Sling ausente é detectado. Essa abordagem permite adicionar o recurso ausente e evitar a falha de determinados recursos do AEM Assets.

### Programas dos primeiros usuários relacionados à entrega de conteúdo {#foundation-early-adopter}

Email **<aemcs-cdn-config-adopter@adobe.com>**, indicando em qual dos primeiros programas abaixo você está interessado.

#### Autenticação básica na CDN (Early Adoter Program, programa de primeiros usuários) {#basicauth-cdn}

Proteja determinados recursos de conteúdo abrindo uma caixa de diálogo de autenticação básica que requer um nome de usuário e senha. Esse recurso destina-se principalmente a casos de uso de autenticação simples, como partes interessadas de negócios que revisam o conteúdo, em vez de servir como uma solução abrangente para os direitos de acesso do usuário final. A lista de nomes de usuário e senhas é gerenciada por meio de um arquivo de configuração no Git, que é implantado por meio do Pipeline de configuração, com uma referência às variáveis de ambiente do Cloud Manager do tipo secreto. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Limpar conteúdo na CDN com uma chave de API de autoatendimento (Early Adoter Program, Programa de adoção antecipada) {#purge-cdn}

Registre uma chave de API de limpeza de CDN de forma automatizada e use-a para invalidar o conteúdo na CDN, seja globalmente ou para um ou mais recursos. [Saiba mais](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Criação de autoatendimento do X-AEM-Edge-Key para CDN gerenciado pelo cliente (BYOCDN) (programa Early Adoter) {#byocdn-keys}

Anteriormente, um tíquete de suporte era necessário para gerar a X-AEM-Edge-Key necessária para a configuração de um CDN gerenciado pelo cliente. Esse resultado agora pode ser obtido de maneira automatizada por meio de um arquivo de configuração implantado usando o pipeline de configuração, removendo qualquer atraso na integração de um novo ambiente. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Redirecionamentos do lado do servidor (programa de primeiros usuários) {#server-side-redirects-early-adopter}

Configure os redirecionamentos do lado do servidor 301/302 no controle do código-fonte e implante na CDN. [Saiba mais](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Observe que há vários outros recursos já disponíveis relacionados à [configuração de CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), incluindo transformações de solicitação e resposta e o roteamento de tráfego para sites fora do AEM.

#### Alertas de regras de filtro de tráfego (Programa de adoção antecipada) {#traffic-filter-rules-alerts-early-adopter}

As [Regras de Filtro de Tráfego](/help/security/traffic-filter-rules-including-waf.md) recém-lançadas, que incluem as regras do WAF (Firewall de Aplicativo Web) opcionalmente licenciáveis, permitem que você configure qual tráfego deve ser permitido ou negado.

Participe do programa de adoção antecipada para que você possa ser alertado sempre que as regras de filtro de tráfego forem acionadas. As notificações por email do Centro de ações mantêm você informado quando ocorrem determinadas condições de tráfego para que você possa tomar as medidas apropriadas.

#### Usuários empresariais podem declarar redirecionamentos fora do Git (Early Adoter Program, Programa de primeiros usuários) {#apache-rewritemaps-early-adopter}

Semelhante ao AEM 6.5, o Apache/Dispatcher assimila mapas de regravação colocados em um local específico no repositório de publicação e os carrega, sem exigir uma execução de pipeline no nível da Web. Essa abordagem permite que os usuários empresariais declarem redirecionamentos usando uma planilha ou interface do usuário, como o ACS Commons Redirect Map Manager ou um aplicativo personalizado. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### O Edge Side Includes (ESI) para Carregar Conteúdo Dinâmico (Early Adoter Program) {#esi-early-adopter}

A CDN Gerenciada pelo Adobe agora oferece suporte a [ESI (Edge Side Includes)](/help/implementing/dispatcher/edge-side-includes.md), uma linguagem de marcação para o assembly de conteúdo dinâmico da Web no nível da borda. Ao incluir trechos ESI, você pode armazenar em cache a página geral do HTML na CDN com TTLs mais altos, enquanto busca com mais frequência a partir da origem as seções menores que exigem atualizações de cadência mais altas (TTLs mais baixos). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

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
