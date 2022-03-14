---
title: Modelos de páginas
description: Modelos de página são usados ao criar uma página que será usada como a base para a nova página
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '3296'
ht-degree: 8%

---

# Modelos de páginas {#page-templates}

Ao criar uma página, você precisa selecionar um modelo. O modelo de página é usado como a base para a nova página. O modelo define a estrutura da página resultante, qualquer conteúdo inicial e os componentes que podem ser usados (propriedades de design). Isso tem várias vantagens:

* Os Modelos de página permitem que autores especializados [criar e editar modelos](/help/sites-cloud/authoring/features/templates.md).
   * Esses autores especializados são chamados de **autores de modelos**
   * Os autores do modelo devem ser membros do `template-authors` grupo.
* Os Modelos de página mantêm uma conexão dinâmica com qualquer página criada a partir delas. Isso garante que todas as alterações no modelo sejam refletidas nas próprias páginas.
* Os Modelos de página tornam o componente de página mais genérico, de modo que o componente de página principal possa ser usado sem personalização.

Com Modelos de página, as partes que fazem uma página são isoladas dentro dos componentes. Você pode configurar as combinações necessárias de componentes em uma interface do usuário, eliminando a necessidade de um novo componente de página ser desenvolvido para cada variação de página.

Este documento:

* Fornece uma visão geral da criação de um modelo de página
* Descreve as tarefas de administrador/desenvolvedor necessárias para criar modelos editáveis
* Descreve os fundamentos técnicos dos modelos editáveis
* Descreve como o AEM avalia a disponibilidade de um modelo

>[!NOTE]
>
>Este documento pressupõe que você já está familiarizado com a criação e edição de modelos. Consulte o documento de criação [Criação de modelos de página](/help/sites-cloud/authoring/features/templates.md), que detalha os recursos de modelos editáveis conforme expostos ao autor do modelo.

>[!TIP]
>
>[O tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) aprofunda-se em como usar Modelos de página implementando um exemplo e é útil para entender como configurar um modelo em um novo projeto

## Criação de um novo modelo {#creating-a-new-template}

A criação de modelos de página é feita principalmente com o [console modelo e editor de modelo](/help/sites-cloud/authoring/features/templates.md) por um autor de modelo. Esta seção fornece uma visão geral desse processo e apresenta uma descrição do que ocorre a nível técnico.

Ao criar um novo modelo editável:

