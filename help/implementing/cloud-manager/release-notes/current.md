---
title: Notas de versão do Cloud Manager 2024.12.0 no Adobe Experience Manager as a Cloud Service
description: Saiba mais sobre o lançamento do Cloud Manager 2024.12.0 no AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: ea1aa471a4fcb2ace6e4079715ac88af2d296e18
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 31%

---

# Notas de versão do Cloud Manager 2024.12.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Saiba mais sobre o lançamento do Cloud Manager 2024.12.0 no AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Consulte as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2024.12.0 no AEM as a Cloud Service é quinta-feira, 5 de dezembro de 2024.

A próxima versão planejada é janeiro de 2024.

## Novidades {#what-is-new}

* **Suporte ao Java 21:** agora, os clientes podem criar opcionalmente com o Java 17 ou Java 21, beneficiando-se de melhorias de desempenho e novos recursos de linguagem. Consulte [Criar ambiente](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) para obter as etapas de configuração, incluindo a atualização da descrição do projeto Maven e determinadas versões da biblioteca. Quando a versão de build é definida como Java 17 ou Java 21, o tempo de execução assume o Java 21 como padrão.

  A partir de fevereiro de 2025, os ambientes sandboxes e dev serão atualizados para o tempo de execução do Java 21, independentemente da versão de build (Java 8, 11, 17 ou 21). Os ambientes de produção serão atualizados em abril de 2025.

* **Tipos de registro A:** O suporte para tipos de registro A foi adicionado para melhorar a Preparação para ativação para domínios que usam configurações de CDN na AEM Cloud Manager. Agora, você tem a opção de entrar em funcionamento adicionando um tipo de registro CNAME ou um tipo de registro A representando os IPs do Fastly, simplificando o roteamento de domínio. Esse aprimoramento elimina a restrição de depender exclusivamente de registros CNAME para a configuração de domínio com o Fastly.

  Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). <!-- CMGR-63076 -->

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

Os pipelines que usam repositórios externos (exceto os hospedados pelo GitHub) e o **Acionador de implantação** definidos como **Nas alterações do Git** agora são iniciados automaticamente.

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