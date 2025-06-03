---
title: Assistente de IA no Adobe Experience Manager (Limited Beta)
description: Use o Assistente de IA no Adobe Experience Manager para encontrar respostas, solucionar problemas e explorar Sites, Assets, Forms e Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: d3ade6ee9216b44b55d6808d8acffe83f1e263c9
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 1%

---

# Sobre o assistente de IA no Adobe Experience Manager {#aem-home}

O Assistente de IA no AEM (Adobe Experience Manager) oferece uma interface conversacional projetada para simplificar a localização de respostas para suas dúvidas relacionadas ao Adobe Experience Manager. Ele ajuda você a acessar o conhecimento sobre produtos, solucionar problemas e explorar as informações disponíveis no Experience League. Durante o programa limitado do Beta, o Assistente de IA é compatível com o Adobe Experience Manager as a Cloud Service, incluindo Sites, Assets, Forms e Cloud Manager.

>[!IMPORTANT]
>Certifique-se de ter revisado e enviado o contrato do usuário para que o Adobe possa ativar o recurso Assistente de IA para que você teste e participe do programa do Beta.
>
>Se tiver dúvidas, envie um email para [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) com o endereço de email associado à sua Adobe ID.

## Privacidade, segurança e governança

O Assistente de IA do AEM foi projetado com forte ênfase em privacidade, segurança e governança.

Este artigo descreve os recursos centralizados na confiança que você pode esperar do Assistente de IA:

* Nenhum dado pessoal é usado pelo Assistente de IA, inclusive para fins de treinamento.
* O Assistente de IA não tem acesso aos dados do consumidor.
* A permissão explícita é necessária para interagir com o Assistente de IA.
* Os prompts fornecidos pelo usuário (perguntas, consultas e assim por diante) não são compartilhados com outros clientes.


## Conheça o Assistente de IA para obter conhecimento sobre produtos {#ai-prod-insights}

O conhecimento do produto abrange conceitos e tópicos derivados da documentação da Adobe Experience League. Essas perguntas podem ser categorizadas nos seguintes subgrupos:

| Conhecimento do produto | Exemplos |
| --- | --- |
| Aprendizado apontado | <ul><li>O que é o Editor Universal?</li><li>Como criar um programa no Cloud Manager?</li></ul> |
| Abrir descoberta | <ul><li>Como usar o Universal Editor?</li><li>Existe uma maneira de copiar o conteúdo de um ambiente para outro?</li></ul> |
| Resolução de problemas | <ul><li>Por que não posso acessar o Universal Editor?</li><li>Por que meu pipeline está falhando?</li></ul> |

O escopo atual do Assistente de IA se concentra em abordar questões de conhecimento do produto para o Adobe Experience Manager as a Cloud Service. Esse escopo inclui suporte abrangente para áreas importantes, como Sites, Assets, Forms e Cloud Manager.

## Assistente de IA para o AEM Forms (Forms Experience Builder) {#ai-forms-builder}

Além do Assistente de IA geral para conhecimento do produto, a AEM oferece um **Assistente de IA especializado para AEM Forms (Forms Experience Builder)**. Este assistente aprimorado pode ajudar você a criar e configurar formulários por meio de prompts de linguagem natural e responder a perguntas específicas de formulários.

### Principais recursos

O Assistente de IA do AEM Forms fornece:

* **Criação de Formulário**: Crie novos formulários do zero usando descrições de linguagem naturais
* **Importação de Design**: Converter designs existentes (PDF, Figma, imagens) em formulários funcionais do AEM
* **Configuração do formulário**: adicionar campos, painéis, regras de validação e lógica condicional
* **Gerenciamento de layout**: organize a estrutura do formulário e otimize para dispositivos diferentes
* **Configuração de Integração**: Configurar envios de formulários e tratamento de dados
* **Conhecimento do Produto**: Responda perguntas sobre recursos e práticas recomendadas do AEM Forms

### Onde acessar

O Assistente de IA do AEM Forms está disponível em:

* **Editor Universal**: para formulários Edge Delivery Services com recursos de edição visual
* **Editor Forms adaptável**: para obter a configuração detalhada do formulário e recursos avançados
* **Interface do usuário do Forms Management**: para tarefas de criação e gerenciamento de formulários de alto nível

### Introdução

>[!NOTE]
>
> O Assistente de IA para o AEM Forms (Forms Experience Builder) está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acesso.

Para saber mais sobre como usar o Assistente de IA para AEM Forms, incluindo exemplos detalhados e práticas recomendadas, consulte a documentação do Assistente de IA para AEM Forms.

### Exemplo de casos de uso

