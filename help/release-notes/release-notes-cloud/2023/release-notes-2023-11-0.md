---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.11.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.11.0.
exl-id: 19cff082-80aa-445c-9462-5e319b7fe0e9
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 16%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2023.11.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2023.11.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2023.11.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 30 de novembro de 2023. O próximo lançamento de recursos (2023.12.0) está planejado para sexta-feira, 14 de dezembro de 2023.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de novembro de 2023 que exibe um resumo dos recursos adicionados na versão 2023.11.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programa de adoção antecipada {#sites-early-adopter}

**[Localizar e substituir cadeias de caracteres em fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**: o Console de Fragmentos de conteúdo fornece aos usuários uma maneira fácil e intuitiva de substituir uma cadeia de caracteres que aparece em vários fragmentos de conteúdo de uma só vez, para ajudar a acelerar a velocidade do conteúdo.

![Localizar e Substituir](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

Interessado em experimentar o recurso e compartilhar feedback? Envie um email para **aemcs-headless-adopter@adobe.com** a partir da sua ID de email oficial para saber mais sobre o programa de adoção antecipada.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na exibição do Assets {#assets-view-features}

* **Editor do Adobe Express incorporado no AEM Assets**: os usuários com acesso ao Express agora têm ferramentas integradas de edição e criação de imagens do Adobe Express e do Adobe Firefly disponíveis diretamente no AEM Assets para melhorar a reutilização do conteúdo e acelerar a velocidade do conteúdo.

  ![Atribuir formulário de metadados a uma pasta](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **Relatórios de uso de armazenamento em Insights**: os administradores agora podem exibir os relatórios de uso de armazenamento disponíveis como parte dos Insights.

  ![Insights do uso do armazenamento](/help/assets/assets/storage-usage-insights.png)

* **Pesquisar configuração da primeira página inicial**: o Experience Manager Assets agora permite que você configure a experiência de página inicial para sua organização. Se você selecionar a opção “Pesquisar primeiro” como a página inicial, poderá configurar o alinhamento da barra de pesquisa, a imagem do fundo e o logotipo da sua organização.

  ![Configuração “Pesquisar primeiro”](/help/assets/assets/search-first-configuration.png)

### Novos recursos no pré-lançamento do Admin View {#admin-view-features-prerelease}

**Visualização de vídeo**: o AEM Assets agora gera representações de visualização de todos os formatos de vídeo com suporte por padrão, sem a necessidade de configurar um perfil de processamento.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos Recursos em [!DNL Experience Manager Forms] {#forms-features}

* **[Componente de caixa de seleção](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: o Forms adaptável baseado em Componentes principais agora pode incluir um componente de caixa de seleção. Permite que os usuários façam escolhas binárias, selecionando ou desmarcando uma opção específica. Normalmente, ela aparece como uma pequena caixa que pode ser clicada ou tocada para alternar entre dois estados: marcado e desmarcado. A caixa de seleção é um elemento de formulário comum usado para apresentar uma opção sim/não ou verdadeira/falsa.

* **[Componente de Termos e Condições](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: o Forms Adaptável baseado em Componentes Principais agora pode incluir um componente de Termos e Condições. Ele permite que os autores de formulários introduzam uma seção específica no formulário em que os usuários recebem os termos, condições ou contratos legais associados ao uso de um serviço, produto ou plataforma. Esse componente foi projetado para informar os usuários sobre as regras, regulamentos e obrigações aos quais eles estão concordando ao enviar o formulário.

  ![Caixa de seleção, Termos e condições e componentes da guia Vertical](/help/forms/assets/forms-components.png)

* **[Componente de guias verticais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: o Forms adaptável baseado em Componentes principais agora pode organizar o conteúdo do formulário em uma lista vertical de guias, fornecendo um layout estruturado e navegável. O uso de guias verticais em um formulário pode aprimorar a experiência geral do usuário simplificando a navegação e melhorando a organização do conteúdo do formulário, especialmente em situações em que um formulário contém várias seções ou informações complexas.



### Novos recursos no pré-lançamento do [!DNL Forms] {#prerelease-features-forms}

* **[Conecte um Forms adaptável com a Lista do Microsoft® SharePoint](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**: o AEM Forms fornece uma integração OOTB para enviar dados de formulários diretamente para a Lista do SharePoint, permitindo que você aproveite os recursos das Listas do SharePoint. Você pode configurar a Lista de SharePoint do Microsoft como uma fonte de dados para um Modelo de dados de formulário e usar a ação de envio **Enviar usando o Modelo de dados de formulário** para conectar um Formulário adaptável à Lista de SharePoint.

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programa de adoção antecipada {#forms-early-adopter}

* **Enviar um Formulário Adaptável para o Cenário do Adobe Workfront Fusion**: o Forms as a Cloud Service oferece opções predefinidas para conectar facilmente um Formulário Adaptável ao Adobe Workfront. Isso simplifica o processo de envio de um Formulário adaptável para um cenário do Adobe Workfront, permitindo acionar um cenário do Workfront Fusion no envio de um Formulário adaptável.

* **Suporte de idiomas da direita para a esquerda**: o Forms adaptável integrado aos Componentes principais agora pode ser apresentado em um idioma da direita para a esquerda (RTL), como árabe, persa e urdu. As línguas RTL são faladas por mais de 2 bilhões de pessoas em todo o mundo. Usar um formulário em linguagem RTL permite estender o alcance dos formulários adaptáveis para atender a esses públicos diversos e aproveitar os mercados de RTL. Em algumas regiões, também é um mandato legal fornecer formulários no idioma local. Ao acomodar idiomas locais, você não só abre portas para um público mais amplo, como também garante a conformidade com as leis e regulamentos relevantes.

  ![Suporte de idioma da direita para a esquerda](/help/forms/assets/right-to-left-language-support.png)

* **[Proteja seus documentos com as APIs do DocAssurance (Parte das APIs de Comunicação)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: as APIs do DocAssurance permitem proteger informações confidenciais ao assinar e criptografar os documentos. Por meio da criptografia, o conteúdo de um documento é transformado em um formato ilegível, garantindo que somente usuários autorizados possam ter acesso. Essa camada fortificada de proteção não apenas protege dados valiosos de olhos não autorizados, mas também proporciona tranquilidade. As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos.

  Você pode escrever para `aem-forms-ea@adobe.com` a partir de sua ID de email oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Agora As Regras De Filtro De Tráfego Do WAF Podem Ser Licenciadas {#cdn-waf-license}

As Regras de filtro de tráfego foram lançadas em outubro e incluíram uma observação de que a categoria especial de regras do Web Application Firewall (WAF) estaria disponível no final deste ano para complementar as regras já disponíveis para clientes do Sites e do Forms. Como atualização, a oferta de Proteção WAF-DDoS agora pode ser licenciada.

Depois de licenciadas, essas regras avançadas do WAF podem ser implantadas na CDN usando o Cloud Manager Configuration Pipeline para adicionar uma camada extra de proteção contra ataques da Web.

Leia sobre [Regras de Filtro de Tráfego](/help/security/traffic-filter-rules-including-waf.md), incluindo o WAF. Fale com a equipe de conta da AEM sobre o licenciamento da Proteção WAF-DDoS ou Segurança aprimorada.

### Programa de Primeiros usuários do mapeamento de domínio {#cdn-config-early-adopter}

Além das [Regras de Filtro de Tráfego (incluindo o WAF)](/help/security/traffic-filter-rules-including-waf.md) recém-lançadas, há uma oportunidade de usar o Pipeline de Configuração para declarar e implantar outros tipos de configuração de CDN. Adoraríamos saber sobre seus casos de uso, incluindo:

* Redirecionamentos do lado do cliente 301/302
* solicitações de proxy na borda para origens arbitrárias
* Transformações de URL
* definindo ou modificando cabeçalhos de solicitação ou resposta
* páginas de erro personalizadas quando o CDN não consegue acessar o AEM
* autenticação por nome de usuário/senha
* qualquer outra configuração útil do CDN

Envie um email para **aemcs-cdn-config-adopter@adobe.com** a partir da sua ID de email oficial com seus comentários.

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Problemas conhecidos {#known-issues}

* Não é possível enviar o Forms adaptável com base nos Componentes principais. O problema ocorre para o Forms adaptável criado usando os Componentes principais versões 2.0.38 - 2.0.60.

  Para resolver o problema. você pode migrar para os Componentes principais do formulário adaptável versão 2.0.62 ou posterior. Para definir uma versão dos Componentes principais do Forms adaptável para seu ambiente, defina versões das dependências `core.forms.components.version`, `core.forms.components.af.version` e `core.wcm.components.version component` no repositório do Forms as a Cloud Service ou no projeto baseado no Arquétipo do AEM e implante as alterações no ambiente do Forms as a Cloud Service. Você pode encontrar a versão mais recente das dependências dos Componentes principais do Forms adaptável em [Repositório Git dos Componentes principais do Forms adaptável](https://github.com/adobe/aem-core-forms-components#system-requirements).
