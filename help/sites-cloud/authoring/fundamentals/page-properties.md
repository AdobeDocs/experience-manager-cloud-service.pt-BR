---
title: Editar as propriedades da página
description: Defina as propriedades desejadas para uma página
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
source-git-commit: 34247d8de3dc1a243eaac152b1d2036f9c237303
workflow-type: tm+mt
source-wordcount: '1955'
ht-degree: 58%

---

# Editar as propriedades da página {#editing-page-properties}

Você pode definir as propriedades desejadas para uma página. Eles podem variar dependendo da natureza da página. Por exemplo, algumas páginas podem estar conectadas a uma live copy, enquanto outras não estão, e as informações da live copy estarão disponível conforme apropriado.

## Propriedades da página {#page-properties}

As propriedades são distribuídas por várias guias.

### Básico {#basic}

* **Título e tags**

   * **Título**  - O título da página é exibido em vários locais. Por exemplo, a lista  **** de organização Sites e as visualizações de  **** Sitescard/list.
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

   Aplique uma identidade de marca consistente em todas as páginas, anexando um arquivo de marca a cada título de página. Essa funcionalidade requer o uso do Componente de página da versão 2.14.0 ou posterior dos [Componentes principais.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)

   * **Override**  - Marque a opção para definir o rastreamento da marca nesta página.
      * O valor será herdado por qualquer página secundária, a menos que também tenha seus valores **Override** definidos.
   * **Sobrepor valor**  - O texto do traçado da marca a ser anexado ao título da página.
      * O valor é anexado ao título da página após um caractere de barra vertical, como &quot;Toscânia cíclica | Sempre pronto para a WKND&quot;

* **ID HTML**

   * **ID**  - ID HTML a ser aplicada ao componente.

* **Mais títulos e descrições**

   * **Título da página**  - Um título a ser usado na página. Normalmente usado pelos componentes do título. Caso esteja vazio, o **Título** será usado.
   * **Título de navegação**  - Você pode especificar um título separado para usar na navegação (por exemplo, se desejar algo mais conciso). Se estiver vazio, o  **** Título será usado.
   * **Subtítulo**  - Um subtítulo para usar na página.
   * **Descrição**  - A sua descrição da página, finalidade ou qualquer outro detalhe que desejar adicionar.

