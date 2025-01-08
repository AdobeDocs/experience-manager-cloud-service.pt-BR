---
title: Notas de versão do Cloud Manager 2024.12.0 no Adobe Experience Manager as a Cloud Service
description: Saiba mais sobre o lançamento do Cloud Manager 2024.12.0 no AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 6f17afc82b2d26fd6025a9ba8449a0cb1b368d48
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 39%

---

# Notas de versão do Cloud Manager 2024.12.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Saiba mais sobre o lançamento do Cloud Manager 2024.12.0 no AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Consulte as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2024.12.0 no AEM as a Cloud Service é quinta-feira, 5 de dezembro de 2024.

A próxima versão está planejada para 23 de janeiro de 2025.


## Novidades {#what-is-new}

* **Regras de qualidade do código:** a partir de quinta-feira, 13 de fevereiro de 2025, a etapa de qualidade do código Cloud Manager agora usa uma versão atualizada do SonarQube 9.9.5.90363.

  As regras atualizadas, disponíveis para o Cloud Manager no AEM as a Cloud Service em [este link](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules), determinam as pontuações de segurança e a qualidade do código para os pipelines do Cloud Manager. Essa atualização pode afetar seus quality gates (portais de qualidade), bloqueando possivelmente as implantações.

<!-- * **Java 21 support:** Customers can now optionally build with Java 17 or Java 21, benefiting from performance improvements and new language features. See [Build environment](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) for configuration steps, including updating your Maven project description, and certain library versions. When the build version is set to Java 17 or Java 21, the runtime defaults to Java 21.

    Starting February 2025, sandboxes and dev environments upgrade to the Java 21 runtime, regardless of the build version (Java 8, 11, 17, or 21). Production environments follow with an upgrade in April 2025. -->

* **Tipos de registro A:** O suporte para tipos de registro A foi adicionado para melhorar a Preparação para ativação para domínios que usam configurações de CDN na AEM Cloud Manager. Agora, você tem a opção de entrar em funcionamento adicionando um tipo de registro CNAME ou um tipo de registro A representando os IPs do Fastly, simplificando o roteamento de domínio. Esse aprimoramento elimina a restrição de depender exclusivamente de registros CNAME para a configuração de domínio com o Fastly.

  Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). <!-- CMGR-63076 -->

<!-- * The AEM Code Quality step now uses SonarQube 9.9 Server, replacing the older 7.4 version. This upgrade brings additional security, performance, and code quality checks, offering more comprehensive analysis and coverage for your projects. -->

* **Adicionar vários domínios a um Site do Edge Delivery:** Agora é possível adicionar vários domínios, incluindo domínios apex e não apex, a um Site do Edge Delivery (EDS) no AEM Cloud Manager. Esse aprimoramento soluciona limitações anteriores que restringiam a capacidade de associar vários domínios a uma origem de EDS. A atualização garante melhor flexibilidade para gerenciar configurações de domínio e simplifica os processos de ativação para sites com configurações de domínio complexas. <!-- CMGR-63007 -->

* **Opções de filtragem avançadas:** As opções de filtragem avançadas foram introduzidas nas páginas de execução de pipeline e páginas de certificado SSL no AEM Cloud Manager. Agora é possível filtrar por vários critérios, fornecendo acesso mais rápido a dados relevantes e melhorando a eficiência da implantação. <!-- CMGR-26263 -->

   * **Filtragem de atividades de pipeline:** inclui filtragem de atividades de pipeline, permitindo que você refine os resultados da pesquisa para atividades de pipeline específicas. Os filtros disponíveis incluem pipeline, ação e status.
     ![Filtragem de atividades de pipeline](/help/implementing/cloud-manager/assets/filters-pipeline.png)


   * **Filtragem de certificados SSL:** Inclui filtragem de certificados SSL, que permite refinar os resultados da pesquisa para certificados específicos. Os filtros disponíveis incluem nome do certificado SSL, propriedade e status.
     ![Filtragem de certificado SSL](/help/implementing/cloud-manager/assets/filters-ssl-certificates.png)

## Programa de adoção antecipada {#early-adoption}

Faça parte do programa de adoção antecipada do Cloud Manager e aproveite a oportunidade de testar alguns dos próximos recursos.

### Traga seu próprio Git: agora com suporte para GitLab e Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

O recurso **Traga seu próprio Git** foi expandido para incluir suporte para repositórios externos, como GitLab e Bitbucket. Esse novo suporte é uma adição ao suporte já existente para repositórios GitHub privados e empresariais. Ao adicionar esses novos repositórios, também é possível vinculá-los diretamente aos seus pipelines. Você pode hospedar esses repositórios em plataformas de nuvem pública ou em sua infraestrutura ou nuvem privada. Essa integração também elimina a necessidade de sincronização constante do código com o repositório da Adobe e oferece a capacidade de validar solicitações de pull antes de mesclá-las em uma ramificação principal.

Os pipelines que usam repositórios externos (exceto os hospedados pelo GitHub) e o **Acionador de implantação** definidos como **Sobre alterações do Git** agora são iniciados automaticamente.

Consulte [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Caixa de diálogo Adicionar repositório](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Atualmente, as verificações de qualidade do código de solicitação de pull prontas para uso são exclusivas de repositórios hospedados no GitHub, mas uma atualização para estender essa funcionalidade a outros fornecedores Git está em andamento.

Se tiver interesse em testar esse novo recurso e compartilhar o seu feedback, envie um email para [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) do seu endereço de email associado à sua Adobe ID. Inclua qual plataforma Git deseja usar e se você está em uma estrutura de repositório privado/público ou empresarial.

## Correções de erros

* Uma proteção foi adicionada para impedir a exclusão de domínios com mapeamentos de domínio ativos no AEM Cloud Manager. Os usuários que tentam excluir esses domínios agora recebem uma mensagem de erro instruindo-os a excluir o mapeamento de domínio antes de continuar com a exclusão do domínio. Esse fluxo de trabalho garante a integridade do domínio e evita erros de configuração acidentais. <!-- CMGR-63033 -->
* Raramente, os usuários não conseguiam adicionar um nome de domínio ou atualizar um certificado SSL devido a um status incorreto associado nos respectivos casos. <!-- CMGR-62816 -->


<!-- ## Known issues {#known-issues} -->
