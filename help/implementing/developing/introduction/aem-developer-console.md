---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: Saiba mais sobre o CRXDE Lite e o AEM as a Cloud Service Developer Console.
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

>[!NOTE]
>
>Este artigo descreve uma experiência renovada para o AEM Cloud Service Developer Console, que agora está na versão beta. Alguns clientes podem acessá-lo clicando em um botão na parte superior da interface clássica. A Adobe agradece seu feedback enviando-o para `aemcs-new-devconsole-ui-beta@adobe.com`. Para obter informações sobre o AEM Developer Console clássico, consulte [este artigo](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console).

O AEM as a Cloud Service Developer Console inclui um conjunto de ferramentas para depuração em ambientes na nuvem. Ele pode ser acessado por meio de um link por ambiente no Cloud Manager.

>[!NOTE]
>O AEM as a Cloud Service Developer Console não deve ser confundido com o [*Adobe Developer Console*](https://developer.adobe.com/developer-console/) de nome semelhante.
>


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

Os desenvolvedores podem acessar os recursos descritos abaixo:

## Pacotes OSGi {#osgi-bundles}

![Nova Tela de Pacotes OSGi no Console de Desenvolvimento](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* Uma visão geral dos pacotes OSGI implantados no tipo de ambiente selecionado. Ela permite uma pesquisa de texto completo.
* É útil obter informações do estado real dos pacotes no ambiente. Você pode obter informações como pacotes exportados, pacotes importados, serviços usados e muito mais.
* Os desenvolvedores desejam verificar o ambiente real e verificar se o pacote faz o que esperam que ele faça.
* **Exemplo de caso de uso:** Um intervalo de versões de uma dependência é especificado no seu pacote. Algo está errado na dependência. Você deseja verificar qual versão da dependência está sendo conectada ao seu pacote. Para verificar, vá para os detalhes do pacote e use a importação de pacotes para verificar qual versão do pacote ou versão do pacote está sendo usada no tempo de execução. Com essas informações, você pode ajustar o intervalo de versões de dependência do Maven ou adaptar seu código.

## Pacotes Java {#java-packages}

![Guia Pacotes Java na Interface do Usuário do Console de Desenvolvimento](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* Um prompt de pesquisa que pode ser usado para pesquisar pacotes que estão ativos no sistema OSGI do ambiente. Neste local, é possível ver qual pacote exporta (ou fornece) o pacote e qual pacote importa (ou usa) o pacote. Você também pode verificar se há pacotes duplicados (mesmo pacote, versões diferentes), o que pode causar problemas em alguns casos.
* **Exemplo de caso de uso:** um serviço personalizado usando o [carregador de classe dinâmica](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) carrega uma classe sem especificar uma versão. Como vários pacotes exportam versões diferentes, a implementação varia, causando alterações no comportamento. O desenvolvedor quer verificar quais pacotes estão no ambiente sem analisar o modelo de recurso. Eles pesquisam o pacote e visualizam todas as versões exportadas. Essa capacidade fornece as informações para inserir um intervalo de versões melhor.

## Servlets {#servlets}

![Guia Servlets na interface do Console de Desenvolvimento](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* Um prompt de pesquisa no qual você pode especificar um caminho com seletores e uma extensão com GET ou POST. Em seguida, ele fornece os resultados dos servlets em ordem de preferência que lida com a solicitação no Sling.
* **Exemplo de caso de uso:** você tem um servlet OSGI que deve ser ativado mediante uma solicitação e imprimir a saída para a resposta. No entanto, em vez da saída esperada, a resposta retorna vazia. Você precisa verificar se algum outro servlet está tendo precedência sobre o seu servlet devido a seletores mais específicos, `resourceType`, extensões ou classificação. Você pesquisa o caminho esperado e descobre que outro servlet está ativo com uma classificação mais alta. Em seguida, decida se você pode colocar seu servlet acima na classificação adicionando seletores, por exemplo.

## Serviços {#services}

![Guia Serviços na interface do Console de Desenvolvimento](/help/implementing/developing/introduction/assets/services-dev-console.png)

* Semelhante à exibição dos Componentes OSGI, mas baseado em serviços. Você pode pesquisar rapidamente quais serviços são fornecidos com determinadas propriedades.

## Componentes OSGi {#osgi-components}

![Guia Componentes OSGi na interface do usuário do Console de Desenvolvimento](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* Uma visão geral dos componentes OSGI presentes no tipo de ambiente selecionado. Ela permite uma pesquisa de texto completo.
* Você pode obter o estado ativo dos componentes OSGI no ambiente. Você pode ver quais serviços ele satisfaz, o pacote que o fornece e o tipo de ativação (imediato ou atrasado).
* **Exemplo de caso de uso 1:** Como desenvolvedor, você precisa verificar se um componente ativado com uma configuração está ativo em um ambiente específico. O motivo é porque o comportamento esperado não está ocorrendo. Basta pesquisar o componente na pesquisa e verificar se o componente está ativo ou não.
* **Exemplo de caso de uso 2:** você deseja ver quais componentes prontos para uso estão disponíveis no ambiente e identificar os serviços aos quais eles dão suporte. Essa capacidade ajuda você a saber mais sobre o Adobe Experience Manager as a Cloud Service. Você pode fazer check-out deles na lista de componentes.

## Integrações {#integrations}

![Guia Integrações na interface do Console de Desenvolvimento](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* Os administradores têm a capacidade de gerar, renomear e excluir credenciais de serviço e tokens de desenvolvedor.

## Repositório {#repository}

* Abre o [Navegador do repositório](/help/implementing/developing/tools/repository-browser.md).

## Status de Despejos/Consultas {#status-dumps-queries}

![Guia Despejos de Status/Consultas na Interface do Usuário do Console de Desenvolvimento](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* Um texto completo ou despejo JSON do estado atual de pacotes, pacotes, configurações, serviços, componentes, trabalhos do sling ou definições do Oak.
* Útil especialmente se o desenvolvedor tiver descoberto algum estado inesperado e quiser comunicar ou documentar esse estado para outros desenvolvedores. Baixar o despejo fornece um instantâneo do estado para referência posterior.

## Configurações {#configurations}

![Guia Configurações na interface do Console de Desenvolvimento](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* Uma lista pesquisável de configurações ativas no ambiente. Você pode ver quais propriedades são fornecidas pelas configurações, verificando a página de detalhes.
* **Exemplo de caso de uso:** um desenvolvedor deseja verificar se as configurações especificadas estão realmente presentes no ambiente. Se a configuração estiver ausente, eles poderão verificar o modelo de recurso ou o modo de execução ou pasta da configuração.

Para programas de Produção, a &quot;Cloud Manager - Função do desenvolvedor&quot; no Adobe Admin Console controla o acesso ao AEM as a Cloud Service Developer Console. Para programas de sandbox, qualquer usuário com um perfil de produto que conceda acesso ao AEM pode usar o Developer Console. Para todos os programas, a &quot;Cloud Manager - Função do desenvolvedor&quot; é necessária para despejos de status e acesso ao navegador do repositório. Para exibir dados de serviços de criação e publicação, os usuários também devem ser atribuídos ao Perfil de produto Usuários do AEM ou Administradores do AEM em ambos os serviços.

Para obter mais informações sobre como configurar permissões de usuário, consulte a [Documentação do Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles).

