---
title: Solução de problemas do Dynamic Media
description: Dicas de solução de problemas ao usar o Dynamic Media.
role: Admin,User
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
source-git-commit: a7152785e8957dcc529d1e2138ffc8c895fa5c29
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 1%

---

# Solução de problemas do Dynamic Media {#troubleshooting-dynamic-media-scene-mode}

O tópico a seguir descreve a solução de problemas para o Dynamic Media.

## Nova configuração do Dynamic Media {#new-dm-config}

Consulte [Solução de problemas de uma nova configuração do Dynamic Media](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config).

## Geral (Todos os Ativos) {#general-all-assets}

Veja a seguir algumas dicas e truques gerais para todos os ativos.

### Propriedades de status da sincronização de ativos {#asset-synchronization-status-properties}

As seguintes propriedades de ativos podem ser revisadas no CRXDE Lite para confirmar a sincronização bem-sucedida do ativo do Adobe Experience Manager para o Dynamic Media:

| **Propriedade** | **Exemplo** | **Descrição** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | Indicador geral de que o nó está vinculado ao Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** ou texto de erro | Status do upload do ativo para o Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Deve ser preenchido para gerar URLs para um ativo remoto do Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **success** ou **falhou:`<error text>`** | Status de sincronização de conjuntos (conjuntos de rotação, conjuntos de imagens e assim por diante), predefinições de imagens, predefinições do visualizador, atualizações de mapa de imagens para um ativo ou imagens que foram editadas. |

### Registro de sincronização {#synchronization-logging}

Erros e problemas de sincronização são registrados em log `error.log` Diretório do servidor do Experience Manager `/crx-quickstart/logs/`). O registro em log é suficiente para determinar a causa raiz da maioria dos problemas. No entanto, é possível aumentar o registro em DEBUG na `com.adobe.cq.dam.ips` do Sling Console ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) para coletar mais informações.

### Controle da versão {#version-control}

Ao substituir um ativo existente do Dynamic Media (mesmo nome e local), você pode manter ambos os ativos ou substituir/criar uma versão:

* Manter ambos cria um ativo com um nome exclusivo para o URL do ativo publicado. Por exemplo, `image.jpg` é o ativo original e `image1.jpg` é o ativo recém-carregado.

* A criação de uma versão não é compatível com o Dynamic Media. A nova versão substitui o ativo existente na entrega.

## Imagens e conjuntos {#images-and-sets}

Se tiver problemas com imagens e conjuntos, consulte as seguintes orientações de solução de problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Como depurar</strong></td>
   <td><strong>Solução</strong></td>
  </tr>
  <tr>
   <td>Não é possível acessar o URL de cópia/botão Incorporar na exibição de detalhes do ativo</td>
   <td>
    <ol>
     <li><p>Vá para CRX/DE:</p>
      <ul>
       <li>Verifique se a predefinição no JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> definido. Esse local se aplica se você tiver atualizado do Experience Manager 6.x para o 6.4 e recusou a migração. Caso contrário, o local será <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Verifique para garantir que o ativo no JCR tenha <code>dam:scene7FileStatus</code><strong> </strong>em Metadados é exibido como <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Atualizar página/navegar para outra página e retornar (o JSP do painel lateral deve ser recompilado)</p> <p>Se isso não funcionar:</p>
    <ul>
     <li>Publicar ativo.</li>
     <li>Faça o upload do ativo novamente e o publique.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>O hotspot carrossel se move após alternar entre slides</td>
   <td><p>Verifique se todos os slides têm o mesmo tamanho.</p> </td>
   <td><p>Use apenas imagens com o mesmo tamanho para o carrossel.</p> </td>
  </tr>
  <tr>
   <td>A imagem não é visualizada com o visualizador do Dynamic Media</td>
   <td><p>Verifique se o ativo contém <code>dam:scene7File</code> nas propriedades Metadados (CRXDE Lite)</p> </td>
   <td><p>Verifique se todos os ativos concluíram o processamento.</p> </td>
  </tr>
  <tr>
   <td>O ativo carregado não é exibido no seletor de ativos</td>
   <td><p>Verificar ativo tem propriedade <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Verifique se todos os ativos concluíram o processamento.</p> </td>
  </tr>
  <tr>
   <td>Banner na exibição de cartão <strong>Novo</strong> quando o ativo não iniciou o processamento</td>
   <td>Verificar ativo <code>jcr:content</code> &gt; <code>dam:assetState</code> = if <code>unprocessed</code> ele não foi selecionado pelo workflow.</td>
   <td>Aguarde até que o ativo seja selecionado por fluxo de trabalho.</td>
  </tr>
  <tr>
   <td>As imagens ou os conjuntos não exibem o URL do visualizador ou o código incorporado</td>
   <td>Verifique se a predefinição do visualizador foi publicada.</td>
   <td><p>Ir para <strong>Ferramentas</strong> &gt; <strong>Ativos</strong> &gt; <strong>Predefinições do visualizador</strong> e publicar a predefinição do visualizador.</p> </td>
  </tr>
 </tbody>
</table>

## Vídeo {#video}

