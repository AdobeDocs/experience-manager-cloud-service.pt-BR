---
title: Configurar e usar microsserviços de ativos
description: Configure e use os microsserviços de ativos nativos em nuvem para processar ativos em escala.
contentOwner: AG
feature: Asset Compute Microservices, Asset Processing, Asset Management
role: Architect, Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 573300a742abfdc518c9c55070f20562a74adadd
workflow-type: tm+mt
source-wordcount: '2893'
ht-degree: 3%

---

# Usar microsserviços de ativos e perfis de processamento {#get-started-using-asset-microservices}

Os microsserviços de ativos fornecem processamento escalável e resiliente de ativos usando aplicativos nativos em nuvem (também chamados de trabalhadores). O Adobe gerencia os serviços para obter o tratamento ideal de diferentes tipos de ativos e opções de processamento.

Os microsserviços de ativos permitem processar uma [ampla variedade de tipos de arquivos](/help/assets/file-format-support.md) que abrangem mais formatos prontos para uso do que o possível com versões anteriores do [!DNL Experience Manager]. Por exemplo, a extração de miniaturas dos formatos PSD e PSB agora é possível, mas anteriormente exigia soluções de terceiros, como o [!DNL ImageMagick].

O processamento de ativos depende da configuração em **[!UICONTROL Processando Perfis]**. O Experience Manager fornece uma configuração padrão básica e permite que os administradores adicionem configurações mais específicas de processamento de ativos. Os administradores criam, mantêm e modificam as configurações dos fluxos de trabalho de pós-processamento, incluindo personalização opcional. A personalização dos fluxos de trabalho permite que os desenvolvedores estendam a oferta padrão.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Uma exibição de alto nível do processamento de ativos](assets/asset-microservices-flow.png "Uma exibição de alto nível do processamento de ativos")

>[!NOTE]
>
>O processamento de ativos descrito aqui substitui o modelo de fluxo de trabalho `DAM Update Asset` existente nas versões anteriores do [!DNL Experience Manager]. O processamento de microsserviços de ativos substitui a maioria das etapas padrão relacionadas à geração de representação e aos metadados, e a configuração do fluxo de trabalho de pós-processamento pode substituir as etapas restantes, se houver.

## Entender as opções de processamento de ativos {#get-started}

[!DNL Experience Manager] permite os seguintes níveis de processamento.

