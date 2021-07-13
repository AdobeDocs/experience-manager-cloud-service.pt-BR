---
title: Configurar o Dynamic Media Cloud Service
description: Saiba como configurar o Dynamic Media no Adobe Experience Manager as a Cloud Service.
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 6933f053e11320d8201922723879983084c52209
workflow-type: tm+mt
source-wordcount: '4057'
ht-degree: 4%

---

# Sobre a configuração do Dynamic Media Cloud Service {#configuring-dynamic-media}

Se você usar o Adobe Experience Manager para ambientes diferentes, como desenvolvimento, armazenamento temporário e produção ao vivo, configure o Dynamic Media Cloud Services para cada um desses ambientes.

## Diagrama de arquitetura do Dynamic Media {#architecture-diagram-of-dynamic-media}

O diagrama de arquitetura a seguir descreve como o Dynamic Media funciona.

Com a nova arquitetura, o Experience Manager é responsável pelos ativos e sincronizações de origem primária com o Dynamic Media para processamento e publicação de ativos:

1. Quando o ativo de origem principal é carregado no Adobe Experience Manager as a Cloud Service, ele é replicado no Dynamic Media. Nesse momento, o Dynamic Media lida com todo o processamento de ativos e a geração de representação, como a codificação de vídeo e as variantes dinâmicas de uma imagem.
1. Depois que as renderizações são geradas, o Experience Manager como um Cloud Service pode acessar com segurança e visualizar as renderizações remotas do Dynamic Media (nenhum binário é enviado de volta ao Experience Manager como uma instância do Cloud Service).
1. Depois que o conteúdo estiver pronto para publicar e aprovar, ele acionará o serviço da Dynamic Media para enviar conteúdo aos servidores de entrega e armazenar em cache o conteúdo na CDN (Content Delivery Network).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>A lista de recursos a seguir requer o uso do CDN pronto para uso fornecido com o Adobe Experience Manager - Dynamic Media. Nenhum outro CDN personalizado é compatível com esses recursos.
>
>* [Imagem inteligente](/help/assets/dynamic-media/imaging-faq.md)
* [Invalidação de cache](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Proteção de hotlink](/help/assets/dynamic-media/hotlink-protection.md)
* [Entrega de conteúdo HTTP/2](/help/assets/dynamic-media/http2faq.md)
* Redirecionamento de URL no nível CDN
* Akamai ChinaCDN (para entrega ideal na China)


<!-- OBSOLETE CONTENT

## (Optional) Migrating Dynamic Media presets and configurations from 6.3 to 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

If you are upgrading Experience Manager as a Cloud Service Dynamic Media from 6.3 to 6.4 or 6.5 (which now includes the ability for zero downtime deployments), you are required to run the following curl command to migrate all your presets and configurations from `/etc` to `/conf` in CRXDE Lite.

>[!NOTE]
>
>If you run your Experience Manager as a Cloud Service instance in compatibility mode--that is, you have the compatibility packaged installed--you do not need to run these commands.

For all upgrades, either with or without the compatibility package, you can copy the default, out-of-the-box viewer presets that originally came with Dynamic Media by running the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

To migrate any custom viewer presets and configurations that you have created from `/etc` to `/conf`, run the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

-->

## Criar uma configuração do Dynamic Media no Cloud Services {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. No Experience Manager como um Cloud Service, selecione o Experience Manager como um logotipo Cloud Service para acessar o console de navegação global.
1. À esquerda do console, selecione o ícone Ferramentas e vá para **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. Na página Navegador de configuração do Dynamic Media, no painel esquerdo, selecione **[!UICONTROL global]** (não selecione o ícone de pasta à esquerda de **[!UICONTROL global]**). Em seguida, selecione **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Criar configuração do Dynamic Media]**, insira um título, o endereço de email da conta do Dynamic Media, a senha e selecione sua região. Essas informações são fornecidas pelo Adobe no email de provisionamento. Entre em contato com o Atendimento ao cliente do Adobe se não tiver recebido esse email.
1. Selecione **[!UICONTROL Conectar-se ao Dynamic Media]**.
1. Na caixa de diálogo **[!UICONTROL Change Password]**, no campo **[!UICONTROL New Password]**, digite uma nova senha que contenha de 8 a 25 caracteres. A senha deve conter pelo menos uma das seguintes opções:

   * Letra maiúscula
   * Letra minúscula
   * Número
   * Caráter especial: `# $ & . - _ : { }`

   O campo **[!UICONTROL Senha atual]** é intencionalmente pré-preenchido e oculto da interação.

   Se necessário, você pode verificar a ortografia de uma senha digitada ou digitada novamente selecionando o ícone de olho da senha para revelar a senha. Selecione o ícone novamente para ocultar a senha.

