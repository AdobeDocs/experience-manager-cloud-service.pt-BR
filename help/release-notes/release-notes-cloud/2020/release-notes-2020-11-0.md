---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2020.11.0.
description: "[!DNL Adobe Experience Manager] Notas de versão as a Cloud Service para 2020.11.0."
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 11%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as Notas de versão gerais de [!DNL Experience Manager] as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento para [!DNL Adobe Experience Manager] O as a Cloud Service 2020.11.0 é 2 de dezembro de 2020.
A seguinte versão (2020.12.0) será lançada em 17 de dezembro de 2020

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novidades do [!DNL Sites] {#what-is-new-sites}

* **[Inicia o Gerenciamento de Hierarquia](/help/sites-cloud/authoring/launches/managing-pages.md) &amp; [Timewarp Futuro](/help/sites-cloud/authoring/launches/preview.md)**: A nova interface para adicionar/remover páginas em um lançamento e a navegação do site com o Timewarp mostram o estado futuro das Inicializações.

* **[Modelos e editor de fragmentos de conteúdo estendido](/help/assets/content-fragments/content-fragments-models.md)**: Novas opções para a validação de entrada em vários tipos de dados, o tipo de dados Enumeração aprimorado com novas visualizações de formulário e o nome de modelo do Fragmento de conteúdo são exibidos e pesquisáveis na interface do usuário do Assets.

* **Classificar as páginas da Live Copy disponíveis para implantação**: Nova opção para classificar as páginas da Live Copy disponíveis para implantação usando o [!UICONTROL Nome], [!UICONTROL Data da última modificação]e [!UICONTROL Data da última implantação] propriedades. O [!UICONTROL Data da última implantação] para uma página é uma nova propriedade introduzida.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novidades do [!DNL Assets] e [!DNL Dynamic Media] {#what-is-new-assets}

* **Assimilação de ativos em massa**: Fornecer aos clientes um serviço de assimilação escalável nativo em nuvem que aproveite [!DNL Experience Manager] Arquitetura as a Cloud Service, incluindo microsserviços de ativos. Os principais casos de uso incluem assimilação em escala com monitoramento, relatórios e agendamento, permitindo a transferência inicial de ativos para armazenamentos de dados em nuvem usando ferramentas comuns de upload de nuvem. Consulte [ferramenta de assimilação em massa de ativos](/help/assets/add-assets.md#asset-bulk-ingestor).

   Essa ferramenta é para administradores de sistema, consultores ou parceiros de implementação. Esse recurso permite a ingestão em grande escala e é usado idealmente durante a ingestão inicial ou ocasionalmente a ingestão em grande escala. Para trabalhos de assimilação menores, use o [[!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) ou [fazer upload usando a interface do usuário do Assets](/help/assets/add-assets.md#upload-assets).

   ![Configuração do importador a granel](/help/assets/assets/bulk-import-config-low-res.png)

* Os usuários agora podem classificar os ativos digitais nas exibições de Cartão e Coluna.

   ![classificar ativos](/help/assets/assets/asset-sort-options.png)

* Os seguintes aprimoramentos são feitos para acessibilidade em [!DNL Experience Manager Assets] nesta versão. Para obter mais informações, consulte [recursos de acessibilidade em [!DNL Assets]](/help/assets/accessibility.md).

   * Ao navegar pela linha do tempo usando um teclado, a tecla Esc pode recolher a opção Mostrar tudo sem perder o foco.
   * Ao navegar usando a tecla de guia do teclado, depois de remover a última tag das tags adicionadas, o campo de tag retém o foco.
   * [!DNL Experience Manager] Os componentes agora contêm as informações apropriadas para o nome, função e valor a serem usados pelos leitores de tela.
   * Após excluir a caixa de combinação Tipo/Tamanho, a caixa de combinação Link, a caixa de combinação Idioma ou a caixa de edição Texto, o foco do teclado retorna para os elementos da interface do usuário seguinte ou anterior ou para um elemento da interface do usuário mais relevante.
   * Ao passar o ponteiro do mouse sobre as opções, dicas como Selecionar e Download são exibidas. Os usuários que usam uma lente de aumento de tela podem não ver as miniaturas do arquivo por causa dessas dicas. Agora, é possível preservar o foco, após remover a opção usando `Escape` chave.
   * Ao selecionar uma célula de grade da grade presente na página, o foco passa para a barra de ação que aparece na tela.
   * Os usuários visuais podem se diferenciar entre um texto normal e um link, já que as pistas visuais (ícone sublinhado e divisa) são exibidas para links para todas as soluções em [!DNL Experience Manager] página inicial.

* **Predefinições do conjunto de lotes no Dynamic Media**: Agora é possível automatizar a criação e a organização de vários ativos em um conjunto de imagens ou conjunto de rotação no momento em que você faz upload de arquivos de ativos para uma pasta individualmente ou usando a assimilação em massa.

   Consulte [Sobre predefinições do conjunto de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).

* Os seguintes aprimoramentos de acessibilidade estão disponíveis em [!DNL Dynamic Media]:

   * Leitores de tela (JAWS, Narrador) narram o nome, a função e o estado dos itens de menu na opção de menu Incorporar tamanho.
   * Os usuários podem navegar na caixa de diálogo Link de email usando o `Tab` chave.
   * O fluxo de trabalho para criar perfis de codificação de vídeo é mais fácil de usar, considerando o aprimoramento do leitor de tela.
   * Ao navegar usando `Tab` , o foco é movido para os elementos apropriados da interface do usuário no fluxo de trabalho para criar um vídeo interativo.
   * A página Publicar, Editar ativo, Editar recortes inteligentes e a página Editor do conjunto de imagens são aprimoradas para estar em conformidade com os padrões da Web. Os usuários da tecnologia assistiva (AT) agora podem navegar facilmente por essas páginas e realizar ações, como recortar imagens.
   * Os visualizadores são aprimorados para permitir que os usuários naveguem usando um teclado.
   * Os usuários de teclado e leitor de tela podem usar a funcionalidade de recorte.
   * Os usuários de teclado podem gerenciar melhor os pontos de conexão.

   Consulte [Acessibilidade em [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novidades {#what-is-new-commerce}

* Lançamento do site de referência CIF Venia - 2020.11.05, que inclui a versão v1.5.0 dos Componentes principais CIF mais recentes. Consulte [Site de referência CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) para obter mais detalhes.

* Lançamento de componentes principais CIF v1.5.0. Consulte [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) para obter mais detalhes.

### Correções de erros {#bug-fixes-commerce}

* A configuração de cliente GraphQL não foi lida corretamente quando a configuração não foi especificada diretamente na configuração do Sling CA, mas em uma das configurações principais. Isso foi corrigido.

## Cloud Manager {#cloud-manager}

### Data de lançamento {#release-date-cm}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2020.11.0 é 12 de novembro de 2020.

### Novidades do [!DNL Cloud Manager] {#what-is-new-cm}

* Uma nova opção de menu **Logon local** agora está disponível para os usuários nas opções do menu Ambiente na **Ambientes** cartão e **Ambientes** páginas de resumo.
Consulte [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md#login-locally) para obter mais detalhes.

* O **Saiba mais** no Cloud Manager foi atualizada com novas imagens na interface do usuário.

### Correções de erros {#bug-fixes-cloud-manager}

* O carregamento de dependências feitas antes da execução da build requer o download de um plug-in Maven.
* O link do rodapé do Cloud Manager para selecionar um idioma agora irá navegar até o local correto.
* Às vezes, durante a verificação do código, o processo SonarQube não era iniciado. Isso será detectado automaticamente e uma reinicialização tentada.
* Todos os pipelines de produção existentes serão ativados automaticamente com a etapa Auditoria de experiência.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Fluxos de trabalhos {#workflows}

* Foi adicionado suporte para pesquisar instâncias de fluxo de trabalho com base em Título do fluxo de trabalho, Modelo do fluxo de trabalho, Status, Iniciador, Caminho da carga útil e Data inicial. Consulte [Pesquisar instâncias do fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### Sincronização de dados do usuário da camada de publicação {#user-sync}

* Os dados do usuário, incluindo atributos de perfil e associações de grupo, podem ser mantidos no nível de publicação. Saiba mais sobre este recurso em [Documentação de registro, logon e perfil do usuário](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### Analisadores de build do SDK {#analyzers}

O plug-in para Maven do Analisador de build do SDK do AEM as a Cloud Service detecta problemas em um projeto Maven, incluindo dependências ausentes. Ele oferece aos desenvolvedores uma oportunidade de descobrir problemas durante o desenvolvimento local, bem antes da implantação em ambientes da nuvem com o Cloud Manager. Para obter mais informações, consulte a documentação [here](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR#developing) e [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

### Outros {#others-foundation}

Novo [Sintaxe &quot;httpd -t&quot;](/help/implementing/dispatcher/disp-overview.md#local-validation) verifique se a configuração do apache e do dispatcher foi executada durante a build do Cloud Manager, que também pode ser executada usando AEM ferramentas do Dispatcher do SDK as a Cloud Service.

## Ferramenta Transferência de conteúdo {#content-transfer-tool}

Siga esta seção para saber mais sobre as novidades e as atualizações do [Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Versão v1.1.12.

### Novidades {#what-is-new-ctt}

* A experiência do usuário para logs foi aprimorada. Carimbos de data e hora adicionados aos logs de Extração e Assimilação. Mensagem adicionada para indicar se os logs estão vazios.

### Correções de erros {#ctt-bug-fixes}

* A ferramenta Transferência de conteúdo ignorava os arquivos de conteúdo se o conjunto de migração contivesse caminhos que tivessem os nomes de arquivo parcialmente semelhantes. Isso foi corrigido.

## Analisador de práticas recomendadas {#best-practices-analyzer}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas é 13 de novembro de 2020.

### Novidades do [!DNL Best Practices Analyzer] {#what-is-new-bpa}

* O Cloud Readiness Analyzer agora é BPA (Best Practices Analyzer). O BPA fornece uma avaliação das práticas recomendadas da implementação de AEM atual e ajuda a avaliar a preparação para mudar de uma instância de AEM existente para AEM as a Cloud Service.

* Um novo detector foi adicionado para detectar o uso de `java.io.InputStream`, que pode causar problemas se for usado em AEM as a Cloud Service.

### Correções de erros {#bpa-bug-fixes}

* Erro que causa os positivos relacionados ao *base do campo de texto* foi corrigido.
