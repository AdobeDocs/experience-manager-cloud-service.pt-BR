---
title: Digital Rights Management em [!DNL Assets]
description: Saiba como gerenciar estados de expiração de ativos e informações de ativos licenciados no [!DNL Experience Manager] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 4%

---

# Digital Rights Management ativos digitais {#digital-rights-management-in-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/drm.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

Os ativos digitais são frequentemente associados a uma licença que especifica os termos e a duração do uso. Usar o [!DNL Experience Manager] você pode gerenciar com eficiência as informações de expiração de ativos e as informações de licenciamento.

## Expiração do ativo {#asset-expiration}

Para aplicar os requisitos de licença para ativos, use as informações de expiração de ativos. As informações de expiração garantem que a publicação do ativo publicado seja desfeita quando ele expirar, o que impede a violação da licença. Um usuário sem permissões de administrador não pode editar, copiar, mover, publicar e baixar um ativo expirado.

Você pode visualizar o status de expiração de um ativo nos seguintes locais:

* **Exibição de cartão**: Para um ativo expirado, um sinalizador no cartão indica que ele expirou.
* **Exibição de lista**: Para um ativo expirado, a variável **[!UICONTROL Status]** exibe a variável **[!UICONTROL Expirado]** banner.
* **Linha do tempo**: é possível visualizar o status de expiração de um ativo na linha do tempo. Selecione o ativo e escolha Linha do tempo.
* **Painel de referências**: também é possível visualizar o status de expiração dos ativos na **[!UICONTROL Referências]** ferroviário. Ele gerencia os status de expiração dos ativos e os relacionamentos entre ativos compostos e subativos, coleções e projetos referenciados.

Para exibir páginas da Web de referência e ativos compostos de um ativo, siga estas etapas:

1. Navegue até o ativo, selecione-o e clique em ![ícone de referências de conteúdo do painel esquerdo](assets/do-not-localize/content-rail-icon.png). O painel esquerdo se abre.
1. Selecionar **[!UICONTROL Referências]** do painel esquerdo.
1. Para ativos expirados, a variável [!UICONTROL Referências] exibe o status de expiração como **[!UICONTROL O ativo expirou]**. Se o ativo tiver subativos expirados, a variável [!UICONTROL Referências] painel exibe o status **[!UICONTROL O ativo tem subativos expirados]**.

### Pesquisar ativos expirados {#search-expired-assets}

Para pesquisar um ativo expirado, incluindo subativos expirados, siga estas etapas:

1. No [!DNL Assets] , clique em **[!UICONTROL Pesquisar]** na barra de ferramentas e pressione `Enter`.

1. Clique no ícone GlobalNav e selecione o **[!UICONTROL Status de expiração]** opção.

1. Selecionar **[!UICONTROL Expirado]**. Os resultados da pesquisa exibem os ativos expirados.

Ao escolher a variável **[!UICONTROL Expirado]** opção, a variável [!DNL Assets] o console exibe somente os ativos e subativos expirados que são referenciados por ativos compostos. Os ativos compostos que fazem referência aos subativos expirados não são exibidos imediatamente após os subativos expirarem. Em vez disso, eles são exibidos depois de [!DNL Experience Manager] O detecta que fazem referência a subativos expirados na próxima vez que o scheduler for executado.

É possível modificar a data de expiração de um ativo publicado para uma data anterior ao ciclo atual do programador. No entanto, o agendamento ainda detecta esse ativo como um ativo expirado na próxima vez e [!DNL Experience Manager] O reflete o status em seu relatório. A data de expiração de um ativo é exibida de forma diferente para usuários em diferentes fusos horários.

Além disso, se um erro impedir que o scheduler detecte ativos expirados no ciclo atual, o scheduler reexamina esses ativos no próximo ciclo e detecta seu status expirado.

Para ativar o [!DNL Assets] para exibir os ativos compostos de referência junto com os ativos secundários expirados, configure **[!UICONTROL Notificação de expiração do DAM do Adobe CQ]** fluxo de trabalho no [!DNL Experience Manager]. O programador baseado em tempo programa um trabalho para verificar em um momento específico se um ativo expirou subativos. Após a conclusão do trabalho, os ativos que expiraram subativos e os ativos referenciados são exibidos como expirados nos resultados da pesquisa.

