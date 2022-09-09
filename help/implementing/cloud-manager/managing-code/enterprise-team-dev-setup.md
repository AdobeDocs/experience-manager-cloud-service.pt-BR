---
title: Configuração da equipe de desenvolvimento corporativa
description: Saiba como configurar e dimensionar sua equipe de desenvolvimento empresarial e veja como AEM as a Cloud Service pode suportar seu processo de desenvolvimento.
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: a31c3693c9b2af9bd7f9d7f1f6fb0a61a4411df0
workflow-type: tm+mt
source-wordcount: '1444'
ht-degree: 1%

---

# Configuração da Equipe de Desenvolvimento Empresarial para AEM as a Cloud Service {#enterprise-setup}

Saiba como configurar e dimensionar sua equipe de desenvolvimento empresarial e veja como AEM as a Cloud Service pode suportar seu processo de desenvolvimento.

## Introdução {#introduction}

Para oferecer suporte a clientes com configurações de desenvolvimento corporativo, o AEM integra-se totalmente ao Cloud Manager e a seu propósito, [Gasodutos de IC/CD.](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) Esses pipelines e serviços são criados com base nas práticas recomendadas, garantindo [teste e a maior qualidade do código.](/help/implementing/cloud-manager/code-quality-testing.md)

## Suporte do Cloud Manager na configuração de desenvolvimento de equipes empresariais {#cloud-manager}

Para garantir a integração rápida, o Cloud Manager fornece tudo o que é necessário para começar a desenvolver experiências digitais imediatamente, incluindo um repositório Git para armazenar personalizações que são criadas, verificadas e implantadas pelo Cloud Manager.

Usando o Cloud Manager, as equipes de desenvolvimento podem trabalhar para confirmar as alterações com frequência, sem depender da equipe do Adobe.

Três tipos de ambientes estão disponíveis no Cloud Manager.

* Desenvolvimento
* Estágio
* Produção

O código pode ser implantado em ambientes de desenvolvimento usando um pipeline de não produção. Para ambientes de preparo e produção, que sempre se unem e, portanto, garantem a validação antes da implantação da produção como prática recomendada, um pipeline de produção usa [portões de qualidade](/help/implementing/cloud-manager/custom-code-quality-rules.md) para validar o código do aplicativo e as alterações de configuração.

O pipeline de produção implanta o código e a configuração no ambiente de preparo primeiro, testa o aplicativo e finalmente implanta na produção.

Um SDK do Cloud Service que é sempre atualizado com as melhorias as a Cloud Service mais recentes permite o desenvolvimento local diretamente utilizando o hardware local do desenvolvedor. Isto permite um desenvolvimento rápido com tempos de resposta muito baixos. Assim, os desenvolvedores podem permanecer em seu ambiente local familiar e escolher entre uma grande variedade de ferramentas de desenvolvimento, além de impulsionar a ambientes de desenvolvimento ou produção, quando bem entenderem.

O Cloud Manager é compatível com configurações flexíveis de várias equipes, que podem ser ajustadas para atender às necessidades de uma empresa. Para garantir implantações estáveis com várias equipes, ao mesmo tempo em que evita situações em que uma equipe afeta a produção de todas as equipes, o pipeline opinativo do Cloud Manager sempre valida e testa o código de todas as equipes.

## Exemplo do mundo real {#real-world-example}

Cada empresa tem requisitos diferentes, incluindo configuração de equipe, processos e fluxos de trabalho de desenvolvimento diferentes. A configuração descrita abaixo é usada pelo Adobe para vários projetos que proporcionam experiências além AEM as a Cloud Service.

