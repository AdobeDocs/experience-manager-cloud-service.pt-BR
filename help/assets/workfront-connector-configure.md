---
title: Configurar [!DNL Workfront for Experience Manager enhanced connector]
description: Configurar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: d4e1247a-342c-4bc4-83bf-4e4902468fb3
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 1%

---

# Configurar o [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-configure.html) |
| AEM as a Cloud Service | Este artigo |

Um usuário com acesso de administrador no [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] configura o conector aprimorado após instalá-lo. Para obter instruções de instalação, consulte [Instalar o conector](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
> A partir de junho de 2022, a Adobe lançou uma nova integração nativa para conectar o Workfront ao Adobe Experience Manager Assets as a Cloud Service. Essa integração se tornou o método necessário para conectar essas duas soluções. Qualquer nova implementação futura do conector aprimorado (1.9.8 e posterior) para conectar o Workfront com o AEM Assets as a Cloud Service está bloqueada.

>[!IMPORTANT]
>
>* A Adobe requer a implantação e a configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por meio de parceiros certificados ou [!DNL Adobe Professional Services]. Se implantada e configurada sem um parceiro certificado ou [!DNL Adobe Professional Services], não é suportada pela Adobe.
>
>* A Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam este conector redundante; se isso ocorrer, pode ser necessário que os clientes façam a transição do uso deste conector.
>
>* O Adobe oferece suporte às versões avançadas de conectores 1.7.4 e superiores. As versões anteriores de pré-lançamento e personalizadas não são compatíveis. Para verificar a versão aprimorada do conector, consulte a etapa 5(a) de [instruções de instalação do conector aprimorado](workfront-connector-install.md).
>
>* Consulte [Exame de certificação de parceiro para o conector aprimorado do Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte o [Guia do Exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Configurar assinaturas de evento {#event-subscriptions}

Inscrições em eventos são usadas para notificar a AEM sobre eventos que ocorrem em [!DNL Adobe Workfront]. Existem três recursos [!DNL Workfront for Experience Manager enhanced connector] que precisam de assinaturas de evento para funcionar:

* Criação automática de pastas vinculadas ao projeto.
* Sincronização de alterações nos valores de formulário personalizado do documento do Workfront com os metadados de ativos do AEM.
* Publicação automática de ativos no Brand Portal após a conclusão do projeto.

Para usar esses recursos, habilite as assinaturas de evento.

* Edite a configuração do [!UICONTROL Workfront Tools] Cloud Services criada na etapa 5 e selecione a guia [!UICONTROL Assinaturas de Eventos].
* Selecione a [!UICONTROL Integração personalizada do Workfront] que você criou na seção 6.
* Clique em [!UICONTROL Habilitar assinaturas de eventos do Workfront].

  ![Assinatura de evento](/help/assets/assets/event-subs.png)

## Configurar pastas vinculadas {#linked-folders}

Para se inscrever nos eventos, siga estas etapas:

1. Navegue até a guia **[!UICONTROL Assinaturas de Eventos]** nos serviços em nuvem.
1. Selecione a integração personalizada criada em [!DNL Workfront].
1. Clique em **[!UICONTROL Habilitar assinaturas de eventos do Workfront]**.

### Configuração da estrutura de pastas vinculada {#linked-folder-structure}

1. Acesse a guia Pastas vinculadas do projeto nos serviços em nuvem.
1. Caminho principal da pasta vinculada: selecione uma pasta no DAM onde deseja criar as pastas vinculadas. Se deixado em branco, o padrão será /content/dam. Verifique se o esquema de metadados das Ferramentas do Workfront e o esquema de metadados da pasta vinculada do Workfront foram aplicados à pasta selecionada.
1. Estrutura de pasta vinculada: insira valores separados por vírgula. Cada valor deve ser `DE:<some-project-custom-form-field>`, Portfolio, Program, Year, Name ou algum &quot;Valor de sequência de caracteres literais&quot; (este último com aspas). No momento, está definido como Portfolio, Programa, Ano, DE:Tipo de projeto, Nome.
1. Configurar permissões: Adicionar permissões de `jcr:all permissions` a `/conf/workfront-tools/settings/cloudconfigs` para o grupo `wf-workfront-users`.
1. Criar título de pasta vinculado no Workfront usando a caixa de seleção de nomes de estrutura de pastas deve ser marcada se o título da pasta no Workfront deve incluir todas as pastas na estrutura. Caso contrário, será o título da última pasta.
1. Sub-folders multifield permite especificar uma lista de pastas que devem ser criadas como uma pasta filho da pasta vinculada.
1. Status do projeto: selecione o status para o qual o projeto deve ser definido para criar a pasta vinculada.
1. Criar uma pasta vinculada em projetos com portfólio: lista de portfólios aos quais o projeto deve pertencer para que você possa criar a pasta vinculada. Deixe essa lista vazia para criar a pasta vinculada para todos os portfólios de projetos.
1. Criar uma pasta vinculada em projetos com campo de formulário personalizado: o campo de formulário personalizado e seu valor correspondente que o projeto deve ter para que você possa criar a pasta vinculada. Essa configuração será ignorada se for deixada vazia. Selecione `CUSTOM FORMS: Create DAM Linked Folder` para o campo e insira `Yes` para o valor.
1. Configurar permissão: configure essas permissões, `jcr:all permissions for /conf/workfront-tools/settings/cloudconfigs` para o `wf-workfront-users group`.
1. Clique em Habilitar criação automática de pastas vinculadas. Volte para a guia Assinaturas de eventos e veja que agora há um evento de criação.

![configuração de pasta vinculada](/help/assets/assets/wf-linked-folder-config.png)

## Mapeamento de esquema de metadados {#metadata-schema-mapping}

### Configurar mapeamento de metadados da pasta {#folder-metadata-mapping}

O mapeamento de metadados entre Projetos Workfront e Pastas AEM é definido nos Esquemas de metadados de pasta AEM. Os esquemas de metadados de pasta devem ser criados e configurados como de costume no AEM. O Workfront Tools adiciona uma lista suspensa de preenchimento automático à guia Configurações de cada campo de formulário de esquema de metadados de pasta. Esse menu suspenso de preenchimento automático permitirá especificar para qual campo do Workfront cada propriedade de pasta do AEM deve ser mapeada.

Para configurar os mapeamentos, siga estas etapas:

1. Adicionar permissões de `jcr:read` a `/conf/global/settings/dam/adminui-extension/foldermetadataschema` para o grupo `wf-workfront-users`.
1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de Metadados de Pasta]**.
1. Selecione o formulário de esquema de metadados da pasta que deseja editar e clique em Editar.
1. Selecione o campo de formulário de esquema de metadados da pasta que deseja editar e selecione a guia Configurações no painel direito.
1. No campo [!UICONTROL Mapeado do Campo do Workfront], selecione o nome do campo do Workfront que você deseja mapear para a propriedade de pasta selecionada do AEM. As opções disponíveis são:

   * Campos de formulário personalizado do projeto
   * Campos de Visão Geral do Projeto (ID, Nome, Descrição, Número de Referência, Data de Conclusão Planejada, Proprietário do Projeto, Patrocinador do Projeto, Portfolio ou Programa)

![configuração de mapeamento de metadados](/help/assets/assets/wf-metadata-mapping-config2.png)

### Configurar o mapeamento de metadados de ativos {#asset-metadata-mapping}

O mapeamento de metadados entre os documentos do Adobe Workfront e o Assets é definido nos Esquemas de metadados do AEM. Os esquemas de metadados devem ser criados e configurados como de costume no AEM. O Workfront Tools adiciona opções de configuração à guia Configurações de cada campo de formulário de esquema de metadados. Essas opções permitirão especificar para qual campo do Workfront cada propriedade do AEM deve ser mapeada.

Para configurar os mapeamentos, siga estas etapas:

1. Navegue até **Ferramentas** > **Assets** > **Esquemas de Metadados**.
1. Selecione o formulário de esquema de metadados que deseja editar e clique em **Editar** ou crie um esquema de metadados do zero.
1. Selecione o campo de formulário de esquema de metadados que deseja editar e selecione a guia **Configurações** no painel direito.
1. No Campo de Formulário Personalizado [!DNL Workfront], selecione o nome do campo [!DNL Workfront] que você deseja mapear para a propriedade do AEM selecionada. As opções disponíveis são:

   * Campos de formulário personalizado de documento
   * Campos de formulário personalizado do projeto
   * Emitir campos de formulário personalizados
   * Campos de formulário personalizado de tarefa
   * Campos de Visão Geral do Projeto (ID, Nome, Descrição ou Número de Referência)

1. Se o campo [!DNL Workfront] selecionado no [!UICONTROL Campo de formulário personalizado do Workfront] for um campo de tipo antecipado do usuário do Workfront, será necessário especificar qual campo de usuário do Workfront você deseja mapear. Para fazer isso, marque Obter valor do campo de objeto referenciado do Workfront e especifique o nome do [!UICONTROL Campo de Formulário personalizado do usuário do Workfront] do qual recuperar o valor a ser mapeado.

   ![configuração de mapeamento de metadados](/help/assets/assets/wf-metadata-mapping-config1.png)

## Mapear propriedade {#map-property}

Esta etapa do fluxo de trabalho permite que um usuário mapeie uma propriedade para um formulário personalizado [!DNL Workfront] em um projeto, tarefa, problema ou documento. O artefato [!DNL Workfront] que esta etapa afeta é pesquisado usando um caminho relativo da carga. As propriedades a serem mapeadas são controladas na configuração da caixa de diálogo de etapas.

**Tipo**: este campo permite selecionar o tipo de objeto do Workfront para o qual as propriedades devem ser mapeadas.

**Propriedade de ID**: este campo permite que você especifique o caminho para a ID do objeto Workfront para o qual as propriedades devem ser mapeadas. O caminho especificado neste campo deve ser relativo à carga do fluxo de trabalho.

**Atribuições de propriedade**: este multicampo permite especificar os mapeamentos entre as propriedades do AEM e os campos do Workfront. Cada item no multicampo especificará um mapeamento. Cada mapeamento deve ter o formato `<workfront-field>=<aem-mapped-property>`.

* O `workfront-field` pode ser

   * Um campo de formulário personalizado identificado pelo prefixo `DE:`.
   * Um campo editável identificado por seu nome. Os nomes de campos são encontrados no [[!DNL Workfront] explorador de API](https://experience.workfront.com/s/api-explorer).

* O `aem-mapped-property` pode ser:

   * Um valor literal. Elas devem estar entre aspas.
   * Uma propriedade do AEM. Essa referência deve ser relativa à carga do workflow.
   * Um valor nomeado. Eles devem estar entre colchetes.
   * Uma concatenação dos 3 itens acima. Especifique usando `{+}`.
   * Uma alteração dos 3 itens acima ao cercar o valor com `{replace(<value>,"old-char","new-char")}`.

* Alguns exemplos são:

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![Configuração para mapear a propriedade](/help/assets/assets/wf-map-property-config.png)

## Definir status {#set-status}

No editor de fluxo de trabalho, edite as propriedades de **[!UICONTROL Workfront - Definir Status]** na guia **[!UICONTROL Argumentos]**.

![Editar fluxo de trabalho para definir o status](/help/assets/assets/wf-set-status.png)

## Sincronização de comentários {#comments-sync}

1. Em [!DNL Experience Manager], acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da Nuvem]** > **[!UICONTROL Configuração de Ferramentas do Workfront]**, selecione a configuração e selecione **[!UICONTROL Propriedades]**.

   ![sincronização de comentários](/help/assets/assets/comments-sync1.png)

1. Selecione a guia **[!UICONTROL Assinaturas de Eventos]**, clique na opção **[!UICONTROL Habilitar Sincronização de Comentários]** em **[!UICONTROL Enviar Comentários feitos no Workfront para o AEM]**.

   ![Sincronização habilitada](/help/assets/assets/wf-comment-sync-enabled.png)

Para testar a sincronização de comentários do Workfront com o AEM, siga estas etapas:

1. Navegue até um documento vinculado no Workfront e adicione um comentário na guia Atualizações.

   ![deixar comentário no Workfront](/help/assets/assets/comments-sync2.png)

1. Navegue até o mesmo documento vinculado no AEM, selecione o documento, abra a opção [!UICONTROL Linha do Tempo] na navegação à esquerda e selecione [!UICONTROL Comentários]. A barra lateral esquerda exibe os comentários sincronizados de [!DNL Workfront].

## Versões do ativo {#asset-versions}

Para manter o histórico de versões de ativos no AEM, configure o controle de versão de ativos no AEM.

1. No Experience Manager, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da Nuvem]** > **[!UICONTROL Configuração de Ferramentas do Workfront]** e abra a guia **[!UICONTROL Avançado]**.

1. Selecione a opção **[!UICONTROL Armazenar ativos com o mesmo nome das versões do ativo existente]**. Quando marcada, essa opção permite armazenar ativos carregados com o mesmo nome e no mesmo local que a versão do ativo existente. Se deixado desmarcado, um novo ativo é criado com um nome diferente (por exemplo, `asset-name.pdf` e `asset-name-1.pdf`).

1. Selecione a opção **[!UICONTROL Atualizar metadados de ativos ao criar uma nova versão]**. Quando marcada, essa opção atualiza os metadados do ativo sempre que uma nova versão do ativo é criada. Se desmarcado, o ativo manterá os metadados que tinha antes da criação da nova versão.

![configurar o controle de versão do ativo](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>Não há suporte para o controle de versão em pastas vinculadas. Ao criar uma prova do [!DNL Workfront] com um documento dentro de uma pasta vinculada, os comentários e as anotações na versão anterior do ativo são removidos.

## Anexar formulários personalizados {#attach-custom-forms}

Esta etapa do fluxo de trabalho permite que os usuários anexem um formulário personalizado a um artefato do [!DNL Workfront]. Essa etapa do fluxo de trabalho pode ser adicionada a qualquer modelo de fluxo de trabalho. O artefato [!DNL Workfront] que esta etapa afeta é pesquisado usando um caminho relativo da carga.

No editor de fluxo de trabalho do Experience Manager, edite as propriedades da etapa de fluxo de trabalho [!UICONTROL Workfront - Anexar formulário personalizado].

![formulários personalizados](/help/assets/assets/wf-custom-forms.png).

## Publicar ativos automaticamente {#auto-publish-assets}

1. No Experience Manager, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da Nuvem]** > **[!UICONTROL Configuração de Ferramentas do Workfront]** e abra a guia **[!UICONTROL Avançado]**.

1. Selecione **[!UICONTROL Publicar ativos automaticamente quando enviados do Workfront]**. Essa opção permite a publicação automática de ativos quando eles são enviados do Workfront para o AEM. Esse recurso pode ser ativado condicionalmente especificando um campo de formulário personalizado do Workfront e o valor para o qual ele deve ser definido. Sempre que um documento é enviado para o AEM, se ele atender à condição, o ativo será publicado automaticamente.

1. Selecione **[!UICONTROL Publicar todos os ativos do projeto no Brand Portal após a conclusão do projeto]**. Esta opção habilita a publicação automática de ativos em [!DNL Brand Portal] quando o status do projeto do Workfront ao qual eles pertencem é alterado para `Complete`.

![configurar publicação automática](/help/assets/assets/wf-auto-publish-config.png)

## Atualizações de formulário personalizado de documento do Workfront {#subscribe-workfront-doc-custom-form-updates}

Para assinar as alterações feitas nos formulários personalizados de documentos do [!DNL Workfront], selecione a opção relevante na guia **[!UICONTROL Avançado]**. Quando você assina essas atualizações, ele atualiza os campos de metadados [!DNL Experience Manager] mapeados quando o campo correspondente no formulário personalizado do documento [!DNL Workfront] é alterado.

![Configuração de atualizações de formulário personalizado de documento do Workfront em [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
