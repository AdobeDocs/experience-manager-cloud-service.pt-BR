---
title: Usar ativos conectados para compartilhar ativos DAM no [!DNL Sites]
description: Usar ativos disponíveis remotamente [!DNL Adobe Experience Manager Assets] implantação ao criar suas páginas da Web em outro [!DNL Adobe Experience Manager Sites] implantação.
contentOwner: AK
mini-toc-levels: 2
feature: Asset Management,Connected Assets,Asset Distribution,User and Groups
role: Admin,User,Architect
exl-id: 2346f72d-a383-4202-849e-c5a91634617a
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '3842'
ht-degree: 13%

---


# Usar ativos conectados para compartilhar ativos DAM no [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html) |
| AEM as a Cloud Service | Este artigo |

Em grandes empresa, a infraestrutura necessária para criar sites pode ser distribuída. Às vezes, os recursos de criação de sites e os ativos digitais usados para criar esses sites podem residir em diferentes implantações. Um motivo pode ser a distribuição geográfica de implantações existentes que são necessárias para trabalhar em conjunto. Outra razão pode ser as aquisições que conduzem a infraestruturas heterogêneas, [!DNL Experience Manager] versões, que a empresa principal deseja usar em conjunto.

A funcionalidade Connected Assets é compatível com os casos de uso acima ao integrar [!DNL Experience Manager Sites] e [!DNL Experience Manager Assets]. Os usuários podem criar páginas da Web no [!DNL Sites] que usam os ativos digitais de um [!DNL Assets] implantações.

>[!NOTE]
>
>Configure o Connected Assets somente quando precisar usar os ativos disponíveis em uma implantação remota do DAM em uma implantação separada do Sites para criação de páginas da Web.

## Visão geral do Connected Assets {#overview-of-connected-assets}

Ao editar páginas no [!UICONTROL Editor de páginas] como destino, os autores podem pesquisar, navegar e incorporar facilmente ativos de uma [!DNL Assets] implantação que atua como uma fonte de ativos. Os administradores criam uma integração única de uma implantação do [!DNL Experience Manager] com [!DNL Sites] com outra implantação do [!DNL Experience Manager] com [!DNL Assets] capacidade. Você também pode usar imagens do Dynamic Media nas páginas da Web do site por meio do Connected Assets e usar as funcionalidades do Dynamic Media, como recorte inteligente e predefinições de imagem.

Para o [!DNL Sites] autores, os ativos remotos estão disponíveis como ativos locais somente leitura. A funcionalidade suporta pesquisa e acesso ininterruptos a ativos remotos no Editor de sites. Para quaisquer outros casos de uso que possam exigir que o conjunto completo de ativos esteja disponível no Sites, considere migrar os ativos em massa em vez de usar os Ativos conectados.

### Pré-requisitos e implantações compatíveis {#prerequisites}

Antes de usar ou configurar esse recurso, verifique o seguinte:

* Os usuários fazem parte dos grupos de usuários apropriados em cada implantação.
* Para [!DNL Adobe Experience Manager] tipos de implantação, um dos critérios compatíveis é atendido. [!DNL Experience Manager] as a Cloud Service [!DNL Assets] funciona com [!DNL Experience Manager] 6.5. Para obter mais informações sobre como essa funcionalidade funciona no [!DNL Experience Manager] 6.5, consulte [Ativos conectados no [!DNL Experience Manager] 6.5 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html).

  | | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.5 [!DNL Sites] no AMS | [!DNL Experience Manager] 6.5 [!DNL Sites] no local |
  |---|---|---|---|
  | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | Compatível | Compatível | Compatível |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] no AMS** | Compatível | Compatível | Compatível |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] no local** | Incompatível | Incompatível | Incompatível |

### Formatos de arquivo não compatíveis {#mimetypes}

Os autores pesquisam imagens e os seguintes tipos de documentos no Localizador de conteúdo e arrastam os ativos pesquisados no Editor de páginas. Os documentos são adicionados ao `Download` componente e imagens para o `Image` componente. Os autores também podem adicionar os ativos remotos em qualquer [!DNL Experience Manager] componente que estende o padrão `Download` ou `Image` componentes. Os formatos compatíveis são:

