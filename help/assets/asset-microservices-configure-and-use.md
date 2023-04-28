---
title: Configurar e usar microsserviços de ativos
description: Configure e use os microsserviços de ativos nativos em nuvem para processar ativos em escala.
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Asset Processing
role: Architect,Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '2932'
ht-degree: 3%

---

# Usar microsserviços de ativos e perfis de processamento {#get-started-using-asset-microservices}

Os microsserviços de ativos oferecem processamento escalável e resiliente de ativos usando aplicativos nativos em nuvem (também chamados de trabalhadores). O Adobe gerencia os serviços para obter o tratamento ideal de diferentes tipos de ativos e opções de processamento.

Os microsserviços de ativos permitem processar um [grande variedade de tipos de arquivos](/help/assets/file-format-support.md) cobrindo mais formatos prontos para uso do que o possível com versões anteriores do [!DNL Experience Manager]. Por exemplo, a extração em miniatura de formatos PSD e PSB agora é possível, mas era exigida anteriormente por soluções de terceiros, como [!DNL ImageMagick].

O processamento de ativos depende da configuração em **[!UICONTROL Processando perfis]**. O Experience Manager oferece uma configuração básica padrão e permite que os administradores adicionem configurações mais específicas de processamento de ativos. Os administradores criam, mantêm e modificam as configurações dos fluxos de trabalho de pós-processamento, incluindo a personalização opcional. Personalizar os fluxos de trabalho permite que os desenvolvedores estendam a oferta padrão.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Uma exibição de alto nível do processamento de ativos](assets/asset-microservices-flow.png "Uma exibição de alto nível do processamento de ativos")

>[!NOTE]
>
>O processamento de ativos descrito aqui substitui a variável `DAM Update Asset` modelo de fluxo de trabalho que existe nas versões anteriores do [!DNL Experience Manager]. A maioria das etapas de geração de representação padrão e relacionadas a metadados é substituída pelo processamento de microsserviços de ativos e as etapas restantes, se houver, podem ser substituídas pela configuração de fluxo de trabalho de pós-processamento.

## Compreender as opções de processamento de ativos {#get-started}

[!DNL Experience Manager] O permite os seguintes níveis de processamento.

