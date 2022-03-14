---
title: Esquemas de metadados definem o layout da página de propriedades de metadados
description: O esquema de metadados define o layout da página de propriedades e as propriedades de metadados exibidas para ativos. Saiba como criar esquema de metadados personalizado, editar esquema de metadados e aplicar esquema de metadados a ativos.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 9e94afeb-1c54-4653-bf52-b0910c0cb6c1
source-git-commit: 7ea0e6c2d277199fc5216aab70e587bd23ac6baa
workflow-type: tm+mt
source-wordcount: '2592'
ht-degree: 8%

---

# Esquemas de metadados {#metadata-schemas}

As organizações vêm com um modelo de metadados que melhora a detecção de ativos, o uso, a interoperabilidade e assim por diante. A aplicação correta de metadados é sacrossanta para manter fluxos de trabalho e processos orientados por metadados. Para aderir à estratégia e aos padrões de metadados de toda a organização, você pode usar esquemas de metadados que ajudam os usuários do DAM a se alinhar. [!DNL Adobe Experience Manager] O permite que métodos fáceis e flexíveis criem, mantenham e apliquem esquemas de metadados.

Em [!DNL Adobe Experience Manager Assets], os schemas contêm campos específicos para informações específicas a serem preenchidas. Também contém informações de layout para exibir campos de metadados de maneira fácil de usar. As propriedades dos metadados incluem título, descrição, tipos MIME, tags e muito mais. Você pode usar o [!UICONTROL Forms do esquema de metadados] para modificar os esquemas existentes ou adicionar esquemas de metadados personalizados.

Para exibir e editar a página de propriedades de um ativo, siga estas etapas:

1. Clique no botão **[!UICONTROL Propriedades da exibição]** nas ações rápidas no bloco de ativos na exibição de cartão. Como alternativa, selecione um ativo e clique em **[!UICONTROL Propriedades]** ![exibir propriedades](assets/do-not-localize/info-circle-icon.png) na barra de ferramentas.

