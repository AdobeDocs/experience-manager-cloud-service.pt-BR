---
title: Trabalhar com conteúdo direcionado em vários sites
description: Se você precisar gerenciar conteúdo direcionado, como atividades, experiências e ofertas entre seus sites, é possível aproveitar o suporte multisite integrado do AEM para conteúdo direcionado
exl-id: 03d2d640-8de8-4c4c-8a1d-756bb2dc8457
source-git-commit: 7dd3a658a88cae98732820ab92da0d27d21beb6f
workflow-type: tm+mt
source-wordcount: '2893'
ht-degree: 88%

---

# Trabalhar com conteúdo direcionado em vários sites {#working-with-targeted-content-in-multisites}

Se você precisar gerenciar conteúdo direcionado, como atividades, experiências e ofertas entre seus sites, é possível aproveitar o suporte multisite integrado do AEM para conteúdo direcionado.

>[!NOTE]
>
>O trabalho com suporte Multisite para conteúdo direcionado é um recurso avançado. Para usar esse recurso, você deve estar familiarizado com o [Multi Site Manager](/help/sites-cloud/administering/msm/overview.md) e a [integração do Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) com o AEM.

Este documento descreve o seguinte:

* Fornece uma breve visão geral do suporte multisite do AEM para conteúdo direcionado.
* Descreve alguns possíveis cenários de uso sobre como você pode vincular sites (em uma marca).
* Fornece um exemplo de demonstração sobre como os profissionais de marketing usariam esse recurso.
* Instruções detalhadas sobre como implementar o suporte Multisite para conteúdo direcionado.

Para configurar como os seus sites compartilham conteúdo personalizado, você precisa realizar as seguintes etapas:

