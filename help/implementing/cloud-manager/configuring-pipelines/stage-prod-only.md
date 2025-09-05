---
title: Pipelines somente de preparo e somente de produção
description: Saiba como dividir implantações de preparo e produção usando pipelines dedicados.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#staging-production-only-pipelines"
hide: true
hidefromtoc: true
index: false
source-git-commit: 24d78f19932a30026c0357db646124c9dd1fa759
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 49%

---

# Dividir pipelines somente de estágio e somente de produção {#stage-prod-only}

Você pode dividir implantações de preparo e produção usando pipelines dedicados.

## Visão geral {#overview}

Os ambientes de preparo e produção são totalmente combinados. Por padrão, as implantações para eles estão vinculadas a um único pipeline. Ou seja, um pipeline de implantação é iniciado nos ambientes de preparo e produção desse programa. Embora esse acoplamento seja normalmente adequado, há certos casos de uso em que há desvantagens:

* Se quiser implantar somente em preparo, rejeite a etapa **Promover para produção** no pipeline. No entanto, a execução será marcada como cancelada.
* Se você quiser implantar o código mais recente em um ambiente de preparo para produção, será necessário reimplantar todo o pipeline, incluindo a implantação de preparo, mesmo que nenhum código tenha sido alterado lá.
* Os ambientes não podem ser atualizados durante as implantações. Se você pausar para testar o ambiente de preparo por vários dias antes de promover para a produção, o ambiente de produção permanecerá bloqueado e não poderá ser atualizado. Isso torna impossíveis tarefas não dependentes, como a atualização de [variáveis de ambiente](/help/implementing/cloud-manager/environment-variables.md).

Os pipelines somente de preparo e somente de produção oferecem soluções para esses casos de uso fornecendo opções de implantação dedicadas.

* **Pipelines de implantação somente de preparo:** implantam somente em um ambiente de preparo e a execução termina quando a implantação e os testes são concluídos. Um pipeline somente de preparo se comporta de forma idêntica ao pipeline de produção de pilha completa acoplado padrão, mas sem as etapas de implantação de produção (aprovação, agendamento, implantação).
* **Pipelines de Implantação Somente de Produção:** Implanta apenas para produção selecionando a execução de estágio bem-sucedida mais recente. Em seguida, implante seus artefatos na produção. Os pipelines somente de produção reutilizam artefatos da implantação de preparo, ignorando a fase de compilação.

Os pipelines somente de preparo e somente de produção não são executados enquanto um pipeline de produção de pilha completa está em andamento e vice-versa. Se o pipeline somente de preparo e o pipeline de produção de pilha completa tiverem o acionador **Sobre alterações do Git** configurado e estiverem apontando para a mesma ramificação e repositório, apenas o pipeline somente de preparo será iniciado automaticamente. Os pipelines somente de produção não iniciam **`On Git Changes`** porque não estão diretamente vinculados a um repositório.

Os pipelines somente de produção são acionados manualmente, pois não estão vinculados diretamente a um repositório para **Sobre alterações do Git**.

Esses pipelines dedicados oferecem mais flexibilidade, mas observe os seguintes detalhes de operação e recomendações.

>[!NOTE]
>
>Os pipelines somente de produção sempre usam artefatos do pipeline somente de preparo. Isso é verdade mesmo se o pipeline de produção acoplado padrão tiver implantado algo diferente para ser preparado enquanto isso.
>
>* Esse cenário pode levar a reversões de código indesejadas.
>* A Adobe recomenda parar de usar o pipeline de produção acoplada padrão assim que você começar a usar os pipelines somente de produção e somente de preparo.
>* Se você ainda decidir executar os pipelines acoplados padrão junto com os pipelines somente de preparo/produção, lembre-se da reutilização de artefatos para evitar reversões de código.

## Criação de pipeline {#pipeline-creation}

