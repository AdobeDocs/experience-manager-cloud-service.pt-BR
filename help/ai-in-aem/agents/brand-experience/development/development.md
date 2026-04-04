---
title: Visão geral do agente de desenvolvimento
description: Saiba como o Agente de desenvolvimento no AEM analisa pipelines com falha no Cloud Manager e cria logs para sugerir correções de código e acelerar a depuração.
feature: Agentic AI, AI Assistant, AI Tools, User Roles
role: User, Admin, Developer
exl-id: 2194556f-aac2-4cdd-8f7f-00c92c8c4424
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---


# Visão geral do agente de desenvolvimento {#development-agent-overview}

[Como parte da Brand Experience Agent](/help/ai-in-aem/agents/brand-experience/overview.md), o Agente de Desenvolvimento ajuda os desenvolvedores e administradores da AEM a criar, depurar, implantar e otimizar o código com mais eficiência.

O agente pode recuperar os status do pipeline e ajudar você a solucionar problemas de etapas de criação com falha, sugerindo correções e economizando tempo ao depurar implantações do AEM as a Cloud Service em ambientes de desenvolvimento, preparo e produção. Ele examina logs de compilação e código relacionado para recomendar uma correção que pode ser aplicada manualmente.

>[!VIDEO](https://video.tv.adobe.com/v/3478006?quality=12&learn=on)

>[!IMPORTANT]
>
>As respostas geradas por IA podem ser imprecisas ou enganosas. Verifique as correções e respostas sugeridas.
>
>Consulte também [Diretrizes de usuário da IA gerativa da Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

>[!NOTE]
>
>A Solução de Problemas do Pipeline é limitada aos Pipelines de Pilha Completa (Implantação e Qualidade de Código), mas o suporte para o **Pipeline de Configuração da Camada da Web** agora está disponível na versão beta. Para solicitar acesso, envie um email para [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com). É necessário acesso pré-existente aos Agentes no AEM.

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

Para acessar este agente, consulte as [notas de versão](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs) para obter instruções sobre como se inscrever no programa beta, certificando-se de indicar seu interesse no Agente de Desenvolvimento. Você também pode enviar um feedback específico do agente de desenvolvimento por email para [aem-devagent@adobe.com.](mailto:aem-devagent@adobe.com)

[Siga um tutorial](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/agents/development-agent-troubleshoot-ci-cd-pipeline) para saber como usar o Agente de Desenvolvimento para solucionar falhas de pipeline.

## Acessar o agente de desenvolvimento por meio do Cloud Manager {#how-to-access-the-agent}

Você acessa o Agente de desenvolvimento por meio do Assistente de IA encontrado nas interfaces do usuário, incluindo o Cloud Manager ou o Experience Hub.

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

O Agente de desenvolvimento exige a função Cloud Manager - Desenvolvedor ou Cloud Manager - Gerente de programas.

## Exemplos de prompts {#sample-prompts}

| Prompt | Resultado |
| --- | --- |
| *Solucionar problemas do meu pipeline com falha* | Executa uma análise do motivo pelo qual um pipeline falhou; se não estiver claro a qual pipeline está sendo referenciado, perguntas adicionais serão feitas ao usuário. |
| *Listar meus pipelines com falha para o Programa Principal.* | Embora os resultados possam variar, esse prompt gera uma tabela de pipelines com falha, com uma sugestão de acompanhamento para fazer referência a um pipeline específico a ser analisado. |
| *Analise meu pipeline com falha chamado &quot;Pipeline de Desenvolvimento&quot;.* | Esse prompt resulta em uma análise do pipeline que falhou com sugestões para corrigir. Se houver várias falhas, serão feitas perguntas adicionais ao usuário. |
| *Solução de problemas de execução de pipeline 1234567* | Ao fornecer uma ID de execução exata do pipeline, uma análise de pipeline é executada. |

## Recursos fora do escopo {#out-of-scope-features}

A solução de problemas de pipeline opera na etapa de Teste de build e unidade e na etapa de Verificação de código nos pipelines de Implantação de pilha completa e Qualidade de código. Para outros tipos e etapas de pipeline, depure as falhas baixando e inspecionando os logs.

Consulte [Logs de Acesso e Download](/help/implementing/cloud-manager/manage-logs.md) para obter mais informações.