1. É possível editar as várias propriedades de metadados editáveis nas guias disponíveis. No entanto, não é possível modificar o ativo [!UICONTROL Tipo] no [!UICONTROL Básico] guia da página de propriedades.

   ![Guia Básico das Propriedades do ativo, onde o tipo de ativo não pode ser alterado](assets/asset-properties-basic-tab.png)

   *Figura: Guia Básico no ativo [!UICONTROL Propriedades].*

   Para modificar o tipo MIME de um ativo, use um formulário de esquema de metadados personalizado ou modifique um formulário existente. Consulte [Editar Forms do esquema de metadados](#edit-metadata-schema-forms) para obter mais informações. Se você modificar o esquema de metadados de um tipo MIME, o layout da página de propriedades dos ativos e todos os subtipos serão modificados. Por exemplo, modificar um esquema jpeg em `default/image` modifica apenas o layout de metadados (propriedades de ativos) para ativos com o tipo MIME `image/jpeg`. No entanto, se você editar o esquema padrão, suas alterações modificarão o layout de metadados para todos os tipos de ativos.

## Formulários de esquema de metadados {#default-metadata-schema-forms}

Para exibir uma lista de formulários ou modelos, em [!DNL Experience Manager] navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**.

[!DNL Experience Manager] O fornece os seguintes modelos de Formulário de esquema de metadados.

| Modelos |  | Descrição |
|---|---|---|
| [!UICONTROL default] |  | O formulário de esquema de metadados básico para ativos. |
|  | Os seguintes formulários filho herdam as propriedades do [!UICONTROL default] formulário: |  |
|  | <ul><li>[!UICONTROL dm_video]</li></ul> | Formulário de esquema para vídeos do Dynamic Media. |
|  | <ul><li>[!UICONTROL imagem]</li></ul> | Formulário de esquema para imagens com o tipo MIME, como `image/jpeg` e `image/png`. <br> O [!UICONTROL imagem] tem os seguintes modelos de formulário filho: <ul><li> [!UICONTROL jpeg]: Formulário de esquema para ativos com subtipo [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff]: Formulário de esquema dos ativos com TIFF de subtipo.</li></ul> |
|  | <ul><li>[!UICONTROL aplicativo]</li></ul> | Formulário de esquema para ativos com tipo MIME, como `application/pdf` e `application/zip`. <br>[!UICONTROL pdf]: Formulário de esquema para ativos com PDF de subtipo. |
|  | <ul><li>[!UICONTROL vídeo]</li></ul> | Formulário de esquema para ativos de vídeo com tipo MIME, como `video/avi` e `video/mp4`. |
| [!UICONTROL collection] |  | Formulário de esquema para coleções. |
| [!UICONTROL contentfragment] |  | Formulário de esquema dos Fragmentos de conteúdo. |
| [!UICONTROL formulários] |  | Este formulário de esquema está relacionado a [!DNL Adobe Experience Manager Forms]. |
| [!UICONTROL ugc_contentfragment] |  | Formulário de esquema para partes de conteúdo geradas pelo usuário e ativos integrados no Experience Manager a partir de redes sociais. |

>[!NOTE]
>
>Para exibir os formulários filho de um formulário de esquema, clique no nome do formulário de esquema.

## Adicionar um formulário de esquema de metadados {#add-a-metadata-schema-form}

Para adicionar um formulário de esquema de metadados, siga estas etapas:

1. Para adicionar um modelo personalizado à lista, clique em **[!UICONTROL Criar]** na barra de ferramentas.

   >[!NOTE]
   >
   >Um símbolo de cadeado é exibido com os modelos não editados. Se você personalizar um modelo, ele não será bloqueado ![bloqueio fechado](assets/do-not-localize/lock_closed_icon.svg).

1. Na caixa de diálogo , forneça o título do formulário de esquema e clique em **[!UICONTROL Criar]** para concluir o processo de criação do formulário.

## Editar formulários de esquema de metadados {#edit-metadata-schema-forms}

É possível editar um formulário de esquema de metadados recém-adicionado ou existente. O formulário de esquema de metadados inclui guias e itens de formulário em guias. Você pode mapear/configurar esses itens de formulário em um campo dentro de um nó de metadados no repositório CRX. É possível adicionar guias ou itens de formulário ao formulário de esquema de metadados. As guias e os itens de formulário derivados do pai estão no estado bloqueado. Não é possível alterá-los no nível filho.

1. No [!UICONTROL Forms do esquema de metadados] selecione um formulário e clique em **[!UICONTROL Editar]** na barra de ferramentas.

1. No **[!UICONTROL Editor de formulário do esquema de metadados]** personalize o formulário de metadados. Arraste os componentes necessários do **[!UICONTROL Criar formulário]** para uma das guias.

   ![Editor de esquema de metadados para personalizar a página Propriedades do ativo](assets/metadata-schema-editor.png)

   *Figura: A [!UICONTROL Editor de formulário do esquema de metadados] com guias disponíveis.*

1. Para configurar um componente, selecione-o e modifique suas propriedades no **[!UICONTROL Configurações]** guia .

### Componentes na [!UICONTROL Criar formulário] guia {#components-within-the-build-form-tab}

O **[!UICONTROL Criar formulário]** lista itens de formulário que você usa no formulário de esquema. O **[!UICONTROL Configurações]** A guia fornece os atributos de cada item selecionado na variável **[!UICONTROL Criar formulário]** guia . A tabela a seguir lista os itens de formulário disponíveis no **[!UICONTROL Criar formulário]** guia :

| Nome do componente | Descrição |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL Título da seção] | Adicione um cabeçalho de seção para obter uma lista de componentes comuns. |
| [!UICONTROL Texto em linha única] | Adicione uma propriedade de texto de linha única. Ele é armazenado como uma string. |
| [!UICONTROL Texto multivalor] | Adicione uma propriedade de texto de vários valores. Ele é armazenado como uma matriz de sequência de caracteres. |
| [!UICONTROL Número] | Adicione um componente de número. |
| [!UICONTROL Data] | Adicione um componente de data. |
| [!UICONTROL Lista suspensa] | Adicione uma lista suspensa. |
| [!UICONTROL Tags padrão] | Adicionar uma tag. |
| [!UICONTROL Tags inteligentes] | Adicione para aumentar os recursos de pesquisa, adicionando automaticamente as tags de metadados. |
| [!UICONTROL Campo oculto] | Adicione um campo oculto. Ele é enviado como um parâmetro POST quando o ativo é salvo. |
| [!UICONTROL Ativo referenciado por] | Adicione este componente para exibir a lista de ativos referenciados pelo ativo. |
| [!UICONTROL Fazer referência ao ativo] | Adicionar para exibir uma lista de ativos que fazem referência ao ativo. |
| [!UICONTROL Referências de produtos] | Adicionar para mostrar a lista de produtos vinculados ao ativo. |
| [!UICONTROL Metadados do contexto] | Adicionar para controlar a exibição de outras guias de metadados na página de propriedades dos ativos. |

