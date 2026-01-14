---
title: Práticas recomendadas do Dynamic Media
description: Saiba mais sobre as práticas recomendadas do Dynamic Media para trabalhar com imagens e vídeo e as práticas recomendadas para visualizadores do Dynamic Media.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Adaptive Streaming, Best Practices, Smart Imaging, Image Profiles, Rulesets, Viewers, Smart Crop, SEO Optimization, Publishing, Video, Renditions, Asset Management
role: User, Admin
mini-toc-levels: 4
exl-id: 39e491bb-367d-4c72-b4ca-aab38d513ac5
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '4048'
ht-degree: 0%

---

# Práticas recomendadas do Dynamic Media{#about-dm-best-practices}

<!--**Organizations today must connect with their customers through an ever-growing array of channels and devices.** The customer experience spans physical stores, websites, mobile apps, social media, email, and e-commerce platforms. This diversity requires organizations to create many more versions of each piece of content. Personalization adds complexity by increasing the number of variations needed for each item. Despite budget constraints for content creation, there's still a need to produce more campaigns in the same timeframe, on a global scale. AEM Dynamic Media offers a comprehensive set of tools to meet these challenges, providing consistent, personalized, high-performance, and optimized brand experiences across all channels and devices. 

Key Features of AEM Dynamic Media:

* **Single File Approach:** Save on storage costs by storing just one master file. AEM Dynamic Media generates all size variations and visual effects on-demand, at the time of delivery, eliminating workflow complexity and last-minute creative changes.
* **Global Reach:** With Smart Imaging, images are automatically optimized during delivery, significantly reducing file size and page weight without sacrificing visual quality. This optimization is tailored for network bandwidth and device pixel ratio.
* **AI-Powered Efficiency:** Smart Crop uses AI to automate the cropping of images and videos, focusing on points of interest. This feature saves countless hours of manual editing and is designed for large-scale enterprise production.
* **Video Made Simple:** Upload a master video file and AEM Dynamic Media will adaptively stream it in multiple languages and with descriptive audio, ensuring a broad reach.
* **Customizable Experience Viewer:** Select, customize, and brand the experience viewers for images and videos with ease. These viewers can be seamlessly integrated into any digital experience.
* **Support for Emerging Formats:** AEM Dynamic Media is also your solution for delivering immersive 3D and panoramic experiences.

In the accompanying guide, you'll find a comprehensive list of best practices for maximizing the benefits of AEM Dynamic Media. As you embark on your Dynamic Media journey, make sure to consult these expert recommendations and resources.

Stage Business Problem Best Practice Recommendation: This section will outline specific business challenges and provide targeted best practices and recommendations to address them effectively. -->

{{see-also-dm}}

As organizações enfrentam uma explosão de canais e dispositivos para se envolver com os usuários. A jornada do cliente abrange lojas físicas, Web, dispositivos móveis, mídias sociais, emails e comércio. Para atender a essa demanda, o Dynamic Media no Adobe Experience Manager (AEM) oferece uma solução abrangente. Ele otimiza a entrega de ativos, lida com a personalização e garante experiências consistentes, com desempenho e alinhadas à marca em canais e dispositivos.

Alguns dos principais princípios do Dynamic Media incluem:

* **Abordagem de arquivo único:** Com o Dynamic Media, você armazena um arquivo de origem principal, e todas as variações de tamanho e efeitos visuais são dinamicamente criados e otimizados no momento da entrega. Essa abordagem economiza custos de armazenamento e elimina a complexidade do fluxo de trabalho.
* **Verdadeiramente global:** a Smart Imaging, aplicada durante a entrega do conteúdo, reduz significativamente o tamanho da imagem e o peso da página sem comprometer a qualidade visual. Ele é otimizado para largura de banda de rede e proporções de pixel de dispositivo.
* **IA ativada:** o Recorte inteligente, um recurso orientado por IA, automatiza o recorte de pontos de interesse de imagem e vídeo. Ele elimina o esforço manual e pode ser dimensionado com eficiência para uso corporativo.
* **Vídeo fácil:** carregue vídeos de origem primária no Dynamic Media e transmita-os de forma adaptável em vários idiomas com áudio descritivo.
* **Biblioteca do visualizador de experiência**: personalize visualizadores de experiência da marca e imagens e vídeos. Esses visualizadores se integram perfeitamente às suas experiências digitais.
* **Suporte a formatos emergentes:** O Dynamic Media permite a entrega de experiências panorâmicas e 3D.

Ao explorar a [Jornada do Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-journey/dm-journey-part1), revisar a lista consolidada de práticas recomendadas abaixo pode ajudá-lo a aproveitar ao máximo seus recursos. Adapte essas práticas recomendadas do Dynamic Media aos requisitos específicos do contexto e do projeto para que você possa otimizar suas experiências em canais e dispositivos.

