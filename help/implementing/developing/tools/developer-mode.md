---
title: Modo de desenvolvedor
seo-title: Developer Mode
description: O Modo de desenvolvedor abre um painel lateral com várias guias que fornecem ao desenvolvedor informações sobre a página atual
seo-description: Developer mode opens a side panel with several tabs that provide a developer with information about the current page
exl-id: fbf11c0f-dc6e-43f3-bcf2-080eacc6ba99
source-git-commit: 1a4c5e618adaef99d82a00e1118d1a0f8536fc14
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Modo de desenvolvedor {#developer-mode}

Ao editar páginas no AEM, várias [modos](/help/sites-cloud/authoring/sites-console/introduction.md#page-modes) estão disponíveis, incluindo o Modo de desenvolvedor. O Modo de desenvolvedor abre um painel lateral com várias guias que fornecem ao desenvolvedor informações técnicas sobre a página atual.

Há duas guias:

* **[Componentes](#components)** para exibir informações sobre estrutura e desempenho.
* **[Erros](#errors)** para ver se há problemas.

Isso ajuda um desenvolvedor a:

* **Descobrir** como as páginas são compostas.
* **Depurar:** o que está acontecendo, onde e quando, o que, por sua vez, ajuda a resolver problemas.

>[!NOTE]
>
>Modo de desenvolvedor:
>
>* Não está disponível em dispositivos móveis ou janelas pequenas na área de trabalho (devido a restrições de espaço).
>  * Isso ocorre quando a largura é menor que 1024px.
>* Está disponível somente para usuários que são membros da `administrators` grupo.

## Abrindo o Modo de Desenvolvedor {#opening-developer-mode}

O modo de desenvolvedor é implementado como um painel lateral para o editor de páginas. Para abrir o painel, selecione **Desenvolvedor** no seletor de modo, na barra de ferramentas do editor de páginas:

![Abrindo modo de desenvolvedor](assets/developer-mode.png)

O painel é dividido em duas guias:

* **[Componentes](#components)** - Isso mostra uma árvore de componentes, semelhante à [árvore de conteúdo](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#content-tree) para autores
* **[Erros](#errors)** - Quando ocorrem problemas, os detalhes são mostrados para cada componente.

### Guia Componentes {#components}

![Guia Componentes](assets/developer-mode-components-tab.png)

Isso mostra uma árvore de componentes que:

* Descreve a cadeia de componentes e modelos renderizados na página. A árvore pode ser expandida para mostrar o contexto dentro da hierarquia.
* Mostra o tempo computacional do lado do servidor necessário para renderizar o componente.
* Permite expandir a árvore e selecionar componentes específicos dentro dela. A seleção fornece acesso aos detalhes do componente; como:
   * Caminho do repositório
   * Links para scripts (acessados em CRXDE Lite)
   * Detalhes do componente, conforme visto na [Console de componentes](/help/sites-cloud/authoring/components-console.md)
* Os componentes selecionados na árvore são indicados por uma borda azul no editor.

Esta guia de componentes ajuda a:

* Determine e compare o tempo de renderização por componente.
* Veja e entenda a hierarquia.
* Entenda e melhore o tempo de carregamento da página ao encontrar componentes lentos.

Cada entrada de componente pode ter as seguintes opções:

![Exemplo de componente do modo de desenvolvedor](assets/developer-mode-component-example.png)

* **Exibir detalhes:** Um link para uma lista que mostra:
   * Todos os scripts de componentes usados para renderizar o componente.
   * O caminho do conteúdo do repositório para este componente específico.

     ![Exibir detalhes](assets/developer-mode-view-details.png)

* **Editar script:** Um link que abre o script de componente no CRXDE Lite.

* **Exibir detalhes do componente:** Abre os detalhes do componente na [Console de componentes](/help/sites-cloud/authoring/components-console.md).

Expandir uma entrada de componente tocando ou clicando na divisa também pode mostrar:

    * A hierarquia dentro do componente selecionado.
    * Tempos de renderização para o componente selecionado isolado, quaisquer componentes individuais aninhados dentro dele e o total combinado.

### Guia Erros {#errors}

![A guia de erros](assets/developer-mode-errors-tab.png)

Esperamos que o **Erros** A guia sempre estará vazia (como acima), mas quando ocorrerem problemas os detalhes a seguir podem ser mostrados para cada componente:

* Um aviso se o componente gravar uma entrada no log de erros, juntamente com detalhes do erro e links diretos para o código apropriado no CRXDE Lite.
* Um aviso se o componente abrir uma sessão de administrador.

Por exemplo, se um método indefinido for chamado, o erro resultante será mostrado no **Erros** e a entrada do componente na árvore do **Componentes** também será marcada com um indicador quando ocorrer um erro.
