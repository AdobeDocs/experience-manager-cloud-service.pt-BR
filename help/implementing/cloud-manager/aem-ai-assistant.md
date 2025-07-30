---
title: Assistente de IA no Adobe Experience Manager (Beta)
description: Use o Assistente de IA para ajudar você a encontrar respostas e solucionar problemas das soluções disponíveis no Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 577e15165057fcf6537b4b0b738a1f45e5feb097
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 1%

---

# Assistente de IA no Adobe Experience Manager {#aem-home}

O Assistente de IA do AEM (Adobe Experience Manager) oferece uma interface conversacional projetada para simplificar a localização de respostas para suas dúvidas relacionadas ao Adobe Experience Manager. Ele ajuda você a obter respostas instantâneas para suas perguntas sobre produtos da AEM (*disponíveis para todos os usuários*) e a automatizar a criação de tíquetes de suporte (*disponíveis para Administradores de Suporte*).

Durante a versão beta privada, o Assistente de IA da AEM é compatível com o AEM as a Cloud Service, incluindo as seguintes soluções:

* Sites
* Assets
* Dynamic Media
* Edge Delivery Services
* Cloud Manager
* Forms

Ele é diretamente incorporado ao AEM e acessível no AEM Experience Hub, Cloud Manager e na interface do usuário do autor.

>[!IMPORTANT]
>Certifique-se de ter revisado e enviado o contrato do usuário para que o Adobe possa habilitar o recurso Assistente de IA para que você teste e participe do programa beta privado.
>
>Se tiver dúvidas, envie um email para [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) com o endereço de email associado à sua Adobe ID.

## Escopo {#scope}

O escopo atual do Assistente de IA do AEM se concentra em abordar questões de conhecimento do produto para o Adobe Experience Manager as a Cloud Service. Esse escopo inclui suporte abrangente para áreas importantes, como Sites, Assets, Forms, Edge Delivery Services e Cloud Manager.

* **Superfícies**: disponível no AEM Experience Hub, IU do autor, Cloud Manager.
* **Recursos**: conhecimento sobre produtos e primeira parada para solução de problemas e orientação, criação automática de tíquetes de suporte e pesquisa.
* **Valor**: economiza tempo, acelera o aprendizado e o tempo de retorno, reduz a necessidade de criar tíquetes de suporte manualmente e melhora a eficiência na criação de tíquetes de suporte.

## Privacidade, segurança e governança{#privacy-security-governance}

O Assistente de IA do AEM foi projetado com forte ênfase em privacidade, segurança e governança.

Este artigo descreve os recursos centralizados na confiança que você pode esperar do Assistente de IA da AEM:

* Nenhum dado pessoal é usado pelo Assistente de IA do AEM, inclusive para fins de treinamento.
* O Assistente do AEM AI não tem acesso aos dados do consumidor.
* É necessária permissão explícita para interagir com o Assistente de IA do AEM.
* Os prompts fornecidos pelo usuário (perguntas, consultas e assim por diante) não são compartilhados com outros clientes.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->


## Conheça o Assistente de IA da AEM para obter conhecimento sobre produtos e criação automatizada de tíquetes de suporte {#ai-prod-insights}

O conhecimento do produto abrange conceitos e tópicos derivados da documentação da Adobe Experience League. Essas perguntas podem ser categorizadas nos seguintes subgrupos:


