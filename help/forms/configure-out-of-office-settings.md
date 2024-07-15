---
title: Como definir as configurações de Ausência Temporária no AEM Forms?
description: Delegue tarefas enquanto estiver fora do escritório ou fora dele para uma execução perfeita do fluxo de trabalho.
exl-id: c7e436f1-8e1c-4334-b3dc-ab9800695301
feature: Adaptive Forms, Workflow
role: Admin, User
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
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

1. Faça logon na instância do AEM. Selecione o ícone ![Caixa de entrada](assets/bell.svg) e selecione **[!UICONTROL Exibir tudo]**. Uma lista dos itens da caixa de entrada é exibida.
1. Selecione o ícone ![Exibir Seletor](assets/viewlist.svg) ou ![Exibir Seletor](assets/calendar.svg) ao lado do botão **[!UICONTROL Criar]** e selecione **[!UICONTROL Configurações]**. A caixa de diálogo de configurações é exibida.
1. Abra a guia **[!UICONTROL Ausência Temporária]** na caixa de diálogo de configurações.
1. Selecione o botão **[!UICONTROL Habilitar/Desabilitar]** para habilitar a configuração Ausência Temporária.
1. Especifique a **[!UICONTROL Hora de Início]** e a **[!UICONTROL Hora de Término]** para a configuração. Os itens são delegados somente durante o período especificado. Deixe o campo **[!UICONTROL Hora de Término]** vazio para delegar itens por um período indefinido.
1. Marque a caixa de seleção **[!UICONTROL Encaminhar meus itens durante este período]**. Se você não selecionar a opção e não especificar um destinatário, seus itens não serão encaminhados a nenhum usuário. Embora você esteja ausente e a configuração esteja ativada, os itens permanecem na sua Caixa de entrada.
1. Selecione **[!UICONTROL Adicionar Atribuído]**. Especifique um usuário no campo **[!UICONTROL Destinatário]** para delegar os itens. Especifique o **[!UICONTROL Modelo de Fluxo de Trabalho]** para delegar ao usuário especificado. É possível selecionar mais de um modelo de fluxo de trabalho.

   Além disso, para atribuir todos os itens, independentemente do modelo de fluxo de trabalho, a um usuário específico, selecione **[!UICONTROL Todos os fluxos de trabalho]** na lista suspensa Modelo de fluxo de trabalho. <br>

   Para atribuir itens a um usuário específico para todos os modelos de fluxo de trabalho, exceto alguns, selecione **[!UICONTROL Todos os Fluxos de Trabalho]** na lista suspensa Modelo de Fluxo de Trabalho, selecione **[!UICONTROL + Adicionar Exceções]** e especifique os modelos de fluxo de trabalho a serem deixados de fora.
   <br>

   Repita a etapa para adicionar mais atribuídos. <br>

   >[!NOTE]
   >
   >A ordem dos designados é importante. Quando um item é atribuído a um usuário que ativou a configuração de ausência temporária, o item é avaliado em relação à lista de responsáveis especificada na ordem em que os responsáveis são adicionados. Quando um item corresponde aos critérios, ele é atribuído ao destinatário e o próximo destinatário não é verificado.


1. Selecione **[!UICONTROL Salvar]**. A configuração entra em vigor na data e hora de início especificadas. Se você fizer logon enquanto estiver fora do escritório, não será considerado como estando no escritório até que altere suas configurações.

Agora, os itens atribuídos a você durante o período de Ausência Temporária são automaticamente atribuídos ao destinatário especificado.
![Ausência temporária](assets/out-of-office.png)

>[!NOTE]
>
>(Somente para itens de fluxo de trabalho centrados em Forms) Habilite a opção **[!UICONTROL Permitir que o destinatário delegue usando a opção &#39;Ausente&#39;]** da etapa **[!UICONTROL Atribuir tarefa]** no fluxo de trabalho. Somente os itens que têm a opção acima ativada são delegados a outros usuários.
>(Somente para itens de fluxo de trabalho centrados em Forms) Habilite a opção **[!UICONTROL Permitir que o destinatário delegue usando as configurações &#39;Ausente&#39;]** da etapa **[!UICONTROL Atribuir tarefa]** no fluxo de trabalho. Somente os itens que têm a opção mencionada anteriormente ativada são delegados a outros usuários.

## Limitações {#limitations}

* Não há suporte para a atribuição de itens a um grupo.
* No momento, não há suporte para a habilitação de Ausência Temporária para tarefas de projeto.
