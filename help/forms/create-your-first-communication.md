---
title: Criar a primeira comunicação interativa
description: Projete comunicações dinâmicas orientadas por dados com facilidade com as Comunicações interativas da AEM Forms
feature: Release Information
role: Admin
hide: true
hidefromtoc: true
source-git-commit: a771aa7e683cfbcacc8a9d5765c63d50169a2756
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 3%

---


# Criar a primeira comunicação interativa


>[!VIDEO](https://video.tv.adobe.com/v/3444094/)

## Etapa 1: Planejar a comunicação interativa

A primeira etapa no planejamento de uma comunicação interativa é finalizar o conteúdo da comunicação interativa. Depois que o conteúdo for finalizado, você deverá analisá-lo para identificar os vários tipos de ativos necessários para criar a Comunicação interativa.

### Considerações de planejamento

Uma comunicação interativa inclui os seguintes elementos:

* **O texto estático** inclui principalmente as partes da comunicação interativa que são genéricas por natureza e estão incluídas na comunicação com todos os clientes. Por exemplo, cabeçalho, rodapé, saudação ou avisos de isenção de responsabilidade.

* **Os dados provenientes de um sistema back-end (modelo de dados de formulário)** são específicos do cliente e são mesclados dinamicamente com a comunicação interativa. Por exemplo, o número da política ou o endereço pode ser originado usando o modelo de dados de formulário.

* **Layout ou modelos** para a versão para impressão e para Web da Comunicação Interativa.

* **Ordem** na qual os vários parágrafos de texto aparecem na Comunicação Interativa.

* **Dados condicionais** que são preenchidos com base em condições predefinidas. Por exemplo, a data em que a comunicação interativa é gerada.

* **Imagens armazenadas em um repositório**, como logotipos e imagens de assinatura. Imagens como logotipos corporativos apareceriam na maioria ou em todas as comunicações interativas.

* **Gráficos e tabelas** necessários para simplificar a representação de dados complexos em uma Comunicação Interativa

### Anatomia da comunicação interativa

Depois de finalizar o conteúdo e os elementos usados para criar a Comunicação interativa, você pode criar uma anatomia da Comunicação interativa. A anatomia deve ter os detalhes listados na seção Considerações de Planejamento. Por exemplo, uma anatomia da conta mensal que uma operadora de telecomunicações envia aos seus clientes.

A anatomia inclui dados com os seguintes modos de entrada:

* Texto estático
* Modelo de dados do formulário
* Dados condicionais
* Imagens


## Etapa 2: Criar modelo de dados de formulário

Um modelo de dados de formulário permite conectar uma Comunicação interativa a fontes de dados diferentes. Por exemplo, perfil de usuário AEM, serviços Web RESTful, serviços Web baseados em SOAP, serviços OData e bancos de dados relacionais. Um modelo de dados de formulário é um esquema de representação de dados unificada de entidades e serviços comerciais disponíveis em fontes de dados conectadas. Você pode usar o modelo de dados de formulário com uma Comunicação interativa para recuperar dados de fontes de dados conectadas. Para obter mais informações sobre o modelo de dados de formulário, consulte [Integração de dados do AEM Forms](/help/forms/data-integration.md).

## Etapa 3: Criar fragmentos

Os fragmentos de documento são componentes reutilizáveis de uma correspondência usados para compor uma comunicação interativa. Os fragmentos de documento são dos tipos: Texto, Lista e Condição.


## Etapa 4: criar modelos

O Editor de comunicações interativas fornece vários modelos OOTB. Você pode modificar esses modelos de acordo com os requisitos de sua organização ou criar um modelo do zero.


## Etapa 5: Criar uma comunicação interativa

Depois de criar todos os blocos de construção, como modelo de dados de formulário, fragmentos de documento e modelos para a versão da Web, você pode começar a criar uma comunicação interativa. Para começar a criar uma comunicação interativa:

1. Faça logon no ambiente as a Cloud Service do AEM Forms.
1. Acesse Forms > Forms e documentos
1. Clique em **Criar** e selecione **Documento de comunicação**. Você verá uma tela de configuração para definir as seguintes opções:

   | Texto | Descrição | Obrigatório |
   |-------|-------------|----------|
   | Nome | Identificador exclusivo da comunicação | Sim |
   | Título | Nome de exibição da sua comunicação | Sim |
   | Descrição | Breve descrição da finalidade da comunicação | Não |
   | Modelo | Selecione um modelo pré-configurado ou comece do zero | Sim |
   | Tags | Adicionar tags de metadados para uma melhor organização | Não |

1. Acesse a guia &quot;Predefinições&quot; e configure as seguintes opções:

   | Texto | Descrição |
   |-------|-------------|
   | Lista de predefinições | Selecione uma predefinição pré-configurada para o tamanho do documento. As opções comuns incluem A4, Carta e muito mais. |
   | Largura predefinida | Exibe a largura da predefinição da lista de predefinições selecionada. |
   | Altura predefinida | Exibe a altura da predefinição da lista de predefinições selecionada. |
   | Unidade de predefinição | Selecione a unidade de medida para as dimensões do documento (por exemplo, Milímetros, Polegadas). |
   | Orientação predefinida | Escolha a orientação do documento - retrato ou paisagem. |

1. Clique em **Criar**. A Comunicação é aberta no editor.
1. Arraste e solte componentes e fragmentos para criar a Comunicação interativa.

   * Use a **Página Mestra** para o conteúdo comum entre páginas. As páginas mestras são designadas para formatar páginas e ajudam a facilitar a consistência do design, pois podem fornecer um formato de plano de fundo e layout para mais de uma página no design de um documento.

   * Use **Páginas** para criar o layout do conteúdo e do documento. Cada página deriva seu tamanho e orientação de uma página-mestre e, por padrão, cada página é associada à página-mestre padrão criada pelo Designer.


1. Use a notação `@` para preencher automaticamente os campos de dados com base no modelo de dados conectado.
1. Use a opção `PDF Preview` para visualizar o documento junto com os dados. Você precisa do arquivo de dados no formato JSON.
