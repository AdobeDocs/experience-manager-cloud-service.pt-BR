---
title: Notas de versão do [!DNL Adobe Experience Manager]  as a Cloud Service 2021.9.0.
description: Notas de versão do [!DNL Adobe Experience Manager]  as a Cloud Service 2021.9.0.
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 21%

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

A data de lançamento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] a versão atual (2021.9.0) é 6 de outubro de 2021.
A data de lançamento da versão seguinte (2021.10.0) é 4 de novembro de 2021.

## Vídeo da versão {#release-video}

Dê uma olhada no [Visão geral da versão de setembro de 2021](https://video.tv.adobe.com/v/337381) vídeo para obter um resumo dos recursos adicionados.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novo recurso na [!DNL Sites] canal de pré-lançamento {#sites-prerelease-features}

* Os modelos de Fragmento de conteúdo agora são definidos automaticamente no estado somente leitura depois de publicados, para evitar a quebra involuntária de consultas de API ativas após a republicação de um modelo editado. Os usuários recebem um aviso ao tentar editar um modelo publicado. A edição é possível ao aceitar o aviso.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Agora os usuários podem classificar os ativos exibidos nos resultados da pesquisa nas visualizações de Coluna e Cartão. A classificação funciona nas colunas Nome, Criado, Modificado ou Nenhum.

  ![Classificar os resultados da pesquisa em [!DNL Assets] nas Visualizações de coluna e cartão](/help/assets/assets/sort-searched-assets.png)
  *Figura: Classificar os resultados da pesquisa em [!DNL Assets] nas Visualizações de coluna e cartão.*

* Para chamar programaticamente o processamento usando microsserviços de ativos, é introduzida uma nova API. Os desenvolvedores agora podem aplicar um perfil de processamento existente no nível da pasta a um ou mais ativos específicos em uma pasta. O perfil de processamento é aplicado com base em atualizações de propriedades de metadados personalizadas. Consulte `AssetProcessor` no [[!DNL Experience Manager] Referência da API](https://www.adobe.io/experience-manager/reference-materials/). Como antes, é possível [usar microsserviços de ativos na interface](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms-sep-2021}

* **Usar funções do Adobe Sign em um formulário adaptável**: a Adobe Sign para níveis de serviço corporativo e comercial tem a opção de expandir as funções para os recipients do Contrato, além apenas do Signatário, para melhor corresponder aos requisitos de fluxo de trabalho. Agora você pode [habilitar cada destinatário do contrato para configurar sua função em um Formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform), sendo Signatário a função padrão.

* **Analytics para Forms adaptável**: agora você pode capturar e rastrear o comportamento do usuário final por meio do Adobe Analytics para Adaptive Forms para coletar insights do usuário final. Ele ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário final.

* **Conecte facilmente o AEM Forms com o Microsoft Dynamics e o Salesforce**: o serviço fornece configuração de fonte de dados pronta para uso e modelos de dados para o Microsoft Dynamics e Salesforce, tornando-o [para os desenvolvedores, mais rápido e fácil configurar o Microsoft Dynamics e o Salesforce como fontes de dados para um formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en).

* **Assine eletronicamente um formulário adaptável usando o DocuSign:** Você pode usar o DocuSign para assinar eletronicamente um formulário adaptável. O serviço fornece uma ação de envio personalizada para usar o DocuSign com um formulário adaptável. Você pode instalar o pacote disponível na Distribuição de software para importar a ação de envio.

### Recursos beta do [!DNL Forms] {#sep-what-is-new-forms-prerelease}

* **Conector de armazenamento unificado:** Use o Conector de armazenamento unificado para externalizar dados em processamento em repositórios gerenciados pelo cliente. Por exemplo, você pode
   * Habilite a funcionalidade de salvar e retomar do Forms Portal e armazene rascunhos de formulários adaptáveis em um repositório de dados gerenciado pelo cliente.
   * Armazene dados de fluxos de trabalho em andamento do AEM (dados de variáveis do fluxo de trabalho AEM) que contenham Dados pessoais confidenciais (SPD) em um repositório gerenciado pelo cliente.

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) Ajudar a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modo síncrono. As APIs permitem criar aplicativos que possibilitam a você:
   * Gerar documentos preenchendo arquivos de modelo com dados XML.
   * Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
   * Gere arquivos de PDF de impressão a partir de um PDF de formulário XFA e do formulário Adobe Acrobat.

Você pode escrever para [!DNL formscsbeta@adobe.com] para se inscrever no programa beta.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* A nova guia &quot;conteúdo de comércio associado&quot; no editor de sites aumenta a eficiência do autor, obtendo rapidamente acesso ao conteúdo de produto AEM relevante para o contexto atual

  ![Conteúdo de comércio associado](/help/assets/CIF/associated-commerce-content.png)

* Interface aprimorada do seletor de produtos para obter melhor experiência do usuário, maior eficiência e suporte para catálogos de produtos complexos

  ![Novo seletor de produtos](/help/assets/CIF/product-picker.png)

* Respeitar a propriedade &quot;include_in_menu&quot; no componente de navegação

### Correções de erros {#bug-fixes-cif}

* A limpeza do cache de menu não está funcionando como esperado

* Erros JS durante a etapa de implantação do AEM CS e quando não estão usando componentes do lado do cliente

* Não é possível criar a configuração de nuvem da CIF em pastas que têm um nó sling:configs

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### Novidades {#what-is-new-screens}

* O Screens as a Cloud Service agora é compatível com o monitoramento básico da reprodução. O player agora relatará várias métricas de reprodução a cada ping (o padrão é 30 segundos). Com base nas métricas, ele fornece a capacidade de detectar vários casos de borda (experiência travada, tela em branco, problema de agendamento e assim por diante). Esse recurso permite que a equipe monitore remotamente se um player está reproduzindo conteúdo corretamente, melhora a reatividade para telas em branco ou experiências com falha no campo e diminui o risco de mostrar uma experiência com falha para o usuário final.
Consulte [Monitoramento básico de reprodução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) para obter mais detalhes.

* O Suporte a miniaturas para vídeos agora é compatível com o Screens as a Cloud Service. Um autor de conteúdo pode definir uma miniatura de vídeos para que a imagem possa ser usada como um espaço reservado e testar corretamente a reprodução e o direcionamento do conteúdo, enquanto o vídeo real está sendo finalizado pela equipe apropriada. A imagem também pode ser usada caso a reprodução do vídeo falhe.
Consulte [Suporte a miniaturas para vídeos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) para obter mais detalhes.

### Correções de erros {#bug-fixes-screens}

* O player não pôde mostrar o conteúdo da página Incorporada e esse problema foi corrigido.

* Após um logon bem-sucedido, a navegação para a página padrão (canais) acabou em uma página Erro interno do servidor.

* As entradas de tag associadas não foram removidas ao remover listas de reprodução.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novos recursos no [!DNL Experience Manager as a Cloud Service] {#foundation-features}

**Rede avançada**

>[!INFO]
>
>O recurso avançado de rede faz parte da versão 2021.9.0 e será ativado para os clientes em meados de outubro.

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] O agora oferece vários tipos de recursos avançados de rede, incluindo:

* Saída flexível da porta para saída de tráfego de portas não padrão. Agora possível sem entrar em contato com o suporte do Adobe.
* Endereço IP de saída dedicado para tráfego de saída do AEM as a Cloud Service de um IP exclusivo, agora oferecendo suporte a todas as portas.
* VPN para proteger o tráfego entre sua infraestrutura e o AEM as a Cloud Service.

Leia o [documentação](/help/security/configuring-advanced-networking.md) para obter mais informações, incluindo como realizar o autoatendimento do fornecimento de rede avançada usando as APIs do Cloud Manager.

**Otimizações de índice**

Para melhorar o desempenho de consultas de pesquisa e indexação, o índice de texto completo lucene-2 não é mais usado pronto para uso no [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] desta versão. Para remover esse índice de texto completo em ambientes AEM de acordo com os clientes AEM, a Engenharia de Adobe trabalha de forma individual e proativa com os clientes para uma remoção suave e sustentável do índice de texto completo Lucene. Visite o [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [documentação](/help/operations/indexing.md#index-optimizations) para obter mais informações e entrar em contato diretamente com nosso suporte em caso de dúvidas.

## Cloud Manager {#cloud-manager}

Esta seção descreve as notas de versão do Cloud Manager no AEM as a Cloud Service 2021.9.0 e 2021.8.0.

## Data de lançamento {#release-date-cm-sept}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.9.0 é 9 de setembro de 2021.
A próxima versão está planejada para 7 de outubro de 2021.

### Novidades {#what-is-new-cm-sept}

* A versão do Arquétipo de Projetos AEM usada pelo Cloud Manager foi atualizada para a versão 30.

* Os cartões de programa na página de aterrissagem do Cloud Manager e a experiência associada foram atualizados.

* O Log da etapa de qualidade do código agora inclui informações detalhadas sobre o processo de verificação OakPal.

* As opções de menu da página Atividade agora incluem uma opção para **Baixar o log** das execuções concluídas pelo Gerador de código. Ao selecionar essa opção, o log da etapa de compilação será baixado.

* Ao clicar diretamente no cartão Programa, agora você será direcionado para a página Visão geral do Cloud Manager.

### Correções de erros {#bug-fixes-sept}

* O usuário verá uma mensagem mais compreensível ao tentar adicionar uma nova Lista de permissões de IP em um programa que atingiu o número máximo permitido de Listas de permissões de IP que podem ser configuradas.

* A URL incorreta foi copiada ao selecionar a opção de menu Copiar URL na tela Repositórios.

## Cloud Acceleration Manager {#cam}

### Data de lançamento {#release-date-october-cam}

A data de lançamento do Cloud Acceleration Manager é 4 de outubro de 2021.

### Novidades {#what-is-new-cam}

* O Cloud Acceleration Manager agora oferece aos usuários a capacidade de visualizar os relatórios do BPA em uma impressão simples ou impressão em PDF para facilitar o compartilhamento. Consulte as Etapas 6 e 7 em [Usando o cartão de análise de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-latest}

A data de lançamento da ferramenta de Transferência de conteúdo v1.6.0 é 4 de outubro de 2021.

### Novidades {#what-is-new-ctt}

* Mapeamento de usuário aprimorado com uma experiência de usuário simplificada, incluindo os seguintes recursos listados abaixo. Para obter mais detalhes, consulte [Utilização da ferramenta Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=pt-BR#using-user-mapping-tool).
   * Testar conexão com a API de gerenciamento de usuários antes de executar o mapeamento de usuários
   * Ignorar erros normalmente e continuar com a atividade Mapeamento de usuário
   * O mapeamento de usuários não falhará mais se o token de acesso expirar (após 24 horas). O Mapeamento de usuário pode ser executado novamente de onde parou pela última vez.

* Para aumentar a robustez da CTT, o conteúdo pode ser assimilado na instância do Autor ou na instância de Publicação de cada vez.

* Quando as versões são incluídas, o caminho `/var/audit` é incluído automaticamente para migrar eventos de auditoria.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa-latest}

A data de lançamento do Analisador de práticas recomendadas v2.1.18 é 2 de setembro de 2021.

### Novidades {#what-is-new}

* Capacidade de detectar e relatar a contagem total de nós.

* Capacidade de detectar e gerar relatórios sobre o tipo e o tamanho de armazenamento do nó.

### Correções de erros {#bug-fixes-bpa}

* O BPA estava detectando falsamente a presença da Commerce Integration Framework.