<!-- In Dynamic Media on AEM, there are sets of methods, techniques, and guidelines that can help you maximize the potential of your rich media content. These best practices can lead to optimal results and increase efficiency in your use of Dynamic Media. They represent the most efficient and effective courses of action in a particular situation. They also unlock high value for your audience and deliver high-quality, engaging content. -->

>[!IMPORTANT]
>
>As práticas recomendadas do Dynamic Media neste artigo podem evoluir com o tempo, à medida que novas tecnologias do Dynamic Media surgem. As informações abaixo são atuais para a versão mais recente do Dynamic Media.


## Assimilar ativos no Dynamic Media

**Business case:** *Gerencie com eficiência grandes volumes de ativos e garanta que somente conteúdo relevante e aprovado seja entregue aos usuários finais.*

Simplifique o gerenciamento de grandes números de ativos com eficiência. Certifique-se de que somente o conteúdo autorizado e apropriado chegue aos usuários finais usando os recursos **Sincronização Seletiva** e **Publicação Seletiva** do Dynamic Media.

* **Sincronização seletiva:**
Um recurso pró-ativo que permite escolher quais ativos sincronizar com o Dynamic Media. Por exemplo, você pode decidir sincronizar somente as pastas que contêm ativos que receberam aprovação final. Esse fluxo de trabalho ajuda você a manter o controle sobre quais ativos estão sendo preparados para entrega aos clientes.

* **Publicação seletiva:**
Após sincronizar os ativos, a Publicação seletiva oferece controle sobre quais ativos ficam visíveis para os clientes. Essa capacidade significa que você pode controlar quais ativos aprovados são realmente entregues por meio de seus canais, garantindo que seus clientes vejam apenas o melhor e mais relevante conteúdo.

Essas duas práticas recomendadas o ajudarão a obter melhor controle, governança e produtividade do seu conteúdo de mídia avançada.

Quer saber mais? Vá para [Configurar publicação seletiva no nível da pasta no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).


## Visualizadores do Dynamic Media

As práticas recomendadas do Visualizador do Dynamic Media são diretrizes essenciais projetadas para otimizar o desempenho, a funcionalidade e a experiência do usuário dos ativos do Dynamic Media no AEM. Essas práticas garantem que os ativos sejam sincronizados, publicados e configurados corretamente para usar todos os recursos do Dynamic Media.

Seguindo essas práticas recomendadas, você pode obter integração perfeita, gerenciamento eficiente de ativos e interações aprimoradas do visualizador. Sincronizar ativos, usar o recorte inteligente e seguir as diretrizes de inclusão de arquivos do JavaScript são práticas importantes. Essas recomendações ajudam a manter a integridade e a confiabilidade da entrega de mídia em várias plataformas e dispositivos.

