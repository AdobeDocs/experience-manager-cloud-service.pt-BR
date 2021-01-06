---
title: Use o Connected Assets para compartilhar ativos do DAM no [!DNL Sites]
description: Use ativos disponíveis em uma implantação remota [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] .
contentOwner: AG
translation-type: tm+mt
source-git-commit: f548a4eecbd2a7c6bad2a848ce493c2dcff3f248
workflow-type: tm+mt
source-wordcount: '2704'
ht-degree: 28%

---


# Use o Connected Assets para compartilhar ativos do DAM no [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Em grandes empresa, a infraestrutura necessária para criar sites pode ser distribuída. Às vezes, os recursos de criação de sites e os ativos digitais usados para criar esses sites podem residir em diferentes implantações. Um motivo pode ser a distribuição geográfica de implantações existentes necessárias para trabalhar em conjunto. Outra razão pode ser as aquisições que levam a uma infraestrutura heterogênea que a empresa pai quer usar em conjunto.

Os usuários podem criar páginas da Web em [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] é o sistema de Gerenciamento de ativos digitais (DAM) que fornece os ativos necessários para sites. [!DNL Experience Manager] agora suporta o caso de uso acima, integrando  [!DNL Sites] e  [!DNL Assets].

## Visão geral do Connected Assets {#overview-of-connected-assets}

Ao editar páginas no [!UICONTROL Editor de páginas] como destino do público alvo, os autores podem pesquisar, navegar e incorporar facilmente ativos de uma implantação [!DNL Assets] diferente que atua como uma fonte de ativos. Os administradores criam uma integração única de uma implantação de [!DNL Experience Manager] com o recurso [!DNL Sites] com outra implantação de [!DNL Experience Manager] com o recurso [!DNL Assets].

Para os autores [!DNL Sites], os ativos remotos estão disponíveis como ativos locais somente leitura. A funcionalidade suporta pesquisa e uso ininterruptos de alguns ativos remotos de cada vez. Para disponibilizar muitos ativos remotos em uma implantação [!DNL Sites] de uma só vez, considere migrar os ativos em massa.

### Pré-requisitos e implantações compatíveis {#prerequisites}

Antes de usar ou configurar esse recurso, verifique o seguinte:

* Os usuários fazem parte dos grupos de usuários apropriados em cada implantação.
* Para [!DNL Adobe Experience Manager] tipos de implantação, um dos critérios suportados é atendido. Para obter mais informações sobre como essa funcionalidade funciona em [!DNL Experience Manager] 6.5, consulte [Ativos conectados no Experience Manager 6.5 Assets](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] como uma  [!DNL Cloud Service] | [!DNL Experience Manager] 6.5  [!DNL Sites] no AMS | [!DNL Experience Manager] 6.5  [!DNL Sites] local |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]como uma[!DNL Cloud Service]** | Compatível | Compatível | Compatível |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] no AMS** | Compatível | Compatível | Compatível |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] local** | Incompatível | Incompatível | Incompatível |

### Formatos de arquivo não suportados {#mimetypes}

Os autores pesquisam por imagens e pelos seguintes tipos de documentos no Localizador de conteúdo e usam os ativos pesquisados no Editor de páginas. Documentos são adicionados ao componente `Download` e às imagens no componente `Image`. Os autores também adicionam os ativos remotos em qualquer componente [!DNL Experience Manager] personalizado que estende os componentes padrão `Download` ou `Image`. Os formatos suportados são:

* **Formatos** de imagem: Os formatos suportados pelo componente  [Imagem ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) . [!DNL Dynamic Media] as imagens não são compatíveis.
* **Formatos** de documento: Consulte os formatos [ de documento ](file-format-support.md#document-formats)suportados.

### Usuários e grupos envolvidos {#users-and-groups-involved}

As várias funções envolvidas para configurar e usar o recurso e seus grupos de usuários correspondentes são descritas abaixo. O escopo local é usado para o caso de uso em que um autor cria uma página da Web. O escopo remoto é usado para a implantação do DAM. O autor [!DNL Sites] busca esses ativos remotos.

| Função | Escopo | Grupo de usuários | Nome do usuário na apresentação | Requisito |
|------|--------|-----------|-----|----------|
| [!DNL Sites] administrador | Local | [!DNL Experience Manager] `administrators` | `admin` | Configure [!DNL Experience Manager] e configure a integração com a implantação remota [!DNL Assets]. |
| Usuário do DAM | Local | `Authors` | `ksaner` | Usado para exibir e duplicar os ativos pesquisados em `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Local | <ul><li>`Authors` (com acesso de leitura no DAM remoto e acesso de autor no local  [!DNL Sites]) </li> <li>`dam-users` no local  [!DNL Sites]</li></ul> | `ksaner` | Os usuários finais são [!DNL Sites] autores que usam essa integração para melhorar sua velocidade de conteúdo. Os autores pesquisam e navegam por ativos no DAM remoto usando [!UICONTROL Localizador de conteúdo] e usando as imagens necessárias em páginas da Web locais. As credenciais do usuário do DAM `ksaner` são usadas. |
| [!DNL Assets] administrador | Remoto | [!DNL Experience Manager] `administrators` | `admin` em remoto  [!DNL Experience Manager] | Configure o CORS (Cross-Origin Resource Sharing). |
| Usuário do DAM | Remoto | `Authors` | `ksaner` em remoto  [!DNL Experience Manager] | Função de autor na implantação remota [!DNL Experience Manager]. Pesquise e procure ativos em Ativos conectados usando o [!UICONTROL Localizador de conteúdo]. |
| Distribuidor do DAM (usuário técnico) | Remoto | <ul> <li> [!DNL Sites] `Authors`</li> <li> `connectedassets-assets-techaccts` </li> </ul> | `ksaner` em remoto  [!DNL Experience Manager] | Este usuário presente na implantação remota é usado pelo [!DNL Experience Manager] servidor local (não pela função de autor [!DNL Sites]) para buscar os ativos remotos, em nome do autor [!DNL Sites]. Essa função não é igual às duas funções `ksaner` acima e pertence a um grupo de usuários diferente. |
| [!DNL Sites] utilizador técnico | Local | `connectedassets-sites-techaccts` | - | Permite que a implantação [!DNL Assets] procure referências a ativos nas páginas da Web [!DNL Sites]. |

## Configurar uma conexão entre [!DNL Sites] e [!DNL Assets] implantações {#configure-a-connection-between-sites-and-assets-deployments}

Um administrador [!DNL Experience Manager] pode criar essa integração. Depois de criadas, as permissões necessárias para usá-las são estabelecidas por meio de grupos de usuários. Os grupos de usuários são definidos na implantação [!DNL Sites] e na implantação do DAM.

Para configurar os ativos conectados e a conectividade [!DNL Sites] local, siga estas etapas:

1. Acesse uma implantação [!DNL Sites] existente. Essa implantação [!DNL Sites] é usada para criação de página da Web, por exemplo, em `https://[sites_servername]:port`. Conforme a criação de página ocorre na implantação [!DNL Sites], vamos chamar a implantação [!DNL Sites] como local da perspectiva de criação de página.

1. Acesse uma implantação [!DNL Assets] existente. Essa implantação [!DNL Assets] é usada para gerenciar ativos digitais, por exemplo, em `https://[assets_servername]:port`.

1. Verifique se os usuários e as funções com o escopo apropriado existem na implantação [!DNL Sites] e na implantação [!DNL Assets] no AMS. Crie um usuário técnico na implantação [!DNL Assets] e adicione-o ao grupo de usuários mencionado em [usuários e grupos envolvidos](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Acesse a implantação local [!DNL Sites] em `https://[sites_servername]:port`. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Configuração de ativos conectados]**. Forneça os seguintes valores:

   1. Um **[!UICONTROL Título]** da configuração.
   1. **[!UICONTROL O]** URL do DAM remoto é o URL do  [!DNL Assets] local no formato  `https://[assets_servername]:[port]`.
   1. Credenciais de um distribuidor do DAM (usuário técnico).
   1. No campo **[!UICONTROL Ponto de montagem]**, digite o caminho local [!DNL Experience Manager] onde [!DNL Experience Manager] busca os ativos. Por exemplo, pasta `connectedassets`. Os ativos obtidos do DAM são armazenados nesta pasta na implantação [!DNL Sites].
   1. **[!UICONTROL O]** URL dos sites locais é o local da  [!DNL Sites] implantação. [!DNL Assets] a implantação usa esse valor para manter referências aos ativos digitais obtidos por essa  [!DNL Sites] implantação.
   1. Credenciais de [!DNL Sites] usuário técnico.
   1. O valor do campo Limite de otimização de transferência binária original **[!UICONTROL especifica se os ativos originais (incluindo as representações) são transferidos sincronicamente ou não.]** Os ativos com tamanho de arquivo menor podem ser buscados prontamente, enquanto os ativos com tamanho de arquivo relativamente maior são sincronizados de forma assíncrona. O valor depende dos recursos de sua rede.
   1. Selecione **[!UICONTROL Datastore compartilhado com o Connected Assets]**, se você usar um datastore para armazenar seus ativos e se o Datastore for o armazenamento comum entre as duas implantações do Nesse caso, o limite não importa, pois os binários de ativos reais estão disponíveis no armazenamento de dados e não são transferidos.

   ![Uma configuração típica para a funcionalidade Ativos conectados](assets/connected-assets-typical-config.png)

   *Figura: Uma configuração típica para a funcionalidade Ativos conectados.*

1. Os ativos digitais existentes na implantação [!DNL Assets] já foram processados e as execuções são geradas. Eles são buscados usando essa funcionalidade, de modo que não há necessidade de regenerar as execuções. Desative os iniciadores do fluxo de trabalho para impedir a regeneração de execuções. Ajuste as configurações do iniciador na implantação ([!DNL Sites]) para excluir a pasta `connectedassets` (os ativos são buscados nessa pasta).

   1. Na implantação [!DNL Sites], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Iniciadores]**.

   1. Procure Iniciadores com fluxos de trabalho como **[!UICONTROL Ativo de atualização do DAM]** e **[!UICONTROL Writeback de metadados do DAM]**.

   1. Selecione o iniciador do fluxo de trabalho e clique em **[!UICONTROL Propriedades]** na barra de ações.

   1. No assistente [!UICONTROL Propriedades], altere os campos **[!UICONTROL Caminho]** como os seguintes mapeamentos para atualizar suas expressões regulares para excluir o ponto de montagem **[!UICONTROL connectedassets]**.

   | Antes | Depois |
   | ------------------------------------------------------- | -------------------------------------------------------------------------- |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Todas as representações disponíveis na implantação remota do são buscadas, quando os autores buscam um ativo. Se você quiser criar mais representações de um ativo buscado, pule esta etapa de configuração. O fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] é acionado e cria mais execuções. Essas execuções estão disponíveis somente na implantação local [!DNL Sites] e não na implantação remota do DAM.

