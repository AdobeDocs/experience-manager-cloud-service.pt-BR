---
title: Gerenciamento de metadados e práticas recomendadas
description: Saiba mais sobre as práticas recomendadas de metadados para gerenciar com eficiência seus ativos digitais.
role: User, Admin
exl-id: d90519df-55a6-4e23-81ad-ff2365d71c0d
feature: Metadata, Best Practices
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 0%

---

<!-- Keywords to focus on:
metadata best practices
aem metadata 
experience manager metadata-->

# Gerenciamento de metadados e práticas recomendadas {#metadata-best-practices}

Para destacar sua empresa e atrair mais clientes, é fundamental utilizar recursos visuais de alta qualidade, como imagens, vídeos e outros ativos digitais. Para isso, é necessário um processo que permita adicionar metadados a todos os ativos digitais, tornando-os facilmente pesquisáveis. Os metadados são os dados que fornecem detalhes essenciais sobre ativos digitais, incluindo o nome, o tipo, o local em um repositório, a data de modificação e as tags associadas do ativo. Os metadados simplificam o gerenciamento de ativos, melhoram a pesquisabilidade e a acessibilidade e garantem o controle eficaz de versões.

Saiba como usar metadados no sistema de Gerenciamento de ativos digitais (DAM) para [gerenciar efetivamente metadados de seus ativos digitais](manage-metadata.md).

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

* **Palavras-chave**: marketing, lançamento de produto, promoção
* **Legenda**: apresentando nosso produto mais recente com excelentes recursos
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

Criar um esquema de metadados personalizado de acordo com seus requisitos é fundamental ao planejar sua estratégia de metadados. Um esquema bem projetado fornece uma estrutura estruturada para categorizar e organizar ativos no Experience Manager.

#### Vídeo: Adicionar campos personalizados ao esquema de metadados

