---
title: Integração com o Adobe Target
description: 'Integração com o Adobe Target '
feature: Administering
role: Admin
exl-id: cf243fb6-5563-427f-a715-8b14fa0b0fc2
source-git-commit: 7d67bdb5e0571d2bfee290ed47d2d7797a91e541
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 2%

---

# Integração com o Adobe Target{#integrating-with-adobe-target}

Como parte da Adobe Marketing Cloud, o Adobe Target permite aumentar a relevância do conteúdo por meio do direcionamento e da medição em todos os canais. A integração do Adobe Target e AEM as a Cloud Service requer:

* usando a interface do usuário de toque para criar uma Configuração do Target em AEM as a Cloud Service (configuração IMS necessária).
* adicionar e configurar o Adobe Target como uma extensão no [Adobe Launch](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/quick-start.html).

O Adobe Launch é necessário para gerenciar propriedades do lado do cliente para o Analytics e o Target em páginas AEM (bibliotecas/tags JS). Dito isso, a integração com o Launch é necessária para o &quot;direcionamento de experiência&quot;. Para exportar Fragmentos de experiência para o Target, você precisa apenas da Configuração do Adobe Target e do IMS.

>[!NOTE]
>
>Os clientes do Adobe Experience Manager as a Cloud Service que não têm uma conta Target existente podem solicitar acesso ao Target Foundation Pack para Experience Cloud. O Foundation Pack fornece uso limitado por volume do Target.

## Criação da configuração do Adobe Target {#create-configuration}

1. Navegue até **Ferramentas** → **Cloud Services**.
   ![](assets/cloudservice1.png "Navegação")
2. Selecione **Adobe Target**.
3. Selecione o botão **Create**.
   ![](assets/tenant1.png "Criar")
4. Preencha os detalhes (veja abaixo) e selecione **Connect**.
   ![](assets/open_screen1.png "ConnectConnect")

### Configuração IMS {#ims-configuration}

Uma configuração IMS para o Launch e o Target é necessária para integrar corretamente o Target ao AEM e ao Launch. Embora a configuração do IMS para o Launch seja pré-configurada AEM as a Cloud Service, a configuração do IMS do Target deve ser criada (após o provisionamento do Target). Consulte [este vídeo](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html) e [esta página](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-ims-adobe-io.html) para saber como criar a configuração IMS do Target.

### ID de locatário da Adobe Target e código de cliente do Adobe Target {#tenant-client}

Ao configurar os campos Adobe Target Tenant ID e Adobe Target Client Code, esteja ciente do seguinte:

1. Para a maioria dos clientes, a ID do locatário e o código do cliente são os mesmos. Isso significa que ambos os campos contêm as mesmas informações e são idênticos. Certifique-se de inserir a ID do locatário em ambos os campos.
2. Para fins herdados, você também pode inserir valores diferentes nos campos ID do locatário e Código do cliente .

Em ambos os casos, esteja ciente de que:

* Por padrão, o Código do cliente (se adicionado primeiro) também é copiado automaticamente para o campo ID do locatário .
* Você tem a opção de alterar o conjunto padrão de ID de locatário.
* Assim, as chamadas de back-end para o Target serão baseadas na ID do locatário e as chamadas do lado do cliente para o Target serão baseadas no Código do cliente.

Como dito anteriormente, o primeiro caso é o mais comum para AEM as a Cloud Service. De qualquer maneira, verifique se os campos **e** contêm as informações corretas, dependendo de seus requisitos.

>[!NOTE]
>
> Se quiser alterar uma Configuração do Target existente:
>
> 1. Insira novamente a ID do locatário.
> 2. Conecte-se novamente ao Target.
> 3. Salve a configuração.


### Editar a configuração do Target {#edit-target-configuration}

Para editar a configuração do Target, siga estas etapas:

1. Selecione uma configuração existente e clique em **Propriedades**.
2. Edite as propriedades.
3. Selecione **Reconectar ao Adobe Target**.
4. Selecione **Salvar e fechar**.

### Adicionar uma configuração a um site {#add-configuration}

Para aplicar uma configuração da interface de toque a um site, acesse: **Sites** → **Selecione qualquer página de site** → **Propriedades** → **Avançado** → **Configuração** → Selecione o locatário de configuração.