| Opção | Descrição | Casos de uso abrangidos |
|---|---|---|
| [Configuração padrão](#default-config) | Ela está disponível como está e não pode ser modificada. Essa configuração fornece um recurso básico de geração de representação. | <ul> <li>Miniaturas padrão usadas pela interface do usuário [!DNL Assets] (48, 140 e 319 pixels) </li> <li> Visualização grande (representação da Web - 1280 pixels) </li><li> Extração de metadados e texto.</li></ul> |
| [Configuração personalizada](#standard-config) | Configurado pelos administradores por meio da interface do usuário. Mais opções são fornecidas para geração de representação estendendo a opção padrão. Estenda a opção pronta para uso para fornecer diferentes formatos e representações. | <ul><li>Representação FPO (somente para posicionamento). </li> <li>Alterar formato de arquivo e resolução de imagens</li> <li> Aplicar condicionalmente a tipos de arquivos configurados. </li> </ul> |
| [Perfil personalizado](#custom-config) | Configurado por administradores via interface de usuário para usar o código personalizado por meio de aplicativos personalizados para chamar o [Serviço Asset Compute](https://experienceleague.adobe.com/pt-br/docs/asset-compute/using/introduction). Suporta requisitos mais complexos em um método escalável e nativo em nuvem. | Consulte [casos de uso permitidos](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Formatos de arquivo não compatíveis {#supported-file-formats}

Os microsserviços de ativos são compatíveis com uma grande variedade de formatos de arquivo para processar, gerar representações ou extrair metadados. Consulte [formatos de arquivo com suporte](file-format-support.md) para obter a lista completa de tipos MIME e a funcionalidade com suporte para cada tipo.

## Configuração padrão {#default-config}

Alguns padrões são pré-configurados para garantir que as representações padrão necessárias no Experience Manager estejam disponíveis. A configuração padrão também garante que as operações de extração de metadados e extração de texto estejam disponíveis. Os usuários podem começar a fazer upload ou atualizar ativos imediatamente e o processamento básico está disponível por padrão.

Com a configuração padrão, somente o perfil de processamento mais básico é configurado. O perfil de processamento não está visível na interface do usuário e você não pode modificá-lo. Ele sempre é executado para processar ativos carregados. Esse perfil de processamento padrão garante que o processamento básico exigido por [!DNL Experience Manager] seja concluído em todos os ativos.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Configuração padrão {#standard-config}

O [!DNL Experience Manager] fornece recursos para gerar representações mais específicas para formatos comuns de acordo com as necessidades do usuário. Um administrador pode criar [!UICONTROL Perfis de Processamento] adicionais para facilitar essa criação de representação. Os usuários atribuem um ou mais perfis disponíveis a pastas específicas para concluir o processamento adicional. Digamos que, por exemplo, o processamento adicional possa gerar representações para a Web, dispositivos móveis e tablets. [Assista a este vídeo para entender como criar e aplicar [!UICONTROL Perfis de Processamento] e como acessar as representações criadas](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/assets/content-automation/creative-operations).

* **Largura e altura da representação**: a especificação de largura e altura da representação fornece tamanhos máximos da imagem de saída gerada. Os microsserviços de ativos tentam produzir a maior representação possível, cuja largura e altura não são maiores que a largura e a altura especificadas, respectivamente. A proporção é preservada, ou seja, a mesma do original. Um valor vazio significa que o processamento de ativos assume a dimensão em pixels do original.

* **Regras de inclusão de tipo MIME**: quando um ativo com um tipo MIME específico é processado, o tipo MIME é verificado primeiro em relação ao valor de tipos MIME excluídos para a especificação de representação. Se ele corresponder a essa lista, essa representação específica não será gerada para o ativo (lista de bloqueios). Caso contrário, o tipo MIME será verificado em relação ao tipo MIME incluído e, se ele corresponder à lista, a representação será gerada (lista de permissões).

* **Representação FPO especial**: ao colocar ativos de grande porte do [!DNL Experience Manager] em documentos do [!DNL Adobe InDesign], um profissional de criação aguarda um tempo considerável depois de [colocar um ativo](https://helpx.adobe.com/br/indesign/using/placing-graphics.html). Enquanto isso, o usuário não pode usar [!DNL InDesign]. Isso interrompe o fluxo de criação e afeta negativamente a experiência do usuário. O Adobe permite colocar temporariamente representações de pequeno porte em documentos do [!DNL InDesign] para começar, que podem ser substituídas por ativos de resolução completa posteriormente. [!DNL Experience Manager] fornece representações que são usadas apenas para posicionamento. Essas representações FPO têm um tamanho de arquivo pequeno, mas têm a mesma proporção.

O perfil de processamento pode incluir uma representação FPO (somente para posicionamento). Consulte a [!DNL Adobe Asset Link] [documentação](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) para entender se você precisa ativá-la para o seu perfil de processamento. Para obter mais informações, consulte a [documentação completa do Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html).

### Criar um perfil padrão {#create-standard-profile}

1. Os administradores acessam **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Processando Perfis]**. Clique em **[!UICONTROL Criar]**.
1. Forneça um nome que ajude a identificar exclusivamente o perfil ao aplicar a uma pasta.
1. Para gerar representações FPO, na guia **[!UICONTROL Imagem]**, habilite **[!UICONTROL Criar Representação FPO]**. Insira um valor de **[!UICONTROL Qualidade]** de 1-100.
1. Para gerar outras representações, clique em **[!UICONTROL Adicionar novo]** e forneça as seguintes informações:

   * Nome do arquivo de cada representação.
   * Formato de arquivo (PNG, JPEG, GIF ou WebP) de cada representação.
   * Largura e altura em pixels de cada representação. Se os valores não forem especificados, será usado o tamanho total em pixels da imagem original.
   * Qualidade em porcentagem de cada representação de JPEG e WebP.
   * Tipos MIME incluídos e excluídos para definir a aplicabilidade de um perfil.

   ![adicionando-perfis-de-processamento](assets/processing-profiles-image.png)

1. Clique em **[!UICONTROL Salvar]**.

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## Perfil personalizado e casos de uso {#custom-config}

O [!DNL Asset Compute Service] oferece suporte a vários casos de uso, incluindo processamento padrão e processamento de formatos específicos de Adobe, como arquivos Photoshop. Também permite a implementação de processamento personalizado ou específico da organização. A personalização do fluxo de trabalho do Ativo de atualização do DAM necessária no passado é manipulada automaticamente ou por meio da configuração de Perfis de processamento. Se essas opções de processamento não atenderem às suas necessidades comerciais, a Adobe recomenda desenvolver e usar o [!DNL Asset Compute Service] para estender os recursos padrão. Para obter uma visão geral, consulte [entender a extensibilidade e quando usá-la](https://experienceleague.adobe.com/pt-br/docs/asset-compute/using/extend/understand-extensibility).

>[!NOTE]
>
>A Adobe recomenda usar um aplicativo personalizado somente quando os requisitos comerciais não puderem ser alcançados usando as configurações padrão ou o perfil padrão.

Ele pode transformar imagens, vídeos, documentos e outros formatos de arquivo em diferentes representações, incluindo miniaturas, texto e metadados extraídos e arquivos.

Os desenvolvedores podem usar o [!DNL Asset Compute Service] para [criar aplicativos personalizados](https://experienceleague.adobe.com/pt-br/docs/asset-compute/using/extend/develop-custom-application) para os casos de uso com suporte. O [!DNL Experience Manager] pode chamar esses aplicativos personalizados na interface do usuário usando perfis personalizados que os administradores configuram. [!DNL Asset Compute Service] dá suporte aos seguintes casos de uso de invocação de serviços externos:

* Use a [!DNL Adobe Photoshop]API ImageCutout[ de ](https://developer.adobe.com/photoshop/photoshop-api-docs/) e salve o resultado como uma representação.
* Chame sistemas de terceiros para fazer alterações, por exemplo, um sistema PIM.
* Use a API [!DNL Photoshop] para gerar uma variedade de representações com base no modelo do Photoshop.
* Use a [API do Adobe Lightroom](https://developer.adobe.com/photoshop/photoshop-api-docs/) para otimizar os ativos assimilados e salvá-los como representações.

>[!NOTE]
>
>Não é possível editar os metadados padrão usando os aplicativos personalizados. Você só pode modificar metadados personalizados.

### Criar um perfil personalizado {#create-custom-profile}

1. Os administradores acessam **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Processando Perfis]** > **[!UICONTROL Criar]**.
1. Na página Processando Perfil, clique na guia **[!UICONTROL Personalizado]** e em **[!UICONTROL Adicionar novo]**.
1. No campo de texto Nome, digite o nome de arquivo desejado da representação e forneça as seguintes informações.

   * Nome de arquivo de cada representação e uma extensão de arquivo compatível.
   * [URL do ponto de extremidade de um aplicativo personalizado do App Builder](https://experienceleague.adobe.com/pt-br/docs/asset-compute/using/extend/deploy-custom-application). O aplicativo deve ser da mesma organização da conta do Experience Manager.
   * Adicionar Parâmetros de Serviço a [passar informações extras ou parâmetros para o aplicativo personalizado](https://experienceleague.adobe.com/pt-br/docs/asset-compute/using/extend/develop-custom-application#extend).
   * Tipos MIME incluídos e excluídos para limitar o processamento a alguns formatos de arquivo específicos.

1. Ao lado do canto superior direito da página, clique em **[!UICONTROL Salvar]**.

Os aplicativos personalizados são aplicativos [Project App Builder](https://developer.adobe.com/app-builder/docs/overview/) headless. Seu aplicativo personalizado obterá todos os arquivos fornecidos se eles estiverem configurados com um perfil de processamento. O aplicativo deve filtrar os arquivos.

>[!CAUTION]
>
>Se o aplicativo App Builder e a conta [!DNL Experience Manager] não forem da mesma organização, a integração não funcionará.

### Exemplo de perfil personalizado {#custom-profile-example}

Para ilustrar o uso do perfil personalizado, vamos considerar um caso de uso para aplicar texto personalizado a imagens da campanha. É possível criar um perfil de processamento que use a API do Photoshop para editar as imagens.

A integração do Asset Compute Service permite que o Experience Manager passe esses parâmetros para o aplicativo personalizado usando o campo [!UICONTROL Parâmetros de Serviço]. Em seguida, o aplicativo personalizado chama a API do Photoshop e passa esses valores para a API. Por exemplo, você pode passar o nome da fonte, a cor do texto, a espessura e o tamanho do texto para adicionar o texto personalizado às imagens da campanha.

<!-- TBD: Check screenshot against the interface. -->

![perfil-processamento-personalizado](assets/custom-processing-profile.png)

*Figura: Use o campo [!UICONTROL Parâmetros de Serviço] para transmitir informações adicionadas à compilação de parâmetros predefinidos para o aplicativo personalizado. Neste exemplo, quando as imagens da campanha são carregadas, elas são atualizadas com texto `Jumanji` na fonte `Arial-BoldMT`.*

## Usar perfis de processamento para processar ativos {#use-profiles}

Crie e aplique Perfis de processamento personalizados adicionais a pastas específicas. Esse fluxo de trabalho permite que o Experience Manager processe ativos que são carregados ou atualizados nessas pastas. O perfil de processamento padrão incorporado é sempre executado, mas não fica visível na interface do usuário do. Se você adicionar um perfil personalizado, ambos os perfis serão usados para processar os ativos carregados.

Aplique perfis de processamento a pastas usando um dos seguintes métodos:

* Os administradores podem selecionar uma definição de perfil de processamento em **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Processamento]** e usar a ação **[!UICONTROL Aplicar Perfil às Pastas]**. Ele abre um navegador de conteúdo que permite navegar até pastas específicas, selecioná-las e confirmar a aplicação do perfil.
* Os usuários podem selecionar uma pasta na interface do usuário do Assets e usar a ação **[!UICONTROL Propriedades]** para abrir a tela de propriedades da pasta. Na guia **[!UICONTROL Processamento de ativos]**, é possível selecionar o perfil de processamento apropriado para essa pasta na lista [!UICONTROL Perfil de Processamento]. Para salvar as alterações, clique em **[!UICONTROL Salvar e fechar]**.
  ![Aplicar perfil de processamento a uma pasta da guia Propriedades do ativo](assets/folder-properties-processing-profile.png)

* Os usuários podem selecionar pastas ou ativos específicos na interface do Assets para aplicar um perfil de processamento e, em seguida, selecionar a opção ![ícone de reprocessamento de ativos](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL Reprocessar Assets]** nas opções disponíveis na parte superior.

>[!TIP]
>
>Somente um perfil de processamento pode ser aplicado a uma pasta. Para gerar mais representações, adicione mais definições de representação ao perfil de processamento existente.

Depois que um perfil de processamento é aplicado a uma pasta, todos os novos ativos carregados (ou atualizados) nessa pasta ou em qualquer uma de suas subpastas são processados usando o perfil de processamento adicional configurado. Esse processamento é executado em adição ao do perfil padrão.

>[!NOTE]
>
>Um perfil de processamento aplicado a uma pasta funciona para toda a árvore, mas pode ser substituído por outro perfil aplicado a uma subpasta. Quando os ativos são carregados para uma pasta, o Experience Manager verifica se as propriedades da pasta que os contém em busca de um perfil de processamento. Se nenhum for aplicado, uma pasta principal na hierarquia será verificada em busca de um perfil de processamento para ser aplicado.

Para verificar se os ativos são processados, visualize as representações geradas na exibição [!UICONTROL Representações] no painel esquerdo. Abra a visualização do ativo e abra o painel esquerdo para acessar a exibição **[!UICONTROL Representações]**. As representações específicas no perfil de processamento, para as quais o tipo de ativo específico corresponde às regras de inclusão do tipo MIME, devem estar visíveis e acessíveis.

![execuções adicionais](assets/renditions-additional-renditions.png)

*Figura: Exemplo de duas representações adicionais geradas por um perfil de processamento aplicado à pasta pai.*

## Workflows de pós-processamento {#post-processing-workflows}

Para uma situação em que é necessário o processamento adicional de ativos que não pode ser obtido usando os Perfis de processamento, workflows de pós-processamento adicionais podem ser adicionados à configuração. O pós-processamento permite adicionar processamento totalmente personalizado além do processamento configurável usando microsserviços de ativos.

Após a conclusão do processamento dos microsserviços, o [!DNL Experience Manager] executa automaticamente fluxos de trabalho de pós-processamento ou [Fluxos de trabalho de início automático](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/assets/configuring/auto-start-workflows), se configurado. Não há necessidade de adicionar iniciadores de fluxo de trabalho manualmente para acionar os fluxos de trabalho. Os exemplos incluem:

* Etapas personalizadas do fluxo de trabalho para processar ativos.
* Integrações para adicionar metadados ou propriedades a ativos de sistemas externos, por exemplo, informações de produto ou processo.
* O processamento adicional é feito por serviços externos.

Para adicionar uma configuração de fluxo de trabalho de pós-processamento ao [!DNL Experience Manager], siga estas etapas:

* Crie um ou mais modelos de fluxo de trabalho. Esses modelos personalizados são chamados de *modelos de fluxo de trabalho de pós-processamento* nesta documentação. Eles são modelos de fluxo de trabalho [!DNL Experience Manager] comuns.
* Adicione as etapas de fluxo de trabalho necessárias a esses modelos. Revise as etapas do fluxo de trabalho padrão e adicione todas as etapas padrão necessárias ao fluxo de trabalho personalizado. As etapas são executadas nos ativos com base em uma configuração de modelo de fluxo de trabalho. Por exemplo, se você quiser que a marcação inteligente ocorra automaticamente no upload do ativo, adicione a etapa ao modelo de fluxo de trabalho de pós-processamento personalizado.
* Adicione a etapa [!UICONTROL Fluxo de trabalho do Ativo de atualização do DAM concluído] ao final. Adicionar esta etapa garante que a Experience Manager saiba quando o processamento termina e o ativo pode ser marcado como processado, ou seja, *Novo* é exibido no ativo.
* Crie uma configuração para o Serviço de execução de fluxo de trabalho personalizado que permita configurar a execução de um modelo de fluxo de trabalho de pós-processamento por um caminho (local da pasta) ou por uma expressão regular.

Para obter detalhes sobre qual etapa do fluxo de trabalho padrão pode ser usada no fluxo de trabalho de pós-processamento, consulte [etapas do fluxo de trabalho no fluxo de trabalho de pós-processamento](developer-reference-material-apis.md#post-processing-workflows-steps) na referência do desenvolvedor.

### Criar modelos de fluxo de trabalho de pós-processamento {#create-post-processing-workflow-models}

Os modelos de fluxo de trabalho de pós-processamento são [!DNL Experience Manager] modelos de fluxo de trabalho comuns. Crie modelos diferentes se precisar de processamento diferente para locais de repositório ou tipos de ativos diferentes.

As etapas de processamento são adicionadas conforme necessário. Você pode usar as etapas compatíveis disponíveis e qualquer etapa de fluxo de trabalho personalizada implementada.

Verifique se a última etapa de cada fluxo de trabalho de pós-processamento é `DAM Update Asset Workflow Completed Process`. A etapa final garante que a Experience Manager reconheça a conclusão do processamento de ativos.

### Configurar a execução do workflow de pós-processamento {#configure-post-processing-workflow-execution}

Depois que os microsserviços de ativos concluírem o processamento dos ativos carregados, você poderá definir um fluxo de trabalho de pós-processamento para processar mais os ativos. Para configurar o pós-processamento usando modelos de fluxo de trabalho, siga um destes procedimentos:

* [Aplicar um modelo de fluxo de trabalho nas Propriedades da pasta](#apply-workflow-model-to-folder).
* [Configurar o serviço Executor de Fluxo de Trabalho Personalizado](#configure-custom-workflow-runner-service).

#### Aplicar um modelo de fluxo de trabalho a uma pasta {#apply-workflow-model-to-folder}

Para casos de uso típicos de pós-processamento, considere usar o método para aplicar um fluxo de trabalho a uma pasta. Para aplicar um modelo de fluxo de trabalho na pasta [!UICONTROL Propriedades], siga estas etapas:

1. Crie um modelo de fluxo de trabalho.
1. Selecione uma pasta, clique em **[!UICONTROL Propriedades]** na barra de ferramentas e clique na guia **[!UICONTROL Processamento do Assets]**.
1. Em **[!UICONTROL Fluxo de trabalho de início automático]**, selecione o fluxo de trabalho necessário, forneça um título para o fluxo de trabalho e salve as alterações.

   ![Aplicar um fluxo de trabalho de pós-processamento a uma pasta em suas Propriedades](assets/post-processing-profile-workflow-for-folders.png)

#### Configurar o serviço de execução de fluxo de trabalho personalizado {#configure-custom-workflow-runner-service}

Você pode configurar o Serviço de Execução de Fluxo de Trabalho Personalizado para as configurações avançadas que não podem ser prontamente atendidas ao aplicar um fluxo de trabalho a uma pasta. Por exemplo, um fluxo de trabalho que usa uma expressão regular. O Adobe CQ DAM Custom Workflow Runner (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) é um serviço OSGi. Ela fornece as duas opções de configuração a seguir:

* Fluxos de trabalho de pós-processamento por caminho (`postProcWorkflowsByPath`): vários modelos de fluxo de trabalho podem ser listados, com base em caminhos de repositório diferentes. Separe caminhos e modelos usando dois-pontos. Há suporte para caminhos de repositório simples. Mapeie-os para um modelo de fluxo de trabalho no caminho `/var`. Por exemplo: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Fluxos de trabalho de pós-processamento por expressão (`postProcWorkflowsByExpression`): vários modelos de fluxo de trabalho podem ser listados, com base em diferentes expressões regulares. Separe as expressões e os modelos com dois pontos. Aponte a expressão regular para apontar diretamente para o nó Asset e não para uma das representações ou arquivos. Por exemplo: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

Para saber como implantar uma configuração OSGi, consulte [implantar em [!DNL Experience Manager]](/help/implementing/deploying/overview.md).

#### Desative a execução do workflow de pós-processamento

Quando o pós-processamento não for necessário, crie e use um Modelo de Fluxo de Trabalho &quot;vazio&quot; na seleção **Fluxo de Trabalho de início automático**.

##### Criar o modelo de fluxo de trabalho de início automático desativado

1. Navegue até **Ferramentas** > **Fluxo de trabalho** > **Modelos**.
1. Clique em **Criar** > **Criar modelo** na barra de ação superior.
1. Forneça um título e nome para o novo Modelo de fluxo de trabalho, por exemplo:
   * Título: desativar o fluxo de trabalho de início automático
   * Nome: disable-auto-start-workflow
1. Clique em **Concluído** para criar o modelo de fluxo de trabalho.
1. Selecionar e editar o modelo de fluxo de trabalho criado
1. No editor de modelo de fluxo de trabalho, clique em **Etapa 1** da definição de modelo e exclua-a.
1. No painel lateral, clique em **Etapas**.
1. Arraste a etapa **Fluxo de trabalho do ativo de atualização do DAM concluído** para a definição do modelo.
1. Clique em **Informações da Página** (ao lado da opção **Painel Lateral**) e em **Abrir Propriedades**.
1. Na guia Básico, clique em **Fluxo de trabalho transitório**.
1. Na barra de ações superior, clique em **Salvar e fechar**.
1. Na barra de ações superior, clique em **Sincronizar**.
1. Feche o editor do modelo de fluxo de trabalho.

##### Aplicar o modelo de fluxo de trabalho de início automático desativado

Siga as etapas descritas em [aplicar um modelo de fluxo de trabalho a uma pasta](#apply-workflow-model-to-folder) e definir o **Desabilitar Fluxo de Trabalho de Início Automático** como o **Fluxo de Trabalho de Início Automático** para pastas que não exigem pós-processamento de ativos.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* Considere suas necessidades para todos os tipos de representações ao criar workflows. Se você não prever a necessidade de uma representação no futuro, remova a etapa de criação do fluxo de trabalho. As representações não podem ser excluídas em massa posteriormente. As representações indesejadas podem ocupar grandes quantidades de espaço de armazenamento após o uso prolongado de [!DNL Experience Manager]. Para ativos individuais, é possível remover representações manualmente da interface do usuário. Para vários ativos, você pode personalizar [!DNL Experience Manager] para excluir representações específicas ou excluir os ativos e carregá-los novamente.
* No momento, o suporte está limitado à geração de representações. Não há suporte para a geração de novo ativo.
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
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Introdução ao Asset Compute Service](https://experienceleague.adobe.com/pt-br/docs/asset-compute/using/introduction).
>* [Entenda a extensibilidade e quando usá-la](https://experienceleague.adobe.com/pt-br/docs/asset-compute/using/extend/understand-extensibility).
>* [Como criar aplicativos personalizados](https://experienceleague.adobe.com/pt-br/docs/asset-compute/using/extend/develop-custom-application).
>* [Tipos MIME com suporte para vários casos de uso](/help/assets/file-format-support.md).

<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
