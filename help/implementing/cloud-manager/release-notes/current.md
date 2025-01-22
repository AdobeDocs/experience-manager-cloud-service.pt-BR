---
title: Notas de versão do Cloud Manager 2025.1.0 no Adobe Experience Manager as a Cloud Service
description: Saiba mais sobre o lançamento do Cloud Manager 2025.1.0 no AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 4ec2f22b399528f35c07a95d7487264149521338
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 10%

---

# Notas de versão do Cloud Manager 2025.1.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Saiba mais sobre o lançamento do Cloud Manager 2025.1.0 no AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Consulte as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2025.1.0 no AEM as a Cloud Service é quarta-feira, 22 de janeiro de 2025.

A próxima versão está planejada para sexta-feira, 13 de fevereiro de 2025.


## Novidades {#what-is-new}

* **Regras de qualidade do código:** a etapa Qualidade do código Cloud Manager começará a usar o SonarQube Server 9.9 com a versão Cloud Manager 2025.2.0, programada para quinta-feira, 13 de fevereiro de 2025.

Para se preparar, as regras atualizadas do SonarQube agora estão disponíveis em [Regras de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules).

Você pode &quot;verificar antecipadamente&quot; as novas regras definindo a seguinte variável de texto do pipeline:

`CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

Além disso, defina a seguinte variável para garantir que a etapa de qualidade do código seja executada para a mesma confirmação (normalmente ignorada para a mesma `commitId`):

`CM_DISABLE_BUILD_REUSE` = `true`

![Página de configuração de variáveis](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>A Adobe recomenda criar um novo pipeline de Qualidade de código CI/CD, configurado para a mesma ramificação que seu pipeline de produção principal. Defina as variáveis apropriadas *antes* da versão de 13 de fevereiro de 2025 para validar se as novas regras aplicadas não introduzem bloqueadores.

* **Suporte à compilação do Java 17 e do Java 21:** agora os clientes podem compilar com o Java 17 ou Java 21, obtendo acesso a aprimoramentos de desempenho e novos recursos de linguagem. Para obter as etapas de configuração, incluindo a atualização das versões do projeto e da biblioteca Maven, consulte [Criar ambiente](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Quando a versão da build é definida como Java 17 ou Java 21, o tempo de execução implantado é o Java 21.

   * **Ativação de recursos**
      * Esse recurso será ativado para todos os clientes na quinta-feira, 13 de fevereiro de 2025, coincidindo com a implantação padrão da nova versão do SonarQube.
      * Os clientes podem habilitá-lo *imediatamente* definindo as duas configurações de variável descritas acima para atualizar a versão 9.9 do SonarQube.

   * **Implantação do Java 21 runtime**
      * O tempo de execução do Java 21 é implantado ao construir com Java 17 ou Java 21.
      * A implantação gradual em todos os ambientes do Cloud Manager começa em fevereiro para sandboxes e ambientes de desenvolvimento e se estende aos ambientes de produção em abril.
      * Os clientes que usam o Java 11 e desejam adotar o tempo de execução do Java 21 *mais cedo* podem contatar o Adobe em [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
