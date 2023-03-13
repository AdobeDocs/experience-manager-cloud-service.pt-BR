---
title: Problemas conhecidos e limitações
description: Problemas conhecidos e limitações do  [!DNL AEM Forms] ambiente as a Cloud Service
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 94825e3b60d970fec5bf696d932ca66bb83fd2f3
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 11%

---

# Problemas conhecidos e limitações {#known-issues-and-limitations}

Antes de começar a usar [!DNL AEM Forms] as a Cloud Service, analise os seguintes problemas e limitações conhecidos:

## Problemas conhecidos {#known-issues}

* Não adicione e execute um teste que envie um formulário adaptável de uma instância de publicação para um fluxo de trabalho AEM em execução em uma instância de autor até aviso adicional.

* Ao importar um Formulário adaptável que use um modelo contendo a variável **[!UICONTROL Salvar]** botão, o botão **[!UICONTROL Salvar]** continua a aparecer no Formulário adaptável mesmo depois de ser removido do modelo correspondente. Remova o **[!UICONTROL Salvar]** do Adaptive Forms antes de publicá-lo. Fique de olho nas notas de versão referentes à disponibilidade do Portal do Forms e ao recurso Salvar como rascunho para restaurar e usar o botão.

* A variável **[!UICONTROL Definir variável]** A etapa de fluxos de trabalho do AEM não é compatível com variáveis do tipo lista de matriz. Você pode usar a etapa do processo para definir variáveis do tipo lista de matriz.

* Ao enviar um formulário adaptável contendo um campo de upload de HTML padrão de um dispositivo Apple iOS, o conteúdo do arquivo não é enviado e um arquivo de 0 byte é recebido na outra extremidade. O problema ocorre intermitentemente e somente ao usar o envio síncrono. Este é um [problema conhecido](https://feedbackassistant.apple.com/feedback/9117687) no Apple iOS.

* Quando você envia um formulário contendo um campo de upload de HTML padrão de um dispositivo Apple iOS, às vezes, o conteúdo do arquivo não é enviado e um arquivo de 0 byte é recebido na outra extremidade. Esse é um problema conhecido no Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

* O AEM Forms as a Cloud Service não gera miniaturas para arquivos de esquema XDP e JSON. O serviço exibe ícones padrão no lugar de miniaturas.

   ![Problema conhecido na miniatura do Forms](/help/forms/assets/forms-tumbnail-known-issue.png)


## Limitações {#limitations}

* O suporte para formulários adaptáveis baseados em XFA não está disponível imediatamente. Se você pretende usar formulários adaptáveis baseados em XFA, entre em contato com o Suporte da Adobe com detalhes do caso de uso e requisitos específicos.

