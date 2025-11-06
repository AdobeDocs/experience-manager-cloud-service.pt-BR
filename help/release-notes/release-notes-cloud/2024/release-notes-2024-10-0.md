---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.10.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.10.0.
feature: Release Information
role: Admin
exl-id: 7a63f04f-10f0-4879-bd06-4182bb288a9b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 12%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2024.10.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2024.10.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2022 ou 2023.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.10.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 31 de outubro de 2024. O próximo lançamento de recursos (2024.11.0) está planejado para sexta-feira, 21 de novembro de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo de Visão geral da versão de outubro de 2024 que exibe um resumo dos recursos adicionados na versão 2024.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3440501?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**Eventos de página modernizados**

Os seguintes eventos de página do AEM Sites agora estão disponíveis como eventos de consumo externo baseados na Plataforma de eventos do AEM as a Cloud Service. Os eventos podem ser processados por meio do Adobe I/O para interagir com processos externos.

* Página publicada
* Página não publicada
* Página excluída

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar variações**

Aproveite a GenAI por meio do novo recurso do AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta da Adobe para consideração no programa.

**OpenAPI REST do AEM para entrega de fragmentos de conteúdo**

A [OpenAPI REST do AEM para Entrega de Fragmento de Conteúdo](/help/headless/aem-content-fragment-delivery-with-openapi.md) está disponível agora para o AEM as a Cloud Service.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Recurso de acesso antecipado no Dynamic Media {#dm-early-access}

**Legendas de vídeo geradas por IA**

Legendas de vídeo geradas por IA no Adobe Dynamic Media usam inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. Esse recurso foi projetado para melhorar a acessibilidade e a experiência do usuário, fornecendo legendas precisas e em tempo real. A IA analisa a faixa de áudio do vídeo para transcrever a fala e criar legendas, que podem ser editadas para precisão ou personalização. Essas legendas ajudam a atender aos requisitos de acessibilidade e melhorar o envolvimento com o vídeo para públicos-alvo que dependem ou preferem suporte de vídeo baseado em texto.

Para obter acesso antecipado ao suporte a legendas geradas por IA em sua conta do Dynamic Media, [crie e envie um caso de Suporte ao Cliente da Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Novos recursos na visualização de ativos {#assets-view-new-features}

**Relatórios Agendados**

Agora os relatórios podem ser gerados automaticamente na visualização do Assets em uma programação recorrente ou em uma data futura, reduzindo o esforço de descobrir insights orientados por dados.

![Relatórios Agendados-](/help/assets/assets/scheduled-reports-tab.png)

### Novos recursos no Content Hub {#content-hub-new-features}

**Gerenciamento de direitos digitais para ativos licenciados**

Agora, as organizações podem aumentar a conformidade com a licença e minimizar o risco de compartilhar ativos com termos de licenciamento, aproveitando o DRM para ativos licenciados para usuários do Content Hub, exigindo que os usuários revisem e aceitem termos de licença antes de começar a baixar ativos licenciados. Para obter mais informações, consulte [Gerenciar ativos licenciados no Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

![baixar-várias-licenças](/help/assets/assets/download-multiple-license.png)

**Configuração de metadados do cartão de ativos**

O Content Hub agora permite configurar os campos de metadados principais que você precisa exibir no Cartão de ativos até um máximo de 6 campos. Para obter mais informações, consulte a seção Cartão de Ativo em [Configurar Content Hub](/help/assets/configure-content-hub-ui-options.md#asset-card).

![Metadados-chave no Cartão de Ativo](/help/assets/assets/asset-card-key-metadata.png)

**Configurar a visibilidade e o download de ativos expirados**

Agora, os administradores podem controlar se precisam que os ativos expirados estejam visíveis no Content Hub. Se os ativos expirados se tornarem visíveis, eles também poderão definir se os usuários podem baixá-los. Para obter mais informações, consulte a seção Assets Expirado em [Configurar Content Hub](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub).

![Ativos expirados no Content Hub](/help/assets/assets/expired-assets-content-hub.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novo recurso no AEM Forms {#forms-new-features}

* [Aprimorar a Experiência do Usuário com Botões de Navegação em Layouts de Painel](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button): Agora é possível adicionar botões de navegação aos layouts de painel, como Guias Horizontais, Guias Verticais, Acordeões ou Assistente. Esses botões melhoram a experiência do usuário simplificando as transições entre painéis, com foco no painel selecionado.

<!--* **Specify Display Styles for Document of Record (DoR) Components**: In an XFA file, you can now specify the display styles for Document of Record components. These styles can later be applied to the corresponding components in Adaptive Forms Editor.-->

### Novos recursos de pré-lançamento no AEM Forms {#forms-new-prerelease-features}

* [Salvar automaticamente um rascunho para os Componentes principais com base no Forms adaptável](/help/forms/save-core-component-based-form-as-draft.md): os usuários agora podem se beneficiar de um recurso de salvamento automático que salva automaticamente um formulário parcialmente preenchido como rascunho. Eles podem retornar mais tarde para terminar de preenchê-lo no mesmo dispositivo ou em outro. Esse recurso melhora as taxas de conversão para organizações ao reduzir o abandono de formulário, pois os usuários não precisam começar novamente o preenchimento do formulário desde o início.

* [Atualize facilmente os escopos do Adobe Sign](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms): você pode modificar os escopos de uma configuração do Adobe Sign diretamente da página Configurações de nuvem do AEM, tornando mais rápido e fácil atualizar as configurações existentes.

* [Suporte a função assíncrona para Forms Adaptável](/help/forms/using-async-funct-in-rule-editor.md): quando o Formulário Adaptável requer operações assíncronas, como aguardar processos externos ou recuperação de dados, você pode implementar essas operações com funções personalizadas e configurá-las no Editor de Regras.

### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Assistente de IA do AEM Forms

[A IA de geração para o Adaptive Forms](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features#aem-forms-ai-assistant-gen-ai) oferece um nível totalmente novo de potência e facilidade aos seus processos de desenvolvimento de formulários. Ele permite que você construa formulários melhores mais rápido do que nunca.

![Assistente de IA de Geração, Forms Adaptável](/help/forms/assets/generative-ai-assistant.png)

Os recursos de IA gerativa disponíveis são:

* **Assistente de IA para consultas de produtos**: obtenha respostas instantâneas para suas perguntas relacionadas ao formulário do AEM. O assistente de IA atua como sua própria base de conhecimento pessoal, fornecendo orientação e recomendações relevantes diretamente na plataforma.

* **Geração de formulário adaptável**: crie formulários completos sem esforço com prompts de IA geradores. A IA gerativa da Adobe gera automaticamente formulários amigáveis que reduzem as quedas e personalizam a experiência.

* **Geração de painel para Forms**: gere seções de formulário personalizadas para necessidades específicas de coleta de dados. Por exemplo, gere seções para coletar informações de pagamento, preferências do cliente ou detalhes da viagem.

* **Alterando Layouts de Formulário**: experimente diferentes layouts e designs usando prompts de IA geradores. Experimente diferentes layouts, como visualizações com assistente ou em abas, para encontrar o ajuste perfeito para o seu formulário. Use prompts de IA gerativos para otimizar seus formulários para a agilidade e criar formulários visualmente envolventes que os usuários adoram.

* **Configurar Ação de Envio**: use prompts de IA gerativa para configurar uma ação de envio facilmente para o seu formulário. Escolha entre uma biblioteca de ações de envio pré-criadas ou ações de envio personalizadas criadas e implantadas pela sua equipe de desenvolvimento.

>[!IMPORTANT]
>
> Interessado em participar do Programa de acesso antecipado para qualquer inovação da Forms? Envie um email de seu endereço oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) com a lista de recursos nos quais você está interessado.

## Complemento CIF {#cloud-services-cif}

### Correções de erros {#bug-fixes-cif}

* Correção dos testes de interface do usuário para funcionarem corretamente com componentes principais do CIF.
* Solução de um problema em que o formato de URL da categoria não funcionava como esperado na instância da nuvem.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Configuração para controlar envios de formulários {#configuration-submissions}

Para controlar os envios de formulários do Coral ou do Foundation em locais específicos, a AEM introduziu uma nova configuração: `com.adobe.granite.ui.components.FormRestrict`. Essa configuração consiste em dois campos:

1. **Adicionar Caminhos Permitidos**: especifica os caminhos em que as ações de formulário são permitidas.
1. **Restringir comportamento**: determina o comportamento de caminhos restritos (caminhos não incluídos na lista de permissões). Você pode escolher entre duas opções:
   * **Pop-up** (padrão): exibe uma notificação pop-up.
   * **Impedir**:Blocks envio de formulário.

>[!NOTE]
>
>Essa configuração não é compatível com todos os formulários do Coral ou Foundation localizados em `/apps`, `/libs`, `/mnt/overlay` e `/mnt/override`.

### Opção de encaminhamento de registro de autoatendimento com rede avançada {#log-forwarding}

Embora os logs do AEM (incluindo o Apache/Dispatcher) e do CDN possam ser baixados da Cloud Manager, muitas organizações acham útil transmitir esses logs para um destino de registro preferencial. A AEM agora oferece suporte ao [encaminhamento de logs](/help/implementing/developing/introduction/log-forwarding.md) para o Armazenamento Azure Blob, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Os logs do AEM podem ser encaminhados opcionalmente por configurações avançadas de rede, como o uso de um endereço IP dedicado.

Este recurso é configurado pelos usuários de maneira automatizada e implantado usando o [Pipeline de Configuração](/help/operations/config-pipeline.md).

### Redirecionamentos de URL sem pipeline para usuários empresariais {#pipeline-free-redirects}

Os redirecionamentos do lado do navegador são úteis quando uma página da Web foi desativada ou movida, ou outros cenários. Com os [Redirecionamentos de URL sem pipeline](/help/implementing/dispatcher/pipeline-free-url-redirects.md), você pode colocar um arquivo de mapa de regravação do Apache em um local de publicação do AEM, onde ele é carregado automaticamente. Não é necessário confirmar o arquivo no controle de origem ou iniciar um pipeline do Cloud Manager.

As opções para publicar o arquivo de regravação incluem carregá-lo como um ativo, usar o ACS Commons Rewrite Map Manager ou interagir com uma interface de usuário personalizada.

### Pipeline de configuração para RDEs {#config-pipeline-rdes}

Os ambientes de desenvolvimento rápido são uma ferramenta poderosa para implantar e testar rapidamente o código e a configuração em um ambiente em nuvem. Os RDEs agora oferecem suporte à [sincronização de arquivos YAML](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline) de configuração, incluindo configurações de CDN, como regras de filtro de tráfego e transformações de solicitação/resposta, bem como encaminhamento de logs e outras opções de configuração. [Consulte a lista completa](/help/operations/config-pipeline.md) de opções de configuração com suporte para obter mais detalhes.

### Novos perfis de produto {#new-product-profiles}

Quando um novo ambiente do AEM é criado, os Perfis de produto são exibidos automaticamente no Adobe Admin Console, permitindo que os administradores atribuam acesso a soluções e recursos licenciados.

Os novos ambientes agora incluem um conjunto atualizado de Perfis de produto, tornando-os compatíveis com recursos futuros, incluindo a geração de credenciais de API no Adobe Developer Console. Os ambientes existentes poderão atualizar seus Perfis de produto em uma versão futura. [Saiba mais](/help/onboarding/aem-cs-team-product-profiles.md).

### Novo AEM Developer Console (Beta público) {#aem-developer-console-beta}

Experimente um [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) renovado, que oferece uma experiência mais interativa para depurar código em ambientes na nuvem.

Qualquer pessoa pode acessar o beta público clicando no botão *Novo Console Disponível* no Developer Console do AEM atual. O Adobe agradece o feedback, que você pode enviar por email para **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![Tela de Pacotes OSGi no AEM Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

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
