---
title: Modo de desenvolvedor
seo-title: Developer Mode
description: O modo Desenvolvedor abre um painel lateral com várias guias que fornecem ao desenvolvedor informações sobre a página atual
seo-description: Developer mode opens a side panel with several tabs that provide a developer with information about the current page
exl-id: fbf11c0f-dc6e-43f3-bcf2-080eacc6ba99
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---

# Modo de desenvolvedor {#developer-mode}

Ao editar páginas em AEM, vários [modos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) estão disponíveis, incluindo o modo Desenvolvedor . O modo Desenvolvedor abre um painel lateral com várias guias que fornecem ao desenvolvedor informações técnicas sobre a página atual.

Há duas guias:

* **[Componentes](#components)** para visualizar informações sobre estrutura e desempenho.
* **[Erros](#errors)** para ver qualquer problema que ocorra.

Isso ajuda um desenvolvedor a:

* **Discover** como as páginas são compostas.
* **Depuração:** o que está acontecendo onde e quando, o que por sua vez ajuda a resolver os problemas.

>[!NOTE]
>
>Modo de desenvolvedor:
>
>* Não está disponível em dispositivos móveis ou janelas pequenas no desktop (devido a restrições de espaço).
>  * Isso ocorre quando a largura é inferior a 1024px.
>* Está disponível somente para usuários que são membros do `administrators` grupo.


## Abrir o Modo de Desenvolvedor {#opening-developer-mode}

O modo Desenvolvedor é implementado como um painel lateral para o editor de páginas. Para abrir o painel, selecione **Desenvolvedor** no seletor de modo na barra de ferramentas do editor de páginas:

![Abrir o modo de desenvolvedor](assets/developer-mode.png)

O painel é dividido em duas guias:

* **[Componentes](#components)** - Mostra uma árvore de componentes, semelhante à [árvore de conteúdo](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree) para autores
* **[Erros](#errors)** - Quando ocorrem problemas, os detalhes são mostrados para cada componente.

### Guia Componentes {#components}

![Guia Componentes](assets/developer-mode-components-tab.png)

Isso mostra uma árvore de componentes que:

* Descreve a cadeia de componentes e modelos renderizados na página. A árvore pode ser expandida para mostrar o contexto na hierarquia.
* Mostra o tempo computacional do lado do servidor necessário para renderizar o componente.
* Permite expandir a árvore e selecionar componentes específicos dentro da árvore. A seleção fornece acesso aos detalhes do componente; como:
   * Caminho do repositório
   * Links para scripts (acessados no CRXDE Lite)
   * Detalhe do componente, como visto na seção [Console de componentes](/help/sites-cloud/authoring/features/components-console.md)
* Os componentes selecionados na árvore são indicados por uma borda azul no editor.

Essa guia de componentes ajuda a:

* Determine e compare o tempo de renderização por componente.
* Consulte e entenda a hierarquia.
* Entenda e melhore o tempo de carregamento da página ao encontrar componentes lentos.

Cada entrada de componente pode ter as seguintes opções:

![Exemplo de componente do modo de desenvolvedor](assets/developer-mode-component-example.png)

* **Exibir detalhes:** Um link para uma lista que mostra:
   * Todos os scripts de componente usados para renderizar o componente.
   * O caminho do conteúdo do repositório para esse componente específico.

      ![Visualizar Detalhes](assets/developer-mode-view-details.png)

* **Editar script:** Um link que abre o script de componente no CRXDE Lite.

* **Exibir detalhes do componente:** Abre os detalhes do componente no [Console Componentes.](/help/sites-cloud/authoring/features/components-console.md)

Expandir uma entrada de componente tocando ou clicando na divisa também pode mostrar:

    * A hierarquia no componente selecionado.
    * Tempos de renderização do componente selecionado de forma isolada, quaisquer componentes individuais aninhados dentro dele e o total combinado.

### Guia Erros {#errors}

![A guia errors](assets/developer-mode-errors-tab.png)

Espero que a variável **Erros** sempre estará vazia (como acima), mas quando ocorrerem problemas, os seguintes detalhes poderão ser mostrados para cada componente:

* Um aviso se o componente gravar uma entrada no log de erros, juntamente com detalhes do erro e links diretos para o código apropriado no CRXDE Lite.
* Um aviso se o componente abrir uma sessão de administrador.

Por exemplo, se um método indefinido for chamado, o erro resultante será exibido na variável **Erros** e a entrada do componente na árvore do **Componentes** também será marcada com um indicador quando ocorrer um erro.
