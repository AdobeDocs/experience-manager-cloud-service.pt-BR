---
title: APIs baseadas em OpenAPI
description: Saiba mais sobre o suporte do AEM as a Cloud Service para APIs baseadas em OpenAPI
feature: Developing
role: Admin, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# APIs baseadas em OpenAPI {#openapi-based-apis}

As APIs mais recentes do AEM as a Cloud Service seguem a especificação da OpenAPI e, portanto, oferecem um conjunto consistente e bem documentado de APIs.

>[!NOTE]
>
> Um [tutorial completo](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) é um recurso recomendado para aprender a configurar e chamar as APIs do AEM baseadas em OpenAPI.

Para endpoints que exigem autenticação, a abordagem de autenticação é diferente com base no endpoint, mas pode usar OAuth de servidor para servidor, OAuth Web App ou OAuth Single Page App (SPA). As credenciais são configuradas por meio de projetos em [Adobe Developer Console](https://developer.adobe.com/developer-console/).

Casos de uso comuns de API envolvem integrações com sistemas, como um CRM ou PIM, em que as APIs do AEM são chamadas para recuperar ou persistir dados. Como parte da implementação da integração, os aplicativos podem assinar [eventos emitidos pela AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview), o que pode acionar a lógica de negócios no Adobe App Builder ou em outra infraestrutura.

Este documento serve como uma visão geral, mas uma documentação mais detalhada está disponível nas seguintes páginas:

* Os links da seção API baseada em OpenAPI da [documentação de referência](https://developer.adobe.com/experience-cloud/experience-manager-apis/). Cada documentação de referência da API também inclui um playground de API, o que facilita a tentativa de um endpoint usando um token de portador gerado com o Adobe Developer Console.

* [Guias](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/) informativos, incluindo [conceitos e sintaxe de API](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/).

* Um tutorial de nível superior descrevendo [abordagens de autenticação](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/overview#authentication-support) e outros conceitos.

* Um tutorial em vídeo focado em [como configurar as APIs baseadas em OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup).

* [Tutorial completo](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) sobre a configuração e a chamada de OpenAPIs com a estratégia de autenticação de servidor para servidor. Tutoriais semelhantes também podem ser encontrados para as abordagens de autenticação de Aplicativo de página única e Aplicativo da Web.

## Configuração do acesso à API {#configuring-api-access}

Algumas APIs do AEM baseadas em OpenAPI precisam de autenticação, o que requer que as credenciais sejam geradas usando o [Adobe Developer Console](https://developer.adobe.com/developer-console/). A configuração envolve as seguintes etapas:

1. Modernização do ambiente do AEM as a Cloud Service. Para obter mais informações, consulte a etapa do tutorial [Modernização do ambiente do AEM as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup?#modernization-of-aem-as-a-cloud-service-environment).
1. Ative o acesso às APIs do AEM usando Perfis de produto. Os Perfis de produto são associados aos Serviços que representam grupos de usuários do AEM com ACLs (Listas de controle de acesso) predefinidas. Embora alguns serviços estejam associados a perfis de produtos específicos por padrão, outros precisam ser explicitamente associados; por exemplo, o Serviço de Usuários da API do AEM Assets não está associado a nenhum [Perfil de Produto](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles), portanto, você deve habilitá-lo para usar a API do AEM Assets. Para obter mais informações, consulte a etapa do tutorial [Habilitar acesso às APIs do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access).
1. Para adicionar a autenticação de servidor para servidor, o usuário que configura a integração deve ser o administrador de sistema da organização no Adobe Admin Console ou adicionado como desenvolvedor ao Perfil do produto em que o Serviço está associado. Para obter mais informações, consulte a etapa do tutorial [Habilitar acesso às APIs do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access).
1. Crie um projeto do Adobe Developer Console (ADC).
1. Configure o projeto ADC. Isso gera credenciais que serão usadas posteriormente para trocar por um token de portador ao invocar a API.
1. Configure a instância do AEM para habilitar a comunicação do Projeto ADC. Isso envolve o registro da ID do cliente com o ambiente configurando e implantando um arquivo YAML, conforme descrito na seção [Registrando uma ID do cliente](#registering-a-client-id) abaixo.

Para obter instruções detalhadas, consulte o [Tutorial Configurar APIs baseadas em OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup).

### Registrar uma ID do cliente {#registering-a-client-id}

As IDs de clientes definem o escopo das APIs em um projeto do Adobe Developer Console para ambientes AEM específicos. Isso é feito da seguinte maneira:

1. Crie um arquivo chamado `api.yaml` ou similar com uma configuração como a do trecho abaixo, incluindo os níveis desejados (autor, publicação, visualização). `Client_id` valores devem vir do(s) projeto(s) de API do Adobe Developer Console.

   As propriedades `kind`, `version` e `metadata` estão descritas no artigo [Pipeline de Configuração](/help/operations/config-pipeline.md#common-syntax). O valor da propriedade `kind` deve ser definido como *API* e a propriedade `version` deve ser definida como *1*.

   ```
   kind: "API"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     allowedClientIDs:
       author:
         - "<client_id>"
       publish:
         - "<client_id>"
       preview:
         - "<client_id>"
   ```

1. Coloque o arquivo em algum lugar em uma pasta de nível superior chamada `config` ou similar, conforme descrito em [Pipeline de configuração](/help/operations/config-pipeline.md#folder-structure).
1. Para tipos de ambiente diferentes de RDE (que usa ferramentas de linha de comando), crie um pipeline de configuração de implantação direcionada no Cloud Manager, conforme referenciado por [esta seção](/help/operations/config-pipeline.md#creating-and-managing) no artigo Pipeline de configuração. Observe que os pipelines de Empilhamento completo e de Camada da Web não implantam o arquivo de configuração.
1. Implante a configuração.
