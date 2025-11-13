---
title: Restaurar conteúdo no AEM as a Cloud Service
description: Saiba como restaurar conteúdo do backup no AEM as a Cloud Service usando o Cloud Manager.
exl-id: 921d0c5d-5c29-4614-ad4b-187b96518d1f
feature: Operations
role: Admin
source-git-commit: 4008b2f81bbd81cef343c6d2b04ba536b66d7d89
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 24%

---


# Restaurar conteúdo no AEM as a Cloud Service {#content-restore}

Você pode restaurar o conteúdo do AEM as a Cloud Service a partir do backup usando o Cloud Manager.



O processo de restauração de autoatendimento do Cloud Manager copia dados de backups de sistema da Adobe e os restaura em seu ambiente original. Uma restauração é executada para retornar dados que foram perdidos, danificados ou acidentalmente excluídos à sua condição original.

O processo de restauração afeta apenas o conteúdo, deixando o código e a versão do AEM inalterados. Você pode iniciar uma operação de restauração de ambientes individuais a qualquer momento.

Se você precisar restaurar o código-fonte implantado anteriormente de maneira fácil e rápida, sem precisar iniciar uma nova execução de pipeline, poderá usar [Restaurar o Código Anterior Implantado](/help/operations/restore-previous-code-deployed.md).

O Cloud Manager fornece dois tipos de backups, a partir dos quais você pode restaurar o conteúdo.

* **Ponto no Tempo (PIT):** essa opção restaura os backups contínuos capturados nas últimas 24 horas.
* **Semana passada:** esse tipo restaura a partir de backups de sistema dos últimos sete dias, exceto as últimas 24 horas.

Em ambos os casos, a versão do código personalizado e a versão do AEM permanecem inalteradas.

>[!TIP]
>
>Também é possível restaurar backups [usando a API pública](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/).

>[!WARNING]
>
>* Esse recurso só deve ser usado quando houver problemas graves com código ou conteúdo.
>* A restauração de um backup exclui todos os dados adicionados após esse backup. O preparo também é revertido para a versão anterior.
>* Antes de iniciar uma restauração de conteúdo, considere outras opções de restauração seletiva de conteúdo.

## Opções de restauração seletiva de conteúdo {#selective-options}

Antes de restaurar para uma restauração completa do conteúdo, considere essas opções para restaurar seu conteúdo com mais facilidade.

* Se um pacote para o caminho excluído estiver disponível, instale-o novamente usando o [Gerenciador de Pacotes](/help/implementing/developing/tools/package-manager.md).
* Se o caminho excluído era uma página no Sites, use a [função Restaurar Árvore](/help/sites-cloud/authoring/sites-console/page-versions.md).
* Se o caminho excluído era uma pasta de ativos e os arquivos originais estão disponíveis, carregue-os novamente via [console do Assets](/help/assets/add-assets.md).
* Se o conteúdo excluído fosse de ativos, considere [restaurar versões anteriores dos ativos](/help/assets/manage-digital-assets.md).

Se nenhuma das opções acima funcionar e o conteúdo do caminho excluído for significativo, execute uma restauração de conteúdo, conforme detalhado nas seções a seguir.

## Criar função de usuário {#user-role}

Por padrão, nenhum usuário tem permissão para executar restaurações de conteúdo em ambientes de desenvolvimento, produção ou preparo. Para delegar essa permissão a usuários ou grupos específicos, use as seguintes etapas gerais.

1. Crie um perfil de produto com um nome expressivo que se refere à restauração do conteúdo.
1. Forneça a permissão **Acesso ao Programa** no programa necessário.
1. Forneça a permissão **Criar Restauração do Ambiente** no ambiente necessário para todos os ambientes do programa, dependendo do seu caso de uso.
1. Atribua usuários a esse perfil.

Para obter detalhes sobre o gerenciamento de permissões, consulte [Permissões personalizadas](/help/implementing/cloud-manager/custom-permissions.md).

## Restaurar o conteúdo de um ambiente {#restoring-content}

