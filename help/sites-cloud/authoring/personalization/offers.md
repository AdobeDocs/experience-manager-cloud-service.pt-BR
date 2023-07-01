---
title: Criação e gerenciamento de ofertas (console Ofertas)
description: Use o console Ofertas para criar ofertas que você possa usar em experiências de atividades
exl-id: 81d2fda2-06a9-48f6-820a-dd9e11d94fcc
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 47%

---

# Criação e gerenciamento de ofertas (console Ofertas) {#creating-and-managing-offers}

O console de **Ofertas** será descontinuado no futuro. Então, a partir de agora, é:

* Disponível somente para clientes que têm ofertas *herdadas* já definidas (ou seja, pré-existentes)
* Recomendado que qualquer oferta herdada seja convertida em ofertas de fragmento de experiência
   * Assim que a última oferta herdada for convertida/removida, o console de **Ofertas** não estará mais disponível.

![Consoles de personalização](/help/sites-cloud/authoring/assets/offers-consoles.png)

>[!NOTE]
>
>Os clientes que têm ofertas herdadas pré-existentes ainda podem usar o console de **Ofertas** para ver as ofertas existentes e criar novas ofertas herdadas.
>
>Os clientes sem ofertas herdadas pré-existentes não verão o console de **Ofertas**.
>
>Todos os clientes podem usar as **Ofertas de fragmentos de experiência** para criar e gerenciar ofertas.

## Conversão de uma oferta herdada em um fragmento de experiência {#convert-legacy-offer-to-experience-fragment}

A opção **Converter em variação de fragmento de experiência** e o fluxo de trabalho foram implementados para ajudá-lo a converter sua oferta herdada em um Fragmento de experiência:

>[!NOTE]
>
>Este é o fluxo de trabalho recomendado para converter ofertas herdadas em fragmentos de experiência.

>[!NOTE]
>
>Você mesmo também pode criar um novo Fragmento de experiência, transferir manualmente o conteúdo da oferta herdada para o fragmento e, em seguida, excluir a oferta herdada.

>[!CAUTION]
>
>A opção **Converter em variação de fragmento de experiência** está disponível para todos os Componentes principais.
>
>Esta opção não será compatível com componentes personalizados. Para esses componentes, você deve converter manualmente o conteúdo em um fragmento de experiência.

>[!CAUTION]
>
>Assim que a última oferta herdada for convertida/removida:
>
>* O console de **Ofertas** não estará mais disponível.
>* O ícone de direcionamento na barra de ferramentas de qualquer outro componente afetado não será mais exibido.

1. Abra uma página que contenha a oferta para edição.

1. Mudar para o modo **Direcionamento** para essa página.

1. Selecione **Iniciar o direcionamento**.

1. Selecione o componente (direcionado) apropriado.

1. A barra de ferramentas do componente fornecerá uma opção para **Converter em variação de fragmento de experiência**:

   ![Conversão da oferta herdada em Fragmento de experiência](/help/sites-cloud/authoring/assets/offers-convert-legacy-icon.png)

1. Uma caixa de diálogo é exibida. Aqui você pode selecionar a **Ação**:

   * Criar novo Fragmento de experiência
   * Adicionar conteúdo a um fragmento de experiência existente

   Para este cenário, selecione **Criar um novo Fragmento de experiência**.

   ![Converter para diálogo da variação do Fragmento da experiência](/help/sites-cloud/authoring/assets/offers-convert-dialog.png)

1. Preencha os campos obrigatórios na caixa de diálogo:

   * **Caminho principal**
Especificar o caminho principal do novo fragmento de experiência
   * **Modelo**
Selecione o modelo a ser usado para criar o fragmento de experiência.
   * **Título do fragmento**
Especifique o título.
   * **Tags de fragmento**
Adicione tags, se necessário.

1. Confirme com **Concluído**.

   Agora, ao navegar até o console **Ofertas de Fragmento de experiência**, você verá seu novo fragmento de experiência, juntamente com suas variações associadas.

### Direcionamento com o modelo de ofertas {#targeting-offers-template}

>[!CAUTION]
>
>Esta opção só está disponível para clientes com ofertas herdadas pré-existentes.
>
>Como no console de **Ofertas**, também não estará mais disponível:
>
>* depois que a última oferta herdada for convertida em Fragmentos de experiência
>* quando as ofertas herdadas estiverem obsoletas (no futuro)
>
>Portanto, a opção recomendada é usar Fragmentos de experiência, não esta opção.

Para clientes com ofertas herdadas pré-existentes, a variável **Usar modelo de oferta** opções estão visíveis ao direcionar componentes que são **não** Fragmentos de experiência:

![Converter em diálogo de variação de Fragmento de experiência](/help/sites-cloud/authoring/assets/offers-legacy-target-non-experience-fragment.png)

## O console de Ofertas {#offers-console}

