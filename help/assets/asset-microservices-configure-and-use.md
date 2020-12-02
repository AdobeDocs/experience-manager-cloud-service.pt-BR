---
title: Configurar e usar microserviços de ativos
description: Configure e use os microserviços de ativos nativos na nuvem para processar ativos em escala.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '2514'
ht-degree: 1%

---


# Usar microserviços de ativos e perfis de processamento {#get-started-using-asset-microservices}

Os microserviços de ativos fornecem processamento escalonável e resiliente de ativos usando aplicativos nativos na nuvem (também chamados de trabalhadores). O Adobe gerencia os serviços para uma manipulação otimizada de diferentes tipos de ativos e opções de processamento.

Os microserviços de ativos permitem que você processe uma [ampla variedade de tipos de arquivos](/help/assets/file-format-support.md) cobrindo mais formatos prontos para uso do que o que é possível com as versões anteriores de [!DNL Experience Manager]. Por exemplo, a extração em miniatura dos formatos PSD e PSB agora é possível e exigia soluções de terceiros como o ImageMagick.

O processamento de ativos depende da configuração em **[!UICONTROL Perfis de processamento]**. O Experience Manager fornece uma configuração padrão básica e permite que os administradores adicionem configurações mais específicas de processamento de ativos. Os administradores criam, mantêm e modificam as configurações de workflows de pós-processamento, incluindo personalização opcional. Personalizar os workflows permite que os desenvolvedores estendam a oferta padrão.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Uma visualização de alto nível de ](assets/asset-microservices-flow.png "processamento de ativosUma visualização de alto nível de processamento de ativos")

>[!NOTE]
>
>O processamento de ativos descrito aqui substitui o modelo de fluxo de trabalho `DAM Update Asset` existente nas versões anteriores de [!DNL Experience Manager]. A maioria das etapas padrão de geração de representação e relacionadas a metadados são substituídas pelo processamento de microserviços de ativos, e as etapas restantes, se houver, podem ser substituídas pela configuração do fluxo de trabalho de pós-processamento.

## Compreender as opções de processamento de ativos {#get-started}

Experience Manager permite os seguintes níveis de processamento.

