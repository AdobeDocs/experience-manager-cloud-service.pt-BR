---
title: 'Hibernar e desibernar ambientes de sandbox '
description: 'Hibernar e desibernar ambientes de sandbox '
translation-type: tm+mt
source-git-commit: 213a7237abd4de75be43af430181f4aa914196f4
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---


# Hibernando e removendo ambientes de sandbox {#hibernating-introduction}

Os ambientes do Programa de sandbox inserem um *modo de hibernação* se nenhuma atividade for detectada por um determinado período de tempo.

>[!NOTE]
>A hibernação é exclusiva aos ambientes do Programa de sandbox. Ambientes regulares de programas não hibernam.

## Hibernação {#hibernation-introduction}

A hibernação pode ocorrer automática ou manualmente. Pode levar alguns minutos para que os ambientes do Programa de sandbox entrem em um *modo de hibernação*. Os dados são preservados durante a hibernação.

A hibernação é classificada como:

* ****  Os ambientes do Automatic Sandbox Program hibernam automaticamente após oito horas de inatividade, o que significa que nem os serviços de criação nem de publicação recebem solicitações.

* **Manual**: Como usuário, você pode hibernar manualmente um ambiente do Programa de sandbox, embora não haja necessidade de fazer isso, pois a hibernação ocorrerá automaticamente após um determinado período (oito horas) de inatividade.

>[!CAUTION]
>Na versão mais recente, vincular ao Console do desenvolvedor diretamente do Cloud Manager não oferecerá a opção de hibernar um ambiente do Programa de sandbox. A solução alternativa é uma vez no Console do desenvolvedor, adicione o seguinte padrão ao final do URL `#release-cm-p1234-e5678 where 1234` 1234 é seu *ID do programa* e 5678 é seu *ID do ambiente*.

### Usando a hibernação manual {#using-manual-hibernation}

Você pode hibernar manualmente seu Programa de sandbox no Console do desenvolvedor de duas maneiras diferentes, usando:

* Tela de detalhes do ambiente
* Tela de listagem do ambiente

>[!NOTE]
>O acesso ao Console do desenvolvedor para obter um Programa de sandbox está disponível para qualquer usuário do Cloud Manager.

Siga as etapas abaixo para hibernar manualmente os ambientes do Programa de sandbox:

1. Navegue até **Console do Desenvolvedor**.
Consulte [Acessando o Console do Desenvolvedor](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) para saber como acessar o **Console do Desenvolvedor** no cartão **Ambientes**.
   >[!IMPORTANT]
   >Vincular ao **Console do desenvolvedor** diretamente do Cloud Manager não oferecerá a opção de hibernar um ambiente de Programa de sandbox. A solução alternativa é uma vez no Console do desenvolvedor, adicione o seguinte padrão ao final do URL `#release-cm-p1234-e5678 where 1234` 1234 é seu *ID do programa* e 5678 é seu *ID do ambiente*.

1. Clique em **Hibernar**, conforme mostrado na figura abaixo:

   ![](assets/hibernate-1.png)

   Ou,

   Clique no link **Ambientes** no canto superior esquerdo para exibir a lista de ambientes e, em seguida, clique em **Hibernar**, conforme mostrado na figura abaixo:

   ![](assets/hibernate-1b.png)

1. Clique em **Hibernar** para confirmar a etapa.

   ![](assets/hibernate-2.png)

1. Quando a hibernação for bem-sucedida, você verá a notificação de conclusão do processo de hibernação para seu ambiente na tela **Console do desenvolvedor**.

   ![](assets/hibernate-4.png)


## Eliminação de hibernação {#de-hibernation-introduction}

1. Navegue até **Console do Desenvolvedor**.
Consulte [Acessando o Console do Desenvolvedor](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) para saber como acessar o **Console do Desenvolvedor** no cartão **Ambientes**.

   >[!IMPORTANT]
   >Vincular ao **Console do desenvolvedor** diretamente do Cloud Manager não oferecerá a opção de desibernar um ambiente do Programa de sandbox. A solução alternativa é uma vez no Console do desenvolvedor, adicione o seguinte padrão ao final do URL `#release-cm-p1234-e5678 where 1234` 1234 é seu *ID do programa* e 5678 é seu *ID do ambiente*.

   >[!NOTE]
   >Como alternativa, você pode navegar até o **Console do Desenvolvedor** para desibernar, tentando acessar o serviço de criação ou publicação de um ambiente já hibernado; nesse caso, uma landing page será exibida com um link para o Console do desenvolvedor. Consulte a seção Acesso a um ambiente hibernado abaixo.

   >[!IMPORTANT]
   >O acesso ao Console do desenvolvedor é definido pelo **Cloud Manager - Developer Role** no **Admin Console**. Um usuário com uma permissão de função de desenvolvedor pode desibernar um ambiente do Programa de sandbox.

1. Clique em **Cancelar hibernação**, conforme mostrado na figura abaixo:

   ![](assets/de-hibernation-img1.png)

   Ou,

   Clique no link **Ambientes** no canto superior esquerdo para exibir a listagem de ambientes e, em seguida, clique em **Cancelar hibernação**, conforme mostrado na figura abaixo

   ![](assets/de-hibernate-1b.png)


1. Clique em **De Hibernate** para confirmar a etapa.

   ![](assets/de-hibernation-img2.png)

1. Você receberá a notificação de que o processo de deshibernação foi iniciado e será atualizado com o progresso.

   ![](assets/de-hibernation-img3.png)

1. Quando o processo for concluído, o ambiente do Programa de sandbox estará ativo novamente.

   ![](assets/de-hibernation-img4.png)

### Permissões para Cancelar hibernação {#permissions-de-hibernate}

Qualquer usuário com um perfil de produto que dê acesso ao AEM como um Cloud Service deve poder acessar o **Console do desenvolvedor**, permitindo que ele remova a hibernação do ambiente.

## Acessar um ambiente hibernado {#accessing-hibernated-environment}

Ao fazer qualquer solicitação do navegador em relação ao nível de criação ou publicação de um ambiente hibernado, o usuário encontrará uma página de aterrissagem descrevendo o status de hibernação do ambiente, conforme mostrado na figura abaixo:

![](assets/de-hibernation-img5.png)

## Considerações importantes {#important-considerations}

São poucas as considerações principais relacionadas a ambientes hibernados e de hibernação:

* Um usuário pode usar um pipeline para implantar código personalizado em ambientes hibernados. O ambiente permanecerá hibernado e o novo código aparecerá no ambiente após a hibernação.

* As atualizações de AEM podem ser aplicadas a ambientes hibernados, que os clientes podem acionar manualmente no Cloud Manager. O ambiente permanecerá hibernado e a nova versão aparecerá no ambiente após a hibernação.

>[!NOTE]
>No momento, o Cloud Manager não indica se um ambiente está hibernado.

## AEM atualizações para ambientes de sandbox {#aem-updates-sandbox}

Consulte [AEM atualizações de versão](/help/implementing/deploying/aem-version-updates.md) para obter mais detalhes.

Um usuário pode aplicar manualmente AEM atualizações aos ambientes em um Programa de sandbox.

Consulte [Atualização do ambiente](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) para saber como atualizar um ambiente.

>[!NOTE]
>* Uma atualização manual só pode ser executada quando o ambiente de destino tiver um pipeline configurado corretamente.
>* Uma atualização manual para o ambiente *Production* ou *Stage* atualizará automaticamente o outro. O conjunto de ambientes Production+Stage deve estar na mesma versão de AEM.






