---
title: Dynatrace
description: Saiba como usar o Dynatrace com o AEM as a Cloud Service
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

O Adobe permite usar o Dynatrace para monitorar o AEM as a Cloud Service como parte da implantação corporativa, identificar a causa de possíveis problemas e tomar medidas para corrigi-los, conforme necessário.

Com o Dynatrace, você pode obter uma capacidade de observação perfeita para todos os seus aplicativos AEM. A Dynatrace descobre seus aplicativos AEM e mostra os caminhos deles, desde o site até o contêiner do Cloud Service, para revelar a experiência do usuário. Interligados com rastreamentos completos em todos os níveis e o Monitoramento de uso real, elevam suas experiências orientadas por conteúdo do AEM a um novo patamar sem lacunas ou pontos cegos. Se surgirem anomalias, a Dynatrace as diagnostica em tempo real, com o mecanismo de IA Davis. Ele aponta a causa básica para o código corrompido antes que seus clientes sejam afetados, minimizando o tempo médio de reparo.

Para saber mais sobre o Dynatrace, consulte a [integração do Adobe AEM Cloud Service](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![Métricas de desempenho do autor e editor do AEM](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Integração do Dynatrace com o AEM as a Cloud Service {#integrating-dynatrace-with-aem-as-a-cloud-service}

Os clientes da Dynatrace podem monitorar seus ambientes AEM solicitando conectividade por meio de um tíquete de suporte ao cliente.

Os detalhes necessários para solicitações de conectividade são descritos abaixo:

| **Campo** | **Descrição** |
|---|---|
| [!DNL Dynatrace Environment URL] | O URL do ambiente do Dynatrace.<br><br>Para clientes SaaS da Dynatrace, o formato é `https://<your-environment-id>.live.dynatrace.com`.<br><br>Para clientes do Dynatrace Managed, o formato é `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | Sua ID de ambiente do Dynatrace. Consulte [Como obter meus Detalhes de Conexão do Dynatrace?](#how-do-i-get-my-dynatrace-connection-details) para saber como obtê-lo. |
| [!DNL Dynatrace Environment Token] | O token de ambiente do Dynatrace. Consulte [Como obter meus Detalhes de Conexão do Dynatrace?](#how-do-i-get-my-dynatrace-connection-details) para saber como obtê-lo.<br><br>Este token deve ser considerado um segredo, portanto, use as práticas de segurança apropriadas. Por exemplo, proteja-a com senha em um site como **zerobin.net**, ao qual o tíquete de suporte ao cliente pode fazer referência, juntamente com a senha. |
| [!DNL Dynatrace API access token] | O token de acesso à API do seu ambiente Dynatrace. Consulte [Criar um token de acesso da API do Dynatrace](#create-dynatrace-access-token) para saber como criá-lo.<br><br>Este token deve ser considerado um segredo, portanto, use as práticas de segurança apropriadas. Por exemplo, proteja-a com senha em um site como **zerobin.net**, ao qual o tíquete de suporte ao cliente pode fazer referência, juntamente com a senha.<br> |
| [!DNL Dynatrace ActiveGate Port] | A porta do Dynatrace AtiveGate à qual a integração do AEM deve se conectar.<br><br>Esta porta só é necessária para o Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Network Zone] | Sua [zona de rede do Dynatrace AtiveGate](https://docs.dynatrace.com/docs/manage/network-zones) para rotear dados de monitoramento do AEM de forma eficiente entre centros de dados e regiões de rede.<br><br>Observação: uma zona de rede Dynatrace AtiveGate é opcional. |
| [!DNL AEM Environment IDs] | A ID ou as IDs de ambiente do AEM que o Dynatrace deve monitorar. |

>[!NOTE]
>
>Depois que o Dynatrace é integrado, os dados não fluem mais para outras ferramentas de APM, como o New Relic, se tiverem sido habilitados anteriormente.

## Perguntas frequentes {#faq}

### Qual licença é necessária para o Dynatrace AEM Monitoring? {#which-license-do-i-need-for-AEM-monitoring}

O monitoramento do Dynatrace AEM exige uma licença da Dynatrace. O licenciamento do Dynatrace AEM é baseado no [monitoramento de pilha completa para contêineres Kubernetes](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring). Os tamanhos de memória dos contêineres monitorados do AEM (serviços de autoria e edição) são detectados automaticamente.

As especificações de implantação do Adobe por ambiente AEM são:

* Produção: em média, 4 contêineres, 16 GB de memória cada
* Não produção: em média, 4 contêineres, 8 GB de memória cada

Para saber mais sobre o licenciamento da Dynatrace, consulte a [Assinatura da Plataforma Dynatrace](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription).

### Como obter meus detalhes de conexão do Dynatrace? {#how-do-i-get-my-dynatrace-connection-details}

1. Execute a seguinte solicitação de API no seu ambiente do Dynatrace:

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   Substitua `<environmentUrl>` pela URL do ambiente do Dynatrace e `<accessToken>` pelo token de acesso da API criado.

1. Copie `<environmentId>` e `<environmentToken>` da carga de resposta e armazene-os em um local seguro.

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### Criar um token de acesso da API do Dynatrace {#create-dynatrace-access-token}

1. Faça logon no ambiente do Dynatrace.
1. Vá para **[!DNL Access tokens]** e clique na opção **[!DNL Generate new token]**.
1. Defina um [!DNL token name].
1. Defina o escopo do token como **[!DNL PaaS integration - Installer download]**.
1. Selecione **[!DNL Generate token]**.
1. Copie o token de acesso gerado e armazene-o em um local seguro.





