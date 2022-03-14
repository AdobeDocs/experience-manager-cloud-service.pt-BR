---
title: Configurar o pipeline
description: Crie um pipeline de front-end para gerenciar a personalização do tema do seu site.
exl-id: 0d77d1a6-98f3-4961-9283-f52c1b5b2a7b
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# Configurar o pipeline {#set-up-your-pipeline}

Crie um pipeline de front-end para gerenciar a personalização do tema do seu site.

## A História Até Agora {#story-so-far}

No documento anterior da jornada de Criação AEM de Site Rápido, [Criar Site a partir de Modelo,](create-site.md) você aprendeu a usar um modelo de site para criar rapidamente um site de AEM que pode ser personalizado ainda mais com ferramentas de front-end e agora você deve:

* Saiba como obter modelos de site AEM.
* Saiba como criar um novo site usando um modelo.
* Veja como baixar o modelo do seu novo site para fornecer ao desenvolvedor de front-end.

Este artigo se baseia nesses fundamentos para que você possa configurar um pipeline front-end, que o desenvolvedor de front-end usará posteriormente na jornada para implantar personalizações de front-end.

## Objetivo {#objective}

Este documento ajuda você a entender os pipelines de front-end e criar um para gerenciar a implantação do tema personalizado do site. Depois de ler, você deve:

* Entenda o que é um pipeline front-end.
* Saiba como configurar um pipeline de front-end no Cloud Manager.

## Função responsável {#responsible-role}

Essa parte da jornada se aplica ao administrador do Cloud Manager.

## Requisitos {#requirements}

* Você precisa ter acesso ao Cloud Manager.
* Você precisa ser um membro do **Gerenciador de implantação** no Cloud Manager.
* Um repositório Git para o ambiente de AEM deve ser configurado no Cloud Manager.
   * Geralmente, isso já acontece em qualquer projeto ativo. No entanto, se não estiver, consulte a documentação dos Repositórios do Cloud Manager disponível na seção [Recursos adicionais](#additional-resources) seção.

## O que é um pipeline front-end {#front-end-pipeline}

O desenvolvimento front-end envolve a personalização de JavaScript, CSS e recursos estáticos que definem o estilo do site AEM. O desenvolvedor de front-end trabalhará em seus próprios ambientes locais para fazer essas personalizações. Quando estiverem prontas, as alterações serão confirmadas no repositório Git AEM. Mas eles só estão comprometidos com o código-fonte. Elas ainda não estão vivas.

O pipeline front-end leva essas personalizações confirmadas e as implanta em um ambiente AEM, geralmente em ambientes de produção ou não.

Dessa forma, o desenvolvimento de front-end pode funcionar separadamente e em paralelo a qualquer desenvolvimento de back-end de pilha completa no AEM, que tem seus próprios pipelines de implantação.

>[!NOTE]
>
>Os pipelines de front-end só podem implantar JavaScript, CSS e recursos estáticos para criar estilo ao site de AEM. O conteúdo do site, como páginas ou ativos, não pode ser implantado em um pipeline.

## Access Cloud Manager {#login}

1. Faça logon no Adobe Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. O Cloud Manager lista os vários programas disponíveis. Toque ou clique no que deseja gerenciar. Se você estiver apenas começando com AEM as a Cloud Service, você provavelmente terá apenas um programa disponível.

   ![Seleção de um programa no Cloud Manager](assets/cloud-manager-select-program.png)

Agora você verá uma visão geral do seu programa. Sua página será diferente, mas semelhante a este exemplo.

![Visão geral do Cloud Manager](assets/cloud-manager-overview.png)

Observe o nome do programa que você acessou ou copie o URL. Você precisará fornecer isso ao desenvolvedor front-end posteriormente.

## Criar um pipeline front-end {#create-front-end-pipeline}

Agora que você acessou o Cloud Manager, é possível criar um pipeline para implantação de front-end.

1. No **Pipelines** na página Cloud Manager , toque ou clique no botão **Adicionar** botão.

   ![Pipelines](assets/pipelines-add.png)

1. No menu pop-up exibido abaixo do **Adicionar** botão selecionar **Adicionar pipeline de não-produção** para efeitos desta jornada.

1. No **Configuração** da guia **Adicionar pipeline de não-produção** que é aberta:
   * Selecionar **Pipeline de implantação**.
   * Forneça um nome ao pipeline na **Nome do pipeline de não produção** campo.

   ![Adicionar configuração de pipeline](assets/add-pipeline-configuration.png)

1. Toque ou clique **Continuar**.

1. No **Código fonte** guia :
   * Selecionar **Código de front-end** como o tipo de código a ser implantado.
   * Verifique se o ambiente correto está selecionado em **Ambientes de implantação qualificados**.
   * Selecione as opções corretas **Repositório**.
   * Definir qual **Ramificação Git** o pipeline deve ser associado a .
   * Defina as **Localização do código** se o desenvolvimento de front-end estiver localizado em um caminho específico no repositório selecionado. O valor padrão é a raiz do repositório, mas com frequência o desenvolvimento de front-end e back-end estarão em caminhos diferentes.

   ![Informações do código-fonte para adicionar pipeline](assets/add-pipeline-source-code.png)

1. Toque ou clique **Salvar**.

O novo pipeline é criado e visível na variável **Pipelines** da janela do Cloud Manager. Tocar no clique nas reticências depois do nome do pipeline revela opções para editar ou exibir detalhes mais detalhadamente, conforme necessário.

![Opções de pipeline](assets/new-pipeline.png)

>[!TIP]
>
>Se você já estiver familiarizado com pipelines no AEMaaCS e quiser saber mais sobre as diferenças entre os diferentes tipos de pipelines, incluindo mais detalhes sobre o pipeline front-end, consulte Configurar pipeline de CI/CD - Cloud Services vinculados no [Recursos adicionais](#additional-resources) abaixo.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de Criação de Site Rápido de AEM, é necessário:

* Entenda o que é um pipeline front-end.
* Saiba como configurar um pipeline de front-end no Cloud Manager.

Crie com base nesse conhecimento e prossiga sua jornada de Criação de Site Rápido de AEM revisando o documento [Conceder acesso ao desenvolvedor de front-end,](grant-access.md) onde você integrará os desenvolvedores de front-end no Cloud Manager para que eles tenham acesso ao seu repositório e pipeline de git do site AEM.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de Criação Rápida de Site revisando o documento [Personalizar o Tema do Site,](customize-theme.md) a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada.

* [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Se quiser obter mais detalhes sobre os recursos do Cloud Manager, consulte diretamente os documentos técnicos detalhados.
* [Repositórios do Cloud Manager](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) - Se você precisar de mais informações sobre como configurar e gerenciar repositórios git para seu projeto AEMaaCS, consulte este documento.
* [Configurar pipeline de CI/CD - Cloud Services](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) - Saiba mais detalhes sobre a configuração de pipelines, tanto a pilha completa quanto o front-end, neste documento.
