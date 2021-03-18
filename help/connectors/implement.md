---
title: Implementação de um conector do AEM
description: Implementação de um conector do AEM
translation-type: tm+mt
source-git-commit: b77113ccc55f2063c684d49e2babdd7563b9d6fc
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 8%

---


Implementação de um conector do AEM
=============================

As referências úteis para a criação de [Conectores do AEM](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) são fornecidas a seguir e devem ser lidas em conjunto com orientações sobre [envio](submit.md) e [manutenção](maintain.md) de conectores.

Observe que uma licença de desenvolvedor para AEM pode ser obtida por meio do [Adobe Exchange Program](https://partners.adobe.com/exchangeprogram/experiencecloud).

Padrões comuns de integração
---------------------------

O AEM é uma solução de gerenciamento de experiência online de ponta e oferece muitas áreas em potencial de integrações. Padrões comuns de integração incluem:

* Extraindo dados de um sistema externo para o AEM. Por exemplo, exportando informações de contato de um CRM para torná-lo disponível para um público-alvo maior que visita um site alimentado por AEM.  As implementações devem usar os [Jobs Programados](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs) do Sling, o que garante que o trabalho seja executado mesmo se os contêineres estiverem inativos. O código deve ser projetado para supor que a tarefa possa ser acionada mais de uma vez.
* Exportação de dados do AEM para um sistema externo. Por exemplo, as configurações de assinatura do boletim informativo enviadas em um site alimentado por AEM para um CRM.
* Recuperação de ativos do AEM. Por exemplo, um Sistema de gerenciamento de conteúdo externo (CMS) que faz referência a um ativo armazenado no AEM Assets. Ou como outro exemplo, um sistema PIM vinculado a uma imagem no AEM Assets.
* Armazenando ativos na infraestrutura do AEM. Por exemplo, um sistema de Gestão de Recursos de Marketing (MRM) armazenando um ativo aprovado no AEM Assets.
* Configuração e renderização de um componente de interface de usuário personalizada. Por exemplo, permita que um autor arraste e solte um componente de vídeo e configure um vídeo específico para ser reproduzido no site ativo.
* Atuando em um ativo com um serviço de parceiro. Por exemplo, enviar um ativo para uma plataforma de vídeo quando uma página é publicada.
* Análise de um site, página ou ativo no Admin Console AEM. Por exemplo, fazer recomendações de SEO para uma página existente ou não publicada.
* Acesso ao nível da página a dados do usuário mantidos por um serviço externo. Por exemplo, aproveite as informações demográficas para personalizar a experiência do site. Leia sobre o ContextHub, uma estrutura para armazenar, manipular e apresentar dados de contexto.
* Tradução da cópia do site ou metadados do ativo. Consulte o [AEM Conector de Bootstrap da Estrutura de Tradução](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) para obter o código de amostra usando a Estrutura de Tradução AEM, que é a implementação preferida dos conectores de tradução.


Documentação útil
--------------------

O Experience Manager as a Cloud Service [documentation](../overview/introduction.md) fornece informações valiosas sobre o desenvolvimento no AEM. Abaixo estão alguns tópicos e referências técnicas específicos que podem ser úteis ao implementar um conector de AEM:

* Adobe Consulting Services (ACS) [AEM Amostras](http://adobe-consulting-services.github.io/acs-aem-samples/) para código bem comentado que ajuda a educar desenvolvedores AEM
* Os vários links de documentação na seção Padrões comuns de integração deste artigo

Recursos da comunidade
--------------------

Além da documentação estática acima, o Adobe e a comunidade de AEM oferecem recursos para ajudar a trazer um conector para o mercado:

* O [Fórum AEM da Comunidade do Adobe](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) é um site ativo onde seus colegas fazem e respondem a perguntas
* Recursos técnicos adicionais do Adobe estão disponíveis para determinados níveis de parceiros. Saiba mais sobre o [Adobe Exchange Program](https://partners.adobe.com/exchangeprogram/experiencecloud).
* Se sua organização deseja obter ajuda de implementação, considere a equipe de [Serviços profissionais](http://www.adobe.com/br/experience-cloud/consulting-services.html) da Adobe ou consulte o [Localizador de parceiros de soluções](https://solutionpartners.adobe.com/home/partnerFinder.html) para obter uma lista de parceiros da Adobe em todo o mundo

Regras de estrutura do pacote
-----------------------

Para oferecer suporte a implantações móveis, AEM como pacotes de Cloud Service, dos quais os conectores são exemplos, têm uma separação estrita entre conteúdo &quot;imutável&quot; e &quot;mutável&quot;. Os pacotes devem ser claramente separados entre aqueles que incluem:

* `/apps`
* `/content` e `/conf`

Os conectores devem seguir essas diretrizes de empacotamento, que são descritas em [this article](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Os conectores existentes também devem ser refatorados para estarem em conformidade.

Além disso, somente o Adobe deve gravar código em `/libs`, com clientes e parceiros gravando em `/apps`.

Os conectores existentes também podem precisar ser refatorados para mover qualquer configuração que tenha sido colocada `/etc` em outras pastas de nível superior, como `/conf`. Essa reestruturação foi feita como parte do AEM 6.5 e está descrita na [AEM documentação 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html).

Recomenda-se que a maioria do código do conector seja colocada em `/apps/connectors/<vendor>` para promover uma estrutura de repositório limpa para clientes que têm vários conectores.

Configurações dos serviços em nuvem
-----------------------------

Um aspecto da implementação do conector é o código que suporta a configuração do conector. Esse código faz com que um cartão com o nome do conector apareça em Ferramentas > Operações > Cloud Services. Quando clicado, um [navegador de configuração](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) é exibido, onde o cliente seleciona a pasta principal para conter a configuração do conector. O código do conector deve resultar em um formulário com todas as propriedades que devem ser configuradas, armazenando os valores em uma pasta de configuração em `/conf`. Posteriormente, essa pasta pode ser selecionada na guia de propriedades Sites ou na guia de propriedades de Ativos.


Configurações sensíveis ao contexto
-----------------------------

[A ](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) configuração sensível ao contexto permite a configuração de camadas em diferentes pastas, incluindo  `/libs`,  `/apps`e subpastas em  `/conf`   `/conf`. Ele suporta herança para que um cliente possa configurar a configuração global enquanto faz alterações específicas para cada microsite. Como é possível aproveitar esse recurso para configurações do Cloud Services, o código do conector deve fazer referência à configuração usando a API de configuração sensível ao contexto, em vez de fazer referência a um nó de configuração específico.

Se as configurações modificadas forem usadas no Conector, arquive o Conector para lidar com incluindo/mesclando qualquer atualização futura nas configurações padrão fornecidas pelo Conector com qualquer configuração de cliente. Lembre-se de que alterar o conteúdo personalizado (como em alterado pelo cliente) ou a configuração sem aviso e consentimento do cliente pode quebrar (ou criar comportamento inesperado) com seu Conector.

Práticas recomendadas de codificação
----------------------

Como o AEM as a Cloud Service é uma solução nativa em nuvem, há algumas diretrizes que podem afetar as estratégias de código de um conector. Consulte [AEM como Diretrizes de desenvolvimento de Cloud Service](/help/implementing/developing/introduction/development-guidelines.md) para obter mais detalhes.

Teste do conector de AEM
-------------------------

Novos conectores devem ser criados (ou conectores existentes modificados) usando técnicas de desenvolvimento de ambiente local. A Equipe do parceiro fornecerá aos parceiros de ISV um ambiente de sandbox onde poderão implantar o Conector de AEM em um aplicativo baunilha para garantir o funcionamento.
