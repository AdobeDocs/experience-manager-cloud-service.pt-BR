---
title: Notas de versão do Cloud Manager 2025.8.0
description: Saiba mais sobre o lançamento do Cloud Manager 2025.8.0 no Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: f72f72e87dabe89cafc0a56feb35f58ae1a97dfb
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 3%

---

# Notas de versão do Cloud Manager 2025.8.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Saiba mais sobre o lançamento do Cloud Manager 2025.8.0 no AEM (Adobe Experience Manager) as a Cloud Service.

Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2025.8.0 no AEM as a Cloud Service é quinta-feira, 7 de agosto de 2025.

A próxima versão está planejada para sexta-feira, 4 de setembro de 2025.

## Novidades {#what-is-new}

* **Adobe Experience Hub em breve**

  A partir de 19 de agosto de 2025, o Adobe iniciará uma implantação em fases do novo Experience Hub para todos os usuários do Adobe Experience Manager.

  O Experience Hub é um ponto de partida unificado que fornece experiências personalizadas e contextuais para ajudar os usuários a atingirem as metas com mais rapidez. A implantação será concluída até 26 de agosto de 2025, disponibilizando-a para todos os usuários. A nova Experience Hub pode ser acessada diretamente em [experience.adobe.com](https://experience.adobe.com/). Para saber mais, consulte [Adobe Experience Hub](/help/implementing/cloud-manager/experience-hub.md).

* **A licença do Edge Delivery Services pode ser incluída em um programa HIPAA de maneira automatizada**

  As organizações com requisitos de dados confidenciais ou da área de saúde agora podem usar o Edge Delivery Services de maneira automatizada, permitindo que a conformidade com a HIPAA atenda a padrões normativos rigorosos. <!-- CMGR-70016 -->

* **O BYOG agora está disponível para o Edge Delivery Services**

  O Cloud Manager agora permite configurar repositórios Git externos, permitindo fluxos de trabalho flexíveis de gerenciamento de código. <!--(CMGR‑69010, CMGR‑70988) --> Também permite extrair o código de uma ramificação escolhida diretamente na interface do usuário do Cloud Manager, reduzindo as tarefas manuais do repositório. Consulte [Configurar site do Edge Delivery para usar um repositório Git externo](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md) <!-- (CMGR‑68085)(CMGR-69015) --> <!-- KT: https://wiki.corp.adobe.com/display/DMSArchitecture/%5B2025%5D+Cloud+Manager+-+Bring+Your+Own+Git+with+EDS -->

* **Provisionamento automatizado para o novo Complemento do Forms**

  Clientes exclusivos de sites geralmente precisam de uma maneira leve e econômica de criar formulários de marketing. O novo Complemento do AEM Forms Sites atende a essa necessidade, adicionando recursos limitados do Forms a um programa do Sites. Ele também cria um caminho de atualização claro para a oferta completa do AEM Forms. <!-- (CMGR-64301) --> <!-- KT: CMGR Provisioning Support for AEM Forms Sites Add-On SKU https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3578379797 -->

  O complemento:
   * Anexa-se a um programa do Sites e é implantado junto a ele, sem nenhum programa ou direito separado do Forms.
   * Tem como alvo casos de uso de formulários de marketing simples.
   * Aparece na lista **Soluções e complementos** durante a criação do Programa de Produção ou a edição do Programa de Produção, somente quando a Organização IMS mantém licenças complementares disponíveis do Forms.

     ![Complementos do Forms](/help/implementing/cloud-manager/release-notes/assets/forms-add-on.png) *O complemento do Forms só poderá ser adicionado ao Programa se as licenças complementares do Forms estiverem disponíveis na sua Organização IMS.*

     ![Complemento do Forms em Soluções e Complementos ao criar um programa de produção](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-creating-production-program.png) *Durante a Criação do Programa, você pode selecionar o complemento Forms na solução Sites.*

     ![Complemento do Forms ao editar um programa de produção](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-editing-production-program.png) *Em **Editar Programa**, selecione o complemento Forms para o programa Sites e execute o pipeline para ativá-lo nos ambientes.*

     Para obter mais informações, consulte [Criar um programa de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).

## Programas do Beta {#private-beta-program}

Participe dos programas beta da Cloud Manager para obter acesso exclusivo aos recursos futuros antes do lançamento geral.

As seguintes oportunidades estão disponíveis no momento:

### Reversão de um clique para implantações de pipeline {#one-click-rollback}

Reverta rapidamente para uma implantação anterior se o código-fonte do cliente mais recente não estiver funcionando como esperado — não é necessário executar novamente o pipeline completo ou reverter as confirmações manualmente.<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![Restaurar o código-fonte do cliente a partir do cartão Ambientes](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *cartão Ambientes acima, mostrando a opção **Restaurar**>**Código anterior implantado**para um ambiente selecionado.*

![Restaurar caixa de diálogo implantada de código anterior](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*Na caixa de diálogo **Restaurar código anterior implantado**, revise a versão implantada no momento e a versão que deseja restaurar e clique em **Confirmar***.

![Restaurando a ativação](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
O *Cloud Manager reverte o ambiente para a compilação anterior, mantém o conteúdo e a configuração intactos e marca o ambiente **Restaurando**até que a implantação seja concluída.*

![Versão do código Source em uso](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *A exibição de detalhes do Ambiente, como visto acima, agora também mostra a versão ativa do código-fonte em uso.*

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [restorecode@adobe.com](mailto:restorecode@adobe.com) com seu endereço de email associado à sua Adobe ID.

Consulte [Restaurar o código anterior implantado no AEM as a Cloud Service](/help/operations/restore-previous-code-deployed.md).

Consulte também [Restauração de Conteúdo no AEM as a Cloud Service](/help/operations/restore.md).

### Ambiente de testes especializados {#specialized-test-environment}

O Cloud Manager agora oferece suporte à adição de um novo tipo de ambiente chamado **Ambiente de teste especializado**. O ambiente foi projetado para ajudar as equipes a validar recursos em condições próximas da produção antes de entrar em funcionamento. Este tipo de ambiente é diferente dos ambientes *Produção + Preparo*, *Desenvolvimento* ou *Desenvolvimento rápido* e oferece um espaço focalizado para execução de cenários de validação avançados.

**Aprimoramentos recentes**

* Agora você pode configurar um Ambiente de teste especializado em um pipeline de não produção por meio de um fluxo de trabalho mais simples e intuitivo. A configuração simplificada acelera a conclusão e reduz os erros de configuração.
* Agora há suporte para **Copiar Conteúdo** em Ambientes de Teste Especializados. Agora você pode executar o **Copiar Conteúdo** com segurança em ambientes de teste isolados que espelham a Produção. <!-- (CMGR‑68900) -->

Consulte [Adicionar um ambiente de teste especializado](/help/implementing/cloud-manager/specialized-test-environment.md).

![Caixa de diálogo Adicionar ambiente com o botão de opção Ambiente de teste especializado selecionado](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

>[!NOTE]
>
>A Adobe fechou solicitações de acesso beta para Ambientes de teste especializados, tendo atingido um número suficiente de participantes. O recurso agora está em preparação para disponibilidade geral.

<!--
If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


### Traga seu próprio Git (BYOG) {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Os clientes agora podem integrar seus repositórios Git do Azure DevOps no Cloud Manager, com suporte para repositórios DevOps do Azure modernos e repositórios VSTS herdados (Visual Studio Team Services).

* Para usuários do Edge Delivery Services, o repositório integrado pode ser usado para sincronizar e implantar o código do site.
* Para usuários do AEM as a Cloud Service e do Adobe Managed Services (AMS), o repositório pode ser vinculado a pipelines de pilha completa e de front-end.

Em breve, haverá suporte para tipos adicionais de pipeline e validação de solicitação de pull por meio de pipelines de qualidade de código.

Consulte [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Caixa de diálogo Adicionar repositório](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->

**Perguntas frequentes sobre o BYOG**

| Pergunta | Resposta |
|---|---|
| *Como um projeto pode voltar para o repositório Git gerenciado pela Adobe, se necessário?* | É simples voltar atrás. [Atualize os pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) para apontar para o repositório do Adobe e remover o repositório externo se ele não for mais necessário. |
| *É possível configurar repositórios diferentes para ambientes diferentes (por exemplo, não produção versus produção) para permitir testes em não produção primeiro?* | Sim, repositórios diferentes podem ser configurados para ambientes separados. Por exemplo, o pipeline de desenvolvimento ou qualidade do código pode apontar para um repositório externo enquanto o pipeline de produção permanece conectado ao repositório do Adobe. Verifique se o trabalho de sincronização entre os dois repositórios permanece ativo durante essa configuração. |
| *As configurações existentes como as listas `IP Allow` continuam a funcionar?* | Sim, as listas `IP Allow` existentes continuam a funcionar normalmente. No entanto, se o repositório Git externo estiver protegido por um firewall, os [endereços IP Adobe necessários deverão ser adicionados à lista de permissões](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *Todos os URLs de repositório do GitLab funcionam? A URL de repositório em uso segue o formato `https://gitlab_dedicated_url.com/path/repo-name.git`, que difere do exemplo na documentação.* | Sim, qualquer repositório do GitLab com suporte para API V3 ou V4 tem suporte, incluindo URLs do GitLab auto-hospedados como o descrito em [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Gerenciar tokens de acesso{#manage-access-tokens}

Use **Gerenciar Tokens de Acesso** no Cloud Manager para exibir, renomear e excluir tokens de acesso associados a repositórios BYOG externos, como GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.

Consulte [Gerenciar Tokens de Acesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->

### Adicionar pipeline de configuração do Edge Delivery {#add-eds-pipeline}

Os Pipelines de configuração agora são compatíveis com sites criados com o Edge Delivery Services, expandindo esse recurso além dos ambientes do Cloud Service. Você pode usar **Pipelines de configuração** para gerenciar configurações como regras de filtragem de tráfego e configurações do Firewall do Aplicativo Web (WAF), quando aplicável. Consulte [Configurações com Suporte](/help/operations/config-pipeline.md#configurations).

**Aprimoramento recente**

* Os pipelines do Edge Delivery Services agora exibem **Configuração** na coluna **Código implantado**, permitindo a identificação instantânea de implantações somente de configuração. <!-- CMGR‑69681 -->
* O Cloud Manager mostra **Adicionar pipeline do Edge Delivery** quando um programa contiver pelo menos um site do Edge Delivery Services e um domínio mapeado. Caso contrário, a opção aparecerá desativada e uma dica de ferramenta explicará os requisitos ausentes. <!-- CMGR‑69680 -->
* A guia **Edge Delivery** mostra um novo widget **Pipelines do Edge Delivery** que lista o Nome, Status, Repositório e Ramificação de cada pipeline. <!-- (CMGR-69052) -->

  ![Widget de pipeline do Edge Delivery mostrando o nome do pipeline, o status, o repositório e a ramificação](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

* O painel **Filtros** adiciona uma seção **Tipo de Entrega**; inclui caixas de seleção **Entrega do Edge** e **Entrega de publicação**. <!-- (CMGR-69682) -->

  ![Painel de filtros mostrando o novo tipo de entrega do Edge e de publicação](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

![Adicionar pipeline do Edge Delivery na lista suspensa Adicionar pipeline](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Adicionar um pipeline do Edge Delivery da página **Visão geral do programa**,**Pipelines**cartão.*

![Caixa de diálogo Adicionar pipeline do Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Caixa de diálogo Adicionar pipeline do Edge Delivery.*

Consulte [Adicionar pipeline de Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) com seu endereço de email associado à sua Adobe ID.


## Correções de erros

* Os pipelines agora fornecem variáveis somente à configuração de domínio ativa do Edge Delivery Services, ignorando qualquer configuração removida durante a recriação do pipeline. <!-- (CMGR‑70039) -->
* A execução do pipeline agora é iniciada de forma confiável; foi corrigido um problema em que alguns pipelines falhavam ao serem iniciados devido a erros internos de manipulação de recursos. <!-- (CMGR‑58167) -->
* A Cópia de conteúdo valida as permissões e bloqueia inicializações do Cloud Manager por usuários que não têm direitos de Gerente de implantação ou Administrador. <!-- (CMGR‑62097) -->


<!-- ## Known issues {#known-issues} -->

