---
title: Criar URLs personalizados usando o Dynamic Media com recursos OpenAPI
description: Use os recursos OpenAPI do Dynamic Media para transformar seus URLs de entrega de ativos longos em URLs personalizados curtos e de marca. Um URL personalizado é uma versão curta, limpa, fácil de lembrar e legível do seu URL de entrega complexo. Você pode incluir o nome da sua marca, nomes de produtos e palavras-chave relevantes no URL personalizado para aumentar a visibilidade da sua marca e o envolvimento do usuário
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: e4ee2e3f251f585a3e057c04d62039a0c2e8bef1
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---


# Usar URLs personalizados{#vanity-urls}

Use o [!DNL Dynamic Media OpenAPI capabilities] para transformar suas URLs de entrega de ativos longos em URLs personalizadas curtas e de marca. Os URLs de entrega de ativos padrão incluem UUIDs de ativos gerados pelo sistema que tornam o URL de entrega complexo, difícil de lembrar e compartilhar. Substitua esses UUIDs de ativos por identificadores simples (IDs personalizadas) para gerar um URL personalizado. Um URL personalizado é uma versão curta, limpa e legível do URL de entrega complexo.

Consulte os seguintes formatos de URL para entender a diferença entre eles:
* [URL de entrega padrão](#standard-urls)
* [URLs personalizadas](#vanity-url)

As URLs de entrega padrão usam `aaid` seguido por uma UUID, enquanto as URLs personalizadas usam `avid` seguido por um identificador personalizado (identificador personalizado).

Use identificadores personalizados simples e curtos para tornar o URL de entrega curto, limpo, legível, fácil de lembrar e compartilhar. Use o nome da sua marca, nomes de produtos e palavras-chave relevantes como IDs personalizadas para aumentar a visibilidade da sua marca e o engajamento do usuário.

Quando o usuário clica na URL personalizada, o [!DNL Dynamic Media with OpenAPI] mapeia automaticamente para o local do ativo original no momento da assimilação e os resolve corretamente no momento da entrega para o servidor do ativo para o usuário.

Saiba como [criar URLs personalizados](#create-vanity-urls).

## URLs de entrega padrão{#standard-urls}

A URL de entrega de ativos [!DNL Dynamic Media with OpenAPI] padrão inclui um identificador exclusivo gerado pelo sistema e segue o formato a seguir.

***Formato:*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:aaid:aem:<asset-uuid>/as/<seoname>.<format>`

A URL de entrega padrão inclui `aaid` (*identificador de ativo real*) após `urn:` e uma UUID entre `urn:aaid:aem:` e `/as/<seoname>.<format>`.

***Exemplo:*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:aaid:aem:43341ab1-4086-44d2-b7ce-ee546c35613b/as/check.jpeg`

No exemplo acima, `43341ab1-4086-44d2-b7ce-ee546c35613b` é a UUID.

## URLs personalizadas{#vanity-url}

Os URLs personalizados incluem um identificador personalizado no lugar da UUID do ativo e seguem o formato a seguir.

***Formato:*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/as/<seoname>.<format>`

A URL personalizada inclui `avid` (*identificador personalizado real*) após `urn:` e sua ID personalizada entre `urn:avid:aem:` e `/<seoname>.<format>`.

***Exemplo:*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:avid:aem:VanityCheck/as/check.jpeg`

No exemplo acima, `VanityCheck` é a ID personalizada que substituiu a UUID.

## Explore os principais recursos e benefícios{#capabilities-and-benefits-of-vanity-urls}

Usar IDs personalizadas significativas para personalizar os URLs de entrega de ativos padrão fornece várias vantagens e um impacto mensurável. Alguns dos principais recursos e benefícios dos URLs personalizados incluem o seguinte.

### Principais recursos{#key-capabilities}

* **Personalização de URL:** Substitua identificadores longos (UUIDs de ativos) na URL de entrega por alternativas mais curtas e alinhadas à marca para gerar uma URL de entrega mais limpa.
* **Redirecionamento em tempo real:** URLs personalizadas redirecionam para UUIDs de ativos originais no tempo de execução sem interromper os fluxos de trabalho. Os usuários veem URLs limpos na barra de endereços enquanto o sistema lida com o roteamento técnico.
* **Gerenciamento fácil de links:** personalize suas URLs personalizadas a qualquer momento, sem afetar o desempenho de entrega de ativos.

### Principais benefícios{#key-benefits}

* **Aprimora a experiência do usuário:** URLs personalizadas e mais curtas são legíveis, fáceis de ler, memorizar e compartilhar.

* **Melhora o engajamento do usuário:** URLs com marcas geram confiança e confiança no usuário. Os usuários têm mais probabilidade de clicar em links profissionais de marca, resultando em taxas de cliques mais altas.

* **Otimização de SEO:** as URLs que incluem palavras-chave relevantes melhoram as classificações e a descoberta do mecanismo de pesquisa.

* **Visibilidade da marca aprimorada:** as URLs específicas da marca fortalecem a presença da marca em todos os canais de marketing, incluindo email, redes sociais e campanhas de publicidade.
Além disso, o uso consistente de URLs de marca em todas as comunicações reforça a identidade e o reconhecimento da marca.

* **Rastreamento e análise de campanhas:** use URLs personalizadas exclusivas para campanhas e canais diferentes, a fim de obter informações detalhadas sobre fontes de tráfego e desempenho de conversão.

## Pré-requisitos{#prerequisites-for-creating-vanity-id}

Para criar a URL personalizada, verifique se você já [aprovou os ativos para entrega pública](/help/assets/manage-organize-assets-view.md#manage-asset-status).

## Criar URLs personalizados{#create-vanity-urls}

Execute as seguintes etapas para criar URLs personalizados:
1. [Configurar metadados de ativos](#set-up-asset-metadata)
1. [Criar e mapear a variável de ambiente do Cloud Manager](#map-cloud-manager-environment-variable)
1. [Aprovar os ativos que exigem URL personalizado para entrega](/help/assets/manage-organize-assets-view.md#manage-asset-status)
1. [Gerar URLs personalizados](#generate-vanity-urls)

### Configurar metadados de ativos{#set-up-asset-metadata}

Execute o seguinte para configurar a ID personalizada no formulário de metadados do ativo:
1. Acesse a página de detalhes da pasta que contém seus ativos para entrega do [!DNL Dynamic Media with OpenAPI].
1. [Edite esse formulário de metadados](/help/assets/metadata-assets-view.md#edit-metadata-forms) seguindo um destes procedimentos:
   * Adicione um novo campo de metadados e especifique a ID personalizada necessária como o valor desse campo.
   * Atualize o campo existente substituindo o valor de uma propriedade de metadados existente pela ID personalizada necessária. Conheça as [práticas recomendadas](#best-practices) para criar a ID personalizada.
     ![ID personalizada](/help/assets/assets/vanity-id-metadata.png)
Saiba mais sobre [esquemas de metadados](/help/assets/metadata-schemas.md).

     >[!NOTE]
     >
     > * Use IDs personalizadas exclusivas para cada ativo. Sempre verifique se os ativos que compartilham o mesmo formulário de metadados têm IDs personalizadas exclusivas para DM com entrega de OpenAPI por meio de URLs personalizados. Se dois ativos compartilharem a mesma ID personalizada, o DM com OpenAPI fornecerá o ativo que recebeu essa ID mais recentemente, substituindo o direito anterior da ID por outro ativo.
     >
     > * Um único ativo pode ter várias IDs personalizadas. [Contate o suporte da Adobe](https://helpx.adobe.com/in/contact.html) e gere uma solicitação para gerar as IDs personalizadas necessárias.

Depois de configurar sua ID personalizada no formulário de metadados de ativos, [mapeie este campo de metadados para o mecanismo de entrega do sistema](#map-cloud-manager-environment-variable).

### Criar e mapear a variável de ambiente do Cloud Manager{#map-cloud-manager-environment-variable}

Execute as seguintes etapas para criar uma variável de ambiente e mapeá-la para o campo de metadados que contém a ID personalizada:

1. [Navegue até a página de configurações do seu ambiente Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) e faça o seguinte:
   1. Adicionar a variável `ASSET_DELIVERY_VANITY_ID`. Esta é a chave.
   1. Use o campo de valor para mapear para a propriedade de metadados do ativo que contém a ID personalizada. O mapeamento segue o formato `dc:<your-metadata-property>`, em que o prefixo do mapeamento de metadados (como dc:) varia com base na propriedade de configuração dos metadados do ativo.
      ![Variável ASSET_DELIVERY_VANITY_ID](/help/assets/assets/environment-config.png)
1. Salve as alterações para reiniciar os pods em seu ambiente.

### Aprovar os ativos para entrega{#approve-assets-for-delivery}

Depois de mapear a variável `ASSET_DELIVERY_VANITY_ID` no ambiente do Cloud Manager para a propriedade de metadados do ativo que contém a ID personalizada, [aprove seus ativos que exigem uma URL personalizada para entrega](/help/assets/manage-organize-assets-view.md#manage-asset-status).

### Gerar URLs personalizados{#generate-vanity-urls}

Faça as seguintes substituições no URL de entrega padrão para transformá-lo em um URL personalizado:

* Substitua **UUID** por sua **ID personalizada**.
* Substituir `aaid` por `avid`.

Consulte a [transformação de URL do padrão para o URL personalizado](#standard-urls) acima.
Saiba como [copiar o Dynamic Media com URLs de entrega de OpenAPI](/help/assets/approve-assets.md#copy-delivery-url-for-approved-assets) para seus ativos.

Quando o usuário clica na URL personalizada, o [!DNL Dynamic Media with OpenAPI] mapeia automaticamente a ID personalizada para a UUID do ativo original no momento da assimilação e os resolve corretamente no momento da entrega para fornecer o ativo ao usuário sem atraso. Você pode personalizar o URL personalizado em tempo real sem afetar o desempenho do delivery do ativo.

[Melhore o impacto de seus URLs personalizados usando os recursos avançados de personalização do AEM Cloud Service.](#scale-using-vanity-url)

## Dimensionar usando URLs personalizados{#scale-using-vanity-url}

O AEM as a Cloud Service permite que você [personalize os nomes DNS e CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/introduction) em seus endereços Web. Use esses recursos do AEMCS com suas URLs personalizadas para transformá-las em endereços da Web exclusivos que sejam limpos, descritivos, de marca, intuitivos e forneçam os [benefícios mencionados acima](#key-benefits).

Consulte o seguinte URL personalizado e seus componentes personalizáveis:

**Formato de URL personalizado:**

`https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/as/<seoname>.<format>`

<table style="border-collapse:collapse; table-layout:auto; width:auto;">
<tr valign="top">
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>https://delivery&#8209;&lt;tenant&gt;.adobeaemcloud.com</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#customize-dns">Personalizar este DNS</a></div>
</td>
<td style="padding:0 6px; white-space:nowrap; text-align:center;">/</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>adobe/assets/urn:avid:aem:</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#rewrite-cdn-rules">Personalizar URL com regras de regravação</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>&lt;vanity-id&gt;</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#create-vanity-urls">Criar ID personalizada</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:left; width:1%;">
<code>/as/&lt;seoname&gt;.&lt;format&gt;</code>
</td>
</tr>
</table>

**Formato de URL personalizado com nomes DNS e CDN personalizados:**

`https://<custom-dns>` `/` `dam/assets/` `<vanity-id>` `/as/<seoname>.<format>`

**Componentes de URL personalizáveis**

* ***[Nome DNS (nome do host):](#customize-DNS)*** `https://delivery-<tenant>.adobeaemcloud.com` é o domínio de servidor que hospeda seus ativos. [Personalizar DNS para alterar o nome do host](#customize-DNS).
* ***[Regras de regravação de CDN:](#rewrite-cdn-rules)*** `adobe/assets/urn:avid:aem:` é a estrutura de caminho que identifica tipos de ativos e métodos de entrega. [Reescreva as regras de CDN](#rewrite-cdn-rules) para modificar o caminho do domínio.

### Personalizar DNS{#customize-dns}

[Acione uma solicitação ao suporte da Adobe](https://helpx.adobe.com/in/contact.html) para gerar o DNS personalizado necessário para sua camada de entrega. Siga estas [práticas recomendadas](#best-practices) para criar nomes DNS personalizados.

### Substituir regras CDN{#rewrite-cdn-rules}

Execute as seguintes etapas para regravar as regras de CDN para delivery:

1. Navegue até o repositório do AEM para criar um arquivo de configuração YAML.
2. Execute as etapas na seção [configuração](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-error-pages#setup) para definir regras CDN e implantar a configuração por meio do pipeline de configuração do Cloud Manager.
Siga estas [práticas recomendadas](#best-practices) para criar seu caminho de domínio.
   [Saiba mais sobre as regras de regravação da CDN](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#request-transformations).

A seguir estão exemplos de regras de regravação para anexar nomes de arquivo com extensões em URLs personalizados. Personalize essas regras de regravação de acordo com seus requisitos específicos. [Contate o suporte da Adobe](https://helpx.adobe.com/in/contact.html) para obter mais assistência:

```- name: cdn-rewrite-rule
  when:
    allOf:
      - reqProperty: tier
        equals: delivery
```

#### Para SVG, GIF e PDF {#svg-gif-pdf}

```
    type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:svg|gif|pdf|docx|xlsx))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/original/as/\1\2
```

#### Para vídeo{#video}

Para vídeos incluindo MP4, MOV, AVI e MKV

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:mp4|mov|avi|mkv))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/play\2
```

#### Para imagem{#image}

Para todos os tipos de imagem, exceto SVG.

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.[^/]+)(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/as/\1\2
```

## Siga as práticas recomendadas para criar URLs personalizados limpos{#best-practices}

Siga estas práticas recomendadas para criar IDs personalizadas, DNS personalizados e nomes de domínio:

1. Não use caracteres especiais em IDs personalizadas, como espaços, barras, hifens e muito mais. O sistema substitui caracteres especiais em IDs personalizadas usando um mapeamento predefinido.
1. Use o nome da sua marca, nomes de produtos e palavras-chave relevantes em suas IDs personalizadas, DNS personalizadas e nomes de domínio para aumentar a visibilidade da sua marca e o envolvimento do usuário.
1. Use palavras curtas e descritivas ou strings que transmitam significado.
1. Use textos que convidam usuários para cliques.
