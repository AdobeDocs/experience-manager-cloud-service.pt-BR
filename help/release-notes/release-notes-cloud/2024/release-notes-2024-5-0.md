---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.5.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.5.0.
feature: Release Information
role: Admin
exl-id: 7b7a27f9-ba57-4eb2-9fcb-653b5213af04
source-git-commit: a8c74573134597e83c2720de3b2a0f75ff7896a2
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 11%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2024.5.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2024.5.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2022 ou 2023.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.5.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 30 de maio de 2024. O próximo lançamento de recursos (2024.6.0) está planejado para sexta-feira, 27 de junho de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo de visão geral da versão de maio de 2024, que exibe um resumo dos recursos adicionados na versão 2024.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no Sites {#sites-new-features}

#### Integração de tradução AEM {#translation-integration}

Ações e workflows de tradução de conteúdo agora acionam eventos para permitir rastreamento etapas de processo relevantes e estados de aplicativos externos. Os seguintes eventos estão sendo gerados. Os usuários poderão se inscrever em eventos usando a Adobe Developer Console.

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

* **[O Serviço de Dados de Monitoramento de Uso Real (RUM) agora está em disponibilidade geral](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**, permitindo a coleta de dados no lado do cliente para o AEM as a Cloud Service.
O serviço de monitoramento de uso real, a coleção do lado do cliente, oferece um reflexo mais preciso das interações, garantindo uma medida confiável do envolvimento do site. Ele permite que os clientes com insights avançados sobre o tráfego e o desempenho da página. É uma ótima oportunidade para saber mais sobre o desempenho da sua página e obter insights para melhorá-la.

#### Criação no AEM para Edge Delivery Services {#edge-enhancements}

Aprimoramentos na estabilidade e em vários aprimoramentos para um melhor experiência de criação.

### Programa de primeiros adotantes {#sites-early-adopter}

**Gerar variações**

Aproveite o GenAI por meio do novo recurso da AEM, [gere variações](/help/generative-ai/generate-variations.md), acessível agora em Cloud Service. A geração de variações ajuda a gerar e dimensionar conteúdo criação por meio do uso de IA generativa. Entre em contato com o Adobe Systems conta conta equipe para obter consideração no programa.

**Navegação de ativos no Console de fragmento do conteúdo**

Os autores de conteúdo agora podem navegar, visualização e realizar ações em imagens e em outras ativos sem precisar sair do Console de fragmentos de conteúdo.

![Navegação de ativos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Interessado em experimentar o recurso e compartilhar feedback? Envie um e-mail para aemcs-headless-adopter@adobe.com da sua ID de email oficial para saber mais sobre o programa do adotador precoce.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novo recursos no Admin visualização {#admin-view-new-features}

* O WebM agora é um arquivo de saída compatível no processamento de perfil para vídeo.
* O MP4 agora é compatível com a integração nativa do AEM no Express (importação e exportação).

### Novos recursos na visualização de ativos {#assets-view-new-features}

**Publicar ativos no AEM e no Dynamic Media**

O Experience Manager Assets agora permite que você [publique ativos no Experience Manager e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md) rapidamente usando a exibição do Assets sem alternar para a exibição do Administrador. Você pode publicar ativos ao fazer upload, navegar e pesquisar ativos.

![verificar publicar status1](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Novo recursos de pré-lançamento no AEM Forms {#forms-new-prerelease-features}

#### Aprimoramento do editor da regra visual para as Componente adaptativas principais baseadas em Forms

Esta versão traz uma atualização significativa para o visual regra editor para formulários adaptáveis com base nos componentes principais. Agora você pode:

* Criar regras na Regra visual editor para [substituir as mensagens](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers) de sucesso/falha do envio de formulário padrão.

* No editor Adaptive Forms Rule, foi adicionada a [capacidade de selecionar tipos diferentes de campos para a operação](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when) WHEN.

* Um autor do formulário agora pode aplicar funções personalizadas para [pré-processar dados antes do envio](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Use a [**Salvar como Funcionalidade de rascunho**](/help/forms/save-core-component-based-form-as-draft.md) para salvar formulários parcialmente concluídos para envio posterior. Isso é útil em cenários em que os usuários precisam interromper o preenchimento de um formulário e voltar para ele mais tarde.



### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O AEM Forms Programa de Acesso Antecipado programa oferece uma oportunidade única a você para obter acesso exclusivo a inovações de ponta antes de qualquer outra pessoa, e ajudar a moldar seu desenvolvimento. O programa oferece acesso a várias inovações.

Este notas de versão lista as inovações entregues no lançamento atual. Para obter a lista completa das inovações disponíveis no Programa de Acesso Antecipado, consulte [AEM Forms documentação](/help/forms/early-access-ea-features.md) do Programa de Acesso Antecipado.

#### Métodos de proteção bot aprimorados

A AEM Forms aprimorou seus recursos de segurança adicionando suporte para duas soluções populares do CAPTCHA: Cloud Turnstile e hCaptcha. Isso adiciona ao já disponível Google reCAPTCHA, fornecendo aos usuários mais opções e flexibilidade na proteção de seus formulários contra bots e envios de spam.

* **Cloudflare Turnstile**: Esse CAPTCHA sem atritos verifica os usuários por meio de um desafio simples que não requer interação explícita. Ele se integra perfeitamente aos seus formulários, melhorando o experiência do usuário.
* **hCaptcha**: Este CAPTCHA focado na privacidade oferece uma alternativa usuário com um focalizar sobre privacidade de dados. Ele visa encontrar um equilíbrio entre segurança e experiência do usuário.
* **Google reCAPTCHA**: AEM Forms continuam a oferecer suporte ao reCAPTCHA v2 e ao reCAPTCHA Enterprise, oferecendo uma solução confiável e bem estabelecida.

Oferecendo várias opções de CAPTCHA, AEM Forms capacitá-lo a selecionar a solução que se alinha melhor às suas necessidades específicas.

Pronto para integrar qualquer uma dessas soluções CAPTCHA ao Adaptive Forms? Nossa documentação fornece instruções detalhadas para cada: [Turnstile de Cloudflare](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [hCaptcha](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components) e [Google reCAPTCHA](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Serviço do Forms

O serviço do Forms gera PDF forms interativo para captura de dados. Ele também pode ser usado para importar ou exportar dados de e para um formulário interativo existente do PDF e validar os dados enviados. Veja um detalhamento de suas funcionalidades:

* **Renderização do Forms**: gere um formulário interativo do PDF a partir de um modelo criado com o AEM Forms Designer e, opcionalmente, dados XML. Isso produz essencialmente um formulário preenchível do PDF opcionalmente pré-preenchido com dados.
* **Extração e Importação de Dados**: importe dados para um formulário existente do PDF, bem como extraia dados de um formulário preenchido do PDF. Os formatos de dados XDP e XML são compatíveis, e a importação para PDF forms não XFA (também conhecida como AcroForms) também é compatível com dados FDF e XFDF.
* **Validação de Dados**: valide os dados enviados, no formato XDP ou XML, em relação a um modelo criado com o AEM Forms Designer.

>[!IMPORTANT]
>
> Se você estiver interessado em participar do nosso programa de Acesso Antecipado para qualquer inovação de acesso antecipado, basta enviar um email do seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acesso. Você pode solicitar acesso a todas as inovações ou a qualquer inovação específica.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Suporte a credenciais de servidor para servidor do OAuth para integrações da AEM com outras soluções da Adobe {#S2S-OAuth-credentials}

O Adobe Developer Console é usado para gerar credenciais para acessar várias APIs. Um desses tipos de credenciais, as credenciais da Conta de serviço (JWT), foi descontinuado em favor das credenciais de servidor para servidor do OAuth, que o AEM Cloud Service agora oferece suporte para integrações com outras soluções da Adobe, como Adobe Analytics e Adobe Target.

[Leia sobre a descontinuação](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md) e [saiba como usar as interface de criação de AEM](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) para configurar integrações com outras Adobe Systems soluções.

### Pico de tráfego nos alertas de origem {#traffic-spike-origin}

[Receba notificações proativas](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert) por meio do Centro de ações quando tráfego padrões no origem são indicativos de um ataque DDoS, permitindo que você investigue e configure tráfego regras de filtro.

### Novos recursos para RDEs {#RDE-new-features}

Os [Ambientes de desenvolvimento rápido (RDEs)](/help/implementing/developing/introduction/rapid-development-environments.md) permitem que os desenvolvedores implantem, revisem e testem rapidamente as alterações na nuvem. Vários novos recursos serão lançados durante o mês de junho. Também convidamos você a se envolver diretamente com a engenharia da Adobe no [canal RDE Discord](https://discord.com/channels/1131492224371277874/1245304281184079872).


#### Suporte RDE para código front-end usando temas de site e modelos de site {#rde-frontend}

[Os RDEs agora oferecem suporte ao código front-end](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) com base em [temas de site](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelos de site](/help/sites-cloud/administering/site-creation/site-templates.md), para participantes iniciais. Com RDEs, isso é feito usando uma diretiva de linha de comando, em vez de um [pipeline de front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md).

#### Aprimoramento de fazendo logon para RDEs {#rde-logging}

Ao depurar o código em um RDE, os desenvolvedores agora [podem configurar e transmitir logs de forma](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging) mais produtiva, usando a linha de comando e sem modificar as propriedades OSGI no controle da versão. Os recursos incluem:

* declarando níveis de log em um por pacote ou nível de classe
* como personalizar o formato de saída de log
* transmissão de vários logs ao mesmo tempo

#### Aprimoramentos na CLI da RDE {#rde-cli-enhancements}

A interface de linha de comando do RDE tem alguns novos recursos que melhoram a experiência do desenvolvedor:

* [o comando de configuração é interativo](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive), facilitando a escolha entre organizações, programas e ambientes. Agora também é possível substituir esses valores na linha de comando.
* [modo](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) silencioso para uma saída menos detalhada.
* [modo](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) json para saída útil quando invocado programaticamente.

### Notificações do centro de ações do Novo {#actions-center-notifications}

O [Centro de Ações](/help/operations/actions-center.md) envia notificações por email quando ocorrem incidentes importantes, ou se notarmos algo sobre seu código ou configuração, onde você deve realizar uma ação proativa. Existem três novos tipos de notificações:

* muitas conexões de saída por meio de uma infraestrutura de rede avançada
* uso de um formato obsoleto de Mapeamento de usuário de serviço
* um possível ataque de DDoS está em andamento

### Programas de adoção antecipado {#foundation-early-adopter}

Email **<aemcs-cdn-config-adopter@adobe.com>**, indicando em quais programas de inicialização você está interessado.

#### Limpe conteúdo no CDN com uma chave de API de autoatendimento (Programa de adoção precoce) {#purge-cdn}

Registre uma chave de API CDN limpeza de autoatendimento e use-a para invalidar conteúdo no CDN, globalmente ou para um ou mais recursos. [Saiba mais](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Criação de autoatendimento de X-AEM-Edge-Key para CDN gerenciados pelo cliente (BYOCDN) (Early Adopter Program) {#byocdn-keys}

Anteriormente, era necessário um ticket de suporte para gerar o X-AEM-Edge-Key necessário para a configuração de um CDN gerenciado pelo cliente. Isso agora pode ser feito de maneira autoatendida por meio de um arquivo de configuração implantado usando o Pipeline de configuração, removendo qualquer atraso na integração de uma nova ambiente. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Redirecionamentos do lado do servidor (Programa Dedonte Antecipado) {#server-side-redirects-early-adopter}

Configure 301/302 lado do servidor redireciona no controle de origem e implantar para o CDN. [Saiba mais](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Observe que já existem vários outros recursos já disponíveis relacionados à [configuração](/help/implementing/dispatcher/cdn-configuring-traffic.md) CDN, incluindo transformações de solicitação e respostas e roteamento tráfego para sites off-AEM.

#### Alertas de regras de Filtrar de tráfego (Programa de primeiros adotadores) {#traffic-filter-rules-alerts-early-adopter}

As Regras[&#128279;](/help/security/traffic-filter-rules-including-waf.md) de Filtrar de Tráfego lançadas recentemente, que incluem as regras de Firewall de Aplicação Web (WAF) que podem ser licenciadas, permite configurar quais tráfego devem ser permitidas ou negadas.

Associar-se o programa de adotante inicial para que você possa ser alertado sempre que suas regras de filtro tráfego forem acionadas. As notificações por email do Centro de ações manterão você informado quando determinadas tráfego condições ocorrerem para que você possa tomar as medidas apropriadas.

#### Usuários empresariais podem declarar redirecionamentos fora do Git (Early Adoter Program, Programa de adoção antecipada) {#apache-rewritemaps-early-adopter}

Semelhante ao AEM 6.5, o Apache/Dispatcher assimilará mapas de regravação colocados em um local específico no repositório de publicação e os carregará, sem exigir uma execução de pipeline no nível da Web. Isso abre oportunidades para que um usuário empresarial declare redirecionamentos usando uma planilha ou uma interface do usuário, como a oferecida pelo ACS Commons Redirect Map Manager ou criada como parte de um aplicativo do cliente. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) para carregamento de conteúdo dinâmico (Programa de primeiros adotadores) {#esi-early-adopter}

O Adobe Systems Managed CDN agora oferece [suporte a Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), uma linguagem de marcação para conjunto de conteúdo web dinâmicos de nível de borda. Ao incluir trechos de ESI, você pode armazenar em cache as página HTML gerais no CDN com TTLs mais altos, enquanto, com mais frequência, a busca por origem seções menores que requerem atualizações de cadência mais altas (TTLs mais baixas). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] Guias {#guides}

* **Publish um tópico ou seus elementos para um fragmento** de experiência
Agora, os Guias Experience Manager permitem publicar um tópico ou seus elementos a um Fragmento de experiência. Um fragmento de experiência é uma unidade de conteúdo modular que integra conteúdo e layout.  Os fragmentos de experiência são fundamentais e podem ajudá-lo a criar experiências consistentes e envolventes.
* **Capacidade de passar os metadados do ativo de tópico para saída do PDF Nativo**
Você pode adicionar os metadados do ativo de tópico ao gerar a saída do PDF nativo. Esse recurso ajuda você a adicionar metadados específicos para diferentes tópicos, como o título do tópico e o autor, aos cabeçalhos e rodapés da página de tópico.

Para obter mais informações sobre recursos e problemas novos e aprimorados corrigidos nessa versão, exiba o [roteiro de versão do Experience Manager Guides](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Notas de versão da Experience Cloud {#experience-cloud}

Você pode encontrar informações sobre versões de outros aplicativos da Experience Cloud [aqui](https://experienceleague.adobe.com/pt-br/docs/release-notes/experience-cloud/current).
Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).
