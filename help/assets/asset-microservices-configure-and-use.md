---
title: Configurar e usar microsserviços de ativos
description: Configure e use os microsserviços de ativos nativos em nuvem para processar ativos em escala.
contentOwner: AG
feature: Microserviços do Asset compute, Fluxo de trabalho, Processamento de ativos
role: Architect,Administrator
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 4b9a48a053a383c2bf3cb5a812fe4bda8e7e2a5a
workflow-type: tm+mt
source-wordcount: '2635'
ht-degree: 1%

---

# Usar microsserviços de ativos e perfis de processamento {#get-started-using-asset-microservices}

Os microsserviços de ativos oferecem processamento escalável e resiliente de ativos usando aplicativos nativos em nuvem (também chamados de trabalhadores). O Adobe gerencia os serviços para obter o tratamento ideal de diferentes tipos de ativos e opções de processamento.

Os microsserviços de ativos permitem processar uma [ampla gama de tipos de arquivos](/help/assets/file-format-support.md) cobrindo mais formatos prontos para uso do que o possível com versões anteriores de [!DNL Experience Manager]. Por exemplo, a extração em miniatura de formatos PSD e PSB agora é possível, mas era necessária anteriormente soluções de terceiros, como [!DNL ImageMagick].

O processamento de ativos depende da configuração em **[!UICONTROL Perfis de processamento]**. O Experience Manager oferece uma configuração básica padrão e permite que os administradores adicionem configurações mais específicas de processamento de ativos. Os administradores criam, mantêm e modificam as configurações dos fluxos de trabalho de pós-processamento, incluindo a personalização opcional. Personalizar os fluxos de trabalho permite que os desenvolvedores estendam a oferta padrão.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Uma visão de alto nível do ](assets/asset-microservices-flow.png "processamento de ativosUma visão de alto nível do processamento de ativos")

>[!NOTE]
>
>O processamento de ativos descrito aqui substitui o modelo de fluxo de trabalho `DAM Update Asset` existente nas versões anteriores de [!DNL Experience Manager]. A maioria das etapas de geração de representação padrão e relacionadas a metadados é substituída pelo processamento de microsserviços de ativos e as etapas restantes, se houver, podem ser substituídas pela configuração de fluxo de trabalho de pós-processamento.

## Compreender as opções de processamento de ativos {#get-started}

[!DNL Experience Manager] O permite os seguintes níveis de processamento.

