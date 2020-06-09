---
title: Configuração do serviço Dynamic Media Cloud
description: Informações sobre como configurar o Dynamic Media no Adobe Experience Manager Cloud Service.
translation-type: tm+mt
source-git-commit: 668908770505b24eae4652106471925d1dcfc18b
workflow-type: tm+mt
source-wordcount: '5123'
ht-degree: 9%

---


# Sobre a configuração do serviço Dynamic Media Cloud {#configuring-dynamic-media-scene-mode}

Se você usar a configuração do Adobe Experience Manager para ambientes diferentes, como um para desenvolvimento, um para armazenamento temporário e outro para produção ao vivo, precisará configurar os Serviços da Dynamic Media Cloud para cada um desses ambientes.

## Diagrama de arquitetura do Dynamic Media {#architecture-diagram-of-dynamic-media-scene-mode}

O diagrama de arquitetura a seguir descreve como o Dynamic Media funciona.

Com a nova arquitetura, o AEM é responsável por ativos principais e sincronizações com o Dynamic Media para processamento e publicação de ativos:

1. Quando o ativo mestre é carregado no AEM, ele é replicado para o Dynamic Media. Nesse ponto, o Dynamic Media lida com todo o processamento de ativos e geração de representação, como codificação de vídeo e variantes dinâmicas de uma imagem.
1. Depois que as renderizações são geradas, o AEM pode acessar e pré-visualização com segurança as renderizações remotas do Dynamic Media (nenhum binário é enviado de volta à instância do AEM).
1. Depois que o conteúdo estiver pronto para ser publicado e aprovado, ele aciona o serviço de Mídia dinâmica para enviar conteúdo para os servidores de delivery e armazená-lo em cache no CDN.

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

## Configuração do serviço Dynamic Media Cloud {#configuring-dynamic-media-cloud-services}

**Antes de configurar o serviço** da Dynamic Media Cloud: Depois de receber seu email de provisionamento com credenciais do Dynamic Media, você deve [fazer logon](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) no Dynamic Media Classic para alterar sua senha. A senha fornecida no email de provisionamento é gerada pelo sistema e deve ser apenas uma senha temporária. É importante que você atualize a senha para que o Serviço da Dynamic Media Cloud seja configurado com as credenciais corretas.

Para configurar os serviços de nuvem de mídia dinâmica:

1. No AEM, toque no logotipo do AEM para acessar o console de navegação global.
1. No lado esquerdo do console, no cabeçalho **[!UICONTROL Ferramentas]**, toque em **[!UICONTROL Serviços da nuvem > Configuração do Dynamic Media]**.
1. Na página Navegador de configuração do Dynamic Media, no painel à esquerda, toque em **[!UICONTROL global]** (não toque ou selecione o ícone de pasta à esquerda de **[!UICONTROL global]**) e, em seguida, toque em **[!UICONTROL Criar]**.
1. Na página Criar configuração de mídia dinâmica, digite um título, o endereço de email da conta do Dynamic Media, a senha e selecione sua região. Eles são fornecidos pela Adobe para você no email de provisionamento. Entre em contato com o suporte se você não recebeu essa solicitação.
1. Click **[!UICONTROL Connect to Dynamic Media]**.

   >[!NOTE]
   >
   >Depois de receber seu email de provisionamento com credenciais do Dynamic Media, [faça logon](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) no Dynamic Media Classic para alterar sua senha. A senha fornecida no email de provisionamento é gerada pelo sistema e deve ser apenas uma senha temporária. É importante atualizar a senha para que o serviço de nuvem do Dynamic Media seja configurado com as credenciais corretas.

1. Quando a conexão for bem-sucedida, você poderá definir o seguinte:

   * **[!UICONTROL Empresa]** - o nome da conta do Dynamic Media. É possível que você tenha várias contas de Dynamic Media para diferentes submarcas, divisões ou diferentes ambientes de preparo/produção.

   * **[!UICONTROL Caminho da pasta raiz da empresa]**

   * **[!UICONTROL Publicar ativos]** - você pode escolher entre as três opções a seguir:
      * **[!UICONTROL Imediatamente]** significa que quando os ativos são carregados, o sistema ingere os ativos e fornece o URL/Incorporado instantaneamente. Não há necessidade de intervenção do usuário para publicar ativos.
      * **[!UICONTROL Na Ativação]** , significa que você precisa publicar explicitamente o ativo primeiro antes de fornecer um URL/link Incorporado.
      * **[!UICONTROL Publicação]** seletiva significa que os ativos são publicados automaticamente apenas para pré-visualização segura e podem ser publicados explicitamente no AEM sem publicação no DMS7 para delivery no domínio público. No futuro, a Adobe aprimorará essa opção para publicar ativos no AEM e publicar ativos no Dynamic Media, mutuamente exclusivos entre si. Ou seja, você pode publicar ativos no DMS7 para poder usar recursos como Recorte inteligente ou representações dinâmicas. Ou, você pode publicar ativos exclusivamente no AEM para visualização; esses mesmos ativos não são publicados no DMS7 para delivery no domínio público.
   * **[!UICONTROL Servidor]** de Pré-visualização seguro - permite que você especifique o caminho do URL para o servidor de pré-visualização de representações seguras. Ou seja, depois que as renderizações são geradas, o AEM pode acessar e pré-visualização com segurança as renderizações remotas do Dynamic Media (nenhum binário é enviado de volta para a instância do AEM).
