---
title: Modelos de páginas
description: Os modelos de página são usados ao criar uma página que será usada como base para a nova página
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: f5aa9229ff06fdcff5474594269ebcf9daf09e41
workflow-type: tm+mt
source-wordcount: '3300'
ht-degree: 6%

---

# Modelos de páginas {#page-templates}

Ao criar uma página, é necessário selecionar um modelo. O modelo de página é usado como a base da nova página. O modelo define a estrutura da página resultante, qualquer conteúdo inicial e os componentes que podem ser usados (propriedades de design). Isso tem várias vantagens:

* Os modelos de página permitem que autores especializados [criar e editar modelos](/help/sites-cloud/authoring/features/templates.md).
   * Tais autores especializados são chamados **autores de modelo**
   * Os autores do modelo devem ser membros do `template-authors` grupo.
* Os modelos de página mantêm uma conexão dinâmica com qualquer página criada a partir deles. Isso garante que qualquer alteração no modelo seja refletida nas próprias páginas.
* Os Modelos de página tornam o componente de página mais genérico para que o componente de página principal possa ser usado sem personalização.

Com os Modelos de página, as partes que fazem uma página são isoladas dentro dos componentes. É possível configurar as combinações necessárias de componentes em uma interface do usuário, eliminando a necessidade de um novo componente de página ser desenvolvido para cada variação de página.

Este documento:

* Fornece uma visão geral da criação de um modelo de página
* Descreve as tarefas de administrador/desenvolvedor necessárias para criar modelos editáveis
* Descreve os fundamentos técnicos de modelos editáveis
* Descreve como o AEM avalia a disponibilidade de um modelo

>[!NOTE]
>
>Este documento supõe que você já esteja familiarizado com a criação e edição de modelos. Consulte o documento de criação [Criação de modelos de página](/help/sites-cloud/authoring/features/templates.md), que detalha os recursos dos modelos editáveis conforme expostos ao autor do modelo.

>[!TIP]
>
>[O tutorial do WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) O explica em detalhes como usar os Modelos de página implementando um exemplo e é útil para entender como configurar um modelo em um novo projeto

## Criação de um novo modelo {#creating-a-new-template}

A criação de modelos de página é feita principalmente com o [console de modelos e editor de modelos](/help/sites-cloud/authoring/features/templates.md) por um autor de modelo. Esta seção fornece uma visão geral desse processo e segue com uma descrição do que ocorre em nível técnico.

Ao criar um novo modelo editável, você:

1. Criar um [pasta dos modelos](#template-folders). Isso não é obrigatório, mas é uma prática recomendada.
1. Selecione um [tipo de modelo](#template-type). Isso é copiado para criar o [definição do modelo](#template-definitions).

   >[!NOTE]
   >
   >Uma seleção de tipos de modelo é fornecida pronta para uso. Também é possível [criar seus próprios tipos de modelo específicos do site](#creating-template-types) se necessário.

1. Configure a estrutura, as políticas de conteúdo, o conteúdo inicial e o layout do novo modelo.

   **Estrutura**

   * A estrutura permite definir os componentes e o conteúdo para o modelo.
   * Os componentes definidos na estrutura do modelo não podem ser movidos em uma página resultante nem excluídos de qualquer página resultante.
   * Se você quiser que os autores de página possam adicionar e remover componentes, adicione um sistema de parágrafo ao modelo.
   * Os componentes podem ser desbloqueados e bloqueados novamente para permitir que você defina o conteúdo inicial.

   Para obter detalhes sobre como um autor de modelo define a estrutura, consulte [Criação de modelos de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Para obter detalhes técnicos da estrutura, consulte [Estrutura](#structure) neste documento.

   **Políticas**

   * As políticas de conteúdo definem as propriedades de design de um componente.

      * Por exemplo, os componentes disponíveis ou as dimensões mínima/máxima.
   * Elas são aplicáveis ao modelo (e às páginas criadas com o modelo).

   Para obter detalhes sobre como um autor de modelo define políticas, consulte [Criação de modelos de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Para obter detalhes técnicos das políticas, consulte [Políticas de conteúdo](#content-policies) neste documento.

   **Conteúdo inicial**

   * O Conteúdo inicial define o conteúdo que será exibido quando uma página for criada pela primeira vez com base no modelo.
   * O conteúdo inicial pode ser editado pelos autores da página.

   Para obter detalhes sobre como um autor de modelo define a estrutura, consulte [Criação de modelos de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author).

   Para obter detalhes técnicos sobre o conteúdo inicial, consulte [Conteúdo inicial](#initial-content) neste documento.

   **Layout**

   * É possível definir o layout do modelo para um intervalo de dispositivos.
   * O Layout responsivo para modelos funciona como na criação de página.

   Para obter detalhes sobre como um autor de modelo define o layout do modelo, consulte [Criação de modelos de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author).

   Para obter detalhes técnicos sobre o layout do modelo, consulte [Layout](#layout) neste documento.

1. Ative o modelo e, em seguida, aguarde-o para árvores de conteúdo específicas.

   * Um modelo pode ser ativado ou desativado para disponibilizá-lo ou indisponibilizá-lo para os autores da página.
   * Um modelo pode ser disponibilizado ou indisponibilizado para determinadas ramificações de página.

   Para obter detalhes sobre como um autor de modelo habilita um modelo, consulte [Criação de modelos de página](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author).

   Para obter detalhes técnicos sobre a ativação de um template, consulte [Ativar e permitir um modelo para nós](#enabling-and-allowing-a-template-for-use)e neste documento

1. Use-a para criar páginas de conteúdo.

   * Ao usar um modelo para criar uma nova página, não há diferença visível e nenhuma indicação entre modelos estáticos e editáveis.
   * Para o autor da página, o processo é transparente.

   Para obter detalhes sobre como um autor de página usa modelos para criar uma página, consulte [Criar e organizar páginas](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   Para obter detalhes técnicos sobre como criar páginas com modelos editáveis, consulte [Páginas de conteúdo resultante](#resultant-content-pages) neste documento.

>[!TIP]
>
>Nunca insira qualquer informação que precise ser internacionalizada em um modelo. Para efeitos de internalização, a [recursos de localização dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=pt-BR) são recomendadas.

>[!NOTE]
>
>Os modelos são ferramentas eficientes para simplificar o fluxo de trabalho de criação de página. No entanto, usar modelos em excesso pode sobrecarregar os autores e tornar confusa a criação da página. Uma boa regra geral é manter o número de modelos abaixo de 100.
>
>A Adobe não recomenda ter mais de 1000 modelos devido a possíveis impactos no desempenho.

>[!NOTE]
>
>A biblioteca cliente do editor presume a presença do `cq.shared` nas páginas de conteúdo e se não contiver o erro de JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` resultará.
>
>Todos os exemplos de páginas de conteúdo contêm `cq.shared`, portanto, qualquer conteúdo baseado nelas inclui automaticamente `cq.shared`. No entanto, se você decidir criar suas próprias páginas de conteúdo do zero sem baseá-las em conteúdo de amostra, não deixe de incluir o `cq.shared` namespace.
>
>Consulte [Uso de bibliotecas do lado do cliente](/help/implementing/developing/introduction/clientlibs.md) para obter mais informações.



## Pastas de Modelos {#template-folders}

Para organizar seus templates, você pode usar as seguintes pastas:

* `global`
* Específico do site

>[!NOTE]
>
>Mesmo que você possa aninhar suas pastas, quando o usuário as visualizar no **Modelos** console, eles são apresentados como uma estrutura plana.

Em uma instância padrão do AEM, a pasta `global` já existe no console modelo. Isso mantém modelos padrão e atua como um fallback se nenhuma política e/ou tipo de modelo for localizado na pasta atual. Você pode adicionar seus modelos padrão a esta pasta ou criar uma nova pasta (recomendado).

>[!NOTE]
>
>A prática recomendada é criar uma nova pasta para manter seus modelos personalizados e não usar o `global` pasta.

>[!CAUTION]
>
>As pastas devem ser criadas por um usuário com `admin` direitos.

Os tipos de modelo e as políticas são herdados em todas as pastas de acordo com a seguinte ordem de precedência:

1. A pasta atual
1. Pai(s) da pasta atual
1. `/conf/global`
1. `/apps`
1. `/libs`

Uma lista de todas as entradas permitidas é criada. Se alguma configuração se sobrepor ( `path`/ `label`), somente a instância mais próxima à pasta atual é apresentada ao usuário.

Para criar uma nova pasta, faça o seguinte:

* Programaticamente ou com CRXDE Lite
* Usar o [Navegador de configuração](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

## Uso do CRXDE Lite {#using-crxde-lite}

1. Uma nova pasta (em /conf) pode ser criada para sua instância de forma programática ou com o CRXDE Lite.

   Deve ser utilizada a seguinte estrutura:

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. Em seguida, você pode definir as seguintes propriedades no nó raiz da pasta:

   `<your-folder-name> [sling:Folder]`

   * Nome: `jcr:title`
   * Tipo: `String`
   * Valor: o título (da pasta) que você deseja exibir na variável **Modelos** console.

1. Além das permissões e privilégios de criação padrão (por exemplo, `content-authors`) agora é necessário atribuir grupos e definir os direitos de acesso (ACLs) necessários para que os autores possam criar modelos na nova pasta.

   A variável `template-authors` grupo é o grupo padrão que precisa ser atribuído. Consulte a seção [ACLs e grupos](#acls-and-groups) para obter detalhes.

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Usar o navegador de configuração {#using-the-configuration-browser}

1. Ir para **Navegação global** -> **Ferramentas** > [**Navegador de configuração**.](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

   As pastas existentes são listadas à esquerda, incluindo a `global` pasta.

1. Clique em **Criar**.
1. No **Criar configuração** caixa de diálogo os seguintes campos precisam ser configurados:

   * **Título**: forneça um título para a pasta de configuração
   * **Modelos editáveis**: marque para permitir modelos editáveis nesta pasta

1. Clique em **Criar**

>[!NOTE]
>
>No [Navegador de configuração,](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) é possível editar a pasta global e ativar a variável **Modelos editáveis** opção se desejar criar templates dentro dessa pasta, no entanto, essa não é a prática recomendada.

### ACLs e grupos {#acls-and-groups}

Depois que as pastas de modelo forem criadas (via CRXDE ou com o Navegador de configuração), as ACLs deverão ser definidas para os grupos apropriados para as pastas de modelo, a fim de garantir a segurança adequada.

As pastas de modelo para o [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) pode ser usado como exemplo.

#### O grupo de autores de modelo {#the-template-authors-group}

A variável `template-authors` group é o grupo usado para gerenciar o acesso a modelos e vem com AEM por padrão, mas está vazio. Os usuários devem ser adicionados ao grupo para o projeto/site.

>[!CAUTION]
>
>A variável `template-authors` O grupo é somente para usuários que devem ser capazes de criar novos templates.
>
>A edição de modelos é muito eficiente e, se não for feita, os modelos existentes poderão ser corrompidos. Portanto, essa função deve ser focada e incluir apenas usuários qualificados.

A tabela a seguir detalha as permissões necessárias para a edição de modelos.

<table>
 <tbody>
  <tr>
   <th>Caminho </th>
   <th>Função/Grupo</th>
   <th>Permissões<br /> </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autores do modelo<br /> </td>
   <td>ler, gravar, replicar</td>
   <td>Autores de modelos que criam, leem, atualizam, excluem e replicam modelos em sites específicos <code>/conf</code> espaço</td>
  </tr>
  <tr>
   <td>Usuário da Web Anônimo</td>
   <td>ler</td>
   <td>O usuário da Web anônimo deve ler os modelos ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>replicateContent autores precisam ativar os modelos de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>ler, gravar, replicar</td>
   <td>Autores de modelos que criam, leem, atualizam, excluem e replicam modelos em sites específicos <code>/conf</code> espaço</td>
  </tr>
  <tr>
   <td>Usuário da Web Anônimo</td>
   <td>ler</td>
   <td>O Usuário Anônimo da Web deve ler as políticas ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>Os autores de conteúdo precisam ativar as políticas de um modelo de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autor do modelo</td>
   <td>ler</td>
   <td>O autor do modelo cria um novo modelo com base em um dos tipos de modelo predefinidos.</td>
  </tr>
  <tr>
   <td>Usuário da Web Anônimo</td>
   <td>nenhuma</td>
   <td>O usuário da Web anônimo não deve acessar os tipos de modelo</td>
  </tr>
 </tbody>
</table>

Este padrão `template-authors` grupo abrange apenas as configurações do projeto, em que todas as `template-authors` os membros têm permissão para acessar e criar todos os modelos. Para configurações mais complexas, onde vários grupos de autores de modelo são necessários para separar o acesso aos modelos, mais grupos de autores de modelo personalizados devem ser criados. No entanto, as permissões para os grupos de autores de modelo ainda seriam as mesmas.

## Tipo de modelo {#template-type}

Ao criar um novo modelo, você precisa especificar um tipo de modelo:

* Os tipos de modelo fornecem modelos para um modelo de maneira eficaz. Ao criar um novo modelo, a estrutura e o conteúdo inicial do tipo de modelo selecionado são usados para criar para o novo modelo.

   * O tipo de modelo é copiado para criar o modelo.
   * Depois que a cópia ocorre, a única conexão entre o modelo e o tipo de modelo é uma referência estática para fins de informação.

* Os tipos de modelo permitem definir:

   * O tipo de recurso do componente de página.
   * A política do nó raiz, que define os componentes permitidos no editor de modelo.
   * É recomendável definir os pontos de interrupção para a grade responsiva e a configuração do emulador móvel no no tipo de modelo.

* O AEM fornece uma pequena seleção de tipos de modelo prontos para uso, como Página HTML5 e Página de formulário adaptável.

   * Exemplos adicionais são fornecidos como parte do [Tutorial WKND.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* Os tipos de modelo normalmente são definidos pelos desenvolvedores.

Os tipos de template prontos para uso são armazenados em:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Você não deve alterar nada no `/libs` caminho. Isso ocorre porque o conteúdo de `/libs` pode ser substituído a qualquer momento por uma atualização do AEM.

Os tipos de modelo específicos do site devem ser armazenados no local comparável do:

* `/apps/settings/wcm/template-types`

As definições para seus tipos de modelos personalizados devem ser armazenadas em pastas definidas pelo usuário (recomendado) ou, como alternativa, em `global`. Por exemplo:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Os tipos de template devem respeitar a estrutura de pastas correta (ou seja, `/settings/wcm/...`), caso contrário, os tipos de template não serão encontrados.

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating a new editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

>[!CAUTION]
>
>The value of `cq:deviceGroups` must be set as a relative path such as `mobile/groups/responsive` and not as an absolute path such as `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>With static templates /help/sites-developing/page-templates-static.md, the value of `cq:deviceGroups` could be set at the root of the site.
>
>With editable templates, this value is now stored at the template level and is not supported at the page root level.
-->

### Criação de Tipos de Modelo {#creating-template-types}

Se você tiver criado um modelo que possa servir como base de outros modelos, poderá copiá-lo como um tipo de modelo.

1. Crie um modelo como faria com qualquer modelo de página [conforme documentado aqui](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author), que servirá como base para o tipo de template.
1. Usando o CRXDE Lite, copie o modelo recém-criado do `templates` para o nó `template-types` sob o nó [pasta modelo](#template-folders).
1. Exclua o modelo da variável `templates` sob o nó [pasta modelo](#template-folders).
1. Na cópia do modelo que está sob o `template-types` nó, excluir tudo `cq:template` e `cq:templateType` propriedades de todos `jcr:content` nós.

Você também pode desenvolver seu próprio tipo de modelo usando um modelo editável de exemplo como base, disponível no GitHub.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-sites-example-custom-template-type no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definições de modelo {#template-definitions}

As definições para modelos editáveis são armazenadas [pastas definidas pelo usuário](#template-folders) (recomendado) ou, em alternativa, no `global`. Por exemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

O nó raiz do modelo é do tipo `cq:Template` com uma estrutura de esqueleto de:

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

Os principais elementos são:

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

Este nó retém propriedades para o modelo:

* **Nome**: `jcr:title`
* **Nome**: `status`
   * ``**Tipo**: `String`
   * **Valor**: `draft`, `enabled` ou `disabled`

### Estrutura {#structure}

Define a estrutura da página resultante:

* É mesclado com o conteúdo inicial ( `/initial`) ao criar uma nova página.
* As alterações feitas na estrutura serão refletidas em qualquer página criada com o modelo.
* A variável `root` ( `structure/jcr:content/root`) define a lista de componentes que estarão disponíveis na página resultante.
   * Os componentes definidos na estrutura do modelo não podem ser movidos para ou excluído de qualquer página resultante.
   * Depois que um componente é desbloqueado, a variável `editable` propriedade está definida como `true`.
   * Depois que um componente que já contém conteúdo for desbloqueado, esse conteúdo será movido para o `initial` filial.

* A variável `cq:responsive` o nó contém definições para o layout responsivo.

### Conteúdo inicial {#initial-content}

Define o conteúdo inicial que uma nova página terá após a criação:

* Contém um `jcr:content` que é copiado para qualquer página nova.
* É mesclado com a estrutura ( `/structure`) ao criar uma nova página.
* Nenhuma página existente será atualizada se o conteúdo inicial for alterado após a criação.
* A variável `root` O nó contém uma lista de componentes para definir o que estará disponível na página resultante.
* Se o conteúdo for adicionado a um componente no modo de estrutura e esse componente for subsequentemente desbloqueado (ou vice-versa), esse conteúdo será usado como conteúdo inicial.

### Layout {#layout}

Quando [editando um modelo, é possível definir o layout](/help/sites-cloud/authoring/features/templates.md), este usa [layout responsivo padrão](/help/sites-cloud/authoring/features/responsive-layout.md).

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### Políticas de conteúdo {#content-policies}

As políticas de conteúdo definem as propriedades de design de um componente. Por exemplo, os componentes disponíveis ou as dimensões mínima/máxima. Elas são aplicáveis ao modelo (e às páginas criadas com o modelo). As políticas de conteúdo podem ser criadas e selecionadas no editor de modelo.

* A propriedade `cq:policy`, no `root` nó
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornece uma referência relativa à política de conteúdo para o sistema de parágrafos da página.

* A propriedade `cq:policy`, nos nós componente-explícito em `root`, fornecem links para as políticas de componentes individuais.

* As definições de políticas reais são armazenadas em:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Os caminhos das definições de política dependem do caminho do componente. `cq:policy` mantém uma referência relativa à própria configuração.

### Políticas da página {#page-policies}

As políticas de página permitem definir a variável [política de conteúdo](#content-policies) para a página (parsys principal), no modelo ou nas páginas resultantes.

### Ativação e permissão de um modelo para uso {#enabling-and-allowing-a-template-for-use}

1. **Ativar o modelo**

   Antes de ser usado, um modelo deve ser ativado por:

   * [Habilitação do modelo](/help/sites-cloud/authoring/features/templates.md) do **Modelos** console.

   * Definir a propriedade de status na variável `jcr:content` nó.

      * Por exemplo, em:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina a propriedade:

         * Nome: status
         * Tipo: String
         * Valor: `enabled`

1. **Modelos permitidos**

   * [Defina os caminhos do Modelo permitidos na **Propriedades da página**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) da página apropriada ou da página raiz de uma sub-ramificação.
   * Defina a propriedade:
      `cq:allowedTemplates`
No 
`jcr:content` nó da ramificação necessária.
   Por exemplo, com um valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de conteúdo resultante {#resultant-content-pages}

Páginas criadas a partir de modelos editáveis:

* São criados com uma subárvore que é mesclada de `structure` e `initial` no modelo

* Ter referências às informações mantidas no modelo e no tipo de modelo. Este objetivo é alcançado com um `jcr:content` com as propriedades:

   * `cq:template` - Fornece a referência dinâmica ao modelo real; permite que as alterações no modelo sejam refletidas nas páginas reais.

   * `cq:templateType` - Fornece uma referência ao tipo de template.

![Como modelos, conteúdo e componentes se inter-relacionam](assets/templates-content-components.png)

O diagrama acima mostra como os modelos, o conteúdo e os componentes se inter-relacionam:

* Controlador - `/content/<my-site>/<my-page>` - A página resultante que faz referência ao modelo. O conteúdo controla todo o processo. De acordo com as definições, ele acessa o modelo e os componentes apropriados.
* Configuração - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - A [modelo e políticas de conteúdo relacionado](#template-definitions) defina a configuração da página.
* Modelo - Pacotes OSGi - O [Pacotes OSGi](/help/implementing/deploying/configuring-osgi.md) implementar a funcionalidade.
* Exibir - `/apps/<my-site>/components` - Nos ambientes do autor e de publicação, o conteúdo é renderizado por componentes.

Ao processar uma página:

* **Modelos**:

   * A variável `cq:template` propriedade de seu `jcr:content` será referenciado para acessar o modelo que corresponde a essa página.

* **Componentes**:

   * O componente da página mesclará as `structure/jcr:content` árvore do modelo com o `jcr:content` árvore da página.
      * O componente de Página permitirá que o autor edite apenas os nós da estrutura do modelo que foram sinalizados como editáveis (bem como quaisquer secundários).
      * Ao renderizar um componente em uma página, o caminho relativo desse componente será retirado do `jcr:content` nó; o mesmo caminho sob o `policies/jcr:content` do modelo será pesquisado.
         * A variável `cq:policy` propriedade deste nó aponta para a política de conteúdo real (ou seja, ele retém a configuração de design desse componente).
            * Isso permite ter vários modelos que reutilizam as mesmas configurações de política de conteúdo.

### Disponibilidade de modelo {#template-availability}

Ao criar uma nova página na interface de administração do site, a lista de modelos disponíveis depende do local da nova página e das restrições de posicionamento especificadas em cada modelo.

As propriedades a seguir determinam se um modelo `T` pode ser usado para que uma nova página seja colocada como secundária da página `P`. Cada uma dessas propriedades é uma string de vários valores que contém zero ou mais expressões regulares usadas para correspondência com caminhos:

* A variável `cq:allowedTemplates` propriedade do `jcr:content` subnó de `P` ou um ancestral de `P`.

* A variável `allowedPaths` propriedade de `T`.

* A variável `allowedParents` propriedade de `T`.

* A variável `allowedChildren` propriedade do modelo de `P`.

A avaliação funciona da seguinte forma:

* O primeiro não vazio `cq:allowedTemplates` propriedade encontrada ao aumentar a hierarquia de páginas que começa com `P` corresponde ao caminho de `T`. Se nenhum dos valores for correspondente, `T` foi rejeitada.

* Se `T` tem um não vazio `allowedPaths` propriedade, mas nenhum dos valores corresponde ao caminho de `P`, `T` foi rejeitada.

* Se ambas as propriedades acima estiverem vazias ou não existirem, `T` é rejeitada, a menos que pertença ao mesmo aplicativo que `P`. `T` pertence ao mesmo aplicativo que `P` se e somente se o nome do segundo nível do caminho de `T` é o mesmo que o nome do segundo nível do caminho de `P`. Por exemplo, o template `/apps/wknd/templates/foo` pertence ao mesmo aplicativo que a página `/content/wknd`.

* Se `T` tem um não vazio `allowedParents` propriedade, mas nenhum dos valores corresponde ao caminho de `P`, `T` foi rejeitada.

* Se o modelo de `P` tem um não vazio `allowedChildren` propriedade, mas nenhum dos valores corresponde ao caminho de `T`, `T` foi rejeitada.

* Em todos os outros casos, `T` é permitido.

O diagrama a seguir descreve o processo de avaliação do modelo:

![Processo de avaliação do modelo](assets/template-evaluation.png)

>[!CAUTION]
>
>O AEM oferece várias propriedades para controlar os modelos permitidos em **Sites**. No entanto, combiná-los pode levar a regras muito complexas que são difíceis de rastrear e gerenciar.
>
>Portanto, o Adobe recomenda que você comece de forma simples, definindo:
>
>* somente o `cq:allowedTemplates` propriedade
>
>* somente na raiz do site
>
>Para obter um exemplo, consulte a [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) conteúdo: `/content/wknd/jcr:content`
>
>As propriedades `allowedPaths`, `allowedParents`, e `allowedChildren` O também pode ser colocado nos modelos para definir regras mais sofisticadas. No entanto, sempre que possível, *muito* mais simples de definir `cq:allowedTemplates` propriedades nas subseções do site se houver necessidade de restringir ainda mais os modelos permitidos.
>
>Uma vantagem adicional é que a `cq:allowedTemplates` as propriedades podem ser atualizadas por um autor na **Avançado** guia do **Propriedades da página**. As outras propriedades do template não podem ser atualizadas usando a interface do usuário (padrão), portanto, seria necessário um desenvolvedor para manter as regras e uma implantação de código para cada alteração.

#### Limite de modelos usados em páginas secundárias {#limiting-templates-used-in-child-pages}

Para limitar quais modelos podem ser usados para criar páginas secundárias em uma determinada página, use o `cq:allowedTemplates` propriedade de `jcr:content` nó da página para especificar a lista de modelos que podem ser páginas secundárias. Cada valor na lista deve ser um caminho absoluto para um modelo de uma página secundária permitida, por exemplo `/apps/wknd/templates/page-content`.

Você pode usar o `cq:allowedTemplates` propriedade no modelo  `jcr:content` para que esta configuração seja aplicada a todas as páginas recém-criadas que usam este modelo.

Se quiser adicionar mais restrições, por exemplo, em relação à hierarquia do template, você poderá usar o `allowedParents/allowedChildren` propriedades no modelo. Em seguida, é possível especificar explicitamente que as páginas criadas a partir de um modelo T devem ser páginas principais/secundárias das páginas criadas a partir de um modelo T.