Os pipelines somente de produção e somente de preparo são criados de maneira semelhante aos [pipelines de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e [pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) acoplados padrão. Consulte esses documentos para obter detalhes.

1. Na janela **Pipelines**, clique em **Adicionar pipeline**.

   * Selecione **Adicionar pipeline de não produção** para [criar um pipeline somente de preparo](#stage-only).
   * Selecione **Adicionar pipeline de produção somente** para [criar um pipeline de produção somente](#prod-only).

![Criação de um pipeline somente de produção/preparo](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-stage-pipeline.png)

>[!NOTE]
>
>Determinadas opções podem estar esmaecidas se os pipelines correspondentes já existirem.
>
>* A opção **Adicionar pipeline somente de produção** não estará disponível se não existir um pipeline somente de preparo.
>* A opção **Adicionar pipeline de produção** não está disponível se já existir um pipeline acoplado padrão.
>* São permitidos apenas um pipeline somente de produção e um pipeline somente de preparo por programa.

### Criar um pipeline somente de preparo {#stage-only}

1. Na caixa de diálogo **Adicionar pipeline de não produção**, na guia **Configuração**, selecione o campo **Pipeline de implantação** para seu pipeline.
1. No campo Nome do pipeline de não produção, insira um nome de texto livre.
1. Selecione as opções de implantação desejadas e clique em **Continuar**.

   ![Guia Configuração na caixa de diálogo Adicionar pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-1.png)

1. Na guia **Source Code**, selecione **Full Stack Code**. Essa opção cria e implanta todo o aplicativo do AEM (back-end, configuração no nível da Dispatcher/Web e quaisquer módulos de front-end no repositório).

1. Na lista suspensa **Ambientes de implantação qualificados**, selecione o ambiente **estágio** como o ambiente de implantação para seu pipeline. Selecionar estágio cria um pipeline dedicado ao ambiente de estágio (a promoção da produção acontece por meio de um pipeline separado).

1. Selecione o **Repositório** e a **Ramificação Git** nas respectivas listas suspensas e clique em **Continuar**.

   ![Guia Código Source na caixa de diálogo Adicionar pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-2.png)

1. Na guia **Auditoria de Experiência**, a URL do Site especificada é a URL de publicação que a Cloud Manager audita quanto à qualidade da página.

1. No campo **Caminho da página**, especifique quais páginas deseja auditar e clique em **![Ícone Adicionar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) Adicionar página**.

   A Auditoria de experiência analisa cada caminho adicionado em termos de desempenho, acessibilidade, aplicativos web progressivos, práticas recomendadas, SEO e outras verificações de qualidade. Você pode adicionar vários caminhos e remover qualquer um clicando em ![ícone de tamanho cruzado 400](https://spectrum.adobe.com/static/icons/ui_18/CrossSize400.svg).

   ![Guia Auditoria de Experiência na caixa de diálogo Adicionar Pipeline de Não Produção](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-3.png)

1. Clique em **Salvar**.


### Criar um pipeline somente de produção {#prod-only}

1. Na caixa de diálogo **Adicionar Pipeline Somente de Produção**, no campo de texto **Nome do Pipeline**, digite o nome de texto livre do pipeline.
1. No campo **Nome do pipeline**, digite o nome desejado.
1. Em **Opções de Implantação de Produção**, selecione **Pausar antes de implantar em Produção**.

   Essa opção insere um portão de aprovação manual logo antes da etapa de produção. O pipeline é interrompido e aguarda um aprovador (como um Gerente de implantação ou um Proprietário da empresa) aprovar ou cancelar a implantação de produção.

   Use isso para controle de alterações ou verificações de última hora.

1. Clique em **Salvar** para criar o pipeline somente de produção com essas opções.

   ![Criação de um pipeline somente de produção](/help/implementing/cloud-manager/configuring-pipelines/assets/add-production-only-pipeline.png)

## Executar pipelines somente de preparo e somente de produção {#running}

Você pode iniciar os novos pipelines [como qualquer outro pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines). Você também pode acionar um pipeline somente de produção diretamente dos detalhes de execução de um pipeline somente de preparo.

<!-- * Stage-only and prod-only pipelines offer a new [emergency mode](#emergency-mode) to skip testing.
Prod-only pipeline run can be triggered directly from the execution details of a [stage-only pipeline](#stage-only-run).


### Emergency Mode {#emergency-mode}

When starting production-only and staging-online pipelines, you are prompted to confirm the start and how it starts.

* **Normal Mode** is a standard run and includes stage testing steps.
* **Emergency Mode** skips stage testing steps.

![Emergency Mode](/help/assets/configure-pipelines/emergency-mode.png) -->

### Executar pipelines somente de estágio {#stage-only-run}

Nos detalhes da execução, um botão **Promover compilação** aparece após as etapas de teste. Clique nele para acionar um pipeline somente de produção que implante os artefatos do estágio desta execução na produção. O botão é exibido somente na última execução bem-sucedida somente de estágio.

![Execução de pipeline somente de preparo](/help/implementing/cloud-manager/configuring-pipelines/assets/stage-only-pipelines-run.png)

Ao clicar em **Promover build**, se existir um pipeline somente de preparo, uma caixa de diálogo de confirmação será aberta para iniciá-lo. Clique em **Executar**.

![Promover Compilação - Caixa de diálogo Executar Pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-run.png)

Se não houver nenhum, uma caixa de diálogo de configuração solicitará que você crie uma.

![Promover compilação - Nenhuma caixa de diálogo de pipeline válida](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-no-valid-pipeline.png)


### Executar pipelines somente de produção {#prod-only-run}

Para um pipeline **somente de produção**, o Cloud Manager exibe os artefatos de origem que são implantados na produção. Verifique a etapa **Preparação de Artefato** para a execução da origem e abra-a para exibir detalhes e logs.


![Detalhes do artefato](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-only-pipelines-run.png)

