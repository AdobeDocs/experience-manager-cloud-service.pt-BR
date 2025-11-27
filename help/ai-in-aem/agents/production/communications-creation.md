---
title: Habilidade de criação de comunicação
description: Saiba mais sobre a habilidade de criação de comunicação do agente de produção de experiência e como usar a linguagem natural para criar comunicações interativas.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 01fce6fcdf1c8ada0422a84fccb9a89f395e2a0e
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---


# Habilidade de criação de comunicação {#ic-creation-skill}

>[!NOTE]
>
> A habilidade de Criação de comunicações está atualmente em alfa. Se você deseja participar, envie uma solicitação de seu endereço de email oficial para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com).

As Comunicações interativas são documentos personalizados, orientados por dados, criados para correspondência de negócios, como demonstrativos de conta, documentos de política, contas, kits de boas-vindas e avisos de benefícios. Ao contrário dos formulários que coletam entradas de usuários, as Comunicações interativas geram documentos de saída com conteúdo dinâmico e específico do destinatário.

A habilidade de criação de comunicação é um recurso do Agente de produção de experiência projetado para desenvolver comunicações interativas usando prompts de linguagem natural. Essa habilidade gera automaticamente correspondência personalizada e orientada por dados para impressão (no formato PDF). A habilidade é revelada pelo Assistente de IA.

Alguns dos principais benefícios da habilidade de criação de comunicação incluem:

* **Desenvolvimento acelerado de comunicação**: crie comunicações rapidamente usando comandos de linguagem natural simples, eliminando a necessidade de aprender interfaces de produtos tradicionais.
* **Correspondência consistente e sobre marcas**: crie comunicações que sigam a identidade visual, os modelos e as diretrizes de estilo de sua organização usando modelos e estilos aprovados.
* **Barreira técnica mais baixa**: permite que usuários empresariais criem comunicações facilmente, sem precisar de conhecimento técnico avançado ou de produtos profundos.

## Recursos {#capabilities}

<!-- * **Create personalized communications with plain text prompt**: You can create communication documents for print (in PDF format) by submitting your requirements in plain language. The agent automatically generates appropriate document structures, layouts, and data bindings based on your natural language description. -->

* **Criar a partir de modelos**: você pode usar modelos organizacionais aprovados para garantir a consistência da marca e os padrões de conformidade. O agente utiliza seus modelos e diretrizes de estilo existentes para criar correspondência na marca que atenda aos requisitos normativos.

* **Importar e converter imagens e documentos existentes em comunicações interativas**: você pode importar e transformar documentos existentes em comunicações interativas. O agente analisa o conteúdo carregado para detectar campos, preservar layouts e criar correspondência orientada por dados com recursos de conteúdo dinâmico. Os formatos compatíveis incluem PDFs, imagens (JPG, PNG) e modelos desenhados à mão.


## Exemplos de prompts {#sample-prompts}

* *Crie uma comunicação para um demonstrativo de empréstimo usando o modelo em https://[aem-author-url]/path/to/pdf/file*
* *Criar uma comunicação do PDF em https://[aem-author-url]/path/to/pdf/file*
* *Criar uma comunicação do arquivo de imagem em https://[aem-author-url]/path/to/image/file*
* Crie uma carta usando o arquivo do PDF em https://[aem-author-url]/path/to/pdf/file


## Refine sua comunicação {#refine-with-ic-editor}


Depois de criar sua estrutura de comunicação inicial usando o Assistente de IA, você pode usar o Editor de comunicações interativas para refinar e aprimorar seu documento. No Editor de comunicações interativas, você pode fornecer prompts em linguagem natural para:

* **Adicionar campos e conteúdo**: adicione novos campos, blocos de texto, imagens, gráficos, tabelas e outros componentes aos seus documentos de comunicação usando prompts de linguagem natural. O agente interpreta as instruções e insere os elementos apropriados com estrutura e formatação adequadas.

* **Editar campos e conteúdo**: modifique campos e conteúdo existentes em seus documentos de comunicação por meio de comandos conversacionais. Atualize as propriedades do campo, altere o conteúdo do texto, ajuste as associações de dados e refine as configurações de componentes.

* **Remover campos e conteúdo**: exclua campos, componentes ou seções indesejados de seus documentos de comunicação usando instruções em linguagem natural. O agente remove os elementos especificados enquanto mantém a estrutura do documento e a integridade do layout.

* **Campos e conteúdo de estilo**: aplique formatação e estilo a campos e conteúdo por meio de prompts de linguagem natural. Ajuste fontes, cores, alinhamento, espaçamento e outras propriedades visuais para corresponder às diretrizes da marca e aos requisitos de design.

### Exemplos de prompts para refinar as comunicações {#sample-prompts-refining}

* *Gerar uma carta de liquidação de reclamação de seguro de veículo*
* *Colocar o texto do aviso em itálico*
* *Alterar o tamanho da fonte do texto do aviso para 12*
* *Atualizar a cor da fonte do texto do aviso de isenção de responsabilidade para vermelho*
* *Atualizar a cor de plano de fundo das caixas de texto de cabeçalho e rodapé para cinza claro*
* *Adicionar um novo painel de aviso de isenção de responsabilidade com campos de assinatura e confirmação*
* *Remover o campo de texto de confirmação*
* *Adicionar uma tabela de detalhes de pagamento com três colunas*
* *Atualize o alinhamento do campo de número da política ao centro*
* *Altere o espaçamento entre linhas da seção de termos e condições para 1.5*

Para obter mais informações sobre os recursos do editor de Comunicação Interativa, consulte [Documentação de Comunicações Interativas](/help/forms/introduction-to-interactive-communication.md).

## Ativação {#activation}

Para habilitar o Agente de produção de experiência para sua organização, a ativação deve ser iniciada por meio do Adobe. Comece o processo fazendo um contato via:

* Email: `experience-production-agent@adobe.com`
* Ou entre em contato com a equipe de conta designada da Adobe.

Ao entrar em contato com o, forneça sua ID da organização da AEM as a Cloud Service.

