---
title: Implementação de um conector do AEM
description: Implementação de um conector do AEM
translation-type: tm+mt
source-git-commit: 69756d6831678151b0e8eb73db81113d49f17447
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 9%

---


Implementação de um conector do AEM
=============================

As referências úteis para a criação de [Conectores do AEM](https://www.adobe.io/apis/experiencecloud/aem/aemconnectors.html) são fornecidas a seguir e devem ser lidas em conjunto com orientações sobre [envio](submit.md) e [manutenção](maintain.md) de conectores.

Observe que uma licença de desenvolvedor para AEM pode ser obtida por meio do Programa [Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

Padrões de integração comuns
---------------------------

AEM é uma solução de gerenciamento de experiência na Web de ponta e oferta muitas áreas potenciais de integrações. Padrões comuns de integração incluem:

* A extrair dados de um sistema externo para AEM. Por exemplo, exportar informações de contato de um CRM para disponibilizá-las a uma audiência mais ampla visitando um site com capacidade para AEM.  As implementações devem usar os Serviços [](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#scheduled-jobs)Agendados do Sling, que garantem que a ordem de produção seja executada mesmo se os container estiverem inativos. O código deve ser projetado para supor que a tarefa possa ser acionada mais de uma vez.
* Exportar dados de AEM para um sistema externo. Por exemplo, as configurações de subscrição de boletins informativos enviadas em um site alimentado por AEM para um CRM.
* Recuperando ativos do AEM. Por exemplo, um Sistema de Gestão de conteúdo externo (CMS) que faz referência a um ativo armazenado no AEM Assets. Ou como outro exemplo, um sistema PIM vinculado a uma imagem no AEM Assets.
* Armazenando ativos na infraestrutura AEM. Por exemplo, um sistema de gerenciamento de Recursos de marketing (MRM) armazenando um ativo aprovado no AEM Assets.
* Configuração e renderização de um componente de interface personalizada. Por exemplo, permita que um autor arraste e solte um componente de vídeo e configure um vídeo específico para ser reproduzido no site ativo.
* Agir em um ativo com um serviço de parceiro. Por exemplo, enviar um ativo para uma plataforma de vídeo quando uma página é publicada.
* Analisando um site, página ou ativo no console de administração AEM. Por exemplo, fazer recomendações de SEO para uma página existente ou não publicada.
* Acesso de nível de página aos dados do usuário mantidos por um serviço externo. Por exemplo, aproveite as informações demográficas para personalizar a experiência do site. Leia sobre o ContextHub, uma estrutura para armazenar, manipular e apresentar dados de contexto.
* Traduzindo cópia do site ou metadados do ativo. Consulte o Conector [do Bootstrap da Estrutura de Tradução](https://github.com/Adobe-Marketing-Cloud/aem-translation-framework-bootstrap-connector) AEM para obter exemplos de código usando a Estrutura de Tradução AEM, que é a implementação preferencial dos conectores de tradução.


Documentação útil
--------------------

Experience Manager como uma [documentação](../overview/introduction.md) de Cloud Service fornece informações valiosas sobre o desenvolvimento em AEM. Abaixo estão alguns tópicos e referências técnicas específicos que podem ser úteis ao implementar um conector AEM:

* Amostras [AEM serviços de consultoria por Adobe (ACS) para obter](http://adobe-consulting-services.github.io/acs-aem-samples/) códigos bem comentados que ajudam a educar AEM desenvolvedores
* Os vários links de documentação na seção Padrões de integração comuns deste artigo

Recursos da comunidade
--------------------

Além da documentação estática acima, a Adobe e os recursos de oferta da comunidade AEM ajudam a trazer um conector ao mercado:

* O Fórum [de](http://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.html) AEM da Comunidade do Adobe é um site ativo onde seus colegas fazem perguntas e respondem a perguntas
* Recursos técnicos adicionais de Adobe estão disponíveis para determinados níveis de parceiros. Saiba mais sobre o Programa [](https://partners.adobe.com/exchangeprogram/experiencecloud)Adobe Exchange.
* Se sua organização deseja obter ajuda de implementação, considere a equipe de [Serviços profissionais](http://www.adobe.com/br/experience-cloud/consulting-services.html) da Adobe ou consulte o [Localizador de parceiros de soluções](https://solutionpartners.adobe.com/home/partnerFinder.html) para obter uma lista de parceiros da Adobe em todo o mundo

Regras de estrutura do pacote
-----------------------

Para suportar implantações contínuas, AEM como pacotes Cloud Service, dos quais os conectores são exemplos, têm uma separação estrita entre o conteúdo &quot;imutável&quot; e &quot;mutável&quot;. Os pacotes devem ser limpos e separados entre os que incluem:

* `/apps`
* `/content` e `/conf`

Os conectores devem seguir essas diretrizes de embalagem, descritas [neste artigo](/help/implementing/developing/introduction/aem-project-content-package-structure.md). Os conectores existentes também devem ser refatorizados para estarem em conformidade.

Além disso, somente o Adobe deve gravar código `/libs`, com clientes e parceiros que escrevem para `/apps`.

Os conectores existentes também podem precisar ser refatorizados para mover qualquer configuração que tenha sido colocada `/etc` em outras pastas de nível superior, como `/conf`. Isso é descrito na documentação [da](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)AEM.

Recomenda-se que a maioria do código do conector seja colocada `/apps/connectors/<vendor>` para promover uma estrutura de repositório limpa para clientes que tenham vários conectores.

Configurações dos serviços em nuvem
-----------------------------

Um aspecto da implementação do conector é o código que suporta a configuração do conector. Esse código faz com que um cartão com o nome do conector apareça em Ferramentas > Operações > Cloud Services. Quando clicado, um navegador [de](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) configuração é exibido, onde o cliente seleciona a pasta pai para conter a configuração do conector. O código do conector deve resultar em um formulário com todas as propriedades que devem ser configuradas, armazenando os valores em uma pasta de configuração em `/conf`. Posteriormente, essa pasta pode ser selecionada na guia de propriedades Sites ou na guia de propriedades Ativos.


Configurações sensíveis ao contexto
-----------------------------

[As Configurações](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) sensíveis ao contexto permitem colocar a configuração em camadas em diferentes pastas, incluindo `/libs`, `/apps`e subpastas em `/conf` `/conf`. Suporta herança para que um cliente possa configurar a configuração global e fazer alterações específicas para cada microsite. Como é possível aproveitar esse recurso para Configurações de Cloud Services, o código do conector deve fazer referência à configuração usando a API de configuração sensível ao contexto em vez de fazer referência a um nó de configuração específico.

Se configurações modificadas forem usadas no Conector, arquitete o Conector para lidar com a inclusão/união de futuras atualizações nas configurações padrão fornecidas pelo Conector com quaisquer configurações do cliente. Lembre-se de que alterar o conteúdo personalizado (como alterado pelo cliente) ou a configuração sem aviso e consentimento do cliente pode quebrar (ou criar um comportamento inesperado) com seu Conector.

Práticas recomendadas de codificação
----------------------

Como a AEM como Cloud Service é uma solução nativa da Cloud, há algumas diretrizes que podem afetar as estratégias de código de um conector. Consulte [AEM como diretrizes](/help/implementing/developing/introduction/development-guidelines.md) de desenvolvimento de Cloud Service para obter mais detalhes.

Teste do conector AEM
-------------------------

Novos conectores devem ser criados (ou conectores existentes modificados) usando técnicas locais de desenvolvimento de ambientes. A Equipe do parceiro fornecerá aos parceiros ISV um ambiente de caixa de proteção onde eles poderão implantar seu conector de AEM em um aplicativo baunilha para garantir que ele funcione.
