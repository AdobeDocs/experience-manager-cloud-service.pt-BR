---
title: Gerenciamento de ambientes
description: Saiba mais sobre os tipos de ambientes que você pode criar e como criá-los para o seu projeto do Cloud Manager.
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 7174b398040acbf9b18b5ac2aa20fdba4f98ca78
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 2%

---

# Gerenciamento de ambientes {#managing-environments}

Saiba mais sobre os tipos de ambientes que você pode criar e como criá-los para o seu projeto do Cloud Manager.

## Tipos de ambientes {#environment-types}

Um usuário com as permissões necessárias pode criar os seguintes tipos de ambiente (dentro dos limites do que está disponível para o locatário específico).

* **Produção e Estágio** - Os ambientes de produção e de preparo estão disponíveis como um par e são usados para fins de produção e teste, respectivamente.

* **Desenvolvimento** - Pode ser criado um ambiente de desenvolvimento para fins de desenvolvimento e de ensaio e pode ser associado apenas a gasodutos não relacionados com a produção.


Os recursos de ambientes individuais dependem das soluções ativadas no [programa.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

* [Sites](/help/sites-cloud/home.md)
* [Assets](/help/assets/home.md)
* [Forms](/help/forms/home.md)
* [Screens](/help/screens-cloud/home.md)

>[!NOTE]
>
>Ambientes de produção e de preparo são criados apenas como um par. Não é possível criar apenas um ambiente de preparo ou de produção.

## Adicionar um ambiente {#adding-environments}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada.

1. Clique no programa para o qual deseja adicionar um ambiente.

1. No **Visão geral do programa** clique em **Adicionar ambiente** no **Ambientes** cartão para adicionar um ambiente.

   ![Cartão de ambientes](assets/no-environments.png)

   * O **Adicionar ambiente** também está disponível no **Ambientes** guia .

      ![Guia Ambientes](assets/environments-tab.png)

   * O **Adicionar ambiente** pode ser desativada devido à falta de permissões ou dependendo dos recursos licenciados.

1. No **Adicionar ambiente** exibida:

   * Selecione um **Tipo de ambiente**.
      * O número de ambientes disponíveis/usados é exibido entre parênteses atrás do tipo de ambiente de desenvolvimento.
   * Forneça uma **Nome do ambiente**.
   * Forneça uma **Descrição do ambiente**.
   * Selecione um **Região da nuvem**.

   ![Caixa de diálogo Adicionar ambiente](assets/add-environment2.png)

1. Clique em **Salvar** para adicionar o ambiente especificado.

O **Visão geral** agora exibe seu novo ambiente na **Ambientes** cartão. Agora você pode configurar pipelines para seu novo ambiente.

## Detalhes do ambiente {#viewing-environment}

Você pode usar o **Ambientes** na página de visão geral para acessar os detalhes de um ambiente de duas maneiras.

1. No **Visão geral** clique no botão **Ambientes** na parte superior da tela.

   ![Guia Ambientes](assets/environments-tab2.png)

   * Como alternativa, clique no botão **Mostrar tudo** no botão **Ambientes** cartão para ir diretamente para o **Ambientes** guia .

      ![Mostrar todas as opções](assets/environment-showall.png)

1. O **Ambientes** abre e lista todos os ambientes para o programa.

   ![A guia ambientes](assets/environment-view-2.png)

1. Clique em um ambiente na lista para revelar seus detalhes.

   ![Detalhes do ambiente](assets/environ-preview1.png)

Como alternativa, clique no botão de reticências do ambiente desejado e selecione **Exibir detalhes**.

![Exibir detalhes do ambiente](assets/view-environment-details.png)

>[!NOTE]
>
>O **Ambientes** O cartão lista apenas três ambientes. Clique no botão **Mostrar tudo** conforme descrito anteriormente para ver todos os ambientes do programa.

### Acesso ao serviço de visualização {#access-preview-service}

O Cloud Manager fornece um serviço de visualização (fornecido como um serviço de publicação adicional) para cada ambiente AEM as a Cloud Service.

Usando o serviço, você pode visualizar a experiência final de um site antes que ele atinja o ambiente de publicação real e esteja disponível publicamente.

Após a criação, o serviço de visualização terá uma lista de permissões IP padrão aplicada a ele, identificada `Preview Default [<envId>]`, que bloqueia todo o tráfego para o serviço de visualização. Você deve desaplicar ativamente a lista de permissões IP padrão do serviço de visualização para ativar o acesso.

![Serviço de visualização e sua lista de permissões](assets/preview-ip-allow.png)

Um usuário com as permissões necessárias deve concluir as etapas das seguintes opções antes de compartilhar o URL do serviço de visualização com qualquer uma das equipes para garantir o acesso ao URL de visualização.

1. Crie uma lista de permissões IP apropriada, aplique-a ao serviço de visualização e desaplique imediatamente a variável `Preview Default [<envId>]` lista de permissões.

   * Consulte o documento [Aplicar e desaplicar Listas de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) para obter mais detalhes.

1. Usar a atualização **LISTA DE PERMISSÕES IP** para remover o IP padrão e adicionar IPs conforme apropriado. Consulte [Gerenciamento de Listas de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md) para saber mais.

Quando o acesso ao serviço de visualização estiver desbloqueado, o ícone de bloqueio antes do nome do serviço de visualização não será mais exibido.

Depois de ativado, você pode publicar conteúdo no serviço de visualização usando a interface Gerenciar publicação no AEM. Consulte o documento [Visualização de conteúdo](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para obter mais detalhes.

>[!NOTE]
>
>Seu ambiente deve estar AEM versão `2021.05.5368.20210529T101701Z` ou mais recente. Para fazer isso, verifique se um pipeline de atualização foi executado com êxito em seu ambiente.

## Atualização de ambientes {#updating-dev-environment}

Como um serviço nativo em nuvem, as atualizações dos ambientes de preparo e produção nos programas de produção são automaticamente gerenciadas pelo Adobe.

No entanto, as atualizações em ambientes de desenvolvimento e em ambientes em programas sandbox são gerenciadas dentro dos programas. Quando esse ambiente não estiver executando a versão de AEM mais recente disponível publicamente, o status na **Ambientes** no cartão **Visão geral** a tela do programa será exibida **Atualização disponível**.

![Status de atualização do ambiente](assets/environ-update.png)

### Atualizações e pipelines {#updates-pipelines}

Os pipelines são a única maneira de [implante o código nos ambientes AEM as a Cloud Service.](deploy-code.md) Por esse motivo, cada pipeline está associado a uma versão de AEM específica.

Se o Cloud Manager detectar que há uma versão mais recente do AEM disponível do que a implantada pela última vez no pipeline, ela mostrará a variável **Atualização disponível** status do ambiente.

O processo de atualização é, portanto, um processo em duas etapas:

1. Atualização do pipeline com a versão de AEM mais recente
1. Execução do pipeline para implantar a nova versão do AEM em um ambiente

### Atualização de seus ambientes {#updating-your-environments}

O **Atualizar** está disponível no **Ambientes** cartão para ambientes e ambientes de desenvolvimento em programas sandbox clicando no botão de reticências do ambiente.

![Atualizar opção do cartão Ambientes](assets/environ-update2.png)

Essa opção também está disponível ao clicar no botão **Ambientes** do programa e selecionando o botão de reticências do ambiente.

![Atualizar opção da guia Ambientes](assets/environ-update3.png)

Um usuário com a **Gerenciador de implantação** A função pode usar essa opção para atualizar o pipeline associado a esse ambiente para a versão de AEM mais recente.

Quando a versão do pipeline é atualizada para a versão de AEM mais recente disponível publicamente, o usuário é solicitado a executar o pipeline associado para implantar a versão mais recente no ambiente .

![Solicitar a execução do pipeline para atualizar o ambiente](assets/update-run-pipeline.png)

O **Atualizar** O comportamento da opção varia dependendo da configuração e do estado atual do programa.

* Se o pipeline já tiver sido atualizado, a variável **Atualizar** solicita que o usuário execute o pipeline.
* Se o pipeline já estiver sendo atualizado, a variável **Atualizar** informa ao usuário que uma atualização já está em execução.
* Se um pipeline apropriado não existir, a variável **Atualizar** solicita que o usuário crie uma.

## Exclusão de ambientes de desenvolvimento {#deleting-environment}

O usuário com as permissões necessárias poderá excluir um ambiente de desenvolvimento.

No **Visão geral** do programa no **Ambientes** , clique no botão de reticências do ambiente de desenvolvimento que deseja excluir.

![A opção de exclusão](assets/environ-delete.png)

A opção de exclusão também está disponível no **Ambientes** da guia **Visão geral** janela do programa. Clique no botão de reticências do ambiente e selecione **Excluir**.

![A opção de exclusão da guia Ambientes.](assets/environ-delete2.png)

>[!NOTE]
>
>* Os ambientes de produção e de preparo criados em um programa de produção não podem ser excluídos.
>* Os ambientes de produção e de preparo em um programa sandbox podem ser excluídos.


## Gerenciamento de acesso {#managing-access}

Selecionar **Gerenciar acesso** no menu elipse do ambiente no **Ambientes** cartão. Você pode navegar diretamente para a instância do autor e gerenciar o acesso do seu ambiente.

![Opção Gerenciar acesso](assets/environ-access.png)

## Acesso ao Console do desenvolvedor {#accessing-developer-console}

Selecionar **Console do desenvolvedor** no menu elipse do ambiente no **Ambientes** cartão. Isso abrirá uma nova guia no navegador com a página de logon no **Console do desenvolvedor**.

![](assets/environ-devconsole.png)

Somente um usuário com a variável **Desenvolvedor** terá acesso à função **Console do desenvolvedor**. No entanto, para programas sandbox, qualquer usuário com acesso ao programa sandbox terá acesso a **Console do desenvolvedor**.

Consulte o documento [Hibernar e desibernar ambientes de sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction) para obter mais detalhes.

Essa opção também está disponível no **Ambiente** da guia **Visão geral** ao clicar no menu de reticências de um ambiente individual.

## Fazer logon localmente {#login-locally}

Selecionar **Logon local** no menu elipse do ambiente no **Ambientes** para fazer logon localmente no Adobe Experience Manager.

![Logon localmente](assets/environ-login-locally.png)

Além disso, você pode fazer logon localmente da **Ambientes** da guia **Visão geral** página.

![Logon localmente na guia Ambientes](assets/environ-login-locally-2.png)

## Gerenciar nomes de domínio personalizados {#manage-cdn}

Os nomes de domínio personalizados são suportados nos programas do Cloud Manager for Sites para serviços de publicação e visualização. Cada ambiente do Cloud Manager pode hospedar até 250 domínios personalizados.

Para configurar nomes de domínio personalizados, navegue até o **Ambientes** e clique em um ambiente para exibir os detalhes do ambiente.

![Detalhes do ambiente](assets/domain-names.png)

As seguintes ações podem ser executadas no serviço de publicação para seu ambiente.

* [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

* [Gerenciar nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)

* [Verificando o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) ou [Certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn).

* [Gerenciamento de listas de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)


## Gerenciamento de listas de permissões de IP {#manage-ip-allow-lists}

As listas de permissões de IP são compatíveis com o Cloud Manager para criar, publicar e visualizar serviços para programas do Sites.

Para gerenciar listas de permissões de IP, navegue até o **Ambientes** da guia **Visão geral** página do seu programa. Clique em um ambiente individual para gerenciar seus detalhes.

### Aplicação de uma lista de permissões de IP {#apply-ip-allow-list}

A aplicação de uma lista de permissões IP associa todos os intervalos IP incluídos na definição da lista de permissões a um serviço de criação ou publicação em um ambiente. Um usuário na **Proprietário da empresa** ou **Gerenciador de implantação** deve estar conectado para poder aplicar uma lista de permissões IP.

A lista de permissões IP deve existir no Cloud Manager para ser aplicada a um ambiente. Para saber mais sobre listas de permissões de IP no Cloud Manager, consulte o documento[Introdução às Listas de permissões IP no Cloud Manager.](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)

Siga estas etapas para aplicar uma lista de permissões IP.

1. Navegue até o ambiente específico do **Ambientes** guia do programa **Visão geral** e navegue até a **LISTAS DE PERMISSÕES de IP** tabela.
1. Use os campos de entrada na parte superior da tabela lista de permissões IP para selecionar a lista de permissões IP e o serviço de criação ou publicação ao qual deseja aplicá-la.
1. Clique em **Aplicar** e confirme seu envio.

### Desaplicar uma Lista de permissões IP {#unapply-ip-allow-list}

A desaplicação de uma lista de permissões IP desassocia todos os intervalos IP incluídos na definição da lista de permissões de um serviço de autor ou editor em um ambiente. Um usuário na **Proprietário da empresa** ou **Gerenciador de implantação** deve estar conectado para poder desaplicar uma lista de permissões IP.

Siga estas etapas para desaplicar uma lista de permissões IP.

1. Navegue até o ambiente específico do **Ambientes** guia do programa **Visão geral** e navegue até a **LISTAS DE PERMISSÕES de IP** tabela.
1. Identifique a linha na qual a regra de lista de permissões IP que você deseja desaplicar é listada.
1. Selecione o botão de reticências no final da linha.
1. Selecionar **Não aplicar** e confirme seu envio.
