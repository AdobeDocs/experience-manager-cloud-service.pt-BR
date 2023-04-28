---
title: Adicione seus ativos digitais ao [!DNL Adobe Experience Manager].
description: Adicione seus ativos digitais ao [!DNL Adobe Experience Manager] como [!DNL Cloud Service].
feature: Asset Management,Upload
role: User,Admin
exl-id: 0e624245-f52e-4082-be21-13cc29869b64
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '3094'
ht-degree: 1%

---

# Adicionar ativos digitais ao [!DNL Adobe Experience Manager] como [!DNL Cloud Service] [!DNL Assets] {#add-assets-to-experience-manager}

[!DNL Adobe Experience Manager Assets] O aceita vários tipos de ativos digitais de várias fontes. Ele armazena os binários e as representações criadas, pode fazer processamento de ativos usando uma variedade de fluxos de trabalho e [!DNL Adobe Sensei] , permite a distribuição por meio de vários canais em várias superfícies.

[!DNL Adobe Experience Manager] enriquece o conteúdo binário dos arquivos digitais carregados com metadados ricos, tags inteligentes, representações e outros serviços de Gerenciamento de ativos digitais (DAM). Você pode fazer upload de vários tipos de arquivos, como imagens, documentos e arquivos de imagem brutos, da pasta local ou de uma unidade de rede para o [!DNL Experience Manager Assets].

Além do upload do navegador mais usado, outros métodos de adicionar ativos à variável [!DNL Experience Manager] existe repositório, incluindo clientes de desktop, como o Adobe Asset Link ou [!DNL Experience Manager] aplicativo de desktop, upload e scripts de assimilação que os clientes criariam e integrações de assimilação automatizadas adicionadas como [!DNL Experience Manager] extensões.

Embora você possa fazer upload e gerenciar qualquer arquivo binário no [!DNL Experience Manager], os formatos de arquivo mais usados têm suporte para serviços adicionais, como extração de metadados ou geração de visualização/representação. Consulte [formatos de arquivo compatíveis](file-format-support.md) para obter detalhes.

