---
title: Uso do GraphiQL IDE no AEM
description: Saiba como usar o GraphiQL IDE no Adobe Experience Manager.
feature: Content Fragments,GraphQL API
source-git-commit: c4490690edb1ec0e2a6b8cca724fe9c290650bc8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 3%

---


# Uso do GraphiQL IDE {#graphiql-ide}

Uma implementação do padrão [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) O IDE está disponível para uso com AEM GraphQL. Pode ser [instalado com AEM](#installing-graphiql-ide).

>[!NOTE]
>
>O GraphiQL está vinculado ao endpoint global (e não funciona com outros endpoints para configurações específicas do Sites).

A ferramenta GraphiQL permite inserir, testar e depurar queries diretamente. O GraphiQL também oferece acesso fácil à documentação, facilitando o aprendizado e a compreensão de quais métodos estão disponíveis.

Por exemplo:

* `http://localhost:4502/content/graphiql.html`

Isso fornece recursos como realce de sintaxe, preenchimento automático, sugestão automática, juntamente com um histórico e documentação online:

![Interface GraphiQL](assets/cfm-graphiql-interface.png "Interface GraphiQL")

## Instalação do AEM GraphiQL IDE {#installing-graphiql-ide}

O GraphiQL IDE é uma ferramenta de desenvolvimento e é necessário apenas em ambientes de nível inferior, como uma instância de desenvolvimento ou local. Por conseguinte, não está incluído no projeto de AEM, mas constitui um pacote separado que pode ser instalado numa base ad hoc.

1. Navegue até o **[Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)** > **AEM as a Cloud Service**.
1. Procure por &quot;GraphiQL&quot; (não deixe de incluir a variável **i** em **GraphiQL**.
1. Baixe a versão mais recente **Pacote de Conteúdo GraphiQL v.x.x**
1. No **Início do AEM** navegue até **Ferramentas** > **Implantação** > **Pacotes**.
1. Clique em **Fazer upload do pacote** e escolha o pacote baixado na etapa anterior. Clique em **Instalar** para instalar o pacote.

