---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.3.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2022.3.0.
exl-id: 761f1605-c421-4f3a-8f90-af23f4f047b1
source-git-commit: bd0981b262f645653723f1b35d871808506d47ba
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 87%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2022.3.0 {#release-notes}

A seção a seguir descreve as notas de versão de recurso da versão 2022.3.0 do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2022.3.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é 31 de março de 2022.
A próxima versão (2022.4.0) está planejada para 5 de maio de 2022.

## Vídeo da versão {#release-video}

Assista ao vídeo [Visão geral da versão de março de 2022](https://video.tv.adobe.com/v/341465) que exibe um resumo dos recursos adicionados na versão 2022.3.0.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Sites] {#prerelease-features-sites}

* Os tipos de dados do modelo de conteúdo agora podem ser definidos como traduzíveis usando uma caixa de seleção simples no editor do modelo de conteúdo. Além disso, as regras e configurações de tradução do AEM são atualizadas automaticamente.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Agora, o [!DNL AEM Dynamic Media] oferece a flexibilidade para [configurar um alias de conta](/help/assets/dynamic-media/dm-alias-account.md) na interface do usuário, garantindo assim a atualização imediata dos URLs do Dynamic Media e do código de inserção do visualizador. Isso afeta positivamente o SEO, para que reflita as atualizações feitas no contexto comercial, como o processo de rebranding.

* Agora você pode usar a interface de usuário do [!DNL Experience Manager Assets] para:

   * Configure a [detecção de ativos duplicados](/help/assets/detect-duplicate-assets.md) em um repositório.

   * Configure a [adição de marcas d´água digitais](/help/assets/watermark-assets.md) em imagens.

* Os administradores agora podem configurar o serviço de email para downloads grandes. Ele permite que os usuários [ativem notificações por email para downloads grandes](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) na interface do [!DNL Experience Manager Assets]. O usuário recebe uma notificação por email contendo o link de download do arquivo ZIP após concluir o processo de download.

* O recurso [Gerenciar publicação](/help/assets/manage-publication.md) está aprimorado, com uma interface de usuário melhorada. Os usuários podem publicar ou desfazer a publicação de conteúdo de e para o destino selecionado, [adicionar conteúdo](/help/assets/manage-publication.md#add-content) à lista de publicação em todo o repositório DAM, [incluir configurações de pasta](/help/assets/manage-publication.md#include-folder-settings) para publicar o conteúdo das pastas selecionadas e aplicar filtros, e [agendar publicações](/help/assets/manage-publication.md#publish-assets-later) para uma data ou hora posterior.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Assets] {#prerelease-features-assets}

* Agora você pode [classificar tags](/help/assets/organize-assets.md#use-tags-to-organize-assets) na janela do seletor de tags em ordem crescente ou decrescente com base no nome da tag, data de criação ou data de modificação.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**: [APIs de geração de documentos](/help/forms/aem-forms-cloud-service-communications.md) ajudam a combinar, reorganizar e validar documentos em PDF. O serviço permite gerar documentos em modo síncrono. As APIs permitem criar aplicativos que possibilitam a você:

   * Montar documentos PDF.
   * Desmontar documentos PDF.
   * Converter e validar documentos PDF e de conformidade.

* **Converter automaticamente formulários PDF com mais de 15 páginas em formulários adaptáveis**: agora você pode usar o serviço automatizado de conversão de formulários para converter formulários PDF com até 40 páginas em formulários adaptáveis. O serviço agora oferece a opção de converter seções de formulários com mais de 15 páginas em fragmentos de formulário adaptáveis. Isso melhora a velocidade de renderização de formulários convertidos e facilita o carregamento de formulários grandes no editor de formulários adaptáveis.

### Novos recursos disponíveis no canal de pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **Usar XCI personalizado para gerar um documento de registro**: agora você pode usar um arquivo XCI personalizado para definir várias propriedades de um documento de registro. Ele substitui o XCI principal pelas alterações personalizadas.

* **Usar CAPTCHA invisível em um formulário adaptável**: é possível usar o CAPTCHA invisível para exibir o teste CAPTCHA somente no caso de uma atividade suspeita. Se nenhuma atividade suspeita for encontrada, o teste CAPTCHA não será exibido.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* SEO aprimorado para cenários com várias lojas: os formatos de URL para PDP/PLP agora podem ser configurados no nível da loja por meio das propriedades de configuração da nuvem do CIF
* O seletor de produto oferece suporte a produtos preparados por meio da nova opção de filtro na interface.  Isso permite que os profissionais de conteúdo preparem o gerenciamento de conteúdo do produto para lançamentos de produtos futuros
* Gerenciamento simplificado de configurações e tratamento de erros do CIF usando o nome de configuração da nuvem do CIF em vez da configuração do URL de proxy
* Seleção manual da categoria para a lista de produtos e os componentes do carrossel. Isso permite que os profissionais de conteúdo usem esses componentes em páginas de conteúdo, fora da experiência de catálogo

### Novos recursos disponíveis no canal de pré-lançamento do CIF  {#prerelease-features-cif}

* Suporte do componente principal de pesquisa CIF do AEM para o Commerce LiveSearch

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novidades {#what-is-new-foundation}

* Para uma solução de problemas mais eficiente e eficaz de recursos personalizados em ambientes na nuvem, lançamos uma nova ferramenta de desenvolvedor — [o Navegador do repositório](/help/implementing/developing/tools/repository-browser.md). É um navegador de HTML leve, somente para leitura, que pode ser iniciado no Console do desenvolvedor. Obtenha visibilidade do repositório de conteúdo nos níveis de editor, autor e pré-visualização e de todos os ambientes, incluindo produção, preparo e desenvolvimento. Navegue pela estrutura do conteúdo, visualize as propriedades e pré-visualize e baixe binários.

  ![repobrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* As credenciais usadas para autenticar chamadas de API de servidor para servidor (por exemplo, para solicitações de API do GraphQL) agora podem ser atualizadas antes da expiração por autoatendimento no Console do desenvolvedor. Consulte a [documentação](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) para obter mais informações.

* As tarefas de manutenção com limpeza de versão e limpeza de log de auditoria, que não tinham sido habilitadas anteriormente, agora estão habilitadas para novos ambientes. Consulte os valores associados no artigo [Tarefa de manutenção](/help/operations/maintenance.md).

* As ferramentas do Dispatcher do SDK do AEM as a Cloud Service agora oferecem suporte a computadores Mac com o chip M1

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da Ferramenta de transferência de conteúdo v1.9.0 é 28 de fevereiro de 2022.

### Novidades {#what-is-new-ctt}

* Proteções de verificação de tamanho - O recurso de verificação de tamanho da Ferramenta de transferência de conteúdo ajuda a reduzir as falhas nas transferências de conteúdo. Com o recurso de verificação de tamanho, os usuários podem: 1) determinar se têm espaço em disco suficiente na `crx-quickstart` subdiretório antes da extração e 2) estime o tamanho do conjunto de migração e verifique se ele é compatível. Se uma ou ambas as verificações forem violadas, os usuários verão avisos na interface da ferramenta de transferência de conteúdo (CTT). Com essa proteção, é possível evitar falhas de transferência de conteúdo e discutir proativamente as opções de migração com o Atendimento ao cliente da Adobe. Consulte [Determinação do tamanho do conjunto de migração e do espaço em disco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=pt-BR#migration-set-size) para obter mais detalhes.

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
* O BPA relatava incorretamente as conclusões relacionadas às definições de índice do OAK em ui.apps como CRÍTICA. Isso foi corrigido.
