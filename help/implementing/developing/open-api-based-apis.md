---
title: APIs baseadas em OpenAPI
description: Saiba mais sobre o suporte do AEM as a Cloud Service para APIs baseadas em OpenAPI
feature: Developing
role: Admin, Architect, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: e735f7d2a39e3165907969d2e27565639499a636
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# APIs baseadas em OpenAPI {#openapi-based-apis}

>[!NOTE]
>
>As APIs abertas estão disponíveis como parte de um programa de acesso antecipado. Se você estiver interessado em acessá-las, recomendamos enviar um email para [aem-apis@adobe.com](mailto:aem-apis@adobe.com) com uma descrição do seu caso de uso.

As APIs mais recentes do AEM as a Cloud Service seguem a especificação da OpenAPI e, portanto, produzem APIs consistentes, bem documentadas e fáceis de usar. Informações detalhadas estão disponíveis nas seguintes páginas:

* Um [tutorial completo](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) sobre como configurar e chamar APIs do AEM baseadas em OpenAPI usando autenticação de servidor para servidor.
* [Guias](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/) informativos, incluindo [conceitos e sintaxe de API](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/).
* A [documentação de referência](https://developer.adobe.com/experience-cloud/experience-manager-apis/) do ponto de extremidade de API, na qual algumas APIs são baseadas em OpenAPI, como [esta API do Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/). A documentação de referência também inclui um playground de API, o que facilita a experimentação de um endpoint usando um token de portador gerado com o Adobe Developer Console.

Um caso de uso comum de API envolve integrações com sistemas, como um CRM ou PIM, em que as APIs do AEM são chamadas para recuperar ou persistir dados. Como parte da implementação da integração, os aplicativos podem assinar [eventos emitidos pela AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview), o que pode acionar a lógica de negócios no Adobe App Builder ou em outra infraestrutura.

Os tipos de autenticação de API compatíveis diferem com base no endpoint, mas podem ser OAuth de servidor para servidor, OAuth Web App e OAuth Single Page App (SPA).

>[!NOTE]
>
> O [tutorial completo](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) é um recurso recomendado para aprender a configurar e chamar as APIs do AEM baseadas em OpenAPI.


## Configuração do acesso à API {#configuring-api-access}

Muitas APIs do AEM baseadas em OpenAPI exigem autenticação, o que requer que as credenciais sejam geradas usando o [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/). A configuração envolve as seguintes etapas:

1. Verifique se os [perfis de produto do seu programa do AEM estão atualizados](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles) e se têm um serviço apropriado habilitado para acessar a API desejada.
1. Crie um novo projeto no Adobe Developer Console e adicione as APIs desejadas ao projeto, também selecionando o tipo de autenticação apropriado.
1. Gerar a credencial, que será usada posteriormente para trocar por um token de portador ao invocar a API.
1. Registre a ID do cliente no ambiente configurando um arquivo YAML, que é implantado usando o pipeline de configuração (ou linha de comando para RDEs).

Consulte o [Tutorial Configurar APIs baseadas em OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/setup) para obter instruções passo a passo.

## Registrar uma ID do cliente {#registering-a-client-id}

As IDs de clientes definem o escopo dos APs em um projeto do Adobe Developer Console para ambientes AEM específicos. Isso é feito da seguinte maneira:

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