| Opção | Descrição | Casos de uso cobertos |
|---|---|---|
| [Configuração padrão](#default-config) | Está disponível como está e não pode ser modificado. Essa configuração fornece recursos de geração de representação muito básicos. | <ul> <li>Miniaturas padrão usadas pela interface do usuário [!DNL Assets] (48, 140 e 319 pixels) </li> <li> Visualização grande (renderização da Web - 1280 pixels) </li><li> Metadados e extração de texto.</li></ul> |
| [Configuração personalizada](#standard-config) | Configurado pelos administradores pela interface do usuário. Fornece mais opções para geração de representação estendendo a opção padrão. Estenda a opção pronta para uso para fornecer diferentes formatos e representações. | <ul><li>Representação de FPO. </li> <li>Alterar o formato do arquivo e a resolução das imagens</li> <li> Aplicar condicionalmente a tipos de arquivo configurados. </li> </ul> |
| [Perfil personalizado](#custom-config) | Configurado pelos administradores pela interface do usuário para usar o código personalizado por meio de aplicativos personalizados para chamar [Asset compute Service](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html). Suporta requisitos mais complexos em um método nativo em nuvem e dimensionável. | Consulte [casos de uso permitidos](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Formatos de arquivo não suportados {#supported-file-formats}

Os microsserviços de ativos oferecem suporte para uma grande variedade de formatos de arquivo para processar, gerar representações ou extrair metadados. Consulte [formatos de arquivo suportados](file-format-support.md) para obter a lista completa de tipos MIME e a funcionalidade suportada para cada tipo.

## Configuração padrão {#default-config}

Alguns padrões são pré-configurados para garantir que as renderizações padrão necessárias no Experience Manager estejam disponíveis. A configuração padrão também garante que as operações de extração de metadados e extração de texto estejam disponíveis. Os usuários podem começar a fazer upload ou atualizar ativos imediatamente e o processamento básico está disponível por padrão.

Com a configuração padrão, somente o perfil de processamento mais básico é configurado. Esse perfil de processamento não está visível na interface do usuário e você não pode modificá-lo. Ele sempre é executado para processar ativos carregados. Esse perfil de processamento padrão garante que o processamento básico exigido por [!DNL Experience Manager] seja concluído em todos os ativos.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Configuração padrão {#standard-config}

[!DNL Experience Manager] forneça recursos para gerar representações mais específicas para formatos comuns, de acordo com as necessidades do usuário. Um administrador pode criar [!UICONTROL Perfis de processamento] adicionais para facilitar essa criação de representação. Em seguida, os usuários atribuem um ou mais perfis disponíveis a pastas específicas para realizar o processamento adicional. Por exemplo, o processamento adicional pode gerar representações para Web, dispositivos móveis e tablets. O vídeo a seguir ilustra como criar e aplicar [!UICONTROL Perfis de processamento] e como acessar as representações criadas.

* **Largura e altura** da representação: A especificação de largura e altura da representação fornece tamanhos máximos da imagem de saída gerada. Os microsserviços de ativos tentam produzir a maior representação possível, que largura e altura não são maiores que a largura e a altura especificadas, respectivamente. A proporção é preservada, ou seja, a mesma do original. Um valor vazio significa que o processamento de ativos assume a dimensão de pixel do original.

* **Regras** de inclusão do tipo MIME: Quando um ativo com um tipo MIME específico é processado, o tipo MIME é verificado primeiro em relação ao valor de tipos MIME excluídos para a especificação de representação. Se corresponder a essa lista, essa representação específica não será gerada para o ativo (lista de bloqueios). Caso contrário, o tipo MIME será verificado em relação ao tipo MIME incluído e, se corresponder à lista, a representação será gerada (lista de permissões).

* **Representação** especial de FPO: Ao colocar ativos de grande porte  [!DNL Experience Manager] em  [!DNL Adobe InDesign] documentos, um profissional criativo aguarda por um tempo substancial após  [colocar um ativo](https://helpx.adobe.com/indesign/using/placing-graphics.html). Enquanto isso, o usuário está bloqueado de usar [!DNL InDesign]. Isso interrompe o fluxo criativo e afeta negativamente a experiência do usuário. O Adobe permite colocar temporariamente representações de pequeno porte em documentos [!DNL InDesign] para começar, o que pode ser substituído por ativos de resolução completa sob demanda posteriormente. [!DNL Experience Manager] O fornece representações que são usadas somente para posicionamento (FPO). Essas renderizações de FPO têm um tamanho de arquivo pequeno, mas têm a mesma proporção.

O perfil de processamento pode incluir uma representação FPO (Somente para posicionamento). Consulte [!DNL Adobe Asset Link] [documentação](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) para entender se você precisa ativá-la para seu perfil de processamento. Para obter mais informações, consulte a [documentação completa do Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html).

### Criar um perfil padrão {#create-standard-profile}

Para criar um perfil de processamento padrão, siga estas etapas:

1. Os administradores acessam **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de processamento]**. Clique em **[!UICONTROL Criar]**.
1. Forneça um nome que ajude você a identificar o perfil exclusivamente ao se aplicar a uma pasta.
1. Para gerar representações FPO, na guia **[!UICONTROL Standard]**, ative **[!UICONTROL Criar representação FPO]**. Insira um valor **[!UICONTROL Quality]** entre 1 e 100.
1. Para gerar outras representações, clique em **[!UICONTROL Adicionar Novo]** e forneça as seguintes informações:

   * Nome do arquivo de cada representação.
   * Formato de arquivo (PNG, JPEG, GIF ou WebP) de cada renderização.
   * Largura e altura em pixels de cada representação. Se os valores não forem especificados, será usado o tamanho total de pixel da imagem original.
   * Qualidade em porcentagem de cada renderização JPEG e WebP.
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

O [!DNL Asset Compute Service] é compatível com uma variedade de casos de uso, como processamento padrão, formatos específicos de Adobe como arquivos Photoshop e implementação de processamento personalizado ou específico da organização. A personalização do fluxo de trabalho do Ativo de atualização DAM necessária no passado é manipulada automaticamente ou por meio da configuração de perfis de processamento. Se as necessidades comerciais não forem atendidas por essas opções de processamento, a Adobe recomenda desenvolver e usar [!DNL Asset Compute Service] para estender os recursos padrão. Para obter uma visão geral, consulte [compreender extensibilidade e quando usá-la](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).

>[!NOTE]
>
>O Adobe recomenda usar um aplicativo personalizado somente quando os requisitos comerciais não puderem ser alcançados usando as configurações padrão ou o perfil padrão.

Ele pode transformar imagens, vídeos, documentos e outros formatos de arquivo em diferentes representações, incluindo miniaturas, texto e metadados extraídos e arquivos.

Os desenvolvedores podem usar o [!DNL Asset Compute Service] para [criar aplicativos personalizados](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) para os casos de uso suportados. [!DNL Experience Manager] O pode chamar esses aplicativos personalizados da interface do usuário usando perfis personalizados configurados pelos administradores. [!DNL Asset Compute Service] O suporta os seguintes casos de uso de invocar serviços externos:

* Use a [API do ImageCutout de [!DNL Adobe Photoshop] e salve o resultado como representação.](https://github.com/AdobeDocs/photoshop-api-docs-pre-release#imagecutout)
* Chame sistemas de terceiros para atualizar dados, por exemplo, um sistema PIM.
* Use a API [!DNL Photoshop] para gerar uma variedade de representações com base no modelo do Photoshop.
* Use [Adobe Lightroom API](https://github.com/AdobeDocs/lightroom-api-docs#supported-features) para otimizar os ativos assimilados e salvá-los como representações.

>[!NOTE]
>
>Não é possível editar os metadados padrão usando os aplicativos personalizados. Você só pode modificar metadados personalizados.

### Criar um perfil personalizado {#create-custom-profile}

Para criar um perfil personalizado, siga estas etapas:

1. Os administradores acessam **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de processamento]**. Clique em **[!UICONTROL Criar]**.
1. Clique na guia **[!UICONTROL Personalizado]**. Clique em **[!UICONTROL Adicionar Novo]**. Forneça o nome de arquivo desejado para a representação.
1. Forneça as seguintes informações.

   * Nome do arquivo de cada renderização e uma extensão de arquivo compatível.
   * [URL de ponto final de um aplicativo](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html) personalizado Firefly. O aplicativo deve ser da mesma organização da conta do Experience Manager.
   * Adicionar Parâmetros de Serviço a [transmitir informações ou parâmetros adicionais ao aplicativo personalizado](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend).
   * Tipos MIME incluídos e excluídos para limitar o processamento a alguns formatos de arquivo específicos.

   Clique em **[!UICONTROL Salvar]**.

Os aplicativos personalizados são aplicativos sem cabeçalho [Project Firefly](https://github.com/AdobeDocs/project-firefly). O aplicativo personalizado obtém todos os arquivos fornecidos se eles estiverem configurados com um perfil de processamento. O aplicativo deve filtrar os arquivos.

>[!CAUTION]
>
>Se o aplicativo Firefly e a conta [!DNL Experience Manager] não forem da mesma organização, a integração não funcionará.

### Um exemplo de um perfil personalizado {#custom-profile-example}

Para ilustrar o uso do perfil personalizado, vamos considerar um caso de uso para aplicar texto personalizado às imagens da campanha. Você pode criar um perfil de processamento que aproveite a API do Photoshop para editar as imagens.

A integração do Asset compute Service permite que o Experience Manager transmita esses parâmetros para o aplicativo personalizado usando o campo [!UICONTROL Parâmetros de Serviço]. O aplicativo personalizado chama a API do Photoshop e transmite esses valores para a API. Por exemplo, é possível passar o nome da fonte, a cor do texto, o peso do texto e o tamanho do texto para adicionar o texto personalizado às imagens da campanha.

<!-- TBD: Check screenshot against the interface. -->

![perfil de processamento personalizado](assets/custom-processing-profile.png)

*Figura: Use o campo  [!UICONTROL Service ] Parameters para transmitir informações adicionais para parâmetros predefinidos incorporados no aplicativo personalizado. Neste exemplo, quando imagens de campanha são carregadas, as imagens são atualizadas com o texto `Jumanji` na fonte `Arial-BoldMT`.*

## Usar perfis de processamento para processar ativos {#use-profiles}

Crie e aplique perfis de processamento adicionais e personalizados a pastas específicas para que o Experience Manager processe ativos carregados ou atualizados nessas pastas. O perfil de processamento padrão integrado é sempre executado, mas não é visível na interface do usuário. Se você adicionar um perfil personalizado, ambos os perfis serão usados para processar os ativos carregados.

Aplique perfis de processamento a pastas usando um dos seguintes métodos:

* Os administradores podem selecionar uma definição de perfil de processamento em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de processamento]** e usar a ação **[!UICONTROL Aplicar perfil à(s) pasta(s)]**. Ele abre um navegador de conteúdo que permite navegar para pastas específicas, selecioná-las e confirmar o aplicativo do perfil.
* Os usuários podem selecionar uma pasta na interface do usuário do Assets, usar a ação **[!UICONTROL Propriedades]** para abrir a tela de propriedades da pasta, clicar na guia **[!UICONTROL Perfis de processamento]** e, na lista pop-up, selecionar o perfil de processamento apropriado para essa pasta. Para salvar as alterações, clique em **[!UICONTROL Salvar e fechar]**.
   ![Aplicar perfil de processamento a uma pasta na guia Propriedades do ativo](assets/folder-properties-processing-profile.png)

>[!TIP]
>
>Somente um perfil de processamento pode ser aplicado a uma pasta. Para gerar mais representações, adicione mais definições de representação ao perfil de processamento existente.

Depois que um perfil de processamento é aplicado a uma pasta, todos os novos ativos carregados (ou atualizados) nessa pasta ou em qualquer subpasta dela são processados usando o perfil de processamento adicional configurado. Esse processamento está além do perfil padrão.

>[!NOTE]
>
>Um perfil de processamento aplicado a uma pasta funciona para a árvore inteira, mas pode ser substituído por outro perfil aplicado a uma subpasta. Quando os ativos são carregados em uma pasta, o Experience Manager verifica as propriedades da pasta contêiner em busca de um perfil de processamento. Se nenhuma for aplicada, uma pasta pai na hierarquia será verificada em busca de um perfil de processamento a ser aplicado.

Para verificar se os ativos são processados, visualize as representações geradas na visualização [!UICONTROL Representações] no painel esquerdo. Abra a visualização de ativos e abra o painel à esquerda para acessar a visualização **[!UICONTROL Representações]**. As representações específicas no perfil de processamento, para as quais o tipo de ativo específico corresponde às regras de inclusão do tipo MIME, devem ser visíveis e acessíveis.

![representações adicionais](assets/renditions-additional-renditions.png)

*Figura: Exemplo de duas representações adicionais geradas por um perfil de processamento aplicado à pasta pai.*

## Fluxos de trabalho de pós-processamento {#post-processing-workflows}

Para uma situação em que é necessário um processamento adicional de ativos que não pode ser obtido usando os perfis de processamento, é possível adicionar mais workflows pós-processamento à configuração. Isso permite adicionar processamento totalmente personalizado sobre o processamento configurável usando microsserviços de ativos.

Os workflows de pós-processamento, se configurados, são executados automaticamente por [!DNL Experience Manager] após a conclusão do processamento de microsserviços. Não há necessidade de adicionar iniciadores de fluxo de trabalho manualmente para acionar os fluxos de trabalho. Os exemplos incluem:

* Etapas de fluxo de trabalho personalizadas para processar ativos.
* Integrações para adicionar metadados ou propriedades a ativos de sistemas externos, por exemplo, informações de produto ou processo.
* Processamento adicional feito por serviços externos.

Para adicionar uma configuração de workflow de pós-processamento a [!DNL Experience Manager], siga estas etapas:

* Crie um ou mais modelos de fluxo de trabalho. Esses modelos personalizados são chamados de *pós-processamento de modelos de fluxo de trabalho* nesta documentação. Esses são modelos de fluxo de trabalho [!DNL Experience Manager] comuns.
* Adicione as etapas de fluxo de trabalho necessárias a esses modelos. Revise as etapas do fluxo de trabalho padrão e adicione todas as etapas padrão necessárias ao fluxo de trabalho personalizado. As etapas são executadas nos ativos com base em uma configuração de modelo de fluxo de trabalho. Por exemplo, se você deseja que a marcação inteligente ocorra automaticamente após o upload do ativo, adicione a etapa ao modelo de fluxo de trabalho de pós-processamento personalizado.
* Adicione a etapa [!UICONTROL Fluxo de trabalho de ativos de atualização do DAM concluída Processo] no final. Adicionar essa etapa garante que o Experience Manager saiba quando o processamento termina e o ativo pode ser marcado como processado, ou seja, *New* é exibido no ativo.
* Crie uma configuração para o Custom Workflow Runner Service que permite configurar a execução de um modelo de fluxo de trabalho de pós-processamento por um caminho (local da pasta) ou por uma expressão regular.

### Criar modelos de fluxo de trabalho de pós-processamento {#create-post-processing-workflow-models}

Os modelos de fluxo de trabalho de pós-processamento são [!DNL Experience Manager] modelos de fluxo de trabalho comuns. Crie modelos diferentes se precisar de processamento diferente para locais de repositório ou tipos de ativos diferentes.

As etapas de processamento devem ser adicionadas com base nas necessidades. Você pode usar qualquer etapa suportada disponível, bem como qualquer etapa de fluxo de trabalho implementada por personalização.

Certifique-se de que a última etapa de cada fluxo de trabalho de pós-processamento seja `DAM Update Asset Workflow Completed Process`. A última etapa ajuda a garantir que o Experience Manager saiba quando o processamento de ativos é concluído.

### Configurar a execução do workflow de pós-processamento {#configure-post-processing-workflow-execution}

Depois que os microsserviços de ativos concluírem o processamento dos ativos carregados, você poderá definir o pós-processamento para processar mais alguns ativos. Para configurar o pós-processamento usando modelos de fluxo de trabalho, você pode executar um dos seguintes procedimentos:

* Configure o serviço Custom Workflow Runner.
* Aplique um modelo de fluxo de trabalho na pasta [!UICONTROL Propriedades].

O Adobe CQ DAM Custom Workflow Runner (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) é um serviço OSGi e fornece duas opções para configuração:

* Fluxos de trabalho de pós-processamento por caminho (`postProcWorkflowsByPath`): Vários modelos de fluxo de trabalho podem ser listados, com base em caminhos de repositório diferentes. Separe caminhos e modelos usando dois pontos. Caminhos de repositório simples são compatíveis. Mapeie-os para um modelo de fluxo de trabalho no caminho `/var`. Por exemplo: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Fluxos de trabalho de pós-processamento por expressão (`postProcWorkflowsByExpression`): Vários modelos de fluxo de trabalho podem ser listados, com base em diferentes expressões regulares. As expressões e os modelos devem ser separados por dois pontos. A expressão regular deve apontar para o nó do ativo diretamente, e não para uma das representações ou arquivos. Por exemplo: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>A configuração do Executor de Fluxo de Trabalho Personalizado é uma configuração de um serviço OSGi. Consulte [implantar no Experience Manager](/help/implementing/deploying/overview.md) para obter informações sobre como implantar uma configuração OSGi.
>O console da Web OSGi, ao contrário das implantações locais e de serviços gerenciados de [!DNL Experience Manager], não está disponível diretamente nas implantações do serviço de nuvem.

Para aplicar um modelo de fluxo de trabalho na pasta [!UICONTROL Properties], siga estas etapas:

1. Crie um modelo de fluxo de trabalho.
1. Selecione uma pasta, clique em **[!UICONTROL Propriedades]** na barra de ferramentas e, em seguida, clique na guia **[!UICONTROL Processamento de Ativos]**.
1. Em **[!UICONTROL Fluxo de trabalho de início automático]**, selecione o fluxo de trabalho necessário, forneça um título do fluxo de trabalho e salve as alterações.

Para obter detalhes sobre qual etapa de fluxo de trabalho padrão pode ser usada no fluxo de trabalho de pós-processamento, consulte [etapas do fluxo de trabalho no fluxo de trabalho de pós-processamento](developer-reference-material-apis.md#post-processing-workflows-steps) na referência do desenvolvedor.

## Práticas recomendadas e limitações {#best-practices-limitations-tips}

* Considere suas necessidades para todos os tipos de representações ao projetar fluxos de trabalho. Se você não prever a necessidade de uma representação no futuro, remova sua etapa de criação do fluxo de trabalho. As representações não podem ser excluídas em massa posteriormente. As representações indesejadas podem ocupar muito espaço de armazenamento após o uso prolongado de [!DNL Experience Manager]. Para ativos individuais, você pode remover as renderizações manualmente da interface do usuário. Para vários ativos, você pode personalizar [!DNL Experience Manager] para excluir representações específicas ou excluir os ativos e carregá-los novamente.
* Atualmente, o suporte está limitado à geração de representações. Não há suporte para a geração de novo ativo.
* Atualmente, o limite de tamanho do arquivo para extração de metadados é de aproximadamente 10 GB. Ao fazer upload de ativos muito grandes, às vezes a operação de extração de metadados falha.

>[!MORELIKETHIS]
>
>* [Introdução ao Asset compute Service](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html).
>* [Entenda a extensibilidade e quando usá-la](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).
>* [Como criar aplicativos](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) personalizados.
>* [Tipos MIME suportados para vários casos](/help/assets/file-format-support.md) de uso.


<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
