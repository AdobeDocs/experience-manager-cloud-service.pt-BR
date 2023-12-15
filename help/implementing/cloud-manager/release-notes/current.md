---
title: Notas de versão do Cloud Manager 2023.12.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2023.12.0 no AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 71ce915413cd968a78a33b7a52d02e09841e1707
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 17%

---


# Notas de versão do Cloud Manager 2023.12.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2023.12.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager versão 2023.12.0 no AEM as a Cloud Service é 14 de dezembro de 2023. A próxima versão está planejada para 18 de janeiro de 2024.

## Novidades {#what-is-new}

* [Permissões personalizadas do Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md) As permitem criar perfis de permissão personalizados com permissões configuráveis para restringir o acesso a programas, pipelines e ambientes para usuários do Cloud Manager.
   * Esse recurso será implementado em fases e a conclusão está prevista para a versão de fevereiro de 2024 do Cloud Manager.
   * Envie um email para `Grp-CloudManager-custom-permissions@adobe.com` no endereço de email associado à sua Adobe ID, se desejar ser habilitado antes.
* Os contêineres de build agora oferecem suporte ao Node.js versão 18 para [pipelines de front-end.](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)
* Para programas recém-criados do Cloud Manager, [a subconta associada do New Relic](/help/implementing/cloud-manager/user-access-new-relic.md) não está ativada por padrão.
   * Para programas existentes nos quais a subconta do New Relic não for acessada por mais de 90 dias, ela será desativada.
   * Se quiser usar a subconta do New Relic, será necessário aceitar por meio do Cloud Manager.
* As implantações de versões secundárias para java 8 e 11 e atualizações para maven [anunciado e iniciado com a versão de outubro do Cloud Manager](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) foram concluídas.
   * O suporte para o Nó 18 foi adicionado para pipelines de front-end e pilha completa.
   * A versão secundária do Java 8 foi atualizada para `jdk1.8.0_371`.
   * A versão secundária do Java 11 foi atualizada para `jdk-11.0.20`.
   * O Maven foi atualizado para a versão 3.8.8
      * O Maven agora desativa todos os inseguros `http://*` espelhos por padrão.
      * [Adobe recomenda](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) Os usuários do atualizam os repositórios Maven para usar HTTPS em vez de HTTP.
   * A imagem base do container de build foi atualizada para Ubuntu 22.04.

## Programa de adoção antecipada {#early-adoption}

Para testar alguns recursos futuros, faça parte do programa de adoção antecipada do Adobe.

### Coleta do lado do cliente por meio do monitoramento de usuário real (RUM) {#rum}

Você pode aproveitar o [Serviço de Dados de Monitoramento do Usuário Real (RUM)](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) para ativar a coleta no lado do cliente para o AEM as a Cloud Service.

O Serviço de dados de monitoramento de usuário real (RUM) oferece um reflexo mais preciso das interações do usuário, garantindo uma medida confiável do engajamento do site. É uma ótima oportunidade para obter insights avançados sobre o desempenho da página. Isso é benéfico para clientes que usam CDN gerenciada por Adobe ou CDN gerenciada por não Adobe. Para clientes que usam um CDN não gerenciado por Adobe, o relatório de tráfego automatizado agora pode ser ativado para eles, eliminando a necessidade de compartilhar qualquer relatório de tráfego com o Adobe.

Se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie um email para `aemcs-rum-adopter@adobe.com` do endereço de email associado à sua Adobe ID. Inclua o nome de domínio dos ambientes de produção, preparo e desenvolvimento em seu email.  A disponibilidade do programa de adoção antecipada deste recurso é limitada.

### Traga seu próprio GitHub {#byo-github}

Se você usa o GitHub para gerenciar repositórios, [agora é possível validar o código diretamente nos seus repositórios do GitHub por meio do Cloud Manager.](/help/implementing/cloud-manager/managing-code/byo-github.md) Essa integração elimina a necessidade de sincronizar consistentemente o código com o repositório da Adobe e permite verificar solicitações “pull” antes de mesclá-las às ramificações principais.

Se você estiver interessado em testar esse novo recurso e compartilhar seus comentários, envie um email para `Grp-CloudManager_BYOG@adobe.com` do endereço de email associado à Adobe ID.

### Restauração de conteúdo de autoatendimento {#content-restore}

[Um novo recurso de restauração de conteúdo de autoatendimento](/help/operations/restore.md) O agora oferece restauração de backup por até sete dias e está disponível para usuários iniciais para fins de avaliação, apresentando:

* Restauração de backup point-in-time nas últimas 24 horas
* Restaurações por tempo fixo de até sete dias

Se você estiver interessado em testar esse novo recurso e compartilhar seus comentários, envie um email para `aemcs-restorefrombackup-adopter@adobe.com` do email associado à Adobe ID.

* O programa de adoção antecipada está limitado apenas a ambientes de desenvolvimento.
* A disponibilidade do programa de adoção antecipada deste recurso é limitada.
* Esse recurso é para recuperação de conteúdo excluído acidentalmente e não se destina à recuperação de desastres.

### Painel de auditoria de experiência {#experience-audit-dashboard}

[O painel de Auditoria de experiência do Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) O inclui uma exibição de tendências das pontuações de desempenho da página, juntamente com insights e recomendações para ajudar você a melhorá-las. A Auditoria de experiência está incluída como uma etapa no pipeline de produção do Cloud Manager.

O painel usa o Google Lighthouse, uma ferramenta de código aberto e automatizada para melhorar a qualidade dos seus aplicativos web. Você pode executá-lo em qualquer página da Web, público ou que exija autenticação. Ele tem auditorias de desempenho, acessibilidade, aplicativos web progressivos, SEO e muito mais.

Interessado em testar o novo painel? Para começar, envie um email para `aem-lighthouse-pilot@adobe.com` do email associado à Adobe ID.