* **Sincronizar Assets do Visualizador:**
Verifique se todos os ativos do visualizador estão sincronizados com o Dynamic Media antes de usar o reprodutor.

   * Acesse a página do gerenciador de exemplo em `/libs/dam/gui/content/s7dam/samplemanager/samplemanager`. Essa página permite ressincronizar os ativos de um visualizador, incluindo ícones prontos para uso, arquivos CSS e predefinições.
   * Se encontrar problemas no visualizador, vá para o artigo [Solução de problemas do Dynamic Media Viewers](/help/assets/dynamic-media/troubleshoot-dm.md#viewers).

* **Publicar Assets:**
Verifique se os ativos foram publicados antes de visualizá-los nos visualizadores de entrega.
* **Vídeos de Reprodução Automática sem áudio:**
Para a funcionalidade de reprodução automática em vídeos, use configurações de vídeo sem áudio porque os navegadores restringem a reprodução de vídeos com volume.
* **Corte inteligente:**
Use o componente de Imagem v3 para recorte inteligente para aprimorar a apresentação do ativo de imagem.
* **Inclusão de arquivo do JavaScript:**
Inclua somente o arquivo JavaScript do visualizador primário na página. Evite fazer referência a arquivos JavaScript adicionais que a lógica de tempo de execução do visualizador pode baixar. Especificamente, não vincule diretamente à biblioteca `Utils.js` do HTML5 SDK a partir do caminho de contexto `/s7viewers` (conhecido como inclusão consolidada do SDK). A lógica do visualizador gerencia o local de `Utils.js` ou bibliotecas de visualizadores de tempo de execução semelhantes, que podem mudar entre versões. A Adobe não retém versões anteriores do visualizador secundário do no servidor, portanto, referenciá-las diretamente pode quebrar a funcionalidade do visualizador em atualizações futuras.
* **Diretrizes de Inserção:**
Use a documentação para incorporar diretrizes específicas a cada visualizador.
Quer saber mais? Ir para [Visualizadores do AEM Assets](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers).
* **Tutorial e exemplos do SDK:**
Revise o [Tutorial do Visualizador do SDK](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/c-tutorial) e os [exemplos de aplicativos do HTML5 SDK](https://s7d9.scene7.com/s7sdk/2024.5/docs/jsdoc/index.html) para obter um entendimento completo das APIs de componentes do SDK.


## Preparar ativos para entrega

### Organize seus ativos

**Business case:** *Organize ativos com eficiência para simplificar fluxos de trabalho.*

Para uma organização de ativos eficiente que simplifica os fluxos de trabalho, use uma ou mais das seguintes práticas recomendadas:

* **Organizar ativos em pastas:**
A organização de ativos envolve categorizá-los em pastas, de modo semelhante à organização de arquivos em um computador. Nomeação adequada, estruturação de subpastas e gerenciamento de arquivos nessas pastas são cruciais para o processamento eficiente de ativos. A implementação de convenções de nomenclatura e práticas de metadados sistemáticas maximiza a utilidade do repositório de ativos digitais.
Quer saber mais? Ir para [Organizar ativos em pastas](/help/assets/organize-assets.md#organize-using-folders).
* **Organizar ativos usando marcas:**
Marcar ativos melhora a capacidade de pesquisa, a criação de coleções e a classificação de pesquisa. A IA do Adobe emprega um algoritmo de autoaprendizado para marcação precisa, permitindo a recuperação rápida de ativos. A IA da Adobe também reconhece e atribui tags relevantes, incluindo tags personalizadas, aos ativos, simplificando o gerenciamento de ativos com marcação descritiva automática.
Quer saber mais? Ir para [Organizar ativos usando marcas](/help/assets/organize-assets.md#use-tags-to-organize-assets).
* **Organizar ativos como coleções:**
O Dynamic Media, juntamente com o Experience Manager Assets, permite a criação, edição e compartilhamento eficientes de coleções de ativos entre usuários. Você pode estabelecer vários tipos de coleções, incluindo listas estáticas e compilações dinâmicas baseadas em pesquisa. Esses tipos de coleção podem ser compartilhados em vários locais com direitos de acesso e edição personalizáveis.
Quer saber mais? Vá para [Organizar ativos como coleções](/help/assets/manage-collections.md).
* **Organizar ativos usando perfis:**
Um perfil de processamento automatiza o manuseio de ativos em pastas designadas, simplificando a organização. A padronização de metadados, nomes de arquivos e estruturas de pastas permite a aplicação consistente e precisa desses perfis à medida que a sua coleção de ativos digitais se expande.
Quer saber mais? Ir para [Organizar ativos usando perfis](/help/assets/organize-assets.md#organize-to-use-profiles).



### Otimizar a qualidade das imagens

**Caso de negócios:** *Obter imagens de boa qualidade do Dynamic Media.*

O aprimoramento da qualidade da imagem requer uma consideração cuidadosa de vários fatores. Pode ser um processo que exige muito tempo. No entanto, existem algumas práticas testadas e verdadeiras que podem ajudá-lo a alcançar os resultados desejáveis. Algumas dessas práticas recomendadas incluem como obter o dimensionamento e a nitidez ideais da imagem e os melhores formatos de imagem a serem usados.

Quer saber mais? Vá para [Práticas recomendadas para otimizar a qualidade das imagens](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md).

Como a percepção da qualidade da imagem varia de pessoa para pessoa, às vezes, uma abordagem sistemática da experimentação é essencial para alcançar resultados desejáveis. O Adobe Experience Manager auxilia esse processo com mais de 100 comandos do Dynamic Media para aprimoramento da imagem.

Quer saber mais? Assista ao [Instantâneo do Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot) (3 minutos, 17 segundos).

Para avaliar o impacto desses diferentes comandos na qualidade da imagem, você pode fazer upload de uma imagem no Dynamic Media, usar a interface da ferramenta no URL especificado e aplicar os comandos que deseja experimentar.

Quer experimentar? Iniciar o [Instantâneo do Dynamic Media](https://snapshot.scene7.com/)

### Padronizar estilos aplicados a imagens

**Business case:** *Padronize com eficiência o estilo e a transformação aplicados aos meus ativos de imagem.*

Use predefinições de imagem regularmente no Dynamic Media para ajustar de forma consistente e dinâmica os tamanhos, os formatos e as propriedades da imagem. Pense em uma Predefinição de imagem como uma macro: é um conjunto nomeado de comandos para dimensionamento e formatação. Por exemplo, se seu site precisa de imagens de produtos em vários tamanhos e formatos, com compactação específica para desktop e dispositivos móveis, as Predefinições de imagem automatizam esse processo com eficiência.

Quer experimentar? Ir para [Princípios básicos da criação de predefinições de imagens para renderizar ativos](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-e)

### Ajustar o foco e o enquadramento de imagens e vídeos

**Caso de negócios:** *Verifique se o principal ponto de interesse das minhas imagens ou vídeos permanece em foco em todos os dispositivos.*

O Recorte inteligente é um recurso do Dynamic Media que usa a IA do Adobe, a IA do Adobe e a estrutura de aprendizado de máquina, para automatizar o recorte de imagens e vídeos. Ele detecta e focaliza de forma inteligente o assunto principal ou ponto de interesse em uma imagem ou vídeo. Essa inteligência garante que o ponto focal seja mantido em vários tamanhos de tela em computadores desktop e dispositivos móveis.

Uma prática recomendada é criar um Perfil de imagem com Recorte inteligente. No perfil, é possível definir vários tamanhos de tela e permitir que a IA do Adobe faça o resto, garantindo que suas imagens e vídeos sejam sempre otimizados para o dispositivo do visualizador.

Quer saber mais? Assista ao [Uso do Corte Inteligente com o AEM Assets Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) (6 minutos, 35 segundos) e [Uso do Corte Inteligente do Dynamic Media para Vídeo](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video) (6 minutos, 22 segundos).

### Melhorar as classificações da SEO

**Caso de negócios:** *Configure o Dynamic Media para obter melhores classificações de SEO.*

Use as recomendações a seguir regularmente para garantir que suas imagens contribuam de maneira eficaz para a sua estratégia geral de SEO.

* **Nomes significativos de arquivos de imagem:**
Use nomes de arquivo descritivos que refletem o conteúdo da imagem. Por exemplo,

   * use `myCompany-Silver-Wrist-Watch`
   * *evitar* `myCompany_Silver_Wrist_Watch` ou `myCompanySilverWristWatch`

  Isso ajuda os mecanismos de pesquisa a entender o contexto da imagem e melhora a SEO. O Google prefere hífens a sublinhados ou espaços no nome do arquivo. Além disso, evite concatenar palavras em um nome de arquivo.
* **Domínio personalizado:**
Implemente um domínio personalizado que inclua sua empresa ou nome da marca para reforçar o reconhecimento e a confiança da marca. Por exemplo,

   * use `http://images.mycompany.com/is/image/companyname/`
   * *evitar* `https://s7d1.scene7.com/is/image/folder/AdobeStock_28563982`

* **Estrutura de pastas compatível com SEO:**
Organize as imagens em uma estrutura de pastas que inclua o nome da empresa ou a marca para melhorar a indexação, como `http://images.mycompany.com/is/image/companyname/`.
* **Conjuntos de regras do Dynamic Media:**
Saiba como você pode transformar condicionalmente URLs com base em vários fatores, aprimorando o SEO e a experiência do usuário.
Quer saber mais? Ir para [Usar conjuntos de regras para transformar URLs](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md).
* **Imagem Inteligente e Recorte Inteligente:**
Use os recursos de Imagem inteligente e Recorte inteligente no Dynamic Media para fornecer imagens otimizadas e responsivas. Isso não só melhora o tempo de carregamento da página, como também contribui positivamente para as classificações de SEO.
Quer saber mais? Vá para [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md) ou assista [Usando o Smart Crop com o AEM Assets Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) (6 minutos, 35 segundos).

Lembre-se de que essas práticas recomendadas se alinham bem com as práticas recomendadas de SEO de imagem da Google. Essas práticas enfatizam a importância de fornecer contexto e clareza aos mecanismos de pesquisa por meio de convenções de nomenclatura adequadas, dados estruturados e entrega de imagem otimizada.

Quer saber mais? Ir para [Práticas recomendadas da estrutura de URL do Google](https://developers.google.com/search/docs/crawling-indexing/url-structure) e [Práticas recomendadas do Google image SEO](https://developers.google.com/search/docs/appearance/google-images)

### Aprimorar dinamicamente imagens e criar efeitos visuais usando comandos

**Caso de negócios:** *Aplicar efeitos visuais avançados a imagens.*

O Dynamic Media oferece um conjunto de comandos para aprimorar imagens e criar efeitos visuais dinamicamente, sem a necessidade de vários ativos estáticos. Veja a seguir algumas explicações resumidas de alguns desses processos e alguns exemplos para orientá-lo:

#### Efeitos dentro da imagem de origem

| Tarefa | O que fazer |
| --- | --- |
| **Carregar e publicar sua imagem original** | <ul><li> Comece fazendo upload da imagem original no Dynamic Media.</li><li> Certifique-se de que ele seja publicado e acessível por meio de um URL.</li><li> Neste exemplo, uma imagem de stock de um relógio com um fundo branco (vamos chamá-lo de &quot;Imagem X&quot;) é carregada no Dynamic Media.<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer)</li></ul> |
| **Criar uma máscara** | <ul><li> Desenvolva uma máscara que defina o assunto (a área onde deseja aplicar efeitos) e o plano de fundo (a área que deseja alterar).<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps)</li><li> As máscaras são normalmente imagens em tons de cinza, onde o branco representa o assunto e o preto representa o plano de fundo. É possível criar máscaras usando ferramentas como o Adobe Photoshop.<br>Deseja saber mais? Ir para [Criação e edição de uma máscara rápida no Photoshop](https://helpx.adobe.com/in/photoshop/using/create-temporary-quick-mask.html).</li><li> Para &quot;Imagem X&quot;, crie uma máscara que descreva com precisão o assunto que você deseja aprimorar. Por exemplo, uma pessoa, um objeto e assim por diante.</li></ul> |
| **Aplicar comandos de URL do Dynamic Media para efeitos** | Depois de usar a máscara, use comandos de URL para aplicar efeitos como um brilho externo ou altere a cor do plano de fundo para &quot;Imagem X&quot;. Veja dois exemplos:<ul><li> **Efeito de brilho externo:**<br> Para adicionar um efeito de brilho externo ao longo do limite do assunto, edite a URL desta maneira:<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;effect=-1&amp;pos=100,100&amp;op_blur=75&amp;op_grow=1&amp;opac=25](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&maskUse=invert&effect=-1&pos=100,100&op_blur=75&op_grow=1&opac=25)<br>Nesta URL, os parâmetros `op_blur`, `op_grow` e `opac` criam o efeito de brilho externo.</li><li> **Alteração da cor do plano de fundo:**<br> Para alterar a cor do plano de fundo, use a URL com um valor de cor de plano de fundo diferente:<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;maskUse=invert&amp;color=255,255,0](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&maskUse=invert&maskUse=invert&color=255,255,0)<br> Neste exemplo, o `color=255,255,0` define a cor do plano de fundo como amarelo. Edite o plano de fundo com uma cor específica para impacto visual.</li></ul> |

#### Adicionar uma borda de imagem

O Dynamic Media permite manipular imagens diretamente por meio de URLs, tornando-as uma ferramenta poderosa para criar experiências digitais dinâmicas. Veja a seguir alguns exemplos. Vamos começar com a seguinte URL da imagem original: [https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel).

| Tarefa | O que fazer |
| --- | --- |
| **Borda branca** | Para adicionar uma borda branca, use a seguinte URL:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10)<br>Nessa URL, o parâmetro `extend=10,10,10,10` especifica o tamanho da borda de dez pixels em todos os lados. |
| **Desfoque ao longo da borda branca** | Para adicionar um efeito de desfoque ao longo da borda branca, edite a URL da seguinte maneira:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;op_blur=60&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10&effect=-1&op_blur=60&color=0,0,0)<br>Nessa URL, o parâmetro `effect=-1` aplica o efeito de desfoque e `op_blur=60` controla a intensidade do desfoque. |
| **Efeito de sombra projetada ao longo do limite externo** | Para adicionar um efeito de sombra projetada ao longo do limite externo, use esta URL:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;$shadow$&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10&effect=-1&$shadow$&color=0,0,0)<br>O parâmetro `$shadow$` cria o efeito de sombra e `color=0,0,0` define a cor da sombra como preto. |

Experimente esses URLs para obter os efeitos visuais desejados.

#### Criar sobreposições de imagem

Se você deseja sobrepor um logotipo ou ícone em uma imagem existente, o Dynamic Media oferece uma maneira simples de fazer isso usando comandos de URL. Vamos analisar os passos.

| Etapa | O que fazer |
| --- | --- |
| **Carregar e publicar a imagem base** | Primeiro, carregue e publique a imagem base na qual você deseja sobrepor o logotipo ou ícone. Você pode usar qualquer imagem como base.<br>Por exemplo, aqui está uma imagem base:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa). |
| **Carregar e publicar o logotipo ou a imagem de ícone** | Em seguida, faça upload e publique a imagem que deseja sobrepor sobre a imagem base. Esta imagem deve ser um PNG transparente com o logotipo ou ícone que você deseja sobrepor.<br>Esta é a imagem PNG transparente de um objeto estrela com efeitos de transparência que será sobreposta:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorate-star](https://s7g2.scene7.com/is/image/genaibeta/decorate-star) |
| **Aplicar a URL do Dynamic Media** | Agora, crie um URL do Dynamic Media que combine a imagem base com a imagem de logotipo ou ícone. Você pode usar comandos de URL para obter esse efeito.<br>A estrutura da URL é semelhante a esta:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&amp;src=decorate-star&amp;scale=1.25&amp;posN=0.33,-.25&amp;fmt=png](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&src=decorate-star&scale=1.25&posN=0.33,-.25&fmt=png)<br>onde o ativo<ul><li> `hotspotRetailBaseImage` é a imagem base.</li><li> `starxp` é a imagem de logotipo/ícone.</li><li> `layer=1` especifica que o logotipo ou ícone deve ser colocado sobre a imagem base.</li><li> `scale=1.25` ajusta o tamanho do logotipo/ícone.</li><li> `posN=0.33,-.25` determina a posição do logotipo/ícone em relação à imagem base.</li><li> `fmt=png` garante que a saída esteja no formato PNG.</li></ul> |

