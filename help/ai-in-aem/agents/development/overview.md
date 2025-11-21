---
title: Visão geral do agente de desenvolvimento
description: Saiba como o Agente de desenvolvimento no AEM analisa pipelines com falha no Cloud Manager e cria logs para sugerir correções de código e acelerar a depuração.
feature: Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 3648dd25c3b3b46663cc09d379aeadfd07cedfa4
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# Visão geral do agente de desenvolvimento {#development-agent-overview}

O Agente de desenvolvimento ajuda os desenvolvedores e administradores do AEM a criar, depurar, implantar e otimizar o código com mais eficiência.

Atualmente, o agente pode recuperar os status do pipeline e ajudar você a solucionar problemas de etapas de criação com falha, sugerindo correções e economizando tempo ao depurar implantações do AEM as a Cloud Service em ambientes de desenvolvimento, preparo e produção. Ele examina logs de compilação e código relacionado para recomendar uma correção que pode ser aplicada manualmente.

>[!IMPORTANT]
>
>As respostas geradas por IA podem ser imprecisas ou enganosas. Verifique as correções e respostas sugeridas.
>
>Consulte também [Diretrizes de usuário da IA gerativa da Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

## Acessar o agente de desenvolvimento por meio do Cloud Manager {#how-to-access-the-agent}

Você acessa o Agente de desenvolvimento por meio do Assistente de IA encontrado nas interfaces do usuário, incluindo o Cloud Manager ou o Experience Hub.

**Para acessar o Agente de Desenvolvimento por meio do Cloud Manager:**

1. Para começar, clique em [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) para abrir sua home page.

   ![página inicial do Adobe Experience Cloud](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. No painel à esquerda, no cabeçalho **Serviços**, clique em **Cloud Manager**.

   ![A lista suspensa que mostra a predefinição do Autor de Conteúdo está selecionada](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >Os widgets, as ferramentas e os artefatos exibidos dependem da persona do usuário, dos direitos e do tipo de implantação do AEM (AEM as a Cloud Service ou Managed Services 6.5/6.5 LTS).

1. No painel à esquerda, em **Programa**, clique em **![Ícone de visão geral](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) Visão geral**.

1. Na página **Visão geral do programa**, no cartão **Pipelines**, clique em um pipeline.

   ![Pipeline selecionado](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-select.png)

1. Na página **Compilação e Verificação de Código**, observe a falha no pipeline.

   ![Falha do pipeline conforme vista na página de Compilação e Verificação de Código](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-failure.png)

1. Próximo ao canto superior direito da interface do usuário do AEM (nas páginas do Cloud Manager ou na instância de autor dos ambientes do AEM), clique no ícone **Assistente de IA**.

   ![Ícone do Assistente de IA na barra de ferramentas](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   Consulte também [Assistente de IA no AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).

1. Na caixa de texto do painel **Assistente de IA** próxima à parte inferior, digite a pergunta ou o prompt e pressione `Enter` ou clique em ![Ícone Enviar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   Por exemplo:
   *No programa &quot;eda-org-01-no-access&quot;, analise a falha no pipeline &quot;no-access&quot; e solucione os problemas.*

   O prompt resultará na seguinte resposta.

   ![Solicitação do Assistente de IA e resposta resultante](/help/ai-in-aem/agents/development/assets/dev-agent-prompt-response.png)


## Permissões {#permissions}

O trabalho de solução de problemas do pipeline do Agente de desenvolvimento exige a função Cloud Manager - Desenvolvedor ou a função Cloud Manager - Gerente de programas.



## Exemplos de prompts {#sample-prompts}

| Prompt | Resultado |
| --- | --- |
| *Listar meus pipelines com falha para o Programa Principal.* | Embora os resultados possam variar, esse prompt deve produzir uma tabela de pipelines com falha, com uma sugestão de acompanhamento para fazer referência a um pipeline específico a ser analisado. |
| *Analise meu pipeline com falha chamado &quot;Pipeline de Desenvolvimento&quot;.* | Esse prompt deve resultar em uma análise do pipeline que falhou com sugestões para corrigir. |

## Recursos fora do escopo {#out-of-scope-features}

A solução de problemas do pipeline opera na etapa de build do pipeline de pilha completa. Para outros tipos e etapas de pipeline, depure as falhas baixando e inspecionando os logs.

Consulte [Logs de Acesso e Download](/help/implementing/cloud-manager/manage-logs.md).

A solução de problemas de pipeline não é compatível com programas que usam BYOGIT (Bring Your Own Git, Traga seu próprio Git).

