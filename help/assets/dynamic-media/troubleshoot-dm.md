---
title: Solução de problemas do Dynamic Media
description: Saiba mais sobre como solucionar problemas de dicas que você pode experimentar ao trabalhar com imagens, conjuntos e visualizadores no Dynamic Media.
contentOwner: Rick Brough
feature: Troubleshooting,Image Sets,Viewers
role: Admin,User
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 1%

---

# Solução de problemas do Dynamic Media {#troubleshooting-dynamic-media-scene-mode}

O tópico a seguir descreve a solução de problemas do Dynamic Media.

## Nova configuração do Dynamic Media {#new-dm-config}

Consulte [Solucionar problemas de uma nova configuração do Dynamic Media](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config).

## Geral (Todos os Assets) {#general-all-assets}

Veja a seguir algumas dicas e truques gerais para todos os ativos.

### Propriedades do status de sincronização do ativo {#asset-synchronization-status-properties}

As seguintes propriedades de ativos podem ser revisadas no CRXDE Lite para confirmar a sincronização bem-sucedida do ativo do Adobe Experience Manager para o Dynamic Media:

| **Propriedade** | **Exemplo** | **Descrição** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a\|364266`** | Indicador geral de que o nó está vinculado ao Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** ou texto de erro | Status do upload do ativo para Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Deve ser preenchido para gerar URLs para ativo remoto do Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **sucesso** ou **falha:`<error text>`** | Status de sincronização de conjuntos (conjuntos de rotação, conjuntos de imagem e assim por diante), predefinições de imagem, predefinições do visualizador, atualizações de mapa de imagem para um ativo ou imagens que foram editadas. |

### Log de sincronização {#synchronization-logging}

Erros e problemas de sincronização registrados em `error.log` (diretório do servidor Experience Manager `/crx-quickstart/logs/`). Há logs suficientes disponíveis para determinar a causa raiz da maioria dos problemas. No entanto, você pode aumentar o log para DEBUG no pacote `com.adobe.cq.dam.ips` por meio do Console Sling ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) para coletar mais informações.

### Controle da versão {#version-control}

Ao substituir um ativo existente do Dynamic Media (mesmo nome e local), você pode manter ambos os ativos ou substituir/criar uma versão:

* Manter ambos cria um ativo com um nome exclusivo para o URL do ativo publicado. Por exemplo, `image.jpg` é o ativo original e `image1.jpg` é o ativo recém-carregado.

* A criação de uma versão não é compatível com o Dynamic Media. A nova versão substitui o ativo existente na entrega.

## Imagens e conjuntos {#images-and-sets}

Se tiver problemas com imagens e conjuntos, consulte a seguinte orientação de solução de problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Como depurar</strong></td>
   <td><strong>Solução</strong></td>
  </tr>
  <tr>
   <td>Não é possível acessar o botão copiar URL/Incorporar na exibição detalhada do ativo</td>
   <td>
    <ol>
     <li><p>Vá para CRX/DE:</p>
      <ul>
       <li>Verifique se a predefinição no JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> foi definida. Esse local se aplica se você atualizou do Experience Manager 6.x para o 6.4 e recusou a migração. Caso contrário, o local é <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Verifique se o ativo no JCR tem <code>dam:scene7FileStatus</code><strong> </strong>em Metadados exibidos como <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Atualizar página/navegar para outra página e voltar (o JSP do painel lateral deve ser recompilado)</p> <p>Se isso não funcionar:</p>
    <ul>
     <li>Publicar ativo.</li>
     <li>Recarregue o ativo e publique-o.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>O ponto de acesso do carrossel se move após alternar entre os slides</td>
   <td><p>Verifique se todos os slides são do mesmo tamanho.</p> </td>
   <td><p>Use somente imagens com o mesmo tamanho para o carrossel.</p> </td>
  </tr>
  <tr>
   <td>A imagem não é visualizada com o visualizador do Dynamic Media</td>
   <td><p>Verifique se o ativo contém <code>dam:scene7File</code> nas propriedades de Metadados (CRXDE Lite)</p> </td>
   <td><p>Verifique se o processamento de todos os ativos foi concluído.</p> </td>
  </tr>
  <tr>
   <td>O ativo carregado não é exibido no seletor de ativos</td>
   <td><p>Verificar se o ativo tem a propriedade <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Verifique se o processamento de todos os ativos foi concluído.</p> </td>
  </tr>
  <tr>
   <td>O banner na exibição de cartão mostra <strong>Novo</strong> quando o ativo não iniciou o processamento</td>
   <td>Verificar ativo <code>jcr:content</code> &gt; <code>dam:assetState</code> = se <code>unprocessed</code> ele não foi selecionado pelo fluxo de trabalho.</td>
   <td>Aguarde até que o ativo seja selecionado pelo fluxo de trabalho.</td>
  </tr>
  <tr>
   <td>As imagens ou conjuntos não exibem o URL do visualizador ou o código de inserção</td>
   <td>Verifique se a predefinição do visualizador foi publicada.</td>
   <td><p>Acesse <strong>Ferramentas</strong> &gt; <strong>Assets</strong> &gt; <strong>Predefinições do Visualizador</strong> e publique a predefinição do visualizador.</p> </td>
  </tr>
 </tbody>
</table>

## Vídeo {#video}

Se tiver problemas com o vídeo, consulte a seguinte orientação para solução de problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Como depurar</strong></td>
   <td><strong>Solução</strong></td>
  </tr>
  <tr>
   <td>O vídeo não pode ser visualizado</td>
   <td>
    <ul>
     <li>Verifique se a pasta tem um perfil de vídeo atribuído a ela (se um formato de arquivo não for compatível). Se não for compatível, somente uma imagem será exibida.</li>
     <li>O perfil de vídeo deve conter mais de uma predefinição de codificação para gerar um conjunto AVS (codificações únicas são tratadas como conteúdo de vídeo para arquivos MP4; para arquivos não compatíveis, são tratadas da mesma forma que não processadas).</li>
     <li>Verifique se o processamento do vídeo foi concluído confirmando <code>dam:scene7FileAvs</code> de <code>dam:scene7File</code> nos metadados.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Atribuir um perfil de vídeo à pasta.</li>
     <li>Editar perfil de vídeo para incluir mais de uma predefinição de codificação.</li>
     <li>Aguarde até que o vídeo termine o processamento.</li>
     <li>Antes de recarregar o vídeo, verifique se o fluxo de trabalho Codificação de Vídeo do Dynamic Media não está em execução.<br/> </li>
     <li>Recarregue o vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>O vídeo não está codificado</td>
   <td>
    <ul>
     <li>Verifique se o Dynamic Media Cloud Service está configurado.</li>
     <li>Verifique se um perfil de vídeo está associado à pasta de upload.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Verifique se a configuração do Dynamic Media em Cloud Services está definida corretamente.</li>
     <li>Verifique se a pasta tem um perfil de vídeo. Além disso, verifique o perfil do vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>O processamento de vídeo demora muito</td>
   <td><p>Para determinar se a codificação de vídeo ainda está em andamento ou se entrou em um estado de falha:</p>
    <ul>
     <li>Verifique o status do vídeo <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Representação de vídeo ausente</td>
   <td><p>Quando o vídeo for carregado, mas não houver representações codificadas:</p>
    <ul>
     <li>Verifique se a pasta tem um perfil de vídeo atribuído a ela.</li>
     <li>Verifique se o processamento do vídeo foi concluído confirmando <code>dam:scene7FileAvs</code> nos metadados.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Atribuir um perfil de vídeo à pasta.</li>
     <li>Aguarde a conclusão do processamento do vídeo.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visualizadores {#viewers}

Se tiver problemas com visualizadores, consulte as seguintes orientações para solução de problemas.

### Problema: as predefinições do visualizador não são publicadas {#viewers-not-published}

**Como depurar**

1. Vá para a página de diagnóstico do gerenciador de amostra: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`.
1. Observe os valores calculados. Ao operar corretamente, você verá o seguinte: `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`.

   >[!NOTE]
   >
   >Pode levar cerca de 10 minutos após a configuração das configurações de nuvem do Dynamic Media para que os ativos do visualizador sejam sincronizados.

