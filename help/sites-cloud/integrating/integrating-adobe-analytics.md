---
title: Integração ao Adobe Analytics
description: 'Integração ao Adobe Analytics '
feature: Administering
role: Admin
exl-id: e353a1fa-3e99-4d79-a0d1-40851bc55506
source-git-commit: e950f2399553c301c97c4fcac549a7ef6a234164
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 3%

---

# Integração ao Adobe Analytics{#integrating-with-adobe-analytics}

Integrar o Adobe Analytics e AEM as a Cloud Service permite rastrear a atividade da página da Web. A integração exige:

* usando a interface do usuário de toque para criar uma configuração do Analytics em AEM as a Cloud Service. Observe que a autenticação IMS é necessária para integrar o Adobe Analytics com AEM as a Cloud Service.
* adicionar e configurar o Adobe Analytics como uma extensão em [Adobe Launch](#analytics-launch). Para obter mais detalhes sobre o Adobe Launch, consulte [esta página](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html).

Comparado às versões anteriores do AEM, o suporte à estrutura não é fornecido na Configuração do Analytics em AEM as a Cloud Service. Em vez disso, agora é feito por meio do Adobe Launch, que é a ferramenta de fato para instrumentar um site AEM com recursos do Analytics (bibliotecas JS). No Adobe Launch, uma propriedade é criada, onde a extensão Adobe Analytics pode ser configurada e as regras são criadas para enviar dados ao Adobe Analytics. O Adobe Launch substituiu a tarefa de análise fornecida pelo sitecatalyst.

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

Os campos presentes na janela de configuração são os seguintes:

![Parâmetros de configuração](assets/properties_field2.png "Parâmetros de configuração")

| Propriedade | Descrição |
|---|---|
| Título | O nome da configuração |
| Configuração IMS | Selecione a configuração IMS (consulte o capítulo abaixo) |
| Segmento | Opção para usar um segmento do Analytics definido no conjunto de relatórios atual. Os relatórios do Analytics serão filtrados com base no segmento. Consulte [esta página](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html) para obter mais detalhes. |
| Report Suites | Um repositório no qual você envia dados e obtém relatórios. Um conjunto de relatórios define o relatório completo e independente de um site específico ou subconjuntos de páginas do site. Você pode exibir os relatórios obtidos de um único conjunto de relatórios e editar esse campo em uma configuração a qualquer momento, de acordo com suas necessidades. |

### Adobe Analytics com autenticação IMS {#configuration-parameters-ims}

Uma configuração IMS é necessária para integrar corretamente o Adobe Analytics com AEM as a Cloud Service. Essa configuração deve ser criada, portanto, consulte esta seção [página](/help/sites-cloud/integrating/integration-adobe-analytics-ims.md) para saber como criar a configuração IMS do Analytics.

### Adicionar uma configuração a um site {#add-configuration}

Para aplicar uma configuração da interface de toque a um site, acesse: **Sites** → **Selecionar qualquer página do site** → **Propriedades** → **Avançado** → **Configuração** → selecione o locatário de configuração.

## Integração do Adobe Analytics em sites AEM usando o Adobe Launch {#analytics-launch}

O Adobe Analytics pode ser adicionado como uma extensão na propriedade do Launch. As regras podem ser definidas para executar o mapeamento e fazer uma chamada de postagem para o Adobe Analytics:

* Observar [este vídeo](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html) para saber como configurar a extensão do Analytics no Launch para um site básico.

* Consulte [esta página](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html) para obter detalhes sobre como criar regras e enviar dados para o Adobe Analytics.

>[!NOTE]
>
>A configuração IMS (contas técnicas) do Launch é pré-configurada AEM as a Cloud Service. Não é necessário criar essa configuração.

>[!NOTE]
>
>As estruturas existentes (herdadas) ainda funcionam, mas não podem ser configuradas na interface do usuário de toque. É aconselhável recriar as configurações de mapeamento de variável no Launch.