## Integração do Adobe Target em sites AEM usando o Adobe Launch {#integrate-target-launch}

AEM oferece uma integração pronta para uso com o Experience Platform Launch. Ao adicionar a extensão Adobe Target ao Experience Platform Launch, é possível usar os recursos do Adobe Target em AEM páginas da Web. As bibliotecas do Target só serão renderizadas usando o Launch.

>[!NOTE]
>
>As estruturas existentes (herdadas) ainda funcionam, mas não podem ser configuradas na interface do usuário de toque. É aconselhável recriar as configurações de mapeamento de variável no Launch.

Como visão geral, as etapas de integração são:

1. Criar uma propriedade do Launch
2. Adicionar as extensões necessárias
3. Criar um elemento de dados (para capturar parâmetros do hub de contexto)
4. Criar uma regra de página
5. Criar e publicar

### Criação de uma propriedade do Launch {#create-property}

Uma propriedade é um container preenchido com extensões, regras, elementos de dados.

1. Selecione o botão **Nova propriedade**.
2. Forneça um nome para a propriedade.
3. Como domínio, insira o IP/host no qual deseja carregar a biblioteca do launch.
4. Selecione o botão **Save**.
   ![](assets/properties_newproperty1.png "LaunchpropertyLaunchproperty")

### Adicionar as extensões necessárias {#add-extension}

**** As extensões são o contêiner que gerencia as principais configurações da biblioteca. A extensão Adobe Target suporta implementações do lado do cliente usando o SDK JavaScript do Target para a Web moderna, a at.js. Você deve adicionar as extensões **Adobe Target** e **Adobe ContextHub**.

1. Selecione a opção Catálogo de extensões e procure pelo Target no filtro .
2. Selecione **Adobe Target** at.js e clique na opção Instalar .
   ![Pesquisa do Target ](assets/search_ext1.png "SearchTarget")
3. Selecione o botão **Configurar**. Observe a janela de configuração com as credenciais de conta do Target importadas e a versão da at.js para essa extensão.
4. Selecione **Save** para adicionar a extensão do Target à propriedade do Launch. Você deve conseguir ver a extensão do Target listada na lista **Extensões instaladas**.
   ![Salvar Extensão ](assets/configure_extension1.png "ExtensionSave")
5. Repita as etapas acima para pesquisar a extensão **Adobe ContextHub** e instalá-la (isso é necessário para a integração com parâmetros contexthub, com base na qual o direcionamento será feito).

### Criar um elemento de dados {#data-element}

**Os** elementos de dados são os espaços reservados para os quais você pode mapear parâmetros do hub de contexto.

1. Selecione **Elementos de Dados**.
2. Selecione **Adicionar elemento de dados**.
3. Forneça o nome do elemento de dados e o mapeie para um parâmetro de hub de contexto.
4. Selecione **Salvar**.
   ![Elemento ](assets/data_elem1.png "de dados")

### Criando uma regra de página {#page-rule}

Em **Rule** definimos e ordenamos uma sequência de ações, que são executadas no site, para alcançar o direcionamento.

1. Adicione um conjunto de ações, como exemplificado na captura de tela.
   ![](assets/rules1.png "Ações")
2. Em Adicionar params a todas as mboxes, adicione o elemento de dados configurado anteriormente (consulte o elemento de dados acima) ao parâmetro que será enviado na chamada de mbox.
   ![](assets/map_data1.png "MboxActions")

### Criar e publicar {#build-publish}

Para saber como criar e publicar, consulte esta [página](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html).

## Alterações na estrutura do conteúdo entre as configurações do Classic e do Touch UI {#changes-content-structure}

| **Alterar** | **Configuração da interface clássica** | **Configuração da interface de toque** | **Consequências** |
|---|---|---|---|
| Localização da configuração do Target. | /etc/cloudservices/testandtarget/ | /conf/tenant/settings/cloudservices/target | Anteriormente, várias configurações estavam presentes em /etc/cloudservices/testandtarget, mas agora uma única configuração está presente em um locatário. |

>[!NOTE]
>
>As configurações herdadas ainda são compatíveis com clientes existentes (sem a opção de editar ou criar novos). As configurações herdadas farão parte dos pacotes de conteúdo carregados pelos clientes que usam o VSTS.