A menos que você tenha uma disposição especial para usar seu próprio servidor empresa ou um servidor especial, a Adobe Systems recomenda deixar essa configuração como especificado.

   * **[!UICONTROL Sincronizar todo o conteúdo]** - Selecionado por padrão. Desmarque essa opção se desejar incluir ou excluir seletivamente ativos da sincronização para o Dynamic Media. Desmarcar essa opção permite escolher entre os dois modos de sincronização de Dynamic Media a seguir:

   * **[!UICONTROL Modo de sincronização de Mídia dinâmica]**
      * **[!UICONTROL Ativado por padrão]** - a configuração é aplicada a todas as pastas por padrão, a menos que você marque uma pasta especificamente para exclusão. <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Desativado por padrão]** - a configuração não é aplicada a nenhuma pasta até que você marque explicitamente uma pasta selecionada para sincronização com o Dynamic Media.
Para marcar uma pasta selecionada para sincronização com o Dynamic Media, abra a página Propriedades da pasta de ativos. Tap the **[!UICONTROL Details]** tab, then from the **[!UICONTROL Dynamic Media sync mode]** drop-down list, choose from the following three options, then save tap **[!UICONTROL Save]**.
         * **[!UICONTROL Herdado]** - Nenhum valor de sincronização explícito na pasta; em vez disso, a pasta herda o valor de sincronização de uma de suas pastas ancestrais ou do modo padrão na configuração da nuvem. O status detalhado para herdado é exibido por meio de uma dica de ferramenta.
         * **[!UICONTROL Ativar para subpastas]** - Inclua tudo nesta subárvore para sincronização com o Dynamic Media. As configurações específicas da pasta substituem o modo padrão na configuração da nuvem.
         * **[!UICONTROL Desabilitado para subpastas]** - Exclua toda a subárvore da sincronização para o Dynamic Media.

   >[!NOTE]
   >
   >Não há suporte para o controle de versão no Dynamic Media. Além disso, a ativação atrasada se aplica somente se **[!UICONTROL Publicar ativos]** na página Editar configuração do Dynamic Media estiver definida como **[!UICONTROL Na ativação]** e, em seguida, somente até a primeira vez que o ativo for ativado.
   >
   >
   >Depois que um ativo é ativado, todas as atualizações são publicadas imediatamente no Delivery S7.

   ![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

1. Toque em **[!UICONTROL Salvar]**.
1. Para pré-visualização segura do conteúdo do Dynamic Media antes de ser publicado, é necessário &quot;permitir a lista&quot; da instância do autor do AEM para se conectar ao Dynamic Media:

   * Faça logon em sua conta do Dynamic Media Classic: [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html). Suas credenciais e logon foram fornecidos pela Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte Técnico.
   * Na barra de navegação próxima à parte superior direita da página, clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configuração de publicação > Servidor]** de imagem.

   * Na página de Publicação do Servidor de Imagens, na lista suspensa Contexto de Publicação, selecione **[!UICONTROL Testar Servidor]** de Imagens.
   * Para o Filtro de endereço do cliente, toque em **[!UICONTROL Adicionar]**.
   * Marque a caixa de seleção para ativar (ativar) o endereço e, em seguida, insira o endereço IP da instância do autor de AEM (não o IP do Dispatcher).
   * Clique em **[!UICONTROL Salvar]**.

Agora você terminou com a configuração básica; você está pronto para usar o Dynamic Media.

