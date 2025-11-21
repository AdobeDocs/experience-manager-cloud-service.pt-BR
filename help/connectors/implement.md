---
title: Implementação de um conector do AEM
description: Saiba mais sobre os conectores, o que eles podem fazer e como implementar essas ferramentas valiosas no Experience Manager.
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
feature: Operations
role: Admin
source-git-commit: a9cec66cf518a19a5a6152d431a052369b5b503a
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 71%

---


Implementação de um conector do AEM
=============================

As referências úteis para a criação de Conectores AEM são fornecidas a seguir e devem ser lidas com orientações sobre [envio](submit.md) e [manutenção](maintain.md) conectores.

Uma licença de desenvolvedor do AEM pode ser obtida através do [Programa Adobe Exchange](https://partners.adobe.com/technologyprogram/experiencecloud.html).

Padrões comuns de integração
---------------------------

O AEM é uma solução de gerenciamento de experiência online de ponta e oferece muitas áreas em potencial de integrações. Padrões comuns de integração incluem:

* Extrair dados de um sistema externo para o AEM. Por exemplo, exportar informações de contato de um CRM para torná-lo disponível para um público-alvo maior que visita um site viabilizado pelo AEM.  As implementações devem usar as [Tarefas agendadas](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs) do Sling, que garante que a tarefa seja executada mesmo se os contêineres fiquem inativos. O código deve ser projetado supondo que a tarefa possa ser acionada mais de uma vez.
* Exportar dados do AEM para um sistema externo. Por exemplo, as configurações de assinatura do boletim informativo são enviadas em um site viabilizado pela AEM para um CRM.
* Recuperar ativos do AEM. Por exemplo, um Sistema de gerenciamento de conteúdo (CMS) externo que faz referência a um ativo armazenado no AEM Assets. Ou como outro exemplo, um sistema PIM vinculado a uma imagem no AEM Assets.
* Armazenar ativos na infraestrutura do AEM. Por exemplo, um sistema de Gestão de Recursos de Marketing (MRM) que armazena um ativo aprovado no AEM Assets.
* Configurar e renderizar um componente de interface personalizado. Por exemplo, permitir que um autor arraste e solte um componente de vídeo e configure um vídeo específico para ser reproduzido no site ativo.
* Atuar em um ativo com um serviço de parceiro. Por exemplo, enviar um ativo para uma plataforma de vídeo quando uma página é publicada.
* Analisar um site, página ou ativo no AEM Admin Console. Por exemplo, fazer recomendações de SEO para uma página existente ou não publicada.
* Acesso em nível de página a dados do usuário mantidos por um serviço externo. Por exemplo, o uso de informações demográficas para personalizar a experiência no site. Leia sobre o ContextHub, uma estrutura para armazenar, manipular e apresentar dados de contexto.
* Traduzir uma cópia do site ou metadados de ativos. Consulte o [Conector de bootstrap da estrutura de tradução do AEM](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) para obter códigos de exemplo usando a Estrutura de tradução do AEM, que é a implementação preferida dos conectores de tradução.


Documentação útil
--------------------

A [documentação](../overview/introduction.md) do Experience Manager as a Cloud Service fornece informações valiosas sobre desenvolvimento no AEM. Abaixo estão alguns tópicos e referências técnicas específicos que podem ser úteis ao implementar um conector do AEM:

* Serviços Adobe Consulting (ACS) [Exemplos do AEM](https://adobe-consulting-services.github.io/acs-aem-samples/) para código bem comentado para ajudar a educar desenvolvedores do AEM
* Os vários links de documentação na seção Padrões comuns de integração deste artigo

Recursos da comunidade
--------------------

Além da documentação estática acima, a Adobe e a comunidade do AEM oferecem recursos para ajudar a trazer um conector para a produção:

* O [Fórum AEM](https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) da comunidade da Adobe é um site ativo no qual seus colegas fazem perguntas e respondem a dúvidas
* Recursos técnicos adicionais da Adobe estão disponíveis para determinados níveis de parceiros. Saiba mais sobre o [Programa Adobe Exchange](https://partners.adobe.com/technologyprogram/experiencecloud.html).
* Se sua organização deseja obter ajuda de implementação, considere a equipe de [Serviços profissionais](https://solutionpartners.adobe.com/s/directory) da Adobe ou consulte o [Localizador de parceiros de soluções](https://solutionpartners.adobe.com/s/directory/) para obter uma lista de parceiros da Adobe em todo o mundo

Regras de estrutura do pacote
-----------------------

Para facilitar as implantações móveis, os pacotes do AEM as a Cloud Service — como conectores — mantêm uma divisão estrita entre conteúdo &quot;imutável&quot; e &quot;mutável&quot;. Os pacotes devem ser claramente organizados de modo a incluir:

* `/apps`
* `/content` e `/conf`

Os conectores devem seguir essas diretrizes de pacotes, que estão descritas em [Estrutura de projetos do AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Os conectores existentes também devem ser alterados para estarem em conformidade.

Além disso, somente a Adobe deve gravar código no `/libs`, com clientes e parceiros escrevendo em `/apps`.

Os conectores existentes também podem precisar ser refatorados para mover qualquer configuração que tenha sido colocada `/etc` em outras pastas de nível superior, como `/conf`. Esta reestruturação foi realizada no âmbito do AEM 6.5 e é descrita na [Documentação do AEM 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/implementing/deploying/restructuring/repository-restructuring).

A Adobe recomenda colocar a maior parte do código do conector em `/apps/connectors/<vendor>` para manter uma estrutura de repositório limpa, especialmente para clientes que usam vários conectores.

Configurações dos serviços em nuvem
-----------------------------

Um aspecto da implementação do conector é o código que suporta a configuração do conector. Esse código faz com que um cartão com o nome do conector apareça em Ferramentas > Operações > Serviços em nuvem. Quando clicado, um [navegador de configuração](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) aparece onde o cliente seleciona a pasta principal para conter a configuração do conector. O código do conector deve resultar em um formulário com todas as propriedades que devem ser configuradas, armazenando os valores em uma pasta de configuração em `/conf`. Posteriormente, essa pasta pode ser selecionada na guia de propriedades do Sites ou na guia de propriedades do Assets.


Configurações sensíveis ao contexto
-----------------------------

As [Configurações sensíveis ao contexto](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) permitem criar camadas de configuração em diferentes pastas, incluindo `/libs`, `/apps`, `/conf` e subpastas em `/conf`. Elas suportam herança, para que um cliente possa configurar a configuração global enquanto faz alterações específicas para cada microsite. Como é possível usar esse recurso para Configurações do Cloud Services, o código do conector deve fazer referência à configuração usando a API de configuração sensível ao contexto, em vez de fazer referência a um nó de configuração específico.

Se as configurações modificadas forem usadas no conector, desenvolva-o para lidar com a inclusão/fusão de qualquer atualização futura nas configurações padrão fornecidas pelo conector com qualquer configuração de cliente. Lembre-se de que modificar conteúdo ou configurações personalizadas pelo cliente sem aviso prévio e consentimento pode interromper ou causar comportamento inesperado em seu conector.

Práticas recomendadas de codificação
----------------------

Como o AEM as a Cloud Service é uma solução nativa em nuvem, há algumas diretrizes que podem afetar as estratégias de código de um conector. Consulte [Diretrizes de desenvolvimento do AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md) para obter mais detalhes.

Testar o conector do AEM
-------------------------

Novos conectores devem ser criados (ou conectores existentes modificados) usando técnicas de desenvolvimento de ambiente local. A Equipe parceira fornece aos parceiros de ISV um ambiente de sandbox onde eles podem implantar o conector do AEM em um aplicativo padrão para garantir o funcionamento.
