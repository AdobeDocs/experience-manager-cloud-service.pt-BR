---
title: AEM Forms as a Cloud Service - Comunicações
description: Mesclar dados automaticamente com modelos XDP e PDF ou gerar saída nos formatos PCL, ZPL e PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 20e54ff697c0dc7ab9faa504d9f9e0e6ee585464
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 1%

---


# Usar processamento síncrono {#sync-processing-introduction}

as a Cloud Service do Forms - As APIs de comunicação permitem criar, montar e fornecer comunicações personalizadas e orientadas por marca, como correspondências comerciais, documentos, declarações, cartas de processamento de solicitações, avisos de benefícios, cartas de processamento de solicitações, contas mensais e kits de boas-vindas. Você pode usar as APIs de comunicações para combinar um modelo (XFA ou PDF) com os dados do cliente para gerar documentos nos formatos PDF, PS, PCL, DPL, IPL e ZPL.

Considere um cenário em que você tem um ou mais modelos e vários registros de dados XML para cada modelo. Você pode usar as APIs de comunicações para gerar um documento de impressão para cada registro. <!-- You can also combine the records into a single document. --> O resultado é um documento PDF não interativo. Um documento PDF não interativo não permite que os usuários insiram dados em seus campos.

Forms as a Cloud Service - As comunicações fornecem APIs por demanda e em lote (APIs assíncronas) para a geração de documentos agendados:

* As APIs síncronas são adequadas para casos de uso sob demanda, baixa latência e geração de documento de registro único. Essas APIs são mais adequadas para casos de uso baseados em ações do usuário. Por exemplo, gerar um documento depois que um usuário preencher um formulário.

* As APIs em lote (APIs assíncronas) são adequadas para casos de uso de geração de documento com várias throughput programada. Essas APIs geram documentos em lotes. Por exemplo, contas telefônicas, demonstrativos de cartão de crédito e demonstrativos de benefícios gerados todo mês.

## Usar operações síncronas {#batch-operations}

Uma operação síncrona é um processo de geração de documentos de maneira linear. Essas APIs são classificadas como APIs de um único locatário e APIs de vários locatários:

### APIs de um único locatário

* APIs de geração de documentos
* APIs de manipulação de documentos

### APIs de vários locatários

* APIs do utilitário de documento

### Autenticar uma API de locatário único

As operações de API de um único locatário suportam dois tipos de autenticação:

* **Autenticação básica**: Autenticação básica é um esquema de autenticação simples integrado ao protocolo HTTP. O cliente envia solicitações HTTP com o cabeçalho de Autorização que contém a palavra Básico seguida de um espaço e uma sequência de caracteres codificada em base64, username:password. Por exemplo, para autorizar como administrador / administrador o cliente envia Básico [nome de usuário da string codificada em base64]: [senha de string codificada em base64].

