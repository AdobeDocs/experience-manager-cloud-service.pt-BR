---
title: Adicionar pipeline de produção
description: Adicionar pipeline de produção
index: false
source-git-commit: 16e3280d7eaf53d8f944a60ec93b21c6676f0133
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---


# Criação de um pipeline de produção {#create-production-pipeline}

Depois de configurar seu programa e ter pelo menos um ambiente usando a interface do usuário do [!UICONTROL Cloud Manager], você estará pronto para configurar o pipeline de implantação.

Siga estas etapas para configurar o comportamento e as preferências do pipeline:

1. Clique em **Configurar pipeline** para configurar seu pipeline.

   ![](assets/set-up-pipeline1.png)

1. A tela **Configurar pipeline** é exibida. Selecione a ramificação e clique em **Next**.

   ![](assets/setup-1.png)

1. Configure suas opções de implantação.

   ![](assets/setup-pipeline.png)

   Você pode definir o acionador para iniciar o pipeline:

   * **Manual**  - uso da interface do usuário para iniciar manualmente o pipeline.
   * **Em alterações no Git**  - inicia o pipeline de CI/CD sempre que há confirmações adicionadas à ramificação git configurada. Mesmo que você selecione essa opção, sempre poderá iniciar o pipeline manualmente.

   Durante a configuração ou edição do pipeline, o Gerenciador de implantação tem a opção de definir o comportamento do pipeline quando uma falha importante for encontrada em qualquer uma das portas de qualidade.

   Isso é útil para clientes que desejam processos mais automatizados. As opções disponíveis são:

   * **Perguntar sempre**  - Essa é a configuração padrão e requer intervenção manual em qualquer falha importante.
   * **Cancelar imediatamente**  - se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que rejeita manualmente cada falha.
   * **Aprovar imediatamente**  - Se selecionado, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. Isso é basicamente emular um usuário que aprova manualmente cada falha.


1. As configurações de pipeline de produção incluem uma terceira guia rotulada como **Auditoria de experiência**. Essa opção fornece uma tabela para os caminhos de URL que devem ser sempre incluídos na Auditoria de experiência.

   >[!NOTE]
   >Você deve clicar em **Adicionar nova página** para definir seu próprio link personalizado.

   ![](assets/setup-3.png)

   Clique em **Adicionar nova página** para fornecer um caminho de URL a ser incluído na Auditoria de experiência.

   Por exemplo, se você deseja incluir `https://wknd.site/us/en/about-us.html` na Auditoria de experiência, insira o caminho `us/en/about-us.html` neste campo e clique em **Salvar**.

   ![](assets/exp-audit4.png)

   O URL que aparece na tabela será:

   `https://publish-p14253-e43686.adobeaemcloud.com/us/en/about-us.html`

   ![](assets/exp-audit5.png)

   É possível incluir no máximo 25 linhas. Se não houver páginas enviadas pelo usuário nesta seção, a página inicial do site será incluída na Auditoria de experiência por padrão.

   Consulte [Compreender os resultados da auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

   >[!NOTE]
   > As páginas configuradas serão enviadas ao serviço e avaliadas de acordo com os testes de desempenho, acessibilidade, SEO (Search Engine Otimization), prática recomendada e PWA (Progressive Web App).

1. Clique em **Salvar** na tela **Editar pipeline**. A página **Visão geral** agora exibe o cartão **Implantar seu programa**. Clique no botão **Implantar** para implantar seu programa.

   ![](assets/configure-pipeline5.png)

