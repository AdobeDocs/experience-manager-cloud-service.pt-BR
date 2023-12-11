---
title: Gerenciamento de metadados e práticas recomendadas
description: Saiba mais sobre as práticas recomendadas de metadados para gerenciar com eficiência seus ativos digitais.
role: User, Admin
hide: true
hidefromtoc: true
source-git-commit: 8434cb580ba8afc018a5a4357a4d249a06c566c2
workflow-type: tm+mt
source-wordcount: '1287'
ht-degree: 0%

---


<!-- Keywords to focus on:
metadata best practices
aem metadata 
experience manager metadata-->

# Gerenciamento de metadados e práticas recomendadas {#metadata-best-practices}

Para destacar sua empresa e atrair mais clientes, é fundamental utilizar recursos visuais de alta qualidade, como imagens, vídeos e outros ativos digitais. Para isso, é necessário um processo que permita adicionar metadados a todos os ativos digitais, tornando-os facilmente pesquisáveis. Os metadados são os dados que fornecem detalhes essenciais sobre ativos digitais, incluindo o nome, o tipo, o histórico de modificações, a localização em um repositório e as tags associadas do ativo. Os metadados simplificam o gerenciamento de ativos, melhoram a pesquisabilidade e a acessibilidade e garantem o controle eficaz de versões.

Saiba como usar metadados no sistema de Gerenciamento de ativos digitais (DAM) para [gerencie metadados de seus ativos digitais](manage-metadata.md).

## Tipos de metadados

Com base nos vários aspectos dos dados, os metadados são categorizados como Metadados técnicos, Metadados informativos e Metadados administrativos.

### Metadados técnicos

Os metadados técnicos compreendem os aspectos técnicos de um ativo. Esse tipo de metadados é crucial para que os usuários entendam as características inerentes dos ativos digitais, facilitando o processamento e a utilização eficientes.
Inclui detalhes como:

* Tamanho do arquivo
* Formato
* Resolução
* Dimensões
* Modo de cores

### Metadados informativos

Os metadados informativos englobam informações descritivas que melhoram a compreensão do conteúdo de um ativo. Esses metadados são fundamentais para a descoberta de conteúdo, a pesquisabilidade e a compreensão do significado do ativo. Os metadados informativos incluem palavras-chave, legendas e descrições.

Por exemplo, ao gerenciar um vídeo no Experience Manager Assets, podemos incluir os seguintes metadados informativos:

* **Palavras-chave**: Marketing, Lançamento de produto, Promoção
* **Legenda**: Apresentando nosso produto mais recente com excelentes recursos
* **Descrição**: uma visão geral detalhada do conteúdo do vídeo.

Os usuários que procuram conteúdo relacionado a marketing podem encontrar e entender facilmente o significado do vídeo acima.


### Metadados administrativos

Os metadados administrativos tratam dos aspectos gerenciais dos ativos digitais. Ele garante o controle de acesso, a conformidade e o gerenciamento do ciclo de vida geral dos ativos no sistema de gerenciamento de ativos digitais. Inclui informações relacionadas com:

* Propriedade do ativo
* Direitos de uso
* Permissões
* Outros detalhes administrativos

Os metadados administrativos garantem o gerenciamento correto de ativos, controlando o acesso e a conformidade no sistema de gerenciamento de ativos digitais.

## Práticas recomendadas de metadados

### Defina sua estratégia de metadados desde o início

O gerenciamento de metadados começa com a definição de uma estratégia de metadados para fornecer uma base para avaliar o valor a longo prazo.

Criar um esquema de metadados personalizado de acordo com seus requisitos é fundamental ao planejar sua estratégia de metadados. Um esquema bem projetado fornece uma estrutura estruturada para categorizar e organizar ativos no Adobe Experience Manager.

#### Vídeo: Adicionar campos personalizados ao esquema de metadados

