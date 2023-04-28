---
title: Digital Rights Management em [!DNL Assets]
description: Saiba como gerenciar estados de expiração de ativos e informações de ativos licenciados no [!DNL Experience Manager] como [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 3%

---

# Digital Rights Management por ativos digitais {#digital-rights-management-in-assets}

Os ativos digitais geralmente são associados a uma licença que especifica os termos e a duração do uso. Usar o [!DNL Experience Manager] você pode gerenciar com eficiência as informações de expiração de ativos e de licenciamento.

## Expiração do ativo {#asset-expiration}

Para impor requisitos de licença para ativos, use informações de expiração de ativos. As informações de expiração garantem que o ativo publicado não seja publicado quando expira, o que impede a violação da licença. Um usuário sem permissões de administrador não pode editar, copiar, mover, publicar e baixar um ativo expirado.

Você pode visualizar o status de expiração de um ativo nos seguintes locais:

* **Exibição de cartão**: Para um ativo expirado, um sinalizador no cartão indica que ele expirou.
* **Exibição de lista**: Para um ativo expirado, a variável **[!UICONTROL Status]** exibe a **[!UICONTROL Expirado]** banner.
* **Linha do tempo**: Você pode visualizar o status de expiração de um ativo na linha do tempo. Selecione o ativo e escolha Linha do tempo.
* **Painel Referências**: Você também pode visualizar o status de expiração dos ativos na **[!UICONTROL Referências]** trilho. Ele gerencia status de expiração de ativos e relacionamentos entre ativos compostos e subativos, coleções e projetos referenciados.

Para exibir a referência a páginas da Web e ativos compostos para um ativo, siga estas etapas:

1. Navegue até o ativo, selecione-o e clique em ![ícone de referências de conteúdo do painel esquerdo](assets/do-not-localize/content-rail-icon.png). O painel esquerdo é aberto.
1. Selecionar **[!UICONTROL Referências]** no painel esquerdo.
1. Para ativos expirados, a variável [!UICONTROL Referências] exibe o status de expiração como **[!UICONTROL O ativo está expirado]**. Se o ativo tiver expirado os subativos, a variável [!UICONTROL Referências] painel exibe o status **[!UICONTROL O ativo venceu os subativos]**.

### Pesquisar ativos expirados {#search-expired-assets}

Para pesquisar um ativo expirado, incluindo subativos expirados, siga estas etapas:

1. No [!DNL Assets] , clique em **[!UICONTROL Pesquisar]** na barra de ferramentas e pressione `Enter`.

1. Clique no ícone de Navegação global e selecione o **[!UICONTROL Status de expiração]** opção.

1. Selecionar **[!UICONTROL Expirado]**. Os resultados da pesquisa exibem os ativos expirados.

Ao escolher a variável **[!UICONTROL Expirado]** , a variável [!DNL Assets] O console exibe somente os ativos e subativos expirados referenciados por ativos compostos. Os ativos compostos que fazem referência a subativos expirados não são exibidos imediatamente após a expiração dos subativos. Em vez disso, elas serão exibidas após [!DNL Experience Manager] O detecta que eles fazem referência a subativos expirados na próxima vez que o agendador for executado.

É possível modificar a data de expiração de um ativo publicado para uma data anterior ao ciclo do programador atual. No entanto, a programação ainda detecta esse ativo como um ativo expirado quando ele é executado na próxima vez e [!DNL Experience Manager] reflete o status em seu relatório. A data de expiração de um ativo é exibida de forma diferente para usuários em fusos horários diferentes.

Além disso, se um erro impedir que o scheduler detecte ativos expirados no ciclo atual, o scheduler reexamina esses ativos no próximo ciclo e detecta seu status expirado.

Para ativar o [!DNL Assets] para exibir os ativos compostos de referência junto com os subativos expirados, configure **[!UICONTROL Notificação de expiração do Adobe CQ DAM]** fluxo de trabalho em [!DNL Experience Manager]. O programador baseado em tempo agendará uma tarefa para verificar em um horário específico se um ativo expirou em subativos. Após a conclusão do trabalho, os ativos que expiraram os subativos e os ativos referenciados são exibidos como expirados nos resultados da pesquisa.

1. Acesse o [!DNL Cloud Manager] Repositório Git associado ao seu ambiente.
1. Confirmar um arquivo chamado `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` no repositório com o seguinte conteúdo.

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. Siga as instruções de [como fazer a configuração do OSGi em [!DNL Experience Manager] como [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

Você pode configurar o scheduler usando as seguintes propriedades:

* A `true` valor da propriedade `cq.dam.expiry.notification.scheduler.istimebased` inicia o agendador. * O valor da propriedade `cq.dam.expiry.notification.scheduler.timebased.rule` é a expressão regular para definir a hora. O exemplo acima inicia o trabalho do agendador em 00 horas.
* If `send_email` está definida como `true`, o criador do ativo (a pessoa que faz upload de um ativo específico para o [!DNL Assets]) recebe um email quando o ativo expira.
* O número máximo de ativos expirados em uma iteração do programador é o valor da propriedade `asset_expired_limit`.
* Para executar o trabalho periodicamente, defina o valor da propriedade `cq.dam.expiry.notification.scheduler.istimebased` as `false` e defina o valor da propriedade `cq.dam.expiry.notification.scheduler.period.rule` com o tempo em segundos.

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1. For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## Estados do ativo {#asset-states}

O [!DNL Assets] O console pode exibir vários estados para ativos. Dependendo do estado atual de um ativo específico, sua exibição de cartão exibe um rótulo que descreve seu estado, por exemplo, Expirado, Publicado, Aprovado, Rejeitado e assim por diante.

1. No [!DNL Assets] interface do usuário, selecione um ativo.

1. Selecionar **[!UICONTROL Publicar]** na barra de ferramentas. Se você não vir [!UICONTROL Publicar] na barra de ferramentas, clique em **[!UICONTROL Mais]** na barra de ferramentas e localize **[!UICONTROL Publicar]** opção.

1. Choose **[!UICONTROL Publicar]** no menu e feche a caixa de diálogo de confirmação.

1. Sair do modo de seleção. O status da publicação do ativo é exibido na parte inferior da miniatura do ativo na exibição de cartão. Na exibição de lista, a coluna Publicado exibe o horário em que o ativo foi publicado.

1. Para exibir a página de detalhes do ativo, no [!DNL Assets] selecione um ativo e clique em **[!UICONTROL Propriedades]**.

1. No [!UICONTROL Avançado] , defina uma data de expiração para o ativo no **[!UICONTROL Expira]** campo.

1. Clique em **[!UICONTROL Salvar]** e, em seguida, clique em **[!UICONTROL Fechar]** para exibir o console Ativo .

1. O status da publicação do ativo indica um status expirado na parte inferior da miniatura do ativo na exibição de cartão. Na exibição de lista, o status do ativo é exibido como **[!UICONTROL Expirado]**.

1. No [!DNL Assets] selecione uma pasta e crie uma tarefa de revisão na pasta.

1. Revise e aprove/rejeite os ativos na tarefa de revisão e clique em **[!UICONTROL Concluído]**.

1. Navegue até a pasta para a qual você criou a tarefa de revisão. O status dos ativos que você aprovou/rejeitou é exibido na parte inferior da exibição de cartão. Na exibição em lista, os status de aprovação e expiração são exibidos em colunas apropriadas.

1. Para pesquisar ativos com base em seu status, clique em **[!UICONTROL Pesquisar]** para exibir a barra de pesquisa.

1. Selecionar `Return` e clique em [!DNL Experience Manager].

1. No painel de pesquisa, clique em **[!UICONTROL Publicar status]** e selecione **[!UICONTROL Publicado]** para procurar ativos publicados em [!DNL Assets].

1. Para pesquisar ativos aprovados ou rejeitados, selecione **[!UICONTROL Status da aprovação]** e selecione a opção apropriada.

1. Para pesquisar ativos com base em seu status de expiração, selecione **[!UICONTROL Status de expiração]** no painel de pesquisa e selecione a opção apropriada.

1. Também é possível pesquisar ativos com base em uma combinação de status em vários aspectos de pesquisa. Por exemplo, você pode procurar ativos publicados que são aprovados em uma tarefa de revisão e não estão expirados. Para pesquisar esses ativos, selecione as opções apropriadas nos aspectos de pesquisa.

## Digital Rights Management em [!DNL Assets] {#digital-rights-management-in-assets-1}

A funcionalidade de DRM impõe a aceitação do contrato de licença antes que você possa baixar um ativo licenciado do [!DNL Assets].

Se você selecionar um ativo protegido e clicar em **[!UICONTROL Baixar]**, você é redirecionado para uma página de licença para aceitar o contrato de licença. Se você não aceitar o contrato de licença, a variável **[!UICONTROL Baixar]** não está disponível.

Se a seleção contiver vários ativos protegidos, selecione um ativo de cada vez, aceite o contrato de licença e continue para baixar o ativo.

Um ativo é considerado protegido se qualquer uma dessas condições for satisfeita:

* A propriedade de metadados do ativo `xmpRights:WebStatement` aponta para o caminho da página que contém o contrato de licença do ativo.
* O valor da propriedade de metadados do ativo `adobe_dam:restrictions` é um HTML bruto que especifica o contrato de licença.

>[!NOTE]
>
>A localização `/etc/dam/drm/licences` foi usada para armazenar licenças nas versões anteriores do [!DNL Experience Manager]. A localização está obsoleta agora. Se você criar ou modificar páginas de licença ou porta as páginas das [!DNL Experience Manager] versões, a Adobe recomenda que você armazene esses ativos em `/apps/settings/dam/drm/licenses` ou `/conf/*/settings/dam/drm/licenses` locais.

### Baixar ativos protegidos por DRM {#downloading-drm-assets}

1. Na exibição de cartão, selecione os ativos que deseja baixar e selecione **[!UICONTROL Baixar]**.
1. Na página **[!UICONTROL Gerenciamento de direitos autorais]**, selecione o ativo que deseja baixar na lista.
1. No [!UICONTROL Licença] painel, escolha **[!UICONTROL Concordar]**. Uma marca de seleção aparece ao lado do ativo. Selecione o **[!UICONTROL Baixar]** opção.

   >[!NOTE]
   >
   >O **[!UICONTROL Baixar]** A opção é ativada somente quando você opta por concordar com o contrato de licença de um ativo protegido. No entanto, se sua seleção incluir ativos protegidos e desprotegidos, somente os ativos protegidos serão listados no painel e a variável **[!UICONTROL Baixar]** está disponível para baixar os ativos desprotegidos. Para aceitar simultaneamente contratos de licença para vários ativos protegidos, selecione os ativos na lista e escolha **[!UICONTROL Concordar]**.

1. Para baixar o ativo ou suas representações, selecione **[!UICONTROL Baixar]** na caixa de diálogo.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
