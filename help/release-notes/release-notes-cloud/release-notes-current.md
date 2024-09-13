---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais para  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 7c195e5640f828d2c59dbabd8f29127692788576
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 12%

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
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização de Produto Prioritária do Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.8.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 29 de agosto de 2024. O próximo lançamento de recursos (2024.9.0) está planejado para sexta-feira, 26 de setembro de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de agosto de 2024 que exibe um resumo dos recursos adicionados na versão 2024.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3433381?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novo recurso no Experience Manager Sites {#new-feature-sites}

**Criação de AEM para Edge Delivery Services**

A funcionalidade [herança](/help/sites-cloud/authoring/universal-editor/inheritance.md) dos sites existentes agora tem suporte, incluindo:

* [Inicializações do AEM](/help/sites-cloud/authoring/launches/overview.md)
* [MSM](/help/sites-cloud/administering/msm/overview.md) no nível da página

Além disso, os seguintes recursos de gerenciamento de página agora são compatíveis:

* [Marcas de AEM](/help/sites-cloud/authoring/sites-console/tags.md) podem ser exportadas como uma [taxonomia](/help/edge/wysiwyg-authoring/taxonomy.md) para Edge Delivery Services.
* [Modelos](/help/edge/wysiwyg-authoring/templates.md) para Edge Delivery Services serão lançados em breve!

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar Variações**

Aproveite a GenAI por meio do novo recurso AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta do Adobe para consideração no programa.


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Recurso de acesso antecipado no Dynamic Media {#dm-early-access}

**Legendas de vídeo geradas por IA**

Legendas de vídeo geradas por IA no Adobe Dynamic Media usam inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. Esse recurso foi projetado para melhorar a acessibilidade e a experiência do usuário, fornecendo legendas precisas e em tempo real. A IA analisa a faixa de áudio do vídeo para transcrever a fala e criar legendas, que podem ser editadas para precisão ou personalização. Essas legendas ajudam a atender aos requisitos de acessibilidade e melhorar o envolvimento com o vídeo para públicos-alvo que dependem ou preferem suporte de vídeo baseado em texto.

Para obter acesso antecipado ao suporte a legendas geradas por IA em sua conta da Dynamic Media, [crie e envie um caso de Suporte ao Cliente do Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Novos recursos na visualização de ativos {#assets-view-new-features}

**Geração de imagem de Adobe Firefly atualizada**

O Assets as a Cloud Service usa o widget mais recente do Firefly, que permite gerar imagens em diferentes estilos usando o Adobe Firefly. Ao definir seu estilo, composição, dimensões e muito mais, usando o editor de Firefly interno, você pode criar e salvar rapidamente os ativos necessários diretamente no repositório do AEM Assets para uso imediato.

![geração de imagem de Adobe Firefly](/help/assets/assets/bugatti-type-57.png)

**Suporte a arquivo PSB**

O Assets as a Cloud Service agora é compatível com documentos grandes da Photoshop (arquivos PSB), além do suporte existente a arquivos PSD.

### Novos aprimoramentos na Content Hub {#content-hub-new-enhancements}

* Melhor manipulação de nomes de arquivo longos, fácil expansão do nome completo através de dica de ferramenta.
* Miniaturas aprimoradas para melhor se ajustar às proporções de conteúdo e cobrir uma área maior de conteúdo.
* Experiência de miniatura personalizada do AEM compatível com o content hub.
* Melhorias na pesquisa de cores.
* As melhorias nas configurações salvam a experiência.
* Página de informações das coleções aprimorada para refletir o nome do criador.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos de pré-lançamento no AEM Forms {#forms-new-prerelease-features}

#### Salvar automaticamente um rascunho para os Componentes principais com base no Forms adaptável

Os usuários agora podem se beneficiar de um recurso de salvamento automático que salva automaticamente um formulário parcialmente preenchido como rascunho. Eles podem retornar mais tarde para terminar de preenchê-lo no mesmo dispositivo ou em outro. Esse recurso melhora as taxas de conversão para organizações ao reduzir o abandono de formulário, pois os usuários não precisam começar novamente o preenchimento do formulário desde o início.


### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Assistente de IA do AEM Forms

A IA gerativa para o Adaptive Forms traz um nível totalmente novo de potência e facilidade para seus processos de desenvolvimento de formulários. Ele permite que você construa formulários melhores mais rápido do que nunca.

![Assistente de IA de Geração, Forms Adaptável](/help/forms/assets/generative-ai-assistant.png)

Os recursos de IA gerativa disponíveis são:

* **Assistente de IA para consultas de produtos**: obtenha respostas instantâneas para suas perguntas relacionadas ao formulário AEM. O assistente de IA atua como sua própria base de conhecimento pessoal, fornecendo orientação e recomendações relevantes diretamente na plataforma.

* **Geração de formulário adaptável**: crie formulários completos sem esforço com prompts de IA geradores. A IA gerativa do Adobe gera automaticamente formulários amigáveis que reduzem as quedas e personalizam a experiência.

* **Geração de painel para Forms**: gere seções de formulário personalizadas para necessidades específicas de coleta de dados. Por exemplo, gere seções para coletar informações de pagamento, preferências do cliente ou detalhes da viagem.

* **Alterando Layouts de Formulário**: experimente diferentes layouts e designs usando prompts de IA geradores. Experimente diferentes layouts, como visualizações com assistente ou em abas, para encontrar o ajuste perfeito para o seu formulário. Use prompts de IA gerativos para otimizar seus formulários para a agilidade e criar formulários visualmente envolventes que os usuários adoram.

* **Configurar Ação de Envio**: use prompts de IA gerativa para configurar uma ação de envio facilmente para o seu formulário. Escolha entre uma biblioteca de ações de envio pré-criadas ou ações de envio personalizadas criadas e implantadas pela sua equipe de desenvolvimento.

>[!IMPORTANT]
>
> Interessado em participar do Programa de acesso antecipado para qualquer inovação da Forms? Envie um email de seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) com a lista de recursos nos quais você está interessado.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

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
