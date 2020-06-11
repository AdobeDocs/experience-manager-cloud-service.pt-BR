---
title: Configurar e usar os microserviços de ativos para processamento de ativos
description: Saiba como configurar e usar os microserviços de ativos nativos na nuvem para processar ativos em escala.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 496ad0831d20eb7653a3c5727999a2abc5728ec7
workflow-type: tm+mt
source-wordcount: '1872'
ht-degree: 3%

---


# Introdução ao uso dos microsserviços de ativos {#get-started-using-asset-microservices}

<!--
* Current capabilities of asset microservices offered. If workers have names then list the names and give a one-liner description. (The feature-set is limited for now and continues to grow. So will this article continue to be updated.)
* How to access the microservices. UI. API. Is extending possible right now?
* Detailed list of what file formats and what processing is supported by which workflows/workers process.
* How/where can admins check what's already configured and provisioned.
* How to create new config or request for new provisioning/purchase.

* [DO NOT COVER?] Exceptions or limitations or link back to lack of parity with AEM 6.5.
-->

Os microserviços de ativos fornecem um processamento escalonável e resiliente de ativos usando serviços em nuvem. A Adobe gerencia os serviços para a melhor manipulação de diferentes tipos de ativos e opções de processamento.

O processamento de ativos depende da configuração em Perfis **[!UICONTROL de]** processamento, que fornecem uma configuração padrão e permitem que um administrador adicione uma configuração de processamento de ativos mais específica. Os administradores podem criar e manter as configurações de workflows de pós-processamento, incluindo personalização opcional. Personalizar workflows permite extensibilidade e personalização completa.

Os microserviços de ativos permitem que você processe uma [ampla variedade de tipos](/help/assets/file-format-support.md) de arquivos que abrangem mais formatos prontos para uso do que o que é possível com as versões anteriores do Experience Manager. Por exemplo, a extração em miniatura dos formatos PSD e PSB agora é possível e exigia soluções de terceiros como o ImageMagick.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Uma visualização de alto nível de](assets/asset-microservices-flow.png "processamento de ativosUma visualização de alto nível de processamento de ativos")

>[!NOTE]
>
> O processamento de ativos descrito aqui substitui o modelo de `DAM Update Asset` fluxo de trabalho existente nas versões anteriores do Experience Manager. A maioria das etapas padrão de geração de representação e relacionadas a metadados são substituídas pelo processamento de microserviços de ativos, e as etapas restantes, se houver, podem ser substituídas pela configuração do fluxo de trabalho de pós-processamento.

## Introdução ao processamento de ativos {#get-started}

O processamento de ativos com microserviços de ativos é pré-configurado com uma configuração padrão, garantindo que as execuções padrão exigidas pelo sistema estejam disponíveis. Ela também garante que as operações de extração de metadados e extração de texto estejam disponíveis. Os usuários podem fazer upload ou atualizar ativos imediatamente e o processamento básico está disponível por padrão.

Para os requisitos específicos de geração de representação ou processamento de ativos, um administrador do AEM pode criar Perfis [!UICONTROL de]processamento adicionais. Os usuários podem atribuir um ou mais perfis disponíveis a pastas específicas para realizar um processamento adicional. Por exemplo, para gerar execuções específicas para Web, dispositivos móveis e tablets. O vídeo a seguir ilustra como criar e aplicar Perfis [!UICONTROL de] processamento e como acessar as execuções criadas.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

