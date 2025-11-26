---
title: Habilidade de atualização de conteúdo
description: Saiba o que é a habilidade de atualização de conteúdo do Agente de produção de experiência e o que ele pode fazer por você.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8b7bdb86c3d1b537b536173b6307c486fe436636
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---


# Habilidade de atualização de conteúdo {#content-update}

A habilidade de atualização de conteúdo do Agente de produção de experiência automatiza a produção de conteúdo para acelerar as tarefas diárias do Adobe Experience Manager (AEM) as a Cloud Service e do Edge Delivery Services.

A habilidade de atualização de conteúdo atualiza o conteúdo existente na CMS, incluindo fragmentos de conteúdo, páginas, formulários e ativos. O agente pode executar ações como atualizar, remover, substituir ou adicionar elementos de conteúdo para manter as experiências precisas e atuais. As entradas podem ser descrições de linguagem natural e, quando usadas com PDFs Jira, as capturas de tela também podem fornecer entradas.

## Visão geral {#overview}

A habilidade de atualização de conteúdo transforma os detalhes que você fornece, por meio de linguagem natural ou visuais, em atualizações de conteúdo na sua página. Você fornece o URL de uma página que precisa ser atualizada, juntamente com detalhes sobre o que precisa ser atualizado, e a habilidade do agente conclui sua tarefa.

## Recursos {#capabilities}

Você pode acessar a habilidade de atualização de conteúdo em:

* [Assistente de IA](#ai-assistant)

* [Jira](#jira)

## Assistente de IA {#ai-assistant}

Você pode acessar os Agentes no AEM por meio do Assistente de IA.

Abra o Assistente de IA em experience.adobe.com e comece a interagir especificando seu prompt em linguagem natural usando o campo `Ask AI Assistant anything`:

![Agente de Descoberta de Acesso](/help/ai-in-aem/agents/production/assets/content-update-ai-assistant-example.png)

### Exemplos de Prompts {#sample-prompts}

Para iniciar atualizações de conteúdo, você pode fornecer uma grande variedade de solicitações em linguagem natural. Você também precisa especificar o URL voltado para o público da página que deseja atualizar. Por exemplo:

* modifique a seguinte página https://www.your-url.com/sale Atualize o cabeçalho principal para &quot;Black Friday Mega Sale - Até 70% Off&quot;, Altere o cronômetro da contagem regressiva para mostrar &quot;Termina em 48 Horas&quot;, Remover &quot;Inscreva-se para obter atualizações&quot;, Altere todos os botões &quot;Comprar agora&quot; para &quot;Agarrar o acordo&quot;

* https://www.your-url.com/laptops/your-laptop-model Atualizar cópia do banner para "Salvar 300 USD Hoje Somente", Atualizar preço de 1.299 USD para 999 USD, Remover banner de opção de financiamento

* https://www.your-url.com/your-sneaker Atualizar status do estoque de "Baixo estoque" para "Voltar no estoque - Quantidades limitadas", Alterar o seletor de tamanho para realçar os tamanhos disponíveis em verde, Remover o selo "Em breve"

* https://www.your-url.com/your-sneaker Atualizar as imagens do produto para mostrar novas colorways

>[!NOTE]
>
>Os uploads de arquivo podem ser usados ao interagir usando o [Jira](#jira), mas não são compatíveis com o Assistente de IA.

## Jira {#jira}

Usar a habilidade de atualização de conteúdo com o Jira permite criar um ticket com instruções que automatizam suas edições.

### Criar um tíquete {#create-a-ticket}

Crie um tíquete Jira (de qualquer tipo).

Há dois detalhes essenciais necessários no campo **Descrição** do seu tíquete:

1. O URL voltado para o público da página que você precisa editar.

1. As mudanças necessárias.

   Atualmente, a habilidade oferece suporte à seguinte variedade de formatos para descrever suas alterações:

   * Linguagem natural na descrição do ticket
      * por exemplo &quot;Alterar o título de X para Y&quot;
   * PDF anotado anexado
      * por exemplo, crie uma PDF da página e adicione anotações detalhando o que você deseja alterar
   * Comentários no PDF anexado
      * por exemplo, crie uma PDF da página e adicione comentários detalhando o que você deseja alterar
   * Captura de tela anotada em anexo
      * por exemplo, faça uma captura de tela de parte da sua página e adicione anotações detalhando o que você deseja alterar
   * Arquivo do Microsoft Word anexado, contendo alterações naturais de idioma

### Invocar o agente a partir do seu tíquete {#invoke-the-agent-from-your-ticket}

Para usar o agente, adicione um comentário ao tíquete. No comentário, mencione o agente com o símbolo `@`, juntamente com o comando que ele deve executar; por exemplo:

* `@aemagent@adobe.com process`

Atualmente, o agente entende os comandos:

* `process` - processar a solicitação
* `cancel` - cancelar uma solicitação de processamento
* `retry` - processar novamente uma solicitação
* `feedback` - aplicar feedback a uma geração anterior
* `reprocess` - reprocessar a solicitação original

### Como o agente interage {#how-the-agent-interacts}

Depois de emitir um comando para o agente, ele responde com comentários no Jira. Os comentários detalham o progresso do agente e as ações tomadas.

No caso de um comando `process` para acionar atualizações, as respostas podem seguir a sequência:

* O comentário inicial confirma que o agente foi iniciado.

* Quando a tarefa for concluída. o agente responde com outro comentário contendo detalhes das ações tomadas.
   * As atualizações de conteúdo feitas pelo agente não são destrutivas; isso significa que são feitas em uma instância de visualização.
   * O comentário contém links para as atualizações, para que você possa revisar e publicar conforme necessário ou atribuir a Jira a quem for responsável.

* A imagem a seguir mostra um exemplo de Jira que aciona o comando `process` para a habilidade de atualização de conteúdo:

  ![Exemplo de Jira usando a habilidade de atualização de conteúdo do Agente de Produção de Experiência](assets/content-update-jira-example.png)

## Ativação {#activation}

Para ativar e obter acesso ao Experience Production Agent, é necessário entrar em contato com a Adobe. Para começar, você pode entrar em contato com:

* `experience-production-agent@adobe.com`
* ou entre em contato com a equipe de conta

Para acelerar o processo, é útil fornecer as seguintes informações:

* Para AEM as a Cloud Service
   * É necessário fornecer:
      * ID da organização
      * `product_id`
      * `profile_id`

   * Esses valores podem ser encontrados usando as seguintes etapas:
      * Seu administrador precisa visitar <https://adminconsole.adobe.com/>
      * Selecionar **Adobe Experience Manager as a Cloud Service**
      * Selecione a instância apropriada do AEM
      * Selecionar o perfil que permite operações de leitura e gravação para o conteúdo em questão
      * Pegue o URL do navegador
      * Extrair `product_id` e `profile_id` do URL.
Por exemplo, <https://adminconsole.adobe.com/products/profiles/users>

* Criação de documentos do Edge Delivery
   * Forneça as seguintes informações à sua equipe do Adobe:
      * Domínios relevantes
      * Informações relevantes do Github:
         * Org
         * Acordo de recompra
         * Ramificação

## Limitações {#limitations}

Atualmente, as limitações do Atualizador de conteúdo são:

* Carregamentos de arquivo podem ser usados ao interagir com o [Jira](#jira), mas não têm suporte ao interagir com o [Assistente de IA](#ai-assistant).
