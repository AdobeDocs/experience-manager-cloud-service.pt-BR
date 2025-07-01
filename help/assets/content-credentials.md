---
title: Integração do Content Credentials
description: O Content Credentials, integrado ao AEM Assets e apresentado na Exibição do Assets, pode oferecer contexto no histórico de um ativo, incluindo como ele foi feito e quem estava envolvido na sua criação. Como um rótulo nutricional para conteúdo digital, o Content Credentials pode ajudar a aumentar a transparência e a criar confiança com os públicos-alvo.
role: User
exl-id: 27c25ae0-4477-40c3-85c8-3e0aa725aba7
source-git-commit: 31c9e742d8bdf69c12788794670817864c9c027a
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# Content Credentials {#content-credentials}

As marcas estão mais preocupadas do que nunca com a transparência de conteúdo, a divulgação de IA e a prevenção da adulteração de ativos. O Content Authenticity Initiative (CAI) na Adobe cria ferramentas compatíveis com o padrão técnico [Coalition for Content Provenance and Authenticity](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model) (C2PA). O Content Credentials, um novo tipo de metadados criptografados e invioláveis, pode ajudar os visualizadores a entender a linhagem do conteúdo e garantir a integridade dos ativos da marca. Eles podem incluir uma grande variedade de dados de origem que oferecem ao insight o histórico de um ativo digital.

Essas informações podem incluir:

* **Emissor ou Assinante:** informações sobre a entidade ou empresa que emitiu a assinatura digital para certificar os certificados ou assina o ativo.
* **Data de Emissão:** a data em que a Content Credential foi aplicada ao ativo.
* **Crédito e Uso:** Informações sobre o produtor do ativo, incluindo nome, identificadores de mídia social ou outras informações relacionadas à identidade.
* **Processo:** Registros de qualquer edição ou modificação feita no ativo.
* **Detalhes do Dispositivo:** Informações sobre o aplicativo ou dispositivo usado para criar ou editar o ativo.
* **Ferramenta de IA usada:** se a IA gerativa foi usada para editar ou criar o ativo, o nome do modelo usado pode ser incluído.
* **Outras Informações Pertinentes:** Dados adicionais também podem ser incluídos para ajudar a oferecer mais contexto sobre o histórico de um ativo.

Para obter uma exibição completa, [Verificar](https://contentcredentials.org/verify) pode oferecer uma insight mais abrangente no histórico de ativos.

O Adobe Experience Manager Assets agora é compatível com o Content Credentials, permitindo que os usuários vejam o Content Credentials diretamente na visualização Assets do AEM. Ao observar os detalhes do ativo, qualquer imagem com o Content Credentials (como aquelas criadas com os serviços GenAI) mostra os detalhes do manifesto em um painel dedicado. Se o ativo for baixado, publicado ou compartilhado, a Content Credentials permanecerá intacta com o ativo.

![ativos](/help/assets/assets/content-credentials.png)

## Acessar o Content Credentials {#access-content-credentials}

1. Vá para Assets View UI e clique em **Assets** no painel esquerdo.
1. Navegue até uma pasta e selecione o ativo desejado.
1. Clique em **Detalhes** e selecione `Cr pin` no painel mais à direita. A guia Content Credentials exibe as seguintes informações sobre o ativo.
   1. **Imagem gerada:** Data e hora em que o Content Credentials foi aplicado.
   1. **Resumo do conteúdo:** indica se o ativo foi gerado parcial ou completamente pela IA ou como foi editado.
      ![credenciais de conteúdo](/help/assets/assets/content-credentials1.png)
   1. **Processo:** Detalha o aplicativo, o dispositivo e a ferramenta de IA (como o Adobe Firefly) usada para gerar o ativo, bem como as alterações feitas posteriormente.
      ![processo](/help/assets/assets/CR-Process.png)
   1. **Sobre esta Content Credentials:** Nome do emissor, juntamente com a data e a hora de emissão.
      ![emissor](/help/assets/assets/CR-issuer.png)