Para alterar o perfil existente, consulte [Configurações para os microserviços](#configure-asset-microservices)de ativos.
Para criar perfis de processamento personalizados específicos às suas necessidades personalizadas, considere integrar-se a outros sistemas, consulte workflows [de](#post-processing-workflows)pós-processamento.

## Configurações para microserviços de ativos {#configure-asset-microservices}

Para configurar os microserviços de ativos, os administradores podem usar a interface de usuário de configuração em **[!UICONTROL Ferramentas > Ativos > Perfis]** de processamento.

### Configuração padrão {#default-config}

Com a configuração padrão, somente o perfil de processamento padrão é configurado. O perfil de processamento padrão não está visível na interface do usuário e você não pode modificá-lo. Ele sempre é executado para processar ativos carregados. Um perfil de processamento padrão garante que todo o processamento básico exigido pelo Experience Manager seja concluído em todos os ativos.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png) -->

O perfil de processamento padrão fornece a seguinte configuração de processamento:

* Miniaturas padrão usadas pela interface do usuário do Ativo (48, 140 e 319 px)
* pré-visualização grande (execução na Web - 1280 px)
* Extração de metadados
* extração de texto

### Formatos de arquivo não suportados {#supported-file-formats}

Os microserviços de ativos oferecem suporte para uma grande variedade de formatos de arquivo em termos da capacidade de gerar execuções ou extrair metadados. Consulte os formatos [de arquivo](file-format-support.md) suportados para obter a lista completa.

### Adicionar perfis de processamento adicionais {#processing-profiles}

perfis de processamento adicionais podem ser adicionados usando a ação **[!UICONTROL Criar]** .

Cada configuração de perfil de processamento inclui uma lista de execuções. Para cada representação, você pode especificar o seguinte:

* Nome da representação.
* Formato de representação compatível, como JPEG, PNG ou GIF.
* Largura e altura da representação em pixels. Se não for especificado, o tamanho total de pixel da imagem original será usado.
* Qualidade de execução de JPEG em porcentagem.
* Tipos MIME incluídos e excluídos para definir a aplicabilidade de um perfil.

![adição de perfis de processamento](assets/processing-profiles-adding.png)

Quando você cria e salva um novo perfil de processamento, ele é adicionado à lista dos perfis de processamento configurados. Você pode aplicar esses perfis de processamento a pastas na hierarquia de pastas para torná-las eficazes para uploads de ativos e processamento de ativos.

<!-- Removed per cqdoc-15624 request by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) -->

#### Largura e altura da representação {#rendition-width-height}

A especificação de largura e altura da representação fornece tamanhos máximos da imagem de saída gerada. O microserviço de ativos tenta produzir a maior representação possível, que a largura e a altura não são maiores que a largura e a altura especificadas, respectivamente. A proporção é preservada, é a mesma do original.

Um valor vazio significa que o processamento de ativos assume a dimensão em pixels do original.

#### Regras de inclusão de tipo MIME {#mime-type-inclusion-rules}

Quando um ativo com um tipo MIME específico é processado, o tipo MIME é verificado pela primeira vez em relação ao valor de tipos MIME excluídos para a especificação de representação. Se corresponder a essa lista, essa representação específica não será gerada para o ativo (lista bloqueada).

Caso contrário, o tipo MIME será verificado em relação ao tipo MIME incluído e, se ele corresponder à lista, a representação será gerada (lista permitida).

#### Representação especial do FPO {#special-fpo-rendition}

