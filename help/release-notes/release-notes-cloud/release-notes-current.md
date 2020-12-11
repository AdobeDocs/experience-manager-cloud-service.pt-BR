---
title: Notas de versão atuais para [!DNL Adobe Experience Manager] como um Cloud Service.
description: Notas de versão atuais para [!DNL Adobe Experience Manager] como um Cloud Service.
translation-type: tm+mt
source-git-commit: 3aff98256eb26176bca52a49286bf2853290b5ef
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 3%

---


# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] como um Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] como Cloud Service 2020.11.0 é 2 de dezembro de 2020.
A seguinte versão (2020.12.0) será lançada em 17 de dezembro de 2020

## [!DNL Adobe Experience Manager Sites] como um Cloud Service  {#sites}

### Novidades em [!DNL Sites] {#what-is-new-sites}

* **[Inicia o Gerenciamento](/help/sites-cloud/authoring/launches/managing-pages.md)  de Hierarquia e o Timewarp [](/help/sites-cloud/authoring/launches/preview.md)** Futuro: Nova interface do usuário para adicionar/remover páginas em uma inicialização e navegar no site com o Timewarp mostra o estado futuro de Inicializações.

* **[Modelos e editor](/help/assets/content-fragments/content-fragments-models.md)** de fragmento de conteúdo estendido: Novas opções para a validação de entrada em vários tipos de dados, tipo de dados de Lista discriminada aprimorado com novas visualizações de formulário e o nome do modelo do Fragmento de conteúdo é exibido e pesquisável na interface do usuário do Assets.

* **Classifique as páginas da Live Copy disponíveis para implantação**: Nova opção para classificar as páginas da Live Copy disponíveis para implantação usando as propriedades  [!UICONTROL Nome], Data [!UICONTROL  da ]última modificação e  [!UICONTROL Última ] implantação. A [!UICONTROL Data da última implementação] de uma página é uma nova propriedade introduzida.

## [!DNL Adobe Experience Manager Assets] como um Cloud Service  {#assets}

### Novidades em [!DNL Assets] e [!DNL Dynamic Media] {#what-is-new-assets}