Se desejar personalizar ainda mais sua configuração, você pode, opcionalmente, concluir qualquer uma das tarefas em [Configuração de configurações avançadas no Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## (Opcional) Configuração das configurações avançadas no Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Se quiser personalizar ainda mais a configuração e configuração do Dynamic Media, ou otimizar seu desempenho, conclua uma ou mais das seguintes tarefas *opcionais* :

* [Configuração e configuração das configurações do Dynamic Media](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Opcional) Ajuste do desempenho do Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### (Opcional) Configuração e configuração das configurações do Dynamic Media {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Use a interface do usuário do Dynamic Media Classic (Scene7) para fazer alterações nas configurações do Dynamic Media.

Algumas das tarefas acima exigem que você faça logon no Dynamic Media Classic (Scene7) aqui: [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

As tarefas de configuração incluem:

* [Configuração de publicação para o Image Server](#publishing-setup-for-image-server)
* [Definição das configurações gerais do aplicativo](#configuring-application-general-settings)
* [Configuração do gerenciamento de cores](#configuring-color-management)
* [Configurar o processamento de ativos](#configuring-asset-processing)
* [Adicionar tipos MIME personalizados para formatos não suportados](#adding-custom-mime-types-for-unsupported-formats)
* [Criando predefinições de conjuntos de lotes para gerar automaticamente Conjuntos de imagens e Conjuntos de rotação](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)

#### Configuração de publicação para o Image Server {#publishing-setup-for-image-server}

As configurações de publicação determinam como os ativos são entregues por padrão a partir do Dynamic Media. Se nenhuma configuração for especificada, o Dynamic Media fornecerá um ativo de acordo com as configurações padrão definidas na Configuração de publicação. Por exemplo, uma solicitação para fornecer uma imagem que não inclui um atributo de resolução gera uma imagem com a configuração Resolução de objeto padrão.

Para configurar a Configuração de publicação: no Dynamic Media Classic, clique em **[!UICONTROL Configuração > Configuração de aplicativo > Configuração de publicação > Servidor]** de imagem.

A tela Servidor de imagens estabelece as configurações padrão para a entrega de imagens. Consulte a tela da interface do usuário para obter a descrição de cada configuração.

* **[!UICONTROL Atributos]** de solicitação - essas configurações impõem limites às imagens que podem ser entregues do servidor.
* **[!UICONTROL Atributos]** de solicitação padrão - essas configurações pertencem à aparência padrão das imagens.
* **[!UICONTROL Atributos]** de miniatura comuns - Essas configurações pertencem à aparência padrão das imagens em miniatura.
* **[!UICONTROL Padrões para campos]** de catálogo - Essas configurações pertencem à resolução e ao tipo de miniatura padrão das imagens.
* **[!UICONTROL Atributos]** de gerenciamento de cores - essas configurações determinam quais perfis de cores ICC são usados.
* **[!UICONTROL Atributos]** de compatibilidade - essa configuração permite que os parágrafos à esquerda e à direita em camadas de texto sejam tratados como na versão 3.6 para compatibilidade com versões anteriores.
* **[!UICONTROL Suporte]** à Localização - Essas configurações permitem gerenciar vários atributos de localidade. Ela também permite que você especifique uma string de mapa de localidade para que você possa definir quais idiomas deseja suportar para as várias dicas de ferramentas nos Visualizadores. Para obter mais informações sobre como configurar o suporte à **Localização]**, consulte [Considerações ao configurar a localização de ativos](https://help.adobe.com/en_US/scene7/using/WS997f1dc4cb0179f034e07dc31412799d19a-8000.html).

#### Definição das configurações gerais do aplicativo {#configuring-application-general-settings}

Para abrir a página Configurações gerais do aplicativo, na barra de navegação global do Dynamic Media Classic, clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações]** gerais.

* **[!UICONTROL Servidores]** - no provisionamento de conta, o Dynamic Media fornece automaticamente os servidores atribuídos para a sua empresa. Esses servidores são usados para construir strings de URL para seu site e aplicativos. Essas chamadas de URL são específicas para sua conta. Não altere nenhum nome de servidor, a menos que seja explicitamente instruído a fazê-lo pelo suporte do AEM.

* **[!UICONTROL Substituir imagens]** - o Dynamic Media não permite que dois arquivos tenham o mesmo nome. A ID do URL de cada item (o nome do arquivo menos a extensão) deve ser exclusiva. Essas opções especificam como os ativos de substituição são carregados: se eles substituem o original ou se tornam duplicados. Os ativos do Duplicado são renomeados com um &quot;-1&quot; (por exemplo, o nome &quot;President.tif&quot; é renomeado como President-1.tif). Essas opções afetam os ativos carregados em uma pasta diferente do original ou os ativos com uma extensão de nome de arquivo diferente do original (como JPG, TIF ou PNG).

* **[!UICONTROL Substituir na pasta atual, mesmo nome/extensão]** da imagem base - Essa opção é a regra mais estrita para substituição. Ele requer que você carregue a imagem de substituição na mesma pasta que a original e que a imagem de substituição tenha a mesma extensão de nome de arquivo que a original. Se esses requisitos não forem atendidos, um duplicado será criado.

   >[!NOTE]
   >
   >Para manter a consistência com o AEM, sempre escolha essa configuração: **Substituir na pasta atual, mesmo nome/extensão da imagem base**

* **[!UICONTROL Substituir em qualquer pasta, mesmo nome/extensão]** do ativo básico - Requer que a imagem de substituição tenha a mesma extensão de nome de arquivo que a imagem original (por exemplo, President.jpg deve substituir President.jpg, não President.tif). No entanto, é possível carregar a imagem de substituição para uma pasta diferente da original. A imagem atualizada reside na nova pasta; o arquivo não pode mais ser encontrado em seu local original
* **[!UICONTROL Substituir em qualquer pasta, o mesmo nome do ativo básico independentemente da extensão]** - Essa opção é a regra de substituição mais inclusiva. Você pode carregar uma imagem de substituição para uma pasta diferente da original, carregar um arquivo com uma extensão de nome de arquivo diferente e substituir o arquivo original. Se o arquivo original estiver em uma pasta diferente, a imagem de substituição residirá na nova pasta para a qual foi carregada.

* **[!UICONTROL Perfis]** de cor padrão - Consulte [Configuração do gerenciamento](#configuring-color-management) de cores para obter mais informações.

>[!NOTE]
>
>Por padrão, o sistema mostra 15 execuções ao selecionar **[!UICONTROL Representações]** e 15 predefinições do visualizador ao selecionar **[!UICONTROL Visualizadores]** na exibição detalhada do ativo. Você pode aumentar esse limite. Consulte [Aumentar ou diminuir o número de predefinições de imagens exibidas](/help/assets/dynamic-media/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) ou [Aumentar ou diminuir o número de predefinições do visualizador exibidas](/help/assets/dynamic-media/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).


#### Configuração do gerenciamento de cores {#configuring-color-management}

O gerenciamento dinâmico de cores de mídia permite que você corrija ativos. Com a correção de cores, os ativos ingeridos retêm seu espaço de cores (RGB, CMYK, Cinza) e o perfil de cores incorporado. Quando você solicita uma representação dinâmica, a cor da imagem é corrigida no espaço de cor do público alvo usando a saída CMYK, RGB ou Gray. See [Configuring Image Presets](/help/assets/dynamic-media/managing-image-presets.md).

Para configurar as propriedades de cor padrão para ativar a correção de cores ao solicitar imagens:

1. [Faça logon no Dynamic Media Classic](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) usando as credenciais fornecidas durante o provisionamento. Navegue até **[!UICONTROL Configuração > Configuração]** do aplicativo.
1. Expanda a área **[!UICONTROL Publicar configuração]** e selecione **[!UICONTROL Servidor de imagens]**. Defina **[!UICONTROL Publicar contexto]** como **[!UICONTROL Serviço de imagem]** ao definir padrões para instâncias de publicação.
1. Role até a propriedade que você precisa alterar, por exemplo, uma propriedade na área Atributos **[!UICONTROL de gerenciamento de]** cores.

   É possível definir as seguintes propriedades de correção de cores:

   * **[!UICONTROL Espaço]** de cor padrão CMYK - Nome do perfil de cor padrão CMYK
   * **[!UICONTROL Espaço]** de cor padrão em escala de cinza - Nome do perfil de cor cinza padrão
   * **[!UICONTROL Espaço]** de cor padrão RGB - Nome do perfil de cor RGB padrão
   * **[!UICONTROL Propósito]** de renderização da conversão de cores - Especifica o propósito de renderização. Acceptable values are: **[!UICONTROL perceptual]**, **[!UICONTROL relative colometric]**, **[!UICONTROL saturation]**, **[!UICONTROL absolute colometric]**. Adobe recommends **[!UICONTROL relative]]**as the default.

1. Toque em **[!UICONTROL Salvar]**.

Por exemplo, você pode definir o **[!UICONTROL Espaço de cor padrão RGB]** como *sRGB* e o **[!UICONTROL Espaço de cor padrão CMYK]** como *WebCoated*.

Isso faria o seguinte:

* Permite a correção de cores para imagens RGB e CMYK.
* Imagens RGB que não tenham um perfil colorido serão consideradas como estando no espaço de cores *sRGB* .
* Imagens CMYK que não têm um perfil colorido serão consideradas como estando no espaço de cores *WebCoated* .
* As renderizações dinâmicas que retornam a saída RGB retornarão no *sRGB *espaço de cor.
* As renderizações dinâmicas que retornam a saída CMYK retornarão no espaço de cores *WebCoated* .

#### Configurar o processamento de ativos {#configuring-asset-processing}

Você pode definir quais tipos de ativos devem ser processados pelo Dynamic Media e personalizar parâmetros avançados de processamento de ativos. Por exemplo, você pode especificar parâmetros de processamento de ativos para fazer o seguinte:

* Converta um Adobe PDF em um ativo eCatalog.
* Converta um Documento do Adobe Photoshop (.PSD) em um ativo de modelo de banner para personalização.
* Rasterize um arquivo do Adobe Illustrator (.AI) ou um arquivo Postscript encapsulado do Adobe Photoshop (.EPS).
* Observação: Perfis de vídeo e Perfis de imagem podem ser usados para definir o processamento de vídeos e imagens, respectivamente.

Consulte [Upload de ativos](/help/assets/add-assets.md).

**Para configurar o processamento de ativos**

1. No AEM, clique no logotipo do AEM para acessar o console de navegação global e, em seguida, clique em **[!UICONTROL Geral > CRXDE Lite]**.
1. No painel esquerdo, navegue até o seguinte:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![mimetypes](assets/mimetypes.png)

1. Na pasta mimeTypes, selecione um tipo mime.
1. No lado direito da página CRXDE Lite, na parte inferior:

   * Clique com o duplo no campo **[!UICONTROL ativado]** . Por padrão, todos os tipos MIME de ativos estão ativados (definidos como **[!UICONTROL true]**), o que significa que os ativos serão sincronizados com o Dynamic Media para processamento. Se desejar excluir esse tipo MIME de ativo do processamento, altere essa configuração para **[!UICONTROL false]**.

   * duplo-clique em **[!UICONTROL jobParam]** para abrir o campo de texto associado. Consulte Tipos [Mime](/help/assets/file-format-support.md) suportados para obter uma lista de valores de parâmetro de processamento permitidos que você pode usar para um determinado tipo mime.

1. Faça uma das seguintes opções:

   * Repita as etapas de 3 a 4 para editar tipos MIME adicionais.
   * Na barra de menus da página CRXDE Lite, clique em **[!UICONTROL Salvar tudo]**.

1. No canto superior esquerdo da página, toque em **[!UICONTROL CRXDE Lite]** para retornar ao AEM.

#### Adicionar tipos MIME personalizados para formatos não suportados {#adding-custom-mime-types-for-unsupported-formats}

Adicione tipos MIME personalizados para formatos não compatíveis com o AEM Assets. Para garantir que qualquer novo nó adicionado no CRXDE Lite não seja excluído pelo AEM, certifique-se mover o tipo MIME antes de `image_` e que seu valor ativado seja definido como **[!UICONTROL false]**.

**Para adicionar tipos MIME personalizados para formatos não suportados**

1. From AEM, tap **[!UICONTROL Tools > Operations > Web Console]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Uma nova guia do navegador é aberta na página Configuração **[!UICONTROL do console da Web do]** Adobe Experience Manager.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Na página, role para baixo até o nome *Adobe CQ Scene7 Asset MIME type Service*, como visto na seguinte captura de tela. À direita do nome, toque em **[!UICONTROL Editar os valores]** de configuração (ícone de lápis).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. Na página **Adobe CQ Scene7 Asset MIME type Service** , clique em qualquer ícone de sinal de mais &lt;+>. O local na tabela onde você clica no sinal de mais para adicionar o novo tipo mime é trivial.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Digite `DWG=image/vnd.dwg` o campo de texto vazio que acabou de ser adicionado.

   Observe que o exemplo `DWG=image/vnd.dwg` é apenas para fins ilustrativos. O tipo MIME que você adicionar aqui pode ser qualquer outro formato sem suporte.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. In the lower-right corner of the page, tap **[!UICONTROL Save]**.

   Nesse ponto, você pode fechar a guia do navegador que tem a página aberta Configuração do console da Web do Adobe Experience Manager.

1. Retorne à guia do navegador que tem seu console AEM aberto.
1. From AEM, tap **[!UICONTROL Tools > General > CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. No painel esquerdo, navegue até o seguinte:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Arraste o tipo mime `image_vnd.dwg` e solte-o diretamente acima `image_` na árvore, como visto na seguinte captura de tela.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Com o tipo mime `image_vnd.dwg` ainda selecionado, na guia **[!UICONTROL Propriedades]**, na linha **[!UICONTROL ativada]**, no cabeçalho da coluna **[!UICONTROL Valor]**, clique duas vezes no valor para abrir a lista suspensa **[!UICONTROL Valor]**.
1. Digite `false` o campo (ou selecione **[!UICONTROL false]** na lista suspensa).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Perto do canto superior esquerdo da página CRXDE Lite, clique em **[!UICONTROL Salvar tudo]**.

#### Criando predefinições de conjuntos de lotes para gerar automaticamente Conjuntos de imagens e Conjuntos de rotação {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

Use predefinições de conjuntos de lotes para automatizar a criação de conjuntos de imagens ou conjuntos de rotação enquanto os ativos são carregados para o Dynamic Media.

Primeiro, defina a convenção de nomenclatura para como os ativos devem ser agrupados em um conjunto. Em seguida, é possível criar uma predefinição de conjunto de lotes, que é um conjunto exclusivo de instruções autocontidas e nomeadas que define como construir o conjunto usando imagens que correspondem às convenções de nomenclatura definidas na fórmula predefinida.

Quando você carrega arquivos, o Dynamic Media cria automaticamente um conjunto com todos os arquivos que correspondem à convenção de nomenclatura definida nas predefinições ativas.

**Configuração da nomenclatura padrão**

Crie uma convenção de nomenclatura padrão que seja usada em qualquer fórmula predefinida de conjunto de lotes. A convenção de nomenclatura padrão selecionada na definição predefinida do conjunto de lotes pode ser tudo o que sua empresa precisa para gerar conjuntos em lote. Uma predefinição de conjunto de lotes é criada para usar a convenção de nomenclatura padrão definida. Você pode criar quantas predefinições de Conjunto de Lotes tiver convenções de nomenclatura alternativas e personalizadas, necessárias para um determinado conjunto de conteúdo, em casos em que haja uma exceção para a nomeação padrão definida pela empresa.

Embora a configuração de uma convenção de nomenclatura padrão não seja necessária para usar a funcionalidade predefinida de conjunto de lotes, as práticas recomendadas recomendam que você use a convenção de nomenclatura padrão para definir quantos elementos da convenção de nomenclatura você deseja agrupar em um conjunto, de modo a facilitar a criação de conjuntos de lotes.

Como alternativa, observe que você pode usar o Código **[!UICONTROL de]** Visualização sem campos de formulário disponíveis. Nessa visualização, você cria suas definições de convenção de nomenclatura totalmente usando expressões regulares.

Dois elementos estão disponíveis para definição, Correspondência e Nome básico. Esses campos permitem que você defina todos os elementos de uma convenção de nomenclatura e identifique a parte da convenção usada para nomear o conjunto no qual eles estão contidos. A convenção de nomenclatura individual de uma empresa pode utilizar uma ou mais linhas de definição para cada um desses elementos. Você pode usar quantas linhas desejar para sua definição exclusiva e agrupá-las em elementos distintos, como para a Imagem principal, o elemento Cor, o elemento Visualização alternativa e o elemento Amostra.

**Para configurar a nomeação padrão**

1. Faça logon em sua conta do Dynamic Media Classic (Scene7): [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Suas credenciais e logon foram fornecidos pela Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte Técnico.

1. Na barra de navegação próxima à parte superior da página, toque em **[!UICONTROL Configuração > Configuração do aplicativo > Predefinições do conjunto de lotes > Nomeação]** padrão.
1. Selecione **[!UICONTROL Exibir formulário]** ou **[!UICONTROL Exibir código]** para especificar como deseja exibir e inserir informações sobre cada elemento.

   Você pode marcar a caixa de seleção Código **[!UICONTROL de]** Visualização para visualização do valor de expressão comum ao lado das seleções de formulário. Você pode inserir ou alterar esses valores para ajudar a definir os elementos da convenção de nomenclatura, se a visualização de formulário limitar você por algum motivo. Se os valores não puderem ser analisados na visualização de formulário, os campos de formulário ficarão inativos.

   >[!NOTE]
   >
   >Campos de formulário desativados não executam nenhuma validação de que suas expressões normais estão corretas. Você verá os resultados da expressão regular que está criando para cada elemento após a linha de resultados. A expressão regular completa fica visível na parte inferior da página.

1. Expanda cada elemento conforme necessário e informe as convenções de nomenclatura que deseja usar.
1. Conforme necessário, execute um dos procedimentos a seguir:

   * Toque em **[!UICONTROL Adicionar]** para adicionar outra convenção de nomenclatura para um elemento.
   * Toque em **[!UICONTROL Remover]** para excluir uma convenção de nomenclatura para um elemento.

1. Faça uma das seguintes opções:

   * Toque em **[!UICONTROL Salvar como]** e digite um nome para a predefinição.
   * Toque em **[!UICONTROL Salvar]** se estiver editando uma predefinição existente.

**Criando uma predefinição de conjunto de lotes**

O Dynamic Media usa predefinições de conjuntos de lotes para organizar ativos em conjuntos de imagens (imagens alternativas, opções de cores, rotação 360) para exibição em visualizadores. As predefinições do conjunto de lotes são executadas automaticamente junto com os processos de upload de ativos no Dynamic Media.

Você pode criar, editar e gerenciar predefinições de conjuntos de lotes. Existem duas formas de definições predefinidas de conjuntos de lotes: uma para uma convenção de nomenclatura padrão que você pode ter configurado e outra para convenções de nomenclatura personalizadas que você cria dinamicamente.

Você pode usar o método de campo de formulário para definir uma predefinição de conjunto de lotes ou o método de código, que permite usar expressões regulares. Como em Nomenclatura padrão, você pode escolher Código de Visualização ao mesmo tempo que está definindo na Visualização de formulário e usar expressões comuns para criar suas definições. Como alternativa, você pode desmarcar qualquer visualização para usar uma ou a outra exclusivamente.

**Para criar uma predefinição de conjunto de lotes**

1. Faça logon em sua conta do Dynamic Media Classic (Scene7): [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Suas credenciais e logon foram fornecidos pela Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte Técnico.

1. Na barra de navegação próxima à parte superior da página, toque em **[!UICONTROL Configuração > Configuração do aplicativo > Predefinições do conjunto de lotes > Predefinição]** do conjunto de lotes.

   Observe que o Formulário **[!UICONTROL de]** Visualização, conforme definido no canto superior direito da página Detalhes, é a visualização padrão.

1. No painel Lista predefinida, toque em **[!UICONTROL Adicionar]** para ativar os campos de definição no painel Detalhes no lado direito da tela.
1. No painel Detalhes, no campo Nome da predefinição, digite um nome para a predefinição.
1. No menu suspenso Tipo de conjunto de lotes, selecione um tipo predefinido.
1. Faça uma das seguintes opções:

   * If you are using a default naming convention that you previously set up under **[!UICONTROL Application Setup > Batch Set Presets > Default Naming]**, expand **[!UICONTROL Asset Naming Conventions]**, and then in the File Naming drop-down list, tap **[!UICONTROL Default]**.

   * To define a new naming convention as you set up the preset, expand **[!UICONTROL Asset Naming Conventions]**, and then in the File Naming drop-down list, click **[!UICONTROL Custom]**.

1. Para ordem de sequência, defina a ordem em que as imagens são exibidas depois que o conjunto é agrupado no Dynamic Media.

   Por padrão, seus ativos são ordenados alfanuméricos. Entretanto, é possível usar uma lista separada por vírgulas de expressões regulares para definir a ordem.

1. Para Definir a Convenção de Nomeação e Criação, especifique o sufixo ou o prefixo para o nome básico definido na Convenção de Nomeação de Ativos. Além disso, defina onde o conjunto será criado na estrutura de pastas Mídia dinâmica.

   Se você definir grandes números de conjuntos, talvez prefira mantê-los separados das pastas que contêm os próprios ativos. Por exemplo, você pode criar uma pasta Conjuntos de imagens e colocar os conjuntos gerados aqui.

1. No painel Detalhes, toque em **[!UICONTROL Salvar]**.
1. Toque em **[!UICONTROL Ativo]** ao lado do novo nome predefinido.

   A ativação da predefinição garante que, ao carregar ativos para o Dynamic Media, a predefinição do conjunto de lotes seja aplicada para gerar o conjunto.

**Criando uma predefinição de conjunto de lotes para a geração automática de um conjunto de rotação 2D**

Você pode usar o Conjunto de Lotes Tipo Conjunto de Lotes Conjunto de **[!UICONTROL rotação de vários eixos]** para criar uma fórmula que automatize a geração de Conjuntos de rotação 2D. O agrupamento de imagens usa expressões regulares de Linha e Coluna para que os ativos de imagem sejam alinhados corretamente no local correspondente na matriz multidimensional. Não há um número mínimo ou máximo de linhas ou colunas que você deve ter em um conjunto de rotação de vários eixos.

Por exemplo, suponha que você queira criar um conjunto de rotação de vários eixos chamado `spin-2dspin`. Você tem um conjunto de imagens de conjunto de rotação que contém três linhas, com 12 imagens por linha. As imagens são nomeadas da seguinte forma:

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

Com essas informações, sua receita de Tipo de Conjunto de Lotes pode ser criada da seguinte maneira:

![chlimage_1-560](assets/chlimage_1-560.png)

O agrupamento para a parte do nome do ativo compartilhado do conjunto de rotação é adicionado ao campo **Correspondência** (como destacado). A parte variável do nome do ativo que contém a linha e a coluna é adicionada aos campos **Linha** e **Coluna**, respectivamente.

Quando o Conjunto de rotação é carregado e publicado, você ativaria o nome da fórmula do Conjunto de rotação 2D que está listada em **Predefinições de conjunto de lote** na caixa de diálogo **Opções de trabalho de upload**.

**Para criar uma predefinição de conjunto de lotes para a geração automática de um conjunto de rotação 2D**

1. Faça logon em sua conta do Dynamic Media Classic (Scene7): [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Suas credenciais e logon foram fornecidos pela Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte Técnico.

1. Na barra de navegação próxima à parte superior da página, clique em **[!UICONTROL Setup > Application Setup > Batch Set Presets > Batch Set Preset**.

   Observe que o Formulário **[!UICONTROL de]** Visualização, conforme definido no canto superior direito da página Detalhes, é a visualização padrão.

1. No painel Lista predefinida, clique em **[!UICONTROL Adicionar]** para ativar os campos de definição no painel Detalhes no lado direito da tela.
1. No painel Detalhes, no campo Nome da predefinição, digite um nome para a predefinição.
1. No menu suspenso Tipo de conjunto de lote, selecione **[!UICONTROL Conjunto de ativos]**.
1. Na lista suspensa Subtipo, selecione Conjunto de rotação de **[!UICONTROL vários eixos]**.
1. Expanda Convenções **[!UICONTROL de nomenclatura de]** ativos e, na lista suspensa Nomenclatura de arquivos, clique em **[!UICONTROL Personalizado]**.
1. Use os atributos **[!UICONTROL Correspondência]** e, opcionalmente, **[!UICONTROL Nome de base]** para definir uma expressão regular para nomear ativos de imagem que compõem o agrupamento.

   Por exemplo, sua expressão regular de Correspondência literal pode parecer com o seguinte:

   `(w+)-w+-w+`

1. Expanda a Posição **[!UICONTROL da Coluna da]** Linha e defina o formato do nome para a posição do ativo de imagem na matriz 2D do Conjunto de rotação.

   Use os parênteses para adotar a posição de linha ou coluna no nome do arquivo.

   Por exemplo, para a sua expressão regular de linha, ela pode parecer com o seguinte:

   `\w+-R([0-9]+)-\w+`

   ou

   `\w+-(\d+)-\w+`

   Para sua expressão regular de coluna, pode ser semelhante ao seguinte:

   `\w+-\w+-C([0-9]+)`

   ou

   `\w+-\w+-C(\d+)`

   Lembre-se de que esses são apenas exemplos. Você pode criar sua expressão normal da maneira que quiser, de acordo com suas necessidades.

   >[!NOTE]
   >
   >Se a combinação de expressões regulares de linha e coluna não puder determinar a posição do ativo dentro da matriz de fiação multidimensional, esse ativo não será adicionado ao conjunto e um erro será registrado.

1. Para Definir a Convenção de Nomeação e Criação, especifique o sufixo ou o prefixo para o nome básico definido na Convenção de Nomeação de Ativos.

   Além disso, defina onde o conjunto de rotação será criado na estrutura de pastas do Dynamic Media Classic.

   Se você definir grandes números de conjuntos, talvez prefira mantê-los separados das pastas que contêm os próprios ativos. Por exemplo, crie uma pasta Conjuntos de rotação para colocar os conjuntos gerados aqui.

1. No painel Detalhes, clique em **[!UICONTROL Salvar]**.
1. Clique em **[!UICONTROL Ativo]** ao lado do novo nome predefinido.

   A ativação da predefinição garante que, ao carregar ativos para o Dynamic Media, a predefinição do conjunto de lotes seja aplicada para gerar o conjunto.

### (Opcional) Ajuste do desempenho do Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Para manter o Dynamic Media em execução <!--(with `dynamicmedia_scene7` run mode)--> sem problemas, a Adobe recomenda as seguintes dicas de ajuste de desempenho/escalabilidade de sincronização:

* Atualização dos parâmetros de trabalho predefinidos para processamento de diferentes formatos de arquivo.
* Atualizando os threads de trabalho de fila do fluxo de trabalho Granite (ativos de vídeo) predefinidos.
* Atualizando os threads de trabalho de fila de trabalho temporário Granite predefinidos (imagens e ativos que não sejam de vídeo).
* Atualização das conexões máximas de upload para o servidor do Dynamic Media Classic.

#### Atualização dos parâmetros de trabalho predefinidos para processamento de diferentes formatos de arquivo

Você pode ajustar os parâmetros de trabalho para processamento mais rápido ao carregar arquivos. Por exemplo, se você estiver carregando arquivos PSD, mas não quiser processá-los como modelos, poderá definir a extração de camada como false (desligado). Nesse caso, o parâmetro de trabalho ajustado apareceria como `process=None&createTemplate=false`.

A Adobe recomenda usar os seguintes parâmetros de trabalho &quot;ajustados&quot; para arquivos PDF, Postscript e PSD:

| Tipo de arquivo | Parâmetros de tarefa recomendados |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| Postscript | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=Layername&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

Para atualizar qualquer um desses parâmetros, siga as etapas em [Habilitar o suporte](#enabling-mime-type-based-assets-scene-upload-job-parameter-support)ao parâmetro de trabalho de upload do Assets/Dynamic Media Classic baseado no tipo MIME.

#### Atualizando a fila Fluxo de Trabalho Transitório do Granite {#updating-the-granite-transient-workflow-queue}

A fila Fluxo de trabalho de trânsito Granite é usada para o fluxo de trabalho de Atualização de ativo **[!UICONTROL do]** DAM. No Dynamic Media, é usado para assimilação e processamento de imagens.

**Para atualizar a fila Fluxo de Trabalho Transitório do Granite**

1. Navegue até [https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr) e pesquise por **Fila: Fila** de Fluxo de Trabalho Transitório Granite.

   >[!NOTE]
   >
   >Uma pesquisa de texto é necessária em vez de um URL direto, pois o PID do OSGi é gerado dinamicamente.

1. No campo **[!UICONTROL Máximo de trabalhos]** paralelos, altere o número para o valor desejado.

   Por padrão, o número máximo de trabalhos paralelos depende do número de núcleos de CPU disponíveis. Por exemplo, em um servidor de 4 núcleos, atribui 2 processos de trabalho. (Um valor entre 0,0 e 1,0 é baseado em relação, ou qualquer número maior que 1 atribuirá o número de threads de trabalho.)

   A Adobe recomenda que 32 Tarefas **[!UICONTROL paralelas]** máximas sejam configuradas para suportar adequadamente o carregamento pesado de arquivos para o Dynamic Media Classic (Scene7).

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Toque em **[!UICONTROL Salvar]**.

#### Atualizando a fila Fluxo de Trabalho do Granite {#updating-the-granite-workflow-queue}

A fila Fluxo de trabalho Granite é usada para workflows não transitórios. No Dynamic Media, costumava processar vídeos com o fluxo de trabalho **[!UICONTROL Dynamic Media Encode Video]** .

**Para atualizar a fila Fluxo de Trabalho de Granite**

1. Navegue até `https://<server>/system/console/configMgr` e pesquise por **Fila: Fila** de Fluxo de Trabalho Granite.

   >[!NOTE]
   >
   >Uma pesquisa de texto é necessária em vez de um URL direto, pois o PID do OSGi é gerado dinamicamente.

1. No campo **[!UICONTROL Máximo de trabalhos]** paralelos, altere o número para o valor desejado.

   Por padrão, o número máximo de trabalhos paralelos depende do número de núcleos de CPU disponíveis. Por exemplo, em um servidor de 4 núcleos, atribui 2 processos de trabalho. (Um valor entre 0,0 e 1,0 é baseado em relação, ou qualquer número maior que 1 atribuirá o número de threads de trabalho.)

   Para a maioria dos casos de uso, a configuração padrão 0.5 é suficiente.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Toque em **[!UICONTROL Salvar]**.

#### Atualização da conexão de upload do Scene7 {#updating-the-scene-upload-connection}

A configuração Scene7 Upload Connection sincroniza os ativos AEM aos servidores do Dynamic Media Classic.

**Para atualizar a conexão de upload do Scene7**

1. Vá até `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. No campo **[!UICONTROL Número de conexões]** e/ou no campo Tempo limite **[!UICONTROL do trabalho]** Ativo, altere o número conforme desejado.

   A configuração **[!UICONTROL Número de conexões]** controla o número máximo de conexões HTTP permitidas para o upload do AEM para o Dynamic Media; normalmente, o valor predefinido de 10 conexões é suficiente.

   A configuração de tempo limite **[!UICONTROL do trabalho]** ativo determina o tempo de espera para que os ativos do Dynamic Media carregados sejam publicados no servidor do delivery. Esse valor é de 2100 segundos ou 35 minutos por padrão.

   Para a maioria dos casos de uso, a configuração de 2100 é suficiente.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Toque em **[!UICONTROL Salvar]**.

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

