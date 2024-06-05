---
title: Ferramentas do Migration Utility/AEM Modernizar ferramentas para converter Forms adaptável baseado em componentes de base em formulários baseados em componentes principais
description: Saiba como instalar e usar o Utilitário de migração/AEM Modernizar ferramentas para converter Forms adaptável com base em Componentes de base em formulários do Componente principal.
Keywords: Migration Utility Tool, Convert Adaptive Forms based on Foundation Components to Core Component based forms, Convert Foundation forms to Core Components forms, Using Modernizer Tool to convert Foundation Components to Core Components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
source-git-commit: cc1f3e2f0ddaed67de541c730c0b97f68c1e0d02
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---


# Introdução

O Utilitário de conversão do Forms, parte de [Ferramenta de Modernização de AEM](https://opensource.adobe.com/aem-modernize-Tools/) ajuda a converter facilmente o Forms adaptável criado com componentes fundamentais herdados em formulários que aproveitam os recursos modernos e compatíveis dos Componentes principais.

## O que são as ferramentas de modernização do AEM?

[Ferramentas de Modernização de AEM](https://opensource.adobe.com/aem-modernize-Tools/) refere-se a um conjunto de utilitários ou aplicativos de software projetados para facilitar o processo de modernização ou atualização de projetos do Adobe Experience Manager (AEM). Normalmente, essas ferramentas ajudam a converter componentes ou funcionalidades mais antigos do AEM em alternativas mais recentes, eficientes e compatíveis. O Utilitário de conversão do Forms é instalado em AEM Modernizar ferramentas para converter Forms adaptável com base em Componentes de base em formulários baseados em Componentes principais.

O Utilitário de conversão do Forms converte o Forms adaptável, que é baseado em Componentes de base mais antigos, em formulários mais recentes baseados em Componentes principais. Esse processo de conversão garante que os formulários estejam alinhados a padrões e recursos modernos, melhorando potencialmente o desempenho, a compatibilidade e a facilidade de manutenção no ambiente do AEM.

![Ferramentas de Modernização de AEM](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
> É recomendável instalar as Ferramentas de modernização do AEM na configuração local do AEM. Migre o Forms adaptável baseado em Componentes de base para formulários baseados em Componentes principais. Baixe o formulário com seus ativos. Em seguida, carregue o formulário e seus ativos no ambiente necessário.

## Considerações ao usar as ferramentas de modernização do AEM {#considerations}

* Nas conversões bem-sucedidas, todas as regras aplicadas ao formulário são removidas. As regras não são migradas automaticamente. Você deve recriar manualmente e aplicar essas regras ao formulário convertido.
* As configurações de tradução usadas no formulário original não são transferidas. Reconfigure a tradução para o formulário convertido.
  <!-- * If the form built on Foundation Components contains custom function rules, you have to rewrite these rules for the converted form based on Core Components.-->

## Pré-requisitos para usar as ferramentas de modernização do AEM

* [Configurar ambiente de desenvolvimento local para o AEM Forms](/help/forms/setup-local-development-environment.md)
* [Ative os Componentes principais adaptáveis do Forms para seu ambiente.](/help/forms/enable-adaptive-forms-core-components.md)

* Adicione usuários à [!DNL forms-users] grupo. Os membros da [!DNL forms-users] grupo tem permissões para criar um Formulário adaptável.

* Usuários com as seguintes funções têm as permissões para instalar as ferramentas de modernização do AEM em um ambiente AEM:
   * Função de desenvolvedor
   * Função de administrador

Para obter uma lista detalhada de grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

## Instalar e configurar ferramentas de Modernização do AEM

Para instalar e configurar as Ferramentas de modernização do AEM:

1. [Instalar ferramentas de Modernização do AEM no ambiente local do AEM Forms](#install-aem-modernize-Tools)
2. [Ativar ferramentas de Modernização do AEM para o ambiente local do AEM Forms](#enable-aem-modernize-Tools)

### Instalar ferramentas de Modernização do AEM no ambiente local do AEM Forms {#install-aem-modernize-Tools}

Execute as seguintes etapas para instalar as Ferramentas de modernização do AEM no ambiente local do AEM Forms:

1. Abra o prompt de comando ou o terminal.
1. Inicie o serviço de autor local do AEM. Por exemplo, execute o seguinte código do para iniciar a instância local do autor do AEM:

   `java -jar aem-author-p4502.jar`

1. Clonar o [Ferramenta de Modernização de AEM](https://git.corp.adobe.com/livecycle/forms-modernizer/tree/convertForms) repositório no seu sistema local.

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tool]
   ```

   Depois de executar o comando com êxito, você terá uma cópia local do repositório da ferramenta Modernizar AEM disponível em sua máquina.

1. Navegue até a`[AEM Modernize Tool Repository]`  em seu sistema local.
1. Execute o seguinte comando:

   ```Shell
       mvn clean install 
   ```
![Imagem de instalação bem-sucedida](/help/forms/assets/aem-modernize-install-steps.png)

Após a instalação bem-sucedida, as Ferramentas de modernização do AEM ficam disponíveis para o seu ambiente.

![Habilitar a ferramenta Utilitário de Migração AEM](/help/forms/assets/enable-aem-modernizer-tools.png)


### Ativar ferramentas de Modernização do AEM para o ambiente local do AEM Forms{#enable-aem-modernize-Tools}

Para ativar e usar as Ferramentas de modernização do AEM para o seu ambiente AEM, é importante mapear as regras para migrar Componentes de base para Componentes principais:

1. Faça logon na instância do autor.
1. Navegue até `http://[host]:[port]/system/console/configMgr`
1. Localize e edite o `AEM Modernize Tools - Component Rewrite Rule Service`.
1. Adicione o `Component Rule Paths` as `/apps/forms-modernizer/rules`.
1. Clique em **Salvar** para salvar as alterações.

![Regra do componente de Modernização do AEM](/help/forms/assets/aem-modernize-tools-component-rule.png)

## Execute o utilitário de conversão de formulários para converter formulários baseados em Componentes de base em formulários baseados em Componentes principais

1. Ir para **[!UICONTROL Ferramentas > Ferramentas de Modernização do AEM > Conversão do Forms]**.

   ![Selecione Ferramentas de Modernização de AEM](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Selecione o **[!UICONTROL Conversão do Forms]** opção.

   ![Selecionar a opção Conversão do Forms](/help/forms/assets/aem-modernize-forms-conversion.png)

1. Clique em **Criar** para criar um novo trabalho.

   ![AEM Modernizar ferramentas Criar trabalho](/help/forms/assets/aem-modernize-tools-create-job.png)

1. Especifique a **[!UICONTROL Nome da tarefa]**.
1. No **[!UICONTROL Formulário]** é possível selecionar uma das seguintes opções:
   * **Nenhum** : selecione a opção se não quiser criar uma cópia dos formulários baseados no Componente de base antes de iniciar a conversão do formulário.
   * **Restaurar** : selecione a opção para restaurar o formulário ao estado em que estava antes de iniciar a conversão do formulário.
   * **Copiar para o Target**: selecione a opção para criar uma cópia dos formulários baseados no Componente de base antes de iniciar a conversão do formulário.
No nosso caso, o **Copiar para o Target** for selecionada. Se a variável **Copiar para o Target** for selecionada, a variável **[!UICONTROL Caminho de origem]** e **[!UICONTROL Caminho de destino]** se tornarem visíveis.

1. Especifique a `source folder` nome no campo **[!UICONTROL Caminho de origem]**.
1. Especifique a `target folder` nome no campo **[!UICONTROL Caminho de destino]**.
1. Selecione **[!UICONTROL Próximo]**.
1. Clique em **[!UICONTROL Adicionar o Forms]**. Todos os formulários no `source folder` é exibida na tela.
1. Selecione o Forms adaptável com base em Componentes de base para convertê-lo em formulários baseados em Componentes principais. Também é possível selecionar vários formulários.

   ![AEM Modernizar ferramentas Selecionar formulário](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Clique em **[!UICONTROL Selecionar]**.
1. Clique em **[!UICONTROL Programar tarefa]** para iniciar o processo de conversão.
1. Clique em **[!UICONTROL Converter]** do **[!UICONTROL Converter páginas]** caixa de diálogo.

   ![AEM Modernizar ferramentas Converter páginas](/help/forms/assets/aem-modernize-tools-convert-form.png)

   Quando o status do processo é alterado para `success`. Navegue até a `target folder` para ver o formulário convertido.

   ![AEM Modernizar o sucesso das ferramentas](/help/forms/assets/aem-modernize-tools-success.png)

1. Selecione o formulário adaptável e selecione > **[!UICONTROL Propriedades]**. A página Propriedades do formulário será aberta.
   ![Pasta de destino das ferramentas de Modernização do AEM](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. Selecionar **[!UICONTROL Salvar e fechar]** para salvar as propriedades do formulário convertido novamente.
   ![Propriedades do formulário adaptável de ferramentas de Modernização de AEM](/help/forms/assets/aem-modernize-tools-af-properties.png)

Agora é possível ver que o Formulário adaptável incorporado aos Componentes de base se transforma no Formulário adaptável incorporado aos Componentes principais.

## Práticas recomendadas {#best-practices}

* Certifique-se de que os formulários baseados nos Componentes de base usem apenas os componentes que tenham um [Componentes principais](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type) disponíveis. Nos casos em que você usa Componentes de base que não têm um Componente principal equivalente, o Componente de base não é convertido. Como resultado, não funciona corretamente ao criar um formulário
* Verifique se as regras para converter os Componentes de base em Componentes principais estão formatadas em XML.



