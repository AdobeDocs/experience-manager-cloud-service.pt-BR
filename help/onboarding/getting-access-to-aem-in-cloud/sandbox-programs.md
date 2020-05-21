---
title: Programas Sandbox - Serviço em nuvem
description: Programas Sandbox - Serviço em nuvem
translation-type: tm+mt
source-git-commit: eb874176c71d7f3d03d953f7bae4cb3db2ffb3b9
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# Programas Sandbox {#sandbox-programs}

## Introdução {#introduction}

Um programa Sandbox é um dos dois tipos de programas disponíveis no serviço AEM Cloud, sendo o outro um programa Regular.

Uma caixa de proteção é normalmente criada para servir aos propósitos de treinamento, execução de demonstrações, ativação ou POCs. Eles não são feitos para transportar tráfego ao vivo.

Os programas do Sandbox incluem Sites e Ativos e serão entregues automaticamente preenchidos com uma ramificação Git que inclui código de amostra, um ambiente de desenvolvimento e um pipeline de não-produção.

Para obter mais informações sobre tipos de programas, consulte [Entendendo Programas e tipos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html)de Programas.

### Atributos de Programas Sandbox {#attributes-sandbox}

Os Programas Sandbox têm os seguintes atributos:

1. **Criação de Programas:** A criação do programa Sandbox inclui o recurso automático:
   * configuração de projeto com código de amostra e conteúdo
   * criação de ambientes de desenvolvimento
   * criação de pipeline de não produção implantando no ambiente de desenvolvimento (ramo mestre implantando no ambiente de desenvolvimento)

1. **As soluções incluem:** Os programas Sandbox incluem Sites e Ativos.

1. **Atualizações do AEM:** As atualizações do AEM podem ser aplicadas manualmente a ambientes em um programa Sandbox e não são enviadas automaticamente.

1. **Hibernação:** Ambientes em um programa Sandbox serão automaticamente hibernados se nenhuma atividade for detectada por um determinado período de tempo. ambientes hibernados podem ser removidos manualmente.

### Criação de um programa Sandbox {#creating-sandbox-program}

Um assistente de criação de programas solicitará que o usuário envie detalhes.

Para obter informações sobre como criar um programa sandbox, consulte [Criação de um Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program)Sandbox.

### Criação de Ambientes Sandbox {#creating-sandbox-environments}

Os programas do Sandbox serão entregues a um ambiente de desenvolvimento no momento da criação do programa de uma maneira criada automaticamente. O ambiente de desenvolvimento vem com um autor e uma camada de publicação por padrão.

O conjunto de ambientes de estágio de produção pode ser adicionado manualmente ao programa Sandbox, quando o usuário estiver pronto para configurar um pipeline de produção.

Para obter informações sobre como criar manualmente um ambiente, consulte [Adicionar Ambientes](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments).

### Excluindo Ambientes do Sandbox  {#deleting-sandbox-environments}

O usuário com as permissões necessárias poderá excluir conjuntos de ambientes de desenvolvimento ou de produção/estágio.

Para obter informações sobre como excluir um ambiente, consulte [Excluir Ambientes](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment).


## Hibernando e removendo Ambientes do Sandbox {#hibernating-introduction}

Os ambientes de programa da caixa de proteção entrarão em um modo *de* hibernação após um período de inatividade.

>[!NOTE]
>A hibernação é exclusiva para ambientes de programas da caixa de proteção. ambientes regulares de programas não serão hibernados.

### Hibernação {#hibernation-introduction}

A hibernação pode ocorrer automática ou manualmente. Pode levar alguns minutos para que um ambiente seja hibernado. Os dados são preservados durante a hibernação.

A hibernação é classificada como:

* **ambientes automáticos** de programa Sandbox são hibernados automaticamente após oito horas de inatividade, o que significa que os serviços de autor ou publicação não recebem solicitação.

* **Manual**: Os clientes podem hibernar manualmente um ambiente de programa de caixa de proteção, embora não haja necessidade de fazer isso, pois a hibernação ocorrerá automaticamente após um período de inatividade.

#### Uso da hibernação manual {#using-manual-hibernation}


A hibernação manual pode ser realizada em qualquer uma das duas telas no console do desenvolvedor.

Siga as etapas abaixo para hibernar manualmente seus ambientes de programa:

1. Navegue até o Developer Console.
1. Clique em Hibernar
1. Clique em Hibernar para confirmar.
1. Quando a hibernação for bem-sucedida, você verá a seguinte tela.
1. Na tela de listagens do ambiente, ilustrada abaixo e que pode ser acessada clicando no link Ambientes na tela de detalhes do ambiente, o botão Hibernar pode ser clicado na linha do ambiente desejado. Uma tela de confirmação será exibida.

### Deshibernação {#de-hibernation-introduction}

>[!IMPORTANT]
>O acesso ao Developer Console é definido pelo &quot;Gerenciador de nuvem - Função do desenvolvedor&quot; no Admin Console. Com essa permissão, um usuário pode cancelar a hibernação de um ambiente.

### Acessar um Ambiente Hibernado {#accessing-hibernated-environment}

Ao fazer solicitações de navegador contra o autor ou a camada de publicação de um ambiente hibernado, o usuário encontrará uma landing page descrevendo o status hibernado do ambiente, como ilustrado abaixo:

Um usuário com o &quot;Gerenciador de nuvem - Função do desenvolvedor&quot; pode clicar no botão do Console do desenvolvedor para acessar o console do desenvolvedor e cancelar a hibernação do ambiente. Informações sobre a configuração de funções podem ser encontradas na Documentação do Cloud Manager.

Se um usuário em uma organização não puder clicar no botão do Developer Console para ser direcionado para o Developer Console, é provável que ele precise receber o &quot;Gerenciador de nuvem - Função de desenvolvedor&quot;.




## Atualizações do AEM para ambientes do Sandbox {#aem-updates-sandbox}


Consulte as atualizações [de versão do](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates)AEM.

O usuário pode aplicar manualmente as atualizações do AEM aos ambientes em um programa Sandbox (veja a figura abaixo). Isso pode ser feito quando o status exibido for ATUALIZAÇÃO DISPONÍVEL. A opção de atualização estará disponível no menu suspenso na placa Ambientes. Ela também pode ser selecionada no menu Gerenciar na tela AMBIENTES.

>[!NOTE]
>É necessário configurar um pipeline de não-produção implantado no ambiente de desenvolvimento de interesse para que seja iniciado um pipeline de atualização manual.

>[!NOTE]
>Um pipeline de produção deve ser configurado para que um pipeline de atualização manual seja iniciado para o conjunto de ambientes Production+Stage.

>[!NOTE]
>A atualização manual para Produção ou ambiente de estágio atualizará automaticamente a outra. O conjunto de ambientes Production+Stage deve estar na mesma versão do AEM.





