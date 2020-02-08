---
title: Introdução à arquitetura do Adobe Experience Manager como um serviço em nuvem
description: 'Introdução à arquitetura do Adobe Experience Manager como um serviço em nuvem. '
translation-type: tm+mt
source-git-commit: 5a846d34ee094e7d2f7fc71dbeef65f3fa58e86c

---


# Uma introdução à arquitetura do Adobe Experience Manager como um serviço em nuvem {#an-introduction-to-the-architecture-adobe-experience-manager-as-a-cloud-service}

O Adobe Experience Manager (AEM) como um serviço em nuvem resultou em alterações na arquitetura.

## Dimensionamento {#scaling}

O AEM como serviço de nuvem agora tem:

* Uma arquitetura dinâmica com um número variável de imagens AEM.

![Arquitetura dinâmicaArquitetura](assets/concepts-01.png "dinâmica")

Esta arquitetura:

* É dimensionado com base no tráfego *real* e na atividade *real* .

* Tem instâncias individuais que só são executadas quando necessário.

* Usa aplicativos modulares.

* Tem um cluster autor como padrão; isso evita a paralisação das tarefas de manutenção.

Isso permite o dimensionamento automático para padrões de uso variados:

![Dimensionamento automático para](assets/concepts-02.png "padrões de uso variadosDimensionamento automático para padrões de uso variados")

Para isso, todas as instâncias do AEM como um serviço em nuvem são criadas iguais, cada uma com as mesmas características de dimensionamento padrão em termos de número de nós, memória alocada e capacidade de computação alocada.

O AEM como um serviço em nuvem é baseado no uso de um mecanismo de orquestração que:

* Monitora constantemente o estado do serviço.

* Dimensiona dinamicamente cada uma das instâncias de serviço de acordo com as necessidades reais; aumentando ou diminuindo conforme apropriado.

Isso:

* É aplicável ao número de nós, à quantidade de memória e à capacidade alocada da CPU em cada nó.

* Permite que o AEM como um serviço em nuvem acomode seus padrões de tráfego à medida que eles mudam.

O dimensionamento de instâncias por locatário do serviço pode ser automático ou manual, nos dois eixos:

* Vertical: a memória alocada e a capacidade da CPU podem ser ampliadas ou reduzidas para um número fixo de nós.

* Horizontal: o número de nós para um determinado serviço pode ser aumentado ou diminuído.

## Ambientes {#environments}