1. [Crie uma nova área](#creating-new-areas) ou [crie uma nova área como uma live copy](#creating-new-areas). Uma área inclui todas as atividades que estão disponíveis para uma *área* da página, ou seja, o local na página em que o componente está direcionado. Criar uma nova área cria uma área vazia, enquanto criar uma nova área como uma live copy permite herdar o conteúdo nas estruturas do site.

1. [Vincule seu site ou sua página](#linking-sites-to-an-area) a uma área.

A qualquer momento, você pode suspender ou restaurar a herança. Além disso, se não quiser suspender a herança, você também poderá criar experiências locais. Por padrão, todas as páginas usam a Área mestra, a menos que você especifique o contrário.

## Introdução ao suporte multisite para conteúdo direcionado {#introduction-to-multisite-support-for-targeted-content}

O suporte multisite para conteúdo direcionado está disponível imediatamente e permite enviar conteúdo direcionado da página mestra que você gerencia por meio do MSM para uma live copy local, ou permite gerenciar modificações globais e locais desse conteúdo.

Você gerencia isso em um **Área**. Áreas separam o conteúdo direcionado (atividades, experiências e ofertas) usado em diferentes sites e fornecem um mecanismo baseado no MSM para criar e gerenciar a herança do conteúdo direcionado junto com a herança do site. Isso evita que você tenha que recriar o conteúdo direcionado nos sites herdados.

Em uma área, apenas as atividades vinculadas a essa área são enviadas para cópias em tempo real. Por padrão, a Área mestra é selecionada. Depois de criar áreas adicionais, você pode vinculá-las a seus sites ou páginas para indicar qual conteúdo direcionado é enviado.

Um site ou uma live copy se vincula a uma área que contém as atividades que precisam estar disponíveis nesse site ou nessa live copy. Por padrão, o site ou a live copy se vincula à área principal, mas você pode vincular outras áreas além das áreas principais.

>[!NOTE]
>
>Você deve estar ciente do seguinte ao usar o suporte multisite para conteúdo direcionado:
>
>* Quando você usa implantações ou cópias em tempo real, é necessário usar uma licença do MSM.
>* Quando você usa a sincronização com o Adobe Target, é necessária uma licença do Adobe Target.

>


## Casos de uso {#use-cases}

Você pode configurar o suporte multisite para conteúdo direcionado de várias maneiras, dependendo do seu caso de uso. Esta seção descreve como isso funcionaria teoricamente com uma marca. Além disso, [Exemplo: Direcionamento de conteúdo com base em geografia](#example-targeting-content-based-on-geography), você pode ver uma aplicação real do conteúdo do direcionamento em vários sites.

O conteúdo direcionado é agrupado nas áreas, que definem o escopo de sites ou páginas. Essas áreas são definidas no nível da marca. Uma marca pode conter várias áreas. Áreas podem ser distintas entre marcas. Embora uma marca possa conter apenas a área mestra e, portanto, ser compartilhada entre todas as marcas, outra marca pode conter várias marcas (por exemplo, por região). Portanto, marcas não precisam espelhar o conjunto de áreas entre elas.

Com o suporte multisite para conteúdo direcionado, você pode, por exemplo, ter dois (ou mais) sites com **uma** marca que tenha um dos seguintes itens:

* Um conjunto completamente *distinto* de conteúdo direcionado - A edição de conteúdo direcionado em um dos sites não afeta o outro. Sites com links para áreas distintas fazem leituras e gravações em suas próprias áreas configuradas. Por exemplo:
   * O Site A se vincula à Área X
   * O Site B se vincula à Área Y
* Um conjunto *compartilhado* de conteúdo direcionado - A edição em um site tem impacto direto nos dois sites; você pode definir essa configuração fazendo com que dois sites se refiram à mesma área. Sites com links para a mesma área compartilham o conteúdo direcionado nessa área. Por exemplo:
   * O Site A se vincula à Área X
   * O Site B se vincula à Área X
* Um conjunto distinto de conteúdo direcionado *herdado* de outro site via MSM - O conteúdo pode ser implantado de forma unidirecional do principal para a live copy. Por exemplo:
   * O Site A se vincula à Área X
   * O Site B se vincula à Área Y (que é uma live copy da Área X)

Você também pode ter **várias** marcas que são usadas em um site, o que pode ser mais complexo que esse exemplo.

![Exemplo de vários sites](/help/sites-cloud/authoring/assets/multisite-example.png)

>[!NOTE]
>
>Para obter uma visão mais técnica desse recurso, consulte [Como o gerenciamento multisite para conteúdo direcionado está estruturado](/help/sites-cloud/authoring/personalization/multisite-structure.md).

## Exemplo: direcionamento de conteúdo com base na região {#example-targeting-content-based-on-geography}

O uso de vários sites para conteúdo direcionado permite compartilhar, implementar ou isolar o conteúdo de personalização. Para ilustrar melhor como esse recurso é usado, considere um cenário em que você deseja controlar como o conteúdo direcionado é implantado com base na região, como no cenário a seguir:

Existem quatro versões do mesmo site com base na região:

* O site **Estados Unidos** está no canto superior esquerdo e é o site mestre. Neste exemplo, ele está aberto no modo Direcionar.
* As outras três versões deste site são **Canadá**, **Grã-Bretanha** e **Austrália**, que são todas cópias em tempo real. Esses sites estão abertos no modo Visualizar.

![Versões multisite](/help/sites-cloud/authoring/assets/multisite-versions.png)

Cada site compartilha conteúdo personalizado em regiões geográficas:

* Canadá compartilha a área mestra com os Estados Unidos.
* A Grã-Bretanha está ligada ao espaço europeu e herda da principal.
* Austrália, por estar no hemisfério sul e não ser aplicável para produtos sazonais, tem seu próprio conteúdo personalizado.

![Diagrama multisite](/help/sites-cloud/authoring/assets/multisite-diagram.png)

Para o hemisfério norte, temos uma atividade de inverno criada, mas, no público-alvo masculino, o profissional de marketing na América do Norte gostaria de uma imagem diferente para o inverno, então ele a modifica no site dos Estados Unidos.

![Versão dos Estados Unidos](/help/sites-cloud/authoring/assets/multisite-us.png)

Depois de atualizar a guia, o site Canadá muda para a nova imagem sem nenhuma ação da nossa parte. Isso acontece porque ele compartilha a área mestra com os Estados Unidos. Nos sites Grã-Bretanha e Austrália, a imagem não muda.

![Alteração de versões](/help/sites-cloud/authoring/assets/multisite-us-change.png)

O profissional de marketing deseja implantar essas alterações na região da Europa e [implantar a live copy](/help/sites-cloud/administering/msm/creating-live-copies.md) tocando ou clicando em **Página de implantação**. Depois de atualizar a guia, o site Grã Bretanha tem a nova imagem, pois a área da Europa herda da área mestra (após a implantação).

![Implantação da live copy](/help/sites-cloud/authoring/assets/multisite-roll-out.png)

A imagem no site Austrália permanece inalterada, o que é o comportamento desejado, já que é verão na Austrália, e o profissional de marketing não deseja alterar esse conteúdo. O site Austrália não muda, pois não compartilha uma área com outra região nem é uma live copy de outra região. O profissional de marketing nunca precisa se preocupar com a substituição do conteúdo direcionado do site da Austrália.

Além disso, para Grã-Bretanha, cuja área é uma live copy da área mestra, você pode ver o status da herança conforme o indicador verde ao lado do nome da atividade. Se uma atividade for herdada, você não poderá modificá-la, a menos que suspenda ou desconecte a live copy.

A qualquer momento, é possível suspender a herança ou desconectá-la completamente. Você também pode sempre adicionar experiências locais que estejam disponíveis apenas para essa experiência, sem suspender a herança.

>[!NOTE]
>
>Para obter uma visão mais técnica desse recurso, consulte [Como o gerenciamento multisite para conteúdo direcionado está estruturado](/help/sites-cloud/authoring/personalization/multisite-structure.md).

### Criação de uma nova área em comparação à criação de uma nova área como live copy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

No AEM, você tem a opção de criar uma nova área ou de criar novas áreas como uma live copy. Criar uma nova área agrupa atividades e qualquer coisa que pertença a essas atividades, como ofertas, experiências e assim por diante. Você cria uma nova área quando deseja criar um conjunto completamente distinto de conteúdo direcionado ou quando deseja compartilhar um conjunto de conteúdo direcionado.

Se, no entanto, você tiver a herança configurada por meio do MSM entre os dois sites, talvez queira herdar essas atividades. Nesse caso, você cria uma nova área como uma live copy, em que Y é uma live copy de X e, portanto, herda todas as atividades também.

>[!NOTE]
>
>A implantação padrão aciona implantações subsequentes do conteúdo direcionado sempre que uma página é uma Live Copy, vinculando-se a uma área que, por sua vez, é uma Live Copy da área vinculada ao blueprint Páginas.

Por exemplo, no diagrama a seguir, há quatro sites: dois deles compartilham a área mestra (e todas as atividades que fazem parte dessa área), um site possui uma área que é uma live copy de outra área e, portanto, compartilha as atividades após a implantação, e um quarto site é completamente separado (e, portanto, requer uma área para suas atividades).

![Detalhes do diagrama](/help/sites-cloud/authoring/assets/multisite-diagram-detail.png)

Para conseguir isso no AEM, você faria o seguinte:

* O Site A vincula-se à Área mestra e não requer a criação de uma área. A Área mestra é selecionada por padrão no AEM. Os Sites A e B compartilham atividades e assim por diante.
* O Site B vincula-se à Área mestra e não requer a criação de uma área. A Área mestra é selecionada por padrão no AEM. Os Sites A e B compartilham atividades e assim por diante.
* O Site C vincula-se à Área herdada, que é uma live copy da Área mestra - Use a opção Criar área como Live Copy, em que você cria uma live copy com base na Área mestra. A Área herdada herda as atividades da área mestra após a implantação.
* O Site D vincula-se à sua própria Área isolada - Use a opção Criar área, em que você cria uma área totalmente nova, sem atividades ainda definidas. A área isolada não compartilhará atividades com nenhum outro site.

## Criação de novas áreas {#creating-new-areas}

Áreas podem abranger atividades e ofertas. Depois de criar uma área em qualquer uma delas (por exemplo, atividades), você também tem a área disponível na outra (por exemplo, ofertas).

>[!NOTE]
>
>A área padrão chamada Área mestre é recolhida por padrão ao tocar ou clicar no nome de uma marca **até** criar outra área. Em seguida, ao selecionar uma marca no console **Atividade** ou **Ofertas**, você verá o console **Área**.

Para criar uma nova área:

1. Navegue até **Personalização** > **Atividades** ou **Ofertas** e, em seguida, acesse sua marca.
1. Toque ou clique em **Criar área**.

   ![Criar área](/help/sites-cloud/authoring/assets/multisite-create-area.png)

1. Clique no ícone **Área** e depois em **Próximo**.
1. No campo **Título**, insira um nome para a nova área. Opcionalmente, selecione tags.
1. Toque ou clique em **Criar**.

   O AEM faz o redirecionamento para a janela da marca, onde ele lista todas as áreas criadas. Se houver outra área além da Área mestra, você poderá criar áreas diretamente no console Marca.

   ![Criar](/help/sites-cloud/authoring/assets/multisite-create.png)

## Criação de áreas como cópias em tempo real {#creating-areas-as-live-copies}

Você cria uma área como uma live copy para herdar o conteúdo direcionado entre estruturas de sites.

Para criar uma área como uma live copy:

1. Navegue até **Personalização** > **Atividades** ou **ofertas** e, em seguida, acesse sua marca.
1. Toque ou clique em **Criar área como Live Copy**.

   ![Criar área como Live Copy](/help/sites-cloud/authoring/assets/multisite-area-as-livecopy.png)

1. Selecione a área que você deseja transformar em uma live copy e clique em **Próximo**.

   ![Criar Live Copy](/help/sites-cloud/authoring/assets/multisite-livecopy.png)

1. No campo **Nome**, digite um nome para a live copy. Por padrão, as sub páginas são incluídas; exclua-as selecionando a caixa de seleção **Excluir sub páginas**.

   ![Criar Live Copy](/help/sites-cloud/authoring/assets/multisite-create-livecopy.png)

1. No menu suspenso **Configurações de implantação**, selecione a configuração apropriada.

   Consulte [Configurações de implementação instaladas](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-and-custom-rollout-configurations) para obter descrições de cada opção.

   Consulte [Criação e sincronização de cópias em tempo real](/help/sites-cloud/administering/msm/creating-live-copies.md) para obter mais informações sobre cópias em tempo real.

   >[!NOTE]
   >
   >Quando uma página é implantada em uma Live Copy e a área configurada para a página Blueprint também é o Blueprint da área configurada para a Live copy da Página, a ação em tempo real **personalizationContentRollout** aciona uma subRollout síncrona, que faz parte da **Configuração de implantação padrão**.

1. Toque ou clique em **Criar**.

   O AEM faz o redirecionamento para a janela da marca, onde ele lista todas as áreas criadas. Se houver outra área além da Área mestra, você poderá criar áreas diretamente na janela da marca.

   ![Criar área](/help/sites-cloud/authoring/assets/multisite-create-2.png)

## Vinculação de sites a uma área {#linking-sites-to-an-area}

Você pode vincular áreas a páginas ou a um site. Áreas são herdadas por todas as subpáginas, a menos que essas páginas sejam sobrepostas por um mapeamento em uma subpágina. Em geral, no entanto, você vincula no nível do site.

Ao vincular, apenas as atividades, experiências e ofertas da área selecionada ficam disponíveis. Essa vinculação evita a confusão acidental de um conteúdo gerenciado independentemente. Se nenhuma outra área estiver configurada, a área mestra de cada marca será usada.

>[!NOTE]
>
>Páginas ou sites que fazem referência à mesma área estão usando o *same* conjunto compartilhado de atividades, experiências e ofertas. A edição de uma atividade, experiência ou oferta compartilhada por vários sites afeta todos esses sites.

Para vincular um site a uma área:

1. Navegue até o site (ou a página) que você deseja vincular a uma área.
1. Selecione o site ou a página e toque ou clique em **Propriedades de exibição**.
1. Toque ou clique na guia **Personalização.**
1. No menu **Marca**, selecione a marca à qual você deseja vincular sua área. Depois de selecionar a marca, as áreas disponíveis serão disponibilizadas no menu **Referência da área**.

   ![Sites de vinculação](/help/sites-cloud/authoring/assets/multisite-english.png)

1. Selecione a área no menu suspenso **Referência da área** e toque ou clique em **Salvar**.

   ![Referência da área](/help/sites-cloud/authoring/assets/multisite-area-reference.png)

## Desconexão da live copy ou suspensão da herança do conteúdo direcionado {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

Você pode querer suspender ou desconectar a herança do conteúdo direcionado. A suspensão ou desconexão da live copy é feita por atividade. Por exemplo, você pode modificar experiências na sua atividade, mas, se essa atividade ainda estiver vinculada à cópia herdada, não será possível modificar a experiência ou qualquer uma das propriedades da atividade.

A suspensão da live copy interrompe temporariamente a herança, mas, no futuro, você poderá restaurar a herança. A desconexão da live copy interrompe permanentemente a herança.

Você suspende ou desconecta a herança do conteúdo direcionado restaurando-o em uma atividade. Se uma página ou site se vincular a uma área que seja uma Live Copy, você poderá visualizar o status de herança de uma atividade.

Uma atividade herdada de outro site é marcada em verde ao lado do seu nome. Uma herança suspensa é marcada em vermelho, e uma atividade criada localmente não tem ícone.

>[!NOTE]
>
>* Apenas é possível suspender ou desconectar cópias em tempo real em uma atividade.
>* Não é necessário suspender ou desconectar cópias em tempo real para estender uma atividade herdada. Você sempre pode criar **novas** experiências e ofertas locais para essa atividade. Se quiser modificar uma atividade existente, será necessário suspender a herança.

>


### Suspensão da herança {#suspending-inheritance}

Para suspender ou desconectar a herança do conteúdo direcionado em uma atividade:

1. Navegue até a página em que você deseja desconectar ou suspender a herança e toque ou clique em **Direcionar** no menu suspenso de modo.
1. Se a sua página estiver vinculada a uma área que é uma live copy, você verá o status da herança. Toque ou clique em **Iniciar o direcionamento**.
1. Para suspender uma atividade, siga um destes procedimentos:

   1. Selecione um elemento da atividade, como o público-alvo. O AEM exibe automaticamente uma caixa de confirmação Suspender Live Copy. (É possível suspender a cópia ao vivo tocando ou clicando em qualquer elemento por todo o processo de Direcionamento.)
   1. Selecione **Suspender Live Copy** no menu suspenso da barra de ferramentas.

   ![Suspender Live Copy](/help/sites-cloud/authoring/assets/multisite-suspend-livecopy.png)

1. Toque ou clique **Suspender** para suspender a atividade. Atividades suspensas são marcadas em vermelho.

   ![Live Copy suspensa](/help/sites-cloud/authoring/assets/multisite-suspended.png)

### Interrupção da herança {#breaking-inheritance}

Para interromper a herança do conteúdo direcionado em uma atividade:

1. Navegue até a página da qual você deseja desconectar a live copy da mestra e toque ou clique em **Direcionar** no menu suspenso de modo.
1. Se a sua página estiver vinculada a uma área que é uma live copy, você verá o status da herança. Toque ou clique em **Iniciar o direcionamento**.
1. Selecione **Desanexar Live Copy** no menu suspenso na barra de ferramentas. O AEM confirma que você deseja desanexar a live copy.
1. Toque ou clique em **Destacar** para desconectar a live copy da atividade. Depois que ela é desconectada, o menu suspenso de herança deixa de ser exibido. A atividade agora é local.

   ![Atividade local](/help/sites-cloud/authoring/assets/multisite-winter.png)

## Restauração da herança do conteúdo direcionado {#restoring-inheritance-of-targeted-content}

Se você suspendeu a herança do conteúdo direcionado em uma atividade, é possível restaurá-la a qualquer momento. No entanto, se você desconectou a live copy, a herança não pode ser restaurada.

Para restaurar a herança do conteúdo direcionado em uma atividade:

1. Navegue até a página onde deseja restaurar a herança e toque ou clique em **Direcionamento** no menu suspenso de modo.
1. Toque ou clique em **Iniciar o direcionamento**.
1. Selecione **Retomar Live Copy** no menu suspenso da barra de ferramentas.

   ![Resumo da live copy](/help/sites-cloud/authoring/assets/multisite-resume.png)

1. Toque ou clique em **Retomar** para confirmar que você deseja retomar a herança da live copy. Quaisquer modificações feitas na atividade atual serão perdidas se você retomar a herança.

## Exclusão de áreas {#deleting-areas}

Ao excluir uma área, você exclui todas as atividades nessa área. O AEM avisa antes que você possa excluir uma área. Se você excluir uma área à qual um site está vinculado, o mapeamento dessa marca será automaticamente remapeado para a área principal.

Para excluir uma área:

1. Navegar para **Personalização** > **Atividades** ou **Ofertas** e depois a sua marca.
1. Toque ou clique no ícone ao lado da área que você deseja excluir.
1. Toque ou clique em **Excluir** e confirme que você deseja excluir a área.
