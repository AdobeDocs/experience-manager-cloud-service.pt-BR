---
title: Alterações notáveis no Adobe Experience Manager (AEM) como um serviço em nuvem
description: Alterações notáveis no Adobe Experience Manager (AEM) como um serviço em nuvem
translation-type: tm+mt
source-git-commit: e76de9b84931dced6383570e384ffdb6fb334daf

---


# Alterações notáveis no Adobe Experience Manager (AEM) como um serviço em nuvem {#notable-changes-aem-cloud}

O serviço da AEM Cloud oferece muitos recursos e possibilidades novos para gerenciar seus projetos do AEM. No entanto, há várias diferenças entre os Sites AEM no local ou no Serviço gerenciado da Adobe em comparação ao serviço da AEM Cloud. Este documento destaca as diferenças importantes.

>[!NOTE]
>Este documento destaca as alterações notáveis no AEM como um todo. Para obter as alterações específicas da solução, consulte:
>
>* [Alterações importantes no AEM Sites no serviço da AEM Cloud](/help/sites-cloud/sites-cloud-changes.md)
>* [Alterações notáveis nos ativos AEM no serviço da AEM Cloud](/help/assets/assets-cloud-changes.md)


As principais diferenças encontram-se nas seguintes áreas:

* [/apps e /libs são imutáveis no tempo de execução](#apps-libs-immutable)
* [Pacotes e configurações OSGi devem ser baseados em repositório](#osgi)
* [Alterações no repositório de publicação não são permitidas](#changes-to-publish-repo)
* [Não são permitidos modos de execução personalizados](#custom-runmodes)
* [Remoção dos agentes de replicação](#replication-agents)
* [Remoção da interface clássica](#classic-ui)
* [Entrega do lado da publicação](#publish-side-delivery)
* [Manuseio e entrega de ativos](#asset-handling)

## /apps e /libs são imutáveis no tempo de execução {#apps-libs-immutable}

Qualquer conteúdo e subpastas em `/apps` e `/libs` é somente leitura. Qualquer recurso ou código personalizado que espera fazer alterações não fará isso. Será retornado um erro de que esse conteúdo é somente leitura e a operação de gravação não pôde ser concluída. Isso tem impacto em várias áreas do AEM:

* Nenhuma alteração é `/libs` permitida.
   * Essa não é uma regra nova, no entanto, ela não foi imposta em versões anteriores no local do AEM.
* Ainda são permitidas sobreposições para áreas em `/libs` que podem ser sobrepostas dentro `/apps`.
   * Essas sobreposições devem vir do Git por meio do pipeline CI/CD.
* As informações de design do modelo estático armazenadas na não `/apps` podem ser editadas pela interface do usuário.
   * É recomendável que você utilize Modelos editáveis.
   * Se os Modelos estáticos ainda forem obrigatórios, as informações de configuração devem vir do Git por meio do pipeline CI/CD.
* As configurações de implantação MSM Blueprint e MSM personalizado devem ser instaladas a partir do Git por meio do pipeline CI/CD.
* As mudanças na tradução do I18n precisam vir do Git através do pipeline de CI/CD.

## Pacotes e configurações OSGi devem ser baseados em repositório {#osgi}

O console da Web, usado em versões anteriores do AEM para alterar as configurações do OSGi, não está disponível no serviço da AEM Cloud. Por conseguinte, as alterações ao OSGi devem ser introduzidas através do pipeline de IC/CD.

* As alterações nas configurações do OSGi só podem ser feitas via persistência de Git como configurações OSGi baseadas em JCR.
* Os pacotes OSGi novos ou atualizados devem ser introduzidos via Git como parte do processo de construção do pipeline de CI/CD.

## Alterações no repositório de publicação não são permitidas {#changes-to-publish-repo}

Alterações diretas no repositório de publicação não são permitidas no serviço da AEM Cloud. Em versões anteriores do AEM ou AEM local no AMS, alterações de código podem ser feitas diretamente no repositório de publicação, por exemplo, para criar usuários, atualizar perfis de usuário e criar nós. Isso não é mais possível e pode ser atenuado das seguintes maneiras:

* Para configuração baseada em conteúdo e conteúdo: faça as alterações na instância do autor e publique-as.
* Para código e configuração: faça as alterações no repositório GIT e execute o pipeline CI/CD para implementá-las.
* Para dados relacionados ao usuário, como envios de formulário ou dados de perfil: use o Serviço de perfil unificado da plataforma da Experience Cloud ou de outra loja com reconhecimento de sessão de terceiros.

## Não são permitidos modos de execução personalizados {#custom-runmodes}

Os seguintes modos de execução são fornecidos prontos para uso para o serviço da AEM Cloud:

* `author`
* `publish`
* `prod`
* `author.prod`
* `publish.prod`
* `stage`
* `author.stage`
* `publish.stage`
* `dev`
* `author.dev`
* `publish.dev`

Modos de execução adicionais ou personalizados não são possíveis no serviço da AEM Cloud.

## Remoção dos agentes de replicação {#replication-agents}

No serviço da AEM Cloud, o conteúdo é publicado usando a Distribuição [de conteúdo](https://sling.apache.org/documentation/bundles/content-distribution.html)Sling. Os agentes de replicação usados em versões anteriores do AEM não são mais usados ou fornecidos, o que pode afetar as seguintes áreas de projetos existentes do AEM:

* Fluxos de trabalho personalizados que enviam conteúdo para agentes de replicação de servidores de visualização, por exemplo.
* Personalização para agentes de replicação para transformar conteúdo
* Usar replicação reversa para trazer o conteúdo da publicação de volta para o autor

## Remoção da interface clássica {#classic-ui}

A interface clássica não está mais disponível no serviço da AEM Cloud.

## Entrega do lado da publicação {#publish-side-delivery}

A aceleração HTTP, incluindo o CDN e o gerenciamento de tráfego para os serviços de autor e publicação, é fornecida por padrão no serviço da AEM Cloud.

Para a transição de projetos do AMS ou de uma instalação local, a Adobe recomenda utilizar a CDN integrada, pois os recursos no serviço da AEM Cloud são otimizados para a CDN fornecida.

## Manuseio e entrega de ativos {#asset-handling}

O upload, o tratamento e o download de ativos foram otimizados no serviço da AEM Cloud para serem mais eficientes, permitindo um melhor dimensionamento e uploads e downloads mais rápidos. No entanto, isso pode afetar alguns códigos personalizados existentes.

* O fluxo de trabalho padrão **DAM Asset Update** em versões anteriores do AEM não está mais disponível.
* Os componentes do site que fornecem um binário **sem transformação** devem usar o download direto.
   * O servlet Sling GET foi alterado para fazer isso por padrão.
* Os componentes do site que fornecem um binário **com transformação** (por exemplo, redimensionamento via servlet) podem continuar a operar como têm.
* Os ativos que entram pelo Gerenciador de pacotes exigem o reprocessamento manual usando a ação **Reprocessar ativos** na interface Ativos.
