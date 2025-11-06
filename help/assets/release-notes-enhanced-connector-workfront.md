---
title: Notas de versão para  [!DNL Workfront for Experience Manager enhanced connector]
description: Notas de versão para  [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 2%

---

# Notas de versão para [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

A seção a seguir descreve as Notas de Versão gerais do [!DNL Workfront for Experience Manager enhanced connector].

A data de lançamento da versão mais recente 1.9.21 do [!DNL Workfront for Experience Manager enhanced connector] é 25 de junho de 2025.

## Destaques da versão {#release-highlights}

A versão mais recente do [!DNL Workfront for Experience Manager enhanced connector] inclui os seguintes aprimoramentos e correções de erros:

* Melhoria no registro de solicitações de API para evitar registros falsos positivos de falhas de autenticação.

* Correção de vazamento de conexão nas chamadas de API do Workfront.

* Suporte ao Workfront Enhanced Connector com 6.5 LTS para versões Java 17 e Java 21.

>[!NOTE]
>
>O AEM 6.4 chegou ao fim do suporte estendido. Consulte nossos [períodos de suporte técnico](https://helpx.adobe.com/br/support/programs/eol-matrix.html). Encontre as versões [aqui](https://experienceleague.adobe.com/docs/?lang=pt-BR) compatíveis.

>[!IMPORTANT]
>
>A Adobe recomenda [atualizar para a versão 1.9.20 mais recente](/help/assets/workfront-connector-install.md) do [!DNL Workfront for Experience Manager enhanced connector].

## Problemas conhecidos {#known-issues}

* Ao configurar pastas vinculadas do projeto com o AEM 6.4, a Experience Manager não salva os valores para **[!UICONTROL subpastas]** e **[!UICONTROL Criar pasta vinculada em projetos com campos de portfólio]**. O valor do campo **[!UICONTROL subpastas]** atualiza para **[!UICONTROL indefinido]** e o valor da **[!UICONTROL Criar pasta vinculada em projetos com portfólio]** atualiza o campo para **[!UICONTROL Portfolio Padrão]** automaticamente após salvar a configuração.

* Quando você usa a experiência clássica do Workfront, a opção **[!UICONTROL Enviar para]**, disponível na lista suspensa **[!UICONTROL Mais]**, não permite selecionar o destino no Experience Manager. A opção **[!UICONTROL Enviar para]** funciona corretamente usando a lista suspensa **[!UICONTROL Ações de Documento]**. A opção **[!UICONTROL Enviar para]** funciona corretamente nas listas suspensas **[!UICONTROL Mais]** e **[!UICONTROL Ações de Documentos]**, disponíveis na nova experiência do Workfront.

## Versões anteriores {#previous-releases}

### Versão de setembro de 2024 {#september-2024-release}

* O tipo MIME é perdido durante o upload e a criação de uma nova versão de um ativo existente.

### Versão de abril de 2024 {#april-2024-release}

* A falha ao fechar clientes HTTP está causando problemas de memória insuficiente.


### Versão de março de 2024 {#march-2024-release}

* O processamento de uploads de vários ativos do Workfront encontra problemas.
* Não adicionar aspas de fechamento ao usar o Workfront para procurar pastas nos resultados do Experience Manager em `SERVER_ERROR`.

### Versão de fevereiro de 2024 {#february-2024-release}

* Ative o recurso de alternância para permitir que os clientes da AEM Cloud configurem e configurem um conector.

* Fechar o `resourceResolver` sem fechar explicitamente a sessão subjacente causa vazamentos de sessão em instâncias do AEM. É crucial fechar explicitamente a sessão, pois o fechamento automático do Resource Resolver não fecha implicitamente a sessão.

### Versão de janeiro de 2024 {#january-2024-release}

* A configuração [!DNL Workfront] em [!DNL CRX DE] atualmente não armazena `project ID`, causando erros ao aplicar a permissão somente leitura. Saiba como [configurar permissões](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html?lang=pt-BR#linked-folders).

* Nenhuma documentação pública sobre como adicionar uma propriedade personalizada à definição de índice pronta para uso. Saiba mais sobre [adição de propriedade personalizada](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html?lang=pt-BR#metadata-schema-mapping).

* A exclusão de configurações de conexão no conector aprimorado afeta significativamente as assinaturas de eventos e outras configurações salvas, fazendo com que elas apontem para um URL antigo.

* A instalação do pacote complementar de formulários não instala o **[!UICONTROL Alternar Roteador]**, resultando na falha do recurso [!DNL WFEC AMS environment Toggle].

* A habilitação de assinaturas de evento na configuração do EWC resulta em falhas repetidas de chamada de API com erro `HTTP 400` ao configurar o conector aprimorado [!DNL Workfront] pela primeira vez.

* A exclusão de comentários em ativos de pastas vinculados na Workfront não consegue encontrar o caminho de pastas vinculadas no AEM.

* O suporte insuficiente para ativos de arquivos grandes no AEM resulta em um problema de tamanho de 4 bytes.

* Sem processamento de tempo de solicitação para fluxos críticos em pastas vinculadas, atualizações de documentos e atualizações de notas.

### Versão de novembro de 2023 {#nov-2023-release}

* Ao visualizar a lista de pastas do AEM, a caixa de diálogo demora mais de um minuto para carregar.
* [!DNL Workfront] usuários autorizados estão recebendo consistentemente logs de erro de falha de autenticação.

### Versão de outubro de 2023 {#october-2023-release}

* Quando assinaturas de evento estão desabilitadas nas Configurações Avançadas, você ainda pode selecionar as opções para **Assinar eventos de atualização de documento para atualizar metadados de ativos do AEM**, **Publicar todos os ativos de projeto no Brand Portal após a conclusão do projeto** e **Habilitar a Sincronização de Comentários**.

* Alguns dos ativos armazenados no Experience Manager não são renderizados adequadamente ao visualizá-los no Workfront.

* Ao reconfigurar a conexão do Experience Manager com o Workfront, assinaturas de evento, como atualização de sincronização de comentários, exclusão e atualização de documentos, não são criadas com sucesso.

* Principais melhorias de desempenho da API para criação de pastas vinculadas, atualização, habilitação de pastas vinculadas, sincronização de comentários, habilitação e desabilitação, salvamento de configurações avançadas no conector.

### Versão de setembro de 2023 {#september-2023-release}

* O conector aprimorado do Experience Manager busca todas as assinaturas de evento do Workfront enquanto exclui uma assinatura de evento para um projeto, o que resulta em um impacto no desempenho do aplicativo.

* Quando um ativo é enviado do Workfront para o Experience Manager, o tipo MIME do ativo não é definido como o atributo `dc:format` no Experience Manager.

* As IDs de projeto do Workfront armazenadas no conector aprimorado do Experience Manager incluem duplicatas.

### Versão de agosto de 2023 {#august-2023-release}

* Não é possível criar pastas vinculadas no Experience Manager, pois não há conta de usuário associada à pasta vinculada.

* Condições de corrida durante atualizações de metadados para um ativo no Experience Manager.

### Versão de junho de 2023 {#june-2023-release}

* Quando a rede avançada está configurada, há problemas ao enviar conteúdo do Adobe Workfront para o AEM as a Cloud Service.


### Versão de maio de 2023 {#may-2023-release}

* O Workfront retorna uma resposta HTTP 409 para assinaturas de evento duplicadas com base em uma chamada REST do Experience Manager para o Workfront, o que resulta em uma exceção de ponteiro nulo.

### Versão de abril de 2023 {#april-2023-release}

A versão 1.9.9 do [!DNL Workfront for Experience Manager enhanced connector], lançada em 10 de abril de 2023, inclui as seguintes atualizações:

* O Experience Manager exibe uma exceção `DateTimeParseException` quando recebe a data da última modificação do Workfront durante a criação da pasta vinculada.

* Problemas ao criar várias pastas de projeto vinculadas em uma curta duração.

* Incapacidade de configurar um limite no número do novo conjunto de pastas vinculadas do projeto.

### Versão de março de 2023 {#march-2023-release}

A versão 1.9.8 do [!DNL Workfront for Experience Manager enhanced connector], lançada em 3 de março de 2023, inclui as seguintes atualizações:

* Melhorias de desempenho no Experience Manager ao criar pastas vinculadas a projetos no Workfront.

* Exclusões de comentários no Workfront agora se refletem no Experience Manager.

* Capacidade de gerenciar o bloqueio de novos clientes no Experience Manager as a Cloud Service para configurar o conector.

### Versão de janeiro de 2023 {#january-2022-release}

A versão 1.9.7 do [!DNL Workfront for Experience Manager enhanced connector], lançada em 2 de fevereiro de 2023, inclui as seguintes atualizações:

* O editor de metadados não lista as propriedades de formulários personalizados do Workfront após instalar a versão 1.9.6.

* O console de desenvolvimento exibe uma mensagem de erro `/content/dam/jcr:content/metadata/wfProjectURL not found` após a instalação do conector aprimorado do Workfront e a abertura da página inicial do Assets.

### Versão de dezembro de 2022 {#december-2022-release}

A versão 1.9.6 do [!DNL Workfront for Experience Manager enhanced connector], lançada em 9 de dezembro, inclui as seguintes atualizações:

**Aprimoramento**

<!--

* Workfront enhanced connector now lets you use new search parameters to be more specific while defining folder names on large repositories.

-->

* O conector aprimorado do Workfront agora é compatível com a pesquisa completa de texto em ativos e pastas.

**Correções de erros**

* Os metadados da Versão do documento não são sincronizados adequadamente entre o Workfront e o Experience Manager.
* Problemas ao criar uma pasta vinculada ao Experience Manager no Workfront quando a pasta estiver usando um esquema que está faltando na definição de configuração global.
* O formulário do editor de esquema de metadados para de responder ao clicar em qualquer campo devido a um tempo de carregamento maior do que o esperado. Adição de uma configuração OSGi específica para formulários personalizados para resolver o problema. Os nomes dos formulários personalizados adicionados ao editor de esquema de metadados estão disponíveis nos logs.

### Versão de novembro de 2022 {#november-2022-release}

A versão 1.9.5 do [!DNL Workfront for Experience Manager enhanced connector], lançada em 11 de novembro, inclui as seguintes atualizações:

* Quando você define apenas um valor para um campo de vários valores no Workfront, o valor do campo não é mapeado corretamente para o Experience Manager.

* O Experience Manager exibe `SERVER_ERROR` na tela **[!UICONTROL Vincular pastas e arquivos externos]** ao acessar as pastas de ativos devido a permissões inválidas em `/content/dam/collections`.

* Habilitar a opção **[!UICONTROL Publicar Assets no Brand Portal]** na página de configuração avançada do conector do Workfront cria um evento incorreto. O evento não é excluído mesmo depois de desabilitar a opção.

  Para resolver o problema:

   1. Atualize para a versão 1.9.5 do conector aprimorado.

   1. Desabilite a opção **[!UICONTROL Publicar Assets no Brand Portal]** nas configurações avançadas.

   1. Habilitar a opção **[!UICONTROL Publicar Assets no Brand Portal]**.

   1. Exclua as assinaturas de evento incorretas.

      1. Executar chamadas GET para `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         Execute uma chamada de API para cada número de página.

      1. Procure o texto a seguir para encontrar assinaturas de evento que correspondam à URL a seguir e não tenham um `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         Verifique se o conteúdo entre `"objId": "",` e `"url"` corresponde à resposta JSON. O método recomendado para fazer isso é copiar de qualquer Assinatura de Evento que tenha um `objId` e, em seguida, excluir o número.

      1. Observe a ID de assinatura do evento.
      1. Exclua a inscrição no evento errada. Efetuar uma chamada de API de Exclusão para `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` como código de resposta significa exclusão bem-sucedida de assinaturas de evento incorretas.

         >[!NOTE]
         >
         >Se você já tiver excluído as assinaturas de evento incorretas antes de executar as etapas mencionadas neste procedimento, ignore a última etapa deste procedimento.

### Versão de outubro de 2022 {#october-2022-release}

A versão 1.9.4 do [!DNL Workfront for Experience Manager enhanced connector], lançada em 7 de outubro, inclui as seguintes atualizações:

* Não é possível exibir a guia Assinaturas de Eventos na página de configuração avançada do conector devido a muitos eventos.

* O Workfront não pode buscar a lista de pastas existentes em um projeto, o que está resultando na criação de pastas duplicadas.

### Versão de setembro de 2022 {#september-2022-release}

A versão 1.9.3 do [!DNL Workfront for Experience Manager enhanced connector], lançada em 16 de setembro, inclui as seguintes atualizações:

* Não é possível carregar um arquivo com mais de 8 GB.
* Problemas ao publicar automaticamente ativos enviados do Workfront para o AEM.
* O campo Caminho raiz não está disponível para o campo Tags ao editar um Formulário de esquema de metadados padrão.
* Problemas ao adicionar novas versões no Workfront usando fluxos de trabalho do AEM.
* Ao executar uma pesquisa de ativos do AEM disponível no Workfront, o AEM exibe uma mensagem de erro.
* Ao criar um fluxo de trabalho do AEM para criação de tarefa a partir de um ativo e não definir um nome de tarefa pai, a tarefa não é criada no Workfront.

### Versão de agosto de 2022 {#august-2022-release}

A versão 1.9.2 do [!DNL Workfront for Experience Manager enhanced connector], lançada em 3 de agosto, inclui as seguintes atualizações:

* A etapa de fluxo de trabalho **[!UICONTROL Carregar Documento]** falha ao anexar um documento ao Workfront.

* A etapa de fluxo de trabalho **[!UICONTROL Carregar Documento]** falha ao anexar um documento a Tarefas e Problemas no Workfront. A etapa do fluxo de trabalho anexa um documento aos Projetos com êxito.

### Versão de julho de 2022 {#july-2022-release}

A versão 1.9.1 do [!DNL Workfront for Experience Manager enhanced connector] inclui as seguintes atualizações:

* Adição de suporte para autenticação entre aplicativos Experience Manager e Workfront usando a chave da API do Workfront para instâncias que são migradas para o Adobe IMS.

* Ao vincular arquivos ou pastas externas, o aplicativo Workfront exibe a mensagem de erro `SERVER_ERROR`. A mensagem de erro se refere a uma exceção não autorizada devido a uma incompatibilidade nas chaves de API.

* Quando você executa um workflow Criar tarefa para um ativo, a exceção Ponteiro nulo é exibida nas mensagens de log.

* Quando você habilita a opção de configuração `Replace Spaces with DASH` em Configurações avançadas no Experience Manager, ela resulta na criação de pastas duplicadas no Workfront.

### Versão de junho de 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] agora inclui as seguintes atualizações:

* Ao carregar por meio de uma pasta vinculada ou usar a ação `Send To` disponível no Workfront para carregar ativos para o Experience Manager as a Cloud Service, os ativos são corrompidos e não podem ser abertos no Adobe Photoshop.

### Versão de março de 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] agora inclui as seguintes atualizações:

* Agora é possível criar pastas vinculadas entre o Adobe Workfront e o AEM Assets as a Cloud Service, mesmo se houver várias configurações de pastas vinculadas do projeto.

* Adição de suporte para paginação de subscrição de evento.

* Adição de suporte para o AEM 6.4.x.

* Adição de suporte para ambientes proxy.

* Várias correções de bugs com base no feedback do parceiro e do cliente.

>[!MORELIKETHIS]
>
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] ao Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=pt-BR)
