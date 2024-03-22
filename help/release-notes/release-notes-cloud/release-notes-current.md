---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: d0b7ec258a7a2c1d83f4d9a8983945a81c83aa2f
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 23%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2024.1.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 25 de janeiro de 2024. O próximo lançamento de recursos (2024.3.0) está planejado para sexta-feira, 4 de abril de 2024.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo de Visão geral da versão de janeiro de 2024 que exibe um resumo dos recursos adicionados na versão 2024.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3427041?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Extension Manager no AEM Sites {#sites-extension-manager}

**Explore o novo [Extension Manager no AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/)** para personalizar a configuração do AEM definindo as extensões da interface do usuário.

![Extension Manager no AEM Sites](/help/assets/sites/extension-manager/homepage.png)

O Extension Manager no AEM Sites permite que desenvolvedores e profissionais acessem, gerenciem e personalizem [Extensões da interface](https://developer.adobe.com/uix/docs/) criado com [Construtor de aplicativos Adobe](https://developer.adobe.com/app-builder/) para aprimorar a funcionalidade do AEM Sites.
Com o Extension Manager, é possível:

* Ativar ou desativar extensões por instância;
* Configurar parâmetros de extensão;
* Visualizar extensões e gerar um link de visualização compartilhável;
* Descubra recursos de extensibilidade da interface do usuário por meio de demonstrações interativas;
* Acesse recursos experimentais do Adobe por meio de extensões primárias.

Estamos buscando ativamente feedback e novos casos de uso para extensões da interface do usuário. Se quiser se conectar, envie um email para `uix@adobe.com`.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Recursos de pré-lançamento da exibição do administrador {#admin-view-prerelease}

**Visualizar representações para todos os tipos de vídeo compatíveis**

O Experience Manager Assets agora gera representações de pré-visualização de todos os tipos de vídeo compatíveis por padrão, sem exigir uma configuração de perfil de processamento

### Exibição de ativos {#assets-view-features}

**Tags inteligentes na lista de bloqueios**

O Assets Essentials agora permite definir uma lista de bloqueios que inclui palavras que não devem ser adicionadas como Tags inteligentes aos ativos quando eles são enviados ao repositório. Esse recurso ajuda a manter a conformidade da marca e reduz o esforço para moderar as Tags inteligentes.

![Tags inteligentes do incluo na lista de bloqueios](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programa de adoção antecipada {#forms-early-adopter}

* **[Enviar um formulário adaptável para o cenário do Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: o Forms as a Cloud Service oferece opções prontas para uso para conectar facilmente um Formulário adaptável ao Adobe Workfront. Isso simplifica o processo de envio de um Formulário adaptável para um cenário do Adobe Workfront, permitindo acionar um cenário do Workfront Fusion no envio de um Formulário adaptável.

* **[Suporte de idiomas da direita para a esquerda](/help/forms/supporting-new-language-localization-core-components.md)**: o Forms adaptável incorporado aos Componentes principais agora pode ser apresentado em um idioma da direita para a esquerda (RTL), como árabe, persa e urdu. As línguas RTL são faladas por mais de 2 bilhões de pessoas em todo o mundo. Usar um formulário em linguagem RTL permite estender o alcance dos formulários adaptáveis para atender a esses públicos diferentes e selecionar mercados de RTL. Em algumas regiões, também é um mandato legal fornecer formulários no idioma local. Ao acomodar idiomas locais, você não só abre portas para um público mais amplo, como também garante a conformidade com as leis e regulamentos relevantes.

  ![Suporte de idioma da direita para a esquerda](/help/forms/assets/right-to-left-language-support.png)

* **[Protect seus documentos com as APIs DocAssurance (Parte das APIs de comunicação)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: As APIs do DocAssurance permitem proteger informações confidenciais, assinando e criptografando os documentos. Por meio da criptografia, o conteúdo de um documento é transformado em um formato ilegível, garantindo que somente usuários autorizados possam ter acesso. Essa camada fortificada de proteção não apenas protege dados valiosos de olhos não autorizados, mas também proporciona tranquilidade. As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos.

  Você pode escrever para `aem-forms-early-adopter-program@adobe.com` do seu id de email oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso.

* **[Você pode aproveitar o Serviço de dados de monitoramento de usuário real (RUM)](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** para ativar a coleta no lado do cliente para o AEM as a Cloud Service.
O Serviço de dados de monitoramento de usuário real (RUM) oferece um reflexo mais preciso das interações do usuário, garantindo uma medida confiável do engajamento do site. É uma ótima oportunidade para obter insights avançados sobre o desempenho da página. Embora isso seja benéfico para clientes que usam CDN gerenciada por Adobe ou CDN não gerenciada por Adobe. Além disso, para clientes que usam um CDN não gerenciado por Adobe, o relatório de tráfego automatizado agora pode ser ativado para eles, eliminando a necessidade de compartilhar qualquer relatório de tráfego com o Adobe.

  Se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie um email para `aemcs-rum-adopter@adobe.com`, juntamente com o nome de domínio para cada um dos ambientes para os quais você deseja habilitar o RUM, a partir do seu endereço de email associado à sua Adobe ID. A equipe de produtos do Adobe habilitará o Serviço de dados de monitoramento de usuário real (RUM) para você.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Suporte para Dynatrace {#dynatrace}

Os clientes do Dynatrace podem monitorar o uso do AEM. [Saiba como](/help/implementing/cloud-manager/dynatrace.md) para solicitar conectividade com seu ambiente Dynatrace para monitoramento do desempenho do aplicativo. Observe que o APM do New Relic, que está disponível para todos os clientes, deixará de coletar dados se o Dynatrace estiver ativado.

### Suporte RDE para código de front-end usando temas de site e modelos de site: programa Early Adoter {#rde-frontend-early-adopter}

[RDEs (Rapid Development Environments, ambientes de desenvolvimento rápido)](/help/implementing/developing/introduction/rapid-development-environments.md) O agora oferece suporte ao código de front-end com base no [temas de site](/help/sites-cloud/administering/site-creation/site-themes.md) e [modelos de site](/help/sites-cloud/administering/site-creation/site-templates.md), para os participantes iniciais. Com RDEs, isso é feito usando uma diretiva de linha de comando, em vez de uma [pipeline de front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Entre em contato com **aemcs-rde-support@adobe.com** para experimentar e fornecer feedback.

### Programa de adoção antecipada da configuração da CDN {#cdn-config-early-adopter}

Além do recém-lançado [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md), que inclui as regras do WAF (Web Application Firewall) opcionalmente licenciáveis, há uma oportunidade de usar o Pipeline de configuração para declarar e implantar [outros tipos de configuração de CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md). Associe-se ao programa de adoção antecipada enviando um email **aemcs-cdn-config-adopter@adobe.com** para obter acesso a:
* Redirecionamentos do lado do cliente 301/302
* solicitações de proxy na borda para origens arbitrárias
* Transformações de URL
* definindo ou modificando cabeçalhos de solicitação ou resposta
* páginas de erro personalizadas quando o CDN não consegue acessar o AEM

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
