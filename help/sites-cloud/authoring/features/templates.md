---
title: Criação de modelos de páginas
description: O modelo define a estrutura da página resultante e, com o editor de modelos, criar e manter modelos não é mais uma tarefa somente para desenvolvedores
exl-id: 4c9dbf26-5852-45ab-b521-9f051c153b2e
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '4538'
ht-degree: 87%

---

# Criação de modelos de páginas   {#creating-page-templates}

Ao criar uma página, é necessário selecionar um modelo, que é usado como base para a criação da nova página. O modelo define a estrutura da página resultante, todo conteúdo inicial e os componentes que podem ser usados.

Com o **Editor de modelos**, criar e manter modelos não é mais uma tarefa somente para desenvolvedores. Um tipo de usuário avançado, chamado de **autor de modelo**, também pode ser envolvido. Os desenvolvedores ainda são necessários para configurar o ambiente, criar bibliotecas de clientes e criar os componentes a serem usados, mas uma vez que essas noções básicas estejam em vigor, o **autor do modelo** terá a flexibilidade de criar e configurar modelos sem um projeto de desenvolvimento.

O **Console de Modelos** permite que os autores de modelo:

* Criem um novo modelo ou copiem um modelo existente.
* Gerenciem o ciclo de vida do modelo.

O **Editor de Modelos** permite que os autores de modelo:

* Adicione componentes ao modelo e posicione-os em uma grade responsiva.
* Pré-configurar os componentes.
* Defina quais componentes podem ser editados nas páginas criadas com o modelo.

Este documento explica como um **autor do modelo** pode usar o console de modelos e o editor para criar e gerenciar modelos editáveis.

Para obter informações detalhadas sobre como os modelos editáveis funcionam em nível técnico, consulte o documento do desenvolvedor [Modelos de Página](/help/implementing/developing/components/templates.md).

>[!NOTE]
>
>O **Editor de modelos** não oferece suporte para direcionamento diretamente no nível do modelo. As páginas criadas com base em um modelo editável podem ser direcionadas, mas os modelos em si não podem.

## Antes de começar {#before-you-start}

>[!NOTE]
>
>Um administrador precisa configurar uma pasta de modelo no **Navegador de configurações** e aplicar permissões apropriadas antes que um autor de modelo possa criar um modelo nessa pasta.