* **&quot;Crie um formulário de feedback do cliente com campos de nome, email, classificação e comentários&quot;**
* **&quot;Converter este formulário de aplicativo do PDF carregado em um formulário adaptável digital&quot;**
* **&quot;Adicionar lógica condicional para mostrar informações do cônjuge somente quando o estado civil for &#39;Casado&#39;&quot;**
* **&quot;Configurar este formulário para enviar dados ao nosso sistema CRM&quot;**

Este Forms AI Assistant especializado representa a próxima evolução na criação de formulários, combinando o poder da IA com os recursos robustos de formulários do AEM para simplificar seu fluxo de trabalho de criação de formulários.

## Como criar perguntas eficazes {#ai-craft-questions}

Para receber as respostas mais precisas do Assistente de IA, é importante formular as perguntas com clareza e contexto. Use as seguintes dicas para garantir que suas consultas sejam claras e bem estruturadas:

* Indique claramente a sua tarefa ou pergunta de maneira concisa.
* Evite textos ambíguos ou sintaxes excessivamente complexas para melhorar a compreensão.
* Inclua um contexto relevante sobre sua tarefa ou pergunta, pois essa abordagem ajuda o Assistente de IA a fornecer respostas mais precisas e relevantes.

### Exemplos de perguntas não suportadas {#ai-unsupported-questions}

| Área | Exemplos |
| --- | --- |
| Insights operacionais | <ul><li>Quantos ambientes de desenvolvimento existem no meu locatário?</li><li>Quem iniciou o último pipeline de produção?</li></ul> |
| Resolução de problemas | <ul><li>Por que meu pipeline de produção está falhando?</li></ul> |
| Tarefa e automação | <ul><li>Configurar um pipeline de qualidade de código de uma ramificação dev para mim.</li></ul> |


## Usar o assistente de IA {#ai-use}


### Iniciar ou redefinir uma conversa

Você pode redefinir o Assistente de IA e iniciar uma nova conversa quando quiser alterar tópicos. Essa capacidade é especialmente útil ao solucionar problemas de consultas que estão falhando ou ao fornecer informações incorretas.

![Botão Iniciar conversa](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**Para iniciar ou redefinir uma conversa:**

1. No Assistente de IA, clique no ícone ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).
1. Para informar ao Assistente de IA sobre um novo tópico ou uma alteração no tópico, clique em **Iniciar nova conversa**.

### Usar capacidade de descoberta

O Assistente de IA inclui um recurso de descoberta para ajudar você a explorar os tópicos e categorias compatíveis.

![Ícone de lâmpada de ideia](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**Para usar a descoberta:**

1. Próximo ao canto superior direito do Assistente de IA, clique no ![ícone Aprender](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).
1. Selecione uma categoria para exibir uma lista de prompts relacionados.
1. Escolha um prompt para entender melhor os tipos de perguntas que o Assistente de IA pode responder.

### Fornecer feedback sobre o Assistente de IA

Sua entrada ajuda a melhorar o Assistente de IA para obter melhor desempenho e precisão.

Compartilhe seu feedback sobre a experiência com o Assistente de IA por meio das seguintes opções:

![Polegar para cima, polegar para baixo e ícones de sinalizador](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| Ícone | Descrição |
| --- | --- |
| ![Ícone de estrutura de tópicos para cima](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Clique em para indicar o que deu certo e para compartilhar um feedback positivo. |
| ![Ícone de estrutura de tópicos com miniaturas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Clique em para fornecer sugestões de melhoria. Adicione comentários específicos sobre sua experiência, que são revisados diariamente. |
| ![Ícone de sinalizador](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Clique em para relatar preocupações ou fornecer feedback detalhado sobre sua interação com o Assistente de IA. |

## Perguntas frequentes sobre o Assistente de IA {#ai-faq}

Estas são as respostas para algumas perguntas comuns sobre o Assistente de IA:

* **As informações fornecidas pelo Assistente de IA são em tempo real?**\
  Não. O Assistente de IA origina seu conteúdo da documentação da Adobe Experience League. As atualizações do conteúdo podem levar algum tempo para refletir em suas respostas.
* **A quais aplicativos do Adobe o Assistente de IA dá suporte?**\
  Atualmente, o Assistente de IA é compatível com o AEM as a Cloud Service, incluindo Sites, Assets, Forms e Cloud Manager, especificamente para consultas de conhecimento sobre produtos.
* **Quais são os recursos do Assistente de IA?**\
  O Assistente de IA foi projetado para responder a consultas relacionadas ao conhecimento do produto Adobe.
* **O Assistente de IA usa informações pessoais para dados de treinamento?**\
  Não. O Assistente de IA não usa informações pessoais para fins de treinamento. Evite compartilhar informações pessoais sobre você ou outras pessoas, incluindo nomes ou detalhes de contato, com o Assistente de IA.
