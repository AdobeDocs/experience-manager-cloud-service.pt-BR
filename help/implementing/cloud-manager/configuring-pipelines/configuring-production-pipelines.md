---
title: Configuração de pipeline de produção
description: Configuração de pipeline de produção
index: false
source-git-commit: 76cff84003576cf23eb1d23674ce6eaf082bbbb1
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# Configuração de um pipeline de produção {#configure-production-pipeline}

O Gerenciador de implantação é responsável pela configuração do pipeline de produção.

>[!NOTE]
>Um Pipeline de produção não pode ser configurado até que a criação de um programa seja concluída, o repositório Git tenha pelo menos uma ramificação e um conjunto de ambientes de Produção e Estágio seja criado.

Antes de começar a implantar seu código, você deve definir as configurações de pipeline do [!UICONTROL Cloud Manager].

>[!NOTE]
>Você pode alterar as configurações do pipeline após a configuração inicial.

## Adicionar um novo pipeline de produção {#adding-production-pipeline}

Depois de configurar seu programa e ter pelo menos um ambiente usando [!UICONTROL Cloud Manager] Interface do usuário do , você está pronto para adicionar um pipeline de produção.

Siga estas etapas para configurar o comportamento e as preferências do pipeline de produção:

1. Navegue até o **Pipelines** do cartão **Visão geral do programa** página.
Clique em **+Adicionar** e selecione **Adicionar pipeline de produção**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **Adicionar pipeline de produção** será exibida. Insira o nome do pipeline.

   Além disso, também é possível configurar **Acionador da implantação** e **Comportamento de falhas importantes da métrica** from **Opções de implantação**. Clique em **Continuar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   Você pode definir os acionadores de implantação para iniciar o pipeline.

   * **Manual** - uso da interface do usuário para iniciar manualmente o pipeline.
   * **Nas alterações no Git** - inicia o pipeline de CI/CD sempre que há confirmações adicionadas à ramificação git configurada. Mesmo que você selecione essa opção, sempre poderá iniciar o pipeline manualmente.

      Durante a configuração ou edição do pipeline, o Gerenciador de implantação tem a opção de definir o comportamento do pipeline quando uma falha importante for encontrada em qualquer uma das portas de qualidade.

      Isso é útil para clientes que desejam processos mais automatizados. As opções disponíveis são:
   Você pode definir o comportamento importante das métricas de falha para iniciar o pipeline.

   * **Perguntar sempre** - Esta é a configuração padrão e requer intervenção manual em qualquer falha importante.
   * **Falhar imediatamente** - Se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que rejeita manualmente cada falha.
   * **Continuar imediatamente** - Se selecionado, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que aprova manualmente cada falha.


1. O **Adicionar pipeline de produção** caixa de diálogo inclui uma segunda guia rotulada como **Código fonte**. **Código de pilha completo** está selecionada. Você pode escolher a variável **Repositório** e **Ramificação Git**. Selecione as Opções de implantação de produção, conforme explicado abaixo. Clique em **Continuar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   Opções de implantação de produção:

   * **Pausar antes de implantar na produção**: Essa opção permite a interrupção da implantação antes da produção.
   * **Programado**: Essa opção permite que o usuário habilite a implantação de produção agendada.

1. O **Adicionar pipeline de produção** caixa de diálogo inclui uma terceira guia rotulada como **Auditoria de experiência**. Essa opção fornece uma tabela para os caminhos de URL que devem ser sempre incluídos na Auditoria de experiência.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >Você deve clicar em **Adicionar página** para definir seu próprio link personalizado. O caminho da página deve começar com `/`.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit2.png)


   Clique em **Adicionar nova página** para fornecer um caminho de URL a ser incluído na Auditoria de experiência.

   Por exemplo, se você deseja incluir `https://wknd.site/us/en/about-us.html` na Auditoria de experiência, insira o caminho `/us/en/about-us.html` neste campo e clique em **Salvar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

   O URL que aparece na tabela será:

   `https://publish-p12361-e112003.adobeaemcloud.com/us/en/about-us.html`

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

   É possível incluir no máximo 25 linhas. Se não houver páginas enviadas pelo usuário nesta seção, a página inicial do site será incluída na Auditoria de experiência por padrão.

   Consulte [Noções básicas dos resultados da auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

   >[!NOTE]
   > As páginas configuradas serão enviadas ao serviço e avaliadas de acordo com os testes de desempenho, acessibilidade, SEO (Search Engine Otimization), prática recomendada e PWA (Progressive Web App).

1. Clique em **Salvar**. O pipeline de produção recém-criado agora é exibido na variável **Pipelines** cartão.

   O pipeline é mostrado no cartão na tela inicial com três ações, conforme mostrado abaixo:

   * **Adicionar** - permite adicionar um novo pipeline.
   * **Acessar informações do repositório** - permite que o usuário obtenha as informações necessárias para acessar o repositório Git do Cloud Manager.
   * **Saiba mais** - navega para entender o recurso de documentação do pipeline de CI/CD.