Antes de começar, é importante considerar que a criação de um modelo requer colaboração. Por esse motivo, a [Função](#roles) é indicada para cada tarefa. Isso não afetará a maneira como você usa um modelo para criar uma página, mas afeta a maneira como uma página se relaciona com o modelo.

### Funções {#roles}

A criação de um novo modelo usando o **Console de modelos** e o **Editor de modelos** exige a colaboração entre as seguintes funções:

* **Administrador**:
   * Cria uma nova pasta de modelos requer direitos de `admin`.
   * Essas tarefas também podem ser realizadas por um desenvolvedor
* **Desenvolvedor**:
   * Concentra-se nos detalhes técnicos/internos
   * Precisa de experiência com o ambiente de desenvolvimento.
   * Fornece ao autor do modelo as informações necessárias. 
* **Autor do modelo**:
   * Esse é um autor específico, membro do grupo `template-authors`
      * Isso atribui os privilégios e permissões necessários. 
   * Pode configurar o uso de componentes e outros detalhes de alto nível que exigem:
      * Algum conhecimento técnico
         * Por exemplo, usar padrões ao definir caminhos.
      * Informações técnicas do desenvolvedor.

Devido à natureza de algumas tarefas, como a criação de uma pasta, é necessário um ambiente de desenvolvimento, o que requer conhecimento/experiência.

As tarefas detalhadas neste documento são listadas com a função responsável por executá-las.

## Criação e gerenciamento de modelos {#creating-and-managing-templates}

Ao criar um modelo editável, você:

* Use o console **Modelo**. Isso está disponível na seção **Geral** do console **Ferramentas**.
   * Ou diretamente em: `https://<host>:<port>/libs/wcm/core/content/sites/templates.html/conf`
* É possível [criar uma pasta para os modelos](#creating-a-template-folder-admin) se necessário
* [Criar um novo modelo](#creating-a-new-template-template-author), inicialmente vazio 
* [Definir propriedades adicionais](#defining-template-properties-template-author) para o modelo, se necessário
* [Editar o modelo](#editing-templates-template-authors) para definir o:
   * [Estrutura](#editing-a-template-structure-template-author) - conteúdo predefinido que não pode ser alterado nas páginas criadas com o modelo.
   * [Conteúdo inicial](#editing-a-template-initial-content-author) - conteúdo predefinido que pode ser alterado nas páginas criadas com o modelo.
   * [Layout](#editing-a-template-layout-template-author) - para um intervalo de dispositivos.
   * [Estilos](/help/sites-cloud/authoring/features/style-system.md) - defina os estilos a serem usados com o modelo e seus componentes.
* [Habilitar o modelo](#enabling-a-template-template-author) para uso ao criar uma página
* [Permitir o modelo](#allowing-a-template-author) para a página ou ramificação necessária do seu site
* [Publicar o modelo](#publishing-a-template-template-author) para torná-lo disponível no ambiente de publicação

>[!NOTE]
>
>Os **Modelos permitidos** geralmente são predefinidos quando seu site for inicialmente configurado.

>[!TIP]
>
>Nunca insira qualquer informação que deve ser internacionalizada em um modelo. <!-- Never enter any information that must be [internationalized](/help/sites-developing/i18n.md) into a template.-->
>
>Para elementos de modelo, como cabeçalhos e rodapés que devem ser localizados, aproveite [os recursos de localização dos componentes principais.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=pt-BR)

### Criação de uma pasta de modelo - Administrador {#creating-a-template-folder-admin}

Uma pasta de modelo deve ser criada para que o projeto mantenha seus modelos específicos de projetos. Trata-se de uma tarefa de administrador e está descrita no documento [Modelos de página](/help/implementing/developing/components/templates.md#template-folders).-->

### Criação de um novo modelo - Autor do modelo {#creating-a-new-template-template-author}

1. Abra o **console Modelos** (em **Ferramentas ->** **Geral**) para navegar até a pasta necessária.

   >[!NOTE]
   >
   >Em uma instância padrão do AEM, a pasta **global** já existe no console modelo. Isso mantém modelos padrão e atua como um fallback se nenhuma política e/ou tipo de modelo for localizado na pasta atual.
   >
   >É uma prática recomendada usar uma [pasta de modelo criada para o seu projeto](/help/implementing/developing/components/templates.md#template-folders).

1. Selecione **Criar**, em seguida **Criar modelo** para abrir o assistente.

1. Escolha um **Tipo de modelo** e clique em **Próximo**.

   >[!NOTE]
   >
   >Os tipos de modelo são layouts predefinidos de modelos e podem ser considerados como modelos para um modelo. Eles são predefinidos pelos desenvolvedores ou pelo administrador do sistema. Mais informações podem ser encontradas no documento do desenvolvedor [Modelos de página](/help/implementing/developing/components/templates.md#template-type).-->

1. Conclua os **Detalhes do modelo**:

   * **Nome do modelo**
   * **Descrição**

1. Selecione **Criar**. Uma confirmação será exibida, selecione **Abrir** para começar a editar o modelo ou **Concluído** para retornar ao console do modelo.

   >[!NOTE]
   >
   >Quando um modelo novo for criado, ele será marcado como **Rascunho** no console. Isso indica que ainda não está disponível para uso por autores da página.

>[!NOTE]
>
>Os modelos são ferramentas eficientes para simplificar o fluxo de trabalho de criação de página. No entanto, usar modelos em excesso pode sobrecarregar os autores e tornar confusa a criação da página. Uma boa regra geral é manter o número de modelos abaixo de 100.
>
>A Adobe não recomenda ter mais de 1000 modelos devido a possíveis impactos no desempenho.

### Definir propriedades do modelo - Autor do modelo   {#defining-template-properties-template-author}

Um modelo pode ter as seguintes propriedades:

* Imagem
   * Imagem a ser usada como [miniatura do modelo](#template-thumbnail-image) para auxiliar na seleção, como no assistente de Criar página.
      * Pode ser enviado
      * Pode ser gerado com base no conteúdo do modelo
* Título
   * Um título usado para identificar o modelo, como no assistente de **Criar página**.
* Descrição
   * Uma descrição opcional para fornecer mais informações sobre o modelo e seu uso, que pode ser visualizada, por exemplo, no assistente **Criar página**.

Para exibir e/ou editar as propriedades:

1. No **console Modelos**, selecione o modelo.
1. Selecione **Propriedades da exibição** na barra de ferramentas ou nas opções rápidas para abrir a caixa de diálogo.
1. Agora você pode exibir ou editar as propriedades do modelo.

>[!NOTE]
>
>O status de um modelo (rascunho, ativado ou desativado) é exibido no console.

#### Imagem em miniatura do modelo {#template-thumbnail-image}

Para definir a miniatura do modelo:

1. Edite as propriedades do modelo.
1. Escolha se deseja fazer upload de uma miniatura ou gerá-la a partir do conteúdo do modelo.
   * Para fazer upload de uma miniatura, selecione **Fazer upload de imagem**
   * Se quiser gerar uma miniatura, selecione **Gerar visualização**
1. Para ambos os métodos, uma visualização da miniatura será exibida.
   * Se não for satisfatório, selecione **Limpar** para carregar outra imagem ou gerar novamente a miniatura.
1. Quando estiver satisfeito com a miniatura, selecione **Salvar e fechar**.

### Ativar e permitir um modelo - Autor do modelo   {#enabling-and-allowing-a-template-template-author}

Para poder usar um modelo ao criar uma página é necessário:

* [Ativar o modelo](#enabling-a-template-template-author) para disponibilizá-lo para o uso na criação de páginas.
* [Permitir o modelo](#allowing-a-template-author) para especificar as ramificações de conteúdo nas quais o modelo pode ser usado.

#### Habilitar um modelo - Autor do modelo {#enabling-a-template-template-author}

Um modelo pode ser habilitado ou desabilitado para torná-lo disponível ou indisponível no assistente de **Criar Página**.

>[!CAUTION]
>
>Depois que um modelo é habilitado, um aviso será exibido quando um autor do modelo começar a atualizá-lo. Isso é para informar ao usuário que o modelo pode ter sido referenciado, de modo que qualquer alteração pode afetar as páginas que lhe fazem referência.

1. No **console Modelos**, selecione o modelo.
1. Selecione **Habilitar** ou **Desabilitar** da barra de ferramentas e depois na caixa de diálogo de confirmação.
1. Agora você pode usar seu modelo quando [criação de uma página](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page), embora você provavelmente queira [editar o modelo](#editing-templates-template-authors) de acordo com suas necessidades.

>[!NOTE]
>
>O status de um modelo (rascunho, ativado ou desativado) é exibido no console.

#### Ativar um modelo - Autor {#allowing-a-template-author}

Um modelo pode ser disponibilizado ou indisponibilizado para determinadas ramificações de página.

1. Abra as [Propriedades da página](/help/sites-cloud/authoring/fundamentals/page-properties.md) da página raiz da ramificação onde deseja que o modelo fique disponível.
1. Abra a guia **Avançado**.
1. Em **Configurações do modelo** use **Adicionar campo** para especificar os caminhos aos seus modelos.

   O caminho pode ser explícito ou usar padrões. Por exemplo:

   `/conf/<your-folder>/settings/wcm/templates/.*`

   A ordem dos caminhos é irrelevante. Todos os caminhos são verificados e todos os modelos são recuperados.

   >[!NOTE]
   >
   >Se a lista **Modelos permitidos** for deixada vazia, a se subirá a árvore até que um valor/lista seja encontrado.
   >
   >
   >Consulte [Disponibilidade de modelos](/help/implementing/developing/components/templates.md#template-availability) - os princípios para modelos permitidos permanecem inalterados.

1. Clique em **Salvar** para salvar as alterações nas propriedades da página.

>[!NOTE]
>
>Geralmente os modelos permitidos são predefinidos para todo o site quando configurado.

### Publicar um modelo - Autor do modelo {#publishing-a-template-template-author}

À medida que o modelo for referenciado quando a página for renderizada, o modelo totalmente configurado deverá ser publicado, para estar disponível no ambiente de publicação.

1. No **console Modelos**, selecione o modelo.
1. Selecione **Publicar** na barra de ferramentas para abrir o assistente.
1. Selecione as **Políticas do conteúdo** para ser publicado em tandem.
1. Selecione **Publicar** na barra de ferramentas para concluir a ação.

## Editar modelos - Autores do modelo   {#editing-templates-template-authors}

Ao criar ou editar um modelo, há vários aspectos que você pode definir. A edição de modelos é semelhante à criação de página.

A variável **Modo** o seletor na barra de ferramentas permite selecionar e editar o aspecto apropriado do modelo:

* [Estrutura](#editing-a-template-structure-template-author)
* [Conteúdo inicial](#editing-a-template-initial-content-author)
* [Layout](#editing-a-template-layout-template-author)

![Seletor de modo do editor de modelos](/help/sites-cloud/authoring/assets/templates-mode.png)

Embora a **Política da página** opção no **Informações da página** permite que você [selecionar as políticas de página necessárias](#page-policies):

![Informações da página do editor de modelos](/help/sites-cloud/authoring/assets/templates-page-information.png)

>[!CAUTION]
>
>Se um autor começar a editar um modelo que já foi habilitado, um aviso será exibido. Isso é para informar ao usuário que o modelo pode ter sido referenciado, de modo que qualquer alteração pode afetar as páginas que lhe fazem referência.

### Atributos do modelo {#template-attributes}

Os seguintes atributos de um modelo podem ser editados:

#### Estrutura {#template-structure}

Os componentes adicionados à [estrutura](#editing-a-template-structure-template-author) não podem ser movidos/removido das páginas resultantes pelos autores da página. Se quiser que os autores de página possam adicionar e remover componentes de páginas resultantes, será necessário adicionar um sistema de parágrafo ao modelo.

Quando os componentes estiverem bloqueados, é possível adicionar conteúdo, que não pode ser editado por autores da página. É possível desbloquear componentes para permitir definir o [Conteúdo inicial](#editing-a-template-initial-content-author).

>[!NOTE]
>
>No modo estrutura, os componentes principais de um componente desbloqueado não podem ser movidos, recortados ou excluídos.

#### Conteúdo inicial {#template-initial-content}

Quando um componente tiver sido desbloqueado, é possível definir o [conteúdo inicial](#editing-a-template-initial-content-author) que é copiado para as páginas resultantes, criadas a partir do modelo. Esses componentes desbloqueados podem ser editados nas páginas resultantes.

>[!NOTE]
>
>No modo de **conteúdo inicial**, e nas páginas resultantes, qualquer componente desbloqueado que tenha uma página principal acessível (ou seja, componentes dentro de um container de layout) pode ser excluído.

#### Layout {#template-layout}

Com o [layout](#editing-a-template-layout-template-author), é possível predefinir o layout do modelo para os formatos de dispositivo necessários. O modo **Layout** de criação do modelo tem a mesma funcionalidade que o modo [**Layout** da criação de página](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode).

#### Políticas da página {#template-page-policies}

As [políticas de página](#page-policies) podem conectar políticas de página predefinidas à página. Essas políticas da página definem as várias configurações de design.

#### Estilos {#template-styles}

O [Sistema de estilos](/help/sites-cloud/authoring/features/style-system.md) permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente, de modo que o autor de conteúdo possa selecioná-los ao editar o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando-o mais flexível.

Consulte a [documentação do Style System](/help/sites-cloud/authoring/features/style-system.md) para obter mais informações.

### Editar um modelo - Estrutura - Autor do modelo {#editing-a-template-structure-template-author}

No modo **Estrutura** você define os componentes e o conteúdo para o modelo, a política do modelo e seus componentes.

* Os componentes definidos na estrutura do modelo não podem ser movidos em uma página resultante nem excluídos de qualquer página resultante.
* Se desejar que os autores de página possam adicionar e remover componentes, adicione um sistema de parágrafo ao modelo.
* Os componentes podem ser desbloqueados e bloqueados novamente para permitir que você defina o [conteúdo inicial](#editing-a-template-initial-content-author).
* As políticas de design dos componentes e página são definidas.

![Estrutura da página do editor de modelos](/help/sites-cloud/authoring/assets/templates-page-structure.png)

Há várias ações que você pode realizar no **Estrutura** do editor de modelos e vários recursos para ajudá-lo a:

#### Adicionar componentes {#add-components}

Existem vários mecanismos para adicionar componentes ao modelo:

* No navegador de **Componentes** no painel lateral.
* Ao usar a opção **Inserir componente**, disponível na barra de ferramentas dos componentes já no modelo ou na caixa **Arrastar componentes até aqui**.
* Ao arrastar um ativo (no navegador de **Ativos** no painel lateral) diretamente no modelo para gerar o componente adequado no local.

Após adicionado, cada componente é marcado com:

* Uma borda
* Um marcador para mostrar o tipo de componente
* Um marcador para mostrar quando o componente foi desbloqueado

>[!NOTE]
>
>Ao adicionar um componente de **Título** pronto ao modelo, ele conterá **estrutura** de texto padrão.
>
>Se você alterar isso e adicionar seu próprio texto, esse texto atualizado será usado quando uma página for criada a partir do modelo.
>
>Se deixar o texto padrão (estrutura) como está, o título será padrão para o nome da página subsequente.

>[!NOTE]
>
>Embora não seja idêntico, adicionar componentes e ativos a um modelo tem muitas coisa em comum com as ações semelhantes ao [criar a página](/help/sites-cloud/authoring/fundamentals/editing-content.md).

#### Ações do componente {#component-actions}

Execute ações nos componentes uma vez que eles tenham sido adicionados ao modelo. Cada instância individual tem uma barra de ferramentas que permite acessar as ações disponíveis. A barra de ferramentas depende do tipo de componente.

![Barra de ferramentas de ações de um componente do modelo](/help/sites-cloud/authoring/assets/templates-component-actions.png)

Além disso, ela pode ser dependente das ações executadas como quando uma política foi associada ao componente, o ícone de configuração de design é disponibilizado.

#### Editar e configurar {#edit-and-configure}

Com essas duas ações você pode adicionar conteúdo aos seus componentes.

#### Estrutura de Borda indicadora {#border-to-indicate-structure}

Ao trabalhar no modo **Estrutura** uma borda laranja indica o componente selecionado no momento. Uma linha pontilhada também indica o componente principal.

#### Política e propriedades (Geral) {#policy-and-properties-general}

As políticas de conteúdo (ou design) definem as propriedades de design de um componente. Por exemplo, os componentes disponíveis ou as dimensões mínima/máxima. Elas são aplicáveis ao modelo (e às páginas criadas com ele).

Crie uma política de conteúdo ou selecione uma existente para um componente.

![Botão Política de conteúdo](/help/sites-cloud/authoring/assets/templates-content-policy-button.png)

Isso permite que você defina os detalhes do design.

![Política de conteúdo](/help/sites-cloud/authoring/assets/template-content-policy.png)

A janela de configuração é dividida em dois.

* Do lado esquerdo da caixa de diálogo, em **Política**, você tem a capacidade de selecionar uma política existente.
* Do lado direito da caixa de diálogo, em **Propriedades**, você pode definir as propriedades específicas ao tipo de componente.

As propriedades disponíveis dependem do componente selecionado. Por exemplo, para um componente de texto, as propriedades definem as opções de copiar e colar, de formatação e de estilo de parágrafo, entre outras.

##### Política {#policy}

As políticas de conteúdo (ou design) definem as propriedades de design de um componente. Por exemplo, os componentes disponíveis ou as dimensões mínima/máxima. Elas são aplicáveis ao modelo (e às páginas criadas com ele).

Em **Política** você pode selecionar uma política existente para aplicar ao componente por meio da lista suspensa.

![Selecionar política](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

Uma nova política pode ser adicionada ao selecionar o botão adicionar ao lado da **Selecionar política** menu suspenso. Atribua um novo título na variável **Título da política** campo.

![Botão Adicionar política](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

A política existente selecionada no **Selecionar política** a lista suspensa pode ser copiada como uma nova política usando o botão copiar ao lado da lista suspensa. Atribua um novo título na variável **Título da política** campo. Por padrão, a política copiada será denominada **Cópia de X**, onde X é o título da política copiada.

![Botão Copiar política](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

É opcional uma descrição da política no campo **Descrição da política**.

No **Outros modelos que também usam a política selecionada** seção, é possível ver quais outros modelos usam a política selecionada na **Selecionar política** lista suspensa.

![Utilização da política atual](/help/sites-cloud/authoring/assets/templates-policy-use.png)

>[!NOTE]
>
>Se vários componentes do mesmo tipo forem adicionados como conteúdo inicial, a mesma política se aplica a todos os componentes.

##### Propriedades {#properties}

No cabeçalho **Propriedades**, é possível definir as configurações do componente. O cabeçalho tem duas guias:

* Principal
* Recursos

###### Principal {#main}

Na guia **Principal**, as configurações mais importantes do componente são definidas.

Por exemplo, para um componente de imagem, as larguras permitidas podem ser definidas juntamente com a ativação de carregamento lento.

Se uma configuração permitir várias configurações, selecione a variável **Adicionar** para adicionar outra configuração.

![Botão Adicionar](/help/sites-cloud/authoring/assets/templates-add-button.png)

Para remover uma configuração, selecione a variável **Excluir** localizado à direita da configuração.

Para remover uma configuração, selecione a variável **Excluir** botão.

![Botão Excluir](/help/sites-cloud/authoring/assets/templates-delete-button.png)

###### Recursos {#features}

A variável **Recursos** permite ativar ou desativar recursos adicionais do componente.

Por exemplo, para um componente de imagem, é possível definir as proporções de corte, as orientações de imagem permitidas e se os uploads são permitidos.

![Guia Recursos](/help/sites-cloud/authoring/assets/templates-features-tab.png)

>[!CAUTION]
>
>Observe que no AEM, as proporções de corte estão definidas como **altura/largura**. Isso difere da definição convencional de largura/altura e é feita por motivos de compatibilidade legal. Os usuários da criação de página não estarão cientes de qualquer diferença desde que você defina o **Nome** claramente, uma vez que este é exibido na interface do usuário.

>[!NOTE]
>
>[As políticas de conteúdo para componentes que implementam o editor de rich text](/help/implementing/developing/extending/rich-text-editor.md) só podem ser definidas para opções disponibilizadas pelo RTE, por meio das configurações da interface.

#### Política e propriedades (container de layout) {#policy-and-properties-layout-container}

As configurações de política e propriedades de um container de layout são semelhantes ao uso geral, mas com algumas diferenças.

>[!NOTE]
>
>A configuração de uma política é obrigatória para componentes de container, pois permite definir componentes que estejam disponíveis no container.

A janela de configuração é dividida em duas, assim como no uso geral da janela.

##### Política {#policy-layout}

As políticas de conteúdo (ou design) definem as propriedades de design de um componente. Por exemplo, os componentes disponíveis ou as dimensões mínima/máxima. Elas são aplicáveis ao modelo (e às páginas criadas com ele).

Em **Política** é possível selecionar uma política existente para aplicar ao componente por meio da lista suspensa. Isso funciona exatamente da mesma forma que a janela de uso geral.

##### Propriedades {#properties-layout}

No cabeçalho **Propriedades**, é posível escolher quais componentes estão disponíveis para o container de layout e definir suas configurações. O cabeçalho tem três guias:

* Componentes permitidos
* Componentes padrão
* Configurações responsivas

###### Componentes permitidos {#allowed-components}

Na guia **Componentes permitidos**, você define quais componentes estão disponíveis para o container de layout.

* Os componentes são agrupados por seus grupos de componentes, que podem ser expandidos e recolhidos.
* Um grupo inteiro pode ser selecionado ou desmarcados, marcando ou desmarcando o nome do grupo.
* Um sinal de menos representa pelo menos um, mas não todos os itens em um grupo estão selecionados.
* Há uma pesquisa disponível para filtrar um componente por nome.
* As contagens listadas à direita do nome do grupo de componentes representam o número total de componentes selecionados nesses grupos, independentemente do filtro.

![Guia Componentes permitidos](/help/sites-cloud/authoring/assets/templates-allowed-components-tab.png)

###### Componentes padrão {#default-components}

Na guia **Componentes padrão**, você define quais componentes são associados automaticamente a determinados tipos de mídia para que, quando um autor arrastar um ativo do navegador de ativos, o AEM saiba com qual componente associá-lo. Observe que somente os componentes com zonas para soltar estão disponíveis para essa configuração.

Selecionar **Adicionar mapeamento** para adicionar um componente totalmente novo e mapeamento de tipo MIME.

Selecione um componente na lista e selecione **Adicionar tipo** para adicionar outro tipo MIME a um componente já mapeado. Clique no ícone **Excluir** para remover a um tipo MIME.

![Guia Componentes padrão](/help/sites-cloud/authoring/assets/templates-default-components-tab.png)

###### Configurações responsivas {#responsive-settings}

Na guia **Configurações responsivas**, é possível configurar o número de colunas na grade resultante do container de layout.

#### Desbloquear e bloquear componentes {#unlock-and-lock-components}

Você desbloqueia/bloqueia componentes para definir se o conteúdo está disponível para alteração no modo **Conteúdo inicial**.

Quando um componente tiver sido desbloqueado:

* Um indicador de cadeado aberto é mostrado na borda.
* A barra de ferramentas do componente é ajustada de acordo.
* Qualquer conteúdo já inserido não será mais exibido no modo **Estrutura**.
   * O conteúdo já inserido é considerado conteúdo inicial e é visível apenas no modo **Conteúdo inicial**.
* Os pais do componente desbloqueado não podem ser movidos, recortados ou excluídos.

![Botão Bloquear componente](/help/sites-cloud/authoring/assets/templates-unlock-component.png)

Isso inclui desbloquear componentes de contêiner para que outros componentes possam ser adicionados, no modo **Conteúdo inicial** ou nas páginas resultantes. Se já tiver adicionado componentes/conteúdo ao container antes de desbloqueá-lo, eles não serão mais exibidos quando estiver no modo **Estrutura**, mas serão exibidos no modo **Conteúdo inicial**. No **modo Estrutura**, somente o componente de container será exibido com a lista de **Componentes permitidos**.

![Componentes permitidos](/help/sites-cloud/authoring/assets/templates-allowed-components.png)

Para economizar espaço, o contêiner de layout não é expandido para acomodar a lista de componentes permitidos. Em vez disso, o container se torna uma lista rolável.

Os componentes configuráveis são mostrados com um ícone de **Política**, no qual você pode tocar ou clicar para editar a política e as propriedades desse componente.

![Ícone de Componente configurável](/help/sites-cloud/authoring/assets/templates-configurable-component.png)

#### Relação com páginas existentes {#relationship-to-existing-pages}

Se a estrutura for atualizada depois de criar as páginas baseadas no modelo, então essas páginas refletirão as alterações no modelo. Um aviso é exibido na barra de ferramentas para lembrá-lo desse fato, junto com caixas de diálogo de confirmação.

![Banner que avisa que o modelo está sendo usado](/help/sites-cloud/authoring/assets/templates-in-use-banner.png)

### Editar um modelo - Conteúdo inicial - Criação {#editing-a-template-initial-content-author}

O modo **Conteúdo inicial** é usado para definir o conteúdo que aparecerá quando uma página for criada pela primeira vez com base no modelo. O conteúdo inicial poderá ser posteriormente editado pelos autores de página.

Embora todo o conteúdo criado no modo **Estrutura** seja visível no **Conteúdo inicial**, somente os componentes que foram desbloqueados podem ser selecionados e editados.

>[!NOTE]
>
>O modo **Conteúdo inicial** pode ser visto como um modo de edição para páginas criadas com esse modelo. Sendo assim, as políticas não estão definidas no modo **Conteúdo inicial**, mas no modo [**Estrutura**](#editing-a-template-structure-template-author).

* Os componentes desbloqueados que estão disponíveis para edição são marcados. Quando selecionados, eles têm uma borda azul:

  ![Modo Conteúdo inicial](/help/sites-cloud/authoring/assets/templates-initial-content-mode.png)

* Os componentes desbloqueados têm uma barra de ferramentas, permitindo editar e configurar o conteúdo:

  ![Componente desbloqueado](/help/sites-cloud/authoring/assets/templates-unlocked-components.png)

* Se um componente do contêiner foi desbloqueado (no modo **estrutura**), você pode adicionar novos componentes ao contêiner (no modo **Conteúdo inicial**). Os componentes adicionados no modo **Conteúdo inicial** podem ser movidos para ou excluído das páginas resultantes.

  Você pode adicionar o componente utilizando a área **Arraste componentes até aqui** ou a opção **Inserir novo componente** na barra de ferramentas do contêiner apropriado.

  ![Adicionar componente](/help/sites-cloud/authoring/assets/templates-add-component.png)
  ![Adicionar componente](/help/sites-cloud/authoring/assets/templates-add-component-dialog.png)

* Se o conteúdo inicial do modelo for atualizado depois que as páginas forem criadas com base no modelo, então essas páginas não serão afetadas por alterações no conteúdo inicial no modelo.

>[!NOTE]
>
>O conteúdo inicial se destina à preparação de componentes e do layout da página que servem como ponto de partida para a criação do conteúdo. Ele não se destina a ser o conteúdo real que permaneceria como está. Por esse motivo, o conteúdo inicial não pode ser traduzido.
>
>Se você precisar incluir texto traduzível no modelo, como em cabeçalhos ou rodapés, poderá usar os recursos de [localização dos componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=pt-BR).

### Editar um modelo - Layout - Autor do modelo {#editing-a-template-layout-template-author}

É possível definir o layout do modelo para um intervalo de dispositivos. O [Layout responsivo](/help/sites-cloud/authoring/features/responsive-layout.md) para modelos funciona como na criação de página.

>[!NOTE]
>
>As modificações no layout serão refletidas no modo **Conteúdo inicial**, mas nenhuma alteração será vista no modo **Estrutura**.

![Edição do modelo de layout](/help/sites-cloud/authoring/assets/templates-edit-layout.png)

### Editar um modelo - Política da página - Autor/desenvolvedor do modelo {#editing-a-template-page-policy-template-author-developer}

A política da página, incluindo as bibliotecas obrigatórias do lado do cliente, é mantida na opção **Política da página** do menu **Informações da página**.

Para acessar a caixa de diálogo **Política da página**:

1. No **Editor de modelo**, selecione **Informações da página** na barra de ferramentas, em seguida **Política da página** para abrir a caixa de diálogo.
1. A caixa de diálogo **Política da página** é aberta e dividida em duas seções:

   * A metade esquerda define as [políticas da página](#page-policies)
   * A metade direita define as [propriedades da página](#page-properties)

   ![Design da página](/help/sites-cloud/authoring/assets/templates-page-design.png)

#### Políticas da página {#page-policies}

É possível aplicar uma política de conteúdo ao modelo ou às páginas resultantes. Isso define a política de conteúdo do sistema de parágrafo principal na página.

![Política da página](/help/sites-cloud/authoring/assets/templates-page-policy.png)

* É possível selecionar uma política existente para a página na lista suspensa **Selecionar política**.

  ![Seletor de políticas](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

  Uma nova política pode ser adicionada ao selecionar o botão adicionar ao lado da **Selecionar política** lista suspensa. Atribua um novo título na variável **Título da política** campo.

  ![Botão Adicionar política](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

  A política existente selecionada no **Selecionar política** a lista suspensa pode ser copiada como uma nova política usando o botão copiar ao lado da lista suspensa. Atribua um novo título na variável **Título da política** campo. Por padrão, a política copiada será denominada **Cópia de X**, onde X é o título da política copiada.

  ![Botão Copiar política](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

* Defina um título para a política no campo **Título da política**. É necessário que a política tenha um título para que possa ser facilmente selecionada na variável **Selecionar política** lista suspensa.

  ![Título da política](/help/sites-cloud/authoring/assets/templates-policy-title.png)

* É opcional uma descrição da política no campo **Descrição da política**.
* No **Outros modelos que também usam a política selecionada** seção, é possível ver quais outros modelos usam a política selecionada na **Selecionar política** lista suspensa.

  ![Uso de políticas](/help/sites-cloud/authoring/assets/templates-policy-use.png)

#### Propriedades da página {#page-properties}

Usando as propriedades de página, é possível definir as bibliotecas do lado do cliente necessárias usando a caixa de diálogo **Design da página**. Essas bibliotecas do lado do cliente incluem folhas de estilo e o javascript a serem carregados com o modelo e as páginas criadas com esse modelo.

![Propriedades da página](/help/sites-cloud/authoring/assets/templates-page-properties.png)

* Especifique as bibliotecas do lado do cliente que deseja aplicar às páginas criadas com este modelo. Inserção do nome de uma biblioteca no campo de texto na seção **Bibliotecas do lado do cliente**.

  ![Bibliotecas do lado do cliente](/help/sites-cloud/authoring/assets/templates-client-side-libraries.png)

* Se as várias bibliotecas forem necessárias, clique no botão Adicionar para adicionar um campo de texto extra para o nome da biblioteca.

  ![Botão Adicionar](/help/sites-cloud/authoring/assets/templates-add-button.png)

  Adicione quantos campos de texto forem necessário para suas bibliotecas do lado do cliente.

* Defina a posição relativa das bibliotecas conforme necessário, ao arrastar os campos usando a alça de arrastar.

  ![Alça de arrastar](/help/sites-cloud/authoring/assets/templates-drag-handle.png)

>[!NOTE]
>
>Embora o autor do modelo possa especificar a política de página no modelo, ele precisa obter detalhes das bibliotecas do lado do cliente apropriadas do desenvolvedor.

### Editar um modelo - Propriedades da página inicial - Criação {#editing-a-template-initial-page-properties-author}

Usando a opção **Propriedades da página inicial**, é possível definir as [propriedades de página](/help/sites-cloud/authoring/fundamentals/page-properties.md) iniciais a ser usadas ao criar páginas resultantes.

1. No editor de modelo, selecione **Informações da página** na barra de ferramentas, em seguida **Propriedades da página inicial** para abrir a caixa de diálogo.

1. Na caixa de diálogo, é possível definir as propriedades que deseja aplicar às páginas criadas com esse modelo.

   ![Propriedades da página inicial dos modelos](/help/sites-cloud/authoring/assets/templates-initial-properties.png)

1. Confirme suas definições com **Concluído**.

## Práticas recomendadas   {#best-practices}

Ao criar modelos, você deve considerar:

1. O impacto das alterações no modelo depois que as páginas tiverem sido criadas a partir dele.

   Esta é uma lista das diferentes operações possíveis nos modelos, juntamente com como elas afetam as páginas criadas a partir deles:

   * Alterações na estrutura:

      * Elas são aplicadas imediatamente às páginas resultantes.
      * A publicação do modelo alterado ainda é necessária para que os visitantes vejam as alterações.

   * Alterações nas políticas de conteúdo e configurações de design:

      * Elas se aplicam imediatamente às páginas resultantes.
      * A publicação das alterações é necessária para que os visitantes vejam as alterações.

   * Alterações no conteúdo inicial:

      * Elas se aplicam somente às páginas criadas após as alterações no modelo.

   * As alterações no layout dependem se o componente modificado faz parte de:

      * Somente estrutura - aplicado imediatamente
      * Possui conteúdo inicial - somente em páginas criadas após a alteração

   Tenha muito cuidado quando:

   * Bloquear ou desbloquear componentes em modelos habilitados.
   * Isso pode ter efeitos colaterais, pois as páginas podem já está usando-os. Normalmente:

      * Os componentes desbloqueados (que estavam bloqueados) não estão presentes nas páginas existentes.
      * Bloquear os componentes (que eram editáveis) ocultará esse conteúdo para que não seja exibido nas páginas.

   >[!NOTE]
   >
   >O AEM emite avisos explícitos ao alterar o status de bloqueio de componentes em modelos que não são mais rascunhos.

1. [Criar suas próprias pastas](#creating-a-template-folder-admin) para modelos específicos do site.
1. [Publicar seus modelos](#publishing-a-template-template-author) a partir do console **Modelos**.
