---
title: Gerenciamento de ambientes
description: Saiba mais sobre os tipos de ambientes que você pode criar e como criá-los para o seu projeto do Cloud Manager.
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: cf1e2717342ca4e00780428d6ccf264bd8eca371
workflow-type: tm+mt
source-wordcount: '2276'
ht-degree: 37%

---


# Gerenciamento de ambientes {#managing-environments}

Saiba mais sobre os tipos de ambientes que você pode criar e como criá-los para o seu projeto do Cloud Manager.

## Tipos de ambientes {#environment-types}

Um usuário com as permissões necessárias pode criar os tipos de ambientes descritos a seguir (dentro dos limites do que está disponível para o locatário específico).

* **Produção + preparo**: os ambientes de produção e preparo estão disponíveis como um par e são usados para fins de produção e teste, respectivamente.

* **Desenvolvimento**: um ambiente de desenvolvimento pode ser criado para fins de desenvolvimento e testes e pode ser associado apenas a pipelines de não produção.

* **Desenvolvimento rápido** - Um ambiente de desenvolvimento rápido (RDE) permite que um desenvolvedor implante e revise alterações rapidamente, minimizando o tempo necessário para testar recursos que comprovadamente funcionam em um ambiente de desenvolvimento local. Consulte [a documentação do ambiente de desenvolvimento rápido](/help/implementing/developing/introduction/rapid-development-environments.md) para obter detalhes sobre como usar um RDE.

Os recursos de ambientes individuais dependem das soluções ativadas no [programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) do ambiente.

* [Sites](/help/sites-cloud/home.md)
* [Assets](/help/assets/home.md)
* [Forms](/help/forms/home.md)
* [Screens](/help/screens-cloud/home.md)

>[!NOTE]
>
>Ambientes de produção e de preparo são criados apenas em pares. Não é possível criar apenas um ambiente de preparo ou de produção.

## Adição de um ambiente {#adding-environments}

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa ao qual deseja adicionar um ambiente.

1. No **Visão geral do programa** clique em **Adicionar ambiente** no **Ambientes** para adicionar um ambiente.

   ![Cartão Ambientes](assets/no-environments.png)

   * A opção **Adicionar ambiente** também está disponível na guia **Ambientes**.

     ![Guia Ambientes](assets/environments-tab.png)

   * A opção **Adicionar ambiente** pode estar desativada devido à falta de permissões ou dependendo dos recursos licenciados.

