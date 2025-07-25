---
title: Notas de versão do Cloud Manager 2025.7.0
description: Saiba mais sobre o lançamento do Cloud Manager 2025.7.0 no Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: f3e31d1f17283086cd6fe9e73d67feac938d6567
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 8%

---

# Notas de versão do Cloud Manager 2025.7.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Saiba mais sobre o lançamento do Cloud Manager 2025.7.0 no AEM (Adobe Experience Manager) as a Cloud Service.

Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2025.7.0 no AEM as a Cloud Service é quinta-feira, 10 de julho de 2025.

A próxima versão está planejada para sexta-feira, 7 de agosto de 2025.

## Novidades {#what-is-new}

* **O Cloud Manager adiciona o suporte ao certificado SSL ECDSA (Elliptic Curve Digital Signature Algorithm)**

  O Cloud Manager agora é compatível com certificados ECDSA. O recurso oferece forte segurança com chaves de tamanhos menores, permitindo que os clientes apliquem criptografia leve e moderna em suas configurações de CDN. <!-- https://jira.corp.adobe.com/browse/CMGR-62399 -->

* **Baixar relatório de uso de licença do site**

  Na página **Detalhes de uso do Sites** (no Cloud Manager, clique em **Licença**. Na tabela Soluções, na linha **Sites**, clique em **Exibir detalhes de uso**). Agora os clientes podem clicar em **Baixar relatório** para exportar seus dados como um arquivo CSV. Este download simplifica a análise e o compartilhamento de tendências de uso. <!-- https://jira.corp.adobe.com/browse/CMGR-42274 -->

  ![Página de detalhes de uso do Sites](/help/implementing/cloud-manager/release-notes/assets/sites-license-usage-page.png)

  Consulte [Painel de licenças](/help/implementing/cloud-manager/license-dashboard.md).

## Programas do Alpha/Beta {#private-beta-program}

Participe dos programas alfa e beta da Cloud Manager para obter acesso exclusivo aos recursos futuros antes do lançamento geral.

As seguintes oportunidades estão disponíveis no momento:

### Reversão de um clique para implantações de pipeline {#one-click-rollback}

