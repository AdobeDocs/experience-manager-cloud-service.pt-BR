---
title: Processar ativos usando manipuladores de mídia e Workflows
description: Saiba mais sobre vários manipuladores de mídia e como usá-los em workflows para executar tarefas em ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f2e257ff880ca2009c3ad6c8aadd055f28309289

---


# Processar ativos usando manipuladores de mídia e Workflows {#processing-assets-using-media-handlers-and-workflows}

Os ativos Adobe Experience Manager (AEM) vêm com um conjunto de workflows padrão e manipuladores de mídia para processar ativos. O fluxo de trabalho define as tarefas gerais a serem executadas nos ativos e, em seguida, delega as tarefas específicas aos manipuladores de mídia, por exemplo, geração de miniaturas ou extração de metadados.

É possível definir um fluxo de trabalho que será executado automaticamente quando um ativo de um tipo específico for carregado no servidor. As etapas de processamento são definidas em termos de uma série de manipuladores de mídia do AEM Assets. O AEM fornece alguns manipuladores [integrados,](#default-media-handlers) e outros podem ser desenvolvidos [](#creating-a-new-media-handler) personalizados ou definidos delegando o processo a uma ferramenta [de linha de](#command-line-based-media-handler)comando.

Os manipuladores de mídia são serviços dentro dos ativos AEM que executam ações específicas em ativos. Por exemplo, quando um arquivo de áudio MP3 é carregado no AEM, um fluxo de trabalho aciona um manipulador MP3 que extrai os metadados e gera uma miniatura. Geralmente, os manipuladores de mídia são usados em combinação com workflows. Os tipos MIME mais comuns são suportados no AEM. tarefas específicas podem ser executadas em ativos estendendo/criando workflows, estendendo/criando manipuladores de mídia ou desabilitando/habilitando manipuladores de mídia.

>[!NOTE]
>
>Consulte a página de formatos [suportados pelos](file-format-support.md) ativos para obter uma descrição de todos os formatos suportados pelos ativos AEM, bem como dos recursos suportados para cada formato.

## Manipuladores de mídia padrão {#default-media-handlers}

Os seguintes manipuladores de mídia estão disponíveis nos ativos AEM e lidam com os tipos MIME mais comuns:

<!-- TBD: Apply correct formatting once table is moved to MD.
-->

<table>
 <tbody>
  <tr>
   <td>Nome do manipulador</td>
   <td>Nome do serviço (no Console do sistema)</td>
   <td>Tipos MIME suportados</td>
  </tr>
  <tr>
   <td>TextHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.TextHandler</p> </td>
   <td>text/plain</td>
  </tr>
  <tr>
   <td>PdfHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pdf.PdfHandler</p> </td>
   <td><p>application/pdf<br /> application/illustrator</p> </td>
  </tr>
  <tr>
   <td>JpegHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.JpegHandler</p> </td>
   <td>image/jpeg</td>
  </tr>
  <tr>
   <td>Mp3Handler</td>
   <td><p>com.day.cq.dam.handler.standard.mp3.Mp3Handler</p> </td>
   <td><p>audio/mpeg</p> </td>
  </tr>
  <tr>
   <td>ZipHandler</td>
   <td><p>com.day.cq.dam.handler.standard.zip.ZipHandler</p> </td>
   <td><p>application/java-archive</p> <p>application/zip</p> </td>
  </tr>
  <tr>
   <td>PictHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pict.PictHandler</p> </td>
   <td><p>image/pict</p> </td>
  </tr>
  <tr>
   <td>StandardImageHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.StandardImageHandler</p> </td>
   <td><p>image/gif</p> <p>image/png</p> <p>aplicativo/photoshop</p> <p>image/jpeg</p> <p>image/tiff</p> <p>image/x-ms-bmp</p> <p>image/bmp</p> </td>
  </tr>
  <tr>
   <td>MSOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler</td>
   <td>application/msword<br /> </td>
  </tr>
  <tr>
   <td>MSPowerPointHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler</td>
   <td>application/vnd.ms-powerpoint<br /> </td>
  </tr>
  <tr>
   <td>OpenOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler</td>
   <td>application/vnd.openxmlformats-officedocument.wordprocessingml.documento<br /> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet<br /> application/vnd.openxmlformats-officedocument.presentationml.apresentação<br /><br /> </td>
  </tr>
  <tr>
   <td>EPubHandler</td>
   <td>com.day.cq.dam.handler.standard.epub.EPubHandler</td>
   <td>application/epub+zip</td>
  </tr>
  <tr>
   <td>GenericAssetHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.GenericAssetHandler</p> </td>
   <td>fallback caso nenhum outro manipulador tenha sido encontrado para extrair dados de um ativo</td>
  </tr>
 </tbody>
</table>

Todos os manipuladores executam as seguintes tarefas:

* extrair todos os metadados disponíveis do ativo.
* criação de uma imagem em miniatura fora do ativo.

É possível visualização dos manipuladores de mídia ativos:

1. No navegador, navegue até `http://localhost:4502/system/console/components`.
1. Clique no link `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. Uma lista com todos os manipuladores de mídia ativos é exibida.

## Uso de manipuladores de mídia em Workflows para executar tarefas em ativos {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

Os manipuladores de mídia são serviços normalmente usados em combinação com workflows.

O AEM tem alguns workflows padrão para processar ativos. Para visualização, abra o console Fluxo de trabalho e clique na guia **[!UICONTROL Modelos]** : os títulos de fluxo de trabalho que são start com os ativos AEM são os ativos específicos.

workflows existentes podem ser estendidos e novos podem ser criados para processar ativos de acordo com requisitos específicos.

O exemplo a seguir mostra como aprimorar o fluxo de trabalho de **[!UICONTROL Sincronização do AEM Assets]** para que os ativos secundários sejam gerados para todos os ativos, exceto documentos PDF.

### Desabilitando/habilitando um manipulador de mídia {#disabling-enabling-a-media-handler}

Os manipuladores de mídia podem ser desativados ou ativados por meio do Console de gerenciamento da Web do Apache Felix. Quando o manipulador de mídia está desativado, suas tarefas não são executadas nos ativos.

Para ativar/desativar um manipulador de mídia:

1. No navegador, navegue até `https://<host>:<port>/system/console/components`.
1. Clique em **[!UICONTROL Desativar]** ao lado do nome do manipulador de mídia. Por exemplo: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Atualize a página: um ícone é exibido ao lado do manipulador de mídia indicando que ele está desativado.
1. Para ativar o manipulador de mídia, clique em **[!UICONTROL Ativar]** ao lado do nome do manipulador de mídia.

### Criação de um novo Media Handler {#creating-a-new-media-handler}

Para suportar um novo tipo de mídia ou para executar tarefas específicas em um ativo, é necessário criar um novo manipulador de mídia. Esta seção descreve como proceder.

#### Classes e interfaces importantes {#important-classes-and-interfaces}

A melhor maneira de start de uma implementação é herdar de uma implementação abstrata fornecida que cuida da maioria das coisas e fornece um comportamento padrão razoável: a `com.day.cq.dam.core.AbstractAssetHandler` classe.

Essa classe já fornece um descritor de serviço abstrato. Portanto, se você herdar desta classe e usar o plug-in maven-sling-sling, certifique-se de definir o sinalizador de herança como `true`.

Implemente os seguintes métodos:

* `extractMetadata()`: extrai todos os metadados disponíveis.
* `getThumbnailImage()`: cria uma imagem em miniatura do ativo passado.
* `getMimeTypes()`: retorna os tipos MIME do ativo.

Este é um modelo de exemplo:

`package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts } `

A interface e as classes incluem:

* `com.day.cq.dam.api.handler.AssetHandler` interface: Esta interface descreve o serviço que adiciona suporte para tipos MIME específicos. A adição de um novo tipo MIME requer a implementação dessa interface. A interface contém métodos para importar e exportar os documentos específicos, para criar miniaturas e extrair metadados.
* `com.day.cq.dam.core.AbstractAssetHandler` classe: Essa classe serve como base para todas as outras implementações do manipulador de ativos e fornece funcionalidade comum.
* classe `com.day.cq.dam.core.AbstractSubAssetHandler`:
   * Essa classe serve como base para todas as outras implementações do manipulador de ativos e fornece a funcionalidade comum usada, além da funcionalidade usada frequentemente na extração de ativos secundários.
   * A melhor maneira de start de uma implementação é herdar de uma implementação abstrata fornecida que cuida da maioria das coisas e fornece um comportamento padrão razoável: a classe com.day.cq.dam.core.AbstractAssetHandler.
   * Essa classe já fornece um descritor de serviço abstrato. Portanto, se você herdar desta classe e usar o plug-in maven-sling-sling, certifique-se de definir o sinalizador de herança como verdadeiro.

É necessário implementar os seguintes métodos:

* `extractMetadata()`: este método extrai todos os metadados disponíveis.
* `getThumbnailImage()`: esse método cria uma imagem em miniatura do ativo passado.
* `getMimeTypes()`: este método retorna o(s) tipo(s) MIME do ativo.

Este é um modelo de exemplo:

empacotar my.own.stuff /&amp;ast;&amp;ast; &amp;ast; @scr.component hereit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ classe pública MyMediaHandler estende com.day.cq.dam.core.AbstractAssetHandler { // implementar as partes relevantes }

A interface e as classes incluem:

* `com.day.cq.dam.api.handler.AssetHandler` interface: Esta interface descreve o serviço que adiciona suporte para tipos MIME específicos. A adição de um novo tipo MIME requer a implementação dessa interface. A interface contém métodos para importar e exportar os documentos específicos, para criar miniaturas e extrair metadados.
* `com.day.cq.dam.core.AbstractAssetHandler` classe: Essa classe serve como base para todas as outras implementações do manipulador de ativos e fornece funcionalidade comum.
* `com.day.cq.dam.core.AbstractSubAssetHandler` classe: Essa classe serve como base para todas as outras implementações do manipulador de ativos e fornece funcionalidade comum usada, além da funcionalidade usada comum para a extração de subativos.

<!--
#### Example: create a specific Text Handler {#example-create-a-specific-text-handler}

In this section, you will create a specific Text Handler that generates thumbnails with a watermark.

Proceed as follows:

Refer to [Development Tools](../sites-developing/dev-tools.md) to install and set up Eclipse with a Maven plugin and for setting up the dependencies that are needed for the Maven project.

After you perform the following procedure, when you upload a txt file into AEM, the file's metadata are extracted and two thumbnails with a watermark are generated.

1. In Eclipse, create `myBundle` Maven project:

    1. In the Menu bar, click **[!UICONTROL File > New > Other]**.
    1. In the dialog, expand the Maven folder, select Maven Project and click **[!UICONTROL Next]**.
    1. Check the Create a simple project box and the Use default Workspace locations box, then click **[!UICONTROL Next]**.
    1. Define the Maven project:

        * Group Id: com.day.cq5.myhandler
        * Artifact Id: myBundle
        * Name: My AEM bundle
        * Description: This is my AEM bundle

    1. Click **[!UICONTROL Finish]**.

1. Set the Java Compiler to version 1.5:

    1. Right-click the `myBundle` project, select Properties.
    1. Select Java Compiler and set following properties to 1.5:

        * Compiler compliance level
        * Generated .class files compatibility
        * Source compatibility

    1. Click **[!UICONTROL OK]**. In the dialog window, click Yes.

1. Replace the code in the pom.xml file with the following code:

1. Create the package `com.day.cq5.myhandler` that contains the Java classes under `myBundle/src/main/java`:

    1. Under myBundle, right-click `src/main/java`, select New, then Package.
    1. Name it `com.day.cq5.myhandler` and click Finish.

1. Create the Java class `MyHandler`:

    1. In Eclipse, under `myBundle/src/main/java`, right-click the `com.day.cq5.myhandler` package, select New, then Class.
    1. In the dialog window, name the Java Class MyHandler and click Finish. Eclipse creates and opens the file MyHandler.java.
    1. In `MyHandler.java` replace the existing code with the following and then save the changes:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;

   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/

   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }

    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two white spaces in a row we dont want to double count
     // The starting of the document is always a whitespace
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a white space then we need to add one extra word
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compile the Java class and create the bundle:

    1. Right-click the myBundle project, select **[!UICONTROL Run As]**, then **[!UICONTROL Maven Install]**.
    1. The bundle `myBundle-0.0.1-SNAPSHOT.jar` (containing the compiled class) is created under `myBundle/target`.

1. In CRX Explorer, create a new node under `/apps/myApp`. Name = `install`, Type = `nt:folder`.
1. Copy the bundle `myBundle-0.0.1-SNAPSHOT.jar` and store it under `/apps/myApp/install` (for example with WebDAV). The new text handler is now active in AEM.
1. In your browser, open the Apache Felix Web Management Console. Select the Components tab and disable the default text handler `com.day.cq.dam.core.impl.handler.TextHandler`.

-->

## Manipulador de Mídia Baseado em Linha de Comando {#command-line-based-media-handler}

O AEM permite que você execute qualquer ferramenta de linha de comando em um fluxo de trabalho para converter ativos (como ImageMagick) e adicionar a nova representação ao ativo. Você só precisa instalar a ferramenta de linha de comando no disco que hospeda o servidor AEM e adicionar e configurar uma etapa do processo ao fluxo de trabalho. O processo chamado `CommandLineProcess`, também permite filtrar de acordo com tipos MIME específicos e criar várias miniaturas com base na nova execução.

As seguintes conversões podem ser executadas e armazenadas automaticamente nos ativos AEM:

* Transformação de EPS e AI usando [ImageMagick](https://www.imagemagick.org/script/index.php) e [Ghostscript](https://www.ghostscript.com/)
* Transcodificação de vídeo FLV usando [FFmpeg](https://ffmpeg.org/)
* Codificação MP3 usando [LAME](http://lame.sourceforge.net/)
* Processamento de áudio usando [SOX](http://sox.sourceforge.net/)

>[!NOTE]
>
>Em sistemas que não sejam Windows, a ferramenta FFMpeg retorna um erro ao gerar execuções para um ativo de vídeo que tem uma única citação (&#39;) no nome do arquivo. Se o nome do arquivo de vídeo incluir uma única citação, remova-a antes de carregá-la para o AEM.

O `CommandLineProcess` processo executa as seguintes operações na ordem em que são listadas:

* Filtros o arquivo de acordo com tipos MIME específicos, se especificado.
* Cria um diretório temporário no disco que hospeda o servidor AEM.
* Transmite o arquivo original para o diretório temporário.
* Executa o comando definido pelos argumentos da etapa. O comando está sendo executado no diretório temporário com as permissões do usuário que está executando o AEM.
* Transmite o resultado de volta para a pasta de execução do servidor AEM.
* Exclui o diretório temporário.
* Cria miniaturas com base nessas execuções, se especificado. O número e as dimensões das miniaturas são definidos pelos argumentos da etapa.

### Um exemplo usando o ImageMagick {#an-example-using-imagemagick}

O exemplo a seguir mostra como configurar a etapa do processo da linha de comando para que cada vez que um ativo com o tipo mime gif ou tiff for adicionado a /content/dam no servidor AEM, uma imagem invertida do original seja criada junto com três miniaturas adicionais (140x100, 48x48 e 10x250).

Para fazer isso, você usará o ImageMagick. O ImageMagick é um conjunto de software gratuito para criar, editar e compor imagens de bitmap e geralmente é usado da linha de comando.

Primeiro instale o ImageMagick no disco que hospeda o servidor AEM:

1. Instale o ImageMagick: consulte a documentação [do](https://www.imagemagick.org/script/download.php)ImageMagick.
1. Configure a ferramenta para que você possa executar a conversão na linha de comando.
1. Para ver se a ferramenta está instalada corretamente, execute o seguinte comando `convert -h` na linha de comando.

   Ele exibe uma tela de ajuda com todas as opções possíveis da ferramenta de conversão.

   >[!NOTE]
   >
   >Em algumas versões do Windows (por exemplo, Windows SE), o comando de conversão pode falhar ao ser executado porque está em conflito com o utilitário de conversão nativo que faz parte da instalação do Windows. Nesse caso, mencione o caminho completo do utilitário ImageMagick usado para converter arquivos de imagem em miniaturas. Por exemplo, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. Para ver se a ferramenta é executada corretamente, adicione uma imagem .jpg ao diretório de trabalho e execute o comando convert `<image-name>.jpg -flip <image-name>-flipped.jpg` na linha de comando.

   Uma imagem virada é adicionada ao diretório.

Em seguida, adicione a etapa do processo da linha de comando ao fluxo de trabalho **[!UICONTROL Atualizar ativo do DAM]**:

1. Vá para o console **[!UICONTROL Fluxo de trabalho]** .
1. Na guia **[!UICONTROL Modelos]** , edite o modelo **[!UICONTROL DAM Update Asset (Atualizar ativo]** DAM).
1. Altere as configurações da etapa de execução **[!UICONTROL ativada pela]** Web da seguinte maneira:

   **Argumentos**:

   `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

1. Salve o fluxo de trabalho.

Para testar o fluxo de trabalho modificado, adicione um ativo ao `/content/dam`.

1. No sistema de arquivos, obtenha uma imagem .tiff de sua escolha. Renomeie-o para `myImage.tiff` e copie-o para `/content/dam`, por exemplo, usando WebDAV.
1. Vá para o console **[!UICONTROL CQ5 DAM]** , por exemplo `http://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Abra o ativo **[!UICONTROL myImage.tiff]** e verifique se a imagem invertida e as três miniaturas foram criadas.

#### Configurando a Etapa do Processo CommandLineProcess {#configuring-the-commandlineprocess-process-step}

Esta seção descreve como definir os **Argumentos de processo** do **CommandLineProcess**.

Os valores dos Argumentos **de** Processo devem ser separados por uma vírgula e não devem ser start com um espaço em branco.

<table>
 <tbody>
  <tr>
   <td> Formato do argumento</td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td> mime:&lt;mime-type&gt;</td>
   <td><p>Argumento opcional. O processo é aplicado se o ativo tiver o mesmo tipo MIME do argumento.</p> <p>Vários tipos MIME podem ser definidos.</p> </td>
  </tr>
  <tr>
   <td> tn:&lt;largura&gt;:&lt;altura&gt;</td>
   <td><p>Argumento opcional. O processo cria uma miniatura com as dimensões definidas no argumento.</p> <p>Várias miniaturas podem ser definidas.<br /> </p> </td>
  </tr>
  <tr>
   <td> cmd: &lt;comando&gt;</td>
   <td><p>Define o comando que será executado. A sintaxe depende da ferramenta de linha de comando.</p> <p>Somente um comando pode ser definido.</p> <p>As variáveis a seguir podem ser usadas para criar o comando:<br/></p> <p><code>${filename}</code>: nome do arquivo de entrada, por exemplo, ‘original.jpg`<br/><code>${file}</code>: nome completo do caminho do arquivo de entrada, por exemplo, "/tmp/cqdam0816.tmp/original.jpg`<br/><code>${directory}</code>: diretório do arquivo de entrada, por exemplo "/tmp/cqdam0816.tmp".<br/> <code>${basename}</code>: nome do arquivo de entrada sem sua extensão, por exemplo, original<br/> <code>${extension}</code>: extensão do arquivo de entrada, por exemplo JPG<br/></p></td>
  </tr>
 </tbody>
</table>

Por exemplo, se ImageMagick estiver instalado no disco que hospeda o servidor AEM e se você criar uma etapa do processo usando **CommandLineProcess** como Implementação e os seguintes valores como Argumentos **de** Processo:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

então, quando o fluxo de trabalho é executado, a etapa se aplica somente aos ativos que têm image/gif ou mime:image/tiff como mime-types, cria uma imagem invertida do original, a converte em .jpg e cria três miniaturas que têm as dimensões: 140 x 100, 48 x 48 e 10 x 250.

Use os seguintes Argumentos **de** Processo para criar as três miniaturas padrão usando o ImageMagick:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Use os seguintes Argumentos **de** Processo para criar a execução ativada pela Web usando o ImageMagick:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>A etapa **CommandLineProcess** se aplica somente aos Ativos (nós do tipo `dam:Asset`) ou descendentes de um Ativo.
