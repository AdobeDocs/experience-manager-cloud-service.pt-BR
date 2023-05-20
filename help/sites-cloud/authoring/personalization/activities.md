---
title: Gerenciamento de atividades
description: O console Atividades permite criar, organizar e gerenciar as atividades de marketing de suas marcas
exl-id: e7cab16d-7678-472d-b75f-7f67b303ba8d
source-git-commit: 56a7f214a4a1a3a58c56f1e06e3a98532054ffee
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 47%

---

# Gerenciamento de atividades {#managing-activities}

O console Atividades permite criar, organizar e gerenciar o marketing [atividades](/help/sites-cloud/authoring/personalization/overview.md#activities) de suas marcas:

* Adicionar marcas
* Para cada marca, adicione e configure atividades
* Administrar atividades

>[!TIP]
>
>Se estiver usando o Adobe Target como mecanismo de direcionamento, você também poderá [exibir dados de desempenho de suas atividades](#viewing-performance-and-converting-winning-experiences-a-b-test). Se estiver usando o teste A/B, você poderá [converter vencedores](#viewing-performance-and-converting-winning-experiences-a-b-test).

No console Atividades, as atividades são organizadas por marca. Você pode usar marcas e pastas para estruturar a organização de suas atividades. Navegue até o console Atividades tocando/clicando **Personalização** e tocando/clicando **Atividades**.

As atividades estão disponíveis no modo Direcionar para a [criação de conteúdo direcionado](/help/sites-cloud/authoring/personalization/targeted-content.md), onde você também pode criar atividades. As atividades criadas no modo Direcionamento são exibidas no console Atividades.

As atividades são exibidas com um rótulo descrevendo que tipo de atividade é definido:

* XT - Direcionamento de experiência do Adobe Target
* A/B - Teste A/B do Adobe Target
* AEM — Direcionamento do Adobe Experience Manager (ou seja, orientado pelo ContextHub)

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
>Você deve proteger o nó de configurações de atividade `cq:ActivitySettings` na instância de publicação para que ele fique inacessível aos usuários normais. O nó de configurações de atividade só deve estar acessível ao serviço que lida com a sincronização de atividades com o Adobe Target.
>
>Consulte os pré-requisitos para integração com o Adobe Target para obter informações detalhadas.
<!--
>See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securingtheactivitysettings) for detailed information.
-->

## Criação de uma marca usando o console Atividades {#creating-a-brand-using-the-activities-console}

Crie uma marca para a qual deseja gerenciar atividades de marketing.

Ao criar uma marca usando o console Atividades, ela também aparece no [console Ofertas](/help/sites-cloud/authoring/personalization/offers.md), onde é possível criar ofertas para as experiências das suas atividades.

1. No console Navegação, clique ou toque em **Personalização**. Clique ou toque **Atividades**.

   ![Navegar para atividades](/help/sites-cloud/authoring/assets/activities-navigation.png)

1. No console Atividades, clique ou toque em **Criar** depois **Criar marca**.
1. Selecione o modelo da marca e clique ou toque em **Próxima**.
1. Digite um título para a marca conforme você quer que ele seja exibido nos consoles Atividades e Ofertas. Opcionalmente, digite ou selecione uma ou mais tags para associar à marca.
1. Clique ou toque em **Criar**. Sua marca aparece no console Atividades.

## Adicionar/editar uma atividade usando o console Atividades {#adding-editing-an-activity-using-the-activities-console}

Adicione uma atividade ou edite uma atividade existente para concentrar seus esforços de marketing em públicos específicos. Ao criar/editar uma atividade, especifique as seguintes informações:

* **Nome:** o nome da atividade.
* **Mecanismo de definição de metas:** o [AEM](/help/sites-cloud/authoring/personalization/overview.md#aem) ou o [Adobe Target](/help/sites-cloud/authoring/personalization/overview.md#adobe-target) como mecanismo de conteúdo direcionado.
* **Selecionar uma configuração de destino:** (somente no Adobe Target) a configuração em nuvem que essa atividade deve usar para se conectar ao Adobe Target. Essa opção aparece somente quando o Adobe Target é selecionado para o Mecanismo de direcionamento.
* **Tipo de atividade:** o tipo de atividade — Teste A/B ou Direcionamento de experiência
* **Objetivo:** (opcional) uma descrição da atividade.
* **Experiências:** mapeamentos entre os nomes de público-alvo e os segmentos de marketing que você está direcionando.
* **Porcentagens de tráfego:** se o teste A/B for selecionado, você poderá alterar a quantidade de tráfego (em porcentagem) de cada experiência.
* **Duração:** o período em que a atividade é aplicada.
* **Prioridade**: a prioridade relativa da atividade. Quando as atividades fornecem conteúdo para os mesmos segmentos de usuários, a atividade de maior prioridade é priorizada.
* **Métrica de meta:** se o Adobe Target for selecionado como o mecanismo de definição de metas, você poderá adicionar métricas de sucesso à atividade. É necessária uma métrica de sucesso.

>[!NOTE]
>
>Para poder **selecionar uma configuração do Target**, você deve estar no grupo **Autores de atividade do Target**.

>[!NOTE]
>
>As novas atividades do Adobe Target precisam ser *criadas* no editor de conteúdo direcionado, não no console **Atividades**, pois a sincronização com o Adobe Target falhará.
>
>No entanto, você pode editar atividades existentes do Adobe Target no console.

Para adicionar uma atividade:

1. Clique ou toque na marca para a qual você está criando a atividade e clique ou toque em **Criar** e em **Criar atividade**. Se estiver editando, selecione a atividade na tela Área mestre e clique ou toque em **Editar atividade**.
1. Forneça as seguintes informações e clique ou toque em **Próxima**:
   * Um nome para a atividade.
   * O mecanismo de direcionamento a ser usado. O ContextHub (AEM) é selecionado por padrão. Se precisar usar o Adobe Target, crie a atividade no editor de conteúdo direcionado.
   * Se você selecionou Adobe Target como mecanismo de direcionamento, selecione/edite a configuração de nuvem a ser usada para se conectar ao Adobe Target. (Tenha cuidado para não selecionar uma estrutura criada para a configuração da nuvem.)
   * (Opcional) O objetivo ou uma descrição da atividade.
   * Selecione o Tipo de atividade.
1. Adicione uma ou mais experiências à atividade. Clique ou toque em **Adicionar experiência**.
1. Se estiver usando o direcionamento por AEM ou o direcionamento de experiência do Adobe Target:
   1. Clique ou toque em **Selecionar público-alvo** e selecione o segmento ao qual a sua experiência está direcionado.
   1. Clique ou toque em **Adicionar experiência**, digite um nome e clique ou toque em **OK**.
   1. Clique ou toque em **Próximo**.
Se estiver usando o teste A/B do Adobe Target:
   1. Clique ou toque no lápis na caixa Públicos para selecionar um público.
   1. Clique ou toque em **Adicionar experiência**, digite um nome e clique ou toque em **OK**.
   1. Insira a porcentagem de tráfego que exibe cada experiência.
   1. Clique ou toque em **Próximo**.
1. Para especificar quando a atividade será iniciada, use o **Início** para selecionar um dos seguintes valores:
   * **Quando ativado:** A atividade começa quando a página que contém o conteúdo direcionado é ativada.
   * **Data e hora especificada:** Uma hora específica. Ao selecionar essa opção, clique ou toque no ícone de calendário, selecione uma data e especifique a hora para iniciar a atividade.
1. Para especificar quando a atividade termina, use o menu suspenso End para selecionar um dos seguintes valores:
   * **Quando desativado**: a atividade termina quando a página que contém o conteúdo direcionado é desativada.
   * **Data e hora especificada**: um horário específico. Ao selecionar essa opção, clique ou toque no ícone de calendário, selecione uma data e especifique a hora para encerrar a atividade.
1. Para especificar uma prioridade para a atividade, use o controle deslizante para selecionar **Baixa**, **Normal** ou **Alta**.
1. Se estiver usando o Adobe Target como mecanismo de direcionamento, selecione o que deseja medir com essa atividade. Consulte [Configuração da atividade e definição de objetivos](/help/sites-cloud/authoring/personalization/targeted-content.md) para obter mais informações sobre as métricas de sucesso disponíveis. Você deve selecionar pelo menos uma meta.
1. Clique ou toque **Salvar**.

   >[!NOTE]
   >
   >Depois de criar uma atividade, é necessário publicá-la para que esteja disponível.

## Atividades de publicação e cancelamento de publicação {#publishing-and-unpublishing-activities}

Você precisa publicar atividades para disponibilizá-las. Por outro lado, talvez você queira tornar as atividades indisponíveis ao desfazer a publicação.

>[!NOTE]
>
>Ao cancelar a publicação de uma atividade, o status da atividade não é alterado, a menos que você atualize a página.

Para publicar ou desfazer a publicação de atividades:

1. Clique ou toque na marca e na área que contém a atividade que deseja publicar ou desfazer a publicação.
1. Toque ou clique no ícone ao lado da atividade ou atividades que deseja publicar ou desfazer a publicação.

   ![Publicação através do console de atividades](/help/sites-cloud/authoring/assets/activities-console.png)

1. Para publicar, toque ou clique **Publish**. Para desfazer a publicação, toque ou clique **Cancelar publicação**. Sua atividade ou atividades são publicadas ou não, e sua publicação é alterada no console Atividades (pode exigir uma atualização).

## Atividades em instâncias de Autor e Publicação {#activities-on-author-and-publish-instances}

Quando uma atividade que usa o mecanismo direcionado do Adobe Target é ativada, uma segunda atividade é criada na instância de publicação:

* A atividade na instância do autor rastreia a atividade na instância do autor e é útil para simular a experiência do visitante. A análise gravada para essa atividade reflete somente o que ocorre na instância do autor.
* A atividade na instância de publicação reflete e responde à atividade no servidor de publicação. Esta é a atividade executada no site público. Somente a atividade de publicação é relevante para rastrear e analisar o uso do site público real.

## Visualização de desempenho e conversão de experiências vencedoras (teste A/B) {#viewing-performance-and-converting-winning-experiences-a-b-test}

Você pode ver o desempenho de qualquer atividade do Adobe Target (XT ou A/B). Se você estiver usando o teste A/B, também poderá converter a experiência vencedora, que se tornará a experiência padrão.

Para visualizar o desempenho da atividade e converter experiências vencedoras:

1. Em **Personalização**, clique ou toque em **Atividades** para navegar até o console **Atividades**.
1. Clique ou toque na marca cujas atividades você deseja ver.
1. Selecione a atividade e clique ou toque em **Propriedades da exibição**, clique na guia **Relatórios** e selecione a atividade na qual deseja exibir o desempenho/converter experiências vencedoras. Os dados de desempenho são exibidos.

   ![Verificar o desempenho da atividade](/help/sites-cloud/authoring/assets/activities-performance.png)

1. Clique ou toque no link **Selecionar vencedor** para promover esta como a experiência padrão.

   A conversão do vencedor faz o seguinte:

   * Desativa a atividade atual
   * Modifica todas as páginas e substitui o conteúdo segmentado pelo conteúdo real da experiência vencedora. O conteúdo da experiência vencedora torna-se parte da página normal **sem** direcionamento.

   ![Conversão do vencedor](/help/sites-cloud/authoring/assets/activities-reports.png)

   Uma experiência vencedora é a experiência que gera mais aumento nos relatórios, com base no índice de conversão.

1. Clique ou toque **Sim** para confirmar que deseja converter o vencedor, desative a experiência atual e substitua-a pelo conteúdo da experiência vencedora.

## Sincronização de atividades com o Adobe Target {#synchronizing-activities-with-adobe-target}

As atividades que usam o mecanismo de direcionamento do Adobe Target são sincronizadas com as campanhas do Adobe Target. Uma atividade é sincronizada automaticamente ao Adobe Target quando as seguintes condições são atendidas:

* A atividade contém pelo menos uma experiência.
* Pelo menos uma experiência contém um segmento mapeado e uma oferta.
* Cada experiência na atividade deve ter o mesmo número de ofertas.

Essas condições se aplicam às atividades nas instâncias de criação e publicação.

Quando uma atividade é sincronizada, uma campanha correspondente é criada no Adobe Target:

* As atividades na instância de publicação têm o mesmo nome que a campanha do Adobe Target correspondente.
* As atividades na instância do autor correspondem às campanhas do Target com o mesmo nome, mais o sufixo `_author`.

![Sincronização com o Adobe Target](/help/sites-cloud/authoring/assets/activities-synch.png)

As atividades do autor são sincronizadas imediatamente quando a atividade é modificada. A sincronização imediata permite a simulação de atividades com o ContextHub.

As atividades de publicação são sincronizadas quando a atividade é publicada na instância de publicação do AEM.

## Solução de problemas de sincronização de atividades {#troubleshooting-activity-synchronization}

Quando o AEM sincroniza uma atividade com o Adobe Target, ele inclui uma propriedade dessa atividade denominada `thirdPartyId`. O valor dessa propriedade se baseia no caminho da atividade no repositório do AEM. Nenhuma campanha no Adobe Target pode ter o mesmo valor para a propriedade `thirdPartyId`. Portanto, uma atividade não será sincronizada se uma campanha existente (de um tipo diferente AB, XT) no Adobe Target usar o mesmo valor para `thirdPartyId`.

Essa situação pode ocorrer nas seguintes circunstâncias:

1. Uma atividade é criada e sincronizada com o Adobe Target.
1. Em outra instância do AEM, uma atividade é criada com a mesma marca e usando o mesmo nome. A sincronização desta atividade falha ao tentar.

Essa situação também pode ocorrer nas seguintes circunstâncias:

1. Uma atividade é criada e sincronizada com o Adobe Target. A atividade é excluída no AEM.
1. Uma atividade é criada com a mesma marca e usando o mesmo nome que a atividade excluída. A sincronização desta atividade falha ao tentar.

Para evitar problemas de sincronização, use sempre nomes exclusivos para atividades. Se uma atividade não for sincronizada, você poderá excluir a campanha no Adobe Target que usa o mesmo nome se essa campanha não estiver sendo usada.

>[!NOTE]
>
>Quando você cria uma campanha no Adobe Target, ele atribui uma propriedade chamada `thirdPartyId` a cada campanha. Quando você exclui a campanha no Adobe Target, a propriedade `thirdPartyId` não é excluída. Não é possível reutilizar o `thirdPartyId` para campanhas de tipos diferentes (AB, XT) e ele não pode ser removido manualmente. Para evitar esse problema, dê a cada campanha um nome exclusivo. Por isso, nomes de campanhas não podem ser reutilizados em diferentes tipos de campanha.
>
>Se você usar o mesmo nome no mesmo tipo de campanha, a campanha existente será substituída.
>
>Se, durante a sincronização, você encontrar o erro “A solicitação falhou. `thirdPartyId` já existe”, altere o nome da campanha e sincronize novamente.
