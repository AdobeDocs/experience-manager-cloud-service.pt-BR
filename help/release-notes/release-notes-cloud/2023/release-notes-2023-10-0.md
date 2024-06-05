---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.10.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2023.10.0.
exl-id: 81a6cbd2-7101-429b-8572-2650c5bea963
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 25%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2023.10.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2023.10.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2021 ou 2022.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Atualizações recentes na documentação](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=pt-BR) para obter detalhes de atualizações de documentação não relacionadas diretamente a uma versão.

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2023.10.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 26 de outubro de 2023. O próximo lançamento de recursos (2023.11.0) está planejado para sexta-feira, 30 de novembro de 2023.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo de Visão geral da versão de outubro de 2023 que exibe um resumo dos recursos adicionados na versão 2023.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425186/?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novos recursos {#assets-features}

**Complemento AEM Assets para Adobe Express**: o Experience Manager Assets agora fornece um complemento para o Adobe Express. O complemento permite acessar diretamente os ativos armazenados no Experience Manager Assets por meio da interface do usuário do Adobe Express. Você pode colocar o conteúdo gerenciado no AEM Assets na tela Express e depois salvar o conteúdo novo ou editado em um repositório do AEM Assets. O complemento oferece os seguintes benefícios principais:

* Maior reutilização de conteúdo ao editar e salvar novos ativos no AEM

* Redução do tempo e esforço gerais para criar novos ativos ou novas versões de ativos existentes

  ![Incluir ativos do complemento Assets](/help/assets/assets/aem-assets-add-on-include-assets.png)

### Novos recursos na visualização de ativos {#assets-view-features}

* **Importar ativos em massa da fonte de dados do OneDrive**: os administradores agora têm a capacidade de [importar um grande número de ativos do OneDrive para o AEM Assets](/help/assets/bulk-import-assets-view.md#onedrive-developer-application). A lista atualizada das fontes de dados com suporte para importação em massa inclui Azure, AWS, Google Cloud, Dropbox e OneDrive.

  ![Atribuir formulário de metadados a uma pasta](/help/assets/assets/bulk-import-source-details-onedrive.png)

* **Suporte a direitos entre organizações para bibliotecas**: o Experience Manager Assets agora permite configurar o acesso às bibliotecas de Creative Cloud em uma Organização IMS diferente. Isso facilita o acesso aos fluxos de trabalho de produtos mais recentes entre a Creative Cloud e o Experience Manager e reduz o tempo e esforço de criação.

### Recursos de pré-lançamento disponíveis em [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Suporte a várias legendas e trilhas de áudio para vídeos no Dynamic Media](/help/assets/dynamic-media/video.md#about-msma)—Agora é possível adicionar facilmente várias legendas e faixas de áudio a um vídeo principal. Esse recurso significa que os vídeos estão acessíveis em um público-alvo global. Você pode personalizar um único vídeo principal publicado para um público-alvo global em vários idiomas e seguir as diretrizes de acessibilidade para diferentes regiões geográficas. Os autores também podem gerenciar as legendas e faixas de áudio em uma única guia na interface do usuário do.

  ![Guia Legendas e faixas de áudio na página Propriedades de um ativo de vídeo selecionado.](/help/release-notes/assets/msma-aem-cs.png)*Guia Legendas e faixas de áudio na página Propriedades de um ativo de vídeo selecionado.*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novos recursos no [!DNL Experience Manager Forms] {#forms-features}

* **[Propriedades personalizadas para o Adaptive Forms](/help/forms/template-editor-core-components.md#add-a-custom-group-name-in-the-policy-of-template-editor)**: você pode associar atributos personalizados (pares de valores chave) a um modelo de formulário ou componente de formulários adaptáveis para permitir que os desenvolvedores de formulários forneçam comportamentos de formulário dinâmicos que se adaptam com base nos valores desses atributos personalizados. Por exemplo, os desenvolvedores podem criar diferentes representações de um componente headless do Forms em plataformas móveis, de desktop ou da Web, com base nos valores de atributos personalizados, melhorando significativamente a experiência do usuário em uma grande variedade de dispositivos.

* **Temas e modelos**: Inicie seu processo de criação de formulários com nossos novos temas e modelos, personalizados para capacitar profissionais experientes e novos autores de formulários. Construídos de maneira contínua usando os Componentes principais do Adaptive Forms, esses temas e modelos meticulosamente preparados permitem que você comece a criar formulários rapidamente para casos de uso comuns.

  ![Modelos prontos para uso](/help/forms/assets/form-templates-ootb.png)


### Programa de adoção antecipada {#forms-early-adopter}

* **[Protect seus documentos com as APIs DocAssurance (Parte das APIs de comunicação)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: As APIs do DocAssurance permitem proteger informações confidenciais, assinando e criptografando os documentos. Por meio da criptografia, o conteúdo de um documento é transformado em um formato ilegível, garantindo que somente usuários autorizados possam ter acesso. Essa camada fortificada de proteção não apenas protege dados valiosos de olhos não autorizados, mas também proporciona tranquilidade. As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos.

  Você pode escrever para `aem-forms-ea@adobe.com` do seu id de email oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Regras de filtro de tráfego, incluindo WAF {#traffic-filter-rules-waf}

[Filtrar o tráfego na CDN gerenciada por Adobe](/help/security/traffic-filter-rules-including-waf.md) declarando regras que correspondem ao tráfego do site por propriedades, incluindo url, endereço IP e agente do usuário — ou definindo limites de taxa de tráfego personalizados para proteger contra ataques de DoS. Os clientes também podem licenciar um conjunto de regras avançadas do Web Application Firewall (WAF) para obter proteção extra contra ameaças sofisticadas de sites.

Recomendamos que você se familiarize com as regras de filtro de tráfego ao [experimentar um tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html)! Ele orienta você na configuração de um novo Pipeline de configuração do Cloud Manager, na declaração de regras em um arquivo de configuração e na análise de logs de CDN para tráfego mal-intencionado.

As regras de filtro de tráfego estão disponíveis agora em ambientes de desenvolvimento, com uma implantação gradual para ambientes de preparo e produção em novembro. Você pode solicitar acesso antecipado no palco e no prod enviando um email **aemcs-waf-adopter@adobe.com**.

As regras avançadas de filtro de tráfego do WAF podem ser licenciadas ainda este ano por meio da Segurança aprimorada ou das ofertas de Proteção WAF-DDoS.

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
