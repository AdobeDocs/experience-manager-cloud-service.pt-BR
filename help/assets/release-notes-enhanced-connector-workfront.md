---
title: Notas da versão [!DNL Workfront for Experience Manager enhanced connector]
description: Notas da versão [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 4b63c00847fa21967560a59c3bcd931433a3a73f
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 1%

---

# Notas da versão [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

A seção a seguir descreve as Notas de versão gerais do [!DNL Workfront for Experience Manager enhanced connector].

## Data de lançamento {#release-date}

A data de lançamento da versão mais recente 1.9.12 do [!DNL Workfront for Experience Manager enhanced connector] O é 9 de agosto de 2023.

## Destaques da versão {#release-highlights}

A versão mais recente do [!DNL Workfront for Experience Manager enhanced connector] O inclui as seguintes atualizações:

* Não é possível criar pastas vinculadas no Experience Manager, pois não há conta de usuário associada à pasta vinculada.

* Condições de corrida durante atualizações de metadados para um ativo no Experience Manager.


>[!NOTE]
>
>O AEM 6.4 chegou ao fim do suporte estendido. Para obter mais detalhes, consulte nossa [períodos de suporte técnico](https://helpx.adobe.com/br/support/programs/eol-matrix.html). Encontrar as versões compatíveis [aqui](https://experienceleague.adobe.com/docs/?lang=en).


>[!IMPORTANT]
>
>Adobe recomenda que você [atualizar para a versão 1.9.12 mais recente](/help/assets/workfront-connector-install.md) do [!DNL Workfront for Experience Manager enhanced connector].

## Problemas conhecidos {#known-issues}

* Ao configurar pastas vinculadas ao projeto com AEM 6.4, o Experience Manager não salva os valores para **[!UICONTROL subpastas]** e **[!UICONTROL Criar pasta vinculada em projetos com portfólio]** campos. O valor para a variável **[!UICONTROL subpastas]** atualizações de campo para **[!UICONTROL indefinido]** e o valor para o **[!UICONTROL Criar pasta vinculada em projetos com portfólio]** atualizações de campo para **[!UICONTROL Portfolio padrão]** automaticamente após salvar a configuração.

* Ao usar a experiência clássica do Workfront, a variável **[!UICONTROL Enviar para]** opção disponível no **[!UICONTROL Mais]** a lista suspensa não permite selecionar o destino dentro do Experience Manager. A variável **[!UICONTROL Enviar para]** A opção funciona corretamente usando o **[!UICONTROL Ações do documento]** lista suspensa. A variável **[!UICONTROL Enviar para]** A opção funciona corretamente para **[!UICONTROL Mais]** lista suspensa e a variável **[!UICONTROL Ações do documento]** disponível na nova experiência do Workfront.

## Versões anteriores {#previous-releases}

### Versão de junho de 2023 {#june-2023-release}

* Quando você tem uma rede avançada configurada, há problemas ao enviar conteúdo do Adobe Workfront para o AEM as a Cloud Service.


### Versão de maio de 2023 {#may-2023-release}

* O Workfront retorna uma resposta HTTP 409 para assinaturas de evento duplicadas com base em uma chamada REST de Experience Manager para Workfront, o que resulta em uma exceção de ponteiro nulo.

### Versão de abril de 2023 {#april-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.9, lançada em 10 de abril de 2023, inclui as seguintes atualizações:

* Experience Manager exibe um `DateTimeParseException` exceção quando recebe a data da última modificação do Workfront durante a criação da pasta vinculada.

* Problemas ao criar várias pastas de projeto vinculadas em uma curta duração.

* Incapacidade de configurar um limite no número do novo conjunto de pastas vinculadas do projeto.

### Versão de março de 2023 {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.8, lançada em 3 de março de 2023, inclui as seguintes atualizações:

* Melhorias de desempenho no Experience Manager ao criar pastas vinculadas ao projeto no Workfront.

* Exclusões de comentários no Workfront agora são refletidas no Experience Manager.

* Capacidade de gerenciar o bloqueio de novos clientes no Experience Manager as a Cloud Service para configurar o conector.


### Versão de janeiro de 2023 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.7, lançada em 2 de fevereiro de 2023, inclui as seguintes atualizações:

* O editor de metadados não lista as propriedades de formulários personalizados do Workfront após instalar a versão 1.9.6.

* O console de desenvolvimento é exibido `/content/dam/jcr:content/metadata/wfProjectURL not found` após instalar o conector aprimorado do Workfront e abrir a página inicial do Assets.

### Versão de dezembro de 2022 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.6, lançada em 9 de dezembro, inclui as seguintes atualizações:

**Aprimoramento**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* O conector aprimorado do Workfront agora é compatível com a pesquisa completa de texto em ativos e pastas.

**Correções de erros**

* Os metadados da Versão do documento não são sincronizados adequadamente entre o Workfront e o Experience Manager.
* Problemas ao criar uma pasta vinculada ao Experience Manager no Workfront quando a pasta estiver usando um esquema que está faltando na definição de configuração global.
* O formulário do editor de esquema de metadados para de responder ao clicar em qualquer campo devido a um tempo de carregamento maior do que o esperado. Adição de uma configuração OSGi específica para formulários personalizados para resolver o problema. Os nomes dos formulários personalizados adicionados ao editor de esquema de metadados estão disponíveis nos logs.

### Versão de novembro de 2022 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.5, lançada em 11 de novembro, inclui as seguintes atualizações:

* Quando você define apenas um valor para um campo de vários valores no Workfront, o valor do campo não é mapeado corretamente para o Experience Manager.

* Experience Manager exibe a variável `SERVER_ERROR` no **[!UICONTROL Vincular pastas e arquivos externos]** ao acessar as pastas de ativos devido a permissões inválidas no `/content/dam/collections`.

* Habilitando o **[!UICONTROL Publicar ativos no Brand Portal]** na página de configuração avançada do conector do Workfront, cria um evento incorreto. O evento não é excluído mesmo depois de desabilitar a opção.

  Para resolver o problema:

   1. Atualize para a versão 1.9.5 do conector aprimorado.

   1. Desative o **[!UICONTROL Publicar ativos no Brand Portal]** em configurações avançadas.

   1. Ativar o **[!UICONTROL Publicar ativos no Brand Portal]** opção.

   1. Exclua as assinaturas de evento incorretas.

      1. Executar chamadas para o GET `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         Execute uma chamada de API para cada número de página.

      1. Procure o texto a seguir para localizar assinaturas de evento que correspondam ao seguinte URL e não tenham um `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         Verifique se o conteúdo entre `"objId": "",` e `"url"` corresponde à resposta JSON. O método recomendado para fazer isso é copiar de qualquer Assinatura de Evento que tenha um `objId` e exclua o número.

      1. Observe a ID de assinatura do evento.

      1. Exclua a inscrição no evento errada. Efetuar uma chamada de API de exclusão para `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` já que o código de resposta significa exclusão bem-sucedida de assinaturas de evento incorretas.
  >[!NOTE]
  >
  >Se você já tiver excluído as assinaturas de evento incorretas antes de executar as etapas mencionadas neste procedimento, ignore a última etapa deste procedimento.

### Versão de outubro de 2022 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.4, lançada em outubro de 2007, inclui as seguintes atualizações:

* Não é possível exibir a guia Assinaturas de Eventos na página de configuração avançada do conector devido a muitos eventos.

* O Workfront não pode buscar a lista de pastas existentes em um projeto, o que está resultando na criação de pastas duplicadas.

### Versão de setembro de 2022 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.3, lançada em 16 de setembro, inclui as seguintes atualizações:

* Não é possível carregar um arquivo com mais de 8 GB.
* Problemas ao publicar automaticamente ativos enviados do Workfront para o AEM.
* O campo Caminho raiz não está disponível para o campo Tags ao editar um Formulário de esquema de metadados padrão.
* Problemas ao adicionar novas versões no Workfront usando workflows AEM.
* Ao executar uma pesquisa de AEM por ativos disponíveis no Workfront, o AEM exibe uma mensagem de erro.
* Ao criar um fluxo de trabalho AEM para criação de tarefa a partir de um ativo e não definir um nome de tarefa pai, a tarefa não é criada no Workfront.

### Versão de agosto de 2022 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.2, lançada em 3 de agosto, inclui as seguintes atualizações:

* A variável **[!UICONTROL Carregar documento]** a etapa de fluxo de trabalho não anexa um documento ao Workfront.

* A variável **[!UICONTROL Carregar documento]** a etapa de fluxo de trabalho não anexa um documento a tarefas e problemas no Workfront. A etapa do fluxo de trabalho anexa um documento aos Projetos com êxito.

### Versão de julho de 2022 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] A versão 1.9.1 inclui as seguintes atualizações:

* Adição de suporte para autenticação entre aplicativos Experience Manager e Workfront usando a chave de API do Workfront para instâncias que são migradas para o Adobe IMS.

* Ao vincular arquivos ou pastas externos, o aplicativo do Workfront exibe a variável `SERVER_ERROR` mensagem de erro. A mensagem de erro se refere a uma exceção não autorizada devido a uma incompatibilidade nas chaves de API.

* Quando você executa um workflow Criar tarefa para um ativo, a exceção Ponteiro nulo é exibida nas mensagens de log.

* Quando você habilita o `Replace Spaces with DASH` opção de configuração em Configurações avançadas no Experience Manager, resulta na criação de pastas duplicadas no Workfront.

### Versão de junho de 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] O agora inclui as seguintes atualizações:

* Ao fazer upload por meio de uma pasta vinculada ou usar o `Send To` ação disponível no Workfront para carregar ativos no Experience Manager as a Cloud Service; os ativos são corrompidos e não podem ser abertos no Adobe Photoshop.

### Versão de março de 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] O agora inclui as seguintes atualizações:

* Agora é possível criar pastas vinculadas entre o Adobe Workfront e o AEM Assets as a Cloud Service, mesmo se houver várias configurações de pastas vinculadas do projeto.

* Adição de suporte para paginação de subscrição de evento.

* Adição de suporte ao AEM 6.4.x.

* Adição de suporte para ambientes proxy.

* Várias correções de bugs com base no feedback do parceiro e do cliente.

>[!MORELIKETHIS]
>
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] com o Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
