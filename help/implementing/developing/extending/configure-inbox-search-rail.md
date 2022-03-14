---
title: Como configurar filtros de pesquisa para a Caixa de entrada?
description: Saiba como configurar filtros de pesquisa para itens da Caixa de entrada.
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 1%

---

# Configurar filtros de pesquisa para a Caixa de entrada {#configure-search-filters-inbox}

Você pode configurar filtros de pesquisa para itens da Caixa de entrada. Baseie seus critérios de pesquisa em uma coluna Caixa de entrada específica para filtrar os resultados.

Por exemplo, para filtrar os itens da Caixa de entrada com base em um intervalo de colunas da Caixa de entrada de data de nascimento, você pode usar o predicado Intervalo de datas para definir o intervalo de datas.

A seguir estão os tipos de predicado disponíveis para Caixa de entrada:

* Predicado do intervalo

* Predicado de texto

* Predicado do intervalo de datas

* Predicado da propriedade de opções

>[!NOTE]
>
>Certifique-se de que você é um membro do `workflow-administrators` para configurar filtros de pesquisa para Caixa de entrada.

## Criar ou abrir uma configuração personalizada {#creating-opening-customized-configuration}

1. Navegar para **[!UICONTROL Ferramentas]**, **[!UICONTROL Geral]**, **[!UICONTROL Pesquisar Forms]**.

1. Selecione o **[!UICONTROL Painel de pesquisa da caixa de entrada]** configuração e toque em **[!UICONTROL Editar]**.
1. Incorpore as alterações na configuração do predicado usando **[!UICONTROL Editar Forms de Pesquisa]**.
1. Selecionar **[!UICONTROL Concluído]** para salvar a configuração.

## Excluir uma configuração personalizada {#delete-customized-configuration}

Para excluir uma configuração personalizada:

1. Navegar para **[!UICONTROL Ferramentas]**, **[!UICONTROL Geral]**, **[!UICONTROL Pesquisar Forms]**.

1. Selecione o **[!UICONTROL Painel de pesquisa da caixa de entrada]** configuração e toque em **[!UICONTROL Excluir]**.

## Configurar predicado de intervalo {#range-predicate}

Você pode filtrar itens da Caixa de entrada para procurar um intervalo de números em uma coluna da Caixa de entrada usando o Predicado de intervalo. Também é possível optar por incluir valores decimais para números.

Para configurar um Predicado de intervalo:

1. Abra o [formulário para configuração](#creating-opening-customized-configuration).
1. Toque no **[!UICONTROL Selecionar predicado]** tabulação e arrastar **[!UICONTROL Predicado de intervalo]** ao formulário.
1. No **[!UICONTROL Configurações]** selecione o nome da coluna Caixa de entrada para basear sua pesquisa, de **[!UICONTROL Nome da coluna]** campo.
1. Especifique o rótulo para o filtro no **[!UICONTROL Rótulo do filtro]** campo. Selecione o **[!UICONTROL Ativar valores decimais]** caixa de seleção para aceitar valores decimais para números ao definir o intervalo.
1. Especifique uma descrição opcional para a configuração e toque em **[!UICONTROL Concluído]** para salvá-lo.

As alterações de configuração são refletidas ao abrir a página Filtros . O rótulo do filtro especificado na etapa 4 é exibido como o rótulo com uma opção para definir os valores máximo e mínimo. Quando premir a tecla Enter, [!DNL Experience Manager] aplica os critérios de pesquisa no nome da coluna especificado na etapa 3 e retorna os itens da Caixa de entrada.

>[!NOTE]
>
>O artigo lista as opções mais recentes da interface do usuário. Os nomes das opções serão atualizados na interface do usuário na próxima versão.

## Configurar predicado de texto {#text-predicate}

Filtrar itens da Caixa de entrada para procurar uma sequência de texto em uma coluna da Caixa de entrada usando o Predicado de texto.

Para configurar um predicado de texto:

1. Abra o [formulário para configuração](#creating-opening-customized-configuration).
1. Toque no **[!UICONTROL Selecionar predicado]** tabulação e arrastar **[!UICONTROL Predicado de texto]** ao formulário.
1. No **[!UICONTROL Configurações]** selecione o nome da coluna Caixa de entrada para basear sua pesquisa, de **[!UICONTROL Nome da coluna]** campo.
1. Especifique o texto que é exibido na caixa de texto Pesquisar como um texto de espaço reservado na **[!UICONTROL Espaço reservado da caixa de texto de pesquisa]** campo.
1. Especifique uma descrição opcional para a configuração e toque em **[!UICONTROL Concluído]** para salvá-lo.

As alterações de configuração são refletidas ao abrir a página Filtros . Quando premir a tecla Enter, [!DNL Experience Manager] aplica o texto de pesquisa especificado na etapa 4 no nome da coluna especificado na etapa 3 e retorna os itens da Caixa de entrada.

## Configurar o predicado de intervalo de datas {#date-range-predicate}

Você pode filtrar itens da Caixa de entrada para procurar um intervalo de datas em uma coluna da Caixa de entrada usando o Predicado de intervalo de datas.

Para configurar um Predicado de intervalo de datas:

1. Abra o [formulário para configuração](#creating-opening-customized-configuration).
1. Toque no **[!UICONTROL Selecionar predicado]** tabulação e arrastar **[!UICONTROL Predicado de intervalo de datas]** ao formulário.
1. No **[!UICONTROL Configurações]** selecione o nome da coluna Caixa de entrada para basear sua pesquisa, de **[!UICONTROL Nome da coluna]** campo.
1. Especifique o rótulo para o filtro de intervalo de datas no **[!UICONTROL Rótulo do filtro]** campo.
1. Especifique a data inicial e os rótulos de data final para o filtro.
1. Especifique uma descrição opcional para a configuração e toque em **[!UICONTROL Concluído]** para salvá-lo.

As alterações de configuração são refletidas ao abrir a página Filtros . O rótulo do filtro especificado na etapa 4 é exibido como o rótulo para o filtro de intervalo de datas junto com os rótulos de data inicial e de data final especificados na etapa 5. [!DNL Experience Manager] aplica os critérios de pesquisa no nome da coluna especificado na etapa 3 e retorna os itens da Caixa de entrada.

## Configurar o predicado de opções de coluna personalizada {#custom-column-options-predicate}

Você pode filtrar itens da Caixa de entrada para procurar uma opção personalizada em uma coluna da Caixa de entrada usando o Predicado de opções de coluna personalizadas.

Para configurar um Predicado de opções de coluna personalizada:

1. Abra o [formulário para configuração](#creating-opening-customized-configuration).
1. Toque no **[!UICONTROL Selecionar predicado]** tabulação e arrastar **[!UICONTROL Predicado de opções de coluna personalizada]** ao formulário.
1. No **[!UICONTROL Configurações]** selecione o nome da coluna Caixa de entrada para basear sua pesquisa, de **[!UICONTROL Nome da coluna]** campo.
1. Especifique o rótulo para o filtro de opções de coluna personalizada no **[!UICONTROL Rótulo do filtro]** campo.
1. Selecione o **[!UICONTROL Seleção única]** caixa de seleção para ativar a seleção de apenas uma opção ao aplicar filtro em uma coluna Caixa de entrada.
1. No **[!UICONTROL Adicionar opções]** seção:
   1. Selecionar **[!UICONTROL Manual]** para definir as opções de pesquisa de filtro manualmente. Toque **[!UICONTROL Adicionar opções de filtro]** para definir a primeira opção. Especifique o rótulo para a opção de coluna e o texto do valor da opção a ser procurado. Por exemplo, se você deseja pesquisar por **Feminino** como um valor em uma coluna Caixa de entrada, você pode especificar **F** como rótulo para a opção de coluna e adicione **Feminino** como o texto do valor da opção. Da mesma forma, é possível adicionar mais opções de filtro.
   1. Selecionar **[!UICONTROL Caminho JSON]** para definir opções usando um caminho de arquivo JSON. A seguir, há uma amostra de arquivo JSON para definir opções de filtro:

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

   1. Selecionar **[!UICONTROL Caminho de opções do CRX]** para definir opções usando os caminhos do repositório CRX. Toque **[!UICONTROL Adicionar caminhos de opções]** para adicionar vários caminhos. Esta é uma amostra para definir `Male` e `Female` opções de filtro:

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

1. Especifique uma descrição opcional para a configuração e toque em **[!UICONTROL Concluído]** para salvá-lo.

As alterações de configuração são refletidas ao abrir a página Filtros . O rótulo do filtro especificado na etapa 4 é exibido como o rótulo para o Predicado de opção de coluna personalizada. [!DNL Experience Manager] aplica os critérios de pesquisa definidos na etapa 6 no nome da coluna especificado na etapa 3 e retorna os itens da Caixa de entrada.

O vídeo a seguir ilustra as etapas para filtrar uma coluna com base no `true` e `false` valores de opção.

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## Exibir filtros de pesquisa com base em predicados {#view-search-filters-for-predicates}

Você pode exibir filtros de pesquisa com base em predicados. Selecionar **[!UICONTROL Filtro]** na página Caixa de entrada. Os filtros são exibidos no painel esquerdo. Em seguida, você pode especificar os critérios de pesquisa para filtrar os itens da Caixa de entrada.

![Página Filtros](assets/apply-filters.png)

Para obter mais informações sobre o gerenciamento de configurações de predicado, consulte [Configuração do Search Forms](search-forms.md).
