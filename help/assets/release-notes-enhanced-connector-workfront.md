---
title: Notas da versão [!DNL Workfront for Experience Manager enhanced connector]
description: Notas da versão [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 14b779c476b88ff1ee9d2798296add14f337dbfa
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 2%

---

# Notas da versão [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

A seção a seguir descreve as Notas de versão gerais de [!DNL Workfront for Experience Manager enhanced connector].

## Data de lançamento {#release-date}

A data de lançamento da versão mais recente 1.9.3 do [!DNL Workfront for Experience Manager enhanced connector] é 16 de setembro de 2022.

## Destaques da versão {#release-highlights}

A versão mais recente do [!DNL Workfront for Experience Manager enhanced connector] O inclui os seguintes aprimoramentos e correções de erros:

* Não é possível carregar um arquivo com mais de 8 GB.
* Problemas ao publicar automaticamente ativos que são enviados do Workfront para o AEM.
* O campo Caminho raiz não está disponível para o campo Tags durante a edição de um Formulário de esquema de metadados padrão.
* Problemas ao adicionar novas versões no Workfront usando AEM workflows.
* Ao executar uma pesquisa AEM por ativos disponíveis no Workfront, AEM exibe uma mensagem de erro.
* Quando você cria um workflow AEM para criação de tarefa a partir de um ativo e não define um nome de tarefa pai, a tarefa não é criada no Workfront.



>[!IMPORTANT]
>
>O Adobe recomenda [atualizar para a versão 1.9.3 mais recente](../assets/update-workfront-enhanced-connector.md) do [!DNL Workfront for Experience Manager enhanced connector].

## Problemas conhecidos {#known-issues}

* Ao configurar pastas vinculadas ao projeto com o AEM 6.4, o Experience Manager não salva os valores para **[!UICONTROL subpastas]** e **[!UICONTROL Criar pasta vinculada em projetos com portfólio]** campos. O valor da variável **[!UICONTROL subpastas]** atualizações de campo para **[!UICONTROL indefinido]** e o valor da variável **[!UICONTROL Criar pasta vinculada em projetos com portfólio]** atualizações de campo para **[!UICONTROL Portfolio padrão]** automaticamente após salvar a configuração.

* Quando estiver usando a experiência clássica do Workfront, a variável **[!UICONTROL Enviar para]** disponível na **[!UICONTROL Mais]** a lista suspensa não permite selecionar o destino desejado no Experience Manager. O **[!UICONTROL Enviar para]** A opção funciona corretamente usando o **[!UICONTROL Ações do documento]** lista suspensa. O **[!UICONTROL Enviar para]** A opção funciona corretamente para **[!UICONTROL Mais]** lista suspensa, bem como a **[!UICONTROL Ações do documento]** lista suspensa disponível na nova experiência do Workfront.

* O Workfront exibe um `SERVER_ERROR` ao vincular documentos ao AEM após a atualização para a versão 8316. Para resolver o problema, atribua `rep:readProperties` para `content/dam/collections` para `wf-workfront-user` Grupo de usuários AEM.

## Versões anteriores {#previous-releases}

### Versão de agosto de 2022 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.2, lançada em agosto de 2003, inclui as seguintes atualizações:

* O **[!UICONTROL Fazer upload do documento]** falha na etapa do fluxo de trabalho ao anexar um documento ao Workfront.

* O **[!UICONTROL Fazer upload do documento]** A etapa do fluxo de trabalho não anexa um documento a Tarefas e Problemas no Workfront. A etapa do fluxo de trabalho anexa um documento aos Projetos com êxito.

### Versão de julho de 2022 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.1 inclui as seguintes atualizações:

* Adição de suporte para autenticação entre aplicativos Experience Manager e Workfront usando a chave de API Workfront para instâncias migradas para o Adobe IMS.

* Quando você vincula arquivos ou pastas externos, o aplicativo Workfront exibe a variável `SERVER_ERROR` mensagem de erro. A mensagem de erro se refere a uma exceção não autorizada devido a uma incompatibilidade nas chaves da API.

* Quando você executa um fluxo de trabalho Criar tarefa para um ativo, a exceção de Ponteiro nulo é exibida nas mensagens de log.

* Ao ativar a variável `Replace Spaces with DASH` opção de configuração em Configurações avançadas no Experience Manager, resulta na criação de pastas duplicadas no Workfront.

### Versão de junho de 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] O agora inclui as seguintes atualizações:

* Ao fazer upload por meio de uma pasta vinculada ou usar o `Send To` ação disponível no Workfront para fazer upload de ativos no Experience Manager as a Cloud Service, os ativos são corrompidos e não podem ser abertos no Adobe Photoshop.

### Versão de março de 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] O agora inclui as seguintes atualizações:

* Agora é possível criar pastas vinculadas entre o Adobe Workfront e o AEM Assets as a Cloud Service, mesmo se houver várias configurações de pastas vinculadas ao projeto.

* Adição de suporte para paginação de assinatura de evento.

* Adição de suporte para AEM 6.4.x.

* Adição de suporte para ambientes proxy.

* Várias correções de erros com base no feedback de parceiros e clientes.

>[!MORELIKETHIS]
>
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] com o Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] com o Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)

