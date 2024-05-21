---
title: Teste funcional
description: Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao processo de implantação do AEM as a Cloud Service para garantir a qualidade e a confiabilidade do seu código.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 305098c7ebcb6145129b146d60538b5177b4f26d
workflow-type: tm+mt
source-wordcount: '1373'
ht-degree: 9%

---


# Introdução {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Teste funcional"
>abstract="Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao processo de implantação do AEM as a Cloud Service para garantir a qualidade e a confiabilidade do seu código."

Saiba mais sobre as portas de qualidade disponíveis no [Processo as a Cloud Service de implantação do AEM](/help/implementing/cloud-manager/deploy-code.md), os diferentes tipos de testes funcionais integrados, como você pode contribuir e como fazer melhor uso deles no contexto de uma estratégia geral de testes.

## Visão geral

O diagrama a seguir fornece uma visão geral de alto nível dos pipelines disponíveis no contexto de uma estratégia de teste geral e do [Processo as a Cloud Service de implantação do AEM](/help/implementing/cloud-manager/deploy-code.md).

![Portas de qualidade de implantação do AEM Cloud Service](assets/functional-testing/quality-gates-compact.svg)

## Propósito

O objetivo dos pipelines de implantação do AEM Cloud Service é facilitar implantações robustas e seguras em vários estágios do ciclo de vida de desenvolvimento e lançamento do produto AEM. Esses pipelines incorporam vários quality gates (portais de qualidade) em diferentes níveis para garantir a integridade e a segurança das implantações para alterações de aplicativos do AEM e atualizações de produtos do AEM.

O Adobe fornece vários quality gates (portais de qualidade) incorporados, enquanto outros exigem sua intervenção para implementação e configuração. Esses quality gates (portais de qualidade) são versáteis, com alguns sendo aplicáveis em vários estágios do ciclo de vida e até mesmo integráveis em sua própria configuração de desenvolvimento e processos de CI/CD.

As portas de qualidade integradas validam principalmente a funcionalidade do produto AEM no contexto de seu aplicativo AEM. Por outro lado, os quality gates (portais de qualidade) personalizados que você configurou foram projetados para verificar se os recursos críticos do aplicativo e as interações do usuário estão funcionando conforme o esperado. Coletivamente, esses dois conjuntos de quality gates (portais de qualidade) trabalham juntos para garantir implantações automatizadas robustas e seguras para suas modificações de código e atualizações de produtos do AEM.

É importante observar que essas portas de qualidade não têm a intenção de ser uma estrutura de testes abrangente para toda a sua estratégia de testes. O produto AEM é submetido a testes abrangentes antes de entrar no processo de implantação do serviço de nuvem AEM. Da mesma forma, seu aplicativo já deve ser de alta qualidade antes de atingir a fase de implantação. Essa abordagem garante que os quality gates (portais de qualidade) se concentrem em seu objetivo principal de salvaguardar o processo de implantação, em vez de substituírem um regime de testes completo.

## Portas de qualidade

O diagrama a seguir fornece uma exibição detalhada das portas de qualidade disponíveis e seu uso na estratégia de teste geral e na [Processo as a Cloud Service de implantação do AEM](/help/implementing/cloud-manager/deploy-code.md).

![Portas de qualidade de implantação do AEM Cloud Service](assets/functional-testing/quality-gates-overview.svg)

### Resumo das Portas de Qualidade Fornecidas pelo Cliente

|                               | Testes de unidade | Personalizado<br/> Testes funcionais | Personalizado<br/> Testes de IU | Cliente<br/> Validações | Manual<br/> Testes |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **Pipeline de produção** | Sim<br/>Bloqueio<br/> | Sim<br/>Bloqueio<br/>Tempo limite de 60m | Sim<br/>Bloqueio<br/>Tempo limite de 30m | Não | Não |
| **Pipeline de não produção** | Sim<br/>Bloqueio<br/> | Opt-In<br/>Bloqueio<br/>Tempo limite de 60m | Opt-In<br/>Bloqueio<br/>Tempo limite de 30m | Não | Não |
| **Validação interna de Adobe** | Sim<br/>Bloqueio<br/> | Sim<br/>Bloqueio<br/>Tempo limite de 60m | Sim<br/>Bloqueio<br/>Tempo limite de 30m | Não | Não |
| **CI/CD do cliente** | Sim | Sim | Sim | Sim | Sim |
| **Desenvolvedor local do cliente** | Sim | Sim | Sim | Sim | Sim |

### Teste de unidade

É recomendável fornecer os testes de unidade para a sua aplicação de AEM, que são a base de cada estratégia de teste. Eles são destinados a funcionar rápido e frequentemente e dar feedback precoce e rápido. Eles são totalmente integrados aos workflows do desenvolvedor, ao seu próprio CI/CD e aos pipelines de implantação do serviço de nuvem AEM.

