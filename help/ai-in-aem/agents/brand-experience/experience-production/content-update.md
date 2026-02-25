---
title: Tarefa de atualização de conteúdo
description: Saiba qual é o trabalho de atualização de conteúdo do Brand Experience Agent e o que ele pode fazer por você.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: 36f4ba8207da67b8e68c9c9851311defc909b495
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 2%

---


# Tarefa de atualização de conteúdo {#content-update}

O trabalho de atualização de conteúdo do [Brand Experience Agent](/help/ai-in-aem/agents/brand-experience/overview.md) automatiza a produção de conteúdo para acelerar as tarefas diárias do Adobe Experience Manager (AEM) as a Cloud Service e Edge Delivery Services.

## Visão geral {#overview}

A tarefa de atualização de conteúdo atualiza o conteúdo existente, incluindo fragmentos de conteúdo, páginas, formulários e ativos. O trabalho pode executar ações como atualizar, remover, substituir ou adicionar elementos de conteúdo para manter as experiências precisas e atuais. As entradas podem ser descrições de linguagem natural e, quando usadas com PDFs Jira, as capturas de tela também podem fornecer entradas.

A tarefa de atualização de conteúdo transforma os detalhes que você fornece, por meio de linguagem natural ou visuais, em atualizações de conteúdo na sua página. Você fornece o URL de uma página que precisa ser atualizada, juntamente com detalhes sobre o que precisa ser atualizado, e a habilidade do agente conclui sua tarefa. Quando usado com o Adobe Experience Manager (AEM) as a Cloud Service, o trabalho cria uma nova [inicialização](/help/sites-cloud/authoring/launches/overview.md) para que você possa examinar as atualizações antes de aplicar. Quando usado com a criação de Documentos, o trabalho cria uma nova [versão](https://experienceleague.adobe.com/en/docs/experience-manager-learn/sites/document-authoring/how-to/document-versions#).

## Recursos {#capabilities}

Você pode acessar a habilidade de atualização de conteúdo em:

* [O assistente de IA](#ai-assistant)
* [Jira](#jira)

## Assistente de IA {#ai-assistant}

Você pode acessar o trabalho no AEM por meio do Assistente de IA.

Abra o Assistente de IA do [`experience.adobe.com`,](https://experience.adobe.com) e comece a interagir especificando seu prompt em linguagem natural, usando o campo `Ask AI Assistant anything`:

![Trabalho de Atualização de Conteúdo](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### Configurar o URL de publicação {#configuring-the-publish-url}

Para usar um URL de publicação (voltado ao público), uma configuração única deve ser feita:

* Pré-requisitos:

   * Para fazer a configuração, o usuário deve ter direitos de Administrador do sistema ou de Administrador de produto.

* Configuração:

   1. Chame a habilidade de Atualização de conteúdo solicitando uma atualização de conteúdo para o URL.
   1. O assistente orientará você na configuração fazendo várias perguntas.
   1. Após a conclusão, o URL de publicação é configurado e pode ser usado.

Por exemplo:

![Habilidade de atualização de conteúdo - configurar URL de publicação](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-publish-url-configuration.png)

### Prompts {#prompts}

Para iniciar atualizações de conteúdo, você pode fornecer uma grande variedade de solicitações em linguagem natural. Você precisa especificar o URL voltado para o público (publicar) ou o URL do ambiente do autor da página que deseja atualizar. Alguns, mas não todos, os verbos suportados; substituir, atualizar, remover, alterar, revisado, modificar, ajustar, excluir.

>[!NOTE]
>
>Os uploads de arquivo podem ser usados ao interagir usando o [Jira](#jira), mas não são compatíveis com o Assistente de IA.

### Exemplos de Prompts {#sample-prompts}

Exemplos de prompts incluem:

* na atualização do `<your-publish-URL>` &quot;Seu café perfeito está a quatro perguntas de distância!&quot; &quot;Seu café, seu caminho!&quot;
* em `<your-author-env-URL>`, substitua a imagem de &quot;holdingcup.png&quot; por &quot;stairhead.png&quot;
* no `<your-publish-URL>`, altere o botão &quot;Faça nosso questionário do Café&quot; para uma versão mais envolvente&quot;
* em `<your-author-env-URL>`, remova a seção &quot;Recompensas não reclamadas é um presente perdido!&quot;

## Jira {#jira}

Usar o trabalho de atualização de conteúdo com o Jira permite criar um ticket com instruções que automatizam suas edições.

### Criar um ticket {#create-a-ticket}

Crie um tíquete Jira (de qualquer tipo). Há dois detalhes essenciais necessários no campo **Descrição** do seu tíquete:

1. O URL voltado para o público da página que você precisa editar.

1. As mudanças necessárias.

   A tarefa oferece suporte à seguinte variedade de formatos para descrever suas alterações:

   * Linguagem natural na descrição do ticket
      * por exemplo &quot;Alterar o título de X para Y&quot;
   * PDF anotado anexado
      * por exemplo, crie uma PDF da página e adicione anotações detalhando o que você deseja alterar
   * Comentários no PDF anexado
      * por exemplo, crie uma PDF da página e adicione comentários detalhando o que você deseja alterar
   * Captura de tela anotada em anexo
      * por exemplo, faça uma captura de tela de parte da sua página e adicione anotações detalhando o que você deseja alterar
   * Arquivo do Microsoft Word anexado, contendo alterações naturais de idioma

### Invocar a tarefa a partir do seu ticket {#invoke-the-job-from-your-ticket}

Para usar a tarefa, adicione um comentário ao seu ticket. No comentário, mencione o trabalho com o símbolo `@`, juntamente com as instruções.

Por exemplo:

* `@aemagent@adobe.com process this ticket`

### Como a tarefa interage {#how-the-agent-interacts}

Depois de emitir um comando para o trabalho, ele responde com comentários na Jira. Os comentários detalham o progresso da tarefa e as ações tomadas.

No caso de um comando `process` para acionar atualizações, as respostas podem seguir a sequência:

* O comentário inicial confirma que o trabalho foi iniciado.

* Quando a tarefa for concluída, o trabalho responderá com outro comentário contendo detalhes das ações tomadas.
   * As atualizações de conteúdo feitas pelo processo não são destrutivas, o que significa que são feitas em uma instância de visualização.
   * O comentário contém links para as atualizações, para que você possa revisar e publicar conforme necessário ou atribuir a Jira a quem for responsável.

* A imagem a seguir mostra um exemplo de Jira que aciona o comando `process` para o trabalho de atualização de conteúdo:

  ![Exemplo de Jira usando o trabalho de atualização de conteúdo do Agente de Produção de Experiência](assets/content-update-jira-example.png)

## Ativação {#activation}

Você pode explorar os Agentes da AEM por meio do [Playground](https://www.aem.live/developer/aem-playground) ou conectar-se com seu CSM ou TAM para discutir o acesso por meio da SKU do Agente.

## Limitações   {#limitations}

Esteja ciente das seguintes limitações:

* Carregamentos de arquivo podem ser usados ao interagir com [Jira](#jira), mas não têm suporte ao interagir com o [Assistente de IA.](#ai-assistant)
