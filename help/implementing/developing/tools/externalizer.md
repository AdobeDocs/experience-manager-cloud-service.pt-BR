---
title: Externalizar URLs
description: O Externalizador é um serviço OSGi que permite transformar programaticamente um caminho de recurso em um URL externo e absoluto.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Externalizar URLs {#externalizing-urls}

No caso do AEM, a **Externalizador** é um serviço OSGi que permite transformar programaticamente um caminho de recurso (por exemplo, `/path/to/my/page`) em um URL externo e absoluto (por exemplo, `https://www.mycompany.com/path/to/my/page`) ao prefixar o caminho com um DNS pré-configurado.

Como uma instância do AEM as a Cloud Service não pode saber seu URL visível externamente e como, às vezes, um link precisa ser criado fora do escopo da solicitação, esse serviço fornece um local central para configurar esses URLs externos e criá-los.

Este artigo explica como configurar o serviço Externalizador e como usá-lo. Para obter detalhes técnicos do serviço, consulte [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## Comportamento padrão do externalizador e como sobrescrever {#default-behavior}

Pronto para uso, o serviço Externalizador mapeia alguns identificadores de domínio para prefixos absolutos de URL que correspondem aos URLs de serviço do AEM gerados para o ambiente, como `author https://author-p12345-e6789.adobeaemcloud.com` e `publish https://publish-p12345-e6789.adobeaemcloud.com`. Os URLs de base para cada um desses domínios padrão são lidos das variáveis de ambiente definidas pelo Cloud Manager.

Para referência, a configuração OSGi padrão para `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` é efetivamente:

```json
{
   "externalizer.domains": [
      "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
      "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
      "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]",
      "preview $[env:AEM_EXTERNALIZER_PREVIEW;default=http://localhost:4503]"
   ]
}
```

>[!CAUTION]
>
>O padrão `local`, `author`, `preview`, e `publish` Os mapeamentos de domínio do externalizador na configuração OSGi devem ser preservados com o original `$[env:...]` valores listados acima.
>
>Implantação de um personalizado `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` arquivo para AEM as a Cloud Service que omite qualquer um desses mapeamentos de domínio prontos para uso pode resultar em um comportamento imprevisível do aplicativo.

Para substituir o `preview` e `publish` valores, use as variáveis de ambiente do Cloud Manager conforme descrito no artigo [Configuração do OSGi para o AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) e a definição de valores predefinidos `AEM_CDN_DOMAIN_PUBLISH` e `AEM_CDN_DOMAIN_PREVIEW` variáveis.

## Configurar o serviço externalizador {#configuring-the-externalizer-service}

O serviço Externalizer permite definir centralmente o domínio que pode ser usado para prefixar programaticamente caminhos de recursos. O serviço Externalizer só deve ser usado para aplicativos com um único domínio.

>[!NOTE]
>
>Como na aplicação de qualquer [Configurações de OSGi para AEM as a Cloud Service,](/help/implementing/deploying/overview.md#osgi-configuration) as etapas a seguir devem ser executadas em uma instância de desenvolvedor local e, em seguida, confirmadas no código do projeto para implantação.

Para definir um mapeamento de domínio para o serviço Externalizador:

1. Navegue até o Gerenciador de configurações por meio de:

   `https://<host>:<port>/system/console/configMgr`

1. Clique em **Day CQ Link Externalizer** para abrir a caixa de diálogo de configuração.

   ![A configuração OSGi do externalizador](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >O link direto para a configuração é `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Definir um **Domínios** mapeamento. Um mapeamento consiste em um nome exclusivo que pode ser usado no código para fazer referência ao domínio, a um espaço e ao domínio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Em que:

   * **`scheme`** geralmente é http ou https, mas pode ser outro protocolo.

      * A Adobe recomenda o uso de https para aplicar links https.
      * Ele é usado se o código do cliente não substituir o esquema ao solicitar a externalização de um URL.

   * **`server`** é o nome do host (um nome de domínio ou endereço ip).
   * **`port`** (opcional) é o número da porta.
   * **`contextpath`** (opcional) só é definido se o AEM estiver instalado como um aplicativo web em um caminho de contexto diferente.

   Por exemplo: `production https://my.production.instance`

   Os seguintes nomes de mapeamento são predefinidos e sempre devem ser definidos, pois o AEM depende deles:

   * `local` - a instância local
   * `author` - o DNS do sistema de criação
   * `publish` - o DNS do site voltado para o público

   >[!NOTE]
   >
   >Uma configuração personalizada permite adicionar uma nova categoria, como `production`, `staging` ou mesmo sistemas externos não-AEM, como `my-internal-webservice`. É útil evitar a codificação rígida desses URLs em diferentes locais na base de código de um projeto.

1. Clique em **Salvar** para salvar as alterações.

### Usar o serviço externalizador {#using-the-externalizer-service}

Esta seção mostra alguns exemplos de como o serviço Externalizador pode ser usado.

>[!NOTE]
>
>Nenhum link absoluto deve ser criado no contexto de HTML. Por conseguinte, esta utilidade não deve ser utilizada em tais casos.

* **Para externalizar um caminho com o domínio &quot;publicar&quot;:**

  ```java
  String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
  ```

  Considerando o mapeamento de domínio:

   * `publish https://www.website.com`

   * `myExternalizedUrl` termina com o valor:

   * `https://www.website.com/contextpath/my/page.html`

* **Para externalizar um caminho com o domínio &quot;author&quot;:**

  ```java
  String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
  ```

  Considerando o mapeamento de domínio:

   * `author https://author.website.com`

   * `myExternalizedUrl` termina com o valor:

   * `https://author.website.com/contextpath/my/page.html`

* **Para externalizar um caminho com o domínio &quot;local&quot;:**

  ```java
  String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
  ```

  Considerando o mapeamento de domínio:

   * `local https://publish-3.internal`

   * `myExternalizedUrl` termina com o valor:

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>Você pode encontrar mais exemplos na [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
