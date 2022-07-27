---
title: Restauração de conteúdo em AEM as a Cloud Service
description: Saiba como restaurar o conteúdo as a Cloud Service AEM do backup usando o Cloud Manager.
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: a61eaa8f13c96c87f45f4074ebd15e1dc8597c2c
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---


# Restauração de conteúdo em AEM as a Cloud Service {#content-restore}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Backup e restauração"
>abstract="Saiba como restaurar o conteúdo as a Cloud Service AEM do backup usando o Cloud Manager."

Saiba como restaurar o conteúdo as a Cloud Service AEM do backup usando o Cloud Manager.

## Visão geral {#overview}

O processo de restauração de autoatendimento do Cloud Manager copia dados de backups do sistema Adobe e os restaura em seu ambiente original. Uma restauração é executada para retornar dados que foram perdidos, danificados ou excluídos acidentalmente para sua condição original.

O processo de restauração afeta apenas o conteúdo, deixando o código e a versão do AEM inalterados. Você pode iniciar uma operação de restauração de ambientes individuais a qualquer momento.

O Cloud Manager fornece dois tipos de backups dos quais você pode restaurar o conteúdo.

* **Ponto no tempo (PIT):** Esse tipo é restaurado a partir de backups contínuos do sistema a partir das últimas 24 horas do tempo atual.
* **Semana passada:** Esse tipo é restaurado a partir de backups de sistema nos últimos sete dias, exceto as 24 horas anteriores.

Em ambos os casos, a versão do código personalizado e AEM versão permanece inalterada.

As métricas de desempenho de restauração de conteúdo no AEM as a ContentService referem-se aos benchmarks padronizados:

* **RTO (Recovery Time Objetive, objetivo de tempo de recuperação):** O Objetivo de Tempo de Recuperação varia dependendo do tamanho do repositório, mas, como regra geral, após o início da sequência de recuperação, ela deve levar cerca de 30 minutos.
* **O RPO (Recovery Point Objetive, objetivo de ponto de recuperação):** O objetivo do ponto de recuperação é no máximo 24 horas

>[!TIP]
>
>Também é possível restaurar backups [usando a API pública.](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)

## Limitações           {#limitations}

O uso do mecanismo de restauração de autoatendimento está sujeito às seguintes limitações.

* As operações de restauração são limitadas a sete dias, o que significa que não é possível restaurar um instantâneo com mais de sete dias.
* No máximo dez restaurações bem-sucedidas são permitidas em todos os ambientes em um programa por mês de calendário.
* Após a criação do ambiente, leva seis horas até que o primeiro instantâneo de backup seja criado. Até que esse instantâneo seja criado, nenhuma restauração poderá ser executada no ambiente.
* Uma operação de restauração não será iniciada se houver uma pilha completa ou um pipeline de configuração de camada da Web em execução no momento para o ambiente .
* Uma restauração não pode ser iniciada se outra restauração já estiver em execução no mesmo ambiente.
* Em casos raros, devido ao limite de 24 horas/sete dias em backups, o backup selecionado pode se tornar indisponível devido a um atraso entre o momento em que foi selecionado e o momento em que a restauração é iniciada.
* Os dados de ambientes excluídos são perdidos permanentemente e não podem ser recuperados.

## Restaurar conteúdo {#restoring-content}

Primeiro, determine o período do conteúdo que você deseja restaurar. Em seguida, para restaurar o conteúdo do ambiente a partir de um backup, execute essas etapas.

>[!NOTE]
>
>Um usuário com a **Proprietário da empresa** ou **Gerenciador de implantação** deve estar conectado para iniciar uma operação de restauração.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada.

1. Clique no programa para o qual deseja iniciar uma restauração.

1. No **Visão geral do programa** na página **Ambientes** , clique no botão de reticências ao lado do ambiente para o qual deseja iniciar uma restauração e selecione **Restaurar conteúdo**.

   ![Opção de restauração](assets/backup-option.png)

   * Como alternativa, você pode navegar diretamente para a **Restaurar conteúdo** da página de detalhes do ambiente de um ambiente específico.

