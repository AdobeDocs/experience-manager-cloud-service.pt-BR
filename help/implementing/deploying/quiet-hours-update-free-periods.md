---
title: Período de silêncio e atualização dos períodos livres
description: Saiba como minimizar o impacto operacional das atualizações automáticas do AEM as a Cloud Service usando o Período de silêncio e os Períodos livres de atualizações.
feature: Deploying
role: Admin
badge: label="Disponibilidade limitada" type="Positive"
exl-id: 54f86a58-eb56-43e6-ab51-7af7466a2d40
source-git-commit: 350b288d30b3fb8d9d308dbd279f579cec0b292c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Período de silêncio e atualização dos períodos livres {#quiet-hours-update-free-periods}

>[!NOTE]
>Esse recurso estará disponível como um recurso de **Disponibilidade limitada** a partir de 25 de setembro. Envie um email para [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) para ativar o recurso em seus programas.

As [atualizações automáticas de manutenção](/help/implementing/deploying/aem-version-updates.md) do AEM as a Cloud Service garantem que suas instâncias permaneçam seguras e atualizadas com as versões de manutenção mais recentes. Dito isso, em alguns casos (como eventos de ativação), pode ser necessário &quot;proteger&quot; essas horas de trabalho críticas contra possíveis interrupções. Dessa forma, a AEM as a Cloud Service oferece a opção de definir um período no qual as atualizações automáticas não ocorrem para seus programas em andamento.

Você pode configurar esses intervalos de tempo usando duas opções de agendamento:

* **Horas de silêncio** - Você pode definir um intervalo de tempo diário (até 8 horas) em que as atualizações não ocorrerão.
* **Atualizar períodos livres** - Você pode definir um período de 7 dias em que as atualizações não ocorrerão. Você pode ter até três períodos livres de atualização em um período de 12 meses.

Os recursos de atualização de períodos livres e horários silenciosos são configurados com base em &quot;por programa&quot;.

Além disso, para obter informações sobre períodos programados de manutenção automática do AEM as a Cloud Service, consulte a página [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

## Horas de silêncio {#quiet-hours}

Ao usar o recurso de horários silenciosos, é possível definir uma janela de tempo durante o dia sem atualizações automáticas. Todas as atualizações de manutenção mudarão para ocorrer fora da janela de tempo configurada. Se, por exemplo, uma atualização for agendada durante as horas de silêncio especificadas, ela será iniciada automaticamente após o término do intervalo de horas de silêncio. O intervalo de tempo configurado não pode exceder 8 horas para que as atualizações ainda possam ocorrer diariamente.

Você pode definir estas horas de silêncio **por programa**, usando seu fuso horário local.

### Como configurar o intervalo de horas de silêncio {#configure-quiet-hours}

O intervalo de horas de silêncio pode ser configurado usando a interface do AEM Cloud Manager da seguinte maneira:

Vá para **Atividades>Atualizações Automáticas>Opções de Atualização**.

![Configuração](assets/main-config.png)

1. Verifique se a opção **Impedir atualizações automáticas durante horas específicas** está alternada.
2. Clique em **Editar**.
3. Defina o intervalo de horas de silêncio na janela de configuração.

![Configuração de Período de Silêncio](assets/quiet-hours.png)

Uma vez definidas, suas horas de início e término especificadas serão aplicadas a todos os dias do calendário subsequentes. Você pode desativar ou reconfigurar o valor de tempo do horário de silêncio conforme necessário.

## Atualizar períodos livres {#update-free-periods}

Ao usar o recurso de atualização de períodos gratuitos, você pode definir um período de 7 dias em que as atualizações não ocorrerão. Uma vez configuradas, todas as atualizações de manutenção serão automaticamente alteradas para que ocorram fora do período definido. Você pode ter até três períodos livres de atualização em um intervalo de 12 meses. Além disso, os períodos livres de atualização podem ser designados com até um ano de antecedência.

Ao configurar essa opção, lembre-se de que (pelo menos) um intervalo de uma semana entre os períodos é obrigatório para facilitar as atualizações automáticas. Dessa forma, esse intervalo de uma semana é aplicado automaticamente e será adicionado ao calendário entre os períodos livres de atualização configurados. Isso pode resultar em alguns dias de calendário não disponíveis para seleção.

Você pode definir os períodos livres de atualização **por programa**.

### Como configurar os períodos livres de atualização {#configure-update-free-periods}

O recurso de atualização de períodos livres pode ser configurado usando a interface do AEM Cloud Manager da seguinte maneira:

Vá para **Atividades>Atualizações Automáticas>Opções de Atualização**.

![Configuração](assets/main-config.png)

1. Acesse a seção Atualizar períodos livres.
2. Clique em **Adicionar período livre de atualização**.
3. Selecione um período livre de atualização de uma semana no calendário.

![Atualizar Configuração de Períodos Livres](assets/update-free-periods.png)

Um ícone **Ativo** será exibido próximo ao período livre de atualização ativo no momento e um ícone **Concluído** próximo aos períodos livres de atualização concluídos.
