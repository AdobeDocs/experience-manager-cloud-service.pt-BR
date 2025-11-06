---
title: Configuração da equipe de desenvolvimento corporativa
description: Saiba como configurar e dimensionar sua equipe de desenvolvimento corporativo e veja como o AEM as a Cloud Service pode apoiar seu processo de desenvolvimento.
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 40%

---

# Configuração da equipe de desenvolvimento corporativo para o AEM as a Cloud Service {#enterprise-setup}

Saiba como configurar e dimensionar sua equipe de desenvolvimento corporativo e veja como o AEM (Adobe Experience Manager) as a Cloud Service pode apoiar seu processo de desenvolvimento.

## Introdução {#introduction}

Para oferecer suporte a clientes com configurações de desenvolvimento corporativo, o AEM as a Cloud Service integra-se totalmente ao Cloud Manager e a seus [pipelines opinativos de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) criados com propósitos específicos. Esses pipelines e serviços são criados com base nas práticas recomendadas, garantindo [testes completos e código da maior qualidade](/help/implementing/cloud-manager/code-quality-testing.md).

## Suporte da Cloud Manager na configuração de desenvolvimento de equipes corporativas {#cloud-manager}

Para garantir uma integração rápida, o Cloud Manager fornece tudo o que é necessário para começar a desenvolver experiências digitais imediatamente, incluindo um repositório Git para armazenar personalizações, que então são criadas, verificadas e implantadas pelo Cloud Manager.

Usando o Cloud Manager, as equipes de desenvolvimento podem trabalhar para confirmar as alterações com frequência, sem depender da equipe da Adobe.

Três tipos de ambientes estão disponíveis no Cloud Manager.

* Desenvolvimento
* Fase
* Produção

O código pode ser implantado em ambientes de desenvolvimento usando um pipeline de não produção. Para ambientes de preparo e produção, que sempre se unem e, portanto, garantem a validação antes da implantação em produção como prática recomendada, um pipeline de produção usa [quality gates (portais de qualidade)](/help/implementing/cloud-manager/custom-code-quality-rules.md) para validar o código do aplicativo e as alterações de configuração.

O pipeline de produção primeiro implanta o código e a configuração no ambiente de preparo, testa o aplicativo e finalmente implanta no ambiente de produção.

Um Cloud Service SDK que é sempre atualizado com as melhorias mais recentes do AEM as a Cloud Service permite o desenvolvimento local diretamente usando o hardware local do desenvolvedor. Essa abordagem permite um desenvolvimento rápido com tempos de resposta muito baixos. Assim, os desenvolvedores podem permanecer em seus ambientes locais familiares e escolher entre uma grande variedade de ferramentas de desenvolvimento, além de enviar para ambientes de desenvolvimento ou produção, quando bem entenderem.

A Cloud Manager oferece suporte a configurações flexíveis de várias equipes, que podem ser ajustadas para atender às necessidades de uma empresa. Para garantir implantações estáveis em várias equipes, o pipeline opinativo da Cloud Manager valida e testa o código de todas as equipes. Essa abordagem ajuda a evitar situações em que as alterações de uma equipe afetam a produção de todas as equipes.

## Exemplo do mundo real {#real-world-example}

Cada empresa tem requisitos diferentes, incluindo configuração de equipes, processos e fluxos de trabalho de desenvolvimento diferentes. A configuração descrita abaixo é usada pela Adobe para vários projetos que proporcionam experiências com base no AEM as a Cloud Service.

