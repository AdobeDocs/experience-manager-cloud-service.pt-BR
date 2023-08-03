---
title: Ferramenta de conversão do Dispatcher do AEM
description: Saiba como converter configurações existentes no AEM Dispatcher em configurações no AEM as a Cloud Service Dispatcher.
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: f7ffe727ecc7f1331c1c72229a5d7f940070c011
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 33%

---

# Conversor do Dispatcher do AEM {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="Conversor do Dispatcher do AEM"
>abstract="O Conversor do Adobe Experience Manager Dispatcher converte as configurações existentes do AEM Dispatcher para configurações do AEM as a Cloud Service Dispatcher."

O Conversor do Adobe Experience Manager Dispatcher converte as configurações existentes do AEM Dispatcher para configurações do AEM as a Cloud Service Dispatcher.

## Introdução ao Dispatcher {#introduction-dispatcher}

O Dispatcher é a ferramenta de armazenamento em cache, balanceamento de carga ou ambos do Adobe Experience Manager. Usar o Dispatcher do AEM também ajuda a proteger seu servidor AEM contra ataques. Portanto, você pode aumentar a segurança da instância do AEM usando o Dispatcher com um servidor Web de classe empresarial.

>[!NOTE]
>O uso mais comum do Dispatcher é armazenar em cache as respostas de uma **instância de publicação do AEM**, para aumentar a capacidade de resposta e a segurança de seu site publicado voltado para o exterior.

Consulte [Visão geral do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) para saber como o Dispatcher executa o cache, retorna documentos e realiza o Balanceamento de carga.

### Testes e configuração do Apache e Dispatcher {#dispatcher-configurations-cloud}

Saiba como estruturar as configurações do AEM as a Cloud Service Apache e Dispatcher e como validá-las e executá-las localmente antes de implantá-las em ambientes de nuvem.

Consulte [Dispatcher na nuvem](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html) para obter mais informações.

## Conversor do Dispatcher do AEM {#aem-dispatcher-converter}

O Conversor do Dispatcher do AEM fornece a capacidade de refatorar configurações existentes no local ou no Managed Services Dispatcher para configurações do Dispatcher compatíveis com AEM as a Cloud Service.

## Uso do Conversor do Dispatcher do AEM {#using-dispatcher-converter}

* Por meio da CLI do Adobe Developer : a Adobe recomenda usar o Conversor do Dispatcher do AEM por meio de `aio-cli-plugin-aem-cloud-service-migration` (Plug-in de refatoração de código as a Cloud Service AEM para a CLI da Adobe Developer).

  Consulte **[Recurso do Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para que você possa aprender a instalar e usar o plug-in.

* Como um utilitário independente : a ferramenta Conversor do Dispatcher do AEM também pode ser executada como um utilitário independente.

  Consulte **[Recurso do Git: Conversor do Dispatcher do AEM Cloud Service](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** para que você possa saber mais sobre o uso e a solução de problemas dessa ferramenta.

>[!IMPORTANT]
>O Conversor do Dispatcher do AEM é desenvolvido usando o NodeJS. O Adobe recomenda que você tenha o NodeJS 10.0+ instalado.
