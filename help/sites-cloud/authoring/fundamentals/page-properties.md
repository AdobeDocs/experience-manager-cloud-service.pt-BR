---
title: Editar as propriedades da página
description: Definir as propriedades obrigatórias de uma página
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
source-git-commit: 5a43b6db8a5743b87d6eafdad31418e6cb45d22b
workflow-type: ht
source-wordcount: '2363'
ht-degree: 100%

---

# Editar as propriedades da página {#editing-page-properties}

Você pode definir as propriedades desejadas para uma página. Isso pode variar dependendo da natureza da página. Por exemplo, algumas páginas podem estar conectadas a uma Live Copy, enquanto outras não estão, e as informações da Live Copy estarão disponíveis conforme apropriado.

## Propriedades da página {#page-properties}

As propriedades são distribuídas por várias guias.

### Básico {#basic}

* **Título e tags**

   * **Título** - o título da página é exibido em vários locais. Por exemplo, a lista da guia **Sites** e as exibições de cartão/lista dos **Sites**.
      * Este campo é obrigatório.
   * **Tags**: aqui você pode adicionar ou remover as tags da página, atualizando a lista na caixa de seleção.
      * Após selecionar uma tag, ela é listada abaixo da caixa de seleção. Você pode remover uma tag dessa lista usando o ícone “x”.
      * Uma tag totalmente nova pode ser inserida digitando o nome em uma caixa de seleção vazia.
         * A nova tag será criada quando você pressionar a tecla Enter.
         * A nova tag será então exibida com uma pequena estrela à direita, indicando que é uma tag nova.
      * Com a funcionalidade de menu suspenso, é possível selecionar tags existentes.
      * Um “x” é exibido ao passar o mouse sobre uma entrada de tag na caixa de seleção, e esse ícone pode ser usado para remover a tag desta página.
      * Para obter mais informações sobre tags, consulte [Uso de tags](/help/sites-cloud/authoring/features/tags.md).
   * **Ocultar na navegação**: indica se a página está visível ou oculta na navegação de página do site resultante.

* **Marcas**

   Aplique uma identidade de marca consistente em todas as páginas, anexando uma descrição da marca a cada título de página. Essa funcionalidade requer o uso do Componente de página da versão 2.14.0 ou posterior do [Componentes principais.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)

   * **Descrição da marca**

      * **Substituir** - marque essa opção para definir a descrição da marca nesta página.
         * O valor será herdado por qualquer página secundária, a menos que também tenha definidos seus valores para **Substituir**.
      * **Substituir valor** - o texto da descrição da marca a ser anexado ao título da página.
         * O valor é anexado ao título da página após um caractere de barra vertical, como &quot;Cycling Tuscany | Sempre pronto para a WKND&quot;

* **ID HTML**

   * **ID** - a ID HTML a ser aplicada ao componente.

* **Mais títulos e descrições**

   * **Título da página** - um título a ser usado na página. Normalmente é usado pelos componentes de título. Se estiver vazio, o **Título** da página será usado.
   * **Título de navegação** - você pode especificar um título separado para usar na navegação (por exemplo, caso deseje algo mais conciso). Caso esteja vazio, o **Título** será usado.
   * **Subtítulo** - um subtítulo para usar na página.
   * **Descrição** - a sua descrição da página, a finalidade dela ou qualquer outro detalhe que desejar adicionar.