| Opção | Descrição | Casos de uso cobertos |
|---|---|---|
| [Configuração padrão](#default-config) | Está disponível como está e não pode ser modificado. Essa configuração fornece recursos de geração de execução muito básicos. | <ul> <li>Miniaturas padrão usadas pela interface do usuário [!DNL Assets] (48, 140 e 319 pixels) </li> <li> Pré-visualização grande (execução na Web - 1280 pixels) </li><li> Metadados e extração de texto.</li></ul> |
| [Configuração personalizada](#standard-config) | Configurado pelos administradores por meio da interface do usuário. Fornece mais opções para a geração de representação estendendo a opção padrão. Estenda a opção predefinida para fornecer diferentes formatos e execuções. | <ul><li>Execução FPO. </li> <li>Alterar o formato e a resolução das imagens</li> <li> Aplica-se condicionalmente aos tipos de arquivos configurados. </li> </ul> |
| [Perfil personalizado](#custom-config) | Configurado pelos administradores por meio da interface do usuário para usar o código personalizado por meio de aplicativos personalizados para chamar [Asset compute Service](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html). Suporta requisitos mais complexos em um método nativo de nuvem e dimensionável. | Consulte [casos de uso permitidos](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Formatos de arquivo não suportados {#supported-file-formats}

Os microserviços de ativos oferecem suporte para uma grande variedade de formatos de arquivo para processar, gerar execuções ou extrair metadados. Consulte [formatos de arquivo suportados](file-format-support.md) para obter a lista completa de tipos MIME e a funcionalidade suportada para cada tipo.

## Configuração padrão {#default-config}

Alguns padrões são pré-configurados para garantir que as execuções padrão necessárias no Experience Manager estejam disponíveis. A configuração padrão também garante que as operações de extração de metadados e extração de texto estejam disponíveis. Os usuários podem fazer upload ou atualizar ativos imediatamente e o processamento básico está disponível por padrão.

Com a configuração padrão, somente o perfil de processamento mais básico é configurado. Esse perfil de processamento não é visível na interface do usuário e você não pode modificá-lo. Ele sempre é executado para processar ativos carregados. Esse perfil de processamento padrão garante que o processamento básico exigido por [!DNL Experience Manager] seja concluído em todos os ativos.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Configuração padrão {#standard-config}

[!DNL Experience Manager] forneça recursos para gerar renderizações mais específicas para formatos comuns, de acordo com as necessidades do usuário. Um administrador pode criar [!UICONTROL Perfis de processamento] adicionais para facilitar essa criação de execução. Em seguida, os usuários atribuem um ou mais dos perfis disponíveis a pastas específicas para concluir o processamento adicional. Por exemplo, o processamento adicional pode gerar representações para Web, dispositivos móveis e tablets. O vídeo a seguir ilustra como criar e aplicar [!UICONTROL Perfis de processamento] e como acessar as execuções criadas.

* **Largura e altura** da representação: A especificação de largura e altura da representação fornece tamanhos máximos da imagem de saída gerada. Os microserviços de ativos tentam produzir a maior representação possível, que a largura e a altura não são maiores que a largura e a altura especificadas, respectivamente. A proporção é preservada, é a mesma do original. Um valor vazio significa que o processamento de ativos assume a dimensão em pixels do original.

* **Regras** de inclusão de tipo MIME: Quando um ativo com um tipo MIME específico é processado, o tipo MIME é verificado pela primeira vez em relação ao valor de tipos MIME excluídos para a especificação de representação. Se corresponder a essa lista, essa representação específica não será gerada para o ativo (lista de bloqueios). Caso contrário, o tipo MIME será verificado em relação ao tipo MIME incluído e, se ele corresponder à lista, a representação será gerada (lista de permissões).

* **Representação** especial do FPO: Ao colocar ativos de grande porte de  [!DNL Experience Manager] dentro de  [!DNL Adobe InDesign] documentos, um profissional criativo espera por um tempo substancial depois de  [colocar um ativo](https://helpx.adobe.com/indesign/using/placing-graphics.html). Enquanto isso, o usuário está impedido de usar [!DNL InDesign]. Isso interrompe o fluxo criativo e afeta negativamente a experiência do usuário. O Adobe permite que execuções de pequeno porte sejam temporariamente colocadas em documentos [!DNL InDesign], que podem ser substituídas posteriormente por ativos de resolução total sob demanda. [!DNL Experience Manager] fornece execuções que são usadas apenas para posicionamento (FPO). Essas renderizações FPO têm um tamanho de arquivo pequeno, mas têm a mesma proporção.

O perfil de processamento pode incluir uma execução FPO (Somente para disposição). Consulte [!DNL Adobe Asset Link] [documentação](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) para saber se você precisa ativá-la para o perfil de processamento. Para obter mais informações, consulte [documentação completa do Link de ativo do Adobe](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html).

### Criar perfil padrão {#create-standard-profile}

Para criar um perfil de processamento padrão, siga estas etapas:

1. Os administradores acessam **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de processamento]**. Clique em **[!UICONTROL Criar]**.
1. Forneça um nome que o ajude a identificar exclusivamente o perfil ao se inscrever em uma pasta.
1. Para gerar execuções de FPO, na guia **[!UICONTROL Standard]**, ative **[!UICONTROL Criar representação de FPO]**. Insira um valor **[!UICONTROL Quality]** entre 1 e 100.
1. Para gerar outras representações, clique em **[!UICONTROL Adicionar Novo]** e forneça as seguintes informações:

   * Nome de arquivo de cada representação.
   * Formato de arquivo (PNG, JPEG, GIF ou WebP) de cada execução.
   * Largura e altura em pixels de cada representação. Se os valores não forem especificados, o tamanho total de pixel da imagem original será usado.
   * Qualidade em porcentagem de cada execução JPEG e WebP.
   * Tipos MIME incluídos e excluídos para definir a aplicabilidade de um perfil.

   ![adição de perfis de processamento](assets/processing-profiles-image.png)

1. Clique em **[!UICONTROL Salvar]**.

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## Perfil personalizado e casos de uso {#custom-config}

O [!DNL Asset Compute Service] oferece suporte a uma variedade de casos de uso, como processamento padrão, formatos específicos de Adobe como arquivos Photoshop e implementação de processamento personalizado ou específico da organização. A personalização do fluxo de trabalho do Ativo de atualização do DAM necessária no passado é feita automaticamente ou pela configuração de perfis de processamento. Se as necessidades de negócios não forem atendidas por essas opções de processamento, a Adobe recomenda desenvolver e usar [!DNL Asset Compute Service] para estender os recursos padrão. Para obter uma visão geral, consulte [compreender a extensibilidade e quando usá-la](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).

>[!NOTE]
>
>A Adobe recomenda usar um aplicativo personalizado somente quando os requisitos comerciais não podem ser cumpridos usando as configurações padrão ou o perfil padrão.

Ele pode transformar imagens, vídeos, documentos e outros formatos de arquivo em diferentes representações, incluindo miniaturas, texto e metadados extraídos e arquivos.

Os desenvolvedores podem usar o [!DNL Asset Compute Service] para [criar aplicativos personalizados](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) que atendam aos casos de uso suportados. [!DNL Experience Manager] pode chamar esses aplicativos personalizados da interface do usuário usando perfis personalizados configurados pelos administradores. [!DNL Asset Compute Service] apoia os seguintes casos de utilização de serviços externos:

* Use a [API do ImageCut](https://github.com/AdobeDocs/photoshop-api-docs-pre-release#imagecutout) de [!DNL Adobe Photoshop] e salve o resultado como execução.
* Chame sistemas de terceiros para atualizar dados, por exemplo, um sistema PIM.
* Use a API [!DNL Photoshop] para gerar várias execuções com base no modelo do Photoshop.
* Use [Adobe Lightroom API](https://github.com/AdobeDocs/lightroom-api-docs#supported-features) para otimizar os ativos assimilados e salvá-los como execuções.

>[!NOTE]
>
>Não é possível editar os metadados padrão usando os aplicativos personalizados. Você só pode modificar metadados personalizados.

### Criar um perfil personalizado {#create-custom-profile}

Para criar um perfil personalizado, siga estas etapas:

1. Os administradores acessam **[!UICONTROL Ferramentas > Ativos > Perfis de processamento]**. Clique em **[!UICONTROL Criar]**.
1. Clique na guia **[!UICONTROL Personalizado]**. Clique em **[!UICONTROL Adicionar Novo]**. Forneça o nome de arquivo desejado para a representação.
1. Forneça as seguintes informações.

   * Nome de arquivo de cada execução e extensão de arquivo compatível.
   * [URL de ponto final de um aplicativo](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html) personalizado Firefly. O aplicativo deve ser da mesma organização que a conta Experience Manager.
   * Adicione Parâmetros de Serviço a [passem informações ou parâmetros adicionais para o aplicativo personalizado](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend).
   * Tipos MIME incluídos e excluídos para limitar o processamento a alguns formatos de arquivo específicos.

   Clique em **[!UICONTROL Salvar]**.

Os aplicativos personalizados são aplicativos sem cabeçalho [Project Firefly](https://github.com/AdobeDocs/project-firefly). O aplicativo personalizado obtém todos os arquivos fornecidos se eles estiverem configurados com um perfil de processamento. O aplicativo deve filtrar os arquivos.

>[!CAUTION]
>
>Se o aplicativo Firefly e a conta [!DNL Experience Manager] não forem da mesma organização, a integração não funcionará.

### Um exemplo de um perfil personalizado {#custom-profile-example}

Para ilustrar o uso personalizado de perfis, considere um caso de uso para aplicar algum texto personalizado a imagens de campanha. Você pode criar um perfil de processamento que aproveita a API do Photoshop para editar as imagens.

A integração do Serviço de asset compute permite que o Experience Manager passe esses parâmetros para o aplicativo personalizado usando o campo [!UICONTROL Parâmetros de Serviço]. O aplicativo personalizado então chama a API do Photoshop e transmite esses valores para a API. Por exemplo, é possível passar o nome da fonte, a cor do texto, o peso do texto e o tamanho do texto para adicionar o texto personalizado às imagens de campanha.

![perfil de processamento personalizado](assets/custom-processing-profile.png)

*Figura: Use o campo  [!UICONTROL Parâmetros ] de serviço para passar informações adicionadas para parâmetros predefinidos criados no aplicativo personalizado. Neste exemplo, quando imagens de campanha são carregadas, as imagens são atualizadas com o texto `Jumanji` na fonte `Arial-BoldMT`.*

## Use perfis de processamento para processar ativos {#use-profiles}

Crie e aplique perfis de processamento adicionais e personalizados a pastas específicas para que o Experience Manager processe o processamento de ativos carregados ou atualizados nessas pastas. O perfil padrão de processamento padrão incorporado é sempre executado, mas não é visível na interface do usuário. Se você adicionar um perfil personalizado, ambos os perfis serão usados para processar os ativos carregados.

Aplique perfis de processamento a pastas usando um dos seguintes métodos:

* Os administradores podem selecionar uma definição de perfil de processamento em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de processamento]** e usar a ação **[!UICONTROL Aplicar Perfil às Pastas]**. Ele abre um navegador de conteúdo que permite navegar para pastas específicas, selecioná-las e confirmar o aplicativo do perfil.
* Os usuários podem selecionar uma pasta na interface do usuário do Assets, usar a ação **[!UICONTROL Properties]** para abrir a tela de propriedades da pasta, clicar na guia **[!UICONTROL Processando Perfis]** e, na lista pop-up, selecionar o perfil de processamento apropriado para essa pasta. Para salvar as alterações, clique em **[!UICONTROL Salvar e fechar]**.
   ![Aplicar o perfil de processamento a uma pasta na guia Propriedades do ativo](assets/folder-properties-processing-profile.png)

>[!TIP]
>
>Somente um perfil de processamento pode ser aplicado a uma pasta. Para gerar mais execuções, adicione mais definições de execução ao perfil de processamento existente.

Depois que um perfil de processamento é aplicado a uma pasta, todos os novos ativos carregados (ou atualizados) nessa pasta ou em qualquer subpasta dela são processados usando o perfil de processamento adicional configurado. Esse processamento é adicionado ao perfil padrão.

>[!NOTE]
>
>Um perfil de processamento aplicado a uma pasta funciona para a árvore inteira, mas pode ser substituído por outro perfil aplicado a uma subpasta. Quando os ativos são carregados em uma pasta, o Experience Manager verifica as propriedades da pasta que os contém para verificar se há um perfil de processamento. Se nenhum for aplicado, uma pasta pai na hierarquia será verificada para que um perfil de processamento seja aplicado.

Para verificar se os ativos são processados, pré-visualização as representações geradas na visualização [!UICONTROL Representações] no painel esquerdo. Abra a pré-visualização de ativos e abra o painel esquerdo para acessar a visualização **[!UICONTROL Representações]**. As representações específicas no perfil de processamento, para as quais o tipo de ativo específico corresponde às regras de inclusão do tipo MIME, devem estar visíveis e acessíveis.

![execuções adicionais](assets/renditions-additional-renditions.png)

*Figura: Exemplo de duas execuções adicionais geradas por um perfil de processamento aplicado à pasta pai.*

## Workflows de pós-processamento {#post-processing-workflows}

Para situações em que é necessário um processamento adicional de ativos que não pode ser obtido usando os perfis de processamento, workflows adicionais pós-processamento podem ser adicionados à configuração. Isso permite adicionar processamento totalmente personalizado sobre o processamento configurável usando os microserviços de ativos.

Os workflows de pós-processamento, se configurados, são executados automaticamente por AEM após a conclusão do processamento dos microserviços. Não há necessidade de adicionar iniciadores de fluxo de trabalho manualmente para acioná-los. Os exemplos incluem:

* Etapas de fluxo de trabalho personalizadas para processar ativos.
* Integrações para adicionar metadados ou propriedades a ativos de sistemas externos, por exemplo, informações sobre produtos ou processos.
* Processamento adicional feito por serviços externos.

A adição de uma configuração de fluxo de trabalho de pós-processamento ao Experience Manager é composta das seguintes etapas:

* Crie um ou mais modelos de fluxo de trabalho. Os documentos o mencionam como *modelos de fluxo de trabalho pós-processamento*, mas esses são modelos de fluxo de trabalho Experience Manager.
* Adicione etapas específicas do fluxo de trabalho a esses modelos. As etapas são executadas nos ativos com base em uma configuração de modelo de fluxo de trabalho.
* Adicione a etapa [!UICONTROL Fluxo de trabalho do ativo de atualização do DAM Processo] concluído no final. A adição desta etapa garante que o Experience Manager saiba quando o processamento termina e que o ativo pode ser marcado como processado, ou seja, *New* é exibido no ativo.
* Crie uma configuração para o Serviço de Execução de Fluxo de Trabalho Personalizado que permita configurar a execução de um modelo de fluxo de trabalho de pós-processamento por um caminho (localização da pasta) ou por uma expressão regular.

### Criar modelos de fluxo de trabalho de pós-processamento {#create-post-processing-workflow-models}

Os modelos de fluxo de trabalho de pós-processamento são modelos regulares de fluxo de trabalho AEM. Crie modelos diferentes se precisar de processamento diferente para locais de repositório ou tipos de ativos diferentes.

As etapas de processamento devem ser adicionadas com base nas necessidades. Você pode usar quaisquer etapas compatíveis disponíveis, bem como quaisquer etapas de fluxo de trabalho implementadas por personalização.

Verifique se a última etapa de cada workflows de pós-processamento é `DAM Update Asset Workflow Completed Process`. A última etapa ajuda a garantir que o Experience Manager saiba quando o processamento de ativos é concluído.

### Configurar a execução do fluxo de trabalho pós-processamento {#configure-post-processing-workflow-execution}

Para configurar os modelos de fluxo de trabalho de pós-processamento a serem executados para ativos carregados ou atualizados no sistema após a conclusão do processamento dos microserviços de ativos, o serviço do Custom Workflow Runner precisa ser configurado.

O serviço Custom Workflow Runner (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) é um serviço OSGi e fornece duas opções para configuração:

* Workflows de pós-processamento por caminho (`postProcWorkflowsByPath`): Vários modelos de fluxo de trabalho podem ser listados, com base em diferentes caminhos de repositório. Caminhos e modelos devem ser separados por dois pontos. Caminhos de repositório simples são suportados e devem ser mapeados para um modelo de fluxo de trabalho no caminho `/var`. Por exemplo: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Workflows de pós-processamento por expressão (`postProcWorkflowsByExpression`): Vários modelos de fluxo de trabalho podem ser listados, com base em diferentes expressões regulares. Expressões e modelos devem ser separados por dois pontos. A expressão regular deve apontar diretamente para o nó Ativo, e não para uma das execuções ou arquivos. Por exemplo: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>A configuração do Custom Workflow Runner é uma configuração de um serviço OSGi. Consulte [implantar em Experience Manager](/help/implementing/deploying/overview.md) para obter informações sobre como implantar uma configuração OSGi.
>O console da Web OSGi, ao contrário das implantações de serviços no local e gerenciados de AEM, não está disponível diretamente nas implantações de serviços em nuvem.

Para obter detalhes sobre qual etapa de fluxo de trabalho padrão pode ser usada no fluxo de trabalho de pós-processamento, consulte [etapas de fluxo de trabalho no fluxo de trabalho de pós-processamento](developer-reference-material-apis.md#post-processing-workflows-steps) na referência do desenvolvedor.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* Considere suas necessidades para todos os tipos de execuções ao projetar workflows. Se você não prever a necessidade de uma representação no futuro, remova a etapa de criação do fluxo de trabalho. As execuções não podem ser excluídas em massa depois. As representações indesejadas podem ocupar muito espaço no armazenamento após o uso prolongado de [!DNL Experience Manager]. Para ativos individuais, você pode remover execuções manualmente da interface do usuário. Para vários ativos, você pode personalizar [!DNL Experience Manager] para excluir representações específicas ou excluir os ativos e carregá-los novamente.
* Atualmente, o suporte está limitado à geração de execuções. Não há suporte para a geração de novo ativo.

>[!MORELIKETHIS]
>
>* [Introdução ao Serviço](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html) de Asset computes.
>* [Entenda a extensibilidade e quando usá-la](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).
>* [Como criar aplicativos](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) personalizados.
>* [Tipos MIME suportados para vários casos](/help/assets/file-format-support.md) de uso.


<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
