---
title: Migration Utility para converter Forms adaptável baseado em componentes de base em formulários baseados em componentes principais
description: Saiba como instalar e usar o Migration Utility para converter o Adaptive Forms com base em componentes de base em formulários baseados em componentes principais.
Keywords: Migration Utility tool, Convert Adaptive Forms based on foundation components to core component based forms, Convert Foundation forms to Core components forms, Using Modernizer tool to convert Foundation Components to Core components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
source-git-commit: 494e90bd5822495f0619e8ebf55f373a26a3ffe6
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 1%

---


# Introdução

Você pode usar o utilitário de migração para converter o Adaptive Forms com base em componentes de base em formulários com base em componentes principais. Você pode usar o [Ferramenta Modernizar AEM](https://opensource.adobe.com/aem-modernize-tools/) como uma ferramenta de utilitário de migração. A variável [AEM Modernizar ferramentas](https://opensource.adobe.com/aem-modernize-tools/) forneça um conjunto de utilitários usados para converter o Adaptive Forms com base em componentes básicos para os recursos modernos e compatíveis dos componentes principais.

## O que são as ferramentas de modernização do AEM?

[AEM Modernizar ferramentas](https://opensource.adobe.com/aem-modernize-tools/) refere-se a um conjunto de utilitários ou aplicativos de software projetados para facilitar o processo de modernização ou atualização de projetos do Adobe Experience Manager (AEM). Normalmente, essas ferramentas ajudam a converter componentes ou funcionalidades mais antigos do AEM em alternativas mais recentes, eficientes e compatíveis.

As Ferramentas de modernização do AEM convertem o Forms adaptável, que é baseado em componentes de base mais antigos, em formulários principais mais recentes baseados em componentes. Esse processo de conversão garante que os formulários estejam alinhados a padrões e recursos modernos, melhorando potencialmente o desempenho, a compatibilidade e a facilidade de manutenção no ambiente do AEM.

![Ferramentas de Modernização de AEM](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
> É recomendável instalar as Ferramentas de modernização do AEM na configuração local do AEM. Migre os formulários com base em base para formulários com base em componentes principais. Baixe o formulário com seus ativos. Em seguida, carregue o formulário e seus ativos no ambiente necessário.

## Pré-requisitos para usar as ferramentas de modernização do AEM

* [Configurar ambiente de desenvolvimento local para o AEM Forms](/help/forms/setup-local-development-environment.md)
* [Ativar os componentes principais adaptáveis do Forms para o seu ambiente.](/help/forms/enable-adaptive-forms-core-components.md)

* Adicione usuários à [!DNL forms-users] grupo. Os membros da [!DNL forms-users] grupo tem permissões para criar um Formulário adaptável.

* Usuários com as seguintes funções têm as permissões para instalar as ferramentas de modernização do AEM em um ambiente AEM:
   * Função de desenvolvedor
   * Função de administrador Para obter uma lista detalhada de grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

## Instalar e configurar ferramentas de Modernização do AEM

Etapas para instalar e configurar as ferramentas de Modernização do AEM:

1. [Instalar ferramentas de Modernização do AEM no ambiente local do AEM Forms](#install-aem-modernize-tools)
2. [Ativar ferramentas de Modernização do AEM para o ambiente local do AEM Forms](#enable-aem-modernize-tools)

### Instalar ferramentas de Modernização do AEM no ambiente local do AEM Forms {#install-aem-modernize-tools}

Execute as seguintes etapas para instalar as Ferramentas de modernização do AEM no ambiente local do AEM Forms:

1. Inicie o serviço de autor local do AEM executando o seguinte na linha de comando:

   `java -jar aem-author-p4502.jar`

   >[!NOTE]
   >
   > Forneça a senha do administrador como `admin`. Qualquer senha de administrador é aceitável, no entanto, é recomendável usar o padrão para desenvolvimento local para reduzir a necessidade de reconfigurar.

1. Clonar o [Ferramentas de Modernização de AEM](https://git.corp.adobe.com/livecycle/forms-modernizer/tree/convertForms) repositório no seu sistema local.

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tools]
   ```
   Substitua o [Caminho do repositório Git de ferramentas de modernização do AEM] com o URL real do Repositório Git correspondente das Ferramentas de modernização do AEM.
Depois de executar o comando com êxito, você terá uma cópia local do repositório de Ferramentas de Modernização AEM disponível em sua máquina.

1. Navegue até a`[AEM Modernize Tools Repository]`  em seu sistema local.
1. Execute o seguinte comando:

   ```Shell
       mvn clean install 
   ```
![Imagem de instalação bem-sucedida](/help/forms/assets/aem-modernize-install-steps.png)

Após a instalação bem-sucedida, as Ferramentas de modernização do AEM ficam disponíveis para o seu ambiente.

![Ativar ferramentas de modernização do AEM](/help/forms/assets/enable-aem-modernizer-tools.png)


### Ativar ferramentas de Modernização do AEM para o ambiente local do AEM Forms{#enable-aem-modernize-tools}

Para ativar e usar as Ferramentas de modernização do AEM para o seu ambiente AEM, é importante mapear as regras para migrar componentes de base para os componentes principais:

1. Faça logon na instância do autor.
1. Navegue até `http://[host]:[port]/system/console/configMgr`
1. Localize e edite o `AEM Modernize Tools - Component Rewrite Rule Service`.
1. Adicione o `Component Rule Paths` as `/apps/forms-modernizer/rules`.
1. Clique em **Salvar** para salvar as alterações.

![Regra do componente de Modernização do AEM](/help/forms/assets/aem-modernize-tools-component-rule.png)

## Execute ferramentas de Modernização de AEM para converter formulários baseados em componentes de base em formulários baseados em componentes principais

1. Ir para **[!UICONTROL Ferramentas > Ferramentas de Modernização do AEM > Conversão do Forms]**.

   ![Selecionar ferramentas de Modernização de AEM](/help/forms/assets/aem-modernize-tools-select.png)

1. Selecione o **[!UICONTROL Conversão do Forms]** opção.

   ![Selecionar a opção Conversão do Forms](/help/forms/assets/aem-modernize-forms-conversion.png)

1. Clique em **Criar** para criar um novo trabalho.

   ![AEM Modernizar ferramentas Criar trabalho](/help/forms/assets/aem-modernize-tools-create-job.png)

1. Especifique a **[!UICONTROL Nome da tarefa]**.
1. No **[!UICONTROL Formulário]** é possível selecionar uma das seguintes opções:
   * **Nenhum** : selecione essa opção se o manuseio de formulário não for necessário.
   * **Restaurar** : selecione esta opção para restaurar o formulário ao estado anterior à última conversão.
   * **Copiar para o Target**: selecione essa opção para copiar o formulário antes de executar a conversão.
No nosso caso, o **Copiar para o Target** for selecionada. Se a variável **Copiar para o Target** for selecionada, a variável **[!UICONTROL Caminho de origem]** e **[!UICONTROL Caminho de destino]** se tornarem visíveis.

1. Especifique a `source folder` nome no campo **[!UICONTROL Caminho de origem]**.
1. Especifique a `target folder` nome no campo **[!UICONTROL Caminho de destino]**.
1. Selecione **[!UICONTROL Próximo]**.
1. Clique em **[!UICONTROL Adicionar o Forms]**. Todos os formulários no `source folder` é exibida na tela.
1. Selecione o formulário com base nos componentes de base para convertê-lo em formulário com base nos componentes principais. Também é possível selecionar vários formulários.

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

Agora é possível ver que o Formulário adaptável criado em componentes de base se transforma no Formulário adaptável criado em componentes principais.

## Considerações ao usar a ferramenta Utilitário de migração {#considerations}

* Se o formulário criado nos componentes de base contiver regras de função personalizadas, será necessário regravar essas regras para o formulário convertido com base nos componentes principais.
* O formulário convertido não inclui regras no editor de regras, exigindo a reescrita de regras para o formulário convertido.
* Você precisa recriar o trabalho de tradução para o formulário convertido.

## Práticas recomendadas {#best-practices}

* O formulário criado nos componentes de base inclui apenas os componentes encontrados nos componentes principais baseados em componentes.
* Verifique se as regras estão formatadas em XML.


