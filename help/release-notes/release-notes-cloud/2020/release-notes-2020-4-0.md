---
title: Notas de versão do Adobe Experience Manager as a Cloud Service para 2020.4.0
description: "[!DNL Adobe Experience Manager] Notas de Versão as a Cloud Service para 2020.4.0."
exl-id: d98a3862-76fa-4b5b-b81a-333f5f532b67
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 93%

---

# Notas de versão do Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

Esta página descreve as notas de versão gerais do [!DNL Experience Manager] as a Cloud Service 2020.4.0.

## Data de lançamento {#release-date}

A Data de lançamento do [!DNL Experience Manager] as a Cloud Service 2020.4.0 é 9 de abril de 2020.

## Novidades do Assets {#assets}

Saiba mais sobre novos recursos, melhorias e correções de erros do [!DNL Experience Manager Assets] e do [!DNL Dynamic Media] na versão atual.

* O [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) oferece suporte aos casos de uso de distribuição de ativos do Experience Manager Assets. O [!DNL Brand Portal] auxilia as organizações a atender às suas necessidades de marketing, distribuindo com segurança os ativos de marca e produto aprovados a agências externas, parceiros, equipes internas e revendedores para download.
   * A configuração do [!DNL Brand Portal] é concluída por meio do console do [!DNL Adobe I/O]. Consulte [Configurar Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html).
   * O fornecimento de ativos no [!DNL Brand Portal] ainda não é compatível com o [!DNL Experience Manager] as a Cloud Service.

* O [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) v2.0 funciona com o [!DNL Experience Manager] as a Cloud Service. O [!DNL Adobe Asset Link] simplifica a colaboração entre profissionais de criação e marketing no processo de criação de conteúdo, conectando o [!DNL Experience Manager Assets] aos aplicativos de desktop do [!DNL Creative Cloud] [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign] por meio do painel no aplicativo do [!DNL Asset Link].
   * O [!DNL Experience Manager] é pré-configurado para [!DNL Adobe Asset Link], o que resulta na [fácil configuração](https://helpx.adobe.com/br/enterprise/using/configure-aem-assets-for-asset-link.html) e implantação mais rápida para os profissionais de criação.
   * Agora o [!DNL Asset Link] oferece suporte a um [alternador de ambientes do Experience Manager](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) que permite que usuários de criação sejam conectados facilmente a um ambiente diferente do [!DNL Experience Manager]. Um exemplo em que essa funcionalidade é útil inclui designers de agências que trabalham com vários clientes, usando diferentes implantações do [!DNL Experience Manager Assets].

* Os usuários podem configurar [fluxos de trabalho pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) para início automático na interface do usuário [!UICONTROL Propriedades] da pasta para as hierarquias de pastas específicas.
   * A interface do usuário [!UICONTROL Propriedades] da pasta é simplificada, com a nova guia [!UICONTROL Processamento de ativos] que contém o perfil de metadados, o perfil de processamento e a nova configuração de fluxo de trabalho de início automático.

     ![Os perfis de processamento podem ser facilmente aplicados a pastas e todos os ativos carregados nas pastas são processados usando esses perfis](/help/assets/assets/asset-processing-folder-properties.png)

   * A opção de reprocessamento de ativos permite selecionar um perfil de processamento específico para reprocessar ativos selecionados pelo usuário nas subpastas.

     ![Reprocessar ativos selecionados usando um perfil de processamento específico](/help/assets/assets/fpo-existing-asset-reprocess.gif)

   * [!DNL Dynamic Media]: adição da configuração de publicação seletiva para que os ativos sejam publicados automaticamente apenas para visualização segura. Além disso, os ativos podem ser publicados explicitamente no Experience Manager, sem publicação no DMS7 para entrega no domínio público.

### Correções de erros {#assets-bug-fixes}

* Correções para problemas de processamento de ativos.
* Correções na configuração do [!DNL Dynamic Media] e publicação de ativos no serviço de entrega do [!DNL Dynamic Media].

>[!MORELIKETHIS]
>
>* [Sobre o Adobe Asset Link](https://www.adobe.com/br/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Configurar Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [Configurar Experience Manager para funcionar com o Asset Link](https://helpx.adobe.com/br/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [Criar fluxo de trabalho no Experience Manager usando microsserviços de ativos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)

## Novidades do Cloud Manager {#whats-new-cloud-manager}

* Agora os URLs do editor estão disponíveis na página Ambiente na interface do usuário do Cloud Manager.
* Alterações na navegação para permitir que o usuário edite, alterne ou adicione um programa na página de visão geral do Cloud Manager.
* Alterações para permitir que o usuário edite o programa no cartão de programa na página de aterrissagem do Cloud Manager.
* Novo status de pipeline **Pipeline Running** exibido no ambiente ao qual está associado.
* Melhorias na compreensão da página de execução do pipeline. Isso inclui a exibição do nome (somente para pipeline de não produção) e tipo do Pipeline e um selo para indicar se o status do pipeline é Em andamento/Cancelado/Com falha.
* Dicas de ferramentas para melhorar a experiência do usuário e a compreensão sobre por que o botão Adicionar Programa/Ambiente está desativado.
* Agora ambientes com falha podem ser excluídos por meio da interface do usuário e da API.
* O processo usado para gerar senhas git tornou-se mais resiliente aos problemas na camada de serviço subjacente.

### Correções de erros {#bug-fixes-cloud-manager}

* Os links para o ambiente de preparo na página de detalhes de execução do pipeline não estavam navegando consistentemente para o local correto.
* As etapas individuais no processo de criação do ambiente atingiriam o tempo limite antes do que o necessário, causando a falha do processo.
* A configuração de Maven usada em Criar contêiner foi atualizada para evitar bloqueios ao baixar metadados de artefato.
* Em alguns casos, a etapa Criar imagem não baixaria os pacotes do cliente com êxito.
* Algumas condições raras impediriam a exclusão de ambientes.
* As notificações da Experience Cloud não eram recebidas de forma consistente.
