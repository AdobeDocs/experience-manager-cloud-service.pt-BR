---
title: Notas de versão do Adobe Experience Manager como Cloud Service para 2020.4.0
description: Notas de versão do Experience Manager para 2020.4.0
translation-type: tm+mt
source-git-commit: 49137535f4f6a6b62e697de6a7a9934f5b861bbc

---


# Release Notes for Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

The following section outlines the general release notes for [!DNL Experience Manager] as a Cloud Service 2020.4.0.

## Release Date {#release-date}

A data de lançamento para [!DNL Experience Manager] o Cloud Service 2020.4.0 é 9 de abril de 2020.

## What&#39;s New in Assets {#assets}

Saiba mais sobre novos recursos, melhorias e correções de erros para [!DNL Experience Manager Assets] e [!DNL Dynamic Media] na versão atual.

* [O Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) oferece suporte aos casos de uso de distribuição de ativos para os Ativos do Experience Manager. [!DNL Brand Portal]O auxilia as organizações a atender às suas necessidades de marketing, distribuindo com segurança os ativos de marca e produto aprovados a agências externas, parceiros, equipes internas e revendedores para download.
   * [!DNL Brand Portal] a configuração é concluída pelo [!DNL Adobe I/O] console.
   * A origem de ativos no ainda não [!DNL Brand Portal] é compatível com o [!DNLEExperience Manager] como um serviço em nuvem.

* [O Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) v2.0 funciona com [!DNL Experience Manager] um serviço em nuvem. [!DNL Adobe Asset Link] simplifica a colaboração entre criativos e profissionais de marketing no processo de criação de conteúdo, conectando-se [!DNL Experience Manager Assets] aos aplicativos de [!DNL Creative Cloud] desktop [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign] por meio do painel no aplicativo [!DNL Asset Link] .
   * [!DNL Experience Manager] é pré-configurado para [!DNL Adobe Asset Link], o que resulta em configuração [](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html) fácil e implantação mais rápida para profissionais criativos.
   * [!DNL Asset Link] agora oferece suporte a um alternador [de ambientes do](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) Experience Manager que permite que usuários criativos se conectem facilmente a um [!DNL Experience Manager] ambiente diferente. Um exemplo onde essa funcionalidade é útil é para designers de agências que trabalham com vários clientes usando diferentes [!DNL Experience Manager Assets] implantações.

* Os usuários podem configurar workflows [de](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) pós-processamento para start automático na interface de usuário [!UICONTROL Propriedades] da pasta para as hierarquias de pastas específicas.
   * A interface de usuário [!UICONTROL Propriedades] da pasta é simplificada, com a nova guia Processamento [!UICONTROL de] ativos contendo perfil de metadados, perfil de processamento e a nova configuração de fluxo de trabalho de start automático.
   * A caixa de diálogo de reprocessamento de ativos permite selecionar um perfil de processamento específico e decidir reprocessar em subpastas.
   * [!DNL Dynamic Media]: Adicionada a configuração de publicação seletiva para que os ativos sejam publicados automaticamente apenas para pré-visualização segura. Além disso, os ativos podem ser publicados explicitamente no Experience Manager sem publicação no DMS7 para delivery no domínio público.

### Correções de erros {#assets-bug-fixes}

* Correções para problemas de processamento de ativos.
* Correções em ativos [!DNL Dynamic Media] de configuração e publicação para o serviço [!DNL Dynamic Media] delivery.

>[!MORELIKETHIS]
>
>* [Sobre o Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Configurar o Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [Configurar o Experience Manager para trabalhar com o Asset Link](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [Criar fluxo de trabalho no Experience Manager usando os microserviços de ativos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)


## Novidades do Cloud Manager {#whats-new-cloud-manager}

* Os URLs do editor agora estão disponíveis na página do Ambiente na interface do usuário do Cloud Manager.
* Alterações na navegação para permitir que o usuário edite, alterne ou adicione um programa da página de visão geral do Cloud Manager.
* Alterações para permitir que o usuário edite o programa do cartão de programa na landing page do Cloud Manager.
* Novo status de pipeline **Pipeline Running** exibido no ambiente ao qual está associado.
* Melhorias na compreensão da página de execução de pipeline. Isso inclui a exibição do nome do Pipeline (somente pipeline de não produção) e do tipo e um selo para indicar se o status do pipeline está Em andamento/Cancelado/Com falha.
* Dicas de ferramentas para melhorar a experiência e a compreensão do usuário sobre por que o botão Adicionar Programa/Ambiente está desativado.
* Ambientes com falha podem ser excluídos por meio da interface do usuário e da API.
* O processo usado para gerar senhas git tornou-se mais resiliente a problemas na camada de serviço subjacente.

### Correções de erros {#bug-fixes-cloud-manager}

* Os links para o ambiente stage na página de detalhes de execução do pipeline não navegavam consistentemente para o local correto.
* As etapas individuais no processo de criação do ambiente atingiriam o tempo limite mais cedo do que o necessário, causando a falha do processo.
* A configuração Maven usada no container build foi atualizada para evitar bloqueios ao baixar metadados de artefato.
* Em alguns casos, a etapa Construir imagem falharia ao baixar os pacotes do cliente com êxito.
* Algumas condições raras impediriam a exclusão de ambientes.
* As notificações da Experience Cloud não foram recebidas de forma consistente.