1. Adicione a implantação [!DNL Sites] como uma origem permitida na configuração do CORS na implantação [!DNL Assets]. Para obter mais informações, consulte [compreender CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

Você pode verificar a conectividade entre as implantações [!DNL Sites] configuradas e a implantação [!DNL Assets].

![Teste de conexão dos ativos conectados configurados  [!DNL Sites]](assets/connected-assets-multiple-config.png)

<!-- TBD: Check if Launchers are to be disabled on CS instances. Is this option even available to the users on CS? -->

## Use ativos remotos {#use-remote-assets}

Os autores do site usam o Localizador de conteúdo para se conectar à implantação do DAM. Os autores podem procurar, buscar e arrastar os ativos remotos em um componente. Para autenticar no DAM remoto, mantenha acessíveis as credenciais do usuário do DAM fornecidas pelo administrador.

Os autores podem usar os ativos disponíveis no DAM local e a implantação remota do DAM, em uma única página da Web. Use o Localizador de conteúdo para alternar entre a pesquisa no DAM local ou a pesquisa no DAM remoto.

Somente as tags de ativos remotos que têm uma tag correspondente exata junto com a mesma hierarquia de taxonomia, estão disponíveis na implantação local [!DNL Sites]. Quaisquer outras tags são descartadas. Os autores podem pesquisar ativos remotos usando todas as tags presentes na implantação remota [!DNL Experience Manager], pois oferta uma pesquisa de texto completo.

### Apresentação do uso {#walk-through-of-usage}

Use a configuração acima para ter uma experiência de criação a fim de entender a funcionalidade. Use documentos ou imagens de sua escolha na implantação remota do DAM.

1. Navegue até a interface [!DNL Assets] na implantação remota acessando **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]** da área de trabalho [!DNL Experience Manager]. Como alternativa, acesse `https://[assets_servername_ams]:[port]/assets.html/content/dam` em um navegador. Carregue os ativos de sua escolha.
1. Na implantação [!DNL Sites], no ativador do perfil, no canto superior direito, clique em **[!UICONTROL Representar como]**. Forneça `ksaner` como nome de usuário, selecione a opção fornecida e clique em **[!UICONTROL OK]**.
1. Abra uma página do site We.Retail em **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL br]** > **[!UICONTROL pt]**. Edite a página. Como alternativa, acesse `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` em um navegador para editar uma página.

   Clique em **[!UICONTROL Alternar painel lateral]** no canto superior esquerdo da página.

