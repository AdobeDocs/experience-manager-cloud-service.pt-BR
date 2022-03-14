---
title: Diferencial de páginas
description: O recurso de diferencial de página permite a comparação lado a lado conveniente de duas páginas com suas diferenças realçadas.
exl-id: 6e5c7f14-c980-48e3-8bdd-a7ec10a9e680
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 97%

---

# Diferencial de páginas   {#page-diff}

## Introdução {#introduction}

A criação de conteúdo é um processo iterativo. Criar com eficiência exige poder ver o que mudou de uma iteração para outra. Visualizar uma versão da página e, em seguida, a outra é um processo ineficiente e propenso a erros. Um autor deseja poder comparar facilmente a página atual lado a lado com outra versão.

O recurso de diferencial de página permite a comparação lado a lado conveniente de duas páginas com suas diferenças realçadas.

>[!NOTE]
>
>O usuário deve ter a permissão de **Modificar/Criar/Excluir** no nó `/content/versionhistory` para usar o recurso.
>
>Consulte [Desenvolvimento e diff de página](/help/implementing/developing/introduction/page-diff.md#operation-details) para obter mais detalhes técnicos sobre este recurso.

## Uso do {#use}

O diferencial lado a lado pode comparar o seguinte:

* [Versões](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page) - versão anterior de uma página com seu estado atual
* [](/help/sites-cloud/administering/msm/creating-live-copies.md#comparing-a-live-copy-page-with-a-blueprint-page)Live Copies - Live Copy com blueprint
* [Lançamentos](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page) - lançamento com sua origem
* [](/help/sites-cloud/administering/translation/managing-projects.md#comparing-language-copies)Cópias de idioma - uma página antes e depois da (nova) tradução

Consulte os respectivos tópicos sobre como iniciar o diferencial nesses contextos.

### Apresentação das diferenças   {#presentation-of-differences}

Independentemente do conteúdo que está sendo comparado, a apresentação das diferenças permanece a mesma.

* O conteúdo selecionado quando você iniciou o diferencial é exibido à esquerda (o ponto de entrada do diferencial).
* O conteúdo comparativo é exibido à direita (com base no qual o conteúdo selecionado é comparado).

Por exemplo, ao comparar versões, a versão atual é exibida à esquerda e a versão anterior é exibida à direita.

A origem de ambas as páginas é exibida claramente na barra de cabeçalho na parte superior da janela do navegador.

![Exibição lado a lado das versões](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

O diferencial detecta alterações no componente e no nível do HTML. Itens que foram alterados são destacados com cores diferentes.

**Alterações de componentes**

* Verde claro - Componente adicionado
* Rosa - Componente removido

**Alterações no HTML**

* Verde escuro - HTML adicionado
* Vermelho - HTML removido

>[!NOTE]
>
>Ao comparar cópias de idiomas, o realce é desativado, pois, em uma tradução, tudo muda, e não seria benéfico realçar.

### Tela cheia e ao sair   {#fullscreen-and-exiting}

Para se concentrar em um conteúdo específico, você pode clicar no ícone de tela inteira para qualquer &quot;lado&quot; da comparação lado a lado, ampliando o conteúdo até o tamanho da janela do navegador.

![Botão de tela cheia](/help/sites-cloud/authoring/assets/versions-full-screen.png)

O lado selecionado preencherá a janela inteira, mas a barra permanecerá no topo, permitindo que você alterne entre as duas páginas.

![Modo de tela cheia](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>Se a largura do navegador não puder acomodar ambos os nomes de página na exibição de tela cheia, somente o nome da página que está sendo exibida será mostrado e o outro estará disponível atrás da elipse.

Você também pode optar por fechar a visualização em tela cheia clicando no ícone Saída da tela cheia.

![Sair do modo de tela cheia](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

Você pode sair do diferencial lado a lado a qualquer momento clicando no botão Fechar do cabeçalho.

## Limitações   {#limitations}

Existem algumas situações em que o recurso de diferencial de páginas pode não detectar uma diferença conforme o esperado.

* Ao diferenciar versões e lançamentos, o recurso de diferencial não leva em consideração os componentes dinâmicos, como navegação estrutural, menus, listas de produtos ou logotipos (componentes que dependem da estrutura do site para renderizar seu conteúdo).
* Para versões, o diferencial não recria a política de controle de acesso e as relações de live copy.
* Se uma página for movida, você não poderá mais executar um diff com versões feitas antes do movimento.
   * Se você tiver problemas com um diff, verifique a [Linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) da página para ver se a página foi movida.

>[!NOTE]
>
>Versões não podem ser comparadas entre si. Somente a versão atual pode ser comparada com outras versões da página. A versão atual é sempre a versão realçada com alterações.

>[!NOTE]
>
>Para obter mais detalhes sobre a operação do mecanismo diff da página, bem como limitações que podem afetar o diff da página, consulte a [documentação do desenvolvedor](/help/implementing/developing/introduction/page-diff.md) desse recurso.