Você também pode optar por realizar processamento adicional nos ativos carregados. Vários perfis de processamento de ativos podem ser configurados na pasta, na qual os ativos são carregados, para adicionar metadados, representações ou serviços de processamento de imagens específicos. Consulte [processar ativos ao fazer upload](#process-when-uploaded).

[!DNL Assets] forneça os seguintes métodos de upload. O Adobe recomenda compreender o caso de uso e a aplicabilidade de uma opção de upload antes de usá-la.

| Método de upload | Quando usar? | Persona Primária |
|---------------------|----------------|-----------------|
| [Interface do usuário do console Assets](#upload-assets) | Carregamento ocasional, facilidade de pressionar e arrastar, carregamento mais rápido. Não use o para fazer upload de um grande número de ativos. | Todos os usuários |
| [Upload da API](#upload-using-apis) | Para decisões dinâmicas durante o upload. | Desenvolvedor |
| Aplicativo de desktop do [[!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Assimilação de ativos de baixo volume, mas não para migração. | Administrador, profissional de marketing |
| [[!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) | Útil quando criativos e profissionais de marketing trabalham em ativos de dentro do [!DNL Creative Cloud] aplicativos de desktop. | Criativo, profissional de marketing |
| [Gestor em massa de ativos](#asset-bulk-ingestor) | Recomendado para migrações em larga escala e ingestões ocasionais em massa. Somente para armazenamentos de dados compatíveis. | Administrador, Desenvolvedor |

## Fazer upload de ativos {#upload-assets}

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The [!UICONTROL Pause] option does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** option appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload` node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click **[!UICONTROL Play]** option.
-->

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, [!DNL Experience Manager] saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->

Para carregar um arquivo (ou vários arquivos), você pode selecioná-los na área de trabalho e arrastar a interface do usuário (navegador da Web) para a pasta de destino. Como alternativa, você pode iniciar o upload na interface do usuário do .

1. No [!DNL Assets] na interface do usuário, navegue até o local onde deseja adicionar ativos digitais.
1. Para fazer upload dos ativos, siga um destes procedimentos:

   * Na barra de ferramentas, clique em **[!UICONTROL Criar]** > **[!UICONTROL Arquivos]**. Você pode renomear o arquivo na caixa de diálogo apresentada, se necessário.
   * Em um navegador compatível com a HTML 5, arraste os ativos diretamente no [!DNL Assets] interface do usuário. A caixa de diálogo para renomear arquivo não é exibida.

   ![criar_menu](assets/create_menu.png)

   Para selecionar vários arquivos, selecione o `Ctrl` ou `Command` e selecione os ativos na caixa de diálogo do seletor de arquivos. Ao usar uma iPad, você pode selecionar apenas um arquivo de cada vez.

1. Para cancelar um upload em andamento, clique em fechar (`X`) ao lado da barra de progresso. Ao cancelar a operação de upload, [!DNL Assets] exclui a parte parcialmente carregada do ativo.
Se você cancelar uma operação de upload antes que os arquivos sejam carregados, [!DNL Assets] para de carregar o arquivo atual e atualiza o conteúdo. No entanto, os arquivos que já foram carregados não são excluídos.

1. A caixa de diálogo andamento do upload em [!DNL Assets] exibe a contagem de arquivos carregados com êxito e os arquivos que não foram carregados.
Além disso, a variável [!DNL Assets] a interface do usuário exibe o ativo mais recente que você fez upload ou a pasta que você criou primeiro.

>[!NOTE]
>
>Para fazer upload de hierarquias de pastas aninhadas, consulte [upload em massa de ativos](#bulk-upload).

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of [!DNL Assets]. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests [!DNL Assets] can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, [!DNL Assets] may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, [!DNL Assets] ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in CRX-DE and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to [!DNL Experience Manager], the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. [!DNL Assets] supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in [!DNL Assets].

>[!NOTE]
>
>Streaming upload is disabled for [!DNL Experience Manager] running on JEE server with servlet-api version lower than 3.1.
-->

### Lidar com uploads quando o ativo já existe {#handling-upload-existing-file}

É possível fazer upload de um ativo com o mesmo caminho (mesmo nome e mesmo local) de um ativo existente. No entanto, uma caixa de diálogo de aviso é exibida com as seguintes opções:

* Substituir ativo existente: Se você substituir um ativo existente, os metadados do ativo e quaisquer modificações anteriores (por exemplo, anotações, corte e assim por diante) feitas no ativo existente serão excluídos.

   >[!NOTE]
   >
   >A opção para substituir ativos não está disponível se o ativo estiver bloqueado ou com check-out.

* Criar outra versão: Uma nova versão do ativo existente é criada no repositório. Você pode exibir as duas versões na [!UICONTROL Linha do tempo] e podem reverter para a versão existente anteriormente, se necessário.
* Mantenha ambos: Se você optar por manter ambos os ativos, o novo ativo será renomeado.

Para reter o ativo duplicado em [!DNL Assets], clique em **[!UICONTROL Manter]**. Para excluir o ativo duplicado carregado, clique em **[!UICONTROL Excluir]**.

### Tratamento de nomes de arquivos e caracteres proibidos {#filename-handling}

[!DNL Experience Manager Assets] impede que você carregue ativos com os caracteres proibidos em seus nomes de arquivo. Se você tentar fazer upload de um ativo com nomes de arquivo contendo um caractere não permitido ou mais, [!DNL Assets] exibe uma mensagem de aviso e interrompe o upload até que você remova esses caracteres ou faça upload com um nome permitido.

Para adequar-se a convenções específicas de nomenclatura de arquivos para a sua organização, o [!UICONTROL Fazer upload de ativos] permite especificar nomes longos para os arquivos carregados. Os seguintes caracteres (lista separada por espaços de) não são suportados:

* Caracteres inválidos para o nome do ativo: `* / : [ \\ ] | # % { } ? &`
* Caracteres inválidos para o nome da pasta de ativos: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Fazer upload em massa de ativos {#bulk-upload}

O criador de ativos em massa pode lidar com um grande número de ativos com eficiência. No entanto, uma assimilação em grande escala não é apenas um despejo de arquivo amplo ou uma migração casual. Para que uma assimilação em grande escala seja um projeto significativo que atende à sua finalidade comercial e seja eficiente, planeje a migração e prepare a organização de ativos. Todas as sugestões são diferentes, portanto, em vez de generalizar, fator na composição de repositório e nas necessidades comerciais avançadas. Veja a seguir algumas sugestões abrangentes para planejar e executar uma assimilação em massa:

* Preparar ativos: Remova ativos que não são necessários no DAM. Considere remover ativos não utilizados, obsoletos ou duplicados. Isso reduz os dados transferidos e os ativos assimilados, levando a ingestões mais rápidas.
* Organizar ativos: Considere organizar o conteúdo em alguma ordem lógica, por exemplo, por tamanho de arquivo, formato de arquivo, caso de uso ou prioridade. Em geral, arquivos complexos grandes exigem mais processamento. Você também pode considerar a assimilação de arquivos grandes separadamente usando a opção de filtragem do tamanho do arquivo (descrita abaixo).
* Gestões do Marcador: Considere dividir a assimilação em vários projetos de assimilação em massa. Isso permite que você veja o conteúdo antes e atualize a assimilação conforme necessário. Por exemplo, você pode assimilar ativos com processamento intensivo durante horas que não sejam de pico ou gradualmente em várias partes. No entanto, é possível assimilar ativos menores e mais simples que não exigem muito processamento de uma só vez.

Para fazer upload de um número maior de arquivos, use uma das abordagens a seguir. Além disso, consulte o [casos de uso e métodos](#upload-methods-comparison)

* [APIs de upload de ativos](developer-reference-material-apis.md#asset-upload): Use um script de carregamento personalizado ou uma ferramenta que aproveite as APIs para adicionar manuseio adicional de ativos (por exemplo, traduzir metadados ou renomear arquivos), se necessário.
* [[!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html): Útil para profissionais criativos e profissionais de marketing que fazem upload de ativos de seu sistema de arquivos local. Use-o para fazer upload de pastas aninhadas disponíveis localmente.
* [Ferramenta de assimilação em massa](#asset-bulk-ingestor): Use para assimilação de grandes quantidades de ativos ocasionalmente ou inicialmente ao implantar [!DNL Experience Manager].

### Ferramenta Importação de ativos em massa {#asset-bulk-ingestor}

A ferramenta é fornecida somente ao grupo de administradores para usar na assimilação em grande escala de ativos dos armazenamentos de dados do Azure ou S3. Assista a uma apresentação em vídeo da configuração e ingestão.

>[!VIDEO](https://video.tv.adobe.com/v/329680/?quality=12&learn=on)

A imagem a seguir ilustra os vários estágios ao assimilar ativos no Experience Manager de um armazenamento de dados:

![Ferramenta Assimilação em massa](assets/bulk-ingestion.png)

**Pré-requisitos**

É necessário ter uma conta de armazenamento externa ou um bucket do Azure ou AWS para usar esse recurso.

>[!NOTE]
>
>Crie o contêiner ou o bucket da conta de armazenamento como privado e aceite as conexões somente de solicitações autorizadas. No entanto, não há suporte para restrições adicionais sobre conexões de rede de entrada.

>[!NOTE]
>
>As contas de armazenamento externo podem ter regras de nome de arquivo/pasta diferentes da ferramenta Importação em massa. Consulte [Manuseio de nomes de arquivo durante a importação em massa](#filename-handling-bulkimport) para obter mais detalhes sobre nomes não permitidos/removidos.


### Configurar a ferramenta Importação em massa {#configure-bulk-ingestor-tool}

Para configurar a ferramenta Importação em massa, siga estas etapas:

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Importação em massa]**. Selecione o **[!UICONTROL Criar]** opção.

1. Especifique um título para a configuração de importação em massa no **[!UICONTROL Título]** campo.

1. Selecione o tipo de fonte de dados no **[!UICONTROL Importar Fonte]** lista suspensa.

1. Forneça os valores para criar uma conexão com a fonte de dados. Por exemplo, se você selecionar **Armazenamento Azure Blob** como fonte de dados, especifique os valores para a conta de armazenamento do Azure, o contêiner de blob do Azure e a chave de acesso do Azure.

1. Selecione o modo de autenticação necessário na lista suspensa. **Chave de Acesso do Azure** fornece acesso completo à conta de armazenamento do Azure, enquanto **Token SAS do Azure** permite que o administrador limite os recursos do token usando permissões e políticas de expiração.

1. Forneça o nome da pasta raiz que contém ativos na fonte de dados na **[!UICONTROL Pasta de Origem]** campo.

1. (Opcional) Forneça o tamanho mínimo de arquivo dos ativos em MB para incluí-los no processo de assimilação no **[!UICONTROL Filtrar por tamanho mínimo]** campo.

1. (Opcional) Forneça o tamanho máximo de arquivo dos ativos em MB para incluí-los no processo de assimilação no **[!UICONTROL Filtrar por tamanho máximo]** campo.

1. (Opcional) Especifique uma lista separada por vírgulas de tipos MIME a serem excluídos da assimilação no **[!UICONTROL Excluir tipos MIME]** campo. Por exemplo, `image/jpeg, image/.*, video/mp4`. Consulte [todos os formatos de arquivo compatíveis](/help/assets/file-format-support.md).

1. Especifique uma lista separada por vírgulas de tipos MIME para incluir da assimilação no **[!UICONTROL Incluir tipos MIME]** campo. Consulte [todos os formatos de arquivo compatíveis](/help/assets/file-format-support.md).

1. Selecione o **[!UICONTROL Excluir arquivo de origem após a importação]** opção para excluir os arquivos originais do armazenamento de dados de origem depois que os arquivos forem importados para o [!DNL Experience Manager].

1. Selecione o **[!UICONTROL Modo de importação]**. Selecionar **Ignorar**, **Substituir** ou **Criar versão**. O modo Ignorar é o padrão e, nesse modo, o assimilador ignora para importar um ativo se ele já existir. Veja o significado de [substituir e criar opções de versão](#handling-upload-existing-file).

1. Especifique um caminho para definir um local no DAM onde os ativos devem ser importados usando o **[!UICONTROL Pasta do Target de ativos]** campo. Por exemplo, `/content/dam/imported_assets`.

1. (Opcional) Especifique o arquivo de metadados a ser importado, fornecido no formato CSV, na função **[!UICONTROL Arquivo de metadados]** campo. Especifique o arquivo CSV no local do blob de origem e consulte o caminho ao configurar a ferramenta Importação em massa. O formato de arquivo CSV referenciado nesse campo é o mesmo do formato de arquivo CSV quando você [Importar e exportar metadados de ativos em massa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/metadata-import-export.html). Se você selecionar a variável **Excluir arquivo de origem após a importação** , filtre os arquivos CSV usando o **Excluir** ou **Incluir tipo MIME** ou **Filtrar por caminho/arquivo** campos. Você pode usar uma expressão regular para filtrar arquivos CSV nesses campos.

1. Clique em **[!UICONTROL Salvar]** para salvar a configuração.

### Gerenciar a configuração da ferramenta Importação em massa {#manage-bulk-import-configuration}

Depois de criar a configuração da ferramenta Importação em massa, você pode executar tarefas para avaliar a configuração antes de assimilar ativos em massa para sua instância do Experience Manager. Selecione a configuração disponível em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Importação em massa]** para exibir as opções disponíveis para gerenciar a configuração da ferramenta Importação em massa .

### Editar a configuração {#edit-configuration}

Selecione a configuração e clique em **[!UICONTROL Editar]** para modificar os detalhes de configuração. Não é possível editar o título da configuração e da fonte de dados de importação ao executar a operação de edição.

### Excluir a configuração {#delete-configuration}

Selecione a configuração e clique em **[!UICONTROL Excluir]** para excluir a configuração Importação em massa.

### Validar conexão com a fonte de dados {#validate-connection}

Selecione a configuração e clique em **[!UICONTROL check]** para validar a conexão com a fonte de dados. No caso de uma conexão bem-sucedida, o Experience Manager exibe a seguinte mensagem:

![Mensagem bem-sucedida de importação em massa](assets/bulk-import-success-message.png)

### Chamar uma execução de teste para o trabalho de importação em massa {#invoke-test-run-bulk-import}

Selecione a configuração e clique em **[!UICONTROL Execução de prática]** para chamar uma execução de teste para o trabalho de importação em massa. O Experience Manager exibe os seguintes detalhes sobre o trabalho de importação em massa:

![Resultado do teste](assets/dry-assets-result.png)

### Manuseio de nomes de arquivo durante a importação em massa {#filename-handling-bulkimport}

Ao importar ativos ou pastas em massa, [!DNL Experience Manager Assets] importa toda a estrutura do que existe na fonte de importação. [!DNL Experience Manager] O segue as regras incorporadas para caracteres especiais nos nomes de ativo e pasta, portanto, esses nomes de arquivo precisam de limpeza. Para o nome da pasta e do ativo, o título definido pelo usuário permanece inalterado e é armazenado em `jcr:title`.

Durante a importação em massa, [!DNL Experience Manager] procure as pastas existentes para evitar a reimportação de ativos e pastas, e também verifique as regras de limpeza aplicadas na pasta principal em que a importação ocorre. Se as regras de limpeza forem aplicadas na pasta pai, as mesmas regras serão aplicadas à fonte de importação. Para nova importação, as seguintes regras de limpeza são aplicadas para gerenciar os nomes de arquivo de ativos e pastas.

**Nomes não permitidos na importação em massa**

Os seguintes caracteres não são permitidos nos nomes de arquivo e pasta:

* Caracteres de uso privado e de controle (0x00 a 0x1F, \u0081, \uE000)
* Nomes de arquivos ou pastas terminando com um ponto (.)

Arquivos ou pastas com nomes que correspondem a essas condições são ignorados durante o processo de importação e marcados como falha.

**Manuseio do nome do ativo na importação em massa**

Para nomes de arquivos de ativos, o nome e o caminho do JCR são limpos usando a API: `JcrUtil.escapeIllegalJcrChars`.

* Caracteres Unicode não são alterados
* Substitua os caracteres especiais por seu Código de escape de URL, por exemplo, `new%asset.png` é atualizado para `new%25asset.png`:

   ```
                   URL escape code   
   
   "               %22
   %               %25
   '               %27
   *               %2A
   /               %2F
   :               %3A
   [               %5B
   \n              %0A
   \r              %0D
   \t              %09
   ]               %5D
   |               %7C
   ```

**Manipulação do nome da pasta na importação em massa**

Para nomes de arquivos de pastas, o nome e o caminho do JCR são limpos usando a API: `DamUtil.getSanitizedFolderName`.

* Os caracteres em maiúsculas são convertidos em minúsculas
* Caracteres Unicode não são alterados
* Substitua os caracteres especiais por um traço (&#39;-&#39;), por exemplo, `new folder` é atualizado para `new-folder`:

   ```
   "                           
   #                         
   %                           
   &                          
   *                           
   +                          
   .                           
   :                           
   ;                          
   ?                          
   [                           
   ]                           
   ^                         
   {                         
   }                         
   |                           
   /         It is used for split folder in cloud storage and is pre-handled, no conversion here.
   \         Not allowed in Azure, allowed in AWS.
   \t
   space     It is the space character.
   ```

<!-- 
[!DNL Experience Manager Assets] manages the forbidden characters in the filenames while you upload assets or folders. [!DNL Experience Manager] updates only the node names in the DAM repository. However, the `title` of the asset or folder remains unchanged.

Following are the file naming conventions that are applied while uploading assets or folders in [!DNL Experience Manager Assets]:

| Characters &Dagger; | When occurring in file names | When occurring in folder names | Example |
|---|---|---|---|
| `. / : [ ] | *` | Replaced with `-` (hyphen). | Replaced with `-` (hyphen). A `.` (dot) in the filename extension is retained as is. | Replaced with `-` (hyphen). | `myimage.jpg` remains as is and `my.image.jpg` changes to `my-image.jpg`. |
| `% ; # , + ? ^ { } "` and whitespaces | Whitespaces are retained | Replaced with `-` (hyphen). | `My Folder.` changes to `my-folder-`. |
| `# % { } ? & .` | Replaced with `-` (hyphen). | NA. | `#My New File.` changes to `-My New File-`. |
| Uppercase characters | Casing is retained as is. | Changed to lowercase characters. | `My New Folder` changes to `my-new-folder`. |
| Lppercase characters | Casing is retained as is. | Casing is retained as is. | NA. |

&Dagger; The list of characters is a whitespace-separated list.
-->

#### Programar uma importação em massa única ou recorrente {#schedule-bulk-import}

Para agendar uma importação em massa única ou recorrente, execute as seguintes etapas:

1. Criar uma configuração de importação em massa.
1. Selecione a configuração e selecione **[!UICONTROL Agendar]** na barra de ferramentas.
1. Defina uma ingestão única ou programe uma hora, uma diária ou uma programação semanal. Clique em **[!UICONTROL Enviar]**.

   ![Programar tarefa de assimilação em massa](assets/bulk-ingest-schedule1.png)


#### Exibir a pasta de destino Ativos {#view-assets-target-folder}

Selecione a configuração e clique em **[!UICONTROL Exibir ativos]** para exibir o local de destino dos Ativos, onde os ativos são importados após a execução do trabalho de Importação em massa.

#### Executar a ferramenta Importação em massa {#run-bulk-import-tool}

Depois [configuração da ferramenta Importação em massa](#configure-bulk-ingestor-tool) e opcionalmente [gerenciamento da configuração da ferramenta Importação em massa](#manage-bulk-import-configuration), é possível executar o trabalho de configuração para iniciar a assimilação em massa de ativos.

Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Importação em massa]**, selecione o [Configuração de importação em massa](#configure-bulk-ingestor-tool) e clique em **[!UICONTROL Executar]** para iniciar o processo de importação em massa. Clique em **[!UICONTROL Executar]** novamente para confirmar.

O Experience Manager atualiza o status da tarefa para **Processamento** e **Bem-sucedido** após a conclusão bem-sucedida do trabalho. Clique em **Exibir ativos** para exibir os ativos importados no Experience Manager.

Quando a tarefa estiver em andamento, você também poderá selecionar a configuração e clicar em **Stop** para interromper o processo de ingestão em massa. Clique em **Executar** novamente para retomar o processo. Você também pode clicar em **Execução de prática** para saber os detalhes dos ativos que ainda estão pendentes de importação.

#### Gerenciar trabalhos após a execução {#manage-jobs-after-execution}

O Experience Manager permite visualizar o histórico dos trabalhos de importação em massa. O Histórico de tarefas inclui o status da tarefa, o criador de trabalhos, os logs, juntamente com outros detalhes como a data e hora de início, a data e a hora de criação e a data e hora de término.

Para acessar o histórico de tarefas de uma configuração, selecione a configuração e clique em **[!UICONTROL Histórico de tarefas]**. Selecione um trabalho e clique em **Abrir**.

![Programar tarefa de assimilação em massa](assets/job-history-bulk-import.png)

Experience Manager exibe o histórico de tarefas. Na página Histórico do trabalho de importação em massa , você também pode clicar em **Excluir** para excluir esse trabalho para a configuração de importação em massa.


## Fazer upload de ativos usando clientes do desktop {#upload-assets-desktop-clients}

Além da interface do usuário do navegador da Web, [!DNL Experience Manager] O suporta outros clientes no desktop. Eles também fornecem experiência de upload sem a necessidade de acessar o navegador da Web.

* [[!DNL Adobe Asset Link]](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) fornece acesso a ativos do [!DNL Experience Manager] nos aplicativos de desktop do Adobe Photoshop, Adobe Illustrator e Adobe InDesign. Você pode fazer upload do documento aberto no momento para [!DNL Experience Manager] diretamente da interface do usuário do Adobe Asset Link a partir desses aplicativos de desktop.
* [[!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) O simplifica o trabalho com ativos no desktop, independentemente do tipo de arquivo ou do aplicativo nativo que os manipula. É particularmente útil fazer upload de arquivos nas hierarquias de pastas aninhadas do seu sistema de arquivos local, pois o upload do navegador suporta apenas o upload de listas de arquivos simples.

## Processar ativos ao fazer upload {#process-when-uploaded}

Para fazer processamento adicional nos ativos carregados, você pode aplicar perfis de processamento nas pastas de upload. Os perfis estão disponíveis no **[!UICONTROL Propriedades]** página de uma pasta em [!DNL Assets]. Um ativo digital sem uma extensão ou com uma extensão incorreta não é processado conforme desejado. Por exemplo, ao fazer upload desses ativos, nada acontece ou um perfil de processamento incorreto pode se aplicar ao ativo. Os usuários ainda podem armazenar os arquivos binários no DAM.

![Propriedades de uma pasta de ativos com opções para adicionar um perfil de processamento](assets/assets-folder-properties.png)

As seguintes guias estão disponíveis:

* [Perfis de metadados](metadata-profiles.md) permite aplicar propriedades de metadados padrão a ativos carregados nessa pasta.
* [Processar perfis](asset-microservices-configure-and-use.md) permite gerar mais representações do que as possíveis por padrão.

Além disso, se [!DNL Dynamic Media] estiver habilitado na implantação, as seguintes guias estarão disponíveis:

* [[!DNL Dynamic Media] Perfis de imagem](dynamic-media/image-profiles.md) permite aplicar cortes específicos (**[!UICONTROL Corte inteligente]** e corte de pixels) e configuração de nitidez para os ativos carregados.
* [[!DNL Dynamic Media] Perfis de vídeo](dynamic-media/video-profiles.md) permite aplicar perfis de codificação de vídeo específicos (resolução, formato, parâmetros).

>[!NOTE]
>
>[!DNL Dynamic Media] o corte e outras operações em ativos são não destrutivas, ou seja, as operações não alteram o original carregado. Em vez disso, fornece parâmetros para cortar ou transformar ao entregar os ativos.

Para pastas que têm um perfil de processamento atribuído, o nome do perfil aparece na miniatura na exibição de cartão. Na exibição de lista, o nome do perfil aparece na variável **[!UICONTROL Perfil de processamento]** coluna.

## Fazer upload ou assimilar ativos usando APIs {#upload-using-apis}

Detalhes técnicos das APIs e protocolo de upload, além de links para SDK de código aberto e clientes de amostra são fornecidos em [upload de ativo](developer-reference-material-apis.md#asset-upload) da referência do desenvolvedor.

## Dicas, práticas recomendadas e limitações {#tips-limitations}

* O upload binário direto é um novo método para fazer upload de ativos. Por padrão, ele é compatível com os recursos e clientes do produto, como [!DNL Experience Manager] interface do usuário, [!DNL Adobe Asset Link]e [!DNL Experience Manager] aplicativo de desktop. Qualquer código personalizado personalizado ou estendido pelas equipes técnicas do cliente deve usar as novas APIs e protocolos de upload.

* A Adobe recomenda adicionar até 1000 ativos em cada pasta em [!DNL Experience Manager Assets]. Embora seja possível adicionar mais ativos a uma pasta, é possível que você tenha problemas de desempenho, como navegação mais lenta para essas pastas.

* Ao selecionar **[!UICONTROL Substituir]** no [!UICONTROL Conflito de nome] , a ID do ativo é gerada novamente para o novo ativo. Essa ID é diferente da ID do ativo anterior. If [Insights de ativos](/help/assets/assets-insights.md) está ativado para rastrear impressões ou cliques com [!DNL Adobe Analytics], a ID de ativo regenerada invalida os dados capturados para o ativo em [!DNL Analytics].

* Alguns métodos de upload não impedem o upload de ativos com [caracteres proibidos](#filename-handling) nos nomes dos arquivos. Os caracteres são substituídos por `-` símbolo.

* O upload de ativos usando o navegador só oferece suporte a listas de arquivos simples e não a hierarquias de pastas aninhadas. Para fazer upload de todos os ativos dentro da pasta aninhada, considere usar [aplicativo de desktop](#upload-assets-desktop-clients).

* O método de importação em massa importa toda a estrutura de pastas como ela existe na fonte de dados. No entanto, somente as pastas que não estão vazias são criadas em [!DNL Experience Manager].


<!-- TBD: Link to file name handling in DA docs when it is documented. 
-->

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* Aplicativo de desktop do [[!DNL Adobe Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=pt-BR)
>* [Sobre [!DNL Adobe Asset Link]](https://www.adobe.com/br/creativecloud/business/enterprise/adobe-asset-link.html)
>* [[!DNL Adobe Asset Link] documentação](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)
>* [Referência técnica para upload de ativos](developer-reference-material-apis.md#asset-upload)

