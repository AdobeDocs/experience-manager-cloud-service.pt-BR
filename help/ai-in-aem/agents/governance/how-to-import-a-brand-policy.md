---
title: Como importar uma política de marca
description: Usar o Adobe Governance Agent para importar uma política de marca
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 94d671ebbd5aeb5992fdbc9d779ffbca51f82585
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---


# Como importar uma política de marca {#how-to-import-a-brand-policy}

## Visão geral {#overview}

Uma política de marca define as regras, os padrões e as restrições que garantem que todo o conteúdo produzido ou atualizado pelo Adobe Experience Manager permaneça consistente com a identidade de marca de uma empresa. Normalmente, isso inclui tom de voz, terminologia, diretrizes visuais e regras editoriais.

O Agente de governança usa as políticas da marca como uma fonte da verdade para analisar páginas existentes e orientar a geração de conteúdo. Os clientes podem fornecer suas próprias políticas de marca originais, que o Agente de governança converte automaticamente em verificações de política legíveis por IA. Essas verificações são usadas para validar o conteúdo e fornecer ao Agente de produção uma estrutura confiável e aplicável para gerar ou atualizar páginas que permanecem alinhadas com a marca.

## O que é uma Política de marca no Agente de governança {#what-is-a-brand-policy-in-the-governance-agent}

No contexto do Agente de governança, uma política de marca é uma representação estruturada das regras de marca que podem ser entendidas e aplicadas pela IA. Em vez de exigir que os clientes reescrevam suas diretrizes em um formato técnico, o Agente de governança aceita as políticas da marca em sua forma original (por exemplo, documentos, diretrizes ou descrições de regras).

Depois de importada, a política é transformada em um conjunto de verificações de política de IA que podem:

* Analisar páginas existentes para detectar inconsistências de marca
* Sinalizar desvios de tom, terminologia ou regras obrigatórias
* Fornecer orientação clara aos agentes downstream
* Garantir que o conteúdo gerado ou atualizado permaneça em conformidade com a marca desde o design

Essa abordagem permite que as equipes reutilizem a documentação da marca existente enquanto se beneficiam da governança automatizada e da produção de conteúdo escalável.

## Como as políticas da marca são usadas {#how-brand-policies-are-used}

Depois que uma política de marca é importada:

* O Agente de governança interpreta e normaliza a política em verificações de IA aplicáveis
* As páginas podem ser analisadas em relação à política para identificar lacunas ou violações
* O Agente de produção usa essas verificações como restrições ao gerar ou atualizar conteúdo
* A conformidade com a marca se torna consistente, repetível e auditável em todos os sites e equipes


## Importar uma política de marca {#import-a-brand-policy}

Para importar uma marca para o Agente de governança:

1. Crie uma marca fornecendo um nome e um domínio principal. Você pode fazer isso clicando no botão **Contexto de Governança** na navegação à esquerda na sua página inicial do Experience Manager e pressionando o botão **+ Adicionar Marca**, conforme mostrado abaixo:

   ![Adicionando uma nova marca](/help/ai-in-aem/agents/governance/assets/add_brand.png){width="70%"}

1. Defina o nome da marca e uma descrição na janela a seguir

   ![Nomeando a marca](/help/ai-in-aem/agents/governance/assets/add_brand_dialogue.png){width="60%"}

1. Novas marcas são criadas no status de rascunho. Certifique-se de alterar a marca recém-criada para um status Ativo, clicando no cartão da marca, pressionando o botão de edição (lápis) no canto superior direito da tela, defina o **Status** como **Ativo** na janela a seguir e clique em **Salvar alterações**. Você precisa ativar as marcas definindo-as como Ativas antes de poder usá-las.

   ![Definir status da marca como Ativo](/help/ai-in-aem/agents/governance/assets/set_brand_active.png){width="60%"}

1. Depois que a marca for criada, crie um domínio principal na janela a seguir pressionando o link **Domínios** à esquerda:

   ![Configurando um domínio para a marca](/help/ai-in-aem/agents/governance/assets/add_domain.png)

   >[!IMPORTANT]
   >
   >Assim como novas marcas, novos domínios são criados com um status padrão de Rascunho. Para alterar isso, vá para sua Marca, clique em **Domínios** e edite seu domínio usando o ícone de lápis e defina seu status como **Ativo**.

1. Após configurar o domínio principal, carregue o documento de política de marca acessando **Políticas** no canto superior esquerdo da janela e pressionando o botão **+ Adicionar política**.

   ![Adicionando uma política a partir do cartão da Marca](/help/ai-in-aem/agents/governance/assets/add_policy_treeview.png)

   >[!NOTE]
   >
   >Como alternativa, você também pode adicionar políticas alternando para a guia **Políticas** e pressionando o link **+ Adicionar Política**.

1. Na próxima janela, pressione em **Fazer upload de PDFs** e selecione o(s) documento(s) de política de marca no formato PDF

   ![Carregar o documento da política de marca](/help/ai-in-aem/agents/governance/assets/upload_brand_policy_document.png){width="70%"}

   O Agente de governança analisará a diretriz de política da marca usando linguagem natural e extrairá as verificações obtidas do documento e as traduzirá em tarefas reais. Depois que o documento for processado, você poderá exibir um resumo da importação, incluindo o número de verificações e o status da política, conforme mostrado abaixo:

   ![Uma janela de visão geral do status da política de marca](/help/ai-in-aem/agents/governance/assets/policy_status.png)

1. Depois que sua marca for criada e seu documento de política for carregado, você poderá obter uma exibição detalhada por marca na guia **Marcas** e clicando no cartão de uma marca. Esta é a exibição que você desejará usar para criar categorias de verificações, pressionando os três pontos ao lado de uma categoria existente e selecionando **+ Adicionar categoria**, como mostrado na captura de tela abaixo:

   ![Adicionar categoria](/help/ai-in-aem/agents/governance/assets/add_category.png)

   Também é possível usar essa visualização para criar, editar e excluir verificações, que detalharemos nas etapas abaixo.

1. Para obter uma exibição mais granular de cada verificação individual, você pode alternar para a guia **Verificações** e exibir uma lista de cada verificação individual extraída de seus documentos de diretriz. É possível filtrar verificações com base na marca ou no status:

   ![Ver verificações de marca individuais](/help/ai-in-aem/agents/governance/assets/see_brand_checks.png)

   Além disso, você pode exibir detalhes adicionais sobre cada verificação individual clicando nos três pontos (**...**) à esquerda da verificação e pressionando **Exibir detalhes**. Isso abrirá uma nova janela com mais informações sobre a verificação:

   ![Exibir detalhes da verificação individual](/help/ai-in-aem/agents/governance/assets/view_check_details.png)

   Você também pode excluir verificações pressionando **Excluir** no mesmo local de menu, ou editando-as pressionando **Editar**:

   ![Editando uma verificação](/help/ai-in-aem/agents/governance/assets/edit_check.png)

1. Você pode adicionar uma verificação manualmente pressionando **Adicionar verificação** no canto superior esquerdo da janela Verificações:

   ![Adicionando uma verificação](/help/ai-in-aem/agents/governance/assets/add_check.png)

   Na tela a seguir, é possível configurar detalhes como:

   * O nome do cheque
   * A regra, descrita em linguagem natural
   * A categoria
   * O(s) escopo(s) aos quais se aplica

   ![Configurando os detalhes da verificação](/help/ai-in-aem/agents/governance/assets/add_check_window.png)

1. Por fim, para obter uma lista de domínios e as marcas às quais eles estão associados, você pode pressionar a guia **Domínios**. Esta seção permitirá adicionar, excluir ou modificar domínios na lista.

