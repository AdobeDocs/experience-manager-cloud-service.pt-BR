---
title: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de versão atuais do  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 8eb087bdda335b0a33e616eb534615396b220369
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 13%

---

# Notas de versão atuais do [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

A seção a seguir descreve as notas da versão de recurso atual (mais recente) do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] a versão atual do recurso (2023.11.0) é 30 de novembro de 2023. A próxima versão do recurso (2023.12.0) está planejada para 14 de dezembro de 2023.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de novembro de 2023 que exibe um resumo dos recursos adicionados na versão 2023.11.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programa de adoção antecipada {#sites-early-adopter}

**[Localizar e substituir strings em fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**: o Console do fragmento de conteúdo fornece aos usuários uma maneira fácil e intuitiva de substituir uma cadeia de caracteres que aparece em vários fragmentos de conteúdo de uma só vez para ajudar a acelerar a velocidade do conteúdo.

![Localizar e substituir](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

Interessado em experimentar o recurso e compartilhar feedback? Enviar um email para **aemcs-headless-adopter@adobe.com** da sua ID de e-mail oficial para saber mais sobre o programa dos participantes antecipados.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na visualização de ativos {#assets-view-features}

* **Editor de Adobe Express incorporado no AEM Assets**: os usuários com acesso ao Express agora têm ferramentas integradas de edição e criação de imagens do Adobe Express e do Adobe Firefly disponíveis diretamente no AEM Assets para melhorar a reutilização do conteúdo e acelerar a velocidade dele.

  ![atribuir formulário de metadados a uma pasta](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **Relatórios de uso de armazenamento em Insights**: os administradores agora podem exibir os relatórios de uso de armazenamento disponíveis como parte do Insights.

  ![insights de uso do armazenamento](/help/assets/assets/storage-usage-insights.png)

* **Pesquisar primeira configuração de página inicial**: o Experience Manager Assets agora permite configurar a experiência de página inicial para sua organização. Se você selecionar pesquisar primeiro como página inicial, poderá configurar o alinhamento da barra de pesquisa, a imagem do plano de fundo e o logotipo da sua organização.

  ![pesquisar primeira configuração](/help/assets/assets/search-first-configuration.png)

### Novos recursos no pré-lançamento do Admin View {#admin-view-features-prerelease}

**Visualização de vídeo**: o AEM Assets agora gera representações de pré-visualização de todos os formatos de vídeo compatíveis por padrão, sem a necessidade de configurar um perfil de processamento.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no [!DNL Experience Manager Forms] {#forms-features}

* **[Componente da caixa de seleção](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: o Forms adaptável baseado em Componentes principais agora pode incluir um componente de caixa de seleção. Permite que os usuários façam escolhas binárias, selecionando ou desmarcando uma opção específica. Normalmente, ela aparece como uma pequena caixa que pode ser clicada ou tocada para alternar entre dois estados: marcado e desmarcado. A caixa de seleção é um elemento de formulário comum usado para apresentar uma opção sim/não ou verdadeira/falsa.

* **[Componente dos Termos e condições](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: o Forms adaptável baseado em Componentes principais agora pode incluir um componente de Termos e condições. Ele permite que os autores de formulários introduzam uma seção específica no formulário em que os usuários recebem os termos, condições ou contratos legais associados ao uso de um serviço, produto ou plataforma. Esse componente foi projetado para informar os usuários sobre as regras, regulamentos e obrigações aos quais eles estão concordando ao enviar o formulário.

  ![Caixa de seleção, Termos e condições e componentes da guia Vertical](/help/forms/assets/forms-components.png)

* **[Componente de guias verticais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: o Forms adaptável baseado em Componentes principais agora pode organizar o conteúdo do formulário em uma lista vertical de guias, fornecendo um layout estruturado e navegável. O uso de guias verticais em um formulário pode aprimorar a experiência geral do usuário simplificando a navegação e melhorando a organização do conteúdo do formulário, especialmente em situações em que um formulário contém várias seções ou informações complexas.



### Novos recursos no pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **[Conectar um Forms adaptável com a lista Microsoft® SharePoint](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**: o AEM Forms fornece uma integração OOTB para enviar dados de formulários diretamente para a Lista do SharePoint, permitindo que você aproveite os recursos de Listas do SharePoint. Você pode configurar a Lista de SharePoint do Microsoft como uma fonte de dados para um Modelo de dados de formulário e usar o **Enviar usando modelo de dados do formulário** enviar ação para conectar um Formulário adaptável à Lista do SharePoint.

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programa de adoção antecipada {#forms-early-adopter}

* **Enviar um formulário adaptável para o cenário do Adobe Workfront Fusion**: o Forms as a Cloud Service oferece opções prontas para uso para conectar facilmente um Formulário adaptável ao Adobe Workfront. Isso simplifica o processo de envio de um Formulário adaptável para um cenário do Adobe Workfront, permitindo acionar um cenário do Workfront Fusion no envio de um Formulário adaptável.

* **[Suporte de idiomas da direita para a esquerda](/help/forms/supporting-new-language-localization-core-components.md)**: o Forms adaptável incorporado aos Componentes principais agora pode ser apresentado em um idioma da direita para a esquerda (RTL), como árabe, persa e urdu. As línguas RTL são faladas por mais de 2 bilhões de pessoas em todo o mundo. Usar um formulário em linguagem RTL permite estender o alcance dos formulários adaptáveis para atender a esses públicos diversos e aproveitar os mercados de RTL. Em algumas regiões, também é um mandato legal fornecer formulários no idioma local. Ao acomodar idiomas locais, você não só abre portas para um público mais amplo, como também garante a conformidade com as leis e regulamentos relevantes.

  ![Suporte de idioma da direita para a esquerda](/help/forms/assets/right-to-left-language-support.png)

* **[Protect seus documentos com as APIs DocAssurance (Parte das APIs de comunicação)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: As APIs do DocAssurance permitem proteger informações confidenciais, assinando e criptografando os documentos. Por meio da criptografia, o conteúdo de um documento é transformado em um formato ilegível, garantindo que somente usuários autorizados possam ter acesso. Essa camada fortificada de proteção não apenas protege dados valiosos de olhos não autorizados, mas também proporciona tranquilidade. As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos.

  Você pode escrever para `aem-forms-early-adopter-program@adobe.com` do seu id de email oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Agora as Regras de filtro de tráfego do WAF podem ser licenciadas {#cdn-waf-license}

As Regras de filtro de tráfego foram lançadas em outubro e incluíram uma observação de que a categoria especial de regras do Web Application Firewall (WAF) estaria disponível no final deste ano para complementar as regras já disponíveis para clientes do Sites e do Forms. Como atualização, a oferta de Proteção WAF-DDoS agora pode ser licenciada.

Depois de licenciadas, essas regras avançadas do WAF podem ser implantadas na CDN usando o Cloud Manager Configuration Pipeline para adicionar uma camada extra de proteção contra ataques da Web.

Ler sobre [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md), incluindo o WAF. Fale com a sua equipe de conta AEM sobre o licenciamento da Proteção WAF-DDoS ou Segurança aprimorada.

### Programa adotante antecipado da configuração da CDN {#cdn-config-early-adopter}

Além do recém-lançado [Regras de filtro de tráfego (incluindo WAF)](/help/security/traffic-filter-rules-including-waf.md), há uma oportunidade de usar o Pipeline de configuração para declarar e implantar outros tipos de configuração de CDN. Adoraríamos saber sobre seus casos de uso, incluindo:
* Redirecionamentos do lado do cliente 301/302
* solicitações de proxy na borda para origens arbitrárias
* Transformações de URL
* definindo ou modificando cabeçalhos de solicitação ou resposta
* páginas de erro personalizadas quando o CDN não consegue acessar o AEM
* autenticação por nome de usuário/senha
* qualquer outra configuração útil do CDN

Enviar um email para **aemcs-cdn-config-adopter@adobe.com** da sua ID de email oficial com o seu feedback.

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Problemas conhecidos {#known-issues}

* Não é possível enviar o Forms adaptável com base nos Componentes principais. O problema ocorre para o Forms adaptável criado usando os Componentes principais versões 2.0.38 - 2.0.60.

  Para resolver o problema. você pode migrar para os Componentes principais do formulário adaptável versão 2.0.62 ou posterior. Para definir uma versão dos Componentes principais adaptáveis do Forms para o seu ambiente, [definir versões do componente core.forms.components.version, core.forms.components.af.version e core.wcm.components.version](/help/forms/enable-adaptive-forms-core-components.md#2-add-adaptive-forms-core-components-dependencies-to-your-git-repository) dependências no repositório as a Cloud Service do Forms ou projeto baseado no Arquétipo do AEM e [implantar as alterações no ambiente as a Cloud Service do Forms](/help/forms/enable-adaptive-forms-core-components.md#build-and-deploy-updated-code-on-an-aem-forms-as-a-cloud-service-environment). Você pode encontrar a versão mais recente das dependências dos Componentes principais do Forms adaptável em [Repositório Git dos Componentes principais adaptáveis do Forms](https://github.com/adobe/aem-core-forms-components#system-requirements).
