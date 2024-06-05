---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2020.11.0.
description: "[!DNL Adobe Experience Manager] Notas de versão as a Cloud Service para 2020.11.0."
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 15%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais do [!DNL Experience Manager] as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Adobe Experience Manager] O as a Cloud Service 2020.11.0 é 2 de dezembro de 2020.
A versão seguinte (2020.12.0) será lançada em 17 de dezembro de 2020

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* **[Inicia o Gerenciamento de Hierarquia](/help/sites-cloud/authoring/launches/managing-pages.md) &amp; [Timewarp do futuro](/help/sites-cloud/authoring/launches/preview.md)**: nova interface para adicionar/remover páginas em um lançamento, e navegar pelo site com o Timewarp mostra o estado futuro de Lançamentos.

* **[Modelos e editor de fragmentos de conteúdo estendido](/help/assets/content-fragments/content-fragments-models.md)**: novas opções para validação de entrada em vários tipos de dados, tipo de dados de Enumeração aprimorado com novas visualizações de formulário e nome do modelo de Fragmento de conteúdo são exibidas e pesquisáveis na interface do usuário do Assets.

* **Classificar as páginas de Live Copy disponíveis para implantação**: nova opção para classificar as páginas de Live Copy disponíveis para implantação usando o [!UICONTROL Nome], [!UICONTROL Última data de modificação], e [!UICONTROL Última data de implantação] propriedades. A variável [!UICONTROL Última data de implantação] para uma página é uma nova propriedade introduzida.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novidades do [!DNL Assets] e [!DNL Dynamic Media] {#what-is-new-assets}

* **Assimilação de ativos em massa**: forneça aos clientes um serviço de assimilação escalável e nativo em nuvem que usa o [!DNL Experience Manager] Arquitetura as a Cloud Service, incluindo microsserviços de ativos. Os principais casos de uso incluem assimilação em escala com monitoramento, relatórios e agendamento, permitindo a transferência inicial de ativos para armazenamentos de dados em nuvem usando ferramentas comuns de upload em nuvem. Consulte [ferramenta de entrada de ativos em massa](/help/assets/add-assets.md#asset-bulk-ingestor).

  Essa ferramenta é para personas de administrador do sistema, consultor ou parceiro de implementação. Esse recurso permite a assimilação em grande escala e é idealmente usado durante a assimilação inicial ou assimilação grande ocasional. Para tarefas de assimilação menores, use o [[!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=pt-BR) ou [fazer upload usando a interface do Assets](/help/assets/add-assets.md#upload-assets).

  ![Configuração do importador em massa](/help/assets/assets/bulk-import-config-low-res.png)

* Agora os usuários podem classificar os ativos digitais nas exibições de Cartão e Coluna.

  ![classificar ativos](/help/assets/assets/asset-sort-options.png)

* Os seguintes aprimoramentos são feitos para acessibilidade no [!DNL Experience Manager Assets] nesta versão. Para obter mais informações, consulte [recursos de acessibilidade no [!DNL Assets]](/help/assets/accessibility.md).

   * Ao navegar pela linha do tempo usando um teclado, a tecla Esc pode recolher a opção Mostrar tudo sem perder o foco.
   * Ao navegar usando a tecla tab do teclado, após remover a última tag das tags adicionadas, o campo de tag manterá o foco.
   * [!DNL Experience Manager] os componentes agora contêm informações apropriadas sobre nome, função e valor a serem usados por leitores de tela.
   * Depois de excluir a caixa de combinação Tipo/Tamanho, a caixa de combinação Link, a caixa de combinação Idioma ou a caixa de edição Texto, o foco do teclado retorna ao elemento da interface do usuário seguinte ou anterior ou a um elemento da interface do usuário mais relevante.
   * Ao passar o ponteiro sobre as opções, dicas como Selecionar e Baixar são exibidas. Os usuários que usam uma lente de aumento de tela podem não ver as miniaturas de arquivo devido a essas dicas. Agora, é possível preservar o foco, após remover a opção usando `Escape` chave.
   * Ao selecionar uma célula de grade na grade presente na página, o foco é alternado para a barra de ação que aparece na tela.
   * Os usuários visuais podem diferenciar entre texto normal e um link, já que dicas visuais (ícone de sublinhado e divisa) são exibidas para links para todas as soluções no [!DNL Experience Manager] página inicial.

* **Predefinições de conjunto de lotes no Dynamic Media**: agora é possível automatizar a criação e a organização de vários ativos em um conjunto de imagens ou em um conjunto de rotação no momento em que você faz upload de arquivos de ativos para uma pasta individualmente ou usando a assimilação em massa.

  Consulte [Sobre predefinições de conjunto de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).

* Os seguintes aprimoramentos de acessibilidade estão disponíveis no [!DNL Dynamic Media]:

   * Os leitores de tela (JAWS, Narrador) narram o nome, a função e o estado dos itens de menu na opção de menu Incorporar tamanho.
   * Os usuários podem navegar pela caixa de diálogo Link de email usando o `Tab` chave.
   * O fluxo de trabalho para criar perfis de codificação de vídeo é mais fácil de usar, considerando os aprimoramentos do leitor de tela.
   * Ao navegar usando `Tab` , o foco é movido para os elementos apropriados da interface do usuário no fluxo de trabalho para criar um vídeo interativo.
   * As páginas Publicar, Editar ativo, Editar cortes inteligentes e Editor de conjunto de imagens foram aprimoradas para cumprir os padrões da Web. Os usuários da tecnologia de assistência (AT) agora podem navegar facilmente nessas páginas e agir nelas, como recortar imagens.
   * Os visualizadores são aprimorados para permitir que os usuários naveguem usando o teclado.
   * Os usuários de teclado e leitor de tela podem usar a funcionalidade de corte.
   * Os usuários de teclado podem gerenciar melhor os pontos de conexão.

  Consulte [Acessibilidade em [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.11.05 que inclui a versão mais recente dos componentes principais CIF v1.5.0. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) para obter mais detalhes.

* Lançamento de componentes principais de CIF v1.5.0. Consulte [Componentes principais do CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) para obter mais detalhes.

### Correções de erros {#bug-fixes-commerce}

* A configuração do cliente do GraphQL não foi lida corretamente quando não está especificada diretamente na configuração da autoridade de certificação do Sling, mas em uma das configurações principais. Isso foi corrigido.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2020.11.0 é 12 de novembro de 2020.

### Novidades do [!DNL Cloud Manager] {#what-is-new-cm}

* Uma nova opção de menu **Logon local** O agora está disponível para usuários nas opções de menu do ambiente na **Ambientes** cartão e **Ambientes** páginas de resumo.
Consulte [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md#login-locally) para obter mais detalhes.

* A guia **Aprender** no Cloud Manager foi atualizada com novas imagens na interface do usuário.

### Correções de erros {#bug-fixes-cloud-manager}

* O carregamento de dependências realizado antes da execução da compilação exigia o download de um plug-in Maven.
* O link do rodapé do Cloud Manager para selecionar um idioma agora direcionará para o local correto.
* Às vezes, durante a verificação do código, o processo SonarQube não era iniciado. O processo agora será detectado automaticamente e haverá uma tentativa de reinicialização.
* Todos os pipelines de produção já existentes serão habilitados automaticamente na etapa Auditoria de experiência.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Fluxos de trabalhos {#workflows}

* Foi adicionado suporte para pesquisar instâncias de fluxo de trabalho com base no Título do fluxo de trabalho, Modelo do fluxo de trabalho, Status, Iniciador, Caminho da carga e Data de início. Consulte [Pesquisar instâncias de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### Sincronização de dados do usuário da camada de publicação {#user-sync}

* Os dados do usuário, incluindo atributos de perfil e associações de grupo, podem ser mantidos no nível de publicação. Saiba mais sobre esse recurso em [Documentação de registro, logon e perfil do usuário](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### Analisadores de build do SDK {#analyzers}

O plug-in para Maven do Analisador de build do SDK do AEM as a Cloud Service detecta problemas em um projeto Maven, incluindo dependências ausentes. Ele oferece aos desenvolvedores uma oportunidade de descobrir problemas durante o desenvolvimento local, bem antes de implantar em ambientes da nuvem com o Cloud Manager. Para obter mais informações, consulte a documentação [aqui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR#developing) e [aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html#building-for-the-sdk).

### Outros {#others-foundation}

Novo [Sintaxe &quot;httpd -t&quot;](/help/implementing/dispatcher/disp-overview.md#local-validation) verifique a configuração do apache e do dispatcher executada durante a compilação do Cloud Manager, que também pode ser executada usando as Ferramentas do Dispatcher do SDK do AEM as a Cloud Service.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Siga esta seção para saber mais sobre as novidades e atualizações do [Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Versão v1.1.12.

### Novidades {#what-is-new-ctt}

* Experiência do usuário para logs aprimorada. Carimbos de data e hora adicionados aos logs de Extração e assimilação. Mensagem adicionada para indicar se os logs estão vazios.

### Correções de erros {#ctt-bug-fixes}

* A Ferramenta de transferência de conteúdo ignorava arquivos de conteúdo se o conjunto de migração contivesse caminhos com nomes de arquivo parcialmente semelhantes. Isso foi corrigido.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas é 13 de novembro de 2020.

### Novidades do [!DNL Best Practices Analyzer] {#what-is-new-bpa}

* O Cloud Readiness Analyzer agora é o Best Practices Analyzer (BPA). O BPA fornece uma avaliação de práticas recomendadas da implementação atual do AEM e ajuda a avaliar a prontidão para mudar de uma instância existente do AEM para o AEM as a Cloud Service.

* Um novo detector foi adicionado para detectar o uso de `java.io.InputStream`, que pode causar problemas se usado no AEM as a Cloud Service.

### Correções de erros {#bpa-bug-fixes}

* Bug que causa os positivos relacionados ao *base de campo de texto* componente foi corrigido.
