---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.4.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.4.0.
exl-id: 153a3172-676f-4434-94d4-12fab8e17734
feature: Release Information
role: Admin
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '2689'
ht-degree: 11%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2024.4.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2024.4.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.4.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 25 de abril de 2024. O próximo lançamento de recursos (2024.5.0) está planejado para sexta-feira, 30 de maio de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de abril de 2024 que exibe um resumo dos recursos adicionados na versão 2024.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3446311?quality=12&captions=por_br)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar variações**

Aproveite a GenAI por meio do novo recurso do AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta da Adobe para consideração no programa.

**Navegação de ativos no Console de Fragmentos de Conteúdo**

Os autores de conteúdo agora podem navegar, visualizar e realizar ações em imagens e outros ativos sem precisar sair do Console de fragmentos de conteúdo.

![Navegação de ativos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Interessado em experimentar o recurso e compartilhar feedback? Envie um email para aemcs-headless-adopter@adobe.com a partir de sua ID de email oficial para saber mais sobre o programa dos participantes antecipados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na visualização de ativos {#assets-view-new-features}


**Pesquisa contextual**

Agora você também pode [pesquisar ativos disponíveis no repositório definindo prompts de texto](/help/assets/search-assets-view.md#contextual-search). O Experience Manager Assets transforma automaticamente esses prompts de texto em filtros de pesquisa e exibe os resultados da pesquisa. Você pode visualizar e modificar filtros automáticos usando o Painel de filtros para restringir ainda mais os resultados da pesquisa.

![Pesquisa contextual](/help/assets/assets/contextual-search-text-prompt1.png)

**Ações rápidas de vídeo expresso**

O Experience Manager Assets agora inclui [ferramentas de edição de vídeo fáceis e intuitivas viabilizadas pelo Adobe Express](/help/assets/edit-videos-assets-view.md) para aumentar a reutilização de conteúdo e acelerar a velocidade do conteúdo. As opções de edição incluem aparar, cortar, redimensionar um vídeo e também converter um MP4 em um arquivo GIF.

![cortar vídeo com o Adobe Express](/help/assets/assets/adobe-express-crop-video.png)

**Representações dinâmicas**

Agora você pode [exibir e baixar representações dinâmicas (incluindo cortes inteligentes)](/help/assets/renditions.md) no Experience Manager Assets. As representações dinâmicas são versões personalizadas de ativos de imagem criados em tempo real para atender a necessidades específicas, como redimensionar imagens com base na resolução do dispositivo ou recortar para se ajustar a diferentes taxas de aspecto. Essas representações permitem que as organizações entreguem experiências personalizadas e otimizadas para diversas necessidades do público-alvo.

![Representações dinâmicas](/help/assets/assets/preset_smart_crop.png)

**Renomeação no local para ativos e pastas**

O Experience Manager Assets agora oferece uma experiência de usuário simplificada, fornecendo a [capacidade de renomear um ativo ou uma pasta com um único clique](/help/assets/manage-organize-assets-view.md).

**Atribuir ou remover um formulário de metadados a várias pastas**

Agora você pode [atribuir ou remover o formulário de metadados a várias pastas](/help/assets/metadata-assets-view.md#assign-metadata-form-to-a-folder).

### Novos recursos na exibição do Administrador {#admin-view-new-features}

**Configuração de compartilhamento de link**

Uma nova experiência de usuário aprimorada para [criar compartilhamentos de links](/help/assets/share-assets.md) e um novo conjunto de configurações que permite que admins personalizem o comportamento padrão desse recurso para seus usuários.

![Configuração de compartilhamento de links](/help/assets/assets/config-email-service.png)



## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Novos recursos no AEM Forms {#forms-new-features}

* **Editor de regras visuais aprimorado para Forms adaptável baseado em componentes principais**: esta versão traz uma atualização significativa para o editor de regras visuais no que se refere a formulários adaptáveis baseados em componentes principais. Esta versão traz uma atualização significativa para o editor visual de regras para formulários adaptáveis com base em componentes principais. Essa atualização se concentra em simplificar as interações com funções personalizadas, permitindo que você crie formulários mais robustos e eficientes.

  Agora é possível simplificar as interações de funções personalizadas ao:

   * [Aproveitando novas anotações para fornecer definições de função mais claras](/help/forms/create-and-use-custom-functions.md#supported-javascript-annotations-for-custom-function).
   * [Usando mecanismos de cache para funções personalizadas, resultando em um desempenho de formulário mais rápido](/help/forms/create-and-use-custom-functions.md#caching-support-for-custom-function).
   * [Trabalhando perfeitamente com objetos globais dentro de funções personalizadas](/help/forms/create-and-use-custom-functions.md#field-and-global-scope-objects-in-custom-functions).
   * [Definindo e utilizando parâmetros opcionais dentro de funções personalizadas](/help/forms/create-and-use-custom-functions.md#parameter).

  Essa atualização também traz os seguintes aprimoramentos para a funcionalidade do editor de regras. É possível:

   * Implemente uma lógica [&quot;when-then-else&quot;](/help/forms/rule-editor-core-components.md#when) poderosa para execução condicional.
   * Aproveite os recursos modernos do JavaScript, como as funções de seta e de esquerda (suporte para ES10).
   * Valide ou redefina não apenas campos, mas também painéis e formulários inteiros, expandindo o controle sobre as interações do usuário.

  Esses avanços fornecem uma experiência mais intuitiva e poderosa para criar regras e funções personalizadas no editor visual de regras.

* **[Criar várias versões de um Formulário adaptável](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)**: agora é possível gerenciar facilmente variações de formulários existentes. Isso simplifica o controle de versões e facilita a comparação para a otimização de formulários, tudo em um único fluxo de trabalho simplificado.

* **[Comparar formulário adaptável](/help/forms/compare-forms.md)**: agora é possível comparar facilmente dois formulários para identificar as diferenças entre dois formulários. Ele facilita a colaboração perfeita, permitindo que os membros da equipe comparem revisões e discutam alterações com eficiência.

* **Aprimoramentos de Acessibilidade para o Componente de Assinatura Escrita**: esta atualização traz melhorias significativas de acessibilidade para o componente de Assinatura Escrita:

  **Navegação do Teclado Aprimorada:**
   * Pressionar a tecla Tab permite que os usuários naveguem por todos os elementos interativos na caixa de diálogo de assinatura.
   * Assinar com um pincel ou teclado e pressionar Enter fecha a caixa de diálogo.
   * O foco permanece no controle de assinatura após assinar e clicar em &quot;OK&quot;.

  **Limpar Funcionalidade de Assinatura:**

   * Um ícone de cruz claro para apagar a assinatura é acessível através da tecla Tab.
   * A caixa de diálogo &quot;Limpar confirmação de assinatura&quot; também pode ser acessada por meio da navegação de guias.

  **Rótulos e Controles Aprimorados:**
   * O rótulo do botão de assinatura do teclado agora está mais claro, usando &quot;aria-label&quot; para anunciar a funcionalidade (como &quot;aria-label=&#39;Sign using Keyboard&#39;&quot;).
   * O contraste aprimorado garante que todos os controles dentro da assinatura de rabisco sejam facilmente distinguíveis.
   * O botão OK/marca de seleção agora indica visualmente quando está inativo.

  **Feedback de Assinatura para Leitores de Tela:**
   * Quando uma assinatura é digitada, os usuários de leitores de tela podem ouvir o texto usado para criar a assinatura.

Essa atualização garante uma experiência mais inclusiva para usuários portadores de deficiências, melhorando a navegação, a clareza e o feedback do componente Assinatura Escrita.

### Programa de adoção antecipada {#forms-early-adopter}

* **[Enviar um Formulário adaptável para o Cenário do Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: o Forms as a Cloud Service oferece uma opção pronta para uso para conectar facilmente um Formulário adaptável ao Adobe Workfront. Isso simplifica o processo de envio de um Formulário adaptável para um cenário do Adobe Workfront, permitindo acionar um cenário do Workfront Fusion no envio de um Formulário adaptável.

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> Usando o Adobe Workfront Fusion Connector, você pode criar fluxos de trabalho que são acionados automaticamente no envio de um Formulário adaptável. Por exemplo, preveja um cenário em que um fluxo de trabalho é iniciado para atribuir a um indivíduo específico a tarefa de revisar dados enviados, permitindo a aprovação ou a rejeição de um aplicativo com base nas informações capturadas por meio do formulário adaptável. Essa integração simplificada aumenta a eficiência e traz um novo nível de automação para seus processos de workflow.|

* **[Serviço de Extensão do Reader](/help/forms/aem-forms-cloud-service-communications-introduction.md#reader-extension-service)**: as APIs de Comunicação da AEM Forms trouxeram o Serviço de Extensão do Reader para permitir que você adicione funcionalidades como preenchimento de formulários e comentários em PDFs comuns, tornando-os interativos para usuários com o Adobe Reader gratuito.

* [Suporte de idiomas da direita para a esquerda](/help/forms/supporting-new-language-localization-core-components.md): o Forms adaptável integrado aos Componentes principais agora pode ser apresentado em um idioma da direita para a esquerda (RTL), como árabe, persa e urdu. As línguas RTL são faladas por mais de 2 bilhões de pessoas em todo o mundo. Usar um formulário em linguagem RTL permite estender o alcance dos formulários adaptáveis para atender a esses públicos diferentes e selecionar mercados de RTL. Em algumas regiões, também é um mandato legal fornecer formulários no idioma local. Ao acomodar idiomas locais, você não só abre portas para um público mais amplo, como também garante a conformidade com as leis e regulamentos relevantes.

* **[Proteja seus documentos com as APIs do DocAssurance (Parte das APIs de Comunicação)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: as APIs do DocAssurance permitem proteger informações confidenciais ao assinar e criptografar os documentos. Por meio da criptografia, o conteúdo de um documento é transformado em um formato ilegível, garantindo que somente usuários autorizados possam ter acesso. Essa camada fortificada de proteção não apenas protege dados valiosos de olhos não autorizados, mas também proporciona tranquilidade. As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos.

  Você pode escrever para `aem-forms-ea@adobe.com` a partir de sua ID de email oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso.

* **[Você pode aproveitar o Serviço de Telemetria Operacional](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** para habilitar a coleção no lado do cliente para o AEM as a Cloud Service.
O Serviço de Telemetria Operacional oferece um reflexo mais preciso das interações do usuário, garantindo uma medida confiável de envolvimento do site. É uma ótima oportunidade para obter insights avançados sobre o desempenho da página. Embora isso seja benéfico para clientes que usam CDN gerenciada pela Adobe ou CDN não gerenciada pela Adobe. Além disso, para clientes que usam um CDN gerenciado pela Adobe, o relatório de tráfego automatizado agora pode ser ativado para eles, eliminando a necessidade de compartilhar qualquer relatório de tráfego com a Adobe.

  Se você estiver interessado em testar esse novo recurso e compartilhar seus comentários, envie um email para `aemcs-rum-adopter@adobe.com`, juntamente com o nome de domínio de cada um dos ambientes para os quais você deseja habilitar a Telemetria Operacional no seu endereço de email associado à sua Adobe ID. A equipe de produtos da Adobe habilitará o Serviço de Telemetria Operacional para você.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Mapeamento de domínio {#cdn-config}

Configure o tráfego na CDN do Adobe das seguintes maneiras:

* [Solicitar transformações](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) - modifique aspectos de solicitações de entrada, incluindo caminhos, parâmetros de consulta e cabeçalhos HTTP antes de serem roteados para o AEM.
* [Transformações de resposta](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) - altere os cabeçalhos HTTP das respostas de saída antes que elas sejam enviadas ao navegador.
* [Seletores de origem](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations#origin-selectors) - rotear o tráfego pela CDN para sites e aplicativos fora da AEM.

Depois que essas regras forem declaradas no controle do código-fonte (Git), você poderá implantá-las na CDN usando o pipeline de configuração do Cloud Manager. Consulte também o recurso de redirecionamentos do lado do cliente na seção inicial do adotante abaixo.

### Páginas de erro personalizadas do CDN {#cdn-error-pages}

No caso improvável de o CDN não poder rotear o tráfego para a origem do AEM, uma página de erro personalizada pode ser declarada, substituindo a versão genérica. [Saiba mais](/help/implementing/dispatcher/cdn-error-pages.md) sobre como fornecer páginas de erro de marca.

### Programas de adoção antecipada {#foundation-early-adopter}

#### Redirecionamentos do lado do servidor (programa de primeiros usuários) {#server-side-redirects-early-adopter}

Configure os redirecionamentos do lado do servidor 301/302 no controle do código-fonte e implante na CDN. [Saiba mais](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) e participe do programa de adoção antecipada enviando um email para **<aemcs-cdn-config-adopter@adobe.com>**.

#### Alertas de regras de filtro de tráfego (Programa de adoção antecipada) {#traffic-filter-rules-alerts-early-adopter}

As [Regras de Filtro de Tráfego](/help/security/traffic-filter-rules-including-waf.md) recém-lançadas, que incluem as regras do WAF (Firewall de Aplicativo Web) opcionalmente licenciáveis, permitem que você configure qual tráfego deve ser permitido ou negado.

Agora você pode enviar um email a **<aemcs-cdn-config-adopter@adobe.com>** para ingressar no programa de adoção antecipada, para que possa ser alertado sempre que suas regras de filtro de tráfego forem acionadas. As notificações por email do Centro de ações manterão você informado quando ocorrerem determinadas condições de tráfego para que você possa tomar as medidas apropriadas.

#### Assimilação de mapas de regravação no tempo de execução do Apache/Dispatcher (Programa de adoção antecipada) {#apache-rewritemaps-early-adopter}

Semelhante ao AEM 6.5, o Apache/Dispatcher assimilará mapas de regravação colocados em um local específico no repositório de publicação e os carregará, sem exigir uma execução de pipeline no nível da Web. Isso abre oportunidades para que um usuário empresarial declare redirecionamentos usando uma interface do usuário, como a oferecida pelo ACS Commons Redirect Map Manager. Contate **<aemcs-cdn-config-adopter@adobe.com>** para obter mais informações.

#### O Edge Side Includes (ESI) para Carregar Conteúdo Dinâmico (Early Adoter Program) {#esi-early-adopter}

O Adobe Managed CDN agora é compatível com o Edge Side Includes (ESI), uma linguagem de marcação para a compilação de conteúdo dinâmico da Web no nível da borda. Ao incluir trechos ESI, você pode armazenar em cache a página geral do HTML na CDN com TTLs mais altos, enquanto busca com mais frequência a partir da origem as seções menores que exigem atualizações de cadência mais altas (TTLs mais baixos). Contate **<aemcs-cdn-config-adopter@adobe.com>** para obter mais informações.

#### Suporte RDE para código de front-end usando temas de site e modelos de site (programa de adoção antecipada) {#rde-frontend-early-adopter}

Os [Ambientes de Desenvolvimento Rápido (RDEs)](/help/implementing/developing/introduction/rapid-development-environments.md) agora oferecem suporte ao código front-end com base nos [temas de site](/help/sites-cloud/administering/site-creation/site-themes.md) e nos [modelos de site](/help/sites-cloud/administering/site-creation/site-templates.md), para usuários iniciais. Com RDEs, isso é feito usando uma diretiva de linha de comando, em vez de um [pipeline de front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Entre em contato com **<aemcs-rde-support@adobe.com>** para experimentar e fornecer feedback.

#### Melhoria no registro para RDEs (Early Adoter Program, programa de adoção antecipada) {#rde-logging-early-adopter}

Ao depurar o código em um [Ambiente de Desenvolvimento Rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md), os desenvolvedores agora podem configurar e transmitir logs com mais eficiência, usando a linha de comando e sem modificar as propriedades OSGI no controle de versão. Os recursos incluem:

* declarar níveis de log em um nível por pacote ou classe
* personalizar o formato de saída do registro
* transmitir vários logs em paralelo

Entre em contato com **<aemcs-rde-support@adobe.com>** para experimentar e fornecer feedback.

## Guias do [!DNL Experience Manager] {#guides}

### Capacidade de traduzir conteúdo em vários idiomas usando grupos de idiomas pré-configurados

O Experience Manager Guides agora permite criar grupos de idiomas e traduzir facilmente seu conteúdo em vários idiomas. Esse recurso ajuda a organizar e gerenciar traduções de acordo com as necessidades da organização.

Por exemplo, se você precisar traduzir o conteúdo para alguns países na Europa, é possível criar um grupo de idiomas para idiomas europeus, como inglês (EN), francês (FR), alemão (DE), espanhol (ES) e italiano (IT).

![painel de tradução](/help/release-notes/assets/guides/translation-languages-2404.png)

*Selecione os grupos de idiomas ou idiomas para os quais você deseja traduzir os documentos.*

>[!NOTE]
>
>Se a pasta de destino de um idioma estiver ausente ou se o idioma de destino for o mesmo da origem, ele ficará esmaecido e exibirá um sinal de aviso.

Como administrador, você pode criar grupos de idiomas e configurá-los para vários perfis de pasta. Como autor, você pode exibir os grupos de idiomas configurados no perfil da pasta.


De modo geral, a criação de grupos de idiomas aumenta a eficiência e a produtividade dos projetos de tradução, melhorando, em última análise, o processo de localização em vários idiomas.

### Experiência remodelada para pesquisar e filtrar arquivos na visualização de repositório

Agora, você tem uma experiência aprimorada ao filtrar arquivos. A funcionalidade renovada para filtrar arquivos fornece uma maneira aprimorada de pesquisar e navegar facilmente pelos arquivos.

![pesquisar arquivos no modo de exibição de repositório](/help/release-notes/assets/guides/repository-filter-search-2404.png)

*Pesquisar os arquivos que contêm o texto`general purpose.`*

Aproveite benefícios como acesso mais rápido a arquivos relevantes e uma interface do usuário mais intuitiva, tornando sua experiência de pesquisa mais estável e eficiente.

![filtro de pesquisa rápida &#x200B;](/help/release-notes/assets/guides/repository-filter-search-quick.png)

*Use os filtros rápidos para procurar arquivos DITA e não DITA.*

Saiba mais sobre o recurso **Pesquisa de filtro** na seção [Painel esquerdo](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/user-guide/author-content/create-preview-topics/author-content-aem-guides/work-with-web-editor/web-editor-features#id2051EA0M0HS).

### Melhorias nos Data Source Connectors

Os seguintes aprimoramentos foram feitos nos conectores de fonte de dados da versão 2024.4.0:

#### Conecte-se às Fontes de Dados dos Quadros de Desenvolvimento (ADO) do Salsify, Akeneo e Microsoft Azure

Além dos conectores prontos para uso existentes, o Experience Manager Guides também fornece conectores para fontes de dados do Salsify, Akeneo e Microsoft Azure DevOps Boards (ADO). Como administrador, você pode baixar e instalar esses conectores. Em seguida, configure os conectores instalados.

#### Copie e cole a amostra de consulta para criar um trecho de conteúdo ou tópico

Você pode copiar e colar facilmente uma amostra de consulta de dados no gerador para criar um trecho de conteúdo ou tópico. Com esse recurso, não é necessário lembrar a sintaxe ou criar um query manualmente. Em vez de digitar manualmente a consulta, você pode copiar e colar uma consulta de exemplo, editá-la e usá-la para buscar os dados de acordo com suas necessidades.

![caixa de diálogo inserir trecho do conteúdo](/help/release-notes/assets/guides/insert-content-snippet.png)

*Copie e edite uma consulta de exemplo para criar o trecho de conteúdo.*

#### Conectar-se a arquivos de dados JSON usando um conector de arquivos


Agora, como administrador, você pode configurar um conector de arquivo JSON para usar arquivos de dados JSON como fonte de dados. Use o conector para importar os arquivos JSON do seu computador ou do Adobe Experience Manager Assets. Em seguida, como autor, você pode criar fragmentos de conteúdo ou tópicos usando os geradores.

Esse recurso ajuda você a usar os dados armazenados em seus arquivos JSON e reutilizá-los em vários snippets. O conteúdo também é atualizado dinamicamente sempre que você atualiza os arquivos JSON.

#### Configurar vários URLs de recursos para um conector criar trechos de conteúdo ou tópicos

Como administrador, você pode configurar vários URLs de recursos para alguns conectores, como Cliente REST genérico, Salsify, Akeneo e placas DevOps (ADO) do Microsoft Azure.
Em seguida, como autor, conecte-se às fontes de dados para criar trechos de conteúdo ou tópicos usando os geradores. Esse recurso é útil, pois você não precisa criar uma fonte de dados para cada URL. Ele ajuda você a buscar dados rapidamente de qualquer um dos recursos de uma fonte de dados específica em um único trecho de conteúdo ou tópico. Exibir mais detalhes sobre os conectores de fonte de dados e como [configurar um conector de fonte de dados na interface do usuário](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/install-guide/cs-ig/web-editor-configs-cs/conf-data-source-connector-tools). Saiba como [usar dados da sua fonte de dados](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/user-guide/author-content/create-preview-topics/author-content-aem-guides/work-with-web-editor/web-editor-content-snippet).

Para obter mais informações sobre os novos recursos e aprimoramentos, exiba [informações sobre as versões do Experience Manager Guides](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
