---
title: Quais são os problemas conhecidos e as limitações do ambiente as a Cloud Service do AEM Forms?
description: Problemas conhecidos e limitações do  [!DNL AEM Forms] ambiente as a Cloud Service.
contentOwner: khsingh
role: Admin, Developer, User
feature: Adaptive Forms
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 93%

---

# Problemas conhecidos e limitações {#known-issues-and-limitations}

Antes de começar a usar o [!DNL AEM Forms] as a Cloud Service, analise os seguintes problemas e limitações conhecidos:

## Problemas conhecidos {#known-issues}

* Até novo aviso, não adicione e execute um teste que envie um formulário adaptável de uma instância de publicação para um fluxo de trabalho do AEM em execução em uma instância de criação.

* Ao importar um formulário adaptável que use um modelo contendo o botão **[!UICONTROL Salvar]**, o botão **[!UICONTROL Salvar]** continua a aparecer no formulário adaptável mesmo após ser removido do modelo correspondente. Remova o botão **[!UICONTROL Salvar]** de seus formulários adaptáveis antes de publicá-los. Acompanhe as notas de versão para saber se o Portal do Forms e o recurso Salvar como rascunho estão disponíveis para restaurar e usar o botão.

* A etapa **[!UICONTROL Definir variável]** dos fluxos de trabalho do AEM não é compatível com variáveis do tipo lista de matriz. Você pode usar a etapa do processo para definir variáveis do tipo lista de matriz.

* Ao enviar um formulário adaptável que contém um campo de upload HTML padrão de um dispositivo Apple iOS, o conteúdo do arquivo não é enviado e um arquivo de 0 byte é recebido do outro lado. O problema ocorre de forma intermitente e somente ao usar o envio síncrono. Este é um [problema conhecido](https://feedbackassistant.apple.com/feedback/9117687) no Apple iOS.

* Ao enviar um formulário contendo um campo de upload HTML padrão de um dispositivo Apple iOS, às vezes o conteúdo do arquivo não é enviado e um arquivo de 0 byte é recebido do outro lado. Esse é um problema conhecido no Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

* O AEM Forms as a Cloud Service não gera miniaturas para arquivos de esquema XDP e JSON. O serviço exibe ícones padrão no lugar de miniaturas.

  ![Problema conhecido na miniatura do Forms](/help/forms/assets/forms-tumbnail-known-issue.png)

* Ao usar um esquema com elementos repetíveis para criar um formulário adaptável baseado em componentes principais, a opção de arrastar e soltar elementos repetíveis da árvore do modelo de dados no editor de formulários adaptáveis não funciona.

## Limitações {#limitations}

* O suporte para formulários adaptáveis baseados em XFA não está disponível imediatamente. Se você pretende usar formulários adaptáveis baseados em XFA, entre em contato com o Suporte da Adobe com detalhes do caso de uso e requisitos específicos.

