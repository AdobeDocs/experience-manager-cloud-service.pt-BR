---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.12.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.12.0.
exl-id: b36add58-a2ba-4299-94be-e0026e9c553c
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 27%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2023.12.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2023.12.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2023.12.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 14 de dezembro de 2023. O próximo lançamento de recursos (2024.1.0) está planejado para quinta-feira, 25 de janeiro de 2023.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the December 2023 Release Overview video for a summary of the features added in the 2023.12.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Programa de adoção antecipada {#sites-early-adopter}

**Você pode aproveitar o [Serviço de Telemetria Operacional](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** para habilitar a coleta no lado do cliente para o AEM as a Cloud Service.

O Serviço de dados de telemetria operacional oferece um reflexo mais preciso das interações do usuário, garantindo uma medida confiável do engajamento do site. É uma ótima oportunidade para obter insights avançados sobre o desempenho da página. Embora isso seja benéfico para clientes que usam CDN gerenciada pela Adobe ou CDN não gerenciada pela Adobe. Além disso, para clientes que usam um CDN gerenciado pela Adobe, o relatório de tráfego automatizado agora pode ser ativado para eles, eliminando a necessidade de compartilhar qualquer relatório de tráfego com a Adobe.

Se você estiver interessado em testar esse novo recurso e compartilhar seus comentários, envie um email para `aemcs-rum-adopter@adobe.com`, juntamente com o nome de domínio, para o ambiente de produção, preparo e desenvolvimento pelo seu endereço de email associado à sua Adobe ID. A equipe de produtos da Adobe habilitará o Serviço de dados de telemetria operacional para você.


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos na exibição do Assets {#assets-view-features}

**Criar imagens de IA generativa com o Adobe Firefly**

Crie novas imagens com base em consultas de pesquisas com uma integração do recurso de “texto para imagem” do Adobe Firefly (requer uma licença do Adobe Firefly).

![Integração do Firefly com o Assets](/help/assets/assets/assets-firefly-integration.png)

**Localizar imagens semelhantes**

Agora é possível encontrar conteúdo com facilidade selecionando uma imagem e visualizando imagens semelhantes no repositório do Experience Manager Assets.

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)


**Video Preview**: AEM Assets now generates preview renditions of all supported video formats by default, without the need to configure a processing profile.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos Recursos em [!DNL Experience Manager Forms] {#forms-features}

* **[Conecte um Forms adaptável com a Lista do Microsoft® SharePoint](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**: o AEM Forms fornece uma integração OOTB para enviar dados de formulários diretamente para a Lista do SharePoint, permitindo que você use os recursos de Listas do SharePoint. Você pode configurar a Lista de SharePoint do Microsoft como uma fonte de dados para um Modelo de dados de formulário e usar a ação de envio **Enviar usando o Modelo de dados de formulário** para conectar um Formulário adaptável à Lista de SharePoint.

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programa de adoção antecipada {#forms-early-adopter}

* **[Enviar um Formulário Adaptável para o Cenário do Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: o Forms as a Cloud Service oferece opções predefinidas para conectar facilmente um Formulário Adaptável ao Adobe Workfront. Isso simplifica o processo de envio de um Formulário adaptável para um cenário do Adobe Workfront, permitindo acionar um cenário do Workfront Fusion no envio de um Formulário adaptável.

* **[Suporte de idiomas da direita para a esquerda](/help/forms/supporting-new-language-localization-core-components.md)**: o Forms adaptável integrado aos Componentes principais agora pode ser apresentado em um idioma da direita para a esquerda (RTL), como árabe, persa e urdu. As línguas RTL são faladas por mais de 2 bilhões de pessoas em todo o mundo. Usar um formulário em linguagem RTL permite estender o alcance dos formulários adaptáveis para atender a esses públicos diferentes e selecionar mercados de RTL. Em algumas regiões, também é um mandato legal fornecer formulários no idioma local. Ao acomodar idiomas locais, você não só abre portas para um público mais amplo, como também garante a conformidade com as leis e regulamentos relevantes.

  ![Suporte de idioma da direita para a esquerda](/help/forms/assets/right-to-left-language-support.png)

* **[Proteja seus documentos com as APIs do DocAssurance (Parte das APIs de Comunicação)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: as APIs do DocAssurance permitem proteger informações confidenciais ao assinar e criptografar os documentos. Por meio da criptografia, o conteúdo de um documento é transformado em um formato ilegível, garantindo que somente usuários autorizados possam ter acesso. Essa camada fortificada de proteção não apenas protege dados valiosos de olhos não autorizados, mas também proporciona tranquilidade. As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos.

  Você pode escrever para `aem-forms-ea@adobe.com` a partir de sua ID de email oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Programa de Primeiros usuários do mapeamento de domínio {#cdn-config-early-adopter}

Além das [Regras de Filtro de Tráfego](/help/security/traffic-filter-rules-including-waf.md) recém-lançadas, que incluem as regras do Firewall de Aplicativo Web (WAF) opcionalmente licenciáveis, há uma oportunidade de usar o Pipeline de Configuração para declarar e implantar outros tipos de configuração CDN. Adoraríamos saber sobre seus casos de uso, incluindo:

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