Se tiver problemas com o vídeo, consulte as seguintes orientações para solução de problemas.

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
     <li>Verifique se a pasta tem um perfil de vídeo atribuído a ela (se não houver suporte no formato de arquivo). Se não houver suporte, somente uma imagem será exibida.</li>
     <li>O perfil de vídeo deve conter mais de uma predefinição de codificação para gerar um conjunto AVS (codificações únicas são tratadas como conteúdo de vídeo para arquivos MP4; para arquivos não suportados, tratados como não processados).</li>
     <li>Verifique se o vídeo terminou de ser processado confirmando <code>dam:scene7FileAvs</code> de <code>dam:scene7File</code> em metadados.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Atribua um perfil de vídeo à pasta.</li>
     <li>Edite o perfil de vídeo para incluir mais de uma predefinição de codificação.</li>
     <li>Aguarde até que o vídeo termine o processamento.</li>
     <li>Antes de recarregar o vídeo, verifique se o fluxo de trabalho Codificar vídeo do Dynamic Media não está em execução.<br/> </li>
     <li>Faça o upload novamente do vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>O vídeo não é codificado</td>
   <td>
    <ul>
     <li>Verifique se o Dynamic Media Cloud Service está configurado.</li>
     <li>Verifique se um perfil de vídeo está associado à pasta de upload.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Verifique se a Configuração do Dynamic Media em Cloud Services está configurada corretamente.</li>
     <li>Verifique se a pasta tem um perfil de vídeo. Além disso, verifique o perfil de vídeo.</li>
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
   <td><p>Quando o vídeo é carregado, mas não há representações codificadas:</p>
    <ul>
     <li>Verifique se a pasta tem um perfil de vídeo atribuído a ela.</li>
     <li>Verifique se o vídeo terminou de ser processado confirmando <code>dam:scene7FileAvs</code> em metadados.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Atribua um perfil de vídeo à pasta.</li>
     <li>Aguarde até que o vídeo termine o processamento.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Espectadores {#viewers}

Se tiver problemas com os visualizadores, consulte a seguinte orientação para solução de problemas.

### Problema: As predefinições do visualizador não são publicadas {#viewers-not-published}

**Como depurar**

1. Vá para a página de diagnóstico do gerenciador de exemplo: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`.
1. Observe valores calculados. Ao operar corretamente, você verá o seguinte: `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`.

   >[!NOTE]
   >
   >Pode levar cerca de 10 minutos após a configuração das configurações de nuvem do Dynamic Media para que os ativos do visualizador sejam sincronizados.

1. Se os ativos não ativados permanecerem, selecione uma das opções **Listar todos os ativos não ativados** botões para ver detalhes.

**Solução**

1. Navegue até a lista predefinida do visualizador nas ferramentas administrativas: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. Selecione todas as predefinições do visualizador e selecione **Publicar**.
1. Navegue de volta ao gerenciador de amostra e observe que a contagem de ativos não ativados agora é zero.

### Problema: A arte-final predefinida do visualizador retorna 404 da Visualização em detalhes do ativo ou Copiar URL/Incorporar código {#viewer-preset-404}

**Como depurar**

No CRXDE Lite, faça o seguinte:

1. Navegar para `<sync-folder>/_CSS/_OOTB` na pasta de sincronização do Dynamic Media (por exemplo, `/content/dam/_CSS/_OOTB`).
1. Encontre o nó de metadados do ativo problemático (por exemplo, `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`).
1. Verifique a presença de `dam:scene7*` propriedades. Se o ativo tiver sido sincronizado e publicado com êxito, você verá a variável `dam:scene7FileStatus` defina como **PublishComplete**.
1. Tente solicitar a arte-final diretamente do Dynamic Media concatenando os valores das seguintes propriedades e literais de string:

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
Exemplo: 
`https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**Solução**

Se os ativos de amostra ou a arte-final predefinida do visualizador não tiver sido sincronizada ou publicada, reinicie todo o processo de cópia/sincronização:

1. Navegue até o CRXDE Lite.
1. Excluir `<sync-folder>/_CSS/_OOTB`.
1. Navegue até o Gerenciador de Pacotes do CRX: `https://localhost:4502/crx/packmgr/`.
1. Procure o pacote do visualizador na lista; começa com `cq-dam-scene7-viewers-content`.
1. Selecionar **Reinstalar**.
1. Em Cloud Services, navegue até a página Configuração do Dynamic Media e abra a caixa de diálogo de configuração da sua configuração Dynamic Media - S7.
1. Não fazer alterações, selecione **Salvar**.
Essa ação de salvar aciona a lógica novamente para criar e sincronizar os ativos de amostra, o CSS predefinido do visualizador e a arte-final.

### Problema: A Visualização de imagem não está sendo carregada na criação de predefinições do visualizador {#image-preview-not-loading}

**Solução**

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e, em seguida, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. No painel à esquerda, navegue até a pasta de conteúdo de amostra no seguinte local:

   `/content/dam/_DMSAMPLE`

1. Exclua o `_DMSAMPLE` pasta.
1. No painel à esquerda, navegue até a pasta de predefinições no seguinte local:

   `/conf/global/settings/dam/dm/presets/viewer`

1. Exclua o `viewer` pasta.
1. Próximo ao canto superior esquerdo da página do CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.
1. No canto superior esquerdo da página do CRXDE Lite, selecione o **Página inicial** ícone .
1. Recrie um [Configuração do Dynamic Media no Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