1. Crie um [pasta dos modelos](#template-folders). Isso não é obrigatório, mas é uma prática recomendada.
1. Selecione um [tipo de modelo](#template-type). Isso é copiado para criar o [definição de modelo](#template-definitions).

   >[!NOTE]
   >
   >Uma seleção de tipos de modelo é fornecida pronta para uso. Você também pode [criar seus próprios tipos de modelo específicos de site](#creating-template-types) se necessário.

1. Configure a estrutura, as políticas de conteúdo, o conteúdo inicial e o layout do novo template.

   **Estrutura**

   * A estrutura permite definir componentes e conteúdo para o modelo.
   * Os componentes definidos na estrutura do modelo não podem ser movidos em uma página resultante ou excluídos de qualquer página resultante.
   * Se desejar que os autores da página possam adicionar e remover componentes, adicione um sistema de parágrafo ao modelo.
   * Os componentes podem ser desbloqueados e bloqueados novamente para permitir que você defina o conteúdo inicial.

   Para obter detalhes sobre como um autor de modelo define a estrutura, consulte [Criação de modelos de página](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   Para obter detalhes técnicos da estrutura, consulte [Estrutura](#structure) neste documento.

   **Políticas**

   * As políticas de conteúdo definem as propriedades de design de um componente.

      * Por exemplo, os componentes disponíveis ou as dimensões mínimas/máximas.
   * Eles são aplicáveis ao modelo (e às páginas criadas com o modelo).

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

1. Ative o modelo e permita árvores de conteúdo específico.

   * Um modelo pode ser ativado ou desativado para torná-lo disponível ou indisponível para os autores da página.
   * Um modelo pode ser disponibilizado ou indisponibilizado para determinadas ramificações de página.

   Para obter detalhes sobre como um autor de modelo habilita um modelo, consulte [Criação de modelos de página](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author).

   Para obter detalhes técnicos sobre como ativar um modelo, consulte [Ativar e permitir um modelo para nós](#enabling-and-allowing-a-template-for-use)e neste documento

1. Use-o para criar páginas de conteúdo.

   * Ao usar um modelo para criar uma nova página, não há diferenças visíveis e nenhuma indicação entre os modelos estáticos e editáveis.
   * Para o autor da página, o processo é transparente.

   Para obter detalhes sobre como um autor de página usa modelos para criar uma página, consulte [Criar e organizar páginas](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   Para obter detalhes técnicos sobre como criar páginas com modelos editáveis, consulte [Páginas de conteúdo resultante](#resultant-content-pages) neste documento.

>[!TIP]
>
>Nunca insira qualquer informação que precise ser internacionalizada em um modelo. Para fins de internalização, o [recursos de localização dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=pt-BR) são recomendadas.

>[!NOTE]
>
>Os modelos são ferramentas poderosas para simplificar o fluxo de trabalho de criação de página. No entanto, muitos modelos podem sobrecarregar os autores e tornar a criação da página confusa. Uma boa regra é manter o número de modelos abaixo de 100.
>
>O Adobe não recomenda ter mais de 1000 modelos devido a possíveis impactos no desempenho.

>[!NOTE]
>
>A biblioteca cliente do editor assume a presença do `cq.shared` namespace nas páginas de conteúdo e se estiver ausente do erro de JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` resultará em .
>
>Todas as páginas de conteúdo de exemplo contêm `cq.shared`, portanto, qualquer conteúdo baseado neles inclui automaticamente `cq.shared`. No entanto, se você decidir criar suas próprias páginas de conteúdo do zero sem basear-nas no conteúdo de amostra, deverá incluir a variável `cq.shared` namespace.
>
>Consulte [Usar bibliotecas do lado do cliente](/help/implementing/developing/introduction/clientlibs.md) para obter mais informações.



## Pastas de modelo {#template-folders}

Para organizar seus modelos, você pode usar as seguintes pastas:

* `global`
* Específico do site

>[!NOTE]
>
>Mesmo que você possa aninhar suas pastas, quando o usuário as visualiza no **Modelos** Eles são apresentados como uma estrutura plana.

Em uma instância padrão do AEM, a pasta `global` já existe no console modelo. Isso mantém modelos padrão e atua como um fallback se nenhuma política e/ou tipo de modelo for localizado na pasta atual. Você pode adicionar seus modelos padrão a esta pasta ou criar uma nova pasta (recomendado).

>[!NOTE]
>
>É prática recomendada criar uma nova pasta para manter seus modelos personalizados e não usar o `global` pasta.

>[!CAUTION]
>
>As pastas devem ser criadas por um usuário com `admin` direitos.

Os tipos e políticas de modelo são herdados em todas as pastas de acordo com a seguinte ordem de precedência:

1. A pasta atual
1. Pai(s) da pasta atual
1. `/conf/global`
1. `/apps`
1. `/libs`

Uma lista de todas as entradas permitidas é criada. Se alguma configuração se sobrepõe ( `path`/ `label`), somente a instância mais próxima da pasta atual é apresentada ao usuário.

Para criar uma nova pasta, você pode fazer o seguinte:

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
   * Valor: O título (para a pasta) que você deseja exibir no **Modelos** console.

1. Além das permissões e privilégios de criação padrão (por exemplo, `content-authors`) agora é necessário atribuir grupos e definir os direitos de acesso necessários (ACLs) para que os autores possam criar modelos na nova pasta.

   O `template-authors` grupo é o grupo padrão que precisa ser atribuído. Consulte a seção [ACLs e grupos](#acls-and-groups) para obter detalhes.

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### Usar o navegador de configuração {#using-the-configuration-browser}

1. Ir para **Navegação global** -> **Ferramentas** > [**Navegador de configuração**.](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

   As pastas existentes são listadas à esquerda, incluindo o `global` pasta.

1. Clique em **Criar**.
1. No **Criar configuração** os seguintes campos precisam ser configurados:

   * **Título**: Forneça um título para a pasta de configuração
   * **Modelos editáveis**: Marque para permitir modelos editáveis nesta pasta

1. Clique em **Criar**

>[!NOTE]
>
>No [Navegador de configuração,](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) você pode editar a pasta global e ativar o **Modelos editáveis** , se desejar criar modelos nessa pasta, no entanto, essa não é a prática recomendada.

### ACLs e grupos {#acls-and-groups}

Depois que as pastas de modelo são criadas (via CRXDE ou com o Navegador de configuração), as ACLs devem ser definidas para os grupos apropriados para as pastas de modelo para garantir a segurança adequada.

As pastas de modelo para a [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) pode ser usado como exemplo.

#### O Grupo de autores de modelo {#the-template-authors-group}

O `template-authors` grupo é o grupo usado para gerenciar o acesso a modelos e vem como padrão com AEM, mas está vazio. Os usuários devem ser adicionados ao grupo para o projeto/site.

>[!CAUTION]
>
>O `template-authors` O grupo é somente para usuários que devem ser capazes de criar novos modelos.
>
>A edição de modelos é muito poderosa e, se não for feita, os modelos existentes podem ser quebrados. Portanto, essa função deve ser focada e incluir apenas usuários qualificados.

A tabela a seguir detalha as permissões necessárias para a edição de modelo.

<table>
 <tbody>
  <tr>
   <th>Caminho</th>
   <th>Função / Grupo</th>
   <th>Permissões<br /> </th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autores do modelo<br /> </td>
   <td>ler, escrever, replicar</td>
   <td>Autores de modelo que criam, leem, atualizam, excluem e replicam modelos em um site específico <code>/conf</code> espaço</td>
  </tr>
  <tr>
   <td>Usuário Anônimo da Web</td>
   <td>leitura</td>
   <td>O Usuário Anônimo da Web deve ler modelos ao renderizar uma página</td>
  </tr>
  <tr>
   <td>Autores de conteúdo</td>
   <td>replicar</td>
   <td>replicateContent autores precisam ativar os modelos de uma página ao ativar uma página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>ler, escrever, replicar</td>
   <td>Autores de modelo que criam, leem, atualizam, excluem e replicam modelos em um site específico <code>/conf</code> espaço</td>
  </tr>
  <tr>
   <td>Usuário Anônimo da Web</td>
   <td>leitura</td>
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
   <td>leitura</td>
   <td>O autor do modelo cria um novo modelo com base em um dos tipos de modelo predefinidos.</td>
  </tr>
  <tr>
   <td>Usuário Anônimo da Web</td>
   <td>nenhum</td>
   <td>O Usuário Anônimo da Web não deve acessar os tipos de modelo</td>
  </tr>
 </tbody>
</table>

Esse padrão `template-authors` abrange apenas as configurações do projeto, em que todas as `template-authors` os membros têm permissão para acessar e criar todos os modelos. Para configurações mais complexas, onde vários grupos de autores de modelo são necessários para separar o acesso a modelos, mais grupos de autores de modelo personalizados devem ser criados. No entanto, as permissões para os grupos de autores de modelo ainda seriam as mesmas.

## Tipo de modelo {#template-type}

Ao criar um novo modelo, você precisa especificar um tipo de modelo:

* Os tipos de modelo fornecem modelos para um modelo de maneira eficaz. Ao criar um novo template, a estrutura e o conteúdo inicial do tipo de template selecionado são usados para criar o novo template.

   * O tipo de modelo é copiado para criar o modelo.
   * Após a cópia, a única conexão entre o modelo e o tipo de modelo é uma referência estática para fins de informação.

* Os tipos de templates permitem definir:

   * O tipo de recurso do componente de página.
   * A política do nó raiz, que define os componentes permitidos no editor de modelo.
   * É recomendável definir os pontos de interrupção para a grade responsiva e a configuração do emulador móvel no tipo de modelo.

* AEM fornece uma pequena seleção de tipos de modelo prontos para uso, como Página do HTML5 e Página do formulário adaptável.

   * Exemplos adicionais são fornecidos como parte do [Tutorial WKND.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* Os tipos de modelo geralmente são definidos pelos desenvolvedores.

Os tipos de modelo prontos para uso são armazenados em:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Você não deve alterar nada na variável `/libs` caminho. Isso ocorre porque o conteúdo da variável `/libs` pode ser substituído a qualquer momento por uma atualização do AEM.

Os tipos de modelo específicos do site devem ser armazenados no local comparável de:

* `/apps/settings/wcm/template-types`

As definições dos tipos de modelos personalizados devem ser armazenadas em pastas definidas pelo usuário (recomendado) ou, alternativamente, em `global`. Por exemplo:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Os tipos de modelo devem respeitar a estrutura correta da pasta (ou seja, `/settings/wcm/...`), caso contrário, os tipos de modelo não serão encontrados.

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

### Criação de tipos de modelo {#creating-template-types}

Se você criou um template que pode servir como base de outros templates, é possível copiar esse template como um tipo de template.

1. Criar um modelo como faria com qualquer modelo de página [conforme documentado aqui](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author), que servirá de base para o seu tipo de modelo.
1. Usando o CRXDE Lite, copie o modelo recém-criado da `templates` para `template-types` nó sob o [pasta de modelos](#template-folders).
1. Excluir o modelo do `templates` nó sob o [pasta de modelos](#template-folders).
1. Na cópia do modelo que está sob o `template-types` nó, excluir tudo `cq:template` e `cq:templateType` `jcr:content` propriedades.

Você também pode desenvolver seu próprio tipo de modelo usando um modelo editável de exemplo como base, disponível no GitHub.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-sites-example-custom-template-type no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definições de modelo {#template-definitions}

Definições para modelos editáveis são armazenadas [pastas definidas pelo usuário](#template-folders) (recomendado) ou alternativamente em `global`. Por exemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

O nó raiz do modelo é do tipo `cq:Template` com uma estrutura esquelética de:

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

Esse nó contém as propriedades do template:

* **Nome**: `jcr:title`
* **Nome**: `status`
   * ``**Tipo**: `String`
   * **Valor**: `draft`, `enabled` ou `disabled`

### Estrutura {#structure}

Define a estrutura da página resultante:

* É mesclado com o conteúdo inicial ( `/initial`) ao criar uma nova página.
* As alterações feitas na estrutura serão refletidas em qualquer página criada com o modelo.
* O `root` ( `structure/jcr:content/root`) define a lista de componentes que estarão disponíveis na página resultante.
   * Os componentes definidos na estrutura do modelo não podem ser movidos para ou excluídos de qualquer página resultante.
   * Depois que um componente é desbloqueado, a variável `editable` está definida como `true`.
   * Depois que um componente que já contém conteúdo for desbloqueado, esse conteúdo será movido para o `initial` ramificação.

* O `cq:responsive` nó contém definições para o layout responsivo.

### Conteúdo inicial {#initial-content}

Define o conteúdo inicial que uma nova página terá após a criação:

* Contém um `jcr:content` nó que é copiado para qualquer página nova.
* É mesclado com a estrutura ( `/structure`) ao criar uma nova página.
* Nenhuma página existente será atualizada se o conteúdo inicial for alterado após a criação.
* O `root` contém uma lista de componentes para definir o que estará disponível na página resultante.
* Se o conteúdo for adicionado a um componente no modo de estrutura e esse componente for subsequentemente desbloqueado (ou vice-versa), esse conteúdo será usado como conteúdo inicial.

### Layout {#layout}

When [editar um modelo, você pode definir o layout](/help/sites-cloud/authoring/features/templates.md), isso usa [layout responsivo padrão](/help/sites-cloud/authoring/features/responsive-layout.md).

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### Políticas de conteúdo {#content-policies}

As políticas de conteúdo definem as propriedades de design de um componente. Por exemplo, os componentes disponíveis ou as dimensões mínimas/máximas. Eles são aplicáveis ao modelo (e às páginas criadas com o modelo). As políticas de conteúdo podem ser criadas e selecionadas no editor de modelo.

* A propriedade `cq:policy`, no `root` nó
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornece uma referência relativa à política de conteúdo para o sistema de parágrafo da página.

* A propriedade `cq:policy`, nos nós explícitos de componente em `root`, fornecer links para as políticas dos componentes individuais.

* As definições reais de política são armazenadas em:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Os caminhos das definições de política dependem do caminho do componente. `cq:policy` mantém uma referência relativa à própria configuração.

### Políticas da página {#page-policies}

As políticas de página permitem definir a variável [política de conteúdo](#content-policies) para a página (parsys principal), no modelo ou nas páginas resultantes.

### Ativar e permitir o uso de um modelo {#enabling-and-allowing-a-template-for-use}

1. **Ativar o modelo**

   Antes de um modelo poder ser usado, ele deve ser habilitado por:

   * [Ativação do template](/help/sites-cloud/authoring/features/templates.md) do **Modelos** console.

   * Definir a propriedade de status na `jcr:content` nó .

      * Por exemplo, em:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina a propriedade :

         * Nome: status
         * Tipo: String
         * Valor: `enabled`

1. **Modelos permitidos**

   * [Defina os caminhos de Modelo permitidos no **Propriedades da página**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) da página ou página raiz apropriada de uma subramificação.
   * Defina a propriedade :
      `cq:allowedTemplates`
No 
`jcr:content` nó da ramificação necessária.
   Por exemplo, com um valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de conteúdo resultante {#resultant-content-pages}

Páginas criadas a partir de modelos editáveis:

* São criados com uma subárvore que é unida a partir de `structure` e `initial` no modelo

* Ter referências às informações contidas no modelo e tipo de modelo. Isso é feito com uma `jcr:content` com as propriedades:

   * `cq:template` - Fornece a referência dinâmica ao modelo real; permite que as alterações no modelo sejam refletidas nas páginas reais.

   * `cq:templateType` - Fornece uma referência ao tipo de modelo .

![Como os modelos, o conteúdo e os componentes se relacionam](assets/templates-content-components.png)

O diagrama acima mostra como os modelos, o conteúdo e os componentes se relacionam:

* Controlador - `/content/<my-site>/<my-page>` - A página resultante que faz referência ao modelo. O conteúdo controla todo o processo. De acordo com as definições, ele acessa o modelo e os componentes apropriados.
* Configuração - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - O [modelo e políticas de conteúdo relacionadas](#template-definitions) defina a configuração da página.
* Modelo - Pacotes OSGi - O [Pacotes OSGI](/help/implementing/deploying/configuring-osgi.md) implemente a funcionalidade.
* Exibir - `/apps/<my-site>/components` - Nos ambientes de autor e publicação, o conteúdo é renderizado pelos componentes.

Ao renderizar uma página:

* **Modelos**:

   * O `cq:template` propriedade da `jcr:content` será referenciado para acessar o modelo que corresponde a essa página.

* **Componentes**:

   * O componente de página mesclará o `structure/jcr:content` árvore do modelo com o `jcr:content` da página.
      * O componente de página permitirá que o autor edite apenas os nós da estrutura do modelo que foram sinalizados como editáveis (bem como qualquer filho).
      * Ao renderizar um componente em uma página, o caminho relativo desse componente será retirado do `jcr:content` nó; o mesmo caminho sob o `policies/jcr:content` O nó do template será pesquisado.
         * O `cq:policy` a propriedade desse nó aponta para a política de conteúdo real (ou seja, contém a configuração de design desse componente).
            * Isso permite ter vários modelos que reutilizam as mesmas configurações de política de conteúdo.

### Disponibilidade de modelo {#template-availability}

Ao criar uma nova página na interface de administração do site, a lista de modelos disponíveis depende do local da nova página e das restrições de posicionamento especificadas em cada modelo.

As seguintes propriedades determinam se um modelo `T` pode ser usada para que uma nova página seja colocada como filho de página `P`. Cada uma dessas propriedades é uma string com vários valores, contendo zero ou mais Expressões Regulares, usadas para correspondência com caminhos:

* O `cq:allowedTemplates` da `jcr:content` subnó de `P` ou um antepassado de `P`.

* O `allowedPaths` propriedade de `T`.

* O `allowedParents` propriedade de `T`.

* O `allowedChildren` propriedade do modelo de `P`.

A avaliação funciona do seguinte modo:

* O primeiro não vazio `cq:allowedTemplates` propriedade encontrada ao ascender a hierarquia de página começando com `P` corresponde ao caminho de `T`. Se nenhum dos valores corresponder, `T` é rejeitada.

* If `T` tem um não vazio `allowedPaths` , mas nenhum dos valores corresponde ao caminho de `P`, `T` é rejeitada.

* Se ambas as propriedades acima estiverem vazias ou inexistentes, `T` é rejeitada, a menos que pertença ao mesmo pedido que `P`. `T` pertence ao mesmo aplicativo que `P` se e somente se o nome do segundo nível do caminho de `T` é igual ao nome do segundo nível do caminho de `P`. Por exemplo, o modelo `/apps/wknd/templates/foo` pertence ao mesmo aplicativo que a página `/content/wknd`.

* If `T` tem um não vazio `allowedParents` , mas nenhum dos valores corresponde ao caminho de `P`, `T` é rejeitada.

* Se o modelo de `P` tem um não vazio `allowedChildren` , mas nenhum dos valores corresponde ao caminho de `T`, `T` é rejeitada.

* Em todos os outros casos, `T` é permitido.

O diagrama a seguir descreve o processo de avaliação do template:

![Processo de avaliação de modelos](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM oferece várias propriedades para controlar os modelos permitidos em **Sites**. No entanto, combiná-las pode levar a regras muito complexas, que são difíceis de rastrear e gerenciar.
>
>Portanto, o Adobe recomenda que você comece de forma simples, definindo:
>
>* somente a variável `cq:allowedTemplates` propriedade
>
>* somente na raiz do site
>
>Para ver um exemplo, consulte a [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) conteúdo: `/content/wknd/jcr:content`
>
>As propriedades `allowedPaths`, `allowedParents`e `allowedChildren` também pode ser colocado nos templates para definir regras mais sofisticadas. No entanto, quando possível, é *many* mais simples de definir `cq:allowedTemplates` propriedades nas subseções do site se houver a necessidade de restringir ainda mais os modelos permitidos.
>
>Uma vantagem adicional é que a variável `cq:allowedTemplates` As propriedades podem ser atualizadas por um autor na função **Avançado** da guia **Propriedades da página**. As outras propriedades do modelo não podem ser atualizadas usando a interface do usuário (padrão), portanto, seria necessário um desenvolvedor para manter as regras e uma implantação de código para cada alteração.

#### Limitação de modelos usados em páginas filhas {#limiting-templates-used-in-child-pages}

Para limitar quais modelos podem ser usados para criar páginas filhas em uma determinada página, use o `cq:allowedTemplates` propriedade de `jcr:content` nó da página para especificar a lista de modelos a serem permitidos como páginas secundárias. Cada valor na lista deve ser um caminho absoluto para um modelo para uma página secundária permitida, por exemplo `/apps/wknd/templates/page-content`.

Você pode usar o `cq:allowedTemplates` na propriedade do modelo  `jcr:content` para que essa configuração seja aplicada a todas as páginas recém-criadas que usam esse modelo.

Se quiser adicionar mais restrições, por exemplo, em relação à hierarquia do modelo, use a variável `allowedParents/allowedChildren` propriedades no modelo. Você pode especificar explicitamente que as páginas criadas a partir de um modelo T devem ser pais/filhos de páginas criadas a partir de um modelo T.
