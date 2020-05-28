---
title: Fase de execução
description: Fase de execução
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 7%

---


# Execução {#execution-phase}

Antes de start da fase de execução, você deve estar a bordo do serviço de nuvem. Você também precisa se familiarizar com o Cloud Manager, pois ele é o único mecanismo para implantar o código no serviço da AEM Cloud.

O Cloud Manager permite que as organizações gerenciem automaticamente o AEM na nuvem. Inclui uma estrutura de integração contínua e entrega contínua (CI/CD) que permite que as equipes de TI e os parceiros de implementação acelerem a entrega de personalizações ou atualizações, sem comprometer o desempenho ou a segurança.

Consulte os seguintes recursos abaixo para obter mais detalhes:

* [Integração com o Experience Manager como um serviço](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/home.html) da Cloud para entender os recursos de autoajuda sobre a integração do Experience Manager como um serviço da Cloud.

* [Integração do Git com o Adobe Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) para saber mais sobre o uso de um repositório do Single Git para implantar o código.

* [Configuração](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/security/ims-support.html#aem-configuration) do Adobe Experience como um serviço em nuvem para saber mais sobre como gerenciar produtos e acesso do usuário no Admin Console.


## Introdução {#introduction}

As etapas exatas da sua transição para o serviço da Cloud dependem dos sistemas que você adquiriu e das práticas de ciclo de vida do desenvolvimento de software que você segue.

A figura a seguir mostra as principais etapas envolvidas na fase de Execução:

![image](/help/move-to-cloud-service/assets/exec-image1.png)

## Transferência de conteúdo {#content-transfer}

Para transferir o conteúdo da sua instância AEM atual para a instância do serviço em nuvem, use a Ferramenta de transferência de conteúdo da Adobe.

Com essa ferramenta, você pode especificar o subconjunto de conteúdo desejado que deseja transferir da sua instância de AEM de origem para a instância de serviço da AEM Cloud.

>[!NOTE]
>Recomenda-se fazer upups frequentes de conteúdo diferencial para encurtar o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar em funcionamento no Cloud Service.

Consulte a Ferramenta [de transferência de](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md) conteúdo para obter mais detalhes.

>[!IMPORTANT]
>O requisito mínimo do sistema para a Ferramenta de transferência de conteúdo é AEM 6.3 + e JAVA 8. Se você estiver em uma versão inferior do AEM, precisará atualizar seu repositório de conteúdo para o AEM 6.5 para usar a Ferramenta de transferência de conteúdo.

## Refatoração de código {#code-refactor}

Desenvolver e executar o código no AEM como um serviço de nuvem requer uma alteração no conjunto de ideias. Observe que o código deve ser resiliente, especialmente porque uma instância pode ser interrompida a qualquer momento. O código em execução no serviço de nuvem deve estar ciente de que ele está sempre em execução em um cluster. Isso significa que há sempre mais de uma instância em execução.

Determinadas alterações são necessárias para que os projetos do AEM Maven sejam compatíveis com o AEM como um serviço em nuvem. O AEM como um serviço em nuvem exige uma separação de *conteúdo* e *código* em pacotes separados para implantação no AEM.

* `/apps` e `/libs` são consideradas áreas imutáveis do AEM, pois não podem ser alteradas (criar, atualizar, excluir) após o AEM ser iniciado (isto é, no tempo de execução). Qualquer tentativa de alterar uma área imutável no tempo de execução falhará.

* Tudo o resto no repositório, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp` , etc. são todas áreas mutáveis, o que significa que podem ser alteradas em tempo de execução.

Consulte a Estrutura [do pacote](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure) recomendada para obter mais detalhes.

Há algumas diretrizes de desenvolvimento adicionais que você precisa conhecer ao desenvolver no AEM como um serviço em nuvem. Consulte [AEM como Diretrizes](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) de desenvolvimento de serviços em nuvem para saber mais.

Na fase de planejamento, você deve ter uma lista de áreas que precisam ser refatorizadas para serem compatíveis com o serviço em nuvem. Você também deve revisar as Diretrizes [de](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) desenvolvimento para obter mais detalhes sobre como redimensionar e otimizar o código para ir para o Serviço de nuvem.

Para ajudar a acelerar algumas de suas tarefas de refatoração de código, você pode usar as seguintes ferramentas:

* [Migração do fluxo de trabalho do ativo](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Dispatcher Converter](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [Ferramentas de Modernização](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

É recomendável refatorar e testar o código localmente antes de enviá-lo para um ambiente de serviço em nuvem por meio do Git do Gerenciador de nuvem.

Consulte a documentação do SDK [do](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) AEM para saber mais.

Alguns recursos adicionais estão listados abaixo:

* Assista a instalação do Dispatcher SDK para entender como instalar o Dispatcher SDK:

   > [!VIDEO](https://video.tv.adobe.com/v/30601)

* Assista a Configuração do Dispatcher SDK para entender como configurar o Dispatcher SDK:

   > [!VIDEO](https://video.tv.adobe.com/v/30602)

* Consulte a documentação Configuração [de desenvolvimento](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) local para configurar um ambiente de desenvolvimento local


Para gerenciar o desenvolvimento contínuo do código no AEM ativo, juntamente com a tarefa de refatoração de código como parte da jornada de transição, é recomendável programar um período de congelamento de código até concluir a reestruturação do projeto Maven para ser compatível com o AEM como um serviço em nuvem.

Quando a reestruturação do projeto estiver concluída, você poderá retomar o desenvolvimento do novo código com base nessa nova estrutura. Isso reduzirá as falhas de pipeline do Gerenciador de nuvem durante a implantação e o teste do código.

>[!NOTE]
>As tarefas Transferência de conteúdo e Refatoração de código não têm de ser feitas sequencialmente. Essas tarefas podem ser feitas independentemente umas das outras. No entanto, a estrutura correta do projeto é necessária para garantir que o conteúdo seja renderizado com êxito no seu ambiente do serviço em nuvem.

## Práticas recomendadas para implantação e teste de código {#best-practices}

As execuções de pipeline do Cloud Manager for Cloud Services oferecerão suporte à execução de testes executados em relação ao ambiente stage.

Consulte Teste [de qualidade de](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing) código para saber mais sobre como escrever scripts de teste e cobertura recomendada de pelo menos 50%.

Além disso, consulte [Como entender regras](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/custom-code-quality-rules.html) de qualidade de código personalizadas para saber mais sobre as regras de qualidade de código personalizadas executadas pelo Gerenciador de nuvem criado com base nas práticas recomendadas da engenharia do AEM.

O uso do Cloud Manager é o único mecanismo para implantar o código em ambientes do serviço de nuvem.

Siga os recursos abaixo para saber como usar o Cloud Manager para gerenciar e implantar seu código.

* [Gerenciamento de ambientes](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [Configuração do seu pipeline CI-CD](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [Implantação do código](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)

## Práticas recomendadas para preparação contínua {#go-live}

Para garantir uma ativação do AEM como um serviço de nuvem sem problemas e bem-sucedida, você deve considerar executar as seguintes etapas:

* Programar código e período de congelamento de conteúdo
* Executar conteúdo final de cima
* Concluir iterações de teste
* Executar testes de desempenho e segurança
* Corte
