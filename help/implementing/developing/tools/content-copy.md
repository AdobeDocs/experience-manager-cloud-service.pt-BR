---
title: A ferramenta de cópia de conteúdo
description: A ferramenta de cópia de conteúdo permite que os usuários copiem conteúdo mutável sob demanda de seus ambientes de produção no AEM as a Cloud Service para ambientes inferiores para fins de teste.
exl-id: f060821d-d559-45d2-b3b1-1b2277694ec4
source-git-commit: f08048b2378b150210a3fd1168206f4efb0c4f8e
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 41%

---

# A ferramenta de cópia de conteúdo {#content-copy}

A ferramenta de cópia de conteúdo permite que os usuários copiem conteúdo mutável sob demanda de seus ambientes de produção no AEM as a Cloud Service para ambientes inferiores para fins de teste.

## Introdução {#introduction}

Os dados atuais e reais são valiosos para fins de teste, validação e aceitação do usuário. A ferramenta de cópia de conteúdo permite copiar o conteúdo de um ambiente de produção AEM as a Cloud Service para um ambiente de preparo, desenvolvimento ou [RDE (Rapid Development Environment, ambiente de desenvolvimento rápido)](/help/implementing/developing/introduction/rapid-development-environments.md) ambiente para esses testes.

O conteúdo a ser copiado é definido por um conjunto de conteúdo. Um conjunto de conteúdo consiste em uma lista de caminhos JCR que contêm o conteúdo mutável a ser copiado de um ambiente de serviço de autoria de origem para um ambiente de serviço de autoria de destino no mesmo programa do Cloud Manager. Os seguintes caminhos são permitidos em um conjunto de conteúdo.

```text
/content
/conf/**/settings/wcm
/conf/**/settings/dam/cfm/models
/conf/**/settings/graphql/persistentQueries
/etc/clientlibs/fd/themes
```

Ao copiar o conteúdo, o ambiente de origem é a fonte de verdade.

* Se o conteúdo tiver sido modificado no ambiente de destino, ele será substituído pelo conteúdo na origem, se os caminhos forem os mesmos.
* Se os caminhos forem diferentes, o conteúdo da origem será mesclado com o conteúdo no destino.

## Permissões {#permissions}

Para usar a ferramenta de cópia de conteúdo, determinadas permissões são necessárias nos ambientes de origem e de destino.

