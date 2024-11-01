---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.9.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.9.0.
feature: Release Information
role: Admin
source-git-commit: 0c4db1b70aa665e1802a316ece26db1e06f40b24
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 13%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2024.9.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2024.9.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2022 ou 2023.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização de Produto Prioritária do Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.9.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 26 de setembro de 2024. O próximo lançamento de recursos (2024.10.0) está planejado para sexta-feira, 31 de outubro de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de setembro de 2024 que exibe um resumo dos recursos adicionados na versão 2024.9.0:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novo recurso no Experience Manager Sites {#new-feature-sites}

#### Gerenciamento de tradução {#translation-management}

Os fluxos de trabalho de tradução e as ações de API do AEM agora acionam eventos para fornecer insights sobre as alterações de estado do trabalho de tradução. Os usuários podem assinar esses eventos por meio da Adobe Developer Console. Consulte [aqui](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/) para obter mais informações sobre a API de gerenciamento de tradução do AEM.

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar Variações**

Aproveite a GenAI por meio do novo recurso AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta do Adobe para consideração no programa.


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Recurso de acesso antecipado no Dynamic Media {#dm-early-access}

**Legendas de vídeo geradas por IA**

Legendas de vídeo geradas por IA no Adobe Dynamic Media usam inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. Esse recurso foi projetado para melhorar a acessibilidade e a experiência do usuário, fornecendo legendas precisas e em tempo real. A IA analisa a faixa de áudio do vídeo para transcrever a fala e criar legendas, que podem ser editadas para precisão ou personalização. Essas legendas ajudam a atender aos requisitos de acessibilidade e melhorar o envolvimento com o vídeo para públicos-alvo que dependem ou preferem suporte de vídeo baseado em texto.

Para obter acesso antecipado ao suporte a legendas geradas por IA em sua conta da Dynamic Media, [crie e envie um caso de Suporte ao Cliente do Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Novos recursos no Seletor de ativos {#asset-selector-new-features}

O Seletor de ativos agora é compatível com a navegação em Coleções para encontrar o ativo desejado.
![Coleções do seletor de ativos](/help/assets/assets/collections-rail-modal-view.png)

### Novos recursos no Content Hub {#content-hub-new-features}

Agora, os administradores podem controlar se precisam que os ativos expirados estejam visíveis no Content Hub. Se os ativos expirados se tornarem visíveis, eles também poderão definir se os usuários podem baixá-los.

![Ativos expirados no Content Hub](/help/assets/assets/view-download-expired-assets.png)

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

## Complemento CIF {#cloud-services-cif}

### Melhorias {#improvements-fixes-cif}

* Tornar o limite de categoria personalizável.

### Correções de erros {#bug-fixes-cif}

* Os campos do Commerce não estão integrados corretamente ao editor de esquema de metadados do Assets.
* Problema com o multicampo de produtos do carrossel para arrastar e soltar.
* Problema com multicampo de categoria do carrossel para arrastar e soltar.
* O clique não funciona para os menus nas Informações de página na página do editor de categoria e produto.
* O número do pedido não está visível na página Confirmação do pedido.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Edge Side Includes (ESI) para Carregar Conteúdo dinâmico {#esi}

O CDN do Adobe Managed agora é compatível com o [ESI (Edge Side Includes)](/help/implementing/dispatcher/edge-side-includes.md), uma linguagem de marcação para o assembly de conteúdo dinâmico da Web no nível da borda. Ao incluir trechos ESI, você pode armazenar em cache a página de HTML geral na CDN com TTLs mais altos, enquanto busca com mais frequência a partir da origem as seções menores que exigem atualizações de cadência mais altas (TTLs mais baixos). Esse recurso será implementado gradualmente.

### Autenticação básica na CDN {#basicauth-cdn}

Protect determinados recursos de conteúdo, exibindo uma caixa de diálogo de autenticação básica que requer um nome de usuário e senha. Esse recurso destina-se principalmente a casos de uso de autenticação simples, como partes interessadas de negócios que revisam o conteúdo, em vez de servir como uma solução abrangente para os direitos de acesso do usuário final. A lista de nome de usuário e senhas é gerenciada por meio de um arquivo de configuração no Git, implantado por meio do Pipeline de configuração, com uma referência a variáveis de ambiente do Cloud Manager do tipo secreto. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

### Redirecionamentos do lado cliente {#client-side-redirects}

Declarar [redirecionamentos do navegador](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors) em um Git de arquivo de configuração que são implantados e avaliados no CDN. Isso pode ser útil para cenários como exclusão de páginas, alteração da estrutura do site e otimização de SEO.

### Novo AEM Developer Console (Beta público) {#aem-developer-console-beta}

Experimente um [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) renovado, que oferece uma experiência mais interativa para depurar código em ambientes na nuvem.

Qualquer pessoa pode acessar o beta público clicando no botão *Novo Console Disponível* no Developer Console AEM atual. O Adobe agradece o feedback, que você pode enviar por email para **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![Tela de Pacotes OSGi no AEM Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

### Usuários empresariais podem declarar redirecionamentos fora do Git (Early Adoter Program, Programa de primeiros usuários) {#apache-rewritemaps-early-adopter}

Semelhante ao AEM 6.5, o Apache/Dispatcher assimila mapas de regravação colocados em um local específico no repositório de publicação e os carrega sem exigir uma execução de pipeline no nível da Web. Essa abordagem permite que os usuários empresariais declarem redirecionamentos usando uma planilha ou uma interface do usuário, como o ACS Commons Redirect Map Manager ou um aplicativo personalizado. Participe do programa de adoção antecipada enviando um email para **<aemcs-cdn-config-adopter@adobe.com>**.

### Pipeline de configuração para RDEs (Early Adoter Program, programa de primeiros usuários) {#config-pipeline-rdes-early-adopter}

O [Pipeline de Configuração](/help/operations/config-pipeline.md) é usado para implantar configurações de arquivos yaml, incluindo opções de CDN (regras de filtro de tráfego, transformações de solicitação/resposta e assim por diante). Associe-se ao programa pioneiro enviando um email para **<aemcs-cdn-config-adopter@adobe.com>** para implantar essas mesmas configurações nos RDEs (Rapid Development Environments), que usam uma CLI.

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
