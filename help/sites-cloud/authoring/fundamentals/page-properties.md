---
title: Editar as propriedades da página
description: Defina as propriedades desejadas para uma página
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
source-git-commit: 628a95d7b7d0e84bfc8edecaaf127dd83ce1e578
workflow-type: tm+mt
source-wordcount: '2428'
ht-degree: 82%

---

# Editar as propriedades da página {#editing-page-properties}

Você pode definir as propriedades desejadas para uma página. Eles podem variar dependendo da natureza da página. Por exemplo, algumas páginas podem estar conectadas a uma live copy, enquanto outras não estão, e as informações da live copy estarão disponível conforme apropriado.

## Propriedades da página {#page-properties}

As propriedades são distribuídas por várias guias.

### Básico {#basic}

* **Título e tags**

   * **Título** - o título da página é exibido em vários locais. Por exemplo, a lista da guia **Sites** e as exibições de cartão/lista dos **Sites**.
      * Este é um campo obrigatório.
   * **Tags** - Aqui você pode adicionar ou remover as tags da página, atualizando a lista na caixa de seleção.
      * Após selecionar uma tag, ela é listada abaixo da caixa de seleção. Você pode remover uma tag dessa lista usando o x.
      * Uma tag totalmente nova pode ser inserida, digitando o nome em uma caixa de seleção vazia.
         * A nova tag será criada ao apertar a tecla enter.
         * A nova tag será então exibida com uma pequena estrela à direita, indicando que é uma nova tag.
      * Com a funcionalidade suspensa, você pode selecionar a partir das tags existentes.
      * Um x será exibido ao passar o mouse em cima de uma entrada de tag na caixa de seleção, que pode ser usado para remover a tag desta página.
      * Para obter mais informações sobre tags, acesse [Usar tags](/help/sites-cloud/authoring/features/tags.md).
   * **Ocultar na navegação** - Indica se a página está visível ou oculta na navegação de página do site resultante.

* **Marcas**

   Aplique uma identidade de marca consistente em todas as páginas, anexando uma descrição da marca a cada título de página. Essa funcionalidade requer o uso do Componente de página da versão 2.14.0 ou posterior do [Componentes principais.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)

   * **Slug da marca**

      * **Substituir** - marque essa opção para definir a descrição da marca nesta página.
         * O valor será herdado por qualquer página secundária, a menos que também tenha definidos seus valores para **Substituir**.
      * **Substituir valor** - o texto da descrição da marca a ser anexado ao título da página.
         * O valor é anexado ao título da página após um caractere de barra vertical, como &quot;Cycling Tuscany | Sempre pronto para a WKND&quot;

* **ID HTML**

   * **ID** - a ID HTML a ser aplicada ao componente.