Ao colocar ativos de grande porte do AEM em documentos do Adobe InDesign, um profissional criativo deve aguardar por um tempo significativo depois de [colocar um ativo](https://helpx.adobe.com/indesign/using/placing-graphics.html). Enquanto isso, o usuário é impedido de usar o InDesign. Isso interrompe o fluxo criativo e afeta negativamente a experiência do usuário. A Adobe permite que execuções de pequeno porte sejam temporariamente colocadas em documentos do InDesign, que podem ser substituídas por ativos de resolução completa sob demanda posteriormente. O Experience Manager fornece execuções que são usadas apenas para posicionamento (FPO). Essas renderizações FPO têm um tamanho de arquivo pequeno, mas têm a mesma proporção.

O perfil de processamento pode incluir uma execução FPO (Somente para disposição). Consulte a [documentação](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) do Adobe Asset Link para saber se você precisa ativá-lo para o perfil de processamento. Para obter mais informações, consulte a documentação [completa do Link de ativos](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)da Adobe.

## Usar microserviços de ativos para processar ativos {#use-asset-microservices}

Crie e aplique perfis de processamento adicionais e personalizados a pastas específicas para que o Experience Manager processe o processamento de ativos carregados ou atualizados nessas pastas. O perfil padrão de processamento padrão incorporado é sempre executado, mas não é visível na interface do usuário. Se você adicionar um perfil personalizado, ambos os perfis serão usados para processar os ativos carregados.

Há duas maneiras de aplicar perfis de processamento a pastas:

* Os administradores podem selecionar uma definição de perfil de processamento em **[!UICONTROL Ferramentas > Ativos > Perfis]** de processamento e usar a ação **[!UICONTROL Aplicar Perfil às pastas]** . Ele abre um navegador de conteúdo que permite navegar para pastas específicas, selecioná-las e confirmar o aplicativo do perfil.
* Os usuários podem selecionar uma pasta na interface do usuário do Assets, usar a ação **[!UICONTROL Propriedades]** para abrir a tela de propriedades da pasta, clicar na guia **[!UICONTROL Perfis de processamento]** e, na lista suspensa, selecionar o perfil de processamento correto para essa pasta. A escolha será salva após a ação **[!UICONTROL Salvar e fechar]**.

>[!NOTE]
>
>Somente um perfil de processamento pode ser aplicado a uma pasta específica. Se você precisar de mais execuções geradas, é possível adicionar mais definições de execução ao perfil de processamento.

Depois que um perfil de processamento é aplicado a uma pasta, todos os novos ativos carregados (ou atualizados) nessa pasta ou em qualquer subpasta dela são processados usando o perfil de processamento adicional configurado. Esse processamento adicional é adicionado ao perfil padrão. Se você aplicar vários perfis a uma pasta, os ativos carregados ou atualizados serão processados usando cada um desses perfis.

>[!NOTE]
>
>Quando os ativos são carregados em uma pasta, o Experience Manager verifica as propriedades da pasta que os contém em busca de um perfil de processamento. Se nenhum for aplicado, ele sobe na árvore de pastas até encontrar um perfil de processamento aplicado e o usa para o ativo. Isso significa que um perfil de processamento aplicado a uma pasta funciona para a árvore inteira, mas pode ser substituído por outro perfil aplicado a uma subpasta.

Os usuários podem verificar se o processamento realmente ocorreu abrindo um ativo recém-carregado para o qual o processamento foi concluído, abrindo a pré-visualização de ativos e clicando na visualização **[!UICONTROL Representações]** do painel esquerdo. As representações específicas no perfil de processamento, para as quais o tipo de ativo específico corresponde às regras de inclusão do tipo MIME, devem estar visíveis e acessíveis.

![execuções adicionais](assets/renditions-additional-renditions.png)*Figura: Exemplo de duas execuções adicionais geradas por um perfil de processamento aplicado à pasta pai*

## workflows de pós-processamento {#post-processing-workflows}

Para situações em que é necessário um processamento adicional de ativos que não pode ser obtido usando os perfis de processamento, workflows adicionais pós-processamento podem ser adicionados à configuração. Isso permite adicionar processamento totalmente personalizado sobre o processamento configurável usando os microserviços de ativos.

Os workflows de pós-processamento, se configurados, são executados automaticamente pelo AEM após a conclusão do processamento dos microserviços. Não há necessidade de adicionar iniciadores de fluxo de trabalho manualmente para acioná-los.

Os exemplos incluem:

* etapas de fluxo de trabalho personalizadas para processar ativos, por exemplo, código Java para gerar representações de formatos de arquivo proprietários.
* integrações para adicionar metadados ou propriedades a ativos de sistemas externos, por exemplo, informações sobre produtos ou processos.
* processamento adicional feito por serviços externos

A adição de uma configuração de fluxo de trabalho de pós-processamento ao Experience Manager é composta das seguintes etapas:

* Criação de um ou mais modelos de fluxo de trabalho. Chamaremos a eles &quot;modelos de fluxo de trabalho de pós-processamento&quot;, mas eles são modelos de fluxo de trabalho AEM comuns.
* Adicionando etapas específicas do fluxo de trabalho a esses modelos. Essas etapas serão executadas nos ativos com base na configuração do modelo de fluxo de trabalho.
* O último passo desse modelo deve ser o `DAM Update Asset Workflow Completed Process` passo. Isso é necessário para garantir que o AEM saiba que o processamento terminou e que o ativo pode ser marcado como processado (&quot;Novo&quot;)
* Criando uma configuração para o Serviço do Executador de Fluxo de Trabalho Personalizado, que permite configurar a execução de um modelo de fluxo de trabalho de pós-processamento por caminho (localização da pasta) ou expressão regular

### Criar modelos de fluxo de trabalho de pós-processamento {#create-post-processing-workflow-models}

Os modelos de fluxo de trabalho de pós-processamento são modelos de fluxo de trabalho AEM comuns. Crie modelos diferentes se precisar de processamento diferente para locais de repositório ou tipos de ativos diferentes.

As etapas de processamento devem ser adicionadas com base nas necessidades. Você pode usar quaisquer etapas compatíveis disponíveis, bem como quaisquer etapas de fluxo de trabalho implementadas por personalização.

Verifique se a última etapa de cada workflows de pós-processamento está `DAM Update Asset Workflow Completed Process`. A última etapa ajuda a garantir que o Experience Manager saiba quando o processamento de ativos é concluído.

### Configurar a execução do fluxo de trabalho pós-processamento {#configure-post-processing-workflow-execution}

Para configurar os modelos de fluxo de trabalho de pós-processamento a serem executados para ativos carregados ou atualizados no sistema após a conclusão do processamento dos microserviços de ativos, o serviço do Custom Workflow Runner precisa ser configurado.

O serviço de Executador de Fluxo de Trabalho Personalizado (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) é um serviço OSGi e fornece duas opções para configuração:

* workflows de pós-processamento por caminho (`postProcWorkflowsByPath`): Vários modelos de fluxo de trabalho podem ser listados, com base em diferentes caminhos de repositório. Caminhos e modelos devem ser separados por dois pontos. Caminhos de repositório simples são suportados e devem ser mapeados para um modelo de fluxo de trabalho no `/var` caminho. Por exemplo: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* workflows de pós-processamento por expressão (`postProcWorkflowsByExpression`): Vários modelos de fluxo de trabalho podem ser listados, com base em diferentes expressões regulares. Expressões e modelos devem ser separados por dois pontos. A expressão regular deve apontar diretamente para o nó Ativo, e não para uma das execuções ou arquivos. Por exemplo: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>A configuração do Custom Workflow Runner é uma configuração de um serviço OSGi. Consulte [implantar no Experience Manager](/help/implementing/deploying/overview.md) para obter informações sobre como implantar uma configuração OSGi.
> O console da Web do OSGi, ao contrário das implantações de serviços locais e gerenciados do AEM, não está disponível diretamente nas implantações de serviços em nuvem.

Para obter detalhes sobre qual etapa de fluxo de trabalho padrão pode ser usada no fluxo de trabalho de pós-processamento, consulte as etapas do [fluxo de trabalho no fluxo de trabalho](developer-reference-material-apis.md#post-processing-workflows-steps) de pós-processamento na referência do desenvolvedor.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* Considere suas necessidades para todos os tipos de execuções ao projetar workflows. Se você não prever a necessidade de uma representação no futuro, remova a etapa de criação do fluxo de trabalho. As execuções não podem ser excluídas em massa depois. As representações indesejadas podem ocupar muito espaço no armazenamento após uso prolongado de [!DNL Experience Manager]. Para ativos individuais, você pode remover execuções manualmente da interface do usuário. Para vários ativos, você pode personalizar [!DNL Experience Manager] para excluir representações específicas ou excluir os ativos e carregá-los novamente.