O que aprender mais? Vá para [src](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-src) para obter mais detalhes sobre o comando `src` e outros comandos de URL do Dynamic Media.


#### Sobreposição de texto promocional

A seguir estão as etapas para sobrepor uma mensagem de texto promocional em uma imagem usando HTML e CSS.

| Etapa | O que fazer |
| --- | --- |
| **Carregar e publicar a imagem base** | Primeiro, carregue e publique a imagem base na qual você deseja sobrepor o texto. Você pode usar qualquer imagem que desejar. Por exemplo, esta é uma amostra de imagem base:<br>[https://s7g2.scene7.com/is/image/genaibeta/leather-sofa](https://s7g2.scene7.com/is/image/genaibeta/leather-sofa)<br> |
| **Aplicar operadores de texto do Dynamic Media** | Com o Dynamic Media, é possível aplicar operadores de texto para sobrepor texto dinâmico diretamente na imagem. O exemplo de URL a seguir demonstra essa capacidade:<br>[https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&amp;posN=-0.3,-0.455&amp;text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF333&amp;wid=600&amp;hei=600](https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&posN=-0.3,-0.455&text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&size=370,70&textAttr=130&bgcolor=FF3333&wid=600&hei=600) |

#### Redimensionamento e corte para vários casos de uso

##### Noções básicas de redimensionamento de imagem

O redimensionamento da imagem envolve a alteração das dimensões, da resolução e do tamanho do arquivo de uma imagem. Estes são alguns pontos principais a serem considerados:

* **Composição de pixels:**
As imagens digitais consistem em pequenos pontos chamados pixels. Quando uma imagem é criada, ela tem um número específico de pixels. O redimensionamento envolve a adição ou subtração de pixels para alterar as dimensões, a resolução e o tamanho do arquivo da imagem.
* **Taxa de proporção:**
Manter a taxa de proporção (a relação entre largura e altura) é fundamental para evitar distorções. Independentemente de você estar fazendo uma imagem maior (upscaling) ou menor (downscaling), preservar a proporção garante a consistência visual.
* **Considerações de qualidade:**
O redimensionamento pode afetar a qualidade da imagem. Evite um aumento drástico, pois isso pode resultar em pixelação. Em vez disso, considere reproduzir a imagem em um tamanho e resolução maiores. Para imagens menores, use as ferramentas apropriadas para manter a resolução.

##### Corte versus redimensionamento

Recortar e redimensionar são técnicas no Dynamic Media que permitem transformar imagens para atender a vários casos de uso, seja criando miniaturas, imagens de exibição de produto ou banners.

* **Recorte:**
Envolve a remoção de parte de uma imagem para alterar sua composição e enquadramento. Ela não altera as dimensões gerais, mas se concentra em uma área específica.
* **Redimensionando:**
Ajusta as dimensões, a resolução e o tamanho do arquivo da imagem inteira, mantendo a proporção.

Vamos explorar um caso de uso que envolve a seguinte imagem de sala de estar:

* **Imagem original da sala de estar:**
  [https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa)
* **Miniatura (200 px x 200 px):**
Uma versão menor adequada para carregamento ou exibição rápidos.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&hei=200&fit=crop)
* **Miniatura com recorte (200 px x 200 px):**
Recortado para focalizar na área do sofá.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&hei=200&cropN=.24,.24,.6,.72&fit=crop)
* **Imagem para exibição do produto (800 px x 600 px):**
Recortado e redimensionado para exibir o sofá.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&amp;hei=600&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&hei=600&cropN=.24,.24,.6,.72&fit=crop)
* **Banner (1720 px x 820 px):**
Derivado da imagem original, enfatizando a sala.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&amp;hei=820&amp;cropN=0,.1,1,1&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&hei=820&cropN=0,.1,1,1&fit=crop)

