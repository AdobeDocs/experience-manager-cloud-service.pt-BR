---
title: Digital Rights Management em [!DNL Assets]
description: Saiba como gerenciar estados de expiração de ativos e informações para ativos licenciados em [!DNL Experience Manager] as a [!DNL Cloud Service].
contentOwner: AG
feature: Gerenciamento de ativos,DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: f993148a9f678cfdaf0693e4964f02b9163cf2ff
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 2%

---

# Digital Rights Management por ativos digitais {#digital-rights-management-in-assets}

Os ativos digitais geralmente são associados a uma licença que especifica os termos e a duração do uso. Usando a plataforma [!DNL Experience Manager], você pode gerenciar com eficiência as informações de expiração de ativos e as informações de licenciamento.

## Expiração do ativo {#asset-expiration}

Para impor requisitos de licença para ativos, use informações de expiração de ativos. As informações de expiração garantem que o ativo publicado não seja publicado quando expira, o que impede a violação da licença. Um usuário sem permissões de administrador não pode editar, copiar, mover, publicar e baixar um ativo expirado.

Você pode visualizar o status de expiração de um ativo nos seguintes locais:

* **Exibição** de cartão: Para um ativo expirado, um sinalizador no cartão indica que ele expirou.
* **Exibição** de lista: Para um ativo expirado, a  **** coluna Status exibe o  **** Expiredbanner.
* **Linha do tempo**: Você pode visualizar o status de expiração de um ativo na linha do tempo. Selecione o ativo e escolha Linha do tempo.
* **Trilho** de referências: Você também pode visualizar o status de expiração dos ativos no painel  **** Referências. Ele gerencia status de expiração de ativos e relacionamentos entre ativos compostos e subativos, coleções e projetos referenciados.

Para exibir a referência a páginas da Web e ativos compostos para um ativo, siga estas etapas:

1. Navegue até o ativo, selecione-o e clique em ![ícone de referências de conteúdo do painel esquerdo](assets/do-not-localize/content-rail-icon.png). O painel esquerdo é aberto.
1. Selecione **[!UICONTROL Referências]** no painel esquerdo.
1. Para ativos expirados, o [!UICONTROL Referências] exibe o status de expiração como **[!UICONTROL Ativo expirado]**. Se o ativo tiver expirado os subativos, o painel [!UICONTROL Referências] exibirá o status **[!UICONTROL Ativo tiver subativos expirados]**.

### Pesquisar ativos expirados {#search-expired-assets}

Para pesquisar um ativo expirado, incluindo subativos expirados, siga estas etapas:

1. No console [!DNL Assets], clique em **[!UICONTROL Pesquisar]** na barra de ferramentas e pressione `Enter`.

1. Clique no ícone de Navegação global e selecione a opção **[!UICONTROL Status de expiração]**.

1. Selecione **[!UICONTROL Expirado]**. Os resultados da pesquisa exibem os ativos expirados.

Ao escolher a opção **[!UICONTROL Expirado]**, o console [!DNL Assets] exibe somente os ativos e subativos expirados referenciados por ativos compostos. Os ativos compostos que fazem referência a subativos expirados não são exibidos imediatamente após a expiração dos subativos. Em vez disso, elas são exibidas depois que [!DNL Experience Manager] detecta que fazem referência a subativos expirados na próxima vez que o programador for executado.

É possível modificar a data de expiração de um ativo publicado para uma data anterior ao ciclo do programador atual. No entanto, a programação ainda detecta um ativo como expirado quando ele é executado na próxima vez e [!DNL Experience Manager] reflete o status em seu relatório. A data de expiração de um ativo é exibida de forma diferente para usuários em fusos horários diferentes.

Além disso, se um erro impedir que o scheduler detecte ativos expirados no ciclo atual, o scheduler reexamina esses ativos no próximo ciclo e detecta seu status expirado.

Para permitir que o console [!DNL Assets] exiba os ativos compostos de referência junto com os subativos expirados, configure o fluxo de trabalho **[!UICONTROL Notificação de expiração do Adobe CQ DAM]** em [!DNL Experience Manager]. O programador baseado em tempo agendará uma tarefa para verificar em um horário específico se um ativo expirou em subativos. Após a conclusão do trabalho, os ativos que expiraram os subativos e os ativos referenciados são exibidos como expirados nos resultados da pesquisa.

