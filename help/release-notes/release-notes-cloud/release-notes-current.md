---
title: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: e9fa68869ca92945c44a79b783fbc8a53a875e81
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 3%

---


# Notas de versão atuais para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir daqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aqueles em 2020, 2021 e assim por diante.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obter detalhes das atualizações de documentação não diretamente relacionadas a uma versão.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] como uma [!DNL Cloud Service] versão atual (2021.9.0) é 6 de outubro de 2021.
A seguinte versão (2021.10.0) é em 28 de outubro de 2021.

## Lançamento de vídeo {#release-video}

Assista ao vídeo [Visão geral da versão de setembro de 2021](https://video.tv.adobe.com/v/337381) para obter um resumo dos recursos adicionados.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novo recurso no canal de pré-lançamento [!DNL Sites] {#sites-prerelease-features}

* Os modelos de Fragmento de conteúdo agora são definidos automaticamente no estado somente leitura depois de serem publicados, para evitar a quebra não intencional de consultas de API ativas após a republicação de um modelo editado. Os usuários recebem um aviso ao tentar editar um modelo publicado. A edição é possível após aceitar o aviso.

## [!DNL Experience Manager Assets] como  [!DNL Cloud Service] {#assets}

### Novos recursos em [!DNL Assets] {#assets-features}

* Os usuários agora podem classificar os ativos exibidos nos resultados da pesquisa nas exibições Coluna e Cartão. A classificação funciona nas colunas Nome, Criado, Modificado ou Nenhum.

   ![Classifique os resultados da pesquisa  [!DNL Assets] nas exibições Coluna e Cartão](/help/assets/assets/sort-searched-assets.png)
   *Figura: Classifique os resultados da pesquisa  [!DNL Assets] nas exibições Coluna e Cartão.*

* Para invocar o processamento programaticamente usando microsserviços de ativos, uma nova API é introduzida. Os desenvolvedores agora podem aplicar um perfil de processamento existente no nível de pasta em um ou mais ativos específicos em uma pasta. O perfil de processamento é aplicado com base em atualizações de propriedades de metadados personalizadas. Consulte `AssetProcessor` no [[!DNL Experience Manager] Referência da API](https://www.adobe.io/experience-manager/reference-materials/). Como antes, é possível [usar microsserviços de ativos da interface do usuário](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] como  [!DNL Cloud Service] {#forms}

### Novidades em [!DNL Forms] {#what-is-new-forms-sep-2021}

* **Usar as funções do Adobe Sign em um formulário** adaptável: Os níveis de serviço Adobe Sign for business and enterprise têm a opção de expandir as funções para os recipients do Agreement, além apenas do Signer, para melhor corresponder aos seus requisitos de fluxo de trabalho. Agora você pode [habilitar cada recipient de contrato para configurar sua função em um Formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform), com o Assinante sendo a função padrão.

* **Analytics para Adaptive Forms**: Agora é possível capturar e rastrear o comportamento do usuário final por meio do Adobe Analytics para o Adaptive Forms para coletar insights do usuário final. Ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário final.

* **Conecte facilmente o AEM Forms com o Microsoft Dynamics e o Salesforce**: O serviço fornece configuração de fonte de dados e modelos de dados prontos para uso para o Microsoft Dynamics e Salesforce, tornando  [mais rápido e fácil para os desenvolvedores configurar o Microsoft Dynamics e o Salesforce como fontes de dados para um formulário](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en) adaptável.

* **Assinar um formulário adaptável por meio do DocuSign:** é possível usar o DocuSign para assinar automaticamente um formulário adaptável. O serviço fornece uma ação de envio personalizada para usar o DocuSign com um formulário adaptável. Você pode instalar o pacote disponível na Distribuição do software para importar a ação de envio.

### Recursos beta de [!DNL Forms] {#sep-what-is-new-forms-prerelease}

* **Conector de armazenamento unificado:** use o Conector de armazenamento unificado para externalizar dados em processo em repositórios gerenciados pelo cliente. Por exemplo, você pode
   * Habilite a funcionalidade de salvar e retomar do Forms Portal e armazene rascunhos de formulários adaptáveis em um repositório de dados gerenciado pelo cliente.
   * Armazene dados de fluxos de trabalho em andamento AEM (dados AEM variáveis de fluxo de trabalho) que contêm dados confidenciais pessoais (SPD) em um repositório gerenciado pelo cliente.

* **[!DNL AEM Forms as a Cloud Service - Communications]**:  [A ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=en) APIshelp de comunicação permite combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos no modo síncrono. As APIs permitem criar aplicativos que permitem:
   * Gere documentos preenchendo arquivos de modelo com dados XML.
   * Gere formulários de saída em vários formatos, incluindo fluxos de PDF não interativos.
   * Gere arquivos PDF de impressão a partir de um PDF de formulário XFA e do Formulário Adobe Acrobat.

Você pode gravar em [!DNL formscsbeta@adobe.com] para se inscrever no programa beta.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* A nova guia &quot;conteúdo comercial associado&quot; no editor Sites aumenta a eficiência do autor ao obter rapidamente acesso ao conteúdo relevante AEM produto para o contexto atual

   ![Conteúdo comercial associado](/help/assets/CIF/associated-commerce-content.png)

* Interface do usuário do seletor de produto aprimorada para melhor experiência do usuário, maior eficiência e suporte para catálogos de produtos complexos

   ![Novo seletor de produto](/help/assets/CIF/product-picker.png)

* Respeite a propriedade &quot;include_in_menu&quot; no componente de navegação

### Correções de erros {#bug-fixes-cif}

* A limpeza do cache do menu não está funcionando como esperado

* Erros JS durante AEM etapa de implantação do CS e quando não estiver usando componentes do cliente

* Não é possível criar a configuração da nuvem CIF em pastas que têm um nó sling:configs

## [!DNL Experience Manager Screens] como  [!DNL Cloud Service] {#screens}

### Novidades {#what-is-new-screens}

* As telas as a Cloud Service agora oferecem suporte para o monitoramento básico da reprodução. O reprodutor reportará várias métricas de reprodução a cada ping (o padrão é 30 segundos). Com base nas métricas, ele fornece a capacidade de detectar vários casos de borda (experiência travada, tela em branco, problema de agendamento, etc.). Esse recurso permite que a equipe monitore remotamente se um player estiver reproduzindo conteúdo corretamente, melhora a reatividade em telas em branco ou falha de experiências no campo e diminui o risco de mostrar uma experiência quebrada para o usuário final.
Consulte [Monitoramento básico da reprodução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) para obter mais detalhes.

* O suporte de miniatura para vídeos no agora é compatível com o Screens as a Cloud Service. Um autor de conteúdo pode definir uma miniatura de vídeos para que a imagem possa ser usada como um espaço reservado e testar corretamente a reprodução e o direcionamento do conteúdo, enquanto o vídeo real está sendo finalizado pela equipe apropriada. A imagem também pode ser usada caso a reprodução do vídeo falhe.
Consulte [Suporte de miniaturas para vídeos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) para obter mais detalhes.

### Correções de erros {#bug-fixes-screens}

* O reprodutor não pôde mostrar o conteúdo da página Incorporada e esse problema foi corrigido.

* Após um logon bem-sucedido, a navegação para a página padrão (canais) terminou em uma página de Erro interno do servidor.

* As entradas de tag associadas não foram removidas ao remover listas de reprodução.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novos recursos em [!DNL Experience Manager as a Cloud Service] {#foundation-features}

**Rede avançada**

>[!INFO]
>
>O recurso avançado de rede faz parte da versão 2021.9.0 e será ativado para clientes em meados de outubro.

[!DNL Adobe Experience Manager] o as a  [!DNL Cloud Service] agora oferece vários tipos de recursos avançados de rede, incluindo:

* Saída de porta flexível para retirar tráfego de portas não padrão. Agora é possível sem entrar em contato com o Suporte do Adobe.
* Endereço IP de saída dedicado para retirar o tráfego de AEM as a Cloud Service de um IP exclusivo, agora com suporte para todas as portas.
* VPN para proteger o tráfego entre sua infraestrutura e AEM as a Cloud Service.

Leia a [documentação](/help/security/configuring-advanced-networking.md) para obter mais informações, incluindo como autofornecer provisionamento de rede avançada usando APIs do Cloud Manager.

**Otimizações de índice**

Para melhorar o desempenho de consultas de pesquisa e indexação, o índice de texto completo lucene-2 não é mais incluído pronto para uso em [!DNL Adobe Experience Manager] como um [!DNL Cloud Service] desta versão. Para remover esse índice de texto completo em ambientes de AEM de acordo com AEM clientes, a Adobe Engineering trabalha de forma individual e pró-ativa com os clientes para obter uma remoção suave e sustentável do índice de texto completo do Lucene. Visite o [!DNL Adobe Experience Manager] como [!DNL Cloud Service] [documentação](/help/operations/indexing.md#index-optimizations) para obter mais informações e entre em contato diretamente com nosso suporte se tiver alguma dúvida.

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.9.0 e 2021.8.0.

## Data de lançamento {#release-date-cm-sept}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2021.9.0 é 9 de setembro de 2021.
A próxima versão está planejada para 07 de outubro de 2021.

### Novidades {#what-is-new-cm-sept}

* A versão do AEM Project Archetype usada pelo Cloud Manager foi atualizada para a versão 30.

* Os cartões de programa na página de aterrissagem do Cloud Manager e a experiência associada foram atualizados.

* O Log de Etapa de Qualidade do Código agora inclui informações de log detalhadas no processo de varredura do OakPal.

* As opções de menu da página Atividade agora incluirão uma opção para **Baixar log** para execuções concluídas do Gerador de código. Ao selecionar essa opção, o log da etapa de build será baixado.

* Clicar diretamente no cartão do Programa agora navegará até a página Visão geral do Cloud Manager .

### Correções de erros {#bug-fixes-sept}

* O usuário verá uma mensagem mais compreensível ao tentar adicionar uma nova Lista de permissões IP em um programa que atingiu o número máximo permitido de Listas de permissões IP que podem ser configuradas.

* URL incorreto foi copiado ao selecionar a opção de menu copiar URL na tela Repositórios.

## Cloud Acceleration Manager {#cam}

### Data de lançamento {#release-date-october-cam}

A data de lançamento do Cloud Acceleration Manager é 4 de outubro de 2021.

### Novidades {#what-is-new-cam}

* O Cloud Acceleration Manager agora oferece aos usuários a capacidade de visualizar os relatórios de BPA em uma pré-visualização que pode ser impressa, permitindo que a impressão ou impressão simples sejam feitas no PDF para proporcionar fácil compartilhamento. Consulte as Etapas 6 e 7 em [Uso do cartão de análise de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-latest}

A Data de lançamento da ferramenta Transferência de conteúdo v1.6.0 é 4 de outubro de 2021.

### Novidades {#what-is-new-ctt}

* Mapeamento de usuário aprimorado com uma experiência de usuário simplificada, incluindo os seguintes recursos listados abaixo. Para obter mais detalhes, consulte [Usar a ferramenta de mapeamento de usuário](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool).
   * Testar conexão com a API de gerenciamento de usuários antes de executar o Mapeamento de usuários
   * Ignore erros com cuidado e continue com a atividade de Mapeamento de usuários
   * O Mapeamento de usuário não falha mais se o Token de acesso expirar (após 24 horas). O Mapeamento de Usuário pode ser executado novamente de onde parou pela última vez.

* Para aumentar a robustez da CTT, o conteúdo pode ser assimilado na instância do autor ou na instância de publicação de cada vez.

* Quando as versões são incluídas, o caminho `/var/audit` é incluído automaticamente para migrar eventos de auditoria.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa-latest}

A data de lançamento do Analisador de práticas recomendadas v2.1.18 é 2 de setembro de 2021.

### Novidades {#what-is-new}

* Capacidade de detectar e relatar a contagem total de nós.

* Capacidade de detectar e relatar no tipo e tamanho do armazenamento do nó.

### Correções de erros {#bug-fixes-bpa}

* O BPA detectou falsamente a presença da Commerce Integration Framework.