| Opção | Descrição | Casos de uso cobertos |
|---|---|---|
| [Configuração padrão](#default-config) | Está disponível como está e não pode ser modificado. Essa configuração fornece recursos de geração de representação muito básicos. | <ul> <li>Miniaturas padrão usadas por [!DNL Assets] interface do usuário (48, 140 e 319 pixels) </li> <li> Visualização grande (renderização da Web - 1280 pixels) </li><li> Metadados e extração de texto.</li></ul> |
| [Configuração personalizada](#standard-config) | Configurado pelos administradores pela interface do usuário. Fornece mais opções para geração de representação estendendo a opção padrão. Estenda a opção pronta para uso para fornecer diferentes formatos e representações. | <ul><li>Representação de FPO. </li> <li>Alterar o formato do arquivo e a resolução das imagens</li> <li> Aplicar condicionalmente a tipos de arquivo configurados. </li> </ul> |
| [Perfil personalizado](#custom-config) | Configurado pelos administradores por meio da interface do usuário para usar código personalizado por meio de aplicativos personalizados para chamar [Serviço Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html). Suporta requisitos mais complexos em um método nativo em nuvem e dimensionável. | Consulte [casos de uso permitidos](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Formatos de arquivo não compatíveis {#supported-file-formats}

Os microsserviços de ativos oferecem suporte para uma grande variedade de formatos de arquivo para processar, gerar representações ou extrair metadados. Consulte [formatos de arquivo compatíveis](file-format-support.md) para obter a lista completa de tipos MIME e a funcionalidade suportada para cada tipo.

## Configuração padrão {#default-config}

Alguns padrões são pré-configurados para garantir que as renderizações padrão necessárias no Experience Manager estejam disponíveis. A configuração padrão também garante que as operações de extração de metadados e extração de texto estejam disponíveis. Os usuários podem começar a fazer upload ou atualizar ativos imediatamente e o processamento básico está disponível por padrão.

Com a configuração padrão, somente o perfil de processamento mais básico é configurado. Esse perfil de processamento não está visível na interface do usuário e você não pode modificá-lo. Ele sempre é executado para processar ativos carregados. Esse perfil de processamento padrão garante que o processamento básico exigido por [!DNL Experience Manager] é concluída em todos os ativos.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Configuração padrão {#standard-config}

[!DNL Experience Manager] forneça recursos para gerar representações mais específicas para formatos comuns, de acordo com as necessidades do usuário. Um administrador pode criar [!UICONTROL Processando perfis] para facilitar essa criação de rendições. Em seguida, os usuários atribuem um ou mais perfis disponíveis a pastas específicas para realizar o processamento adicional. Por exemplo, o processamento adicional pode gerar representações para Web, dispositivos móveis e tablets. O vídeo a seguir ilustra como criar e aplicar [!UICONTROL Processando perfis] e como acessar as representações criadas.

* **Largura e altura da representação**: A especificação de largura e altura da representação fornece tamanhos máximos da imagem de saída gerada. Os microsserviços de ativos tentam produzir a maior representação possível, que largura e altura não são maiores que a largura e a altura especificadas, respectivamente. A proporção é preservada, ou seja, a mesma do original. Um valor vazio significa que o processamento de ativos assume a dimensão de pixel do original.

* **Regras de inclusão do tipo MIME**: Quando um ativo com um tipo MIME específico é processado, o tipo MIME é verificado primeiro em relação ao valor de tipos MIME excluídos para a especificação de representação. Se corresponder a essa lista, essa representação específica não será gerada para o ativo (lista de bloqueios). Caso contrário, o tipo MIME será verificado em relação ao tipo MIME incluído e, se corresponder à lista, a representação será gerada (lista de permissões).

* **Representação especial de FPO**: Ao colocar ativos de grande porte da [!DNL Experience Manager] em [!DNL Adobe InDesign] documentos, um profissional criativo espera por um tempo substancial depois que [colocar um ativo](https://helpx.adobe.com/indesign/using/placing-graphics.html). Enquanto isso, o usuário está bloqueado de usar [!DNL InDesign]. Isso interrompe o fluxo criativo e afeta negativamente a experiência do usuário. O Adobe permite colocar temporariamente representações de pequeno porte no [!DNL InDesign] documentos para começar, que podem ser substituídos por ativos de resolução completa sob demanda posteriormente. [!DNL Experience Manager] O fornece representações que são usadas somente para posicionamento (FPO). Essas renderizações de FPO têm um tamanho de arquivo pequeno, mas têm a mesma proporção.

O perfil de processamento pode incluir uma representação FPO (Somente para posicionamento). Consulte [!DNL Adobe Asset Link] [documentação](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) para entender se é necessário ativá-lo para o perfil de processamento. Para obter mais informações, consulte [Documentação completa do Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html).

### Criar um perfil padrão {#create-standard-profile}

Para criar um perfil de processamento padrão, siga estas etapas:

1. Acesso dos administradores **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Processando perfis]**. Clique em **[!UICONTROL Criar]**.
1. Forneça um nome que ajude você a identificar o perfil exclusivamente ao se aplicar a uma pasta.
1. Para gerar representações FPO, no **[!UICONTROL Imagem]** guia , habilitar **[!UICONTROL Criar representação FPO]**. Insira um **[!UICONTROL Qualidade]** entre 1 e 100.
1. Para gerar outras representações, clique em **[!UICONTROL Adicionar novo]** e fornecer as seguintes informações:

   * Nome do arquivo de cada representação.
   * Formato de arquivo (PNG, JPEG, GIF ou WebP) de cada renderização.
   * Largura e altura em pixels de cada representação. Se os valores não forem especificados, será usado o tamanho total de pixel da imagem original.
   * Qualidade em porcentagem de cada JPEG e renderização de WebP.
   * Tipos MIME incluídos e excluídos para definir a aplicabilidade de um perfil.

   ![perfis de processamento-adição](assets/processing-profiles-image.png)

1. Clique em **[!UICONTROL Salvar]**.

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## Perfil personalizado e casos de uso {#custom-config}

O [!DNL Asset Compute Service] O suporta uma variedade de casos de uso, como processamento padrão, formatos específicos de Adobe como arquivos Photoshop e implementação de processamento personalizado ou específico da organização. A personalização do fluxo de trabalho do Ativo de atualização DAM necessária no passado é manipulada automaticamente ou por meio da configuração de perfis de processamento. Se as necessidades comerciais não forem atendidas por essas opções de processamento, o Adobe recomenda desenvolver e usar [!DNL Asset Compute Service] para estender os recursos padrão. Para obter uma visão geral, consulte [entenda a extensibilidade e quando usá-la](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).

>[!NOTE]
>
>O Adobe recomenda usar um aplicativo personalizado somente quando os requisitos comerciais não puderem ser alcançados usando as configurações padrão ou o perfil padrão.

Ele pode transformar imagens, vídeos, documentos e outros formatos de arquivo em diferentes representações, incluindo miniaturas, texto e metadados extraídos e arquivos.

Os desenvolvedores podem usar o [!DNL Asset Compute Service] para [criar aplicativos personalizados](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) para os casos de uso suportados. [!DNL Experience Manager] O pode chamar esses aplicativos personalizados da interface do usuário usando perfis personalizados configurados pelos administradores. [!DNL Asset Compute Service] O suporta os seguintes casos de uso de invocar serviços externos:

* Use [!DNL Adobe Photoshop]&#39;s [API ImageCutout](https://developer.adobe.com/photoshop/photoshop-api-docs/) e salve o resultado como representação.
* Chame sistemas de terceiros para atualizar dados, por exemplo, um sistema PIM.
* Use [!DNL Photoshop] API para gerar várias representações com base no modelo do Photoshop.
* Use [API do Adobe Lightroom](https://developer.adobe.com/photoshop/photoshop-api-docs/) para otimizar os ativos assimilados e salvá-los como representações.

>[!NOTE]
>
>Não é possível editar os metadados padrão usando os aplicativos personalizados. Você só pode modificar metadados personalizados.

### Criar um perfil personalizado {#create-custom-profile}

Para criar um perfil personalizado, siga estas etapas:

1. Acesso dos administradores **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Processando perfis]**. Clique em **[!UICONTROL Criar]**.
1. Clique em **[!UICONTROL Personalizado]** guia . Clique em **[!UICONTROL Adicionar novo]**. Forneça o nome de arquivo desejado para a representação.
1. Forneça as seguintes informações.

   * Nome do arquivo de cada renderização e uma extensão de arquivo compatível.
   * [URL de ponto final de um aplicativo personalizado do App Builder](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html). O aplicativo deve ser da mesma organização da conta do Experience Manager.
   * Adicionar parâmetros de serviço a [transmitir informações ou parâmetros adicionais ao aplicativo personalizado](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend).
   * Tipos MIME incluídos e excluídos para limitar o processamento a alguns formatos de arquivo específicos.

   Clique em **[!UICONTROL Salvar]**.

Os aplicativos personalizados não têm cabeça [Construtor de aplicativos do projeto](https://developer.adobe.com/app-builder/docs/overview/) aplicativos. Seu aplicativo personalizado obtém todos os arquivos fornecidos se eles estiverem configurados com um perfil de processamento. O aplicativo deve filtrar os arquivos.

>[!CAUTION]
>
>Se o aplicativo App Builder e [!DNL Experience Manager] não forem da mesma organização, a integração não funcionará.

### Um exemplo de um perfil personalizado {#custom-profile-example}

Para ilustrar o uso do perfil personalizado, vamos considerar um caso de uso para aplicar texto personalizado às imagens da campanha. Você pode criar um perfil de processamento que aproveite a API do Photoshop para editar as imagens.

A integração do Asset compute Service permite que o Experience Manager transmita esses parâmetros para o aplicativo personalizado usando o [!UICONTROL Parâmetros de serviço] campo. O aplicativo personalizado chama a API do Photoshop e transmite esses valores para a API. Por exemplo, é possível passar o nome da fonte, a cor do texto, o peso do texto e o tamanho do texto para adicionar o texto personalizado às imagens da campanha.

<!-- TBD: Check screenshot against the interface. -->

![perfil de processamento personalizado](assets/custom-processing-profile.png)

*Figura: Use [!UICONTROL Parâmetros de serviço] para transmitir informações adicionadas aos parâmetros predefinidos criados no aplicativo personalizado. Neste exemplo, quando imagens da campanha são carregadas, as imagens são atualizadas com `Jumanji` texto em `Arial-BoldMT` fonte.*

## Usar perfis de processamento para processar ativos {#use-profiles}

Crie e aplique perfis de processamento adicionais e personalizados a pastas específicas para que o Experience Manager processe ativos carregados ou atualizados nessas pastas. O perfil de processamento padrão integrado é sempre executado, mas não é visível na interface do usuário. Se você adicionar um perfil personalizado, ambos os perfis serão usados para processar os ativos carregados.

Aplique perfis de processamento a pastas usando um dos seguintes métodos:

* Os administradores podem selecionar uma definição de perfil de processamento em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Processando perfis]** e use **[!UICONTROL Aplicar perfil às pastas]** ação. Ele abre um navegador de conteúdo que permite navegar para pastas específicas, selecioná-las e confirmar o aplicativo do perfil.
* Os usuários podem selecionar uma pasta na interface do usuário do Assets, usar **[!UICONTROL Propriedades]** para abrir a tela de propriedades da pasta, clique no botão **[!UICONTROL Processamento de ativos]** e na guia [!UICONTROL Perfil de processamento] selecione o perfil de processamento apropriado para essa pasta. Para salvar as alterações, clique em **[!UICONTROL Salvar e fechar]**.
   ![Aplicar perfil de processamento a uma pasta na guia Propriedades do ativo](assets/folder-properties-processing-profile.png)

* Os usuários podem selecionar pastas ou ativos específicos na interface do usuário do Assets para aplicar um perfil de processamento e, em seguida, selecionar ![ícone de reprocessamento de ativos](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL Reprocessar ativos]** nas opções disponíveis na parte superior.

>[!TIP]
>
>Somente um perfil de processamento pode ser aplicado a uma pasta. Para gerar mais representações, adicione mais definições de representação ao perfil de processamento existente.

Depois que um perfil de processamento é aplicado a uma pasta, todos os novos ativos carregados (ou atualizados) nessa pasta ou em qualquer uma de suas subpastas são processados usando o perfil de processamento adicional configurado. Esse processamento é executado em adição ao do perfil padrão.

>[!NOTE]
>
>Um perfil de processamento aplicado a uma pasta funciona para a árvore inteira, mas pode ser substituído por outro perfil aplicado a uma subpasta. Quando os ativos são carregados em uma pasta, o Experience Manager verifica as propriedades da pasta contêiner em busca de um perfil de processamento. Se nenhum for aplicado, uma pasta principal na hierarquia será verificada em busca de um perfil de processamento para ser aplicado.

Para verificar se os ativos são processados, visualize as renderizações geradas no [!UICONTROL Representações] no painel esquerdo. Abra a visualização de ativos e abra o painel à esquerda para acessar o **[!UICONTROL Representações]** exibir. As representações específicas no perfil de processamento, para as quais o tipo de ativo específico corresponde às regras de inclusão do tipo MIME, devem ser visíveis e acessíveis.

![representações adicionais](assets/renditions-additional-renditions.png)

*Figura: Exemplo de duas representações adicionais geradas por um perfil de processamento aplicado à pasta pai.*

## Fluxos de trabalho de pós-processamento {#post-processing-workflows}

Para uma situação em que é necessário um processamento adicional de ativos que não pode ser obtido usando os perfis de processamento, é possível adicionar mais workflows pós-processamento à configuração. O pós-processamento permite que você adicione processamento totalmente personalizado sobre o processamento configurável usando microsserviços de ativos.

Fluxos de trabalho de pós-processamento ou [Fluxo de trabalho de início automático](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/auto-start-workflows.html), se configuradas, são executadas automaticamente por [!DNL Experience Manager] após a conclusão do processamento de microsserviços. Não há necessidade de adicionar iniciadores de fluxo de trabalho manualmente para acionar os fluxos de trabalho. Os exemplos incluem:

* Etapas de fluxo de trabalho personalizadas para processar ativos.
* Integrações para adicionar metadados ou propriedades a ativos de sistemas externos, por exemplo, informações de produto ou processo.
* Processamento adicional feito por serviços externos.

Para adicionar uma configuração de fluxo de trabalho de pós-processamento ao [!DNL Experience Manager]siga estas etapas:

* Crie um ou mais modelos de fluxo de trabalho. Esses modelos personalizados são chamados de *modelos de fluxo de trabalho de pós-processamento* nesta documentação. Esses [!DNL Experience Manager] modelos de fluxo de trabalho.
* Adicione as etapas de fluxo de trabalho necessárias a esses modelos. Revise as etapas do fluxo de trabalho padrão e adicione todas as etapas padrão necessárias ao fluxo de trabalho personalizado. As etapas são executadas nos ativos com base em uma configuração de modelo de fluxo de trabalho. Por exemplo, se você deseja que a marcação inteligente ocorra automaticamente após o upload do ativo, adicione a etapa ao modelo de fluxo de trabalho de pós-processamento personalizado.
* Adicionar [!UICONTROL Processo Concluído do Fluxo de Trabalho de Ativos de Atualização do DAM] no final. Adicionar essa etapa garante que o Experience Manager saiba quando o processamento termina e que o ativo pode ser marcado como processado, ou seja, *Novo* é exibido no ativo.
* Crie uma configuração para o Custom Workflow Runner Service que permite configurar a execução de um modelo de fluxo de trabalho de pós-processamento por um caminho (local da pasta) ou por uma expressão regular.

Para obter detalhes sobre qual etapa de fluxo de trabalho padrão pode ser usada no fluxo de trabalho de pós-processamento, consulte [etapas do fluxo de trabalho no fluxo de trabalho de pós-processamento](developer-reference-material-apis.md#post-processing-workflows-steps) na referência do desenvolvedor.

### Criar modelos de fluxo de trabalho de pós-processamento {#create-post-processing-workflow-models}

Os modelos de fluxo de trabalho de pós-processamento são regulares [!DNL Experience Manager] modelos de fluxo de trabalho. Crie modelos diferentes se precisar de processamento diferente para locais de repositório ou tipos de ativos diferentes.

As etapas de processamento são adicionadas conforme necessário. Você pode usar ambas as etapas, as etapas compatíveis e todas as etapas de fluxo de trabalho implementadas de forma personalizada.

Certifique-se de que a última etapa de cada fluxo de trabalho de pós-processamento seja `DAM Update Asset Workflow Completed Process`. A última etapa ajuda a garantir que o Experience Manager saiba quando o processamento de ativos é concluído.

### Configurar a execução do workflow de pós-processamento {#configure-post-processing-workflow-execution}

Depois que os microsserviços de ativos concluírem o processamento dos ativos carregados, você poderá definir um fluxo de trabalho de pós-processamento para processar ainda mais os ativos. Para configurar o pós-processamento usando modelos de fluxo de trabalho, você pode executar um dos seguintes procedimentos:

* [Aplicar um modelo de fluxo de trabalho em Propriedades da pasta](#apply-workflow-model-to-folder).
* [Configurar o serviço de Execução de Fluxo de Trabalho Personalizado](#configure-custom-workflow-runner-service).

#### Aplicar um modelo de fluxo de trabalho a uma pasta {#apply-workflow-model-to-folder}

Para casos de uso típicos de pós-processamento, considere usar o método para aplicar um fluxo de trabalho a uma pasta. Para aplicar um modelo de fluxo de trabalho na pasta [!UICONTROL Propriedades]siga estas etapas:

1. Crie um modelo de fluxo de trabalho.
1. Selecione uma pasta e clique em **[!UICONTROL Propriedades]** na barra de ferramentas e, em seguida, clique em **[!UICONTROL Processamento de ativos]** guia .
1. Em **[!UICONTROL Fluxo de trabalho de início automático]**, selecione o fluxo de trabalho necessário, forneça um título para o fluxo de trabalho e salve as alterações.

   ![Aplicar um fluxo de trabalho de pós-processamento a uma pasta em suas Propriedades](assets/post-processing-profile-workflow-for-folders.png)

#### Configurar o serviço de Execução de Fluxo de Trabalho Personalizado {#configure-custom-workflow-runner-service}

Você pode configurar o serviço de execução do fluxo de trabalho personalizado para as configurações avançadas que não podem ser cumpridas aplicando um fluxo de trabalho a uma pasta. Por exemplo, um workflow que usa uma expressão regular. O Adobe CQ DAM Custom Workflow Runner (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) é um serviço OSGi. Ela fornece as duas opções a seguir para configuração:

* Fluxos de trabalho de pós-processamento por caminho (`postProcWorkflowsByPath`): Vários modelos de fluxo de trabalho podem ser listados, com base em caminhos de repositório diferentes. Separe caminhos e modelos usando dois pontos. Caminhos de repositório simples são suportados. Mapeie-os para um modelo de fluxo de trabalho na `/var` caminho. Por exemplo: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Fluxos de trabalho de pós-processamento por expressão (`postProcWorkflowsByExpression`): Vários modelos de fluxo de trabalho podem ser listados, com base em diferentes expressões regulares. As expressões e os modelos devem ser separados por dois pontos. A expressão regular deve apontar para o nó do ativo diretamente, e não para uma das representações ou arquivos. Por exemplo: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

Para saber como implantar uma configuração OSGi, consulte [implantar em [!DNL Experience Manager]](/help/implementing/deploying/overview.md).

#### Desative a execução do workflow de pós-processamento

Quando o pós-processamento não for necessário, crie e use um Modelo de fluxo de trabalho &quot;vazio&quot; na __Fluxo de trabalho de início automático__ seleção.

##### Criar o modelo de fluxo de trabalho de início automático desativado

1. Navegar para __Ferramentas > Fluxo de trabalho > Modelos__
1. Selecionar __Criar > Criar modelo__ formar a barra de ação superior
1. Forneça um título e nome para o novo Modelo de Fluxo de Trabalho, por exemplo:
   * Título: Desativar fluxo de trabalho de início automático
   * Nome: disable-auto-start-workflow
1. Selecionar __Concluído__ para criar o modelo de fluxo de trabalho
1. __Selecionar__ e __Editar__ o modelo de fluxo de trabalho recém-criado
1. No editor de Modelo de fluxo de trabalho, selecione __Etapa 1__ na definição do modelo e exclua-a
1. Abra o __Painel lateral__ e selecione __Etapas__
1. Arraste o __Fluxo de Trabalho de Ativos de Atualização do DAM Concluído__ etapa na definição do modelo
1. Selecione o __Informações da página__ (ao lado do __Painel lateral__ alternar) e selecione __Abrir propriedades__
1. Em __Básico__ guia , selecione __Fluxo de trabalho transitório__
1. Selecionar __Salvar e fechar__ na barra de ação superior
1. Selecionar __Sincronizar__ na barra de ação superior
1. Feche o editor de Modelo de fluxo de trabalho

##### Aplicar o modelo de fluxo de trabalho de início automático desativado

Siga as etapas descritas em [aplicar um modelo de fluxo de trabalho a uma pasta](#apply-workflow-model-to-folder) e defina a __Desativar fluxo de trabalho de início automático__ como __Fluxo de trabalho de início automático__ para pastas não exigem pós-processamento de ativos.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* Considere suas necessidades para todos os tipos de representações ao projetar fluxos de trabalho. Se você não prever a necessidade de uma representação no futuro, remova sua etapa de criação do fluxo de trabalho. As representações não podem ser excluídas em massa posteriormente. As representações indesejadas podem ocupar muito espaço de armazenamento após uso prolongado de [!DNL Experience Manager]. Para ativos individuais, você pode remover as renderizações manualmente da interface do usuário. Para vários ativos, você pode personalizar [!DNL Experience Manager] para excluir representações específicas ou excluir os ativos e carregá-los novamente.
* Atualmente, o suporte está limitado à geração de representações. Não há suporte para a geração de novo ativo.
* Atualmente, o limite de tamanho do arquivo para extração de metadados é de aproximadamente 15 GB. Ao fazer upload de ativos muito grandes, às vezes a operação de extração de metadados falha.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Introdução ao Asset compute Service](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html).
>* [Entenda a extensibilidade e quando usá-la](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).
>* [Como criar aplicativos personalizados](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html).
>* [Tipos MIME suportados para vários casos de uso](/help/assets/file-format-support.md).


<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
