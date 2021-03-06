---
title: Notas de versão do  [!DNL Adobe Experience Manager] as a Cloud Service 2021.3.0.
description: '"[!DNL Adobe Experience Manager] Notas de versão as a Cloud Service para 2021.3.0."'
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
source-git-commit: 71647239fc5e740faa25524a01a8ef21ed2d7a3b
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 10%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>Desse ponto, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aqueles em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento para [!DNL Adobe Experience Manager] O as a Cloud Service 2021.3.0 é 25 de março de 2021.
A seguinte versão (2021.4.0) será lançada em 29 de abril de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* [Uma versão do Progressive Web App (PWA) de um site](/help/sites-cloud/authoring/features/enable-pwa.md) agora pode ser ativado no nível do projeto por meio de uma configuração simples.
* Extensões do modelo de fragmento de conteúdo - agora é possível definir tipos de dados de texto de várias linhas como listas de vários campos.
* Aprimoramentos de UX do Editor de fragmento de conteúdo - fragmentos filho aninhados agora são exibidos na navegação estrutural e na visualização aprimorada de ações de publicação, salvamento e salvamento

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novidades do [!DNL Assets] {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] estende a funcionalidade Ativos conectados para suportar o uso de [!DNL Dynamic Media] imagens nos componentes principais compatíveis. Consulte [usar o Connected Assets](/help/assets/use-assets-across-connected-assets-instances.md).
* Os administradores do Experience Manager podem agendar assimilações de ativos em massa em uma data ou hora específica. Além disso, os administradores podem agendar ingestões recorrentes com base em data e hora. Consulte [ingestão de ativos em massa](/help/assets/add-assets.md#asset-bulk-ingestor).

### Correções de erros no [!DNL Assets] {#bug-fixes-assets}

* A página de direitos autorais não é exibida ao tentar baixar vários ativos gerenciados por direitos. (CQ-4314403)
* Ao optar por editar um arquivo INDD, a resolução muda inesperadamente. (CQ-4317376)
* Somente a última página do Modelo de InDesign está lá na Representação de PDF. (CQ-4317305)
* O seletor de tags demora para abrir quando o seletor faz parte de um esquema de metadados complexo. (CQ-4316426)
* Ao fazer upload do ativo com o mesmo nome de arquivo de um existente, a caixa de diálogo de conflito de nomes não é exibida para solicitar que o usuário crie uma versão. (CQ-4315424)
* As Propriedades de metadados da pasta podem ser definidas e salvas no menu pop-up da página Propriedades de uma pasta. Embora a seleção seja salva no repositório, ela não é exibida quando as Propriedades de metadados da pasta são abertas novamente. (CQ-4314429)
* Os ativos com nomes de arquivo contendo espaços ou caracteres especiais são carregados por meio do navegador. (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] como [!DNL Cloud Service] {#forms}

A AEM Forms tem ajudado muitas organizações a oferecer excelentes experiências de integração e inscrição ao longo dos anos. Essas experiências têm ajudado organizações a converter leads em vendas, processar dados capturados do cliente, fornecer experiências responsivas com base no perfil do público-alvo e muito mais. Agora, o AEM Forms está disponível como um serviço em nuvem.

Você pode usar [AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) para criar formulários digitais, conecte formulários às fontes de dados existentes, integre formulários ao Adobe Sign para adicionar assinaturas eletrônicas a formulários, gere o Documento de registro (DoR) para arquivar formulários enviados como arquivos PDF. O serviço também pode converter PDF forms existentes em formulários digitais. Além dos recursos padrão do AEM Forms, o serviço oferece vários recursos nativos em nuvem como dimensionamento automático, tempo de inatividade zero para atualizações e ambiente de desenvolvimento nativo em nuvem. Ler [esta postagem de blog](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html) para saber mais sobre os recursos do AEM Forms as a Cloud Service.

Entre em contato com o representante do Adobe para obter uma demonstração ou para se inscrever no serviço.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Suporte para Adobe Commerce 2.4.2

* O componente de detalhes do produto agora pode ser usado e configurado em qualquer página de conteúdo

* Lançamento do site de referência CIF Venia - 2021.03.25, que inclui a versão mais recente dos Componentes principais CIF v1.9.0. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25) para obter mais detalhes.

* Lançamento de componentes principais CIF v1.9.0. Consulte [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0) para obter mais detalhes.


## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.3.0.

## Data de lançamento {#release-date-cm-march}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.3.0 é 11 de março de 2021.
A próxima versão está planejada para 8 de abril de 2021.

### Novidades {#what-is-new-march}

* Clientes com ambientes com configurações pré-existentes de Nome de domínio personalizado para [LISTAS DE PERMISSÕES de IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn), [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) e [Nomes de Domínio Personalizados](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) O verá uma mensagem sobre suas configurações existentes anteriormente e poderá se autoservir por meio da interface do usuário.

* Os usuários com as permissões necessárias agora podem editar um Programa, permitindo que façam o seguinte de maneira automatizada:

   * Adicionar a solução Sites a um programa existente com Ativos ou vice-versa.
   * Remova Sites ou Ativos de um programa existente com Sites e Ativos.
   * Adicione o segundo direito de solução não utilizado a um programa existente ou como um novo Programa.

* **Atualização de push do AEM** o rótulo será exibido para ambos *Execução de pipeline* e *Atividade* telas.

* Se um ambiente estiver hibernado, mas também houver uma atualização de AEM disponível, a variável **Hibernado** o status terá precedência sobre **Atualização disponível**.

* Agora os usuários podem ver suas funções do Cloud Manager selecionando a opção &quot;Exibir função(ões) do Cloud Manager&quot; após navegar até o ícone Perfil do usuário (canto superior direito) do Unified Shell.

* O rótulo **Pedido de aprovação** foi renomeado para **Aprovação de produção** para maior clareza.

* O **Versão** foi renomeado para **Tag Git** na tela Production pipeline execution .

* Os rótulos que definem o comportamento quando métricas importantes não atingirem o limite definido foram renomeados para refletir seu comportamento verdadeiro: **Cancelar imediatamente** e **Aprovar imediatamente**.

* As listas de desaprovação de classe e método foram atualizadas com base na versão `2021.3.4997.20210303T022849Z-210225` do SDK do AEM Cloud Service.

* O pipeline de Produção do Cloud Manager agora incluirá [Teste de interface personalizada](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) capacidade.

### Correções de erros {#bug-fixes-cm-march}

* O controle de versão do pacote foi ignorado em alguns casos durante AEM atualização por push.

* Alguns problemas de qualidade não foram detectados corretamente quando os pacotes eram incorporados em outros pacotes.

* Em situações obscuras, o nome de programa padrão gerado ao abrir a caixa de diálogo Adicionar programa pode ser uma duplicata de um nome de programa existente.

* Ocasionalmente, se o usuário sair da página de execução do pipeline imediatamente após iniciar um pipeline, uma mensagem de erro será exibida informando que a ação falhou, embora a execução realmente comece.

* A etapa de build foi reiniciada desnecessariamente quando as builds do cliente resultaram em pacotes inválidos.

* Ocasionalmente, o usuário pode ver um status verde &quot;ativo&quot; ao lado de uma  de IP Lista de permissões mesmo quando essa configuração não foi implantada.

* Todos os pipelines de produção existentes serão ativados automaticamente com a etapa Auditoria de experiência.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta Transferência de conteúdo v1.3.4 é 19 de março de 2021.

### Correções de erros {#bug-fixes-ctt}

* A CTT ignorava o conteúdo de pastas com o mesmo nome, mas com um hífen no nome. Isso foi corrigido.

### Data de lançamento {#release-date-ctt-march}

A Data de lançamento da ferramenta Transferência de conteúdo v1.3.0 é 4 de março de 2021.

### Novidades da ferramenta Transferência de conteúdo {#what-is-new-ctt-march}

* O CTT agora é instalado em `/apps` em vez de `/libs` Os marcadores de navegador para determinadas páginas podem não ser mais válidos.
* Quando a CTT estiver instalada, o usuário precisará navegar por um nível adicional para chegar à página Transferência de conteúdo . Consulte [Usar a ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html) para obter mais detalhes.

### Correções de erros {#bug-fixes-ctt-march}

* Ao migrar conteúdo de um caminho específico, a CTT estava extraindo recursos não relacionados. Isso foi corrigido

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.8 é 22 de março de 2021.

### Novidades do Analisador de práticas recomendadas {#what-is-new-bpa}

* Capacidade de filtrar as conclusões do ACS Commons do relatório BPA na interface do usuário, bem como do relatório exportado como um arquivo CSV.

## Ferramentas de refatoração de código {#code-refactoring-tools}

### Novidades nas Ferramentas de refatoração de código {#what-is-new-crt}

* Novos recursos e melhorias para o Repository Modernizer. Consulte [Recurso do GitHub: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obter a versão mais recente.
   * Normalize as configurações do OSGi (exceto as configurações do RepoInit) para o formato preferencial .cfg.json.
   * Renomeie as pastas de configuração do OSGi para o formato especificado.
   * Gere o projeto ui.apps.structure.
   * Crie o módulo de análise.

* Novos recursos e melhorias para o Dispatcher Converter. Consulte [Recurso do GitHub: Conversor do Dispatcher](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * Criação de arquivos separados para inclusões diferentes em vez de no conteúdo de vinculação.
   * Capacidade de lidar com o caminho da pasta de vhosts e o caminho para arquivos vhost.
   * Geração de arquivos farm com configurações de clientes grandes no intervalo de 600 e mais.
