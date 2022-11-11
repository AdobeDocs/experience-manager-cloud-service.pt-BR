---
title: Notas da versão [!DNL Workfront for Experience Manager enhanced connector]
description: Notas da versão [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 31198a1279e07d0a1afe41100d3cfe59d02fd686
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 1%

---

# Notas da versão [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

A seção a seguir descreve as Notas de versão gerais de [!DNL Workfront for Experience Manager enhanced connector].

## Data de lançamento {#release-date}

A data de lançamento da versão mais recente 1.9.5 do [!DNL Workfront for Experience Manager enhanced connector] é 11 de novembro de 2022.

## Destaques da versão {#release-highlights}

A versão mais recente do [!DNL Workfront for Experience Manager enhanced connector] O inclui os seguintes aprimoramentos e correções de erros:

* Ao definir apenas um valor para um campo de vários valores no Workfront, o valor do campo não é mapeado adequadamente para Experience Manager.

* Experience Manager exibe a `SERVER_ERROR` no **[!UICONTROL Vincular arquivos e pastas externos]** ao acessar as pastas de ativos devido a permissões inválidas em `/content/dam/collections`.

* Ativar o **[!UICONTROL Publicar ativos no Brand Portal]** na página Configuração de conector aprimorado do Workfront, um evento é criado incorretamente. O evento não é excluído mesmo após a desativação da opção .

   Para resolver o problema:

   1. Atualize para a versão 1.9.5 do conector aprimorado.

   1. Desative o **[!UICONTROL Publicar ativos no Brand Portal]** em configurações avançadas.

   1. Ative o **[!UICONTROL Publicar ativos no Brand Portal]** opção.

   1. Exclua as assinaturas de evento incorretas.

      1. Executar chamadas GET para `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         Execute uma chamada de API para cada número de página.

      1. Procure o seguinte texto para localizar assinaturas de evento que correspondam ao seguinte URL e não tenham uma `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         Certifique-se de que o conteúdo entre `"objId": "",` e `"url"` corresponde à resposta JSON. O método recomendado para fazer isso é copiar de qualquer Assinatura de evento que tenha uma `objId` e, em seguida, exclua o número.

      1. Observe a ID de assinatura do evento.

      1. Exclua a assinatura de evento incorreta. Faça uma chamada de Excluir API para `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` como o código de resposta significa exclusão bem-sucedida de assinaturas de evento incorretas.
   >[!NOTE]
   >
   >Se você já tiver excluído as assinaturas de evento incorretas antes de executar as etapas mencionadas neste procedimento, ignore a última etapa deste procedimento.


>[!IMPORTANT]
>
>O Adobe recomenda [atualizar para a versão 1.9.5 mais recente](../assets/update-workfront-enhanced-connector.md) do [!DNL Workfront for Experience Manager enhanced connector].

## Problemas conhecidos {#known-issues}

* Ao configurar pastas vinculadas ao projeto com o AEM 6.4, o Experience Manager não salva os valores para **[!UICONTROL subpastas]** e **[!UICONTROL Criar pasta vinculada em projetos com portfólio]** campos. O valor da variável **[!UICONTROL subpastas]** atualizações de campo para **[!UICONTROL indefinido]** e o valor da variável **[!UICONTROL Criar pasta vinculada em projetos com portfólio]** atualizações de campo para **[!UICONTROL Portfolio padrão]** automaticamente após salvar a configuração.

* Quando estiver usando a experiência clássica do Workfront, a variável **[!UICONTROL Enviar para]** disponível na **[!UICONTROL Mais]** a lista suspensa não permite selecionar o destino desejado no Experience Manager. O **[!UICONTROL Enviar para]** A opção funciona corretamente usando o **[!UICONTROL Ações do documento]** lista suspensa. O **[!UICONTROL Enviar para]** A opção funciona corretamente para **[!UICONTROL Mais]** lista suspensa, bem como a **[!UICONTROL Ações do documento]** lista suspensa disponível na nova experiência do Workfront.

## Versões anteriores {#previous-releases}

### Versão de outubro de 2022 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.4, lançada em 07 de outubro, inclui as seguintes atualizações:

* Não é possível exibir a guia Subscrições do evento na página de configuração do conector aprimorado devido a um grande número de eventos.

* O Workfront não pode buscar a lista de pastas existentes em um projeto, o que resulta na criação de pastas duplicadas.

### Versão de setembro de 2022 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.3, lançada em 16 de setembro, inclui as seguintes atualizações:

* Não é possível carregar um arquivo com mais de 8 GB.
* Problemas ao publicar automaticamente ativos que são enviados do Workfront para o AEM.
* O campo Caminho raiz não está disponível para o campo Tags durante a edição de um Formulário de esquema de metadados padrão.
* Problemas ao adicionar novas versões no Workfront usando AEM workflows.
* Ao executar uma pesquisa AEM por ativos disponíveis no Workfront, AEM exibe uma mensagem de erro.
* Quando você cria um workflow AEM para criação de tarefa a partir de um ativo e não define um nome de tarefa pai, a tarefa não é criada no Workfront.

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