* **Inclusão** de ativos em massa: Ofereça aos clientes um serviço de ingestão escalável e nativo de nuvem que aproveita  [!DNL Experience Manager] como uma arquitetura de Cloud Service, incluindo microserviços de ativos. Os principais casos de uso incluem ingestão em escala com monitoramento, relatórios e agendamento, enquanto permitem a transferência inicial de ativos para armazenamentos de dados em nuvem usando ferramentas comuns de upload em nuvem. Consulte [ferramenta de assimilação em massa de ativos](/help/assets/add-assets.md#asset-bulk-ingestor).
Esta ferramenta destina-se a administradores do sistema, consultores ou parceiros de implementação. Este recurso permite a ingestão em grande escala e é usado idealmente durante a ingestão inicial ou a ingestão ocasional em grande escala. Para tarefas de ingestão menores, use o [[!DNL Experience Manager] aplicativo desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) ou [upload usando a interface de usuário do Assets](/help/assets/add-assets.md#upload-assets).

   ![Configuração do importador a granel](/help/assets/assets/bulk-import-config-low-res.png)

* Os usuários agora podem classificar os ativos digitais em visualizações de cartão e coluna.

   ![classificar ativos](/help/assets/assets/asset-sort-options.png)

* Os seguintes aprimoramentos são feitos para acessibilidade em [!DNL Experience Manager Assets] nesta versão. Para obter mais informações, consulte [recursos de acessibilidade em [!DNL Assets]](/help/assets/accessibility.md).

   * Ao navegar pela linha do tempo usando um teclado, a tecla Esc pode recolher a opção Mostrar tudo sem perder o foco.
   * Ao navegar usando a tecla de guia do teclado, depois de remover a última tag das tags adicionadas, o campo da tag mantém o foco.
   * [!DNL Experience Manager] os componentes agora contêm informações apropriadas para nome, função e valor a serem usados pelos leitores de tela.
   * Depois que você exclui a caixa de combinação Tipo/Tamanho, a caixa de combinação Link, a caixa de combinação Idioma ou a caixa de edição de texto, o foco do teclado retorna para os elementos da interface do usuário anterior ou seguinte ou para um elemento da interface do usuário mais relevante.
   * Ao passar o ponteiro do mouse sobre as opções, dicas como Selecionar e Download são exibidas. Os usuários que usam uma lente de aumento de tela podem não ver as miniaturas do arquivo devido a essas dicas. Agora, é possível preservar o foco, depois de remover a opção usando a tecla `Escape`.
   * Ao selecionar uma célula de grade da grade presente na página, o foco muda para a barra de ação que aparece na tela.
   * Os usuários visuais podem diferenciar entre um texto normal e um link, à medida que pistas visuais (ícone sublinhado e divisa) são exibidas para links para todas as soluções no home page [!DNL Experience Manager].

* **Predefinições de conjunto de lotes no Dynamic Media**: Agora você pode automatizar a criação e a organização de vários ativos em um conjunto de imagens ou conjunto giratório no momento em que carrega os arquivos de ativos para uma pasta individualmente ou usando a ingestão em massa.

   Consulte [Sobre predefinições de conjuntos de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).

* Os seguintes aprimoramentos de acessibilidade estão disponíveis em [!DNL Dynamic Media]:

   * Os leitores de tela (JAWS, Narrador) registram o nome, a função e o estado dos itens de menu na opção de menu Incorporar tamanho.
   * Os usuários podem navegar na caixa de diálogo Link de email usando a tecla `Tab`.
   * O fluxo de trabalho para criar perfis de codificação de vídeo é mais fácil de usar, dada a melhoria do leitor de tela.
   * Ao navegar usando a tecla `Tab`, o foco se move para os elementos apropriados da interface do usuário no fluxo de trabalho para criar um vídeo interativo.
   * A página Publicar, a página Editar ativo, a página Editar recortes inteligentes e a página Editor de conjuntos de imagens são aprimoradas para atender aos padrões da Web. Os usuários da tecnologia assistiva (AT) agora podem navegar por essas páginas facilmente e realizar ações como cortar imagens.
   * Os visualizadores são aprimorados para permitir que os usuários naveguem usando um teclado.
   * Os usuários do teclado e do leitor de tela podem usar a funcionalidade de recorte.
   * Os usuários de teclado podem gerenciar melhor os pontos de conexão.

   Consulte [Acessibilidade em [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.11.05 que inclui a versão mais recente dos componentes principais CIF v1.5.0. Consulte [CIF Site de Referência de Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) para obter mais detalhes.

* Componentes principais CIF lançados v1.5.0. Consulte [CIF Componentes principais](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) para obter mais detalhes.

### Correções de erros {#bug-fixes-commerce}

* A configuração do cliente GraphQL não era lida corretamente quando a configuração não era especificada diretamente na configuração da CA Sling, mas em uma das configurações principais. Isso foi corrigido.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2020.12.0 é 10 de dezembro de 2020.

### Novidades em [!DNL Cloud Manager] {#what-is-new-cm}

* Gerenciamento de autoatendimento de [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) e [Nomes de Domínio Personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Gerenciamento de autoatendimento de [Listas de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* A página de detalhes atualizada **Ambiente** permite que os usuários gerenciem Nomes de domínio personalizados e Listas de permissões de IP em seus ambientes.

### Correções de erros {#bug-fixes-cloud-manager}

* Algumas ocorrências de falhas em estágio de digitalização de código sem fornecer resultados abordados.

* O cartão de ambiente não exibia consistentemente o botão **Adicionar**.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Fluxos de trabalhos {#workflows}

* Foi adicionado suporte para pesquisar instâncias de fluxo de trabalho com base em Título do fluxo de trabalho, Modelo do fluxo de trabalho, Status, Iniciador, Caminho da carga e Data do Start. Consulte [Pesquisar Instâncias do Fluxo de Trabalho](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### Sincronização de Dados de Usuário da Camada de Publicação {#user-sync}

* Os dados do usuário, incluindo atributos de perfil e associações de grupo, podem ser mantidos na camada de publicação. Saiba mais sobre este recurso na [documentação de registro, logon e Perfil do usuário](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### Analisadores de compilação do SDK {#analyzers}

O AEM como um plug-in Maven do Cloud Service SDK Build Analyzer detecta problemas em um projeto maven, incluindo dependências ausentes. Ele oferece aos desenvolvedores uma oportunidade de descobrir problemas durante o desenvolvimento local, bem antes de implantar ambientes da Cloud com o Cloud Manager. Para obter mais informações, consulte a documentação [aqui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) e [aqui](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

### Outros {#others-foundation}

A nova sintaxe [&quot;httpd -t&quot;](/help/implementing/dispatcher/disp-overview.md#local-validation) verifica se há configuração de cache e despachante executada durante a compilação do Cloud Manager, que também pode ser executada usando AEM como Ferramentas do Dispatcher do Cloud Service SDK.

## Ferramentas de refatoração de código {#code-refactoring-tools}

### Novidades em [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Nova versão do plug-in AIO-CLI lançada. A versão mais recente deste plug-in inclui correções de erros para o AEM Dispatcher Converter e o Repository Modernizer, além de oferecer suporte a um novo utilitário - Index Converter. Consulte [Experiência unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para saber mais sobre este plug-in.

* Index Converter é um utilitário que pode ser usado para transformar as Definições de índice OAK personalizado de um cliente em AEM como Definições de índice OAK compatíveis com Cloud Service.
Consulte [Index Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obter mais detalhes.

* Novo recurso adicionado ao [Modernizador do repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que cria um pacote separado `ui.config` para conter todas as configurações de OSGi.

### Correções de erros {#crt-bug-fixes}

* Várias correções de erros feitas nas ferramentas AEM Dispatcher Converter e Repository Modernizer.
Consulte [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Modernizador do Repositório](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).