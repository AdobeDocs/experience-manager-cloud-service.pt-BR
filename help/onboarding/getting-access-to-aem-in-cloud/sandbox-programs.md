---
title: Programas Sandbox - Serviço em nuvem
description: Programas Sandbox - Serviço em nuvem
translation-type: tm+mt
source-git-commit: e7cad0cd67f04eac5627e72339ccb1c4f54cc8c8
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---


# Programas Sandbox {#sandbox-programs}

## Introdução {#introduction}

Um programa Sandbox é um dos dois tipos de programas disponíveis no serviço AEM Cloud, sendo o outro um programa Regular.

Uma caixa de proteção é normalmente criada para servir aos propósitos de treinamento, execução de demonstrações, ativação ou Prova de conceito (POC). Eles não são feitos para transportar tráfego ao vivo.

Os programas Sandbox incluem Sites e Ativos e são preenchidos automaticamente com uma ramificação Git que inclui código de amostra, um ambiente de desenvolvimento e um pipeline de não-produção.

Para obter mais informações sobre tipos de programas, consulte [Entendendo Programas e tipos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html)de Programas.

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

Para saber como criar um Programa Sandbox, consulte [Criar um Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program)Sandbox.

### Criação de Ambientes Sandbox {#creating-sandbox-environments}

Os Programas do Sandbox são entregues a um ambiente de desenvolvimento no momento da criação do programa de uma maneira criada automaticamente. O ambiente de desenvolvimento inclui um autor e uma camada de publicação por padrão.

O conjunto de ambientes de estágio de produção pode ser adicionado manualmente ao Programa Sandbox, quando o usuário estiver pronto para configurar um pipeline de produção.

Para saber como criar manualmente um ambiente, consulte [Adicionar Ambientes](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments) para obter mais detalhes.

### Excluindo Ambientes do Sandbox  {#deleting-sandbox-environments}

O usuário com as permissões necessárias pode excluir um ou mais conjuntos de ambientes de desenvolvimento ou de produção/estágio.

Para excluir um ambiente, consulte [Excluir Ambientes](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment) para obter mais detalhes.


## Hibernando e removendo Ambientes do Sandbox {#hibernating-introduction}

ambientes de Programa da caixa de proteção entram em um modo *de* hibernação se nenhuma atividade for detectada por um determinado período de tempo.

>[!NOTE]
>A hibernação é exclusiva aos ambientes de Programa Sandbox. ambientes comuns não hibernam.

### Hibernação {#hibernation-introduction}

A hibernação pode ocorrer automática ou manualmente. Pode levar alguns minutos para que ambientes de Programa Sandbox entrem no modo *de* hibernação. Os dados são preservados durante a hibernação.

A hibernação é classificada como:

* **Os ambientes de Programa da caixa de proteção automática** são hibernados automaticamente após oito horas de inatividade, o que significa que nem o autor nem os serviços de publicação recebem solicitação.

* **Manual**: Como usuário, você pode hibernar manualmente um ambiente do Programa do Sandbox, embora não haja nenhum requisito para fazer isso, uma vez que a hibernação ocorrerá automaticamente após determinado período (oito horas) de inatividade.

#### Uso da hibernação manual {#using-manual-hibernation}

Você pode hibernar manualmente seu Programa do Sandbox no Developer Console de duas maneiras diferentes, usando:

* Tela de detalhes do Ambiente
* Tela de listagem do Ambiente

Siga as etapas abaixo para hibernar manualmente os ambientes do Programa Sandbox:

1. Navegue até o **Developer Console**.
Consulte [Acessar o Developer Console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) para saber como acessar o **Developer Console** a partir da placa de **Ambientes** .
1. Clique em Hibernar, conforme mostrado na figura abaixo:
1. Clique em **Hibernar** para confirmar a etapa
1. Quando a hibernação for bem-sucedida, você verá a seguinte tela.

#### Acessar um Ambiente Hibernado {#accessing-hibernated-environment}

Ao fazer solicitações de navegador contra o autor ou a camada de publicação de um ambiente hibernado, o usuário encontrará uma landing page descrevendo o status hibernado do ambiente, como ilustrado abaixo:

Um usuário com o Gerenciador de **nuvem - Função** de desenvolvedor pode clicar no botão Console do desenvolvedor para acessar o console do desenvolvedor e cancelar a hibernação do ambiente. Informações sobre a configuração de funções podem ser encontradas na Documentação do Cloud Manager.

Se um usuário em uma organização não puder clicar no botão do Developer Console para ser direcionado para o Developer Console, é provável que ele precise receber o &quot;Gerenciador de nuvem - Função de desenvolvedor&quot;.


### Deshibernação {#de-hibernation-introduction}

1. Navegue até o **Developer Console**.
Consulte [Acessar o Developer Console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) para saber como acessar o **Developer Console** a partir da placa de **Ambientes** .

   >[!IMPORTANT]
   >O acesso ao Console do desenvolvedor é definido pelo Gerenciador da **nuvem - Função** do desenvolvedor no Console **de** administração. Um usuário com uma permissão de função de desenvolvedor pode cancelar a hibernação de um ambiente do Programa Sandbox.

1. Clique em **Cancelar hibernação**, como mostrado na figura abaixo:

   ![](assets/de-hibernation-img1.png)

1. Clique em **Deshibernar** para confirmar a etapa.

   ![](assets/de-hibernation-img2.png)

1. Você receberá a notificação de que o processo de hibernação foi iniciado e será atualizado com o andamento.

   ![](assets/de-hibernation-img3.png)

1. Quando o processo for concluído, o ambiente do Programa Sandbox estará ativo novamente.

   ![](assets/de-hibernation-img4.png)


## Atualizações do AEM para Ambientes do Sandbox {#aem-updates-sandbox}


Consulte as atualizações [de versão do](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates) AEM para obter mais detalhes.

Um usuário pode aplicar manualmente as atualizações do AEM aos ambientes em um Programa Sandbox (veja a figura abaixo). Isso pode ser feito quando o status exibido for **ATUALIZAÇÃO DISPONÍVEL**.

A opção Atualizar está disponível no menu suspenso no Cartão de **Ambientes** . Essa opção também está disponível no botão **Gerenciar** , se você clicar em **Detalhes** no cartão de **Ambientes** .

>[!NOTE]
>É necessário configurar um pipeline de *não produção* que implante no ambiente de desenvolvimento de interesse para que seja iniciado um pipeline de atualização manual.

>[!NOTE]
>Um pipeline *de produção* deve ser configurado para que um pipeline de atualização manual seja iniciado para o conjunto de ambientes Production+Stage.

>[!NOTE]
>A atualização manual para o *Production* ou *Stage* ambiente atualizará automaticamente o outro. O conjunto de ambientes Production+Stage deve estar na mesma versão do AEM.





