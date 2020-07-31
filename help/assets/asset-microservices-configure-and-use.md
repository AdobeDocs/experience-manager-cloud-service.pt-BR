---
title: Configurar e usar os microserviços de ativos para processamento de ativos
description: Saiba como configurar e usar os microserviços de ativos nativos na nuvem para processar ativos em escala.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f5ebd1ae28336e63d8f3a89d7519cf74b46a3bfd
workflow-type: tm+mt
source-wordcount: '2208'
ht-degree: 1%

---


# Usar microserviços e perfis de processamento de ativos {#get-started-using-asset-microservices}

<!--
* Current capabilities of asset microservices offered. If workers have names then list the names and give a one-liner description. (The feature-set is limited for now and continues to grow. So will this article continue to be updated.)
* How to access the microservices. UI. API. Is extending possible right now?
* Detailed list of what file formats and what processing is supported by which workflows/workers process.
* How/where can admins check what's already configured and provisioned.
* How to create new config or request for new provisioning/purchase.

* [DO NOT COVER?] Exceptions or limitations or link back to lack of parity with AEM 6.5.
-->

Os microserviços de ativos fornecem processamento escalonável e resiliente de ativos usando serviços em nuvem. O Adobe gerencia os serviços para uma manipulação otimizada de diferentes tipos de ativos e opções de processamento.

O processamento de ativos depende da configuração em Perfis **[!UICONTROL de]** processamento, que fornecem uma configuração padrão e permitem que um administrador adicione uma configuração de processamento de ativos mais específica. Os administradores podem criar e manter as configurações de workflows de pós-processamento, incluindo personalização opcional. Personalizar workflows permite extensibilidade e personalização completa.

Os microserviços de ativos permitem que você processe uma [ampla variedade de tipos](/help/assets/file-format-support.md) de arquivos que abrangem mais formatos prontos para uso do que o que é possível com as versões anteriores do Experience Manager. Por exemplo, a extração em miniatura dos formatos PSD e PSB agora é possível e exigia soluções de terceiros como o ImageMagick.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Uma visualização de alto nível de](assets/asset-microservices-flow.png "processamento de ativosUma visualização de alto nível de processamento de ativos")

>[!NOTE]
>
>O processamento de ativos descrito aqui substitui o modelo de `DAM Update Asset` fluxo de trabalho existente nas versões anteriores do [!DNL Experience Manager]. A maioria das etapas padrão de geração de representação e relacionadas a metadados são substituídas pelo processamento de microserviços de ativos, e as etapas restantes, se houver, podem ser substituídas pela configuração do fluxo de trabalho de pós-processamento.

## Compreender as opções de processamento de ativos {#get-started}

Experience Manager permite os seguintes níveis de processamento.