<!-- TBD: Ratings are not available in Experience Manager as a Cloud Service. Removed via cqdoc-18089 ticket. 
| [!UICONTROL Asset Rating]        | Add to display options for rating the asset.                                       |
-->

#### Editar o componente de metadados {#edit-the-metadata-component}

Para editar as propriedades de um componente de metadados no formulário, clique no componente para editar todas ou um subconjunto das seguintes propriedades na **[!UICONTROL Configurações]** guia . É recomendável mapear apenas um campo para uma determinada propriedade no esquema de metadados. Caso contrário, o campo adicionado mais recente mapeado para a propriedade será escolhido pelo sistema.

**Rótulo do campo**: O nome da propriedade de metadados exibida na página de propriedades do ativo.

**Mapear para propriedade**: Essa propriedade especifica o caminho relativo ou o nome do nó do ativo, onde ele é salvo no repositório CRX. Começa com `./` para indicar que o caminho está sob o nó do ativo.

A seguir estão exemplos de valores válidos para uma propriedade:

* `./jcr:content/metadata/dc:title`: armazena o valor no nó de metadados do ativo como a propriedade `dc:title`.

* `./jcr:created`: Armazena a data e a hora de criação de um ativo. É uma propriedade protegida. Se você configurar essas propriedades, o Adobe recomenda marcá-las como Desativar edição. Caso contrário, o erro &quot;Os ativos falharam ao serem modificados&quot; ocorre ao salvar as propriedades do ativo.

Para garantir que o componente seja exibido corretamente no formulário de esquema de metadados, o caminho da propriedade não deve incluir espaços.

* **Espaço reservado**: Use essa propriedade para especificar o texto de espaço reservado relevante em relação à propriedade de metadados.
* **Obrigatório**: Use essa propriedade para marcar uma propriedade de metadados como obrigatória na página de propriedades.
* **Desativar edição**: Use essa propriedade para não permitir edições em uma propriedade na página de propriedades.
* **Mostrar campo vazio em somente leitura**: Marque essa propriedade para exibir uma propriedade de metadados na página de propriedades, mesmo que ela não tenha um valor. Por padrão, quando uma propriedade de metadados não tem valor, ela não é listada na página de propriedades.
* **Mostrar lista ordenada**: Use essa propriedade para exibir uma lista ordenada de opções.
* **Opções**: Use essa propriedade para especificar opções em uma lista.
* **Descrição** : Use essa propriedade para adicionar uma breve descrição para o componente de metadados.
* **Classe**: Classe de objeto à qual a propriedade está associada.
* **Excluir**: Clique em [!UICONTROL Excluir] para excluir um componente do formulário de esquema.

>[!NOTE]
>
>O [!UICONTROL Campo oculto] não inclui esses atributos. Em vez disso, inclui propriedades, como atributos Nome, Valor, Rótulo do campo e Descrição. Os valores do componente Campo oculto são enviados como um parâmetro de POST sempre que o ativo é salvo. Ele não é salvo como metadados para o ativo.

Se você selecionar a opção **[!UICONTROL Obrigatório]**, poderá pesquisar por ativos sem metadados obrigatórios. No painel **[!UICONTROL Filtros]**, expanda o predicado **[!UICONTROL Validação de metadados]** e selecione a opção **[!UICONTROL Inválido]**. Os resultados de pesquisa exibem ativos que não têm metadados obrigatórios configurados por meio do formulário de esquema.

Se você adicionar o componente Metadados contextuais a qualquer guia de qualquer formulário de esquema, o componente aparecerá como uma lista na página de propriedades dos ativos aos quais o schema específico é aplicado. A lista inclui todas as outras guias, exceto a guia à qual você aplicou o componente de Metadados contextuais. No momento, esse recurso fornece funcionalidades básicas para controlar a exibição de metadados com base no contexto.

Para exibir qualquer guia na página de propriedades, além da guia em que o componente de Metadados contextuais é aplicado, selecione a guia na lista. A guia é adicionada à página de propriedades.

### Especificar propriedades no arquivo JSON {#specify-properties-in-json-file}

