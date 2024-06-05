---
title: Gerenciar seus sites de demonstração
description: Saiba mais sobre as ferramentas disponíveis para ajudá-lo a gerenciar seus sites de demonstração e como removê-los.
exl-id: 988c6e09-c43e-415f-8d61-998c294c5a11
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 89%

---

# Gerenciar seus sites de demonstração {#manage-demo-sites}

Saiba mais sobre as ferramentas disponíveis para ajudá-lo a gerenciar seus sites de demonstração e como removê-los.

## A história até agora {#story-so-far}

No documento anterior da jornada do complemento Demonstrações de Referência do AEM, [Criar Site,](create-site.md) você criou um novo site de demonstração com base nos modelos do Complemento de demonstração de referência. Agora você deve:

* Entender como acessar o ambiente de criação do AEM.
* Saber como criar um site com base em um modelo.
* Entender as noções básicas de navegação na estrutura do site e edição de uma página.

Se você também [habilitou o AEM Screens para o site de demonstração,](screens.md)é preciso:

* Ter noções básicas do AEM Screens.
* Entender o conteúdo de demonstração da We.Cafe.
* Saber como configurar o AEM Screens para a We.Cafe.

Agora que você tem seu próprio site de demonstração para explorar, este artigo descreve as ferramentas disponíveis para ajudá-lo a gerenciar seus sites de demonstração e como removê-los.

## Objetivo {#objective}

Este documento ajuda você a entender como gerenciar os sites de demonstração criados. Depois de ler esse documento, você deverá:

* Entenda como acessar os Utilitários de demonstração de autoatendimento.
* Saiba quais utilitários estão disponíveis para você.
* Como excluir um site ou modelo de demonstração existente.

## Acesso aos utilitários de demonstração de autoatendimento {#accessing-utilities}

Agora que tem seus próprios sites de demonstração, você provavelmente gostaria de saber como gerenciá-los. O pipeline não só implantou os modelos do site para fornecer conteúdo aos sites de demonstração, como também implantou um conjunto de utilitários para gerenciar esses sites.

1. Na barra de navegação global do AEM, selecione **Ferramentas** > **Demonstrações de referência** > **Utilitários de demonstração de referência**.

   ![Utilitários de demonstração de autoatendimento](assets/demo-utilities.png)

1. Os Utilitários de demonstração de referência são uma coleção de funcionalidades úteis que ajudarão a configurar e monitorar seu ambiente do Adobe Experience Manager. A exibição inicial é o **Painel**, que serve como uma verificação de status do ambiente e de sua funcionalidade de demonstração.

   ![Painel](assets/dashboard.png)

Os Utilitários de demonstração de autoatendimento fornecem várias ferramentas.

* **Excluir sites** - Selecione o site que deseja excluir nesta instância do Adobe Experience Manager. Lembre-se de que essa é uma ação destrutiva e não pode ser desfeita depois de iniciada.
* **Excluir modelos de site** - Selecione o Modelo de site que deseja excluir nesta instância do Adobe Experience Manager. Antes de excluir um Modelo de site, verifique se todos os sites que fazem referência ao modelo também foram excluídos. Lembre-se de que essa é uma ação destrutiva e não pode ser desfeita depois de iniciada.
* **Cache de autor principal** - Ele buscará vários recursos na instância do Adobe Experience Manager, acelerando os tempos de busca. Pode levar alguns segundos.
* **Aplicativo Android** - Ferramentas para instalar e iniciar o aplicativo Android de demonstração. Crie um site com base no **Aplicativo de página única WKND** para preencher esta página. Uso de um dispositivo Android, emulador ou Bluestacks.
* **Preferências do usuário** - Desative as caixas de diálogo do pop-up tutorial.
* **Configurar GraphQL** - Configure rapidamente o ponto de extremidade GraphQL global.

## Exclusão de sites de demonstração e modelos {#deleting}

Depois de testar um conjunto de funcionalidades do AEM, talvez você não precise mais do seu site de demonstração ou mesmo do modelo no qual ele se baseia. É fácil excluir sites de demonstração e modelos de site.

1. Acesse o **Utilitários de demonstração de referência** e selecione **Excluir Sites**.

   ![Excluir sites](assets/delete-sites.png)

1. Os sites disponíveis são apresentados em uma lista. Verifique o site ou sites que deseja excluir e selecione **Excluir**.

   >[!CAUTION]
   >
   >A exclusão de site e modelo é uma ação destrutiva e não pode ser desfeita depois de iniciada.

1. Confirme a exclusão do site na caixa de diálogo.

   ![Confirmar exclusão do site](assets/confirm-site-delete.png)

1. O AEM exclui o site ou sites selecionados e mostra o progresso onde o botão **Excluir** estava anteriormente.

   ![Excluir progresso](assets/delete-progress.png)

O site foi excluído.

É possível excluir modelos da mesma maneira no cabeçalho **Excluir modelos de site** nos **Utilitários de demonstração de referência**.

>[!CAUTION]
>
>Antes de excluir um Modelo de site, verifique se todos os sites que fazem referência ao modelo também foram excluídos.

## Fim da jornada? {#end-of-journey}

Parabéns! Você concluiu a jornada do complemento Demonstrações de referência do AEM. Agora você deve:

* Tenha uma compreensão básica do Cloud Manager e entenda como os pipelines fornecem conteúdo e configuração ao AEM.
* Saiba como usar o Cloud Manager para criar um programa.
* Saiba como ativar o Complemento de demonstrações de referência para o novo programa e executar um pipeline para implantar o conteúdo complementar.
* Entenda como acessar o ambiente de criação do AEM para criar um site com base em um modelo.
* Entenda como acessar os Utilitários de demonstração de autoatendimento.
* Saiba como excluir um site ou modelo de demonstração existente.

Agora você está pronto para explorar os recursos do AEM usando seus próprios sites de demonstração. No entanto, o AEM é uma ferramenta poderosa e há muitas opções adicionais disponíveis. Confira alguns dos recursos adicionais disponíveis na [seção Recursos adicionais](#additional-resources) para saber mais sobre os recursos que você viu nesta jornada.

## Recursos adicionais {#additional-resources}

* [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=pt-BR) - se quiser obter mais detalhes sobre os recursos do Cloud Manager, consulte diretamente os documentos técnicos detalhados.
* [Criar Site](/help/sites-cloud/administering/site-creation/create-site.md) - saiba como usar o AEM para criar um site usando modelos de site para definir o estilo e a estrutura do site.
* [Convenções de nomenclatura de página do AEM](/help/sites-cloud/authoring/sites-console/organizing-pages.md#page-name-restrictions-and-best-practices). - Consulte esta página para entender as convenções de organização das páginas do AEM.
* [Manuseio básico do AEM](/help/sites-cloud/authoring/basic-handling.md): consulte este documento se você for novo no AEM para entender os conceitos básicos, como navegação e organização do console.
* [Documentação técnica do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=pt-BR) - Se já tiver conhecimento profundo do AEM, você poderá consultar diretamente os documentos técnicos aprofundados.
* [Modelos de site](/help/sites-cloud/administering/site-creation/site-templates.md) - Se você quiser saber mais sobre a estrutura dos modelos de site e como eles são usados para criar sites, consulte este documento.
