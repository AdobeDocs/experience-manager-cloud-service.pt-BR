---
title: Integração com o Adobe Campaign Classic
description: Saiba como integrar o AEM as a Cloud Service com o Adobe Campaign Classic para criar conteúdo atraente para suas campanhas.
feature: Administering
role: Admin
exl-id: 23874955-bdf3-41be-8a06-53d2afdd7f2b
source-git-commit: cab630838f5cce3c2a2749c61b0aa7504dc403f7
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 100%

---

# Integração com o Adobe Campaign Classic {#integrating-campaign-classic}

Ao integrar o AEM as a Cloud Service com o Adobe Campaign, você pode gerenciar a entrega de emails, o conteúdo e os formulários diretamente no AEM as a Cloud Service. As etapas de configuração no Adobe Campaign Classic e no AEM as a Cloud Service são necessárias para permitir a comunicação bidirecional entre as soluções.

Essa integração permite que o AEM as a Cloud Service e o Adobe Campaign Classic sejam usados de forma independente. Os profissionais de marketing podem criar campanhas e usar o direcionamento no Adobe Campaign, enquanto os criadores de conteúdo podem trabalhar em paralelo no design de conteúdo no AEM as a Cloud Service. A integração permite que o conteúdo e o design da campanha no AEM sejam direcionados e entregues pelo Campaign.

## Etapas de integração {#integration-steps}

A integração entre o AEM e o Campaign requer várias etapas em ambas as soluções.