Em vez de especificar propriedades para as opções na guia **[!UICONTROL Configurações]**, defina as opções em um arquivo JSON especificando pares de valores chave correspondentes. Especifique o caminho do arquivo JSON no campo **[!UICONTROL Caminho JSON]**.

#### Adicionar ou excluir uma guia no formulário de esquema {#add-delete-a-tab-in-the-schema-form}

O editor de esquema permite adicionar ou excluir uma guia. O formulário de esquema padrão inclui a variável **[!UICONTROL Básico]**, **[!UICONTROL Avançado]** , **[!UICONTROL IPTC]** e **[!UICONTROL Extensão IPTC]** guias.

![Guias padrão no formulário Esquema de metadados](assets/metadata-schema-form-tabs.png)

Clique em `+` para adicionar uma guia em um formulário de esquema. Por padrão, a nova guia tem o nome `Unnamed-1`. Você pode modificar o nome da variável **[!UICONTROL Configurações]** guia . Clique em `X` para excluir uma guia.

![Adicionar ou excluir uma guia usando o Editor de esquema de metadados](assets/metadata-schema-form-new-tab.png)

## Excluir formulários de esquema de metadados {#deleting-metadata-schema-forms}

O Experience Manager permite excluir somente formulários de esquema personalizados. Ela não permite excluir os formulários/modelos de esquema padrão. No entanto, é possível excluir quaisquer alterações personalizadas nesses formulários.

Para excluir um formulário, selecione-o e clique no ícone excluir.

>[!NOTE]
>
>Após excluir as alterações personalizadas em um formulário padrão, o ícone de bloqueio é exibido novamente antes na interface do Esquema de metadados para indicar que o formulário foi revertido para seu estado padrão.

>[!NOTE]
>
>* Após excluir as alterações personalizadas em um formulário padrão, o bloqueio ![bloqueio fechado](assets/do-not-localize/lock_closed_icon.svg) será exibido novamente antes do formulário. Indica que o formulário é revertido para seu estado padrão.
>* Não é possível excluir os formulários de esquema de metadados padrão em [!DNL Assets].


## Formulários de esquema para tipos MIME {#schema-forms-for-mime-types}

[!DNL Experience Manager] O fornece formulários padrão para vários tipos MIME prontos para uso. No entanto, é possível adicionar formulários personalizados a ativos de vários tipos MIME.

### Adicionar novos formulários para tipos MIME {#adding-new-forms-for-mime-types}

Crie um formulário no tipo de formulário apropriado. Por exemplo, para adicionar um modelo para a variável `image/png` , crie o formulário nos formulários de &quot;imagem&quot;. O título do formulário de esquema é o nome do subtipo. Nesse caso, o título é `png`.

#### Usar um modelo de esquema existente para vários tipos MIME {#use-an-existing-schema-template-for-various-mime-types}

Você pode usar um modelo existente para um tipo MIME diferente. Por exemplo, use a variável `image/jpeg` formulário para ativos do tipo MIME `image/png`.

Nesse caso, crie um nó em `/etc/dam/metadataeditor/mimetypemappings` no repositório CRX. Especifique um nome para o nó e defina as seguintes propriedades:

| Nome | Descrição | Tipo | Valor |
|------|-------------|------|-------|
| `exposedmimetype` | Nome do formulário existente a ser mapeado | `String` | `image/jpeg` |
| `mimetypes` | Lista de tipos MIME que usam o formulário definido na variável `exposedmimetype` atributo | `String` | `image/png` |

[!DNL Assets] O mapeia os seguintes tipos MIME e formulários de esquema:

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

## Conceder acesso aos esquemas de metadados {#grant-access-to-metadata-schemas}

O recurso Esquema de metadados está disponível somente para administradores do . No entanto, os administradores podem fornecer acesso a não administradores modificando algumas permissões. Forneça permissões para que usuários não administradores criem, modifiquem e excluam no `/conf` pasta.

## Aplicar metadados específicos da pasta {#applying-folder-specific-metadata}

[!DNL Assets] permite definir uma variante de um schema de metadados e aplicá-la a uma pasta específica.

Por exemplo, você pode definir uma variante do esquema de metadados padrão e aplicá-la a uma pasta. Ao aplicar o schema modificado, ele substitui o schema de metadados padrão original aplicado aos ativos na pasta.

