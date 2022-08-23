---
title: Exteriorização de URLs
description: O Externalizador é um serviço OSGi que permite transformar programaticamente um caminho de recurso em um URL externo e absoluto.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: 28903c1cbadece9d0ef575cdc0f0d7fd32219538
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Exteriorização de URLs {#externalizing-urls}

Em AEM, a variável **Externalizador** é um serviço OSGi que permite transformar programaticamente um caminho de recurso (por exemplo, `/path/to/my/page`) em um URL externo e absoluto (por exemplo, `https://www.mycompany.com/path/to/my/page`) ao prefixar o caminho com um DNS pré-configurado.

Como uma instância AEM as a Cloud Service não pode saber seu URL externamente visível e, às vezes, um link deve ser criado fora do escopo da solicitação, esse serviço fornece um local central para configurar esses URLs externos e criá-los.

Este artigo explica como configurar o serviço Externalizador e como usá-lo. Para obter detalhes técnicos do serviço, consulte a seção [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## Comportamento padrão do Externalizador e Como substituir {#default-behavior}

Pronto para uso, o serviço Externalizador mapeia um punhado de identificadores de domínio para prefixos de URL absolutos que correspondem aos URLs do serviço de AEM que foram gerados para o ambiente, como `author https://author-p12345-e6789.adobeaemcloud.com` e `publish https://publish-p12345-e6789.adobeaemcloud.com`. Os URLs básicos de cada um desses domínios padrão são lidos a partir de variáveis de ambiente definidas pelo Cloud Manager.

Para referência, a configuração padrão do OSGi para `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` é efetivamente:

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
>O padrão `local`, `author`, `preview`e `publish` Os mapeamentos de domínio do Externalizador na configuração OSGi devem ser preservados com o `$[env:...]` valores listados acima.
>
>Implantar um `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` para AEM as a Cloud Service que omite qualquer um desses mapeamentos de domínio prontos para uso podem resultar em comportamento imprevisível do aplicativo.

Para substituir o `preview` e `publish` use as variáveis de ambiente do Cloud Manager, conforme descrito no artigo [Configuração do OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) e definir o predefinido `AEM_CDN_DOMAIN_PUBLISH` e `AEM_CDN_DOMAIN_PREVIEW` variáveis.

## Configurar o serviço Externalizador {#configuring-the-externalizer-service}

O serviço Externalizador permite definir centralmente o domínio que pode ser usado para prefixar programaticamente caminhos de recursos. O serviço Externalizador só deve ser usado para aplicativos com um único domínio.

>[!NOTE]
>
>Como ao aplicar qualquer [configurações OSGi para AEM as a Cloud Service,](/help/implementing/deploying/overview.md#osgi-configuration) as etapas a seguir devem ser executadas em uma instância de desenvolvedor local e, em seguida, confirmadas no código do projeto para implantação.

Para definir um mapeamento de domínio para o serviço Externalizador:

1. Navegue até o Configuration Manager por:

   `https://<host>:<port>/system/console/configMgr`

1. Clique em **Externalizador de links CQ do dia** para abrir a caixa de diálogo de configuração.

   ![A configuração OSGi do Externalizador](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >O link direto para a configuração é `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Defina um **Domínios** mapeamento. Um mapeamento consiste em um nome exclusivo que pode ser usado no código para fazer referência ao domínio, a um espaço e ao domínio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Em que:

   * **`scheme`** geralmente é http ou https, mas pode ser outro protocolo.

      * É recomendável usar https para aplicar links https.
      * Ele será usado se o código do cliente não substituir o esquema ao solicitar a externalização de um URL.
   * **`server`** é o nome do host (um nome de domínio ou endereço ip).
   * **`port`** (opcional) é o número da porta.
   * **`contextpath`** (opcional) só será definido se AEM for instalado como um aplicativo web em um caminho de contexto diferente.

   Por exemplo: `production https://my.production.instance`

   Os seguintes nomes de mapeamento são predefinidos e devem sempre ser definidos conforme AEM dependem deles:

   * `local` - a instância local
   * `author` - DNS do sistema de criação
   * `publish` - DNS, o sítio web público

   >[!NOTE]
   >
   >Uma configuração personalizada permite adicionar uma nova categoria, como `production`, `staging` ou mesmo sistemas externos não AEM como `my-internal-webservice`. É útil evitar a codificação rígida desses URLs em diferentes locais na base de código de um projeto.

1. Clique em **Salvar** para salvar as alterações.

### Uso do Serviço Externalizador {#using-the-externalizer-service}

Esta seção mostra alguns exemplos de como o serviço Externalizador pode ser usado.

>[!NOTE]
>
>Nenhum link absoluto deve ser criado no contexto do HTML. Por conseguinte, este utilitário não deve ser utilizado nestes casos.

* **Para exteriorizar um caminho com o domínio &quot;publicar&quot;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Considerando o mapeamento de domínio:

   * `publish https://www.website.com`

   * `myExternalizedUrl` termina com o valor :

   * `https://www.website.com/contextpath/my/page.html`

* **Para exteriorizar um caminho com o domínio &quot;autor&quot;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Considerando o mapeamento de domínio:

   * `author https://author.website.com`

   * `myExternalizedUrl` termina com o valor :

   * `https://author.website.com/contextpath/my/page.html`

* **Para exteriorizar um caminho com o domínio &quot;local&quot;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Considerando o mapeamento de domínio:

   * `local https://publish-3.internal`

   * `myExternalizedUrl` termina com o valor :

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>Você pode encontrar mais exemplos na [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
