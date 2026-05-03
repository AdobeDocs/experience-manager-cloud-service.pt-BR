---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: Saiba mais sobre o AEM as a Cloud Service Developer Console e seu conjunto de ferramentas somente leitura para depurar ambientes de nuvem.
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: 51c14ba3c15e0136911003752253d21ed673a0eb
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---


# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

O AEM as a Cloud Service Developer Console inclui um conjunto de ferramentas somente leitura para depurar ambientes de nuvem. Ele pode ser acessado por meio de um link por ambiente no Cloud Manager e oferece recursos para visualizar pacotes, configurações OSGi, serviços e servlets e muito mais.

>[!NOTE]
>
>Este artigo descreve uma experiência renovada para o AEM Cloud Service Developer Console, que agora está na versão beta.
>
>* Um conjunto limitado de usuários pode acessar o novo console por meio de um botão na parte superior do Developer Console atual.
>* A Adobe agradece qualquer feedback, que você possa enviar para `aemcs-new-devconsole-ui-beta@adobe.com`.
>* Para obter a documentação sobre o AEM Developer Console atual, consulte [este artigo.](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)
>* O AEM as a Cloud Service Developer Console não deve ser confundido com o [*Adobe Developer Console* de nome semelhante.](https://developer.adobe.com/developer-console/)

>[!TIP]
>
>O Developer Console é somente leitura. Se você estiver trabalhando no desenvolvimento local usando o SDK e precisar modificar as configurações do OSGi ou o conteúdo do repositório, poderá usar:
>
>* [CRXDE Lite](/help/implementing/developing/tools/crxde.md)

<!--
There are multiple ways of accessing it:

1. Launch from Cloud Manager  

1. Type a url that can be determined by adjusting the Author or Publish service urls as follows:
   ```  
   https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com
   ```  

1. As a shortcut, the following Cloud Manager CLI command can be used to launch the AEM as a Cloud Service Developer Console based on an environment parameter described below:    
   ```
   aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>
   ```
-->

## Pré-requisitos {#prerequisites}

O Developer Console só pode ser acessado por usuários com determinadas funções em determinados programas.

* Para programas de produção, a &quot;Cloud Manager - Função do desenvolvedor&quot; no Adobe Admin Console controla o acesso à Developer Console.
* Para programas de sandbox, qualquer usuário com um perfil de produto que conceda acesso ao AEM pode usar o Developer Console.
* Para todos os programas, a &quot;Cloud Manager - Função do desenvolvedor&quot; é necessária para despejos de status e acesso ao navegador do repositório.

Para visualizar dados de serviços de autoria e publicação, os usuários também devem ser atribuídos ao &quot;Usuários do AEM&quot; ou ao &quot;Perfil de produto de administradores do AEM&quot; em ambos os serviços.

Para obter mais informações sobre como configurar permissões de usuário, consulte a [Documentação do Cloud Manager.](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)

## Guia Pacotes OSGi {#osgi-bundles}

A guia **Pacotes OSGi** fornece uma visão geral dos pacotes OSGi implantados no ambiente selecionado e oferece uma pesquisa de texto completo.

![Nova tela de pacotes OSGi na Developer Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* A guia fornece informações sobre o estado real dos pacotes no ambiente, como pacotes exportados, pacotes importados, serviços usados e muito mais.
* É ideal verificar o status de pacotes e ver se o pacote faz o que é esperado.

**Exemplo de caso de uso:** Digamos que você especifique um intervalo de versões para uma dependência no seu pacote. Mas algo dá errado com a dependência e você precisa verificar qual versão da dependência é realmente usada pelo pacote. Para verificar, abra o Developer Console e clique em um nome de pacote na guia **Pacotes OSGi** para acessar os detalhes do pacote, e use a opção **Importar pacotes** para verificar qual versão do pacote ou versão do pacote está sendo usada no tempo de execução. Com essas informações, você pode ajustar o intervalo de versões de dependência do Maven ou adaptar seu código.

## Guia Pacotes Java {#java-packages}

A guia **Pacotes Java** oferece um campo de pesquisa para pesquisar pacotes que estão ativos no sistema OSGi do ambiente.

![Guia Pacotes Java na interface do usuário do Developer Console](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* Você pode ver qual pacote exporta (ou fornece) o pacote e quais pacotes importam (ou usam) o pacote.
* Você também pode verificar se há pacotes duplicados (mesmo pacote, versões diferentes), o que pode causar problemas em alguns casos.

**Exemplo de caso de uso:** Digamos que um serviço personalizado usando o [carregador de classe dinâmica](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) carregue uma classe sem especificar uma versão. Como vários pacotes exportam versões diferentes, a implementação varia, causando alterações no comportamento. Verifique quais pacotes estão no ambiente sem analisar o modelo de recursos. Usando essa guia, é possível pesquisar o pacote e exibir todas as versões exportadas, e então usar um intervalo de versões melhor.

## Guia Configurações {#configurations}

A guia **Configurações** oferece uma lista pesquisável de configurações ativas no ambiente. Você pode ver quais propriedades são fornecidas por cada configuração clicando nelas e visualizando a página de detalhes.

![Guia Configurações na interface do Developer Console](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* **Exemplo de caso de uso:** digamos que você queira verificar se as configurações especificadas estão realmente presentes no ambiente. Se você pesquisar a guia **Configurações** no console e a configuração estiver ausente, poderá verificar o modelo de recurso, o modo de execução da configuração ou a pasta.

## Guia Servlets {#servlets}

A guia **Servlets** oferece um campo de pesquisa onde você pode especificar um caminho com seletores e uma extensão com GET ou POST. Em seguida, ele fornece uma lista de servlets em ordem de preferência que lida com a solicitação no Sling.

![Guia Servlets na interface do Developer Console](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

**Exemplo de caso de uso:** digamos que você tenha um servlet OSGi que deve ser ativado após uma solicitação e imprimir a saída para a resposta. No entanto, em vez da saída esperada, você recebe uma resposta vazia. Você precisa verificar se algum outro servlet está tendo precedência sobre o seu servlet devido a seletores mais específicos, `resourceType`, extensões ou classificação. Você pesquisa o caminho esperado e descobre que outro servlet está ativo com uma classificação mais alta. Você pode decidir se pode aumentar a classificação do servlet adicionando seletores, por exemplo.

## Guia Serviços {#services}

A guia **Serviços** fornece uma visão geral dos serviços presentes no ambiente selecionado e oferece uma pesquisa de texto completo.

![Guia Serviços na interface do Developer Console](/help/implementing/developing/introduction/assets/services-dev-console.png)

Clique em um serviço para exibir seus detalhes.

## Guia Componentes do OSGi {#osgi-components}

A guia **Componentes OSGi** fornece uma visão geral dos componentes OSGi presentes no tipo de ambiente selecionado e oferece uma pesquisa de texto completo. Você pode ver o estado ativo dos componentes OSGi no ambiente e quais serviços ele satisfaz, o pacote que os fornece e o tipo de ativação (imediata ou atrasada).

![Guia Componentes OSGi na interface do usuário do Developer Console](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* **Exemplo de caso de uso 1:** Digamos que você precise verificar se um componente ativado com uma configuração está ativo em um ambiente específico desde que você esteja encontrando um comportamento inesperado. Basta pesquisar o componente na pesquisa e verificar se o componente está ativo ou não.
* **Exemplo de caso de uso 2:** digamos que você queira ver quais componentes prontos para uso estão disponíveis no ambiente e identificar os serviços aos quais eles dão suporte para aprender mais sobre o Adobe Experience Manager as a Cloud Service. Você pode verificar os componentes na lista de componentes.

## Guia Integrações {#integrations}

A guia **Integrações** permite que administradores gerem, renomeiem e excluam credenciais de serviço e tokens de desenvolvedor.

![Guia Integrações na interface do Developer Console](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

## Guia Repositório {#repository}

A guia **Repositório** abre o navegador [Repositório.](/help/implementing/developing/tools/repository-browser.md)

## Guia Status Dumps / Consultas {#status-dumps-queries}

A guia **Despejos de status/consultas** permite baixar um despejo de texto completo ou JSON do estado atual de pacotes, pacotes, configurações, serviços, componentes, trabalhos do sling ou definições do Oak.

![Guia Despejos de Status/Consultas na Interface do Usuário do Developer Console](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

Você também pode abrir a [Ferramenta de desempenho da consulta.](/help/operations/query-and-indexing-best-practices.md#query-performance-tool)

* **Exemplo de caso de uso:** esta guia é especialmente útil se você encontrar um estado inesperado e quiser comunicá-lo ou documentá-lo para outros desenvolvedores. Baixar o despejo fornece um instantâneo do estado para referência posterior.
