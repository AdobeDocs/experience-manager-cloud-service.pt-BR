---
title: Console da Web
description: Saiba como usar o Console da Web do Adobe Experience Manager (AEM) para gerenciar configurações e pacotes OSGi para desenvolvimento local.
content-type: reference
topic-tags: configuring
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 3aaa615f-d3bf-4d1a-9dff-b6e271f0e9a6
source-git-commit: 3995e0090e1b0be1cbc430c3da7458b6ce867e09
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 0%

---


# Console da Web {#web-console}

Saiba como usar o Console da Web do Adobe Experience Manager (AEM) para gerenciar configurações e pacotes OSGi para desenvolvimento local.

## Visão geral {#overview}

O AEM as a Cloud Service trata a configuração e o código [ como imutáveis em tempo de execução.](/help/release-notes/aem-cloud-changes.md#apps-libs-immutable) Isso significa que todas as configurações devem ser implantadas como você codificaria em um ambiente de produção. Para instâncias de produção, isso garante que portas de qualidade sejam aprovadas e oferece um nível de estabilidade e clareza do ambiente atual.

No entanto, atualizações e alterações de pacote ad-hoc [Configuração OSGi](/help/implementing/deploying/configuring-osgi.md) geralmente são necessárias para testar os desenvolvimentos locais. Como parte do [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md), o Console da Web habilita essas atualizações em tempo real.

Com o AEM as a Cloud Service sendo executado localmente, o console pode ser acessado de `http://<host>:<port>/system/console`.

O Console da Web oferece uma seleção de telas e opções para manter os pacotes OSGi, incluindo:

* [Configuração](#configuration): para configurar os pacotes OSGi e, portanto, é o mecanismo subjacente para configurar os parâmetros de sistema do AEM
* [Pacotes](#bundles): para instalar pacotes
* [Componentes](#components): para controlar o status dos componentes necessários para o AEM
* [Gerando configurações OSGi](#generating-osgi-configurations): para gerar automaticamente configurações OSGi como JSON

Quaisquer alterações feitas são aplicadas imediatamente à SDK em execução. Não é necessário reiniciar.

No Console da Web, todas as descrições que mencionam as configurações padrão estão relacionadas aos padrões do Sling. O AEM tem seus próprios padrões e, portanto, os padrões definidos podem ser diferentes daqueles documentados pelo console.

O Console da Web no Adobe Experience Manager (AEM) é baseado no [Console de Gerenciamento da Web do Apache Felix.](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html) O Apache Felix é um esforço da comunidade para implementar a Plataforma de serviço OSGi R4, que inclui a estrutura OSGi e os serviços padrão.

>[!NOTE]
>
>O Console da Web só está disponível no SDK do AEM as a Cloud Service para fins de desenvolvimento local. Não está disponível na produção.

>[!TIP]
>
>Para verificar o status de suas configurações, pacotes e componentes OSGi em um ambiente de produção, use o [Developer Console.](/help/implementing/developing/introduction/aem-developer-console.md)

## Configuração {#configuration}

A tela **Configuração** é usada para configurar pacotes OSGi e, portanto, é o mecanismo subjacente para configurar parâmetros de sistema do AEM. A guia **Configuração** pode ser acessada por:

* O menu suspenso: **OSGi -> Configuração**
* URL: `http://<host>:<port>/system/console/configMgr`

Uma lista de configurações é exibida:

![A tela Configuração](assets/configuration.png)

Há dois tipos de configurações disponíveis na lista desta tela:

* **As configurações** permitem que você atualize as configurações existentes. Eles têm uma identidade persistente (PID) e podem ser:
   * Padrão e integral para o AEM - São obrigatórios, se excluídos, os valores retornarão às configurações padrão.
   * Instâncias criadas de configurações de fábrica - Essas instâncias são criadas pelo usuário, a exclusão remove a instância.
* **As Configurações de Fábrica** permitem criar uma instância do objeto de funcionalidade necessário. Ele é alocado para uma Identidade persistente e, em seguida, listado na lista Configurações.

Selecionar qualquer entrada na lista exibe os parâmetros relacionados a essa configuração:

![Parâmetros de configuração](assets/configuration-parameters.png)

Em seguida, você pode atualizar os parâmetros conforme necessário e:

* **Salvar** para salvar as alterações feitas.
   * Para uma configuração de fábrica, isso cria uma instância com uma identidade persistente.
   * A nova instância é listada em Configurações.
* **Redefinir** para redefinir os parâmetros mostrados na tela para os que foram salvos por último.
* **Excluir** para excluir a configuração atual.
   * Se for padrão, os parâmetros são retornados às configurações padrão.
   * Se criada a partir de uma configuração de fábrica, a instância específica é excluída.
* **Desassociar** para desassociar a configuração atual do pacote.
* **Cancelar** para cancelar as alterações atuais.

>[!TIP]
>
>Consulte [Configuração de OSGi para Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) para obter mais detalhes sobre configurações de OSGi.

## Pacotes {#bundles}

A tela **Pacotes** é usada para instalar pacotes OSGi necessários para o AEM. A tela é acessada por um dos seguintes métodos:

* O menu suspenso: **OSGi -> Pacotes**
* URL: `http://<host>:<port>/system/console/bundles`

Uma lista de pacotes é exibida:

![Pacotes](assets/bundles.png)

Com essa tela, você pode:

* **Instalar ou atualizar** para instalar um novo pacote ou atualizar um pacote existente.
   * Você pode **Procurar** para localizar o arquivo que contém o seu pacote e especificar se ele deve **Iniciar** imediatamente e em que **Nível inicial**.
* **Recarregar** para atualizar a lista exibida.
* **Atualizar Pacotes** para verificar as referências de todos os pacotes e atualizar, conforme necessário.
   * Por exemplo, após uma atualização, a versão antiga e a nova ainda podem estar em execução devido a referências anteriores. Essa opção verifica e move todas as referências para a nova versão, permitindo que a versão antiga seja interrompida.
* **Iniciar** para iniciar um pacote de acordo com o nível inicial especificado.
* **Stop** para parar o pacote.
* **Desinstalar** para desinstalar o pacote do sistema.

A lista especifica o status do pacote. clicando no nome de um pacote específico com mostrar mais informações.

>[!TIP]
>
>Após **Atualizar**, a Adobe recomenda que você clique em **Atualizar Pacotes**.

## Componentes {#components}

A tela **Componentes** permite habilitar e desabilitar componentes. Ele pode ser acessado das seguintes maneiras:

* O menu suspenso: **Principal -> Componentes**
* URL: `http://<host>:<port>/system/console/components`

Uma lista de componentes é exibida. Os ícones estão disponíveis para cada linha para permitir que você ative, desative ou (quando apropriado) abra os detalhes de configuração de um componente específico.

![Componentes](assets/components.png)

Clicar no nome de um componente específico exibe mais informações sobre o seu status. Aqui você também pode ativar, desativar ou recarregar o componente.

![Detalhes do componente](assets/component-details.png)

>[!NOTE]
>
>Habilitar ou desabilitar um componente se aplica somente até que o SDK seja reiniciado.
>
>O estado inicial é definido no descritor do componente, que é gerado durante o desenvolvimento e armazenado no pacote no momento da criação do pacote.

## Gerar configurações de OSGi {#generating-osgi-configs}

O Console da Web pode ser usado para configurar componentes OSGi e exportar configurações OSGi como JSON. Isso é útil para configurar componentes OSGi fornecidos pela AEM cujas propriedades OSGi e formatos de valor talvez você não esteja familiarizado ao definir configurações OSGi em seu projeto do AEM.

Consulte o documento [Configuração de OSGi para Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-web-console) para obter mais informações.
