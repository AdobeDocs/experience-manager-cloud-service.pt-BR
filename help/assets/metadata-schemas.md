---
title: Esquemas de metadados
description: O esquema de metadados define o layout da página de propriedades e as propriedades de metadados exibidas para ativos. Saiba como criar esquema de metadados personalizado, editar esquema de metadados e aplicar esquema de metadados a ativos.
contentOwner: AG
feature: Metadata
role: Business Practitioner,Administrator
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '2513'
ht-degree: 15%

---


# Esquemas de metadados {#metadata-schemas}

Nos ativos Adobe Experience Manager (AEM), um esquema de metadados define o layout da página de propriedades e as propriedades de metadados exibidas para ativos que usam o esquema específico. As propriedades dos metadados incluem título, descrição, tipos MIME, tags e assim por diante.

Você pode usar o editor de Forms do esquema de metadados para modificar esquemas existentes ou adicionar esquemas de metadados personalizados.

1. Para exibir a página de propriedades de um ativo, clique ou toque no ícone **[!UICONTROL Exibir propriedades]** de Ações rápidas no bloco de ativos na exibição Cartão. Como alternativa, selecione o ativo na interface do usuário e clique ou toque no ícone **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Edite várias propriedades de metadados em várias guias. No entanto, não é possível modificar o tipo de ativo na página de propriedades.
Para modificar o tipo MIME de um ativo, use um formulário de esquema de metadados personalizado ou modifique um formulário existente. Consulte [Editar o esquema de metadados Forms](#edit-metadata-schema-forms) para obter mais informações. Se você modificar o esquema de metadados para um determinado tipo MIME, o layout da página de propriedades para ativos com o tipo MIME atual e todos os subtipos de ativos serão modificados. Por exemplo, modificar um esquema jpeg em `default/image` modifica apenas o layout de metadados (propriedades de ativos) para ativos com o tipo MIME `image/jpeg`. No entanto, se você editar o esquema padrão, suas alterações modificarão o layout de metadados para todos os tipos de ativos.

1. Para exibir uma lista de formulários/modelos, clique no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**.
AEM fornece os seguintes modelos prontos para uso:

   * **padrão**: O formulário de esquema de metadados básico para ativos.

   Os seguintes formulários filho herdam as propriedades do formulário padrão:
i. **image**: Formulário de esquema para ativos com o tipo MIME &quot;imagem&quot;, por exemplo, `image/jpeg`, `image/png` e assim por diante.
O formulário &quot;image&quot; tem os seguintes modelos de formulário filho:
a. **jpeg**: Formulário de esquema para ativos com subtipo `jpeg`.
b. **tiff**: Formulário de esquema dos ativos com subtipo `tiff`.

   ii. **aplicativo**: Formulário de esquema para ativos com tipo MIME  `application`, por exemplo  `application/pdf`,  `application/zip`e assim por diante.
a. **pdf**: Formulário de esquema para ativos com subtipo `pdf`.

   iii. **Vídeo**: Formulário de esquema para ativos com tipo MIME  `video`, como  `video/avi`,  `video/mp4`, e assim por diante.

   * **coleção**: Formulário de esquema para coleções.
   * **contentfragment:** formulário de esquema dos Fragmentos de conteúdo.


>[!NOTE]
>
>Para exibir os formulários filho de um formulário de esquema, clique/toque no nome do formulário de esquema.

## Adicionar um formulário de esquema de metadados {#add-a-metadata-schema-form}

1. Para adicionar um modelo personalizado à lista, clique em **[!UICONTROL Create]** na barra de ferramentas.

   >[!NOTE]
   >
   >Os modelos não atualizados têm um ícone de cadeado antes deles. Se você personalizar qualquer um dos modelos, o ícone de bloqueio antes do modelo desaparece.

1. Na caixa de diálogo , insira o título do formulário Schema e clique em **[!UICONTROL Create]** para concluir o processo de criação do formulário.

## Editar formulários de esquema de metadados {#edit-metadata-schema-forms}

É possível editar um formulário de esquema de metadados recém-adicionado ou existente. O formulário de esquema de metadados inclui o seguinte:

* Guias
* Itens de formulário nas guias.

Você pode mapear/configurar esses itens de formulário em um campo dentro de um nó de metadados no repositório CRX.

É possível adicionar novas guias ou itens de formulário ao formulário de esquema de metadados. As guias e os itens de formulário derivados do pai estão no estado bloqueado. Não é possível alterá-los no nível filho.

1. Na página Formulários de esquema, marque a caixa de seleção ao lado de um formulário e clique no ícone **Editar** na barra de ferramentas.
1. Na página **[!UICONTROL Editor de esquema de metadados]**, personalize a página de propriedades do ativo arrastando um ou mais componentes da lista de tipos de componentes na guia **[!UICONTROL Criar formulário]** para a guia **[!UICONTROL Básico]**.
1. Para configurar um componente, selecione-o e modifique suas propriedades na guia **Settings**.

### Componentes na guia Criar formulário {#components-within-the-build-form-tab}

A guia **[!UICONTROL Criar formulário]** lista os itens de formulário que você usa no formulário de esquema. A guia **[!UICONTROL Settings]** fornece os atributos de cada item selecionado na guia **[!UICONTROL Criar formulário]**. A tabela a seguir lista os itens de formulário disponíveis na guia **[!UICONTROL Criar formulário]**:

<table>
 <tbody>
  <tr>
   <td><strong>Nome do componente</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Título da seção</td>
   <td>Adicione um cabeçalho de seção para obter uma lista de componentes comuns.</td>
  </tr>
  <tr>
   <td>Texto em linha única</td>
   <td>Adicione uma propriedade de texto de linha única. Ele é armazenado como uma string.</td>
  </tr>
  <tr>
   <td>Texto multivalor</td>
   <td>Adicione uma propriedade de texto de vários valores. Ele é armazenado como uma matriz de sequência de caracteres.</td>
  </tr>
  <tr>
   <td>Número</td>
   <td>Adicione um componente de número.</td>
  </tr>
  <tr>
   <td>Data</td>
   <td>Adicione um componente de data.</td>
  </tr>
  <tr>
   <td>Lista suspensa</td>
   <td>Adicione uma lista suspensa.</td>
  </tr>
  <tr>
   <td>Tags padrão</td>
   <td>Adicionar uma tag. </td>
  </tr>
  <tr>
   <td>Tags inteligentes</td>
   <td>Adicione para aumentar os recursos de pesquisa adicionando automaticamente as tags de metadados.<br /> </td>
  </tr>
  <tr>
   <td>Campo oculto</td>
   <td>Adicione um campo oculto. Ele é enviado como um parâmetro POST quando o ativo é salvo.</td>
  </tr>
  <tr>
   <td>Ativo referenciado por</td>
   <td>Adicione este componente para exibir a lista de ativos referenciados pelo ativo.</td>
  </tr>
  <tr>
   <td>Fazer referência ao ativo</td>
   <td>Adicionar para exibir uma lista de ativos que fazem referência ao ativo.</td>
  </tr>
  <tr>
   <td>Referências de produtos</td>
   <td>Adicionar para mostrar a lista de produtos vinculados ao ativo.</td>
  </tr>
  <tr>
   <td>Classificação do ativo</td>
   <td>Adicionar para exibir opções para classificar o ativo.</td>
  </tr>
  <tr>
   <td>Metadados do contexto</td>
   <td>Adicionar para controlar a exibição de outras guias de metadados na página de propriedades dos ativos.</td>
  </tr>
 </tbody>
</table>

#### Editar o componente de metadados {#edit-the-metadata-component}

Para editar as propriedades de um componente de metadados no formulário, clique no componente e edite todas ou um subconjunto das seguintes propriedades na guia **[!UICONTROL Settings]**.

**Rótulo** do campo: O nome da propriedade de metadados exibida na página de propriedades do ativo.

**Mapear para propriedade**: Essa propriedade especifica o caminho/nome relativo para o nó do ativo, onde ele é salvo no repositório CRX. Ele começa com `./` porque indica que o caminho está no nó do ativo.

A seguir estão os valores válidos para essa propriedade:

* . `/jcr:content/metadata/dc:title`: armazena o valor no nó de metadados do ativo como a propriedade `dc:title`.

* . `/jcr:created`: exibe a propriedade jcr no nó do ativo. Se você configurar essas propriedades nas propriedades de exibição, recomendamos marcá-las como Desativar edição, pois elas estão protegidas. Caso contrário, o erro &quot;Os ativos falharam ao serem modificados&quot; ocorre ao salvar as propriedades do ativo.

Para garantir que o componente seja exibido corretamente no formulário de esquema de metadados, o caminho da propriedade não deve incluir espaços.

**Espaço reservado**: Use essa propriedade para especificar o texto de espaço reservado relevante em relação à propriedade de metadados.

**Obrigatório**: Use essa propriedade para marcar uma propriedade de metadados como obrigatória na página de propriedades.

**Desativar edição**: Use essa propriedade para tornar uma propriedade de metadados não editável na página Propriedades .

**Mostrar Campo Vazio Em Somente** Leitura: Marque essa propriedade para exibir uma propriedade de metadados na página de propriedades, mesmo que ela não tenha um valor. Por padrão, quando uma propriedade de metadados não tem valor, ela não é listada na página de propriedades.

**Mostrar ordem** da lista: Use essa propriedade para exibir uma lista ordenada de opções

**Opções**: Usar esta propriedade para especificar opções em uma lista

**Descrição** : Use essa propriedade para adicionar uma breve descrição para o componente de metadados.

**Classe**: Classe de objeto à qual a propriedade está associada.

**Excluir**: Clique em para excluir um componente do formulário de esquema.

>[!NOTE]
>
>O componente Campo oculto não inclui esses atributos. Em vez disso, inclui propriedades, como atributos Nome, Valor, Rótulo do campo e Descrição. Os valores do componente Campo oculto são enviados como um parâmetro de POST sempre que o ativo é salvo. Ele não é salvo como metadados para o ativo.

Se você selecionar a opção **[!UICONTROL Obrigatório]**, poderá pesquisar por ativos sem metadados obrigatórios. No painel **[!UICONTROL Filtros]**, expanda o predicado **[!UICONTROL Validação de metadados]** e selecione a opção **[!UICONTROL Inválido]**. Os resultados de pesquisa exibem ativos que não têm metadados obrigatórios configurados por meio do formulário de esquema.

Se você adicionar o componente Metadados contextuais a qualquer guia de qualquer formulário de esquema, o componente aparecerá como uma lista na página de propriedades dos ativos aos quais o schema específico é aplicado. A lista inclui todas as outras guias, exceto a guia à qual você aplicou o componente de Metadados contextuais. No momento, esse recurso fornece funcionalidades básicas para controlar a exibição de metadados com base no contexto.

Para incluir qualquer guia na página de propriedades, além da guia em que o componente de Metadados contextuais é aplicado, selecione a guia na lista. A guia é adicionada à página de propriedades.

### Especificar propriedades no arquivo JSON {#specify-properties-in-json-file}

Em vez de especificar propriedades para as opções na guia **[!UICONTROL Configurações]**, defina as opções em um arquivo JSON especificando pares de valores chave correspondentes. Especifique o caminho do arquivo JSON no campo **[!UICONTROL Caminho JSON]**.

#### Adicione e exclua uma guia no formulário de esquema {#add-delete-a-tab-in-the-schema-form}

O editor de esquema permite adicionar ou excluir uma guia. O formulário de esquema padrão inclui as guias **[!UICONTROL Básico]**, **[!UICONTROL Avançado]**, **[!UICONTROL IPTC]** e **[!UICONTROL Extensão IPTC]**, por padrão.

Clique em `+` para adicionar uma nova guia em um formulário de esquema. Por padrão, a nova guia tem o nome `Unnamed-1`. Você pode modificar o nome da guia **[!UICONTROL Settings]**. Clique em `X` para excluir uma guia.

## Exclusão de formulários de esquema de metadados {#deleting-metadata-schema-forms}

AEM permite excluir somente formulários de esquema personalizados. Ela não permite excluir os formulários/modelos de esquema padrão. No entanto, é possível excluir quaisquer alterações personalizadas nesses formulários.

Para excluir um formulário, selecione-o e clique no ícone excluir.

>[!NOTE]
>
>Após excluir as alterações personalizadas em um formulário padrão, o ícone de bloqueio é exibido novamente antes na interface do Esquema de metadados para indicar que o formulário foi revertido para seu estado padrão.

>[!NOTE]
>
>Não é possível excluir os formulários de esquema de metadados prontos para uso no AEM Assets.

## Formulários de esquema para tipos MIME {#schema-forms-for-mime-types}

O AEM Assets fornece formulários padrão para vários tipos MIME prontos para uso. No entanto, é possível adicionar formulários personalizados a ativos de vários tipos MIME.

### Adicionar novos formulários para tipos MIME {#adding-new-forms-for-mime-types}

Crie um novo formulário no tipo de formulário apropriado. Por exemplo, para adicionar um novo modelo para o subtipo **image/png**, crie o formulário nos formulários &quot;image&quot;. O título do formulário de esquema é o nome do subtipo. Nesse caso, o título é &quot;png.**&quot;**

#### Uso de um modelo de esquema existente para vários tipos MIME {#using-an-existing-schema-template-for-various-mime-types}

Você pode usar um modelo existente para um tipo MIME diferente. Por exemplo, use o formulário `image/jpeg` para ativos do tipo MIME `image/png`.

Nesse caso, crie um novo nó em `/etc/dam/metadataeditor/mimetypemappings` no repositório CRX. Especifique um nome para o nó e defina as seguintes propriedades:

| **Nome** | **Descrição** | **Tipo** | **Valor** |
|---|---|---|---|
| `exposedmimetype` | Nome do formulário existente a ser mapeado | Sequência de caracteres | `image/jpeg` |
| `mimetypes` | Lista de tipos MIME que usam o formulário definido no atributo `exposedmimetype` | Sequência de caracteres | `image/png` |

O AEM Assets mapeia os seguintes tipos MIME e formulários de esquema:

| Formulário de esquema | Tipos MIME |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | vídeo/x-quicktime |
| vídeo/mpeg4 | video/mp4 |
| vídeo/avi | vídeo/avi, vídeo/msvideo, vídeo/x-msvideo |
| vídeo/wmv | video/x-ms-wmv |
| vídeo/flv | video/x-flv |

## Conceder acesso aos esquemas de metadados {#granting-access-to-metadata-schemas}

O recurso Esquema de metadados está disponível somente para administradores do . No entanto, os administradores podem fornecer acesso a não administradores modificando algumas permissões. O não administrador deve ter permissões para criar, modificar e excluir na pasta `/conf`.

## Aplicar metadados específicos da pasta {#applying-folder-specific-metadata}

O AEM Assets permite definir uma variante de um esquema de metadados e aplicá-la a uma pasta específica.

Por exemplo, você pode definir uma variante do esquema de metadados padrão e aplicá-la a uma pasta. Ao aplicar o schema modificado, ele substitui o schema de metadados padrão original aplicado aos ativos na pasta.

Somente os ativos carregados na pasta à qual esse esquema é aplicado estarão em conformidade com os metadados modificados definidos no esquema de metadados da variante.

Os ativos em outras pastas onde o esquema original é aplicado continuam em conformidade com os metadados definidos no esquema original.

A herança de metadados por ativos é baseada no esquema aplicado à pasta de primeiro nível na hierarquia. Em outras palavras, se uma pasta não contiver subpastas, os ativos na pasta herdarão os metadados do esquema aplicado à pasta.

Se a pasta tiver uma subpasta, os ativos na subpasta herdarão os metadados do esquema aplicado no nível da subpasta se um esquema diferente for aplicado no nível da subpasta. No entanto, se nenhum esquema ou o mesmo schema for aplicado no nível da subpasta, os ativos da subpasta herdarão os metadados do schema aplicado no nível da pasta pai.

1. Clique no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**. A página **[!UICONTROL Formulários de esquema de metadados]** é exibida.
1. Marque a caixa de seleção ao lado de um formulário, por exemplo, o formulário de metadados padrão, clique ou toque no ícone de cópia e salve-o como um formulário personalizado. Especifique um nome personalizado para o formulário, por exemplo `my_default`. Como alternativa, é possível criar um formulário personalizado.

1. Na página **[!UICONTROL Forms do esquema de metadados]**, selecione o formulário `my_default` e clique no ícone **[!UICONTROL Editar]**.
1. Na página **[!UICONTROL Editor de esquema de metadados]** , adicione um campo de texto ao formulário de esquema. Por exemplo, adicione um campo com o rótulo **[!UICONTROL Category]**.
1. Clique em **[!UICONTROL Salvar]**. O formulário modificado é listado na página **[!UICONTROL Forms]** do Esquema de Metadados.
1. Clique/toque em **[!UICONTROL Aplicar às pastas]** na barra de ferramentas para aplicar os metadados personalizados a uma pasta.
1. Selecione a pasta na qual aplicar o schema modificado e clique/toque em **[!UICONTROL Aplicar]**.
1. Se a pasta tiver o outro esquema de metadados aplicado, será exibida uma mensagem avisando que você está prestes a substituir o esquema de metadados existente. Clique em **Substituir**.
1. Clique em **OK** para fechar a mensagem de sucesso.
1. Navegue até a pasta na qual você aplicou o esquema de metadados modificado.

## Definição de metadados obrigatórios {#defining-mandatory-metadata}

Você pode definir campos obrigatórios em um nível de pasta, que é empregado em ativos que são carregados na pasta. Se você carregar ativos com metadados ausentes para os campos obrigatórios definidos anteriormente, uma indicação visual para metadados ausentes será exibida nos ativos na exibição de Cartão.

>[!NOTE]
>
>Um campo de metadados pode ser definido como obrigatório com base no valor de outro campo. Na exibição Cartões, AEM não exibe a mensagem de aviso sobre a falta de metadados para esses campos de metadados obrigatórios.

1. Clique no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**. A página **[!UICONTROL Formulários de esquema de metadados]** é exibida.
1. Salve o formulário de metadados padrão como um formulário personalizado. Por exemplo, salve-o como `my_default`.
1. Edite o formulário personalizado. Adicione um campo obrigatório. Por exemplo, adicione um campo **[!UICONTROL Category]** e torne o campo obrigatório.
1. Clique em **[!UICONTROL Salvar]**. O formulário modificado é listado na página **[!UICONTROL Forms]** do Esquema de Metadados. Selecione o formulário e clique ou toque em **[!UICONTROL Aplicar à(s) pasta(s)]** na barra de ferramentas para aplicar os metadados personalizados a uma pasta.
1. Navegue até a pasta e faça upload de alguns ativos com metadados ausentes para o campo obrigatório adicionado ao formulário personalizado. Uma mensagem para os metadados ausentes do campo obrigatório é exibida na exibição Cartão do ativo.
1. (Opcional) Acesse `https://[server]:[port]/system/console/components/`. Configure e habilite o componente `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` que está desabilitado por padrão. Defina uma frequência na qual o AEM verifica a validade dos metadados nos ativos.

   Essa configuração adiciona uma propriedade `hasValidMetadata` a `jcr:content` de ativos. Usando essa propriedade, AEM pode filtrar resultados em uma pesquisa.

   >[!NOTE]
   >
   >Se um ativo for adicionado após a verificação agendada, ele não será sinalizado com `hasValidMetadata` até a próxima verificação agendada. Os ativos não aparecem em resultados de pesquisa intermediária.

   >[!CAUTION]
   >
   >As verificações de validação de metadados consomem muitos recursos e podem afetar o desempenho do sistema. Agendar as verificações em conformidade. Se o servidor não conseguir lidar com a carga, tente desabilitar este trabalho
