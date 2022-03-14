---
title: Implementação de um conector do AEM
description: Implementação de um conector do AEM
exl-id: 70024424-8c52-493e-bbc9-03d238b8a5f5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 10%

---

Implementação de um conector do AEM
=============================

As referências úteis para a criação de [Conectores do AEM](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) são fornecidas a seguir e devem ser lidas em conjunto com orientações sobre [envio](submit.md) e [manutenção](maintain.md) de conectores.

Observe que é possível obter uma licença de desenvolvedor para AEM por meio do [Programa de troca de Adobe](https://partners.adobe.com/exchangeprogram/experiencecloud).

Padrões comuns de integração
---------------------------

O AEM é uma solução de gerenciamento de experiência online de ponta e oferece muitas áreas em potencial de integrações. Padrões comuns de integração incluem:

* Extraindo dados de um sistema externo para o AEM. Por exemplo, exportando informações de contato de um CRM para torná-lo disponível para um público-alvo maior que visita um site alimentado por AEM.  As implementações devem usar o [Trabalhos agendados](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs), que garante que a tarefa seja executada mesmo se os contêineres estiverem inativos. O código deve ser projetado para supor que a tarefa possa ser acionada mais de uma vez.
* Exportação de dados do AEM para um sistema externo. Por exemplo, as configurações de assinatura do boletim informativo enviadas em um site alimentado por AEM para um CRM.
* Recuperação de ativos do AEM. Por exemplo, um Sistema de gerenciamento de conteúdo externo (CMS) que faz referência a um ativo armazenado no AEM Assets. Ou como outro exemplo, um sistema PIM vinculado a uma imagem no AEM Assets.
* Armazenando ativos na infraestrutura do AEM. Por exemplo, um sistema de Gestão de Recursos de Marketing (MRM) armazenando um ativo aprovado no AEM Assets.
* Configuração e renderização de um componente de interface de usuário personalizada. Por exemplo, permita que um autor arraste e solte um componente de vídeo e configure um vídeo específico para ser reproduzido no site ativo.
* Atuando em um ativo com um serviço de parceiro. Por exemplo, enviar um ativo para uma plataforma de vídeo quando uma página é publicada.
* Análise de um site, página ou ativo no Admin Console AEM. Por exemplo, fazer recomendações de SEO para uma página existente ou não publicada.
* Acesso ao nível da página a dados do usuário mantidos por um serviço externo. Por exemplo, aproveite as informações demográficas para personalizar a experiência do site. Leia sobre o ContextHub, uma estrutura para armazenar, manipular e apresentar dados de contexto.
* Tradução da cópia do site ou metadados do ativo. Consulte a [Conector de Bootstrap da Estrutura de Tradução AEM](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) para código de exemplo usando a Estrutura de tradução de AEM, que é a implementação preferida dos conectores de tradução.


Documentação útil
--------------------

Experience Manager as a Cloud Service [documentação](../overview/introduction.md) O fornece informações valiosas sobre o desenvolvimento no AEM. Abaixo estão alguns tópicos e referências técnicas específicos que podem ser úteis ao implementar um conector de AEM:

* Serviços Adobe Consulting (ACS) [Exemplos de AEM](http://adobe-consulting-services.github.io/acs-aem-samples/) para código bem comentado para ajudar a educar desenvolvedores de AEM
* Os vários links de documentação na seção Padrões comuns de integração deste artigo

Recursos da comunidade
--------------------

Além da documentação estática acima, o Adobe e a comunidade de AEM oferecem recursos para ajudar a trazer um conector para o mercado:

* A comunidade do Adobe [Fórum AEM](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) é um site ativo no qual seus colegas fazem perguntas e respondem a perguntas
* Recursos técnicos adicionais do Adobe estão disponíveis para determinados níveis de parceiros. Saiba mais sobre o [Programa de troca de Adobe](https://partners.adobe.com/exchangeprogram/experiencecloud).
* Se sua organização deseja obter ajuda de implementação, considere a equipe de [Serviços profissionais](http://www.adobe.com/br/experience-cloud/consulting-services.html) da Adobe ou consulte o [Localizador de parceiros de soluções](https://solutionpartners.adobe.com/home/partnerFinder.html) para obter uma lista de parceiros da Adobe em todo o mundo

Regras de estrutura do pacote
-----------------------

Para oferecer suporte a implantações móveis, AEM pacotes as a Cloud Service, dos quais os conectores são exemplos, têm uma separação estrita entre conteúdo &quot;imutável&quot; e &quot;mutável&quot;. Os pacotes devem ser claramente separados entre aqueles que incluem:

* `/apps`
* `/content` e `/conf`

Os conectores devem seguir essas diretrizes de embalagem, descritas em [este artigo](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Os conectores existentes também devem ser refatorados para estarem em conformidade.

Além disso, somente o Adobe deve gravar o código no `/libs`, com clientes e parceiros escrevendo em `/apps`.

Os conectores existentes também podem precisar ser refatorados para mover qualquer configuração que tenha sido colocada `/etc` em outras pastas de nível superior, como `/conf`. Esta reestruturação foi realizada no âmbito do AEM 6.5 e é descrita no [Documentação do AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=pt-BR).

Recomenda-se que a maioria do código do conector seja colocada em `/apps/connectors/<vendor>` para promover uma estrutura de repositório limpa para clientes que têm vários conectores.

Configurações dos serviços em nuvem
-----------------------------

Um aspecto da implementação do conector é o código que suporta a configuração do conector. Esse código faz com que um cartão com o nome do conector apareça em Ferramentas > Operações > Cloud Services. Quando clicado, uma [navegador de configuração](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) aparece onde o cliente seleciona a pasta pai para conter a configuração do conector. O código do conector deve resultar em um formulário com todas as propriedades que devem ser configuradas, armazenando os valores em uma pasta de configuração em `/conf`. Posteriormente, essa pasta pode ser selecionada na guia de propriedades Sites ou na guia de propriedades de Ativos.


Configurações sensíveis ao contexto
-----------------------------

[Configurações sensíveis ao contexto](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) permite criar camadas de configuração em diferentes pastas, incluindo `/libs`, `/apps`, `/conf` e subpastas em `/conf`. Ele suporta herança para que um cliente possa configurar a configuração global enquanto faz alterações específicas para cada microsite. Como é possível aproveitar esse recurso para configurações do Cloud Services, o código do conector deve fazer referência à configuração usando a API de configuração sensível ao contexto, em vez de fazer referência a um nó de configuração específico.

Se as configurações modificadas forem usadas no Conector, arquive o Conector para lidar com incluindo/mesclando qualquer atualização futura nas configurações padrão fornecidas pelo Conector com qualquer configuração de cliente. Lembre-se de que alterar o conteúdo personalizado (como em alterado pelo cliente) ou a configuração sem aviso e consentimento do cliente pode quebrar (ou criar comportamento inesperado) com seu Conector.

Práticas recomendadas de codificação
----------------------

Como AEM as a Cloud Service é uma solução nativa em nuvem, há algumas diretrizes que podem afetar as estratégias de código de um conector. Consulte [AEM Diretrizes de desenvolvimento as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md) para obter mais detalhes.

Teste do conector de AEM
-------------------------

Novos conectores devem ser criados (ou conectores existentes modificados) usando técnicas de desenvolvimento de ambiente local. A Equipe do parceiro fornecerá aos parceiros de ISV um ambiente de sandbox onde poderão implantar o Conector de AEM em um aplicativo baunilha para garantir o funcionamento.
