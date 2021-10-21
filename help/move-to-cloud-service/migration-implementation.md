---
title: Fase de implementação
description: Fase de implementação
exl-id: 176dd79d-0d72-443c-87db-dab24fb48b96
source-git-commit: 3b0b1a192e25958b3b049893f5b7e1001e071f69
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 90%

---

# Implementação {#implementation-phase}

Antes de iniciar a fase de execução, você deve estar integrado ao Cloud Service. Você também precisa se familiarizar com o Cloud Manager, pois ele é o único mecanismo para implantar código no AEM Cloud Service.

O Cloud Manager permite que as organizações gerenciem automaticamente o AEM na Nuvem. Inclui uma estrutura de integração contínua e entrega contínua (CI/CD) que permite que as equipes de TI e os parceiros de implementação acelerem a entrega de personalizações ou atualizações, sem comprometer o desempenho ou a segurança.

Consulte os seguintes recursos abaixo para obter mais detalhes:

* [Integração com o Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html) para compreender recursos de autoajuda sobre integração do Experience Manager as a Cloud Service.

* [Integração do Git com o Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) para saber mais sobre o uso de um único repositório Git para implantar código.

* [Configuração do Adobe Experience as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#aem-configuration) para saber mais sobre como gerenciar produtos e o acesso dos usuários no Admin Console.


## Introdução {#introduction}

As etapas precisas da sua transição para o Cloud Service dependem dos sistemas que você adquiriu e das práticas de ciclo de vida de desenvolvimento de software seguidas.

A figura a seguir mostra as principais etapas envolvidas na fase de Execução:

![imagem](/help/move-to-cloud-service/assets/exec-image1.png)

## Transferência de conteúdo {#content-transfer}

Para transferir o conteúdo da sua instância do AEM atual para a instância do Cloud Service, use a ferramenta Transferência de conteúdo da Adobe.

Com essa ferramenta, você pode especificar o subconjunto de conteúdo desejado que deseja transferir da instância de origem do AEM para a instância do AEM Cloud Service.

>[!NOTE]
>É recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Consulte a [Ferramenta Transferência de conteúdo](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md) para obter mais detalhes.

>[!IMPORTANT]
>O requisito mínimo do sistema para a ferramenta Transferência de conteúdo é o AEM 6.3 + e JAVA 8. Se você estiver em uma versão inferior do AEM, precisará atualizar seu repositório de conteúdo para o AEM 6.5 para usar a ferramenta Transferência de conteúdo.

## Refatoração do código {#code-refactor}

O desenvolvimento e a execução de código no AEM as a Cloud Service requer uma mudança de mentalidade. Vale lembrar que o código deve ser resiliente, especialmente porque uma instância pode ser interrompida a qualquer momento. O código em execução no Cloud Service deve reconhecer o fato de que ele está sempre em execução em um cluster. Isso significa que sempre há mais de uma instância em execução.

Certas alterações são necessárias para que projetos do AEM Maven sejam compatíveis com o AEM as a Cloud Service. O AEM as a Cloud Service requer uma separação de *conteúdo* e *código* em pacotes discretos para implantação no AEM.

* `/apps` e `/libs` são consideradas áreas imutáveis do AEM, pois não podem ser alteradas (criar, atualizar, excluir) após o AEM ser iniciado (isto é, no tempo de execução). Qualquer tentativa de alterar uma área imutável no tempo de execução falhará.

* Todo o restante no repositório, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp` , etc. são áreas mutáveis, o que significa que podem ser alteradas em tempo de execução.

Consulte [Estrutura de pacotes recomendada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure) para obter mais detalhes.

Existem algumas diretrizes de desenvolvimento adicionais que você precisa conhecer ao desenvolver no AEM as a Cloud Service. Para saber mais, consulte [Diretrizes de desenvolvimento do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html).

Na fase de Planejamento, você deve ter uma lista de áreas que precisam ser refatoradas para serem compatíveis com o Cloud Service. Você também deve rever as [Diretrizes de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html) para obter mais detalhes sobre como refatorar e otimizar o código para migrar para o Cloud Service.

Para ajudar a acelerar algumas das tarefas de refatoração de código, você pode usar as seguintes ferramentas:

* [Migração de fluxo de trabalho de ativos](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Conversor do Dispatcher Converter](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [Ferramentas de Modernização](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

É recomendável refatorar e testar o código localmente antes de enviá-lo para um ambiente do Cloud Service por meio do Git do Cloud Manager.

Consulte a documentação do [SDK do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) para saber mais.

Alguns recursos adicionais estão listados abaixo:

* Assista Instalar o SDK do Dispatcher para entender como instalar o SDK do Dispatcher:

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Assista Configurar o SDK do Dispatcher para entender como configurar o SDK do Dispatcher:

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

* Consulte a documentação de [Configuração de desenvolvimento local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) para configurar um ambiente de desenvolvimento local


Para gerenciar o desenvolvimento contínuo do seu código no AEM ativo, juntamente com a tarefa de refatoração de código como parte da sua jornada de transição, é recomendável programar um período de congelamento do código até você concluir a reestruturação do seu projeto Maven para que ele seja compatível com o AEM as a Cloud Service.

Depois que a reestruturação do projeto estiver concluída, você poderá retomar o desenvolvimento de novos códigos com base nessa nova estrutura. Isso reduzirá as falhas de pipeline do Cloud Manager durante os testes e a implantação do código.

>[!NOTE]
>As tarefas de Transferência de conteúdo e Refatoração do código não precisam ser realizadas sequencialmente. Elas podem ser realizadas independentemente uma da outra. No entanto, é necessário ter a estrutura correta do projeto para garantir que o conteúdo seja renderizado com êxito no seu ambiente do Cloud Service.

## Práticas recomendadas para testes e implantação do código {#best-practices}

As execuções de pipeline do Cloud Manager para o Cloud Services oferecerão suporte à execução de testes que são executados no ambiente de preparo.

Consulte [Testes de qualidade do código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing) para saber mais sobre como escrever scripts de teste e a cobertura recomendada de pelo menos 50%.

Além disso, consulte [Noções básicas sobre regras de qualidade de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md) para saber mais sobre as regras de qualidade de código personalizadas executadas pelo Cloud Manager e criadas com base nas práticas recomendadas do AEM Engineering.

O uso do Cloud Manager é o único mecanismo para implantar código em ambientes do Cloud Service.

Siga os recursos abaixo para saber como usar o Cloud Manager para gerenciar e implantar seu código.

* [Gerenciamento de ambientes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [Configurar seu pipeline de CI-CDConfiguração do seu pipeline CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [Implantação do código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)


