---
title: Como definir as configurações de Ausência Temporária no AEM Forms?
description: Delegue tarefas enquanto estiver fora do escritório ou fora dele para uma execução perfeita do fluxo de trabalho.
exl-id: c7e436f1-8e1c-4334-b3dc-ab9800695301
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 1%

---


# Definir configuração de Ausência Temporária {#configure-out-of-office-settings}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/configure-out-of-office-settings.html) |
| AEM as a Cloud Service | Este artigo |

Se você planeja ficar fora do escritório, é possível especificar o que acontece com os itens atribuídos a você nesse período.

Você tem a opção de especificar uma data e hora de início e uma data e hora de término para que suas configurações de ausência temporária entrem em vigor. Se você estiver localizado em um fuso horário diferente do servidor, o fuso horário usado será o do cliente.

Você pode definir uma pessoa padrão para a qual todos os seus itens serão enviados. Você também pode especificar exceções para itens de processos específicos a serem enviados para um usuário diferente ou para permanecer em sua Caixa de entrada até retornar. Se a pessoa designada também estiver fora do escritório, o item vai para o usuário designado. Se o item não puder ser atribuído a um usuário que não esteja ausente, o item permanecerá em sua Caixa de entrada.

Você pode segregar a delegação de itens com base nos modelos de fluxo de trabalho. Por exemplo, é possível atribuir um item relacionado ao Fluxo de trabalho A ao usuário A e atribuir um item relacionado ao Fluxo de trabalho B ao usuário B.


>[!NOTE]
>
>* Quando você habilita a configuração Fora do escritório, todos os itens disponíveis em sua Caixa de entrada antes de habilitar a configuração permanecem em sua caixa de entrada. Somente os itens recebidos após a ativação da configuração são delegados.
>* Quando você desativa a configuração Ausência Temporária, os itens delegados não são automaticamente atribuídos de volta a você. Você pode usar a funcionalidade de declaração para atribuir itens a você.
>* Quando o Usuário A delega itens ao Usuário B e o Usuário B delega ainda mais ao Usuário C, os itens são atribuídos apenas ao Usuário C e não ao Usuário B.
>* Quando houver um loop na atribuição, as tarefas permanecerão com o usuário original. Por exemplo, quando o Usuário A delega itens ao Usuário B, o Usuário B delega ao Usuário C, o Usuário C delega ao Usuário D e o Usuário D delega ao Usuário B, um loop é criado. Nessa situação, o item permanece com o Usuário original. O usuário A é o usuário original no exemplo acima.

## Ativar a configuração de Ausência Temporária para sua conta {#enable-out-of-office}

Execute as seguintes etapas para Ativar a configuração Ausência Temporária para sua conta e delegar seus Itens da Caixa de entrada a outro usuário:

1. Faça logon na instância do AEM. Selecione o ![Caixa de entrada](assets/bell.svg) e selecione **[!UICONTROL Exibir todos]**. Uma lista dos itens da caixa de entrada é exibida.
1. Selecione o ![Exibir seletor](assets/viewlist.svg) ou ![Exibir seletor](assets/calendar.svg) ícone ao lado do **[!UICONTROL Criar]** e selecione **[!UICONTROL Configurações]**. A caixa de diálogo de configurações é exibida.
1. Abra o **[!UICONTROL Fora do escritório]** na caixa de diálogo de configurações.
1. Selecione o **[!UICONTROL Ativar/desativar]** botão para ativar a configuração Out of Office.
1. Especifique a **[!UICONTROL Hora de início]**  e **[!UICONTROL Hora de término]** para a configuração. Os itens são delegados somente durante o período especificado. Deixe a **[!UICONTROL Hora de término]** campo vazio para delegar itens por um período indefinido.
1. Selecione o **[!UICONTROL Encaminhar meus itens durante este período]** caixa de seleção Se você não selecionar a opção e não especificar um destinatário, seus itens não serão encaminhados a nenhum usuário. Embora você esteja ausente e a configuração esteja ativada, os itens permanecem na sua Caixa de entrada.
1. Selecionar **[!UICONTROL Adicionar atribuidor]**. Especifique um usuário no **[!UICONTROL Destinatário]** campo ao qual os itens serão delegados. Especifique a **[!UICONTROL Modelo de fluxo de trabalho]** para delegar ao usuário especificado. É possível selecionar mais de um modelo de fluxo de trabalho.

   Além disso, para atribuir todos os itens, independentemente do modelo de workflow, a um usuário específico, selecione **[!UICONTROL Todos os fluxos de trabalho]** na lista suspensa Workflow Model. <br>

   Para atribuir itens a um usuário específico para todos os modelos de workflow, exceto alguns, selecione **[!UICONTROL Todos os fluxos de trabalho]** na lista suspensa Modelo de workflow, selecione **[!UICONTROL + Adicionar exceções]**e especifique os modelos de fluxo de trabalho que serão deixados de fora.
   <br>

   Repita a etapa para adicionar mais atribuídos. <br>

   >[!NOTE]
   >
   >A ordem dos designados é importante. Quando um item é atribuído a um usuário que ativou a configuração de ausência temporária, o item é avaliado em relação à lista de responsáveis especificada na ordem em que os responsáveis são adicionados. Quando um item corresponde aos critérios, ele é atribuído ao destinatário e o próximo destinatário não é verificado.


1. Selecionar **[!UICONTROL Salvar]**. A configuração entra em vigor na data e hora de início especificadas. Se você fizer logon enquanto estiver fora do escritório, não será considerado como estando no escritório até que altere suas configurações.

Agora, os itens atribuídos a você durante o período de Ausência Temporária são automaticamente atribuídos ao destinatário especificado.
![Fora do escritório](assets/out-of-office.png)

>[!NOTE]
>
>(Somente para itens de fluxo de trabalho centrados no Forms) Ative a opção **[!UICONTROL Permitir que o destinatário delegue usando as configurações &quot;Ausente&quot;]** opção do **[!UICONTROL Atribuir tarefa]** etapa no fluxo de trabalho. Somente os itens que têm a opção acima ativada são delegados a outros usuários.
>(Somente para itens de fluxo de trabalho centrados no Forms) Ative a opção **[!UICONTROL Permitir que o destinatário delegue usando as configurações &quot;Ausente&quot;]** opção do **[!UICONTROL Atribuir tarefa]** etapa no fluxo de trabalho. Somente os itens que têm a opção mencionada anteriormente ativada são delegados a outros usuários.

## Limitações {#limitations}

* Não há suporte para a atribuição de itens a um grupo.
* No momento, não há suporte para a habilitação de Ausência Temporária para tarefas de projeto.