* **Mais títulos e descrições**

   * **Título da página** - um título a ser usado na página. Normalmente usado pelos componentes do título. Caso esteja vazio, o **Título** será usado.
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

   * Permite que você insira uma vanity URL para esta página, o que pode permitir que você tenha um URL menor e/ou mais expressivo.
   * Por exemplo, se o URL personalizado estiver definido como `welcome` para a página identificada pelo caminho`/v1.0/startpage` para o site `http://example.com`, em seguida, `http://example.com/welcome`será o URL personalizado de `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >URLs personalizadas:
   >
   >* Deve ser exclusiva, dessa forma, é necessário tomar cuidado para que o valor não seja utilizado por outra página.
   >* Não é compatível com padrões do regex.
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
      * Para obter mais detalhes, consulte [Nomes de página localizados em SEO e Práticas recomendadas de gerenciamento de URL](/help/overview/seo-and-url-management.md#localized-page-names).

* **Configuração**

   * **Herdado de &lt;path>** - ativar/desativar herança; alterna a disponibilidade de **Configuração na nuvem** para seleção

   * **Configuração na nuvem** - O caminho para a configuração selecionada

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

   * **Url Canônica** - pode ser usado para substituir o Url canônico da página; se deixado em branco, o URL da página será seu URL canônico

   * **Tags de robôs** - selecione as tags de robôs para controlar o comportamento dos rastreadores de mecanismo de pesquisa.

      >[!NOTE]
      >
      >Algumas das opções estão em conflito entre si. Em caso de conflito, a opção mais permissiva tem precedência.

   * **Gerar mapa de site** - quando selecionado, um sitemap.xml será gerado para esta página e seus descendentes

### Imagens {#images}

* **Imagem em destaque**

   Selecione e configure a imagem a ser apresentada. Isso é usado em componentes que fazem referência à página; por exemplo, teasers, listas de páginas etc.

   * **Imagem**

      Você pode **Selecionar** um Ativo ou procure um arquivo para fazer upload, em seguida **Editar** ou **Limpar**.

   * **Texto alternativo** - um texto utilizado para representar o significado e/ou a função da imagem; por exemplo, para uso por leitores de tela.

   * **Herdar - Valor obtido do ativo DAM** - quando marcado, isso preencherá o texto alternativo com o valor da variável `dc:description`metadados no DAM

* **Miniatura**

   Configurar a miniatura de página

   * **Gerar visualização** - gere uma visualização da página para usar como miniatura
   * **Fazer upload da imagem** - faça upload de uma imagem para usar como miniatura
   * **Selecionar imagem** - selecione um Ativo existente para usar como miniatura
   * **Reverter** - esta opção fica disponível após você ter feito uma alteração na miniatura. Se você não quiser manter sua alteração, poderá reverter essa alteração antes de salvar.

### Redes sociais {#social-media}

* **Compartilhamento em rede social**

   Define as opções de compartilhamento disponíveis na página. Expõe as opções disponíveis para o [Componente de compartilhamento principal](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/sharing.html?lang=pt-BR).

   * **Permitir o compartilhamento de usuário para Facebook**
   * **Permitir o compartilhamento de usuário para Pinterest**
   * **Variação preferida de XF**
      * Define a variação do fragmento de experiência usada para gerar metadados para a página

### Cloud Services {#cloud-services}

* **Configurações do Cloud Service** - defina propriedades para os serviços em nuvem

### Personalização {#personalization}

* **Configurações do ContextHub**

   * **Herdado de &lt;path>** - ativar/desativar herança; alterna a disponibilidade de **Caminho do ContextHub** e **Caminho dos segmentos** para seleção

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
   * Exibir as **permissões efetivas**

### Blueprint {#blueprint}

Essa guia só fica visível para páginas que servem como blueprints. Blueprints servem como base para as Live Copies que fazem parte do [Gerenciamento de vários sites.](/help/sites-cloud/administering/msm/overview.md)

* **Live Copies atuais** - lista páginas que são baseadas nesta (ou seja, são Live Copies da) página do blueprint

* **Configurações de implantação** - controla as circunstâncias sob as quais as modificações serão propagadas no Live Copy

### Live Copy  {#live-copy}

Essa guia só fica visível para páginas configuradas como cópias em tempo real.

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
>Para obter mais detalhes, consulte [Ativação de recursos progressivos do aplicativo web](/help/sites-cloud/authoring/features/enable-pwa.md).

* **Configurar experiência instalável**

   * **Ativar o PWA** - ativar/desativar o recurso; permite que os usuários instalem o site como um PWA
   * **StartupURL** - o URL de inicialização preferencial
   * **Modo de exibição** - como o navegador deve ser oculto ou apresentado ao usuário no dispositivo local
   * **Orientação da tela** - como o PWA lidará com as orientações dos dispositivos
   * **Cor do tema** - a cor do aplicativo que afeta a forma como o sistema operacional do usuário local exibe a barra de ferramentas da interface do usuário nativa e os controles de navegação
   * **Cor do plano de fundo** - a cor de fundo do aplicativo, que é mostrada à medida que o aplicativo é carregado
   * **Ícone** - o ícone que representa o aplicativo no dispositivo do usuário

* **Gerenciamento de cache (avançado)**

   * **Estratégia de armazenamento em cache e frequência de atualização de conteúdo** - define o modelo de armazenamento em cache do seu PWA
   * **Arquivos para armazenar em cache para uso offline**
      * **Pré-armazenamento em cache de arquivos (pré-visualização técnica)** - os arquivos hospedados no AEM serão salvos no cache do navegador local quando o trabalhador do serviço estiver instalando e antes de ser usado
      * **Bibliotecas do lado do cliente** - bibliotecas do lado do cliente para armazenar em cache para experiência offline
      * **Inclusões de caminho** - as solicitações de rede para os caminhos definidos são interceptadas e o conteúdo em cache é retornado de acordo com a estratégia de Cache configurada e a frequência de atualização de conteúdo
      * **Exclusões de caminho** - esses arquivos nunca serão armazenados em cache, independentemente das configurações em File pre-caching e Path insions

## Editar as propriedades da página {#editing-page-properties-1}

* No console **Sites**:
   * [Criação de uma nova página](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) (um subconjunto das propriedades)
   * Ao clicar ou tocar em **Propriedades**
      * Para uma página única
      * Para várias páginas (apenas um subconjunto das propriedades está disponível para edição em massa)
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

É possível selecionar várias páginas para a edição de itens em massa através de diversos métodos, incluindo:

* Ao navegar no console **Sites**
* Após usar a opção **Pesquisar** para localizar um conjunto de páginas

Após selecionar as páginas e, em seguida, clicar ou tocar na opção **Propriedades**, as propriedades em massa serão mostradas:

![Propriedades da página de edição em massa](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

Só é possível fazer a edição de itens em massa nas páginas que:

* Compartilham o mesmo tipo de recurso
* Não fazem parte de uma live copy
   * Uma mensagem será mostrada quando as propriedades forem abertas, se qualquer página estiver em uma live copy.

Depois de entrar na edição de itens em massa é possível:

* **Exibir**

   * Uma lista das páginas impactadas
      * Você pode selecionar/desmarcar conforme necessário
      * Guias
         * As propriedades são ordenadas em guias, como ao exibir as propriedades para uma página única.
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
      * Quando o campo tem vários valores (por exemplo, Tags), você pode acrescentar um novo valor ou remover um valor comum.
   * Os campos que são comuns, mas têm valores diferentes em várias páginas, serão indicados com um valor especial; como o texto `<Mixed Entries>`.

>[!NOTE]
>
>O componente da página pode ser configurado para especificar os campos disponíveis para edição de itens em massa. Consulte Configurar sua página para a edição de itens em massa das propriedades da página.

<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
