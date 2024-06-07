---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 68e2f6867a2cbcaf52fa6de259fe118e31ee7573
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 10%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.5.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 30 de maio de 2024. O próximo lançamento de recursos (2024.6.0) está planejado para sexta-feira, 27 de junho de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo de visão geral da versão de maio de 2024, que exibe um resumo dos recursos adicionados na versão 2024.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no Sites {#sites-new-features}

#### Integração de tradução com o AEM {#translation-integration}

As ações e os fluxos de trabalho de tradução de conteúdo agora acionam eventos para permitir o rastreamento de etapas e estados de processo relevantes a partir de aplicativos externos. Os eventos a seguir estão sendo gerados. Os usuários poderão assinar eventos usando o Console do Adobe Developer.

* `TRANSLATION_JOB_CREATED`
* `TRANSLATION_JOB_CONTENT_ADDITION_STARTED`
* `TRANSLATION_JOB_CONTENT_ADDITION_COMPLETED`
* `TRANSLATION_JOB_CONTENT_DELETION_STARTED`
* `TRANSLATION_JOB_CONTENT_DELETION_COMPLETED`
* `TRANSLATION_JOB_COMMITTED_FOR_TRANSLATION`
* `TRANSLATION_JOB_READY_FOR_REVIEW`
* `TRANSLATION_JOB_APPROVED`
* `TRANSLATION_JOB_COMPLETED`
* `TRANSLATION_JOB_CANCELLED`
* `TRANSLATION_JOB_ERROR`

#### Serviço de dados de monitoramento de uso real (RUM) {#real-use-monitoring}

* **[O Serviço de dados de monitoramento de uso real (RUM) agora está disponível](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md)** permitindo a coleta de dados no lado do cliente para o AEM as a Cloud Service.
O serviço de monitoramento de uso real, a coleção do lado do cliente, oferece um reflexo mais preciso das interações, garantindo uma medida confiável do envolvimento do site. Ele permite que os clientes com insights avançados sobre o tráfego e o desempenho da página. É uma ótima oportunidade para saber mais sobre o desempenho da sua página e obter insights para melhorá-la.

#### Criação de AEM para Edge Delivery Services {#edge-enhancements}

Estabilidade aprimorada e várias melhorias para uma melhor experiência de criação.

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar variações**

Aproveite a GenAI por meio do novo recurso AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta do Adobe para consideração no programa.

**Navegação de ativos no Console de fragmentos de conteúdo**

Os autores de conteúdo agora podem navegar, visualizar e realizar ações em imagens e outros ativos sem precisar sair do Console de fragmentos de conteúdo.

![Navegação de ativos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Interessado em experimentar o recurso e compartilhar feedback? Envie um email para aemcs-headless-adopter@adobe.com a partir de sua ID de email oficial para saber mais sobre o programa dos participantes antecipados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na exibição do Administrador {#admin-view-new-features}

* WebM agora é um arquivo de saída compatível no perfil de processamento para vídeo.
* O MP4 agora é compatível com a integração nativa do AEM no Express (importação e exportação).

### Novos recursos na visualização de ativos {#assets-view-new-features}

**Publicar ativos no AEM e no Dynamic Media**

O Experience Manager Assets agora permite que você [publicar ativos no Experience Manager e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md) usando a visualização Assets sem alternar para a visualização Administração. Você pode publicar ativos ao fazer upload, navegar e pesquisar ativos.

![verificar status de publicação1](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Novos recursos de pré-lançamento no AEM Forms {#forms-new-prerelease-features}

#### Editor de regras visuais aprimorado para Forms adaptável baseado em componentes principais

Esta versão traz uma atualização significativa para o editor visual de regras para formulários adaptáveis com base em componentes principais. Agora você pode:

* Criar regras no editor de regras visuais para [substituir mensagens de sucesso/falha no envio do formulário padrão](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* No Editor de regras do Forms adaptável, foi adicionada a capacidade de [selecionar diferentes tipos de campos para a operação WHEN](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* Um autor de formulário agora pode aplicar funções personalizadas a [pré-processar dados antes do envio](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Use o [**Salvar como rascunho**](/help/forms/save-core-component-based-form-as-draft.md) funcionalidade para salvar formulários parcialmente preenchidos para envio posterior. Isso é útil em cenários nos quais os usuários precisam interromper o preenchimento de um formulário e retornar a ele posteriormente.



### Recursos iniciais do usuário no AEM Forms {#forms-new-early-adopter-features}

O programa AEM Forms Early Adoter Program oferece uma oportunidade única para você obter acesso exclusivo a inovações de ponta antes de qualquer outra pessoa e ajudar a moldar seu desenvolvimento.
O programa oferece acesso a várias inovações.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no âmbito do Early Adoter Program, consulte [Documentação do programa AEM Forms Early Adoter](/help/forms/early-adopter-ea-features.md).

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
> Se você estiver interessado em participar do nosso programa Early Adoter para qualquer inovação de Early Adoter, basta enviar um email do seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acesso. Você pode solicitar acesso a todas as inovações ou a qualquer inovação específica.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Suporte a credenciais de servidor para servidor do OAuth para integrações de AEM com outras soluções de Adobe {#S2S-OAuth-credentials}

O Console do Adobe Developer é usado para gerar credenciais para acessar várias APIs. Um desses tipos de credenciais, as credenciais da Conta de serviço (JWT), foi descontinuado em favor das credenciais de servidor para servidor do OAuth, que a AEM Cloud Service agora oferece suporte para integrações com outras soluções de Adobe, como Adobe Analytics e Adobe Target.

[Leia sobre a descontinuação](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md) e [saiba como usar a interface do autor do AEM](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) para configurar integrações com outras soluções Adobe.

### Pico de tráfego em alertas de origem {#traffic-spike-origin}

[Receber notificações proativas](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert) por meio do Centro de ações, quando os padrões de tráfego na origem indicarem um ataque de DDoS, permitindo investigar e configurar regras de filtro de tráfego.

### Novos recursos para RDEs {#RDE-new-features}

[RDEs (Rapid Development Environments, ambientes de desenvolvimento rápido)](/help/implementing/developing/introduction/rapid-development-environments.md) Permita que os desenvolvedores implantem, revisem e testem rapidamente as alterações na nuvem. Vários novos recursos serão lançados durante o mês de junho. Também convidamos você a se envolver diretamente com a engenharia de Adobe no [Canal de Discórdia RDE](https://discord.com/channels/1131492224371277874/1245304281184079872).


#### Suporte RDE para código front-end usando temas de site e modelos de site {#rde-frontend}

[Os RDEs agora oferecem suporte ao código front-end](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) baseado em [temas de site](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelos de site](/help/sites-cloud/administering/site-creation/site-templates.md), para os participantes iniciais. Com RDEs, isso é feito usando uma diretiva de linha de comando, em vez de uma [pipeline de front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md).

#### Logon aprimorado para RDEs {#rde-logging}

Ao depurar o código em um RDE, os desenvolvedores agora podem [configure e transmita logs com mais produtividade](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging), usando a linha de comando e sem modificar as propriedades OSGI no controle de versão. Os recursos incluem:

* declaração de níveis de log em um nível por pacote ou classe
* personalização do formato de saída de log
* transmissão de vários logs em paralelo

#### Aprimoramentos da CLI do RDE {#rde-cli-enhancements}

A interface de linha de comando do RDE tem alguns novos recursos que melhoram a experiência do desenvolvedor:

* [o comando setup é interativo](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive), facilitando a escolha entre organizações, programas e ambientes. Agora também é possível substituir esses valores na linha de comando.
* [modo silencioso](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) para uma saída menos detalhada.
* [modo json](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) para obter uma saída útil quando invocada programaticamente.

### Novas notificações da Central de Ações {#actions-center-notifications}

[Centro de ações](/help/operations/actions-center.md) O envia notificações por email quando ocorrem incidentes importantes ou se observarmos algo sobre seu código ou configuração, onde você deve tomar medidas proativas. Existem três novos tipos de notificações:

* muitas conexões de saída por meio de uma infraestrutura de rede avançada
* uso de um formato obsoleto de Mapeamento de usuário de serviço
* um possível ataque de DDoS está em andamento

### Programas de adoção antecipada {#foundation-early-adopter}

E-mail **<aemcs-cdn-config-adopter@adobe.com>**, indicando em qual dos programas de primeiros usuários abaixo você está interessado.

#### Limpar conteúdo na CDN com uma chave de API de autoatendimento (Early Adoter Program, Programa de adoção antecipada) {#purge-cdn}

Registre uma chave de API de limpeza de CDN de forma automatizada e use-a para invalidar o conteúdo na CDN, seja globalmente ou para um ou mais recursos. [Saiba mais](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Criação de autoatendimento de X-AEM-Edge-Key para CDN gerenciado pelo cliente (BYOCDN) (Early Adoter Program) {#byocdn-keys}

Anteriormente, um tíquete de suporte era necessário para gerar o X-AEM-Edge-Key necessário para a configuração de um CDN gerenciado pelo cliente. Isso agora pode ser feito de forma automatizada por meio de um arquivo de configuração implantado usando o pipeline de configuração, removendo qualquer atraso na integração de um novo ambiente. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Redirecionamentos do lado do cliente (Programa de primeiros usuários) {#client-side-redirects-early-adopter}

Configure os redirecionamentos do lado do cliente 301/302 no controle do código-fonte e implante na CDN. [Saiba mais](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Observe que há vários outros recursos já disponíveis relacionados ao [Configuração da CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), incluindo transformações de solicitação e resposta, e roteamento de tráfego para sites fora do AEM.

#### Alertas de regras de filtro de tráfego (Programa de adoção antecipada) {#traffic-filter-rules-alerts-early-adopter}

O recém-lançado [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md), que incluem as regras opcionalmente licenciáveis do Web Application Firewall (WAF), permite configurar o tráfego que deve ser permitido ou negado.

Participe do programa de adoção antecipada para que você possa ser alertado sempre que as regras de filtro de tráfego forem acionadas. As notificações por email do Centro de ações manterão você informado quando ocorrerem determinadas condições de tráfego para que você possa tomar as medidas apropriadas.

#### Usuários empresariais podem declarar redirecionamentos fora do Git (Early Adoter Program, Programa de adoção antecipada) {#apache-rewritemaps-early-adopter}

Semelhante ao AEM 6.5, o Apache/Dispatcher assimilará mapas de regravação colocados em um local específico no repositório de publicação e os carregará, sem exigir uma execução de pipeline no nível da Web. Isso abre oportunidades para que um usuário empresarial declare redirecionamentos usando uma planilha ou uma interface do usuário, como a oferecida pelo ACS Commons Redirect Map Manager ou criada como parte de um aplicativo do cliente. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) para o carregamento de conteúdo dinâmico (Early Adoter Program) {#esi-early-adopter}

O CDN gerenciado por Adobe agora é compatível [ESI (Edge Side Includes)](/help/implementing/dispatcher/edge-side-includes.md), uma linguagem de marcação para a montagem de conteúdo dinâmico da Web no nível da borda. Ao incluir trechos ESI, você pode armazenar em cache a página de HTML geral na CDN com TTLs mais altos, enquanto busca com mais frequência a partir da origem as seções menores que exigem atualizações de cadência mais altas (TTLs mais baixos). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] Guias {#guides}

* **Publicar um tópico ou seus elementos em um fragmento de experiência**
Agora, os Guias de Experience Manager permitem publicar um tópico ou seus elementos em um Fragmento de experiência. Um Fragmento de experiência é uma unidade de conteúdo modular que integra conteúdo e layout.  Fragmentos de experiência são instrumentais e podem ajudar você a criar experiências consistentes e envolventes.
* **Capacidade de transmitir os metadados de ativo de tópico para saída de PDF nativo**
Você pode adicionar os metadados do ativo do tópico enquanto gera a saída de PDF nativo. Esse recurso ajuda você a adicionar metadados específicos para diferentes tópicos, como o título do tópico e o autor, aos cabeçalhos e rodapés da página de tópico.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos na versão, consulte o [Roteiro de versão dos Guias do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Notas de versão da Experience Cloud {#experience-cloud}

Você pode encontrar informações sobre lançamentos de outros aplicativos Experience Cloud [aqui](https://experienceleague.adobe.com/pt-br/docs/release-notes/experience-cloud/current).
Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine o [Atualização de produtos prioritários para o Adobe](https://www.adobe.com/subscription/priority-product-update.html).