>[!VIDEO](https://video.tv.adobe.com/v/3425977)

Sua estratégia de metadados pode incluir a definição do seguinte:

* **Objetivos:** descreva claramente os objetivos e os resultados esperados dos metadados. Identifique o que você deseja alcançar adicionando os metadados.

* **Propósito:** definir por que você está capturando metadados. Especifique o valor que ele adiciona aos seus processos, sistemas ou organização.

* **Plano de acessibilidade:** crie um plano para facilitar o acesso e a descoberta dos metadados. Explique quem vai usá-lo e as ferramentas ou métodos a serem usados.

* **Propriedades de metadados:** identifique e defina cada propriedade de metadados com cuidado. Certifique-se de que cada propriedade tenha uma razão clara para ser incluída, conectando-se aos objetivos e à finalidade.

Para garantir resultados consistentes em todo o repositório, planeje cuidadosamente a estratégia. Saiba mais sobre [esquemas de metadados](metadata-schemas.md).

### Criar um plano de governança de metadados

A governança de dados garante que os esforços de gerenciamento de metadados da organização estejam alinhados aos objetivos gerais de negócios.
A estratégia de governação pode incluir:

* Estabelecer políticas e procedimentos para o gerenciamento de dados e metadados.
* Definição de padrões para a qualidade e a integridade dos dados.
* Definição de funções e responsabilidades no gerenciamento de dados.

Determine de onde vêm as informações e examine os detalhes da estratégia de metadados, incluindo as propriedades e suas fontes. Ele pode ser dimensionado dependendo da complexidade da estratégia. Em grandes empresas, há um sistema de gerenciamento de metadados mestre supervisionando vários sistemas na pilha mestre.

>[!NOTE]
>
>Saiba como [gerenciar metadados de seus ativos digitais](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/metadata.html).

### Ser consistente com a estratégia de metadados

Uma estratégia de metadados consistente garante a organização e a recuperação eficazes de ativos digitais. Adotar uma abordagem estratégica para capturar e implementar valores de metadados, permitindo a flexibilidade para a evolução sem alterações desnecessárias. <br>

No gerenciamento de metadados de toda a empresa, a consistência é importante ao nomear e fazer referência aos ativos. Por exemplo, ao gerenciar vários ativos simultaneamente, &quot;considere adicionar metadados em massa&quot;. <br>

Estas são algumas das práticas recomendadas:

* **Evite valores duplicados:** se você tiver uma coleção de imagens de uma campanha de marketing, use nomes consistentes e evite duplicatas.

  Por exemplo, em vez de usar nomes duplicados como *campaign_image_001* e *campaign_image_002*, implemente uma convenção de nomenclatura sistemática, como *event_promotion* e *product_launch*, garantindo uma identificação clara e ordenada.

* **Usar vocabulários controlados de maneira eficaz:** implemente vocabulários controlados empregando termos padronizados para marcas. Saiba como implementar a [Estrutura de Marcação do AEM](/help/implementing/developing/introduction/tagging-framework.md) de maneira eficaz.

  Por exemplo, use de maneira consistente termos como *product_launch* ou *event_promotion* ao marcar imagens com temas para manter a sequência sistemática.

* **Manter precisão e integridade:** Para manter a consistência dos metadados, precisão, integridade e alinhamento em várias fontes são cruciais.
Por exemplo, ao adicionar metadados a um documento do PDF, verifique se os detalhes como nomes de autores e palavras-chave são precisos e completos.

#### Vídeo: adicionar metadados em massa aos ativos

>[!VIDEO](https://video.tv.adobe.com/v/3425978)

### Avaliar e melhorar a capacidade de pesquisa de metadados

Avalie sua estratégia de metadados para melhorar a capacidade de pesquisa de metadados. Simplifique os fluxos de trabalho e aprimore os recursos de pesquisa para obter uma reutilização eficiente. Evite lidar com metadados que não têm um propósito claro.

Você pode considerar as seguintes práticas recomendadas para otimizar a capacidade de pesquisa de metadados:

* **Otimização de palavra-chave:** melhore a pesquisabilidade de metadados otimizando palavras-chave associadas a ativos. Você pode melhorar a relevância de palavras-chave para ativos específicos no [!UICONTROL Assets Manager] seguindo estas etapas:

   1. Vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivo]** > **[!UICONTROL [Pasta de ativos]]**.
   1. Selecione o ativo para o qual deseja atualizar os metadados e clique em **[!UICONTROL Propriedades]**.
   1. Navegue até a guia **[!UICONTROL Avançado]** e clique em **[!UICONTROL Adicionar]** em **[!UICONTROL Elevar para palavras-chave de pesquisa]**. <br>Você deve usar o esquema de metadados padrão para elevar as palavras-chave de pesquisa.
   1. Insira a palavra-chave para a qual deseja impulsionar a pesquisa e clique em **[!UICONTROL Adicionar]**.<br>
Você pode adicionar várias palavras-chave e organizá-las de acordo com sua prioridade.
   1. Clique em **[!UICONTROL Salvar e fechar]**.
Pesquise o ativo usando as palavras-chave adicionadas. O ativo aparece entre os principais resultados da pesquisa.

  Saiba como [impulsionar a pesquisa no Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

* **Campos de metadados personalizados:** personalize seus campos de metadados para capturar informações adicionais sobre ativos. Por exemplo, adicione campos específicos para obter detalhes do projeto, informações de direitos autorais ou quaisquer outros dados relevantes que melhorem os recursos de pesquisa. Saiba [como editar ou adicionar metadados personalizados](meta-edit.md) no Experience Manager Assets.


* **Validação de metadados:** implemente verificações de validação para entradas de metadados para garantir consistência e precisão. Usar vocabulários controlados torna o processo de validação mais suave e diminui a chance de entradas indefinidas ou inconsistentes. Isso pode envolver a configuração de diretrizes para determinadas propriedades de metadados para evitar informações ambíguas ou inconsistentes.

* **Rastreamento de uso**: avalie a relevância e o uso de diferentes propriedades de metadados ao longo do tempo. Identifique e priorize metadados usados com frequência ou contribua significativamente para os processos de pesquisa e recuperação.

#### Vídeo: adicionar palavras-chave para melhorar a capacidade de pesquisa

>[!VIDEO](https://video.tv.adobe.com/v/3425979)

### Mantenha os metadados simples e fáceis de entender

Simplifique os metadados para melhorar a governança e a adoção pelos usuários. Mantenha-o simples e fácil de entender, incentivando os usuários a adicionar informações essenciais.
Experimente as seguintes práticas recomendadas para simplificar os metadados:

* **Otimizar opções de propriedade:** concentre-se em realçar propriedades essenciais sem sobrecarregar os usuários com campos de metadados demais para serem preenchidos. Por exemplo, ao adicionar metadados para uma imagem, inclua apenas campos principais como título, descrição e tags para uma categorização eficaz.

* **Elimine propriedades padrão desnecessárias:** simplifique o formulário de metadados eliminando propriedades padrão prontas para uso irrelevantes para o seu caso de uso. Remova as propriedades padrão raramente usadas para uma interface e experiência mais limpas.

* **Revise e atualize metadados periodicamente:** atualize metadados regularmente e adapte-se às necessidades e tecnologias em constante mudança para garantir que os usuários forneçam informações valiosas ao longo do tempo.

### Analisar jornada de conteúdo

Examine o conteúdo do supply chain para encontrar fontes de metadados e envolver todas as partes interessadas, começando pelo topo, para obter uma abordagem completa de práticas recomendadas. Envolva diferentes membros da equipe para garantir suporte completo em toda a organização. <br>Incorpore metadados em vários estágios para compartilhar a responsabilidade de fornecer detalhes do ativo durante o carregamento. Por exemplo, a integração do [!DNL Experience Manager Assets] e do [!DNL Workfront] oferece benefícios substanciais em termos de gerenciamento de metadados, aprimorando a eficiência e a colaboração na criação e no gerenciamento de conteúdo. Essa integração garante uma sincronização de metadados eficiente para ativos vinculados, atualizando automaticamente os detalhes do projeto quando alterações são feitas em [!DNL Workfront].

Comunicar antecipadamente os objetivos, os progressos, os marcos e os desafios para receber contribuições e cooperação de todas as partes interessadas. Estimule a colaboração em toda a organização para criar processos eficientes e metadados valiosos.

Saiba mais sobre [metadados e seus conceitos relacionados](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-concepts.html) para gerenciar efetivamente os metadados do Experience Manager.
