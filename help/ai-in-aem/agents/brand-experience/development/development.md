---
title: Visão geral do trabalho de desenvolvimento
description: Saiba como o trabalho de desenvolvimento no AEM analisa pipelines com falha no Cloud Manager e cria logs para sugerir correções de código e acelerar a depuração.
feature: Agentic AI, AI Assistant, AI Tools, User Roles
role: User, Admin, Architect, Developer
exl-id: 2194556f-aac2-4cdd-8f7f-00c92c8c4424
source-git-commit: 71e3770a7a26b8d3144717513f3ec1c997b3b435
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---


# Visão geral do trabalho de desenvolvimento {#development-job-overview}

[Como parte do Brand Experience Agent](/help/ai-in-aem/agents/brand-experience/overview.md), o trabalho de desenvolvimento ajuda os desenvolvedores e administradores do AEM a criar, depurar, implantar e otimizar o código com mais eficiência.

O trabalho pode recuperar os status do pipeline e ajudar você a solucionar problemas de etapas de criação com falha, sugerindo correções e economizando tempo ao depurar implantações do AEM as a Cloud Service em ambientes de desenvolvimento, preparo e produção. Ele examina logs de compilação e código relacionado para recomendar uma correção que pode ser aplicada manualmente.

>[!VIDEO](https://video.tv.adobe.com/v/3478012?captions=por_br&quality=12&learn=on)

>[!IMPORTANT]
>
>As respostas geradas por IA podem ser imprecisas ou enganosas. Verifique as correções e respostas sugeridas.
>
>Consulte também [Diretrizes de usuário da IA gerativa da Adobe Experience Cloud.](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

Para acessar este trabalho, consulte as [notas de versão](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs) para obter instruções sobre como se inscrever no programa beta, certificando-se de indicar seu interesse no trabalho de desenvolvimento. Você também pode enviar um feedback específico do trabalho de desenvolvimento por email para [aem-devagent@adobe.com.](mailto:aem-devagent@adobe.com)

[Siga um tutorial](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/ai/development-agent-troubleshoot-ci-cd-pipeline) para saber como usar o Agente de Desenvolvimento para solucionar falhas de pipeline.

## Acessar o trabalho de desenvolvimento por meio do Cloud Manager {#how-to-access-the-job}

Você acessa o trabalho de desenvolvimento por meio do Assistente de IA encontrado nas interfaces do usuário, incluindo o Cloud Manager ou o Experience Hub.

1. Para começar, clique em [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) para abrir sua home page.

   ![página inicial do Adobe Experience Cloud](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. No painel à esquerda, no cabeçalho **Serviços**, clique em **Cloud Manager**.

   ![A lista suspensa que mostra a predefinição do Autor de Conteúdo está selecionada](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >Os widgets, as ferramentas e os artefatos exibidos dependem da persona do usuário, dos direitos e do tipo de implantação do AEM (AEM as a Cloud Service ou Managed Services 6.5/6.5 LTS).

1. No painel à esquerda, em **Programa**, clique em **![Ícone de visão geral](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) Visão geral**.

1. Na página **Visão geral do programa**, no cartão **Pipelines**, clique em um pipeline.

   ![Pipeline selecionado](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-select.png)

1. Na página **Compilação e Verificação de Código**, observe a falha no pipeline.

   ![Falha do pipeline conforme vista na página de Compilação e Verificação de Código](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-failure.png)

1. Próximo ao canto superior direito da interface do usuário do AEM (nas páginas do Cloud Manager ou na instância de autor dos ambientes do AEM), clique no ícone **Assistente de IA**.

   ![Ícone do Assistente de IA na barra de ferramentas](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   Consulte também [Assistente de IA no AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).

1. Na caixa de texto do painel **Assistente de IA** próxima à parte inferior, digite a pergunta ou o prompt e pressione `Enter` ou clique em ![Ícone Enviar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   Por exemplo:
   *No programa &quot;eda-org-01-no-access&quot;, analise a falha no pipeline &quot;no-access&quot; e solucione os problemas.*

   O prompt resultará na seguinte resposta.

   ![Solicitação do Assistente de IA e resposta resultante](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-prompt-response.png)


## Permissões {#permissions}

O trabalho de desenvolvimento requer a função Cloud Manager - Desenvolvedor ou a função Cloud Manager - Gerente de programas.

## Exemplos de prompts {#sample-prompts}

| Prompt | Resultado |
| --- | --- |
| *Solucionar problemas do meu pipeline com falha* | Executa uma análise do motivo pelo qual um pipeline falhou; se não estiver claro a qual pipeline está sendo referenciado, perguntas adicionais serão feitas ao usuário. |
| *Listar meus pipelines com falha para o Programa Principal.* | Embora os resultados possam variar, esse prompt gera uma tabela de pipelines com falha, com uma sugestão de acompanhamento para fazer referência a um pipeline específico a ser analisado. |
| *Analise meu pipeline com falha chamado &quot;Pipeline de Desenvolvimento&quot;.* | Esse prompt resulta em uma análise do pipeline que falhou com sugestões para corrigir. Se houver várias falhas, serão feitas perguntas adicionais ao usuário. |
| *Solução de problemas de execução de pipeline 1234567* | Ao fornecer uma ID de execução exata do pipeline, uma análise de pipeline é executada. |

## Recursos fora do escopo {#out-of-scope-features}

A solução de problemas do pipeline opera na etapa de compilação do pipeline de pilha completa. Para outros tipos e etapas de pipeline, depure as falhas baixando e inspecionando os logs.

Consulte [Logs de Acesso e Download](/help/implementing/cloud-manager/manage-logs.md) para obter mais informações.
