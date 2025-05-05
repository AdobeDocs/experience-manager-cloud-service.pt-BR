---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.9.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.9.0.
feature: Release Information
role: Admin
exl-id: 75ecd154-112a-4468-9962-de50bb1f4cd0
source-git-commit: 1481983bde41bda51e725930bae492aa599b6c93
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
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber um notificação de email mensal sobre atualizações a Experience Cloud notas de versão, assine a [atualização Adobe Systems prioritária](https://www.adobe.com/subscription/priority-product-update.html) dos produtos.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.9.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 26 de setembro de 2024. O próximo lançamento de recursos (2024.10.0) está planejado para sexta-feira, 31 de outubro de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Dê uma olhada no vídeo de visão geral da versão de setembro de 2024 para ver um resumo dos recursos adicionados na versão 2024.9.0:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novo recurso na Sites de Experience Manager {#new-feature-sites}

#### Gerenciamento de tradução {#translation-management}

Os fluxos de trabalho de tradução e as ações de API do AEM agora acionam eventos para fornecer ao insight informações sobre alterações de estado do trabalho de tradução. Os usuários podem assinar esses eventos por meio da Adobe Developer Console. Consulte [aqui](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/) para obter mais informações sobre a API do AEM Translation Management.

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar Variações**

Aproveite a GenAI por meio do novo recurso do AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta da Adobe para consideração no programa.


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Recurso de acesso antecipado no Dynamic Media {#dm-early-access}

**Legendas de vídeo geradas por IA**

Legendas de vídeo geradas por IA no Adobe Dynamic Media usam inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. Esse recurso foi projetado para melhorar a acessibilidade e a experiência do usuário, fornecendo legendas precisas e em tempo real. A IA analisa a faixa de áudio do vídeo para transcrever a fala e criar legendas, que podem ser editadas para precisão ou personalização. Essas legendas ajudam a atender aos requisitos de acessibilidade e melhorar a envolvimento de vídeo para públicos que dependem ou preferem suporte a vídeos baseados em texto.

Para obter acesso antecipado ao suporte a legendas geradas por IA em sua Mídia dinâmica conta, [crie e envie um caso](/help/assets/dynamic-media/video.md##enable-dash) Adobe Systems de Suporte ao cliente.

### Novos recursos no Seletor de ativos {#asset-selector-new-features}

O Seletor de ativos agora é compatível com a navegação em Coleções para encontrar o ativo desejado.
![Coleções do seletor de ativos](/help/assets/assets/collections-rail-modal-view.png)

### Novos recursos no Content Hub {#content-hub-new-features}

Agora, os administradores podem controlar se precisam que os ativos expirados estejam visíveis no Content Hub. Se os ativos expirados se tornarem visíveis, eles também poderão definir se os usuários podem baixá-los.

![O ativos expirado no Content Hub](/help/assets/assets/view-download-expired-assets.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novo recursos de pré-lançamento no AEM Forms {#forms-new-prerelease-features}

#### Automático salvar um rascunho dos Componentes principais baseados em Forms adaptativos

Os usuários agora podem se beneficiar de um recurso de salvamento automático que salva automaticamente um formulário parcialmente preenchido como rascunho. Eles podem retornar mais tarde para terminar de preenchê-lo no mesmo dispositivo ou em outro. Esse recurso melhora as taxas de conversão para organizações ao reduzir o abandono de formulário, pois os usuários não precisam começar novamente o preenchimento do formulário desde o início.


### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Assistente de IA do AEM Forms

Ia generativa para Forms adaptável traz um novo nível de poder e facilidade aos processos de desenvolvimento de formulários. Ele permite que você build formulários melhores mais rápido do que nunca.

![Assistente de IA de Geração, Forms Adaptável](/help/forms/assets/generative-ai-assistant.png)

Os recursos de IA gerativa disponíveis são:

* **Assistente de IA para consultas de produtos**: obtenha respostas instantâneas para suas perguntas relacionadas ao formulário do AEM. O assistente de IA atua como sua própria base de conhecimento pessoal, fornecendo orientação e recomendações relevantes diretamente na plataforma.

* **Geração de formulário adaptável**: crie formulários completos sem esforço com prompts de IA geradores. A IA generativa da Adobe Systems gera automaticamente formulários usuário amigáveis que reduzem abandonos e personalizam as experiência.

* **Geração de painel para Forms**: gere seções de formulário adaptadas a necessidades específicas coleção de dados. Por exemplo, gere seções para coletar informações de pagamento, preferências do cliente ou detalhes de viagem.

* **Alteração de layouts** de formulário: Experimento com layouts e designs diferentes usando prompts de IA generativos. Experimente diferentes layouts curtir assistente ou exibições com guias para encontrar o ajuste perfeito para o seu formulário. Use prompts de IA generativos para otimizar seus formulários para responsividade móvel e criar formulários visualmente envolventes que os usuários amam.

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
* O número do pedido não está visível no Página de Confirmação de pedido.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Edge Side Includes (ESI) para Carregar Conteúdo dinâmico {#esi}

A CDN Gerenciada pelo Adobe agora oferece suporte a [ESI (Edge Side Includes)](/help/implementing/dispatcher/edge-side-includes.md), uma linguagem de marcação para o assembly de conteúdo dinâmico da Web no nível da borda. Ao incluir trechos ESI, você pode armazenar em cache a página geral do HTML na CDN com TTLs mais altos, enquanto busca com mais frequência a partir da origem as seções menores que exigem atualizações de cadência mais altas (TTLs mais baixos). Esse recurso será implementado gradualmente.

### Autenticação básica na CDN {#basicauth-cdn}

Proteja determinados recursos de conteúdo abrindo uma caixa de diálogo de autenticação básica que requer um nome de usuário e senha. Este recurso tem como alvo principalmente casos de uso de autenticação leves, curtir as partes interessadas em negócios que revisam conteúdo, em vez de servir como uma solução abrangente para direitos de acesso de usuário fim. A lista de nome de usuário e senhas é gerenciada por meio de um arquivo de configuração no Git que é implantado por meio do Pipeline de configuração, com uma referência a variáveis de ambiente do Tipo secreto do Cloud Manager. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

### Redirecionamentos do lado do servidor {#server-side-redirects}

Declare [navegador redireciona](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) em um arquivo de configuração Git implantado e avaliado no CDN. Isso pode ser útil para cenários como exclusão de páginas, alteração na estrutura do site e otimização SEO.

### Novo AEM Developer Console (Beta público) {#aem-developer-console-beta}

Experimente um [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) renovado, que oferece uma experiência mais interativa para depurar código em ambientes na nuvem.

Qualquer pessoa pode acessar o beta público clicando no botão *Novo Console Disponível* no Developer Console do AEM atual. O Adobe agradece o feedback, que você pode enviar por email para **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![Tela de Pacotes OSGi no AEM Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

### Usuários empresariais podem declarar redirecionamentos fora do Git (Early Adoter Program, Programa de primeiros usuários) {#apache-rewritemaps-early-adopter}

Semelhante ao AEM 6.5, o Apache/Dispatcher assimila mapas de regravação colocados em um local específico no repositório de publicação e os carrega sem exigir uma execução de pipeline no nível da Web. Essa abordagem permite que os usuários empresariais declarem redirecionamentos usando uma planilha ou uma interface do usuário, como o ACS Commons Redirect Map Manager ou um aplicativo personalizado. Participe do programa de adoção antecipada enviando um email para **<aemcs-cdn-config-adopter@adobe.com>**.

### Pipeline de configuração para RDEs (Early Adoter Program, programa de primeiros usuários) {#config-pipeline-rdes-early-adopter}

O [Pipeline de Configuração](/help/operations/config-pipeline.md) é usado para implantar configurações de arquivos yaml, incluindo opções de CDN (regras de filtro de tráfego, transformações de solicitação/resposta e assim por diante). Associe-se ao programa pioneiro enviando um email para **<aemcs-cdn-config-adopter@adobe.com>** para implantar essas mesmas configurações nos RDEs (Rapid Development Environments), que usam uma CLI.

## Guias do [!DNL Experience Manager] {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente dos Guias [de Adobe Experience Manager aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

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
