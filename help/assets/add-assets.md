---
title: Adicione seus ativos digitais a [!DNL Adobe Experience Manager].
description: Adicione seus ativos digitais a [!DNL Adobe Experience Manager] como a [!DNL Cloud Service].
translation-type: tm+mt
source-git-commit: a5c9ec14af4241734fb6f6c88d5fc982e52924ce
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 1%

---


# Adicionar ativos digitais ao Adobe Experience Manager {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager] enriquece o conteúdo binário dos arquivos digitais carregados com metadados ricos, tags inteligentes, execuções e outros serviços de Gerenciamento de ativos digitais (DAM). Você pode carregar vários tipos de arquivos, como imagens, documentos e arquivos de imagem brutos, da pasta local ou de uma unidade de rede para [!DNL Experience Manager Assets].

Vários métodos de upload são fornecidos. Além do upload mais usado do navegador, existem outros métodos de adicionar ativos ao repositório [!DNL Experience Manager], incluindo clientes desktop, como o Adobe Asset Link ou [!DNL Experience Manager] aplicativo desktop, scripts de upload e ingestão que os clientes criariam e integrações de ingestão automatizadas adicionadas como extensões [!DNL Experience Manager].

Vamos nos concentrar nos métodos de upload para usuários finais aqui e fornecer links para artigos que descrevem aspectos técnicos do upload e ingestão de ativos usando [!DNL Experience Manager] APIs e SDKs.

Embora seja possível carregar e gerenciar qualquer arquivo binário em [!DNL Experience Manager], os formatos de arquivo mais usados têm suporte para serviços adicionais, como extração de metadados ou geração de pré-visualização/execução. Consulte [formatos de arquivo suportados](file-format-support.md) para obter detalhes.