>[!NOTE]
>
>Um usuário deve ter [permissões apropriadas](#user-role) para iniciar uma operação de restauração.

**Para restaurar o conteúdo de um ambiente:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa para o qual deseja iniciar uma restauração.

1. Liste todos os ambientes do programa seguindo um destes procedimentos:

   * No menu do lado esquerdo, em **Serviços**, clique em ![Ícone de dados](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambientes**.

     ![Guia Ambientes](assets/environments-1.png)

   * No menu do lado esquerdo, em **Programa**, clique em **Visão Geral** e, no cartão **Ambientes**, clique em ![ícone de Fluxo de Trabalho](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Mostrar Tudo**.

     ![Mostrar todas as opções](assets/environments-2.png)

     >[!NOTE]
     >
     >O cartão **Ambientes** lista apenas três ambientes. Clique em **Mostrar tudo** no cartão para ver *todos* os ambientes do programa.

1. Na tabela Ambientes, à direita de um ambiente cujo conteúdo você deseja restaurar, clique em ![Mais ícone ou ícone de menu de reticências](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e em **Restaurar conteúdo**.

   ![Opção Restaurar conteúdo do menu de reticências](/help/operations/assets/environments-ellipsis-menu.png)

1. Na guia **Restaurar Conteúdo** da página suspensa do ambiente, na lista suspensa **Tempo para restaurar**, selecione o período de tempo da restauração.

   ![Guia Restaurar Conteúdo de um ambiente](/help/operations/assets/environments-content-restore-tab.png)

   * Se você escolheu **Últimas 24 horas**, no campo adjacente **Hora**, especifique a hora exata a ser restaurada dentre as últimas 24 horas.
   * Se você escolheu **Semana passada**, no campo adjacente **Dia**, selecione uma data dentre os últimos sete dias, exceto as últimas 24 horas.

1. Depois de selecionar uma data ou especificar uma hora, a seção **Backups disponíveis** abaixo mostra uma lista de backups disponíveis que podem ser restaurados

1. Clique no ![ícone de informações](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) ao lado de um backup para ver sua versão de código e a versão do AEM e pesar o impacto da restauração antes de selecionar um backup (consulte [Escolher o backup correto](#choosing-backup)).

   ![Informações de backup](assets/backup-info.png)

   O carimbo de data e hora exibido nas opções de restauração é baseado no fuso horário do computador do usuário.

1. Na extremidade direita da linha que representa o backup que você deseja restaurar, clique em ![Girar CCW em negrito ou restaurar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RotateCCWBold_18_N.svg) para iniciar o processo de restauração.

1. Revise os detalhes na caixa de diálogo **Restaurar conteúdo** e clique em **Restaurar**.

   ![Confirmar restauração](assets/backup-restore.png)

O processo de backup é iniciado. Você pode exibir seu status na lista **[Atividades de Restauração](#restore-activity)**. O tempo necessário para a conclusão de uma operação de restauração depende do tamanho e do perfil do conteúdo que está sendo restaurado.

Quando a restauração é concluída com sucesso, o ambiente faz o seguinte:

* Executa o mesmo código e versão do AEM do momento de início da operação de restauração.
* Ele tem o mesmo conteúdo que estava disponível no carimbo de data e hora do instantâneo escolhido, com os índices recriados para corresponder ao código atual.

## Escolha o backup correto {#choosing-backup}

O processo de restauração de autoatendimento do Cloud Manager restaura apenas o conteúdo no AEM. Por isso, você deve considerar cuidadosamente as alterações de código que foram feitas entre o ponto de restauração desejado e a hora atual. Revise o histórico de confirmações entre a ID de confirmação atual e a que está sendo restaurada.

Existem vários cenários.

* O código personalizado do ambiente e a restauração estão no mesmo repositório e na mesma ramificação.
* O código personalizado do ambiente e a restauração compartilham um repositório, usam uma ramificação separada e se originam de uma confirmação comum.
* O código personalizado do ambiente e a restauração estão em repositórios diferentes.
   * Nesse caso, uma ID de confirmação não é exibida.
   * A Adobe recomenda clonar ambos os repositórios e usar uma ferramenta para comparar as ramificações.

Além disso, lembre-se de que uma restauração pode fazer com que seus ambientes de produção e de preparo fiquem fora de sincronia. Você é responsável pelas consequências da restauração do conteúdo.

## Atividades de restauração {#restore-activity}

A lista **Atividade de Restauração** mostra o status das dez solicitações de restauração mais recentes, incluindo quaisquer operações de restauração ativas.

![Atividades de restauração](assets/backup-activity.png)

Ao clicar no ![ícone de Informações](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) para um backup, você pode baixar logs para esse backup e inspecionar os detalhes do código, incluindo as diferenças entre o instantâneo e os dados no momento em que a restauração foi iniciada.

## Backup externo {#offsite-backup}

Os backups normais protegem contra o risco de exclusões acidentais ou falhas técnicas nos serviços em nuvem do AEM, mas riscos adicionais podem surgir da falha de uma região. Além da disponibilidade, o maior risco durante interrupções em uma região é a perda de dados.

A AEM as a Cloud Service reduz esse risco para todos os ambientes de produção do AEM. Ou seja, ele copia continuamente todo o conteúdo do AEM para uma região remota. Esse processo disponibiliza o conteúdo para recuperação por três meses. Esse recurso é conhecido como backup externo.

O AEM Service Reliability Engineering restaura ambientes de preparo e produção do AEM Cloud Service a partir de backups externos durante paralisações da região de dados.

## Limitações           {#limitations}

O uso do mecanismo de restauração de autoatendimento está sujeito às seguintes limitações.

* As operações de restauração são limitadas a sete dias, o que significa que não é possível restaurar um instantâneo com mais de sete dias.
* No máximo dez restaurações bem-sucedidas são permitidas em todos os ambientes em um programa por mês.
* Após a criação do ambiente, pode levar até seis horas para que o primeiro instantâneo de backup seja criado. Até que esse instantâneo seja criado, nenhuma restauração poderá ser executada no ambiente.
* Uma operação de restauração não será iniciada se houver uma pilha completa ou um pipeline de configuração de camada da Web em execução no momento para o ambiente.
* Uma restauração não pode ser iniciada se outra restauração já estiver em execução no mesmo ambiente.
* Em casos raros, devido ao limite de 24 horas/sete dias para backups, o backup selecionado pode se tornar indisponível devido a um atraso entre o momento em que foi selecionado e o momento em que a restauração é iniciada.
* Os dados de ambientes excluídos são perdidos permanentemente e não podem ser recuperados.
