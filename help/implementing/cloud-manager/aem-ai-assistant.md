---
title: Assistente de IA no Adobe Experience Manager (beta privado)
description: Use o Assistente de IA no Adobe Experience Manager para encontrar respostas, solucionar problemas e explorar Sites, Assets, Dynamic Media, Cloud Manager e Forms.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 0afd74120380c9ae3d02db9fb684189c2f19648f
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 0%

---

# Sobre o Assistente de IA do AEM no Adobe Experience Manager {#aem-home}

O Assistente de IA no AEM (Adobe Experience Manager) oferece uma interface conversacional projetada para simplificar a localização de respostas para suas dúvidas relacionadas ao Adobe Experience Manager. Ele ajuda você a acessar o conhecimento sobre produtos, solucionar problemas e explorar as informações disponíveis no Experience League. Durante o programa beta privado, o Assistente de IA da AEM é compatível com o Adobe Experience Manager as a Cloud Service, incluindo Sites, Assets, Dynamic Media, Cloud Manager e Forms.

>[!IMPORTANT]
>Certifique-se de ter revisado e enviado o contrato do usuário para que o Adobe possa habilitar o recurso Assistente de IA para que você teste e participe do programa beta privado.
>
>Se tiver dúvidas, envie um email para [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) com o endereço de email associado à sua Adobe ID.

## Privacidade, segurança e governança

O Assistente de IA do AEM foi projetado com forte ênfase em privacidade, segurança e governança.

Este artigo descreve os recursos centralizados na confiança que você pode esperar do Assistente de IA da AEM:

* Nenhum dado pessoal é usado pelo Assistente de IA do AEM, inclusive para fins de treinamento.
* O Assistente do AEM AI não tem acesso aos dados do consumidor.
* É necessária permissão explícita para interagir com o Assistente de IA do AEM.
* Os prompts fornecidos pelo usuário (perguntas, consultas e assim por diante) não são compartilhados com outros clientes.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->


## Conheça o AEM AI Assistant para obter conhecimento sobre o produto {#ai-prod-insights}

O conhecimento do produto abrange conceitos e tópicos derivados da documentação da Adobe Experience League. Essas perguntas podem ser categorizadas nos seguintes subgrupos:

| Conhecimento do produto | Exemplos |
| --- | --- |
| Aprendizado apontado | <ul><li>O que é o Editor Universal?</li><li>Como criar um programa no Cloud Manager?</li></ul> |
| Abrir descoberta | <ul><li>Como usar o Universal Editor?</li><li>Existe uma maneira de copiar o conteúdo de um ambiente para outro?</li></ul> |
| Resolução de problemas | <ul><li>Por que não posso acessar o Universal Editor?</li><li>Por que meu pipeline está falhando?</li></ul> |

O escopo atual do Assistente de IA do AEM se concentra em abordar questões de conhecimento do produto para o Adobe Experience Manager as a Cloud Service. Esse escopo inclui suporte abrangente para áreas importantes, como Sites, Assets, Forms e Cloud Manager.

## Como criar perguntas eficazes {#ai-craft-questions}

Para receber as respostas mais precisas do Assistente de IA do AEM, é importante formular as perguntas com clareza e contexto. Use as seguintes dicas para garantir que suas consultas sejam claras e bem estruturadas:

* Indique claramente a sua tarefa ou pergunta de maneira concisa.
* Evite textos ambíguos ou sintaxes excessivamente complexas para melhorar a compreensão.
* Inclua um contexto relevante sobre sua tarefa ou pergunta, pois essa abordagem ajuda o Assistente do AEM AI a fornecer respostas mais precisas e relevantes.
Por exemplo, no seu prompt, é útil nomear a solução da AEM em que você está trabalhando: Sites, Assets, Dynamic Media, Cloud Manager e Forms.

### Exemplos de perguntas não suportadas {#ai-unsupported-questions}

| Área | Exemplos |
| --- | --- |
| Insights operacionais | <ul><li>Quantos ambientes de desenvolvimento existem no meu locatário?</li><li>Quem iniciou o último pipeline de produção?</li></ul> |
| Resolução de problemas | <ul><li>Por que meu pipeline de produção está falhando?</li></ul> |
| Tarefa e automação | <ul><li>Configurar um pipeline de qualidade de código de uma ramificação dev para mim.</li></ul> |


## Usar o Assistente do AEM AI {#ai-use}

### Habilitar o acesso ao Assistente de IA do AEM por meio do Admin Console

Para usar o Assistente de IA do AEM, sua organização deve aceitar no nível da Admin Console. Um administrador de produto cria (ou escolhe) um grupo de usuários e concede a ele a nova permissão &quot;Assistente de IA&quot;. Qualquer pessoa adicionada a esse grupo obtém acesso ao Assistente instantaneamente no AEM. Se o objetivo for a disponibilidade em toda a empresa, o administrador simplesmente atribuirá todos os usuários a esse grupo.

![Assistente do AEM AI na Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

Da perspectiva de um funcionário, o processo é simples: identifique o administrador do produto para o Adobe Experience Manager em sua organização e solicite para ser adicionado ao grupo de usuários habilitado para IA. Quando você aparece nesse grupo, o ícone Assistente é exibido automaticamente na próxima vez que você entrar.

Os administradores devem ter em mente a governança normal do Cloud Manager. Você deve ter direitos de administrador de produto no Admin Console para criar perfis, gerenciar grupos de usuários ou editar permissões. Se os usuários também precisarem do recurso **Criar Tíquete de Suporte** interno do Assistente, adicione a função padrão **Administrador de Suporte** (função padrão do Admin Console) aos mesmos indivíduos ou grupos.

![Criação de tíquete de suporte técnico no Assistente AEM AI da Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

Para obter uma apresentação guiada sobre como configurar usuários e grupos no AEM as a Cloud Service, consulte [Configurar acesso ao AEM as a Cloud Service](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/accessing/overview).

Consulte também [Permissões personalizadas](/help/implementing/cloud-manager/custom-permissions.md).


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