Eles são implementados usando JUnit e executados com Maven. Consulte [Módulo principal do Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/core.html#unit-tests) para ver um exemplo de teste unitário para AEM e introdução.

### Qualidade do código

Esse quality gate (portal de qualidade) é configurado imediatamente e executa a análise de código estático no código do aplicativo AEM.

Consulte [Teste de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md) e [Regras de qualidade do código personalizado](/help/implementing/cloud-manager/custom-code-quality-rules.md) para obter mais informações.

### Testes do produto

Os testes funcionais do produto são um conjunto de testes estáveis de integração HTTP (ITs) com funcionalidade principal no AEM, como tarefas de autoria e replicação. O Adobe fornece e os mantém prontos para uso. Eles têm como objetivo impedir a implantação de alterações no código de aplicativo personalizado se isso quebrar as funcionalidades principais no produto AEM.

Eles são implementados usando Junit, são executados usando Maven e usam o formulário oficial [Clientes de teste de AEM](https://github.com/adobe/aem-testing-clients). O conjunto de testes do produto é mantido como um [projeto de código aberto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke)O segue as práticas recomendadas do e pode ser considerado um bom ponto de partida para a implementação dos testes.

### Testes funcionais personalizados

Assim como os testes de produtos, os testes funcionais de clientes são testes de integração HTTP (ITs) e também são implementados usando o Junit, são executados usando o Maven e criados sobre o ambiente oficial [Clientes de teste de AEM](https://github.com/adobe/aem-testing-clients).

>[!NOTE]
>
>Testes funcionais personalizados são executados nos pipelines de produção e não produção (aceitação), que são usados pelas implantações de alterações do aplicativo AEM e atualizações de push de produto AEM e, portanto, são uma contribuição essencial para ajudar a garantir o funcionamento adequado do aplicativo e aumentar a segurança da versão. Os testes funcionais do cliente também são executados em pipelines internos de validação de pré-lançamento para cada cliente, o que ajuda a fornecer feedback antecipado.

Para manter a eficiência das execuções de pipeline, recomendamos nos concentrar nos principais recursos e fluxos de interação do usuário. Recomenda-se um tempo de execução de ~15 minutos ou menos para testes funcionais. Recomenda-se que conjuntos de testes funcionais completos que não se encaixem nessa porta de qualidade sejam executados como parte dos pipelines gerais de validação do cliente durante o fluxo de desenvolvimento do cliente.

Consulte [testes de produtos de código aberto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) ou o [Módulo it.tests do Arquétipo de projetos AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/ittests.html) para obter exemplos.

Consulte [Testes funcionais Java](/help/implementing/cloud-manager/java-functional-testing.md) para obter mais informações.

### Testes de interface do usuário personalizados

Para maximizar o controle de risco para o desenvolvimento específico do cliente, a Adobe incentiva capturar testes críticos de interface do usuário no AEM CS. Elas devem ser mantidas em número bastante limitado, mas com o maior impacto na experiência do cliente.

Os testes são compactados em uma imagem Docker - projetada para ser o mais volátil possível (com suporte para Cypress, Selenium, Java e Javascript). Elas seguem as mesmas características e finalidades dos testes funcionais personalizados.

>[!NOTE]
>
>Os testes de interface do usuário personalizados são executados nos pipelines de produção e não produção (aceitação) usados pelas implantações de alterações do aplicativo AEM e atualizações de push de produto AEM e, portanto, são uma contribuição essencial para ajudar a garantir o funcionamento adequado do aplicativo e aumentar a segurança da versão. Os testes de interface do usuário do cliente também são executados em pipelines internos de validação de pré-lançamento para cada cliente, o que ajuda a fornecer feedback antecipado.
>
>Os contêineres que não forem do Selenium devem executar testes usando um proxy HTTP com base nas variáveis de ambiente na [Seção de teste da interface do usuário.](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing)

Para manter as execuções de pipeline eficientes, recomendamos nos concentrar nos principais recursos e fluxos de interação do usuário. Recomenda-se que os conjuntos de testes de interface do usuário completa que não se encaixam nessa porta de qualidade sejam executados como parte dos pipelines gerais de validação do cliente durante o fluxo de desenvolvimento do cliente.

Consulte [testes de exemplo de código aberto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/) ou o [Módulo ui.tests do Arquétipo de projetos do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uitests.html) para obter exemplos.

Consulte [Testes de interface personalizados](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) para obter mais informações.

### Auditoria de experiência

A porta de qualidade da auditoria de experiência está funcionando [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) realiza auditorias na página do cliente na web.

Essa porta de qualidade é fornecida pelo AEM pronto para uso, mas não bloqueia os pipelines de implantação. Por padrão, uma auditoria na página raiz (`/`) da instância de publicação for executada. Você pode contribuir configurando até 25 caminhos personalizados que são considerados para auditorias.

Consulte [Teste de auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais informações.

### Validações de clientes

A porta de qualidade das validações de clientes é um espaço reservado para a estratégia e o esforço de teste do próprio cliente, executados antes que as alterações no aplicativo do cliente atinjam os pipelines de implantação de nuvem do AEM.

Aqui você pode escolher as ferramentas e estruturas que preferir. Ao contrário dos testes de função do cliente e testes de interface do usuário personalizados, não há limites as a Cloud Service para o AEM e, portanto, recomendamos executar testes funcionais e de interface do usuário de longa duração aqui.

Embora você possa escolher qualquer ferramenta e estrutura, recomendamos alinhar testes de integração baseados em HTTP e testes de interface do usuário com as ferramentas e estruturas disponíveis nos testes funcionais personalizados e nos quality gates (portais de qualidade) de testes de interface do usuário personalizados. Recomendamos a integração [Ambientes de desenvolvimento rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) em sua estratégia de teste local para testar o mais próximo possível dos ambientes de nuvem do AEM.

### Teste manual

A porta de qualidade do teste manual é um espaço reservado para clientes que fazem testes manuais. Os pipelines de nuvem de AEM não são compatíveis com testes manuais e, portanto, isso precisa acontecer como parte de sua própria estratégia de teste local.

Para testes manuais, pode ser útil integrar o a um ambiente de desenvolvimento adicional do AEM Cloud Service.
