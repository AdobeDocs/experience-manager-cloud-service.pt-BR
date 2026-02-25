---
title: Tarefa de atualização de conteúdo
description: Saiba qual é o trabalho de atualização de conteúdo do Brand Experience Agent e o que ele pode fazer por você.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: 71e3770a7a26b8d3144717513f3ec1c997b3b435
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 2%

---


# Tarefa de atualização de conteúdo {#content-update}

O trabalho de atualização de conteúdo do [Brand Experience Agent](/help/ai-in-aem/agents/brand-experience/overview.md) automatiza a produção de conteúdo para acelerar as tarefas diárias do Adobe Experience Manager (AEM) as a Cloud Service e Edge Delivery Services.

## Visão geral {#overview}

A tarefa de atualização de conteúdo atualiza o conteúdo existente, incluindo fragmentos de conteúdo, páginas, formulários e ativos. O trabalho pode executar ações como atualizar, remover, substituir ou adicionar elementos de conteúdo para manter as experiências precisas e atuais. As entradas podem ser descrições de linguagem natural e, quando usadas com PDFs Jira, as capturas de tela também podem fornecer entradas.

A tarefa de atualização de conteúdo transforma os detalhes que você fornece, por meio de linguagem natural ou visuais, em atualizações de conteúdo na sua página. Você fornece o URL de uma página que precisa ser atualizada, juntamente com detalhes sobre o que precisa ser atualizado, e a habilidade do agente conclui sua tarefa.

## Recursos {#capabilities}

Você pode acessar a habilidade de atualização de conteúdo em:

* [O assistente de IA](#ai-assistant)
* [Jira](#jira)

## Assistente de IA {#ai-assistant}

Você pode acessar o trabalho no AEM por meio do Assistente de IA.

Abra o Assistente de IA do [`experience.adobe.com`,](https://experience.adobe.com) e comece a interagir especificando seu prompt em linguagem natural, usando o campo `Ask AI Assistant anything`:

![Trabalho de Atualização de Conteúdo](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### Exemplos de Prompts {#sample-prompts}

Para iniciar atualizações de conteúdo, você pode fornecer uma grande variedade de solicitações em linguagem natural. Você também precisa especificar o URL voltado para o público da página que deseja atualizar. Por exemplo:

* Modifique a seguinte página `https://www.your-url.com/sale` Atualize o cabeçalho principal para &quot;Black Friday Mega Sale - Até 70% Off&quot;, Altere o cronômetro da contagem regressiva para mostrar &quot;Termina em 48 Horas&quot;, Remova &quot;Inscreva-se para obter atualizações&quot;, Altere todos os botões &quot;Comprar agora&quot; para &quot;Agarrar o negócio&quot;

* `https://www.your-url.com/laptops/your-laptop-model` Atualize a cópia do banner para &quot;Salve hoje US$ 300&quot;, atualize o preço de US$ 1.299 para US$ 999, remova o banner de opção de financiamento

* `https://www.your-url.com/your-sneaker` Atualize o status do estoque de &quot;Baixo estoque&quot; para &quot;Voltar no estoque - Quantidades limitadas&quot;, Altere o seletor de tamanho para realçar os tamanhos disponíveis em verde, Remova o selo &quot;Em breve&quot;

* `https://www.your-url.com/your-sneaker` Atualize as imagens do produto para mostrar novas colorways

>[!NOTE]
>
>Os uploads de arquivo podem ser usados ao interagir usando o [Jira](#jira), mas não são compatíveis com o Assistente de IA.

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

Para usar a tarefa, adicione um comentário ao seu ticket. No comentário, mencione o trabalho com o símbolo `@`, juntamente com o comando que deve ser executado; por exemplo:

* `@aemagent@adobe.com process`

Atualmente, o trabalho entende os comandos:

* `process` - processar a solicitação
* `cancel` - cancelar uma solicitação de processamento
* `retry` - processar novamente uma solicitação
* `feedback` - aplicar feedback a uma geração anterior
* `reprocess` - reprocessar a solicitação original

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

Para ativar e obter acesso ao trabalho de criação de comunicação, entre em contato com a Adobe. Para começar, você pode:

* Contato `experience-production-agent@adobe.com`
* Ou entre em contato com a equipe de conta

Para acelerar o processo, é útil fornecer as seguintes informações:

* Para o AEM as a Cloud Service, é necessário fornecer:
   * ID da organização
   * `product_id`
   * `profile_id`

   * Esses valores podem ser encontrados seguindo estas etapas:
      1. Seu administrador precisa visitar [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com)
      1. Selecionar **Adobe Experience Manager as a Cloud Service**
      1. Selecione a instância apropriada do AEM
      1. Selecionar o perfil que permite operações de leitura e gravação para o conteúdo em questão
      1. Pegue o URL do navegador
      1. Extrair `product_id` e `profile_id` do URL.
Por exemplo, `https://adminconsole.adobe.com/products/profiles/users`

* Criação de documentos do Edge Delivery
   * Forneça as seguintes informações à sua equipe do Adobe:
      * Domínios relevantes
      * Informações relevantes do Github:
         * Org
         * Acordo de recompra
         * Ramificação

## Limitações {#limitations}

Esteja ciente das seguintes limitações:

* Carregamentos de arquivo podem ser usados ao interagir com [Jira](#jira), mas não têm suporte ao interagir com o [Assistente de IA.](#ai-assistant)