Fique à vontade para explorar essas variações de acordo com suas necessidades específicas.
Deseja saber mais sobre os comandos disponíveis em um URL? Vá para [Referência de comando](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference).

### Entregar imagens do GIF

**Caso de negócios:** *Transmitir GIFs usando Dynamic Media*

Você pode fazer upload e entregar GIFs por meio do Dynamic Media. Para renderizar uma GIF animada, substitua `is/image` por `is/content` na URL. Por exemplo, se você carregou `abc.gif`, use o seguinte:

* Esse caminho de URL renderiza uma visualização estática do GIF:

  ```
  https://your.domain.com/is/image/yourfolder/abc
  ```

* Esse caminho de URL renderiza a visualização de animação do GIF:

  ```
  https://your.domain.com/is/content/yourfolder/abc
  ```

>[!NOTE]
>
>Ao usar `is/content` no caminho da URL, os comandos de transformação de imagem não são aplicados ao ativo.

### Publicar um vídeo para meu site

**Caso de negócios:** *Publique rapidamente um vídeo para um site de marketing.*

* **Selecione um perfil de vídeo:**
Primeiro, no Dynamic Media, selecione um perfil de vídeo adequado. Você pode optar pelo perfil *Codificação de vídeo adaptável* disponível no AEM Assets em Perfis de vídeo. Essas configurações de codificação predefinidas garantem que o vídeo seja otimizado para reprodução em vários dispositivos e condições de largura de banda. Como alternativa, você pode criar seu próprio perfil de Vídeo adaptável.
* **Atribuir o perfil:**
Atribua o perfil de vídeo escolhido às pastas onde o vídeo será carregado. Essa etapa garante que as configurações de codificação corretas sejam aplicadas durante o processo de upload.
* **Carregar o vídeo original:**
Carregue o arquivo de vídeo original. Verifique se é um vídeo de alta resolução com boa qualidade. Quanto melhor o vídeo de origem, melhor o resultado final.
* **Visualizar e publicar:**
Visualize o vídeo para garantir que tudo fique com a aparência esperada. Depois de satisfeito, publique-o. Essa etapa torna o vídeo acessível ao seu público-alvo.
* **Vincular ou incorporar:**
Após a publicação, você tem duas opções.

   * **Vincular diretamente:**
