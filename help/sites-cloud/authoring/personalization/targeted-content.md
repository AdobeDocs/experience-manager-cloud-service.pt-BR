---
title: Criação de conteúdo direcionado usando o modo Direcionar
description: O modo de direcionamento e o componente do Target fornecem ferramentas para a criação de conteúdo para experiências
exl-id: 8d80d867-2d0f-4ddb-8a06-f9441e6d85ce
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '5282'
ht-degree: 87%

---

# Criação de conteúdo direcionado usando o modo Direcionar {#authoring-targeted-content-using-targeting-mode}

Crie conteúdo direcionado usando o modo de Direcionamento do AEM. O modo de direcionamento e o componente do Target fornecem ferramentas para a criação de conteúdo para experiências:

* Reconheça facilmente o conteúdo direcionado que está na página. Uma linha pontilhada forma uma borda ao redor de todo o conteúdo direcionado.
* Selecione uma marca e uma atividade para ver as experiências.
* Adicione ou remova experiências de uma atividade.
* Realize testes A/B e converta os vencedores (somente no Adobe Target).
* Adicione ofertas criadas a uma experiência ou use as ofertas de uma biblioteca.
* Configure metas e monitore o desempenho.
* Simule a experiência do usuário.
* Para obter mais personalização, configure o componente do Target.

>[!NOTE]
>
>O modo de direcionamento está disponível no Editor de páginas e no Editor de fragmentos de experiência.
>
>A documentação a seguir é aplicável a ambos (já que os dois operam na mesma base), embora tenha sido escrita para o Editor de páginas.

>[!CAUTION]
>
>Ao direcionar no Editor de páginas, somente os componentes do Fragmento de experiência podem ser direcionados.
>
>Outros tipos de componentes podem ser convertidos em um Fragmento de experiência usando o ícone **Converter em variação de fragmento de experiência** na barra de ferramentas do componente.

<!--
>Other component types can be converted to an Experience Fragment using the **Convert to experience fragment variation** icon on the component toolbar:
>
>![Converting component to Experience Fragment](/help/sites-cloud/authoring/assets/offers-convert-legacy-icon.png)
-->

