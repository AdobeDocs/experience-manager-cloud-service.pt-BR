---
title: Visualização do PDF no Editor de comunicação interativa com diferentes opções de dados
description: Visualização do PDF no Editor de comunicação interativa com diferentes opções de dados para visualizar as Comunicações interativas de três maneiras diferentes.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 9adc7a5669d8bf1e64cc93998cb2f91ffa9d3dd6
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Visualização do PDF no Editor de comunicação interativa

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

O recurso de visualização do PDF permite que os usuários visualizem as Comunicações interativas de três maneiras diferentes: sem dados, com dados locais baseados em JSON ou com dados de amostra do modelo de dados configurado.

## Principais benefícios

- Visualize as Comunicações interativas com dados de amostra para visualizar como os dados em tempo real aparecerão quando mesclados com a comunicação.

- Faça upload de arquivos de dados JSON locais para gerar visualizações orientadas por dados sem a configuração de backend.

- Use os Modelos de dados de formulário (FDM) conectados para simular a integração de dados em tempo real com dados de amostra durante o design.

- Alterne facilmente entre as opções de dados (sem dados, dados locais, FDM) para validar o layout, a estrutura e a personalização.

## Visualização do PDF no Editor de comunicação interativa com diferentes opções de dados

Visualize comunicações interativas sem dados, dados locais ou dados de amostra do modelo de dados configurado para testes e validação flexíveis.

+++&#x200B;1. Visualizar sem dados.

1.1. Abra a sua comunicação interativa no Editor IC.

1.2. Use a opção Visualização do PDF e selecione a opção **Sem Dados** para exibir uma comunicação sem dados.

![Localizar IC Docu](/help/forms/interactive-communication/assets/nodata.png)

+++

+++&#x200B;2. Visualizar com dados JSON locais

2.1. Prepare um arquivo JSON estruturado. Para referência, você pode copiar os dados de amostra do esquema JSON [(FDM)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/work-with-form-data-model) usado para a comunicação.

2.2. No Editor IC, vá para **Visualização do PDF** > Usando Dados Locais.

2.3. Selecione e faça upload do arquivo JSON para renderizar uma pré-visualização do PDF com os dados fornecidos.

![Localizar IC Docu](/help/forms/interactive-communication/assets/localdata.png)

+++

+++&#x200B;3. Visualizar com o modelo de dados 

3.1. Selecione **Usando Modelo de Dados** para usar dados de exemplo de um Modelo de Dados de Formulário (FDM) já configurado da IC.

3.2. A pré-visualização preenche automaticamente os dados dos campos de modelo. Verifique se os dados de amostra são salvos no FDM na primeira utilização ou se a visualização pode ser exibida como sem dados.

![Localizar IC Docu](/help/forms/interactive-communication/assets/datamodel.png)

+++