1. No campo **[!UICONTROL Repetir senha]**, digite novamente a nova senha e, em seguida, selecione **[!UICONTROL Concluído]**.

   A nova senha é salva quando você seleciona **[!UICONTROL Salvar]** no canto superior direito da página **[!UICONTROL Criar configuração do Dynamic Media]**.

   Se você selecionou **[!UICONTROL Cancelar]** na caixa de diálogo **[!UICONTROL Alterar senha]**, ainda deverá inserir uma nova senha ao salvar a configuração recém-criada do Dynamic Media.

   Consulte também [Alterar a senha para Dynamic Media](#change-dm-password).

1. Quando a conexão for bem-sucedida, você poderá definir o seguinte:

   | Propriedade | Descrição |
   |---|---|
   | Empresa | O nome da conta do Dynamic Media. É possível ter várias contas do Dynamic Media para diferentes submarcas, divisões ou ambientes de preparo/produção. |
   | Caminho da pasta raiz da empresa | O caminho da pasta raiz da sua empresa. |
   | Publicar ativos | Você pode escolher entre as três opções a seguir:<br>**[!UICONTROL Imediatamente ]**- Quando os ativos são carregados, o sistema assimila os ativos e fornece o URL/Incorporado instantaneamente. Não há necessidade de intervenção do usuário para publicar ativos.<br>**[!UICONTROL Em ativação]**  - você deve publicar explicitamente o ativo primeiro antes que um link URL/Incorporar seja fornecido.<br>**[!UICONTROL Publicação seletiva ]**- Os ativos são publicados automaticamente apenas para visualização segura. Eles também podem ser publicados explicitamente no Experience Manager como um Cloud Service, sem publicação no DMS7 para entrega no domínio público. No futuro, essa opção pretende publicar ativos no Experience Manager as a Cloud Service e publicar ativos no Dynamic Media, mutuamente exclusivos entre si. Ou seja, você pode publicar ativos no DMS7 para usar recursos como um Recorte inteligente ou representações dinâmicas. Ou, você pode publicar ativos exclusivamente no Experience Manager como Cloud Service para visualização; esses mesmos ativos não são publicados no DMS7 para entrega no domínio público. |
   | Servidor de visualização seguro | Permite que você especifique o caminho do URL para seu servidor de visualização de representações seguras. Ou seja, depois que as renderizações são geradas, o Experience Manager como um Cloud Service pode acessar com segurança e visualizar as renderizações remotas do Dynamic Media (nenhum binário é enviado de volta ao Experience Manager como uma instância do Cloud Service).<br>A menos que você tenha um acordo especial para usar o servidor da sua empresa ou um servidor especial, o Adobe recomenda deixar essa configuração como especificado. |
   | Sincronizar todo o conteúdo | Selecionado por padrão. Desmarque essa opção se desejar incluir ou excluir seletivamente ativos da sincronização com o Dynamic Media. Desmarcar essa opção permite escolher entre os dois modos de sincronização Dynamic Media a seguir:<br>**[!UICONTROL Modo de sincronização Dynamic Media]**<br>**[!UICONTROL Ativar por padrão ]**- A configuração é aplicada a todas as pastas por padrão, a menos que você marque uma pasta especificamente para exclusão. <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Desativado por padrão]**  - A configuração não é aplicada a nenhuma pasta até que você marque explicitamente uma pasta selecionada para sincronização com o Dynamic Media.<br>Para marcar uma pasta selecionada para sincronização com o Dynamic Media, selecione uma pasta de ativos e, na barra de ferramentas, selecione  **[!UICONTROL Propriedades]**. Na guia **[!UICONTROL Details]**, na lista suspensa **[!UICONTROL Dynamic Media sync mode]**, escolha entre as três opções a seguir. Quando terminar, selecione **[!UICONTROL Save]**. *Lembre-se: essas três opções não estarão disponíveis se você tiver selecionado **Sincronizar todo o**conteúdo anteriormente.* Consulte também  [Trabalhar com publicação seletiva no nível da pasta no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).<br>**[!UICONTROL Herdado ]**- Nenhum valor de sincronização explícito na pasta. Em vez disso, a pasta herda o valor de sincronização de uma de suas pastas ancestrais ou o modo padrão na configuração da nuvem. O status detalhado de herdado é exibido por meio de uma dica de ferramenta.<br>**[!UICONTROL Ativar para subpastas]**  - Inclua tudo nesta subárvore para sincronização com o Dynamic Media. As configurações específicas da pasta substituem o modo padrão na configuração da nuvem.<br>**[!UICONTROL Desabilitado para subpastas ]**- Exclua tudo nesta subárvore da sincronização com o Dynamic Media. |

   >[!NOTE]
   Não há suporte para o controle de versão no Dynamic Media. Além disso, a ativação atrasada se aplica somente se **[!UICONTROL Publicar ativos]** na página Editar configuração do Dynamic Media estiver definida como **[!UICONTROL Na ativação]**. E então, somente até a primeira vez que o ativo é ativado.
   Depois que um ativo é ativado, todas as atualizações são publicadas imediatamente no S7 Delivery.

   ![dynamicmediaconfiguration2atualizado](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Selecione **[!UICONTROL Salvar]**. A nova senha e configuração do Dynamic Media são salvas. Se você selecionou **[!UICONTROL Cancelar]** em vez disso, nenhuma atualização de senha ocorrerá.
1. Na caixa de diálogo **[!UICONTROL Configuração do Dynamic Media]**, selecione **[!UICONTROL OK]** para iniciar a configuração.

   >[!IMPORTANT]
   Quando a nova configuração do Dynamic Media terminar a configuração, você receberá uma notificação de status Experience Manager como uma caixa Cloud Service Inbox.
   Esta notificação da Caixa de entrada informa se a configuração foi bem-sucedida ou não.
Consulte [Solucionar problemas de uma nova configuração do Dynamic Media](#troubleshoot-dm-config) e [Sua caixa de entrada](/help/sites-cloud/authoring/getting-started/inbox.md) para obter mais informações.

1. Para visualizar com segurança o conteúdo do Dynamic Media antes de ser publicado, o Experience Manager como Cloud Service usa a validação baseada em token por padrão. No entanto, também é possível &quot;lista de permissões&quot; mais IPs para fornecer aos usuários acesso a visualização segura do conteúdo. Para configurar essa ação, faça o seguinte: <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

   * Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta. Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Caso não tenha essas informações, entre em contato com o Atendimento ao cliente do Adobe.
   * Na barra de navegação próxima ao canto superior direito da página, vá para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Publicar configuração]** > **[!UICONTROL Servidor de imagem]**.
   * Na página Publicação do servidor de imagens, na lista suspensa **[!UICONTROL Publicar contexto]**, selecione **[!UICONTROL Testar fornecimento de imagem]**.
   * Para o Filtro de endereço do cliente, selecione **[!UICONTROL Adicionar]**.
   * Para ativar (ativar) o endereço, marque a caixa de seleção e digite o endereço IP da instância do autor do Experience Manager (não o IP do Dispatcher).
   * Selecione **[!UICONTROL Salvar]**.

Agora você terminou com a configuração básica; você está pronto para usar o Dynamic Media.

Se você quiser personalizar ainda mais sua configuração, poderá, opcionalmente, concluir qualquer uma das tarefas em [Configurar configurações avançadas no Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Solução de problemas de uma nova configuração do Dynamic Media {#troubleshoot-dm-config}

Quando uma nova configuração do Dynamic Media terminar a configuração, você receberá uma notificação de status Experience Manager como uma caixa Cloud Service Inbox. Esta notificação informa se a configuração foi bem-sucedida ou não, como visto nas imagens a seguir na Caixa de entrada.

![Êxito na Caixa de entrada do Experience Manager](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Falha na Caixa de entrada do Experience Manager](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

Consulte também [Sua Caixa de entrada](/help/sites-cloud/authoring/getting-started/inbox.md).

**Para solucionar problemas de uma nova configuração do Dynamic Media:**

1. Próximo ao canto superior direito da Experience Manager como uma Cloud Service, selecione o ícone de sino e selecione **[!UICONTROL Exibir todos]**.
1. Na página Caixa de entrada, selecione a notificação de sucesso para ler uma visão geral do status e logs da configuração.

   Se a configuração falhar, selecione a notificação de falha semelhante à captura de tela a seguir.

   ![Falha na configuração do Dynamic Media](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. Na página **[!UICONTROL DMSETUP]**, revise os detalhes de configuração que descrevem a falha. Em especial, tome nota de quaisquer mensagens de erro ou códigos de erro. Entre em contato com o Atendimento ao cliente do Adobe com essas informações.

   ![Página Configurar Dynamic Media](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Alterar a senha para Dynamic Media {#change-dm-password}

A expiração da senha no Dynamic Media é definida como 100 anos a partir da data atual do sistema.

A senha deve conter pelo menos uma das seguintes opções:

* Letra maiúscula
* Letra minúscula
* Número
* Caráter especial: `# $ & . - _ : { }`

Se necessário, você pode verificar a ortografia de uma senha digitada ou digitada novamente selecionando o ícone de olho da senha para revelar a senha. Selecione o ícone novamente para ocultar a senha.

A senha alterada é salva quando você seleciona **[!UICONTROL Salvar]** no canto superior direito da página **[!UICONTROL Editar configuração do Dynamic Media]**.

1. No Experience Manager como um Cloud Service, selecione o Experience Manager como um logotipo Cloud Service para acessar o console de navegação global.
1. À esquerda do console, selecione o ícone Ferramentas e vá para **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. Na página Navegador de configuração do Dynamic Media, no painel esquerdo, selecione **[!UICONTROL global]**. Não selecione o ícone de pasta à esquerda de **[!UICONTROL global]**. Em seguida, selecione **[!UICONTROL Edit]**.
1. Na página **[!UICONTROL Editar configuração do Dynamic Media]**, logo abaixo do campo **[!UICONTROL Senha]**, selecione **[!UICONTROL Alterar senha]**.
1. Na caixa de diálogo **[!UICONTROL Alterar senha]**, faça o seguinte:

   * No campo **[!UICONTROL New Password]**, digite uma nova senha.

      O campo **[!UICONTROL Senha atual]** é intencionalmente pré-preenchido e oculto da interação.

   * No campo **[!UICONTROL Repetir senha]**, digite novamente a nova senha e, em seguida, selecione **[!UICONTROL Concluído]**.

1. No canto superior direito da página **[!UICONTROL Editar configuração do Dynamic Media]**, selecione **[!UICONTROL Salvar]** e selecione **[!UICONTROL OK]**.

## (Opcional) Defina as Configurações avançadas no Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Para personalizar ainda mais a configuração e configuração do Dynamic Media ou otimizar seu desempenho, você pode concluir uma ou mais das seguintes tarefas *opcionais*:

* [Configuração e configuração das configurações do Dynamic Media](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Opcional) Ajuste o desempenho do Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### (Opcional) Configuração e configuração das configurações do Dynamic Media {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Use a interface do usuário do Dynamic Media Classic para alterar as configurações do Dynamic Media.

Algumas das tarefas acima exigem que você abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta.

As tarefas de configuração e configuração incluem:

* [Configuração de publicação para o servidor de imagem](#publishing-setup-for-image-server)
* [Definir configurações gerais do aplicativo](#configuring-application-general-settings)
* [Configurar o gerenciamento de cores](#configuring-color-management)
* [Editar tipos MIME para formatos compatíveis](#editing-mime-types-for-supported-formats)
* [Adicionar tipos MIME para formatos não suportados](#adding-mime-types-for-unsupported-formats)

<!-- * [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Configuração de publicação para o servidor de imagem {#publishing-setup-for-image-server}

As configurações de Configuração de publicação determinam como os ativos são entregues por padrão no Dynamic Media. Se nenhuma configuração for especificada, o Dynamic Media fornece um ativo de acordo com as configurações padrão definidas na Configuração de publicação. Por exemplo, uma solicitação para fornecer uma imagem que não inclua um atributo de resolução gera uma imagem com a configuração Resolução de objeto padrão .

Para configurar a Configuração de publicação: no Dynamic Media Classic, vá para **[!UICONTROL Configuração > Configuração do aplicativo > Configuração de publicação > Servidor de imagem]**.

A tela Servidor de imagens estabelece as configurações padrão para entrega de imagens. Consulte a tela da interface do usuário para obter uma descrição de cada configuração.

**[!UICONTROL Atributos de solicitação]**  - essas configurações impõem limites às imagens que podem ser entregues a partir do servidor.
**[!UICONTROL Atributos de solicitação padrão]**  - Essas configurações pertencem à aparência padrão das imagens.
**[!UICONTROL Atributos de miniatura comuns]**  - Essas configurações pertencem à aparência padrão das imagens em miniatura.
**[!UICONTROL Padrões para campos de catálogo]** - Essas configurações pertencem à resolução e ao tipo de miniatura padrão de imagens.
**[!UICONTROL Atributos de gerenciamento de cores]**  - Essas configurações determinam quais perfis de cores ICC são usados.
**[!UICONTROL Atributos de compatibilidade]**  - Essa configuração permite que parágrafos anteriores e posteriores em camadas de texto sejam tratados como na versão 3.6 para compatibilidade com versões anteriores.
**[!UICONTROL Suporte à localização]**  - Essas configurações permitem gerenciar vários atributos de localidade. Ela também permite especificar uma sequência de mapa de localidade para que você possa definir quais idiomas deseja suportar para as várias dicas de ferramentas em Visualizadores. Para obter mais informações sobre como configurar o **[!UICONTROL Suporte de localização]**, consulte [Considerações ao configurar a localização de ativos](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets).

#### Definir configurações gerais do aplicativo {#configuring-application-general-settings}

Para abrir a página Configurações gerais do aplicativo , na barra Navegação global do Dynamic Media Classic, vá para **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais]**.

**[!UICONTROL Servidores]**  - No provisionamento da conta, a Dynamic Media fornece automaticamente os servidores atribuídos à sua empresa. Esses servidores são usados para criar strings de URL para seu site e aplicativos. Essas chamadas de URL são específicas da sua conta do . Não altere nenhum nome de servidor a menos que seja explicitamente instruído a fazê-lo pelo Experience Manager como suporte ao Cloud Service.
**[!UICONTROL Substituir imagens]**  - o Dynamic Media não permite que dois arquivos tenham o mesmo nome. A ID de URL de cada item (o nome do arquivo menos a extensão) deve ser exclusiva. Essas opções especificam como os ativos de substituição são carregados: se substituem o original ou se tornam duplicatas. Os ativos duplicados são renomeados com um &quot;-1&quot; (por exemplo, chair.tif é renomeado chair-1.tif). Essas opções afetam os ativos carregados em uma pasta diferente do original ou os ativos com uma extensão de arquivo diferente do original.
**[!UICONTROL Substituir na pasta atual, mesmo nome/extensão de imagem base]**  - Essa opção é a regra mais estrita para substituição. Ela requer que você carregue a imagem de substituição na mesma pasta do original e que ela tenha a mesma extensão de arquivo do original. Se esses requisitos não forem atendidos, uma duplicata será criada. Para manter a consistência com o Experience Manager como um Cloud Service, sempre escolha **[!UICONTROL Overwrite in current folder, same base image name/extension]**.
**[!UICONTROL Substituir em qualquer pasta, mesmo nome/extensão do ativo básico]**  - Requer que a imagem de substituição tenha a mesma extensão de arquivo que a imagem original. Por exemplo, chair.jpg deve substituir chair.jpg, não chair.tif. No entanto, é possível fazer upload da imagem de substituição para uma pasta diferente da original. A imagem atualizada reside na nova pasta; o arquivo não pode mais ser encontrado em seu local original.
**[!UICONTROL Substituir em qualquer pasta, o mesmo nome do ativo base independentemente da extensão]**  - Essa opção é a regra de substituição mais inclusiva. Você pode carregar uma imagem de substituição em uma pasta diferente do original, carregar um arquivo com uma extensão de arquivo diferente e substituir o arquivo original. Se o arquivo original estiver em uma pasta diferente, a imagem de substituição residirá na nova pasta para a qual foi carregada.
**[!UICONTROL Perfis de cores padrão]**  - Consulte  [Configurar o ](#configuring-color-management) gerenciamento de cores para obter mais informações. Por padrão, o sistema mostra 15 execuções ao selecionar **[!UICONTROL Representações]** e 15 predefinições do visualizador ao selecionar **[!UICONTROL Visualizadores]** na exibição detalhada do ativo. Você pode aumentar esse limite. Consulte [Aumente ou diminua o número de predefinições de imagens que exibem](/help/assets/dynamic-media/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) ou [Aumente ou diminua o número de predefinições do visualizador que exibem](/help/assets/dynamic-media/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### Configurar o gerenciamento de cores {#configuring-color-management}

O gerenciamento de cores do Dynamic Media permite corrigir a cor dos ativos. Com a correção de cores, os ativos assimilados retêm seu espaço de cores (RGB, CMYK, Cinza) e o perfil de cores incorporado. Quando você solicita uma representação dinâmica, a cor da imagem é corrigida no espaço de cores de destino usando saída CMYK, RGB ou Cinza. Consulte [Configurar predefinições de imagem](/help/assets/dynamic-media/managing-image-presets.md).

Para configurar as propriedades de cores padrão para ativar a correção de cores ao solicitar imagens:

1. Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta usando as credenciais fornecidas durante o provisionamento.
1. Vá para **[!UICONTROL Configurar > Configuração do Aplicativo]**.
1. Expanda a área **[!UICONTROL Publicar configuração]** e selecione **[!UICONTROL Servidor de imagens]**. Defina **[!UICONTROL Publicar contexto]** como **[!UICONTROL Serviço de imagem]** ao definir padrões para instâncias de publicação.
1. Role até a propriedade que você deve alterar, por exemplo, uma propriedade na área **[!UICONTROL Atributos de gerenciamento de cores]**.
Você pode definir as seguintes propriedades de correção de cores:

   | Propriedade | Descrição |
   |---|---|
   | Espaço de cores padrão CMYK | Nome do perfil de cores CMYK padrão. |
   | Espaço de cor padrão da escala de cinza | Nome do perfil de cor cinza padrão. |
   | Espaço de cores padrão RGB | Nome do perfil de cores RGB padrão. |
   | Propósito de renderização da conversão de cores | Especifica o propósito de renderização. Os valores aceitáveis são: **[!UICONTROL perceptual]**, **[!UICONTROL calorimetria relativa]**, **[!UICONTROL saturação]**, **[!UICONTROL calorimetria absoluta]**. O Adobe recomenda **[!UICONTROL relative]** como padrão. |

1. Selecione **[!UICONTROL Salvar]**.

Por exemplo, você pode definir o **[!UICONTROL Espaço de cor padrão RGB]** como *sRGB* e o **[!UICONTROL Espaço de cor padrão CMYK]** como *WebCoated*.

Isso faria o seguinte:

* Permite a correção de cores para imagens RGB e CMYK.
* Imagens RGB que não têm um perfil de cor são consideradas como estando no espaço de cores *sRGB*.
* Imagens CMYK que não têm um perfil de cor são consideradas como estando no espaço de cores *WebCoated*.
* As representações dinâmicas que retornam a saída RGB, retornam no espaço de cores *sRGB*.
* As representações dinâmicas que retornam saída CMYK, retornam no espaço de cores *WebCoated*.

#### Editar tipos MIME para formatos compatíveis {#editing-mime-types-for-supported-formats}

Você pode definir quais tipos de ativos são processados pelo Dynamic Media e personalizar parâmetros avançados de processamento de ativos. Por exemplo, você pode especificar parâmetros de processamento de ativos para fazer o seguinte:

* Converter um Adobe PDF em um ativo de eCatalog.
* Converta um documento do Adobe Photoshop (.PSD) em um ativo de modelo de banner para personalização.
* Rasterize um arquivo Adobe Illustrator (.AI) ou um arquivo Adobe Photoshop Encapsulated PostScript® (.EPS).
* [É possível usar ](/help/assets/dynamic-media/video-profiles.md) Perfis de vídeo e  [Perfis de ](/help/assets/dynamic-media/image-profiles.md) imagem para definir o processamento de vídeos e imagens, respectivamente.

Consulte [Fazer upload de ativos](/help/assets/add-assets.md).

**Para editar tipos MIME para formatos compatíveis:**

1. No Experience Manager como um Cloud Service, selecione o Experience Manager como um logotipo Cloud Service para acessar o console de navegação global e, em seguida, vá para **[!UICONTROL General > CRXDE Lite]**.
1. No painel à esquerda, navegue até o seguinte:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipos MIME](assets/mimetypes.png)

1. Na pasta mimeTypes , selecione um tipo MIME.
1. No lado direito da página CRXDE Lite, na parte inferior:

   * Toque duas vezes no campo **[!UICONTROL enabled]**. Por padrão, todos os tipos de ativos MIME são ativados (definidos como **[!UICONTROL true]**), o que significa que os ativos são sincronizados com a Dynamic Media para processamento. Se desejar excluir esse tipo MIME de ativo do processamento, altere essa configuração para **[!UICONTROL false]**.

   * Toque duas vezes em **[!UICONTROL jobParam]** para abrir seu campo de texto associado. Consulte [Tipos MIME suportados](/help/assets/file-format-support.md) para obter uma lista de valores de parâmetros de processamento permitidos que você pode usar para um determinado tipo MIME.

1. Faça uma das seguintes opções:
   * Repita as etapas 3 a 4 para editar mais tipos MIME.
   * Na barra de menu da página CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.

1. No canto superior esquerdo da página, selecione **[!UICONTROL CRXDE Lite]** para retornar a Experience Manager como Cloud Service.

#### Adicionar tipos MIME para formatos não suportados {#adding-mime-types-for-unsupported-formats}

Você pode adicionar tipos MIME personalizados para formatos não compatíveis no Experience Manager Assets. Para garantir que qualquer novo nó adicionado no CRXDE Lite não seja excluído pelo Experience Manager, mova o tipo MIME antes de `image_`. Além disso, verifique se o valor ativado está definido como **[!UICONTROL false]**.

**Para adicionar tipos MIME para formatos não suportados:**

1. No Experience Manager as a Cloud Service, vá para **[!UICONTROL Tools > Operations > Web Console]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Uma nova guia do navegador é aberta para a página **[!UICONTROL Configuração do console da Web do Adobe Experience Manager]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Na página, role para baixo até o nome *Adobe CQ Scene7 Asset MIME type Service*, como visto na seguinte captura de tela. À direita do nome, toque em **[!UICONTROL Editar os valores]** de configuração (ícone de lápis).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. Na página **Adobe CQ Scene7 Asset MIME type Service**, selecione qualquer ícone de sinal de mais &lt;+>. O local na tabela onde você seleciona o sinal de mais para adicionar o novo tipo MIME é trivial.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Digite `DWG=image/vnd.dwg` no campo de texto vazio que acabou de adicionar.

   O tipo MIME `DWG=image/vnd.dwg` é somente para fins de amostra. O tipo MIME adicionado aqui pode ser qualquer outro formato não suportado.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. No canto inferior direito da página, selecione **[!UICONTROL Save]**.

   Nesse ponto, você pode fechar a guia do navegador que tem a página de Configuração do Console da Web do Adobe Experience Manager aberta.

1. Retorne à guia do navegador que tem seu Experience Manager aberto como console do Cloud Service.
1. No Experience Manager como um Cloud Service, vá para **[!UICONTROL Tools > General > CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. No painel à esquerda, navegue até o seguinte:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Arraste o tipo MIME `image_vnd.dwg` e solte-o diretamente acima de `image_` na árvore, como visto na seguinte captura de tela.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Com o tipo MIME `image_vnd.dwg` ainda selecionado, na guia **[!UICONTROL Propriedades]**, na linha **[!UICONTROL ativada]**, no cabeçalho da coluna **[!UICONTROL Valor]**, toque duas vezes no valor. A lista suspensa **[!UICONTROL Value]** é aberta.
1. Digite `false` no campo (ou selecione **[!UICONTROL false]** na lista suspensa).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Próximo ao canto superior esquerdo da página CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.



### (Opcional) Ajuste o desempenho do Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Para manter o Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> funcionando sem problemas, o Adobe recomenda as seguintes dicas de ajuste de desempenho/escalabilidade da sincronização:

* Atualização dos parâmetros de Trabalho predefinidos para processamento de diferentes formatos de arquivo.
* Atualizar os encadeamentos de trabalho de fila predefinidos do fluxo de trabalho Granite (ativos de vídeo).
* Atualização dos threads de trabalho de fila predefinidos do fluxo de trabalho transitório do Granite (imagens e ativos que não são de vídeo).
* Atualização das conexões máximas de upload para o servidor do Dynamic Media Classic.

#### Atualizar os parâmetros de Trabalho predefinidos para o processamento de diferentes formatos de arquivo

Você pode ajustar parâmetros de trabalho para processamento mais rápido ao carregar arquivos. Por exemplo, se você carregar arquivos PSD, mas não quiser processá-los como modelos, poderá definir a extração de camada como false (off). Nesse caso, o parâmetro de trabalho ajustado aparece da seguinte maneira: `process=None&createTemplate=false`.

Caso deseje ativar a criação do modelo, use os seguintes parâmetros: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

O Adobe recomenda usar os seguintes parâmetros de trabalho &quot;ajustados&quot; para arquivos PDF, PostScript® e PSD:

| Tipo de arquivo | Parâmetros de tarefa recomendados |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Para atualizar qualquer um desses parâmetros, consulte [Edição de tipos MIME para formatos compatíveis](#editing-mime-types-for-supported-formats).

Consulte também [Adicionar tipos MIME para formatos não suportados](#adding-mime-types-for-unsupported-formats).

#### Atualize a fila de Fluxo de trabalho transitório do Granite {#updating-the-granite-transient-workflow-queue}

A fila Fluxo de trabalho de trânsito do Granite é usada para o fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]**. No Dynamic Media, é usado para assimilação e processamento de imagens.

**Para atualizar a fila de Fluxo de trabalho transitório do Granite:**

1. Navegue até [https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr) e procure por **Fila: Fila de Fluxo de Trabalho Transitório do Granite**.

   >[!NOTE]
   Uma pesquisa de texto é necessária em vez de um URL direto porque o PID do OSGi é gerado dinamicamente.

1. No campo **[!UICONTROL Máximo de Trabalhos Paralelos]**, altere o número para o valor desejado.

   Você pode aumentar **[!UICONTROL Máximo de trabalhos paralelos]** para suportar adequadamente o upload pesado de arquivos para o Dynamic Media. O valor exato depende da capacidade do hardware. Em determinados cenários, como uma migração inicial ou um upload em massa único, você pode usar um valor grande. Esteja ciente, no entanto, de que o uso de um valor grande (como duas vezes o número de núcleos) pode ter efeitos negativos em outras atividades simultâneas. Dessa forma, teste e ajuste o valor com base no seu caso de uso específico.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Selecione **[!UICONTROL Salvar]**.

#### Atualizar a fila do Fluxo de trabalho do Granite {#updating-the-granite-workflow-queue}

A fila Fluxo de trabalho do Granite é usada para fluxos de trabalho não transitórios. No Dynamic Media, ele processava vídeo com o fluxo de trabalho **[!UICONTROL Codificação de vídeo do Dynamic Media]**.

**Para atualizar a fila do Fluxo de trabalho do Granite:**

1. Navegue até `https://<server>/system/console/configMgr` e procure por **Fila: Fila de fluxo de trabalho do Granite**.

   >[!NOTE]
   Uma pesquisa de texto é necessária em vez de um URL direto porque o PID do OSGi é gerado dinamicamente.

1. No campo **[!UICONTROL Máximo de Trabalhos Paralelos]**, altere o número para o valor desejado.

   Por padrão, o número máximo de trabalhos paralelos depende do número de núcleos de CPU disponíveis. Por exemplo, em um servidor de 4 núcleos, atribui dois threads de trabalho. (Um valor entre 0,0 e 1,0 é baseado em relação ou qualquer número maior que um atribui o número de threads de trabalho.)

   Para a maioria dos casos de uso, a configuração padrão 0.5 é suficiente.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Selecione **[!UICONTROL Salvar]**.

#### Atualizar a conexão de upload do Scene7 {#updating-the-scene-upload-connection}

A configuração Scene7 Upload Connection sincroniza ativos do Experience Manager para servidores do Dynamic Media Classic.

**Para atualizar a conexão de upload do Scene7:**

1. Vá até `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. No campo **[!UICONTROL Number of connections]** ou no campo **[!UICONTROL Ative job timeout]**, ou em ambos, altere o número conforme desejado.

   A configuração **[!UICONTROL Number of connections]** controla o número máximo de conexões HTTP permitidas para upload do Experience Manager para o Dynamic Media. Normalmente, o valor predefinido de dez conexões é suficiente.

   A configuração **[!UICONTROL Tempo limite do trabalho ativo]** determina o tempo de espera para que os ativos Dynamic Media carregados sejam publicados no servidor de delivery. Esse valor é de 2100 segundos ou 35 minutos por padrão.

   Para a maioria dos casos de uso, a configuração de 2100 é suficiente.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Selecione **[!UICONTROL Salvar]**.

<!-- NOTE - OBSOLETE that customisations to replication agents to transform content are no longer used; the following content is obsolete now 

### (Optional) Filtering assets for replication {#optional-filtering-assets-for-replication}

In non-Dynamic Media deployments, you replicate *all* assets (both images and video) from your Experience Manager as a Cloud Service author environment to the Experience Manager as a Cloud Service publish node. This workflow is necessary because the Experience Manager as a Cloud Service publish servers also deliver the assets.

However, in Dynamic Media deployments, because assets are delivered by way of the cloud service, there is no need to replicate those same assets to Experience Manager as a Cloud Service publish nodes. Such a "hybrid publishing" workflow avoids extra storage costs and longer processing times to replicate assets. Other content, such as Site pages, continue to be served from the Experience Manager as a Cloud Service publish nodes.

The filters provide a way for you to *exclude* assets from being replicated to the Experience Manager as a Cloud Service publish node.

#### Using default asset filters for replication {#using-default-asset-filters-for-replication}

If you are using Dynamic Media for imaging and/or video, then you can use the default filters that we provide as-is. The following filters are active by default:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>Mimetype</strong></td>
   <td><strong>Renditions</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Delivery</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Starts with <strong>image/</strong></p> <p>Contains <strong>application/</strong> and ends with <strong>set</strong>.</p> </td>
   <td>The out-of-the-box "filter-images" (applies to single images assets, including interactive images) and "filter-sets" (applies to Spin Sets, Image Sets, Mixed Media Sets, and Carousel Sets) will:
    <ul>
     <li>Exclude from replication the original image and static image renditions.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Video Delivery</td>
   <td>filter-video</td>
   <td>Starts with <strong>video/</strong></td>
   <td>The out-of-the-box "filter-video" will:
    <ul>
     <li>Exclude from replication the original video and static thumbnail renditions.<br /> <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Filters apply to mime types and cannot be path specific.

#### Customizing asset filters for replication {#customizing-asset-filters-for-replication}

1. In Experience Manager as a Cloud Service, select the Experience Manager as a Cloud Service logo to access the global navigation console and select the **[!UICONTROL Tools > General > CRXDE Lite]**.
1. In the left folder tree, navigate to `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` to review the filters.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. To define the Mime Type for the filter, you can locate the Mime Type as follows:

   In the left rail, expand `content > dam > <locate_your_asset> > jcr:content > metadata`, and then in the table, locate `dc:format`.

   The following graphic is an example of an asset's path to `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Notice that the `dc:format` for the asset `Fiji Red.jpg` is `image/jpeg`.

   To have this filter apply to all images, regardless of their format, set the value to `image/*` where `*` is a regular expression that is applied to all images of any format.

   To have the filter apply only to images of the type JPEG, enter a value of `image/jpeg`.

1. Define what renditions you want to include or exclude from replication.

   Characters that you can use to filter for replication include the following:

<table>
 <tbody>
  <tr>
   <td><strong>Character to use</strong></td>
   <td><strong>How it filters assets for replication</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>Wildcard character<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>Includes assets for replication.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Excludes assets from replication.</td>
  </tr>
 </tbody>
</table>

   Navigate to `content/dam/<locate your asset>/jcr:content/renditions`.

   The following graphic is an example of an asset's renditions.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   If you only wanted to replicate the original, then you would enter `+original`.

   -->
