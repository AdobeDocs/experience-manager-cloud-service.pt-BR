---
title: Integração ao Adobe Analytics
description: 'Integração ao Adobe Analytics '
feature: Administering
role: Admin
exl-id: e353a1fa-3e99-4d79-a0d1-40851bc55506
source-git-commit: acd44bd7ff211466acc425148cab18dc7ae6d44c
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 3%

---

# Integração ao Adobe Analytics{#integrating-with-adobe-analytics}

Integrar o Adobe Analytics e AEM as a Cloud Service permite rastrear a atividade da página da Web. A integração exige:

* usando a interface do usuário de toque para criar uma configuração do Analytics em AEM as a Cloud Service.
* adicionar e configurar o Adobe Analytics como uma extensão em [Adobe Launch](#analytics-launch). Para obter mais detalhes sobre o Adobe Launch, consulte [esta página](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html).

Comparado às versões anteriores do AEM, o suporte à estrutura não é fornecido na Configuração do Analytics em AEM as a Cloud Service. Em vez disso, agora é feito por meio do Adobe Launch, que é a ferramenta de fato para instrumentar um site AEM com recursos do Analytics (bibliotecas JS). No Adobe Launch, uma propriedade é criada, onde a extensão Adobe Analytics pode ser configurada e as regras são criadas para enviar dados ao Adobe Analytics. O Adobe Launch substituiu a tarefa de análise fornecida pelo sitecatalyst.

>[!NOTE]
>Adicionado no canal de pré-lançamento é o requisito para a autenticação IMS a fim de integrar o Adobe Analytics com AEM as a Cloud Service. Consulte a [Configuração do Adobe Analytics com autenticação IMS (canal de pré-lançamento)](#configuration-parameters-ims) para obter mais detalhes. Veja o canal de pré-lançamento [documentação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) para obter informações sobre como ativar essa configuração para seu ambiente.

>[!NOTE]
>
>Os clientes da Adobe Experience Manager as a Cloud Service que não têm uma conta existente do Analytics podem solicitar acesso ao Analytics Foundation Pack para Experience Cloud. Este Foundation Pack fornece uso limitado por volume do Analytics.

## Criação da configuração do Adobe Analytics {#analytics-configuration}

1. Navegar para **Ferramentas** → **Cloud Services**.
2. Selecionar **Adobe Analytics**.
   ![Janela Adobe Analytics](assets/analytics_screen2.png "Janela Adobe Analytics")
3. Selecione o **Criar** botão.
4. Preencha os detalhes (veja abaixo) e clique em **Connect**.

### Parâmetros de configuração {#configuration-parameters}

Os campos de configuração presentes na janela Configuração do Adobe Analytics são:

![Parâmetros de configuração](assets/properties_field1.png "Parâmetros de configuração")

| Propriedade | Descrição |
|---|---|
| Empresa | Empresa de logon do Adobe Analytics |
| Nome de usuário | Usuário da API do Adobe Analytics |
| Senha | Senha Adobe Analytics usada para autenticação |
| Centro de dados | O data center da Adobe Analytics com o qual sua conta está associada (servidor por exemplo, San Jose, Londres) |
| Segmento | Opção para usar um segmento do Analytics definido no conjunto de relatórios atual. Os relatórios do Analytics serão filtrados com base no segmento. Consulte [esta página](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html) para obter mais detalhes. |
| Report Suites | Um repositório no qual você envia dados e obtém relatórios. Um conjunto de relatórios define o relatório completo e independente de um site específico ou subconjuntos de páginas do site. Você pode exibir os relatórios obtidos de um único conjunto de relatórios e editar esse campo em uma configuração a qualquer momento, de acordo com suas necessidades. |

### Configuração do Adobe Analytics com autenticação IMS (canal de pré-lançamento) {#configuration-parameters-ims}

Adicionado no canal de pré-lançamento é o requisito para a autenticação IMS a fim de integrar o Adobe Analytics com AEM as a Cloud Service. Veja o canal de pré-lançamento [documentação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) para obter informações sobre como ativar essa configuração para seu ambiente. Isso significa que uma configuração de IMS para o Launch e o Analytics é necessária para integrar adequadamente o Analytics ao AEM e ao Launch. Embora a configuração IMS do Launch seja pré-configurada AEM as a Cloud Service, a configuração IMS do Analytics deve ser criada.

Consulte esta [página](/help/sites-cloud/integrating/integration-adobe-analytics-ims.md) para saber como criar a configuração IMS do Analytics.

Depois de executar as etapas na [Criação da configuração do Adobe Analytics](#configuration-parameters) seção os campos presentes na janela de configuração são os seguintes:

![Parâmetros de configuração](assets/properties_field2.png "Parâmetros de configuração")

| Propriedade | Descrição |
|---|---|
| Título | O nome da configuração |
| Configuração IMS | Selecione a configuração IMS (consulte a descrição acima) |
| Segmento | Opção para usar um segmento do Analytics definido no conjunto de relatórios atual. Os relatórios do Analytics serão filtrados com base no segmento. Consulte [esta página](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html) para obter mais detalhes. |
| Conjuntos de relatórios | Um repositório no qual você envia dados e obtém relatórios. Um conjunto de relatórios define o relatório completo e independente de um site específico ou subconjuntos de páginas do site. Você pode exibir os relatórios obtidos de um único conjunto de relatórios e editar esse campo em uma configuração a qualquer momento, de acordo com suas necessidades. |

### Adicionar uma configuração a um site {#add-configuration}

Para aplicar uma configuração da interface de toque a um site, acesse: **Sites** → **Selecionar qualquer página do site** → **Propriedades** → **Avançado** → **Configuração** → selecione o locatário de configuração.

## Integração do Adobe Analytics em sites AEM usando o Adobe Launch {#analytics-launch}

O Adobe Analytics pode ser adicionado como uma extensão na propriedade do Launch. As regras podem ser definidas para executar o mapeamento e fazer uma chamada de postagem para o Adobe Analytics:

* Observar [este vídeo](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html) para saber como configurar a extensão do Analytics no Launch para um site básico.

* Consulte [esta página](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html) para obter detalhes sobre como criar regras e enviar dados para o Adobe Analytics.

>[!NOTE]
>
>As estruturas existentes (herdadas) ainda funcionam, mas não podem ser configuradas na interface do usuário de toque. É aconselhável recriar as configurações de mapeamento de variável no Launch.

>[!NOTE]
>
>A configuração IMS (contas técnicas) do Launch é pré-configurada AEM as a Cloud Service. Os usuários não precisam criar essa configuração.