| Conhecimento do produto | Disponível para todos os usuários<br>Exemplos |
| :--- | :--- |
| Aprendizado apontado | <ul><li>O que é o Editor Universal?</li><li>Como criar um programa no Cloud Manager?</li></ul> |
| Abrir descoberta | <ul><li>Como usar o Universal Editor?</li><li>Existe uma maneira de copiar o conteúdo de um ambiente para outro?</li></ul> |
| Resolução de problemas | <ul><li>Por que não posso acessar o Universal Editor?</li><li>Por que meu pipeline está falhando?</li></ul> |
| **Criação do tíquete de suporte** | **Disponível somente para Administradores de Suporte &#x200B;**<br>**Exemplos** |
| Criação automatizada de tíquetes de suporte, capturando o histórico e o contexto do bate-papo do Assistente de IA | <ul><li>Crie um tíquete de suporte para mim.</li></ul> |
| Recuperar status do tíquete de suporte | <ul><li>Mostre-me todos os tíquetes de suporte que abri.</li><li>Mostre-me o status do tíquete &quot;E—&quot;</li></ul> |

{style="table-layout:auto"}


## Como criar perguntas eficazes {#ai-craft-questions}

Para receber as respostas mais precisas do Assistente de IA do AEM, é importante formular suas perguntas com clareza e contexto. Use as seguintes dicas para garantir que suas consultas sejam claras e bem estruturadas:

* Indique claramente a sua tarefa ou pergunta de maneira concisa.
* Evite textos ambíguos ou sintaxes excessivamente complexas para melhorar a compreensão.
* Inclua um contexto relevante sobre sua tarefa ou pergunta, pois essa abordagem ajuda o Assistente do AEM AI a fornecer respostas mais precisas e relevantes.
Por exemplo, no seu prompt, é útil nomear a solução da AEM em que você está trabalhando: Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager ou Forms.

### Exemplos de perguntas não suportadas {#ai-unsupported-questions}

| Área | Exemplos |
| --- | --- |
| Insights operacionais | <ul><li>Quantos ambientes de desenvolvimento existem no meu locatário?</li><li>Quem iniciou o último pipeline de produção?</li></ul> |
| Resolução de problemas | <ul><li>Por que meu pipeline de produção está falhando?</li></ul> |
| Tarefa e automação | <ul><li>Configurar um pipeline de qualidade de código de uma ramificação dev para mim.</li></ul> |


## Usar o Assistente do AEM AI {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AEM AI Assistant access through Admin Console 

To use the AEM AI Assistant, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AEM AI Assistant in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in the AEM AI Assistant of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### Iniciar ou redefinir uma conversa

Você pode redefinir o Assistente de IA do AEM e iniciar uma nova conversa quando quiser alterar tópicos. Essa capacidade é especialmente útil ao solucionar problemas de consultas que estão falhando ou ao fornecer informações incorretas.

![Botão Iniciar conversa](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**Para iniciar ou redefinir uma conversa:**

1. No Assistente do AEM AI, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).
1. Para informar o Assistente do AEM AI sobre um novo tópico ou uma alteração no tópico, clique em **Iniciar nova conversa**.

### Usar capacidade de descoberta

O Assistente de IA do AEM inclui um recurso de descoberta para ajudar você a explorar os tópicos e categorias compatíveis.