>[!NOTE]
>
> Para obter mais informações, consulte [Implantação - modos de execução](/help/implementing/deploying/overview.md#runmodes)

O AEM como um serviço em nuvem é disponibilizado como instâncias individuais com cada instância representando um ambiente AEM completo. Há quatro tipos de ambientes disponíveis com o AEM como um serviço em nuvem:

* **Ambiente** de produção: hospeda os aplicativos para os profissionais de negócios.

* **Ambiente** de estágio: está sempre acoplado a um único ambiente de produção em uma relação 1:1. O ambiente stage é usado para vários testes de desempenho e qualidade antes que as alterações no aplicativo sejam encaminhadas para o ambiente de produção.

* **Ambiente** de desenvolvimento: permite que os desenvolvedores implementem aplicativos AEM nas mesmas condições de tempo de execução que os ambientes stage e production.

* **Ambiente** de demonstração: podem ser usados para avaliação, demonstração, protótipo e treinamento.

Os ambientes de desenvolvimento e demonstração são geralmente chamados de ambientes *não produtivos* .

## Programas {#programs}

Qualquer novo projeto do AEM está sempre vinculado a exatamente uma base de código específica, onde você pode armazenar configuração e código personalizado para o seu projeto. Essas informações são armazenadas em um repositório de código, acessível pelos clientes Git habituais, disponibilizados para você no momento em que novos programas são criados.

Um programa AEM é o contêiner que inclui:

|  Elemento do programa |  Número |
|--- |--- |
| Repositório de código (Git) |  1 |
| Imagem da linha de base (Sites ou Ativos) |  1 |
| Estágio e ambiente de produção definidos (1:1) | 0 ou 1 |
| Ambientes não produtivos (desenvolvimento ou demonstração) | 0 a N |
| Pipeline para cada ambiente | 0 ou 1 |

Dois tipos de programas estão inicialmente disponíveis para o AEM como um serviço em nuvem:

* Serviço de sites da AEM Cloud

* Serviço AEM Cloud Assets

Ambos permitem acesso a vários recursos e funcionalidades. A camada do autor conterá toda a funcionalidade Sites e Ativos para todos os programas, mas os programas Ativos não terão uma camada de publicação por padrão.

## Arquitetura de tempo de execução {#runtime-architecture}

Há vários componentes principais dessa nova arquitetura:

<!--- needs reworking -->

![AEM como um serviço em nuvem -](assets/concepts-03.png "Arquitetura de tempo de execuçãoAEM como um serviço em nuvem - Arquitetura de tempo de execução")

* Para AEM Sites como um serviço em nuvem:

   * Continua a existir o conceito de uma camada de criação e uma camada de publicação para cada ambiente (em um nível alto).

   * A camada do autor é feita de dois ou mais nós em um único cluster do autor. Ele é dimensionado automaticamente, dependendo da atividade de criação.

      * Autores/criadores de conteúdo fazem logon na camada de autor do AEM para criar, editar e gerenciar conteúdo.

      * O logon na camada do autor é gerenciado pelo Adobe Identity Management Services (IMS).

      * A integração e o processamento de ativos usam um Serviço de computação de ativos dedicado.
   * A camada de publicação é composta de dois ou mais nós em um único farm de publicação: podem operar independentemente uns dos outros. Cada nó consiste em um editor de AEM e um servidor da Web equipado com o módulo do Dispatcher de AEM. Ele é dimensionado automaticamente com as necessidades de tráfego do site.

      * Os usuários finais ou os visitantes do site visitam o site por meio do serviço de publicação de AEM.


* Para ativos AEM como um serviço em nuvem:

   * A arquitetura inclui apenas um ambiente de criação.

* Tanto a camada do autor quanto a camada de publicação leem e persistem no conteúdo de/para um Serviço de repositório de conteúdo.

   * A camada de publicação lê apenas o conteúdo da camada de persistência.

   * A camada do autor lê e grava conteúdo de e para a camada de persistência.

   * O armazenamento de blobs é compartilhado na camada de publicação e autor; os arquivos não são *movidos*.

   * Quando o conteúdo é aprovado da camada do autor, isso é uma indicação de que pode ser ativado, portanto, enviado para a camada de persistência da camada de publicação. Isso acontece por meio do serviço de replicação, um pipeline middleware. Este pipeline recebe o novo conteúdo, com os nós de serviço de publicação individuais a assinar o conteúdo enviado para o pipeline.

      >[!NOTE]
      >
      >For more details see [Replication](/help/operations/replication.md).

   * Desenvolvedores e administradores gerenciam o AEM como um aplicativo de serviço em nuvem usando um serviço de Integração contínua/Entrega contínua (CI/CD), disponibilizado pelo Gerenciador [da](/help/overview/what-is-new-and-different.md#cloud-manager)Cloud. Isso inclui implantações de código e configuração usando o pipeline CI/CD do Gerenciador de nuvem. Qualquer coisa relacionada ao monitoramento, manutenção e solução de problemas (por exemplo, arquivos de registro) é exposta aos clientes no Cloud Manager.

   * O acesso aos níveis de autor e publicação sempre ocorre por meio de um balanceador de carga. Isso está sempre atualizado com os nós ativos em cada uma das camadas.

   * Para a camada de publicação, um Serviço de Rede de entrega contínua (CDN) também está disponível como o primeiro ponto de entrada.

* Para instâncias de demonstração do AEM como um serviço em nuvem, a arquitetura é simplificada em um único nó do autor. Por conseguinte, não apresenta todas as características do ambiente normal de desenvolvimento, fase ou produção. Isso também significa que pode haver algum tempo de inatividade e que não há suporte para operações de backup/restauração.

## Arquitetura de implantação {#deployment-architecture}

O Cloud Manager gerencia todas as atualizações nas instâncias do AEM como um serviço em nuvem. É obrigatório, sendo a única maneira de criar, testar e implantar o aplicativo do cliente, tanto para o autor quanto para as camadas de publicação. Essas atualizações podem ser acionadas pela Adobe, quando uma nova versão do Serviço da AEM Cloud estiver pronta, ou pelo Cliente, quando uma nova versão de seu aplicativo estiver pronta.

Tecnicamente, isso é implementado devido ao conceito de um pipeline de implantação, acoplado a cada ambiente dentro de um programa. Quando um pipeline do Gerenciador de nuvem está em execução, ele cria uma nova versão do aplicativo do cliente, tanto para o autor quanto para os níveis de publicação. Isso é feito combinando os pacotes mais recentes do cliente com a imagem mais recente da linha de base da Adobe. Quando as novas imagens são criadas e testadas com êxito, o Cloud Manager automatiza totalmente o cutover para a versão mais recente da imagem, atualizando todos os nós de serviço usando um padrão de atualização contínua. Isso não resulta em tempo de inatividade para o serviço de autor ou publicação.

<!--- needs reworking -->

![AEM como um serviço em nuvem -](assets/concepts-04.png "Arquitetura de implantaçãoAEM como um serviço em nuvem - Arquitetura de implantação")

## Distribuição de conteúdo {#content-distribution}

O Adobe Experience Manager como um serviço em nuvem modificou a forma como o conteúdo de publicação funciona. Com o AEM como um serviço em nuvem, a estrutura de replicação de versões anteriores do AEM não é mais usada para publicar páginas (mover as alterações da instância do autor para as instâncias de publicação).

O AEM como um serviço em nuvem agora usa o recurso [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) para mover o conteúdo apropriado. Isso usa uma execução de serviço de pipeline em E/S da Adobe, que está fora do tempo de execução do AEM.

A configuração é automatizada, incluindo autoconfiguração automática quando nós de publicação são adicionados, removidos ou reciclados durante o tempo de execução.

Uma única solicitação de publicação ou cancelamento de publicação pode incluir vários recursos, mas retornará um único status aplicado a todos; será bem-sucedido para todos os recursos no serviço de publicação de AEM ou falhará para todos. Isso garante que os recursos dentro do serviço de publicação de AEM nunca estarão em um estado inconsistente.

**Diagrama da arquitetura de distribuição de conteúdo de alto nível**

![Diagrama da arquitetura de distribuição de conteúdo de alto nívelDiagrama da arquitetura de distribuição de conteúdo de alto nível](assets/architecture-diagram.png "")

## Principais desenvolvimentos {#key-evolutions}

A nova arquitetura do AEM como um serviço em nuvem apresenta algumas mudanças e inovações fundamentais em relação às gerações anteriores:

* Todos os arquivos (blobs) são carregados e servidos diretamente de um armazenamento de dados em nuvem. O fluxo associado de bits nunca passa pela JVM dos serviços de autor e publicação do AEM. Como resultado, os nós dos serviços de autor e publicação do AEM podem ser menores em tamanho e mais compatíveis com a expectativa de dimensionamento automático rápido. Para profissionais de negócios, isso resulta em uma experiência mais rápida ao carregar e baixar imagens, vídeos etc.

* Todas as operações que consistem em publicar conteúdo agora envolvem um pipeline seguindo um padrão de assinatura. O conteúdo publicado é enviado para várias filas no pipeline, nas quais todos os nós do serviço de publicação se inscrevem. Como resultado, a camada do autor não precisa estar ciente do número de nós no serviço de publicação; isso permite o dimensionamento automático rápido da camada de publicação.

* O conceito de um mestre dourado foi introduzido para automatizar o ciclo de vida dos nós de publicação. O mestre de ouro é um nó de publicação especializado, nunca acessado por nenhum usuário final e a partir do qual todos os nós do serviço de publicação são criados. Operações de manutenção, como compactação, são executadas no repositório de conteúdo anexado ao mestre dourado. Os nós de publicação são reciclados diariamente e não exigem qualquer tipo de manutenção de rotina; no passado, essa manutenção exigia algum tempo de inatividade, especialmente para a instância do autor.

* A arquitetura separa completamente o conteúdo do aplicativo do código e da configuração do aplicativo. Todos os códigos e configurações são praticamente imutáveis e são enviados para a imagem de linha de base usada para criar os vários nós dos serviços de autor e publicação. Como resultado, há uma garantia absoluta de que cada nó é idêntico, e as alterações no código e na configuração só podem ser feitas globalmente executando um pipeline do Gerenciador de nuvem.
