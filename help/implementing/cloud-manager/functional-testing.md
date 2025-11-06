---
title: Teste funcional
description: Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao processo de implantação do AEM as a Cloud Service para garantir a qualidade e a confiabilidade do seu código.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 5%

---


# Introdução {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Teste funcional"
>abstract="Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao processo de implantação do AEM as a Cloud Service. O teste garante a qualidade e a confiabilidade do seu código."

Descubra os quality gates (portais de qualidade) disponíveis no [processo de implantação do AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) e os vários tipos de testes funcionais integrados. Saiba como você pode contribuir e otimizar o uso deles dentro da estrutura de uma estratégia de teste abrangente.

## Sobre o teste funcional

O diagrama a seguir fornece uma visão geral de alto nível dos pipelines disponíveis no contexto de uma estratégia geral de teste e do [processo de implantação do AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md).

![Portões de qualidade de implantação do AEM Cloud Service](assets/functional-testing/quality-gates-compact.svg)

## Finalidade dos testes funcionais

O objetivo dos pipelines de implantação do AEM Cloud Service é facilitar implantações robustas e seguras em vários estágios do ciclo de vida de desenvolvimento e lançamento de produtos do AEM. Esses pipelines incorporam vários quality gates (portais de qualidade) em diferentes níveis para garantir a integridade e a segurança das implantações para alterações de aplicativos do AEM e atualizações de produtos do AEM.

O Adobe fornece várias portas de qualidade integradas, enquanto outras exigem sua intervenção para implementação e configuração. Essas portas de qualidade são versáteis, aplicadas em vários estágios do ciclo de vida e integradas diretamente à configuração de desenvolvimento e aos processos de CI/CD.

Os quality gates (portais de qualidade) incorporados validam principalmente a funcionalidade do produto AEM no contexto do aplicativo do AEM. Por outro lado, os quality gates (portais de qualidade) personalizados que você configurou foram projetados para verificar se os recursos críticos do aplicativo e as interações do usuário estão funcionando conforme o esperado. Coletivamente, esses dois conjuntos de quality gates (portais de qualidade) trabalham juntos para garantir implantações automatizadas robustas e seguras para suas modificações de código e atualizações de produtos da AEM.

É importante observar que essas portas de qualidade não têm a intenção de ser uma estrutura de testes abrangente para toda a sua estratégia de testes. O produto da AEM é submetido a testes abrangentes antes de entrar no processo de implantação do AEM Cloud Service. Da mesma forma, seu aplicativo já deve ser de alta qualidade antes de atingir a fase de implantação. Essa abordagem garante que os quality gates (portais de qualidade) se concentrem em seu objetivo principal de salvaguardar o processo de implantação, em vez de substituírem um regime de testes completo.

## Portas de qualidade em teste

O diagrama a seguir fornece uma exibição detalhada dos quality gates (portais de qualidade) disponíveis e seu uso na estratégia geral de teste e no [processo de implantação do AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md).

![Portões de qualidade de implantação do AEM Cloud Service](assets/functional-testing/quality-gates-overview.svg)

### Resumo dos quality gates (portais de qualidade) fornecidos pelo cliente

|                               | Testes de unidade | Testes funcionais <br/> personalizados | Testes de Interface do Usuário <br/> Personalizados | Validações de Cliente<br/> | Teste manual<br/> |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **Pipeline de produção** | Sim<br/>Bloqueio<br/> | Sim<br/>Bloqueio<br/>60m Tempo Limite | Sim<br/>Bloqueio<br/>30m Tempo Limite | Não | Não |
| **Pipeline de Não Produção** | Sim<br/>Bloqueio<br/> | Aceitação<br/>Bloqueio<br/>60m Tempo Limite | Aceitação<br/>Bloqueio<br/>30m Tempo Limite | Não | Não |
| **Validação interna do Adobe** | Sim<br/>Bloqueio<br/> | Sim<br/>Bloqueio<br/>60m Tempo Limite | Sim<br/>Bloqueio<br/>30m Tempo Limite | Não | Não |
| **CI/CD do cliente** | Sim | Sim | Sim | Sim | Sim |
| **Desenvolvedor local do cliente** | Sim | Sim | Sim | Sim | Sim |

### Teste de unidade

É recomendável fornecer os testes de unidade para seu aplicativo AEM, que são a base de cada estratégia de teste. Eles são destinados a funcionar rápido e frequentemente e dar feedback precoce e rápido. Eles são totalmente integrados aos fluxos de trabalho do desenvolvedor, ao seu próprio CI/CD e aos pipelines de implantação do AEM Cloud Service.