Você pode usar o AEM ou o Adobe Target como mecanismo de direcionamento (é necessário ter uma conta válida do Adobe Target para usá-lo). Se você estiver usando o Adobe Target, é necessário configurar a integração primeiro. Consulte as [instruções de integração com o Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

![Direcionamento de conteúdo](../assets/targeted-content.png)

As atividades e experiências que você vê no modo de Direcionamento refletem o [console Atividades](/help/sites-cloud/authoring/personalization/activities.md):

* As alterações feitas nas atividades e experiências usando o modo de direcionamento são refletidas no console de atividades.
* As alterações feitas no console de atividades são refletidas no modo de direcionamento.

>[!NOTE]
>
>Quando você cria uma campanha no Adobe Target, ele atribui uma propriedade chamada `thirdPartyId` a cada campanha. Quando você exclui a campanha no Adobe Target, o thirdPartyId não é excluído. Não é possível reutilizar o `thirdPartyId` para campanhas de tipos diferentes (AB, XT) e ele não pode ser removido manualmente. Para evitar esse problema, dê a cada campanha um nome exclusivo. Nomes de campanha não podem ser reutilizados em diferentes tipos de campanha.
>
>Se você usar o mesmo nome no mesmo tipo de campanha, a campanha existente será substituída.
>
>Se, durante a sincronização, você encontrar o erro “A solicitação falhou. `thirdPartyId` já existe”, altere o nome da campanha e sincronize novamente.

>[!NOTE]
>
>Ao direcionar, a combinação de marca e atividade é mantida no nível do usuário e não no nível do canal.

## Alternar para o modo de direcionamento {#switching-to-targeting-mode}

Alterne para o modo de direcionamento para acessar as ferramentas de criação de conteúdo direcionado.

Para alternar para o modo de direcionamento:

1. Abra a página para a qual deseja criar conteúdo direcionado.
1. Na barra de ferramentas na parte superior da página, selecione o menu suspenso de modo para revelar os tipos disponíveis.

   ![Modo Direcionar](../assets/targeted-mode.png)

1. Selecione **Direcionamento**. As opções de direcionamento são exibidas na parte superior da página.

   ![Barra de ferramentas de direcionamento](../assets/targeted-toolbar.png)

## Adicionar uma atividade usando o modo de direcionamento {#adding-an-activity-using-targeting-mode}

Use o modo de direcionamento para adicionar uma atividade a uma marca. Ao adicionar uma atividade, ela conterá a experiência padrão. Após adicionar a atividade, você deve iniciar o processo de direcionamento de conteúdo para a atividade.

Você também pode criar e gerenciar atividades do Adobe Target a partir do AEM com a opção de selecionar o mecanismo de direcionamento (AEM ou Adobe Target) e o tipo de atividade (direcionamento de experiência ou teste A/B).

Além disso, é possível gerenciar metas e métricas para todas as atividades do Adobe Target e gerenciar os públicos-alvo do Adobe Target. Os relatórios de atividades do Adobe Target, incluindo a conversão de vencedores para testes A/B, também são incluídos.

Quando você adiciona uma atividade, ela também aparece no [console de atividades](/help/sites-cloud/authoring/personalization/activities.md).

Para adicionar uma atividade:

1. Use o menu suspenso **Marca** para selecionar a marca para a qual deseja criar a atividade.

   >[!NOTE]
   >
   >É recomendado [criar marcas por meio do console de atividades](/help/sites-cloud/authoring/personalization/activities.md#creating-a-brand-using-the-activities-console).
   >
   >
   >Se você criar uma marca de qualquer outra maneira, faça com que o nó `/campaigns/<brand>/master` exista ou ocorrerá um erro ao tentar criar uma atividade.

1. Selecione + ao lado do menu suspenso **Atividade**.
1. Digite um nome para a atividade.

   >[!NOTE]
   >
   >Ao criar uma atividade e ter uma configuração de nuvem do Adobe Target anexada à página ou a uma página principal, o AEM assume automaticamente o Adobe Target como mecanismo.

1. No menu suspenso do mecanismo de **Direcionamento**, selecione o mecanismo direcionamento.

   * Se você selecionar **ContextHub AEM**, os campos restantes estarão esmaecidos e indisponíveis. Selecione **Criar**.

   * Se você selecionar **Adobe Target**, será possível selecionar uma configuração (por padrão, é a configuração inserida ao configurar a conta) e o tipo de atividade. <!--If you select **Adobe Target**, you can select a configuration (by default, it is the configuration you provided when you [configured the account](/help/sites-administering/opt-in.md)) and Activity Type.-->

1. No menu Atividade, selecione **Direcionamento de experiência** ou **Teste A/B**.

   * Direcionamento de experiência: gerencie as atividades do Adobe Target a partir do AEM.
   * Teste A/B: crie/gerencie atividades de teste A/B no Adobe Target a partir do AEM.

## O processo de direcionamento: criar, direcionar, metas e configurações {#the-targeting-process-create-target-and-goals-settings}

O modo de direcionamento permite configurar vários aspectos de uma atividade. Use o seguinte processo de três etapas para criar conteúdo direcionado para uma atividade de marca:

1. [Criar](#create-authoring-the-experiences): adicione ou remova experiências e adicione ofertas para cada experiência.
1. [Direcionar](#target-configuring-the-audiences): especifique o público-alvo ao qual cada experiência é direcionada. Você pode direcionar a um público-alvo específico e, se estiver usando o teste A/B, decidir qual porcentagem do tráfego vai para qual experiência.
1. [Metas e configurações](#goals-settings-configuring-the-activity-and-setting-goals): programe a atividade e defina a prioridade. Você também pode definir metas para métricas de sucesso.

Use o procedimento a seguir para iniciar o processo de direcionamento de conteúdo para uma atividade.

>[!NOTE]
>
>Para usar o processo de direcionamento, você deve ser membro do grupo de usuários Autores da atividade de direcionamento.

Para adicionar uma atividade:

1. No menu suspenso **Marca**, selecione a marca que contém a atividade em que você está trabalhando.
1. No menu suspenso **Atividade**, selecione a atividade para a qual você está criando conteúdo direcionado.
1. Para revelar os controles que guiarão você pelo processo de direcionamento, selecione **Iniciar o Direcionamento**.

   ![Iniciar o direcionamento](../assets/targeted-start-targeting.png)

   >[!NOTE]
   >
   >Para alterar a atividade com a qual você está trabalhando, selecione **Voltar**.

## Criar: criação das experiências {#create-authoring-the-experiences}

A etapa Criar do direcionamento de conteúdo envolve a criação de experiências. Durante essa etapa, é possível criar ou excluir as experiências da atividade e adicionar ofertas a cada experiência.

### Visualização de ofertas de experiência no modo de direcionamento {#seeing-experience-offers-in-targeting-mode}

Após [iniciar o processo de direcionamento](#the-targeting-process-create-target-and-goals-settings), selecione uma experiência para ver as ofertas que são fornecidas para ela. Ao selecionar uma experiência, os componentes direcionados na página são alterados para mostrar a oferta dessa experiência.

>[!CAUTION]
>
>Tenha cuidado ao desativar o direcionamento para um componente que já está direcionado na instância de criação. A respectiva atividade também é excluída automaticamente da instância de publicação.

>[!NOTE]
>
>Uma oferta é o conteúdo de um componente direcionado.

As experiências são exibidas no painel Públicos-alvo. No exemplo a seguir, as experiências incluem **Padrão**, **Feminino**, **Feminino acima de 30** e **Feminino abaixo de 30**. Este exemplo mostra a oferta Padrão de um componente de **Imagem** direcionado.

![Componente de imagem direcionado](../assets/targeted-image-component.png)

Quando uma experiência diferente é selecionada, o componente de imagem mostra a oferta para essa experiência.

![Componente de imagem direcionado alterado](../assets/targeted-image-different.png)

Quando uma experiência é selecionada e o componente de destino não inclui uma oferta para essa experiência, o componente exibe **Adicionar oferta** sobreposta à oferta padrão semitransparente. Quando nenhuma oferta é criada para uma experiência, a oferta **Padrão** é exibida no segmento que está mapeado para a experiência.

![Adicionar oferta](../assets/targeted-add-offer.png)

A experiência padrão também é exibida quando as propriedades do visitante não correspondem aos segmentos mapeados às experiências. Consulte [Adicionar experiências usando o modo de direcionamento](#adding-and-removing-experiences-using-targeting-mode).

### Ofertas personalizadas e ofertas de biblioteca {#custom-offers-and-library-offers}

Ofertas que são [criadas na página](#adding-a-custom-offer) e usadas para uma única experiência são chamadas de ofertas personalizadas. A imagem a seguir é sobreposta ao conteúdo de uma oferta personalizada:

![Ícone da oferta personalizada](../assets/targeted-custom-offer-icon.png)

As ofertas [adicionadas de uma biblioteca de ofertas](#adding-an-offer-from-an-offer-library) são sobrepostas com a seguinte imagem:

![Ícone da oferta da biblioteca](../assets/targeted-library-offer-icon.png)

É possível salvar ofertas personalizadas em uma biblioteca de ofertas, caso deseje reutilizá-las futuramente. Você também pode converter uma oferta de biblioteca em uma oferta personalizada se quiser modificar o conteúdo de uma experiência. Após a edição, é possível salvar a oferta novamente na biblioteca.

### Adicionar e remover experiências usando o modo de direcionamento {#adding-and-removing-experiences-using-targeting-mode}

Usando a etapa Criar [do processo de direcionamento](#the-targeting-process-create-target-and-goals-settings), você pode adicionar e remover experiências. Além disso, é possível duplicar e renomear uma experiência.

#### Adição de experiências usando o modo de direcionamento {#adding-experiences-using-targeting-mode}

Para adicionar uma experiência:

1. Para adicionar uma experiência, selecione **+** **Adicionar Direcionamento de Experiência**, que aparece abaixo das experiências existentes no painel **Públicos-alvo**.
1. Selecione o público-alvo. Por padrão, esse será o nome da experiência. Você pode digitar outro nome, se desejar. Selecione **OK**.

#### Remoção de experiências usando o modo de direcionamento {#removing-experiences-using-targeting-mode}

Para excluir uma experiência:

1. Selecione a seta ao lado do nome da experiência.

   ![Excluir e experiência](../assets/targeted-delete-experiene.png)

1. Clique em **Excluir**.

#### Renomear experiências usando o modo de direcionamento {#renaming-experiences-using-targeting-mode}

Para renomear experiências usando o modo de direcionamento:

1. Selecione a seta ao lado do nome da experiência.
1. Clique em **Renomear experiência** e digite o novo nome.
1. Selecione outro local na tela para salvar as alterações.

#### Edição de públicos-alvo usando o modo de direcionamento {#editing-audiences-using-targeting-mode}

Para editar os públicos-alvo usando o modo de direcionamento:

1. Selecione a seta ao lado do nome da experiência.
1. Clique em **Editar público** e selecione um novo público.
1. Clique em **OK**.

#### Duplicar experiências usando o modo de direcionamento {#duplicating-experiences-using-targeting-mode}

Para copiar experiências usando o modo de direcionamento:

1. Selecione a seta ao lado do nome da experiência.
1. Clique em **Duplicar** e escolha o público.
1. Renomeie a experiência, se desejar, e clique em **OK**.

### Criar ofertas usando o modo de direcionamento {#creating-offers-using-targeting-mode}

Direcione um componente para criar ofertas de experiências. Os componentes direcionados fornecem o conteúdo usado como ofertas para experiências.

* [Direcionar um componente existente](#creating-a-default-offer-by-targeting-an-existing-component). O conteúdo se torna a oferta da experiência padrão.
* [Adicione um componente de Direcionamento](#creating-an-offer-by-adding-a-target-component) e, em seguida, adicione o conteúdo ao componente.

Depois que um componente for direcionado, você poderá adicionar ofertas para cada experiência:

* [Adicionar ofertas personalizadas](#adding-a-custom-offer).
* [Adicionar ofertas a partir de uma biblioteca](#adding-an-offer-from-an-offer-library).

As seguintes ferramentas estão disponíveis para trabalhar com ofertas:

* [Adicionar uma oferta personalizada a uma biblioteca de ofertas](#adding-a-custom-offer-to-a-library).
* [Converter uma oferta da biblioteca em uma oferta personalizada](#converting-a-library-offer-to-a-custom-library).
* [Abrir uma oferta da biblioteca e editar o conteúdo](#editing-a-library-offer).

#### Criação de uma oferta padrão por meio do direcionamento de um componente existente {#creating-a-default-offer-by-targeting-an-existing-component}

Direcione um componente na página para usá-lo como a oferta para a experiência padrão da atividade. Quando você direciona um componente, ele é envolvido em um componente de direcionamento e seu conteúdo se torna a oferta para a experiência padrão.

Após direcionar um componente, somente ele poderá ser usado na oferta. Não é possível remover o componente da oferta ou adicionar outros componentes.

Execute o seguinte procedimento depois de [iniciar o processo de direcionamento](#the-targeting-process-create-target-and-goals-settings).

1. Selecione o componente a ser direcionado. A barra de ferramentas do componente aparece, semelhante ao exemplo a seguir.

   ![Componente direcionado](../assets/targeted-component.png)

1. Selecione o ícone Target.

   ![Botão Direcionar](../assets/targeted-target-button.png)

   O conteúdo do componente é a oferta para a experiência padrão. Quando um componente é direcionado, seu nó padrão é replicado para cada experiência. Isso é necessário para editar o nó de conteúdo correto durante a criação da experiência. Para essas experiências diferentes do padrão,[&#x200B; adicione uma oferta personalizada](#adding-a-custom-offer) ou[&#x200B; adicione uma oferta da biblioteca](#adding-an-offer-from-an-offer-library).

#### Criação de uma oferta adicionando um componente de Direcionamento {#creating-an-offer-by-adding-a-target-component}

Adicione um componente de Direcionamento para criar a oferta para experiência Padrão. O componente de Direcionamento é um contêiner de outros componentes e os componentes incluídos nele tornam-se direcionados. No componente de Direcionamento, é possível adicionar vários componentes para criar uma oferta. Além disso, é possível usar componentes diferentes em cada experiência para criar ofertas diferentes.

Consulte [Configuração das opções do componente de Direcionamento](#configuring-target-component-options) para obter informações sobre como personalizar esse componente.

>[!NOTE]
>
>As ofertas criadas usando o [console Ofertas](/help/sites-cloud/authoring/personalization/offers.md) também podem conter vários componentes. Essas ofertas pertencem a uma biblioteca de ofertas e podem ser usadas em várias experiências.

Como o componente de direcionamento é um container, ele aparece como uma área onde é possível soltar outros componentes.

No modo de direcionamento, o componente de direcionamento tem uma borda azul, e a mensagem de direcionamento indica a natureza direcionada.

![Área de destino do direcionamento](../assets/targeted-drop-target.png)

No modo de Edição, o componente de Direcionamento tem um ícone de alvo.

![Ícone da área de destino do direcionamento](../assets/targeted-drop-target-icon.png)

Quando você arrasta os componentes ao componente de Direcionamento, eles se tornam componentes direcionados.

![Área de destino com direcionamentos](../assets/targeted-drop-zone-populated.png)

Quando você adiciona um componente ao componente de direcionamento, ele fornece conteúdo para uma experiência específica. Para especificar a experiência, selecione-a antes de adicionar os componentes.

Você pode adicionar um componente de direcionamento à página no modo de edição ou de direcionamento. Você pode adicionar componentes ao componente de direcionamento somente no modo de direcionamento. O componente de direcionamento pertence ao grupo de componentes de personalização.

Se estiver editando o conteúdo direcionado, você deve selecionar **Iniciar o direcionamento** antes de fazer isso.

1. Arraste o componente de direcionamento até a página onde deseja que a oferta apareça.
1. Por padrão, nenhuma ID de localização está definida. Selecione o botão de configuração cog wheel para definir o local.

   >[!NOTE]
   >
   >Se definido pelo administrador, talvez seja necessário definir explicitamente a localização.
   >
   >Os administradores podem decidir se essa configuração é obrigatória em `https://<host>:<port>/system/console/configMgr/com.day.cq.personalization.impl.servlets.TargetingConfigurationServlet`
   >
   >Para exigir que os usuários insiram um local, marque a caixa de seleção **Forçar local**.

1. Selecione a experiência para a qual deseja criar a oferta.
1. Crie a oferta:

   * Para a experiência padrão, arraste os componentes para área de destino e edite suas propriedades como de costume para criar o conteúdo da oferta.
   * Para experiências não tradicionais, [adicione uma oferta personalizada](#adding-a-custom-offer) ou [uma oferta da biblioteca](#adding-an-offer-from-an-offer-library).

#### Adicionar uma oferta personalizada {#adding-a-custom-offer}

Gere uma oferta criando o conteúdo de um componente direcionado no modo de direcionamento. Quando você cria uma oferta personalizada, ela é usada como oferta para uma única experiência.

Se decidir que a oferta pode ser usada para outras experiências, poderá criar uma oferta personalizada e [adicioná-la à biblioteca](#adding-a-custom-offer-to-a-library). Para obter informações sobre como usar o console Ofertas para criar uma oferta reutilizável, consulte [Adicionar uma oferta a uma biblioteca de ofertas](/help/sites-cloud/authoring/personalization/offers.md#add-an-offer-to-an-offer-library).

1. Selecione a experiência à qual você está adicionando a oferta.
1. Para exibir o menu de componentes, selecione o componente de destino ao qual você está adicionando a oferta.

   ![Adicionar uma oferta](../assets/targeted-component-menu.png)

1. Selecione o ícone +.

   O conteúdo da oferta padrão é usado como a oferta da experiência atual.

1. Selecione a oferta para exibir o menu de ofertas e selecione o ícone de edição.

   ![Barra de ferramentas do componente de direcionamento](../assets/targeted-offer-menu.png)

1. Edite o conteúdo do componente.

#### Adicionar uma oferta a partir de uma biblioteca de ofertas {#adding-an-offer-from-an-offer-library}

Adicione uma oferta da [biblioteca de ofertas](/help/sites-cloud/authoring/personalization/offers.md) a uma experiência. É possível adicionar qualquer oferta da biblioteca da marca que você está direcionando.

Não é possível adicionar ofertas de biblioteca à experiência padrão.

1. Selecione a experiência à qual você está adicionando a oferta.
1. Para exibir o menu de componentes, selecione o componente de destino ao qual você está adicionando a oferta.

   ![Oferta direcionada](../assets/targeted-add-offer-large.png)

1. Selecione o ícone de pasta.

   ![Ícone de pasta](../assets/targeted-folder-button.png)

1. Selecione a oferta da biblioteca e clique no ícone de marca de seleção.

   ![Biblioteca de ofertas](../assets/targeted-select-content.png)

   O seletor de ofertas permite procurar ou filtrar ofertas. Ao procurar ou filtrar, você também pode classificar as ofertas e alterar a forma como as visualiza. O número no canto superior direito indica quantas ofertas estão disponíveis na biblioteca atual.

   * Selecione **Procurar** para navegar para outra pasta. O painel de navegação é aberto e você clica na seta para mostrar o detalhamento das pastas. Selecione **Procurar** novamente para fechar o painel de navegação.

   ![Procurar conteúdo](../assets/targeted-select-content-browse.png)

   * Selecione **Filtro** para filtrar as ofertas com base em palavras-chave ou marcas. Digite as palavras-chave e selecione as tags no menu suspenso. Selecione **Filtro** novamente para fechar o painel de filtragem.

   ![Filtrar conteúdo](../assets/targeted-filter.png)

   * Altere a forma como você classifica as ofertas clicando ou tocando na seta ao lado de **Do mais novo ao mais antigo**. As ofertas podem ser ordenadas da mais recente para a mais antiga ou da mais antiga para a mais recente.

   ![Filtrar ordem de classificação](../assets/targeted-filter-sort.png)

   Selecione o ícone ao lado de **Exibir como** para exibir as ofertas como mosaicos ou como uma lista.

   ![Botão Exibir como](../assets/targeted-view-as-button.png)

#### Adicionar uma oferta personalizada a uma biblioteca {#adding-a-custom-offer-to-a-library}

Adicione uma oferta personalizada à [biblioteca de ofertas](/help/sites-cloud/authoring/personalization/offers.md) caso queira reutilizar a oferta em várias experiências. É possível adicionar ofertas à biblioteca da marca que você está direcionando atualmente.

Para obter informações sobre como usar o console Ofertas para criar uma oferta reutilizável, consulte [Adicionar uma oferta a uma biblioteca de ofertas](/help/sites-cloud/authoring/personalization/offers.md#add-an-offer-to-an-offer-library).

1. Selecione a experiência para exibir a oferta personalizada.
1. Selecione a oferta personalizada para exibir o menu de ofertas e selecione o ícone **Salvar oferta na biblioteca de ofertas**.

   ![Salvar oferta na biblioteca de ofertas](../assets/targeted-save-offer-library-button.png)

1. Digite um nome para a oferta, selecione a biblioteca à qual está adicionando a oferta e selecione o ícone de marca de seleção.

#### Converter uma oferta de biblioteca em uma biblioteca personalizada {#converting-a-library-offer-to-a-custom-library}

Converta uma oferta da biblioteca em uma oferta personalizada para alterar a oferta da experiência atual sem alterar a de outras experiências.

1. Selecione a experiência para exibir a oferta da biblioteca.
1. Selecione a oferta da biblioteca para revelar o menu de ofertas e selecione o ícone Converter em oferta em linha.

   ![Converter para oferta inline](../assets/targeted-convert-inline.png)

#### Editar uma oferta da biblioteca {#editing-a-library-offer}

Abra uma oferta de biblioteca de uma experiência no modo de direcionamento para editá-la. As alterações feitas aparecem em todas as experiências que usam a oferta.

1. Selecione a experiência para exibir a oferta da biblioteca.
1. Converta a oferta da biblioteca em uma oferta local/personalizada. Consulte [Converter uma oferta de biblioteca a uma biblioteca personalizada](#converting-a-library-offer-to-a-custom-library).
1. Edite o conteúdo da oferta.

1. Salve na biblioteca. Consulte [Adicionar uma oferta personalizada a uma biblioteca](#adding-a-custom-offer-to-a-library).

## Direcionar: configuração dos públicos-alvo {#target-configuring-the-audiences}

A etapa Direcionar do [processo de direcionamento](#the-targeting-process-create-target-and-goals-settings) envolve mapear públicos-alvo para as experiências com as quais você trabalhou na etapa Criar. A página Direcionar mostra os públicos-alvo que são direcionados por cada experiência. Você pode especificar ou alterar o público-alvo de cada experiência. Se estiver usando o Adobe Target, será possível criar testes A/B que permitem direcionar uma porcentagem do tráfego de um público-alvo para uma experiência específica.

### Se estiver usando o direcionamento do AEM ou o Adobe Target (direcionamento de experiência) {#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

Os públicos são exibidos no lado esquerdo do diagrama de mapeamento e as experiências, no lado direito.

![Mapeamento de públicos](../assets/targeted-diagram.png)

Defina um público usando um segmento. A configuração da nuvem para a página determina os segmentos que estão disponíveis para você. Quando a página não está associada a uma configuração de nuvem do Adobe Target, os segmentos do AEM estarão disponíveis para definir públicos-alvo. Quando a página está associada a uma configuração de nuvem do Adobe Target, você usará segmentos do Target.

Para obter informações sobre mecanismos de direcionamento, consulte [Mecanismo de direcionamento](/help/sites-cloud/authoring/personalization/overview.md#targeting-engine).

Um público-alvo não deve ser usado por mais de uma experiência. Um símbolo de aviso é exibido ao lado de uma experiência quando ela é mapeada para um público-alvo que já está mapeado para outra experiência.

![Ícone de aviso](../assets/targeted-warn.png)

### Associação de experiências com públicos-alvo (AEM ou Adobe Target) {#associating-experiences-with-audiences-aem-or-adobe-target}

Use o procedimento a seguir para associar uma experiência a um público-alvo ao usar o direcionamento do AEM (ou direcionamento de experiência do Adobe Target):

1. Selecione a seta suspensa ao lado na caixa de público-alvo que está mapeada para a experiência.
1. (Opcional) Selecione **Editar** e digite uma palavra-chave para pesquisar pelo segmento desejado.
1. Na lista de públicos, selecione o público e selecione **OK**.

### Se estiver usando o Teste A/B (Adobe Target) {#if-you-are-using-a-b-testing-adobe-target}

Se tiver uma atividade de teste A/B, os públicos-alvo estarão à esquerda, a porcentagem de visualização de cada experiência estará no meio e as experiências estarão à direita.

É possível alterar as porcentagens desde que sua soma seja 100%. Um público-alvo pode ser usado por várias experiências no teste A/B.

![Direcionamento A/B](../assets/targeted-ab.png)

### Associação de públicos-alvo e porcentagens de tráfego com teste A/B {#associating-audiences-and-traffic-percentages-with-a-b-testing}

1. Selecione a caixa suspensa ao lado do público-alvo mapeado para a experiência.
1. (Opcional) Clique em **Editar** e digite uma palavra-chave para pesquisar pelo segmento desejado.
1. Selecione **OK.**
1. Insira porcentagens para configurar como o tráfego de público-alvo será roteado para cada experiência. O número total precisa ser igual a 100.
1. (Opcional) Edite o nome da experiência clicando no menu suspenso ao lado do nome da experiência.

## Metas e Configurações: configuração da atividade e definição de metas {#goals-settings-configuring-the-activity-and-setting-goals}

A etapa Metas e configurações do [processo de direcionamento](#the-targeting-process-create-target-and-goals-settings) envolve a configuração do comportamento da atividade da marca. Especifique quando a atividade começa e termina e sua prioridade. Além disso, você também acompanha metas. Especificamente, você pode decidir o que deseja medir com suas atividades.

As Métricas de Meta só estarão disponíveis se você usar o Adobe Target como seu mecanismo de direcionamento. É necessário ter, pelo menos, uma métrica de meta. Se o Adobe Analytics estiver configurado e você tiver uma configuração de nuvem A4T do Analytics, será possível selecionar se deseja que a fonte de relatórios seja o Adobe Target ou o Adobe Analytics.

As métricas de meta são medidas apenas para a campanha publicada.

Se estiver usando o AEM como o mecanismo de direcionamento:

![AEM como mecanismo de direcionamento](../assets/targeted-goals.png)

Se estiver usando o Adobe Target como mecanismo de direcionamento:

![Adobe Target como mecanismo de direcionamento](../assets/targeted-engine.png)

Se estiver usando o Adobe Target como mecanismo de direcionamento e tiver o A4T Analytics configurado para a conta, terá um menu suspenso **Fonte de relatórios** adicional:

![A4T](../assets/targeted-source.png)

As seguintes métricas de sucesso estão disponíveis (usadas somente para publicação):

| Métrica | Descrição | Opções |
|---|---|---|
| Conversão | A porcentagem de visitantes que clicaram em qualquer parte da experiência que está sendo testada. Uma conversão pode ser contada uma vez por visitante ou cada vez que um visitante conclui uma conversão. A métrica de conversão é definida como uma das seguintes opções | Visualizou uma página — é possível definir qual página o público visualizou selecionando “URL é” e, em seguida, definindo o URL ou vários URLs, ou selecionando “URL contém” e adicionando um caminho ou palavra-chave. Visualizou uma mbox — é possível definir a mbox visualizada pelo público inserindo o nome da mbox. É possível inserir várias mboxes clicando em Adicionar uma mbox. |
| Receita | Receita gerada pela visita. Você pode escolher entre as métricas de receita listadas. Para qualquer uma dessas opções, a visualização de uma mbox indica que a meta foi atingida. É possível definir a mbox ou várias mboxes. | Receita por visitante (RPV), Valor médio de pedido (AOV), Vendas totais, Pedidos |
| Envolvimento | Você pode medir três tipos de envolvimento | Exibições de página, Pontuação personalizada, Tempo no site |

Além disso, há configurações avançadas que permitem determinar como contar as métricas de sucesso. As opções incluem contagem da métrica por impressão ou uma vez por visitante, além de escolher se deseja manter o usuário na atividade ou removê-lo.

Use as configurações avançadas para determinar o que acontece **após** um usuário encontrar a métrica de meta. A tabela a seguir mostra as opções disponíveis.

| Após um usuário encontrar essa métrica de meta... | Você seleciona o seguinte para acontecer... |
|---|---|
| Incrementar contagem e manter usuário em atividade | Especifica como a contagem é incrementada: uma vez por participante, em cada impressão, excluindo atualizações de página, em cada impressão |
| Incrementar contagem, liberar usuário e permitir reentrada | Selecione a experiência que o visitante vê ao entrar na atividade novamente: mesma experiência, experiência aleatória, experiência inédita |
| Incrementar contagem, liberar usuário e reentrada de barra | Determina o que o usuário vê em vez do conteúdo da atividade: mesma experiência, sem rastreamento, conteúdo padrão ou outro conteúdo de atividade |

Consulte a [documentação do Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=pt-BR) para obter mais informações sobre métricas de sucesso.

### Definição de configurações (direcionamento do AEM) {#configuring-settings-aem-targeting}

Para definir as configurações se estiver usando o direcionamento do AEM:

1. Para especificar quando a atividade será iniciada, use o menu suspenso **Início** para selecionar um dos seguintes valores:

   * **Quando ativada**: a atividade começa quando a página que contém o conteúdo direcionado é ativada.
   * **Data e hora especificadas**: uma hora específica. Ao selecionar essa opção, selecione o ícone de calendário, selecione uma data e especifique a hora para iniciar a atividade.

1. Para especificar quando a atividade se encerra, use o menu suspenso **Término** para selecionar um dos seguintes valores:

   * **Quando desativada**: a atividade termina quando a página que contém o conteúdo direcionado é desativada.
   * **Data e hora especificadas**: uma hora específica. Ao selecionar essa opção, selecione o ícone de calendário, selecione uma data e especifique a hora para encerrar a atividade.

1. Para especificar uma prioridade para a atividade, use o controle deslizante para selecionar **Baixa**, **Normal** ou **Alta**.

### Definição de metas e configurações (Adobe Target) {#configuring-goals-settings-adobe-target}

Para definir metas e configurações se estiver usando o Adobe Target:

1. Para especificar quando a atividade será iniciada, use o menu suspenso **Início** para selecionar um dos seguintes valores:

   * **Quando ativada**: a atividade começa quando a página que contém o conteúdo direcionado é ativada.
   * **Data e hora especificadas**: uma hora específica. Ao selecionar essa opção, selecione o ícone de calendário, selecione uma data e especifique a hora para iniciar a atividade.

1. Para especificar quando a atividade se encerra, use o menu suspenso **Término** para selecionar um dos seguintes valores:

   * **Quando desativada**: a atividade termina quando a página que contém o conteúdo direcionado é desativada.
   * **Data e hora especificadas**: uma hora específica. Ao selecionar essa opção, selecione o ícone de calendário, selecione uma data e especifique a hora para encerrar a atividade.

1. Para especificar uma prioridade para a atividade, use o controle deslizante para selecionar **Baixa**, **Normal** ou **Alta**.
1. Se você tiver configurado o Adobe Analytics com sua conta do Adobe Target, verá o menu suspenso **Fonte de relatórios**. Selecione **Adobe Target** ou **Adobe Analytics** como a fonte.

   Se selecionar o **Adobe Analytics**, selecione a empresa e o conjunto de relatórios. Se selecionar **Adobe Target**, nenhuma ação será necessária.

   ![Fonte dos relatórios](../assets/targeted-reporting-source.png)

1. Na área **Métrica de meta**, em **Meu objetivo principal**, selecione a métrica de sucesso que deseja rastrear - Conversão, Receita, Participação - e insira como essa métrica é medida (ou que ação o público-alvo executa para indicar que um objetivo foi atingido). Consulte a definição das métricas de objetivo na tabela anterior e consulte a [documentação do Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=pt-BR) sobre métricas de sucesso.

   Você pode renomear a meta ao clicar nos três pontos no canto superior direito e selecionar **Renomear**.

   Se precisar limpar todos os campos, clique nos três pontos no canto superior direito e selecione **Limpar todos os campos**.

   Todas as métricas também têm configurações avançadas que podem ser definidas. Selecione **Configurações avançadas** para acessá-las. Consulte a definição de como as métricas de sucesso são contadas na tabela anterior, bem como a [documentação do Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=pt-BR).

   >[!NOTE]
   >
   >Você deve ter, pelo menos, uma meta definida.

   ![Métrica de objetivo](../assets/targeted-goal-metric.png)

   >[!NOTE]
   >
   >Se houver informações ausentes em sua métrica, uma linha vermelha circundará a métrica.

1. Clique em **Adicionar uma nova métrica** para configurar métricas de sucesso adicionais.

   ![Métricas adicionais](../assets/targeted-additional-metrics.png)

   >[!NOTE]
   >
   >É possível remover metas adicionais clicando ou tocando nos três pontos e clicando ou tocando em **Excluir**. O AEM exige que você tenha pelo menos uma meta definida.

1. Se quiser ter mais controle sobre como as métricas de sucesso são contadas, selecione **Configurações avançadas** para acessá-las.
1. Clique em **Salvar**.

Após a configuração, é possível [visualizar o desempenho de suas atividades](/help/sites-cloud/authoring/personalization/activities.md#viewing-performance-and-converting-winning-experiences-a-b-test) que usam o Adobe Target (direcionamento de experiência ou de teste A/B). Além disso, com o direcionamento de teste A/B, é possível [converter os vencedores](/help/sites-cloud/authoring/personalization/activities.md#viewing-performance-and-converting-winning-experiences-a-b-test).

## Simulação de uma Experiência {#simulating-an-experience}

Simule a experiência de um visitante para verificar se o conteúdo da página aparece como esperado de acordo com o design de seu conteúdo direcionado. Ao simular, carregue perfis de usuário diferentes e veja o conteúdo direcionado para esses usuários.

Os critérios a seguir determinam o conteúdo que aparece ao simular a experiência de um visitante:

* Os dados no armazenamento de sessão do usuário (via Context Hub).
* As [Atividades que estão ativadas](/help/sites-cloud/authoring/personalization/activities.md).
* As [regras que definem os segmentos](/help/sites-cloud/authoring/personalization/segmentation.md).
* O conteúdo das experiências nos componentes do Target.
* A [configuração do mecanismo de direcionamento](/help/sites-cloud/authoring/personalization/activities.md).

Se algum conteúdo inesperado aparecer na página ao carregar um perfil, verifique a configuração de cada item nesta lista.

>[!NOTE]
>
>Se estiver usando o teste A/B ao simular experiências, elas serão mostradas com base na porcentagem de tráfego. Isso é controlado pelo Adobe Target, o que pode levar a resultados inesperados para os autores. (A atividade _author é sincronizada com configurações específicas que permitem a reavaliação durante a simulação). Os autores podem precisar atualizar para ver as outras experiências com base nas suas configurações de tráfego.

Para simular a experiência do visitante, use as seguintes ferramentas:

* A simulação da atividade no modo Direcionamento: a página exibe as ofertas para o usuário que está selecionado no Context Hub. É possível editar as ofertas direcionadas ao usuário.
* Modo de visualização: use o Context Hub para selecionar os usuários e locais que atendem aos critérios dos segmentos nos quais suas experiências se baseiam. Quando suas seleções do Context Hub são alteradas, o conteúdo direcionado é alterado de acordo.

1. Para alternar para o modo de Visualização, selecione **Visualização** na barra de ferramentas.
1. Na barra de ferramentas, selecione o ícone do Context Hub.

   ![Botão ContextHub](../assets/targeted-contexthub-button.png)

1. Use o Context Hub para alterar as propriedades do contexto. Por exemplo, selecione a propriedade Persona para selecionar um usuário diferente.

   ![Barra de ferramentas do ContextHub](../assets/targeted-contexthub-toolbar.png)

   A página é alterada para mostrar o conteúdo que é direcionado para o contexto atual.

1. Para alterar as ofertas exibidas, alterne para o modo Direcionamento. Com a atividade de simulação selecionada, edite as ofertas para o contexto que você configurou no modo Visualização.

## Configuração das opções do componente do Target {#configuring-target-component-options}

É possível personalizar o componente do Target acessando as opções do componente de uma das duas formas a seguir:

1. Depois de direcionar o componente, no componente de Direcionamento, selecione o componente e o ícone de configurações (engrenagem).

   ![Configurações do componente](../assets/targeted-component-settings.png)

   O AEM exibe a janela de opções do componente de Direcionamento.

   ![Caixa de diálogo do Target](../assets/targeted-dialog.png)

1. Como alternativa, para acessar essas configurações no modo de tela cheia, na janela de opções do componente de Direcionamento, selecione o ícone de tela cheia.

   ![Botão de tela cheia](../assets/targeted-fullscreen.png)

   O AEM exibe a janela de opções do componente de Direcionamento em tela cheia.

   ![Componente em tela cheia](../assets/targeted-target-as-enging.png)

1. Defina as configurações do componente de Direcionamento conforme descrito nas tabelas a seguir.

| Opção | Descrição |
|---|---|
| Local | O local é uma sequência de caracteres que dá um nome ao local do conteúdo direcionado e conecta ofertas a lugares (ou locais ou componentes) na página onde essas ofertas devem ser colocadas. Este campo é um valor genérico. Se você adicionar uma oferta a um componente, ela se lembrará da ID de localização. Quando a página é executada, o mecanismo avalia os segmentos do usuário e, com base nisso, decide as experiências das campanhas ativas que devem ser exibidas. Em seguida, verifica as IDs de localização na página e tenta corresponder as ofertas com essas IDs. |
| Mecanismo | Selecione entre Regras do lado do cliente (sem rastreamento), Adobe Target, ContextHub e Adobe Campaign, dependendo do mecanismo que deseja usar. |

Se você selecionar Adobe Target como mecanismo:

![Target como mecanismo](../assets/targeted-target-as-enging.png)

| Opção | Descrição |
|---|---|
| Destinação exata | Habilitar o direcionamento preciso informa ao componente para esperar que os dados do contexto do cliente ou do hub de contexto estejam disponíveis antes de enviar a solicitação para o Adobe Target. Pode aumentar o tempo de carregamento. Ao criar, o direcionamento preciso está sempre ativado. Se você marcar a caixa de seleção de Direcionamento preciso, a mbox executará primeiro um mboxDefine e depois um mboxUpdate, o que resultará em uma solicitação de Ajax quando os dados estiverem disponíveis. Se você não marcar a caixa de seleção de Direcionamento preciso, a mbox executará um mboxCreate, que resultará em uma solicitação síncrona de imediato (neste caso, nem todos os dados de contexto podem estar disponíveis). Observação: ativar ou desativar o direcionamento preciso em um componente específico não afeta as configurações definidas globalmente. Sempre é possível substituir as configurações globais selecionando Direcionamento preciso no componente. |
| Incluir segmentos resolvidos | Selecionar essa caixa de seleção inclui todos os segmentos resolvidos na chamada da mbox e quaisquer parâmetros configurados na página e na estrutura. Somente funciona em situações com a API XML na qual você está sincronizando os segmentos do AEM. Se você tiver segmentos no AEM que não são manipulados pelo Adobe Target (como segmentos de script), essa opção permite resolver o segmento no AEM e enviar informações para o Adobe Target de que o segmento está ativo. |
| Parâmetros herdados de contexto | Lista os parâmetros de contexto herdados da estrutura do Adobe Target, se houver, associados à página selecionada. |
| Parâmetros de contexto | Selecione Adicionar campo para configurar parâmetros de contexto adicionais (mesma opção disponível na estrutura do Target). Os parâmetros de contexto adicionados ao componente se aplicam somente a ele, não a outros componentes, como ocorre ao adicionar parâmetros de contexto diretamente à estrutura. |
| Parâmetros estáticos | Selecione Add field para configurar parâmetros estáticos adicionais (mesma opção disponível na estrutura do Target). Os parâmetros estáticos adicionados ao componente se aplicam somente a ele, não a outros componentes, como ocorre ao adicionar parâmetros estáticos diretamente à estrutura. Os parâmetros estáticos não provêm do contexto (contexto do cliente do content hub). |

>[!NOTE]
>
>Ao selecionar um componente e torná-lo compatível com o público-alvo, o AEM também substitui o componente e injeta um componente do Adobe Target. (O componente do Adobe Target não é usado apenas ao adicioná-lo manualmente à página, mas também quando você direciona um componente já existente).
>
>Selecione **Adobe Campaign** como mecanismo se estiver integrando o AEM com o Adobe Campaign. Consulte Integrar o AEM com o Adobe Campaign para obter mais informações.
>
>Selecione **ContextHub** como mecanismo se estiver usando o ContextHub para o direcionamento. Consulte Configuração do ContextHub para obter mais informações.
<!--You select **Adobe Campaign** as the engine if you are integrating AEM with Adobe Campaign. See [Integrating AEM with Adobe Campaign](/help/sites-administering/campaign.md) for more information.-->
<!--Select **ContextHub** as the engine if you are using ContextHub for targeting. See [Configuring ContextHub](/help/sites-administering/contexthub-config.md).-->