1. Abra a guia [!UICONTROL Ativos] e clique em **[!UICONTROL Efetue logon nos Ativos conectados]**.
1. Forneça as credenciais - `ksaner` como nome de usuário e `password` como senha. Este usuário tem permissões de criação nas implantações [!DNL Experience Manager].
1. Procure o ativo que você adicionou ao DAM. Os ativos remotos são exibidos no painel esquerdo. Filtre por imagens ou documentos e filtre também por tipos de documentos compatíveis. Arraste as imagens em um componente `Image` e os documentos em um componente `Download`.

   Os ativos obtidos são somente leitura na implantação local [!DNL Sites]. Você ainda pode usar as opções fornecidas pelos componentes [!DNL Sites] para editar o ativo obtido. A edição por componentes não é destrutiva.

   ![Opções para filtrar tipos de documentos e imagens ao pesquisar ativos no DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opções para filtrar tipos de documentos e imagens ao pesquisar ativos no DAM remoto.*

1. Um autor do site será notificado se ocorrer uma busca assíncrona de ativo e uma falha na tarefa de busca. Durante a criação ou mesmo após a criação, os autores podem ver informações detalhadas sobre tarefas de busca e erros na interface do usuário [trabalhos assíncronos](/help/operations/asynchronous-jobs.md).

   ![Notificação sobre a busca assíncrona de ativos que ocorre em segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: notificação sobre a busca assíncrona de ativos que ocorre em segundo plano.*

1. Ao publicar uma página, [!DNL Experience Manager] exibe uma lista completa de ativos que são usados na página. Verifique se os ativos remotos foram buscados com êxito no momento da publicação. Para verificar o status de cada ativo buscado, consulte [tarefas assíncronas](/help/operations/asynchronous-jobs.md) a interface do usuário.

   >[!NOTE]
   >
   >Mesmo se um ou mais ativos remotos não forem buscados, a página será publicada. O componente que usa o ativo remoto é publicado vazio. A área de notificação [!DNL Experience Manager] exibe uma notificação para erros que são exibidos na página de trabalhos assíncronos.

>[!CAUTION]
>
>Depois de usados em uma página da Web, os ativos remotos obtidos são pesquisáveis e utilizáveis por qualquer pessoa que tenha permissões para acessar a pasta local. Os ativos buscados são armazenados na pasta local (`connectedassets` na caminhada acima). Os ativos também podem ser pesquisados e visualizados no repositório local por meio do [!UICONTROL Localizador de conteúdo].

Os ativos buscados podem ser usados como qualquer outro ativo local, exceto se os metadados associados não puderem ser editados.

### Verificar o uso de um ativo nas páginas da Web {#asset-usage-references}

[!DNL Experience Manager] permite que os usuários do DAM verifiquem todas as referências a um ativo. Ele ajuda a entender e gerenciar o uso de um ativo em [!DNL Sites] remoto e em ativos compostos. Muitos autores de páginas da Web em [!DNL Experience Manager Sites] implantação podem usar um ativo em [!DNL Assets] remoto em diferentes páginas da Web. Para simplificar o gerenciamento de ativos e não levar a referências quebradas, é importante que os usuários do DAM verifiquem o uso de um ativo em páginas da Web locais e remotas. A guia [!UICONTROL Referências] na página [!UICONTROL Propriedades] de um ativo lista as referências locais e remotas do ativo.

Para visualização e gerenciamento de referências na implantação [!DNL Assets], siga estas etapas:

1. Selecione um ativo no console [!DNL Assets] e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Clique na guia **[!UICONTROL Referências]**. Consulte **[!UICONTROL Referências locais]** para usar o ativo na implantação [!DNL Assets]. Consulte **[!UICONTROL Referências Remotas] para usar o ativo na implantação [!DNL Sites] na qual o ativo foi obtido usando a funcionalidade Ativos Conectados.

   ![referências remotas nas Propriedades do ativo](assets/connected-assets-remote-reference.png)

1. As referências para [!DNL Sites] páginas exibem a contagem total de referências para cada [!DNL Sites] local. Pode levar algum tempo para encontrar todas as referências e exibir o número total de referências.
1. A lista de referências é interativa e os usuários do DAM podem clicar em uma referência para abrir a página de referência. Se referências remotas não puderem ser buscadas por algum motivo, uma notificação será exibida informando o usuário da falha.
1. Os usuários podem mover ou excluir o ativo. Ao mover ou excluir um ativo, o número total de referências de todos os ativos/pastas selecionados é exibido em uma caixa de diálogo de aviso. Ao excluir um ativo para o qual as referências ainda não são exibidas, uma caixa de diálogo de aviso é exibida.

   ![forçar aviso de exclusão](assets/delete-referenced-asset.png)

## Limitações e práticas recomendadas {#tip-and-limitations}

* Para obter insights sobre o uso de ativos, configure a funcionalidade [Asset Insight](/help/assets/assets-insights.md) na instância [!DNL Sites].

### Permissões e gerenciamento de ativos {#permissions-and-managing-assets}

* Os ativos locais não são sincronizados com os ativos originais na implantação remota. As edições, exclusões ou revogação de permissões na implantação do DAM não são propagadas para a jusante.
* Os ativos locais são cópias somente leitura. [!DNL Experience Manager]Os componentes do fazem edições não destrutivas nos ativos. Nenhuma outra edição é permitida.
* Os ativos buscados localmente estão disponíveis apenas para fins de criação. Os fluxos de trabalho de atualização de ativos não podem ser aplicados e os metadados não podem ser editados.
* Somente as imagens e os formatos de documento listados são compatíveis. [!DNL Dynamic Media] ativos, Fragmentos de conteúdo e Fragmentos de experiência não são suportados.
* [!DNL Experience Manager] não busca os schemas de metadados. Isso significa que nem todos os metadados obtidos podem ser exibidos. Se o schema for atualizado separadamente, todas as propriedades serão exibidas.
* Todos os autores [!DNL Sites] têm permissões de leitura nas cópias buscadas, mesmo que os autores não possam acessar a implantação remota do DAM.
* Não há suporte de API para personalizar a integração.
* A funcionalidade suporta pesquisa e uso ininterruptos de ativos remotos. Para disponibilizar muitos ativos remotos em uma só implantação local, você pode migrar os ativos.
* Não é possível usar um ativo remoto como uma miniatura de página na interface do usuário [!UICONTROL Propriedades da página]. Você pode definir uma miniatura de uma página da Web na interface do usuário [!UICONTROL Propriedades da página] a partir da [!UICONTROL Miniatura] clicando em [!UICONTROL Selecionar imagem].

### Configuração e licenciamento {#setup-licensing}

* [!DNL Assets] a implantação em  [!DNL Adobe Managed Services] é suportada.
* [!DNL Sites] pode se conectar a um único  [!DNL Assets] repositório de cada vez.
* Uma licença de [!DNL Assets] funcionando como repositório remoto.
* Uma ou mais licenças de [!DNL Sites] trabalhando como implantação de criação local.

### Uso {#usage}

* Os usuários podem pesquisar ativos remotos e arrastá-los na página local durante a criação. Nenhuma outra funcionalidade é suportada.
* A operação de busca expira após 5 segundos. Os autores podem ter problemas ao buscar ativos, digamos se houver problemas de rede. Os autores podem tentar novamente arrastando o ativo remoto de [!UICONTROL Localizador de conteúdo] para [!UICONTROL Editor de páginas].
* Edições simples que não são destrutivas e a edição compatível por meio do componente `Image` do podem ser realizadas nos ativos buscados. Os ativos são somente leitura.
* O único método para recuperar o ativo é arrastá-lo para uma página. Não há suporte a API ou outros métodos para recuperar um ativo para atualizá-lo.
* Se os ativos forem descontinuados do DAM, eles continuarão a ser usados nas páginas [!DNL Sites].
* As entradas de referência remota de um ativo são buscadas de forma assíncrona. As referências e a contagem total não são em tempo real e pode haver alguma diferença se um autor do Sites usa o ativo enquanto um usuário do DAM está visualizando a referência. Os usuários do DAM podem atualizar a página e tentar novamente em alguns minutos para obter a contagem total.

## Solução de problemas {#troubleshoot}

Para solucionar erros comuns, siga estas etapas:

* Se você não conseguir pesquisar ativos remotos do [!UICONTROL Localizador de conteúdo], verifique se as funções e permissões necessárias estão no lugar.
* Um ativo obtido da barragem remota pode não ser publicado em uma página da Web por um ou mais motivos. Ele não existe no servidor remoto, falta de permissões apropriadas para buscá-lo ou falha na rede pode ser o motivo. Verifique se o ativo não foi removido do DAM remoto. Verifique se as permissões apropriadas estão em vigor e se os pré-requisitos foram atendidos. Tente adicionar o ativo novamente à página e publique-o novamente. Verifique a [lista de trabalhos assíncronos](/help/operations/asynchronous-jobs.md) quanto a erros na busca de ativos.
* Se você não conseguir acessar a implantação remota do DAM a partir da implantação local [!DNL Sites], verifique se os cookies entre sites são permitidos. Se os cookies entre sites estiverem bloqueados, as duas implantações de [!DNL Experience Manager] podem não ser autenticadas. Por exemplo, [!DNL Google Chrome] no modo Incognito pode bloquear cookies de terceiros. Para permitir cookies no navegador [!DNL Chrome], clique no ícone &#39;olho&#39; na barra de endereços, navegue até Site Not Working > Blocked, selecione o URL do DAM remoto e permita o cookie do token de logon. Como alternativa, consulte a ajuda sobre [como ativar cookies de terceiros](https://support.google.com/chrome/answer/95647).

   ![Erro de cookie no Chrome no modo cognito](assets/chrome-cookies-incognito-dialog.png)

* Se referências remotas não forem recuperadas e resultar em uma mensagem de erro, verifique se a implantação do Sites está disponível e verifique se há problemas de conectividade de rede. Tente novamente mais tarde para verificar. [!DNL Assets] a implantação tenta estabelecer conexão duas vezes com a  [!DNL Sites] implantação e, em seguida, informa uma falha.

![falha ao repetir referências remotas de ativos](assets/reference-report-failure.png)
