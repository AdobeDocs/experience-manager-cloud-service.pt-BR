---
title: Criação e gerenciamento de ofertas
description: Use o console Ofertas para criar ofertas que você pode usar em experiências de atividades
exl-id: 81d2fda2-06a9-48f6-820a-dd9e11d94fcc
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 100%

---

# Criação e gerenciamento de ofertas {#creating-and-managing-offers}

Use o console Ofertas para criar ofertas que você pode [usar em experiências de atividades](/help/sites-cloud/authoring/personalization/targeted-content.md). A criação de ofertas no console Ofertas poupa tempo quando várias experiências exigem a mesma oferta:

* Crie a oferta uma única vez na biblioteca e use-a em várias experiências das suas atividades de marca.
* Se a oferta for alterada na biblioteca, a alteração afetará todas as experiências que utilizam essa oferta.

O console Ofertas organiza ofertas por marca. Cada marca contém uma biblioteca de ofertas que podem ser usadas nas experiências de uma marca. Use pastas para definir uma estrutura hierárquica para organizar ofertas em cada biblioteca. Uma estrutura de pastas lógica permite que os autores naveguem e encontrem ofertas facilmente. Ferramentas de marcação e pesquisa também permitem que os autores encontrem ofertas.

## Adicionar uma marca usando o console Ofertas {#add-a-brand-using-the-offers-console}

Crie uma marca à qual as suas ofertas estejam associadas. Abra uma marca no console Ofertas para acessar sua biblioteca de ofertas, onde você pode criar pastas e ofertas.

Quando você cria uma marca usando o console Ofertas, ela também aparece no [console Atividades](/help/sites-cloud/authoring/personalization/activities.md), onde é possível adicionar e administrar atividades da marca.

1. No console Navegação, clique ou toque em **Personalização** > **Ofertas**.

   ![Navegação até o console Ofertas](/help/sites-cloud/authoring/assets/offers-navigation.png)

1. Clique ou toque em **Criar** e depois em **Criar** **marca**.
1. Selecione o modelo da marca e clique ou toque em **Próximo**.
1. Digite o título que você deseja atribuir para a exibição da marca nos consoles Ofertas e Atividades. Opcionalmente, digite ou selecione uma ou mais tags para associar à marca.
1. Clique ou toque em **Criar**.

## Adicionar uma pasta a uma biblioteca de ofertas {#add-a-folder-to-an-offer-library}

Adicione uma pasta à biblioteca de ofertas de uma marca para organizar e armazenar ofertas. É possível criar uma pasta abaixo da marca ou abaixo de outras pastas.

1. No console Ofertas, abra a localização em que você deseja criar a pasta. Por exemplo, abra a marca para criar uma pasta de nível superior ou abra outra pasta na biblioteca.
1. Clique ou toque em **Criar** > **Criar pasta ou oferta**.

   ![Criação da pasta de ofertas](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Selecione **Pasta** e clique em **Avançar**.
1. Digite o título que você atribuir para a exibição da pasta na biblioteca de ofertas e digite ou selecione tags.

   ![Definição das propriedades da pasta](/help/sites-cloud/authoring/assets/offers-folder-properties.png)

1. Clique ou toque em **Criar**.

## Adicionar uma oferta a uma biblioteca de ofertas {#add-an-offer-to-an-offer-library}

Adicione uma oferta à biblioteca de ofertas de uma marca para que ela possa ser adicionada às experiências da marca. Ao adicionar uma oferta, você fornece um título para ela. Também é possível associar a oferta a uma ou mais tags para melhorar a capacidade de pesquisa.

Depois de criar a oferta, você pode abri-la para criar o conteúdo.

1. No console Ofertas, abra a localização em que você deseja criar a oferta. Por exemplo, abra a marca para criar uma oferta de nível superior ou abra uma pasta na biblioteca.
1. Clique ou toque em **Criar** > **Criar pasta ou oferta**.

   ![Criação da pasta de ofertas](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Selecione o modelo **Página de oferta** e clique ou toque em **Próximo**.
1. Digite um título para a oferta e, opcionalmente, selecione ou digite uma ou mais tags a serem associadas à oferta. Em seguida, clique ou toque em **Criar**.
1. Na caixa de diálogo de confirmação, para abrir a oferta para edição, clique ou toque em **Abrir página**.

## Edição de uma oferta {#editing-an-offer}

Abra uma oferta e edite o conteúdo como você deseja que ele apareça nas experiências que o utilizam. Quando você edita uma oferta que é usada em qualquer experiência, suas alterações aparecem nessas experiências.

É possível abrir uma oferta contida em uma pasta de uma biblioteca de ofertas ou a partir de resultados de pesquisas. Também é possível abrir uma oferta de uma experiência que a utiliza.

1. No console Ofertas, toque ou clique no ícone ao lado da oferta e depois clique ou toque em **Editar**.
1. Adicione componentes à oferta e edite o conteúdo dos componentes como de costume.

## Exclusão de uma oferta {#deleting-an-offer}

Exclua uma oferta quando ela não for mais necessária. Quando você tentar excluir uma oferta usada em uma experiência, será necessário confirmar a exclusão. A confirmação exclui a oferta e a remove das experiências.

Você pode excluir uma oferta enquanto visualiza o conteúdo de uma pasta em uma biblioteca de ofertas ou os resultados de pesquisas.

1. No console Ofertas, toque ou clique no ícone ao lado da oferta e depois clique ou toque em **Excluir**.

   Selecione a oferta e clique ou toque em **Excluir**.

1. Na caixa de diálogo exibida, clique ou toque em **Excluir** para confirmar a exclusão.
1. Se a oferta for usada em uma ou mais experiências, será exibida uma caixa de diálogo indicando que essa oferta é referenciada:

   * Para excluir a oferta e removê-la das experiências, clique ou toque em **Forçar exclusão**.
   * Para manter a oferta, clique ou toque em **Cancelar**.

## Procurar ofertas {#searching-for-offers}

Procure ofertas de qualquer marca usando palavras-chave para correspondência do título.

![Procurar por uma oferta](/help/sites-cloud/authoring/assets/offers-search.png)

Os critérios de pesquisa atuais aparecem ao lado dos resultados da pesquisa. Você também pode classificar os resultados por coluna em ordem crescente ou decrescente. É possível realizar uma pesquisa em qualquer pasta de qualquer biblioteca de ofertas. Os resultados da pesquisa serão os mesmos, independentemente da pasta atual.

Para pesquisar ofertas:

1. Na parte superior do console Ofertas, clique ou toque no ícone de lupa. Por padrão, a pesquisa é limitada a ofertas.
1. Insira sua palavra-chave para procurar ofertas. Selecione um dos resultados.
