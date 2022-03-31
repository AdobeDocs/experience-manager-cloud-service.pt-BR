---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 372e40eb90d87d9ed366e08a3c0117068542680b
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 34%

---


# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a versão atual (2022.3.0) é 31 de março de 2022.
A seguinte versão (2022.4.0) é em 28 de abril de 2022.

## Vídeo da versão {#release-video}

Dê uma olhada no [Visão geral da versão de março de 2022](https://video.tv.adobe.com/v/341465) vídeo para obter um resumo dos recursos adicionados na versão 2022.3.0.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Agora, o [!DNL AEM Dynamic Media] oferece a flexibilidade para [configurar um alias de conta](/help/assets/dynamic-media/dm-alias-account.md) na interface do usuário, garantindo assim a atualização imediata dos URLs do Dynamic Media e do código de inserção do visualizador. Isso afeta positivamente o SEO, para que reflita as atualizações feitas no contexto comercial, como o processo de rebranding.

* Agora você pode usar a interface de usuário do [!DNL Experience Manager Assets] para:

   * Configure o [detecção de ativos duplicados](/help/assets/manage-digital-assets.md#detect-duplicate-assets) em um repositório.

   * Configurar [adição de marcas d&#39;água digitais](/help/assets/watermark-assets.md) para imagens.

* Os administradores agora podem configurar o serviço de email para downloads grandes. Ele permite que os usuários [ativem notificações por email para downloads grandes](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) na interface do [!DNL Experience Manager Assets]. O usuário recebe uma notificação por email contendo o link de download do arquivo ZIP após concluir o processo de download.

* O recurso [Gerenciar publicação](/help/assets/manage-publication.md) está aprimorado, com uma interface de usuário melhorada. Os usuários podem publicar ou desfazer a publicação de conteúdo de e para o destino selecionado, [adicionar conteúdo](/help/assets/manage-publication.md#add-content) à lista de publicação em todo o repositório DAM, [incluir configurações de pasta](/help/assets/manage-publication.md#include-folder-settings) para publicar o conteúdo das pastas selecionadas e aplicar filtros, e [agendar publicações](/help/assets/manage-publication.md#publish-assets-later) para uma data ou hora posterior.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Assets] {#prerelease-features-assets}

* Você pode [classificar tags](/help/assets/organize-assets.md#use-tags-to-organize-assets) ao criar tags inteligentes e ao aplicar filtros de pesquisa usando o predicado tags .

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**: [APIs de geração de documentos](/help/forms/aem-forms-cloud-service-communications.md) ajuda a combinar, reorganizar e validar documentos do PDF. O serviço permite gerar documentos no modo síncrono. As APIs permitem criar aplicativos que possibilitam a você:

   * Montar documentos PDF.
   * Desmonte documentos do PDF.
   * Converta e valide documentos compatíveis com PDF/A.

* **Converter automaticamente PDF forms maiores que 15 páginas em formulários adaptáveis**: Agora é possível usar o serviço automated forms conversion para converter PDF forms com até 40 páginas em formulários adaptáveis. O serviço agora oferece a opção de converter seções de formulários com mais de 15 páginas em fragmentos de formulário adaptáveis. Ajuda a melhorar a velocidade de renderização de formulários convertidos e facilita o carregamento de formulários grandes no editor de formulários adaptável.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **Use o XCI personalizado para gerar um Documento de Registro**: Agora você pode usar um arquivo XCI personalizado para definir várias propriedades de um Documento de registro. Substitui o XCI principal pelas alterações personalizadas.

* **Usar CAPTCHA invisível em um formulário adaptável**: Você pode usar o CAPTCHA invisível para mostrar o desafio CAPTCHA somente no caso de uma atividade suspeita. Se não for encontrada qualquer atividade suspeita, o desafio CAPTCHA não é apresentado.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* Beta: Suporte ao AEM CIF Search Core Component Commerce LiveSearch
* SEO aprimorado para cenários de várias lojas: Os formatos de URL para PDP/PLP agora podem ser configurados em um nível de loja por meio das propriedades da Configuração da nuvem da CIF
* O seletor de produto oferece suporte a produtos preparados por meio da nova opção de filtro na interface do usuário.  Isso permite que os profissionais de conteúdo preparem o gerenciamento de conteúdo de produtos para lançamentos de produtos futuros
* Gerenciamento simplificado de configurações e tratamento de erros da CIF usando o nome da Configuração da nuvem da CIF em vez do url de proxy de configuração
* Seleção manual da categoria para a lista de produtos e os componentes do carrossel. Isso permite que os profissionais de conteúdo usem esses componentes em páginas de conteúdo, fora da experiência de catálogo

## [!DNL Experience Manager] como [!DNL Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* Para obter uma solução de problemas mais eficiente e eficaz de recursos personalizados em ambientes Cloud, lançamos uma nova ferramenta de desenvolvedor - [o navegador do repositório](/help/implementing/developing/tools/repository-browser.md). É um navegador de HTML leve, somente leitura, que pode ser inicializado no Console do desenvolvedor. Obtenha visibilidade sobre o repositório de conteúdo nos níveis de editor, autor e visualização e em todos os ambientes, incluindo produção, estágio e desenvolvimento. Navegue pela estrutura do conteúdo, visualize as propriedades e visualize e baixe binários.

   ![repobrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* As credenciais usadas para autenticar chamadas de API de servidor para servidor (por exemplo, para solicitações de API GraphQL) agora podem ser atualizadas antes da expiração em uma maneira de autoatendimento a partir do Console do desenvolvedor. Consulte a [documentação](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) para obter mais informações.

* As tarefas de manutenção de limpeza de versão e limpeza de log de auditoria, que não tinham sido anteriormente habilitadas, serão habilitadas para novos ambientes. Consulte os valores associados na [Tarefa de manutenção](/help/operations/maintenance.md) artigo 10. o

* AEM Ferramentas as a Cloud Service do Dispatcher SDK agora oferecem suporte a computadores Mac com o chip M1

## Cloud Manager {#cloud-manager}

### Data de lançamento de fevereiro {#release-date-cm-feb}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2022.02.0 é 10 de fevereiro de 2022. A próxima versão está prevista para 10 de março de 2022.

### Novidades {#what-is-new-cm-feb}

* Novo acelerado [pipelines de configuração da camada da Web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) foram introduzidos para implantar exclusivamente a configuração HTTPD/dispatcher.
   * Você deve estar AEM versão `2021.12.6151.20211217T120950Z` ou mais recentes e [aceitar o modo flexível das ferramentas do dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para usar esse recurso.
   * Esse recurso será implementado em uma abordagem em fases durante as duas semanas seguintes à versão 2022.02.0.
* A experiência de página de aterrissagem do Cloud Manager foi atualizada para oferecer navegação aprimorada, fácil alternância entre exibições de grade/bloco e pop-ups para resumo rápido do programa.
* Um novo limite de falha (`< D`) foi adicionado ao [métrica de classificação de confiabilidade.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * Os clientes com problemas graves de qualidade que afetam a estabilidade do sistema, relacionados principalmente a índices inválidos e processos de fluxo de trabalho, não poderão implantar até que esses problemas sejam resolvidos.
* A gravidade da `BannedPath` [regra de qualidade](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) O foi alterado de bloqueador para crítico.
* O assistente de pipeline informará o usuário quando uma atualização de ambiente de AEM pode ser necessária antes de configurar um [pipelines de configuração da camada da Web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) associado a ela.

### Correções de erros {#bug-fixes-cm-feb}

* As senhas antigas do repositório Git agora são sempre invalidadas quando uma nova senha é gerada.
* A atualização de variáveis de ambiente por meio da API não interfere mais na execução de um pipeline em raras situações.

### Data de lançamento de março {#release-date-cm-march}

A data de lançamento do Cloud Manager versão 2022.3.0 em AEM as a Cloud Service 10 de março de 2022. A próxima versão está planejada para 7 de abril de 2022.

### Novidades {#what-is-new-cm-march}

* O acesso ao log de Ambiente de AEM pode ser feito usando a função Desenvolvedor .

### Correções de erros {#bug-fixes-cm-march}

* Um subconjunto de repositórios git criados manualmente tinha um valor de nome incorreto que impedia a efetivação do recurso de reuso de artefato de compilação. Os nomes desses repositórios foram alterados e os usuários verão o nome corrigido na API/interface do usuário do Cloud Manager.
* Os artefatos de construção provenientes de gasodutos que não são de produção foram reutilizados de forma imprópria em gasodutos de produção em pilha completa.
* Ao adicionar ou editar um pipeline de qualidade de código, as opções para lidar com falhas de métrica não são mais exibidas.
* Algumas configurações inesperadas de variável de pipeline podem causar na etapa de build.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta Transferência de conteúdo v1.9.0 é 28 de fevereiro de 2022.

### Novidades {#what-is-new-ctt}

* Verificar medidas de proteção - O recurso Tamanho da verificação da ferramenta Transferência de conteúdo ajuda a reduzir transferências de conteúdo com falha.  Com o recurso Verificar tamanho, os usuários podem 1) determinar se têm espaço em disco suficiente no `crx-quickstart` subdiretório antes da extração e 2) estime o tamanho do conjunto de migração e verifique se ele é compatível. Se uma ou ambas as verificações forem violadas, os usuários verão avisos na interface do usuário da CTT. Com essa garantia, você pode evitar falhas de transferência de conteúdo e discutir proativamente as opções de migração com o Atendimento ao cliente do Adobe. Consulte [Determinando o tamanho e o espaço em disco do conjunto de migração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) para obter mais detalhes.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.26 é 16 de março de 2022.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar ativos não processados. Se ativos não processados forem detectados, precisarão ser definidos como processados ou removidos do conjunto de migração durante a transferência de conteúdo para evitar problemas durante a assimilação de conteúdo.
* Capacidade de detectar se o conteúdo tem mais de 1.000 URLs personalizados. Usar um alto número de URLs personalizados não é uma prática recomendada, pois coloca uma carga nos servidores do Dispatcher e do Publish.
* Capacidade de identificar problemas relacionados às definições de índice do Oak e de detectar incompatibilidades com o AEM as a Cloud Service.
* Capacidade de detectar e relatar o uso de configurações do Externalizador. No AEM as a Cloud Service, as configurações do Externalizador são definidas pelo Cloud Manager, portanto, as configurações existentes precisam ser alteradas para manter a compatibilidade.

### Correções de erros {#bug-fixes-bpa}

* Em alguns cenários, o BPA falhou ao ser executado por causa do FormsSelectiveFeaturesAnalysis, que gerou um erro de assertiva. Isso foi corrigido.
* O BPA relatava conclusões relacionadas ao padrão WRK como GRAVE em vez de CRÍTICA. Isso foi corrigido.
* O BPA relatava incorretamente as conclusões relacionadas às definições de índice do OAK em ui.apps como CRÍTICA. Isso foi corrigido