* **Formatos de imagem**: os formatos que a variável [Componente de imagem](file-format-support.md#image-formats) suporta.
* **Formatos de documento**: Consulte a [formatos de documento compatíveis](file-format-support.md#document-formats).

### Usuários e grupos envolvidos {#users-and-groups-involved}

As várias funções envolvidas para configurar o recurso e seus grupos de usuários correspondentes são descritas abaixo. O escopo local é usado para o caso de uso em que um autor cria uma página da Web. O escopo remoto é usado para a implantação do DAM que hospeda os ativos necessários. A variável [!DNL Sites] O autor do busca esses ativos remotos.

| Função | Escopo | Grupo de usuários | Descrições |
|------|--------|-----------|----------|
| [!DNL Sites] administrador | Local | [!DNL Experience Manager] `administrators` | Configurar [!DNL Experience Manager] e configurar a integração com o controle remoto [!DNL Assets] implantação. |
| Usuário do DAM | Local | `Authors` | Usado para exibir e duplicar os ativos pesquisados em `/content/DAM/connectedassets/`. |
| [!DNL Sites] autor | Local | <ul><li>`Authors` (com acesso de leitura no DAM remoto e acesso de autor no local) [!DNL Sites]) </li> <li>`dam-users` no local [!DNL Sites]</li></ul> | Os usuários finais estão [!DNL Sites] autores que usam essa integração para melhorar a velocidade do conteúdo. Os autores podem pesquisar e procurar ativos no DAM remoto usando [!UICONTROL Localizador de conteúdo] e usando as imagens necessárias nas páginas da Web locais. |
| [!DNL Assets] administrador | Remoto | [!DNL Experience Manager] `administrators` | Configure o CORS (Cross-Origin Resource Sharing). |
| Usuário do DAM | Remoto | `Authors` | Função de autor no controle remoto [!DNL Experience Manager] implantação. Pesquise e procure ativos no Connected Assets usando o [!UICONTROL Localizador de conteúdo]. |
| Distribuidor do DAM (usuário técnico) | Remoto | <ul> <li> [!DNL Sites] `Authors`</li> <li> `connectedassets-assets-techaccts` </li> </ul> | Este usuário presente na implantação remota é usado por [!DNL Experience Manager] servidor local (não o [!DNL Sites] função de autor) para buscar os ativos remotos, em nome da [!DNL Sites] autor. |
| [!DNL Sites] usuário técnico | Local | `connectedassets-sites-techaccts` | Permite [!DNL Assets] implantação para pesquisar referências a ativos na [!DNL Sites] páginas da Web. |

### Arquitetura do Connected Assets {#connected-assets-architecture}

Experience Manager permite conectar uma implantação remota do DAM como uma origem a vários Experience Manager [!DNL Sites] implantações. No entanto, é possível conectar um [!DNL Sites] com apenas uma implantação remota do DAM.

Avalie o número ideal de instâncias do Sites para se conectar a uma implantação remota do DAM. O Adobe recomenda conectar de forma incremental as instâncias do Sites à implantação e testar se não há impacto no desempenho no DAM remoto, pois cada instância do Sites conectada contribui para o tráfego de dados no DAM remoto.

Os diagramas a seguir ilustram os cenários compatíveis:

![Arquitetura do Connected Assets](assets/connected-assets-architecture.png)

O diagrama a seguir ilustra um cenário incompatível:

![Arquitetura do Connected Assets](assets/connected-assets-architecture-unsupported.png)

## Configurar uma conexão entre [!DNL Sites] e [!DNL Assets] implantações {#configure-a-connection-between-sites-and-assets-deployments}

Um [!DNL Experience Manager] administrador pode criar essa integração. Depois de criadas, as permissões necessárias para usá-la são estabelecidas por meio de grupos de usuários. Os grupos de usuários são definidos no [!DNL Sites] implantação e na implantação do DAM.

Para configurar ativos conectados e locais [!DNL Sites] conectividade, siga estas etapas:

1. Acessar um existente [!DNL Sites] implantação. Este [!DNL Sites] a implantação é usada para criação de página da Web, digamos no `https://<sites_server_fqdn>:[port]`. Conforme a criação da página acontece em [!DNL Sites] implantação, vamos chamar a variável [!DNL Sites] implantação como local da perspectiva de criação da página.

1. Acessar um existente [!DNL Assets] implantação. Este [!DNL Assets] a implantação é usada para gerenciar ativos digitais, digamos no `https://[assets_servername]:port`.

1. Verifique se os usuários e as funções com o escopo apropriado existem no [!DNL Sites] implantação e no [!DNL Assets] implantação no AMS. Criar um usuário técnico em [!DNL Assets] implantação e adicionar ao grupo de usuários mencionado em [usuários e grupos envolvidos](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Acessar o local [!DNL Sites] implantação em `https://[sites_servername]:port`. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Configuração do Connected Assets]** e forneça os seguintes valores:

   1. A **[!UICONTROL Título]** da configuração.
   1. **[!UICONTROL URL do DAM remoto]** é o URL do [!DNL Assets] localização no formato `https://[assets_servername]:[port]`.
   1. Credenciais de um distribuidor do DAM (usuário técnico).
   1. No **[!UICONTROL Ponto de montagem]** insira o local [!DNL Experience Manager] caminho onde [!DNL Experience Manager] O busca os ativos. Por exemplo, `connectedassets` pasta. Os ativos buscados no DAM são armazenados nesta pasta na [!DNL Sites] implantação.
   1. **[!UICONTROL URL de sites locais]** é o local do [!DNL Sites] implantação. [!DNL Assets] A implantação do usa esse valor para manter referências aos ativos digitais buscados por este [!DNL Sites] implantação.
   1. Credenciais de [!DNL Sites] usuário técnico.
   1. O valor de **[!UICONTROL Limite binário original da otimização de transferência]** o campo especifica se os ativos originais (incluindo as representações) são transferidos de forma síncrona ou não. Ativos com tamanho de arquivo menor podem ser buscados prontamente, enquanto ativos com tamanho de arquivo relativamente maior são melhor sincronizados de forma assíncrona. O valor depende dos recursos da rede.
   1. Selecionar **[!UICONTROL Armazenamento de dados compartilhado com o Connected Assets]**, se você usar um armazenamento de dados para armazenar seus ativos e o armazenamento de dados for compartilhado entre as duas implantações. Nesse caso, o limite não importa, pois os binários de ativos reais estão disponíveis no armazenamento de dados e não são transferidos.

   ![Uma configuração típica da funcionalidade Connected Assets](assets/connected-assets-typical-config.png)

   *Figura: uma configuração normal da funcionalidade Connected Assets.*

1. Os ativos digitais existentes no [!DNL Assets] já forem processadas e as representações forem geradas. Essas representações são buscadas usando essa funcionalidade, de modo que não há necessidade de gerar novamente as representações. Desative os iniciadores do fluxo de trabalho para impedir a regeneração de representações. Ajuste as configurações do iniciador no ([!DNL Sites]) para excluir o `connectedassets` pasta (os ativos são obtidos nesta pasta).

   1. Ligado [!DNL Sites] implantação, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Iniciadores]**.

   1. Procure Iniciadores com fluxos de trabalho como **[!UICONTROL Ativo de atualização do DAM]** e **[!UICONTROL Writeback de metadados do DAM]**.

   1. Selecione o iniciador do fluxo de trabalho e clique em **[!UICONTROL Propriedades]** na barra de ações.

   1. No [!UICONTROL Propriedades] assistente, altere o **[!UICONTROL Caminho]** como os seguintes mapeamentos para atualizar suas expressões regulares para excluir o ponto de montagem **[!UICONTROL connectedassets]**.

   | Antes | Depois |
   | ------ | ------------ |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Todas as representações disponíveis na implantação remota são buscadas, quando os autores buscam um ativo. Se você quiser criar mais representações de um ativo buscado, pule esta etapa de configuração. A variável [!UICONTROL Ativo de atualização DAM] o fluxo de trabalho é acionado e cria mais representações. Essas representações estão disponíveis somente no local [!DNL Sites] e não na implantação remota do DAM.