1. Acesse o repositório Git [!DNL Cloud Manager] associado ao seu ambiente.
1. Confirme um arquivo chamado `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` no repositório com o seguinte conteúdo.

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. Siga as instruções de [como fazer a configuração OSGi em [!DNL Experience Manager] as a2/>. [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md)

Você pode configurar o scheduler usando as seguintes propriedades:

* Um valor `true` da propriedade `cq.dam.expiry.notification.scheduler.istimebased` inicia o agendador. * O valor da propriedade `cq.dam.expiry.notification.scheduler.timebased.rule` é a expressão regular para definir o tempo. O exemplo acima inicia o trabalho do agendador em 00 horas.
* Se `send_email` estiver definido como `true`, o criador de ativos (a pessoa que faz upload de um ativo específico para [!DNL Assets]) receberá um email quando o ativo expirar.
* O número máximo de ativos expirados em uma iteração do programador é o valor da propriedade `asset_expired_limit`.
* Para executar o trabalho periodicamente, defina o valor da propriedade `cq.dam.expiry.notification.scheduler.istimebased` como `false` e defina o valor da propriedade `cq.dam.expiry.notification.scheduler.period.rule` com o tempo em segundos.

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1.  For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## Estados do ativo {#asset-states}

O console [!DNL Assets] pode exibir vários estados para ativos. Dependendo do estado atual de um ativo específico, sua exibição de cartão exibe um rótulo que descreve seu estado, por exemplo, Expirado, Publicado, Aprovado, Rejeitado e assim por diante.

1. Na interface do usuário [!DNL Assets], selecione um ativo.

1. Selecione **[!UICONTROL Publicar]** na barra de ferramentas. Se você não vir a opção [!UICONTROL Publish] na barra de ferramentas, clique em **[!UICONTROL Mais]** na barra de ferramentas e localize a opção **[!UICONTROL Publicar]**.

1. Escolha **[!UICONTROL Publish]** no menu e feche a caixa de diálogo de confirmação.

1. Sair do modo de seleção. O status da publicação do ativo é exibido na parte inferior da miniatura do ativo na exibição de cartão. Na exibição de lista, a coluna Publicado exibe o horário em que o ativo foi publicado.

1. Para exibir a página Detalhes do ativo, na interface [!DNL Assets], selecione um ativo e clique em **[!UICONTROL Propriedades]**.

1. Na guia [!UICONTROL Advanced], defina uma data de expiração para o ativo a partir do campo **[!UICONTROL Expires]**.

1. Clique em **[!UICONTROL Salvar]** e em **[!UICONTROL Fechar]** para exibir o console Ativo.

1. O status da publicação do ativo indica um status expirado na parte inferior da miniatura do ativo na exibição de cartão. Na exibição de lista, o status do ativo é exibido como **[!UICONTROL Expirado]**.

1. No console [!DNL Assets], selecione uma pasta e crie uma tarefa de revisão na pasta.

1. Revise e aprove/rejeite os ativos na tarefa de revisão e clique em **[!UICONTROL Concluir]**.

1. Navegue até a pasta para a qual você criou a tarefa de revisão. O status dos ativos que você aprovou/rejeitou é exibido na parte inferior da exibição de cartão. Na exibição em lista, os status de aprovação e expiração são exibidos em colunas apropriadas.

1. Para pesquisar ativos com base em seu status, clique em **[!UICONTROL Pesquisar]** para exibir a barra de pesquisa.

1. Selecione `Return` e clique em [!DNL Experience Manager].

1. No painel de pesquisa, clique em **[!UICONTROL Publicar status]** e selecione **[!UICONTROL Publicado]** para procurar ativos publicados em [!DNL Assets].

1. Para pesquisar ativos aprovados ou rejeitados, selecione **[!UICONTROL Status de Aprovação]** e selecione a opção apropriada.

1. Para pesquisar ativos com base no status de expiração, selecione **[!UICONTROL Status de expiração]** no painel de pesquisa e selecione a opção apropriada.

1. Também é possível pesquisar ativos com base em uma combinação de status em vários aspectos de pesquisa. Por exemplo, você pode procurar ativos publicados que são aprovados em uma tarefa de revisão e não estão expirados. Para pesquisar esses ativos, selecione as opções apropriadas nos aspectos de pesquisa.

## Digital Rights Management em [!DNL Assets] {#digital-rights-management-in-assets-1}

A funcionalidade de DRM impõe a aceitação do contrato de licença antes que você possa baixar um ativo licenciado de [!DNL Assets].

Se você selecionar um ativo protegido e clicar em **[!UICONTROL Download]**, será redirecionado para uma página de licença para aceitar o contrato de licença. Se você não aceitar o contrato de licença, a opção **[!UICONTROL Download]** não estará disponível.

Se a seleção contiver vários ativos protegidos, selecione um ativo de cada vez, aceite o contrato de licença e continue para baixar o ativo.

Um ativo é considerado protegido se qualquer uma dessas condições for satisfeita:

* A propriedade de metadados do ativo `xmpRights:WebStatement` aponta para o caminho da página que contém o contrato de licença do ativo.
* O valor da propriedade de metadados do ativo `adobe_dam:restrictions` é um HTML bruto que especifica o contrato de licença.

>[!NOTE]
>
>O local `/etc/dam/drm/licences` foi usado para armazenar licenças nas versões anteriores de [!DNL Experience Manager]. A localização está obsoleta agora. Se você criar ou modificar páginas de licença ou porta as páginas de versões anteriores [!DNL Experience Manager], o Adobe recomenda que você armazene esses ativos em `/apps/settings/dam/drm/licenses` ou `/conf/*/settings/dam/drm/licenses` locais.

### Baixar ativos protegidos por DRM {#downloading-drm-assets}

1. Na exibição de cartão, selecione os ativos que deseja baixar e selecione **[!UICONTROL Download]**.
1. Na página **[!UICONTROL Gerenciamento de direitos autorais]**, selecione o ativo que deseja baixar na lista.
1. No painel [!UICONTROL Licença], escolha **[!UICONTROL Concordar]**. Uma marca de seleção aparece ao lado do ativo. Selecione a opção **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >A opção **[!UICONTROL Download]** só é ativada quando você opta por concordar com o contrato de licença de um ativo protegido. No entanto, se sua seleção incluir ativos protegidos e desprotegidos, somente os ativos protegidos serão listados no painel e a opção **[!UICONTROL Download]** estará disponível para baixar os ativos desprotegidos. Para aceitar simultaneamente contratos de licença para vários ativos protegidos, selecione os ativos na lista e escolha **[!UICONTROL Concordar]**.

1. Para baixar o ativo ou suas representações, selecione **[!UICONTROL Download]** na caixa de diálogo.
