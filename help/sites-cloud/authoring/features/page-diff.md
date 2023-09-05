---
title: Diferencial de páginas
description: O recurso de diferencial de páginas permite a comparação conveniente lado a lado de duas páginas com suas diferenças destacadas.
exl-id: 6e5c7f14-c980-48e3-8bdd-a7ec10a9e680
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 93%

---

# Diferencial de páginas   {#page-diff}

## Introdução {#introduction}

A criação de conteúdo é um processo iterativo. A criação com eficiência requer a capacidade de ver o que foi alterado de uma iteração para outra. Visualizar uma versão da página e, em seguida, a outra é ineficiente e sujeita a erros. Um autor deseja poder comparar facilmente a página atual lado a lado com a outra versão.

O recurso de diferencial de páginas permite a comparação conveniente lado a lado de duas páginas com suas diferenças destacadas.

>[!NOTE]
>
>O usuário precisa ter a permissão para **Modificar/Criar/Excluir** no nó `/content/versionhistory` para usar o recurso.
>
>Consulte [Desenvolvimento e diff de página](/help/implementing/developing/introduction/page-diff.md#operation-details) para obter mais detalhes técnicos sobre este recurso.

## Utilização {#use}

O diferencial lado a lado pode comparar o seguinte:

* [Versões](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page) - versão anterior de uma página com seu estado atual
* [Live Copies](/help/sites-cloud/administering/msm/creating-live-copies.md#comparing-a-live-copy-page-with-a-blueprint-page) - Live Copy com blueprint
* [Lançamentos](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page) - lançamento com sua origem
* [Cópias de idioma](/help/sites-cloud/administering/translation/managing-projects.md#comparing-language-copies) - uma página antes e depois da (nova) tradução

Consulte os respectivos tópicos sobre como iniciar o diferencial nesses contextos.

### Apresentação das diferenças   {#presentation-of-differences}

Independentemente do conteúdo sendo comparado, a apresentação do diferencial permanece a mesma.

* O conteúdo selecionado quando você iniciou o diferencial é exibido à esquerda (o ponto de entrada do diferencial).
* O conteúdo a ser comparado é exibido à direita (ou seja, aquele com o qual o conteúdo selecionado será comparado).

Por exemplo, ao comparar versões, a versão atual será exibida à esquerda e a versão anterior será exibida à direita.

A origem de ambas as páginas é claramente exibida na barra de cabeçalho na parte superior da janela do navegador.

![Exibição lado a lado das versões](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

O recurso diferencial detecta alterações no nível do componente e do HTML. Os itens alterados serão realçados com cores diferentes.

**Alterações de componente**

* Verde-claro - Componente adicionado
* Rosa - Componente removido

**Alterações no HTML**

* Verde-escuro - HTML adicionado
* Vermelho - HTML removido

>[!NOTE]
>
>Ao comparar cópias em idiomas diferentes, o realce é desativado, pois em uma tradução tudo é alterado e o realce não traria benefício algum.

### Tela cheia e ao sair   {#fullscreen-and-exiting}

Para focar em um conteúdo específico, você pode clicar no ícone de tela cheia para qualquer “lado” do diferencial lado a lado, ampliando o conteúdo até o tamanho da janela do navegador.

![Botão de tela cheia](/help/sites-cloud/authoring/assets/versions-full-screen.png)

O lado selecionado preencherá a janela inteira, mas a barra permanecerá no topo, permitindo que você alterne entre as duas páginas.

![Modo de tela cheia](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>Se a largura do navegador não puder acomodar ambos os nomes de página na exibição de tela cheia, somente o nome da página que está sendo exibida será mostrado e o outro estará disponível atrás das reticências.

Você também pode optar por fechar a visualização em tela cheia clicando no ícone Saída da tela cheia.

![Sair do modo de tela cheia](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

É possível sair do diferencial lado a lado a qualquer momento clicando no botão Fechar no cabeçalho.

## Limitações   {#limitations}

Há algumas situações em que o recurso de diferencial de páginas pode não detectar uma diferença conforme esperado.

* Ao comparar versões e inicializações, o diferencial não leva em conta componentes dinâmicos como navegações estruturais, menus, listas de produtos ou logotipos (componentes que dependem da estrutura do site para renderizar seu conteúdo).
* Para versões, o diferencial não recria a política de controle de acesso e as relações com a Live Copy.
* Se uma página for movida, não será mais possível fazer uma comparação com nenhuma versão feita antes da movimentação.
   * Se você tiver problemas com um diferencial, verifique a [Linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) da página para ver se ela foi movida.

>[!NOTE]
>
>As versões não podem ser comparadas entre si. Somente a versão atual pode ser comparada com outras versões da página. A versão atual é sempre a versão realçada com alterações.

>[!NOTE]
>
>Para obter mais detalhes sobre a operação do mecanismo de diferencial de páginas, bem como limitações que podem afetá-lo, consulte a [documentação do desenvolvedor](/help/implementing/developing/introduction/page-diff.md) desse recurso.
