---
title: Integração do Content Credentials
description: O Content Credentials, integrado ao AEM Assets e apresentado na Exibição do Assets, pode oferecer contexto no histórico de um ativo, incluindo como ele foi feito e quem estava envolvido na sua criação. Como um rótulo nutricional para conteúdo digital, o Content Credentials pode ajudar a aumentar a transparência e a criar confiança com os públicos-alvo.
role: User
exl-id: 27c25ae0-4477-40c3-85c8-3e0aa725aba7
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Content Credentials {#content-credentials}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas de metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>documentação para desenvolvedores do AEM Assets</b></a>
        </td>
    </tr>
</table>

As marcas estão mais preocupadas do que nunca com a transparência de conteúdo, a divulgação de IA e a prevenção da adulteração de ativos. A CAI (Content Authenticity Initiative, iniciativa de autenticidade de conteúdo) na Adobe cria ferramentas compatíveis com o padrão técnico [Coalition for Content Provenance and Authenticity](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model) (C2PA). O Content Credentials, um novo tipo de metadados criptografados e invioláveis, pode ajudar os visualizadores a entender a linhagem do conteúdo e garantir a integridade dos ativos da marca. Eles podem incluir uma grande variedade de dados de origem que oferecem insights sobre o histórico de um ativo digital.

Essas informações podem incluir:

* **Emissor ou Assinante:** informações sobre a entidade ou empresa que emitiu a assinatura digital para certificar os certificados ou assina o ativo.
* **Data de Emissão:** a data em que a Content Credential foi aplicada ao ativo.
* **Crédito e Uso:** Informações sobre o produtor do ativo, incluindo nome, identificadores de mídia social ou outras informações relacionadas à identidade.
* **Processo:** Registros de qualquer edição ou modificação feita no ativo.
* **Detalhes do Dispositivo:** Informações sobre o aplicativo ou dispositivo usado para criar ou editar o ativo.
* **Ferramenta de IA usada:** se a IA gerativa foi usada para editar ou criar o ativo, o nome do modelo usado pode ser incluído.
* **Outras Informações Pertinentes:** Dados adicionais também podem ser incluídos para ajudar a oferecer mais contexto sobre o histórico de um ativo.

Para obter uma exibição completa, [Verificar](https://contentcredentials.org/verify) pode oferecer um insight mais abrangente sobre o histórico do ativo.

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