1. Se os ativos desativados permanecerem, selecione um dos botões **Listar todos os Assets** desativados para ver os detalhes.

**Solução**

1. Navegar até a lista de predefinições do visualizador nas ferramentas administrativas: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. Selecione todas as predefinições do visualizador e selecione **Publicar**.
1. Volte para o gerenciador de amostra e observe que a contagem de ativos desativados agora é zero.

### Problema: o trabalho artístico predefinido do visualizador retorna 404 da Pré-visualização nos detalhes do ativo ou Copiar URL/Código incorporado {#viewer-preset-404}

**Como depurar**

No CRXDE Lite, faça o seguinte:

1. Navegue até a pasta `<sync-folder>/_CSS/_OOTB` na pasta de sincronização do Dynamic Media (por exemplo, `/content/dam/_CSS/_OOTB`).
1. Localize o nó de metadados do ativo problemático (por exemplo, `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`).
1. Verifique a presença de `dam:scene7*` propriedades. Se o ativo foi sincronizado e publicado com êxito, você vê que o conjunto `dam:scene7FileStatus` é para **PublishComplete**.
1. Tente solicitar o trabalho artístico diretamente da Dynamic Media, concatenando os valores das seguintes propriedades e literais de string:

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
Exemplo: `https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**Solução**

Se o trabalho artístico de ativos de amostra ou predefinição do visualizador não tiver sido sincronizado ou publicado, reinicie todo o processo de cópia/sincronização:

1. Navegue até CRXDE Lite.
1. Excluir `<sync-folder>/_CSS/_OOTB`.
1. Navegue até o CRX Package Manager: `https://localhost:4502/crx/packmgr/`.
1. Procure o pacote do visualizador na lista; ele começa com `cq-dam-scene7-viewers-content`.
1. Selecione **Reinstalar**.
1. Em Cloud Services, navegue até a página Configuração do Dynamic Media e abra a caixa de diálogo de configuração do Dynamic Media - S7.
1. Não fazer alterações, selecione **Salvar**.
Essa ação de salvar aciona a lógica novamente para criar e sincronizar os ativos de amostra, o CSS de predefinição do visualizador e o trabalho artístico.

### Problema: a Visualização da imagem não está sendo carregada na criação das predefinições do visualizador {#image-preview-not-loading}

**Solução**

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. No painel à esquerda, navegue até a pasta de conteúdo de amostra no seguinte local:

   `/content/dam/_DMSAMPLE`

1. Exclua a pasta `_DMSAMPLE`.
1. No painel à esquerda, navegue até a pasta de predefinições no seguinte local:

   `/conf/global/settings/dam/dm/presets/viewer`

1. Exclua a pasta `viewer`.
1. Próximo ao canto superior esquerdo da página do CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.
1. No canto superior esquerdo da página do CRXDE Lite, selecione o ícone **Voltar à página inicial**.
1. Recrie uma [Configuração do Dynamic Media nos Serviços de Nuvem](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
