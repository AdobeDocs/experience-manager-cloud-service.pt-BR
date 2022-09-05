---
title: AEM Forms as a Cloud Service - Comunicações
description: Mesclar dados automaticamente com modelos XDP e PDF ou gerar saída nos formatos PCL, ZPL e PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 07b9118b8cfc27bc9e2bfa134fbb57c7ae2728ad
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 1%

---


# Usar processamento síncrono {#sync-processing-introduction}

As comunicações permitem criar, montar e fornecer comunicações personalizadas e orientadas por marcas, como correspondências comerciais, documentos, demonstrativos, cartas de processamento de solicitações, avisos de benefícios, cartas de processamento de solicitações, contas mensais e kits de boas-vindas. Você pode usar as APIs de comunicações para combinar um modelo (XFA ou PDF) com os dados do cliente para gerar documentos nos formatos PDF, PS, PCL, DPL, IPL e ZPL.

Considere um cenário em que você tem um ou mais modelos e vários registros de dados XML para cada modelo. Você pode usar as APIs de comunicações para gerar um documento de impressão para cada registro. <!-- You can also combine the records into a single document. --> O resultado é um documento PDF não interativo. Um documento PDF não interativo não permite que os usuários insiram dados em seus campos.


As comunicações fornecem APIs para geração de documentos sob demanda e programada. Você pode usar APIs síncronas para APIs sob demanda e em lote (APIs assíncronas) para geração de documento agendado:

* As APIs síncronas são adequadas para casos de uso sob demanda, baixa latência e geração de documento de registro único. Essas APIs são mais adequadas para casos de uso baseados em ações do usuário. Por exemplo, gerar um documento depois que um usuário preencher um formulário.

* As APIs em lote (APIs assíncronas) são adequadas para casos de uso de geração de documento com várias throughput programada. Essas APIs geram documentos em lotes. Por exemplo, contas telefônicas, demonstrativos de cartão de crédito e demonstrativos de benefícios gerados todo mês.

## Usar operações síncronas {#batch-operations}

Uma operação síncrona é um processo de geração de documentos de maneira linear. APIs separadas estão disponíveis para:

* Gera um documento do PDF a partir de um modelo e mescla dados nele.
* Gere um documento PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) de um arquivo XDP ou documento PDF.
* Montar documentos PDF
* Desmontar documentos PDF
* Converter um documento em um documento compatível com PDF/A
* Validar um documento compatível com PDF/A


### Autenticar uma chamada de API

As operações síncronas são compatíveis com dois tipos de autenticação:

* **Autenticação básica**: Autenticação básica é um esquema de autenticação simples integrado ao protocolo HTTP. O cliente envia solicitações HTTP com o cabeçalho de Autorização que contém a palavra Básico seguida de um espaço e uma sequência de caracteres codificada em base64, username:password. Por exemplo, para autorizar como administrador / administrador o cliente envia Básico [nome de usuário da string codificada em base64]: [senha de string codificada em base64].

* **Autenticação por token:** A autenticação baseada em token usa um token de acesso (token de autenticação portador) para fazer solicitações ao Experience Manager as a Cloud Service. O AEM Forms as a Cloud Service fornece APIs para recuperar com segurança o token de acesso. Para recuperar e usar o token para autenticar uma solicitação:

   1. [Recupere credenciais do Experience Manager as a Cloud Service no Console do desenvolvedor](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [Instale as credenciais do Experience Manager as a Cloud Service em seu ambiente](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (Servidor de Aplicativos, Servidor da Web ou outros servidores não AEM) configurados para enviar solicitações para (fazer chamadas) o serviço em nuvem.
   1. [Gere um token JWT e trocou-o com as APIs do Adobe IMS para um token de acesso](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. Execute a API do Experience Manager com o token de acesso como um token de autenticação do portador.
   1. [Defina as permissões apropriadas para o usuário da conta técnica no ambiente Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >O Adobe recomenda usar a autenticação baseada em token em um ambiente de produção.


### (Somente para APIs de geração de documento) Configurar ativos e permissões

Para usar APIs síncronas, o seguinte é obrigatório:

* Modelos PDF ou XDP
* [Dados a serem mesclados com modelos](#form-data)
* Usuários com privilégios de administrador de Experience Manager
* Fazer upload de modelos e outros ativos para a instância do Experience Manager Forms Cloud Service

### (Somente para APIs de geração de documento) Faça upload de modelos e outros ativos para sua instância do Experience Manager

Uma organização geralmente tem vários modelos. Por exemplo, um modelo cada para demonstrativos de cartão de crédito, demonstrativos de benefícios e aplicações de reivindicações. Faça upload de todos esses modelos XDP e PDF para sua instância do Experience Manager. Para fazer upload de um template:

1. Abra a instância do Experience Manager.
1. Vá para Forms > Forms e Documentos
1. Clique em Criar > Pasta e crie uma pasta. Abra a pasta.
1. Clique em Criar > Upload de arquivo e faça upload dos modelos.


### Chamar uma API

O [Documentação de referência da API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) O fornece informações detalhadas sobre todos os parâmetros, métodos de autenticação e vários serviços fornecidos pelas APIs. A documentação de referência da API também fornece o arquivo de definição da API no formato .yaml . Você pode baixar o arquivo .yaml e carregá-lo no postman para verificar a funcionalidade das APIs.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Somente membros do grupo forms-users podem acessar APIs de comunicações.