1. Adicione o [!DNL Sites] como uma origem permitida na configuração do CORS no [!DNL Assets] implantação. Para obter mais informações, consulte [compreender o CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

1. Configurar [suporte a cookie no mesmo site](/help/security/same-site-cookie-support.md).

Você pode verificar a conectividade entre as configurações [!DNL Sites] implantações e [!DNL Assets] implantação.

![Teste de conexão do Connected Assets configurado [!DNL Sites]](assets/connected-assets-multiple-config.png)
*Figura: Teste de conexão do Connected Assets configurado [!DNL Sites].*

<!-- TBD: Check if Launchers are to be disabled on CS instances. Is this option even available to the users on CS? -->

## Usar ativos do Dynamic Media {#dynamic-media-assets}


Com o Connected Assets, você pode usar ativos de imagem processados pelo [!DNL Dynamic Media] da implantação remota do DAM em páginas do Sites, e usar funcionalidades do Dynamic Media, como predefinições de recorte inteligente e de imagem.

Para usar [!DNL Dynamic Media] com Connected Assets:

1. Configurar [!DNL Dynamic Media] na implantação remota do DAM com o modo de sincronização ativado.
1. Configurar [Connected Assets](#configure-a-connection-between-sites-and-assets-deployments).
1. Configurar [!DNL Dynamic Media] na instância do Sites com o mesmo nome de empresa configurado no DAM remoto. A implantação do Sites deve ter acesso somente leitura à conta do Dynamic Media para funcionar com ativos conectados. Portanto, desative o modo de Sincronização na configuração do Dynamic Media na instância do Sites.

>[!CAUTION]
>
>Com ativos conectados e [!DNL Dynamic Media] configuração, você não pode usar [!DNL Dynamic Media] para processar ativos locais disponíveis no [!DNL Sites] implantação.

## Configurar o [!DNL Dynamic Media] {#configure-dynamic-media}

Para configurar [!DNL Dynamic Media] em [!DNL Assets] e [!DNL Sites] implantações:

1. Crie a configuração do Connected Assets conforme descrito acima, exceto ao configurar a funcionalidade, selecione **[!UICONTROL Buscar representação original para Ativos conectados do Dynamic Media]** opção.

1. Configurar [!DNL Dynamic Media] no local [!DNL Sites] e remoto [!DNL Assets] implantações. Siga as instruções para [configurar [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

   * Use o mesmo nome de empresa em todas as configurações.
   * No local [!DNL Sites], em [!UICONTROL Modo de sincronização do Dynamic Media], selecione **[!UICONTROL Desabilitado por padrão]**. A variável [!DNL Sites] a implantação deve ter acesso somente leitura à [!DNL Dynamic Media] conta.
   * No local [!DNL Sites], no **[!UICONTROL Publicar ativos]** selecione **[!UICONTROL Publicação seletiva]**. Não selecionar **[!UICONTROL Sincronizar todo o conteúdo]**.
   * No modo remoto [!DNL Assets] implantação, em [!UICONTROL Modo de sincronização do Dynamic Media], selecione **[!UICONTROL Ativado por padrão]**.

1. Ativar [[!DNL Dynamic Media] suporte no Componente principal de imagem](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media). Esse recurso habilita o padrão [Componente de imagem](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/image.html) para exibir [!DNL Dynamic Media] imagens quando [!DNL Dynamic Media] as imagens são usadas por autores em páginas da web no local [!DNL Sites] implantação.

## Usar ativos remotos {#use-remote-assets}

Os autores do site usam o Localizador de conteúdo para se conectar à implantação do DAM. Os autores podem procurar, buscar e arrastar os ativos remotos em um componente. Para autenticar no DAM remoto, mantenha acessíveis as credenciais fornecidas pelo administrador (se houver).

Os autores podem usar os ativos disponíveis no DAM local e na implantação remota do DAM, em uma única página da Web. Use o Localizador de conteúdo para alternar entre a pesquisa no DAM local ou a pesquisa no DAM remoto.

São buscadas somente as tags de ativos remotos que têm uma tag exata correspondente junto com a mesma hierarquia de taxonomia, disponível no local [!DNL Sites] implantação. Quaisquer outras tags são descartadas. Os autores podem pesquisar ativos remotos usando todas as tags presentes no local [!DNL Experience Manager] implantação, pois oferece uma pesquisa de texto completo.

### Apresentação do uso {#walk-through-of-usage}

Use a configuração acima para ter uma experiência de criação a fim de entender a funcionalidade. Use documentos ou imagens de sua escolha na implantação remota do DAM.

1. Navegue até a [!DNL Assets] na implantação remota, acessando **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]** de [!DNL Experience Manager] espaço de trabalho. Como alternativa, acesse `https://[assets_servername_ams]:[port]/assets.html/content/dam` em um navegador. Carregue os ativos de sua escolha.

1. No [!DNL Sites] implantação, no ativador de perfil no canto superior direito, clique em **[!UICONTROL Representar como]**. Especifique o nome de usuário, selecione a opção fornecida e clique em **[!UICONTROL OK]**.

1. Abra um [!DNL Sites] e edite a página.

   Clique em **[!UICONTROL Alternar painel lateral]** no canto superior esquerdo da página.

1. Abra o [!UICONTROL Assets] (Localizador de conteúdo remoto) e clique em **[!UICONTROL Fazer logon no Connected Assets]**.

1. Especifique as credenciais para fazer logon no Connected Assets. Este usuário tem permissões de criação em [!DNL Experience Manager] implantações.

1. Procure o ativo que você adicionou ao DAM. Os ativos remotos são exibidos no painel esquerdo. Filtre por imagens ou documentos e filtre também por tipos de documentos compatíveis. Arraste as imagens em um componente `Image` e os documentos em um componente `Download`.

   Os ativos buscados são somente leitura no local [!DNL Sites] implantação. Você ainda pode usar as opções fornecidas pelo seu [!DNL Sites] componentes para editar o ativo buscado. A edição por componentes não é destrutiva.

   ![Opções para filtrar tipos de documentos e imagens ao pesquisar ativos no DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opções para filtrar tipos de documentos e imagens ao pesquisar ativos no DAM remoto.*

1. Um autor do site será notificado se a busca original de um ativo for realizada de forma assíncrona e se qualquer tarefa de busca falhar. Durante a criação ou até mesmo após a criação, os autores podem ver informações detalhadas sobre as tarefas de busca e erros no [trabalhos assíncronos](/help/operations/asynchronous-jobs.md) interface do usuário.

   ![Notificação sobre a busca assíncrona de ativos que ocorre em segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: notificação sobre a busca assíncrona de ativos que ocorre em segundo plano.*

1. Ao publicar uma página, [!DNL Experience Manager] O exibe uma lista completa dos ativos usados na página. Verifique se os ativos remotos foram buscados com êxito no momento da publicação. Para verificar o status de cada ativo buscado, consulte [trabalhos assíncronos](/help/operations/asynchronous-jobs.md) interface do usuário.

   >[!NOTE]
   >
   >Mesmo se um ou mais ativos remotos não forem buscados completamente, a página será publicada. A variável [!DNL Experience Manager] área de notificação exibe uma notificação para erros que são mostrados na página de trabalhos assíncronos.

>[!CAUTION]
>
>Uma vez usados em uma página da Web, os ativos remotos buscados podem ser pesquisados e usados por qualquer pessoa com permissões para acessar a pasta local. Os ativos buscados são armazenados na pasta local (`connectedassets` na apresentação acima). Os ativos também podem ser pesquisados e visualizados no repositório local por meio do [!UICONTROL Localizador de conteúdo].

Os ativos buscados podem ser usados como qualquer outro ativo local, exceto se os metadados associados não puderem ser editados.

### Verificar o uso de um ativo em várias páginas da Web {#asset-usage-references}

[!DNL Experience Manager] permite que os usuários do DAM verifiquem todas as referências a um ativo. Ele ajuda a entender e gerenciar o uso de um ativo no [!DNL Sites] e em ativos compostos. Muitos autores de páginas da Web no [!DNL Experience Manager Sites] A implantação do pode usar um ativo em um DAM remoto em diferentes páginas da Web. Para simplificar o gerenciamento de ativos e não resultar em referências quebradas, é importante que os usuários do DAM verifiquem o uso de um ativo em páginas da Web locais e remotas. A variável [!UICONTROL Referências] em do ativo [!UICONTROL Propriedades] A página lista as referências locais e remotas do ativo.

Para exibir e gerenciar referências no [!DNL Assets] implantação, siga estas etapas:

1. Selecione um ativo no [!DNL Assets] e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Clique em **[!UICONTROL Referências]** guia. Consulte **[!UICONTROL Referências locais]** para uso do ativo no [!DNL Assets] implantação. Consulte **[!UICONTROL Referências remotas] para uso do ativo em [!DNL Sites] implantação em que o ativo foi buscado usando a funcionalidade Connected Assets.

   ![Referências remotas na página Propriedades do ativo](assets/connected-assets-remote-reference.png)

1. As referências para [!DNL Sites] as páginas exibem a contagem total de referências para cada local [!DNL Sites]. Pode levar algum tempo para encontrar todas as referências e exibir o número total de referências.
1. A lista de referências é interativa e os usuários do DAM podem clicar em uma referência para abrir a página de referência. Se as referências remotas não puderem ser buscadas por algum motivo, uma notificação será exibida informando o usuário sobre a falha.
1. Os usuários podem mover ou excluir o ativo. Ao mover ou excluir um ativo, o número total de referências de todos os ativos/pastas selecionados é exibido em uma caixa de diálogo de aviso. Ao excluir um ativo para o qual as referências ainda não foram recuperadas, uma caixa de diálogo de aviso é exibida.

   ![aviso de forçar exclusão](assets/delete-referenced-asset.png)

### Gerenciar atualizações de ativos no DAM remoto {#handling-updates-to-remote-assets}

Depois [configuração de uma conexão](#configure-a-connection-between-sites-and-assets-deployments) entre implantações remotas do DAM e do Sites, os ativos no DAM remoto são disponibilizados na implantação do Sites. Em seguida, você pode atualizar, excluir, renomear e mover operações nos ativos ou pastas remotos do DAM. As atualizações, com algum atraso, estão disponíveis automaticamente na implantação do Sites. Além disso, se um ativo no DAM remoto for usado em uma página do Experience Manager Sites local, as atualizações do ativo no DAM remoto serão exibidas na página Sites.

Ao mover um ativo de um local para outro, verifique se [ajustar referências](manage-digital-assets.md) para que o ativo seja exibido na página Sites. Se você mover um ativo para um local que não está acessível na implantação local do Sites, o ativo não será exibido na implantação do Sites.

Também é possível atualizar as propriedades de metadados de um ativo no DAM remoto e as alterações estão disponíveis na implantação local do Sites.

Os autores do Sites podem visualizar as atualizações disponíveis na implantação do Sites e, em seguida, republicar as alterações para disponibilizá-las na instância de publicação do AEM.

Experience Manager exibe um `expired` Indicador visual de status em ativos no Localizador de conteúdo do Remote Assets para impedir que os autores de sites usem o ativo em uma página do Sites. Se você usar um ativo com um `expired` Em uma página do Sites, o ativo não é exibido na instância de publicação do Experience Manager.

## Perguntas frequentes {#frequently-asked-questions}

+++**Você deve configurar o Connected Assets se precisar usar os ativos disponíveis no [!DNL Sites] implantação?**

Não há necessidade de configurar o Connected Assets nesse caso. Você pode usar os ativos disponíveis no [!DNL Sites] implantação.

+++

+++**Quando você precisa configurar o recurso Connected Assets?**

Configure o recurso Ativos conectados somente quando precisar usar os ativos disponíveis em uma implantação remota do DAM em um [!DNL Sites] implantação.

+++

+++**É possível conectar vários [!DNL Sites] implantações em uma implantação remota do DAM após configurar o Connected Assets?**

Sim, você pode conectar vários [!DNL Sites] implantações em uma implantação remota do DAM após configurar o Connected Assets. Para obter mais informações, consulte [Arquitetura do Connected Assets](#connected-assets-architecture).

+++

+++**Quantas implantações remotas do DAM você pode conectar a um [!DNL Sites] implantação após configurar o Connected Assets?**

É possível conectar uma implantação remota do DAM a um [!DNL Sites] implantação após configurar o Connected Assets. Para obter mais informações, consulte [Arquitetura do Connected Assets](#connected-assets-architecture).

+++

+++**Você pode usar os ativos da Dynamic Media de seu [!DNL Sites] implantação após configurar o Connected Assets?**

Depois de configurar o Connected Assets, [!DNL Dynamic Media] os ativos estão disponíveis em [!DNL Sites] implantação em um modo somente leitura. Como resultado, não é possível usar [!DNL Dynamic Media] para processar ativos no [!DNL Sites] implantação. Para obter mais informações, consulte [Configure uma conexão entre implantações do Sites e do Dynamic Media](#dynamic-media-assets).

+++

+++**Você pode usar ativos dos tipos de formato Imagem e Documento da implantação remota do DAM no [!DNL Sites] implantação após configurar o Connected Assets?**

Sim, você pode usar ativos dos tipos de formato Imagem e Documento da implantação remota do DAM no [!DNL Sites] implantação após configurar o Connected Assets.

+++

+++**É possível usar fragmentos de conteúdo e ativos de vídeo da implantação remota do DAM no [!DNL Sites] implantação após configurar o Connected Assets?**

Não, não é possível usar fragmentos de conteúdo e ativos de vídeo da implantação remota do DAM no [!DNL Sites] implantação após configurar o Connected Assets.

+++

+++**Você pode usar os ativos do Dynamic Media da implantação remota do DAM no [!DNL Sites] implantação após configurar o Connected Assets?**

Sim, você pode configurar e usar os ativos de imagem do Dynamic Media a partir da implantação remota do DAM no [!DNL Sites] implantação após configurar o Connected Assets. Para obter mais informações, consulte [Configure uma conexão entre implantações do Sites e do Dynamic Media](#dynamic-media-assets).

+++

+++**Após configurar os Ativos conectados, você pode executar as operações atualizar, excluir, renomear e mover nos ativos ou pastas remotos do DAM?**

Sim, após configurar o Connected Assets, você pode executar as operações atualizar, excluir, renomear e mover nos ativos ou pastas remotos do DAM. As atualizações, com algum atraso, estão disponíveis automaticamente na implantação do Sites. Para obter mais informações, consulte [Gerenciar atualizações de ativos no DAM remoto](#handling-updates-to-remote-assets).

+++

+++**Após configurar os Ativos conectados, você pode adicionar ou modificar ativos em sua [!DNL Sites] e disponibilizá-los na implantação remota do DAM?**

É possível adicionar ativos à [!DNL Sites] no entanto, esses ativos não podem ser disponibilizados para a implantação remota do DAM.

+++


## Limitações e práticas recomendadas {#tip-and-limitations}

* Para obter insights sobre o uso do ativo, configure o [Assets Insight](/help/assets/assets-insights.md) funcionalidade no [!DNL Sites] instância.
* O uso do navegador de caminho nos componentes de criação não é compatível com os ativos conectados.

* Não é possível arrastar o ativo remoto para a [Caixa de diálogo Configurar componente de imagem](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=en#configure-dialog). No entanto, é possível arrastar o ativo remoto diretamente para o componente de imagem na página Sites sem clicar em **[!UICONTROL Configurar]**.

### Permissões e gerenciamento de ativos {#permissions-and-managing-assets}

* Os ativos locais são cópias somente leitura. [!DNL Experience Manager] os componentes fazem edições não destrutivas nos ativos. Nenhuma outra edição é permitida.
* Os ativos buscados localmente estão disponíveis apenas para fins de criação. Os fluxos de trabalho de atualização de ativos não podem ser aplicados e os metadados não podem ser editados.
* Ao usar [!DNL Dynamic Media] in [!DNL Sites] páginas, o ativo original não é buscado e armazenado na implantação local. A variável `dam:Asset` nó, os metadados e as representações geradas pelo [!DNL Assets] implantação são todas buscadas no [!DNL Sites] implantação.
* Somente as imagens e os formatos de documento listados são compatíveis. [!DNL Content Fragments] e [!DNL Experience Fragments] não são compatíveis.
* [!DNL Experience Manager] O não busca os esquemas de metadados. Isso significa que todos os metadados buscados podem não ser exibidos. Se o schema for atualizado separadamente no [!DNL Sites] implantação, todas as propriedades de metadados serão exibidas.
* Todos [!DNL Sites] os autores têm permissões de leitura nas cópias buscadas, mesmo que os autores não possam acessar a implantação remota do DAM.
* Não há suporte de API para personalizar a integração.
* A funcionalidade suporta pesquisa e uso ininterruptos de ativos remotos. Para disponibilizar muitos ativos remotos em uma só implantação local, você pode migrar os ativos.
* Não é possível usar um ativo remoto como miniatura de página no [!UICONTROL Propriedades da página] interface do usuário. É possível definir uma miniatura de uma página da Web no [!UICONTROL Propriedades da página] a interface do usuário do [!UICONTROL Miniatura] clicando em [!UICONTROL Selecionar imagem].

### Configuração e licenciamento {#setup-licensing}

* [!DNL Assets] implantação em [!DNL Adobe Managed Services] é compatível.
* [!DNL Sites] pode se conectar a um único [!DNL Assets] de cada vez.
* Uma licença de [!DNL Assets] é necessário trabalhar como repositório remoto.
* Uma ou mais licenças de [!DNL Sites] é necessário trabalhar como implantação de criação local.

### Uso {#usage}

* Os usuários podem pesquisar ativos remotos e arrastá-los na página local durante a criação. Nenhuma outra funcionalidade é suportada.
* A operação de busca expira após 5 segundos. Os autores podem ter problemas ao buscar ativos, digamos se houver problemas de rede. Os autores podem tentar novamente, arrastando o ativo remoto de [!UICONTROL Localizador de conteúdo] para [!UICONTROL Editor de páginas].
* Edições simples que não são destrutivas e a edição compatível por meio do `Image` componente, pode ser feito em ativos buscados. Os ativos são somente leitura.
* O único método para buscar novamente o ativo é arrastá-lo em uma página. Não há suporte para API ou outros métodos para buscar novamente um ativo e atualizá-lo.
* Se os ativos forem desativados do DAM, continuarão em uso em [!DNL Sites] páginas.
* As entradas de referência remota de um ativo são buscadas de forma assíncrona. As referências e a contagem total não estão em tempo real e pode haver alguma diferença se um [!DNL Sites] O autor do usa o ativo enquanto um usuário do DAM visualiza a referência. Os usuários do DAM podem atualizar a página e tentar novamente em alguns minutos para obter a contagem total.

## Solução de problemas {#troubleshoot}

Para solucionar erros comuns, siga estas etapas:

* Se não conseguir pesquisar ativos remotos no [!UICONTROL Localizador de conteúdo], em seguida, verifique se as funções e permissões necessárias estão em vigor.

* Um ativo buscado no DAM remoto não pode ser publicado em uma página da Web por um ou mais motivos. Ele não existe no servidor remoto, a falta de permissões apropriadas para buscá-lo ou uma falha de rede podem ser os motivos. Verifique se o ativo não foi removido do DAM remoto. Verifique se as permissões apropriadas estão em vigor e se os pré-requisitos foram atendidos. Tente adicionar o ativo novamente à página e publique-o novamente. Verifique a [lista de trabalhos assíncronos](/help/operations/asynchronous-jobs.md) quanto a erros na busca de ativos.

* Se não conseguir acessar a implantação remota do DAM a partir do local [!DNL Sites] garantir que os cookies entre sites sejam permitidos e [suporte a cookie no mesmo site](/help/security/same-site-cookie-support.md) está configurado. Se os cookies entre sites estiverem bloqueados, as implantações do [!DNL Experience Manager] não pode autenticar. Por exemplo, [!DNL Google Chrome] no modo Incógnito pode bloquear cookies de terceiros. Para permitir cookies no [!DNL Chrome] navegador, clique no ícone &quot;olho&quot; na barra de endereços e navegue até **Site não funciona** > **Bloqueado**, selecione o URL do DAM remoto e permita o cookie de token de logon. Como alternativa, consulte [como ativar cookies de terceiros](https://support.google.com/chrome/answer/95647).

  ![Erro de cookie no navegador Chrome no modo Incógnito](assets/chrome-cookies-incognito-dialog.png)

* Se as referências remotas não forem recuperadas e resultarem em uma mensagem de erro, verifique se [!DNL Sites] a implantação está disponível e verifique se há problemas de conectividade de rede. Tente novamente mais tarde para verificar. [!DNL Assets] A implantação do tenta estabelecer duas vezes a conexão com o [!DNL Sites] e, em seguida, relata uma falha.

  ![falha ao recuperar referências remotas de ativos](assets/reference-report-failure.png)

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar ativos no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
