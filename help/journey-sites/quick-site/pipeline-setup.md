---
title: Configurar o seu pipeline
description: Crie um pipeline de front-end para gerenciar a personalização do tema do seu site.
exl-id: 0d77d1a6-98f3-4961-9283-f52c1b5b2a7b
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
recommendations: noDisplay, noCatalog
source-git-commit: 8c4b34a77ef85869048fae254728c58cf0d99b66
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 79%

---


# Configurar o seu pipeline {#set-up-your-pipeline}

{{traditional-aem}}

Crie um pipeline de front-end para gerenciar a personalização do tema do seu site.

## A história até agora {#story-so-far}

No documento anterior da jornada de Criação rápida de sites do AEM, [Criar site a partir de modelo](create-site.md), você aprendeu a usar um modelo de site para criar rapidamente um site do AEM que pode ser personalizado ainda mais com ferramentas de front-end; agora, você deve:

* Entenda como obter modelos de site do AEM.
* Saiba como criar um site usando um modelo.
* Veja como baixar o modelo do seu novo site para fornecer ao desenvolvedor de front-end.

Este artigo desenvolve esses fundamentos para que você possa configurar um pipeline de front-end, que o desenvolvedor de front-end usará posteriormente na jornada para implantar personalizações de front-end.

## Objetivo {#objective}

Este documento ajuda você a entender os pipelines de front-end e como criar um para gerenciar a implantação do tema personalizado do site. Depois de ler esse documento, você deverá:

* Entender o que é um pipeline de front-end.
* Saber como configurar um pipeline de front-end no Cloud Manager.

## Função de responsabilidade {#responsible-role}

Essa parte da jornada se aplica ao administrador do Cloud Manager.

## Requisitos {#requirements}

* É necessário ter acesso ao Cloud Manager.
* É necessário ser um membro da função **Gerenciador de implantação** no Cloud Manager.
* Um repositório Git para o ambiente do AEM deve ser configurado no Cloud Manager.
   * Geralmente, isso já acontece em qualquer projeto ativo. No entanto, se não estiver, consulte a documentação dos repositórios do Cloud Manager, disponível na seção [Recursos adicionais](#additional-resources).

## O que é um pipeline de front-end {#front-end-pipeline}

O desenvolvimento de front-end envolve personalização de JavaScript, CSS e recursos estáticos que definem o estilo do site do AEM. O desenvolvedor de front-end trabalhará no ambiente local dele para fazer essas personalizações. Quando prontas, as alterações são confirmadas no repositório Git do AEM. Mas elas são confirmadas apenas para o código-fonte. Elas ainda não estão ativas.

O pipeline de front-end pega essas personalizações confirmadas e as implanta em um ambiente do AEM, geralmente em ambientes de produção ou não.

Dessa forma, o desenvolvimento de front-end pode funcionar separadamente e em paralelo a qualquer desenvolvimento de back-end de pilha completa no AEM, que tem seus próprios pipelines de implantação.

>[!NOTE]
>
>Os pipelines de front-end só podem implantar JavaScript, CSS e recursos estáticos para desenvolver o estilo do site do AEM. O conteúdo do site, como páginas ou ativos, não pode ser implantado em um pipeline.

## Acessar o Cloud Manager {#login}

1. Faça logon no Adobe Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. O Cloud Manager lista os vários programas disponíveis. Selecione aquele que deseja gerenciar. Se você estiver apenas começando no AEM as a Cloud Service, provavelmente terá apenas um programa disponível.

   ![Seleção de um programa no Cloud Manager](assets/cloud-manager-select-program.png)

Você está vendo uma visão geral do seu programa. Sua página será diferente, mas semelhante a este exemplo.

![Visão geral do Cloud Manager](assets/cloud-manager-overview.png)

Observe o nome do programa que você acessou ou copie o URL. Você precisa fornecê-lo ao desenvolvedor de front-end posteriormente.

## Criar um pipeline de front-end {#create-front-end-pipeline}

Agora que você acessou o Cloud Manager, é possível criar um pipeline para implantação de front-end.

1. Na seção **Pipelines** da página do Cloud Manager, selecione o botão **Adicionar**.

   ![Pipelines](assets/pipelines-add.png)

1. No menu pop-up exibido abaixo do botão **Adicionar**, selecione **Adicionar pipeline de não produção** para os fins desta jornada.

1. Na guia **Configuração** da caixa de diálogo **Adicionar pipeline de não produção** que é aberta:
   * Selecione **Pipeline de implantação**.
   * Forneça um nome ao pipeline no campo **Nome do pipeline de não produção**.

   ![Adicionar configuração de pipeline](assets/add-pipeline-configuration.png)

1. Selecione **Continuar**.

1. Na guia **Código-fonte**:
   * Selecione **Código de front-end** como o tipo de código a ser implantado.
   * Verifique se o ambiente correto está selecionado em **Ambientes de implantação qualificados**.
   * Selecione o **Repositório** correto.
   * Defina a qual **Ramificação Git** o pipeline deve ser associado.
   * Defina a **Localização do código** se o desenvolvimento de front-end estiver localizado em um caminho específico no repositório selecionado. O valor padrão é a raiz do repositório, mas muitas vezes o desenvolvimento do front-end e do back-end estão em caminhos diferentes.

   ![Informações do código-fonte para adicionar pipeline](assets/add-pipeline-source-code.png)

1. Selecione **Salvar**.

O novo pipeline é criado e fica visível na seção **Pipelines** da janela do Cloud Manager. Tocar ou clicar nas reticências depois do nome do pipeline revela opções para editar ou exibir mais detalhes, conforme necessário.

![Opções de pipeline](assets/new-pipeline.png)

>[!TIP]
>
>Caso já conheça sobre os pipelines no AEMaaCS e deseje saber mais sobre as diferenças entre os diferentes tipos de pipelines, incluindo mais detalhes sobre o pipeline de front-end, consulte Configurar pipeline de CI/CD - Cloud Services, na seção [Recursos adicionais](#additional-resources) abaixo.

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada de Criação rápida de sites do AEM, você deve:

* Entender o que é um pipeline de front-end.
* Saber como configurar um pipeline de front-end no Cloud Manager.

Desenvolva esse conhecimento e prossiga com sua jornada de Criação rápida de sites do AEM, revisando a seguir o documento [Conceder acesso ao desenvolvedor de front-end](grant-access.md), onde você integrará os desenvolvedores de front-end no Cloud Manager para que eles tenham acesso ao seu repositório e pipeline de Git do site do AEM.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de Criação Rápida de Sites revisando o documento [Personalizar o Tema do Site](customize-theme.md), os recursos opcionais a seguir fornecerão uma melhor explicação dos conceitos mencionados neste documento. Porém, eles não são obrigatórios para continuar na jornada.

* [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=pt_BR) - Se quiser obter mais detalhes sobre os recursos do Cloud Manager, consulte diretamente os documentos técnicos detalhados.
* [Repositórios do Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md): se precisar de mais informações sobre como configurar e gerenciar repositórios Git para seu projeto do AEMaaCS, consulte este documento.
* [Configurar pipeline de CI/CD - Cloud Services](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md): consulte este documento para saber mais detalhes sobre a configuração de pipelines, tanto de pilha completa quanto de front-end.
