---
title: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
translation-type: tm+mt
source-git-commit: bd0efdcea679fa8dc312b17309a5ef0a3c27efc9
workflow-type: tm+mt
source-wordcount: '1748'
ht-degree: 3%

---


# Notas de versão atuais para [!DNL Adobe Experience Manager] como Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais para a versão atual (mais recente) de [!DNL Experience Manager] como um Cloud Service.

>[!NOTE]
>Desse ponto, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aqueles em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obter detalhes das atualizações de documentação não diretamente relacionadas a uma versão.

## Data de lançamento {#release-date}

A Data de lançamento de [!DNL Adobe Experience Manager] como Cloud Service 2021.2.0 é 25 de fevereiro de 2021.
A seguinte versão (2021.3.0) será lançada em 25 de março de 2021.

## [!DNL Adobe Experience Manager Sites] como um Cloud Service  {#sites}

* **[O componente](/help/implementing/developing/hybrid/remote-page.md)** RemotePage: Adição de suporte para visualizar e editar SPA externos no AEM usando o .

* **[Edição de um SPA externo no AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: Adição da capacidade de carregar um aplicativo de página única independente em uma instância do AEM, adicionar seções editáveis de conteúdo e ativar a criação.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## Novidades em [!DNL Assets] {#what-is-new-assets}

* [!DNL Experience Manager Assets] as a  [!DNL Cloud Service] tem direito a ter uma  [!DNL Brand Portal] instância pré-configurada. O usuário [!DNL Cloud Manager] pode ativar [!DNL Brand Portal] em [!DNL Experience Manager Assets] como um [!DNL Cloud Service]. Consulte [ativar Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=en).

* Agora, as empresas podem criar ativos usando [!DNL Brand Portal]. O recurso de fornecimento de ativos aproveita [!DNL Brand Portal] para ajudar os clientes a se envolverem com usuários de agências a obter ativos para novas campanhas de marketing, fotografias e projetos. Consulte [origem do ativo em [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html).

* O relatório de uso [!DNL Brand Portal] agora exibe somente os usuários ativos. Os usuários inativos não são exibidos agora. Os usuários ativos são aqueles cuja conta está atribuída a um perfil de produto no [!DNL Admin Console]. Consulte [[!DNL Brand Portal] relatórios](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* Em [!DNL Brand Portal], uma nova configuração de download é introduzida, permitindo que você crie uma pasta separada para cada ativo ao baixar pastas, coleção e assim por diante. Consulte [configurações de download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  -->

## Correções de erros em [!DNL Assets] {#bug-fixes-assets}

* Quando uma nova versão de um ativo existente é criada após resolver o conflito de nomes, os metadados do ativo original são substituídos. (CQ-4313594)
* Quando um ativo com texto de anotação longo é impresso, o texto da anotação é cortado, mesmo se espaço estiver disponível. (CQ-4314101)
* Quando vários ativos são selecionados para atualizar as propriedades, às vezes ocorre um erro ou as propriedades de um ativo desmarcado são atualizadas. (CQ-4316532)
* Ao tentar abrir [!UICONTROL Painel de pesquisa do administrador de ativos], a página permanece em branco e clicar em [!UICONTROL Editar] > [!UICONTROL Configurações] gera um erro. (CQ-4315079)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Gerenciamento de experiência do produto: Enriqueça as páginas do catálogo de produtos individualmente com Fragmentos de experiência.

* Propriedades do console do produto estendido para mostrar Ativos vinculados e Fragmentos de experiência, incluindo ações para navegar rapidamente para o conteúdo associado.

* Lançamento do site de referência CIF Venia - 2021.02.24, que inclui a versão mais recente dos Componentes principais CIF v1.8.0. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) para obter mais detalhes.

* Lançamento de componentes principais CIF v1.8.0. Consulte [Componentes principais CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) para obter mais detalhes.

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.3.0.

## Data de lançamento {#release-date-cm-march}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.3.0 é 11 de março de 2021.
A próxima versão está planejada para 8 de abril de 2021.


### Novidades {#what-is-new-march}

* Os clientes com ambientes com configurações pré-existentes de Nome de domínio personalizado para [Lista de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn), [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn) e [Nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) verão uma mensagem sobre suas configurações existentes anteriormente e poderão se autoservir por meio da interface do usuário.

* Os usuários com as permissões necessárias agora podem editar um Programa, permitindo que façam o seguinte de maneira automatizada:

   * Adicionar a solução Sites a um programa existente com Ativos ou vice-versa.
   * Remova Sites ou Ativos de um programa existente com Sites e Ativos.
   * Adicione o segundo direito de solução não utilizado a um programa existente ou como um novo Programa.

* **AEM o** recurso Push Updatelabel será exibido para  *Pipeline* Execution e  ** Ativityscreens.

* Se um ambiente estiver hibernado, mas também houver uma atualização de AEM disponível, o status **Hibernado** terá prioridade sobre **Atualização disponível**.

* Agora os usuários podem ver suas funções do Cloud Manager selecionando a opção &quot;Exibir função(ões) do Cloud Manager&quot; após navegar até o ícone Perfil do usuário (canto superior direito) do Unified Shell.

* O rótulo **Application for Approval** foi renomeado para **Production Approval** para maior clareza.

* O rótulo **Version** foi renomeado para **Git Tag** na tela de execução do pipeline de Produção.

* Os rótulos que definem o comportamento quando métricas importantes não atingirem o limite definido foram renomeados para refletir seu comportamento verdadeiro: **Cancelar Imediatamente** e **Aprovar Imediatamente**.

* As listas de desaprovação de classe e método foram atualizadas com base na versão `2021.3.4997.20210303T022849Z-210225` do SDK do Cloud Service AEM.

* O pipeline de Produção do Cloud Manager agora incluirá o recurso [Teste de interface personalizada](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing).

### Correções de erros {#bug-fixes-cm-march}

* O controle de versão do pacote foi ignorado em alguns casos durante AEM atualização por push.

* Alguns problemas de qualidade não foram detectados corretamente quando os pacotes eram incorporados em outros pacotes.

* Em situações obscuras, o nome de programa padrão gerado ao abrir a caixa de diálogo Adicionar programa pode ser uma duplicata de um nome de programa existente.

* Ocasionalmente, se o usuário sair da página de execução do pipeline imediatamente após iniciar um pipeline, uma mensagem de erro será exibida informando que a ação falhou, embora a execução realmente comece.

* A etapa de build foi reiniciada desnecessariamente quando as builds do cliente resultaram em pacotes inválidos.

* Ocasionalmente, o usuário pode ver um status verde &quot;ativo&quot; ao lado de uma  de IP Lista de permissões mesmo quando essa configuração não foi implantada.

* Todos os pipelines de produção existentes serão ativados automaticamente com a etapa Auditoria de experiência.


### Data de lançamento {#release-date-cm}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.2.0 é 11 de fevereiro de 2021.

### Novidades {#what-is-new-cloud-manager}


* Os clientes do Assets agora poderão escolher quando e onde implantar sua instância do Brand Portal de forma automatizada por meio da interface do usuário do Cloud Manager. Para um programa regular (não sandbox) com a solução Assets, o Brand Portal agora pode ser provisionado no ambiente de produção. O provisionamento pode ser feito apenas uma vez no ambiente de Produção.

* O Arquétipo de projeto AEM usado na Criação de projeto e sandbox foi atualizado para a versão 25.

* A lista de APIs obsoletas identificadas durante a verificação de código foi refinada para incluir classes e métodos adicionais obsoletos nas versões mais recentes do SDK do Cloud Service.

* O perfil do SonarQube para o Cloud Manager foi atualizado para remover a regra do Sonar squid:S2142. Isso não entrará mais em conflito com as verificações de Interrupção de encadeamento.

* A interface do usuário do Cloud Manager informará o usuário que pode não ser temporariamente capaz de adicionar/atualizar o nome de domínio porque o ambiente associado tem um pipeline em execução anexado a ele ou que está aguardando a etapa de aprovação.

* As propriedades definidas nos arquivos `pom.xml` do cliente prefixados com o sonar agora serão removidas dinamicamente para evitar falhas de verificação de qualidade e criação.

* A interface do usuário do Cloud Manager informará o usuário que pode não ser temporariamente capaz de selecionar um certificado SSL se ele estiver sendo usado por um nome de domínio que está sendo implantado no momento.

* Foram adicionadas Regras de qualidade de código adicionais para cobrir problemas de compatibilidade de Cloud Service.

### Correções de erros {#bug-fixes-cloud-manager}

* A correspondência do certificado SSL com um nome de domínio não diferencia maiúsculas de minúsculas.

* A interface do usuário do Cloud Manager agora informará um usuário se as chaves privadas do certificado não atenderem ao limite de 2048 bits com uma mensagem de erro apropriada.

* A interface do usuário do Cloud Manager informará o usuário que pode não ser temporariamente capaz de selecionar um certificado SSL se ele estiver sendo usado por um nome de domínio que está sendo implantado no momento.

* Em alguns casos, um problema interno pode causar a interrupção da exclusão do ambiente.

* Algumas falhas de pipeline eram relatadas incorretamente como erros de pipeline.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-march}

A Data de lançamento da ferramenta Transferência de conteúdo v1.3.0 é 4 de março de 2021.

### Novidades na ferramenta Transferência de conteúdo {#what-is-new-ctt-march}

* O CTT agora é instalado em `/apps` em vez de `/libs` marcadores do navegador para determinadas páginas, podem não ser mais válidos.
* Quando a CTT estiver instalada, o usuário precisará navegar por um nível adicional para chegar à página Transferência de conteúdo . Consulte [Usar a ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html) para obter mais detalhes.

### Correções de erros {#bug-fixes-ctt-march}

* Ao migrar conteúdo de um caminho específico, a CTT estava extraindo recursos não relacionados. Isso foi corrigido


### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta Transferência de conteúdo v1.2.4 é 10 de fevereiro de 2021.

### Correções de erros {#bug-fixes-ctt}

* Ao mapear vários usuários, as IDs IMS de alguns estavam sendo mapeadas incorretamente. Isso foi corrigido.

### Data de lançamento {#release-date-ctt-feb}

A Data de lançamento da ferramenta Transferência de conteúdo v1.2.2 é 1 de fevereiro de 2021.

### Novidades na ferramenta Transferência de conteúdo {#what-is-new-ctt}

* Novo recurso e interface do usuário adicionados à ferramenta Transferência de conteúdo - Ferramenta de mapeamento de usuário. Esse recurso mapeia automaticamente usuários e grupos existentes para suas IDs de sistema do Adobe Identity Management como parte da atividade de migração de conteúdo.
Consulte [Usar a ferramenta de mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obter mais detalhes.
* A ferramenta Transferência de conteúdo agora migra todos os grupos e usuários referenciados no conjunto de migração, incluindo filhos.
* Os usuários podem selecionar determinados caminhos em `/etc` ao criar conjuntos de migração.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.2 é 18 de fevereiro de 2021.

### Novidades do Analisador de práticas recomendadas {#what-is-new-bpa}

* Capacidade de detectar o uso da implementação do AEM Forms e do AEM Forms e indicar áreas relevantes para a migração para o AEM Forms as a Cloud Service.
* Capacidade de detectar e relatar o uso e a contagem de componentes e modelos personalizados.
* Capacidade de detectar o tipo de armazenamento de nó e armazenamento de dados usado.
* Capacidade de detectar o uso do Dynamic Media.
* Capacidade de detectar a versão do Java usada.

## Ferramentas de refatoração de código {#code-refactoring-tools}

### Novidades nas Ferramentas de refatoração de código {#what-is-new-crt}

* Nova versão do plug-in AIO-CLI lançada. A versão mais recente deste plug-in inclui vários novos recursos e correções de bugs do Repository Modernizer e do Dispatcher Converter.    Consulte [Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para saber mais sobre esse plug-in.

* Novos recursos e melhorias para o Repository Modernizer. Consulte [Recurso GitHub: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para a versão mais recente.
   * Normalize as configurações do OSGi (exceto as configurações do RepoInit) para o formato preferencial .cfg.json.
   * Renomeie as pastas de configuração do OSGi para o formato especificado.
   * Gere o projeto ui.apps.structure.
   * Crie o módulo de análise.

* Novos recursos e melhorias para o Dispatcher Converter. Consulte [Recurso GitHub: Conversor do Dispatcher](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * Criação de arquivos separados para inclusões diferentes em vez de no conteúdo de vinculação.
   * Capacidade de lidar com o caminho da pasta de vhosts e o caminho para arquivos vhost.
   * Geração de arquivos farm com configurações de clientes grandes no intervalo de 600 e mais.

## [!DNL Adobe Experience Manager] como uma Fundação Cloud Service  {#aem-as-a-cloud-service-foundation}

### Problemas conhecidos {#known-issues-foundation}

**Descrição do problema**

Em determinados casos, uma criação de projeto local pode falhar durante a execução do `aemanalyser-maven-plugin` com a seguinte mensagem de erro:

```
[ERROR] repoinit: Parsing error in repoinit from extension : Encountered "" at line 15, column 37.
 
Was expecting one of:
 
     
 
[ERROR] Analyser detected errors on feature
```

**Solução alternativa**

Para contornar esse problema, selecione a versão mais recente do `aemanalyser-maven-plugin` no arquivo pai `pom.xml`:

```xml
<aemanalyser.version>0.9.2</aemanalyser.version>
```

