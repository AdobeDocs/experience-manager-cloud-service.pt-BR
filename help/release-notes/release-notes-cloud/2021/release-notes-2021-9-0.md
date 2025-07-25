---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.9.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2021.9.0.
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 16%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais da versão atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Aqui, você pode navegar até as notas de versão das versões anteriores; por exemplo, para aquelas em 2020 e 2021.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2021.9.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é quinta-feira, 6 de outubro de 2021.
A versão seguinte (2021.10.0) será lançada em sexta-feira, 4 de novembro de 2021.

## Vídeo da versão {#release-video}

Assista ao vídeo [Visão geral da versão de setembro de 2021](https://video.tv.adobe.com/v/337381) para ver um resumo dos recursos adicionados.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novo recurso no canal de pré-lançamento do [!DNL Sites] {#sites-prerelease-features}

* Os modelos de Fragmento de conteúdo agora são definidos automaticamente em um estado somente leitura depois de publicados, para evitar a quebra involuntária de consultas de API ativas após a republicação de um modelo editado. Os usuários recebem um aviso ao tentar editar um modelo publicado. A edição é possível ao aceitar o aviso.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos no [!DNL Assets] {#assets-features}

* Agora os usuários podem classificar os ativos exibidos nos resultados da pesquisa nas visualizações de Coluna e Cartão. A classificação funciona nas colunas Nome, Criado, Modificado ou Nenhum.

  ![Classificar os resultados da pesquisa em [!DNL Assets] nos modos de exibição de Coluna e Cartão](/help/assets/assets/sort-searched-assets.png)
  *Figura: Classifique os resultados da pesquisa em [!DNL Assets] nos modos de exibição Coluna e Cartão.*

* Para chamar programaticamente o processamento usando microsserviços de ativos, é introduzida uma nova API. Os desenvolvedores agora podem aplicar um perfil de processamento existente no nível da pasta a um ou mais ativos específicos em uma pasta. O perfil de processamento é aplicado com base em atualizações de propriedades de metadados personalizadas. Consulte `AssetProcessor` na [[!DNL Experience Manager] referência da API](https://developer.adobe.com/experience-manager/reference-materials/). Como antes, é possível [usar microsserviços de ativos da interface do usuário](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature by way of CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novidades do [!DNL Forms] {#what-is-new-forms-sep-2021}

* **Usar funções do Adobe Sign em um Formulário adaptável** - Os níveis de serviço corporativo e empresarial do Adobe Sign permitem que você expanda, opcionalmente, as funções dos destinatários do Contrato, além apenas do Signatário, para melhor atender aos requisitos de fluxo de trabalho. Agora você pode [habilitar cada destinatário do contrato para configurar sua função em um Formulário Adaptável](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html?lang=pt-BR#addsignerstoanadaptiveform), sendo que Signatário é a função padrão.

* **Analytics para Forms adaptável** - Agora é possível capturar e rastrear o comportamento do usuário final por meio do Adobe Analytics para Forms adaptável para coletar insights do usuário final. Ele ajuda a tomar decisões informadas com base em dados para melhorar a experiência do usuário final.

* **Conecte facilmente o Adobe Experience Manager (AEM) Forms com o Microsoft® Dynamics e Salesforce** - O serviço fornece configuração de fonte de dados pronta para uso e modelos de dados para o Microsoft® Dynamics e Salesforce. Isso torna o [mais rápido e fácil para os desenvolvedores configurarem o Microsoft® Dynamics e o Salesforce como fontes de dados para um formulário adaptável](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=pt-BR).

* **Assinar eletronicamente um formulário adaptável usando o DocuSign** - Você pode usar o DocuSign para assinar eletronicamente um formulário adaptável. O serviço fornece uma ação de envio personalizada para usar o DocuSign com um formulário adaptável. Você pode instalar o pacote disponível na Distribuição de software para importar a ação de envio.

### Recursos do Beta de [!DNL Forms] {#sep-what-is-new-forms-prerelease}

* **Conector de armazenamento unificado** - Use o Conector de armazenamento unificado para externalizar dados em processamento para repositórios gerenciados pelo cliente. Por exemplo, você pode
   * Habilite a funcionalidade de salvar e retomar do Forms Portal e armazene rascunhos de formulários adaptáveis em um repositório de dados gerenciado pelo cliente.
   * Armazene dados de fluxos de trabalho em andamento do AEM (dados de variáveis do fluxo de trabalho AEM) que contenham Dados pessoais confidenciais (SPD) em um repositório gerenciado pelo cliente.

* **[!DNL AEM Forms as a Cloud Service - Communications]** - [APIs de comunicação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html?lang=pt-BR) ajudam a combinar modelos XDP e dados XML para gerar documentos de impressão em vários formatos. O serviço permite gerar documentos em modo síncrono. As APIs permitem criar aplicativos que possibilitam a você:
   * Gerar documentos preenchendo arquivos de modelo com dados XML.
   * Gerar formulários de saída em vários formatos, incluindo fluxos de impressão de PDF não interativos.
   * Gere arquivos de PDF de impressão a partir de um PDF de formulário XFA e do formulário Adobe Acrobat.

Você pode enviar um email a [!DNL formscsbeta@adobe.com] para se cadastrar no programa beta.

## Complemento CIF {#cloud-services-cif}

### Novidades {#what-is-new-cif}

* A nova guia &quot;conteúdo comercial associado&quot; no editor do AEM Sites aumenta a eficiência do autor, obtendo rapidamente acesso ao conteúdo relevante do produto AEM para o contexto atual

  ![Conteúdo comercial associado](/help/assets/CIF/associated-commerce-content.png)

* Interface aprimorada do seletor de produtos para obter melhor experiência do usuário, maior eficiência e suporte para catálogos de produtos complexos

  ![Novo Seletor de Produtos](/help/assets/CIF/product-picker.png)

* Respeitar a propriedade &quot;include_in_menu&quot; no componente de navegação

### Correções de erros {#bug-fixes-cif}

* A limpeza do cache de menu não está funcionando como esperado

* Erros JS durante a etapa de implantação do AEM CS e quando não estão usando componentes do lado do cliente

* Não é possível criar a configuração de nuvem do CIF em pastas que têm um nó sling:configs

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### Novidades {#what-is-new-screens}

* O Screens as a Cloud Service agora é compatível com o monitoramento básico de reprodução. O player agora relata várias métricas de reprodução a cada ping (o padrão é 30 segundos). Com base nas métricas, é possível detectar vários casos de borda (experiência travada, tela em branco, problema de agendamento e assim por diante). Esse recurso permite que a equipe monitore remotamente se um player está reproduzindo conteúdo corretamente. Ele melhora a reatividade para telas em branco ou experiências com falha no campo e diminui o risco de mostrar uma experiência com falha para o usuário.
Consulte [Monitoramento básico de reprodução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=pt-BR#playback-monitoring) para obter mais detalhes.

* O Suporte a miniaturas para vídeos agora é compatível com o Screens as a Cloud Service. Um autor de conteúdo pode definir uma miniatura de vídeos para que a imagem seja usada como um espaço reservado e testar corretamente a reprodução e o direcionamento do conteúdo, enquanto o vídeo real está sendo finalizado pela equipe apropriada. A imagem também pode ser usada caso a reprodução do vídeo falhe.
Consulte [Suporte a miniaturas para vídeos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html?lang=pt-BR) para obter mais detalhes.

### Correções de erros {#bug-fixes-screens}

* O reprodutor não pôde mostrar o conteúdo da página Incorporada e esse problema foi corrigido.

* Após um logon bem-sucedido, a navegação para a página padrão (canais) acabou em uma página Erro interno do servidor.

* As entradas de tag associadas não foram removidas durante a remoção de listas de reprodução.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novos recursos no [!DNL Experience Manager as a Cloud Service] {#foundation-features}

**Rede avançada**

>[!INFO]
>
>O recurso avançado de rede faz parte da versão 2021.9.0 e foi ativado para clientes em meados de outubro de 2021.

O [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] agora oferece vários tipos de recursos avançados de rede, incluindo:

* Saída flexível da porta para saída de tráfego de portas não padrão. Agora possível sem entrar em contato com o suporte do Adobe.
* Endereço IP de saída dedicado para tráfego de saída do AEM as a Cloud Service a partir de um IP exclusivo, agora oferecendo suporte a todas as portas.
* VPN para proteger o tráfego entre sua infraestrutura e a AEM as a Cloud Service.

Leia a [documentação](/help/security/configuring-advanced-networking.md) para obter mais informações, incluindo como provisionar o autoatendimento de redes avançadas usando APIs do Cloud Manager.

**Otimizações de índice**

Para melhorar o desempenho de consultas de pesquisa e indexação, o índice de texto completo lucene-2 não é mais usado pronto para uso no [!DNL Adobe Experience Manager] como um [!DNL Cloud Service] desta versão. Para remover esse índice de texto completo em ambientes AEM de acordo com os clientes AEM, a Engenharia de Adobe trabalha de forma individual e proativa com os clientes para uma remoção suave e sustentável do índice de texto completo Lucene. Visite a [!DNL Adobe Experience Manager] como uma [!DNL Cloud Service] [documentação](/help/operations/indexing.md#index-optimizations) para obter mais informações e contate o suporte da Adobe diretamente em caso de dúvidas.

## Cloud Manager {#cloud-manager}

Esta seção descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.9.0 e 2021.8.0.

## Data de lançamento {#release-date-cm-sept}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.9.0 é 9 de setembro de 2021.
A próxima versão está planejada para 7 de outubro de 2021.

### Novidades {#what-is-new-cm-sept}

* A versão do Arquétipo de Projetos AEM usada pelo Cloud Manager foi atualizada para a versão 30.

* Os cartões de programa na página de destino do Cloud Manager e a experiência associada foram atualizados.

* O Log da etapa de qualidade do código agora inclui informações detalhadas sobre o processo de verificação OakPal.

* As opções de menu da página Atividade agora incluem uma opção para **Baixar o log** das execuções concluídas pelo Gerador de código. Selecionar essa opção baixa o log da etapa de criação.

* Ao clicar diretamente no cartão Programa agora, você é direcionado para a página Visão geral da Cloud Manager.

### Correções de erros {#bug-fixes-sept}

* Os usuários agora veem uma mensagem mais compreensível ao tentar adicionar um incluo na lista de permissões IP em um programa que atingiu o número máximo permitido de listas de permissões IP que podem ser configuradas.

* O URL incorreto foi copiado ao selecionar a opção de menu Copiar URL na tela Repositórios.

## Cloud Acceleration Manager {#cam}

### Data de lançamento {#release-date-october-cam}

A data de lançamento do Cloud Acceleration Manager é 4 de outubro de 2021.

### Novidades {#what-is-new-cam}

* O Cloud Acceleration Manager agora oferece aos usuários a capacidade de visualizar os relatórios do BPA em uma visualização imprimível, permitindo uma impressão simples ou impressão em PDF para facilitar o compartilhamento. Consulte as Etapas 6 e 7 em [Usando o Cartão de Análise de Práticas Recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=pt-BR#best-practices-analysis).

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

### Data de lançamento {#release-date-ctt-latest}

A data de lançamento da ferramenta de Transferência de conteúdo v1.6.0 é 4 de outubro de 2021.

### Novidades {#what-is-new-ctt}

* Mapeamento de usuário aprimorado com uma experiência de usuário simplificada, incluindo os seguintes recursos listados abaixo. Para obter mais detalhes, consulte [Usando a Ferramenta de Mapeamento de Usuário](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=pt-BR#using-user-mapping-tool).
   * Testar conexão com a API de gerenciamento de usuários antes de executar o mapeamento de usuários
   * Ignorar erros normalmente e continuar com a atividade Mapeamento de usuário
   * O mapeamento de usuários não falhará mais se o token de acesso expirar (após 24 horas). O Mapeamento de usuário pode ser executado novamente de onde parou pela última vez.

* Para aumentar a robustez da CTT, o conteúdo pode ser assimilado na instância do autor ou na instância do Publish de cada vez.

* Quando as versões são incluídas, o caminho `/var/audit` é incluído automaticamente para migrar eventos de auditoria.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa-latest}

A data de lançamento do Analisador de práticas recomendadas v2.1.18 é 2 de setembro de 2021.

### Novidades {#what-is-new}

* Capacidade de detectar e relatar a contagem total de nós.

* Capacidade de detectar e gerar relatórios sobre o tipo e o tamanho de armazenamento do nó.

### Correções de erros {#bug-fixes-bpa}

* O BPA estava detectando falsamente a presença de Commerce integration framework.
