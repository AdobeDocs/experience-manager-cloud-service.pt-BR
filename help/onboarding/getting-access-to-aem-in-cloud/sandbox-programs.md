---
title: Programas Sandbox - Serviço em nuvem
description: Programas Sandbox - Serviço em nuvem
translation-type: tm+mt
source-git-commit: a4d4e5fb1743d7fe8b7b16bac904dac51143d6f7
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 0%

---


# Programas do Sandbox {#sandbox-programs}

## Introdução {#introduction}

Um programa Sandbox é um dos dois tipos de programas disponíveis no serviço AEM Cloud, sendo o outro um programa Regular.

Uma caixa de proteção é normalmente criada para servir aos propósitos de treinamento, execução de demonstrações, ativação ou Prova de conceito (POC). Eles não são feitos para transportar tráfego ao vivo. Eles não estão sujeitos ao [AEM como um compromisso](https://www.adobe.com/legal/service-commitments.html)de serviço na nuvem.

Os ambientes criados em uma caixa de proteção não estão configurados para dimensionamento automático. Portanto, não são adequados para testes de desempenho ou de carga.

Os programas Sandbox incluem Sites e Ativos e são preenchidos automaticamente com um repositório Git, um ambiente de desenvolvimento e um pipeline de não-produção.  O repositório Git é preenchido com um projeto de amostra baseado no tipo de arquivo do AEM Project.

Consulte [Como entender Programas e tipos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html) de Programas para saber mais sobre os tipos de Programas.

### Atributos de Programas Sandbox {#attributes-sandbox}

Os Programas Sandbox têm os seguintes atributos:

1. **Criação de Programas:** A criação do programa Sandbox inclui o recurso automático:
   * configuração de projeto com código de amostra e conteúdo
   * criação de ambientes de desenvolvimento
   * criação de pipeline de não produção implantando no ambiente de desenvolvimento (ramo mestre implantando no ambiente de desenvolvimento)

1. **Soluções:** Os programas da caixa de proteção incluem AEM Sites e Assets.

1. **Atualizações do AEM:** As atualizações do AEM podem ser aplicadas manualmente a ambientes em um programa Sandbox e não são enviadas automaticamente.

1. **Hibernação:** Ambientes em um programa Sandbox serão automaticamente hibernados se nenhuma atividade for detectada por um determinado período de tempo. ambientes hibernados podem ser removidos manualmente.

### Criação de um Programa Sandbox {#creating-sandbox-program}

O assistente de criação de programas permite criar um Programa Sandbox.

Para saber como criar um Programa Sandbox, consulte [Criar um Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-sandbox-program) Sandbox para obter mais detalhes.

### Criação de Ambientes Sandbox {#creating-sandbox-environments}

Os Programas do Sandbox são entregues a um ambiente de desenvolvimento no momento da criação do programa de uma maneira criada automaticamente. O ambiente de desenvolvimento inclui um autor e uma camada de publicação por padrão.

O conjunto de ambientes de estágio de produção pode ser adicionado manualmente ao Programa Sandbox, quando o usuário estiver pronto para configurar um pipeline de produção.

Para saber como criar manualmente um ambiente, consulte [Adicionar Ambientes](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments) para obter mais detalhes.

### Excluindo Ambientes do Sandbox {#deleting-sandbox-environments}

O usuário com as permissões necessárias pode excluir um ou mais conjuntos de ambientes de desenvolvimento ou de produção/estágio.

Para excluir um ambiente, consulte [Excluir Ambientes](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment) para obter mais detalhes.


## Hibernando e removendo Ambientes do Sandbox {#hibernating-introduction}

ambientes de Programa da caixa de proteção entram em um modo *de* hibernação se nenhuma atividade for detectada por um determinado período de tempo.

>[!NOTE]
>A hibernação é exclusiva aos ambientes de Programa Sandbox. ambientes comuns não hibernam.

### Hibernação {#hibernation-introduction}

A hibernação pode ocorrer automática ou manualmente. Pode levar alguns minutos para que ambientes de Programa Sandbox entrem no modo *de* hibernação. Os dados são preservados durante a hibernação.

A hibernação é classificada como:

* **ambientes automáticos** de Programa Sandbox são hibernados automaticamente após oito horas de inatividade, o que significa que nem o autor nem os serviços de publicação recebem solicitações.

* **Manual**: Como usuário, você pode hibernar manualmente um ambiente do Programa do Sandbox, embora não haja nenhum requisito para fazer isso, uma vez que a hibernação ocorrerá automaticamente após um determinado período (oito horas) de inatividade.

>[!CAUTION]
>Na versão mais recente, vincular ao Developer Console diretamente do Cloud Manager não lhe dará a opção de hibernar um ambiente de Programa Sandbox. A solução alternativa é uma vez no Developer Console, adicione o seguinte padrão ao final do url `#release-cm-p1234-e5678 where 1234` 1234 como sua ID *do* Programa e 5678 como sua ID *do* Ambiente.

#### Uso da hibernação manual {#using-manual-hibernation}

Você pode hibernar manualmente seu Programa do Sandbox no Developer Console de duas maneiras diferentes, usando:

* Tela de detalhes do Ambiente
* Tela de listagem do Ambiente

>[!NOTE]
>O acesso ao Developer Console para um Programa do Sandbox está disponível para qualquer usuário do Cloud Manager.

Siga as etapas abaixo para hibernar manualmente os ambientes do Programa Sandbox:

1. Navegue até o **Developer Console**.
Consulte [Acessar o Developer Console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) para saber como acessar o **Developer Console** a partir da placa de **Ambientes** .
   >[!IMPORTANT]
   >Vincular ao Console **do** desenvolvedor diretamente do Gerenciador de nuvem não lhe dará a opção de hibernar um ambiente de Programa do Sandbox. A solução alternativa é uma vez no Developer Console, adicione o seguinte padrão ao final do url `#release-cm-p1234-e5678 where 1234` 1234 como sua ID *do* Programa e 5678 como sua ID *do* Ambiente.

1. Click **Hibernate**, as shown in the figure below:

   ![](assets/hibernate-1.png)

   Ou,

   Clique no link **Ambientes** na parte superior esquerda para visualização na lista ambientes e clique em **Hibernar**, como mostrado na figura abaixo:

   ![](assets/hibernate-1b.png)

1. Clique em **Hibernar** para confirmar a etapa.

   ![](assets/hibernate-2.png)

1. Quando a hibernação for bem-sucedida, você verá a notificação de conclusão do processo de hibernação do seu ambiente na tela do Console **do** desenvolvedor.

   ![](assets/hibernate-4.png)


### Deshibernação {#de-hibernation-introduction}

1. Navegue até o **Developer Console**.
Consulte [Acessar o Developer Console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) para saber como acessar o **Developer Console** a partir da placa de **Ambientes** .

   >[!IMPORTANT]
   >Vincular ao Console **do** desenvolvedor diretamente do Gerenciador de nuvem não lhe dará a opção de cancelar a hibernação de um ambiente de Programa do Sandbox. A solução alternativa é uma vez no Developer Console, adicione o seguinte padrão ao final do url `#release-cm-p1234-e5678 where 1234` 1234 como sua ID *do* Programa e 5678 como sua ID *do* Ambiente.

   >[!NOTE]
   >Como alternativa, você pode navegar até o **Developer Console** para cancelar a hibernação tentando acessar o serviço de autor ou publicação de um ambiente já hibernado; nesse caso, uma landing page será exibida com um link para o Developer Console. Consulte a seção Acessar um Ambiente hibernado abaixo.

   >[!IMPORTANT]
   >O acesso ao Console do desenvolvedor é definido pelo Gerenciador da **nuvem - Função** do desenvolvedor no Console **de** administração. Um usuário com uma permissão de função de desenvolvedor pode cancelar a hibernação de um ambiente do Programa Sandbox.

1. Clique em **Cancelar hibernação**, como mostrado na figura abaixo:

   ![](assets/de-hibernation-img1.png)

   Ou,

   Clique no link **Ambientes** na parte superior esquerda para visualização na lista ambientes e clique em **Deshibernar**, como mostrado na figura abaixo

   ![](assets/de-hibernate-1b.png)


1. Clique em **Deshibernar** para confirmar a etapa.

   ![](assets/de-hibernation-img2.png)

1. Você receberá a notificação de que o processo de hibernação foi iniciado e será atualizado com o andamento.

   ![](assets/de-hibernation-img3.png)

1. Quando o processo for concluído, o ambiente do Programa Sandbox estará ativo novamente.

   ![](assets/de-hibernation-img4.png)

#### Permissões para hibernar {#permissions-de-hibernate}

Qualquer usuário com um perfil de produto que dê acesso ao AEM como um serviço em nuvem deve poder acessar o **Developer Console**, permitindo que ele hiberne o ambiente.

Consulte [Adicionar usuários e funções](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html) no Cloud Manager sobre como configurar permissões de usuário.

#### Acessar um Ambiente Hibernado {#accessing-hibernated-environment}

Ao fazer solicitações de navegador contra o autor ou a camada de publicação de um ambiente hibernado, o usuário encontrará uma landing page descrevendo o status hibernado do ambiente, como mostrado na figura abaixo:

![](assets/de-hibernation-img5.png)

### Considerações importantes {#important-considerations}

Poucas considerações importantes relacionadas aos ambientes hibernados e com hibernação são:

* Um usuário pode usar um pipeline para implantar código personalizado em ambientes hibernados. O ambiente permanecerá hibernado e o novo código aparecerá no ambiente depois de ser deshibernado.

* As atualizações do AEM podem ser aplicadas a ambientes hibernados, que os clientes podem acionar manualmente a partir do Cloud Manager. O ambiente permanecerá hibernado e a nova versão aparecerá no ambiente depois de ser deshibernada.

>[!NOTE]
>Atualmente, o Cloud Manager não indica se um ambiente está hibernado.

## Atualizações do AEM para Ambientes do Sandbox {#aem-updates-sandbox}

Consulte as atualizações [de versão do](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates) AEM para obter mais detalhes.

Um usuário pode aplicar manualmente as atualizações do AEM aos ambientes em um Programa Sandbox.

Consulte [Atualização do Ambiente](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#updating-dev-environment) para saber como atualizar um ambiente.

>[!NOTE]
>* Uma atualização manual só pode ser executada quando o ambiente de destino tiver um pipeline configurado corretamente.
>* Uma atualização manual do *Production* ou do *Stage* ambiente atualizará automaticamente o outro. O conjunto de ambientes Production+Stage deve estar na mesma versão do AEM.