* **Horário ligado/desligado**

   >[!NOTE]
   >
   > Consulte [Momento da ativação e da desativação - Configuração do acionador](/help/operations/replication.md#on-and-off-times-trigger-configuration) para obter detalhes sobre como configurar a replicação automática relacionada.

   >[!NOTE]
   >Se tanto o **Momento da ativação** quanto o **Momento da desativação** estiverem no passado e a replicação automática estiver configurada, a ação relevante será acionada imediatamente.

   * **Momento da ativação** - a data e a hora em que a página publicada ficará visível (renderizada) no ambiente de publicação. A página deve ser publicada manualmente ou por replicação automática pré-configurada.

      * Se já [publicada (manualmente)](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) essa página será mantida inativa (oculta) até a renderização no horário especificado.
      * Se não for publicada e configurada para replicação automática, a página será publicada automaticamente e, em seguida, renderizada no horário especificado.
      * Se não for publicada e não estiver configurada para replicação automática, a página não será publicada automaticamente. Um 404 será exibido quando for feita uma tentativa de acessar a página.
   * **Momento de desligar** - semelhante a e frequentemente utilizado em combinação com **Momento de ligar**, define o momento em que a página publicada será oculta no ambiente de publicação.

   * Deixe esses campos (**Momento de ligar** e **Hora de desligar**) vazios para páginas que deseja publicar imediatamente e que estão disponíveis no ambiente de publicação até que sejam desativadas (o cenário normal).


* **URL personalizada**

   * Permite inserir uma URL personalizada para esta página, o que permite utilizar uma URL mais curta e/ou expressiva.
   * Por exemplo, se o URL personalizado estiver definido como `welcome` para a página identificada pelo caminho`/v1.0/startpage` para o site `http://example.com`, em seguida, `http://example.com/welcome`será o URL personalizado de `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >URLs personalizadas:
   >
   >* Ela deve ser exclusiva, portanto, é necessário verificar se o valor já não está sendo usado por outra página.
   >* Não é compatível com padrões de regex.
   >* Não deve ser definido como uma página existente.


   * **Adicionar** - toque ou clique para mostrar um campo e definir uma URL personalizada para a página.
      * Toque ou clique novamente para adicionar vários.
      * Toque ou clique no ícone **Remover** para excluir o URL personalizado.
   * **Redirecionar URL personalizado** - indica se você deseja que a página use o URL personalizado.


### Avançado  {#advanced}

* **Configurações**

   * **Idioma** - o idioma da página
   * **Raiz de idioma** - deve ser marcado se a página for a raiz de uma cópia de idioma
   * **Redirecionar** - indica a página de redirecionamento automático para a página atual.  com um status HTML `302 Found`.
      * **Redirecionamento permanente** — quando marcado, a página redireciona para o caminho de destino fornecido junto com um status HTML `301 Moved Permanently`.
   * **Design** - indica se a página está visível ou oculta na navegação de página do site resultante
   * **Pseudônimo** - especifica um pseudônimo para ser usado com esta página
      * Por exemplo: se você definir um pseudônimo de `private` para a página `/content/wknd/us/en/magazine/members-only`, essa página poderá ser acessada por meio de `/content/wknd/us/en/magazine/private`
      * A criação de um pseudônimo define a propriedade de `sling:alias` no nó da página, que afeta apenas o recurso, não o caminho do repositório.
      * As páginas acessadas por pseudônimos no editor não podem ser publicadas. As [Opções de publicação](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) no editor só estão disponíveis para páginas acessadas por meio de seus caminhos de fato.
      * Para obter mais detalhes, consulte [Nomes de páginas localizados em Práticas recomendadas de gerenciamento de SEO e URL](/help/overview/seo-and-url-management.md#localized-page-names).

* **Configuração**

   * **Herdado de &lt;path>**: ativa/desativa a herança; habilita/desabilita a opção de selecionar a **Configuração da nuvem** 

   * **Configuração da nuvem**: o caminho para a configuração selecionada

* **Configurações de modelos**

   * **Modelos permitidos** - [define a lista de modelos que estará disponível](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) dentro desta sub-ramificação

* **Requisitos de autenticação**

   * **Habilitar** - habilitar o uso de autenticação para acessar a página

      >[!NOTE]
      >
      >Os grupos de usuários fechados para a página são definidos na guia **[Permissões](#permissions)**.

   * **Página de logon** - a página a ser usada para logon

* **Exportar**

   * **Exportar configuração** - especifica uma configuração de exportação

* **SEO**

   * **URL canônica**: pode ser usada para sobrescrever a URL canônica da página; se deixada em branco, a URL da página será a URL canônica

   * **Tags de robôs**: seleciona as tags de robôs para controlar o comportamento dos rastreadores de mecanismos de pesquisa.

      >[!NOTE]
      >
      >Algumas das opções entram em conflito entre si. Em caso de conflito, a opção mais permissiva tem prioridade.

   * **Gerar mapa do site**: quando selecionado, um arquivo sitemap.xml será gerado para esta página e suas descendentes

### Imagens {#images}

* **Imagem em destaque**

   Selecione e configure a imagem a ser colocada em destaque. Isso é usado em componentes que fazem referência à página; por exemplo, teasers, listas de páginas etc.

   * **Imagem**

      Você pode **Selecionar** um ativo ou procurar um arquivo para fazer upload e, em seguida, **Editar** ou **Limpar**.

   * **Texto alternativo**: um texto utilizado para representar o significado e/ou a função da imagem; por exemplo, para ser usado por leitores de tela.

   * **Herdar - Valor obtido do ativo do DAM**: quando marcado, o texto alternativo será preenchido com o valor dos `dc:description`metadados no DAM

* **Miniatura**

   Configurar a miniatura de página

   * **Gerar visualização** - gere uma visualização da página para usar como miniatura
   * **Fazer upload da imagem** - faça upload de uma imagem para usar como miniatura
   * **Selecionar imagem** - selecione um Ativo existente para usar como miniatura
   * **Reverter** - esta opção fica disponível após você ter feito uma alteração na miniatura. Se você não quiser manter a alteração, poderá revertê-la antes de salvar.

### Cloud Services {#cloud-services}

* **Configurações do Cloud Service** - defina propriedades para os serviços em nuvem

### Personalização {#personalization}

* **Configurações do ContextHub**

   * **Herdado de &lt;path>**: ativa/desativa a herança; habilita/desabilita a opção de selecionar o **caminho do ContextHub** e o **caminho dos segmentos**

   * **Caminho do ContextHub** - defina a [configuração do ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **Caminho dos segmentos** - defina o [Caminho dos segmentos](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **Configuração de direcionamento**

   * **Marca** - defina uma [Marca para especificar um escopo para Direcionamento](/help/sites-cloud/authoring/personalization/targeted-content.md).
   >[!NOTE]
   >Para selecionar essa opção, é necessário que a conta de usuário esteja no `Target Administrators`grupo.

### Permissões  {#permissions}

* **Permissões**

   * **Adicionar permissões**
   * **Editar grupo de usuários fechado**
   * Exibir as **Permissões ativas**

### Blueprint {#blueprint}

Essa guia só fica visível para páginas que servem como blueprints. Os blueprints servem como base para as Live Copies que fazem parte do [Gerenciamento de vários sites.](/help/sites-cloud/administering/msm/overview.md)

* **Live Copies atuais** - lista páginas que são baseadas nesta (ou seja, são Live Copies da) página do blueprint

* **Configurações de implantação** - controla as circunstâncias sob as quais as modificações serão propagadas no Live Copy

### Live Copy  {#live-copy}

Essa guia só fica visível para páginas configuradas como Live Copies. Assim como os blueprints, as Live Copies fazem parte do [Gerenciamento de vários sites.](/help/sites-cloud/administering/msm/overview.md).

* **Sincronizar** - sincronizar o Live Copy com o blueprint, mantendo as modificações locais
* **Redefinir** - redefinir o Live Copy para o estado de blueprint, removendo as modificações locais
* **Suspender** - suspender modificações adicionais de implantação na Live Copy 
* **Desanexar** - desanexar Live Copy do blueprint

* **Origem**

   * Exibe o caminho do blueprint para esta Live Copy

* **Status**

   * Lista o status atual da Live Copy da página

* **Configuração**

   * **Herança da Live Copy** - quando marcado, a configuração da Live Copy terá efeito em todas as páginas secundárias
   * **Herdar configurações de implantação da principal** - se marcado, a configuração de implantação é herdada da página principal
   * **Escolher configuração de implantação** - define as circunstâncias sob as quais as modificações serão propagadas a partir do blueprint e só estarão disponíveis quando **Herdar configurações de implantação da principal** não estiver selecionado

### Visualizar {#preview}

Quando um ambiente de Visualização estiver habilitado, você verá:

* URL de visualização - o URL usado para acessar o conteúdo no ambiente de Visualização

### Aplicativo web progressivo {#progressive-web-app}

Por meio de uma configuração simples, um autor de conteúdo agora pode ativar recursos do aplicativo web progressivo (PWA) para experiências criadas no AEM Sites.

>[!NOTE]
>
>Para obter mais detalhes, consulte [Ativação de recursos do aplicativo web progressivo](/help/sites-cloud/authoring/features/enable-pwa.md).

* **Configurar experiência instalável**

   * **Ativar o PWA**: ativa/desativa o recurso; isso permite que os usuários instalem o site como um PWA
   * **StartupURL**: URL de inicialização preferencial
   * **Modo de exibição**: como o navegador deve ser oculto ou apresentado ao usuário no dispositivo local
   * **Orientação da tela**: como o PWA lidará com a orientação dos dispositivos
   * **Cor do tema**: isso define a cor do aplicativo, o que afeta como o sistema operacional do usuário local exibe a barra de ferramentas da interface nativa e os controles de navegação
   * **Cor do fundo**: a cor do fundo do aplicativo, exibido quando o aplicativo é carregado
   * **Ícone**: o ícone que representa o aplicativo no dispositivo do usuário

* **Gerenciamento de cache (avançado)**

   * **Estratégia de armazenamento em cache e frequência de atualização de conteúdo**: define o modelo de armazenamento em cache do seu PWA
   * **Arquivos para armazenar em cache para uso offline**
      * **Pré-armazenamento em cache de arquivos (visualização técnica)**: os arquivos hospedados no AEM serão salvos no cache do navegador local quando o serviço secundário estiver sendo instalado e antes de ser usado
      * **Bibliotecas do lado do cliente**: bibliotecas do lado do cliente para armazenar em cache e oferecer a experiência offline
      * **Inclusões de caminhos**: as solicitações de rede para os caminhos definidos são interceptadas e o conteúdo em cache é retornado de acordo com a estratégia de armazenamento em cache e a frequência de atualização de conteúdo configuradas
      * **Exclusões de caminhos**: esses arquivos nunca serão armazenados em cache, independentemente das configurações definidas em Pré-armazenamento em cache de arquivos e Inclusões de caminhos

## Editar as propriedades da página {#editing-page-properties-1}

* No console **Sites**:
   * [Criação de uma nova página](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) (um subconjunto das propriedades)
   * Ao clicar ou tocar em **Propriedades**
      * Para uma única página
      * Para várias páginas (somente um subconjunto das propriedades está disponível para edição em massa)
* No editor de páginas:
   * Ao usar **Informações da página** (em seguida, **Abrir propriedades**)

### No console Sites - Página única {#from-the-sites-console-single-page}

Ao clicar ou tocar em **Propriedades** para definir as propriedades da página:

1. Usando o console **Sites**, navegue até o local da página no qual deseja visualizar e editar as propriedades.
1. Selecione a opção **Propriedades da exibição** para a página desejada usando uma das seguintes opções:
   * [Ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)
   * As propriedades da página serão exibidas usando as guias adequadas.
1. Exiba ou edite as propriedades conforme necessário.
1. Em seguida, clique em **Salvar** para salvar as atualizações, e em **Fechar** para retornar ao console.

### Ao editar uma página {#when-editing-a-page}

Ao editar uma página, você pode usar as **Informações da página** para definir as propriedades da página:

1. Abra a página na qual deseja editar as propriedades.
1. Selecione o ícone **Informações da página** para abrir o menu de seleção:
1. Selecione a opção **Abrir propriedades** e será exibida uma caixa de diálogo para você editar as propriedades classificadas por guia. Os seguintes botões também estão disponíveis à direita da barra de ferramentas:
   * **Cancelar**
   * **Salvar e fechar**
1. Use o botão **Salvar e fechar** para salvar as alterações.

### No console Sites - Várias páginas {#from-the-sites-console-multiple-pages}

No console **Sites**, é possível selecionar várias páginas e usar **Propriedades de exibição** para exibir e/ou editar as propriedades da página. Isso é conhecido como edição em massa das propriedades da página.

>[!NOTE]
>
>A edição em massa de propriedades também está disponível no Assets. É muito semelhante, mas difere em alguns pontos. Consulte Editar propriedades de vários ativos para obter detalhes.
>
>Também existe o Editor de itens em massa, que permite que você pesquise o conteúdo de várias páginas usando o GQL (Google Query Language) e, em seguida, editar o conteúdo diretamente no editor de itens em massa antes de salvar as alterações para as páginas de origem.

<!--
>Bulk editing of properties is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for details.
>
>There is also the [Bulk Editor](/help/sites-administering/bulk-editor.md), which allows you to search for content from multiple pages using GQL (Google Query Language) and then edit the content directly in the bulk editor before saving your changes to the originating pages.
-->

Você pode selecionar várias páginas para a edição em massa por meio de vários métodos, incluindo:

* Ao navegar pelos consoles dos **Sites**
* Depois de usar a função **Pesquisar** para localizar um conjunto de páginas

Após selecionar as páginas e, em seguida, clicar ou tocar na opção **Propriedades**, as propriedades em massa serão mostradas:

![Propriedades da página de edição em massa](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

Só é possível editar em massa as páginas que:

* Compartilham o mesmo tipo de recurso
* Não fazem parte de uma live copy
   * Uma mensagem será mostrada quando as propriedades forem abertas, se qualquer página estiver em uma live copy.

Depois de entrar na edição de itens em massa é possível:

* **Exibir**

   * Uma lista das páginas afetadas
      * Você pode selecionar/desmarcar, se necessário
      * Guias
         * Assim como ao visualizar propriedades de uma única página, as propriedades são ordenadas em guias.
   * Um subconjunto de propriedades
      * As propriedades que estão disponíveis em todas as páginas selecionadas e tenham sido explicitamente definidas como disponíveis para a edição de itens em massa estão visíveis.
      * Se você reduzir a seleção de página para uma página, em seguida, todas as propriedades ficarão visíveis.
   * Propriedades comuns com um valor comum
      * Apenas as propriedades com um valor comum são mostradas no modo de Exibição.
      * Quando o campo tem vários valores (por exemplo, Tags), eles só serão exibidos quando *todos* forem comuns. Se apenas alguns forem comuns, eles só serão exibidos durante a edição.
      * Quando não existirem propriedades com um valor comum, uma mensagem será exibida.

* **Editar**

   * Você pode atualizar os valores nos campos disponíveis.
      * Os novos valores serão aplicados a todas as páginas selecionadas ao escolher **Concluído**.
      * Quando o campo tem vários valores (por exemplo, tags), você pode anexar um novo valor ou remover um valor comum.
   * Os campos que são comuns, mas têm valores diferentes em várias páginas, serão indicados com um valor especial; como o texto `<Mixed Entries>`.
