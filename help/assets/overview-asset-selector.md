---
title: Seletor de ativos para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Use o Seletor de ativos para pesquisar, localizar e recuperar metadados e representações de ativos no aplicativo.
role: Admin, User
exl-id: 62b0b857-068f-45b7-9018-9c59fde01dc3
source-git-commit: 0b8c345efa4c8f59b423644944ca2a6f8d54cbb4
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 34%

---

# Seletor de ativos de micro front-end {#Overview}

O Seletor de ativos de micro front-end fornece uma interface do usuário que se integra facilmente ao repositório [!DNL Experience Manager Assets] para navegar ou pesquisar ativos digitais disponíveis no repositório e usá-los na experiência de criação do aplicativo.

A interface do usuário de micro front-end é disponibilizada em sua experiência de aplicativo usando o pacote de Seletor de ativos. Quaisquer atualizações no pacote são automaticamente importadas e o Seletor de ativos implantado mais recente é automaticamente carregado no aplicativo.

![Visão geral](assets/overview.png)

O Seletor de ativos oferece muitos benefícios, como:

* Facilidade de integração com qualquer um dos aplicativos [Adobe](/help/assets/integrate-asset-selector-adobe-app.md) ou [não-Adobe](/help/assets/integrate-asset-selector-non-adobe-app.md) usando a biblioteca JavaScript Vanilla.
* Manutenção facilitada, pois as atualizações do pacote do Seletor de ativos são implantadas automaticamente no Seletor de ativos disponível para seu aplicativo. Não há atualizações necessárias no aplicativo para carregar as modificações mais recentes.
* Facilidade de personalização, pois há propriedades disponíveis que controlam a exibição do Seletor de ativos no aplicativo.
* Filtros de pesquisa de texto completo, prontos para uso e personalizados que navegam rapidamente até os ativos para uso na experiência de criação.
* Capacidade de alternar repositórios em uma organização IMS para seleção de ativos.
* Capacidade de classificar ativos por nome, dimensões e tamanho e visualizá-los na exibição de Lista, Grade, Galeria ou Cascata.

<!--Perform the following tasks to integrate and use Asset Selector with your [!DNL Experience Manager Assets] repository:

1. [Install Asset Selector](#installation)
2. [Integrate Asset Selector using Vanilla JS](#integration-using-vanilla-js)
3. [Use Asset Selector](#using-asset-selector)
-->

<!--
## Setting up Asset Selector {#asset-selector-setup}

![Asset Selector set up](assets/asset-selector-prereqs.png)
-->

## Pré-requisitos{#prereqs}

Você deve garantir os seguintes métodos de comunicação:

* O aplicativo está sendo executado em HTTPS.
* O URL do aplicativo está na lista de permissões de URLs de redirecionamento do cliente IMS.
* O fluxo de logon do IMS é configurado e renderizado usando um pop-up no navegador da Web. Portanto, os pop-ups devem ser ativados ou permitidos no navegador de destino.

Use os pré-requisitos acima se precisar do fluxo de trabalho de autenticação IMS do Seletor de ativos. Como alternativa, se você já estiver autenticado com o fluxo de trabalho do IMS, é possível adicionar as informações do IMS.

**Ver mais**

* [Integrar o Seletor de ativos a um aplicativo Adobe](/help/assets/integrate-asset-selector-adobe-app.md)
* [Integrar o Seletor de ativos a um aplicativo não-Adobe](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [Integrar APIs abertas de mídia dinâmica do Seletor de ativos](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!IMPORTANT]
>
> Este repositório serve como uma documentação complementar que descreve as APIs disponíveis e exemplos de uso para integração do Seletor de ativos. Antes de tentar instalar ou usar o Seletor de ativos, verifique se sua organização recebeu o acesso ao Seletor de ativos como parte do perfil as a Cloud Service do Experience Manager Assets. Se não tiver sido provisionado, você não poderá integrar ou usar esses componentes. Para solicitar o provisionamento, o administrador do programa deve levantar um tíquete de suporte marcado como P2 do Admin Console e incluir as seguintes informações:
>
>* Nomes de domínio em que o aplicativo de integração está hospedado.
>* Após o provisionamento, sua organização receberá `imsClientId`, `imsScope` e um `redirectUrl` correspondentes aos ambientes solicitados que são essenciais para a configuração do Seletor de ativos. Sem essas propriedades válidas, não é possível executar as etapas de instalação.

## Instalação {#installation}

O Seletor de ativos está disponível por meio da CDN do ESM (por exemplo, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) e da versão [UMD](https://github.com/umdjs/umd).

Nos navegadores usando a **Versão UMD** (recomendado):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

Em navegadores com suporte a `import maps` usando a **Versão CDN do ESM**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

No Deno/Webpack Module Federation usando a **Versão CDN do ESM**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

## Utilização do Seletor de ativos {#using-asset-selector}

Depois que o Seletor de ativos estiver configurado e você for autenticado para usar o Seletor de ativos com o aplicativo [!DNL Adobe Experience Manager] as a [!DNL Cloud Service], você poderá selecionar ativos ou executar várias outras operações para pesquisar seus ativos no repositório.

![using-asset-selector](assets/using-asset-selector.png)

* **A**: [Ocultar/Mostrar painel](#hide-show-panel)
* **B**: [Alternador de repositório](#repository-switcher)
* **C**: [Ativos](#repository)
* **D**: [Filtros](#filters)
* **E**: [Barra de pesquisa](#search-bar)
* **F**: [Classificação](#sorting)
* **G**: [Classificação em ordem crescente ou decrescente](#sorting)
* **H**: [Exibição](#types-of-view)

### Ocultar/Mostrar painel {#hide-show-panel}

Para ocultar pastas na navegação à esquerda, clique no ícone **[!UICONTROL Ocultar pastas]**. Para desfazer as alterações, clique no ícone **[!UICONTROL Ocultar pastas]** novamente.

### Alternador de repositório {#repository-switcher}

O Seletor de ativos também permite alternar repositórios para seleção de ativos. Você pode selecionar o repositório de sua escolha no menu suspenso disponível no painel esquerdo. As opções de repositório disponíveis na lista suspensa se baseiam na propriedade `repositoryId` definida no arquivo `index.html`. Ela se baseia no ambiente da organização IMS selecionada que é acessado pelo usuário conectado. Os consumidores podem transmitir um `repositoryID` de sua preferência e, nesse caso, o Seletor de ativos interrompe a renderização do alternador de repositório e renderiza ativos somente do repositório especificado.

### Repositório de ativos

É uma coleção de pastas de ativos que você pode usar para executar operações.

### Filtros prontos para uso {#filters}

O Seletor de ativos também fornece opções de filtro prontas para uso para refinar os resultados da pesquisa. Os filtros disponíveis são os seguintes:

* **[!UICONTROL Status]:** inclui o estado atual do ativo entre `all`, `approved`, `rejected` ou `no status`.
* **[!UICONTROL Tipo de arquivo]:** inclui `folder`, `file`, `images`, `documents` ou `video`.
* **[!UICONTROL Status de expiração]:** menciona os ativos com base em sua duração de expiração. Você pode marcar a caixa de seleção `[!UICONTROL Expired]` para filtrar ativos que expiraram ou definir `[!UICONTROL Expiration Duration]` de um ativo para exibir ativos com base em sua duração de expiração. Quando um ativo já expirou ou está prestes a expirar, um selo aparece para descrever o mesmo. Além disso, você pode controlar se deseja permitir o uso (ou arrastar e soltar) de um ativo expirado. Veja mais sobre [personalizar ativos expirados](/help/assets/asset-selector-customization.md#customize-expired-assets). Por padrão, o selo **Expirando em breve** é exibido para ativos que expiram nos próximos 30 dias. No entanto, você pode configurar a expiração usando a propriedade `expirationDate`.

  >[!TIP]
  >
  > Para visualizar ou filtrar ativos com base em suas datas de expiração futuras, mencione o intervalo de datas futuro no campo `[!UICONTROL Expiration Duration]`. Ele exibe os ativos com o selo **expirando em breve** neles.

* **[!UICONTROL Tipo MIME]:** inclui `JPG`, `GIF`, `PPTX`, `PNG`, `MP4`, `DOCX`, `TIFF`, `PDF`, `XLSX`.
* **[!UICONTROL Tamanho da Imagem]:** inclui largura mínima/máxima, altura mínima/máxima da imagem.

  ![rail-view-example](assets/filters-asset-selector.png)

### Pesquisa personalizada

Além da pesquisa de texto completo, o Seletor de ativo permite pesquisar ativos em arquivos usando a pesquisa personalizada. Você pode usar filtros de pesquisa personalizados nos modos de exibição Modal e Painel.

![custom-search](assets/custom-search1.png)

Você também pode criar um filtro de pesquisa padrão para salvar os campos que pesquisa frequentemente e usá-los posteriormente. Para criar uma pesquisa personalizada para seus ativos, você pode usar a propriedade `filterSchema`.

### Barra de pesquisa {#search-bar}

O Seletor de ativos permite executar uma pesquisa de texto completo dos ativos no repositório selecionado. Por exemplo, se você digitar a palavra-chave `wave` na barra de pesquisa, todos os ativos com a palavra-chave `wave` mencionada em qualquer uma das propriedades de metadados serão exibidos.

### Classificação {#sorting}

Você pode classificar ativos no Seletor de ativos por nome, dimensões ou tamanho de um ativo. Também é possível classificar os ativos em ordem crescente ou decrescente.

### Tipos de visualização {#types-of-view}

O Seletor de ativos permite exibir o ativo em quatro exibições diferentes:

* **![exibição de lista](assets/do-not-localize/list-view.png) [!UICONTROL Exibição de Lista]** A exibição de lista exibe arquivos e pastas roláveis em uma única coluna.
* **![exibição de grade](assets/do-not-localize/grid-view.png) [!UICONTROL Exibição de grade]** A exibição de grade exibe arquivos e pastas com rolagem em uma grade de linhas e colunas.
* **![exibição de galeria](assets/do-not-localize/gallery-view.png) [!UICONTROL exibição de galeria]** A exibição de galeria exibe arquivos ou pastas em uma lista horizontal bloqueada no centro.
* **![exibição em cascata](assets/do-not-localize/waterfall-view.png) [!UICONTROL exibição em cascata]** A exibição em cascata exibe arquivos ou pastas no formato de uma Bridge.

**Gráfico de Visão Geral**


## Saiba mais sobre os principais recursos {#key-capabilities-asset-selector}

<table>
<tr>
    <td>
        <img src="assets/integrate-asset-selector.gif" width="70px" height="70px" alt="Integrar gráfico do Seletor de ativos"><br/>
        <a href="integrate-asset-selector.md">Seletor de ativos de integração</a>
        <p>
        <em>Conheça os vários recursos para integrar o Seletor de ativos a vários aplicativos.
        </p>
     </td>
    <td>
        <img src="assets/with-adobe-app.gif" width="70px" height="70px" alt="Integrar o Seletor de ativos ao gráfico de aplicativos do Adobe"><br/>
        <a href="integrate-asset-selector.md">Integrar o Seletor de ativos aos aplicativos Adobe</a>
        <p>
        <em>Saiba como integrar o Seletor de ativos a vários aplicativos Adobe.</em>
        </p>
    </td>
    <td>
        <img src="assets/third-party-app.gif" width="70px" height="70px" alt="Integrar gráfico do Seletor de ativos"><br/>
        <a href="integrate-asset-selector.md">Integrar o Seletor de ativos a aplicativos de terceiros</a>
        <p>
        <em>Descarte os recursos para integrar o Seletor de ativos a aplicativos que não sejam do Adobe.</em>
        </p>
    </td>
    <td>
        <img src="assets/with-dynamic-media-open-api.gif" width="70px" height="70px" alt="Integrar gráfico do Seletor de ativos"><br/>
        <a href="integrate-asset-selector.md">Integrar o Seletor de ativos às APIs abertas do Dynamic Media</a>
        <p>
        <em>Saiba como integrar o Seletor de ativos às APIs do Dynamic Media Open.</em>
        </p>
     </td>
</tr>
<tr>
    <td>
        <img src="assets/asset-selector-examples.gif" width="70px" height="70px" alt="Gráfico de propriedades do Seletor de ativos"><br/>
        <a href="asset-selector-customization.md">Propriedades do seletor de ativos</a>
        <p>
        <em>Saiba mais sobre as noções básicas de personalização de vários componentes do Seletor de ativos, como filtros, seleção de ativos, ativos expirados e muito mais. </em>
        </p>
    </td>
    <td>
        <img src="assets/asset-selector-properties.gif" width="70px" height="70px" alt="Gráfico de exemplos do Seletor de ativos"><br/>
        <a href="asset-selector-customization.md">Exemplos de seletores de ativos</a>
        <p>
        <em>Entenda o uso de propriedades de maneira prática. </em>
        </p>
    </td>
    <td>
        <img src="assets/customize-asset-selector.gif" width="70px" height="70px" alt="Personalizar gráfico do Seletor de ativos"><br/>
        <a href="asset-selector-customization.md">Personalizações do seletor de ativos</a>
        <p>
        <em>Configure e personalize vários componentes do Seletor de ativos com base em sua usabilidade. </em>
        </p>
    </td>
    <td>
        <img src="assets/asset-selector-upload.gif" width="70px" height="70px" alt="Gráfico de upload do Seletor de ativos"><br/>
        <a href="asset-selector-upload.md">Carregamento do seletor de ativos</a>
        <p>
        <em>Saiba como carregar arquivos ou pastas para o Seletor de ativos do seu sistema de arquivos local ou de terceiros. </em>
        </p>
    </td>
</tr>
</table>

>[!MORELIKETHIS]
>
>* [Personalizações do Seletor de ativos](/help/assets/asset-selector-customization.md)
>* [Integrar o Seletor de ativos a vários aplicativos](/help/assets/integrate-asset-selector.md)
>* [Propriedades do Seletor de ativos](/help/assets/asset-selector-properties.md)
>* [Integrar o Seletor de ativos ao Dynamic Media com recursos OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
