---
title: Ferramenta do Migration Utility/AEM Modernizar ferramentas para converter Forms adaptável baseado em componentes básicos em formulários baseados em Componentes principais
description: Saiba como instalar e usar o Migration Utility/AEM Modernizar ferramentas para converter Forms adaptável com base em componentes de base em formulários baseados em componentes principais.
Keywords: Migration Utility Tool, Convert Adaptive Forms based on Foundation Components to Core Component based forms, Convert Foundation forms to Core Components forms, Using Modernizer Tool to convert Foundation Components to Core Components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
exl-id: ee71a576-96a7-4c81-b3a3-1d678f010cba
feature: Adaptive Forms, Core Components
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 5%

---

# Introdução

<span class="preview"> O recurso está disponível no programa de adoção antecipada. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

O Utilitário de conversão do Forms, parte do conjunto da [Ferramenta de modernização do AEM](https://opensource.adobe.com/aem-modernize-tools/), ajuda a converter facilmente o Adaptive Forms criado com componentes fundamentais herdados em formulários que aproveitam os recursos modernos e compatíveis dos Componentes principais.

## O que são as Ferramentas de modernização do AEM?

[Ferramentas de Modernização do AEM](https://opensource.adobe.com/aem-modernize-tools/) refere-se a um conjunto de utilitários ou aplicativos de software criados para facilitar o processo de modernização ou atualização de projetos do Adobe Experience Manager (AEM). Normalmente, essas Ferramentas ajudam a converter componentes ou funcionalidades mais antigos no AEM em alternativas mais recentes, eficientes e compatíveis. O Utilitário de conversão do Forms é instalado em Ferramentas de modernização do AEM para converter Forms adaptável com base em Componentes de base em formulários baseados em Componentes principais.

O Utilitário de conversão do Forms converte o Forms adaptável, que é baseado em Componentes de base mais antigos, em formulários mais recentes baseados em Componentes principais. Esse processo de conversão garante que os formulários estejam alinhados a padrões e recursos modernos, melhorando potencialmente o desempenho, a compatibilidade e a facilidade de manutenção no ambiente do AEM.

![Ferramentas de Modernização do AEM](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
>É recomendável instalar as Ferramentas de modernização do AEM na configuração local do AEM. Migre o Forms adaptável baseado em Componentes de base para formulários baseados em Componentes principais. Baixe o formulário com seus ativos. Em seguida, carregue o formulário e seus ativos no ambiente necessário.

## Considerações ao usar as ferramentas de Modernização do AEM {#considerations}

* Nas conversões bem-sucedidas, todas as regras aplicadas ao formulário são removidas. As regras não são migradas automaticamente. Você deve recriar manualmente e aplicar essas regras ao formulário convertido.
* As configurações de tradução usadas no formulário original não são transferidas. Reconfigure a tradução para o formulário convertido.
* Se o formulário criado nos Componentes de base contiver scripts ou regras de função personalizadas, é necessário regravá-los para o formulário convertido com base nos Componentes principais.
* Os seguintes componentes de base OOTB ainda não são compatíveis com os Componentes principais e, portanto, são excluídos no formulário convertido:

   * Bloco do Adobe Sign
   * Gráfico
   * Listagem de anexos de arquivo
   * Espaço reservado para nota de rodapé
   * Opção de imagem
   * Botão Próximo
   * Botão Anterior
   * Rabiscar a assinatura
   * Etapa de resumo
   * Barra de ferramentas

## Pré-requisitos para usar as ferramentas de Modernização do AEM

* [Configurar o ambiente de desenvolvimento local para o AEM Forms](/help/forms/setup-local-development-environment.md).
* Instale os componentes principais adaptáveis do Forms mais recentes até o momento para ativar o ambiente do AEM Cloud Service.
* Adicione usuários ao grupo [!DNL forms-users]. Os membros do grupo [!DNL forms-users] têm permissões para criar um Formulário adaptável.
* Os usuários com as seguintes funções têm permissões para instalar as Ferramentas de modernização do AEM em um ambiente do AEM:

   * Função de desenvolvedor
   * Função de administrador

Para obter uma lista detalhada de grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

## Instalar e configurar as Ferramentas de modernização do AEM

Para instalar e configurar as Ferramentas de modernização do AEM:

1. [Instalar as Ferramentas de modernização do AEM no ambiente local do AEM Forms](#install-aem-modernize-Tools)
1. [Ativar as Ferramentas de modernização do AEM para o ambiente local do AEM Forms](#enable-aem-modernize-Tools)

### Instalar as Ferramentas de modernização do AEM no ambiente local do AEM Forms {#install-aem-modernize-Tools}

Execute as seguintes etapas para instalar as Ferramentas de modernização do AEM no ambiente local do AEM Forms:

1. Abra o prompt de comando ou o terminal.
1. Inicie o Serviço de autor do AEM local. Por exemplo, execute o seguinte código do para iniciar a instância local do AEM Author:

   `java -jar aem-author-p4502.jar`

1. Clonar o repositório da [Ferramenta de Modernização do AEM](https://github.com/adobe/forms-modernizer) no sistema local.

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tool]
   ```

   Depois de executar o comando com êxito, você terá uma cópia local do repositório da Ferramenta de modernização do AEM disponível em sua máquina.

1. Navegue até `[AEM Modernize Tool Repository]` em seu sistema local.
1. Execute o seguinte comando:

   ```Shell
       mvn clean install 
   ```

![Imagem de instalação bem-sucedida](/help/forms/assets/aem-modernize-install-steps.png)

Após a instalação bem-sucedida, as Ferramentas de modernização do AEM ficam disponíveis para o seu ambiente.

![Habilitar a Ferramenta do Utilitário de Migração do AEM](/help/forms/assets/enable-aem-modernizer-tools.png)


### Ativar as Ferramentas de modernização do AEM para o ambiente local do AEM Forms{#enable-aem-modernize-Tools}

Para ativar e usar as Ferramentas de modernização do AEM para o seu ambiente do AEM, é importante mapear as regras para migrar Componentes de base para Componentes principais:

1. Faça logon na instância do autor.
1. Navegue até `http://[host]:[port]/system/console/configMgr`
1. Localize e edite o `AEM Modernize Tools - Component Rewrite Rule Service`.
1. Adicione o `Component Rule Paths` como `/apps/forms-modernizer/rules`.
1. Clique em **Salvar** para salvar as alterações.

![Regra do componente de Modernização do AEM](/help/forms/assets/aem-modernize-tools-component-rule.png)

## Execute o utilitário de Conversão de Formulário para converter formulários baseados em Componentes de Base em formulários baseados em Componentes Principais

1. Acesse **[!UICONTROL Ferramentas > Ferramentas de Modernização do AEM > Conversão do Forms]**.

   ![Selecionar ferramentas de Modernização do AEM](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Selecione a opção **[!UICONTROL Conversão do Forms]**.

   ![Selecionar opção de Conversão do Forms](/help/forms/assets/aem-modernize-forms-conversion.png)

1. Clique em **Criar** para criar um novo trabalho.

   ![Ferramentas de Modernização do AEM para Criar Trabalho](/help/forms/assets/aem-modernize-tools-create-job.png)

1. Especifique o **[!UICONTROL Nome do Trabalho]**.
1. Na guia **[!UICONTROL Formulário]**, você pode selecionar uma das seguintes opções:

   * **Nenhum** : selecione a opção se não quiser criar uma cópia dos formulários baseados no Componente de Fundação antes de iniciar a conversão do formulário.
   * **Restaurar** : selecione a opção para restaurar o formulário ao estado em que estava antes de iniciar a conversão do formulário.
   * **Copiar para Destino**: selecione a opção para criar uma cópia dos formulários baseados no Componente de Base antes de iniciar a conversão do formulário.

   No nosso caso, a opção **Copiar para Destino** está selecionada. Se a opção **Copiar para o Destino** estiver selecionada, as opções **[!UICONTROL Caminho do Source]** e **[!UICONTROL Caminho do Destino]** ficarão visíveis.

1. Especifique o nome `source folder` no **[!UICONTROL Caminho do Source]**.
1. Especifique o nome `target folder` no **[!UICONTROL Caminho de Destino]**.
1. Selecione **[!UICONTROL Próximo]**.
1. Clique em **[!UICONTROL Adicionar Forms]**. Todos os formulários no `source folder` aparecem na tela.
1. Selecione o Forms adaptável com base em Componentes de base para convertê-lo em formulários baseados em Componentes principais. Também é possível selecionar vários formulários.

   ![Ferramentas de Modernização do AEM - Selecionar Formulário](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Clique em **[!UICONTROL Selecionar]**.
1. Clique em **[!UICONTROL Agendar trabalho]** para iniciar o processo de conversão.
1. Clique em **[!UICONTROL Converter]** na caixa de diálogo **[!UICONTROL Converter páginas]**.

   ![Ferramentas de Modernização do AEM Converter Páginas](/help/forms/assets/aem-modernize-tools-convert-form.png)

   Quando o status do processo for alterado para `success`. Navegue até `target folder` para ver o formulário convertido.

   ![Êxito na Modernização de Ferramentas do AEM](/help/forms/assets/aem-modernize-tools-success.png)

1. Selecione o Formulário adaptável e selecione > **[!UICONTROL Propriedades]**. A página Propriedades do formulário será aberta.

   ![Pasta de Destino de Ferramentas de Modernização do AEM](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. Selecione **[!UICONTROL Salvar e Fechar]** para salvar novamente as propriedades do formulário convertido.
   ![Propriedades do formulário adaptável das ferramentas de Modernização do AEM](/help/forms/assets/aem-modernize-tools-af-properties.png)

Agora é possível ver que o Formulário adaptável incorporado aos Componentes de base se transforma no Formulário adaptável incorporado aos Componentes principais.

## Práticas recomendadas {#best-practices}

* Certifique-se de que os formulários baseados em Componentes de Base usem apenas os componentes que tenham um [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type) equivalente disponível. Nos casos em que você usa Componentes de base que não têm um Componente principal equivalente, o Componente de base não é convertido. Como resultado, não funciona corretamente ao criar um formulário
* Verifique se as regras para converter os Componentes de base em Componentes principais estão formatadas em XML.