1. [Instalar o pacote de integração do AEM no Campaign.](#install-package)
1. [Criar um operador para o AEM no Campaign](#create-operator)
1. [Configurar a integração do Campaign no AEM](#campaign-integration)
1. [Configurar o externalizador do AEM](#externalizer)
1. [Configurar o usuário remoto de campanha no AEM](#configure-user)
1. [Configurar a conta externa do AEM no Campaign](#acc-setup)

Este documento aborda detalhadamente cada uma dessas etapas

## Pré-requisitos {#prerequisites}

* Acesso de administrador ao Adobe Campaign Classic
   * Para executar a integração, é necessário ter uma instância do Adobe Campaign Classic em funcionamento, incluindo um banco de dados configurado.
   * Se você precisar de detalhes adicionais sobre como definir e configurar o Adobe Campaign Classic, consulte a [documentação do Adobe Campaign Classic,](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html?lang=pt-BR) em particular, o Guia de instalação e configuração.

* Acesso de administrador ao AEM as a Cloud Service

## Instalação do pacote de integração do AEM no Campaign {#install-package}

O pacote de **Integração do AEM** no Adobe Campaign inclui várias configurações padrão necessárias para se conectar ao AEM.

1. Como administrador, faça logon na instância do Adobe Campaign usando o console do cliente.

1. Selecione **Ferramentas** > **Avançado** > **Importar pacote...**.

   ![Importar pacote](assets/import-package.png)

1. Clique em **Instalar um pacote padrão** e, em seguida, clique em **Próximo**.

1. Verifique o pacote de **integração do AEM**.

   ![Instalar um pacote padrão](assets/select-package.png)

1. Clique em **Próximo** e, em seguida, em **Iniciar** para começar a instalação.

   ![Progresso da instalação](assets/installation.png)

1. Quando a instalação for concluída, clique em **Fechar**.

O pacote de integração agora está instalado.

## Criação do operador para o AEM no Campaign {#create-operator}

O pacote de integração cria automaticamente o operador `aemserver` que o AEM usa para conectar-se ao Adobe Campaign. Você deve definir uma zona de segurança para esse operador e definir sua senha.

1. Faça logon no Adobe Campaign como administrador usando o console do cliente.

1. Selecione **Ferramentas** -> **Explorador** na barra de menus.

1. No explorador, navegue até o nó **Administração** > **Gerenciamento de acesso** > **Operadores**.

1. Selecione o operador `aemserver`.

1. Na guia **Editar** do operador, selecione a subguia **Direitos de acesso** e clique no link **Editar os parâmetros de acesso...**.

   ![Definir zona de segurança](assets/access-rights.png)

1. Selecione a zona de segurança apropriada e defina a máscara IP confiável conforme necessário.

1. Clique em **Salvar**.

1. Faça logout do cliente do Adobe Campaign.

1. No sistema de arquivos do servidor do Adobe Campaign, navegue até o local de instalação do Campaign e edite o arquivo `serverConf.xml` como administrador. Normalmente, esse arquivo está localizado em:
   * `C:\Program Files\Adobe\Adobe Campaign Classic v7\conf` no Windows.
   * `/usr/local/neolane/nl6/conf/eng` no Linux.

1. Procure por `securityZone` e certifique-se de que os seguintes parâmetros estejam definidos para a zona de segurança do operador do AEM.

   * `allowHTTP="true"`
   * `sessionTokenOnly="true"`
   * `allowUserPassword="true"`.

1. Salve o arquivo.

1. Certifique-se de que a zona de segurança não seja substituída pela respectiva configuração no arquivo `config-<server name>.xml`.

   * Se o arquivo de configuração contiver uma configuração de zona de segurança separada, altere o atributo `allowUserPassword` para `true`.

1. Se quiser alterar a porta do servidor do Adobe Campaign Classic, substitua `8080` pela porta desejada.

>[!CAUTION]
>
>Por padrão, não há zona de segurança configurada para o operador. Para conectar o AEM ao Adobe Campaign, você deve selecionar uma zona conforme detalhado nas etapas anteriores.
>
>A Adobe recomenda fortemente a criação de uma zona de segurança dedicada ao AEM para evitar quaisquer problemas de segurança. Para obter mais informações sobre esse tópico, consulte a [Documentação do Adobe Campaign Classic.](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/security-zones.html?lang=pt-BR)

1. No cliente do Campaign, retorne ao operador `aemserver` e selecione a guia **Geral**.

1. Clique no link **Redefinir senha...**.

1. Especifique uma senha e armazene-a em um local seguro para uso futuro.

1. Clique em **OK** para salvar a senha do operador `aemserver`.

## Configuração da integração do Campaign no AEM {#campaign-integration}

O AEM usa [o operador já configurado no Campaign](#create-operator) para se comunicar com o Campaign

1. Faça logon na instância de criação do AEM como administrador.

1. No painel lateral da navegação global, selecione **Ferramentas** > **Cloud Services** > **Cloud Services herdado** > **Adobe Campaign** e, depois, clique em **Configurar agora**.

   ![Configurar o Adobe Campaign](assets/configure-campaign-service.png)

1. Na caixa de diálogo, crie uma configuração do serviço do Campaign inserindo um **Título** e clique em **Criar**.

   ![Caixa de diálogo Configurar o Campaign](assets/configure-campaign-dialog.png)

1. Uma nova janela e uma nova caixa de diálogo são abertas para editar a configuração. Forneça as informações necessárias.

   * **Nome do usuário** - este é [o operador do pacote de integração do AEM com o Adobe Campaign criado na etapa anterior.](#create-operator) Por padrão, é `aemserver`.
   * **Senha** - esta é a senha do [operador do pacote de integração do AEM com o Adobe Campaign criado na etapa anterior.](#create-operator)
   * **Endpoint da API** - este é o URL da instância do Adobe Campaign.

   ![Configurar o Adobe Campaign no AEM](assets/configure-campaign.png)

1. Selecione **Conectar ao Adobe Campaign** para verificar a conexão e clique em **OK**.

Agora, o AEM pode se comunicar com o Adobe Campaign.

>[!NOTE]
>
>Certifique-se de que o servidor do Adobe Campaign possa ser acessado pela Internet. O AEM as a Cloud Service não pode acessar redes privadas.

## Configurar o Externalizador do AEM  {#externalizer}

O Externalizador é um serviço OSGi no AEM que transforma um caminho de recurso em um URL externo e absoluto, que é necessário para o AEM fornecer conteúdo que o Campaign possa usar.

1. Faça logon na instância de criação do AEM como administrador.
1. Confirme a instância de publicação na configuração do Externalizador verificando o despejo de status dos serviços OSGi no [console do desenvolvedor.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=pt-BR#osgi-services)
1. Se não estiver correto, faça as alterações necessárias no repositório Git da instância correspondente e [implante a configuração usando o Cloud Manager.](/help/implementing/cloud-manager/deploy-code.md)

```text
Service 3310 - [com.day.cq.commons.externalizer] (pid: com.day.cq.commons.impl.externalizerImpl)",
"  from Bundle 420 - Day Communique 5 Commons Library (com.day.cq.cq-commons), version 5.12.16",
"    component.id: 2149",
"    component.name: com.day.cq.commons.impl.externalizerImpl",
"    externalizer.contextpath: ",
"    externalizer.domains: [local https://author-p17558-e33255-cmstg.adobeaemcloud.com, author https://author-p17558-e33255-cmstg.adobeaemcloud.com,
     publish https://publish-p17558-e33255-cmstg.adobeaemcloud.com]",
"    externalizer.encodedpath: false",
"    externalizer.host: ",
"    feature-origins: [com.day.cq:cq-quickstart:slingosgifeature:cq-platform-model_quickstart_author:6.6.0-V23085]",
"    service.bundleid: 420",
"    service.description: Creates absolute URLs",
"    service.scope: bundle",
"    service.vendor: Adobe Systems Incorporated",
```

>[!NOTE]
>
>A instância de publicação deve ser acessível através do servidor do Adobe Campaign.

## Configurar o usuário remoto de campanha no AEM {#configure-user}

Para que o Campaign se comunique com o AEM, é necessário definir uma senha para o usuário `campaign-remote` no AEM.

1. Faça logon no AEM como administrador.
1. No console de navegação principal, clique em **Ferramentas** no painel esquerdo.
1. Em seguida, clique em **Segurança** -> **Usuários** para abrir o console de administração do usuário.
1. Localize o usuário `campaign-remote`.
1. Selecione o usuário `campaign-remote` e clique em **Propriedades** para editá-lo.
1. Na janela **Editar configurações de usuário**, clique em **Alterar senha**.
1. Forneça uma nova senha para o usuário e anote-a em um local seguro para uso futuro.
1. Clique em **Salvar** para salvar a alteração da senha.
1. Clique em **Salvar e fechar** para salvar as alterações no usuário `campaign-remote`.

## Configuração da conta externa do AEM no Campaign {#acc-setup}

Ao [instalar o pacote de **integração do AEM** no Campaign,](#install-package) uma conta externa é criada para o AEM. Ao configurar essa conta externa, o Adobe Campaign pode conectar-se ao AEM as a Cloud Service, permitindo a comunicação bidirecional das soluções.

1. Faça logon no Adobe Campaign como administrador usando o console do cliente.

1. Selecione **Ferramentas** -> **Explorador** na barra de menus.

1. No explorador, navegue até o nó **Administração** > **Plataforma** > **Contas externas**.

   ![Contas externas](assets/external-accounts.png)

1. Localize a conta externa do AEM. Por padrão, ela tem os valores:

   * **Tipo** - AEM
   * **Rótulo** - Instância do AEM
   * **Nome interno** - aemInstance

1. Na guia **Geral** dessa conta, insira as informações de usuário definidas na etapa [Definir senha do usuário remoto de campanha](#set-campaign-remote-password).

   * **Servidor** - O endereço do servidor do autor do AEM
      * O servidor do autor do AEM deve ser acessível através da instância do servidor do Adobe Campaign Classic.
      * Certifique-se de que o endereço do servidor **não** termine em uma barra.
   * **Conta** - Por padrão, esse é o usuário `campaign-remote` definido no AEM na etapa [Definir senha do usuário remoto de campanha](#set-campaign-remote-password).
   * **Senha** - Esta senha é igual à do usuário `campaign-remote` definido no AEM na etapa [Definir senha do usuário remoto de campanha](#set-campaign-remote-password).

1. Marque a caixa de seleção **Ativado**.

1. Clique em **Salvar**.

O Adobe Campaign agora pode se comunicar com o AEM.

## Próximas etapas {#next-steps}

Com o Adobe Campaign Classic e o AEM as a Cloud Service configurados, a integração está concluída.

Agora você pode aprender a criar um informativo no Adobe Experience Manager seguindo para [este documento.](/help/sites-cloud/authoring/campaign/creating-newsletters.md)