1. Na caixa de diálogo **Adicionar ambiente**:

   * Selecione um [**tipo de ambiente**.](#environment-types)
      * O número de ambientes disponíveis/usados é exibido entre parênteses atrás do nome do tipo de ambiente.
   * Forneça um **nome** de ambiente.
   * Forneça uma **descrição** do ambiente.
   * Se você estiver adicionando um **Produção + Preparo** ambiente, você deve fornecer um nome e uma descrição de ambiente para os ambientes de produção e de preparo.
   * Selecione uma **região principal** no menu suspenso.
      * A região primária não pode ser alterada após a criação.
      * Dependendo dos direitos disponíveis, talvez seja possível configurar [várias regiões](#multiple-regions).

   ![Caixa de diálogo Adicionar ambiente](assets/add-environment2.png)

1. Clique em **Salvar** para adicionar o ambiente especificado.

A tela **Visão geral** agora exibe seu novo ambiente no cartão **Ambientes**. Agora você pode configurar pipelines para seu novo ambiente.

## Várias regiões de publicação {#multiple-regions}

Um usuário com a variável **Proprietário da empresa** a função pode configurar ambientes de produção e de preparo para incluir até três regiões de publicação adicionais, além da região principal. Regiões de publicação adicionais podem melhorar a disponibilidade. Consulte a [Documentação adicional das regiões de publicação](/help/operations/additional-publish-regions.md) para obter mais detalhes.

>[!TIP]
>
>Você pode usar o [API do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/api-usage/creating-programs-and-environments/#creating-aem-cloud-service-environments) para consultar uma lista atual de regiões disponíveis.

### Adicionando várias regiões de publicação a um novo ambiente {#add-regions}

Ao adicionar um ambiente, você pode optar por configurar regiões adicionais, além da região principal.

1. Selecione o **Região principal**.
   * A região primária não pode ser alterada após a criação do ambiente.
1. Selecione a opção **Adicionar regiões de publicação adicionais** e um novo **Regiões de publicação adicionais** opção é exibida.
1. No **Regiões de publicação adicionais** selecione uma região extra.
1. A região selecionada é adicionada abaixo do menu suspenso para indicar sua seleção.
   * Toque ou clique no `X` ao lado da região selecionada, para que você possa desmarcá-la.
1. Selecione outra região na **Regiões de publicação adicionais** para adicionar outra região.
1. Toque ou clique **Salvar** quando estiver pronto para criar seu ambiente.

![Seleção de várias regiões](assets/select-multiple-regions.png)

As regiões selecionadas se aplicam aos ambientes de produção e de preparo.

Se você não especificar regiões adicionais, [você pode fazer isso posteriormente após a criação dos ambientes.](#edit-regions)

Se desejar provisionar [rede avançada](/help/security/configuring-advanced-networking.md) para o programa, recomenda-se que esse provisionamento seja feito antes de adicionar outras regiões de publicação aos ambientes usando a API do Cloud Manager. Caso contrário, o tráfego das regiões de publicação adicionais passa pelo proxy da região primária.

### Editar várias regiões de publicação {#edit-regions}

Inicialmente, se você não tiver especificado regiões adicionais, poderá fazer isso depois que os ambientes forem criados, se tiver os direitos necessários.

Você também pode remover regiões de publicação adicionais. No entanto, você só pode adicionar ou remover regiões em uma transação. Se você precisar adicionar uma região e remover uma região, primeiro adicione, salve a alteração e remova (ou vice-versa).

1. No console Visão geral do programa, clique no botão de reticências do ambiente de produção e selecione **Editar** no menu.

   ![Editar ambiente](assets/select-edit-environment.png)

1. No **Editar ambiente de produção** faça as alterações necessárias nas regiões de publicação adicionais.
   * Use o **Regiões de publicação adicionais** para selecionar regiões adicionais.
   * Clique no X ao lado das regiões de publicação adicionais selecionadas para desmarcá-las.

   ![Editar ambiente](assets/edit-environment.png)

1. Toque ou clique **Salvar** para salvar as alterações.

As alterações feitas no ambiente de produção se aplicam aos ambientes de produção e de preparo. As alterações em várias regiões de publicação podem ser editadas somente no ambiente de produção.

Se desejar provisionar [rede avançada](/help/security/configuring-advanced-networking.md) para o programa, recomenda-se que esse provisionamento seja feito antes de adicionar outras regiões de publicação aos ambientes. Caso contrário, o tráfego das regiões de publicação adicionais passa pelo proxy da região primária.

## Detalhes do ambiente {#viewing-environment}

Você pode usar o **Ambientes** na página de visão geral para acessar os detalhes de um ambiente de duas maneiras.

1. No **Visão geral** clique no link **Ambientes** na parte superior da tela.

   ![Guia Ambientes](assets/environments-tab2.png)

   * Como alternativa, clique no link **Mostrar tudo** botão no **Ambientes** para ir diretamente para o **Ambientes** guia.

     ![Mostrar todas as opções](assets/environment-showall.png)

1. A tela **Ambientes** abre, listando todos os ambientes do programa.

   ![Guia Ambientes](assets/environment-view-2.png)

1. Clique em um ambiente na lista para que você possa revelar seus detalhes.

   ![Detalhes do ambiente](assets/environ-preview1.png)

Como alternativa, clique no botão de reticências do ambiente desejado e selecione **Exibir detalhes**.

![Exibir detalhes do ambiente](assets/view-environment-details.png)

>[!NOTE]
>
>O cartão **Ambientes** lista apenas três ambientes. Clique em **Mostrar tudo** conforme descrito anteriormente para ver todos os ambientes do programa.

### Acesso ao serviço de visualização {#access-preview-service}

O Cloud Manager fornece um serviço de visualização (fornecido como um serviço de publicação extra) para cada ambiente as a Cloud Service AEM.

Usando o serviço, você pode visualizar a experiência final de um site antes que ele atinja o ambiente de publicação real e esteja disponível publicamente.

Lista de permissões Na criação, o serviço de visualização tem um arquivo de IP de visualização padrão rotulado como, `Preview Default [<envId>]`, que bloqueia todo o tráfego para o serviço de visualização. Lista de permissões Desaplique a pesquisa de IP padrão do serviço de visualização para poder habilitar o acesso.

![Serviço de visualização e sua lista de permissões](assets/preview-ip-allow.png)

Um usuário com as permissões necessárias deve concluir as etapas a seguir antes de compartilhar a URL do serviço de visualização para garantir o acesso a ela.

1. Crie uma inclui na lista de permissões IP apropriada, aplique-a ao serviço de visualização e desaplique imediatamente a `Preview Default [<envId>]` incluir na lista de permissões.

   * Consulte [Aplicando e desaplicando Listas de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) para obter mais detalhes.

1. Use o fluxo de trabalho da **Lista de permissões de IP** para remover o IP padrão e adicionar IPs conforme apropriado. Consulte [Gerenciamento de listas de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md) para saber mais.

Depois que o acesso ao serviço de visualização é desbloqueado, o ícone de bloqueio na frente do nome do serviço de visualização não é mais exibido.

Uma vez ativado, você poderá publicar conteúdo no serviço de visualização usando a interface do usuário Gerenciar publicação no AEM. Consulte [Visualização de conteúdo](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para obter mais detalhes.

>[!NOTE]
>
>Seu ambiente deve estar na versão `2021.05.5368.20210529T101701Z` do AEM, ou uma versão mais recente, para usar o serviço de visualização. Verifique se um pipeline de atualização foi executado com êxito em seu ambiente para que você possa usar o serviço de visualização.

## Atualização de ambientes {#updating-dev-environment}

Como um serviço de nuvem nativo, as atualizações dos ambientes de preparo e produção nos programas de produção são gerenciadas automaticamente pela Adobe.

No entanto, as atualizações para ambientes de desenvolvimento e de programas de sandbox são gerenciadas dentro dos programas. Quando o ambiente não estiver executando a versão mais recente do AEM disponível publicamente, o status na variável **Ambientes** no **Visão geral** A tela do programa mostra **Atualização disponível**.

![Status de atualização do ambiente](assets/environ-update.png)

### Atualizações e pipelines {#updates-pipelines}

Os pipelines são a única maneira de [implantar código nos ambientes do AEM as a Cloud Service.](deploy-code.md) Por esse motivo, cada pipeline está associado a uma versão específica do AEM.

Se o Cloud Manager detectar que está disponível uma versão do AEM mais recente do que a implantada pela última vez no pipeline, ele mostrará a **Atualização disponível** status do ambiente.

O processo de atualização é, portanto, um processo de duas etapas:

1. Atualização do pipeline com a versão mais recente do AEM
1. Execução do pipeline para implantar a nova versão do AEM em um ambiente

### Atualização dos ambientes {#updating-your-environments}

A variável **Atualizar** está disponível na **Ambientes** para ambientes de desenvolvimento e de programas de sandbox clicando no botão de reticências do ambiente.

![Opção Atualizar no cartão Ambientes](assets/environ-update2.png)

Essa opção também está disponível clicando no link **Ambientes** do programa e selecionando o botão de reticências do ambiente.

![Opção Atualizar na guia Ambientes](assets/environ-update3.png)

Um usuário com a função **Gerente de implantação** pode usar essa opção para atualizar o pipeline associado a esse ambiente para a versão mais recente do AEM.

Quando a versão do pipeline é atualizada para a versão mais recente do AEM disponível publicamente, o usuário é solicitado a executar o pipeline associado para implantar a nova versão no ambiente.

![Solicitação para executar o pipeline para atualizar o ambiente](assets/update-run-pipeline.png)

O comportamento da opção **Atualizar** varia dependendo da configuração e do estado atual do programa.

* Se o pipeline já tiver sido atualizado, a opção **Atualizar** solicitará que o usuário execute o pipeline.
* Se o pipeline estiver sendo atualizado, a variável **Atualizar** informará ao usuário que uma atualização já está em execução.
* Se um pipeline apropriado não existir, a opção **Atualizar** solicitará que o usuário crie um.

## Exclusão de ambientes de desenvolvimento {#deleting-environment}

O usuário com a permissão necessária pode excluir um ambiente de desenvolvimento.

No **Visão geral** tela do programa no **Ambientes** clique no botão de reticências do ambiente de desenvolvimento que deseja excluir.

![A opção de exclusão](assets/environ-delete.png)

A opção de exclusão também está disponível na guia **Ambientes** da janela **Visão geral** do programa. Clique no botão de reticências do ambiente e selecione **Excluir**.

![A opção de exclusão na guia Ambientes](assets/environ-delete2.png)

>[!NOTE]
>
>* Os ambientes de produção e de preparo criados em um programa de produção não podem ser excluídos.
>* Os ambientes de produção e de preparo em um programa de sandbox podem ser excluídos.

## Gerenciamento de acesso {#managing-access}

Selecione **Gerenciar acesso** no menu de reticências do ambiente no cartão **Ambientes**. Você pode navegar diretamente para a instância de autoria e gerenciar o acesso ao seu ambiente.

![Opção Gerenciar acesso](assets/environ-access.png)

>[!TIP]
>
>Consulte [Equipe as a Cloud Service do AEM e perfis de produto](/help/onboarding/aem-cs-team-product-profiles.md) se quiser saber como os perfis de produto e de equipe as a Cloud Service do AEM podem conceder e limitar o acesso às soluções Adobe licenciadas.

## Acesso ao Developer Console {#accessing-developer-console}

Selecione **Developer Console** no menu de reticências do ambiente no cartão **Ambientes**. Uma nova guia é aberta no navegador com a página de logon na **Console do desenvolvedor**.

![Faça logon no Console do desenvolvedor](assets/environ-devconsole.png)

Somente um usuário com o **Desenvolvedor** A função tem acesso à **Console do desenvolvedor**. No entanto, para programas de sandbox, qualquer usuário com acesso ao programa de sandbox tem acesso a **Console do desenvolvedor**.

Consulte [Hibernação e cancelamento da hibernação de ambientes de sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/introduction-sandbox-programs.html#hibernation) para obter mais detalhes.

Essa opção também está disponível na guia **Ambiente** da janela **Visão geral** clicando no menu de reticências de um ambiente individual.

## Logon local {#login-locally}

Selecionar **Logon local** no menu de reticências do ambiente no **Ambientes** para que você possa fazer logon localmente no Adobe Experience Manager.

![Logon local](assets/environ-login-locally.png)

Além disso, você pode fazer logon localmente na **Ambientes** guia do **Visão geral** página.

![Logon local na guia Ambientes](assets/environ-login-locally-2.png)

## Gerenciar nomes de domínio personalizados {#manage-cdn}

Os nomes de domínio personalizados são suportados nos programas do Sites do Cloud Manager para serviços de publicação e visualização. Cada ambiente do Cloud Manager pode hospedar no máximo 250 domínios personalizados.

Para configurar nomes de domínio personalizados, navegue até o **Ambientes** e clique em um ambiente para exibir os detalhes.

![Detalhes do ambiente](assets/domain-names.png)

As ações a seguir podem ser realizadas no serviço de publicação do seu ambiente.

* [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

* [Gerenciar nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)

* [Verificar o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) ou [Certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn).

* [Gerenciamento de listas de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)


## Gerenciamento de listas de permissões de IP {#manage-ip-allow-lists}

As listas de permissões IP são compatíveis com os serviços de criação, publicação e visualização do Cloud Manager para programas do Sites.

Para gerenciar listas de permissões de IP, navegue até a página **Ambientes** guia do **Visão geral** página do seu programa. Clique em um ambiente individual para gerenciar seus detalhes.

### Aplicação de uma lista de permissões de IP {#apply-ip-allow-list}

A aplicação de uma incluir na lista de permissões lista de permissões de IP associa todos os intervalos IP incluídos na definição do arquivo a um serviço de autoria ou publicação em um ambiente. Um usuário no **Proprietário da empresa** ou **Gerente de implantação** A função deve estar conectada para poder aplicar uma inclui na lista de permissões IP.

O arquivo de inclui na lista de permissões IP deve existir no Cloud Manager para ser aplicado a um ambiente. Para saber mais sobre as listas de permissões de IP no Cloud Manager, consulte [Introdução às Listas de permissões de IP no Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

**Para aplicar uma inclui na lista de permissões de IP:**

1. Navegue até o ambiente específico na guia **Ambientes** da tela **Visão geral** do programa e acesse a tabela **Listas de permissões de IP**.
1. Use os campos de entrada na parte superior da tabela de inclui na lista de permissões de IP para poder selecionar o arquivo de inclui na lista de permissões de IP e o serviço de autoria ou publicação ao qual deseja aplicá-lo.
1. Clique em **Aplicar** e confirme o envio.

### Cancelamento de aplicação de uma inclui na lista de permissões de IP {#unapply-ip-allow-list}

O cancelamento da aplicação de uma inclui na lista de permissões de IP desassocia todos os intervalos de IP incluídos na definição do arquivo de inclui na lista de permissões de um serviço de autoria ou edição em um ambiente. Um usuário no **Proprietário da empresa** ou **Gerente de implantação** A função deve estar conectada para poder desaplicar um incluo na lista de permissões IP.

**Para desaplicar uma inclui na lista de permissões de IP:**

1. Navegue até o ambiente específico na guia **Ambientes** da tela **Visão geral** do programa e acesse a tabela **Listas de permissões de IP**.
1. Identifique a linha na qual a regra de inclui na lista de permissões de IP que você deseja desaplicar está listada.
1. Selecione o botão de reticências no final da linha.
1. Clique em **Cancelar aplicação** e confirme o envio.
