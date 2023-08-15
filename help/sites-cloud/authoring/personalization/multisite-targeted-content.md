---
title: Trabalhar com conteúdo direcionado em vários sites
description: Se você precisar gerenciar conteúdo direcionado, como atividades, experiências e ofertas entre seus sites, poderá se beneficiar do suporte integrado a vários sites do AEM para conteúdo direcionado
exl-id: 03d2d640-8de8-4c4c-8a1d-756bb2dc8457
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2890'
ht-degree: 31%

---

# Trabalhar com conteúdo direcionado em vários sites {#working-with-targeted-content-in-multisites}

Se você precisar gerenciar conteúdo direcionado, como atividades, experiências e ofertas entre seus sites, poderá se beneficiar do suporte integrado a vários sites do AEM para conteúdo direcionado.

>[!NOTE]
>
>Trabalhar com suporte a vários sites para conteúdo direcionado é um recurso avançado. Para usar esse recurso, você deve estar familiarizado com o [Gerenciador de vários sites](/help/sites-cloud/administering/msm/overview.md) e a [integração do Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) com o AEM.

Este documento descreve o seguinte:

* Fornece uma breve visão geral do suporte AEM multissite para conteúdo direcionado.
* Descreve alguns cenários de uso possíveis sobre como vincular sites (em uma marca).
* Fornece um exemplo de demonstração sobre como os profissionais de marketing usariam esse recurso.
* Instruções detalhadas sobre como implementar suporte multissite para conteúdo direcionado.

Para configurar como seus sites compartilham conteúdo personalizado, é necessário executar as seguintes etapas:

1. [Criar uma nova área](#creating-new-areas) ou [criar uma nova área como live copy](#creating-new-areas). Uma área inclui todas as atividades disponíveis para um *área* da página; ou seja, o local na página onde o componente é direcionado. A criação de uma nova área cria uma área vazia, enquanto a criação de uma nova área como uma live copy permite herdar o conteúdo nas estruturas do site.

1. [Vincular site ou página](#linking-sites-to-an-area) para uma área.

A qualquer momento, você pode suspender ou restaurar a herança. Além disso, se você não quiser suspender a herança, também poderá criar experiências locais. Por padrão, todas as páginas usam a Área mestre, a menos que você especifique o contrário.

## Introdução ao suporte multissite para conteúdo direcionado {#introduction-to-multisite-support-for-targeted-content}

O suporte multisite para conteúdo direcionado está disponível imediatamente e permite enviar conteúdo direcionado da página principal que você gerencia por meio do MSM para uma live copy local ou permite gerenciar modificações globais e locais desse conteúdo.

Esse gerenciamento é feito em uma **Área**. Áreas separam o conteúdo direcionado (atividades, experiências e ofertas) usado em diferentes sites e fornecem um mecanismo baseado no MSM para criar e gerenciar a herança do conteúdo direcionado junto com a herança do site. Isso evita que você tenha que recriar o conteúdo direcionado em sites herdados.

Em uma área, somente as atividades vinculadas a essa área são enviadas para cópias dinâmicas. Por padrão, a Área mestre é selecionada. Depois de criar áreas adicionais, você pode vinculá-las aos seus sites ou páginas para indicar qual conteúdo direcionado é enviado.

Um site ou uma live copy são vinculados a uma área que contém as atividades que precisam estar disponíveis nesse site ou live copy. Por padrão, o site ou a Live Copy são vinculados à área principal, mas você também pode vincular outras áreas além dela.

>[!NOTE]
>
>Você deve estar ciente do seguinte ao usar suporte a vários sites para conteúdo direcionado:
>
>* Quando você está usando implantações ou Live Copies, é necessária uma licença do MSM.
>* Quando você está usando a sincronização com o Adobe Target, é necessária uma licença do Adobe Target.
>

## Casos de uso {#use-cases}

Você pode configurar o suporte multissite para conteúdo direcionado de várias maneiras, dependendo do seu caso de uso. Esta seção descreve como isso funcionaria teoricamente com uma marca. Além disso, em [Exemplo: direcionamento de conteúdo com base na região](#example-targeting-content-based-on-geography), você pode ver uma aplicação real do direcionamento de conteúdo em vários sites.

O conteúdo direcionado é envolvido em áreas chamadas, que definem o escopo de sites ou páginas. Essas áreas são definidas no nível da marca. Uma marca pode conter várias áreas. As áreas podem ser distintas entre marcas. Embora uma marca possa conter apenas a área principal e, portanto, seja compartilhada entre todas as marcas, outra marca pode conter várias marcas (por exemplo, por região). Portanto, as marcas não precisam refletir o conjunto de áreas entre elas.

Com suporte multisite para conteúdo direcionado, você pode, por exemplo, ter dois (ou mais) sites com **um** que tenham uma das seguintes características:

* Um conjunto completamente *distinto* de conteúdo direcionado - A edição de conteúdo direcionado em um dos sites não afeta o outro. Sites vinculados à áreas distintas fazem leituras e gravações em suas próprias áreas configuradas. Por exemplo:
   * O site A vincula à área X
   * O site B vincula à área Y
* Um conjunto *compartilhado* de conteúdo direcionado - A edição em um site afeta os dois sites diretamente; você pode configurar isso fazendo com que dois sites referenciem à mesma área. Sites vinculados à mesma área compartilham o conteúdo direcionado nessa área. Por exemplo:
   * O site A vincula à área X
   * O Site B vincula-se à Área X
* Um conjunto distinto de conteúdo direcionado *herdado* de outro site por meio do MSM. O conteúdo pode ser implantado de forma unidirecional do original para a Live Copy. Por exemplo:
   * O site A vincula à área X
   * O Site B vincula-se à Área Y (que é uma Live Copy da Área X)

Você também pode ter **múltiplo** marcas usadas em um site, que pode ser mais complexo do que este exemplo.

![Exemplo de multisite](/help/sites-cloud/authoring/assets/multisite-example.png)

>[!NOTE]
>
>Para obter uma visão mais técnica desse recurso, consulte [Como é estruturado o gerenciamento de vários sites para conteúdo direcionado](/help/sites-cloud/authoring/personalization/multisite-structure.md).

## Exemplo: direcionamento de conteúdo com base na geografia {#example-targeting-content-based-on-geography}

Usar vários sites para conteúdo direcionado permite compartilhar, implantar ou isolar conteúdo de personalização. Para ilustrar melhor como esse recurso é usado, considere um cenário em que você deseje controlar como o conteúdo direcionado é implantado com base na geografia, como no seguinte cenário:

Há quatro versões do mesmo site com base na geografia:

* A variável **Estados Unidos** site está no canto superior esquerdo e é o site-mestre. Neste exemplo, ele está aberto no modo Direcionamento.
* As outras três versões deste site são **Canadá**, **Grã-Bretanha**, e **Austrália**, que são todas cópias dinâmicas. Esses sites estão abertos no modo Visualização.

![Versões multisite](/help/sites-cloud/authoring/assets/multisite-versions.png)

Cada site compartilha conteúdo personalizado em regiões geográficas:

* O Canadá compartilha a área principal com os Estados Unidos.
* A Grã-Bretanha está vinculada à área europeia e herda da área principal.
* A Austrália, por estar no hemisfério sul e não ser aplicável para produtos sazonais, tem seu próprio conteúdo personalizado.

![Diagrama multisite](/help/sites-cloud/authoring/assets/multisite-diagram.png)

Para o hemisfério norte, temos uma atividade de inverno criada, mas, para o público-alvo masculino, o profissional de marketing na América do Norte gostaria de uma imagem diferente para o inverno, então ele(a) a modifica no site dos Estados Unidos.

![Versão dos Estados Unidos](/help/sites-cloud/authoring/assets/multisite-us.png)

Depois de atualizar a guia, o site canadense muda para a nova imagem sem nenhuma ação de nossa parte. Ele faz isso porque compartilha a área principal com os Estados Unidos. Nos sites da Grã-Bretanha e Austrália, a imagem não muda.

![Alteração de versões](/help/sites-cloud/authoring/assets/multisite-us-change.png)

O profissional de marketing gostaria de implantar essas alterações na região europeia e [implanta a live copy](/help/sites-cloud/administering/msm/creating-live-copies.md) tocando ou clicando em **Página de implantação**. Depois de atualizar a guia, o site da Grã-Bretanha tem a nova imagem, pois a área da Europa herda da área principal (após a implantação).

![Implantação de Live Copy](/help/sites-cloud/authoring/assets/multisite-roll-out.png)

A imagem no site da Austrália permanece inalterada, o que é o comportamento desejado, pois é o verão na Austrália e o profissional de marketing não deseja alterar esse conteúdo. O site da Austrália não muda porque não compartilha uma área com nenhuma outra região, nem é uma live copy de outra região. O profissional de marketing nunca precisa se preocupar se o conteúdo direcionado do site australiano será substituído.

Além disso, para a Grã-Bretanha, cuja área é uma Live Copy da área principal, é possível ver o status da herança pelo indicador verde ao lado do nome da atividade. Se uma atividade for herdada, não será possível modificá-la, a menos que você suspenda ou desanexe a live copy.

A qualquer momento, você pode suspender a herança ou desanexá-la completamente. Você também pode sempre adicionar experiências locais que só estão disponíveis para essa experiência, sem suspender a herança.

>[!NOTE]
>
>Para obter uma visão mais técnica desse recurso, consulte [Como é estruturado o gerenciamento de vários sites para conteúdo direcionado](/help/sites-cloud/authoring/personalization/multisite-structure.md).

### Criação de uma nova área em vez da criação de uma nova área como live copy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

No AEM, você tem a opção de criar uma nova área ou criar uma nova área como livecopy. A criação de uma nova área agrupa atividades e qualquer coisa que pertença a essas atividades, como ofertas, experiências e assim por diante. Crie uma nova área quando quiser criar um conjunto completamente distinto de conteúdo direcionado ou compartilhar um conjunto de conteúdo direcionado.

No entanto, se você tiver a herança configurada por meio do MSM entre os dois sites, convém herdar as atividades. Nesse caso, você cria uma nova área como uma live copy, onde Y é uma live copy de X e, portanto, herda todas as atividades também.

>[!NOTE]
>
>A implantação padrão aciona implantações subsequentes do conteúdo direcionado sempre que uma página se trata de uma Live Copy vinculada a uma área que é, em si, uma Live Copy da área vinculada ao blueprint das páginas.

Por exemplo, no diagrama a seguir, há quatro sites: dois deles compartilham a área principal (e todas as atividades que fazem parte dessa área), um site possui uma área que é uma Live Copy de outra área e, portanto, compartilha as atividades após a implantação, e o quarto site está completamente separado (e, portanto, requer uma área para suas atividades).

![Detalhes do diagrama](/help/sites-cloud/authoring/assets/multisite-diagram-detail.png)

Para fazer isso no AEM, você faria o seguinte:

* O Site A vincula-se à Área mestre - nenhuma criação de área é necessária. A Área principal é selecionada por padrão no AEM. Os sites A e B compartilham atividades, entre outros.
* O Site B vincula-se à Área mestre - nenhuma criação de área é necessária. A Área principal é selecionada por padrão no AEM. Os sites A e B compartilham atividades, entre outros.
* O site C vincula-se à Área herdada, que é uma live copy da Área mestre - Criar área como Live Copy, onde você cria uma live copy com base na Área mestre. A Área herdada herda atividades da Área mestre na implantação.
* O Site D vincula à sua própria Área isolada - Criar área onde você cria uma área totalmente nova sem atividades ainda definidas. A área isolada não compartilhará atividades com nenhum outro site.

## Criação de novas áreas {#creating-new-areas}

As áreas podem abranger atividades e ofertas. Depois de criar uma área em uma delas (por exemplo, atividades ), você também terá a área disponível na outra (por exemplo, ofertas).

>[!NOTE]
>
>A área padrão chamada Área mestre é recolhida por padrão ao tocar ou clicar no nome de uma marca **até** criar outra área. Em seguida, ao selecionar uma marca no console **Atividade** ou **Ofertas**, você verá o console **Área**.

Para criar uma nova área:

1. Navegue até **Personalização** > **Atividades** ou **Ofertas** e, em seguida, acesse sua marca.
1. Toque ou clique em **Criar área**.

   ![Criar área](/help/sites-cloud/authoring/assets/multisite-create-area.png)

1. Clique em **Área** e clique em **Próxima**.
1. No **Título** insira um nome para a nova área. Opcionalmente, selecione tags.
1. Toque ou clique em **Criar**.

   O AEM redireciona para a janela da marca, onde lista todas as áreas criadas. Se houver outra área além da Área principal, você poderá criar áreas diretamente no console Marca.

   ![Criar](/help/sites-cloud/authoring/assets/multisite-create.png)

## Criação de áreas como Live Copies {#creating-areas-as-live-copies}

Você cria uma área como uma live copy para herdar o conteúdo direcionado nas estruturas do site.

Para criar uma área como uma live copy:

1. Navegue até **Personalização** > **Atividades** ou **ofertas** e, em seguida, acesse sua marca.
1. Toque ou clique em **Criar área como Live Copy**.

   ![Criar área como Live Copy](/help/sites-cloud/authoring/assets/multisite-area-as-livecopy.png)

1. Selecione a área que você deseja transformar em uma Live Copy e clique em **Próximo**.

   ![Criar Live Copy](/help/sites-cloud/authoring/assets/multisite-livecopy.png)

1. No campo **Nome**, digite um nome para a live copy. Por padrão, as sub páginas são incluídas; exclua-as selecionando a caixa de seleção **Excluir sub páginas**.

   ![Criar Live Copy](/help/sites-cloud/authoring/assets/multisite-create-livecopy.png)

1. No **Configurações de implantação** selecione a configuração apropriada.

   Consulte [Configurações de implantação instaladas](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-and-custom-rollout-configurations) para obter descrições de cada opção.

   Consulte [Criação e sincronização de Live Copies](/help/sites-cloud/administering/msm/creating-live-copies.md) para obter mais informações sobre live copies.

   >[!NOTE]
   >
   >Quando uma página é implantada em uma Live Copy e a área configurada para a página Blueprint também é o Blueprint da área configurada para a Live copy da Página, a ação dinâmica **personalizationContentRollout** aciona uma subRollout síncrona, que faz parte da **Configuração de implantação padrão**.

1. Toque ou clique em **Criar**.

   O AEM redireciona para a janela da marca, onde lista todas as áreas criadas. Se houver outra área além da Área principal, você poderá criar áreas diretamente na janela da marca.

   ![Criar área](/help/sites-cloud/authoring/assets/multisite-create-2.png)

## Vincular sites a uma área {#linking-sites-to-an-area}

Você pode vincular áreas a páginas ou a um site. Áreas são herdadas por todas as subpáginas, a menos que essas páginas sejam sobrepostas por um mapeamento em uma subpágina. Em geral, no entanto, você vincula no nível do site.

Ao vincular, somente essas atividades, experiências e ofertas da área selecionada estarão disponíveis. Isso evita a mistura acidental de conteúdo gerenciado independentemente. Se nenhuma outra área for configurada, a área principal de cada marca será usada.

>[!NOTE]
>
>Páginas ou sites que fazem referência à mesma área estão usando o *mesmo* conjunto compartilhado de atividades, experiências e ofertas. A edição de uma atividade, experiência ou oferta compartilhada por vários sites afeta todos esses sites.

Para vincular um site a uma área:

1. Navegue até o site (ou página) que deseja vincular a uma área.
1. Selecione o site ou página e toque ou clique **Propriedades da exibição**.
1. Toque ou clique na guia **Personalização.**
1. No **Marca** selecione a marca à qual deseja vincular sua área. Após selecionar a marca, as áreas disponíveis estarão disponíveis na **Referência da área** menu.

   ![Vincular sites](/help/sites-cloud/authoring/assets/multisite-english.png)

1. Selecione a área no menu suspenso **Referência da área** e toque ou clique em **Salvar**.

   ![Referência da área](/help/sites-cloud/authoring/assets/multisite-area-reference.png)

## Desanexando a Live Copy ou suspendendo a herança do conteúdo direcionado {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

Talvez você queira suspender ou desanexar a herança do conteúdo direcionado. A suspensão ou desanexação da live copy é feita por atividade. Por exemplo, você pode querer modificar as experiências na atividade, mas se essa atividade ainda estiver vinculada à cópia herdada, não será possível modificar a experiência ou qualquer propriedade da atividade.

Suspender a live copy interrompe temporariamente a herança, mas no futuro você poderá restaurar a herança. Desanexar a live copy interrompe permanentemente a herança.

Você suspende ou desconecta a herança do conteúdo direcionado restaurando-o em uma atividade. Se uma página ou site for vinculado a uma área que se trata de uma Live Copy, você poderá ver o status de herança de uma atividade.

Uma atividade que está herdando de outro site é marcada em verde ao lado do nome da atividade. Uma herança suspensa é marcada como vermelha e uma atividade criada localmente não tem ícone.

>[!NOTE]
>
>* Você só pode suspender ou desanexar live copies em uma atividade.
>* Não é necessário suspender ou desanexar live copies para estender uma atividade herdada. Você sempre pode criar **novo** experiências e ofertas locais para essa atividade. Se quiser modificar uma atividade existente, suspenda a herança.
>

### Suspendendo herança {#suspending-inheritance}

Para suspender ou desanexar a herança do conteúdo direcionado em uma atividade do:

1. Navegue até a página em que deseja desanexar ou suspender a herança e toque ou clique **Direcionamento** no menu suspenso do modo.
1. Se a página estiver vinculada a uma área que é uma live copy, você verá o status da herança. Toque ou clique em **Iniciar o direcionamento**.
1. Para suspender uma atividade, siga um destes procedimentos:

   1. Selecione um elemento da atividade, como o público-alvo. O AEM exibe automaticamente uma caixa de confirmação Suspender Live Copy. (Você pode suspender a live copy tocando ou clicando em qualquer elemento no processo de definição de metas.)
   1. Selecionar **Suspender Live Copy** no menu suspenso na barra de ferramentas.

   ![Suspender Live Copy](/help/sites-cloud/authoring/assets/multisite-suspend-livecopy.png)

1. Toque ou clique em **Suspender** para suspender a atividade. Atividades suspensas são marcadas em vermelho.

   ![Live Copy suspensa](/help/sites-cloud/authoring/assets/multisite-suspended.png)

### Interromper herança {#breaking-inheritance}

Para interromper a herança do conteúdo direcionado em uma atividade do:

1. Navegue até a página onde deseja desanexar a live copy da página principal e toque ou clique **Direcionamento** no menu suspenso do modo.
1. Se a página estiver vinculada a uma área que é uma live copy, você verá o status da herança. Toque ou clique em **Iniciar o direcionamento**.
1. Selecione **Desanexar Live Copy** no menu suspenso na barra de ferramentas. O AEM confirma que você deseja desanexar a live copy.
1. Toque ou clique **Desanexar** para desanexar a live copy da atividade. Depois de desanexado, o menu suspenso relativo à herança não é mais exibido. A atividade agora é uma atividade local.

   ![Atividade local](/help/sites-cloud/authoring/assets/multisite-winter.png)

## Restauração da herança do conteúdo direcionado {#restoring-inheritance-of-targeted-content}

Se você suspendeu a herança do conteúdo direcionado em uma atividade do, é possível restaurá-la a qualquer momento. No entanto, se você tiver desanexado a live copy, não será possível restaurar a herança.

Para restaurar a herança do conteúdo direcionado em uma atividade do:

1. Navegue até a página em que deseja restaurar a herança e toque ou clique em **Direcionamento** no menu suspenso de modo.
1. Toque ou clique em **Iniciar o direcionamento**.
1. Selecione **Retomar Live Copy** no menu suspenso da barra de ferramentas.

   ![Retomar a Live Copy](/help/sites-cloud/authoring/assets/multisite-resume.png)

1. Toque ou clique **Retomar** para confirmar se deseja retomar a herança da live copy. Quaisquer modificações feitas na atividade atual serão perdidas se você retomar a herança.

## Excluindo áreas {#deleting-areas}

Ao excluir uma área, todas as atividades nessa área são excluídas. O AEM avisa antes que você possa excluir uma área. Ao excluir uma área à qual um site está vinculado, o mapeamento dessa marca será automaticamente redefinido para a área principal.

Para excluir uma área:

1. Navegue até **Personalização** > **Atividades** ou **Ofertas** e, em seguida, acesse sua marca.
1. Toque ou clique no ícone ao lado da área que deseja excluir.
1. Toque ou clique **Excluir** e confirme se deseja excluir a área.
