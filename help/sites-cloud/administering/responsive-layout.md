---
title: Configurar o contêiner de layout e o modo de layout
description: Saiba como configurar o contêiner de layout e o modo de layout para ativar layouts responsivos para seus autores de conteúdo.
exl-id: 469e8151-8231-4ccc-b7f6-855545f87440
solution: Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 3%

---

# Configurar o contêiner de layout e o modo de layout {#configuring-layout-container-and-layout-mode}

O [Layout responsivo](/help/sites-cloud/authoring/page-editor/responsive-layout.md) é um mecanismo para realizar o [design responsivo da Web.](https://en.wikipedia.org/wiki/Responsive_web_design) Isso permite que o autor de conteúdo crie páginas da Web com layout e dimensões dependentes dos dispositivos que seus usuários utilizam.

O AEM permite um layout responsivo para suas páginas usando uma combinação de mecanismos:

* **[Contêiner de layout](/help/sites-cloud/authoring/page-editor/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)** - Este componente fornece um sistema de parágrafo de grade que permite adicionar e posicionar componentes em uma grade responsiva.
   * Ela pode ser usada como o parsys padrão da página e/ou disponibilizada aos autores no navegador de componentes.
   * O componente **Contêiner de Layout** padrão é definido em `/libs/wcm/foundation/components/responsivegrid`.
   * É possível definir contêineres de layout:
      * Como um componente que o usuário pode adicionar a uma página.
      * Como o parsys padrão da página.
      * Como componente e parsys padrão.
         * Você pode ter o contêiner de layout como padrão para a página, permitindo que o usuário adicione mais contêineres de layout aqui; por exemplo, para obter o controle da coluna.
* **[Modo de layout](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)** - Depois que o contêiner de layout é posicionado na página, você pode usar o modo **Layout** para posicionar conteúdo na grade responsiva.
* **[Emulador](/help/sites-cloud/authoring/page-editor/responsive-layout.md#selecting-a-device-to-emulate)** - Permite criar e editar sites responsivos que reorganizam o layout de acordo com o tamanho do dispositivo ou da janela, redimensionando componentes interativamente. Usuários podem ver como o conteúdo é renderizado usando o emulador.

Com esses mecanismos de grade responsivos, você pode:

* Use pontos de interrupção (que indicam o agrupamento de dispositivos) para definir comportamentos de conteúdo diferentes com base no layout do dispositivo.
* Ocultar componentes com base no grupo de dispositivos (defina em qual ponto de interrupção um componente será ocultado).
* Usar o alinhamento com a grade (colocar componentes na grade, redimensionar conforme necessário, definir quando eles devem ser recolhidos/refluir para ficarem lado a lado ou acima/abaixo).
* Executar o controle da coluna.

>[!NOTE]
>
>Ao criar um site a partir do [Arquétipo de Projeto](#addlink) ou do [Modelo de Site Padrão](#addlink), o layout responsivo geralmente é configurado. Caso contrário, você deve [ativar o componente Contêiner de layout](#enable-the-layout-container-component-for-page) para suas páginas.

## Ativar o emulador {#enabling-emulator}

O [Arquétipo de Projeto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) e o [Modelo de Site Padrão](/help/sites-cloud/administering/site-creation/site-templates.md#standard-site-template) já estão habilitados para usar o emulador. Se você desenvolveu seu próprio conteúdo não baseado nos Componentes principais ou no arquétipo, consulte o documento [Design responsivo](/help/implementing/developing/introduction/responsive-design.md) para obter detalhes sobre como desenvolver seus componentes enquanto aproveita esses recursos.

## Ativar modo de layout para o site {#activate-layout-mode-for-your-site}

O modo **Layout** permite usar o emulador para ajustar o layout do conteúdo para diferentes dispositivos. O site de exemplo WKND já está habilitado para o modo **Layout**. Siga estas etapas para ativar seu próprio site.

### Configurar pontos de interrupção {#configure-breakpoints}

Os pontos de interrupção são essenciais para um design responsivo e definem como e quando o conteúdo é ajustado ao dispositivo de destino. No entanto, tenha cuidado, pois cada ponto de interrupção introduzido gerará trabalho adicional para os autores acomodarem o conteúdo. Muitas vezes, dois pontos de interrupção podem ser suficientes, incluindo o ponto de interrupção padrão que está sempre lá. A Adobe recomenda não criar mais de três pontos de interrupção, incluindo o padrão, ou seja, não mais de dois nós abaixo de `cq:responsive/breakpoint`.

* Os pontos de interrupção têm um título e uma largura:
   * O título descreve o agrupamento genérico de dispositivos, com orientação se necessário.
      * Por exemplo, `phone`, `tablet`
   * A largura define a largura máxima em pixels para esse agrupamento de dispositivo genérico.
      * Por exemplo, se o telefone do ponto de interrupção tiver uma largura de 768, isso indicará a largura máxima do layout usado para um dispositivo telefônico.
* Os pontos de interrupção podem ser definidos:
   * No modelo de página, de onde as configurações são copiadas para qualquer página criada com esse modelo.
   * No nó da página, de onde as configurações são herdadas por qualquer página secundária.
* Os pontos de interrupção são visíveis como marcadores na parte superior do editor de página quando você está usando o emulador.
* Os pontos de interrupção são herdados da hierarquia do nó principal e podem ser substituídos à vontade.
* Há um ponto de interrupção padrão (pronto para uso) que abrange tudo o que está acima do último ponto de interrupção configurado.
* Os pontos de interrupção podem ser definidos usando CRXDE Lite ou XML.

Os pontos de interrupção devem ser considerados para projetos novos e existentes.

* Se estiver configurando um novo projeto, você deve adicionar pontos de interrupção aos modelos.
* Se você estiver migrando um projeto existente (com conteúdo existente), será necessário:
   * Adicione pontos de interrupção aos modelos.
   * Adicionar os mesmos pontos de interrupção às páginas existentes.

Por causa da herança, você só precisa fazer isso para a página raiz do seu conteúdo.

#### Configurar pontos de interrupção usando o CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. Usando o CRXDE Lite, navegue até:

   * A definição do modelo.
   * O nó `jcr:content` da página.

1. Em `jcr:content`, crie o nó:

   * Nome: `cq:responsive`
   * Tipo: `nt:unstructured`

1. Nesta seção, crie o nó:

   * Nome: `breakpoints`
   * Tipo: `nt:unstructured`

1. No nó pontos de interrupção, é possível criar qualquer número de pontos de interrupção. Cada definição é um único nó com as seguintes propriedades:

   * Nome: `<descriptive name>`
   * Tipo: `nt:unstructured`
   * Título: `String <descriptive title seen in Emulator>`
   * Largura: `Decimal <value of breakpoint>`

#### Configurar pontos de interrupção usando XML {#configuring-breakpoints-using-xml}

Os pontos de interrupção estão localizados dentro da seção `<jcr:content>` de `.context.html` na pasta de modelo (ou conteúdo) apropriada.

Um exemplo de definição:

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

## Ativar o redimensionamento de componentes para a página {#enable-component-resizing-for-the-page}

Redimensionar componentes no modo **Layout** é uma parte importante do design responsivo, que pode ser usado no site de amostra WKND. Siga estas etapas para ativar seu próprio site.

### Definir contêiner de layout como parsys principal {#set-layout-container-as-main-parsys}

Para definir o parsys principal da página para ser um contêiner de layout, defina o parsys como:

`wcm/foundation/components/responsivegrid`

Em:

* Componente da página
* Modelo de página (para uso futuro)

Os dois exemplos a seguir ilustram a definição:

* **HTL:**

  ```xml
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP:**

  ```xml
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### Incluir o CSS responsivo {#include-the-responsive-css}

#### CSS para pontos de interrupção usando MENOS {#css-for-breakpoints-using-less}

O AEM usa MENOS para gerar partes do CSS necessário, que precisam ser incluídas em seus projetos.

Você deve criar uma [biblioteca do cliente](/help/implementing/developing/introduction/clientlibs.md) para fornecer configurações adicionais e chamadas de função. A seguinte extração MENOS é um exemplo do mínimo que você deve adicionar ao seu projeto:

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

A definição da grade base pode ser encontrada em:

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### Considerações sobre estilo {#styling-considerations}

Os componentes mantidos em um contêiner responsivo são redimensionados (juntamente com seus respectivos elementos DOM de HTML) de acordo com o tamanho da grade responsiva. Portanto, nessas circunstâncias, é recomendável evitar (ou atualizar) definições de elementos DOM de largura fixa (contidos).

Por exemplo:

* Antes:

   * `width=100px`

* Depois:

   * `max-width=100px`

#### Conformidade com redimensionamento e imagem adaptável {#resizing-and-adaptive-image-compliance}

Qualquer redimensionamento de um componente na grade acionará os seguintes ouvintes, conforme apropriado:

* `beforeedit`
* `beforechildedit`
* `afteredit`
* `afterchildedit`

Para redimensionar e atualizar corretamente o conteúdo de uma imagem adaptável incluída em uma grade responsiva, é necessário adicionar um conjunto `afterEdit` definido como ouvinte `REFRESH_PAGE` no arquivo `EditConfig` de cada componente contido.

Por exemplo:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

O mecanismo de imagem adaptável é disponibilizado por meio de um script que controla a seleção da imagem correta para o tamanho atual da janela. Ela é ativada depois que o DOM está pronto ou ao receber um evento dedicado. Atualmente, a página deve ser atualizada para refletir corretamente o resultado da ação do usuário.

>[!CAUTION]
>
>As clientlibs de folha de estilos personalizadas devem ser carregadas como parte do cabeçalho para que funcionem corretamente no autor e na publicação.

## Ativar o componente de Contêiner de layout para a página {#enable-the-layout-container-component-for-page}

Para um layout responsivo eficaz, o autor de conteúdo deve ser capaz de arrastar instâncias do componente Contêiner de layout para a página. Isso já está habilitado para o site de exemplo WKND. Siga estas etapas para ativar seu próprio site.

### Ativar o componente de Contêiner de layout para edição de página {#enable-the-layout-container-component-for-page-editing}

Para permitir que os autores adicionem outras grades responsivas às páginas de conteúdo, é necessário ativar o componente Contêiner de layout para a página. Você pode fazer isso usando:

* **Através do Ambiente de Autor** - [Edite seus modelos de página](/help/sites-cloud/authoring/sites-console/templates.md) para habilitar o Contêiner de Layout de uma página.
* **Definição de Componente** - Use `allowedComponent` ou uma inclusão estática ao definir o componente.

### Configurar a grade do contêiner de layout {#configure-the-grid-of-the-layout-container}

Você pode configurar o número de colunas disponíveis para cada instância específica do contêiner de layout [ editando seus modelos de página.](/help/sites-cloud/authoring/sites-console/templates.md)