* **Horário ligado/desligado**

   >[!NOTE]
   >
   > Consulte [Ativação e desativação - Configuração do acionador](/help/operations/replication.md#on-and-off-times-trigger-configuration) para obter detalhes sobre como configurar a replicação automática relacionada.

   >[!NOTE]
   >Se o **No Tempo** ou **Tempo desligado** estiver no passado e a replicação automática estiver configurada, a ação relevante será acionada imediatamente.

   * **No momento**  - a data e a hora em que a página publicada ficará visível (renderizada) no ambiente de publicação. A página deve ser publicada manualmente ou por replicação automática pré-configurada.

      * Se já [publicado (manualmente)](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) esta página será mantida inativa (oculta) até a renderização no horário especificado.
      * Se não for publicada e configurada para replicação automática, a página será publicada automaticamente e renderizada, no horário especificado.
      * Se não for publicada e não estiver configurada para replicação automática, a página não será publicada automaticamente, portanto, um 404 será visualizado quando uma tentativa de acessar a página for feita.
   * **Hora de desligar**  - Semelhante ao que é usado em combinação com  **Hora de ligar**, isso define o horário em que a página publicada ficará oculta no ambiente de publicação.

   * Deixe esses campos (**No horário** e **Tempo desligado**) vazios para as páginas que deseja publicar imediatamente e que estão disponíveis no ambiente de publicação até que sejam desativadas (o cenário normal).


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


   * **Adicionar**  - Toque ou clique para mostrar um campo para definir uma URL personalizada para a página.
      * Toque ou clique novamente para adicionar vários.
      * Toque ou clique no ícone **Remove** para excluir a URL personalizada.
   * **Redirecionar URL personalizada**  - Indica se você deseja que a página use a URL personalizada.


### Avançado  {#advanced}

* **Configurações**

   * **Idioma**  - O idioma da página
   * **Raiz do idioma**  - Deve ser verificado se a página é a raiz de uma cópia de idioma
   * **Redirecionar**  - Indica a página para a qual essa página deve redirecionar automaticamente
   * **Design**  - Indica se a página é exibida ou oculta na navegação de página do site resultante
   * **Alias**  - Especifica um alias a ser usado com esta página

   >[!NOTE]
   >
   >O alias ajusta a propriedade `sling:alias` para definir um nome de alias para o recurso (isso afeta apenas o recurso, não o caminho).
   >
   >Por exemplo: se você definir um alias de `latin-lang` para o `/content/we-retail/spanish` nó, essa página poderá ser acessada por meio de `/content/we-retail/latin-language`
   >
   >Para obter mais detalhes, consulte Nomes de página localizados em SEO e Práticas recomendadas de gerenciamento de URL.

   <!--
  >For further details see [Localized page names under SEO and URL Management Best Practices](/help/managing/seo-and-url-management.md#localized-page-names).
  -->

* **Configuração**

   * **Configuração da nuvem**  - o caminho para a configuração

* **Configurações do modelo**

   * **Modelos permitidos**  -  [Define a lista de modelos que estará ](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) disponível nesta subramificação

* **Requisitos de autenticação**

   * **Habilitar**  - Habilitar o uso da autenticação para acessar a página

      >[!NOTE]
      >
      >Os grupos de usuários fechados para a página são definidos na guia **[Permissões](#permissions)**.

   * **Página de logon**  - A página a ser usada para logon

* **Exportar**

   * **Exportar configuração**  - Especifica uma configuração de exportação

### Miniatura  {#thumbnail}

Configurar a miniatura da página

* **Gerar visualização**  - Gere uma visualização da página para usar como miniatura
* **Carregar imagem**  - Carregue uma imagem para usar como miniatura
* **Selecionar imagem**  - Selecione um ativo existente para usar como miniatura
* **Reverter**  - essa opção ficará disponível depois que você fizer uma alteração na miniatura. Se você não quiser manter sua alteração, poderá reverter essa alteração antes de salvar.

### Redes sociais {#social-media}

* **Compartilhamento em rede social**

   Define as opções de compartilhamento disponíveis na página. Expõe as opções disponíveis para o [Componente de compartilhamento principal](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/sharing.html).

   * **Permitir o compartilhamento de usuário para Facebook**
   * **Permitir o compartilhamento de usuário para Pinterest**
   * **Variação preferida de XF**
      * Define a variação do fragmento de experiência usada para gerar metadados para a página

### Cloud Services {#cloud-services}

* **Configurações de Cloud Service**  - Defina as propriedades para os serviços em nuvem

   <!--Define properties for [cloud services](/help/sites-developing/extending-cloud-config.md).
  -->

### Personalização {#personalization}

* **Configurações do ContextHub**

   * **Caminho do ContextHub**  - Defina a configuração do  [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **Caminho dos segmentos**  - Definir o caminho  [dos segmentos](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **Configuração de direcionamento**

   * **Marca**  - Define uma  [Marca para especificar um escopo para a segmentação](/help/sites-cloud/authoring/personalization/targeted-content.md).
   >[!NOTE]
   >Para selecionar essa opção, é necessário que a conta de usuário esteja no `Target Administrators`grupo.

### Permissões  {#permissions}

* **Permissões**

   * Adicionar permissões
   * Editar grupo de usuários fechado
   * Exibir as permissões efetivas

   <!--[Add Permissions](/help/sites-administering/user-group-ac-admin.md) -->

   <!-- [Edit Closed User Group](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)-->

   <!-- View the [Effective Permissions](/help/sites-administering/user-group-ac-admin.md)-->

### Blueprint {#blueprint}

Essa guia só fica visível para páginas que servem como blueprints. Os blueprints servem como base para as Live Copies são parte do [Gerenciamento de vários sites.](/help/sites-cloud/administering/msm/overview.md)

* **Live Copies atuais**  - Lista as páginas que são baseadas nesta (ou seja, que são Live Copies de) página do blueprint

* **Configurações de implantação**  - Controla as circunstâncias sob as quais as modificações serão propagadas na Live Copy

### Live Copy  {#live-copy}

* **Sincronizar**  - Sincronize a Live Copy com o Blueprint, mantendo as modificações locais
* **Redefinir**  - Redefinir Live Copy para estado do Blueprint, removendo modificações locais
* **Suspender**  - Suspender Live Copy de modificações adicionais na implantação
* **Desanexar**  - Desanexar Live Copy do Blueprint

* **Fonte**

   * Exibe o caminho do blueprint para esta Live Copy

* **Status**

   * Lista o status atual da Live Copy da página

* **Configuração**

   * **Herança da Live Copy**  - se marcada, a configuração da Live Copy é eficaz em todos os filhos
   * **Herdar configurações de implantação do Pai**  - se marcada, a configuração de implantação é herdada do pai da página
   * **Escolher configuração de implementação**  - Define as circunstâncias sob as quais as modificações serão propagadas do Blueprint e só estarão disponíveis quando  **Herdar configurações de implementação dos** parceiros não selecionados

### Visualizar {#preview}

Quando um ambiente de Visualização estiver ativado, você verá:

* URL de visualização - o URL usado para acessar o conteúdo no ambiente de visualização

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
   * Os campos que são comuns, mas têm valores diferentes em várias páginas, serão indicados com um valor especial; como o texto `<Mixed Entries>`. Para evitar a perda de dados, alguns cuidados devem ser tomados ao editar os campos.

>[!NOTE]
>
>O componente da página pode ser configurado para especificar os campos disponíveis para edição de itens em massa. Consulte Configurar sua página para a edição de itens em massa das propriedades da página.

<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
