---
title: Notas de versão do Cloud Manager 2023.11.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2023.11.0 no AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 71746b00c2d4ee05126af54241db30a7d3aeab1c
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 13%

---


# Notas de versão do Cloud Manager 2023.11.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2023.11.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager 2023.11.0 no AEM as a Cloud Service é 14 de novembro de 2023. A próxima versão está planejada para 7 de dezembro de 2023.

## Novidades {#what-is-new}

* O Firewall-DDOS Protection (WAF-DDOS) do aplicativo da Web agora está disponível para compra como parte de seus direitos de AEM as a Cloud Service e [O pode ser configurado no autoatendimento.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* Especializado [Configuração de pipelines de implantação](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) Os pipelines agora estão disponíveis para definir configurações de ambiente, tarefas de manutenção, regras de CDN e muito mais em minutos.
* [Ao copiar conteúdo](/help/implementing/developing/tools/content-copy.md) de um ambiente superior para um ambiente de desenvolvimento, uma mensagem agora é mostrada recomendando cuidado ao copiar grandes conjuntos de conteúdo, já que os ambientes de desenvolvimento são limitados pela capacidade.
* [A página de detalhes de execução do pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) Agora, o mostrará todas as etapas em uma execução de pipeline com as que ainda não foram iniciadas esmaecidas.
* Em ambos **[Atividade](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)** e **[Pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)** páginas, um resumo da execução do pipeline agora está disponível ao clicar em um pipeline com um status de execução.
* Um novo **Duração** A seção foi adicionada à seção [página de detalhes do pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) que inclui a duração média da etapa do pipeline com base na tendência histórica desse programa.
* No [página de execução do pipeline,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity-window) as etapas concluídas agora exibem duração.
* Execuções que [reutilizar artefatos de build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) Agora, o mostrará o link para a execução que criou esses artefatos inicialmente.
* A opção para selecionar **Falhas de métricas importantes** agora pode ser configurado para [pipelines de qualidade de código](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) também.


## Programa de adoção antecipada {#early-adoption}

Faça parte do nosso programa de adoção antecipada e tenha a chance de testar alguns recursos futuros.

### Traga seu próprio GitHub {#byo-github}

Se você usar o GitHub para gerenciar os repositórios, [agora você pode validar o código diretamente nos repositórios GitHub por meio do Cloud Manager.](/help/implementing/cloud-manager/managing-code/byo-github.md) Essa integração elimina a necessidade de sincronizar consistentemente o código com o repositório Adobe e permite verificar solicitações de pull antes de mesclá-las às ramificações principais.

Se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie um email para `Grp-CloudManager_BYOG@adobe.com` do endereço de email associado à Adobe ID.

### Permissões personalizadas {#custom-permissions}

[Permissões personalizadas do Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md) O permite criar novos perfis de permissão personalizados com permissões configuráveis para restringir o acesso a programas, pipelines e ambientes para usuários do Cloud Manager.

se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie e envie um email `Grp-CloudManager-custom-permissions@adobe.com` do endereço de email associado à Adobe ID.

### Restauração de conteúdo de autoatendimento {#content-restore}

[Um novo recurso de restauração de conteúdo de autoatendimento](/help/operations/restore.md) O agora oferece restauração de backup por até sete dias e está disponível para usuários iniciais para fins de avaliação, apresentando:

* Restauração de backup point-in-time nas últimas 24 horas
* Restaurações por tempo fixo de até sete dias

Se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie um email para `aemcs-restorefrombackup-adopter@adobe.com` do email associado à Adobe ID. Observação:

* O programa de adoção antecipada está limitado apenas a ambientes de desenvolvimento.
* A disponibilidade do programa de adoção antecipada deste recurso é limitada.
* Esse recurso é para recuperação de conteúdo excluído acidentalmente e não se destina à recuperação de desastres.

### Painel de auditoria de experiência {#experience-audit-dashboard}

[O painel de Auditoria de experiência do Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) O inclui uma exibição de tendências das pontuações de desempenho da página, juntamente com insights e recomendações para ajudar você a melhorá-las. A Auditoria de experiência está incluída como uma etapa no pipeline de produção do Cloud Manager.

O painel usa o Google Lighthouse, uma ferramenta de código aberto e automatizada para melhorar a qualidade dos seus aplicativos Web. Você pode executá-la em qualquer página da Web, pública ou que exija autenticação. Ele tem auditorias de desempenho, acessibilidade, aplicativos web progressivos, SEO e muito mais.

Interessado em testar o novo painel? Envie um email para `aem-lighthouse-pilot@adobe.com` do email associado à sua Adobe ID e podemos começar.

## Problemas conhecidos {#known-issues}

Há um erro conhecido impedindo [configuração de pipelines de implantação](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md##config-deployment-pipeline) de ser encaminhado para produção.

Se a variável **Pausar antes de implantar na produção** é necessária uma opção para um pipeline de implantação de configuração. Veja a seguir a solução alternativa sugerida até que o erro seja resolvido.

1. Executar o pipeline.
1. Teste o código no ambiente de preparo.
1. Quando a implantação e a aprovação estiverem disponíveis, clique em **Rejeitar**.
1. Edite o pipeline para desativar o **Pausar antes de implantar na produção** opção.
1. Execute o pipeline novamente. Ele será executado novamente no preparo e depois na produção.
