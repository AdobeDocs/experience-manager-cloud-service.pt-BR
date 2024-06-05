---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.3.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2024.3.0.
exl-id: b3816929-2c0a-4d6a-b583-c928d2182ecd
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '2292'
ht-degree: 8%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2024.3.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2024.3.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.3.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 11 de abril de 2024. O próximo lançamento de recursos (2024.4.0) está planejado para sexta-feira, 25 de abril de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de março de 2024 que exibe um resumo dos recursos adicionados na versão 2024.3.0:

>[!VIDEO](https://video.tv.adobe.com/v/3428342?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no [!DNL Experience Manager Sites] {#sites-features}

**Criação de AEM para Edge Delivery Services**

O AEM Sites agora pode ser usado como fonte de conteúdo para o Edge Delivery Services. Os autores gerenciam seus sites no AEM usando o novo Universal Editor com criação wysiwyg no contexto. Isso permite que as empresas criem páginas da Web rápidas e de alto desempenho com o Edge Delivery Services e, ao mesmo tempo, aproveitem os poderosos recursos de AEM para o gerenciamento de conteúdo.

![Criação no AEM](/help/edge/assets/universal_editor_edge_delivery_services.png)

Para obter mais informações, consulte [documentação](/help/edge/overview.md) e assista ao [Gems do AEM - Introdução à criação e aos Edge Delivery Services do AEM](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-gems-getting-started-with-aem-authoring-and-edge-delivery/m-p/652694#M43905)

**Editor universal para implementações headless**

O Editor universal também permite que aplicativos web dissociados utilizem a mesma criação intuitiva em contexto WYSIWYG, anteriormente exclusiva de sites tradicionais. Os criadores de conteúdo agora podem compor visualmente layouts usando fragmentos de conteúdo com a mesma facilidade que os componentes dentro das páginas.

O que diferencia o Editor Universal é sua adaptabilidade a diversas arquiteturas da Web, acomodando renderização no lado do servidor e do cliente, mantendo-se independente de estrutura e eliminando a necessidade de hospedagem do AEM. Integrar aplicativos web existentes com o Universal Editor para edição de conteúdo é simples, exigindo principalmente que os desenvolvedores incorporem atributos de dados específicos em suas marcações.

Com isso, o Editor universal garante uma experiência de edição consistente, independentemente da estrutura do conteúdo ou da pilha de tecnologia subjacente. Para obter mais informações, consulte [Introdução ao Universal Editor](/help/implementing/universal-editor/introduction.md).

**OpenAPIs de gerenciamento de conteúdo para fragmentos e modelos de conteúdo**

Agora os desenvolvedores podem interagir programaticamente com os Fragmentos de conteúdo e modelos de Fragmento de conteúdo e executar operações de CruD neles usando as OpenAPIs de gerenciamento de conteúdo. Para obter mais informações, consulte [Documentação da API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)

**Suporte de gerenciamento de vários sites para Fragmentos de experiência**

O suporte ao Gerenciamento multisite foi estendido para estruturas de pastas que armazenam fragmentos de experiência, permitindo que os usuários implantem uma estrutura de conteúdo completa com fragmentos de experiência.

**Comparar versões de fragmentos de conteúdo**

O novo Editor de fragmento de conteúdo agora permite que os autores de conteúdo comparem e visualizem diferenças entre a versão atual de um fragmento de conteúdo e uma versão anterior.

### Programa de adoção antecipada {#sites-early-adopter}

**Gerar variações**

Aproveite a GenAI por meio do novo recurso AEM, [gerar variações](/help/generative-ai/generate-variations.md), acessível agora no Cloud Service. Gerar variações ajuda a gerar e dimensionar a criação de conteúdo por meio do uso de IA gerativa. Entre em contato com a equipe de conta do Adobe para consideração no programa.

**Navegação de ativos no Console de fragmentos de conteúdo**

Os autores de conteúdo agora podem navegar, visualizar e realizar ações em imagens e outros ativos sem precisar sair do Console de fragmentos de conteúdo.

![Navegação de ativos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Interessado em experimentar o recurso e compartilhar feedback? Envie um email para aemcs-headless-adopter@adobe.com a partir de sua ID de email oficial para saber mais sobre o programa dos participantes antecipados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na exibição do Administrador {#admin-view}

**Integração nativa com o Adobe Express**

A AEM Assets integra-se nativamente com o Adobe Express, o que permite acessar diretamente os ativos armazenados no AEM Assets na interface do usuário do Adobe Express. Você pode colocar o conteúdo gerenciado no AEM Assets na tela Express e depois salvar o conteúdo novo ou editado em um repositório do AEM Assets.

![Incluir ativos do complemento Assets](/help/assets/assets/adobe-express-native-integration.png)

**Visualizar representações para todos os tipos de vídeo compatíveis**

O Experience Manager Assets agora gera representações de pré-visualização de todos os tipos de vídeo compatíveis por padrão, sem exigir uma configuração de perfil de processamento.

### Novos recursos na visualização de ativos {#assets-view}

**Gerenciar permissões para coleções**

O Assets Essentials permite que os administradores gerenciem os níveis de acesso para coleções privadas disponíveis no repositório. Como administrador, você pode criar grupos de usuários e atribuir permissões a esses grupos para gerenciar níveis de acesso. Você também pode delegar os privilégios de gerenciamento de permissões a grupos de usuários.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Novos recursos para o AEM Forms {#forms-new-features}

* **[Adobe Experience Manager Forms Edge Delivery Services](/help/edge/docs/forms/overview.md)**: o AEM Forms Edge Delivery Services é um conjunto de serviços combináveis que permite um ambiente de desenvolvimento rápido, em que os autores podem atualizar, publicar e lançar novos formulários rapidamente. Esses serviços oferecem experiências de formulários excepcionais e de alto impacto que impulsionam o engajamento e as conversões. Essas experiências de formulários são fáceis de criar e desenvolver.

  ![Recursos do EDS Forms](/help/edge/assets/eds-forms-features.png)

Esses serviços permitem:

* Trabalhe com várias fontes de conteúdo no mesmo site de formulários e use suas ferramentas de criação preferidas, como o Microsoft Excel, o Google Sheets ou o Adaptive Forms Editor.
* Ofereça experiências de Inscrição digital que carregam e renderizam de forma rápida e contínua, monitorando o desempenho de seus formulários por meio do monitoramento real de usuários (RUM).
* Use HTML simples, CSS moderno e JavaScript padrão para criar experiências excepcionais, evitando a curva de aprendizado íngreme de uma estrutura específica.


### Novos recursos no Pré-lançamento do AEM Forms {#forms-pre-release}

* **Editor de regras visuais aprimorado para Forms adaptável baseado em componentes principais**: esta versão traz uma atualização significativa ao editor visual de regras para formulários adaptáveis com base em componentes principais. Esta versão traz uma atualização significativa para o editor visual de regras para formulários adaptáveis com base em componentes principais. Essa atualização se concentra em simplificar as interações com funções personalizadas, permitindo que você crie formulários mais robustos e eficientes.

  Agora é possível simplificar as interações de funções personalizadas ao:

   * Uso de novas anotações para fornecer definições de função mais claras.
   * Uso de mecanismos de armazenamento em cache para funções personalizadas, resultando em um desempenho de formulário mais rápido.
   * Trabalhar perfeitamente com objetos globais dentro de funções personalizadas.
   * Definição e utilização de parâmetros opcionais em funções personalizadas.

  Essa atualização também traz os seguintes aprimoramentos para a funcionalidade do editor de regras. É possível:

   * Implemente uma lógica poderosa do tipo &quot;quando-então-mais&quot; para execução condicional.
   * Aproveite os recursos modernos do JavaScript, como as funções de seta e de esquerda (suporte para ES10).
   * Valide ou redefina não apenas campos, mas também painéis e formulários inteiros, expandindo o controle sobre as interações do usuário.

  Esses avanços fornecem uma experiência mais intuitiva e poderosa para criar regras e funções personalizadas no editor visual de regras.

* **Criar várias versões de um Formulário adaptável**: Agora é possível gerenciar facilmente variações de formulários existentes. Isso simplifica o controle de versões e facilita a comparação para a otimização de formulários, tudo em um único fluxo de trabalho simplificado.

* **Comparar formulário adaptável**: agora é possível comparar facilmente dois formulários para identificar as diferenças entre dois. Ele facilita a colaboração perfeita, permitindo que os membros da equipe comparem revisões e discutam alterações com eficiência.

* **Aprimoramentos de acessibilidade para o componente de assinatura assinável**: esta atualização traz melhorias significativas de acessibilidade para o componente de Assinatura Escrita:

  **Navegação do teclado aprimorada:**
   * Pressionar a tecla Tab permite que os usuários naveguem por todos os elementos interativos na caixa de diálogo de assinatura.
   * Assinar com um pincel ou teclado e pressionar Enter fecha a caixa de diálogo.
   * O foco permanece no controle de assinatura após assinar e clicar em &quot;OK&quot;.

  **Limpar funcionalidade de assinatura:**

   * Um ícone de cruz claro para apagar a assinatura é acessível através da tecla Tab.
   * A caixa de diálogo &quot;Limpar confirmação de assinatura&quot; também pode ser acessada por meio da navegação de guias.

  **Rótulos e controles aprimorados:**
   * O rótulo do botão de assinatura do teclado agora está mais claro, usando &quot;aria-label&quot; para anunciar a funcionalidade (como &quot;aria-label=&#39;Sign using Keyboard&#39;&quot;).
   * O contraste aprimorado garante que todos os controles dentro da assinatura de rabisco sejam facilmente distinguíveis.
   * O botão OK/marca de seleção agora indica visualmente quando está inativo.

  **Feedback de assinatura para Reader de tela:**
   * Quando uma assinatura é digitada, os usuários de leitores de tela podem ouvir o texto usado para criar a assinatura.

Essa atualização garante uma experiência mais inclusiva para usuários portadores de deficiências, melhorando a navegação, a clareza e o feedback do componente Assinatura Escrita.

### Programa de adoção antecipada {#forms-early-adopter}

* **[Enviar um formulário adaptável para o cenário do Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: o Forms as a Cloud Service oferece uma opção pronta para uso para conectar facilmente um Formulário adaptável ao Adobe Workfront. Isso simplifica o processo de envio de um Formulário adaptável para um cenário do Adobe Workfront, permitindo acionar um cenário do Workfront Fusion no envio de um Formulário adaptável.

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> Usando o Adobe Workfront Fusion Connector, você pode projetar fluxos de trabalho que são acionados automaticamente no envio de um Formulário adaptável. Por exemplo, preveja um cenário em que um fluxo de trabalho é iniciado para atribuir a um indivíduo específico a tarefa de revisar dados enviados, permitindo a aprovação ou a rejeição de um aplicativo com base nas informações capturadas por meio do formulário adaptável. Essa integração simplificada aumenta a eficiência e traz um novo nível de automação para seus processos de workflow.|

* **Serviço de extensão Reader**: as APIs de comunicação da AEM Forms trouxeram o Serviço de extensão do Reader para permitir que você adicione funcionalidades como preenchimento de formulário e comentários a PDF regulares, tornando-os interativos para usuários com o Adobe Reader gratuito.

* [Suporte de idiomas da direita para a esquerda](/help/forms/supporting-new-language-localization-core-components.md): o Forms adaptável incorporado aos Componentes principais agora pode ser apresentado em um idioma da direita para a esquerda (RTL), como árabe, persa e urdu. As línguas RTL são faladas por mais de 2 bilhões de pessoas em todo o mundo. Usar um formulário em linguagem RTL permite estender o alcance dos formulários adaptáveis para atender a esses públicos diferentes e selecionar mercados de RTL. Em algumas regiões, também é um mandato legal fornecer formulários no idioma local. Ao acomodar idiomas locais, você não só abre portas para um público mais amplo, como também garante a conformidade com as leis e regulamentos relevantes.

* **[Protect seus documentos com as APIs DocAssurance (Parte das APIs de comunicação)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: As APIs do DocAssurance permitem proteger informações confidenciais, assinando e criptografando os documentos. Por meio da criptografia, o conteúdo de um documento é transformado em um formato ilegível, garantindo que somente usuários autorizados possam ter acesso. Essa camada fortificada de proteção não apenas protege dados valiosos de olhos não autorizados, mas também proporciona tranquilidade. As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos.

  Você pode escrever para `aem-forms-ea@adobe.com` do seu id de email oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso.

* **[Você pode aproveitar o Serviço de dados de monitoramento de usuário real (RUM)](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** para ativar a coleta no lado do cliente para o AEM as a Cloud Service.
O Serviço de dados de monitoramento de usuário real (RUM) oferece um reflexo mais preciso das interações do usuário, garantindo uma medida confiável do engajamento do site. É uma ótima oportunidade para obter insights avançados sobre o desempenho da página. Embora isso seja benéfico para clientes que usam CDN gerenciada por Adobe ou CDN não gerenciada por Adobe. Além disso, para clientes que usam um CDN não gerenciado por Adobe, o relatório de tráfego automatizado agora pode ser ativado para eles, eliminando a necessidade de compartilhar qualquer relatório de tráfego com o Adobe.

  Se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie um email para `aemcs-rum-adopter@adobe.com`, juntamente com o nome de domínio para cada um dos ambientes para os quais você deseja habilitar o RUM, a partir do seu endereço de email associado à sua Adobe ID. A equipe de produtos do Adobe habilitará o Serviço de dados de monitoramento de usuário real (RUM) para você.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Programas de adoção antecipada {#foundation-early-adopter}

#### Alertas de regras de filtro de tráfego (Programa de adoção antecipada) {#traffic-filter-rules-alerts-early-adopter}

O recém-lançado [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md), que incluem as regras opcionalmente licenciáveis do Web Application Firewall (WAF), permite configurar o tráfego que deve ser permitido ou negado.

Agora você pode enviar um email **<aemcs-cdn-config-adopter@adobe.com>** para participar do programa de adoção antecipada para que você possa ser alertado sempre que as regras de filtro de tráfego forem acionadas. As notificações por email do Centro de ações manterão você informado quando ocorrerem determinadas condições de tráfego para que você possa tomar as medidas apropriadas.

#### Configuração da CDN (Early Adoter Program) {#cdn-config-early-adopter}

Além do recém-lançado [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md), que incluem as regras de Firewall de Aplicativo Web (WAF) opcionalmente licenciáveis, há uma oportunidade de usar o Pipeline de configuração para declarar e implantar outros tipos de configuração de CDN. [Saiba mais](/help/implementing/dispatcher/cdn-configuring-traffic.md) e se juntar ao programa de adoção antecipada enviando e-mail **<aemcs-cdn-config-adopter@adobe.com>** para obter acesso a:

* Redirecionamentos do lado do cliente 301/302
* solicitações de proxy na borda para origens arbitrárias (como aplicativos não-AEM)
* Transformações de URL
* definindo ou modificando cabeçalhos de solicitação ou resposta
* páginas de erro personalizadas quando o CDN não consegue acessar o AEM

#### Assimilação de tempo de execução de mapas de regravação do Apache/Dispatcher (Programa de adoção antecipada) {#apache-rewritemaps-early-adopter}

Semelhante ao AEM 6.5, o Apache/Dispatcher assimilará mapas de regravação colocados em um local específico no repositório de publicação e os carregará, sem exigir uma execução de pipeline no nível da Web. Isso abre oportunidades para que um usuário empresarial declare redirecionamentos usando uma interface do usuário, como a oferecida pelo ACS Commons Redirect Map Manager. Entre em contato com **<aemcs-cdn-config-adopter@adobe.com>** para obter mais informações.

#### Edge Side Includes (ESI) para o carregamento de conteúdo dinâmico (Early Adoter Program) {#esi-early-adopter}

O CDN gerenciado por Adobe agora é compatível com ESI (Edge Side Includes), uma linguagem de marcação para a montagem de conteúdo dinâmico da Web no nível da borda. Ao incluir trechos ESI, você pode armazenar em cache a página de HTML geral na CDN com TTLs mais altos, enquanto busca com mais frequência a partir da origem as seções menores que exigem atualizações de cadência mais altas (TTLs mais baixos). Entre em contato com **<aemcs-cdn-config-adopter@adobe.com>** para obter mais informações.

#### Suporte RDE para código de front-end usando temas de site e modelos de site (programa de adoção antecipada) {#rde-frontend-early-adopter}

[RDEs (Rapid Development Environments, ambientes de desenvolvimento rápido)](/help/implementing/developing/introduction/rapid-development-environments.md) O agora oferece suporte ao código de front-end com base no [temas de site](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelos de site](/help/sites-cloud/administering/site-creation/site-templates.md), para os participantes iniciais. Com RDEs, isso é feito usando uma diretiva de linha de comando, em vez de uma [pipeline de front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Entre em contato com **<aemcs-rde-support@adobe.com>** para experimentar e fornecer feedback.

#### Melhoria no registro para RDEs (Early Adoter Program, programa de adoção antecipada) {#rde-logging-early-adopter}

Ao depurar o código em um [RDE (Rapid Development Environment, ambiente de desenvolvimento rápido)](/help/implementing/developing/introduction/rapid-development-environments.md), os desenvolvedores agora podem configurar e transmitir logs com mais eficiência, usando a linha de comando e sem modificar as propriedades OSGI no controle de versão. Os recursos incluem:

* declarar níveis de log em um nível por pacote ou classe
* personalizar o formato de saída do registro
* transmitir vários logs em paralelo

Entre em contato com **<aemcs-rde-support@adobe.com>** para experimentar e fornecer feedback.

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
