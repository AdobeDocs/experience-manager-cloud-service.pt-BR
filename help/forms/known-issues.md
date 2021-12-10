---
title: Problemas conhecidos e limitações
description: Problemas conhecidos e limitações de  [!DNL AEM Forms] Ambiente as a Cloud Service
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# Problemas conhecidos e limitações {#known-issues-and-limitations}

Antes de começar a usar [!DNL AEM Forms] as a Cloud Service, analise os seguintes problemas conhecidos e limitações:

## Problemas conhecidos {#known-issues}

* Não adicione nem execute um teste que envie um Formulário adaptável de uma instância de publicação para um Fluxo de trabalho AEM em execução em uma instância do autor até um aviso em contrário.

* Ao importar um formulário adaptável que usa um modelo contendo a variável **[!UICONTROL Salvar]** , o botão **[!UICONTROL Salvar]** continua a aparecer no formulário adaptável mesmo depois de removê-lo do modelo correspondente. Remova o **[!UICONTROL Salvar]** do Adaptive Forms antes de publicá-lo. Fique de olho nas notas de versão para ver a disponibilidade do Portal do Forms e Salve como um recurso de rascunho para restaurar e usar o botão .

* O **[!UICONTROL Definir variável]** A etapa de AEM Workflows não suporta variáveis do tipo array list. Você pode usar a etapa do processo para definir variáveis do tipo array list.

* Ao enviar um formulário adaptável contendo um campo de carregamento HTML padrão de um dispositivo Apple iOS, o conteúdo do arquivo não é enviado e um arquivo de 0 byte é recebido na outra extremidade. O problema ocorre intermitentemente e somente no uso do envio síncrono. Isso é uma [problema conhecido](https://feedbackassistant.apple.com/feedback/9117687) no Apple iOS.

* Às vezes, ao enviar um formulário contendo um campo de carregamento HTML padrão de um dispositivo Apple iOS, o conteúdo do arquivo não é enviado e um arquivo de 0 byte é recebido na outra extremidade. Esse é um problema conhecido no Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)


## Limitações           {#limitations}

* O suporte para Forms adaptável baseado em XFA não está disponível imediatamente. Se você pretende usar o Forms adaptável baseado em XFA, entre em contato com o Suporte ao Adobe com detalhes do caso de uso e requisitos específicos.