>[!CAUTION]
>
>Este console será descontinuado no futuro, pois oferece uma maneira herdada de personalizar o conteúdo.
>
>Você tem tempo para se preparar. Veja como [converter as ofertas legadas existentes em uma oferta de fragmento de experiência](#convert-legacy-offer-to-experience-fragment).

Use o console Ofertas para criar ofertas que você possa [uso em experiências de atividade](/help/sites-cloud/authoring/personalization/targeted-content.md). A criação de ofertas no console Ofertas economiza tempo quando várias experiências exigem a mesma oferta:

* Crie a oferta uma única vez na biblioteca e use-a em várias experiências das suas atividades de marca.
* Altere a oferta na biblioteca e a alteração afetará todas as experiências que a utilizam.

O console de Ofertas organiza as ofertas por marca. Cada marca contém uma biblioteca de ofertas que podem ser usadas nas experiências de uma marca. Use pastas para definir uma estrutura hierárquica para organizar ofertas em cada biblioteca. Uma estrutura de pastas lógica permite que os autores encontrem ofertas facilmente navegando. As ferramentas de marcação e pesquisa também permitem que os autores encontrem ofertas.

### Adicionar uma marca usando o console Ofertas {#add-a-brand-using-the-offers-console}

Crie uma marca à qual suas ofertas estão associadas. Abra uma marca no console Ofertas para acessar sua biblioteca de ofertas, onde você pode criar pastas e ofertas.

Ao criar uma marca usando o console Ofertas, ela também aparece no [Console de atividades](/help/sites-cloud/authoring/personalization/activities.md) onde é possível adicionar e administrar atividades da marca.

1. No console Navegação, clique ou toque em **Personalização** > **Ofertas**.

   ![Navegação até o console Ofertas](/help/sites-cloud/authoring/assets/offers-navigation.png)

1. Clique ou toque em **Criar** e depois em **Criar** **marca**.
1. Selecione o modelo da marca e clique ou toque em **Próxima**.
1. Digite um título para a marca conforme você quer que ele seja exibido nos consoles Ofertas e Atividades. Opcionalmente, digite ou selecione uma ou mais tags para associar à marca.
1. Clique ou toque em **Criar**.

### Adicionar uma pasta a uma biblioteca de ofertas {#add-a-folder-to-an-offer-library}

Adicione uma pasta à biblioteca de ofertas de uma marca para organizar e armazenar ofertas. Você pode criar uma pasta abaixo da marca ou abaixo de outras pastas.

1. No console Ofertas, abra o local em que deseja criar a pasta. Por exemplo, abra a marca para criar uma pasta de nível superior ou abra outra pasta na biblioteca.
1. Clique ou toque **Criar** > **Criar pasta ou oferta**.

   ![Criação da pasta de ofertas](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Selecione **Pasta** e clique em **Avançar**.
1. Digite o título que você atribuir para a exibição da pasta na biblioteca de ofertas e digite ou selecione tags.

   ![Definição das propriedades da pasta](/help/sites-cloud/authoring/assets/offers-folder-properties.png)

1. Clique ou toque em **Criar**.

### Adicionar uma oferta a uma biblioteca de ofertas {#add-an-offer-to-an-offer-library}

Adicione uma oferta à biblioteca de ofertas de uma marca para que ela possa ser adicionada às experiências da marca. Ao adicionar uma oferta, você fornece um título. Você também pode associar a oferta a uma ou mais tags para aprimorar a pesquisa.

Depois de criar a oferta, você pode abri-la para criar o conteúdo.

1. No console Ofertas, abra o local em que deseja criar a oferta. Por exemplo, abra a marca para criar uma oferta de nível superior ou abra uma pasta na biblioteca.
1. Clique ou toque **Criar** > **Criar pasta ou oferta**.

   ![Criação da pasta de ofertas](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Selecione o **Página de oferta** e clique ou toque em **Próxima**.
1. Digite um título para a oferta e, opcionalmente, selecione ou digite uma ou mais tags para associar à oferta e clique ou toque em **Criar**.
1. Na caixa de diálogo de confirmação, para abrir a oferta para edição, clique ou toque em **Abrir página**.

### Edição de uma oferta {#editing-an-offer}

Abra uma oferta e edite o conteúdo conforme deseja que ele seja exibido nas experiências que a utilizam. Ao editar uma oferta usada em qualquer experiência, suas alterações aparecem nas experiências.

É possível abrir uma oferta de uma pasta em uma biblioteca de ofertas ou dos resultados da pesquisa. Você também pode abrir uma oferta de uma experiência que usa a oferta.

1. No console Ofertas, toque ou clique no ícone ao lado da oferta e clique ou toque **Editar**.
1. Adicione componentes à oferta e edite o conteúdo do componente como de costume.

### Exclusão de uma oferta {#deleting-an-offer}

Exclua uma oferta quando ela não for mais necessária. Ao tentar excluir uma oferta usada em uma experiência do, você será solicitado a confirmar a exclusão. A confirmação exclui a oferta e a remove das experiências.

É possível excluir uma oferta ao visualizar o conteúdo da pasta em uma biblioteca de ofertas ou em resultados de pesquisa.

1. No console Ofertas, toque ou clique no ícone ao lado da oferta e clique ou toque **Excluir**.

   Selecione a oferta e clique ou toque em **Excluir**.

1. Na caixa de diálogo exibida, clique ou toque em **Excluir** para confirmar a exclusão.
1. Se a oferta for usada em uma ou mais experiências, uma caixa de diálogo será exibida para indicar que a oferta é referenciada:

   * Para excluir a oferta e removê-la das experiências, clique ou toque **Forçar Exclusão**.
   * Para manter a oferta, clique ou toque em **Cancelar**.

### Procurando Ofertas {#searching-for-offers}

Procure ofertas de qualquer marca usando palavras-chave para corresponder ao título.

![Procurar por uma oferta](/help/sites-cloud/authoring/assets/offers-search.png)

Os critérios de pesquisa atuais aparecem ao lado dos resultados da pesquisa. Você também pode classificar os resultados por coluna em ordem crescente ou decrescente. É possível executar uma pesquisa em qualquer pasta de qualquer biblioteca de ofertas. Os resultados da pesquisa são os mesmos independentemente da pasta atual.

Para pesquisar ofertas:

1. Na parte superior do console Ofertas, clique ou toque no ícone de lupa. Por padrão, a pesquisa é limitada a ofertas.
1. Digite sua palavra-chave para procurar ofertas. Selecione nos resultados.