Reverta rapidamente para uma implantação anterior se o código-fonte do cliente mais recente não estiver funcionando como esperado — não é necessário executar novamente o pipeline completo ou reverter as confirmações manualmente.<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![Restaurar o código-fonte do cliente a partir do cartão Ambientes](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *cartão Ambientes acima, mostrando a opção **Restaurar**>**Código anterior implantado**&#x200B;para um ambiente selecionado.*


![Restaurar caixa de diálogo implantada de código anterior](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*Na caixa de diálogo **Restaurar código anterior implantado**, revise a versão implantada no momento e a versão que deseja restaurar e clique em **Confirmar***.


![Restaurando a ativação](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
O *Cloud Manager reverte o ambiente para a compilação anterior, mantém o conteúdo e a configuração intactos e marca o ambiente **Restaurando**&#x200B;até que a implantação seja concluída.*


![Versão do código Source em uso](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *A exibição de detalhes do Ambiente, como visto acima, agora também mostra a versão ativa do código-fonte em uso.*

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [restorecode@adobe.com](mailto:restorecode@adobe.com) com seu endereço de email associado à sua Adobe ID.

Consulte [Restaurar o código anterior implantado no AEM as a Cloud Service](/help/operations/restore-previous-code-deployed.md).

Consulte também [Restauração de Conteúdo no AEM as a Cloud Service](/help/operations/restore.md).


### Ambiente de testes especializados {#specialized-test-environment}

O Cloud Manager agora oferece suporte à adição de um novo tipo de ambiente chamado **Ambiente de teste especializado**. O ambiente foi projetado para ajudar as equipes a validar recursos em condições próximas da produção antes de entrar em funcionamento. Este tipo de ambiente é diferente dos ambientes *Produção + Preparo*, *Desenvolvimento* ou *Desenvolvimento rápido* e oferece um espaço focalizado para execução de cenários de validação avançados.

Aprimoramento recente: agora você pode configurar ambientes de teste especializados em um pipeline de não produção por meio de um fluxo de trabalho mais simples e intuitivo. A configuração simplificada acelera a conclusão e reduz os erros de configuração.

Consulte [Adicionar um ambiente de teste especializado](/help/implementing/cloud-manager/specialized-test-environment.md).

![Caixa de diálogo Adicionar ambiente com o botão de opção Ambiente de teste especializado selecionado](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) com seu endereço de email associado à sua Adobe ID.


### Traga seu próprio Git (BYOG) - agora com suporte para Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Os clientes agora podem integrar seus repositórios Git do Azure DevOps no Cloud Manager, com suporte para repositórios DevOps do Azure modernos e repositórios VSTS herdados (Visual Studio Team Services).

* Para usuários do Edge Delivery Services, o repositório integrado pode ser usado para sincronizar e implantar o código do site.
* Para usuários do AEM as a Cloud Service e do Adobe Managed Services (AMS), o repositório pode ser vinculado a pipelines de pilha completa e de front-end.

Em breve, haverá suporte para tipos adicionais de pipeline e validação de solicitação de pull por meio de pipelines de qualidade de código.

Consulte [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Caixa de diálogo Adicionar repositório](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

Se tiver interesse em testar esse novo recurso e compartilhar o seu feedback, envie um email para [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) do seu endereço de email associado à sua Adobe ID. Inclua qual plataforma Git deseja usar e se você está em uma estrutura de repositório privado/público ou empresarial.


**Perguntas frequentes sobre o BYOG**

| Pergunta | Resposta |
|---|---|
| *Como um projeto pode voltar para o repositório Git gerenciado pela Adobe, se necessário?* | É simples voltar atrás. [Atualize os pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) para apontar para o repositório do Adobe e remover o repositório externo se ele não for mais necessário. |
| *É possível configurar repositórios diferentes para ambientes diferentes (por exemplo, não produção versus produção) para permitir testes em não produção primeiro?* | Sim, repositórios diferentes podem ser configurados para ambientes separados. Por exemplo, o pipeline de desenvolvimento ou qualidade do código pode apontar para um repositório externo enquanto o pipeline de produção permanece conectado ao repositório do Adobe. Verifique se o trabalho de sincronização entre os dois repositórios permanece ativo durante essa configuração. |
| *As configurações existentes, como listas de permissões IP, continuam a funcionar?* | Sim, as listas de permissões IP existentes continuam a funcionar normalmente. No entanto, se o repositório Git externo estiver protegido por um firewall, os [endereços IP Adobe necessários deverão ser adicionados à lista de permissões](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *Todos os URLs de repositório do GitLab funcionam? A URL de repositório em uso segue o formato `https://gitlab_dedicated_url.com/path/repo-name.git`, que difere do exemplo na documentação.* | Sim, qualquer repositório do GitLab com suporte para API V3 ou V4 tem suporte, incluindo URLs do GitLab auto-hospedados como o descrito em [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Gerenciar tokens de acesso{#manage-access-tokens}

Use **Gerenciar Tokens de Acesso** no Cloud Manager para exibir, renomear e excluir tokens de acesso associados a repositórios BYOG externos, como GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.

Consulte [Gerenciar Tokens de Acesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) com seu endereço de email associado à sua Adobe ID.


### Adicionar pipeline de configuração do Edge Delivery {#add-eds-pipeline}

Os Pipelines de configuração agora são compatíveis com sites criados com o Edge Delivery Services, expandindo esse recurso além dos ambientes do Cloud Service. Você pode usar **Pipelines de configuração** para gerenciar configurações como regras de filtragem de tráfego e configurações do Firewall do Aplicativo Web (WAF), quando aplicável. Consulte [Configurações com Suporte](/help/operations/config-pipeline.md#configurations).

![Adicionar pipeline do Edge Delivery na lista suspensa Adicionar pipeline](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Adicionar um pipeline do Edge Delivery da página **Visão geral do programa**,**Pipelines**&#x200B;cartão.*

![Caixa de diálogo Adicionar pipeline do Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Caixa de diálogo Adicionar pipeline do Edge Delivery.*

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) com seu endereço de email associado à sua Adobe ID.


## Correções de erros

* O Cloud Manager agora atualiza a versão de lançamento de todos os pipelines durante as atualizações do ambiente, garantindo um rastreamento consistente de versões em todos os tipos de pipeline. <!-- CMGR-69043 -->
* A interface do usuário agora exibe mensagens de erro de status e detalhadas quando um certificado SSL de Validação de domínio (DV) falha, ajudando a entender e resolver problemas de certificado. <!-- CMGR-68872 -->
* Ao editar um mapeamento de domínio, a interface do usuário agora impede a seleção de certificados SSL que não correspondem ao domínio escolhido, reduzindo erros de configuração e melhorando a confiabilidade durante a configuração. <!-- CMGR-64307 -->
* Em algumas situações, os certificados não eram excluídos corretamente, mantendo o domínio ainda ativo. <!-- CMGR-69867 -->
* Correção de um problema que poderia bloquear atualizações do *Adobe Assets* para o *Adobe Assets Ultimate* em determinados casos. As transições agora são mais tranquilas e confiáveis. <!-- CMGR-69506 -->
* Solução de um problema em que os campos principais de região são definidos automaticamente ao criar ambientes de várias regiões para oferecer suporte a serviços e implantações downstream sem problemas. <!-- CMGR-69471 -->
* Correção de um problema em que alguns pipelines de configuração não eram interrompidos corretamente após a execução. Agora, os pipelines são concluídos com sucesso e fechados conforme esperado, melhorando a confiabilidade. <!-- CMGR-69344 -->


<!-- ## Known issues {#known-issues} -->

