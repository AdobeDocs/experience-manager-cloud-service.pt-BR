---
title: Notas de versão do Cloud Manager 2025.2.0 no Adobe Experience Manager as a Cloud Service
description: Saiba mais sobre o lançamento do Cloud Manager 2025.2.0 no AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: c2a0961cae6d36d8ea3116c6e7982889257f90c8
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 5%

---

# Notas de versão do Cloud Manager 2025.2.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

Saiba mais sobre o lançamento do Cloud Manager 2025.2.0 no AEM (Adobe Experience Manager) as a Cloud Service.


Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2025.2.0 no AEM as a Cloud Service é quinta-feira, 13 de fevereiro de 2025.

A próxima versão está planejada para sexta-feira, 13 de março de 2025.

## Novidades {#what-is-new}

* **Atualização das regras de qualidade do código.**
A partir de quinta-feira, 13 de fevereiro de 2025, a etapa de qualidade do código do Cloud Manager agora usa uma versão atualizada do SonarQube 9.9.5.90363.

  As regras atualizadas, disponíveis para o Cloud Manager no AEM as a Cloud Service em [este link](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules), determinam as pontuações de segurança e a qualidade do código para os pipelines do Cloud Manager. Esta atualização pode afetar suas portas de qualidade, possivelmente bloqueando implantações.

* **Suporte à compilação do Java 17 e do Java 21.**

  Os clientes agora podem criar com o Java 17 ou Java 21, obtendo acesso a aprimoramentos de desempenho e novos recursos de linguagem. Para obter as etapas de configuração, incluindo a atualização das versões do projeto e da biblioteca Maven, consulte [Criar ambiente](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Quando a versão da build é definida como Java 17 ou Java 21, o tempo de execução implantado é o Java 21.

   * **Ativação de recursos**
      * Esse recurso será ativado para todos os clientes na quinta-feira, 13 de fevereiro de 2025, coincidindo com a implantação padrão da nova versão do SonarQube.
      * Os clientes podem habilitá-lo *imediatamente* definindo as duas configurações de variável descritas acima para atualizar a versão 9.9 do SonarQube.

   * **Implantação do Java 21 runtime**
      * O tempo de execução do Java 21 é implantado ao construir com Java 17 ou Java 21.
      * A implantação gradual em todos os ambientes do Cloud Manager começa em fevereiro para sandboxes e ambientes de desenvolvimento e se estende aos ambientes de produção em abril.
      * Os clientes que usam o Java 11 e desejam adotar o Java 21 runtime *previous* podem entrar em contato com a Adobe em [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).

* **99,99% de tempo de atividade para o Edge Delivery Services.**
A geração de relatórios de alta disponibilidade com 99,99% de tempo de atividade está agora disponível para programas Edge Delivery Services qualificados. Para ativar esse recurso, os clientes devem integrar seus sites do Edge Delivery Services com êxito e aplicar seu Service level agreement (SLA) de 99,99% no Cloud Manager.

  Consulte também [SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla).

* **Experiência de convite de usuário aprimorada para o Edge Delivery Services.**
Foram feitos aprimoramentos na experiência de convidar usuários para o repositório de conteúdo associado ao Edge Delivery Services. <!-- CMGR-65331 -->

* **Criação automática de perfis de administrador em instâncias de publicação.**
Anteriormente, o Cloud Manager permitia a criação manual de perfis de administrador em instâncias de publicação, mas não oferecia suporte à criação automática por padrão. Com essa atualização, os perfis de administrador agora são criados automaticamente em instâncias de publicação, melhorando a usabilidade e reduzindo o tempo de configuração para os clientes.

  Para obter mais detalhes, consulte [Permissões personalizadas](/help/implementing/cloud-manager/custom-permissions.md).

  ![Filtragem de atividades de pipeline](/help/implementing/cloud-manager/release-notes/assets/product-profiles.png)

* **Transição para OAuth para ambientes do Cloud Service.**
Os novos ambientes do Cloud Service agora usam a autenticação de serviço para serviço baseada em OAuth para projetos de integração do Adobe Developer Console, em vez do método de autenticação JWT usado anteriormente. A autenticação JWT foi descontinuada e está planejada para o fim da vida útil em junho de 2025.

* **Suporte para chaves privadas EC (curva elíptica) (secp384r1).**
A Cloud Manager agora oferece suporte a `secp384r1` chaves privadas de Curva Elíptica (EC), proporcionando maior segurança e conformidade para certificados SSL OV/EV gerenciados pelo cliente.
Para obter mais detalhes, consulte [Requisitos para certificados SSL OV/EV gerenciados pelo cliente](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md). <!-- CMGR-63636 -->

<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## Correções de erros

* **(UI) Correção de um problema que impedia a configuração de CDN para domínios no Cloud Manager.**
Os clientes que tentavam adicionar uma configuração CDN no Cloud Manager encontraram um erro de tela ao selecionar um domínio no menu suspenso. Esse bug da interface do usuário impedia o mapeamento de domínio em ambientes de produção, bloqueando o processo de configuração.

  Além disso, alguns domínios permaneceram inacessíveis no back-end, apesar de terem sido removidos da interface do usuário. Esse problema gerava conflitos com as configurações de CDN existentes.

  Com essa correção, agora é possível selecionar um domínio na lista suspensa sem encontrar um erro. As inconsistências de backend que impediam a reconfiguração do domínio foram solucionadas. E, finalmente, a validação aprimorada agora garante que domínios conflitantes sejam removidos corretamente antes de adicioná-los novamente.<!-- CMGR-64888 -->
* **(Back-end) Correção de um problema que fazia com que notificações de expiração de SSL fossem enviadas várias vezes.**
Um erro foi identificado em que o scheduler de notificação de expiração do SSL, projetado para ser executado uma vez por dia à meia-noite, era acionado incorretamente duas vezes por dia, uma vez à meia-noite e novamente às 12h30. Esse problema resultava no envio de várias notificações redundantes sobre certificados SSL que estavam expirando.

  O programador de notificações agora é executado corretamente apenas uma vez por dia, conforme esperado. E você não receberá mais notificações de expiração de SSL duplicadas. <!-- CMGR-64748 -->




<!-- ## Known issues {#known-issues} -->