1. Acesse o [!DNL Cloud Manager] Repositório Git associado ao seu ambiente.
1. Confirmar um arquivo chamado `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` no repositório com o seguinte conteúdo.

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. Siga as instruções de [como fazer a configuração OSGi no [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

Você pode configurar o scheduler usando as seguintes propriedades:

* A `true` valor da propriedade `cq.dam.expiry.notification.scheduler.istimebased` inicia o programador. * O valor da propriedade `cq.dam.expiry.notification.scheduler.timebased.rule` é a expressão regular que define o tempo. O exemplo acima inicia o trabalho do scheduler às 00 horas.
* Se `send_email` está definida como `true`, o criador do ativo (a pessoa que faz upload de um ativo específico para [!DNL Assets]) recebe um email quando o ativo expira.
* O número máximo de ativos expirados em uma iteração do scheduler é o valor da propriedade `asset_expired_limit`.
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

A variável [!DNL Assets] O console do pode exibir vários estados para ativos. Dependendo do estado atual de um ativo específico, a exibição de cartão exibe um rótulo que descreve seu estado, por exemplo, Expirado, Publicado, Aprovado, Rejeitado etc.

1. No [!DNL Assets] selecione um ativo.

1. Selecionar **[!UICONTROL Publish]** na barra de ferramentas. Se você não vir [!UICONTROL Publish] na barra de ferramentas, clique em **[!UICONTROL Mais]** na barra de ferramentas e localize **[!UICONTROL Publish]** opção.

1. Escolher **[!UICONTROL Publish]** no menu e feche a caixa de diálogo de confirmação.

1. Saia do modo de seleção. O status de publicação do ativo aparece na parte inferior da miniatura do ativo na exibição de cartão. Na exibição em lista, a coluna Publicado exibe a hora em que o ativo foi publicado.

1. Para exibir a página de detalhes do ativo, na [!DNL Assets] selecione um ativo e clique em **[!UICONTROL Propriedades]**.

1. No [!UICONTROL Avançado] defina uma data de expiração para o ativo na guia **[!UICONTROL Expira]** campo.

1. Clique em **[!UICONTROL Salvar]** e clique em **[!UICONTROL Fechar]** para exibir o console de Ativos.

1. O status de publicação do ativo indica um status expirado na parte inferior da miniatura do ativo na exibição de cartão. Na exibição em lista, o status do ativo é exibido como **[!UICONTROL Expirado]**.

1. No [!DNL Assets] selecione uma pasta e crie uma tarefa de revisão na pasta.

1. Revise e aprove/rejeite os ativos na tarefa de revisão e clique em **[!UICONTROL Concluído]**.

1. Navegue até a pasta para a qual você criou a tarefa de revisão. O status dos ativos aprovados/rejeitados é exibido na parte inferior da exibição de cartão. Na exibição em lista, os status de aprovação e expiração são exibidos nas colunas apropriadas.

1. Para pesquisar ativos com base em seus status, clique em **[!UICONTROL Pesquisar]** para exibir a barra de pesquisa.

1. Selecionar `Return` e clique em [!DNL Experience Manager].

1. No painel de pesquisa, clique em **[!UICONTROL Publicar status]** e selecione **[!UICONTROL Publicado]** para pesquisar ativos publicados em [!DNL Assets].

1. Para pesquisar ativos aprovados ou rejeitados, selecione **[!UICONTROL Status de aprovação]** e selecione a opção apropriada.

1. Para pesquisar ativos com base no status de expiração, selecione **[!UICONTROL Status de expiração]** no painel pesquisar e selecione a opção apropriada.

1. Também é possível pesquisar ativos com base em uma combinação de status em vários aspectos da pesquisa. Por exemplo, você pode pesquisar ativos publicados que sejam aprovados em uma tarefa de revisão e não estejam expirados. Para pesquisar esses ativos, selecione as opções apropriadas nos aspectos de pesquisa.

## Digital Rights Management em [!DNL Assets] {#digital-rights-management-in-assets-1}

A funcionalidade DRM impõe a aceitação do contrato de licença antes que você possa baixar um ativo licenciado do [!DNL Assets].

Se você selecionar um ativo protegido e clicar em **[!UICONTROL Baixar]**, você será redirecionado para uma página de licença para aceitar o contrato de licença. Se você não aceitar o contrato de licença, a variável **[!UICONTROL Baixar]** opção não está disponível.

Se a seleção contiver vários ativos protegidos, selecione um ativo de cada vez, aceite o contrato de licença e continue para baixar o ativo.

Um ativo é considerado protegido se qualquer uma destas condições for satisfeita:

* A propriedade de metadados do ativo `xmpRights:WebStatement` aponta para o caminho da página que contém o contrato de licença do ativo.
* O valor da propriedade de metadados do ativo `adobe_dam:restrictions` é um HTML bruto que especifica o contrato de licença.

>[!NOTE]
>
>A localização `/etc/dam/drm/licences` foi usado para armazenar licenças nas versões anteriores do [!DNL Experience Manager]. A localização está obsoleta agora. Se você criar ou modificar páginas de licença, ou portar as páginas do anterior [!DNL Experience Manager] versões, a Adobe recomenda que você armazene esses ativos em `/apps/settings/dam/drm/licenses` ou `/conf/*/settings/dam/drm/licenses` locais.

### Baixar ativos protegidos por DRM {#downloading-drm-assets}

1. Na exibição de cartão, selecione os ativos que deseja baixar e selecione **[!UICONTROL Baixar]**.
1. Na página **[!UICONTROL Gerenciamento de direitos autorais]**, selecione o ativo que deseja baixar na lista.
1. No [!UICONTROL Licença] escolha **[!UICONTROL Concordo]**. Uma marca de seleção aparece ao lado do ativo. Selecione o **[!UICONTROL Baixar]** opção.

   >[!NOTE]
   >
   >A variável **[!UICONTROL Baixar]** A opção é ativada somente quando você opta por concordar com o contrato de licença de um ativo protegido. No entanto, se sua seleção incluir ativos protegidos e desprotegidos, somente os ativos protegidos serão listados no painel e no **[!UICONTROL Baixar]** A opção está disponível para baixar os ativos desprotegidos. Para aceitar simultaneamente contratos de licença para vários ativos protegidos, selecione os ativos na lista e escolha **[!UICONTROL Concordar]**.

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