Você também pode optar por fazer um processamento adicional nos ativos carregados. Vários perfis de processamento de ativos podem ser configurados na pasta, na qual os ativos são carregados, para adicionar metadados específicos, representações ou serviços de processamento de imagens. Consulte [processar ativos quando carregados](#process-when-uploaded).

>[!NOTE]
>
>[!DNL Experience Manager] como um  [!DNL Cloud Service] aproveitador de uma nova maneira de fazer upload de ativos - fazer upload binário direto. Por padrão, ele é suportado pelos recursos e clientes prontos para uso do produto, como [!DNL Experience Manager] interface do usuário, [!DNL Adobe Asset Link], [!DNL Experience Manager] aplicativo desktop e, portanto, transparente para os usuários finais.
>
>O código de upload personalizado ou estendido pelas equipes técnicas dos clientes precisa usar as novas APIs e protocolos de upload.

Os ativos como [!DNL Cloud Service] fornecem os seguintes métodos de upload. O Adobe recomenda que você entenda o caso de uso e a aplicabilidade de uma opção de upload antes de usá-la.

| Método de upload | Quando usar? | Persona principal |
|---------------------|----------------|-----------------|
| [Interface do usuário do console Ativos](#upload-assets) | Carregamento ocasional, facilidade de pressionar e arrastar, carregamento do localizador. Não use para carregar um grande número de ativos. | Todos os usuários |
| [Carregar API](#upload-using-apis) | Para decisões dinâmicas durante o upload. | Desenvolvedor |
| [[!DNL Experience Manager] aplicativo para desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Entrada de ativos de baixo volume, mas para migração. | Administrador, Marketer |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) | Útil quando criativos e profissionais de marketing trabalham em ativos de dentro dos [!DNL Creative Cloud] aplicativos de desktop compatíveis. | Creative, Marketer |
| [Adquirente em massa do ativo](#asset-bulk-ingestor) | Recomendado para migrações em grande escala e ingestões ocasionais em massa. Somente para armazenamentos de dados suportados. | Administrador, Desenvolvedor |

## Carregar ativos {#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   ![chlimage_1-211](assets/chlimage_1-211.png)

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The Pause button does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** button appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload`node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click the **[!UICONTROL Play]** icon.

   ![chlimage_1-212](assets/chlimage_1-212.png)
-->

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->

Para carregar um arquivo (ou vários arquivos), você pode selecioná-los na área de trabalho e arrastar a interface do usuário (navegador da Web) para a pasta de destino. Como alternativa, você pode iniciar o upload a partir da interface do usuário.

1. Na interface do usuário [!DNL Assets], navegue até o local onde deseja adicionar ativos digitais.
1. Para fazer upload dos ativos, execute um dos procedimentos a seguir:

   * Na barra de ferramentas, clique em **[!UICONTROL Criar]** > **[!UICONTROL Ficheiros]**. Você pode renomear o arquivo na caixa de diálogo apresentada, se necessário.
   * Em um navegador compatível com HTML5, arraste os ativos diretamente na interface do usuário [!DNL Assets]. A caixa de diálogo para renomear o arquivo não é exibida.

   ![create_menu](assets/create_menu.png)

   Para selecionar vários arquivos, selecione a tecla `Ctrl` ou `Command` e selecione os ativos na caixa de diálogo do seletor de arquivos. Ao usar um iPad, você pode selecionar apenas um arquivo de cada vez.

1. Para cancelar um upload em andamento, clique em fechar (`X`) ao lado da barra de progresso. Quando você cancela a operação de upload, [!DNL Assets] exclui a parte parcialmente carregada do ativo.
Se você cancelar uma operação de upload antes que os arquivos sejam carregados, [!DNL Assets] interrompe o upload do arquivo atual e atualiza o conteúdo. No entanto, os arquivos que já foram carregados não são excluídos.

1. A caixa de diálogo de progresso do upload em [!DNL Assets] exibe a contagem de arquivos carregados com êxito e os arquivos que não foram carregados.
Além disso, a interface do usuário [!DNL Assets] exibe o ativo mais recente que você carregou ou a pasta que criou primeiro.

>[!NOTE]
>
>Para carregar hierarquias de pastas aninhadas, consulte [itens de upload em massa](#bulk-upload).

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of [!DNL Assets]. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests [!DNL Assets] can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, [!DNL Assets] may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, [!DNL Assets] ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in Crx-de and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to [!DNL Experience Manager], the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. [!DNL Assets] supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in [!DNL Assets].

>[!NOTE]
>
>Streaming upload is disabled for [!DNL Experience Manager] running on JEE server with servlet-api version lower than 3.1.
-->

### Manuseio de uploads quando o ativo já existe {#handling-upload-existing-file}

Você pode carregar um ativo com o mesmo caminho (mesmo nome e mesmo local) de um ativo existente. No entanto, uma caixa de diálogo de aviso é exibida com as seguintes opções:

* Substituir ativo existente: Se você substituir um ativo existente, os metadados do ativo e quaisquer modificações anteriores (por exemplo, anotações, recortes e assim por diante) que você fez no ativo existente serão excluídos.
* Criar outra versão: Uma nova versão do ativo existente é criada no repositório. Você pode visualização as duas versões na [!UICONTROL Linha do tempo] e pode reverter para a versão existente anteriormente, se necessário.
* Mantenha ambos: Se você optar por manter ambos os ativos, o novo ativo será renomeado com o número `1` anexado ao seu nome.

>[!NOTE]
>
>Quando você seleciona **[!UICONTROL Substituir]** na caixa de diálogo [!UICONTROL Conflito de nomes], a ID do ativo é regenerada para o novo ativo. Essa ID é diferente da ID do ativo anterior.
>
>Se o Asset Insights estiver habilitado para rastrear impressões ou cliques com [!DNL Adobe Analytics], a ID de ativo regenerada invalida os dados capturados para o ativo em [!DNL Analytics].

Para manter o ativo do duplicado em [!DNL Assets], clique em **[!UICONTROL Manter]**. Para excluir o ativo de duplicado carregado, toque/clique em **[!UICONTROL Excluir]**.

### Manuseio de nome de arquivo e caracteres proibidos {#filename-handling}

[!DNL Experience Manager Assets] tenta impedir que você carregue ativos com os caracteres proibidos em seus nomes de arquivo. Se você tentar carregar um ativo com um nome de arquivo contendo um caractere não permitido ou mais, [!DNL Assets] exibirá uma mensagem de aviso e interromperá o upload até que você remova esses caracteres ou faça upload com um nome permitido. Alguns métodos de upload não impedem o upload de ativos com caracteres proibidos nos nomes de arquivos, mas substituem os caracteres por `-`.

Para adequar-se a convenções de nomenclatura de arquivos específicas para sua organização, a caixa de diálogo [!UICONTROL Carregar ativos] permite que você especifique nomes longos para os arquivos carregados. Os seguintes caracteres (lista separada por espaços de) não são suportados:

* caracteres inválidos para nome de arquivo de ativo `* / : [ \\ ] | # % { } ? &`
* caracteres inválidos para o nome da pasta de ativos `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Carregar ativos em massa {#bulk-upload}

O incorporador de ativos em massa pode lidar com milhares de ativos com eficiência. No entanto, uma ingestão em grande escala não é apenas um depósito de arquivos amplo e grande ou uma migração cega. Para ser um projeto significativo que atende a sua finalidade comercial, o planejamento e a preparação dos ativos levam a uma ingestão muito mais eficiente. Todas as ingestões não são as mesmas e as generalizações não podem ser feitas sem considerar a composição de repositório e as necessidades de negócios diversificadas. A seguir estão sugestões abrangentes para planejar e executar uma ingestão em massa:

* Preparar ativos: Remova ativos que não são necessários no DAM. Considere remover ativos não utilizados, obsoletos ou duplicados. Isso reduz os dados transferidos e os ativos assimilados, o que resulta em ingestões mais rápidas.
* Organizar ativos: Considere organizar o conteúdo em alguma ordem lógica, por exemplo, por tamanho de arquivo, formato de arquivo, caso de uso ou prioridade. Em geral, arquivos complexos grandes exigem mais processamento. Você também pode considerar a assimilação de arquivos grandes separadamente usando a opção de filtragem do tamanho do arquivo (descrita abaixo).
* Perguntas mais frequentes: Considere dividir sua ingestão em vários projetos de ingestão em massa. Isso permite que você visualize o conteúdo mais cedo e atualize sua ingestão, conforme necessário. Por exemplo, você pode assimilar ativos de processamento intensivo durante horas que não sejam de pico ou gradualmente em várias partes. Entretanto, é possível assimilar ativos menores e mais simples que não exigem muito processamento de uma só vez.

Para carregar um número maior de arquivos, use uma das seguintes abordagens. Além disso, consulte os [casos de uso e métodos](#upload-methods-comparison)

* [APIs](developer-reference-material-apis.md#asset-upload-technical) de upload de ativos: Use um script de upload personalizado ou uma ferramenta que aproveite as APIs para adicionar manuseio adicional de ativos (por exemplo, traduzir metadados ou renomear arquivos), se necessário.
* [[!DNL Experience Manager] aplicativo](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) para desktop: Útil para profissionais de criação e profissionais de marketing que carregam ativos de seu sistema de arquivos local. Use-o para carregar pastas aninhadas disponíveis localmente.
* [Ferramenta](#asset-bulk-ingestor) de ingestão em massa: Use para a ingestão de grandes quantidades de ativos ocasionalmente ou inicialmente durante a implantação  [!DNL Experience Manager].

### Ferramenta de assimilação de itens em massa {#asset-bulk-ingestor}

A ferramenta é fornecida somente para o grupo de administradores a ser usado para a ingestão em grande escala de ativos do Azure ou de armazenamentos de dados S3.

Para configurar a ferramenta, siga estas etapas:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Importação em massa]**. Selecione a opção **[!UICONTROL Criar]**.

![Configuração do importador a granel](assets/bulk-import-config.png)

1. Na página [!UICONTROL configuração de importação em massa], forneça os valores necessários.

   * [!UICONTROL Título]: Um título descritivo.
   * [!UICONTROL Fonte] de importação: Selecione a fonte de dados aplicável.
   * [!UICONTROL Filtrar por tamanho] mínimo: Forneça o tamanho mínimo de arquivo dos ativos em MB.
   * [!UICONTROL Filtrar por tamanho] máximo: Forneça o tamanho máximo de arquivos dos ativos em MB.
   * [!UICONTROL Excluir tipos] Mime: Lista separada por vírgulas de tipos MIME para excluir da ingestão. Por exemplo, `image/jpeg, image/.*, video/mp4`.
   * [!UICONTROL Incluir tipos] Mime: Lista separada por vírgulas de tipos MIME para incluir na ingestão. Consulte [todos os formatos de arquivo suportados](/help/assets/file-format-support.md).
   * [!UICONTROL Modo] de importação: Selecione Ignorar, Substituir ou Criar versão. O modo Ignorar é o padrão e, nesse modo, o ingresso pula para importar um ativo se ele já existir. Consulte o significado de [substituir e criar opções de versão](#handling-upload-existing-file).
   * [!UICONTROL Pasta] de Público alvo de ativos: Importe a pasta no DAM onde os ativos devem ser importados. Por exemplo, `/content/dam/imported_assets`

1. Você pode excluir, modificar, executar e fazer mais com as configurações de ingresso criadas. Quando você seleciona uma configuração de importação em massa de assimiladores, a opção a seguir está disponível na barra de ferramentas.

   * [!UICONTROL Editar]: Editar a configuração selecionada.
   * [!UICONTROL Excluir]: Excluir a configuração selecionada.
   * [!UICONTROL Verificar]: Valide a conexão com o armazenamento de dados.
   * [!UICONTROL Execução] seca: Chame uma execução de teste da ingestão em massa.
   * [!UICONTROL Executar]: Executar a configuração selecionada.
   * [!UICONTROL Parar]: Encerre uma configuração ativa.
   * [!UICONTROL Status] do trabalho: Visualização do status da configuração quando ela é usada em um trabalho de importação em andamento ou usada para um trabalho concluído.
   * [!UICONTROL Ativos] de visualização: Visualização a pasta público alvo, se ela existir.

## Fazer upload de ativos usando clientes desktop {#upload-assets-desktop-clients}

Além da interface de usuário do navegador da Web, [!DNL Experience Manager] oferece suporte a outros clientes no desktop. Eles também fornecem experiência de upload sem a necessidade de acessar o navegador da Web.

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) fornece acesso a ativos  [!DNL Experience Manager] em aplicativos de desktop Adobe Photoshop, Adobe Illustrator e Adobe InDesign. Você pode fazer upload do documento atualmente aberto para [!DNL Experience Manager] diretamente da interface do usuário do Adobe Asset Link a partir desses aplicativos de desktop.
* [[!DNL Experience Manager] o aplicativo desktop ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) simplifica o trabalho com ativos no desktop, independentemente do tipo de arquivo ou do aplicativo nativo que os manipula. É particularmente útil fazer upload de arquivos nas hierarquias de pastas aninhadas a partir do sistema de arquivos local, já que o upload do navegador suporta apenas o upload de listas de arquivos simples.

## Processar ativos quando carregados {#process-when-uploaded}

Para fazer um processamento adicional nos ativos carregados, você pode aplicar perfis de processamento nas pastas carregadas. Os perfis estão disponíveis na página **[!UICONTROL Propriedades]** de uma pasta em [!DNL Assets].

![assets-folder-properties](assets/assets-folder-properties.png)

As seguintes guias estão disponíveis:

* [Os ](metadata-profiles.md) perfis de metadados permitem aplicar propriedades de metadados padrão a ativos carregados nessa pasta
* [O processamento de ](asset-microservices-configure-and-use.md) perfis permite que você gere mais execuções do que são possíveis por padrão.

Além disso, se [!DNL Dynamic Media] estiver ativado na implantação, as seguintes guias estarão disponíveis:

* [Os ](dynamic-media/image-profiles.md) perfis de Imagem de Dynamic Media permitem aplicar recortes específicos (recorte **[!UICONTROL inteligente e recorte de]** pixels) e configurações de nitidez aos ativos carregados.
* [Os ](dynamic-media/video-profiles.md) perfis de vídeo do Dynamic Media permitem que você aplique perfis de codificação de vídeo específicos (resolução, formato, parâmetros).

>[!NOTE]
>
>O corte do Dynamic Media e outras operações em ativos não são destrutivas, ou seja, não alteram o original carregado, mas fornecem parâmetros para o corte ou transformação de mídia a ser feito ao entregar os ativos

Para pastas com um perfil de processamento atribuído, o nome do perfil aparece na miniatura na visualização do cartão. Na visualização da lista, o nome do perfil aparece na coluna **[!UICONTROL Processando Perfil]**.

## Carregar ou assimilar ativos usando APIs {#upload-using-apis}

Detalhes técnicos das APIs e protocolo de upload, além de links para SDK de código aberto e clientes de amostra, são fornecidos na seção [upload de ativos](developer-reference-material-apis.md#asset-upload-technical) da referência do desenvolvedor.

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] aplicativo para desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [About [!DNL Adobe Asset Link]](https://www.adobe.com/br/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] documentação](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Referência técnica para upload de ativos](developer-reference-material-apis.md#asset-upload-technical)

