---
title: Configuração da equipe de desenvolvimento corporativa
description: Saiba como configurar e dimensionar sua equipe de desenvolvimento corporativo e veja como o AEM as a Cloud Service pode apoiar seu processo de desenvolvimento.
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1437'
ht-degree: 83%

---

# Configuração da equipe de desenvolvimento corporativa para o AEM as a Cloud Service {#enterprise-setup}

Saiba como configurar e dimensionar sua equipe de desenvolvimento corporativo e veja como o AEM as a Cloud Service pode apoiar seu processo de desenvolvimento.

## Introdução {#introduction}

Para oferecer suporte a clientes com configurações de desenvolvimento corporativo, o AEM as a Cloud Service integra-se totalmente ao Cloud Manager e a seus pipelines opinativos [de CI/CD criados com propósitos específicos](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Esses pipelines e serviços são criados com base nas práticas recomendadas, garantindo [testes completos e código de maior qualidade](/help/implementing/cloud-manager/code-quality-testing.md).

## Apoio do Cloud Manager à configuração de desenvolvimento de equipes corporativas {#cloud-manager}

Para garantir uma integração rápida, o Cloud Manager fornece tudo o que é necessário para começar a desenvolver experiências digitais imediatamente, incluindo um repositório Git para armazenar as personalizações que então são compiladas, verificadas e implantadas pelo Cloud Manager.

Usando o Cloud Manager, as equipes de desenvolvimento podem trabalhar para confirmar as alterações com frequência, sem depender da equipe da Adobe.

Três tipos de ambientes estão disponíveis no Cloud Manager.

* Desenvolvimento
* Fase
* Produção

O código pode ser implantado em ambientes de desenvolvimento usando um pipeline de não produção. Para ambientes de preparo e produção, que sempre se unem e, portanto, garantem a validação antes da implantação em produção como prática recomendada, um pipeline de produção usa [quality gates (portais de qualidade)](/help/implementing/cloud-manager/custom-code-quality-rules.md) para validar o código do aplicativo e as alterações de configuração.

O pipeline de produção primeiro implanta o código e a configuração no ambiente de preparo, testa o aplicativo e finalmente implanta no ambiente de produção.

Um SDK Cloud Service que é sempre atualizado com as melhorias mais recentes do AEM as a Cloud Service permite o desenvolvimento local utilizando diretamente o hardware local do desenvolvedor. Assim é possível um desenvolvimento rápido com tempos de resposta muito baixos. Assim, os desenvolvedores podem permanecer em seus ambientes locais familiares e escolher entre uma grande variedade de ferramentas de desenvolvimento, além de enviar para ambientes de desenvolvimento ou produção, quando bem entenderem.

O Cloud Manager é compatível com configurações flexíveis de várias equipes, que podem ser ajustadas para atender às necessidades de cada empresa. Para garantir implantações estáveis com várias equipes e, ao mesmo tempo, evitar situações em que uma equipe afeta a produção de todas as equipes, o pipeline opinativo do Cloud Manager sempre valida e testa o código de todas as equipes.

## Exemplo do mundo real {#real-world-example}

Cada empresa tem requisitos diferentes, incluindo configuração de equipes, processos e fluxos de trabalho de desenvolvimento diferentes. A configuração descrita abaixo é usada pela Adobe para vários projetos que proporcionam experiências com base no AEM as a Cloud Service.

Por exemplo, os aplicativos da Adobe Creative Cloud, como o Adobe Photoshop ou o Adobe Illustrator, incluem recursos de conteúdo, como tutoriais, amostras e guias disponíveis para os usuários finais. Esse conteúdo é consumido pelos aplicativos cliente usando o AEM as a Cloud Service sem periféricos, fazendo chamadas de API para o nível de publicação do AEM Cloud para recuperar o conteúdo estruturado como fluxos JSON e aproveitando a [rede de entrega de conteúdo (CDN) no AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#content-delivery) para fornecer conteúdo estruturado e não estruturado com desempenho ideal.

As equipes que contribuem com esse projeto seguem o processo descrito a seguir.

Cada equipe usa seu próprio fluxo de trabalho de desenvolvimento e tem um repositório Git separado. Um repositório Git compartilhado adicional é usado para integrar os projetos. Esse repositório Git contém a estrutura raiz do repositório Git do Cloud Manager, incluindo a configuração compartilhada do dispatcher.

A integração de um novo projeto exige a listagem no arquivo do projeto Maven do reator, na raiz do repositório Git compartilhado. Para a configuração do dispatcher, um novo arquivo de configuração é criado dentro do projeto do dispatcher. Esse arquivo é então incluído pela configuração principal do dispatcher. Cada equipe é responsável por seu próprio arquivo de configuração do dispatcher. As alterações no repositório Git compartilhado são raras e geralmente apenas são necessárias quando um novo projeto é integrado. O trabalho principal é realizado por cada equipe de projeto em seu próprio repositório Git.

![Diagrama do fluxo de trabalho](/help/implementing/cloud-manager/assets/team-setup1.png)

O repositório Git de cada equipe é configurado usando o [Arquétipo de Projetos AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) e, por conseguinte, segue as práticas recomendadas para a criação de projetos AEM. A única exceção é a configuração do dispatcher, que é feita no repositório Git compartilhado conforme descrito acima.

Cada equipe usa um fluxo de trabalho Git simplificado com duas ramificações + N, seguindo o modelo de fluxo Git:

* Uma ramificação de liberação estável contendo o código de produção.

* Uma ramificação de desenvolvimento contendo o desdobramento mais recente.

* Para cada recurso, uma nova ramificação é criada.

O desenvolvimento é realizado em uma ramificação de recursos. Quando o recurso é consolidado, ele é mesclado na ramificação de desenvolvimento. Os recursos concluídos e validados são extraídos da ramificação de desenvolvimento e mesclados na ramificação estável.

Todas as alterações são realizadas por meio de solicitações pull (PRs). Cada PR é automaticamente validada por quality gates (portais de qualidade). O Sonar é usado para verificar a qualidade do código, e um grupo de conjuntos de teste é executado para garantir que o novo código não esteja introduzindo qualquer regressão.

A configuração no repositório Git do Cloud Manager tem duas ramificações.

* Uma ramificação de liberação estável contendo o código de produção de todas as equipes.
* Uma ramificação de desenvolvimento contendo o código de desenvolvimento de todas as equipes.

Cada push para o repositório Git de uma equipe na ramificação estável ou de desenvolvimento aciona um [Ação do GitHub](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code).

Todos os projetos seguem a mesma configuração para a ramificação estável. Um push para a ramificação estável de um projeto é enviado automaticamente para a ramificação estável no repositório Git do Cloud Manager. O pipeline de produção no Cloud Manager é configurado para ser acionado por um push para a ramificação estável. O pipeline de produção é, portanto, executado por cada push de qualquer equipe em uma ramificação estável e a implantação em produção é atualizada se for aprovada em todos os quality gates (portais de qualidade).

![Diagrama de push](/help/implementing/cloud-manager/assets/team-setup2.png)

Um push para a ramificação de desenvolvimento é tratado de forma diferente. Embora um push para uma ramificação de desenvolvedor no repositório Git de uma equipe também acione uma ação do GitHub e o código seja enviado automaticamente para a ramificação de desenvolvimento no repositório Git do Cloud Manager, o pipeline de não produção não é acionado automaticamente pelo push de código. É acionado por uma chamada à API do Cloud Manager.

A execução do pipeline de produção inclui a verificação do código de todas as equipes por meio dos quality gates (portais de qualidade) fornecidos. Depois que o código é implantado em produção, os testes e as auditorias são executados para garantir que tudo está funcionando conforme o esperado. Uma vez aprovadas por todos os portais, as alterações são implementadas na produção sem interrupção ou tempo de inatividade.

Para o desenvolvimento local, é usado o [SDK do AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing). O SDK permite a configuração de um autor, editor e dispatcher local. Assim, é possível realizar o desenvolvimento offline e obter tempos de resposta rápidos. Às vezes, somente o ambiente de autoria é usado para desenvolvimento, mas a configuração rápida de ambientes do dispatcher e de publicação permite testar tudo localmente antes de enviar para o repositório Git.

Os membros de cada equipe geralmente verificam o código do Git compartilhado para seu próprio código de projeto. Não há necessidade de realizar o checkout de outros projetos, pois eles são independentes.

![Checkout local e SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

Essa configuração do mundo real pode ser usada como um blueprint e personalizada para as necessidades de uma empresa. O conceito flexível de ramificação e mesclagem do Git permite variações dos fluxos de trabalho acima, personalizados para as necessidades de cada equipe. O AEM as a Cloud Service oferece suporte a todas essas variações sem prejudicar o valor principal do pipeline opinativo do Cloud Manager.

>[!TIP]
>
>Consulte [Trabalhar com vários repositórios Git de origem](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html?lang=pt-BR#managing-code) para saber mais sobre esta configuração.

### Considerações para uma configuração de várias equipes {#considerations}

Com o repositório Git do Cloud Manager e o pipeline de produção, o código de produção completo é sempre executado por todos os quality gates (portais de qualidade), tratando-o como uma única unidade de implantação. Dessa forma, o sistema de produção está sempre ativo, sem interrupções ou tempo de inatividade.

Por outro lado, sem esse sistema em vigor, como cada equipe pode implantar separadamente, existe o risco de que uma atualização de uma única equipe possa levar a problemas de estabilidade na produção. Além disso, requer coordenação e tempo de inatividade planejado para lançar atualizações. Com um número crescente de equipes, o esforço de coordenação se torna muito mais complexo e rapidamente incontrolável.

Se um problema for detectado nos quality gates (portais de qualidade), a produção não será afetada e o problema poderá ser detectado e corrigido sem a necessidade de envolver o pessoal da Adobe. Sem o Cloud Service e sem sempre testar toda a implantação, implantações parciais podem causar paralisações que exigem uma solicitação de reversão ou até mesmo uma restauração completa de um backup. Os ensaios parciais também podem levar a outros problemas que terão de ser resolvidos posteriormente, exigindo coordenação e apoio do pessoal da Adobe.

>[!TIP]
>
>Para qualquer configuração de várias equipes, é fundamental definir um modelo de governança e um conjunto de padrões que todas as equipes devem seguir. O blueprint anterior de uma configuração de várias equipes permite dimensionar para um número maior de equipes, que você pode usar como ponto de partida.