Por exemplo, os aplicativos do Adobe Creative Cloud, como Adobe Photoshop ou Adobe Illustrator, incluem recursos de conteúdo, como tutoriais, amostras e guias disponíveis para os usuários finais. Esse conteúdo é consumido pelos aplicativos clientes usando AEM as a Cloud Service de forma headless, fazendo chamadas de API para o AEM Cloud publish tier para recuperar o conteúdo estruturado como fluxos JSON e aproveitando o [Rede de entrega de conteúdo (CDN) AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#content-delivery) para fornecer conteúdo estruturado e não estruturado com desempenho ideal.

As equipes que contribuem com esse projeto seguem o seguinte processo.

Cada equipe usa seu próprio fluxo de trabalho de desenvolvimento e tem um repositório Git separado. Um repositório Git compartilhado adicional é usado para integrar projetos. Esse repositório Git contém a estrutura raiz do repositório Git do Cloud Manager, incluindo a configuração compartilhada do dispatcher.

A integração de um novo projeto requer a listagem no arquivo do projeto Maven do reator na raiz do repositório Git compartilhado. Para a configuração do dispatcher, um novo arquivo de configuração é criado dentro do projeto do dispatcher. Esse arquivo é então incluído pela configuração principal do dispatcher. Cada equipe é responsável por seu próprio arquivo de configuração de dispatcher. As alterações no repositório Git compartilhado são raras e geralmente só são necessárias quando um novo projeto é integrado. O trabalho principal é feito por cada equipe de projeto em seu próprio repositório Git.

![Diagrama de fluxo de trabalho](/help/implementing/cloud-manager/assets/team-setup1.png)

O repositório Git de cada é configurado usando o [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt_BR) e, por conseguinte, segue as melhores práticas para a criação de projetos AEM. A única exceção é a configuração do dispatcher que é feita no repositório Git compartilhado conforme descrito acima.

Cada equipe usa um fluxo de trabalho git simplificado com duas ramificações + N, seguindo o modelo de fluxo git:

* Uma ramificação de liberação estável contém o código de produção.

* Uma ramificação de desenvolvimento contém o desenvolvimento mais recente.

* Para cada recurso, uma nova ramificação é criada.

O desenvolvimento é feito em uma ramificação de recursos. Quando o recurso amadurece, ele é mesclado na ramificação de desenvolvimento. Os recursos concluídos e validados são extraídos da ramificação de desenvolvimento e mesclados na ramificação estável.

Todas as alterações são feitas por meio de solicitações de pull (PRs). Cada PR é automaticamente validada por portas de qualidade. O Sonar é usado para verificar a qualidade do código, e um conjunto de conjuntos de teste é executado para garantir que o novo código não esteja introduzindo qualquer regressão.

A configuração no repositório Git do Cloud Manager tem duas ramificações.

* Uma ramificação de lançamento estável contém o código de produção de todas as equipes.
* Uma ramificação de desenvolvimento contém o código de desenvolvimento de todas as equipes.

Cada push para o repositório Git de uma equipe no desenvolvimento ou na ramificação estável aciona uma [Ação do GitHub.](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code)

Todos os projetos seguem a mesma configuração para a ramificação estável. Um push para a ramificação estável de um projeto é enviado automaticamente para a ramificação estável no repositório Git do Cloud Manager. O pipeline de produção no Cloud Manager é configurado para ser acionado por um push para a ramificação estável. O pipeline de produção é, portanto, executado por cada push de qualquer equipe em uma ramificação estável e a implantação de produção é atualizada se todas as portas de qualidade passarem.

![Diagrama de push](/help/implementing/cloud-manager/assets/team-setup2.png)

Os esforços para o ramo de desenvolvimento são tratados de forma diferente. Embora um push para uma ramificação de desenvolvedor no repositório Git de uma equipe também esteja acionando uma ação GitHub e o código seja enviado automaticamente para a ramificação de desenvolvimento no repositório Git do Cloud Manager, o pipeline de não produção não é acionado automaticamente pelo push de código. Ela é acionada por uma chamada para a API do Cloud Manager.

A execução do pipeline de produção inclui a verificação do código de todas as equipes por meio das portas de qualidade fornecidas. Depois que o código é implantado no estágio, os testes e as auditorias são executados para garantir que tudo funcione conforme o esperado. Depois que todas as portas forem passadas, as alterações serão implementadas para produção sem interrupção ou tempo de inatividade.

Para o desenvolvimento local, a variável [SDK para AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing) é usada. O SDK permite que um autor, publicação e dispatcher locais sejam configurados. Isso permite o desenvolvimento offline e tempos de resposta rápidos. Às vezes, somente o ambiente do autor é usado para desenvolvimento, mas a configuração rápida de ambientes do dispatcher e de publicação permite testar tudo localmente antes de enviar para o repositório Git.

Os membros de cada equipe geralmente fazem check-out do código no git compartilhado para , bem como em seu próprio código de projeto. Não há necessidade de realizar check-out de outros projetos, pois eles são independentes.

![Check-out local e SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

Essa configuração do mundo real pode ser usada como um blueprint e depois personalizada para as necessidades de uma empresa. O conceito flexível de ramificação e mesclagem do git permite variações dos fluxos de trabalho acima, personalizados para as necessidades de cada equipe. AEM as a Cloud Service suporta todas essas variações sem sacrificar o valor principal do pipeline do Cloud Manager opinado.

>[!TIP]
>
>Consulte o documento [Trabalhando com vários repositórios Git de origem](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html#managing-code) para saber mais sobre essa configuração.

### Considerações para uma configuração de vários grupos {#considerations}

Com o repositório Git do Cloud Manager e o pipeline de produção, o código de produção completo é sempre executado por todas as portas de qualidade, tratando-o como uma unidade de implantação. Dessa forma, o sistema de produção está sempre ativo sem interrupção ou tempo de inatividade.

Por outro lado, sem esse sistema em vigor, porque cada equipe pode implantar separadamente, existe o risco de que uma atualização de uma única equipe possa levar a problemas de estabilidade de produção. Além disso, requer coordenação e tempo de inatividade planejado para lançar atualizações. Com um número crescente de equipes, o esforço de coordenação tornar-se-á muito mais complexo e rapidamente incontrolável.

Se for detectado um problema nas portas de qualidade, a produção não é afetada e o problema pode ser detectado e corrigido sem o pessoal de Adobe necessário para entrar. Sem o Cloud Service e sem sempre testar toda a implantação, implantações parciais podem causar paralisações que exigem uma solicitação de reversão ou até mesmo uma restauração completa de um backup. Os ensaios parciais podem também conduzir a outros problemas que terão de ser resolvidos depois de o fato exigir de novo a coordenação e o apoio do pessoal Adobe.

>[!TIP]
>
>Para qualquer configuração de várias equipes, é crucial definir um modelo de governança e um conjunto de padrões que todas as equipes devem seguir. O blueprint anterior de uma configuração de várias equipes permite dimensionar em um número maior de equipes, que você pode usar como ponto de partida.
