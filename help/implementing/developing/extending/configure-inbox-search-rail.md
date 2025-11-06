---
title: Como configurar filtros de pesquisa para a Caixa de entrada?
description: Saiba como configurar filtros de pesquisa para itens da Caixa de entrada.
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 1%

---

# Configurar filtros de pesquisa para a Caixa de entrada {#configure-search-filters-inbox}

Você pode configurar filtros de pesquisa para itens da Caixa de entrada. Baseie seus critérios de pesquisa em uma coluna específica da Caixa de entrada para filtrar os resultados.

Por exemplo, para filtrar os itens da Caixa de entrada com base em um intervalo de colunas da Caixa de entrada de data de nascimento, você pode usar o predicado de Intervalo de datas para definir o intervalo de datas.

A seguir estão os tipos de predicado disponíveis para a Caixa de entrada:

* Predicado do intervalo

* Predicado de texto

* Predicado do intervalo de datas

* Predicado da propriedade de opções

>[!NOTE]
>
>Certifique-se de que você é membro do grupo `workflow-administrators` para configurar filtros de pesquisa para a Caixa de Entrada.

## Criar ou abrir uma configuração personalizada {#creating-opening-customized-configuration}

1. Navegue até **[!UICONTROL Ferramentas]**, **[!UICONTROL Geral]**, **[!UICONTROL Pesquisar Forms]**.

1. Selecione a configuração do **[!UICONTROL Painel de Pesquisa da Caixa de Entrada]** e selecione **[!UICONTROL Editar]**.
1. Incorpore as alterações de configuração do predicado usando **[!UICONTROL Editar Forms de Pesquisa]**.
1. Selecione **[!UICONTROL Concluído]** para salvar a configuração.

## Excluir uma configuração personalizada {#delete-customized-configuration}

Para excluir uma configuração personalizada:

1. Navegue até **[!UICONTROL Ferramentas]**, **[!UICONTROL Geral]**, **[!UICONTROL Pesquisar Forms]**.

1. Selecione a configuração do **[!UICONTROL Painel de Pesquisa da Caixa de Entrada]** e selecione **[!UICONTROL Excluir]**.

## Configurar predicado de intervalo {#range-predicate}

Você pode filtrar itens da Caixa de entrada para procurar um intervalo numérico em uma coluna da Caixa de entrada usando o Predicado do intervalo. Também é possível optar por incluir valores decimais para números.

Para configurar um predicado de intervalo:

