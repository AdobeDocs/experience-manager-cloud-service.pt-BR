---
title: Uso do GraphiQL IDE no AEM
description: Saiba como usar o GraphiQL IDE no Adobe Experience Manager.
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 100%

---

# Uso do GraphiQL IDE {#graphiql-ide}

Uma implementação do padrão [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE está disponível para uso com o GraphQL do AEM. Pode ser [instalado com o AEM](#installing-graphiql-ide).

>[!NOTE]
>
>O GraphiQL está vinculado ao endpoint global (e não funciona com outros endpoints para configurações específicas do Sites).

A ferramenta GraphiQL permite inserir, testar e depurar consultas diretamente. O GraphiQL também oferece acesso fácil à documentação, facilitando o aprendizado e a compreensão de quais métodos estão disponíveis.

Por exemplo:

* `http://localhost:4502/content/graphiql.html`

Isso fornece recursos como realce de sintaxe, preenchimento automático e sugestão automática, juntamente com um histórico e uma documentação online:

![Interface GraphiQL](assets/cfm-graphiql-interface.png "Interface GraphiQL")

## Instalação do AEM GraphiQL IDE {#installing-graphiql-ide}

O GraphiQL IDE é uma ferramenta de desenvolvimento necessária apenas em ambientes de nível inferior, como uma instância local ou de desenvolvimento. Portanto, não está incluído no projeto do AEM, mas constitui um pacote separado que pode ser instalado em base ad hoc.

1. Navegue até o **[Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)** > **AEM as a Cloud Service**.
1. Pesquise por &quot;GraphiQL&quot; (não deixe de incluir o **i** em **GraphiQL**.
1. Baixe a versão mais recente do **pacote de conteúdo GraphiQL v.x.x.x**
1. No menu de **Início do AEM**, navegue até **Ferramentas** > **Implantação** > **Pacotes**.
1. Clique em **Fazer upload do pacote** e escolha o pacote baixado na etapa anterior. Clique em **Instalar** para instalar o pacote.