Por exemplo, os aplicativos da Adobe Creative Cloud, como o Adobe Photoshop ou o Adobe Illustrator, incluem recursos de conteúdo, como tutoriais, amostras e guias disponíveis para os usuários finais. Os aplicativos clientes consomem conteúdo do AEM as a Cloud Service de forma headless. Eles fazem chamadas de API para o nível de publicação da AEM Cloud para recuperar o conteúdo estruturado como fluxos JSON. Além disso, a [Rede de Entrega de Conteúdo (CDN) no AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#content-delivery) é usada para fornecer conteúdo estruturado e não estruturado com desempenho ideal.

As equipes que contribuem com esse projeto seguem o processo descrito a seguir.

Cada equipe usa seu próprio fluxo de trabalho de desenvolvimento e tem um repositório Git separado. Um repositório Git compartilhado adicional é usado para integrar os projetos. Esse repositório Git contém a estrutura raiz do repositório Git do Cloud Manager, incluindo a configuração compartilhada do Dispatcher.

A integração de um novo projeto exige a listagem no arquivo do projeto Maven do reator, na raiz do repositório Git compartilhado. Para configuração do Dispatcher, um novo arquivo de configuração é criado dentro do projeto do Dispatcher. A configuração principal do Dispatcher inclui esse arquivo. Cada equipe é responsável por seu próprio arquivo de configuração do Dispatcher. As alterações no repositório Git compartilhado são raras e geralmente só são necessárias quando um novo projeto é integrado. O trabalho principal é feito por cada equipe de projeto em seu próprio repositório Git.

![Diagrama do fluxo de trabalho](/help/implementing/cloud-manager/assets/team-setup1.png)

O repositório Git de cada equipe é configurado usando o [Arquétipo de Projetos AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/developing/archetype/overview) e, portanto, segue as práticas recomendadas para a configuração de Projetos AEM. A única exceção é a configuração do Dispatcher, que é feita no repositório Git compartilhado conforme descrito acima.

Cada equipe usa um fluxo de trabalho Git simplificado com duas ramificações + N, seguindo o modelo de fluxo Git:

* Uma ramificação de liberação estável contendo o código de produção.

* Uma ramificação de desenvolvimento contendo o desdobramento mais recente.

* Para cada recurso, uma nova ramificação é criada.

O desenvolvimento é realizado em uma ramificação de recursos. Quando o recurso amadurece, ele é mesclado na ramificação de desenvolvimento. Os recursos concluídos e validados são extraídos da ramificação de desenvolvimento e mesclados na ramificação estável.

Todas as alterações são feitas por meio de PRs (Pull Requests). Os quality gates (portais de qualidade) validam automaticamente cada PR. O Sonar é usado para verificar a qualidade do código, e um grupo de conjuntos de teste é executado para garantir que o novo código não esteja introduzindo qualquer regressão.

A configuração no repositório Git do Cloud Manager tem duas ramificações.

* Uma ramificação de liberação estável contendo o código de produção de todas as equipes.
* Uma ramificação de desenvolvimento contendo o código de desenvolvimento de todas as equipes.

Cada push para o repositório Git de uma equipe na ramificação estável ou de desenvolvimento aciona uma [ação do GitHub](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code).

Todos os projetos seguem a mesma configuração para a ramificação estável. Um push para a ramificação estável de um projeto é enviado automaticamente para a ramificação estável no repositório Git do Cloud Manager. Um push para a ramificação estável aciona o pipeline de produção no Cloud Manager. Cada push de qualquer equipe em uma ramificação estável aciona o pipeline de produção. A implantação de produção é atualizada se todos os quality gates (portais de qualidade) forem aprovados.

![Diagrama de push](/help/implementing/cloud-manager/assets/team-setup2.png)

Um push para a ramificação de desenvolvimento é tratado de forma diferente. Um push para uma ramificação de desenvolvedor no repositório Git de uma equipe também aciona uma ação do GitHub. Essa ação envia automaticamente o código para a ramificação de desenvolvimento no repositório Git do Cloud Manager. No entanto, esse push de código não aciona automaticamente o pipeline de não produção. Uma chamada para a API do Cloud Manager a aciona.

A execução do pipeline de produção inclui a verificação do código de todas as equipes por meio dos quality gates (portais de qualidade) fornecidos. Depois que o código é implantado em produção, os testes e as auditorias são executados para que tudo funcione conforme o esperado. Quando todas as portas são aprovadas, as alterações são implementadas na produção sem interrupção ou tempo de inatividade.

Para o desenvolvimento local, é usado o [SDK do AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing). O SDK permite a configuração de um autor, publicação e Dispatcher local. Esse fluxo de trabalho permite o desenvolvimento offline e tempos de resposta rápidos. Às vezes, somente o ambiente de criação é usado para desenvolvimento, mas a configuração rápida de ambientes do Dispatcher e de publicação permite testar tudo localmente antes de enviar para o repositório Git.

Os membros de cada equipe geralmente verificam o código do Git compartilhado para seu próprio código de projeto. Não é necessário conferir outros projetos, pois eles são independentes.

![Check-out local e SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

Essa configuração do mundo real pode ser usada como um blueprint e personalizada para as necessidades de uma empresa. O conceito flexível de ramificação e mesclagem do Git permite variações dos fluxos de trabalho acima, personalizados para as necessidades de cada equipe. O AEM as a Cloud Service oferece suporte a todas essas variações sem prejudicar o valor principal do pipeline opinativo do Cloud Manager.

>[!TIP]
>
>Consulte [Trabalhar com vários repositórios Git da Source](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-manager/content/managing-code/multiple-git-repos#managing-code) para saber mais sobre essa configuração.

### Considerações para uma configuração de várias equipes {#considerations}

Com o repositório Git da Cloud Manager e o pipeline de produção, o código de produção completo sempre passa por todos os quality gates (portais de qualidade), tratando-o como uma única unidade de implantação. Dessa forma, o sistema de produção está sempre ativo, sem interrupções ou tempo de inatividade.

Por outro lado, sem esse sistema em vigor, como cada equipe pode implantar separadamente, há o risco de que uma atualização de uma única equipe possa levar a problemas de estabilidade na produção. Além disso, requer coordenação e tempo de inatividade planejado para lançar atualizações. Com um número cada vez maior de equipes, o esforço de coordenação torna-se muito mais complexo e rapidamente impossível de gerenciar.

Se um problema for detectado nas portas de qualidade, a produção não será afetada e o problema poderá ser detectado e corrigido sem a necessidade de envolver o pessoal da Adobe. Sem o uso do Cloud Service ou a realização de testes frequentes em toda a implantação, as implantações parciais poderão causar paralisações que exigem uma solicitação de reversão ou até mesmo uma restauração completa a partir de um backup. Testes parciais também podem causar problemas adicionais que devem ser resolvidos posteriormente, exigindo coordenação e suporte da equipe da Adobe.

>[!TIP]
>
>Para qualquer configuração de várias equipes, é crucial definir um modelo de governança e um conjunto de padrões que todas as equipes devem seguir. O blueprint anterior de uma configuração de várias equipes permite dimensionar para um número maior de equipes, que você pode usar como ponto de partida.
