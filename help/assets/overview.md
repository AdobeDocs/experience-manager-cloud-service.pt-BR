---
title: Introdução ao Assets as a Cloud Service para gerenciamento de ativos digitais no AEM
description: Introdução ao Assets as a Cloud Service para gerenciamento de ativos digitais no AEM
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: f72f72e87dabe89cafc0a56feb35f58ae1a97dfb
workflow-type: tm+mt
source-wordcount: '5078'
ht-degree: 8%

---

# Introdução ao Assets as a Cloud Service para gerenciamento de ativos digitais no AEM {#assets-as-cloud-service-digital-asset-management-aem}

O AEM Assets as a Cloud Service oferece uma solução PaaS nativa em nuvem para que as empresas não apenas executem suas operações de Gerenciamento de ativos digitais e Dynamic Media, mas também usem recursos inteligentes de próxima geração, como IA/ML. Tudo isso em um sistema que está sempre atualizado, sempre disponível e aprendendo.

A Adobe oferece uma solução robusta de gerenciamento de ativos digitais (DAM) para você aproveitar ao máximo seus ativos digitais. O Adobe Experience Manager Assets tem duas experiências separadas que usam o mesmo repositório de Cloud Services para atender aos seus requisitos. Para obter informações sobre experiências personalizadas para o AEM Assets, consulte [Experiências personalizadas disponíveis para o Gerenciamento de ativos digitais](#persona-based-experiences).

Para obter informações sobre as ofertas do AEM Assets Ultimate e do AEM Assets Prime, consulte [Assets as a Cloud Service Ultimate](/help/assets/assets-ultimate-overview.md) e [Assets as a Cloud Service Prime](/help/assets/assets-prime.md).

Alguns dos principais recursos do Gerenciamento de ativos digitais da Adobe incluem:

![add-tags](assets/aem-assets-features-landing-page.png)


>[!BEGINTABS]

>[!TAB Assimilação de ativos]

## Assimilação de ativos {#asset-ingestion}

Use o recurso de importação em massa para importar um grande número de ativos diretamente de uma fonte de dados, como Azure, AWS, Google Cloud, Dropbox e OneDrive, para o Assets as a Cloud Service.

Você pode executar a operação de importação em massa usando a exibição Admin ou a exibição Assets. A exibição do Assets fornece mais opções de fonte de dados em comparação à exibição do Administrador.

Além da interface de usuário do navegador da Web, o Experience Manager oferece suporte a outros clientes no desktop. Eles também fornecem experiência de upload sem a necessidade de acessar o navegador da Web.

* O Adobe Asset Link fornece acesso a ativos do Experience Manager em aplicativos de desktop da Adobe Photoshop, Adobe Illustrator e Adobe InDesign. Você pode fazer upload do documento aberto para o Experience Manager. Você pode fazer isso diretamente por meio da interface do Adobe Asset Link encontrada nesses aplicativos de desktop.

* O aplicativo de desktop do Experience Manager simplifica o trabalho com ativos no desktop, independentemente do tipo de arquivo ou do aplicativo nativo que os manipula. É útil fazer upload de arquivos em hierarquias de pastas aninhadas a partir do sistema de arquivos local, pois o upload do navegador só suporta o upload de listas de arquivos simples.

Use estes links para acessar a documentação detalhada sobre estas ferramentas de assimilação de ativos:

<table>
<td>
   <a href="/help/assets/bulk-import-assets-view.md">
   <img alt="Ferramenta Importação em massa" src="./assets/bulk-images.jpeg" />
   </a>
   <div>
      <a href="/help/assets/bulk-import-assets-view.md">
      <strong>Usar ferramenta Importação em Massa</strong>
      </a>
   </div>
   <p>
      <em>Saiba como importar um grande número de ativos diretamente de uma fonte de dados</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/en/docs/experience-manager-desktop-app/using/get-started">
   <img alt="Usar o aplicativo de desktop do AEM" src="./assets/desktop-app-upload.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/en/docs/experience-manager-desktop-app/using/get-started">
      <strong>Usar aplicativo de desktop do AEM</strong>
      </a>
   </div>
   <p>
      <em>Saiba como usar o aplicativo de desktop do AEM para carregar arquivos em hierarquias de pastas aninhadas a partir do sistema de arquivos local.</em>
   </p>
</td>
<td>
   <a href="https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html">
   <img alt="Usar o Adobe Asset Link" src="./assets/adobe-asset-link.jpeg" />
   </a>
   <div>
      <a href="https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html">
      <strong>Usar o Adobe Asset Link</strong>
      </a>
   </div>
   <p>
      <em>Saiba como carregar ativos para o Experience Manager usando aplicativos do Creative Cloud.</em>
   </p>
</td>
</table>

>[!TAB Recursos alimentados por IA]

**Tags inteligentes**: as Tags inteligentes usam a estrutura artificialmente inteligente do Adobe Sensei para treinar o algoritmo de reconhecimento de imagem de acordo com sua estrutura de tags e sua taxonomia comercial. Essa inteligência de conteúdo é usada para aplicar tags relevantes em um conjunto diferente de ativos. Por padrão, o AEM aplica tags inteligentes automaticamente a ativos carregados.

**Marcação e pesquisa inteligente baseadas em cores**: o AEM Assets usa os recursos de IA da Adobe Sensei para distinguir cores em uma imagem e aplicar essas características como marcas automaticamente na assimilação. Essas tags permitem uma experiência de pesquisa aprimorada, com base na composição de cores da imagem.

**Metadados gerados por IA**: o AEM Assets usa IA para gerar metadados automaticamente, incluindo Título, Descrição e Palavras-chave. Esses campos gerados pela IA melhoram a precisão dos metadados, tornando os ativos mais fáceis de pesquisar, categorizar e recomendar. Essa abordagem não só aumenta a eficiência eliminando a marcação manual, mas também garante a consistência e a escalabilidade em grandes volumes de conteúdo digital.

**Renomear ativos alimentados por IA** em massa: [O modo de exibição do Assets permite renomear vários ativos de uma só vez usando a Inteligência Artificial](/help/assets/bulk-rename-assets-view.md). Você pode selecionar vários arquivos de uma vez e renomeá-los todos juntos. Alguns dos exemplos de prompts de renomeação conversacional incluem *Alterar todos os arquivos para &#39;my-file&#39; e anexar um número incremental* e *Prefixar os arquivos com 001, 002, etc. e traduzir para inglês*.

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="Tags inteligentes no AEM Assets" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>Adicionar tags inteligentes de IA aos ativos</strong>
      </a>
   </div>
   <p>
      <em>Saiba como aplicar marcas inteligentes automaticamente a ativos carregados.</em>
   </p>
</td>


<td>
   <a href="/help/assets/color-tag-images.md">
   <img alt="Adicionar tags inteligentes baseadas em cores" src="./assets/color-tags.jpg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong>Adicionar marcas inteligentes baseadas em cores</strong>
      </a>
   </div>
   <p>
      <em>Saiba como aplicar tags baseadas em cores automaticamente na assimilação.</em>
   </p>
</td>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="Metadados gerados por IA" src="./assets/ai-generated-metadata-landing.jpg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>Metadados gerados pela IA</strong>
      </a>
   </div>
   <p>
      <em>Use a IA para gerar metadados de ativos, como Título e Descrição. </em>
   </p>
</td>
</table>

**Pesquisa contextual**: o AEM Assets permite pesquisar ativos disponíveis no repositório definindo prompts de texto. O Experience Manager Assets transforma automaticamente os prompts de texto em filtros de pesquisa e exibe os resultados da pesquisa. Você pode visualizar e modificar filtros automáticos usando o Painel Filtros para restringir mais os resultados da pesquisa. Alguns dos exemplos de prompt de texto conversacional incluem o seguinte:

* *Imagens com pelo menos 200px de altura e 100px de largura com praia e céu limpo* e
* *Preciso de imagens do céu azul com altura de 1500 e 2500 pixels, criadas no mês passado, que não tenham expirado e tenham sido aprovadas*.

**Gerar ativos usando o Adobe Firefly no AEM**: o AEM Assets permite gerar um ativo, se a consulta de pesquisa não retornar resultados, usando o Adobe Firefly em tempo real. O AEM Assets também permite fazer upload da imagem gerada para o repositório do AEM Assets na interface do usuário do AEM Assets.

**Integração com o Adobe Express**: o AEM Assets integra-se nativamente com o Adobe Express, o que permite acessar os ativos armazenados diretamente no AEM Assets na interface do usuário do Adobe Express. Você também pode usar a Inteligência artificial do Adobe Firefly no Express para gerar imagens usando prompts de texto simples e colocá-las na tela do Express. Em seguida, você pode salvar o conteúdo novo ou editado em um repositório do AEM Assets.

<table>
<td>
   <a href="/help/assets/search-assets-view.md#contextual-search">
   <img alt="Pesquisa contextual" src="./assets/ai-based-search.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#contextual-search">
      <strong>Pesquisa contextual</strong>
      </a>
   </div>
   <p>
      <em>Saiba como pesquisar ativos usando prompts de texto simples.</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md#search-firefly">
   <img alt="Gerar ativos usando o Adobe Firefly" src="./assets/adobe-firefly.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#search-firefly">
      <strong>Gerar ativos usando o Adobe Firefly</strong>
      </a>
   </div>
   <p>
      <em>Gerar ativos em tempo real usando o Adobe Firefly.</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="Integração com o Adobe Express" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>Integração com o Adobe Express</strong>
      </a>
   </div>
   <p>
      <em>Usar os recursos de IA do Adobe Express na interface do usuário do AEM Assets.</em>
   </p>
</td>
</table>

**Smart Imaging**: o Smart Imaging oferece um desempenho ainda melhor de entrega de ativos de imagem, otimizando automaticamente o formato de imagem e o tamanho do arquivo com base na capacidade do navegador do cliente. Ele funciona com suas predefinições de imagem existentes e usa inteligência na entrega. Essa inteligência reduz ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador e da conexão de rede.

**Recorte inteligente**: um recurso de IA do Adobe Sensei, para detectar automaticamente o ponto focal em qualquer imagem ou vídeo, e recortar para mantê-lo. Ele captura o ponto de interesse desejado, independentemente do tamanho da tela e, portanto, elimina tarefas manuais tediosas e fornece imagens e vídeos de alta qualidade e carregamento rápido que ficam bem em qualquer dispositivo ou tela.

**Legendas de vídeo geradas por IA**: as legendas de vídeo geradas por IA no Adobe Dynamic Media usam inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. Esse recurso foi projetado para melhorar a acessibilidade e a experiência do usuário, fornecendo legendas precisas. As legendas são geradas a partir do áudio original, todas as faixas de áudio adicionais ou legendas extras são fornecidas na guia `Captions and Audio` da página de propriedades do vídeo. Com suporte para mais de 60 idiomas, as legendas podem ser revisadas e visualizadas antes da publicação do vídeo.
<table>
<td>
   <a href="/help/assets/dynamic-media/imaging-faq.md">
   <img alt="Imagem inteligente" src="./assets/smart-imaging.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/imaging-faq.md">
      <strong>Imagens inteligentes</strong>
      </a>
   </div>
   <p>
      <em>Otimize o formato e o tamanho de arquivo de uma imagem com base no recurso de navegador do usuário e na velocidade da rede.</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video">
   <img alt="Corte inteligente" src="./assets/smart-cropping.jpg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video">
      <strong>Recorte inteligente</strong>
      </a>
   </div>
   <p>
      <em>Use a IA para detectar o ponto focal automaticamente em qualquer imagem ou vídeo e recorte para mantê-lo</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/video.md">
   <img alt="Legendas de vídeo geradas por IA" src="./assets/videos-with-captions.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/video.md">
      <strong>Legendas de vídeo geradas por IA</strong>
      </a>
   </div>
   <p>
      <em>Use a inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. </em>
   </p>
</td>
</table>

>[!TAB Descoberta de ativos]

## Descoberta de ativos {#asset-discovery}

Depois de importar seus ativos para o AEM Assets, é um desafio encontrar os ativos certos rapidamente a partir de uma coleção tão grande.

O AEM Assets fornece recursos que ajudam você a encontrar rapidamente o ativo certo. Esses recursos incluem marcação gerada por IA (tags inteligentes), metadados personalizados e recursos de pesquisa aprimorados.

**Gerenciamento de metadados**: os metadados são o aspecto mais crítico ao iniciar a jornada de gerenciamento de ativos. O gerenciamento de metadados fica completamente fora do controle dos administradores depois que os ativos são distribuídos para os usuários. Metadados de ativos eficientes garantem uma pesquisa melhor, que é o destino final de qualquer ferramenta DAM.


**Metadata Forms**: o Assets as a Cloud Service fornece muitos campos de metadados padrão por padrão. Se você tiver necessidades adicionais de metadados e precisar de mais campos para adicionar metadados específicos de negócios. Os formulários de metadados permitem que as empresas adicionem campos de metadados personalizados à página Detalhes de um ativo. Os metadados específicos de negócios melhoram a governança e a descoberta de ativos. É possível criar formulários do zero ou redefinir a finalidade de um formulário existente.

<table>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="Visualização Gerenciar metadados do Assets" src="./assets/manage-metadata-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>Gerenciar metadados no modo de exibição Assets</strong>
      </a>
   </div>
   <p>
      <em>Saiba como gerenciar metadados e formulários de metadados usando o modo de exibição do Assets.</em>
   </p>
</td>


<td>
   <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298">
   <img alt="Práticas recomendadas de gerenciamento de metadados" src="./assets/metadata-best-practices.jpeg" />
   </a>
   <div>
      <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298">
      <strong>Práticas recomendadas de gerenciamento de metadados</strong>
      </a>
   </div>
   <p>
      <em>Saiba como gerenciar metadados antes e depois de migrar seus ativos para o AEM.</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-metadata.md">
   <img alt="Usar o Adobe Asset Link" src="./assets/metadata-management-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-metadata.md">
      <strong>Gerenciar metadados no modo de exibição de Administrador</strong>
      </a>
   </div>
   <p>
      <em>Saiba como gerenciar metadados e formulários de metadados usando o modo de exibição de Administrador.</em>
   </p>
</td>
</table>

**Tags inteligentes**: as Tags inteligentes usam a estrutura artificialmente inteligente do Adobe Sensei para treinar o algoritmo de reconhecimento de imagem de acordo com sua estrutura de tags e sua taxonomia comercial. Essa inteligência de conteúdo é usada para aplicar tags relevantes em um conjunto diferente de ativos. Por padrão, o AEM aplica tags inteligentes automaticamente a ativos carregados.

**Pesquisar ativos**: depois que os metadados corretos estiverem em vigor, o AEM Assets permitirá que você pesquise usando vários operadores, curingas, consultas avançadas e filtros personalizados.

**Pesquisa contextual**: a AEM Assets também fornece o recurso de Pesquisa contextual, que permite pesquisar ativos disponíveis no repositório definindo solicitações de texto. O Experience Manager Assets transforma automaticamente os prompts de texto em filtros de pesquisa e exibe os resultados da pesquisa. Você pode visualizar e modificar filtros automáticos usando o Painel Filtros para restringir mais os resultados da pesquisa.

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="Tags inteligentes no AEM Assets" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>Adicionar marcas inteligentes aos ativos</strong>
      </a>
   </div>
   <p>
      <em>Saiba como aplicar marcas inteligentes automaticamente a ativos carregados.</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md">
   <img alt="Pesquisar visualização do Assets" src="./assets/search-assets-view-landing.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md">
      <strong>Pesquisar ativos no modo de exibição Assets</strong>
      </a>
   </div>
   <p>
      <em>Saiba como usar a Pesquisa Contextual de maneira eficaz e outros recursos de pesquisa no modo de exibição do Assets.</em>
   </p>
</td>
<td>
   <a href="/help/assets/search-best-practices.md">
   <img alt="Pesquisar práticas recomendadas" src="./assets/search-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-best-practices.md">
      <strong>Pesquisar práticas recomendadas</strong>
      </a>
   </div>
   <p>
      <em>Saiba mais sobre vários cenários para ajudar os usuários do AEM a realizar pesquisas de nível básicas a avançadas.</em>
   </p>
</td>
</table>

>[!TAB Governança de ativos]

## Gerenciamento e governança de ativos {#asset-management-governance}

Depois de fazer upload dos ativos no AEM Assets e definir os metadados para melhorar a descoberta, você pode executar várias tarefas de gerenciamento de ativos digitais usando a interface amigável do Assets view.

**Tarefas de gerenciamento de ativos**: algumas das tarefas básicas incluem operações de pesquisa, download, movimentação, cópia, renomeação, exclusão, atualização e edição.

Você também pode manter versões de ativos, definir o status dos ativos e definir a expiração dos ativos.

**Minha Workspace**: a exibição do Assets também inclui um espaço de trabalho personalizável que fornece widgets. Esses widgets fornecem acesso conveniente a áreas principais da interface do usuário do Assets e às informações mais relevantes para você. Esta página serve como uma solução única para fornecer uma visão geral dos itens de trabalho e conceder acesso rápido aos principais fluxos de trabalho.

**Content Credentials**: outro recurso poderoso ao qual o AEM Assets oferece suporte é o Content Credentials. As marcas estão mais preocupadas do que nunca com a transparência de conteúdo, a divulgação de IA e a prevenção da adulteração de ativos. O Content Authenticity Initiative (CAI) na Adobe cria ferramentas em conformidade com o padrão técnico Coalition for Content Provenance and Authenticity (C2PA). O Content Credentials, um novo tipo de metadados criptografados e invioláveis, pode ajudar os visualizadores a entender a linhagem do conteúdo e garantir a integridade dos ativos da marca. Eles podem incluir uma grande variedade de dados de origem que oferecem ao insight o histórico de um ativo digital.

<table>
<td>
   <a href="/help/assets/manage-organize-assets-view.md">
   <img alt="Tarefas de gerenciamento de ativos" src="./assets/asset-management.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-organize-assets-view.md">
      <strong>Tarefas de gerenciamento de ativos</strong>
      </a>
   </div>
   <p>
      <em>Saiba como executar algumas tarefas básicas e avançadas de gerenciamento de ativos.</em>
   </p>
</td>


<td>
   <a href="/help/assets/my-workspace-assets-view.md">
   <img alt="Mt Workspace" src="./assets/my-workspace.jpeg" />
   </a>
   <div>
      <a href="/help/assets/my-workspace-assets-view.md">
      <strong>Meu Workspace</strong>
      </a>
   </div>
   <p>
      <em>Saiba como trabalhar com o My Workspace para acessar rapidamente as principais áreas da interface do usuário do Assets.</em>
   </p>
</td>
<td>
   <a href="/help/assets/content-credentials.md">
   <img alt="Content Credentials" src="./assets/content-credentials.jpeg" />
   </a>
   <div>
      <a href="/help/assets/content-credentials.md">
      <strong>Content Credentials</strong>
      </a>
   </div>
   <p>
      <em>Obtenha insights sobre o histórico de um ativo digital usando o Content Credentials.</em>
   </p>
</td>
</table>

**Coleções**: o AEM Assets também permite que você organize seus ativos em coleções. Uma coleção é um conjunto de ativos, pastas ou outras coleções na exibição do Adobe Experience Manager Assets. Use coleções para compartilhar ativos entre usuários. Diferente de pastas, uma coleção pode incluir ativos de locais diferentes. Você pode compartilhar várias coleções com um usuário. Cada coleção contém referências a ativos. A integridade referencial dos ativos é mantida entre as coleções.

**Notificações**: as notificações de exibição do Assets permitem monitorar as operações realizadas nos ativos, pastas ou coleções disponíveis no repositório. Você precisa selecionar e assinar o conteúdo sobre o qual deseja receber notificações. Você também pode configurar as categorias para as quais receberá notificações.

**Detectar ativos duplicados**: o AEM Assets também oferece suporte à detecção de ativos duplicados. Se um usuário do DAM carregar um ou mais ativos que já existem no repositório, o Experience Manager detectará a duplicação e notificará o usuário.



<table>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="Gerenciar coleções" src="./assets/manage-collections.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong>Gerenciar Coleções</strong>
      </a>
   </div>
   <p>
      <em>Saiba como organizar seus ativos em coleções para um compartilhamento eficiente de ativos.</em>
   </p>
</td>


<td>
   <a href="/help/assets/manage-notifications-assets-view.md">
   <img alt="Definir notificações" src="./assets/manage-notifications.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong>Definir Notificações</strong>
      </a>
   </div>
   <p>
      <em>Saiba como definir notificações para monitorar as operações realizadas em ativos, pastas ou coleções.</em>
   </p>
</td>
<td>
   <a href="/help/assets/detect-duplicate-assets.md">
   <img alt="Detectar ativos duplicados" src="./assets/duplicate-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/detect-duplicate-assets.md">
      <strong>Detectar ativos duplicados</strong>
      </a>
   </div>
   <p>
      <em>Detectar ativos duplicados carregados no AEM Assets e notificar os usuários.</em>
   </p>
</td>
</table>

>[!TAB Integrações]

## Integração com aplicativos Adobe e não-Adobe {#integration-adobe-non-adode-apps}

O AEM Assets pode se integrar perfeitamente a vários aplicativos Adobe e não Adobe. Esta é uma exibição resumida das integrações disponíveis:

+++**Integração com aplicativos Adobe e não-Adobe**

* **Dynamic Media com recursos OpenAPI**: [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) oferece um conjunto abrangente de APIs de [pesquisa](/help/assets/search-assets-api.md) e [entrega](/help/assets/deliver-assets-apis.md). Ele permite que os desenvolvedores integrem facilmente o delivery de ativos aos seus aplicativos. Os aplicativos incluem o Adobe e aplicativos de terceiros. Ele fornece uma interface de usuário do seletor de ativos de micro front-end para pesquisar e selecionar ativos aprovados. O seletor pode ser facilmente integrado a qualquer aplicativo com base em estruturas JavaScript, como React JS, Angular JS e Vanilla JS.

* **Seletor de ativos de micro front-end**: o Seletor de ativos de micro front-end fornece uma interface que se integra ao repositório do Experience Manager Assets para que você possa navegar ou pesquisar ativos digitais disponíveis no repositório. Em seguida, você pode usá-los na experiência de criação do aplicativo.
É possível integrar o Seletor de ativos a um aplicativo da Adobe ou que não seja da Adobe.

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="Visão geral do Dynamic Media com recursos OpenAPI" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>Visão geral dos recursos do Dynamic Media com OpenAPI</strong>
      </a>
   </div>
   <p>
      <em>Saiba mais sobre os principais benefícios e como ativá-los. </em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Restringir o acesso a ativos no Experience Manager" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Restringir o acesso aos ativos no Experience Manager</strong>
      </a>
   </div>
   <p>
      <em> Configure as funções para restringir o acesso aos ativos aprovados.</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="Seletor de ativos" src="./assets/integration-asset-selector.jpeg" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>Seletor de ativos de micro front-end</strong>
      </a>
   </div>
   <p>
      <em>Saiba como integrar o Seletor de Ativos de Microfront-end a um aplicativo da Adobe ou que não seja da Adobe.</em>
   </p>
</td>
</table>

+++

+++**Integração nativa com aplicativos da Adobe**

* **Integração com o Adobe Workfront**: [!DNL Adobe Workfront] é um aplicativo de gerenciamento de trabalho que ajuda você a gerenciar todo o ciclo de vida do trabalho em um único local. A integração entre o [!DNL Workfront] e o [!DNL Adobe Experience Manager Assets] permite que as organizações melhorem a velocidade do conteúdo e o prazo para comercialização, conectando intrinsecamente o gerenciamento de trabalho e de ativos digitais. No contexto do gerenciamento de trabalho no Workfront, os usuários têm acesso aos documentos e imagens necessários.

  Ofertas do Adobe para [integrar [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] nativamente](https://experienceleague.adobe.com/en/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations).

* **Integração com o Figma**: o AEM Assets integra-se nativamente com o Figma, o que permite que os designers acessem os ativos armazenados diretamente no AEM Assets na Interface do Usuário do Figma. Você pode colocar conteúdo gerenciado no AEM Assets na tela do Figma e depois salvar conteúdo novo ou editado no repositório do AEM Assets. Para acessar o AEM Assets Connector disponível na página da Comunidade Figma, clique [aqui](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector).

* **Integração nativa com o Adobe Express**: o AEM Assets integra-se nativamente com o Adobe Express, o que permite acessar os ativos armazenados diretamente no AEM Assets na interface do usuário do Adobe Express. Você pode colocar o conteúdo gerenciado no AEM Assets na tela Express e depois salvar o conteúdo novo ou editado em um repositório do AEM Assets.

* **Conectar o AEM Assets ao Creative Cloud**: o Experience Manager Assets pode se conectar a um direito do Creative Cloud provisionado em uma organização IMS diferente. Essa capacidade permite usar as integrações mais recentes do Creative Cloud no AEM Assets, incluindo o Express e o Creative Cloud Libraries. Se seus produtos da Creative Cloud e o AEM Assets forem provisionados para organizações IMS separadas, você poderá se conectar a uma organização diferente da Creative Cloud para executar fluxos de trabalho integrados entre as duas soluções.

<table>
<td>
   <a href="/help/assets/workfront-integrations.md">
   <img alt="Integração com o Adobe Workfront" src="./assets/integration-adobe-workfront.jpeg" />
   </a>
   <div>
      <a href="/help/assets/workfront-integrations.md">
      <strong>Integração com o Adobe Workfront</strong>
      </a>
   </div>
   <p>
      <em>Integre com o Adobe Workfront para gerenciar todo o ciclo de vida do trabalho em um único local.</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="Integração com o Figma" src="./assets/integration-commerce.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong>Integração com o Figma</strong>
      </a>
   </div>
   <p>
      <em>Acessar os ativos armazenados no AEM Assets na Interface do Usuário do Figma</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="Integração nativa com o Adobe Express" src="./assets/integration-adobe-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>Integração nativa com o Adobe Express</strong>
      </a>
   </div>
   <p>
      <em>Coloque os ativos disponíveis no AEM Assets na tela do Express e salve os ativos atualizados no AEM. </em>
   </p>
</td>


</table>


* **Integração com o Adobe Journey Optimizer**: combine fluxos de trabalho de marketing e criação usando o Adobe Experience Manager Assets. Integrado nativamente à Adobe Journey Optimizer, acesse o Assets as a Cloud Service para armazenar, gerenciar, descobrir e distribuir ativos digitais. Ele fornece um repositório único e centralizado de ativos que você pode usar para preencher suas mensagens.

* **Integração com o Commerce**: a Integração do Adobe Experience Manager (AEM) Assets para Commerce combina os recursos avançados do AEM as a Digital Asset Management (DAM) system com o Adobe Commerce para melhorar as experiências de comércio eletrônico. Esses recursos são fornecidos pela conexão de projetos do Commerce ao eficiente ambiente de gerenciamento de ativos da AEM, para fornecer uma maneira contínua, escalável e eficiente de gerenciar e fornecer ativos em vitrines comerciais.
* **Integração do AEM Assets com fluxos de Criação Baseada em Documentos para o Edge Delivery Services**: quando o [!DNL AEM Assets] se integra às suas ferramentas de Criação Baseada em Documentos, como o [!DNL Microsoft Word] ou o [!DNL Google Docs], ele fornece um Seletor de Ativos na sua ferramenta de criação. Use este Seletor de ativos para acessar [!DNL AEM Assets] e inserir ativos aprovados em seu conteúdo.
Se você já tiver um site do [!DNL Edge Delivery Services], consulte a documentação do [[!DNL AEM Assets] plugin](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) para saber como integrar o [!DNL AEM Assets] ao seu projeto existente do [!DNL AEM].

* **Integrando [!DNL AEM Assets] com fluxos de criação baseados em [!DNL Universal Editor] para[!DNL Edge Delivery Services]**: configure o [!DNL Universal Editor] para integrar com [!DNL AEM Assets]. Essa integração permite que você use o [!DNL Dynamic Media with OpenAPI capabilities] para entregar ativos.

   * Consulte [Configuração no [!DNL Edge Delivery] Site](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) para saber como adicionar uma função de seletor de ativos personalizada no [!DNL Universal Editor]. O seletor de ativos personalizados permite inserir ativos no conteúdo do [!DNL Universal Editor] diretamente.
   * Consulte a [Visão geral da extensão](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para saber como acessar [!DNL AEM Assets] e inserir os ativos durante a criação em [!DNL Universal Editor].

<table>
<td>
   <a href="https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/combine/assets">
   <img alt="Integração com o Adobe Journey Optimizer" src="./assets/integration-figma.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/combine/assets">
      <strong>Integração com o Adobe Journey Optimizer</strong>
      </a>
   </div>
   <p>
      <em>Reúna os fluxos de trabalho de marketing e criação usando a integração com o AJO</em>
   </p>
</td>
<td>
   <a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/overview">
   <img alt="Integração com o Commerce" src="./assets/integration-ajo.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/overview">
      <strong>Integração com o Commerce</strong>
      </a>
   </div>
   <p>
      <em>Integre o AEM Assets com o Commerce para aprimorar as experiências de comércio eletrônico.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
   <img alt="Integrar o AEM Assets com o EDS" src="./assets/integrate-ue-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
      <strong>Integrar o AEM Assets com o EDS</strong>
      </a>
   </div>
   <p>
      <em>Integre o AEM Assets a fluxos de criação baseados em documento e no Editor Universal.</em>
   </p>
</td>
</table>

+++

>[!TAB Ativação de ativos]

## Ativação de ativo {#asset-activation}

Libere todo o potencial de seus ativos digitais com o AEM Assets usando o Content Hub para Dynamic Media — incluindo recursos avançados de OpenAPI. A AEM Assets oferece um conjunto abrangente de soluções projetadas para simplificar a transformação de ativos e otimizar a entrega em vários canais.

+++**Centro de conteúdo**

O Content Hub está disponível como parte do Experience Manager Assets as a Cloud Service para democratizar o acesso a conteúdo sobre a marca para organizações e seus parceiros de negócios. Ele se concentra na distribuição de ativos para ativação em escala e criação de variantes de conteúdo na marca para melhorar a agilidade de marketing.

A Content Hub oferece os seguintes benefícios principais:

* **Localize e compartilhe todos os ativos aprovados pela marca disponíveis em um portal intuitivo**: o AEM Assets serve como uma única fonte da verdade e todos os ativos aprovados são automaticamente disponibilizados no Content Hub em uma hierarquia simples para melhorar a experiência de pesquisa.

* **Interface de usuário configurável**: as propriedades mais comuns no Content Hub, como filtros de pesquisa, campos disponíveis ao adicionar ou importar ativos, propriedades de ativos, conteúdo de banner para identidade visual, são configuráveis e um administrador pode configurar facilmente a interface de usuário do Content Hub com base em seus requisitos.

* **Capacite os usuários não criativos a editar e remixar conteúdo enquanto permanecem na marca**: o Content Hub permite criar novo conteúdo com o Adobe Express (se você tiver direitos para o Adobe Express). Você pode editar o conteúdo existente com ferramentas fáceis de usar, produzir variações na marca com modelos e elementos da marca e criar novo conteúdo com os recursos mais recentes da GenAI da Adobe Firefly.

* **Obter insights sobre como o conteúdo é usado entre equipes**: [!DNL Content Hub] fornece insights valiosos sobre ativos, abordando um desafio comum que as partes interessadas de marketing geralmente enfrentam: as estatísticas de uso de ativos usadas em campanhas de marketing, canais e diferentes regiões. Ao obter uma compreensão clara do desempenho e da popularidade dos ativos, ele fornece insights acionáveis essenciais para melhorar a experiência do usuário.

<table>
<td>
   <a href="/help/assets/product-overview.md">
   <img alt="Visão geral do Content Hub" src="./assets/content-hub-overview.jpeg" />
   </a>
   <div>
      <a href="/help/assets/product-overview.md">
      <strong>Visão geral do Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Saiba mais sobre o Content Hub, seus principais benefícios e como acessá-lo. </em>
   </p>
</td>


<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="Configurar a interface do usuário do Content Hub" src="./assets/content-hub-configuration.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>Configurar a Interface do Usuário do Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Saiba como configurar as opções disponíveis na interface do usuário do Content Hub.</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="Editar usando o Adobe Express" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>Editar usando o Adobe Express</strong>
      </a>
   </div>
   <p>
      <em>Saiba como editar imagens no Content Hub usando o Adobe Express.</em>
   </p>
</td>
</table>

+++

+++**Dynamic Media**

O Dynamic Media ajuda você a fornecer ativos avançados de merchandising visual e marketing sob demanda. Ele também ajuda a criar e fornecer experiências de visualização interativa, incluindo zoom, rotação de 360 graus e vídeo. Seus ativos são dimensionados dinamicamente para consumo em sites da Web, móveis e sociais. Usando um conjunto de ativos de origem primária, como imagens, vídeo e 3D, o Dynamic Media gera e entrega várias variações desse conteúdo avançado, em tempo real, por meio de sua CDN (Content Delivery Network, rede de entrega de conteúdo) global, escalável e otimizada para o desempenho.

O Dynamic Media oferece os seguintes recursos principais:

* **Smart Imaging**: o Smart Imaging oferece um desempenho ainda melhor de entrega de ativos de imagem, otimizando automaticamente o formato de imagem e o tamanho do arquivo com base na capacidade do navegador do cliente. Ele funciona com suas predefinições de imagem existentes e usa inteligência na entrega. Essa inteligência reduz ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador e da conexão de rede.

* **Conjuntos de vídeos adaptados**: um Conjunto de vídeos adaptados agrupa versões do mesmo vídeo codificadas em taxas de bits e formatos diferentes. Você começa com seu vídeo original, o qual você carrega no sistema. O Dynamic Media dimensiona ou transcodifica automaticamente esse vídeo em vários vídeos. Em seguida, no momento do delivery, ele determina de forma inteligente qual tela de vídeo, qual qualidade e qual formato usar, além de fornecê-la ao telefone, tablet ou computador desktop.

* **Recorte inteligente**: um recurso de IA do Adobe Sensei, para detectar automaticamente o ponto focal em qualquer imagem ou vídeo, e recortar para mantê-lo. Ele captura o ponto de interesse desejado, independentemente do tamanho da tela e, portanto, elimina tarefas manuais tediosas e fornece imagens e vídeos de alta qualidade e carregamento rápido que ficam bem em qualquer dispositivo ou tela.

* **Modelos do Dynamic Media**: crie modelos personalizáveis em tempo real para seus banners e folhetos usando os modelos do Dynamic Media, um editor de modelos do WYSIWYG. Publique seu modelo do Dynamic Media e use-o nos aplicativos downstream. Um modelo do Dynamic Media inclui camadas de imagem e texto. Adicione parâmetros às camadas de imagem e texto do modelo e use URLs do Dynamic Media para reposicionar e redimensionar a camada e atualizar seu conteúdo em tempo real.

* **Múltiplos áudio e legenda**: adicione várias legendas e faixas de áudio a um vídeo principal. Esse recurso significa que os vídeos estão acessíveis a um público-alvo global. Você pode personalizar um único vídeo principal publicado para um público-alvo global em vários idiomas e seguir as diretrizes de acessibilidade para diferentes regiões geográficas. Os autores também podem gerenciar as legendas e faixas de áudio em uma única guia na interface do usuário do.

* **Suporte para Dynamic Adaptive Streaming over HTTP (DASH)**: o Dynamic Media oferece suporte para o streaming adaptável na entrega de vídeo do Dynamic Media (com CMAF habilitado), o que garante uma melhor experiência de exibição de vídeos por parte do usuário. DASH é o protocolo padrão internacional para transmissão de vídeo adaptável e é amplamente adotado no setor.

* **Legendas de vídeo geradas por IA**: as legendas de vídeo geradas por IA no Adobe Dynamic Media usam inteligência artificial para gerar legendas automaticamente para conteúdo de vídeo. Com suporte para mais de 60 idiomas, as legendas podem ser revisadas e visualizadas antes da publicação do vídeo.

Para obter informações sobre ofertas do Dynamic Media disponíveis, consulte [Dynamic Media Prime e Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).



<table>
<td>
   <a href="/help/assets/dynamic-media/dynamic-media.md">
   <img alt="Trabalhar com o Dynamic Media" src="./assets/work-with-dynamic-media.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dynamic-media.md">
      <strong>Trabalhar com o Dynamic Media</strong>
      </a>
   </div>
   <p>
      <em>Saiba como fornecer ativos para consumo em sites da Web, móveis e sociais. </em>
   </p>
</td>


<td>
   <a href="/help/assets/dynamic-media/dm-journey-part1.md">
   <img alt="Jornada do Dynamic Media" src="./assets/dm-journey.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-journey-part1.md">
      <strong>Jornada do Dynamic Media</strong>
      </a>
   </div>
   <p>
      <em>Saiba como o Dynamic Media agrega valor ao seu trabalho.</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/dm-best-practices.md">
   <img alt="Conectar o AEM Assets à Creative Cloud" src="./assets/dm-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-best-practices.md">
      <strong>Práticas recomendadas do Dynamic Media</strong>
      </a>
   </div>
   <p>
      <em>Práticas recomendadas para trabalhar com imagens, vídeos e visualizadores.</em>
   </p>
</td>
</table>

+++

+++**Dynamic Media com recursos da OpenAPI**

No mundo digital veloz de hoje, explorar todo o potencial dos ativos digitais da sua marca é crucial para se manter à frente da concorrência. Uma solução holística de Gerenciamento de Assets digital (DAM) facilita a governança de ativos, promove a consistência da marca e acelera a entrega de conteúdo, garantindo a integridade da marca e experiências excepcionais para o cliente.

O Dynamic Media com recursos de OpenAPI coloca o DAM no centro de um ecossistema de conteúdo supply chain ágil e eficiente para garantir a governança e a entrega de ativos.

O Dynamic Media com recursos OpenAPI oferece os seguintes benefícios principais:

* **Integrações perfeitas**: o Dynamic Media com recursos OpenAPI oferece um conjunto abrangente de APIs de pesquisa e entrega. Ele permite que seus desenvolvedores [integrem facilmente a entrega de ativos a seus aplicativos](/help/assets/integrate-dynamic-media-open-apis.md). Os aplicativos incluem o Adobe e aplicativos de terceiros. Ele fornece uma [interface de usuário do seletor de ativos de front-end de micro](/help/assets/overview-asset-selector.md) para pesquisar e selecionar ativos aprovados. O seletor pode ser facilmente integrado a qualquer aplicativo com base em estruturas JavaScript, como React JS, Angular JS e Vanilla JS.

* **Gerenciamento centralizado de ativos digitais**: o DAM é a única fonte da verdade para todos os ativos digitais. Seus ativos digitais são gerenciados centralmente no AEM Assets e entregues a aplicativos de consumo por referência usando URLs de entrega, sem copiar binários de ativos.

* **Atualizações em tempo real**: quaisquer alterações feitas em ativos aprovados no DAM, incluindo atualizações de versão e modificações de metadados, são refletidas automaticamente nas URLs de entrega. Com um valor curto de TTL (Time-to-Live) de 10 minutos configurado para o Dynamic Media com recursos OpenAPI por meio do CDN, as atualizações ficam visíveis em todas as interfaces de criação e publicação em menos de 10 minutos.

* **Consistência da marca**: somente [ativos aprovados pela marca](/help/assets/approve-assets.md) são expostos aos aplicativos downstream. [Os gerentes de marca e profissionais de marketing mantêm controle rigoroso sobre os ativos da marca](/help/assets/restrict-assets-delivery.md). Somente a versão aprovada e mais recente do ativo está disponível para uso, garantindo a consistência da marca em todos os canais e aplicativos.

* **Entrega otimizada para a Web**: os ativos digitais são entregues em formatos otimizados para a Web para aprimorar os Componentes principais da Web das suas experiências digitais. Essa otimização inclui suporte para representações WebP para imagens, transmissão adaptável por meio dos protocolos HLS ou DASH para vídeos e representações originais para documentos.

* **Transformação de ativo dinâmico**: o sistema permite a transformação de imagem instantânea usando parâmetros de URL conhecidos como modificadores de imagem. [Por exemplo, largura, altura, girar, virar, qualidade, recorte, formato e recorte inteligente](/help/assets/deliver-assets-apis.md). As representações transformadas são geradas dinamicamente e entregues perfeitamente por meio da CDN.

* **Entrega segura de ativos**: o Dynamic Media com recursos OpenAPI fornece um mecanismo para controlar o acesso aos seus ativos digitais. Você pode especificar funções ou grupos de usuários como metadados para ativos que serão protegidos e definir um período predefinido durante o qual [somente usuários autorizados podem acessar esses ativos](/help/assets/restrict-assets-delivery.md). Os URLs de entrega dos ativos protegidos não são resolvidos para usuários não autorizados durante o período restrito.

Para obter informações sobre ofertas do Dynamic Media disponíveis, consulte [Dynamic Media Prime e Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="Visão geral do Dynamic Media com recursos OpenAPI" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>Visão geral dos recursos do Dynamic Media com OpenAPI</strong>
      </a>
   </div>
   <p>
      <em>Saiba mais sobre os principais benefícios e como ativá-los. </em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Restringir o acesso a ativos no Experience Manager" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Restringir o acesso aos ativos no Experience Manager</strong>
      </a>
   </div>
   <p>
      <em> Configure as funções para restringir o acesso aos ativos aprovados.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="Integrar o AEM Assets remoto com o AEM Sites" src="./assets/integration-aem-sites.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong>Integrar o AEM Assets remoto com o AEM Sites</strong>
      </a>
   </div>
   <p>
      <em>Integrar o AEM Assets remoto ao ambiente do AEM Sites. </em>
   </p>
</td>
</table>

+++

>[!TAB Insights]

## Insights do ativo {#asset-insights}

Os relatórios de ativos fornecem aos administradores visibilidade sobre as atividades do ambiente de exibição do Adobe Experience Manager Assets. Esses dados fornecem informações úteis sobre como os usuários interagem com o conteúdo e o produto. Todos os usuários podem acessar o painel Insights e aqueles que estão atribuídos ao perfil de produto do administrador podem criar relatórios definidos pelo usuário.

Você pode gerar vários tipos de relatórios, como Upload, Download e Entrega do Dynamic Media.

* **Insights no modo de exibição do Assets**: o modo de exibição do Assets permite que você visualize dados em tempo real do seu ambiente de exibição do Assets com o painel Insights. Você pode visualizar métricas de evento em tempo real dos últimos 30 dias ou dos últimos 12 meses. Os eventos incluem Downloads, Uploads, Uso de armazenamento, Pesquisas principais, Contagem de ativos por tamanho e Contagem de ativos por tipo de ativo.

* **Integração do Adobe Analytics no modo de exibição de Administrador**: a funcionalidade do Assets Insights permite rastrear as classificações de usuário e as estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas da Adobe. Ele ajuda a fornecer insights sobre o desempenho e a popularidade das imagens. O Assets Insights captura detalhes da atividade do usuário, como o número de vezes que uma imagem é classificada, clicada e impressões (número de vezes que uma imagem é carregada no site). Ele atribui pontuações a imagens com base nessas estatísticas. Você pode usar as pontuações e as estatísticas de desempenho para selecionar imagens populares para inclusão em catálogos, campanhas de marketing e assim por diante. Você pode até mesmo formular políticas de arquivamento e renovação de licença com base nessas estatísticas. Para permitir que o Assets Insights exiba estatísticas de uso de ativos, primeiro configure o recurso para buscar dados de relatórios do Adobe Analytics.

* **Content Hub Insights**: o Content Hub fornece insights valiosos sobre ativos, abordando um desafio comum que as partes interessadas de marketing geralmente enfrentam: as estatísticas de uso de ativos usadas em campanhas de marketing, canais e diferentes regiões. Ao obter uma compreensão clara do desempenho e da popularidade dos ativos, ele fornece insights acionáveis essenciais para melhorar a experiência do usuário.

<table>
<td>
   <a href="/help/assets/manage-reports-assets-view.md">
   <img alt="Gerenciar relatórios na visualização do Assets" src="./assets/assets-insights-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-reports-assets-view.md">
      <strong>Gerenciar relatórios no modo de exibição do Assets</strong>
      </a>
   </div>
   <p>
      <em>Derive insights sobre as principais métricas de sucesso usando a exibição do Assets. </em>
   </p>
</td>


<td>
   <a href="/help/assets/asset-reports.md">
   <img alt="Gerenciar relatórios no modo de exibição de Administração" src="./assets/assets-insights-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/asset-reports.md">
      <strong>Gerenciar relatórios no modo de exibição de Administrador</strong>
      </a>
   </div>
   <p>
      <em>Saiba como gerenciar relatórios integrados do Adobe Analytics no modo de exibição de Administração.</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="Insights do Assets no Content Hub" src="./assets/asset-insights-content-hub.jpeg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>Insights do Assets no Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Saiba como exibir insights do Assets no Content Hub.</em>
   </p>
</td>
</table>

>[!ENDTABS]

## Experiências personalizadas disponíveis para o Gerenciamento de ativos digitais {#persona-based-experiences}

A Adobe oferece uma solução robusta de gerenciamento de ativos digitais (DAM) para você aproveitar ao máximo seus ativos digitais. O Adobe Experience Manager Assets tem duas experiências separadas que usam o mesmo repositório do Cloud Services:

* **Visualização de admin**: a interface existente do Assets as a Cloud Service. Use a exibição de Administrador para todos os recursos avançados de Gerenciamento de ativos digitais, incluindo integrações, fluxos de trabalho, automação de conteúdo, publicação e muito mais.

* **Visualização de ativos**: a experiência leve de gerenciamento de ativos da Adobe para armazenar, gerenciar, descobrir e usar ativos digitais. Interface do usuário simplificada com recursos essenciais de gerenciamento de ativos digitais. Desenvolvida para usuários leves de DAM, com foco no upload, gerenciamento de metadados, pesquisa, download e compartilhamento.

![add-tags](assets/newui-overview.svg)

Usuários que possuem acesso à visualização de admin também podem acessar a visualização de ativos. O Assets View fornece uma interface simplificada que facilita o gerenciamento, a descoberta e a distribuição de ativos digitais. Um amplo conjunto de usuários de diferentes funções, incluindo equipes de criação, marketing e linha de negócios, pode colaborar em ativos e acessar os ativos corretos e aprovados quando e onde for necessário. Muitos usuários casuais de DAM preferem a visualização de ativos, visto que ela contém apenas um subconjunto de recursos. A experiência é direcionada para consumidores de ativos criativos do tipo somente leitura e que não exigem muito do DAM.

Bibliotecários, desenvolvedores e superusuários do DAM podem continuar a usar a visualização de admin ou alternar entre as interfaces, conforme necessário. Você pode selecionar a experiência que funciona melhor para sua função.

Para obter informações sobre como acessar o modo de exibição Assets e algumas das simplificações que ele oferece no modo de exibição Admin, consulte [Introdução ao modo de exibição Assets](/help/assets/assets-view-introduction.md).

## Assistente de IA no AEM

Para clientes que possuem [critérios de pré-requisito concluídos](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access), o Assistente de IA do AEM está disponível para usuários de suas organizações. Consulte [Assistente de IA no AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).
