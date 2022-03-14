---
title: Gerenciamento de atividades
description: O console Atividades permite criar, organizar e gerenciar as atividades de marketing das suas marcas
exl-id: e7cab16d-7678-472d-b75f-7f67b303ba8d
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '2002'
ht-degree: 86%

---

# Gerenciamento de atividades {#managing-activities}

O console Atividades permite criar, organizar e gerenciar as [atividades](/help/sites-cloud/authoring/personalization/overview.md#activities) de marketing das suas marcas:

* Adicionar marcas
* Para cada marca, adicione e configure atividades
* Administrar atividades

>[!TIP]
>
>Se estiver usando o Adobe Target como seu mecanismo de direcionamento, também é possível [visualizar dados de desempenho das suas atividades](#viewing-performance-and-converting-winning-experiences-a-b-test). Se estiver usando testes de A/B, você poderá [converter vencedores](#viewing-performance-and-converting-winning-experiences-a-b-test).

No console Atividades, as atividades são organizadas por marca. É possível usar marcas e pastas para estruturar a organização das suas atividades. Navegue até o console Atividades tocando/clicando em **Personalização** e depois em **Atividades**.

As atividades estão disponíveis no modo Direcionar para [criação de conteúdo direcionado](/help/sites-cloud/authoring/personalization/targeted-content.md), onde também é possível criar atividades. As atividades que você cria no modo Direcionar aparecem no console Atividades.

As atividades são exibidas com um rótulo descrevendo o tipo de atividade definido:

* XT - Direcionamento de experiência do Adobe Target
* A/B - Testes A/B do Adobe Target
* AEM - Direcionamento do Adobe Experience Manager (ou seja, orientado pelo ContextHub)

![Tipos de atividades](/help/sites-cloud/authoring/assets/activities-types.png)

>[!NOTE]
>
>Os tipos de atividades disponíveis são determinados pelo seguinte:
>
>* Se a opção `xt_only` estiver ativada no locatário do Adobe Target (clientcode) usado no AEM para conectar-se ao Adobe Target, você poderá criar **somente** atividades XT no AEM.
>
>* Se as opções `xt_only` **não** estiverem ativadas no locatário do Adobe Target (clientcode), você poderá criar atividades XT **e** A/B no AEM.
>
>**Nota adicional:** a opção `xt_only` é uma configuração aplicada em um determinado locatário do Target (clientcode) e só pode ser modificada diretamente no Adobe Target. Não é possível ativar ou desativar essa opção no AEM.

>[!CAUTION]
>
>Você deve proteger o nó de configurações da atividade `cq:ActivitySettings` na instância de publicação, para que ela fique inacessível aos usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
>
>Consulte Pré-requisitos para integração com o Adobe Target para obter informações detalhadas.
<!--
>See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securingtheactivitysettings) for detailed information.
-->

## Criação de uma marca com o uso do console Atividades {#creating-a-brand-using-the-activities-console}

Crie uma marca cujas atividades de marketing você deseja gerenciar.

Ao criar uma marca usando o console Atividades , ela também aparece na [Console de ofertas](/help/sites-cloud/authoring/personalization/offers.md) onde você pode criar ofertas para as experiências de suas atividades.

1. No console Navegação, clique ou toque em **Personalização**. Clique ou toque em **Atividades**.

   ![Navegar para atividades](/help/sites-cloud/authoring/assets/activities-navigation.png)

1. No console Atividades, clique ou toque em **Criar** e depois em **Criar marca**.
1. Selecione o modelo da marca e clique ou toque em **Próximo**.
1. Digite o título que você deseja atribuir à exibição da marca nos consoles Atividades e Ofertas. Opcionalmente, digite ou selecione uma ou mais tags para associar à marca.
1. Clique ou toque em **Criar**. Sua marca aparece no console Atividades.

## Adição/edição de uma atividade com o uso do console Atividades {#adding-editing-an-activity-using-the-activities-console}

Adicione uma atividade ou edite uma atividade existente para concentrar seus esforços de marketing em públicos-alvo específicos. Ao criar/editar uma atividade, você especifica as seguintes informações:

* **Nome:** o nome da atividade.
* **Mecanismo de definição de metas:** o [AEM](/help/sites-cloud/authoring/personalization/overview.md#aem) ou o [Adobe Target](/help/sites-cloud/authoring/personalization/overview.md#adobe-target) como mecanismo de conteúdo direcionado.
* **Selecionar uma configuração de destino:** (somente no Adobe Target) a configuração em nuvem que essa atividade deve usar para se conectar ao Adobe Target. Essa opção aparece somente quando o Adobe Target é selecionado para o Mecanismo de direcionamento.
* **Tipo de atividade**: O tipo de atividade - Teste A/B ou Direcionamento de experiência
* **Objetivo:** (opcional) uma descrição da atividade.
* **Experiências:** mapeamentos entre os nomes de público-alvo e os segmentos de marketing que você está direcionando.
* **Porcentagens de tráfego:** se o teste A/B for selecionado, você poderá alterar a quantidade de tráfego (em porcentagem) de cada experiência.
* **Duração:** o período em que a atividade é aplicada.
* **Prioridade**: a prioridade relativa da atividade. Quando as atividades fornecem conteúdo para os mesmos segmentos de usuários, a atividade de maior prioridade é priorizada.
* **Métrica de meta:** se o Adobe Target for selecionado como o mecanismo de definição de metas, você poderá adicionar métricas de sucesso à atividade. É necessária uma métrica de sucesso.

>[!NOTE]
>
>As novas atividades do Adobe Target precisam ser *criadas* no editor de conteúdo direcionado, não no console **Atividades**, pois a sincronização com o Adobe Target falhará.
>
>No entanto, você pode editar as atividades existentes do Adobe Target no console.

Para adicionar uma atividade:

1. Clique ou toque na marca para a qual você está criando a atividade e clique ou toque em **Criar** e em **Criar atividade**. Se estiver editando, selecione a atividade na tela Área mestre e clique ou toque em **Editar atividade**.
1. Forneça as informações a seguir e clique ou toque em **Próximo**:
   * Um nome para a atividade.
   * O mecanismo de direcionamento que será usado. ContextHub (AEM) é a opção selecionada por padrão. Se precisar usar o Adobe Target, crie a atividade no editor de conteúdo direcionado.
   * Se o Adobe Target estiver selecionado como mecanismo de segmentação, selecione/edite a configuração da nuvem a ser usada para conexão com o Adobe Target. (Cuidado para não selecionar uma estrutura criada para a sua configuração da nuvem.)
   * (Opcional) O objetivo ou uma descrição da atividade.
   * Selecione o Tipo de atividade.
1. Adicione uma ou mais experiências à atividade. Clique ou toque em **Adicionar experiência**.
1. Se estiver usando o direcionamento do AEM ou o direcionamento de experiência do Adobe Target:
   1. Clique ou toque em **Selecionar público-alvo** e selecione o segmento ao qual a experiência se destina.
   1. Clique ou toque em **Adicionar experiência**, digite um nome e clique ou toque em **OK**.
   1. Clique ou toque em **Próximo**.
Se estiver usando a opção Teste A/B do Adobe Target:
   1. Clique ou toque no ícone de lápis na caixa de públicos-alvo para selecionar um público-alvo.
   1. Clique ou toque em **Adicionar experiência**, digite um nome e clique ou toque em **OK**.
   1. Insira a porcentagem de tráfego que exibe cada experiência.
   1. Clique ou toque em **Próximo**.
1. Para especificar quando a atividade começa, use o menu suspenso **Início** para selecionar um dos seguintes valores:
   * **Quando ativado:** a atividade é iniciada quando a página que inclui o conteúdo direcionado é ativada.
   * **Data e hora especificada:** um horário específico. Ao selecionar essa opção, clique ou toque no ícone de calendário, selecione uma data e especifique a hora para iniciar a atividade.
1. Para especificar quando a atividade termina, use o menu suspenso Fim para selecionar um dos seguintes valores:
   * **Quando desativado:** a atividade termina quando a página que inclui o conteúdo direcionado é desativada.
   * **Data e hora especificada**: um horário específico. Ao selecionar essa opção, clique ou toque no ícone de calendário, selecione uma data e especifique a hora para concluir a atividade.
1. Para especificar uma prioridade para a atividade, use o controle deslizante para selecionar **Baixa**, **Normal** ou **Alta**.
1. Se estiver usando o Adobe Target como mecanismo de direcionamento, selecione o que deseja medir com essa atividade. Consulte [Configuração da atividade e da definição de metas](/help/sites-cloud/authoring/personalization/targeted-content.md) para obter mais informações sobre as métricas de sucesso disponíveis. É necessário selecionar pelo menos um objetivo.
1. Clique ou toque em **Salvar**.

   >[!NOTE]
   >
   >Depois de criar uma atividade, você precisa publicá-la para que ela fique disponível.

## Publicar e cancelar a publicação de atividades {#publishing-and-unpublishing-activities}

É necessário publicar atividades para disponibilizá-las. Por outro lado, talvez você queira torná-las indisponíveis cancelando essa publicação.

>[!NOTE]
>
>Ao cancelar a publicação de uma atividade, o status da atividade não é alterado, a menos que você atualize a página.

Para publicar ou cancelar a publicação de atividades:

1. Clique ou toque na marca e, em seguida, na área que contém a atividade que você deseja publicar ou cuja publicação você deseja cancelar.
1. Toque ou clique no ícone ao lado das atividades que você deseja publicar ou cuja publicação você deseja cancelar.

   ![Publicação por meio do console de atividades](/help/sites-cloud/authoring/assets/activities-console.png)

1. Para publicar, toque ou clique em **Publicar**. Para cancelar a publicação, toque ou clique em **Cancelar publicação**. Suas atividades são publicadas ou sua publicação é cancelada, e seu status é alterado no console Atividades (pode exigir uma atualização).

## Atividades em instâncias de Autor e Publicação {#activities-on-author-and-publish-instances}

Quando uma atividade que usa o mecanismo direcionado do Adobe Target é ativada, uma segunda atividade é criada na instância de publicação:

* A atividade na instância de autor rastreia a atividade na instância de autor e é útil para simular a experiência do visitante. A análise registrada para essa atividade reflete apenas o que ocorre na instância de autor.
* A atividade na instância de publicação reflete e responde à atividade no servidor de publicação. Esta é a atividade que é executada no site público-alvo. Somente a atividade de publicação é relevante para rastrear e analisar o uso do site público-alvo real.

## Visualização do desempenho e conversão de experiências vencedoras (teste A/B) {#viewing-performance-and-converting-winning-experiences-a-b-test}

Você pode ver o desempenho de qualquer atividade do Adobe Target (XT ou A/B). Se estiver usando testes A/B, você também poderá converter a experiência vencedora, que então se tornará a experiência padrão.

Para visualizar o desempenho da atividade e converter experiências vencedoras:

1. Em **Personalização**, clique ou toque em **Atividades** para navegar até o **Atividades** console.
1. Clique ou toque na marca cujas atividades você deseja ver.
1. Selecione a atividade e clique ou toque em **Propriedades da exibição**, clique na guia **Relatórios** e selecione a atividade na qual deseja exibir o desempenho/converter experiências vencedoras. Os dados de desempenho são exibidos.

   ![Verificar o desempenho da atividade](/help/sites-cloud/authoring/assets/activities-performance.png)

1. Clique ou toque no **Empurrar vencedor** link para encaminhar essa experiência como a experiência padrão.

   A conversão do vencedor faz o seguinte:

   * Desativa a atividade atual
   * Modifica todas as páginas e substitui o conteúdo segmentado pelo conteúdo real da experiência vencedora. O conteúdo da experiência vencedora torna-se parte da página normal **without** direcionamento.

   ![Conversão de vencedor](/help/sites-cloud/authoring/assets/activities-reports.png)

   Uma experiência vencedora é a experiência que gera mais Incentivo nos relatórios, que se baseia na taxa de conversão.

1. Clique ou toque em **Sim** para confirmar que você deseja converter o vencedor, desativando a experiência atual e substituindo-a pelo conteúdo da experiência vencedora.

## Sincronização de atividades com o Adobe Target {#synchronizing-activities-with-adobe-target}

As atividades que usam o mecanismo de direcionamento do Adobe Target são sincronizadas com campanhas do Adobe Target. Uma atividade é sincronizada automaticamente com o Adobe Target quando as seguintes condições são atendidas:

* A atividade contém pelo menos uma experiência.
* Pelo menos uma experiência contém um segmento mapeado e uma oferta.
* Cada experiência na atividade deve ter o mesmo número de ofertas.

Essas condições se aplicam a atividades em instâncias de autor e publicação.

Quando uma atividade é sincronizada, uma campanha correspondente é criada no Adobe Target:

* As atividades na instância de publicação têm o mesmo nome que a campanha do Adobe Target correspondente.
* As atividades na instância do autor correspondem às campanhas do Target com o mesmo nome `_author` sufixo.

![Sincronização com o Adobe Target](/help/sites-cloud/authoring/assets/activities-synch.png)

As atividades de autor são sincronizadas imediatamente quando a atividade é modificada. A sincronização imediata permite a simulação de atividades com o ContextHub.

Atividades de publicação são sincronizadas quando a atividade é publicada na instância de publicação do AEM.

## Solução de problemas com a sincronização de atividades {#troubleshooting-activity-synchronization}

Quando o AEM sincroniza uma atividade com o Adobe Target, o AEM inclui uma propriedade da atividade chamada `thirdPartyId`. O valor dessa propriedade se baseia no caminho da atividade no repositório do AEM. Nenhuma campanha no Adobe Target pode ter o mesmo valor para a propriedade `thirdPartyId`. Portanto, uma atividade não será sincronizada se uma campanha existente (de um tipo diferente AB, XT) no Adobe Target usar o mesmo valor para `thirdPartyId`.

Essa situação pode ocorrer nas seguintes circunstâncias:

1. Uma atividade é criada e sincronizada com o Adobe Target.
1. Em outra instância do AEM, uma atividade é criada com a mesma marca e usando o mesmo nome. A sincronização dessa atividade falha ao ser tentada.

Essa situação também pode ocorrer nas seguintes circunstâncias:

1. Uma atividade é criada e sincronizada com o Adobe Target. A atividade é então excluída no AEM.
1. Uma atividade é criada com a mesma marca e usando o mesmo nome da atividade excluída. A sincronização dessa atividade falha ao ser tentada.

Para evitar problemas de sincronização, sempre use nomes exclusivos para atividades do . Se uma atividade não for sincronizada, você poderá excluir a campanha no Adobe Target que usa o mesmo nome se essa campanha não estiver sendo usada.

>[!NOTE]
>
>Quando você cria uma campanha no Adobe Target, ele atribui uma propriedade chamada `thirdPartyId` a cada campanha. Quando você exclui a campanha no Adobe Target, a propriedade `thirdPartyId` não é excluída. Não é possível reutilizar o `thirdPartyId` para campanhas de tipos diferentes (AB, XT) e ele não pode ser removido manualmente. Para evitar esse problema, nomeie cada campanha com um nome exclusivo; os nomes de campanha, portanto, não podem ser reutilizados em tipos de campanha diferentes.
>
>Se você usar o mesmo nome no mesmo tipo de campanha, a campanha existente será substituída.
>
>Se, durante a sincronização, você encontrar o erro “A solicitação falhou. `thirdPartyId` já existe”, altere o nome da campanha e sincronize novamente.