1. Abra o formulário [para configuração](#creating-opening-customized-configuration).
1. Selecione a guia **[!UICONTROL Selecionar predicado]** e arraste o **[!UICONTROL Predicado do intervalo]** para o formulário.
1. Na guia **[!UICONTROL Configurações]**, selecione o nome de coluna da Caixa de Entrada na qual basear sua pesquisa, no campo **[!UICONTROL Nome da Coluna]**.
1. Especifique o rótulo para o filtro no campo **[!UICONTROL Rótulo do Filtro]**. Marque a caixa de seleção **[!UICONTROL Habilitar Valores Decimais]** para aceitar valores decimais para números ao definir o intervalo.
1. Especifique uma descrição opcional para a configuração e selecione **[!UICONTROL Concluído]** para salvá-la.

As alterações de configuração são refletidas ao abrir a página Filtros. O rótulo do filtro especificado na etapa 4 é exibido como o rótulo com uma opção para definir os valores máximo e mínimo. Quando você pressiona a tecla Enter, [!DNL Experience Manager] aplica os critérios de pesquisa no nome da coluna especificado na etapa 3 e retorna os itens da Caixa de Entrada.

>[!NOTE]
>
>O artigo lista as opções mais recentes da interface do usuário. Os nomes das opções são atualizados na interface do usuário na versão futura.

## Configurar predicado de texto {#text-predicate}

Filtre itens da Caixa de entrada para procurar uma sequência de texto em uma coluna da Caixa de entrada usando o Predicado de texto.

Para configurar um predicado de texto:

1. Abra o formulário [para configuração](#creating-opening-customized-configuration).
1. Selecione a guia **[!UICONTROL Selecionar predicado]** e arraste o **[!UICONTROL Predicado de texto]** para o formulário.
1. Na guia **[!UICONTROL Configurações]**, selecione o nome de coluna da Caixa de Entrada na qual basear sua pesquisa, no campo **[!UICONTROL Nome da Coluna]**.
1. Especifique o texto que é exibido na caixa de texto Pesquisar como um texto de espaço reservado no campo **[!UICONTROL Espaço Reservado para Caixa de Texto Pesquisar]**.
1. Especifique uma descrição opcional para a configuração e selecione **[!UICONTROL Concluído]** para salvá-la.

As alterações de configuração são refletidas ao abrir a página Filtros. Quando você pressiona a tecla Enter, [!DNL Experience Manager] aplica o texto de pesquisa especificado na etapa 4 no nome da coluna especificado na etapa 3 e retorna os itens da Caixa de Entrada.

## Configurar predicado do intervalo de datas {#date-range-predicate}

Você pode filtrar itens da Caixa de entrada para procurar um intervalo de datas em uma coluna da Caixa de entrada usando o Predicado do intervalo de datas.

Para configurar um Predicado de intervalo de datas:

1. Abra o formulário [para configuração](#creating-opening-customized-configuration).
1. Selecione a guia **[!UICONTROL Selecionar predicado]** e arraste o **[!UICONTROL Predicado do intervalo de datas]** para o formulário.
1. Na guia **[!UICONTROL Configurações]**, selecione o nome de coluna da Caixa de Entrada na qual basear sua pesquisa, no campo **[!UICONTROL Nome da Coluna]**.
1. Especifique o rótulo para o filtro de intervalo de datas no campo **[!UICONTROL Rótulo do Filtro]**.
1. Especifique os rótulos da data inicial e da data final para o filtro.
1. Especifique uma descrição opcional para a configuração e selecione **[!UICONTROL Concluído]** para salvá-la.

As alterações de configuração são refletidas ao abrir a página Filtros. O rótulo do filtro especificado na etapa 4 é exibido como o rótulo do filtro de intervalo de datas, juntamente com os rótulos de data inicial e data final especificados na etapa 5. [!DNL Experience Manager] aplica os critérios de pesquisa ao nome da coluna especificado na etapa 3 e retorna os itens da Caixa de Entrada.

## Configurar o predicado de opções de coluna personalizada {#custom-column-options-predicate}

Você pode filtrar itens da Caixa de entrada para procurar uma opção personalizada em uma coluna da Caixa de entrada usando o Predicado de opções de coluna personalizada.

Para configurar um Predicado de opções de coluna personalizada:

1. Abra o formulário [para configuração](#creating-opening-customized-configuration).
1. Selecione a guia **[!UICONTROL Selecionar predicado]** e arraste o **[!UICONTROL Predicado de opções de coluna personalizada]** para o formulário.
1. Na guia **[!UICONTROL Configurações]**, selecione o nome de coluna da Caixa de Entrada na qual basear sua pesquisa, no campo **[!UICONTROL Nome da Coluna]**.
1. Especifique o rótulo para o filtro de opções de coluna personalizada no campo **[!UICONTROL Rótulo do Filtro]**.
1. Marque a caixa de seleção **[!UICONTROL Seleção única]** para habilitar a seleção de apenas uma opção ao aplicar o filtro em uma coluna da Caixa de Entrada.
1. Na seção **[!UICONTROL Adicionar opções]**:
   1. Selecione **[!UICONTROL Manual]** para definir as opções de pesquisa de filtro manualmente. Selecione **[!UICONTROL Adicionar opções de filtro]** para definir a primeira opção. Especifique o rótulo para a opção de coluna e o texto do valor da opção a ser pesquisado. Por exemplo, se você deseja procurar por **Feminino** como um valor em uma coluna da Caixa de Entrada, você pode especificar **F** como rótulo para a opção de coluna e adicionar **Feminino** como o texto de valor da opção. Da mesma forma, é possível adicionar mais opções de filtro.
   1. Selecione **[!UICONTROL Caminho JSON]** para definir opções usando um caminho de arquivo JSON. Este é um exemplo de arquivo JSON para definir opções de filtro:

      ```JSON
          {
         "options":[
            {
            "text":"Female",
            "value":"F"
            },
            {
            "text":"Male",
            "value":"M"
            }
          ]
        }
      ```

   1. Selecione **[!UICONTROL Caminho de Opções do CRX]** para definir opções usando os caminhos de repositório do CRX. Selecione **[!UICONTROL Adicionar Caminhos de Opção]** para adicionar vários caminhos. Este é um exemplo para definir as opções de filtro `Male` e `Female`:

      ```JSON
         <gender jcr:primaryType="sling:OrderedFolder">
                        <male
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Male"
                            value="M"/>
                        <female
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Female"
                            value="F"/>
                    </gender>
      ```

1. Especifique uma descrição opcional para a configuração e selecione **[!UICONTROL Concluído]** para salvá-la.

As alterações de configuração são refletidas ao abrir a página Filtros. O rótulo do filtro especificado na etapa 4 é exibido como o rótulo do Predicado de opção de coluna personalizada. [!DNL Experience Manager] aplica os critérios de pesquisa definidos na etapa 6 no nome da coluna especificado na etapa 3 e retorna os itens da Caixa de Entrada.

O vídeo a seguir ilustra as etapas para filtrar uma coluna com base nos valores de opção `true` e `false`.

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## Exibir filtros de pesquisa com base em predicados {#view-search-filters-for-predicates}

Você pode exibir filtros de pesquisa com base em predicados. Selecione **[!UICONTROL Filtro]** na página Caixa de Entrada. Os filtros são exibidos no painel esquerdo. Em seguida, você pode especificar os critérios de pesquisa para filtrar itens da Caixa de entrada.

![Página de filtros](assets/apply-filters.png)

Para obter mais informações sobre como gerenciar configurações de predicado, consulte [Configurando Forms de Pesquisa](search-forms.md).