* **Autenticação por token:** A autenticação baseada em token usa um token de acesso (token de autenticação portador) para fazer solicitações ao Experience Manager as a Cloud Service. O AEM Forms as a Cloud Service fornece APIs para recuperar com segurança o token de acesso. Para recuperar e usar o token para autenticar uma solicitação:

   1. [Recupere as credenciais do Experience Manager as a Cloud Service no Console do desenvolvedor](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [Instale as credenciais do Experience Manager as a Cloud Service em seu ambiente](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (Servidor de Aplicativos, Servidor da Web ou outros servidores não AEM) configurados para enviar solicitações para (fazer chamadas) o serviço em nuvem.
   1. [Gere um token JWT e trocou-o com as APIs do Adobe IMS para um token de acesso](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. Execute a API do Experience Manager com o token de acesso como um token de autenticação do portador.
   1. [Defina as permissões apropriadas para o usuário da conta técnica no ambiente Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >O Adobe recomenda usar a autenticação baseada em token em um ambiente de produção.

### Autenticar uma API de vários locatários

#### Cabeçalhos de autenticação

Cada chamada à API HTTP de entrada para a API do Cloud Manager deve conter esses três cabeçalhos:

* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

Os valores que devem ser enviados na variável `x-api-key` e `x-gw-ims-org-id` os cabeçalhos são fornecidos na tela Detalhes de credenciais no [Console do Adobe Developer](https://developer.adobe.com/console). O valor da variável `x-api-key` é a ID do cliente e o valor da variável `x-gw-ims-org-id` é a ID da organização.

#### Configurar o console do Adobe Developer para gerar um token de acesso

Para configurar APIs de autenticação, crie um projeto no Console do Adobe Developer e adicione APIs de comunicação ao projeto no Console do Adobe Developer. A integração gera a Chave da API, Segredo do cliente, Carga (JWT):

1. Entre em contato com o administrador do Adobe Developer Console. Solicite ao administrador que adicione como desenvolvedor.
1. Faça logon em `https://developer.adobe.com/console/`. Use a conta de desenvolvedor provisionada pelo administrador para fazer logon no Adobe Developer Console.
1. Selecione sua organização no canto superior direito. Se não souber sua organização, entre em contato com o administrador.
1. Toque **[!UICONTROL Criar novo projeto]**. Uma tela para começar a usar o novo projeto é exibida. Toque **[!UICONTROL Adicionar API]**. Uma tela com uma lista de todas as APIs ativadas para sua conta é exibida.
1. Selecionar **[!UICONTROL AEM Forms - Comunicações]** e tocar **[!UICONTROL Próximo]**. Uma tela para configurar a API é exibida.
1. Selecionar **[!UICONTROL OPÇÃO 1 Gerar um par de chaves]** e tocar **[!UICONTROL Gerar par de chaves]**. Ele cria e baixa o arquivo de configuração. O arquivo de configuração baixado contém todas as configurações do aplicativo, juntamente com a única cópia da chave privada. O Adobe não registra a chave privada, certifique-se de armazenar com segurança o arquivo baixado. Toque **[!UICONTROL Próximo]**.
1. Selecionar **[!UICONTROL Integrações - Cloud Service]** e tocar **[!UICONTROL Salvar API configurada]**. Toque **[!UICONTROL Conta de serviço (JWT)]** para exibir a chave da API, o segredo do cliente e outras informações necessárias para acessar as APIs. Você configura para usar o token para acessar as APIs.

#### Gerar e usar um token de acesso de forma programada

Para gerar um token de acesso programaticamente, gere um JSON Web Token (JWT) e troque-o pelo Adobe Identity Management Service (IMS) para obter um token de acesso.

Use as seguintes chaves, chamadas de afirmações, para construir o objeto JSON JWT:

* `exp`- a expiração solicitada do token de acesso, expressa como um número de segundos desde 1º de janeiro de 1970 GMT. Para a maioria dos casos de uso, esse é um valor relativamente pequeno. Por exemplo, daqui a cinco minutos, esse valor deve ser 1670923791.
* `iss` - a ID da organização do projeto do Console do Adobe Developer, no formato org_ident@AdobeOrg.
* `sub` - a ID da conta técnica da integração com o Adobe Developer Console, no formato: id@techacct.adobe.com.
* `aud` - a ID do cliente da integração do Console do Adobe Developer com o `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - definido como o valor literal `true`

Esse objeto JSON deve ser codificado em base64 e assinado usando a chave privada do projeto. Finalmente, o valor codificado é enviado no corpo de uma solicitação de POST para `https://ims-na1.adobelogin.com/ims/exchange/jwt` juntamente com a ID do cliente e o Segredo do cliente para o projeto.

##### Exemplo

```JSON
    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache
```

#### Suporte de idioma para JWT

Embora seja possível fazer todo o processo de geração e troca de JWT no código personalizado, é mais comum usar uma biblioteca de nível superior para fazer isso. Várias dessas bibliotecas estão listadas na [Documentação JWT do Adobe I/O](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

### (Somente para APIs de geração de documento) Configurar ativos e permissões

Para usar APIs síncronas, o seguinte é obrigatório:

* Usuários com privilégios de administrador de Experience Manager
* Fazer upload de modelos e outros ativos para a instância do Experience Manager Forms Cloud Service

### (Somente para APIs de geração de documento) Faça upload de modelos e outros ativos para sua instância do Experience Manager

Uma organização geralmente tem vários modelos. Por exemplo, um modelo cada para demonstrativos de cartão de crédito, demonstrativos de benefícios e aplicações de reivindicações. Faça upload de todos esses modelos XDP e PDF para sua instância do Experience Manager. Para fazer upload de um template:

1. Abra a instância do Experience Manager.
1. Vá para Forms > Forms e Documentos
1. Clique em Criar > Pasta e crie uma pasta. Abra a pasta.
1. Clique em Criar > Upload de arquivo e faça upload dos modelos.

### Chamar uma API

O [Documentação de referência da API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) O fornece informações detalhadas sobre todos os parâmetros, métodos de autenticação e vários serviços fornecidos pelas APIs. A documentação de referência da API também fornece o arquivo de definição da API no formato .yaml . Você pode baixar o arquivo .yaml e fazer upload dele para [Postman](https://www.postman.com/) para verificar a funcionalidade das APIs.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Somente membros do grupo forms-users podem acessar APIs de comunicações.