| Recurso de cópia de conteúdo | Grupo de administradores AEM | Função de gerente de implantação |
|---|---|---|
| Criar e modificar [conjuntos de conteúdo](#create-content-set) | Obrigatório | Não obrigatório |
| Iniciar ou cancelar o [processo de cópia de conteúdo](#copy-content) | Obrigatório | Obrigatório |

## Criação de um conjunto de conteúdo {#create-content-set}

Antes que qualquer conteúdo possa ser copiado, um conjunto de conteúdo deve ser definido. Depois de definido, os conjuntos de conteúdo podem ser reutilizados para copiar conteúdo. Siga estas etapas para criar um conjunto de conteúdo.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Acesse a página **Conjuntos de conteúdo** na tela **Ambientes**.

1. Na parte superior direita da tela, clique em **Adicionar conjunto de conteúdo**.

   ![Conjuntos de conteúdo](assets/content-sets.png)

1. Na guia **Detalhes** do assistente, forneça um nome e uma descrição para o conjunto de conteúdo e toque ou clique em **Continuar**.

   ![Detalhes do conjunto de conteúdo](assets/add-content-set-details.png)

1. Na guia **Caminhos de conteúdo** do assistente, especifique os caminhos do conteúdo mutável a ser incluído no conjunto de conteúdo.

   1. Insira o caminho no campo **Adicionar caminho de inclusão**.
   1. Clique em **Adicionar caminho** para adicionar o caminho ao conjunto de conteúdo.
   1. Clique em **Adicionar caminho** novamente, conforme necessário.
      * São permitidos até 50 caminhos.

   ![Adicionar caminhos ao conjunto de conteúdo](assets/add-content-set-paths.png)

1. Se você precisar refinar ou restringir seu conjunto de conteúdo, os subcaminhos poderão ser excluídos.

   1. Na lista de caminhos incluídos, clique em **Adicionar subcaminhos de exclusão** ao lado do caminho que deseja restringir.
   1. Insira o subcaminho a ser excluído abaixo do caminho selecionado.
   1. Toque ou clique em **Excluir caminho**.
   1. Toque ou clique em **Adicionar subcaminhos de exclusão** novamente para adicionar caminhos adicionais a serem excluídos, se necessário.
      * Os caminhos excluídos devem ser relativos ao caminho incluído.
      * Não há limite para o número de caminhos excluídos.

   ![Excluir caminhos](assets/add-content-set-paths-excluded.png)

1. É possível editar os caminhos especificados, se necessário.

   1. Clique no X ao lado dos subcaminhos excluídos para excluí-los.
   1. Clique no botão de reticências ao lado dos caminhos para que você possa revelar **Editar** e **Excluir** opções.

   ![Editar lista de caminhos](assets/add-content-set-excluded-paths.png)

1. Toque ou clique em **Criar** para criar o conjunto de conteúdo.

O conjunto de conteúdo agora pode ser usado para copiar conteúdo entre ambientes.

## Editar um conjunto de conteúdo {#edit-content-set}

Para esse processo, as etapas são semelhantes às da criação de conteúdo. Em vez de clicar em **Adicionar conjunto de conteúdo**, selecione um conjunto existente no console e selecione **Editar** no menu reticências.

![Editar conjunto de conteúdo](assets/edit-content-set.png)

Ao editar o conjunto de conteúdo, você pode expandir os caminhos configurados para revelar os subcaminhos excluídos.

## Copiar conteúdo {#copy-content}

Após criar um conjunto de conteúdo, você pode usá-lo para copiar o conteúdo. Siga estas etapas para poder copiar o conteúdo.

>[!NOTE]
> Não use a Cópia de conteúdo em um ambiente enquanto [transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md) a operação está em execução nesse ambiente.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Acesse a página **Conjuntos de conteúdo** na tela **Ambientes**.

1. Selecione um conjunto de conteúdo no console e clique em **Copiar conteúdo** no menu de reticências.

   ![Cópia de conteúdo](assets/copy-content.png)

   >[!NOTE]
   >
   >Um ambiente pode não ser selecionável se:
   >
   >* O usuário não tiver as permissões apropriadas.
   >* O ambiente tiver um pipeline em execução ou uma operação de cópia de conteúdo em andamento.
   >* O ambiente está hibernando ou sendo inicializado.

1. Na caixa de diálogo **Copiar conteúdo**, especifique a origem e o destino da sua ação de cópia de conteúdo.

   ![Copiar conteúdo](assets/copying-content.png)

   * O conteúdo só pode ser copiado de um ambiente superior para um ambiente inferior ou entre ambientes de desenvolvimento/RDE, em que a hierarquia de ambientes é a seguinte (do mais alto para o mais baixo):
      * Produção
      * Estágios
      * Desenvolvimento / RDE

1. Se necessário, também é possível optar por **Incluir listas de controle de acesso** no processo de cópia.

1. Toque ou clique em **Copiar**.

O processo de cópia será iniciado. O status do processo de cópia é exibido no console do conjunto de conteúdo selecionado.

## Atividade de cópia de conteúdo {#copy-activity}

Você pode monitorar o status dos processos de cópia na página **Atividade de cópia de conteúdo**.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Acesse a página **Atividade de cópia de conteúdo** na tela **Ambientes**.

![Atividade de cópia de conteúdo](assets/copy-content-activity.png)

### Status da cópia de conteúdo {#statuses}

Depois de começar a copiar o conteúdo, o processo poderá ter um dos status a seguir.

| Status | Descrição |
|---|---|
| Em andamento | A operação de cópia de conteúdo está em andamento |
| Falhou | A operação de cópia de conteúdo falhou |
| Concluído | A operação de cópia de conteúdo foi concluída com sucesso |
| Cancelado | O usuário cancela uma operação de cópia de conteúdo após iniciá-la |

### Cancelando um Processo de Cópia {#canceling}

Se você precisar abortar uma operação de cópia de conteúdo após iniciá-la, é possível cancelá-la opcionalmente.

Para isso, no **Atividade de cópia de conteúdo** selecione a **Cancelar** ação do menu de reticências do processo de cópia iniciado anteriormente.

![Cancelar cópia de conteúdo](assets/content-copy-cancel.png)

>[!NOTE]
>
>Ao cancelar uma operação de cópia de conteúdo, pode resultar em uma cópia parcial do conteúdo no ambiente de destino. Essa situação pode deixar o ambiente de destino em um estado inutilizável.
>
>Se o ambiente estiver em tal estado devido ao cancelamento, entre em contato com o Atendimento ao cliente da Adobe para obter assistência.

## Limitações {#limitations}

A ferramenta de cópia de conteúdo tem as seguintes limitações.

* O conteúdo não pode ser copiado de um ambiente inferior para um ambiente superior.
* O conteúdo só pode ser copiado de e para os serviços de autoria.
* Não é possível copiar conteúdo entre programas.
* Não é possível executar operações de cópia de conteúdo simultâneas no mesmo ambiente.
* Até 50 caminhos podem ser especificados por conjunto de conteúdo. Não há limitação de caminhos excluídos.
* A ferramenta de cópia de conteúdo não deve ser usada como uma ferramenta de clonagem ou de espelhamento porque não pode rastrear conteúdo movido ou excluído na origem.
* A ferramenta de cópia de conteúdo não tem recurso de controle de versão e não pode detectar automaticamente o conteúdo modificado ou o conteúdo recém-criado no ambiente de origem em um conjunto de conteúdo desde a última operação de cópia de conteúdo.
   * Se quiser atualizar o ambiente de destino somente com alterações de conteúdo, você deverá criar um conjunto de conteúdo desde a última operação de cópia de conteúdo. Em seguida, especifique os caminhos na instância de origem em que as alterações foram feitas desde a última operação de cópia de conteúdo.
* As informações da versão não são incluídas em uma cópia de conteúdo.