Use o URL fornecido para vincular diretamente ao vídeo. Use o hiperlink adequado no site de marketing.
   * **Inserir o vídeo:**
Copie o código incorporado fornecido e cole-o na HTML da página da Web onde deseja que o vídeo apareça. Isso permite que o vídeo seja reproduzido diretamente no site.

Quer saber mais? Ir para [Vídeo](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/video).

### Configurar vídeos para obter qualidade e engajamento ideais

**Caso de negócios:** *Configure vídeos para obter a melhor qualidade e participação.*

Para garantir a melhor qualidade e o melhor envolvimento para seus vídeos, considere implementar uma combinação das seguintes estratégias de práticas recomendadas:

* **Usar o Visualizador de Vídeo interno do HTML5:**
As Predefinições do visualizador de vídeo do Dynamic Media HTML5 são players de vídeo robustos. Use-os para evitar problemas comuns associados à reprodução de vídeo e aos dispositivos móveis da HTML5.
Essas predefinições abordam desafios como a entrega adaptável da transmissão da taxa de bits e o alcance limitado do navegador do desktop.
Quer saber mais? Vá para [Prática recomendada: usar o visualizador de vídeo do HTML 5](/help/assets/dynamic-media/video.md#best-practice-using-the-html-video-viewer).

* **Usar Perfis de Vídeo do Dynamic Media:**
Os perfis de vídeo no Dynamic Media ajudam no gerenciamento eficiente de vídeo, na qualidade consistente e na transmissão adaptável.
Quer saber mais? Vá para [Perfis de vídeo do Dynamic Media](/help/assets/dynamic-media/video-profiles.md).

* **Siga as Práticas Recomendadas para Codificação de Vídeo:**
Aplique perfis de codificação de vídeo que mantêm a qualidade original do vídeo sem redução excessiva durante a codificação.
Quer saber mais? Ir para [Práticas recomendadas para codificação de vídeos](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos).

* **Adotar transmissão adaptável em vez de transmissão progressiva:**
O fluxo adaptável ajusta a qualidade do vídeo com base na velocidade de conexão da Internet do visualizador e nos recursos do dispositivo.
Ele usa protocolos como HLS (HTTP Live Streaming) ou DASH (`Dynamic Adaptive Streaming over HTTP`) para garantir a melhor qualidade de reprodução.
Ao contrário da transmissão progressiva, que fornece vídeos linearmente, a transmissão adaptável minimiza o buffer e oferece uma experiência de visualização contínua.

### Internacionalizar vídeos para consumo multilíngue

**Caso de negócios:** *Prepare vídeos para consumo multilíngue.*

Internacionalizar vídeos para consumo multilíngue é essencial para alcançar um público global. O Dynamic Media fornece recursos que podem ajudar você a alcançar essa meta.

* **Carregar seus vídeos:**
   * Primeiro, crie um perfil de codificação de vídeo. Você pode usar o perfil Codificação de vídeo adaptável predefinido que acompanha o Dynamic Media ou criar seu próprio perfil personalizado.
   * Associe o perfil de processamento de vídeo a uma ou mais pastas nas quais você faz upload dos vídeos de origem primária.
   * Faça upload dos vídeos de origem principal para essas pastas. O Dynamic Media os codifica com base no perfil de processamento de vídeo atribuído.
   * O Dynamic Media é compatível principalmente com vídeos de formato curto (até 30 minutos) com uma resolução mínima superior a 25 × 25. Arquivos de vídeo de até 15 GB podem ser carregados1.

* **Gerenciar seus vídeos:**
   * Organize, navegue e pesquise ativos de vídeo no AEM.
   * Pré-visualizar e publicar ativos de vídeo.
   * Visualize o vídeo de origem e suas representações codificadas junto com miniaturas associadas.
   * Edite as propriedades do vídeo, como título, descrição e tags2.

* **Localização:**
   * Para cada geografia/idioma de destino, crie faixas de áudio e legendas.
   * Adicione essas faixas de áudio e legendas aos seus vídeos da interface do AEM.
   * À medida que os usuários reproduzem os vídeos, eles podem selecionar seu idioma preferido para áudio e legendas.

* **Publicação:**
   * Se você estiver usando o AEM como o sistema de Gerenciamento de conteúdo da Web (WCM), poderá adicionar vídeos diretamente às suas páginas da Web.
   * Se você estiver usando um sistema WCM de terceiros, é possível vincular ou incorporar vídeos nas páginas da Web usando URLs ou códigos incorporados.

Quer saber mais? Vá para [Sobre o suporte a várias legendas e faixas de áudio para vídeos no Dynamic Media](/help/assets/dynamic-media/video.md#about-msma).


## Entregar ativos aos clientes

### Otimizar tamanhos de imagem e minimizar o tempo de carregamento da página

**Business case:** *Otimize o tamanho das imagens para qualquer navegador ou tela e reduza o tempo de carregamento da página.*

O Dynamic Media Smart Imaging é uma ferramenta poderosa que aumenta o desempenho do delivery de imagens, otimizando automaticamente o formato, o tamanho e a qualidade da imagem com base nos recursos do navegador do cliente.

A Adobe recomenda que você use os recursos do Smart Imaging em vez de configurar manualmente o formato da imagem para `webp` ou `avif`. Veja o porquê:

* **Compatibilidade do navegador:**
A Smart Imaging garante que o formato de imagem entregue seja compatível com o navegador do usuário.
* **Compactação ideal:**
Ele seleciona o melhor formato para compactação com base no navegador específico, nas condições de rede e na resolução da tela.
* **Formatos modernos:**
Embora o `avif` seja um formato mais novo que oferece melhor compactação, ele ainda não tem suporte universal em todos os navegadores.
* **Práticas recomendadas:**
Para garantir o melhor formato otimizado para a Web, você pode confiar no Smart Imaging para fazer a seleção de formato, em vez de usar manualmente os comandos `fmt=webp` ou `fmt=avif`.

Com a Smart Imaging, você pode garantir que suas imagens sejam entregues da maneira mais eficiente possível, sob medida para o ambiente de navegação de cada usuário. Essa abordagem simplifica o processo e pode resultar em melhor desempenho em termos de tempo de carregamento de imagem e experiência geral do usuário.

Quer saber mais? Vá para [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md).

### Pós-entrega de ativos aos clientes

**Business case:** *Depois de publicar novo conteúdo ou substituir conteúdo existente, como é possível garantir que as alterações apareçam imediatamente na CDN?*

A CDN (Content Delivery Network) armazena em cache os ativos do Dynamic Media para entrega rápida aos clientes. Quando são feitas atualizações nesses ativos, é importante que as alterações entrem em vigor imediatamente no site. Ao limpar ou invalidar o cache da CDN, os ativos entregues pelo Dynamic Media podem ser atualizados rapidamente. Essa abordagem elimina a necessidade de aguardar a expiração do cache com base no valor TTL (Time To Live), que normalmente é definido como dez horas. Dependendo do caso de uso específico, é possível atualizar as configurações de CDN TTL (Time to Live) de acordo.

Quer saber mais? Ir para [Invalidar o cache CDN por meio do Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

