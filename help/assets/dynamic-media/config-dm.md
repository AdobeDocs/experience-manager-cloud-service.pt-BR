---
title: Configuração do Dynamic Media Cloud Service
description: Informações sobre como configurar o Dynamic Media no Adobe Experience Manager como um Cloud Service.
translation-type: tm+mt
source-git-commit: c0db892d58f762bd5659596371ece86950e9cdd7
workflow-type: tm+mt
source-wordcount: '3869'
ht-degree: 8%

---


# Sobre a configuração do Dynamic Media Cloud Service {#configuring-dynamic-media}

Se você usar a configuração da Adobe Experience Manager para ambientes diferentes, como um para desenvolvimento, um para armazenamento temporário e outro para produção ao vivo, é necessário configurar Cloud Services Dynamic Media para cada um desses ambientes.

## Diagrama de arquitetura do Dynamic Media {#architecture-diagram-of-dynamic-media}

O diagrama de arquitetura a seguir descreve como a Dynamic Media funciona.

Com a nova arquitetura, AEM é responsável por ativos de origem primária e sincronizações com a Dynamic Media para processamento e publicação de ativos:

1. Quando o ativo de origem principal é carregado para AEM, ele é replicado para a Dynamic Media. Nesse ponto, a Dynamic Media lida com todo o processamento de ativos e geração de representação, como codificação de vídeo e variantes dinâmicas de uma imagem.
1. Depois que as renderizações são geradas, AEM podem acessar e pré-visualização com segurança as renderizações remotas do Dynamic Media (nenhum binário é enviado de volta à instância AEM).
1. Depois que o conteúdo estiver pronto para ser publicado e aprovado, ele aciona o serviço da Dynamic Media para enviar o conteúdo para os servidores de delivery e armazená-lo em cache no CDN.

![chlimage_1-550](assets/chlimage_1-550.png)

<!-- OBSOLETE CONTENT

## (Optional) Migrating Dynamic Media presets and configurations from 6.3 to 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

If you are upgrading AEM Dynamic Media from 6.3 to 6.4 or 6.5 (which now includes the ability for zero downtime deployments), you are required to run the following curl command to migrate all your presets and configurations from `/etc` to `/conf` in CRXDE Lite.

>[!NOTE]
>
>If you run your AEM instance in compatibility mode--that is, you have the compatibility packaged installed--you do not need to run these commands.

For all upgrades, either with or without the compatibility package, you can copy the default, out-of-the-box viewer presets that originally came with Dynamic Media by running the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

To migrate any custom viewer presets and configurations that you have created from `/etc` to `/conf`, run the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

-->

## Criação de uma nova configuração do Dynamic Media no Cloud Services {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. Em AEM, toque no logotipo AEM para acessar o console de navegação global.
1. No lado esquerdo do console, toque no ícone Ferramentas e em **[!UICONTROL Cloud Services > Configuração do Dynamic Media]**.
1. Na página Navegador de configuração do Dynamic Media, no painel à esquerda, toque em **[!UICONTROL global]** (não toque ou selecione o ícone de pasta à esquerda de **[!UICONTROL global]**) e, em seguida, toque em **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Criar Configuração do Dynamic Media]**, digite um título, o endereço de email da conta do Dynamic Media, a senha e selecione sua região. Eles são fornecidos por Adobe no e-mail de provisionamento. Entre em contato com o suporte se você não recebeu essa solicitação.
1. Clique em **[!UICONTROL Conectar-se ao Dynamic Media]**.
1. Na caixa de diálogo **[!UICONTROL Alterar Senha]**, no campo **[!UICONTROL Nova Senha]**, digite uma nova senha que contenha de 8 a 25 caracteres. A senha deve conter pelo menos um dos seguintes:

   * Letra maiúscula
   * Letra minúscula
   * Número
   * Caráter especial: `# $ & . - _ : { }`

   Observe que o campo **[!UICONTROL Senha atual]** está intencionalmente pré-preenchido e oculto da interação.

   Se necessário, você pode verificar a ortografia de uma senha que digitou ou digitou novamente tocando no ícone do olho da senha para revelar a senha. Toque no ícone novamente para ocultar a senha.