| Configuração | Descrição | Casos de uso cobertos |
|---|---|---|
| [Configuração padrão](#default-config) | Está disponível como está e não pode ser modificado. Essa configuração fornece recursos de geração de execução muito básicos. | Miniaturas padrão usadas pela interface [!DNL Assets] do usuário (48, 140 e 319 px); pré-visualização grande (execução na Web - 1280 px); Metadados e extração de texto. |
| [Configuração padrão](#standard-config) | Configurado pelos administradores somente pela interface do usuário. Fornece mais opções para a geração de representação do que a configuração padrão acima. | Alterar o formato e a resolução das imagens; gerar execuções FPO. |
| [Configuração personalizada](#custom-config) | Configurado pelos administradores por meio da interface do usuário para chamar trabalhadores personalizados que suportam requisitos mais complexos. Aproveita uma nuvem nativa [!DNL Asset Compute Service]. | Consulte casos [de uso](#custom-config)permitidos. |

Para criar perfis de processamento personalizados específicos às suas necessidades personalizadas, considere integrar-se a outros sistemas, consulte workflows [de](#post-processing-workflows)pós-processamento.

## Formatos de arquivo não suportados {#supported-file-formats}

Os microserviços de ativos oferecem suporte para uma grande variedade de formatos de arquivo em termos da capacidade de gerar execuções ou extrair metadados. Consulte os formatos [de arquivo](file-format-support.md) suportados para obter a lista completa.

## Configuração padrão {#default-config}

Alguns padrões são pré-configurados para garantir que as execuções padrão necessárias no Experience Manager estejam disponíveis. A configuração padrão também garante que as operações de extração de metadados e extração de texto estejam disponíveis. Os usuários podem fazer upload ou atualizar ativos imediatamente e o processamento básico está disponível por padrão.

Com a configuração padrão, somente o perfil de processamento mais básico é configurado. Esse perfil de processamento não é visível na interface do usuário e você não pode modificá-lo. Ele sempre é executado para processar ativos carregados. Esse perfil de processamento padrão garante que o processamento básico exigido por [!DNL Experience Manager] ele seja concluído em todos os ativos.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## perfil padrão {#standard-config}

[!DNL Experience Manager] forneça recursos para gerar renderizações mais específicas para formatos comuns, de acordo com as necessidades do usuário. Um administrador pode criar Perfis  de processamento adicionais para facilitar a criação dessa execução. Em seguida, os usuários atribuem um ou mais dos perfis disponíveis a pastas específicas para concluir o processamento adicional. Por exemplo, o processamento adicional pode gerar representações para Web, dispositivos móveis e tablets. O vídeo a seguir ilustra como criar e aplicar Perfis [!UICONTROL de] processamento e como acessar as execuções criadas.

* **Largura e altura** da representação: A especificação de largura e altura da representação fornece tamanhos máximos da imagem de saída gerada. Os microserviços de ativos tentam produzir a maior representação possível, que a largura e a altura não são maiores que a largura e a altura especificadas, respectivamente. A proporção é preservada, é a mesma do original. Um valor vazio significa que o processamento de ativos assume a dimensão em pixels do original.

* **Regras** de inclusão de tipo MIME: Quando um ativo com um tipo MIME específico é processado, o tipo MIME é verificado pela primeira vez em relação ao valor de tipos MIME excluídos para a especificação de representação. Se corresponder a essa lista, essa representação específica não será gerada para o ativo (lista de bloqueios). Caso contrário, o tipo MIME será verificado em relação ao tipo MIME incluído e, se ele corresponder à lista, a representação será gerada (lista de permissões).

* **Representação** especial do FPO: Ao colocar ativos de grande porte de [!DNL Experience Manager] dentro de [!DNL Adobe InDesign] documentos, um profissional criativo espera por um tempo substancial depois de [colocar um ativo](https://helpx.adobe.com/indesign/using/placing-graphics.html). Enquanto isso, o usuário está impedido de usar [!DNL InDesign]. Isso interrompe o fluxo criativo e afeta negativamente a experiência do usuário. O Adobe permite que as execuções de pequeno porte sejam colocadas temporariamente em [!DNL InDesign] documentos para começar, o que pode ser substituído por ativos de resolução completa sob demanda posteriormente. [!DNL Experience Manager] fornece execuções que são usadas apenas para posicionamento (FPO). Essas renderizações FPO têm um tamanho de arquivo pequeno, mas têm a mesma proporção.

O perfil de processamento pode incluir uma execução FPO (Somente para disposição). Consulte a [!DNL Adobe Asset Link] documentação [](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) para saber se você precisa ativá-la para o perfil de processamento. Para obter mais informações, consulte a documentação [completa do Link de ativo do](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)Adobe.

### Criar perfil padrão {#create-standard-profile}

Para criar um perfil de processamento padrão, siga estas etapas:

1. Os administradores acessam **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Perfis **** de processamento. Clique em **[!UICONTROL Criar]**.
1. Forneça um nome que o ajude a identificar exclusivamente o perfil ao se inscrever em uma pasta.
1. Para gerar execuções de FPO, na guia **[!UICONTROL Padrão]** , ative **[!UICONTROL Criar representação]** de FPO. Insira um valor de **[!UICONTROL Qualidade]** entre 1 e 100.
1. Para gerar outras representações, clique em **[!UICONTROL Adicionar novo]** e forneça as seguintes informações:

   * Nome de arquivo de cada representação.
   * Formato de arquivo (PNG, JPEG ou GIF) de cada execução.
   * Largura e altura em pixels de cada representação. Se os valores não forem especificados, o tamanho total de pixel da imagem original será usado.
   * Qualidade em porcentagem de cada execução JPEG.
   * Tipos MIME incluídos e excluídos para definir a aplicabilidade de um perfil.

   ![adição de perfis de processamento](assets/processing-profiles-adding.png)

1. Clique em **[!UICONTROL Salvar]**.

O vídeo a seguir demonstra a utilidade e o uso do perfil padrão.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

<!-- Removed per cqdoc-15624 request by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## perfil personalizado e casos de uso {#custom-config}

<!-- **TBD items**:

* Overall cross-linking with the extensibility content.
* Mention how to get URL of worker. Worker URL for Dev, Stage, and Prod environments.
* Mention mapping of service parameters. Link to compute service article.
* Review from flow perspective shared in Jira ticket.
-->

Alguns casos complexos de uso do processamento de ativos não podem ser realizados usando configurações padrão, pois as necessidades das organizações são variadas. Adobe ofertas [!DNL Asset Compute Service] para esses casos de uso. É um serviço escalonável e extensível para processar ativos digitais. Ele pode transformar imagens, vídeos, documentos e outros formatos de arquivo em diferentes representações, incluindo miniaturas, texto extraído e metadados e arquivos.

Os desenvolvedores podem usar o Asset Compute Service para criar funcionários personalizados especializados que atendam a casos de uso complexos e predefinidos. [!DNL Experience Manager] pode chamar esses funcionários personalizados da interface do usuário usando perfis personalizados configurados pelos administradores. [!DNL Asset Compute Service] apoia os seguintes casos de utilização de serviços externos:

* Chame [!DNL Adobe Photoshop] a API de recorte de imagem e salve o resultado como execução.
* Chame sistemas de terceiros para atualizar dados, por exemplo, um sistema PIM.
* Use a [!DNL Photoshop] API para gerar várias execuções com base no modelo da Photoshop.
* Use a [!DNL Adobe Lightroom] API para otimizar os ativos assimilados e salvá-los como execuções.

>[!NOTE]
>
>Não é possível editar os metadados padrão usando os trabalhadores personalizados. Você só pode modificar metadados personalizados.

### Criar um perfil personalizado {#create-custom-profile}

Para criar um perfil personalizado, siga estas etapas:

1. Os administradores acessam **[!UICONTROL Ferramentas > Ativos > Perfis]** de processamento. Clique em **[!UICONTROL Criar]**.
1. Click on **[!UICONTROL Custom]** tab. Clique em **[!UICONTROL Adicionar novo]**. Forneça o nome de arquivo desejado para a representação.
1. Forneça as seguintes informações e clique em **[!UICONTROL Salvar]**.

   * Nome de arquivo de cada execução e extensão de arquivo compatível.
   * URL de ponto final de um aplicativo personalizado Firefly. O aplicativo deve ser da mesma organização que a conta Experience Manager.
   * Adicione parâmetros de serviço, conforme necessário.
   * Tipos MIME incluídos e excluídos para definir a aplicabilidade de um perfil.

![perfil de processamento personalizado](assets/custom-processing-profile.png)

>[!CAUTION]
>
>Se o aplicativo Firefly e a [!DNL Experience Manager] conta não forem da mesma organização, a integração não funcionará.

## Usar perfis de processamento para processar ativos {#use-profiles}

Crie e aplique perfis de processamento adicionais e personalizados a pastas específicas para que o Experience Manager processe o processamento de ativos carregados ou atualizados nessas pastas. O perfil padrão de processamento padrão incorporado é sempre executado, mas não é visível na interface do usuário. Se você adicionar um perfil personalizado, ambos os perfis serão usados para processar os ativos carregados.

Aplique perfis de processamento a pastas usando um dos seguintes métodos:

* Os administradores podem selecionar uma definição de perfil de processamento em **[!UICONTROL Ferramentas > Ativos > Perfis]** de processamento e usar a ação **[!UICONTROL Aplicar Perfil às pastas]** . Ele abre um navegador de conteúdo que permite navegar para pastas específicas, selecioná-las e confirmar o aplicativo do perfil.
* Users can select a folder in the Assets user interface, use **[!UICONTROL Properties]** action to open folder properties screen, click on the **[!UICONTROL Processing Profiles]** tab, and in the popup list, select the correct processing profile for that folder. Para salvar as alterações, clique em **[!UICONTROL Salvar e fechar]**.

>[!NOTE]
>
>Somente um perfil de processamento pode ser aplicado a uma pasta específica. Para gerar mais execuções, adicione mais definições de execução ao perfil de processamento existente.

Depois que um perfil de processamento é aplicado a uma pasta, todos os novos ativos carregados (ou atualizados) nessa pasta ou em qualquer subpasta dela são processados usando o perfil de processamento adicional configurado. Esse processamento é adicionado ao perfil padrão. Se você aplicar vários perfis a uma pasta, os ativos carregados ou atualizados serão processados usando cada um desses perfis.

>[!NOTE]
>
>Um perfil de processamento aplicado a uma pasta funciona para a árvore inteira, mas pode ser substituído por outro perfil aplicado a uma subpasta. Quando os ativos são carregados em uma pasta, o Experience Manager verifica as propriedades da pasta que os contém para verificar se há um perfil de processamento. Se nenhum for aplicado, uma pasta pai na hierarquia será verificada para que um perfil de processamento seja aplicado.

Os usuários podem verificar se o processamento realmente ocorreu abrindo um ativo recém-carregado para o qual o processamento foi concluído, abrindo a pré-visualização de ativos e clicando na visualização **[!UICONTROL Representações]** do painel esquerdo. As representações específicas no perfil de processamento, para as quais o tipo de ativo específico corresponde às regras de inclusão do tipo MIME, devem estar visíveis e acessíveis.

![execuções adicionais](assets/renditions-additional-renditions.png)

*Figura: Exemplo de duas execuções adicionais geradas por um perfil de processamento aplicado à pasta pai.*

## workflows de pós-processamento {#post-processing-workflows}

Para situações em que é necessário um processamento adicional de ativos que não pode ser obtido usando os perfis de processamento, workflows adicionais pós-processamento podem ser adicionados à configuração. Isso permite adicionar processamento totalmente personalizado sobre o processamento configurável usando os microserviços de ativos.

Os workflows de pós-processamento, se configurados, são executados automaticamente por AEM após a conclusão do processamento dos microserviços. Não há necessidade de adicionar iniciadores de fluxo de trabalho manualmente para acioná-los. Os exemplos incluem:

* Etapas de fluxo de trabalho personalizadas para processar ativos.
* Integrações para adicionar metadados ou propriedades a ativos de sistemas externos, por exemplo, informações sobre produtos ou processos.
* Processamento adicional feito por serviços externos.

A adição de uma configuração de fluxo de trabalho de pós-processamento ao Experience Manager é composta das seguintes etapas:

* Crie um ou mais modelos de fluxo de trabalho. Os documentos o mencionam como modelos *de fluxo de trabalho de* pós-processamento, mas esses são modelos comuns de fluxo de trabalho de Experience Manager.
* Adicione etapas específicas do fluxo de trabalho a esses modelos. As etapas são executadas nos ativos com base em uma configuração de modelo de fluxo de trabalho.
* Adicione a etapa Processo [!UICONTROL Concluído do Fluxo de Trabalho de Atualização de Ativo do] DAM no final. Adicionar essa etapa garante que o Experience Manager saiba quando o processamento termina e que o ativo pode ser marcado como processado, ou seja, *Novo* é exibido no ativo.
* Crie uma configuração para o Serviço de Execução de Fluxo de Trabalho Personalizado que permita configurar a execução de um modelo de fluxo de trabalho de pós-processamento por um caminho (localização da pasta) ou por uma expressão regular.

### Criar modelos de fluxo de trabalho de pós-processamento {#create-post-processing-workflow-models}

Os modelos de fluxo de trabalho de pós-processamento são modelos regulares de fluxo de trabalho AEM. Crie modelos diferentes se precisar de processamento diferente para locais de repositório ou tipos de ativos diferentes.

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
>O console da Web OSGi, ao contrário das implantações de serviços no local e gerenciados de AEM, não está disponível diretamente nas implantações de serviços em nuvem.

Para obter detalhes sobre qual etapa de fluxo de trabalho padrão pode ser usada no fluxo de trabalho de pós-processamento, consulte as etapas do [fluxo de trabalho no fluxo de trabalho](developer-reference-material-apis.md#post-processing-workflows-steps) de pós-processamento na referência do desenvolvedor.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* Considere suas necessidades para todos os tipos de execuções ao projetar workflows. Se você não prever a necessidade de uma representação no futuro, remova a etapa de criação do fluxo de trabalho. As execuções não podem ser excluídas em massa depois. As representações indesejadas podem ocupar muito espaço no armazenamento após uso prolongado de [!DNL Experience Manager]. Para ativos individuais, você pode remover execuções manualmente da interface do usuário. Para vários ativos, você pode personalizar [!DNL Experience Manager] para excluir representações específicas ou excluir os ativos e carregá-los novamente.
* Atualmente, o suporte está limitado à geração de execuções. Não há suporte para a geração de novo ativo.
