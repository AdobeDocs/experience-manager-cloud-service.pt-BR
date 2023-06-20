---
title: Teste funcional
description: Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao processo de implantação do AEM as a Cloud Service para garantir a qualidade e a confiabilidade do seu código.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 88%

---


# Teste funcional {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Teste funcional"
>abstract="Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao processo de implantação do AEM as a Cloud Service para garantir a qualidade e a confiabilidade do seu código."

Saiba mais sobre os três diferentes tipos de testes funcionais integrados ao [processo de implantação do AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) para garantir a qualidade e a confiabilidade do seu código.

## Escopo

O objetivo das etapas de teste funcional no pipeline do Cloud Manager é garantir que a funcionalidade essencial do seu aplicativo esteja executando conforme o esperado.

Essa fase de teste é o último nível de teste automatizado antes da implantação do seu código na produção.

Os testes funcionais não devem substituir, mas sim complementar e estender outras estratégias de teste, como testes de unidade,
testes de integração ou testes funcionais realizados fora da execução do pipeline no Cloud Manager.

## Visão geral {#overview}

Existem três tipos diferentes de testes funcionais no AEM as a Cloud Service.

* [Teste funcional do produto](#product-functional-testing)
* [Teste funcional personalizado](#custom-functional-testing)
* [Testes de interface do usuário personalizados](#custom-ui-testing)

Para todos os testes funcionais, os resultados detalhados dos testes podem ser baixados como um arquivo `.zip` usando o botão **Baixar log de compilação** na tela de visão geral da compilação como parte do [processo de implantação.](/help/implementing/cloud-manager/deploy-code.md)

Esses logs não incluem os logs do processo de tempo de execução real do AEM. Para acessá-los, consulte o documento [Acesso e gerenciamento de logs](/help/implementing/cloud-manager/manage-logs.md) para obter mais detalhes.

Tanto os testes funcionais do produto quanto os testes funcionais personalizados de amostra se baseiam nos [Clientes de teste do AEM.](https://github.com/adobe/aem-testing-clients)

### Teste funcional do produto {#product-functional-testing}

Os testes funcionais do produto são um conjunto de testes estáveis de integração HTTP (ITs) com funcionalidade principal no AEM, como tarefas de autoria e replicação. Esses testes são mantidos pela Adobe e têm como objetivo impedir a implantação de alterações no código de aplicativo personalizado, caso interrompa as funcionalidades principais.

* [Pipelines de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md): os testes funcionais do produto são executados automaticamente sempre que um novo código é implantado no Cloud Manager e não podem ser ignorados.
* [Pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md): os testes funcionais do produto podem ser opcionalmente selecionados para serem executados sempre que você executar o pipeline de não produção.

Os testes funcionais do produto são mantidos como um projeto de código aberto. Consulte os [testes funcionais do produto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) no GitHub para obter detalhes.

### Teste funcional personalizado {#custom-functional-testing}

Embora o teste funcional do produto seja definido pela Adobe, você pode criar seu próprio teste de qualidade para o seu aplicativo. Isso é executado como um teste funcional personalizado como parte da [pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) ou, opcionalmente [pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) para garantir a qualidade do seu aplicativo.

O teste funcional personalizado é executado tanto para implantações de código personalizado quanto para atualizações por push, o que torna especialmente importante criar bons testes funcionais, a fim de impedir que as alterações de código do AEM quebrem o código do aplicativo. A etapa de teste funcional personalizado está sempre presente e não pode ser ignorada.

Consulte [Testes funcionais de Java](/help/implementing/cloud-manager/java-functional-testing.md) para obter mais informações.


### Testes de interface do usuário personalizados {#custom-ui-testing}

Os testes de interface do usuário personalizados são um recurso opcional que permite criar e executar automaticamente testes na interface do usuário para seus aplicativos. Os testes de interface do usuário são testes baseados em Selenium, compactados em uma imagem do Docker, para permitir uma grande variedade de linguagens e estruturas, como Java e Maven, Node e WebDriver.io, ou qualquer outra estrutura e tecnologia criada no Selenium.

Consulte [Teste personalizado da interface](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) para obter mais informações.