Somente os ativos carregados na pasta à qual esse esquema é aplicado estão em conformidade com os metadados modificados definidos no esquema de metadados da variante. [!DNL Assets] em outras pastas onde o esquema original é aplicado, continue em conformidade com os metadados definidos no esquema original.

A herança de metadados por ativos é baseada no esquema aplicado à pasta de nível superior na hierarquia. O mesmo schema é aplicado ou herdado pelas subpastas. Se um schema diferente for aplicado no nível da subpasta, a herança será interrompida.

1. Em [!DNL Experience Manager] , navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**. A página **[!UICONTROL Formulários de esquema de metadados]** é exibida.
1. Marque a caixa de seleção ao lado de um formulário, por exemplo, o formulário de metadados padrão, e clique no botão **[!UICONTROL Copiar]** e salve-o como um formulário personalizado. Especifique um nome personalizado para o formulário, por exemplo `my_default`. Como alternativa, é possível criar um formulário personalizado.

1. No **[!UICONTROL Forms do esquema de metadados]** selecione o `my_default` e clique em **[!UICONTROL Editar]**.
1. No **[!UICONTROL Editor de esquema de metadados]** adicione um campo de texto ao formulário de esquema. Por exemplo, adicione um campo com o rótulo **[!UICONTROL Categoria]**.
1. Clique em **[!UICONTROL Salvar]**. O formulário modificado é listado na variável **[!UICONTROL Forms do esquema de metadados]** página.
1. Clicar/tocar **[!UICONTROL Aplicar às pastas]** na barra de ferramentas para aplicar os metadados personalizados a uma pasta.
1. Selecione a pasta na qual aplicar o schema modificado e clique/toque em **[!UICONTROL Aplicar]**.
1. Se a pasta tiver o outro esquema de metadados aplicado, será exibida uma mensagem avisando que você está prestes a substituir o esquema de metadados existente. Clique em **Substituir**.
1. Clique em **OK** para fechar a mensagem de sucesso.
1. Navegue até a pasta na qual você aplicou o esquema de metadados modificado.

## Definição de metadados obrigatórios {#defining-mandatory-metadata}

Você pode definir campos obrigatórios em um nível de pasta, que é empregado em ativos que são carregados na pasta. Se você carregar ativos com metadados ausentes para os campos obrigatórios definidos anteriormente, uma indicação visual para metadados ausentes será exibida nos ativos na exibição de Cartão.

>[!NOTE]
>
>Um campo de metadados pode ser definido como obrigatório com base no valor de outro campo. Na exibição Cartões, o Experience Manager não exibe a mensagem de aviso sobre a falta de metadados para esses campos de metadados obrigatórios.

1. Clique no logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**. A página **[!UICONTROL Formulários de esquema de metadados]** é exibida.
1. Salve o formulário de metadados padrão como um formulário personalizado. Por exemplo, salve como `my_default`.
1. Edite o formulário personalizado. Adicione um campo obrigatório. Por exemplo, adicione uma **[!UICONTROL Categoria]** e tornar o campo obrigatório.
1. Clique em **[!UICONTROL Salvar]**. O formulário modificado é listado na variável **[!UICONTROL Forms do esquema de metadados]** página. Selecione o formulário e clique ou toque em **[!UICONTROL Aplicar às pastas]** na barra de ferramentas para aplicar os metadados personalizados a uma pasta.
1. Navegue até a pasta e faça upload de alguns ativos com metadados ausentes para o campo obrigatório adicionado ao formulário personalizado. Uma mensagem para os metadados ausentes do campo obrigatório é exibida na exibição Cartão do ativo.
1. (Opcional) Acesso `https://[server]:[port]/system/console/components/`. Configurar e ativar `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` componente que é desativado por padrão. Defina uma frequência na qual o Experience Manager verifica a validade dos metadados nos ativos.

   Essa configuração adiciona uma propriedade `hasValidMetadata` para `jcr:content` dos ativos. Usando essa propriedade, o Experience Manager pode filtrar resultados em uma pesquisa.

   >[!NOTE]
   >
   >Se um ativo for adicionado após a verificação agendada, o ativo não será sinalizado com `hasValidMetadata` até a próxima verificação programada. Os ativos não aparecem em resultados de pesquisa intermediária.

   >[!CAUTION]
   >
   >As verificações de validação de metadados consomem muitos recursos e podem afetar o desempenho do sistema. Agendar as verificações em conformidade. Se o servidor não conseguir lidar com a carga, tente desabilitar este trabalho