1. No campo **[!UICONTROL Repetir senha]**, digite novamente a nova senha e, em seguida, toque em **[!UICONTROL Concluído.]**

   A nova senha é salva quando você toca em **[!UICONTROL Salvar]** no canto superior direito da página **[!UICONTROL Criar Configuração do Dynamic Media]**.

   Se você tocou em **[!UICONTROL Cancelar]** na caixa de diálogo **[!UICONTROL Alterar senha]**, ainda é necessário digitar uma nova senha ao tocar em **[!UICONTROL Salvar]** para salvar a configuração recém-criada do Dynamic Media.

   Consulte também [Alterar a senha para Dynamic Media](#change-dm-password).

1. Quando a conexão for bem-sucedida, você poderá definir o seguinte:

   | Propriedade | Descrição |
   |---|---|
   | Empresa | O nome da conta do Dynamic Media. É possível que você tenha várias contas da Dynamic Media para diferentes submarcas, divisões ou ambientes de preparo/produção diferentes. |
   | Caminho da pasta raiz da empresa | O caminho da pasta raiz do empresa. |
   | Publicar ativos | Você pode escolher entre as três opções a seguir:<br>**[!UICONTROL Imediatamente ]**: Quando os ativos são carregados, o sistema recebe os ativos e fornece o URL/Incorporado instantaneamente. Não há necessidade de intervenção do usuário para publicar ativos.<br>**[!UICONTROL Na Ativação]**: É necessário publicar explicitamente o ativo primeiro antes que um link URL/Incorporado seja fornecido.<br>**[!UICONTROL Publicação ]**seletiva: Os ativos são publicados automaticamente apenas para pré-visualização segura e podem ser publicados explicitamente em AEM sem publicação no DMS7 para delivery no domínio público. No futuro, o Adobe aprimorará essa opção para publicar ativos para AEM e publicar ativos na Dynamic Media, mutuamente exclusivos entre si. Ou seja, você pode publicar ativos no DMS7 para poder usar recursos como Recorte inteligente ou representações dinâmicas. Ou, você pode publicar ativos exclusivamente em AEM para visualização; esses mesmos ativos não são publicados no DMS7 para delivery no domínio público. |
   | Servidor de visualização seguro | Permite que você especifique o caminho do URL para o servidor de pré-visualização de representações seguras. Ou seja, depois que as renderizações são geradas, AEM podem acessar e pré-visualização com segurança as renderizações remotas do Dynamic Media (nenhum binário é enviado de volta à instância AEM).<br>A menos que você tenha uma disposição especial para usar seu próprio servidor empresa ou um servidor especial, a Adobe Systems recomenda deixar essa configuração como especificado. |
   | Sincronizar todo o conteúdo | Selecionado por padrão. Desmarque essa opção se desejar incluir ou excluir seletivamente ativos da sincronização para o Dynamic Media. Desmarcar essa opção permite escolher entre os dois modos de sincronização do Dynamic Media a seguir:<br>**[!UICONTROL Modo de sincronização do Dynamic Media]**<br>**[!UICONTROL Ativar por padrão ]**: A configuração é aplicada a todas as pastas por padrão, a menos que você marque uma pasta especificamente para exclusão. <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Desativado por padrão]**: A configuração não é aplicada a nenhuma pasta até que você marque explicitamente uma pasta selecionada para sincronização com o Dynamic Media.<br>Para marcar uma pasta selecionada para sincronização com o Dynamic Media, selecione uma pasta de ativos e, na barra de ferramentas, toque em  **[!UICONTROL Propriedades]**. Na guia **[!UICONTROL Details]**, na lista suspensa **[!UICONTROL Modo de sincronização Dynamic Media]**, escolha uma das três opções a seguir. Quando terminar, toque em **[!UICONTROL Salvar]**. *Lembre-se: essas três opções não estarão disponíveis se você tiver selecionado **Sincronizar todo o**conteúdo anteriormente.* Consulte também  [Trabalhar com publicação seletiva no nível da pasta no Dynamic Media.](/help/assets/dynamic-media/selective-publishing.md)<br>**[!UICONTROL Herdado ]**: Nenhum valor de sincronização explícito na pasta; em vez disso, a pasta herda o valor de sincronização de uma de suas pastas ancestrais ou o modo padrão na configuração da nuvem. O status detalhado para herdado é exibido por meio de uma dica de ferramenta.<br>**[!UICONTROL Ativar para subpastas]**: Inclua tudo nesta subárvore para sincronização com o Dynamic Media. As configurações específicas da pasta substituem o modo padrão na configuração da nuvem.<br>**[!UICONTROL Desativado para subpastas ]**: Exclua da sincronização de tudo nesta subárvore para o Dynamic Media. |

   >[!NOTE]
   >
   >Não há suporte para o controle de versão no Dynamic Media. Além disso, a ativação atrasada se aplica somente se **[!UICONTROL Publicar ativos]** na página Editar configuração do Dynamic Media estiver definida como **[!UICONTROL Na ativação]** e, em seguida, somente até a primeira vez que o ativo for ativado.
   >
   >
   >Depois que um ativo é ativado, todas as atualizações são publicadas imediatamente no Delivery S7.

   ![dynamicmediaconfiguration2atualizado](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Toque em **[!UICONTROL Salvar]**. A nova senha e configuração do Dynamic Media são salvas. Se você tocou em **[!UICONTROL Cancelar]**, nenhuma atualização de senha ocorre.
1. Na caixa de diálogo **[!UICONTROL Configuração do Dynamic Media]**, toque em **[!UICONTROL OK]** para iniciar a configuração.

   >[!IMPORTANT]
   >
   >Quando a nova configuração do Dynamic Media terminar a configuração, você receberá uma notificação de status na Caixa de entrada AEM.
   >
   >Esta notificação de Caixa de entrada informa se a configuração foi bem-sucedida ou não.
   > Consulte [Resolução de problemas de uma nova configuração do Dynamic Media](#troubleshoot-dm-config) e [Caixa de entrada](/help/sites-cloud/authoring/getting-started/inbox.md) para obter mais informações.

1. Para pré-visualização segura do conteúdo do Dynamic Media antes de ele ser publicado, é necessário &quot;lista de permissões&quot; a instância do autor AEM para se conectar ao Dynamic Media. Para configurar isso, faça o seguinte:

   * Abra o [aplicativo Dynamic Media Classic para desktop](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta. Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte Técnico.
   * Na barra de navegação próxima à parte superior direita da página, clique em **[!UICONTROL Configuração > Configuração de aplicativo > Configuração de publicação > Servidor de imagem]**.

   * Na página Publicação do Servidor de Imagens, na lista suspensa Contexto de Publicação, selecione **[!UICONTROL Servidor de Imagens de Teste]**.
   * Para o Filtro de endereço do cliente, toque em **[!UICONTROL Adicionar]**.
   * Marque a caixa de seleção para ativar (ativar) o endereço e, em seguida, insira o endereço IP da instância do autor de AEM (não o IP do Dispatcher).
   * Clique em **[!UICONTROL Salvar]**.

Agora você terminou com a configuração básica; você está pronto para usar o Dynamic Media.

Se desejar personalizar ainda mais sua configuração, você pode, opcionalmente, concluir qualquer uma das tarefas em [Configuração de configurações avançadas no Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Solução de problemas de uma nova configuração do Dynamic Media {#troubleshoot-dm-config}

Quando uma nova configuração do Dynamic Media terminar sua configuração, você receberá uma notificação de status na Caixa de entrada AEM. Esta notificação informa se a configuração foi bem-sucedida ou não, conforme visto nas seguintes imagens respectivas da Caixa de entrada.

![aeminboxsuccess](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![falha de aeminbox](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

Consulte também [Sua Caixa de Entrada](/help/sites-cloud/authoring/getting-started/inbox.md).

**Para solucionar problemas de uma nova configuração do Dynamic Media**

1. Perto do canto superior direito da página de AEM, toque no ícone do sino e em **[!UICONTROL Visualização Todos]**.
1. Na página Caixa de entrada, toque na notificação de sucesso para ler uma visão geral do status e dos registros da configuração.

   Se a configuração falhar, toque na notificação de falha semelhante à captura de tela a seguir.

   ![dmsetupfailed](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. Na página **[!UICONTROL DMSETUP]**, reveja os detalhes de configuração que descrevem a falha. Em especial, tome nota de quaisquer mensagens de erro ou códigos de erro. Você precisará entrar em contato com o Adobe Care com essas informações.

   ![dmsetuppage](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Alteração da senha para Dynamic Media {#change-dm-password}

A expiração da senha no Dynamic Media é definida para 100 anos a partir da data atual do sistema.

A senha deve conter pelo menos um dos seguintes:

* Letra maiúscula
* Letra minúscula
* Número
* Caráter especial: `# $ & . - _ : { }`

Se necessário, você pode verificar a ortografia de uma senha que digitou ou digitou novamente tocando no ícone do olho da senha para revelar a senha. Toque no ícone novamente para ocultar a senha.

A senha alterada é salva quando você toca em **[!UICONTROL Salvar]** no canto superior direito da página **[!UICONTROL Editar configuração do Dynamic Media]**.

1. Em AEM, toque no logotipo AEM para acessar o console de navegação global.
1. No lado esquerdo do console, toque no ícone Ferramentas e em **[!UICONTROL Cloud Services > Configuração do Dynamic Media.]**
1. Na página Navegador de configuração do Dynamic Media, no painel esquerdo, toque em **[!UICONTROL global]** (não toque nem selecione o ícone de pasta à esquerda de **[!UICONTROL global]**) e, em seguida, toque em **[!UICONTROL Editar.]**
1. Na página **[!UICONTROL Editar Configuração do Dynamic Media]**, logo abaixo do campo **[!UICONTROL Senha]**, toque em **[!UICONTROL Alterar Senha.]**
1. Na caixa de diálogo **[!UICONTROL Alterar senha]**, faça o seguinte:

   * No campo **[!UICONTROL Nova senha]**, digite uma nova senha.

      Observe que o campo **[!UICONTROL Senha atual]** está intencionalmente pré-preenchido e oculto da interação.

   * No campo **[!UICONTROL Repetir senha]**, digite novamente a nova senha e, em seguida, toque em **[!UICONTROL Concluído.]**

1. No canto superior direito da página **[!UICONTROL Editar Configuração do Dynamic Media]**, toque em **[!UICONTROL Guardar]** e, em seguida, toque em **[!UICONTROL OK.]**

## (Opcional) Configuração de configurações avançadas no Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Se quiser personalizar ainda mais a configuração e configuração do Dynamic Media, ou otimizar seu desempenho, você pode concluir uma ou mais das seguintes tarefas *opcionais*:

* [Configuração e configuração das configurações do Dynamic Media](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Opcional) Ajuste do desempenho da Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### (Opcional) Configuração e configuração das configurações do Dynamic Media {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Use a interface do usuário do Dynamic Media Classic para fazer alterações nas configurações do Dynamic Media.

Algumas das tarefas acima exigem que você abra o [aplicativo Dynamic Media Classic desktop](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta.

As tarefas de configuração incluem:

* [Configuração de publicação para o Image Server](#publishing-setup-for-image-server)
* [Definição das configurações gerais do aplicativo](#configuring-application-general-settings)
* [Configuração do gerenciamento de cores](#configuring-color-management)
* [Edição de tipos MIME para formatos suportados](#editing-mime-types-for-supported-formats)
* [Adicionar tipos MIME para formatos não suportados](#adding-mime-types-for-unsupported-formats)

<!-- * [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Configuração de publicação para o Image Server {#publishing-setup-for-image-server}

As configurações de publicação determinam como os ativos são entregues por padrão da Dynamic Media. Se nenhuma configuração for especificada, a Dynamic Media fornece um ativo de acordo com as configurações padrão definidas na Configuração de publicação. Por exemplo, uma solicitação para fornecer uma imagem que não inclui um atributo de resolução gera uma imagem com a configuração Resolução de objeto padrão.

Para configurar a Configuração de publicação: no Dynamic Media Classic, clique em **[!UICONTROL Configuração > Configuração de aplicativo > Configuração de publicação > Servidor de imagem]**.

A tela Servidor de imagens estabelece as configurações padrão para a entrega de imagens. Consulte a tela da interface do usuário para obter a descrição de cada configuração.

**[!UICONTROL Atributos]**  de solicitação - essas configurações impõem limites às imagens que podem ser entregues do servidor.
**[!UICONTROL Atributos]**  de solicitação padrão - essas configurações pertencem à aparência padrão das imagens.
**[!UICONTROL Atributos]**  de miniatura comuns - Essas configurações pertencem à aparência padrão das imagens em miniatura.
**[!UICONTROL Padrões para campos]** de catálogo - Essas configurações pertencem à resolução e ao tipo de miniatura padrão das imagens.
**[!UICONTROL Atributos]**  de gerenciamento de cores: essas configurações determinam quais perfis de cores ICC são usados.
**[!UICONTROL Atributos]**  de compatibilidade - essa configuração permite que os parágrafos à esquerda e à direita em camadas de texto sejam tratados como na versão 3.6 para compatibilidade com versões anteriores.
**[!UICONTROL Suporte]**  à localização - Essas configurações permitem gerenciar vários atributos de localidade. Ela também permite que você especifique uma string de mapa de localidade para que você possa definir quais idiomas deseja suportar para as várias dicas de ferramentas nos Visualizadores. Para obter mais informações sobre como configurar **[!UICONTROL Suporte à Localização]**, consulte [Considerações ao configurar a localização de ativos](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets).

#### Definição das configurações gerais do aplicativo {#configuring-application-general-settings}

Para abrir a página Configurações gerais do aplicativo, na barra de navegação global do Dynamic Media Classic, clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais.]**

**[!UICONTROL Servidores]**  - Em provisionamento de conta, a Dynamic Media fornece automaticamente os servidores atribuídos para sua empresa. Esses servidores são usados para construir strings de URL para seu site e aplicativos. Essas chamadas de URL são específicas para sua conta. Não altere nenhum nome de servidor, a menos que seja explicitamente instruído a fazê-lo pelo suporte AEM.
**[!UICONTROL Substituir imagens]**  - o Dynamic Media não permite que dois arquivos tenham o mesmo nome. A ID do URL de cada item (o nome do arquivo menos a extensão) deve ser exclusiva. Essas opções especificam como os ativos de substituição são carregados: se eles substituem o original ou se tornam duplicados. Os ativos do duplicado são renomeados com um &quot;-1&quot; (por exemplo, o nome &quot;President.tif&quot; é renomeado como President-1.tif). Essas opções afetam os ativos carregados em uma pasta diferente do original ou os ativos com uma extensão de nome de arquivo diferente do original (como JPG, TIF ou PNG).
**[!UICONTROL Substituir na pasta atual, mesmo nome/extensão]**  da imagem base - Essa opção é a regra mais estrita para substituição. Ele requer que você carregue a imagem de substituição na mesma pasta que a original e que a imagem de substituição tenha a mesma extensão de nome de arquivo que a original. Se esses requisitos não forem atendidos, um duplicado será criado. Para manter a consistência com o AEM, sempre escolha **[!UICONTROL Substituir na pasta atual, o mesmo nome/extensão da imagem base]**.
**[!UICONTROL Substituir em qualquer pasta, o mesmo nome/extensão]**  do ativo básico - Requer que a imagem de substituição tenha a mesma extensão de nome de arquivo que a imagem original (por exemplo, o arquivo visit.jpg deve substituir o arquivo .jpg, não o domínio .tif). No entanto, é possível carregar a imagem de substituição para uma pasta diferente da original. A imagem atualizada reside na nova pasta; o arquivo não pode mais ser encontrado em seu local original.
**[!UICONTROL Substituir em qualquer pasta, o mesmo nome do ativo básico independentemente da extensão]**  - Essa opção é a regra de substituição mais inclusiva. Você pode carregar uma imagem de substituição para uma pasta diferente da original, carregar um arquivo com uma extensão de nome de arquivo diferente e substituir o arquivo original. Se o arquivo original estiver em uma pasta diferente, a imagem de substituição residirá na nova pasta para a qual foi carregada.
**[!UICONTROL Perfis]**  de cor padrão - Consulte  [Configuração do ](#configuring-color-management) gerenciamento de cores para obter mais informações. Por padrão, o sistema mostra 15 execuções ao selecionar **[!UICONTROL Representações]** e 15 predefinições do visualizador ao selecionar **[!UICONTROL Visualizadores]** na exibição detalhada do ativo. Você pode aumentar esse limite. Consulte [Aumentar ou diminuir o número de predefinições de imagens exibidas](/help/assets/dynamic-media/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) ou [Aumentar ou diminuir o número de predefinições do visualizador exibidas](/help/assets/dynamic-media/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### Configuração do gerenciamento de cores {#configuring-color-management}

O gerenciamento dinâmico de cores de mídia permite que você corrija ativos. Com a correção de cores, os ativos ingeridos retêm seu espaço de cores (RGB, CMYK, Cinza) e o perfil de cores incorporado. Quando você solicita uma representação dinâmica, a cor da imagem é corrigida no espaço de cor do público alvo usando a saída CMYK, RGB ou Gray. Consulte [Configuração de predefinições de imagens](/help/assets/dynamic-media/managing-image-presets.md).

Para configurar as propriedades de cor padrão para ativar a correção de cores ao solicitar imagens:

1. Abra o [aplicativo Dynamic Media Classic para desktop](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon na sua conta usando as credenciais fornecidas durante o provisionamento.
1. Navegue até **[!UICONTROL Configuração > Configuração de Aplicativo]**.
1. Expanda a área **[!UICONTROL Publicar configuração]** e selecione **[!UICONTROL Servidor de imagens]**. Defina **[!UICONTROL Publicar contexto]** como **[!UICONTROL Serviço de imagem]** ao definir padrões para instâncias de publicação.
1. Role até a propriedade que você precisa alterar, por exemplo, uma propriedade na área **[!UICONTROL Atributos de gerenciamento de cores]**.
É possível definir as seguintes propriedades de correção de cores:

   | Propriedade | Descrição |
   |---|---|
   | Espaço de cor padrão CMYK | Nome do perfil de cor CMYK padrão. |
   | Espaço de cor padrão em escala de cinza | Nome do perfil de cor cinza padrão. |
   | Espaço de cor padrão RGB | Nome do perfil de cor RGB padrão. |
   | Propósito de renderização da conversão de cores | Especifica o propósito de renderização. Os valores aceitáveis são: **[!UICONTROL perceptual]**, **[!UICONTROL colométrica relativa]**, **[!UICONTROL saturação]**, **[!UICONTROL colométrica absoluta.]** Adobe recomenda  **** como padrão. |

1. Toque em **[!UICONTROL Salvar]**.

Por exemplo, você pode definir o **[!UICONTROL Espaço de cor padrão RGB]** como *sRGB* e o **[!UICONTROL Espaço de cor padrão CMYK]** como *WebCoated*.

Isso faria o seguinte:

* Permite a correção de cores para imagens RGB e CMYK.
* Imagens RGB que não tenham um perfil colorido serão consideradas como estando no espaço de cores *sRGB*.
* Imagens CMYK que não têm um perfil colorido serão consideradas como estando em *WebCoated* espaço colorido.
* As representações dinâmicas que retornam a saída RGB retornarão no espaço de cores *sRGB*.
* As representações dinâmicas que retornam a saída CMYK retornarão no espaço de cores *WebCoated*.

#### Edição de tipos MIME para formatos suportados {#editing-mime-types-for-supported-formats}

Você pode definir quais tipos de ativos são processados pela Dynamic Media e personalizar parâmetros avançados de processamento de ativos. Por exemplo, você pode especificar parâmetros de processamento de ativos para fazer o seguinte:

* Converter um Adobe PDF em um ativo eCatalog.
* Converta um Documento Adobe Photoshop (.PSD) em um ativo de modelo de banner para personalização.
* Rasterize um arquivo Adobe Illustrator (.AI) ou um arquivo Adobe Photoshop Encapsulated Postscript (.EPS).
* [Os ](/help/assets/dynamic-media/video-profiles.md) Perfis de vídeo e os  [Perfis ](/help/assets/dynamic-media/image-profiles.md) de imagem podem ser usados para definir o processamento de vídeos e imagens, respectivamente.

Consulte [Upload de ativos](/help/assets/add-assets.md).

**Para editar os tipos MIME para formatos suportados**

1. Em AEM, clique no logotipo AEM para acessar o console de navegação global e clique em **[!UICONTROL Geral > CRXDE Lite]**.
1. No painel esquerdo, navegue até o seguinte:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![mimetypes](assets/mimetypes.png)

1. Na pasta mimeTypes, selecione um tipo mime.
1. No lado direito da página CRXDE Lite, na parte inferior:

   * Clique com o duplo no campo **[!UICONTROL enabled]**. Por padrão, todos os tipos MIME de ativos estão ativados (definidos como **[!UICONTROL true]**), o que significa que os ativos serão sincronizados com a Dynamic Media para processamento. Se desejar excluir esse tipo MIME de ativo do processamento, altere essa configuração para **[!UICONTROL false]**.

   * Clique com o duplo **[!UICONTROL jobParam]** para abrir o campo de texto associado. Consulte [Tipos MIME Suportados](/help/assets/file-format-support.md) para obter uma lista de valores de parâmetro de processamento permitidos que você pode usar para um determinado tipo MIME.

1. Faça uma das seguintes opções:
   * Repita as etapas de 3 a 4 para editar tipos MIME adicionais.
   * Na barra de menus da página CRXDE Lite, clique em **[!UICONTROL Salvar tudo.]**

1. No canto superior esquerdo da página, toque em **[!UICONTROL CRXDE Lite]** para retornar ao AEM.

#### Adicionar tipos MIME para formatos sem suporte {#adding-mime-types-for-unsupported-formats}

Adicione tipos MIME personalizados para formatos não compatíveis com o AEM Assets. Para garantir que qualquer novo nó adicionado no CRXDE Lite não seja excluído pelo AEM, certifique-se mover o tipo MIME antes de `image_` e que seu valor ativado seja definido como **[!UICONTROL false]**.

**Para adicionar tipos MIME para formatos não suportados**

1. No AEM, toque em **[!UICONTROL Ferramentas > Operações > Console Web.]**

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Uma nova guia do navegador é aberta na página **[!UICONTROL Configuração do Adobe Experience Manager Web Console]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Na página, role para baixo até o nome *Adobe CQ Scene7 Asset MIME type Service*, como visto na seguinte captura de tela. À direita do nome, toque em **[!UICONTROL Editar os valores]** de configuração (ícone de lápis).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. Na página **Adobe CQ Scene7 Asset MIME type Service**, clique em qualquer ícone de sinal de mais &lt;+>. O local na tabela onde você clica no sinal de mais para adicionar o novo tipo mime é trivial.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Digite `DWG=image/vnd.dwg` no campo de texto vazio que você acabou de adicionar.

   Observe que o exemplo `DWG=image/vnd.dwg` é apenas para fins ilustrativos. O tipo MIME que você adicionar aqui pode ser qualquer outro formato sem suporte.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. No canto inferior direito da página, toque em **[!UICONTROL Salvar]**.

   Nesse ponto, você pode fechar a guia do navegador que tem a página aberta Configuração do Adobe Experience Manager Web Console.

1. Retorne à guia do navegador que tem seu console AEM aberto.
1. Em AEM, toque em **[!UICONTROL Ferramentas > Geral > CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. No painel esquerdo, navegue até o seguinte:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Arraste o tipo mime `image_vnd.dwg` e solte-o diretamente acima de `image_` na árvore, conforme exibido na seguinte captura de tela.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Com o tipo mime `image_vnd.dwg` ainda selecionado, na guia **[!UICONTROL Propriedades]**, na linha **[!UICONTROL ativada]**, no cabeçalho da coluna **[!UICONTROL Valor]**, clique duas vezes no valor para abrir a lista suspensa **[!UICONTROL Valor]**.
1. Digite `false` no campo (ou selecione **[!UICONTROL false]** na lista suspensa).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Perto do canto superior esquerdo da página CRXDE Lite, clique em **[!UICONTROL Salvar tudo]**.



### (Opcional) Ajuste do desempenho do Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Para manter o Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> funcionando sem problemas, o Adobe recomenda as seguintes dicas de ajuste de desempenho/escalabilidade de sincronização:

* Atualização dos parâmetros de trabalho predefinidos para processamento de diferentes formatos de arquivo.
* Atualizando os threads de trabalho de fila do fluxo de trabalho Granite (ativos de vídeo) predefinidos.
* Atualizando os threads de trabalho de fila de transientes predefinidos do Granite (imagens e ativos que não sejam de vídeo).
* Atualização das conexões máximas de upload para o servidor Dynamic Media Classic.

#### Atualização dos parâmetros de trabalho predefinidos para processamento de diferentes formatos de arquivo

Você pode ajustar os parâmetros de trabalho para processamento mais rápido ao carregar arquivos. Por exemplo, se você estiver carregando arquivos PSD, mas não quiser processá-los como modelos, poderá definir a extração de camada como false (desligado). Nesse caso, o parâmetro de trabalho ajustado apareceria como `process=None&createTemplate=false`.

O Adobe recomenda usar os seguintes parâmetros de trabalho &quot;ajustados&quot; para arquivos PDF, Postscript e PSD:

| Tipo de arquivo | Parâmetros de tarefa recomendados |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| Postscript | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=Layername&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- To update any of these parameters, follow the steps in [Enabling MIME type-based Assets/Dynamic Media Classic upload job parameter support](#enabling-mime-type-based-assets-scene-upload-job-parameter-support). -->

#### Atualizando a fila do Fluxo de Trabalho Transitório do Granite {#updating-the-granite-transient-workflow-queue}

A fila Fluxo de trabalho de trânsito Granite é usada para o fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]**. No Dynamic Media, é usado para assimilação e processamento de imagens.

**Para atualizar a fila Fluxo de Trabalho Transitório do Granite**

1. Navegue até [https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr) e procure **Fila: Fila de Fluxo de Trabalho Transitório Granite**.

   >[!NOTE]
   >
   >Uma pesquisa de texto é necessária em vez de um URL direto, pois o PID do OSGi é gerado dinamicamente.

1. No campo **[!UICONTROL Máximo de trabalhos paralelos]**, altere o número para o valor desejado.

   Você pode aumentar **[!UICONTROL Máximo de trabalhos paralelos]** para suportar adequadamente o carregamento pesado de arquivos para a Dynamic Media. O valor exato depende da capacidade do hardware. Em certos cenários, ou seja, uma migração inicial ou um carregamento em massa único, é possível usar um valor grande. No entanto, esteja ciente de que o uso de um valor grande (como duas vezes o número de núcleos) pode ter efeitos negativos em outras atividades simultâneas. Dessa forma, você deve testar e ajustar o valor com base no seu caso de uso específico.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Toque em **[!UICONTROL Salvar]**.

#### Atualizando a fila do Fluxo de Trabalho do Granite {#updating-the-granite-workflow-queue}

A fila Fluxo de trabalho Granite é usada para workflows não transitórios. No Dynamic Media, costumava processar vídeos com o fluxo de trabalho **[!UICONTROL Codificar vídeo]** do Dynamic Media.

Para atualizar a fila do Fluxo de Trabalho de Granite:

1. Navegue até `https://<server>/system/console/configMgr` e procure **Fila: Fila de Fluxo de Trabalho Granite**.

   >[!NOTE]
   >
   >Uma pesquisa de texto é necessária em vez de um URL direto, pois o PID do OSGi é gerado dinamicamente.

1. No campo **[!UICONTROL Máximo de trabalhos paralelos]**, altere o número para o valor desejado.

   Por padrão, o número máximo de trabalhos paralelos depende do número de núcleos de CPU disponíveis. Por exemplo, em um servidor de 4 núcleos, atribui 2 processos de trabalho. (Um valor entre 0,0 e 1,0 é baseado em relação, ou qualquer número maior que 1 atribuirá o número de threads de trabalho.)

   Para a maioria dos casos de uso, a configuração padrão 0.5 é suficiente.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Toque em **[!UICONTROL Salvar]**.

#### Atualização da conexão de upload do Scene7 {#updating-the-scene-upload-connection}

A configuração Scene7 Upload Connection sincroniza AEM ativos aos servidores Dynamic Media Classic.

Para atualizar a conexão de upload do Scene7:

1. Vá até `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. No campo **[!UICONTROL Número de conexões]** e/ou no campo **[!UICONTROL Tempo limite do trabalho ativo]**, altere o número conforme desejado.

   A configuração **[!UICONTROL Número de conexões]** controla o número máximo de conexões HTTP permitidas para AEM upload do Dynamic Media; normalmente, o valor predefinido de 10 conexões é suficiente.

   A configuração **[!UICONTROL Tempo limite do trabalho ativo]** determina o tempo de espera para os ativos Dynamic Media carregados serem publicados no servidor de delivery. Esse valor é de 2100 segundos ou 35 minutos por padrão.

   Para a maioria dos casos de uso, a configuração de 2100 é suficiente.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Toque em **[!UICONTROL Salvar.]**

<!-- NOTE - OBSOLETE that customisations to replication agents to transform content are no longer used; the following content is obsolete now 

### (Optional) Filtering assets for replication {#optional-filtering-assets-for-replication}

In non-Dynamic Media deployments, you replicate *all* assets (both images and video) from your AEM author environment to the AEM publish node. This workflow is necessary because the AEM publish servers also deliver the assets.

However, in Dynamic Media deployments, because assets are delivered by way of the cloud service, there is no need to replicate those same assets to AEM publish nodes. Such a "hybrid publishing" workflow avoids extra storage costs and longer processing times to replicate assets. Other content, such as Site pages, continue to be served from the AEM publish nodes.

The filters provide a way for you to *exclude* assets from being replicated to the AEM publish node.

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

1. In AEM, tap the AEM logo to access the global navigation console and tap the **[!UICONTROL Tools > General > CRXDE Lite]**.
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

