---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais para  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 08b23f093e4362a9885919a3e3d87bdcaada8876
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 11%

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

A data de lançamento da versão atual (2024.10.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 31 de outubro de 2024. O próximo lançamento de recursos (2024.11.0) está planejado para sexta-feira, 21 de novembro de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- ## Release Video {#release-video}

Have a look at the October 2024 Release Overview video for a summary of the features added in the 2024.10.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**Eventos de página modernizados**

Os seguintes eventos de página do AEM Sites agora estão disponíveis como eventos de consumo externo baseados na Plataforma de eventos do AEM as a Cloud Service. Os eventos podem ser processados por meio do Adobe I/O para interagir com processos externos.
* Página publicada
* Página não publicada
* Página excluída

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar Variações**

Aproveite a GenAI por meio do novo recurso AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta do Adobe para consideração no programa.

AEM **OpenAPI REST para Entrega de Fragmento de Conteúdo**

A [OpenAPI REST para Entrega de Fragmento de Conteúdo](/help/headless/aem-rest-openapi-content-fragment-delivery.md) do AEM está disponível agora para o AEM as a Cloud Service.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Recurso de acesso antecipado no Dynamic Media {#dm-early-access}

**Legendas de vídeo geradas por IA**

Legendas de vídeo geradas por IA no Adobe Dynamic Media usam inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. Esse recurso foi projetado para melhorar a acessibilidade e a experiência do usuário, fornecendo legendas precisas e em tempo real. A IA analisa a faixa de áudio do vídeo para transcrever a fala e criar legendas, que podem ser editadas para precisão ou personalização. Essas legendas ajudam a atender aos requisitos de acessibilidade e melhorar o envolvimento com o vídeo para públicos-alvo que dependem ou preferem suporte de vídeo baseado em texto.

Para obter acesso antecipado ao suporte a legendas geradas por IA em sua conta da Dynamic Media, [crie e envie um caso de Suporte ao Cliente do Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Novos recursos na visualização de ativos {#assets-view-new-features}

**Relatórios Agendados**

Agora os relatórios podem ser gerados automaticamente na visualização do Assets em uma programação recorrente ou em uma data futura, reduzindo o esforço de descobrir insights orientados por dados.

![Relatórios Agendados-](/help/assets/assets/scheduled-reports-tab.png)

### Novos recursos no Content Hub {#content-hub-new-features}

**Gerenciamento de direitos digitais para ativos licenciados**

Agora, as organizações podem aumentar a conformidade com a licença e minimizar o risco de compartilhar ativos com termos de licenciamento, aproveitando o DRM para ativos licenciados para usuários do Content Hub, exigindo que os usuários revisem e aceitem termos de licença antes de começar a baixar ativos licenciados.

![baixar-várias-licenças](/help/assets/assets/download-multiple-license.png)

**Configuração de metadados do cartão de ativos**

O Content Hub agora permite configurar os campos de metadados principais que você precisa exibir no Cartão de ativos até um máximo de 6 campos.

![Metadados-chave no Cartão de Ativo](/help/assets/assets/asset-card-key-metadata.png)

**Configurar a visibilidade e o download de ativos expirados**

Agora, os administradores podem controlar se precisam que os ativos expirados estejam visíveis no Content Hub. Se os ativos expirados se tornarem visíveis, eles também poderão definir se os usuários podem baixá-los.

![Ativos expirados no Content Hub](/help/assets/assets/expired-assets-content-hub.png)

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

### Correções de erros {#bug-fixes-cif}

* Correção dos testes de interface do usuário para funcionarem corretamente com os componentes principais do CIF.
* Solução de um problema em que o formato de URL da categoria não funcionava como esperado na instância da nuvem.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Configuração para controlar envios de formulários {#configuration-submissions}

Para controlar os envios de formulários do Coral ou do Foundation em locais específicos, o AEM introduziu uma nova configuração: `com.adobe.granite.ui.components.FormRestrict`. Essa configuração consiste em dois campos:

1. **Adicionar Caminhos Permitidos**: especifica os caminhos em que as ações de formulário são permitidas.
1. **Restringir comportamento**: determina o comportamento de caminhos restritos (caminhos não incluídos na lista de permissões). Você pode escolher entre duas opções:
   * **Pop-up** (padrão): exibe uma notificação pop-up.
   * **Impedir**:Bloqueia o envio de formulários.

>[!NOTE]
>
>Essa configuração não é compatível com todos os formulários do Coral ou Foundation localizados em `/apps`, `/libs`, `/mnt/overlay` e `/mnt/override`.

### Opção de encaminhamento de registro de autoatendimento com rede avançada {#log-forwarding}

Embora o AEM (incluindo o Apache/Dispatcher) e os logs de CDN possam ser baixados da Cloud Manager, muitas organizações acham útil transmitir esses logs para um destino de registro preferencial. O AEM agora oferece suporte ao [encaminhamento de logs](/help/implementing/developing/introduction/log-forwarding.md) para Azure Blob Storage, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Os logs de AEM podem ser encaminhados opcionalmente por configurações avançadas de rede, como o uso de um endereço IP dedicado.

Este recurso é configurado pelos usuários de maneira automatizada e implantado usando o [Pipeline de Configuração](/help/operations/config-pipeline.md).

### Redirecionamentos de URL sem pipeline para usuários empresariais {#pipeline-free-redirects}

Os redirecionamentos do lado do navegador são úteis quando uma página da Web foi desativada ou movida, ou outros cenários. Com os [Redirecionamentos de URL sem pipeline](/help/implementing/dispatcher/pipeline-free-url-redirects.md), você pode colocar um arquivo de mapa de regravação do Apache em um local de publicação do AEM, onde ele é carregado automaticamente. Não é necessário confirmar o arquivo no controle de origem ou iniciar um pipeline do Cloud Manager.

As opções para publicar o arquivo de regravação incluem carregá-lo como um ativo, usar o ACS Commons Rewrite Map Manager ou interagir com uma interface de usuário personalizada.

### Pipeline de configuração para RDEs {#config-pipeline-rdes}

Os ambientes de desenvolvimento rápido são uma ferramenta poderosa para implantar e testar rapidamente o código e a configuração em um ambiente em nuvem. Os RDEs agora oferecem suporte à [sincronização de arquivos YAML](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline) de configuração, incluindo configurações de CDN, como regras de filtro de tráfego e transformações de solicitação/resposta, bem como encaminhamento de logs e outras opções de configuração. [Consulte a lista completa](/help/operations/config-pipeline.md) de opções de configuração com suporte para obter mais detalhes.

### Novos perfis de produto {#new-product-profiles}

Quando um novo ambiente AEM é criado, os Perfis de produto são exibidos automaticamente no Adobe Admin Console, permitindo que os administradores atribuam acesso a soluções e recursos licenciados.

Os novos ambientes agora incluem um conjunto atualizado de Perfis de produto, tornando-os compatíveis com recursos futuros, incluindo a geração de credenciais de API no Adobe Developer Console. Os ambientes existentes poderão atualizar seus Perfis de produto em uma versão futura. [Saiba mais](/help/onboarding/aem-cs-team-product-profiles.md).

### Novo AEM Developer Console (Beta público) {#aem-developer-console-beta}

Experimente um [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) renovado, que oferece uma experiência mais interativa para depurar código em ambientes na nuvem.

Qualquer pessoa pode acessar o beta público clicando no botão *Novo Console Disponível* no Developer Console AEM atual. O Adobe agradece o feedback, que você pode enviar por email para **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![Tela de Pacotes OSGi no AEM Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

## Guias do [!DNL Experience Manager] {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente do Adobe Experience Manager Guides [aqui](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0).

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
