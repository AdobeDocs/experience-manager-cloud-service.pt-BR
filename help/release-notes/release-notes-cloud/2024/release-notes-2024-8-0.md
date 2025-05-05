---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.8.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.8.0.
feature: Release Information
role: Admin
exl-id: dd1d4b8f-8331-4e97-a754-37e720974db6
source-git-commit: 4b8086920bc3e3b9c5ed2a74934645fbc69acf71
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 15%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2024.8.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2024.8.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2022 ou 2023.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.8.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 29 de agosto de 2024. O próximo lançamento de recursos (2024.9.0) está planejado para sexta-feira, 26 de setembro de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Dê uma olhada no vídeo de visão geral da versão de agosto de 2024 para ver um resumo dos recursos adicionados na versão 2024.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3433381?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novo recurso na Sites de Experience Manager {#new-feature-sites}

**criação de AEM para serviços de entrega de borda**

A funcionalidade [herança](/help/sites-cloud/authoring/universal-editor/inheritance.md) dos sites existentes agora tem suporte, incluindo:

* [Inicializações do AEM](/help/sites-cloud/authoring/launches/overview.md)
* [MSM](/help/sites-cloud/administering/msm/overview.md) no nível da página

Além disso, os seguintes recursos de gerenciamento de página agora são compatíveis:

* [&#128279;](/help/sites-cloud/authoring/sites-console/tags.md)AEM Tags podem ser exportadas como uma [taxonomia](/help/edge/wysiwyg-authoring/taxonomy.md) para os Serviços de entrega de edge.
* [Os modelos](/help/sites-cloud/authoring/universal-editor/templates.md) para o Edge Delivery Services serão disponibilizados em breve.

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar Variações**

Aproveite a GenAI por meio do novo recurso do AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta da Adobe para consideração no programa.


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na visualização de ativos {#assets-view-new-features}

**Geração de imagem do Adobe Firefly atualizada**

O Assets as a Cloud Service agora usa o widget mais recente do Firefly, que permite gerar imagens em diferentes estilos usando o Adobe Firefly. Ao definir seu estilo, composição, dimensões e muito mais, usando o editor Firefly integrado, você pode criar e salvar rapidamente os ativos necessários diretamente no repositório do AEM Assets para uso imediato.

![Geração de imagem do Adobe Firefly](/help/assets/assets/bugatti-type-57.png)

**Suporte a arquivo PSB**

O Assets as a Cloud Service agora é compatível com documentos grandes da Photoshop (arquivos PSB), além do suporte existente a arquivos PSD.

### melhorias do Novo no Content Hub {#content-hub-new-enhancements}

* Melhor manuseio de nomes de arquivos longos, fácil expansão do nome completo por meio da dica de ferramenta.
* Miniaturas aprimoradas para ajustar melhor conteúdo proporção e cobrir uma área maior de conteúdo.
* Miniaturas personalizadas experiência de AEM compatíveis com conteúdo hub.
* Melhorias na pesquisa de cores.
* As melhorias nas configurações salvam a experiência.
* Foram aprimoradas as informações página das coleções para refletir o nome do criador.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novo recursos de pré-lançamento no AEM Forms {#forms-new-prerelease-features}

#### Automático salvar um rascunho dos Componentes principais baseados em Forms adaptativos

Agora os usuários podem se beneficiar de um recurso de salvamento automático que salva um formulário parcialmente concluído como um rascunho automaticamente. Eles podem retornar mais tarde para terminar de preenchê-lo no mesmo dispositivo ou em outro. Esse recurso melhora as taxas de conversão para organizações ao reduzir o abandono de formulário, pois os usuários não precisam começar novamente o preenchimento do formulário desde o início.


### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Assistente de IA do AEM Forms

Ia generativa para Forms adaptável traz um novo nível de poder e facilidade aos processos de desenvolvimento de formulários. Ele permite que você build formulários melhores mais rápido do que nunca.

![Assistente de IA generativo, Forms adaptável](/help/forms/assets/generative-ai-assistant.png)

Os recursos de IA generativa no oferta são:

* **Assistente de IA para consultas** de produto: obtenha respostas instantâneas para suas AEM perguntas relacionadas a formulários. O assistente de IA atua como seu próprio knowledge base pessoal, fornecendo orientações e recomendações insight diretamente na plataforma.

* **Geração de formulário adaptável**: crie formulários completos sem esforço com Prompts do Generative AI. Nossa IA gerativa gera automaticamente formulários amigáveis que reduzem as quedas e personalizam a experiência.

* **Geração de painel para Forms**: gere seções de formulário personalizadas para necessidades específicas de coleta de dados. Por exemplo, gere seções para coletar informações de pagamento, preferências do cliente ou detalhes da viagem.

* **Alterando Layouts de Formulário**: experimente diferentes layouts e designs usando Solicitações de IA Gerativa. Experimente diferentes layouts, como visualizações com assistente ou em abas, para encontrar o ajuste perfeito para o seu formulário. Use os Prompts de IA gerativa para otimizar seus formulários para a agilidade móvel e criar formulários visualmente envolventes que os usuários adoram.

* **Configure a ação** de envio: use prompts de IA generativos para configurar sem esforço uma ação de envio para o formulário. Escolha entre uma biblioteca de ações de envio pré-criadas ou entre uma lista de ações de envio personalizadas, criadas e implantadas pela sua própria equipe de desenvolvimento.

>[!IMPORTANT]
>
> Se você estiver interessado em participar do Programa de Acesso Antecipado para qualquer inovação, basta enviar um email de seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) com a lista de recursos nos quais você está interessado.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Programas dos primeiros usuários relacionados à entrega de conteúdo {#foundation-early-adopter}

Email **<aemcs-cdn-config-adopter@adobe.com>**, indicando em qual dos primeiros programas abaixo você está interessado.

#### Autenticação básica na CDN (Early Adoter Program, programa de primeiros usuários) {#basicauth-cdn}

Proteja determinados recursos de conteúdo abrindo uma caixa de diálogo de autenticação básica que requer um nome de usuário e senha. Esse recurso destina-se principalmente a casos de uso de autenticação simples, como partes interessadas de negócios que revisam o conteúdo, em vez de servir como uma solução abrangente para os direitos de acesso do usuário final. A lista de nomes de usuário e senhas é gerenciada por meio de um arquivo de configuração no Git, que é implantado por meio do Pipeline de configuração, com uma referência às variáveis de ambiente do Cloud Manager do tipo secreto. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Redirecionamentos do lado do servidor (programa de primeiros usuários) {#server-side-redirects-early-adopter}

Configure os redirecionamentos do lado do servidor 301/302 no controle do código-fonte e implante na CDN. [Saiba mais](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Observe que há vários outros recursos já disponíveis relacionados à [configuração de CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), incluindo transformações de solicitação e resposta e o roteamento de tráfego para sites fora do AEM.

#### Empresas usuários podem declarar redirecionamentos fora do Git (Early Adopter Program) {#apache-rewritemaps-early-adopter}

Semelhante ao AEM 6.5, o Apache/dispatcher assimilar mapas de reescrita colocados em um local específico no publicar repositório e carregue-os, sem exigir uma execução do pipeline de nível da Web. Essa abordagem permite que os usuários corporativos declarem redirecionamentos usando uma planilha ou uma interface, curtir o ACS Commons Redirect Map Manager ou uma aplicativo personalizada. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) para carregamento de conteúdo dinâmico (Programa de primeiros adotadores) {#esi-early-adopter}

O Adobe Systems Managed CDN agora oferece [suporte a Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), uma linguagem de marcação para conjunto de conteúdo web dinâmicos de nível de borda. Ao incluir trechos ESI, você pode armazenar em cache a página geral do HTML na CDN com TTLs mais altos, enquanto busca com mais frequência a partir da origem as seções menores que exigem atualizações de cadência mais altas (TTLs mais baixos). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

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