1. No **Restaurar conteúdo** da página de detalhes do ambiente, selecione primeiro o período de tempo da restauração no **Tempo para restaurar** lista suspensa.

   1. Se você selecionar **Últimas 24 horas** o vizinho **Hora** permite especificar o tempo exato nas últimas 24 horas para restauração.

      ![Últimas 24 horas](assets/backup-time.png)

   1. Se você selecionar **Semana passada** o vizinho **Dia** permite selecionar uma data nos últimos sete dias, exceto as 24 horas anteriores.

      ![Semana passada](assets/backup-date.png)

1. Depois de selecionar uma data ou especificar uma hora, a variável **Backups disponíveis** a seção abaixo mostra uma lista de backups disponíveis que podem ser restaurados

   ![Backups disponíveis](assets/backup-available.png)

1. Encontre o backup que deseja restaurar usando o ícone de informações para exibir informações sobre a versão do código e AEM versão incluída nesse backup e considere as implicações de uma restauração quando [escolher o backup.](#choosing-the-right-backup)

   ![Informações de backup](assets/backup-info.png)

   * Observe que o carimbo de data e hora exibido para as opções de restauração é baseado no fuso horário do computador do usuário.

1. Clique no botão **Restaurar** ícone na extremidade direita da linha que representa o backup que você deseja restaurar para iniciar o processo de restauração.

1. Revise os detalhes da **Restaurar conteúdo** , antes de confirmar sua solicitação, clicando em **Restaurar**.

   ![Confirmar restauração](assets/backup-restore.png)

O processo de backup é iniciado e você pode visualizar seu status na **[Restaurar atividade](#restore-activity)** tabela. O tempo necessário para a conclusão de uma operação de restauração depende do tamanho e do perfil do conteúdo que está sendo restaurado.

Quando a restauração for concluída com êxito, o ambiente:

* Execute o mesmo código e AEM versão do no momento de iniciar a operação de restauração.
* Ter o mesmo conteúdo que estava disponível no carimbo de data e hora do instantâneo escolhido, com os índices recriados para corresponder ao código atual.

## Escolhendo o backup certo {#choosing-backup}

Restaura apenas o conteúdo do para o AEM. Por isso, você deve considerar cuidadosamente as alterações de código que foram feitas entre seu ponto de restauração desejado e o horário atual, revisando o histórico de commit entre a sua ID de confirmação atual e a que está sendo restaurada.

Há vários cenários.

* O código personalizado no ambiente e a restauração estão no mesmo repositório e na mesma ramificação.
* O código personalizado no ambiente e a restauração estão no mesmo repositório, mas em uma ramificação diferente com uma confirmação comum.
* O código personalizado no ambiente e a restauração estão em repositórios diferentes.
   * Nesse caso, uma ID de confirmação não será exibida.
   * É altamente recomendável clonar ambos os repositórios e usar uma ferramenta de comparação para comparar as ramificações.

Além disso, lembre-se de que uma restauração pode fazer com que seus ambientes de produção e de preparo fiquem fora de sincronia. Você é responsável pelas consequências da restauração do conteúdo.

## Restaurar atividade {#restore-activity}

O **Restaurar atividade** tabela mostra o status das dez solicitações de restauração mais recentes, incluindo quaisquer operações de restauração ativas.

![Atividade de restauração](assets/backup-activity.png)

Ao clicar no ícone de informações de um backup, é possível baixar logs desse backup, além de inspecionar os detalhes do código, incluindo as diferenças entre o snapshot e os dados no momento em que a restauração foi iniciada.

## Backup externo {#offsite-backup}

Os backups regulares cobrem o risco de exclusões acidentais ou falhas técnicas nos serviços da nuvem AEM, mas podem surgir riscos adicionais da falha de uma região. Além da disponibilidade, o maior risco de paralisação nessa região é a perda de dados.

AEM as a Cloud Service reduz esse risco para todos os ambientes de produção AEM copiando continuamente todo o conteúdo AEM para uma região remota e disponibilizando-o para recuperação por um período de três meses. Esse recurso é conhecido como backup externo.

A restauração dos serviços em nuvem AEM para ambientes de preparo e produção a partir de backup externo é realizada pela AEM Service Reliability Engineering em caso de paralisação da região de dados.