![Ícone de lâmpada de ideia](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**Para usar a descoberta:**

1. Próximo ao canto superior direito do Assistente de IA do AEM, clique em ![Ícone Saiba](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).
1. Selecione uma categoria para exibir uma lista de prompts relacionados.
1. Escolha um prompt para entender melhor os tipos de perguntas que o Assistente de IA do AEM pode responder.

### Fornecer feedback sobre o Assistente de IA da AEM

Sua entrada ajuda a melhorar o Assistente de IA do AEM para obter melhor desempenho e precisão.

Compartilhe seu feedback sobre a sua experiência com o Assistente de IA da AEM por meio das seguintes opções:

![Polegar para cima, polegar para baixo e ícones de sinalizador](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| Ícone | Descrição |
| --- | --- |
| ![Ícone de estrutura de tópicos para cima](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Clique em para indicar o que deu certo e para compartilhar um feedback positivo. |
| ![Ícone de estrutura de tópicos com miniaturas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Clique em para fornecer sugestões de melhoria. Adicione comentários específicos sobre sua experiência, que são revisados diariamente. |
| ![Ícone de sinalizador](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Clique em para relatar dúvidas ou fornecer feedback detalhado sobre sua interação com o Assistente de IA da AEM. |

## Perguntas frequentes sobre o Assistente de IA do AEM {#ai-faq}

Estas são as respostas para algumas perguntas comuns sobre o Assistente de IA:

* **As informações fornecidas pelo Assistente de IA do AEM são em tempo real?**\
  Não. O Assistente de IA origina seu conteúdo da documentação da Adobe Experience League. As atualizações do conteúdo podem levar algum tempo para refletir em suas respostas.
* **A quais aplicativos do Adobe o Assistente do AEM AI oferece suporte?**\
  Atualmente, o Assistente de IA oferece suporte a consultas de conhecimento de produtos na AEM as a Cloud Service, incluindo Sites, Assets, Dynamic Media, Cloud Manager e Forms.
* **Quais são os recursos do Assistente do AEM AI?**\
  O Assistente de IA do AEM foi projetado para responder a consultas relacionadas ao conhecimento do produto Adobe.
* **O Assistente do AEM AI usa informações pessoais para dados de treinamento?**\
  Não. O Assistente de IA da AEM não usa informações pessoais para fins de treinamento. Evite compartilhar informações pessoais sobre você ou outras pessoas, incluindo nomes ou detalhes de contato, com o Assistente de IA da AEM.


## Assistente de IA do AEM Forms (Forms Experience Builder) {#ai-forms-builder}

Além do Assistente geral de IA da AEM para conhecimento do produto, a AEM oferece um **[Assistente de IA da AEM Forms (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)** especializado. Este assistente aprimorado pode ajudar você a criar e configurar formulários por meio de prompts de linguagem natural e responder a perguntas específicas de formulários.

### Principais recursos

O Assistente de IA do AEM Forms fornece:

* **Criação de Formulário**: crie novos formulários do zero usando descrições de linguagem naturais.
* **Importação de Design**: converta designs existentes (PDF, Figma, imagens) em AEM Forms funcional.
* **Configuração do formulário**: adicione campos, painéis, regras de validação e lógica condicional.
* **Gerenciamento de layout**: organize a estrutura do formulário e otimize para dispositivos diferentes.
* **Configuração de Integração**: Configurar envios de formulários e tratamento de dados.
* **Conhecimento do Produto**: Responda perguntas sobre recursos do AEM Forms e práticas recomendadas.

### Onde acessar

O Assistente de IA do AEM Forms está disponível no seguinte site:

* **Editor Universal**: para formulários Edge Delivery Services com recursos de edição visual.
* **Editor Forms adaptável**: para obter a configuração detalhada do formulário e recursos avançados.
* **Interface do usuário do Forms Management**: para tarefas de criação e gerenciamento de formulários de alto nível.

### Introdução

>[!NOTE]
>
> O Assistente de IA do AEM Forms (Forms Experience Builder) está disponível no programa beta privado. Envie um email de seu endereço comercial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acesso.

Para saber mais sobre como usar o AEM Forms AI Assistant, consulte a documentação do [AEM Forms AI Assistant](/help/edge/docs/forms/forms-ai-assistant.md).

### Exemplo de casos de uso

* **&quot;Crie um formulário de feedback do cliente com campos de nome, email, classificação e comentários&quot;**
* **&quot;Converter este formulário de aplicativo do PDF carregado em um formulário adaptável digital&quot;**
* **&quot;Adicionar lógica condicional para mostrar informações do cônjuge somente quando o estado civil for &#39;Casado&#39;&quot;**
* **&quot;Configurar este formulário para enviar dados ao sistema de Gerenciamento de Relacionamento com o Cliente&quot;**

Este AEM Forms AI Assistant especializado representa a próxima evolução na criação de formulários, combinando o poder da IA com os recursos robustos de formulários do AEM para simplificar seu fluxo de trabalho de criação de formulários.