>[!VIDEO](https://video.tv.adobe.com/v/3425977)

Sua estratégia de metadados pode incluir a definição do seguinte:

* **Objetivos:** Descreva claramente os objetivos e os resultados esperados dos metadados. Identifique o que você deseja alcançar adicionando os metadados.

* **Finalidade:** Defina por que você está capturando metadados. Especifique o valor que ele adiciona aos seus processos, sistemas ou organização.

* **Plano de acessibilidade:** Crie um plano para tornar os metadados facilmente acessíveis e detectáveis. Explique quem o usará e as ferramentas ou métodos a serem usados.

* **Propriedades dos metadados:** Identifique e defina cada propriedade de metadados com cuidado. Certifique-se de que cada propriedade tenha um motivo claro para ser incluída, conectando-se aos objetivos e à finalidade.

Planeje cuidadosamente a estratégia para garantir resultados consistentes em todo o repositório.

### Criar um plano de governança de metadados

A governança de dados garante que os esforços de gerenciamento de metadados da organização estejam alinhados aos objetivos gerais de negócios.
A estratégia de governação pode incluir:

* Estabelecer políticas e procedimentos para o gerenciamento de dados e metadados.
* Definição de padrões para a qualidade e a integridade dos dados.
* Definição de funções e responsabilidades no gerenciamento de dados.

Determine de onde vêm as informações e examine os detalhes da estratégia de metadados, incluindo as propriedades e suas fontes. Ele pode ser dimensionado dependendo da complexidade da estratégia. Em grandes empresas, há um sistema de gerenciamento de metadados mestre supervisionando vários sistemas na pilha mestre.

<br>

>[!NOTE]
>
>Saiba como [gerencie metadados de seus ativos digitais](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/metadata.html).

### Ser consistente com a estratégia de metadados

Uma estratégia de metadados consistente garante a organização e a recuperação eficazes de ativos digitais. Adotar uma abordagem estratégica para capturar e implementar valores de metadados, permitindo a flexibilidade para a evolução sem alterações desnecessárias. <br>
No gerenciamento de metadados de toda a empresa, a consistência é importante ao nomear e fazer referência aos ativos. Por exemplo, ao gerenciar vários ativos simultaneamente, considere adicionar metadados em massa. <br>
Estas são algumas das práticas recomendadas:

* **Evite valores duplicados:** Se você tiver uma coleção de imagens de uma campanha de marketing, use nomes consistentes e evite duplicatas.<br>
Por exemplo, em vez de usar nomes duplicados como *campaign_image_001* e *campaign_image_002*, implementar uma convenção de nomenclatura sistemática, como *product_launch_001* e *product_launch_002*, garantindo uma identificação clara e ordenada.

* **Usar vocabulários controlados de forma eficaz:** Implemente vocabulários controlados empregando termos padronizados para tags. <br>
Por exemplo, use termos consistentes como *product_launch* ou *event_promotion* ao marcar imagens com temas para manter a sequência sistemática.

* **Manter a precisão e a integridade:** Para manter a consistência dos metadados, a precisão, a integridade e o alinhamento em várias fontes são cruciais.<br>
Por exemplo, ao adicionar metadados a um documento PDF, verifique se os detalhes como nomes de autores e palavras-chave são precisos e completos.

#### Vídeo: adicionar metadados em massa aos ativos

>[!VIDEO](https://video.tv.adobe.com/v/3425978)

### Avaliar e melhorar a capacidade de pesquisa de metadados

Avalie sua estratégia de metadados para melhorar a capacidade de pesquisa de metadados. Simplifique os fluxos de trabalho e aprimore os recursos de pesquisa para obter uma reutilização eficiente. Evite lidar com metadados que não têm um propósito claro.<br>
Você pode considerar as seguintes práticas recomendadas para otimizar a capacidade de pesquisa de metadados:

* **Otimização de palavra-chave:** Melhore a capacidade de pesquisa de metadados otimizando palavras-chave associadas a ativos. Você pode melhorar a relevância de palavras-chave para ativos específicos no Gerenciador de ativos seguindo estas etapas:

   1. Ir para **[!UICONTROL Assets]** > **[!UICONTROL Arquivo]** > **[!UICONTROL [Pasta do ativo]]**.
   1. Selecione o ativo para o qual deseja atualizar os metadados e clique em **[!UICONTROL Propriedades]**.
   1. Navegue até a **[!UICONTROL Avançado]** e clique em **[!UICONTROL Adicionar]** no **[!UICONTROL Elevar para palavras-chave de pesquisa]**.
   1. Insira a palavra-chave para a qual deseja impulsionar a pesquisa e clique em **[!UICONTROL Adicionar]**.<br>
Você pode adicionar várias palavras-chave e organizá-las de acordo com sua prioridade.
   1. Clique em **[!UICONTROL Salvar e fechar]**.<br>
Pesquise o ativo usando as palavras-chave adicionadas. O ativo aparece entre os principais resultados da pesquisa.

  Saiba como [impulsionar pesquisa no Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

* **Campos de metadados personalizados:** Personalize os campos de metadados para capturar informações adicionais sobre ativos. Por exemplo, adicione campos específicos para obter detalhes do projeto, informações de direitos autorais ou quaisquer outros dados relevantes que melhorem os recursos de pesquisa.

* **Validação de metadados:** Implemente verificações de validação para entradas de metadados para garantir consistência e precisão. Isso pode envolver a configuração de diretrizes para determinadas propriedades de metadados para evitar informações ambíguas ou inconsistentes.

* **Rastreamento de uso:** Avalie a relevância e o uso de diferentes propriedades de metadados ao longo do tempo. Identifique e priorize metadados usados com frequência ou contribua significativamente para os processos de pesquisa e recuperação.

#### Vídeo: adicionar palavras-chave para melhorar a capacidade de pesquisa

>[!VIDEO](https://video.tv.adobe.com/v/3425979)

### Mantenha os metadados simples e fáceis de entender

Simplifique os metadados para melhorar a governança e a adoção pelos usuários. Mantenha-o simples e fácil de entender, incentivando os usuários a adicionar informações essenciais. <br>
Experimente as seguintes práticas recomendadas para simplificar os metadados:

* **Otimizar opções de propriedade:** Concentre-se em destacar propriedades essenciais sem sobrecarregar os usuários com muitos campos de metadados para preencher. Por exemplo, ao adicionar metadados para uma imagem, inclua apenas campos principais como título, descrição e tags para uma categorização eficaz.

* **Eliminar propriedades padrão desnecessárias:** Simplifique o formulário de metadados eliminando propriedades padrão prontas para uso irrelevantes para o seu caso de uso. Remova as propriedades padrão raramente usadas para uma interface e experiência mais simples.

* **Revise e atualize os metadados periodicamente:** Atualize os metadados regularmente e adapte-se às necessidades e tecnologias em constante mudança para garantir que os usuários forneçam informações valiosas ao longo do tempo.

### Analisar jornada de conteúdo

Examine a cadeia de fornecimento de conteúdo para encontrar fontes de metadados e envolver todas as partes interessadas, começando pelo topo, para obter uma abordagem completa de práticas recomendadas. Envolva diferentes membros da equipe para garantir suporte completo em toda a organização. Incorpore metadados em vários estágios para compartilhar a responsabilidade de fornecer detalhes do ativo durante o upload.

Comunicar antecipadamente os objetivos, os progressos, os marcos e os desafios para receber contribuições e cooperação de todas as partes interessadas. Estimule a colaboração em toda a organização para criar processos eficientes e metadados valiosos.

Saiba mais sobre [metadados e conceitos relacionados](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-concepts.html) para gerenciar efetivamente os metadados de Experience Manager.
