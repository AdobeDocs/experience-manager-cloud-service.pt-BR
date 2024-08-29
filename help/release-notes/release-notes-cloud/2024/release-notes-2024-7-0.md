---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.7.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.7.0.
feature: Release Information
role: Admin
source-git-commit: 2edaca5637c735645e2b761377b9681d9b48daa1
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 18%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2024.7.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2024.7.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2022 ou 2023.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização de Produto Prioritária do Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.7.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 25 de julho de 2024. O próximo lançamento de recursos (2024.8.0) está planejado para sexta-feira, 29 de agosto de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de julho de 2024 para ver um resumo dos recursos adicionados na versão 2024.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/3431707?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novo recurso no Experience Manager Sites {#new-feature-sites}

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar Variações**

Aproveite a GenAI por meio do novo recurso AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta do Adobe para consideração no programa.

**Navegação de ativos no Console de Fragmentos de Conteúdo**

Os autores de conteúdo agora podem navegar, visualizar e realizar ações em imagens e outros ativos sem precisar sair do Console de fragmentos de conteúdo.

![Navegação de ativos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Interessado em experimentar o recurso e compartilhar feedback? Envie um email para aemcs-headless-adopter@adobe.com a partir de sua ID de email oficial para saber mais sobre o programa dos participantes antecipados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Carregar ativos usando o Seletor de ativos**

O Seletor de ativos agora oferece aos autores de conteúdo a capacidade de fazer upload de ativos finais diretamente do seletor, arrastando ou navegando do sistema de arquivos local. Isso permite que os ativos finais sejam carregados no DAM a partir do aplicativo de sua escolha.

### Novos recursos na visualização de ativos {#assets-view-new-features}

**Integração de credenciais do conteúdo**

O Experience Manager Assets agora é compatível com credenciais de conteúdo para os formatos de imagem compatíveis. Isso fornece informações sobre a linhagem do ativo e como ele foi criado, incluindo se ele foi modificado com a IA generativa.

![Credenciais de conteúdo](/help/assets/assets/content-credentials.png)

**Visualizações do conteúdo das pastas**

O Experience Manager Assets agora exibe visualizações do conteúdo das pastas em suas miniaturas ao navegar ou pesquisar conteúdo, o que melhora a descoberta de ativos disponíveis no repositório do AEM Assets.

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no AEM Forms {#forms-new-prerelease-features}

#### Editor de regras visuais aprimorado para Forms adaptável baseado em componentes principais

Os autores de formulários adaptáveis podem usar campos de formulário repetíveis em funções prontas para uso disponíveis no editor visual de regras para componentes principais a fim de criar uma lógica de negócios complexa nos formulários, sem precisar de personalização ou assistência da equipe de desenvolvimento.

### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado do AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de ponta antes de qualquer outra pessoa e ajudar a moldar seu desenvolvimento. O programa oferece acesso a várias inovações.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Criar formulários adaptáveis usando o Editor universal

Aproveite o [Editor Universal](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) do Adobe Experience Manager para criar formulários adaptáveis usando a criação de arrastar e soltar WYSIWYG, para experiências de inscrição headless e headful, entregues pelo Serviço Edge Delivery. Os autores de formulários adaptáveis podem criar e iniciar facilmente experimentos para variações de formulários nas páginas da Web e determinar as experiências de melhor desempenho para os usuários finais.

>[!IMPORTANT]
>
> Se você estiver interessado em participar do Programa de Acesso Antecipado do Adobe para qualquer inovação de acesso antecipado, basta enviar um email do seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acesso. Você pode solicitar acesso a todas as inovações ou a qualquer inovação específica.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Limpar conteúdo na CDN com uma chave de API de autoatendimento {#purge-cdn}

A definição do TTL usando o cabeçalho HTTP Cache-Control é uma abordagem eficaz para equilibrar o desempenho da entrega de conteúdo e a atualização de conteúdo. No entanto, em cenários em que é essencial fornecer imediatamente conteúdo atualizado, pode ser útil limpar diretamente o cache da CDN.

[Saiba como](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) configurar por autoatendimento um token de API de limpeza usando o pipeline de configuração do Cloud Manager, para poder [invocar as APIs de limpeza](/help/implementing/dispatcher/cdn-cache-purge.md), com qualquer uma destas variações:
* URL único
* Vários URLs usando uma tag
* Limpeza completa do cache do CDN

### Configuração de autoatendimento do X-AEM-Edge-Key para CDN gerenciada pelo cliente {#customermanaged-keys}

Anteriormente, um tíquete de suporte era necessário para gerar a X-AEM-Edge-Key necessária para a configuração de um CDN gerenciado pelo cliente. Agora, isso se torna autoatendimento ao declarar o valor principal em um arquivo de configuração implantado usando o Pipeline de configuração, removendo qualquer atraso na integração de um novo ambiente. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

### Alertas de regras de filtro de tráfego {#traffic-filter-rules-alerts}

As Regras de filtro de tráfego, que incluem as regras opcionalmente licenciáveis do Web Application Firewall (WAF), permitem configurar o tráfego que deve ser bloqueado.

Agora é possível [assinar alertas](/help/security/traffic-filter-rules-including-waf.md#traffic-filter-rules-alerts) sempre que as regras de filtro de tráfego forem acionadas. As notificações por email do Centro de ações mantêm você informado quando ocorrem determinadas condições de tráfego para que você possa tomar as medidas apropriadas.

### Programas dos primeiros usuários relacionados à entrega de conteúdo {#foundation-early-adopter}

Email **<aemcs-cdn-config-adopter@adobe.com>**, indicando em qual dos primeiros programas abaixo você está interessado.

#### Autenticação básica na CDN (Early Adoter Program, programa de primeiros usuários) {#basicauth-cdn}

Protect determinados recursos de conteúdo, exibindo uma caixa de diálogo de autenticação básica que requer um nome de usuário e senha. Esse recurso destina-se principalmente a casos de uso de autenticação simples, como partes interessadas de negócios que revisam o conteúdo, em vez de servir como uma solução abrangente para os direitos de acesso do usuário final. A lista de nomes de usuário e senhas é gerenciada por meio de um arquivo de configuração no Git, que é implantado por meio do Pipeline de configuração, com uma referência às variáveis de ambiente do Cloud Manager do tipo secreto. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Redirecionamentos do lado do cliente (programa de primeiros usuários) {#client-side-redirects-early-adopter}

Configure os redirecionamentos do lado do cliente 301/302 no controle do código-fonte e implante na CDN. [Saiba mais](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Observe que há vários outros recursos já disponíveis relacionados à [configuração de CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), incluindo transformações de solicitação e resposta, e roteamento de tráfego para sites fora do AEM.

#### Usuários empresariais podem declarar redirecionamentos fora do Git (Early Adoter Program, Programa de primeiros usuários) {#apache-rewritemaps-early-adopter}

Semelhante ao AEM 6.5, o Apache/Dispatcher assimila mapas de regravação colocados em um local específico no repositório de publicação e os carrega, sem exigir uma execução de pipeline no nível da Web. Essa abordagem permite que os usuários empresariais declarem redirecionamentos usando uma planilha ou interface do usuário, como o ACS Commons Redirect Map Manager ou um aplicativo personalizado. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### O Edge Side Includes (ESI) para Carregar Conteúdo Dinâmico (Early Adoter Program) {#esi-early-adopter}

O CDN do Adobe Managed agora é compatível com o [ESI (Edge Side Includes)](/help/implementing/dispatcher/edge-side-includes.md), uma linguagem de marcação para o assembly de conteúdo dinâmico da Web no nível da borda. Ao incluir trechos ESI, você pode armazenar em cache a página de HTML geral na CDN com TTLs mais altos, enquanto busca com mais frequência a partir da origem as seções menores que exigem atualizações de cadência mais altas (TTLs mais baixos). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

### Programa de adoção antecipada de notificações do Centro de ações relacionadas à integridade do conteúdo {#actions-center-notifications}

A [Central de Ações](/help/operations/actions-center.md) envia notificações por email quando ocorrem incidentes importantes, ou se algo for notado sobre seu código ou configuração, onde você deve tomar medidas pró-ativas. O Adobe agora introduziu vários novos tipos de notificações associados à integridade do conteúdo. Esse recurso está disponível por meio de um programa de adoção antecipada. Para participar, entre em contato com o Atendimento ao cliente do Adobe.

#### As páginas contêm um grande número de nós {#page-nodes}

Um grande número de nós pode degradar o desempenho da renderização e reduzir o tempo de carregamento da página. Receba uma notificação proativa pelo Centro de ações quando um grande número de nós for detectado em uma página, permitindo que você siga as etapas necessárias para reduzir o número total de nós em uma página.

#### Grande número de instâncias de fluxo de trabalho em execução {#running-workflows}

O desempenho do mecanismo de fluxo de trabalho é afetado quando há um grande número de fluxos de trabalho em execução no ambiente de criação. Você recebe uma notificação proativa por meio do Centro de ações quando um grande número de instâncias de fluxo de trabalho em execução é detectado. Esse processo permite configurar um trabalho de limpeza para encerrar fluxos de trabalho em execução desnecessários.

#### Usuários adicionados diretamente aos grupos personalizados {#users-customgroups}

Você recebe uma notificação proativa por meio do Centro de ações quando os usuários são adicionados diretamente aos grupos personalizados. Esse processo permite seguir as práticas recomendadas do IMS, adicionando usuários aos grupos IMS relevantes e, em seguida, incluindo esses grupos IMS como membros de grupos AEM.

#### Conteúdo JCR ausente {#jcr-content}

O Centro de ações o notifica proativamente quando conteúdo JCR ausente é detectado. Essa abordagem permite adicionar o conteúdo ausente e evitar a falha de determinados recursos do AEM Assets.

#### Fluxos de trabalho concluídos não removidos {#workflows}

O Centro de ações notifica proativamente quando workflows concluídos há mais de 90 dias não foram removidos. Essa abordagem ajuda a melhorar o desempenho do mecanismo de fluxo de trabalho, reduzindo o número de instâncias de fluxo de trabalho.

#### Recurso Sling ausente {#sling-resource}

O Centro de ações envia uma notificação proativa quando um recurso Sling ausente é detectado. Essa abordagem permite adicionar o recurso ausente e evitar a falha de determinados recursos do AEM Assets.

## Guias do [!DNL Experience Manager] {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente do Adobe Experience Manager Guides [aqui](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universal {#universal-editor}

Você pode encontrar uma lista completa de versões do Universal Editor [aqui](/help/release-notes/universal-editor/current.md).

## Gerar variações {#generate-variations}

Você pode encontrar uma lista completa de versões de Gerar Variações [aqui](/help/generative-ai/release-notes-generate-variations.md).

## Notas de versão da Experience Cloud {#experience-cloud}

Você pode encontrar informações sobre lançamentos de outros aplicativos Experience Cloud [aqui](https://experienceleague.adobe.com/pt-br/docs/release-notes/experience-cloud/current).
