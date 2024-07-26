---
title: integração do Content credentials
description: Os contents credentials, integrados ao AEM Assets e exibidos na Exibição do Assets, podem oferecer contexto ao histórico de um ativo, incluindo como ele foi feito e quem estava envolvido na sua criação. Como um rótulo nutricional para conteúdo digital, os Contents credentials podem ajudar a aumentar a transparência e a criar confiança com os públicos-alvo.
role: User
source-git-commit: 1c0ffe9d6e45f1d6b3574d1ac5611b2c2e2d00e0
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Credenciais de conteúdo {#content-credentials}

As marcas estão mais preocupadas do que nunca com a transparência de conteúdo, a divulgação de IA e a prevenção da adulteração de ativos. A CAI (Content Authenticity Initiative, iniciativa de autenticidade de conteúdo) na Adobe cria ferramentas compatíveis com o padrão técnico [Coalition for Content Provenance and Authenticity](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model) (C2PA). Os contents credentials, que são um novo tipo de metadados criptografados e invioláveis, podem ajudar os visualizadores a entender a linhagem do conteúdo e garantir a integridade dos ativos da marca. Eles podem incluir uma grande variedade de dados de origem que oferecem insights sobre o histórico de um ativo digital.

Essas informações podem incluir:

* **Emissor ou Assinante:** informações sobre a entidade ou empresa que emitiu a assinatura digital para certificar os certificados ou assina o ativo.
* **Data de Emissão:** a data em que a Credencial de Conteúdo foi aplicada ao ativo.
* **Crédito e Uso:** Informações sobre o produtor do ativo, incluindo nome, identificadores de mídia social ou outras informações relacionadas à identidade.
* **Processo:** Registros de qualquer edição ou modificação feita no ativo.
* **Detalhes do Dispositivo:** Informações sobre o aplicativo ou dispositivo usado para criar ou editar o ativo.
* **Ferramenta de IA usada:** se a IA gerativa foi usada para editar ou criar o ativo, o nome do modelo usado pode ser incluído.
* **Outras Informações Pertinentes:** Dados adicionais também podem ser incluídos para ajudar a oferecer mais contexto sobre o histórico de um ativo.

Para obter uma exibição completa, [Verificar](https://contentcredentials.org/verify) pode oferecer um insight mais abrangente sobre o histórico do ativo.

O Adobe Experience Manager Assets agora é compatível com o Content credentials, permitindo que os usuários vejam os Contents credentials diretamente na visualização do no Assets AEM. Ao observar os detalhes do ativo, qualquer imagem com Contents credentials (como aqueles criados com os serviços GenAI) mostra os detalhes do manifesto em um painel dedicado. Se o ativo for baixado, publicado ou compartilhado, os Contents credentials permanecerão intactos com o ativo.

![ativos](/help/assets/assets/content-credentials.png)

## Acessar Contents credentials {#access-content-credentials}

1. Vá para Assets View UI e clique em **Assets** no painel esquerdo.
1. Navegue até uma pasta e selecione o ativo desejado.
1. Clique em **Detalhes** e selecione `Cr pin` no painel mais à direita. A guia Contents credentials exibe as seguintes informações sobre o ativo.
   1. **Imagem gerada:** Data e hora em que os Contents credentials foram aplicados.
   1. **Resumo do conteúdo:** indica se o ativo foi gerado parcial ou completamente pela IA ou como foi editado.
      ![contents credentials](/help/assets/assets/content-credentials1.png)
   1. **Processo:** Detalha o aplicativo, o dispositivo e a ferramenta de IA (como o Adobe Firefly) usados para gerar o ativo, bem como as alterações feitas posteriormente.
      ![processo](/help/assets/assets/CR-Process.png)
   1. **Sobre estes Contents credentials:** Nome do emissor, juntamente com a data e hora da emissão.
      ![emissor](/help/assets/assets/CR-issuer.png)
