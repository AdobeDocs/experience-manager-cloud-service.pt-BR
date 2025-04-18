---
title: Notas de versão do Cloud Manager 2025.4.0
description: Saiba mais sobre o lançamento do Cloud Manager 2025.4.0 no Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: fcd9ead02ca5061778001d954ae9a9fc6088d5d1
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 41%

---

# Notas de versão do Cloud Manager 2025.4.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Saiba mais sobre o lançamento do Cloud Manager 2025.4.0 no AEM (Adobe Experience Manager) as a Cloud Service.


Consulte também as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2025.4.0 no AEM as a Cloud Service é quinta-feira, 10 de abril de 2025.

A próxima versão está planejada para sexta-feira, 8 de maio de 2025.

## Novidades {#what-is-new}

* **(UI) Visibilidade de implantação aprimorada**

  A página de detalhes de execução do pipeline no Cloud Manager agora mostra uma mensagem de status (&quot;*Aguardando - outra atualização em andamento*&quot;) quando uma implantação está aguardando a conclusão de outra implantação. Esse fluxo de trabalho facilita a compreensão do sequenciamento durante a implantação do ambiente.  <!-- CMGR-66890 -->

  ![Caixa de diálogo de implantação de desenvolvimento mostrando detalhes e detalhamento](/help/implementing/cloud-manager/release-notes/assets/dev-deployment.png)

* **(UI) Aprimoramento de validação de domínio**

  Ao adicionar um domínio, o Cloud Manager agora exibe um erro se o domínio já estiver instalado em uma conta do Fastly: &quot;*O domínio já está instalado em uma conta do Fastly. Remova-o primeiro de lá antes de adicionar ao Cloud Service.*&quot;

## Programa de adoção antecipada {#early-adoption}

Participe do Programa de adoção antecipada da Cloud Manager para obter acesso exclusivo aos recursos futuros antes do lançamento geral.

As seguintes oportunidades de adoção antecipada estão disponíveis atualmente:

### Traga seu próprio Git: agora com suporte para GitLab e Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

O recurso **Traga seu próprio Git** foi expandido para incluir suporte para repositórios externos, como GitLab e Bitbucket. Esse novo suporte é uma adição ao suporte já existente para repositórios GitHub privados e empresariais. Ao adicionar esses novos repositórios, também é possível vinculá-los diretamente aos seus pipelines. Você pode hospedar esses repositórios em plataformas de nuvem pública ou em sua infraestrutura ou nuvem privada. Essa integração também elimina a necessidade de sincronização constante do código com o repositório da Adobe e oferece a capacidade de validar solicitações de pull antes de mesclá-las em uma ramificação principal.

Os pipelines que usam repositórios externos (exceto os hospedados pelo GitHub) e o **Acionador de implantação** definidos como **Sobre alterações do Git** agora são iniciados automaticamente.

Consulte [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Caixa de diálogo Adicionar repositório](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Atualmente, as verificações de qualidade do código de solicitação de pull prontas para uso são exclusivas de repositórios hospedados no GitHub, mas uma atualização para estender essa funcionalidade a outros fornecedores Git está em andamento.

Se tiver interesse em testar esse novo recurso e compartilhar o seu feedback, envie um email para [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) do seu endereço de email associado à sua Adobe ID. Inclua qual plataforma Git deseja usar e se você está em uma estrutura de repositório privado/público ou empresarial.

<!--
### AEM Home {#aem-home}

AEM Home introduces a centralized starting point for managing content, assets, and sites within Adobe Experience Manager. Designed to deliver a personalized experience, AEM Home lets you navigate the AEM ecosystem seamlessly according to your roles and goals. Acting as a guide, it provides key insights and recommended actions to help you achieve your objectives efficiently. With a clear, persona-driven layout, AEM Home ensures quick access to essential tools, supporting a streamlined and effective experience across all AEM features.

Available to early adopters, AEM Home offers an optimized experience focused on improving workflows, prioritizing goals, and delivering results. Opting in lets you influence AEM Home's development by providing feedback that helps shape its future and enhances its value for the entire AEM community.

If you are interested in testing this new capability and sharing your feedback, send an email to [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) from your email address associated with your Adobe ID. Be sure to include the following information:

* The role that best fits your profile: Content author, Developer, Business owner, Admin, or Other (provide a description).
* Your primary AEM access surface: AEM Sites, AEM Assets, AEM Forms, Cloud Manager, or Other (provide a description). -->

## Correções de erros

* **Problema com certificados sem o campo Nome Comum (CN)**

  O Cloud Manager não lança mais uma resposta NullPointerException (NPE) e 500 HTTP ao processar certificados EV/OV que não incluem um Nome Comum (CN) no campo Assunto. Os certificados modernos geralmente omitem o CN e, em vez disso, usam o Nome alternativo de requerente (SAN). Essa correção garante que a ausência de CN não cause mais uma falha durante o processo de criação da configuração quando a SAN estiver presente. <!-- CMGR-67548 -->

* **Problema de verificação de domínio com correspondência de certificado incorreta**

  O Cloud Manager não verifica mais os domínios incorretamente usando certificados errados. Anteriormente, a lógica de validação usava a correspondência baseada em padrões em vez da correspondência exata, o que fazia com que domínios como `should-not-be-verified.example.com` aparecessem como verificados devido a sobreposição com certificados válidos para `example.com`. Essa correção garante que a validação do domínio agora verifique se há correspondências exatas, evitando associações de certificado incorretas. <!-- CMGR-67225 -->

* **Exclusividade imposta para nomes de encaminhamento de portas de Rede Avançada**

  O Cloud Manager agora impõe nomes exclusivos para encaminhamentos de portas de rede avançada. Anteriormente, nomes duplicados eram permitidos, o que poderia gerar conflitos. Essa correção garante que cada entrada de encaminhamento de porta tenha um nome distinto, alinhado às práticas recomendadas para a integridade da configuração de rede. <!-- CMGR-67082 -->


<!-- ## Known issues {#known-issues} -->

