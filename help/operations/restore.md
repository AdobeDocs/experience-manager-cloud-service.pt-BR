---
title: Restauração de conteúdo no AEM as a Cloud Service
description: Saiba como restaurar conteúdo do backup no AEM as a Cloud Service usando o Cloud Manager.
exl-id: 921d0c5d-5c29-4614-ad4b-187b96518d1f
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 57%

---


# Restauração de conteúdo no AEM as a Cloud Service {#content-restore}

Saiba como restaurar conteúdo do backup no AEM as a Cloud Service usando o Cloud Manager.

>[!NOTE]
>
>Este recurso só está disponível para [o programa pioneiro](/help/implementing/cloud-manager/release-notes/current.md#early-adoption) e tem certas limitações além daquelas documentadas no artigo. Na fase inicial de adoção:
>
>* O recurso só está disponível em ambientes de desenvolvimento.
>* As restaurações de conteúdo são limitadas a duas por mês por programa.
>
>Para obter detalhes sobre o sistema de backup e restauração existente para AEM as a Cloud Service, consulte [Backup e restauração no AEM as a Cloud Service](/help/operations/backup.md).

## Visão geral {#overview}

O processo de restauração de autoatendimento do Cloud Manager copia dados de backups de sistema da Adobe e os restaura em seu ambiente original. Uma restauração é executada para retornar dados que foram perdidos, danificados ou acidentalmente excluídos à sua condição original.

O processo de restauração afeta apenas o conteúdo, deixando o código e a versão do AEM inalterados. Você pode iniciar uma operação de restauração de ambientes individuais a qualquer momento.

O Cloud Manager fornece dois tipos de backups, a partir dos quais você pode restaurar o conteúdo.

* **Ponto no tempo (PIT):** Esse tipo restaura a partir de backups de sistema contínuos das últimas 24 horas, contadas a partir da hora atual.
* **Semana passada:** esse tipo restaura a partir de backups de sistema dos últimos sete dias, exceto as últimas 24 horas.

Em ambos os casos, a versão do código personalizado e a versão do AEM permanecem inalteradas.

>[!TIP]
>
>Também é possível restaurar backups [usando a API pública.](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)

## Restauração de conteúdo {#restoring-content}

Primeiro, determine o intervalo de tempo do conteúdo que você deseja restaurar. Em seguida, para restaurar o conteúdo do ambiente a partir de um backup, execute essas etapas.

>[!NOTE]
>
>Um usuário com a variável **Proprietário da empresa** ou **Gerente de implantação** A função deve estar conectada para iniciar uma operação de restauração.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique no programa para o qual deseja iniciar uma restauração.

1. No **Visão geral do programa** página, no campo **Ambientes** clique no botão de reticências ao lado do ambiente para o qual deseja iniciar uma restauração e selecione **Restaurar conteúdo**.

   ![Opção de restauração](assets/backup-option.png)

   * Como alternativa, você pode navegar diretamente para a guia **Restaurar conteúdo** da página de detalhes de um ambiente específico.

1. No **Restaurar conteúdo** da página detalhes do ambiente, selecione primeiro o intervalo de tempo da restauração na **Tempo de restauração** lista suspensa.

   1. Se você selecionar **Últimas 24 horas** o vizinho **Hora** permite especificar a hora exata a ser restaurada dentre as últimas 24 horas.

      ![Últimas 24 horas](assets/backup-time.png)

   1. Se você selecionar **Semana passada** o vizinho **Dia** permite selecionar uma data dentre os últimos sete dias, exceto as 24 horas anteriores.

      ![Semana passada](assets/backup-date.png)

1. Depois de selecionar uma data ou especificar uma hora, a seção **Backups disponíveis** abaixo mostra uma lista de backups disponíveis que podem ser restaurados

   ![Backups disponíveis](assets/backup-available.png)

1. Encontre o backup que deseja restaurar usando o ícone de informações para exibir informações sobre a versão do código e do AEM incluídas nesse backup e considere as implicações de uma restauração quando [escolhendo o backup.](#choosing-the-right-backup)

   ![Informações de backup](assets/backup-info.png)

   * O carimbo de data e hora exibido nas opções de restauração é baseado no fuso horário do computador do usuário.

1. Clique em **Restaurar** ícone na extremidade direita da linha que representa o backup que você deseja restaurar para iniciar o processo de restauração.

1. Revise os detalhes na caixa de diálogo **Restaurar conteúdo** antes de confirmar sua solicitação clicando em **Restaurar**.

   ![Confirmar restauração](assets/backup-restore.png)

O processo de backup é iniciado e você pode visualizar seu status no **[Atividades de restauração](#restore-activity)** lista. O tempo necessário para a conclusão de uma operação de restauração depende do tamanho e do perfil do conteúdo que está sendo restaurado.

Quando a restauração for concluída com sucesso, o ambiente:

* Executará o mesmo código e versão do AEM do momento de início da operação de restauração.
* Terá o mesmo conteúdo que estava disponível no carimbo de data e hora do instantâneo escolhido, com os índices recriados para corresponder ao código atual.

## Escolher o backup certo {#choosing-backup}

O processo de restauração de autoatendimento do Cloud Manager restaura apenas o conteúdo para AEM. Por isso, você deve considerar cuidadosamente as alterações de código que foram feitas entre o ponto de restauração desejado e o horário atual, revisando o histórico de confirmações entre a ID de confirmação atual e a que está sendo restaurada.

Existem vários cenários.

* O código personalizado no ambiente e a restauração estão no mesmo repositório e na mesma ramificação.
* O código personalizado no ambiente e a restauração estão no mesmo repositório, mas em uma ramificação diferente com uma confirmação em comum.
* O código personalizado no ambiente e a restauração estão em repositórios diferentes.
   * Nesse caso, uma ID de confirmação não será exibida.
   * É recomendável clonar ambos os repositórios e usar uma ferramenta para comparar as ramificações.

Além disso, lembre-se de que uma restauração pode fazer com que seus ambientes de produção e de preparo fiquem fora de sincronia. Você é responsável pelas consequências da restauração do conteúdo.

## Atividades de restauração {#restore-activity}

A variável **Atividades de restauração** A lista mostra o status das dez solicitações de restauração mais recentes, incluindo quaisquer operações de restauração ativas.

![Atividades de restauração](assets/backup-activity.png)

Ao clicar no ícone de informações de um backup, é possível baixar logs desse backup e inspecionar os detalhes do código, incluindo as diferenças entre o instantâneo e os dados no momento em que a restauração foi iniciada.

## Backup externo {#offsite-backup}

Os backups normais protegem contra o risco de exclusões acidentais ou falhas técnicas nos serviços em nuvem do AEM, mas riscos adicionais podem surgir da falha de uma região. Além da disponibilidade, o maior risco durante interrupções em uma região é a perda de dados.

O AEM as a Cloud Service reduz esse risco para todos os ambientes de produção do AEM, copiando continuamente todo o conteúdo do AEM para uma região remota e disponibilizando-o para recuperação por um período de três meses. Esse recurso é conhecido como backup externo.

A restauração dos serviços em nuvem do AEM para ambientes de preparo e produção a partir do backup externo é realizada pelo Serviço de engenharia de confiabilidade do AEM em caso de interrupções da região de dados.

## Limitações           {#limitations}

O uso do mecanismo de restauração de autoatendimento está sujeito às seguintes limitações.

* As operações de restauração são limitadas a sete dias, o que significa que não é possível restaurar um instantâneo com mais de sete dias.
* No máximo dez restaurações bem-sucedidas são permitidas em todos os ambientes em um programa por mês.
* Após a criação do ambiente, pode levar até seis horas para que o primeiro instantâneo de backup seja criado. Até que esse instantâneo seja criado, nenhuma restauração poderá ser executada no ambiente.
* Uma operação de restauração não será iniciada se houver uma pilha completa ou um pipeline de configuração de camada da Web em execução no momento para o ambiente.
* Uma restauração não pode ser iniciada se outra restauração já estiver em execução no mesmo ambiente.
* Em casos raros, devido ao limite de 24 horas/sete dias para backups, o backup selecionado pode se tornar indisponível devido a um atraso entre o momento em que foi selecionado e o momento em que a restauração é iniciada.
* Os dados de ambientes excluídos são perdidos permanentemente e não podem ser recuperados.