Eles são implementados usando JUnit e executados com Maven. Consulte o [módulo principal do Arquétipo de Projeto do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/using#unit-tests) para obter um exemplo de teste unitário para o AEM e a introdução.

### Qualidade do código

Esse quality gate (portal de qualidade) é configurado imediatamente e executa a análise de código estático no código do aplicativo do AEM.

Consulte [Teste de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md) e [Regras de qualidade do código personalizado](/help/implementing/cloud-manager/custom-code-quality-rules.md) para obter mais informações.

### Testes do produto

Os testes funcionais do produto são testes estáveis de integração HTTP (ITs) para a funcionalidade principal do AEM, incluindo tarefas de autoria e replicação. A Adobe fornece e os mantém prontos para uso. Eles têm como objetivo impedir a implantação de alterações no código de aplicativo personalizado se isso quebrar as funcionalidades principais no produto AEM.

Eles usam JUnit para implementação, são executados com Maven e dependem dos [Clientes de teste AEM](https://github.com/adobe/aem-testing-clients) oficiais. O conjunto de testes do produto é mantido como
um [projeto de código aberto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) segue as práticas recomendadas e pode ser considerado um bom ponto de partida para a implementação de seus testes.

### Testes funcionais personalizados

Semelhante aos testes de produtos, os testes funcionais de clientes são testes de integração HTTP (ITs) implementados com JUnit, executados usando Maven e criados sobre os [Clientes de teste AEM](https://github.com/adobe/aem-testing-clients) oficiais.

>[!NOTE]
>
>Testes funcionais personalizados são executados em pipelines de produção e não produção (aceitação) usados para implantações de alteração de aplicativo do AEM e atualizações de push de produto do AEM. Eles desempenham um papel crucial para garantir que seu aplicativo funcione corretamente e para melhorar a segurança da versão. Os testes funcionais do cliente também são executados em pipelines internos de validação de pré-lançamento para cada cliente, o que ajuda a fornecer feedback antecipado.

Para manter execuções eficientes de pipelines, a Adobe recomenda que você se concentre nos principais recursos e fluxos de interação do usuário principal, visando um tempo de execução de teste funcional de cerca de 15 minutos ou menos. Conjuntos de testes funcionais completos que excedem esse tempo devem ser executados como parte dos pipelines gerais de validação do cliente durante o processo de desenvolvimento.

Consulte [testes de produtos de código aberto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) ou o módulo [it.tests do Arquétipo de Projetos do AEM](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests) para ver exemplos.

Consulte [Testes funcionais Java](/help/implementing/cloud-manager/java-functional-testing.md) para obter mais informações.

### Testes de interface do usuário personalizados

Para maximizar o controle de riscos para o desenvolvimento específico do cliente, a Adobe incentiva você a capturar testes críticos de interface do usuário na AEM as a Cloud Service. Mantenha-os limitados, mas concentrados em maximizar o impacto na experiência do cliente.

Os testes são compactados em uma imagem Docker - projetada para ser o mais volátil possível (com suporte para Cypress, Playwright, Selenium, Java e JavaScript). Elas seguem as mesmas características e finalidades dos testes funcionais personalizados.

>[!NOTE]
>
>Os testes de interface do usuário personalizados são executados em pipelines de produção e não produção (aceitação) usados para implantações de alteração de aplicativo do AEM e atualizações de push de produto do AEM. Elas são essenciais para garantir o funcionamento adequado do aplicativo e melhorar a segurança da versão. Os testes de interface do usuário do cliente também são executados em pipelines internos de validação de pré-lançamento para cada cliente, o que ajuda a fornecer feedback antecipado.
>
>Os contêineres que não são Selenium devem executar testes usando um proxy HTTP com base nas variáveis de ambiente na [Seção de Testes de Interface](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing).

Para manter as execuções de pipeline eficientes, a Adobe recomenda que você se concentre nos principais recursos e fluxos de interação do usuário. Os conjuntos de testes de interface do usuário completos que excedem essa porta de qualidade devem ser executados como parte dos pipelines de validação geral do cliente. Incorpore-os ao processo de desenvolvimento do cliente.

Consulte [testes de exemplo de código aberto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/) ou o módulo [ui.tests do Arquétipo de Projetos do AEM](/help/implementing/cloud-manager/ui-testing.md) para ver exemplos.

Consulte [Testes de interface personalizados](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) para obter mais informações.

### Auditoria de experiência

O portal de qualidade da auditoria de experiência está executando [auditorias do Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) na página da Web do cliente.

Esse quality gate (portal de qualidade) é fornecido pela AEM pronta para uso, mas não bloqueia os pipelines de implantação. Por padrão, uma auditoria na página raiz (`/`) da instância de publicação é executada. Você pode contribuir configurando até 25 caminhos personalizados que são considerados para auditorias.

Consulte [Teste de auditoria de experiência](/help/implementing/cloud-manager/reports/report-experience-audit.md) para obter mais informações.

### Validações de cliente

O quality gate (portal de qualidade) de validações do cliente é um espaço reservado para a estratégia e o esforço de teste do próprio cliente, executados antes que as alterações no aplicativo do cliente atinjam os pipelines de implantação de nuvem do AEM.

Aqui você pode escolher as ferramentas e estruturas que preferir. Ao contrário dos testes de função do cliente e testes de interface do usuário personalizados, não há limites relacionados à AEM as a Cloud Service. Dessa forma, a Adobe recomenda que você execute testes funcionais e de interface do usuário de longa duração aqui.

Embora você possa escolher qualquer ferramenta e estrutura, a Adobe sugere alinhar a integração baseada em HTTP e os testes de interface com as ferramentas e estruturas usadas nos quality gates (portais de qualidade) funcionais e de testes de interface do usuário personalizados. Além disso, a Adobe recomenda incorporar os [Ambientes de desenvolvimento rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) à sua estratégia de teste local para refletir os ambientes de nuvem da AEM.

### Teste manual

A porta de qualidade do teste manual é um espaço reservado para clientes que fazem testes manuais. Como os pipelines de nuvem do AEM não são compatíveis com testes manuais, ele deve ser incluído em sua estratégia de teste local.

Para testes manuais, pode ser útil integrar a um ambiente de desenvolvimento adicional do AEM Cloud Service.
