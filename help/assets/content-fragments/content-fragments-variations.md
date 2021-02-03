---
title: Variações - Criação dos fragmentos de conteúdo
description: As variações permitem que você crie conteúdo para o fragmento e, em seguida, crie variações desse conteúdo de acordo com a finalidade (se necessário).
translation-type: tm+mt
source-git-commit: 972d242527871660d55b9a788b9a53e88d020749
workflow-type: tm+mt
source-wordcount: '2186'
ht-degree: 16%

---


# Variações - Criação dos fragmentos de conteúdo{#variations-authoring-fragment-content}

[As ](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) variações são um recurso significativo de fragmentos de conteúdo, pois permitem que você crie e edite cópias do conteúdo principal para uso em canais específicos e/ou cenários.

Na guia **Variações** é possível:

* [Insira o ](#authoring-your-content) conteúdo do fragmento,
* [Criar e gerenciar ](#managing-variations) variações do  **** conteúdo mestre,

Executar várias outras ações, dependendo do tipo de dados que está sendo editado; por exemplo:

* [Inserir ativos visuais no fragmento](#inserting-assets-into-your-fragment)  (imagens)

* Selecione entre [Rich Text](#rich-text), [Texto sem formatação](#plain-text) e [Markdown](#markdown) para edição

* [Fazer upload de conteúdo](#uploading-content)

* [Estatísticas](#viewing-key-statistics)  de chave de visualização (sobre texto de várias linhas)

* [Resumir texto](#summarizing-text)

* [Sincronizar variações com conteúdo Principal](#synchronizing-with-master)

>[!CAUTION]
>
>Depois que um fragmento é publicado e/ou referenciado, AEM exibirá um aviso quando um autor abrir o fragmento para edição novamente. Isso serve para avisar que as alterações no fragmento também afetarão as páginas referenciadas.

## Criação do seu conteúdo {#authoring-your-content}

Ao abrir o fragmento do conteúdo para edição, a guia **Variações** será aberta por padrão. Aqui você pode criar o conteúdo, para obter variações Principais ou possíveis. O fragmento estruturado contém vários campos, de vários tipos de dados, que foram definidos no modelo de conteúdo.

É possível:

* faça edições diretamente na guia **Variações**

   * cada tipo de dados fornece opções de edição diferentes

* para os campos **Texto de várias linhas** você também pode abrir o [editor de tela cheia](#full-screen-editor) para:

   * selecione [Format](#formats)
   * consulte mais opções de edição (para o formato [Rich Text](#rich-text))
   * acesse um intervalo de [ações](#actions)

Por exemplo:

![editor de tela cheia](assets/cfm-variations-02.png)

### Editor de tela cheia {#full-screen-editor}

Ao editar um campo de texto de várias linhas, você pode abrir o editor de tela cheia; toque ou clique no texto real e selecione o seguinte ícone de ação:

![ícone do editor de tela cheia](assets/cfm-variations-03.png)

Isso abrirá o editor de texto de tela cheia:

![editor de tela cheia](assets/cfm-variations-fullscreentexteditor.png)

O editor de texto em tela cheia fornece:

* Acesso a várias [ações](#actions)
* Dependendo do [formato](#formats), opções de formatação adicionais ([Rich Text](#rich-text))

### Ações {#actions}

As seguintes ações também estão disponíveis (para todos os [formatos](#formats)) quando o editor de tela cheia (ou seja, texto de várias linhas) está aberto:

* Selecione o [formato](#formats) ([Rich Text](#rich-text), [Texto simples,](#plain-text) [Markdown](#markdown))

* [Carregar conteúdo](#uploading-content)

* [Mostrar estatísticas de texto](#viewing-key-statistics)

* [Sincronizar com Principal](#synchronizing-with-master)  (ao editar uma variação)

* [Resumir texto](#summarizing-text)

### Formatos {#formats}

As opções para editar texto de várias linhas dependem do formato selecionado:

* [Texto formatado](#rich-text)
* [Texto sem formatação](#plain-text)
* [Markdown](#markdown)

O formato pode ser selecionado no editor de tela cheia.

### Texto formatado {#rich-text}

A edição de rich text permite formatar:

* Negrito
* Itálico
* Sublinhado
* Alinhamento: esquerda, centro, direita
* Lista com marcadores
* Lista numerada
* Recuo: aumento, diminuição
* Criar/Quebrar hiperlinks
* Colar texto/do Word
* Inserir uma tabela
* Estilo do parágrafo: Parágrafo, Título 1/2/3
* [Inserir ativo](#inserting-assets-into-your-fragment)
* Abra o editor de tela cheia, onde as seguintes opções de formatação estão disponíveis:
   * Pesquisar  
   * Localizar/substituir
   * Verificador ortográfico
   * [Anotações](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Inserir fragmento](#inserting-content-fragment-into-your-fragment) do conteúdo; disponível quando seu  **campo de texto** Várias linhas está configurado com  **Permitir referência** de fragmento.

As [ações](#actions) também podem ser acessadas pelo editor de tela cheia.

### Texto sem formatação {#plain-text}

Texto simples permite a entrada rápida de conteúdo sem formatação ou informações de marcação. Você também pode abrir o editor de tela cheia para mais [ações](#actions).

>[!CAUTION]
>
>Se selecionar **Texto simples**, poderá perder qualquer formatação, marcação e/ou ativos inseridos no **Rich Text** ou na **Marcação**.

### Markdown {#markdown}

>[!NOTE]
>
>Para obter informações completas, consulte a documentação [Markdown](/help/assets/content-fragments/content-fragments-markdown.md).

Isso permite que você formate o texto usando a marcação. Você pode definir:

* Cabeçalhos
* Quebras de parágrafos e linhas
* Links
* Imagens
* Bloquear aspas
* Listas
* Ênfase
* Blocos de código
* Escapas de barra invertida

Você também pode abrir o editor de tela cheia para mais [ações](#actions).

>[!CAUTION]
>
>Se você alternar entre **Rich Text** e **Marcação**, poderá ver efeitos inesperados com Cotas de bloqueio e Bloqueios de código, já que esses dois formatos podem ter diferenças na maneira como são tratados.

### Referências de fragmento {#fragment-references}

Se o Modelo de fragmento de conteúdo contiver Referências de fragmento, os autores do fragmento poderão ter opções adicionais:

* [Editar fragmento do conteúdo](#fragment-references-edit-content-fragment)
* [Novo fragmento de conteúdo](#fragment-references-new-content-fragment)

![Referências de fragmento](assets/cfm-variations-12.png)

#### Editar fragmento do conteúdo {#fragment-references-edit-content-fragment}

A opção **Editar fragmento de conteúdo** abrirá
uma nova guia do navegador, com o fragmento de conteúdo aberto no editor de fragmentos de conteúdo.

#### Novo fragmento de conteúdo {#fragment-references-new-content-fragment}

A opção **Novo fragmento de conteúdo** permitirá que você crie um fragmento completamente novo. Para conseguir isso, uma variação do assistente de criação de fragmento de conteúdo será aberta no editor.

Você poderá criar um novo fragmento ao:

1. Navegação até a pasta desejada e seleção dela.
1. Selecionando **Next**.
1. Especificação de propriedades; por exemplo **Title**.
1. Selecionando **Create**.
1. Finalmente:
   1. **O** Donell retornará (para o fragmento original) e referenciará o novo fragmento.
   1. **A opção** Abrir referenciará o novo fragmento, bem como abrirá o novo fragmento, para edição, em uma nova guia do navegador.

### Exibindo Estatísticas-Chave {#viewing-key-statistics}

Quando o editor de tela cheia estiver aberto, a ação **Estatísticas de texto** exibirá uma variedade de informações sobre o texto.

Por exemplo:

![estatísticas](assets/cfm-variations-04.png)

### Carregando conteúdo {#uploading-content}

Para facilitar o processo de criação de fragmentos de conteúdo, é possível carregar texto, preparado em um editor externo e adicioná-lo diretamente ao fragmento.

### Resumo de texto {#summarizing-text}

O texto de resumo foi projetado para ajudar os usuários a reduzir o comprimento do texto para um número predefinido de palavras, mantendo os pontos-chave e o significado geral.

>[!NOTE]
>
>A um nível mais técnico, o sistema mantém as frases que classifica como proporcionando a *melhor relação de densidade e exclusividade das informações* de acordo com algoritmos específicos.

>[!CAUTION]
>
>O fragmento de conteúdo deve ter uma pasta de idioma válida (Código ISO) como ancestral; isso é usado para determinar o modelo de idioma a ser usado.
>
>Por exemplo, `en/` como no seguinte caminho:
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
O inglês está disponível prontamente.
Outros idiomas estão disponíveis como Pacotes de modelo de idioma no Compartilhamento de pacotes:
* [Francês (França)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-fr)
* [Alemão (Alemanha)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-de)
* [Italiano (Itália)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-it)
* [Espanhol (Espanha)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-es)



1. Selecione **Principal** ou a variação necessária.
1. Abra o editor de tela cheia.

1. Selecione **Resumir texto** na barra de ferramentas.

   ![resumo](assets/cfm-variations-05.png)

1. Especifique o número de palavras do público alvo e selecione **Start**:
1. O texto original é exibido lado a lado com a sumariação proposta:

   * Todas as frases a serem eliminadas são destacadas em vermelho, com greve.
   * Clique em qualquer frase destacada para mantê-la no conteúdo resumido.
   * Clique em qualquer frase não realçada para eliminá-la.

1. Selecione **Resumo** para confirmar as alterações.

1. O texto original é exibido lado a lado com a sumariação proposta:

   * Todas as frases a serem eliminadas são destacadas em vermelho, com greve.
   * Clique em qualquer frase destacada para mantê-la no conteúdo resumido.
   * Clique em qualquer frase não realçada para eliminá-la.

   ![comparação de resumo](assets/cfm-variations-06.png)

### Anotar em um fragmento de conteúdo {#annotating-a-content-fragment}

Para anotar um fragmento:

1. Selecione **Principal** ou a variação necessária.

1. Abra o editor de tela cheia.

1. O ícone **Anotar** está disponível na barra de ferramentas superior. Você pode selecionar algum texto, se necessário.

   ![anotação](assets/cfm-variations-07.png)

1. Uma caixa de diálogo abrirá. Aqui você pode inserir sua anotação.

   ![anotação](assets/cfm-variations-07a.png)

1. Selecione **Aplicar** na caixa de diálogo.

   ![anotação](assets/cfm-variations-annotations-apply-icon.png)

   Se a anotação tiver sido aplicada ao texto selecionado, o texto permanecerá destacado.

   ![anotação](assets/cfm-variations-07b.png)

1. Feche o editor de tela cheia; as anotações ainda são destacadas. Se selecionada, uma caixa de diálogo será aberta para que você possa editar a anotação ainda mais.

1. Selecione **Salvar**.

1. Feche o editor de tela cheia; as anotações ainda são destacadas. Se selecionada, uma caixa de diálogo será aberta para que você possa editar a anotação ainda mais.

   ![anotação](assets/cfm-variations-07c.png)

### Visualização, edição, exclusão de anotações {#viewing-editing-deleting-annotations}

Anotações:

* São indicados pelo realce do texto, em tela cheia e no modo normal do editor. Os detalhes completos de uma anotação podem ser exibidos, editados e/ou excluídos clicando-se no texto realçado, que reabrirá a caixa de diálogo.

   >[!NOTE]
   Um seletor suspenso é fornecido se várias anotações tiverem sido aplicadas a uma parte do texto.

* Quando você exclui o texto inteiro ao qual a anotação foi aplicada, a anotação também é excluída.

* É possível listar e excluir selecionando a guia **Anotações** no editor de fragmentos.

   ![Anotações](assets/cfm-variations-08.png)

* Pode ser exibido e excluído em [Linha do tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) para o fragmento selecionado.

### Inserir ativos no fragmento {#inserting-assets-into-your-fragment}

Para facilitar o processo de criação de fragmentos de conteúdo, você pode adicionar [Ativos](/help/assets/manage-digital-assets.md) (imagens) diretamente ao fragmento.

Eles serão adicionados à sequência de parágrafo do fragmento sem qualquer formatação; a formatação pode ser feita quando o fragmento [é usado/referenciado em uma página](/help/sites-cloud/authoring/fundamentals/content-fragments.md).

>[!CAUTION]
Esses ativos não podem ser movidos ou excluídos em uma página de referência, isso deve ser feito no editor de fragmentos.
No entanto, a formatação do ativo (por exemplo, tamanho) deve ser feita no [editor de página](/help/sites-cloud/authoring/fundamentals/content-fragments.md). A representação do ativo no editor de fragmentos é apenas para a criação do fluxo de conteúdo.

>[!NOTE]
Existem vários métodos de adicionar [imagens](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) ao fragmento e/ou página.

1. Posicione o cursor na posição que deseja adicionar a imagem.
1. Use o ícone **Inserir ativo** para abrir a caixa de diálogo de pesquisa.

   ![inserir ícone de ativo](assets/cfm-variations-09.png)

1. Na caixa de diálogo, é possível:

   * navegue até o ativo necessário no DAM
   * procurar o ativo no DAM

   Depois de localizado, selecione o ativo desejado clicando na miniatura.

1. Use **Selecionar** para adicionar o ativo ao sistema de parágrafo do fragmento de conteúdo no local atual.

   >[!CAUTION]
   Se, após adicionar um ativo, você alterar o formato para:
   * **Texto simples:** o ativo será completamente perdido do fragmento.
   * **Marcação**: o ativo não estará visível, mas ainda estará lá ao retornar para **Rich Text**.


### Inserir um fragmento de conteúdo no fragmento {#inserting-content-fragment-into-your-fragment}

Para facilitar o processo de criação de fragmentos de conteúdo, você também pode adicionar outro Fragmento de conteúdo ao fragmento.

Eles serão adicionados como referência, no local atual do fragmento.

>[!NOTE]
Esta opção está disponível quando seu **texto de várias linhas** está configurado com **Permitir referência de fragmento**.

>[!CAUTION]
Esses ativos não podem ser movidos ou excluídos em uma página de referência, isso deve ser feito no editor de fragmentos.
No entanto, a formatação do ativo (por exemplo, tamanho) deve ser feita no [editor de página](/help/sites-cloud/authoring/fundamentals/content-fragments.md). A representação do ativo no editor de fragmentos é apenas para a criação do fluxo de conteúdo.

>[!NOTE]
Existem vários métodos de adicionar [imagens](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) ao fragmento e/ou página.

1. Posicione o cursor na posição em que deseja adicionar o fragmento.
1. Use o ícone **Inserir fragmento de conteúdo** para abrir a caixa de diálogo de pesquisa.

   ![ícone Inserir fragmento do conteúdo](assets/cfm-variations-13.png)

1. Na caixa de diálogo, é possível:

   * navegue até o fragmento necessário na pasta Ativos
   * pesquisar o fragmento

   Depois de localizado, selecione o fragmento desejado clicando na miniatura.

1. Use **Selecione** para adicionar uma referência ao Fragmento de conteúdo selecionado ao fragmento de conteúdo atual (no local atual).

   >[!CAUTION]
   Se, após adicionar uma referência a outro fragmento, você alterar o formato para:
   * **Texto** sem formatação: a referência será completamente perdida do fragmento.
   * **Marcação**: a referência continuará.


## Gerenciando variações {#managing-variations}

### Criando uma Variação {#creating-a-variation}

As variações permitem que você pegue o conteúdo **Principal** e varie-o de acordo com a finalidade (se necessário).

Para criar uma nova variação:

1. Abra o fragmento e verifique se o painel lateral está visível.
1. Selecione **Variações** na barra de ícones no painel lateral.
1. Selecione **Criar variação**.
1. Uma caixa de diálogo será aberta, especifique o **Título** e a **Descrição** da nova variação.
1. Selecione **Adicionar**; o fragmento **Mestre** será copiado para a nova variação, que agora está aberta para [edição](#editing-a-variation).

   >[!NOTE]
   Ao criar uma nova variação, é sempre **Principal** que é copiada, não a variação que está aberta no momento.

### Editando uma Variação {#editing-a-variation}

É possível fazer alterações no conteúdo de variação após:

* [Criando sua variação](#creating-a-variation).
* Abrindo um fragmento existente e selecionando a variação necessária no painel lateral.

![edição de uma variação](assets/cfm-variations-10.png)

### Renomeação de uma Variação {#renaming-a-variation}

Para renomear uma variação existente:

1. Abra o fragmento e selecione **Variações** no painel lateral.
1. Selecione a variação necessária.
1. Selecione **Renomear** no menu suspenso **Ações**.

1. Digite o novo **Título** e/ou **Descrição** na caixa de diálogo resultante.

1. Confirme a ação **Renomear**.

>[!NOTE]
Isso só afeta a variação **Title**.

### Excluindo uma Variação {#deleting-a-variation}

Para excluir uma variação existente:

1. Abra o fragmento e selecione **Variações** no painel lateral.
1. Selecione a variação necessária.
1. Selecione **Excluir** no menu suspenso **Ações**.

1. Confirme a ação **Delete** na caixa de diálogo.

>[!NOTE]
Não é possível excluir **Principal**.

### Sincronização com {#synchronizing-with-master} Principal

**O** Masteris é parte integrante de um fragmento de conteúdo e, por definição, contém a cópia principal do conteúdo, enquanto as variações contêm as versões individuais atualizadas e personalizadas desse conteúdo. Quando for Principal, é possível que estas alterações sejam igualmente relevantes para as variações e, por conseguinte, tenham de ser propagadas para elas.

Ao editar uma variação, você tem acesso à ação para sincronizar o elemento atual da variação com o Principal. Isso permite que você copie automaticamente as alterações feitas no Principal para a variação necessária.

>[!CAUTION]
A sincronização só está disponível para copiar alterações *do **Master**para a variação*.
Somente o elemento atual da variação será sincronizado.
A sincronização só funciona no tipo de dados **Texto de várias linhas**.
A transferência de alterações *de uma variação para **Mestre*** não está disponível como uma opção.

1. Abra o fragmento do conteúdo no editor de fragmentos. Verifique se **Principal** foi editado.

1. Selecione uma variação específica e, em seguida, a ação de sincronização apropriada de:

   * o seletor suspenso **Ações** - **Sincronizar elemento atual com principal**

      ![sincronização com principal](assets/cfm-variations-11a.png)

   * a barra de ferramentas do editor de tela cheia - **Sincronizar com principal**

      ![sincronização com principal](assets/cfm-variations-11b.png)

1. Principal e a variação será mostrada lado a lado:

   * verde indica o conteúdo adicionado (à variação)
   * vermelho indica o conteúdo removido (da variação)
   * azul indica texto substituído

   ![sincronização com principal](assets/cfm-variations-11c.png)

1. Selecione **Sincronizar**, a variação será atualizada e mostrada.
