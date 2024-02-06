---
title: Dynatrace
description: Saiba como usar o Dynatrace com AEM as a Cloud Service
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
source-git-commit: fec3aa6debec49014406ab241c3ce0338ec5a1d2
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

O Adobe oferece a capacidade de usar o Dynatrace para monitorar o AEM as a Cloud Service como parte da implantação corporativa, identificar a causa de possíveis problemas e tomar medidas para corrigi-los conforme necessário.

Com o Dynatrace, você pode obter uma observabilidade perfeita para todas as suas aplicações de AEM. O Dynatrace oferece visibilidade abrangente sobre a experiência do usuário final, detectando automaticamente seus aplicativos AEM e visualizando suas dependências do site, do container ao Cloud Service. Interligados com rastreamentos completos em todas as camadas e o Monitoramento de usuários reais, leve suas experiências com AEM orientadas por conteúdo para o próximo nível sem lacunas ou pontos cegos. Se surgirem anomalias, o Dynatrace as diagnostica em tempo real, com o mecanismo IA Davis, e aponta a causa raiz para o código corrompido antes que seus clientes sejam afetados, minimizando o tempo médio de reparo.

Para saber mais sobre o Dynatrace, consulte o [integração com o Adobe AEM Cloud Service](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![Métricas de desempenho do autor e editor de AEM](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Integração do Dynatrace com o AEM as a Cloud Service {#integrating-dynatrace-with-aem-as-a-cloud-service}

Os clientes do Dynatrace podem monitorar seus ambientes AEM solicitando conectividade por meio de um tíquete de suporte ao cliente.

Os detalhes necessários para solicitações de conectividade são descritos abaixo:

| **Campo** | **Descrição** |
|---|---|
| [!DNL Dynatrace Environment URL] | O URL do ambiente do Dynatrace.<br><br>Para clientes SaaS do Dynatrace, o formato é `https://<your-environment-id>.live.dynatrace.com`.<br><br>Para clientes do Dynatrace Managed, o formato é `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | Sua ID de ambiente do Dynatrace. Consulte [Obter informações do ambiente do Dynatrace](#get-dynatrace-env-info) para saber como fazer isso. |
| [!DNL Dynatrace Environment Token] | Seu token de ambiente do Dynatrace. Consulte [Obter informações do ambiente do Dynatrace](#get-dynatrace-env-info) para saber como fazer isso.<br><br>Isso deve ser considerado um segredo, portanto, use as práticas de segurança apropriadas. Por exemplo, proteja-a com senha em um site como **zerobin.net**, que o tíquete de suporte ao cliente pode mencionar, junto com a senha. |
| [!DNL Dynatrace API access token] | O token de acesso à API do seu ambiente Dynatrace.  Consulte [Criar um token de acesso da API do Dynatrace](#create-dynatrace-access-token) para saber como criar isso.<br><br>Isso deve ser considerado um segredo, portanto, use as práticas de segurança apropriadas. Por exemplo, proteja-a com senha em um site como **zerobin.net**, que o tíquete de suporte ao cliente pode mencionar, junto com a senha.<br><br>Observação: isso só é necessário para o Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Port] | A porta AtiveGate do Dynatrace à qual a integração AEM deve se conectar.<br><br>Observação: isso só é necessário para o Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Network Zone] | Seu [Zona de rede do Dynatrace AtiveGate](https://docs.dynatrace.com/docs/manage/network-zones) rotear dados de monitoramento de AEM com eficiência em data centers e regiões de rede.<br><br>Observação: uma zona de rede Dynatrace AtiveGate é opcional. |
| [!DNL AEM Environment ID(s)] | As IDs de ambiente do AEM que o Dynatrace deve monitorar. |

>[!NOTE]
>
>Depois que o Dynatrace for integrado, os dados não fluirão mais para outras ferramentas de APM, como o New Relic, se tiverem sido habilitados anteriormente.


## Criar um token de acesso da API do Dynatrace {#create-dynatrace-access-token}

1. Faça logon no ambiente do Dynatrace.
1. No [!DNL Dynatrace] , acesse [!DNL Manage] > [!DNL Access tokens].
1. Selecionar [!DNL Generate new token].
1. Definir um [!DNL token name].

1. Opcional: Defina um [!DNL expiration date]. Gere um novo token antes que ele expire.
1. Defina o [!DNL token scope] para [!DNL PaaS integration - Installer download]
1. Selecionar [!DNL Generate token].
1. Copie o token de acesso gerado e armazene-o em um local seguro.


## Obter informações do ambiente do Dynatrace {#get-dynatrace-env-info}

1. Execute a seguinte solicitação de API no ambiente do Dynatrace:

`curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"`

Substituir \&lt;environmenturl> com o URL do ambiente Dynatrace e \&lt;accesstoken> com o token de acesso da API criado.

1. Copie os \&lt;environmentid> e \&lt;environmenttoken> da carga de resposta e armazene-as em um local seguro.

```
{
   "tenantUUID": "<environmentId>",
   "tenantToken": "<environmentToken>",
   "communicationEndpoints": [
   ... 
   ],
   "formattedCommunicationEndpoints": "<endpoints>" 
}
```


