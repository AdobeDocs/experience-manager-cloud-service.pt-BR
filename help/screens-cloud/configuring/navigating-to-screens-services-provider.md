---
title: Navegar até o provedor de serviços do Screens
description: Esta página descreve como navegar até o Provedor de Serviços Screens.
exl-id: 9eff6fe8-41d4-4cf3-b412-847850c4e09c
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: ea374f6e521d3b94d1d38af5c8f6780275ae2cb4
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 4%

---

# Navegar até o provedor de serviços do Screens {#setup-screens-services-provider}

## Introdução {#introduction}

**O Screens Services Provider** permite que o autor de conteúdo, desenvolvedores e administradores gerenciem exibições e reprodutores para reprodução de conteúdo depois que o conteúdo é adicionado aos canais. Depois que os usuários recebem acesso ao AEM Cloud Service, eles devem poder fazer logon no Provedor de serviços da Screens.

Esta seção descreve como configurar o Provedor de Serviços Screens.


## Objetivo {#objective}

A seção a seguir mostra como configurar e configurar o Provedor de Serviços Screens.

## Etapas para configurar o Provedor de serviços Screens {#screens-services-provider}

Siga as etapas abaixo para configurar o Provedor de Serviços Screens:

1. Navegue até o Provedor de Serviços Screens [aqui](https://experience.adobe.com/screens).

   >[!CAUTION]
   >Se você tiver acesso a várias organizações, verifique se fez logon na Organização correta. Para alterar a organização, clique no nome da organização no canto superior direito da tela e escolha a organização correta que você precisa acessar.

1. Clique no ícone de engrenagem ao lado de Projeto (canto superior esquerdo)

   ![imagem](/help/screens-cloud/assets/configure/configure-screens0.png)

1. Insira os seguintes detalhes na caixa de diálogo Editar configurações.
   * **URL do Publish** - AEM publicar URL (por exemplo, `https://publish-p12345-e12345.adobeaemcloud.com`)
   * **URL do Autor** - URL do autor do AEM (por exemplo, `https://author-p12345-e12345.adobeaemcloud.com`)

   >[!NOTE]
   >Crie e publique pelo menos um Canal de tela AEM antes de configurar o AEM no Provedor de serviço Screens. Para criar um canal, navegue até /screens.html em seu provedor de conteúdo.

   ![imagem](/help/screens-cloud/assets/configure/configure-screens4.png)

1. Clique em **Salvar** para se conectar ao provedor de conteúdo do Screens.

1. Ao configurar a instância de publicação AEM para permitir o acesso somente a endereços IP confiáveis pelo recurso de Inclui na lista de permissões de IP do Cloud Manager, é necessário configurar um cabeçalho com um valor principal na caixa de diálogo de configurações, como mostrado abaixo.
Os IPs que precisam ser colocados na lista de permissões também precisam ser movidos para o arquivo de configuração e precisam ser [desaplicados](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list) das configurações do Cloud Manager.

   ![imagem](/help/screens-cloud/assets/configure/configure-screens20.png)
A mesma chave precisa ser configurada na configuração do CDN do AEM.  É recomendável não colocar o valor do cabeçalho diretamente no GITHub e usar uma [referência secreta](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-credentials-authentication#rotating-secrets).
Um exemplo de [configuração de CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf) é fornecido abaixo:
tipo: &quot;CDN&quot;
versão: &quot;1&quot;
metadados:
envTypes: [&quot;dev&quot;, &quot;estágio&quot;, &quot;prod&quot;]
dados:
trafficFilters:
regras:
- name: &quot;block-request-from-not-allowed-ips&quot;
quando:
allOf:
- reqProperty: clientIp
notIn: [&quot;101.41.112.0/24&quot;]
- reqProperty: tier
é igual a: publicar
action: block
- name: &quot;allow-requests-with-header&quot;
quando:
allOf:
- reqProperty: tier
é igual a: publicar
- reqProperty: path
é igual a: /screens/channels.json
- reqHeader: x-screens-tecla de inclui na lista de permissões
é igual a: ${\
   {CDN_HEADER_KEY}
ação:
type: allow

1. Selecione **Canais** na barra de navegação à esquerda e clique em **abrir no provedor de conteúdo**.

   ![imagem](/help/screens-cloud/assets/configure/configure-screens1.png)

1. O Provedor de conteúdo do Screens é aberto em outra guia que permite criar o conteúdo.

   ![imagem](/help/screens-cloud/assets/configure/configure-screens2.png)





## O que vem a seguir {#whats-next}

Depois de saber como configurar o Provedor de Serviços Screens, navegue até [Usando o Provedor de Conteúdo Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html#screens-content-provider) para obter mais detalhes.
